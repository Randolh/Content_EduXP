# Lección 3: Validación Schematizada de Payloads con Zod y Error Handler

Validar manualmente cada campo de una petición HTTP enviada por el cliente (`if (!req.body.email) ...`) produce código repetitivo y propenso a fallos. En esta lección aprenderás a utilizar **Zod** para declarar esquemas de datos reutilizables y a crear un **Middleware Centralizado de Errores**.

---

## 1. Instalación de Zod y Creación de Esquemas

**Zod** es una librería de declaración y validación de esquemas basada en código JavaScript.

```bash
npm install zod
```

### Definición de Esquemas (`src/modules/users/users.schema.js`)

```javascript
import { z } from 'zod';

// Esquema de validación para registro de usuario
export const registroUsuarioSchema = z.object({
  nombre: z.string({
    required_error: 'El nombre es obligatorio'
  }).min(3, 'El nombre debe tener al menos 3 caracteres'),

  email: z.string({
    required_error: 'El email es obligatorio'
  }).email('El formato del correo electrónico no es válido'),

  password: z.string({
    required_error: 'La contraseña es obligatoria'
  }).min(6, 'La contraseña debe tener al menos 6 caracteres'),

  rol: z.enum(['USER', 'ADMIN']).optional().default('USER')
});
```

---

## 2. Middleware Genérico de Validación (`validate.js`)

Creamos un middleware reutilizable que recibe cualquier esquema Zod y valida el `req.body` antes de que la petición llegue al controlador:

```javascript
// src/middlewares/validate.js
export function validate(schema) {
  return (req, res, next) => {
    try {
      // parseOrThrow sanitiza y valida el body
      req.body = schema.parse(req.body);
      next();
    } catch (error) {
      if (error.name === 'ZodError') {
        const errorFormateado = new Error('Error de validación en los datos enviados');
        errorFormateado.statusCode = 400;
        errorFormateado.details = error.errors.map(err => ({
          campo: err.path.join('.'),
          mensaje: err.message
        }));
        return next(errorFormateado);
      }
      next(error);
    }
  };
}
```

---

## 3. Middleware Centralizado de Errores (`errorHandler.js`)

Express reconoce una función de 4 parámetros `(err, req, res, next)` como el controlador global de excepciones de toda la aplicación.

```javascript
// src/middlewares/errorHandler.js

export function errorHandler(err, req, res, next) {
  const statusCode = err.statusCode || 500;
  const message = err.message || 'Error interno del servidor';

  console.error(`[ERROR ${statusCode}]: ${message}`);

  res.status(statusCode).json({
    success: false,
    error: {
      message,
      statusCode,
      ...(err.details && { details: err.details })
    }
  });
}

// Middleware para capturar rutas inexistentes (HTTP 404)
export function notFoundHandler(req, res, next) {
  res.status(404).json({
    success: false,
    error: {
      message: `Ruta no encontrada: ${req.method} ${req.originalUrl}`,
      statusCode: 404
    }
  });
}
```

### Registrar los Middlewares de Error en `src/app.js`:

> [!IMPORTANT]
> `notFoundHandler` y `errorHandler` deben registrarse **después** de todas las rutas de la aplicación.

```javascript
import express from 'express';
import { errorHandler, notFoundHandler } from './middlewares/errorHandler.js';
import usersRoutes from './modules/users/users.routes.js';

const app = express();
app.use(express.json());

// Rutas de la API
app.use('/api/users', usersRoutes);

// Manejo de 404 y Errores Globales
app.use(notFoundHandler);
app.use(errorHandler);

export default app;
```

---

## 💡 Autoevaluación

> [!QUIZ]
> ¿Dónde se deben registrar los middlewares de manejo de errores en una aplicación Express?
> - [ ] Al principio de `src/app.js`, antes de los middlewares `express.json()` y `cors()`.
> - [x] Al final de `src/app.js`, exactamente después de la declaración de todas las rutas de la API.
> - [ ] En el archivo `server.js` dentro del callback `app.listen()`.
>
> **Explicación**: Express procesa las solicitudes en orden. Si una ruta o middleware falla y llama a `next(error)`, el flujo continuará bajando hasta encontrar el middleware de error `(err, req, res, next)`.

---

## 🛠️ Ejercicio Práctico: Aplicando Zod a un Endpoint de Registro

**Objetivo**: Aplicar el middleware de validación con Zod en la ruta `POST /api/users/registro`.

<details class="exercise-solution">
<summary>💡 Ver solución paso a paso</summary>

<div class="solution-content">

```javascript
// src/modules/users/users.routes.js
import { Router } from 'express';
import { validate } from '../../middlewares/validate.js';
import { registroUsuarioSchema } from './users.schema.js';

const router = Router();

router.post('/registro', validate(registroUsuarioSchema), (req, res) => {
  res.status(201).json({
    success: true,
    data: {
      mensaje: 'Usuario validado y registrado exitosamente',
      usuario: req.body
    }
  });
});

export default router;
```

Si envías una petición `POST` con un email inválido o sin contraseña, Zod retornará automáticamente una respuesta HTTP 400 formateada con el listado detallado de errores.

</div>
</details>

---

## 📌 Resumen

- **Zod** permite definir validaciones estrictas y sanitizar cuerpos de peticiones.
- Un middleware de validación genérico intercepta los `ZodError` y devuelve HTTP 400.
- El middleware de errores de 4 parámetros `(err, req, res, next)` captura todas las excepciones no controladas en un solo lugar.
- En la siguiente lección conectarás la API con bases de datos relacionales reales (**MySQL / SQLite**).
