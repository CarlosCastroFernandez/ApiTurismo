# ApiTurismo
Api Turismo Trabajo de Clase
# Recursos Utilizados
#### Hemos utilizado una base de datos en las que representamos una tabla de hotel una de restaurante una de cliente y una de propietario
#### siendo asi la estructura de nuestra base de datos en MySQL :

create table propietario(<br>
id int primary key auto_increment,<br>
nombre varchar(120),<br>
apellido varchar (120),<br>
correo varchar(120),<br>
contraseña varchar(120),<br>
token varchar (120)<br>
);<br>

CREATE TABLE hotel (<br>
    id INT PRIMARY KEY AUTO_INCREMENT,<br>
    nombre VARCHAR(255) NOT NULL,<br>
    direccion VARCHAR(255) NOT NULL,<br>
    estrellas INT,<br>
    descripcion TEXT,<br>
    precio_noche DOUBLE,<br>
    metros_cuadrados DOUBLE,<br>
    num_habitaciones INT,<br>
    anio_fundado int,<br>
	propietario_id int,<br>
	foreign key (propietario_id) references propietario (id)<br>
);<br>

CREATE TABLE restaurante (<br>
    id INT PRIMARY KEY AUTO_INCREMENT,<br>
    nombre VARCHAR(255) NOT NULL,<br>
    tipo VARCHAR(50),<br>
    direccion VARCHAR(255) NOT NULL,<br>
    descripcion TEXT,<br>
    valoracion DOUBLE,<br>
    anio_fundado int,<br>
    propietario_id int,<br>
    foreign key (propietario_id) references propietario (id)<br>
);<br>
create table cliente(<br>
id int primary key auto_increment,<br>
nombre varchar(120),<br>
apellido varchar (120),<br>
correo varchar(120),<br>
contraseña varchar(120),<br>
token varchar (120),<br>
hotel_id int,<br>
restaurante_id int,<br>
foreign key (hotel_id) references hotel (id),<br>
foreign key (restaurante_id) references restaurante (id)<br>
);<br>
#### Hay que tener en ceunta que estas tablas las hemos rellenado de datos ficticios en los que mas adelante veremos como obtenemos respuesta de estos recursos
# Endpoints
#### En nuestro controlador de hotel tenemos los siguientes endpoints:
  @GetMapping("")<br>
  @GetMapping("/{id}")<br>
  @GetMapping("/{idPropietario}")<br>
  @GetMapping("{año}")<br>
  @GetMapping("/{direccion}")<br>
  @PostMapping("/saveHotel")   <br>
  @PutMapping("/{id}")<br>
  @DeleteMapping("/{id}")<br>
#### En nuestro controlador de restaurante tenemos los siguientes endpoints:
  @GetMapping("")<br>
  @GetMapping("/{idPropietarioR}")<br>
  @GetMapping("/{id}")<br>
  @GetMapping("/{año}")<br>
  @GetMapping("/{direccion}")<br>
  @PostMapping("/saveRestaurante")<br>
  @PutMapping("/{id}")<br>
  @DeleteMapping("/{id}")<br>

  # Algunos ejemplos de Respuestas:
  ##### POST http://localhost:8080/restaurantes/saveRestaurante?token=tokenPropietario1

HTTP/1.1 200 <br>
Content-Type: application/json<br>
Transfer-Encoding: chunked<br>
Date: Sat, 10 Feb 2024 18:13:50 GMT<br>
Keep-Alive: timeout=60<br>
Connection: keep-alive<br>
<br>
{<br>
  "id": 22,<br>
  "nombre": "pendejada",<br>
  "tipo": null,<br>
  "direccion": "La Parla",<br>
  "descripcion": null,<br>
  "valoracion": null,<br>
  "anioFundado": null,<br>
  "propietarioRId": []<br>
  {<br>
  "id": 1<br>
  "nombre":Jon<br>
  "apellido":Doe<br>
  },<br>
  "clientes": null<br>
}<br>
Response file saved.<br>
> 2024-02-10T191350.200.json<br>

Response code: 200; Time: 39ms (39 ms); Content length: 159 bytes (159 B)<br>
##### DELETE http://localhost:8080/restaurantes/22?token=tokenPropietario1

HTTP/1.1 200 <br>
Content-Type: application/json<br>
Transfer-Encoding: chunked<br>
Date: Sat, 10 Feb 2024 18:32:01 GMT<br>
Keep-Alive: timeout=60<br>
Connection: keep-alive<br>
<br>
{<br>
  "id": 22,<br>
  "nombre": "Chuck Norris",<br>
  "tipo": null,<br>
  "direccion": "La Parla",<br>
  "descripcion": null,<br>
  "valoracion": null,<br>
  "anioFundado": null,<br>
  "propietarioRId": null,<br>
  "clientes": []<br>
}<br>
Response file saved.<br>
> 2024-02-10T193201.200.json<br>
<br>
Response code: 200; Time: 268ms (268 ms); Content length: 160 bytes (160 B)<br>

##### PUT http://localhost:8080/hoteles/18?token=tokenPropietario1

HTTP/1.1 200 <br>
Content-Type: application/json<br>
Transfer-Encoding: chunked<br>
Date: Sat, 10 Feb 2024 19:04:33 GMT<br>
Keep-Alive: timeout=60<br>
Connection: keep-alive<br>

{<br>
  "id": 18,<br>
  "nombre": "Periquito",<br>
  "direccion": "Calle la manuela Nogales 4",<br>
  "estrellas": null,<br>
  "descripcion": null,<br>
  "precioNoche": null,<br>
  "metrosCuadrados": null,<br>
  "numHabitaciones": null,<br>
  "anioFundado": null,<br>
  "propietarioId": {<br>
    "id": 2,<br>
    "nombre": "Alice",<br>
    "apellido": "Smith"<br>
  },<br>
  "clientes": []<br>
}<br>
Response file saved.<br>
> 2024-02-10T200433.200.json<br>

Response code: 200; Time: 304ms (304 ms); Content length: 266 bytes (266 B)<br>

##### GET http://localhost:8080/restaurantes/5?token=tokenMiguel

HTTP/1.1 200 <br>
Content-Type: application/json<br>
Transfer-Encoding: chunked<br>
Date: Sat, 10 Feb 2024 19:28:36 GMT<br>
Keep-Alive: timeout=60<br>
Connection: keep-alive<br>

{<br>
  "id": 5,<br>
  "nombre": "Comida Asiática Express",<br>
  "tipo": "Asiática",<br>
  "direccion": "222 Calle Oriental",<br>
  "descripcion": "Variedad de platos asiáticos para llevar o disfrutar en el lugar.",<br>
  "valoracion": 4.2,<br>
  "anioFundado": 2017,<br>
  "propietarioRId": {<br>
    "id": 1,<br>
    "nombre": "John",<br>
    "apellido": "Doe"<br>
  },<br>
  "clientes": []<br>
}<br>
Response file saved.<br>
> 2024-02-10T202836.200.json<br>

Response code: 200; Time: 244ms (244 ms); Content length: 285 bytes (285 B)<br>

##### GET http://localhost:8080/hoteles/2?token=tokenMiguel
HTTP/1.1 200 <br>
Content-Type: application/json<br>
Transfer-Encoding: chunked<br>
Date: Sat, 10 Feb 2024 19:30:14 GMT<br>
Keep-Alive: timeout=60<br>
Connection: keep-alive<br>

[<br>
  {<br>
    "id": 2,<br>
    "nombre": "Prueba Cambio",<br>
    "direccion": "456 Calle Secundaria",<br>
    "estrellas": 3,<br>
    "descripcion": "Un lugar acogedor para toda la familia",<br>
    "precioNoche": 120.0,<br>
    "metrosCuadrados": 800.0,<br>
    "numHabitaciones": 50,<br>
    "anioFundado": 2010,<br>
    "propietarioId": {<br>
      "id": 2,<br>
      "nombre": "Alice",<br>
      "apellido": "Smith"<br>
    },<br>
    "clientes": []<br>
  },<br>
  {<br>
    "id": 6,<br>
    "nombre": "Gran Hotel Montaña",<br>
    "direccion": "333 Calle de las Cumbres",<br>
    "estrellas": 4,<br>
    "descripcion": "Situado en las alturas con vistas panorámicas",<br>
    "precioNoche": 220.0,<br>
    "metrosCuadrados": 1600.0,<br>
    "numHabitaciones": 90,<br>
    "anioFundado": 2006,<br>
    "propietarioId": {<br>
      "id": 2,<br>
      "nombre": "Alice",<br>
      "apellido": "Smith"<br>
    },<br>
    "clientes": []<br>
  },<br>
  {<br>
    "id": 10,<br>
    "nombre": "Hotel de Montaña Escarpada",<br>
    "direccion": "777 Camino Escarpado",<br>
    "estrellas": 3,<br>
    "descripcion": "Aventuras en un entorno montañoso",<br>
    "precioNoche": 130.0,<br>
    "metrosCuadrados": 900.0,<br>
    "numHabitaciones": 40,<br>
    "anioFundado": 2019,<br>
    "propietarioId": {<br>
      "id": 2,<br>
      "nombre": "Alice",<br>
      "apellido": "Smith"<br>
    },<br>
    "clientes": []<br>
  },<br>
  {<br>
    "id": 14,<br>
    "nombre": "Estancia Elegante",<br>
    "direccion": "222 Elegancia Avenue",<br>
    "estrellas": 5,<br>
    "descripcion": "Donde el lujo se encuentra con la elegancia",<br>
    "precioNoche": 320.0,<br>
    "metrosCuadrados": 1800.0,<br>
    "numHabitaciones": 95,<br>
    "anioFundado": 2007,<br>
    "propietarioId": {<br>
      "id": 2,<br>
      "nombre": "Alice",<br>
      "apellido": "Smith"<br>
    },<br>
    "clientes": []<br>
  },<br>
  {<br>
    "id": 18,<br>
    "nombre": "Periquito",<br>
    "direccion": "Calle la manuela Nogales 4",<br>
    "estrellas": null,<br>
    "descripcion": null,<br>
    "precioNoche": null,<br>
    "metrosCuadrados": null,<br>
    "numHabitaciones": null,<br>
    "anioFundado": null,<br>
    "propietarioId": {<br>
      "id": 2,<br>
      "nombre": "Alice",<br>
      "apellido": "Smith"<br>
    },<br>
    "clientes": []<br>
  }<br>
]<br>
Response file saved.<br>
> 2024-02-10T203014.200.json<br>

Response code: 200; Time: 50ms (50 ms); Content length: 1493 bytes (1,49 kB)<br>
  
