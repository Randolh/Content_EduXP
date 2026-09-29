# 4. Arquitectura Modular (Feature-Based): Modulos Autocontenidos

La **Arquitectura Modular** (tambien denominada *Feature-Based*, *Vertical Slice* o *Orientada a Componentes*) propone un cambio de paradigma radical: **agrupar el codigo por dominio de negocio en lugar de agruparlo por rol tecnico**.

---

## Objetivos de la Leccion
- Comprender los principios de **Alta Cohesion** y **Bajo Acoplamiento** a nivel de directorios.
- Disenar la jerarquia de carpetas de un modulo autocontenido.
- Implementar la carpeta `shared/` para utilidades transversales (Cross-Cutting Concerns).
- Construir un modulo completo de Express.js listo para ser conectado o extraido como servicio autonomo.

---

## Principio de Cohesion Espacial

El principio rector de la Arquitectura Modular establece que:  
> *"Las cosas que cambian juntas, deben vivir juntas en el arbol de archivos."*

En lugar de desmembrar una funcionalidad en cinco directorios remotos, colocamos todos los archivos correspondientes a esa caracteristica dentro de una sola carpeta:

```text
Estructura Modular Profesional en Express.js:
src/
├── app.js                         # Configuracion del servidor Express
├── server.js                      # Punto de entrada y conexion de red
│
├── modules/                       # Modulos de Negocio Autocontenidos
│   ├── auth/                      # Dominio de Autenticacion
│   │   ├── auth.routes.js
│   │   ├── auth.controller.js
│   │   ├── auth.service.js
│   │   ├── auth.validator.js
│   │   └── index.js               # Punto de exportacion publica del modulo
│   │
│   ├── products/                  # Dominio de Productos
│   │   ├── products.routes.js
│   │   ├── products.controller.js
│   │   ├── products.service.js
│   │   └── products.repository.js
│   │
│   └── orders/                    # Dominio de Pedidos
│       ├── orders.routes.js
│       ├── orders.controller.js
│       ├── orders.service.js
│       └── orders.repository.js
│
└── shared/                        # Elementos Transversales Compartidos
    ├── config/                    # Variables de entorno
    ├── database/                  # Pool de conexiones a base de datos
    ├── middlewares/               # Error handler global, auth verify
    └── utils/                     # Helpers matematicos o de formato
```

---

## Anatomia de un Modulo Autocontenido

Cada modulo opera como una mini-aplicacion independiente. Internamente, el modulo conserva sus propias capas (rutas, controlador, servicio, repositorio), pero todas encapsuladas en su propio directorio:

### 1. El Servicio del Modulo (`src/modules/products/products.service.js`)
```javascript
export class ProductsService {
    #repo;

    constructor(productsRepository) {
        this.#repo = productsRepository;
    }

    async getCatalog(filters) {
        return await this.#repo.findAll(filters);
    }

    async createProduct(data) {
        if (data.price <= 0) {
            const err = new Error("El precio del producto debe ser positivo.");
            err.statusCode = 400;
            throw err;
        }
        return await this.#repo.save(data);
    }
}
```

### 2. El Controlador del Modulo (`src/modules/products/products.controller.js`)
```javascript
export class ProductsController {
    #service;

    constructor(productsService) {
        this.#service = productsService;
    }

    list = async (req, res, next) => {
        try {
            const items = await this.#service.getCatalog(req.query);
            res.json({ success: true, count: items.length, data: items });
        } catch (error) {
            next(error);
        }
    };

    create = async (req, res, next) => {
        try {
            const newItem = await this.#service.createProduct(req.body);
            res.status(201).json({ success: true, data: newItem });
        } catch (error) {
            next(error);
        }
    };
}
```

### 3. Las Rutas del Modulo (`src/modules/products/products.routes.js`)
```javascript
import { Router } from 'express';

export function createProductsRouter(controller) {
    const router = Router();

    router.get('/', controller.list);
    router.post('/', controller.create);

    return router;
}
```

### 4. Punto de Entrada Publico del Modulo (`src/modules/products/index.js`)
Este archivo actua como el **Facade / Contrato Publico** del modulo. Instancia las dependencias internas y expone unicamente el enrutador listo para ser montado por `app.js`:

```javascript
import { ProductsRepository } from './products.repository.js';
import { ProductsService } from './products.service.js';
import { ProductsController } from './products.controller.js';
import { createProductsRouter } from './products.routes.js';

// Cableado de dependencias del modulo
const repo = new ProductsRepository();
const service = new ProductsService(repo);
const controller = new ProductsController(service);
const router = createProductsRouter(controller);

// Exportacion del router y del servicio (para uso inter-modular si fuera necesario)
export { router as productsRouter, service as productsService };
```

---

## Montaje en `app.js`

El archivo principal de Express queda limpio, declarativo y sumamente legible:

```javascript
import express from 'express';
import { productsRouter } from './modules/products/index.js';
import { ordersRouter } from './modules/orders/index.js';
import { errorHandler } from './shared/middlewares/error.middleware.js';

const app = express();
app.use(express.json());

// Montaje desacoplado de modulos
app.use('/api/products', productsRouter);
app.use('/api/orders', ordersRouter);

// Middleware centralizado de errores
app.use(errorHandler);

export default app;
```

---

## Beneficios Clave del Enfoque Modular
1. **Eliminacion del Shotgun Surgery:** Si necesitas alterar el modulo de `products`, todos los archivos involucrados estan juntos en `modules/products/`.
2. **Escalabilidad de Equipos:** El Equipo A puede ser dueno absoluto de `modules/products` mientras el Equipo B trabaja en `modules/orders` sin generar conflictos en Git.
3. **Facilidad de Extraccion a Microservicios:** Si un modulo crece desmedidamente en trafico, basta con cortar la carpeta `modules/products` y moverla a un repositorio independiente con minima friccion.

---

## Ejercicio Practico

Crea la estructura de carpetas para un modulo llamado `src/modules/customers/`.  
Define dentro de el sus archivos `customers.routes.js`, `customers.controller.js`, `customers.service.js` e `index.js`, asegurando que `index.js` exporte el router configurado.
