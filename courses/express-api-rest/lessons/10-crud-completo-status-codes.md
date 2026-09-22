# Lección 10: CRUD Completo y Respuestas Semánticas (Status Codes)

En esta lección aprenderás a construir una API RESTful que implemente todas las operaciones del ciclo **CRUD (Create, Read, Update, Delete)** devolviendo códigos de estado HTTP semánticos y estructurados.

---

## 1. Códigos de Estado HTTP en APIs REST

Una API REST profesional debe indicar explícitamente el resultado de cada solicitud mediante el código de estado HTTP adecuado:

- **`200 OK`**: Petición exitosa (GET, PUT, PATCH).
- **`201 Created`**: Recurso creado exitosamente (POST).
- **`204 No Content`**: Recurso eliminado exitosamente sin contenido en la respuesta (DELETE).
- **`400 Bad Request`**: Los datos enviados por el cliente son inválidos o incompletos.
- **`404 Not Found`**: El recurso solicitado no existe.

---

## 2. Implementación de los Endpoints CRUD

```javascript
import express from 'express';

const app = express();
app.use(express.json());

let productos = [
  { id: 1, nombre: 'Laptop', precio: 999 },
  { id: 2, nombre: 'Mouse', precio: 25 }
];

// GET /api/productos - Obtener todos
app.get('/api/productos', (req, res) => {
  res.status(200).json(productos);
});

// POST /api/productos - Crear un recurso (201 Created)
app.post('/api/productos', (req, res) => {
  const { nombre, precio } = req.body;
  if (!nombre || !precio) {
    return res.status(400).json({ error: 'Nombre y precio son obligatorios' });
  }

  const nuevoProducto = { id: Date.now(), nombre, precio: Number(precio) };
  productos.push(nuevoProducto);
  res.status(201).json(nuevoProducto);
});

// PUT /api/productos/:id - Actualizar completamente un recurso
app.put('/api/productos/:id', (req, res) => {
  const id = Number(req.params.id);
  const index = productos.findIndex((p) => p.id === id);

  if (index === -1) {
    return res.status(404).json({ error: 'Producto no encontrado' });
  }

  productos[index] = { id, ...req.body };
  res.status(200).json(productos[index]);
});

// DELETE /api/productos/:id - Eliminar un recurso (204 No Content)
app.delete('/api/productos/:id', (req, res) => {
  const id = Number(req.params.id);
  const existe = productos.some((p) => p.id === id);

  if (!existe) {
    return res.status(404).json({ error: 'Producto no encontrado' });
  }

  productos = productos.filter((p) => p.id !== id);
  res.status(204).send(); // 204 no envía cuerpo de respuesta
});

app.listen(3000, () => console.log('Servidor CRUD listo en puerto 3000'));
```

---

## Autoevaluación

> [!QUIZ]
> ¿Cuál es el código de estado HTTP adecuado para responder tras crear exitosamente un nuevo registro con `POST`?
> - [ ] `200 OK`
> - [x] `201 Created`
> - [ ] `302 Found`
>
> **Explicación**: El código `201 Created` le comunica al cliente que la petición tuvo éxito y que se ha creado un nuevo recurso en el servidor.

---

## Ejercicio Práctico

Agrega un endpoint `PATCH /api/productos/:id` que permita actualizar únicamente el campo `precio` de un producto existente sin sobreescribir la propiedad `nombre`.
