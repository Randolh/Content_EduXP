# 6. Matriz de Decision, Migracion Gradual y Proyecto Integrador

En esta leccion final consolidaras el criterio arquitectonico para saber con certeza cuando implementar el Enfoque por Capas, cuando optar por el Enfoque Modular, como ejecutar una migracion gradual sin detener la operacion del negocio y revisaras el **Proyecto Integrador**.

---

## Objetivos de la Leccion
- Aplicar una matriz de decision tecnica objetiva basada en complejidad y equipo.
- Disenar una estrategia de refactorizacion paso a paso de Capas a Modular (Strangler Fig Pattern).
- Implementar la arquitectura completa del Proyecto Final Integrador en Express.js.

---

## Matriz de Decision: ¿Que Enfoque Seleccionar?

El rol de un ingeniero de software no es aplicar dogmaticamente un patron, sino elegir la herramienta mas eficiente para el contexto especifico del proyecto:

| Criterio del Proyecto | Enfoque por Capas (Layered) | Enfoque Modular (Feature-Based) |
| :--- | :--- | :--- |
| **Tamano del Proyecto** | Pequeno o Mediano (< 15 entidades). | Mediano a Grande (15+ entidades). |
| **Tamano del Equipo** | 1 a 3 desarrolladores. | 4 o mas desarrolladores en multiples equipos. |
| **Frecuencia de Cambios** | Estable, pocas caracteristicas nuevas por mes. | Alta velocidad, multiples releases semanales. |
| **Complejidad del Dominio** | CRUDs estandar con reglas de negocio simples. | Reglas de negocio densas con flujos complejos. |
| **Tiempo Inicial de Setup** | Ultrarrapido (estructura inmediata). | Requiere analisis previo de limites de dominio. |
| **Ruta hacia Microservicios** | No prevista o innecesaria. | Altamente probable o contemplada a futuro. |

---

## Estrategia de Migracion Gradual (Patron Strangler)

Si ya tienes una aplicacion Express en produccion construida con arquitectura por capas tradicional, **no intentes reescribirla desde cero en una sola semana**. Las reescrituras totales suelen fracasar.

La mejor practica es la migracion incremental:
1. **Paso 1:** Crea la carpeta `src/modules/` en tu proyecto existente.
2. **Paso 2:** Selecciona una funcionalidad nueva que deba construirse y creala 100% como un modulo autocontenido en `modules/nueva-feature/`.
3. **Paso 3:** Monta el router del nuevo modulo en `app.js` junto a las rutas viejas.
4. **Paso 4:** Conforme toque dar mantenimiento a funcionalidades viejas, toma un dominio (por ejemplo `auth`), extrae sus controladores, rutas y servicios dispersos y unificalos en `modules/auth/`.
5. Con el tiempo, las carpetas horizontales viejas iran vaciandose hasta desaparecer sin riesgos operativos.

---

## Proyecto Final Integrador: Sistema de Gestion Modular en Express

A continuacion se presenta la implementacion de la aplicacion modular que consolida todo el curso, demostrando la interconexion entre modulos, capa shared y manejo de errores:

```javascript
// src/shared/middlewares/error.middleware.js
export function errorHandler(err, req, res, next) {
    const status = err.statusCode || 500;
    const message = err.message || "Error interno del servidor.";
    
    console.error(`[ERROR HTTP ${status}]: ${message}`);
    
    res.status(status).json({
        success: false,
        status,
        error: message
    });
}
```

```javascript
// src/modules/products/index.js
import { Router } from 'express';

class ProductsService {
    #products = [
        { id: 1, name: "Servidor Rack 2U", stock: 10, price: 2500 }
    ];

    async getById(id) {
        return this.#products.find(p => p.id === Number(id)) || null;
    }

    async decrementStock(id, qty) {
        const prod = await this.getById(id);
        if (!prod || prod.stock < qty) return false;
        prod.stock -= qty;
        return true;
    }
}

const productsService = new ProductsService();
const productsRouter = Router();

productsRouter.get('/:id', async (req, res, next) => {
    try {
        const prod = await productsService.getById(req.params.id);
        if (!prod) {
            const err = new Error("Producto no encontrado.");
            err.statusCode = 404;
            throw err;
        }
        res.json({ success: true, data: prod });
    } catch (e) { next(e); }
});

export { productsRouter, productsService };
```

```javascript
// src/modules/orders/index.js
import { Router } from 'express';
import { productsService } from '../products/index.js'; // Contrato formal de fachada

class OrdersService {
    #orders = [];

    async createOrder(productId, quantity) {
        // Consulta limpia a la interfaz publica del modulo vecino
        const product = await productsService.getById(productId);
        if (!product) {
            const err = new Error("El producto solicitado no existe.");
            err.statusCode = 404;
            throw err;
        }

        const success = await productsService.decrementStock(productId, quantity);
        if (!success) {
            const err = new Error("Existencias insuficientes para liquidar la orden.");
            err.statusCode = 400;
            throw err;
        }

        const order = {
            id: this.#orders.length + 1,
            productId,
            quantity,
            total: product.price * quantity,
            createdAt: new Date().toISOString()
        };

        this.#orders.push(order);
        return order;
    }
}

const ordersService = new OrdersService();
const ordersRouter = Router();

ordersRouter.post('/', async (req, res, next) => {
    try {
        const { productId, quantity } = req.body;
        const newOrder = await ordersService.createOrder(productId, quantity);
        res.status(201).json({ success: true, data: newOrder });
    } catch (e) { next(e); }
});

export { ordersRouter };
```

```javascript
// src/app.js - Servidor ensamblador
import express from 'express';
import { productsRouter } from './modules/products/index.js';
import { ordersRouter } from './modules/orders/index.js';
import { errorHandler } from './shared/middlewares/error.middleware.js';

const app = express();
app.use(express.json());

// Montaje modular de sub-aplicaciones
app.use('/api/products', productsRouter);
app.use('/api/orders', ordersRouter);

// Manejador centralizado
app.use(errorHandler);

export default app;
```

---

## Conclusiones del Curso
Has completado el curso **Arquitectura en Express: Modular vs Capas**. Ahora posees los fundamentos teoricos, la experiencia practica y el discernimiento de ingenieria para disenar y escalar arquitecturas backend de alto nivel en Node.js y Express.js.
