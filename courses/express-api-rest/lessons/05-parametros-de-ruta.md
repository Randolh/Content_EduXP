# Lección 5: Capturar datos desde la URL (req.params)

En esta lección aprenderás a **extraer variables dinámicas directamente desde la URL** usando `req.params`.

---

## 1. Parámetros Dinámicos (`:id`)

Cuando quieres consultar un elemento específico por su ID (ej. `/api/productos/5`), usas dos puntos `:` en la definición de la ruta:

```javascript
app.get('/api/productos/:id', (req, res) => {
  const idProducto = req.params.id;
  
  res.json({
    mensaje: `Consultando el producto con ID: ${idProducto}`
  });
});
```

Si el cliente visita `/api/productos/99`, la propiedad `req.params.id` valdrá `"99"`.

---

## Autoevaluación

> [!QUIZ]
> ¿Cómo se define un parámetro dinámico en la ruta de Express?
> - [ ] Anteponiendo un signo de dólares `$id`
> - [x] Anteponiendo dos puntos `:id`
> - [ ] Encerrándolo entre paréntesis `(id)`
>
> **Explicación**: Los dos puntos `:` le indican a Express que esa sección de la URL será una variable accesible en `req.params`.

---

## Ejercicio Práctico

Crea una ruta `app.get('/api/usuarios/:nombre', ...)` que responda en JSON con un saludo personalizado usando `req.params.nombre`.
