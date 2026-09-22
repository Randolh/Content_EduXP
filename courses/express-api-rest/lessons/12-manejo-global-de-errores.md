# Lección 12: Manejo Global de Errores y Excepciones Asíncronas

En esta lección aprenderás a capturar y gestionar de forma centralizada todos los errores en Express mediante el **Middleware Global de Manejo de Errores** (`err, req, res, next`).

---

## 1. El Middleware de Errores de 4 Parámetros

En Express, un middleware se reconoce como controlador de errores **únicamente si recibe exactamente 4 argumentos**: `(err, req, res, next)`. Se coloca al final de todas las rutas.

```javascript
import express from 'express';

const app = express();
app.use(express.json());

// Ruta que lanza un error deliberado o una excepción asíncrona
app.get('/api/datos-sensibles', (req, res, next) => {
  try {
    throw new Error('Fallo al conectar con el servicio externo');
  } catch (err) {
    next(err); // Delega el error al middleware global de errores
  }
});

// Middleware Centralizado de Errores (debe ubicarse AL FINAL de todas las rutas)
app.use((err, req, res, next) => {
  console.error('🔥 Error capturado en servidor:', err.stack);

  const statusCode = err.statusCode || 500;
  res.status(statusCode).json({
    status: 'error',
    message: err.message || 'Error interno del servidor'
  });
});
```

---

## 2. Errores Asíncronos en Express

Cuando trabajas con `async/await`, las promesas rechazadas no son capturadas automáticamente por Express a menos que uses `try/catch` llamando a `next(error)`.

```javascript
// Wrapper asíncrono reutilizable (asyncHandler)
const asyncHandler = (fn) => (req, res, next) => {
  Promise.resolve(fn(req, res, next)).catch(next);
};

// Endpoint asíncrono limpio
app.get('/api/usuarios', asyncHandler(async (req, res) => {
  const usuarios = await obtenerUsuariosDeBD(); // Si falla, se envía a next(err)
  res.json(usuarios);
}));
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué distingue la firma de un Middleware de Errores en Express en comparación con un middleware convencional?
> - [ ] Utiliza la palabra clave `error`.
> - [x] Requiere exactamente 4 parámetros en su definición `(err, req, res, next)`.
> - [ ] Se declara al principio de la aplicación antes de las rutas.
>
> **Explicación**: Express examina la cantidad de argumentos de las funciones de middleware. La presencia de 4 parámetros indica a Express que se trata de un middleware de manejo de errores.

---

## Ejercicio Práctico

Crea una clase personalizada de error `ErrorPersonalizado` que herede de `Error` y acepte un mensaje y un `statusCode` (ej. 404).
