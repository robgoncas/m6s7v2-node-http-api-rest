
# Repaso: API, API REST, API RESTful, Métodos HTTP, Códigos HTTP, Postman

## 1. ¿Qué es una API?
Una **API** (Application Programming Interface) es un conjunto de reglas que permite la interacción entre diferentes sistemas de software. Proporciona un medio para que las aplicaciones se comuniquen entre sí, generalmente exponiendo funciones o datos que otros sistemas pueden usar.

## 2. ¿Qué es una API REST?
**REST** (Representational State Transfer) es un estilo de arquitectura para diseñar servicios web que se basa en los estándares HTTP. Las API que siguen estos principios son llamadas **API REST**. Estas API permiten la interacción entre clientes y servidores utilizando las operaciones estándar de HTTP.

## 3. ¿Qué es una API RESTful?
Una **API RESTful** es una API que sigue los principios de REST y está diseñada para ser simple, escalable y sin estado. Algunas características clave de una API RESTful son:
- Uso de métodos HTTP (GET, POST, PUT, DELETE, etc.).
- Uso de URL para acceder a los recursos.
- Comunicación sin estado (cada solicitud contiene toda la información necesaria).

## 4. Métodos HTTP más comunes
Los **métodos HTTP** son acciones que se pueden realizar sobre los recursos de una API. Los más utilizados son:
- **GET**: Obtener información de un recurso.
- **POST**: Enviar datos para crear un nuevo recurso.
- **PUT**: Actualizar completamente un recurso existente.
- **PATCH**: Actualizar parcialmente un recurso.
- **DELETE**: Eliminar un recurso.

## 5. Códigos de estado HTTP
Los **códigos de estado HTTP** son respuestas estándar del servidor que indican el resultado de una solicitud HTTP:
- **2xx: Éxito**
  - **200 OK**: Solicitud exitosa.
  - **201 Created**: Recurso creado exitosamente.
- **3xx: Redirección**
  - **301 Moved Permanently**: El recurso ha sido movido permanentemente.
- **4xx: Error del cliente**
  - **400 Bad Request**: La solicitud es incorrecta.
  - **401 Unauthorized**: Falta autenticación.
  - **404 Not Found**: Recurso no encontrado.
- **5xx: Error del servidor**
  - **500 Internal Server Error**: Error en el servidor.
  - **503 Service Unavailable**: Servicio no disponible.

## 6. Postman
**Postman** es una herramienta que facilita la creación, prueba y documentación de API. Permite realizar solicitudes HTTP a servidores para interactuar con una API y verificar su funcionamiento. Con Postman puedes:
- Hacer solicitudes GET, POST, PUT, DELETE, entre otras.
- Ver las respuestas del servidor y sus códigos de estado.
- Crear colecciones de pruebas automatizadas.

---

## 7. Estructura simple de un servidor web con el módulo `http`

A continuación, un ejemplo básico de un servidor en Node.js usando el módulo `http` que maneja solicitudes GET y POST.

```javascript
// Importar el módulo http
const http = require('http');

// Crear el servidor
const server = http.createServer((req, res) => {
    // Definir la cabecera de la respuesta
    res.setHeader('Content-Type', 'application/json');

    // Manejar diferentes rutas y métodos
    if (req.method === 'GET' && req.url === '/') {
        // Respuesta para una solicitud GET en la raíz
        res.statusCode = 200;
        res.end(JSON.stringify({ message: 'Bienvenido a la API' }));
    } else if (req.method === 'POST' && req.url === '/datos') {
        let body = '';

        // Obtener los datos del cuerpo de la solicitud POST
        req.on('data', chunk => {
            body += chunk.toString();
        });

        req.on('end', () => {
            res.statusCode = 200;
            res.end(JSON.stringify({
                message: 'Datos recibidos',
                data: JSON.parse(body)
            }));
        });
    } else {
        // Respuesta para cualquier otra ruta
        res.statusCode = 404;
        res.end(JSON.stringify({ message: 'Ruta no encontrada' }));
    }
});

// Definir el puerto en el que escucha el servidor
const PORT = 3000;
server.listen(PORT, () => {
    console.log(`Servidor escuchando en http://localhost:${PORT}`);
});
```

### Explicación:
- El servidor maneja dos rutas:
  - **GET** `/`: Devuelve un mensaje de bienvenida.
  - **POST** `/datos`: Recibe datos del cliente, los procesa y devuelve una respuesta con los datos enviados.
- La respuesta se envía en formato JSON.
- Si la ruta no existe, devuelve un código de estado **404**.
