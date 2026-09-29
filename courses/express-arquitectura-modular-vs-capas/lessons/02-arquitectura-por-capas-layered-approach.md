# 2. Arquitectura por Capas (Layered Approach): Estructura y Flujo

La **Arquitectura por Capas** (*Layered / N-Tier Architecture*) es el patron mas intuitivo y extendido en el desarrollo backend. Su objetivo central es aplicar el principio de **Separacion de Responsabilidades (SoC)** organizando el codigo en capas horizontales donde cada capa tiene un rol tecnico exclusivo.

---

## Objetivos de la Leccion
- Comprender la funcion y limites de cada capa: Rutas, Controladores, Servicios y Repositorios.
- Implementar el flujo unidireccional estricto de peticion y respuesta.
- Aislar los objetos de transporte HTTP (`req`, `res`) de la logica comercial pura.
- Estructurar un proyecto Express real siguiendo el patron por capas.

---

## Anatomia de las Cuatro Capas Estandar

En una aplicacion Express profesional por capas, la peticion viaja en un solo sentido descendente:

```text
Flujo de una Peticion en Arquitectura por Capas:
Cliente HTTP ──► [ Rutas ] ──► [ Controlador ] ──► [ Servicio ] ──► [ Repositorio ] ──► Base de Datos
                (Enrutamiento)   (HTTP / Parsing)    (Reglas Negocio)   (SQL / ORM)
```

| Capa | Responsabilidad Exclusiva | Lo que NUNCA debe hacer |
| :--- | :--- | :--- |
| **1. Rutas (`routes/`)** | Mapear el metodo HTTP (GET, POST) y la URL al controlador correspondiente. Aplicar middlewares de autorizacion o validacion de esquemas. | No debe contener logica de procesamiento ni consultas de base de datos. |
| **2. Controladores (`controllers/`)** | Extraer datos de la peticion (`req.body`, `req.params`, `req.query`), invocar al servicio adecuado y retornar el codigo HTTP con el formato JSON (`res.status(200).json(...)`). | No debe ejecutar calculos matematicos comerciales ni sentencias SQL. |
| **3. Servicios (`services/`)** | Albergar la **Logica de Negocio** pura (calcular comisiones, aplicar descuentos, verificar limites, orquestar envios de correos). Es agnostico a Express. | **NUNCA debe recibir los objetos `req` ni `res`**. No debe saber si la llamada vino de HTTP, CLI o un cron. |
| **4. Repositorios / Modelos (`repositories/`)** | Ejecutar consultas a la base de datos (SELECT, INSERT, UPDATE) o comunicarse con bases de datos externas. | No debe tomar decisiones de reglas de negocio (ej. no debe decidir si el usuario tiene saldo suficiente). |

---

## Implementacion Practica Paso a Paso

### 1. Capa de Rutas (`src/routes/users.routes.js`)
```javascript
import { Router } from 'express';
import { UsersController } from '../controllers/users.controller.js';

const router = Router();
const controller = new UsersController();

router.get('/', controller.getAllUsers);
router.get('/:id', controller.getUserById);
router.post('/', controller.createUser);

export default router;
```

### 2. Capa de Controlador (`src/controllers/users.controller.js`)
El controlador solo habla el lenguaje HTTP:
```javascript
import { UsersService } from '../services/users.service.js';

export class UsersController {
    constructor() {
        this.usersService = new UsersService();
    }

    createUser = async (req, res, next) => {
        try {
            const { email, password, nombre } = req.body;
            
            // Invocacion a la capa de servicio con datos puros
            const nuevoUsuario = await this.usersService.registerUser({ email, password, nombre });
            
            // Retorno semantico HTTP 201 Created
            return res.status(201).json({
                success: true,
                data: nuevoUsuario
            });
        } catch (error) {
            next(error); // Pasa el error al middleware global de errores
        }
    };

    getUserById = async (req, res, next) => {
        try {
            const { id } = req.params;
            const usuario = await this.usersService.getUserDetails(id);
            return res.status(200).json({ success: true, data: usuario });
        } catch (error) {
            next(error);
        }
    };
}
```

### 3. Capa de Servicio (`src/services/users.service.js`)
El servicio no tiene ninguna dependencia de `express`. Recibe y devuelve datos puros de JavaScript:
```javascript
import { UsersRepository } from '../repositories/users.repository.js';

export class UsersService {
    constructor() {
        this.usersRepo = new UsersRepository();
    }

    async registerUser({ email, password, nombre }) {
        // Regla de Negocio 1: Validar si el correo ya existe
        const usuarioExistente = await this.usersRepo.findByEmail(email);
        if (usuarioExistente) {
            const err = new Error("El correo electronico ya se encuentra en uso.");
            err.statusCode = 409;
            throw err;
        }

        // Regla de Negocio 2: Aplicar reglas de transformacion
        const fechaRegistro = new Date().toISOString();
        const payloadLimpio = {
            email: email.toLowerCase().trim(),
            nombre: nombre.trim(),
            passwordHash: `hash_seguro_${password}`, // Simulacion de bcrypt
            fechaRegistro
        };

        // Persistir en el repositorio
        return await this.usersRepo.create(payloadLimpio);
    }

    async getUserDetails(id) {
        const usuario = await this.usersRepo.findById(id);
        if (!usuario) {
            const err = new Error("Usuario no encontrado.");
            err.statusCode = 404;
            throw err;
        }
        return usuario;
    }
}
```

### 4. Capa de Repositorio (`src/repositories/users.repository.js`)
```javascript
export class UsersRepository {
    // Simulacion de coleccion en base de datos
    #db = [
        { id: "1", email: "admin@eduxp.org", nombre: "Administrador" }
    ];

    async findByEmail(email) {
        return this.#db.find(u => u.email === email) || null;
    }

    async findById(id) {
        return this.#db.find(u => u.id === id) || null;
    }

    async create(datos) {
        const nuevo = { id: String(Date.now()), ...datos };
        this.#db.push(nuevo);
        return nuevo;
    }
}
```

---

## Ventajas del Enfoque por Capas
1. **Facil de Ensenar y Comprender:** Es el modelo estandar de referencia en la industria y la academia.
2. **Pruebas Unitarias Aisladas:** La capa `UsersService` puede ser testeada al 100% pasando repositorios mockeados sin necesidad de enviar peticiones HTTP reales.
3. **Reutilizacion de Logica:** Si un script CLI o tarea programada necesita registrar un usuario, simplemente importa `UsersService` sin depender de Express.

---

## Ejercicio Practico

Siguiendo el flujo de 4 capas presentado, implementa en tu editor la capa de `ProductsRoutes`, `ProductsController`, `ProductsService` y `ProductsRepository` para una entidad `Product` con operaciones `getAll` y `create`.
