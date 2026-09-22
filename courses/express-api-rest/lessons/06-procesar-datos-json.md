# Lección 6: Recibir datos en formato JSON (req.body)

En esta lección aprenderás a **recibir objetos JSON enviados desde el cliente** mediante `express.json()` y `req.body`.

---

## 1. Middleware `express.json()` y `req.body`

Por defecto, Express no sabe cómo leer objetos JSON en las peticiones. Debes incluir primero la línea `app.use(express.json())`:

```javascript
import express from 'express';

const app = express();

// Indispensable para habilitar la lectura de JSON
app.use(express.json());

app.post('/api/usuarios', (req, res) => {
  const datos = req.body; // { nombre: "Carlos", email: "carlos@ejemplo.com" }

  res.status(201).json({
    mensaje: "Usuario recibido con éxito",
    usuario: datos
  });
});
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué middleware nativo de Express se debe habilitar para poder leer datos enviados en formato JSON dentro de `req.body`?
> - [ ] `app.use(express.text())`
> - [x] `app.use(express.json())`
> - [ ] `app.use(express.static())`
>
> **Explicación**: `express.json()` parsea el cuerpo del request y lo convierte en un objeto JavaScript manejable.

---

## Ejercicio Práctico

Habilita `express.json()`, crea un endpoint `POST` en `/api/libros` que reciba `{ titulo, autor }` y lo devuelva impreso con estado HTTP 201.
