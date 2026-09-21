# Lección 1: Express Core: Servidores, Rutas HTTP y Middlewares

**Express.js** es el framework web minimalista y flexible más utilizado en el ecosistema Node.js para crear APIs REST y aplicaciones de backend. En esta lección aprenderás a inicializar un servidor Express, manejar las peticiones HTTP y entender la piedra angular de Express: **los Middlewares**.

---

## 1. Setup e Instalación del Servidor Express

Para iniciar un proyecto backend con Express usando **ES Modules**, configuramos el archivo `package.json`:

```bash
mkdir mi-backend-express
cd mi-backend-express
npm init -y
npm install express dotenv cors
```

### `package.json`
```json
{
  "name": "mi-backend-express",
  "version": "1.0.0",
  "type": "module",
  "main": "src/server.js",
  "scripts": {
    "start": "node src/server.js",
    "dev": "node --watch src/server.js"
  }
}
```

---

## 2. Estructura del Servidor y Middlewares

Los **Middlewares** son funciones que se ejecutan en secuencia durante el ciclo de vida de una petición HTTP antes de llegar a la respuesta final. Tienen acceso a los objetos `req` (petición), `res` (respuesta) y a la función `next()` para pasar el control al siguiente middleware.

### `src/app.js` (Configuración de Express y Middlewares)

```javascript
import express from 'express';
import cors from 'cors';

const app = express();

// Middleware 1: Permitir solicitudes origen cruzado (CORS)
app.use(cors());

// Middleware 2: Parsear automáticamente cuerpos de peticiones JSON
app.use(express.json());

// Middleware 3: Logger personalizado de peticiones HTTP
app.use((req, res, next) => {
  const timestamp = new Date().toISOString();
  console.log(`[${timestamp}] ${req.method} => ${req.originalUrl}`);
  next(); // ¡Crucial! Pasa al siguiente middleware o ruta
});

// Ruta Healthcheck
app.get('/api/health', (req, res) => {
  res.json({
    status: 'OK',
    mensaje: 'Servidor Express en ejecución',
    timestamp: new Date()
  });
});

export default app;
```

### `src/server.js` (Punto de entrada)

```javascript
import dotenv from 'dotenv';
import app from './app.js';

dotenv.config();

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => {
  console.log(`🚀 API REST escuchando en http://localhost:${PORT}`);
});
```

---

## 3. Extracción de Parámetros en Express

Express permite capturar datos del cliente a través de 3 vías principales:

```javascript
// A. req.params -> Parámetros de ruta (/api/productos/42)
app.get('/api/productos/:id', (req, res) => {
  const { id } = req.params;
  res.json({ idConsultado: id });
});

// B. req.query -> Parámetros de consulta (/api/productos?categoria=laptops&orden=precio)
app.get('/api/productos', (req, res) => {
  const { categoria, orden } = req.query;
  res.json({ categoria, orden });
});

// C. req.body -> Payload JSON enviado en POST/PUT
app.post('/api/productos', (req, res) => {
  const { nombre, precio } = req.body;
  res.status(201).json({
    mensaje: 'Producto creado exitosamente',
    producto: { id: Date.now(), nombre, precio }
  });
});
```

---

## 💡 Autoevaluación

> [!QUIZ]
> ¿Qué sucede si en un middleware personalizado olvidas llamar a la función `next()` y no envías una respuesta con `res.json()` o `res.send()`?
> - [ ] Express lanza automáticamente un error 500 Internal Server Error.
> - [x] La petición del cliente se quedará colgada indefinidamente esperando respuesta hasta dar un timeout.
> - [ ] El servidor se reiniciará automáticamente.
>
> **Explicación**: `next()` es la señal explícita para que Express avance a la siguiente función middleware. Sin `next()` o sin enviar respuesta, la cadena de ejecución se congela.

---

## 🛠️ Ejercicio Práctico: Middleware Restringido por API Key

**Objetivo**: Crear un middleware que proteja la ruta `/api/admin` exigiendo la cabecera HTTP `x-api-key`.

**Instrucciones**:
1. Si la cabecera `req.headers['x-api-key']` es igual a `'mi-secreto-123'`, llama a `next()`.
2. De lo contrario, responde inmediatamente con estado HTTP 401 Unauthorized `{ error: 'Acceso denegado' }`.

<details class="exercise-solution">
<summary>💡 Ver solución paso a paso</summary>

<div class="solution-content">

```javascript
function verificarApiKey(req, res, next) {
  const apiKey = req.headers['x-api-key'];

  if (apiKey && apiKey === 'mi-secreto-123') {
    return next(); // Continuar a la ruta protegida
  }

  res.status(401).json({
    success: false,
    error: 'Acceso no autorizado: API Key inválida o faltante.'
  });
}

// Aplicar el middleware únicamente a la ruta protegida
app.get('/api/admin', verificarApiKey, (req, res) => {
  res.json({ mensaje: 'Bienvenido al panel confidencial de administración.' });
});
```

</div>
</details>

---

## 📌 Resumen

- Express simplifica la creación de servidores HTTP en Node.js.
- `express.json()` es indispensable para procesar solicitudes con payload JSON.
- Los **Middlewares** procesan solicitudes secuencialmente; recuerda siempre invocar `next()`.
- En la siguiente lección aprenderás a estructurar una API profesional con arquitectura en 4 capas (**Routes, Controller, Service, Model**).
