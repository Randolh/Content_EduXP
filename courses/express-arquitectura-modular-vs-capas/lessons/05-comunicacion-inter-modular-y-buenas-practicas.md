# 5. Comunicacion Inter-Modular, Inyeccion y Dependencias Circulares

Cuando dividimos una aplicacion en modulos independientes de negocio, surge un desafio arquitectonico critico: **¿Como se comunican los modulos entre si cuando una operacion requiere datos de otro dominio?** En esta leccion exploraras patrones para orquestar dependencias evitando el acoplamiento rigido y las dependencias circulares.

---

## Objetivos de la Leccion
- Resolver la interaccion entre dominios (por ejemplo, el modulo `orders` verificando stock en el modulo `products`).
- Identificar y resolver **Dependencias Circulares** en Node.js.
- Aplicar el patron de Inyeccion de Dependencias (Dependency Injection) manual.
- Implementar comunicacion orientada a eventos mediante `EventEmitter` nativo.

---

## El Desafio: Modulos que Necesitan Colaborar

Imagina que un cliente genera una nueva orden en el modulo `orders`. Para procesarla, la orden necesita:
1. Verificar si hay stock disponible del producto (Dominio `products`).
2. Descontar las unidades del inventario (Dominio `products`).
3. Registrar la factura (Dominio `billing`).

### Enfoque Erroneo (Acoplamiento Fuerte y Dependencia Circular):
Si `orders.service.js` importa directamente el repositorio interno de `products`, estamos rompiendo el encapsulamiento:

```javascript
// ANTIPATRON: Acceso no autorizado a las tripas de otro modulo
import { ProductsRepository } from '../products/products.repository.js'; // ❌ PROHIBIDO
```

---

## Solucion 1: Interfaces de Servicio y Fachadas Publicas

Un modulo **solo debe interactuar con otro modulo a traves del contrato publico expuesto en su archivo `index.js`**, jamas accediendo a los repositorios o controladores privados del vecino:

```text
Regla de Comunicacion:
[ Modulo Orders ] ──► (Invocacion de Metodo Publico) ──► [ Modulo Products: index.js ]
                                                                   │
                                                                   ▼
                                                         [ ProductsService ]
```

```javascript
// src/modules/orders/orders.service.js
export class OrdersService {
    #ordersRepo;
    #productsService; // Dependencia inyectada

    constructor(ordersRepo, productsService) {
        this.#ordersRepo = ordersRepo;
        this.#productsService = productsService;
    }

    async placeOrder({ clienteId, items }) {
        // 1. Consultar a traves del servicio formal de productos
        for (const item of items) {
            const disponible = await this.#productsService.checkAvailability(item.productoId, item.cantidad);
            if (!disponible) {
                const err = new Error(`Stock insuficiente para producto ${item.productoId}`);
                err.statusCode = 400;
                throw err;
            }
        }

        // 2. Crear la orden
        const nuevaOrden = await this.#ordersRepo.create({ clienteId, items });

        // 3. Reservar el stock
        for (const item of items) {
            await this.#productsService.reserveStock(item.productoId, item.cantidad);
        }

        return nuevaOrden;
    }
}
```

---

## Solucion 2: Arquitectura Desacoplada Basada en Eventos (`EventEmitter`)

Si no deseas que `orders` conozca en absoluto la existencia de `products` o `notifications`, puedes utilizar el patron **Publicador/Suscriptor (Pub/Sub)** con el modulo nativo `events` de Node.js:

```javascript
// src/shared/events/eventBus.js
import { EventEmitter } from 'events';
export const eventBus = new EventEmitter();
```

### 1. El Modulo Orders Publica el Evento
```javascript
// src/modules/orders/orders.service.js
import { eventBus } from '../../shared/events/eventBus.js';

export class OrdersService {
    async completeOrder(orderData) {
        // Logica de creacion de orden...
        const ordenGuardada = { id: 101, ...orderData };

        // Emite el evento sin importarle quien lo escucha
        eventBus.emit('order:created', ordenGuardada);

        return ordenGuardada;
    }
}
```

### 2. Otros Modulos se Suscriben de Forma Autonoma
```javascript
// src/modules/products/products.subscriber.js
import { eventBus } from '../../shared/events/eventBus.js';

export function initProductsSubscribers(productsService) {
    eventBus.on('order:created', async (orden) => {
        console.log(`[Products Module] Descontando stock por orden ${orden.id}`);
        // productsService.discountStock(orden.items);
    });
}
```

> [!TIP]
> La comunicacion por eventos desacopla los modulos al 100%. Si manana creas un nuevo modulo `analytics` o `email-marketing`, solo debes anadir un nuevo suscriptor sin tocar una sola linea de codigo en el modulo `orders`.

---

## Prevencion de Dependencias Circulares

Una dependencia circular ocurre cuando:  
Modulo A importa Modulo B, y Modulo B importa Modulo A.  
En Node.js esto suele provocar que una de las exportaciones se resuelva como un objeto vacio `{}` o `undefined`, arrojando errores del tipo `TypeError: Class extends value undefined is not a constructor`.

### Reglas de Oro para Evitar Ciclos:
1. **Flujo Unidireccional:** Si `orders` depende de `products`, `products` **nunca** debe depender de `orders`.
2. **Capa Compartida (`shared/`):** Si dos modulos necesitan una misma funcion utilitaria o constante, extraela a `src/shared/`.
3. **Inyeccion de Dependencias en el Arranque:** Conecta las dependencias en `index.js` o `app.js` en lugar de importar instancias directamente entre archivos de servicios.

---

## Ejercicio Practico

Implementa un `eventBus` en un archivo compartido. Crea dos modulos simulados: `AuthModule` y `AuditModule`.  
Cuando `AuthModule` ejecute `login(usuario)`, debe emitir el evento `auth:login-success`. `AuditModule` debe escuchar el evento e imprimir en consola: `"Registro de auditoria: Usuario conectado a las [FECHA]"`.
