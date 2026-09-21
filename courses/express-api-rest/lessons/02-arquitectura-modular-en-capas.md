# Lección 2: Arquitectura Limpia Modular: Routes, Controller, Service y Model

Construir una API REST en un solo archivo funciona para prototipos pequeños, pero se vuelve inmantenible en proyectos reales. En esta lección aprenderás a implementar el patrón de diseño modular en 4 capas (**Routes**, **Controller**, **Service**, **Model**), garantizando la separación de responsabilidades y la reusabilidad del código.

---

## 1. La Arquitectura en 4 Capas

```text
[ Cliente HTTP ] ──► Routes (Rutas HTTP)
                          │
                     Controllers (HTTP Req/Res & Status Codes)
                          │
                     Services (Lógica de Negocio y Reglas)
                          │
                     Models (Acceso a Datos / Persistencia)
```

1. **Routes (Rutas)**: Asocia la URL y el verbo HTTP (`GET`, `POST`, `PUT`, `DELETE`) con su controlador.
2. **Controller (Controlador)**: Extrae datos de la petición (`req.body`, `req.params`), invoca al servicio y retorna la respuesta HTTP (`res.json()`).
3. **Service (Servicio)**: Contiene la lógica de negocio pura (cálculos, validaciones relacionales, reglas del sistema).
4. **Model (Modelo)**: Interactúa directamente con la base de datos o almacén de datos.

---

## 2. Implementación Paso a Paso de un Módulo (`products`)

Estructura del módulo de productos:
```text
src/modules/products/
├── products.routes.js
├── products.controller.js
├── products.service.js
└── products.model.js
```

### 1. Capa de Modelo (`products.model.js`)

```javascript
// Simulación de base de datos en memoria
const productosDB = [
  { id: 1, nombre: 'Teclado Mecánico RGB', precio: 85.00 },
  { id: 2, nombre: 'Mouse Inalámbrico Pro', precio: 45.50 }
];

export const ProductsModel = {
  async findAll() {
    return productosDB;
  },

  async findById(id) {
    return productosDB.find(p => p.id === Number(id)) || null;
  },

  async create(datos) {
    const nuevoProducto = { id: Date.now(), ...datos };
    productosDB.push(nuevoProducto);
    return nuevoProducto;
  }
};
```

### 2. Capa de Servicio (`products.service.js`)

```javascript
import { ProductsModel } from './products.model.js';

export const ProductsService = {
  async obtenerTodos() {
    return ProductsModel.findAll();
  },

  async obtenerPorId(id) {
    const producto = await ProductsModel.findById(id);
    if (!producto) {
      const error = new Error(`Producto con ID ${id} no encontrado.`);
      error.statusCode = 404;
      throw error;
    }
    return producto;
  },

  async crearProducto(datos) {
    if (!datos.nombre || datos.precio <= 0) {
      const error = new Error('El nombre y un precio positivo son obligatorios.');
      error.statusCode = 400;
      throw error;
    }
    return ProductsModel.create(datos);
  }
};
```

### 3. Capa de Controlador (`products.controller.js`)

```javascript
import { ProductsService } from './products.service.js';

export const ProductsController = {
  async getAll(req, res, next) {
    try {
      const productos = await ProductsService.obtenerTodos();
      res.json({ success: true, data: productos });
    } catch (error) {
      next(error);
    }
  },

  async getById(req, res, next) {
    try {
      const producto = await ProductsService.obtenerPorId(req.params.id);
      res.json({ success: true, data: producto });
    } catch (error) {
      next(error);
    }
  },

  async create(req, res, next) {
    try {
      const nuevoProducto = await ProductsService.crearProducto(req.body);
      res.status(201).json({ success: true, data: nuevoProducto });
    } catch (error) {
      next(error);
    }
  }
};
```

### 4. Capa de Rutas (`products.routes.js`)

```javascript
import { Router } from 'express';
import { ProductsController } from './products.controller.js';

const router = Router();

router.get('/', ProductsController.getAll);
router.get('/:id', ProductsController.getById);
router.post('/', ProductsController.create);

export default router;
```

---

## 3. Formato Unificado de Respuestas HTTP

Todas las respuestas de la API deben ser consistentes:

```json
// Éxito (HTTP 200 / 201)
{
  "success": true,
  "data": { ... }
}

// Error (HTTP 400 / 404 / 500)
{
  "success": false,
  "error": {
    "message": "Descripción clara del error",
    "statusCode": 404
  }
}
```

---

## 💡 Autoevaluación

> [!QUIZ]
> ¿Cuál es la responsabilidad principal de la capa de Controlador (Controller)?
> - [ ] Ejecutar sentencias SQL directas hacia la base de datos.
> - [x] Recibir las peticiones HTTP (`req`), llamar al Servicio correspondiente y enviar la respuesta HTTP (`res`) con su código de estado.
> - [ ] Validar variables de entorno y configurar el puerto del servidor.
>
> **Explicación**: El controlador actúa como intermediario entre la capa web (HTTP) y la capa de lógica de negocio (Service).

---

## 🛠️ Ejercicio Práctico: Implementando el recurso `Categories`

**Objetivo**: Crear la estructura modular para el recurso `categories` con soporte para listado `GET /api/categories`.

<details class="exercise-solution">
<summary>💡 Ver solución paso a paso</summary>

<div class="solution-content">

```javascript
// src/modules/categories/categories.routes.js
import { Router } from 'express';

const router = Router();

router.get('/', (req, res) => {
  res.json({
    success: true,
    data: [
      { id: 1, nombre: 'Electrónica' },
      { id: 2, nombre: 'Hogar' }
    ]
  });
});

export default router;
```

Registrar en `src/app.js`:
```javascript
import categoriesRoutes from './modules/categories/categories.routes.js';

app.use('/api/categories', categoriesRoutes);
```

</div>
</details>

---

## 📌 Resumen

- Separar la aplicación en **Routes, Controller, Service y Model** facilita el mantenimiento.
- Los controladores solo gestionan HTTP; la lógica de negocio vive en los **Servicios**.
- Estandarizar las respuestas JSON mejora la integración con el frontend.
- En la siguiente lección aprenderás a automatizar las validaciones de entrada usando **Zod**.
