# PruebasSoftware
Ejemplos de pruebas de software: Unitarias, Integración y API
Pruebas Automatizadas Implementadas 



1. Pruebas Unitarias (`ClienteApp.Tests/Unitarias/ClienteServiceTests.cs`)
ObtenerPorId_ClienteExistente_DebeRetornarClienteEsperado
  * **Objetivo:** Verificar de forma aislada el comportamiento del método `ClienteService.ObtenerPorId(int id)`.
  * **Funcionamiento:** Utiliza un objeto simulado (`Mock<IClienteRepository>`) configurado para devolver un cliente específico al consultar el ID `1`. Comprueba que el servicio retorne exactamente los datos del cliente esperado (`NotNull`, `Id`, `Nombre` y `Correo`) y valida mediante `Verify(..., Times.Once)` que el repositorio sea consultado una única vez[cite: 3].

### 2. Pruebas de Integración (`ClienteApp.Tests/Integracion/ClienteRepositoryTests.cs`)
* **`ObtenerPorId_IdInexistente_DebeRetornarNulo`**: 
  * **Objetivo:** Validar la interacción real entre `ClienteService`, `ClienteRepository` y una base de datos **SQLite** temporal cuando se consulta un registro que no existe[cite: 3].
  * **Funcionamiento:** Inicializa una base de datos SQLite limpia y ejecuta `service.ObtenerPorId(999)`. Comprueba mediante `Assert.Null(resultado)` que la consulta retorne un valor nulo sin generar excepciones[cite: 3].

### 3. Pruebas de API (`ClienteApp.Tests/Api/ClientesApiTests.cs`)
Utilizando `HttpClient` y `WebApplicationFactory<Program>` (`ClienteApiFactory`) para levantar el servidor web de pruebas en memoria:

ObtenerPorId_ClienteExistente_DebeRetornar200
  * **Objetivo:** Verificar el flujo exitoso de consulta de un cliente a través de solicitudes HTTP.
  * **Funcionamiento:** Registra primero un cliente nuevo mediante `POST /api/Clientes` para obtener su identificador asignado y posteriormente realiza una petición `GET /api/Clientes/{id}`[cite: 3]. Valida que el endpoint responda con el código de estado **`200 OK`** y que el cuerpo JSON coincida con el cliente registrado.

* **`ObtenerPorId_ClienteInexistente_DebeRetornar404`**: 
  * **Objetivo:** Comprobar el manejo adecuado de recursos no encontrados en la API.
  * **Funcionamiento:** Envía una solicitud `GET /api/Clientes/99999` con un identificador inexistente y verifica que el controlador devuelva el código de estado **`404 Not Found`.


### Evidencias de Ejecución


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e8326696-a362-4e9d-a998-da00d66fe0ca" />

