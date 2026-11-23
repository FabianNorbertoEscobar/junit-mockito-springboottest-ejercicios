# Prácticas de testing con Java

Repositorio de prácticas para aprender y aplicar **JUnit 5**, **Mockito** y las herramientas de testing de **Spring Boot**. El proyecto está organizado en tres módulos Maven independientes, cada uno enfocado en un nivel diferente de pruebas automatizadas.

## Stack y tecnologías

- **Java 15**
- **Maven**
- **JUnit Jupiter 5.6.3**
- **Mockito 3.6.28**
- **Spring Boot 2.4.4**
- **Spring Web MVC**
- **Spring WebFlux** para pruebas reactivas
- **Spring Data JPA / Hibernate**
- **Base de datos H2** en memoria
- **Spring Boot Test**
- **MockMvc**, **TestRestTemplate** y **WebTestClient**
- **Springfox Swagger 3.0.0**
- **Jackson** para serialización y validación de JSON

## Estructura del repositorio

```text
.
├── junit5_app/       # Fundamentos y funcionalidades de JUnit 5
├── app-mockito/      # Pruebas unitarias de servicios con Mockito
└── springboot_test/  # API REST, persistencia y pruebas de integración
```

Cada carpeta contiene su propio `pom.xml` y puede ejecutarse de forma independiente.

## Funcionalidades y prácticas desarrolladas

### `junit5_app`

Prácticas sobre el ciclo de vida y las principales capacidades de JUnit 5:

- Tests de modelos de cuentas bancarias.
- Validación de saldos, débitos, créditos y transferencias entre cuentas.
- Asociación entre cuentas y bancos.
- Validación de excepciones, incluyendo `DineroInsuficienteException`.
- Uso de `@BeforeAll`, `@BeforeEach`, `@AfterEach` y `@AfterAll`.
- Tests anidados con `@Nested`, nombres descriptivos y etiquetas con `@Tag`.
- Assertions individuales y agrupadas con `assertAll`.
- Tests parametrizados con `@ValueSource`, `@CsvSource`, `@CsvFileSource` y `@MethodSource`.
- Tests repetidos con `@RepeatedTest`.
- Tests condicionados por sistema operativo, versión de Java, propiedades del sistema y variables de entorno.
- Suposiciones con `assumeTrue` y `assumingThat`.
- Validación de tiempos de ejecución con `@Timeout` y `assertTimeout`.
- Uso de `TestInfo` y `TestReporter`.

### `app-mockito`

Prácticas de testing unitario aislando las dependencias de un servicio:

- Búsqueda de exámenes por nombre.
- Carga de preguntas asociadas a un examen.
- Guardado de exámenes y preguntas.
- Uso de `@Mock`, `@InjectMocks` y `@ExtendWith(MockitoExtension.class)`.
- Configuración de comportamientos con `when(...).thenReturn(...)`.
- Respuestas dinámicas con `Answer`.
- Matchers como `any`, `anyLong` y `anyList`.
- Verificación de interacciones con `verify`.
- Casos con resultados, listas vacías y datos no encontrados.

### `springboot_test`

Aplicación REST de cuentas bancarias que permite:

- Listar todas las cuentas.
- Consultar el detalle de una cuenta.
- Crear una cuenta.
- Eliminar una cuenta.
- Transferir dinero entre cuentas.
- Consultar y actualizar el saldo mediante la capa de servicio.
- Registrar el total de transferencias realizadas por un banco.
- Persistir entidades con Spring Data JPA.
- Cargar datos iniciales mediante `import.sql`.
- Ejecutar la aplicación con una base H2.
- Exponer documentación Swagger para los controladores.

La API principal está disponible bajo el prefijo `/api/cuentas`:

| Método | Endpoint | Descripción |
|---|---|---|
| `GET` | `/api/cuentas` | Lista las cuentas |
| `GET` | `/api/cuentas/{id}` | Consulta una cuenta |
| `POST` | `/api/cuentas` | Crea una cuenta |
| `POST` | `/api/cuentas/transferir` | Realiza una transferencia |
| `DELETE` | `/api/cuentas/{id}` | Elimina una cuenta |

También se practican distintos niveles de prueba:

- **Unitarias de controlador** con `@WebMvcTest`, `MockMvc` y `@MockBean`.
- **Integración de persistencia** con `@DataJpaTest`.
- **Integración de la aplicación completa** con `@SpringBootTest`.
- Pruebas HTTP con `TestRestTemplate`.
- Pruebas HTTP reactivas con `WebTestClient`.
- Validación de códigos HTTP, headers, cuerpos JSON y operaciones CRUD.

## Cómo ejecutar los tests

Desde la raíz del repositorio:

```bash
cd junit5_app && mvn test
cd ../app-mockito && mvn test
cd ../springboot_test && ./mvnw test
```

En Windows, dentro de `springboot_test`, se puede utilizar:

```bat
mvnw.cmd test
```

## Cómo ejecutar la aplicación Spring Boot

```bash
cd springboot_test
./mvnw spring-boot:run
```

La API quedará disponible en `http://localhost:8080`. La interfaz de Swagger puede consultarse en `http://localhost:8080/swagger-ui/`.

## Objetivo del repositorio

El objetivo es practicar el diseño y la ejecución de pruebas automatizadas en Java, comenzando por pruebas unitarias con JUnit 5, incorporando mocks con Mockito y avanzando hacia pruebas de persistencia, controladores e integración en una aplicación Spring Boot.
