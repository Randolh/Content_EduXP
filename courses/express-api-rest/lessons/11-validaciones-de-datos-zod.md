# Lección 11: Validación Estricta de Datos con Zod

En esta lección aprenderás a proteger tus endpoints backend validando la estructura y el tipo de los datos entrantes (`req.body`) utilizando la librería de esquemas TypeScript/JavaScript **Zod**.

---

## 1. ¿Por qué validar datos en el Backend?

Nunca debemos confiar en la información enviada por los clientes. Un usuario o atacante puede enviar tipos de datos erróneos (ej. texto donde se espera un número, un email inválido o inyecciones).

---

## 2. Definición de Esquemas y Middleware de Validación

Instalamos la librería con `npm install zod`.

```javascript
import express from 'express';
import { z } from 'zod';

const app = express();
app.use(express.json());

// 1. Definir el esquema de validación
const productoSchema = z.object({
  nombre: z.string({ required_error: 'El nombre es obligatorio' }).min(3, 'Mínimo 3 caracteres'),
  precio: z.number().positive('El precio debe ser un número mayor a 0'),
  categoria: z.enum(['electronica', 'ropa', 'hogar']),
  disponible: z.boolean().default(true)
});

// 2. Middleware de Validación Reutilizable
function validarEsquema(schema) {
  return (req, res, next) => {
    const resultado = schema.safeParse(req.body);
    if (!resultado.success) {
      return res.status(400).json({
        error: 'Datos de entrada inválidos',
        detalles: resultado.error.errors.map((e) => e.message)
      });
    }
    // Asignar los datos parseados y limpios a req.body
    req.body = resultado.data;
    next();
  };
}

// 3. Uso en Endpoints
app.post('/api/productos', validarEsquema(productoSchema), (req, res) => {
  // Aquí req.body tiene la garantía total de ser válido
  res.status(201).json({ mensaje: 'Producto creado', producto: req.body });
});
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué ventaja ofrece `schema.safeParse(data)` en lugar de `schema.parse(data)` al usar Zod?
> - [ ] `safeParse` es más lento.
> - [x] `safeParse` retorna un objeto `{ success: true/false }` sin lanzar una excepción que detenga el servidor.
> - [ ] `safeParse` borra todos los datos.
>
> **Explicación**: `safeParse` procesa los datos de forma segura retornando un objeto booleano `success` e información sobre los errores sin requerir bloques `try/catch` para capturar excepciones de validación.

---

## Ejercicio Práctico

Crea un esquema Zod para validar un objeto `usuario` con los campos: `username` (string de min 4 caracteres), `email` (string con formato email válido) y `edad` (número min 18).
