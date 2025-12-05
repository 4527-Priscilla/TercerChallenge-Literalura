**<h1 align="center">:books:  DESAFÍO LITERALURA :books:</h1>**

**<h2 align="center"> Proyecto Alura Latam One - Practicando Spring Boot</h2>**

<p align="center">
    <img src="assets/Libros_portada.jpg" alt="Libros " width="700">
</p>

Este proyecto forma parte del curso **Alura Latam One - _Practicando Spring Boot._** En este desafío se realiza una aplicación de consola desarrollada con Spring Boot, que permite a los usuarios interactuar con la API de **Gutendex** (un índice de libros del Proyecto Gutenberg) y persistir la información de los libros y autores consultados en una base de datos local.

## :gear: Funcionalidades

La aplicación se ejecuta a través de un menú interactivo en la consola, ofreciendo las siguientes opciones de persistencia y consulta:

**1- Buscar Libro por Título:** Persistencia de Libro y Autor, manejo de relaciones @OneToMany y @ManyToOne.

**2- Listar Libros Registrados:** Consulta simple findAll().

**3- Listar Autores Registrados:** Consulta optimizada con FETCH JOIN.

**4- Listar Autores Vivos en Año:** Consulta JPQL personalizada que compara fechas de nacimiento y fallecimiento.

**5- Listar Libros por Idioma:** Consulta por palabra clave de Spring Data JPA: findByIdioma(String idioma).


## :computer: Tecnologías

- **Java** 17+ _Core Language_

- **Spring Boot** 3.x _Configuración y auto-configuración_

- **Spring Data JPA** Starter _Abstracción de persistencia_

- **H2 Database** Runtime _Base de datos en memoria para desarrollo_

- **Gutendex API** Cliente REST _Consumo de datos externos_

- **Jackson** Built-in _Conversión de JSON a objetos Java_

## :rocket: Inicio Rápido

### Requisitos

:white_check_mark: Asegúrate de tener el **JDK 17** o superior instalado.

### Ejecución

Abre el proyecto en tu IDE (IntelliJ, Eclipse, VS Code).

Ejecuta la clase principal ChallengeApplication.java.

La aplicación se ejecutará como un CommandLineRunner y automáticamente te presentará el menú de opciones.

### <ins> :thinking: ¿Cómo funciona? </ins> :thinking:

La aplicación sigue un flujo estructurado al buscar contenido:

- **Menú y Entrada:** El usuario selecciona una opción del menú y proporciona una entrada (ej. Opción 1, el título de un libro).

- **Verificación Local (Persistencia):** Se utiliza el método libroRepository.existsByTitulo() para verificar inmediatamente si el libro ya se encuentra en la base de datos H2. Esto evita llamadas innecesarias a la API externa.

- **Consulta Externa:** Si es nuevo, la clase ConsumoAPI realiza la solicitud HTTP. La respuesta JSON es inmediatamente procesada por la clase ConvierteDatos (utilizando la librería Jackson) y se mapea a los records de Java (DatosLibro, DatosAutor).

- **Persistencia:**
    - Autor Único: La aplicación busca si el autor ya existe utilizando un método personalizado del repositorio (autorRepository.findByNombreContainingIgnoreCase()). Esto es crucial para mantener la integridad de los datos y evitar duplicados de autores.

    - Relación y Guardado: Si el autor existe, se reutiliza su ID. Si no, se crea y se guarda primero. Finalmente, la entidad Libro se crea, se vincula con la instancia persistente del Autor (estableciendo la relación @ManyToOne), y se guarda en la base de datos (libroRepository.save()).

- **Resultado:** La información del libro y autor registrados se imprime en la consola, confirmando la persistencia.


 <img src="assets/Imagen_ejemplo.jpg" alt="Libros " width="480">
