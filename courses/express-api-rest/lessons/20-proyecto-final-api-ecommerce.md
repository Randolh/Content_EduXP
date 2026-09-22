# Lección 20: Proyecto Final Integrador: EduXP Store API

¡Felicitaciones por llegar a la lección final! En este proyecto integrador pondrás a prueba todo tu conocimiento construyendo la **EduXP Store API**, una API RESTful profesional completa para una plataforma de E-Commerce con autenticación JWT, seguridad, validaciones Zod, paginación y roles de usuario.

---

## 📋 Arquitectura y Requisitos del Proyecto

Construirás un servidor Express con la siguiente estructura de endpoints:

```text
POST   /api/auth/register    -> Registro de usuarios (Password Hashing con bcrypt)
POST   /api/auth/login       -> Login de usuarios (Generación de JWT)
GET    /api/auth/profile     -> Perfil del usuario autenticado (Protegido con JWT)

GET    /api/products         -> Catálogo con paginación, filtros por categoría y búsqueda
POST   /api/products         -> Crear producto (Protegido: requireAuth + requireRole('admin'))
DELETE /api/products/:id     -> Eliminar producto (Protegido: requireAuth + requireRole('admin'))

POST   /api/orders           -> Crear orden de compra (Protegido: requireAuth)
GET    /api/orders/mine      -> Ver las órdenes del usuario actual (Protegido: requireAuth)
```

---

## 💻 Código de Referencia Integrador (`server.js`)

```javascript
import express from 'express';
import cors from 'cors';
import helmet from 'helmet';
import bcrypt from 'bcryptjs';
import jwt from 'jsonwebtoken';
import { z } from 'zod';

const app = express();

// Middlewares de Seguridad Global
app.use(helmet());
app.use(cors());
app.use(express.json());

const JWT_SECRET = process.env.JWT_SECRET || 'secreto_super_seguro_eduxp';

// "Bases de Datos" simuladas en memoria
const usuarios = [];
const productos = [
  { id: 1, nombre: 'Laptop Pro', precio: 1200, categoria: 'tecnologia' },
  { id: 2, nombre: 'Teclado Mecánico', precio: 80, categoria: 'tecnologia' }
];
const ordenes = [];

// Middlewares de Autenticación y Roles
function requireAuth(req, res, next) {
  const authHeader = req.headers.authorization;
  if (!authHeader || !authHeader.startsWith('Bearer ')) {
    return res.status(401).json({ error: 'Token de acceso no proporcionado' });
  }
  const token = authHeader.split(' ')[1];
  try {
    req.user = jwt.verify(token, JWT_SECRET);
    next();
  } catch (err) {
    res.status(403).json({ error: 'Token inválido o expirado' });
  }
}

function requireRole(...roles) {
  return (req, res, next) => {
    if (!roles.includes(req.user.role)) {
      return res.status(403).json({ error: 'No tienes los permisos requeridos' });
    }
    next();
  };
}

// 1. Endpoint Registro
app.post('/api/auth/register', async (req, res, next) => {
  try {
    const { email, password, role = 'user' } = req.body;
    if (!email || !password) return res.status(400).json({ error: 'Faltan campos' });

    const passwordHash = await bcrypt.hash(password, 10);
    const nuevoUsuario = { id: Date.now(), email, passwordHash, role };
    usuarios.push(nuevoUsuario);

    res.status(201).json({ mensaje: 'Usuario registrado exitosamente', id: nuevoUsuario.id });
  } catch (err) { next(err); }
});

// 2. Endpoint Login
app.post('/api/auth/login', async (req, res, next) => {
  try {
    const { email, password } = req.body;
    const user = usuarios.find((u) => u.email === email);
    if (!user) return res.status(401).json({ error: 'Credenciales inválidas' });

    const coincide = await bcrypt.compare(password, user.passwordHash);
    if (!coincide) return res.status(401).json({ error: 'Credenciales inválidas' });

    const token = jwt.sign({ id: user.id, email: user.email, role: user.role }, JWT_SECRET, { expiresIn: '2h' });
    res.json({ mensaje: 'Login exitoso', token });
  } catch (err) { next(err); }
});

// 3. Endpoint Productos Paginados
app.get('/api/products', (req, res) => {
  const { search, limit = 10, page = 1 } = req.query;
  let items = [...productos];
  if (search) items = items.filter((p) => p.nombre.toLowerCase().includes(search.toLowerCase()));

  const paginados = items.slice((page - 1) * limit, page * limit);
  res.json({ total: items.length, page: Number(page), data: paginados });
});

// 4. Endpoint Crear Producto (Admin únicamente)
app.post('/api/products', requireAuth, requireRole('admin'), (req, res) => {
  const { nombre, precio, categoria } = req.body;
  const nuevo = { id: Date.now(), nombre, precio, categoria };
  productos.push(nuevo);
  res.status(201).json(nuevo);
});

// Middleware Global de Errores
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ error: 'Error interno del servidor', detalle: err.message });
});

app.listen(4000, () => console.log('🚀 EduXP Store API ejecutándose en puerto 4000'));
```

---

## 🏆 Criterios de Evaluación y Entrega

1. **Respuestas HTTP Semánticas**: Uso adecuado de códigos 200, 201, 400, 401, 403, 404 y 500.
2. **Seguridad**: Passwords encriptados con `bcrypt`, firmas de JWT válidas y protección con Helmet.
3. **Control de Acceso**: Endpoints administrativos restringidos exclusivamente a usuarios con rol `'admin'`.
4. **Resiliencia**: Captura centralizada de excepciones asíncronas con el middleware global de errores.

¡Felicidades! Al completar esta API habrás adquirido las competencias necesarias para construir backends reales en Node.js y Express para la industria.
