# Lección 19: Paginación, Filtrado y Búsqueda por Parámetros (req.query)

En esta lección aprenderás a construir endpoints de lectura flexibles capturando parámetros de consulta en la URL mediante **`req.query`** para implementar paginación, filtros por categoría y búsqueda textual.

---

## 1. Parámetros Query (`req.query`)

Los Query Parameters se agregan al final de la URL comenzando con un signo `?` y separados por `&` (ej. `/api/productos?page=1&limit=10&search=laptop`).

```javascript
import express from 'express';

const app = express();

const productos = Array.from({ length: 50 }, (_, i) => ({
  id: i + 1,
  nombre: `Producto ${i + 1}`,
  categoria: i % 2 === 0 ? 'tecnologia' : 'hogar',
  precio: (i + 1) * 10
}));

// GET /api/productos?page=1&limit=5&category=tecnologia&search=Prod
app.get('/api/productos', (req, res) => {
  let { page = 1, limit = 10, category, search } = req.query;

  page = Number(page);
  limit = Number(limit);
  let resultado = [...productos];

  // 1. Filtrado por categoría
  if (category) {
    resultado = resultado.filter((p) => p.categoria.toLowerCase() === category.toLowerCase());
  }

  // 2. Búsqueda por texto (case insensitive)
  if (search) {
    resultado = resultado.filter((p) => p.nombre.toLowerCase().includes(search.toLowerCase()));
  }

  // 3. Paginación (slice)
  const inicio = (page - 1) * limit;
  const fin = inicio + limit;
  const paginados = resultado.slice(inicio, fin);

  res.json({
    paginaActual: page,
    limitePorPagina: limit,
    totalElementos: resultado.length,
    totalPaginas: Math.ceil(resultado.length / limit),
    datos: paginados
  });
});
```

---

## Autoevaluación

> [!QUIZ]
> En la URL `/api/libros?autor=cervantes&orden=asc`, ¿cómo accedes al valor del parámetro `autor` en Express?
> - [ ] `req.params.autor`
> - [x] `req.query.autor`
> - [ ] `req.body.autor`
>
> **Explicación**: Los parámetros de consulta ubicados después del carácter `?` en la URL son analizados por Express y expuestos en el objeto `req.query`.

---

## Ejercicio Práctico

Implementa una ordenación dinámica capturando `req.query.sort` para ordenar un arreglo de productos por precio en orden ascendente (`asc`) o descendente (`desc`).
