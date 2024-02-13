# ApiTurismo
Api Turismo Trabajo de Clase
# Recursos Utilizados
#### Hemos utilizado una base de datos en las que representamos una tabla de hotel una de restaurante una de cliente y una de propietario
#### siendo asi la estructura de nuestra base de datos en MySQL :

create table propietario(
id int primary key auto_increment,
nombre varchar(120),
apellido varchar (120),
correo varchar(120),
contraseña varchar(120),
token varchar (120)
);

CREATE TABLE hotel (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(255) NOT NULL,
    direccion VARCHAR(255) NOT NULL,
    estrellas INT,
    descripcion TEXT,
    precio_noche DOUBLE,
    metros_cuadrados DOUBLE,
    num_habitaciones INT,
    anio_fundado int,
	propietario_id int,
	foreign key (propietario_id) references propietario (id)
);

CREATE TABLE restaurante (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(255) NOT NULL,
    tipo VARCHAR(50),
    direccion VARCHAR(255) NOT NULL,
    descripcion TEXT,
    valoracion DOUBLE,
    anio_fundado int,
    propietario_id int,
    foreign key (propietario_id) references propietario (id)
);
create table cliente(
id int primary key auto_increment,
nombre varchar(120),
apellido varchar (120),
correo varchar(120),
contraseña varchar(120),
token varchar (120),
hotel_id int,
restaurante_id int,
foreign key (hotel_id) references hotel (id),
foreign key (restaurante_id) references restaurante (id)
);
#### Hay que tener en ceunta que estas tablas las hemos rellenado de datos ficticios en los que mas adelante veremos como obtenemos respuesta de estos recursos
# Endpoints
#### En nuestro controlador de hotel tenemos los siguientes endpoints:
  @GetMapping("")
  @GetMapping("/{id}")
  @GetMapping("/{idPropietario}")
  @GetMapping("{año}")
  @GetMapping("/{direccion}")
  @PostMapping("/saveHotel")   
  @PutMapping("/{id}")
  @DeleteMapping("/{id}")
#### En nuestro controlador de restaurante tenemos los siguientes endpoints:
  @GetMapping("")
  @GetMapping("/{idPropietarioR}")
  @GetMapping("/{id}")
  @GetMapping("/{año}")
  @GetMapping("/{direccion}")
  @PostMapping("/saveRestaurante")
  @PutMapping("/{id}")
  @DeleteMapping("/{id}")

  # Algunos ejemplos de Respuestas:
  ##### POST http://localhost:8080/restaurantes/saveRestaurante?token=tokenPropietario1

HTTP/1.1 200 
Content-Type: application/json
Transfer-Encoding: chunked
Date: Sat, 10 Feb 2024 18:13:50 GMT
Keep-Alive: timeout=60
Connection: keep-alive

{
  "id": 22,
  "nombre": "pendejada",
  "tipo": null,
  "direccion": "La Parla",
  "descripcion": null,
  "valoracion": null,
  "anioFundado": null,
  "propietarioRId": []
  {
  "id": 1
  "nombre":Jon
  "apellido":Doe
  },
  "clientes": null
}
Response file saved.
> 2024-02-10T191350.200.json

Response code: 200; Time: 39ms (39 ms); Content length: 159 bytes (159 B)
##### DELETE http://localhost:8080/restaurantes/22?token=tokenPropietario1

HTTP/1.1 200 
Content-Type: application/json
Transfer-Encoding: chunked
Date: Sat, 10 Feb 2024 18:32:01 GMT
Keep-Alive: timeout=60
Connection: keep-alive

{
  "id": 22,
  "nombre": "Chuck Norris",
  "tipo": null,
  "direccion": "La Parla",
  "descripcion": null,
  "valoracion": null,
  "anioFundado": null,
  "propietarioRId": null,
  "clientes": []
}
Response file saved.
> 2024-02-10T193201.200.json

Response code: 200; Time: 268ms (268 ms); Content length: 160 bytes (160 B)

##### PUT http://localhost:8080/hoteles/18?token=tokenPropietario1

HTTP/1.1 200 
Content-Type: application/json
Transfer-Encoding: chunked
Date: Sat, 10 Feb 2024 19:04:33 GMT
Keep-Alive: timeout=60
Connection: keep-alive

{
  "id": 18,
  "nombre": "Periquito",
  "direccion": "Calle la manuela Nogales 4",
  "estrellas": null,
  "descripcion": null,
  "precioNoche": null,
  "metrosCuadrados": null,
  "numHabitaciones": null,
  "anioFundado": null,
  "propietarioId": {
    "id": 2,
    "nombre": "Alice",
    "apellido": "Smith"
  },
  "clientes": []
}
Response file saved.
> 2024-02-10T200433.200.json

Response code: 200; Time: 304ms (304 ms); Content length: 266 bytes (266 B)

##### GET http://localhost:8080/restaurantes/5?token=tokenMiguel

HTTP/1.1 200 
Content-Type: application/json
Transfer-Encoding: chunked
Date: Sat, 10 Feb 2024 19:28:36 GMT
Keep-Alive: timeout=60
Connection: keep-alive

{
  "id": 5,
  "nombre": "Comida Asiática Express",
  "tipo": "Asiática",
  "direccion": "222 Calle Oriental",
  "descripcion": "Variedad de platos asiáticos para llevar o disfrutar en el lugar.",
  "valoracion": 4.2,
  "anioFundado": 2017,
  "propietarioRId": {
    "id": 1,
    "nombre": "John",
    "apellido": "Doe"
  },
  "clientes": []
}
Response file saved.
> 2024-02-10T202836.200.json

Response code: 200; Time: 244ms (244 ms); Content length: 285 bytes (285 B)

##### GET http://localhost:8080/hoteles/2?token=tokenMiguel
HTTP/1.1 200 
Content-Type: application/json
Transfer-Encoding: chunked
Date: Sat, 10 Feb 2024 19:30:14 GMT
Keep-Alive: timeout=60
Connection: keep-alive

[
  {
    "id": 2,
    "nombre": "Prueba Cambio",
    "direccion": "456 Calle Secundaria",
    "estrellas": 3,
    "descripcion": "Un lugar acogedor para toda la familia",
    "precioNoche": 120.0,
    "metrosCuadrados": 800.0,
    "numHabitaciones": 50,
    "anioFundado": 2010,
    "propietarioId": {
      "id": 2,
      "nombre": "Alice",
      "apellido": "Smith"
    },
    "clientes": []
  },
  {
    "id": 6,
    "nombre": "Gran Hotel Montaña",
    "direccion": "333 Calle de las Cumbres",
    "estrellas": 4,
    "descripcion": "Situado en las alturas con vistas panorámicas",
    "precioNoche": 220.0,
    "metrosCuadrados": 1600.0,
    "numHabitaciones": 90,
    "anioFundado": 2006,
    "propietarioId": {
      "id": 2,
      "nombre": "Alice",
      "apellido": "Smith"
    },
    "clientes": []
  },
  {
    "id": 10,
    "nombre": "Hotel de Montaña Escarpada",
    "direccion": "777 Camino Escarpado",
    "estrellas": 3,
    "descripcion": "Aventuras en un entorno montañoso",
    "precioNoche": 130.0,
    "metrosCuadrados": 900.0,
    "numHabitaciones": 40,
    "anioFundado": 2019,
    "propietarioId": {
      "id": 2,
      "nombre": "Alice",
      "apellido": "Smith"
    },
    "clientes": []
  },
  {
    "id": 14,
    "nombre": "Estancia Elegante",
    "direccion": "222 Elegancia Avenue",
    "estrellas": 5,
    "descripcion": "Donde el lujo se encuentra con la elegancia",
    "precioNoche": 320.0,
    "metrosCuadrados": 1800.0,
    "numHabitaciones": 95,
    "anioFundado": 2007,
    "propietarioId": {
      "id": 2,
      "nombre": "Alice",
      "apellido": "Smith"
    },
    "clientes": []
  },
  {
    "id": 18,
    "nombre": "Periquito",
    "direccion": "Calle la manuela Nogales 4",
    "estrellas": null,
    "descripcion": null,
    "precioNoche": null,
    "metrosCuadrados": null,
    "numHabitaciones": null,
    "anioFundado": null,
    "propietarioId": {
      "id": 2,
      "nombre": "Alice",
      "apellido": "Smith"
    },
    "clientes": []
  }
]
Response file saved.
> 2024-02-10T203014.200.json

Response code: 200; Time: 50ms (50 ms); Content length: 1493 bytes (1,49 kB)
  
