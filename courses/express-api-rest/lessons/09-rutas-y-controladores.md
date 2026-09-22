# Lección 8: Organizar tu API en Rutas y Controladores

En esta lección final aprenderás a **organizar tu servidor dividiendo las rutas con `express.Router()`**.

---

## 1. Separar Rutas con `express.Router()`

Tener todas las rutas en un solo archivo `server.js` se vuelve desordenado cuando la aplicación crece.

### Archivo 1: `rutasUsuarios.js`
```javascript
import { Router } from 'express';

const router = Router();

router.get('/', (req, res) => {
  res.json([{ id: 1, nombre: "Ana" }]);
});

export default router;
```

### Archivo 2: `server.js`
```javascript
import express from 'express';
import rutasUsuarios from './rutasUsuarios.js';

const app = express();

// Usar el enrutador bajo el prefijo /api/usuarios
app.use('/api/usuarios', rutasUsuarios);

app.listen(3000);
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué clase de Express nos permite agrupar rutas en archivos independientes?
> - [ ] `express.Group()`
> - [x] `express.Router()`
> - [ ] `express.Module()`
>
> **Explicación**: `express.Router()` instancia un minienrutador aislado que se puede montar en cualquier app principal.

---

## Ejercicio Práctico Final

Crea un archivo de rutas `rutasProductos.js` con un endpoint `GET /` que devuelva 2 productos de prueba, y móntalo en `server.js` bajo `/api/productos`.
