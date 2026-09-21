# Lección 5: Autenticación con JWT, Cookies `httpOnly`, Bcrypt y Roles (RBAC)

¡Llegaste a la lección integradora del curso de **Express y APIs REST**! En esta lección aprenderás a implementar un sistema completo de seguridad profesional: encriptación de contraseñas con **bcryptjs**, generación de JSON Web Tokens (**JWT**), envío seguro en cookies `httpOnly` y autorización basada en roles (**RBAC**).

---

## 1. Instalación de Librerías de Seguridad

```bash
npm install bcryptjs jsonwebtoken cookie-parser
```

---

## 2. Hashing de Contraseñas con `bcryptjs`

Las contraseñas de los usuarios nunca deben almacenarse en texto plano. **Bcrypt** aplica un algoritmo de hash criptográfico unidireccional con un factor de costo (salt).

```javascript
import bcrypt from 'bcryptjs';

// 1. Encriptar contraseña antes de guardar en la Base de Datos
export async function hashearPassword(passwordPlana) {
  const salt = await bcrypt.genSalt(10);
  return bcrypt.hash(passwordPlana, salt);
}

// 2. Verificar contraseña ingresada en el Login
export async function compararPassword(passwordPlana, hashGuardado) {
  return bcrypt.compare(passwordPlana, hashGuardado);
}
```

---

## 3. Autenticación Stateless con JWT y Cookies `httpOnly`

Un **JWT** (JSON Web Token) firmado permite verificar la identidad del usuario sin almacenar sesiones en el servidor. Al almacenarlo en una cookie con la bandera `httpOnly: true`, protegemos el token de ataques de robo por scripts maliciosos de JavaScript (**XSS**).

### Servicio de Autenticación (`auth.service.js`)

```javascript
import jwt from 'jsonwebtoken';
import { UsersModel } from '../users/users.model.js';
import { hashearPassword, compararPassword } from '../../utils/security.js';

const JWT_SECRET = process.env.JWT_SECRET || 'secreto_super_seguro_eduxp';

export const AuthService = {
  async registrar({ nombre, email, password }) {
    const usuarioExistente = await UsersModel.findByEmail(email);
    if (usuarioExistente) {
      const error = new Error('El correo electrónico ya está registrado.');
      error.statusCode = 400;
      throw error;
    }

    const passwordHash = await hashearPassword(password);
    return UsersModel.create({ nombre, email, password: passwordHash, rol: 'USER' });
  },

  async login({ email, password }) {
    const usuario = await UsersModel.findByEmail(email);
    if (!usuario) {
      const error = new Error('Credenciales inválidas.');
      error.statusCode = 401;
      throw error;
    }

    const esValida = await compararPassword(password, usuario.password);
    if (!esValida) {
      const error = new Error('Credenciales inválidas.');
      error.statusCode = 401;
      throw error;
    }

    // Generar Token JWT válido por 2 horas
    const token = jwt.sign(
      { id: usuario.id, email: usuario.email, rol: usuario.rol },
      JWT_SECRET,
      { expiresIn: '2h' }
    );

    return { token, usuario: { id: usuario.id, nombre: usuario.nombre, email: usuario.email, rol: usuario.rol } };
  }
};
```

---

## 4. Middlewares de Autenticación y Control de Roles (RBAC)

### A. Middleware de Verificación de JWT (`auth.middleware.js`)

```javascript
import jwt from 'jsonwebtoken';

const JWT_SECRET = process.env.JWT_SECRET || 'secreto_super_seguro_eduxp';

export function autenticarToken(req, res, next) {
  // Extraer token desde las Cookies o del Header Authorization
  const token = req.cookies?.access_token || req.headers.authorization?.split(' ')[1];

  if (!token) {
    return res.status(401).json({
      success: false,
      error: { message: 'Acceso denegado: Token no proporcionado.', statusCode: 401 }
    });
  }

  try {
    const payload = jwt.verify(token, JWT_SECRET);
    req.user = payload; // Adjuntar datos del usuario verificado a req.user
    next();
  } catch (error) {
    res.status(403).json({
      success: false,
      error: { message: 'Token inválido o expirado.', statusCode: 403 }
    });
  }
}
```

### B. Middleware de Autorización por Roles (`role.middleware.js`)

```javascript
export function requerirRol(...rolesPermitidos) {
  return (req, res, next) => {
    if (!req.user || !rolesPermitidos.includes(req.user.rol)) {
      return res.status(403).json({
        success: false,
        error: {
          message: `Permisos insuficientes. Requiere rol: ${rolesPermitidos.join(' o ')}`,
          statusCode: 403
        }
      });
    }
    next();
  };
}
```

---

## 5. Endpoints de Registro, Login y Ruta Protegida por Rol

```javascript
// src/modules/auth/auth.routes.js
import { Router } from 'express';
import { AuthService } from './auth.service.js';
import { autenticarToken } from '../../middlewares/auth.middleware.js';
import { requerirRol } from '../../middlewares/role.middleware.js';

const router = Router();

// Endpoint de Login con Cookie Segura
router.post('/login', async (req, res, next) => {
  try {
    const { token, usuario } = await AuthService.login(req.body);

    // Configurar cookie httpOnly segura
    res.cookie('access_token', token, {
      httpOnly: true,
      secure: process.env.NODE_ENV === 'production',
      sameSite: 'strict',
      maxAge: 2 * 60 * 60 * 1000 // 2 horas
    });

    res.json({ success: true, data: { usuario, token } });
  } catch (error) {
    next(error);
  }
});

// Ruta del perfil del usuario (Requiere Autenticación)
router.get('/perfil', autenticarToken, (req, res) => {
  res.json({ success: true, data: { usuario: req.user } });
});

// Ruta de Administración (Requiere Autenticación y Rol ADMIN)
router.get('/panel-admin', autenticarToken, requerirRol('ADMIN'), (req, res) => {
  res.json({ success: true, data: { mensaje: 'Bienvenido al panel exclusivo de administradores.' } });
});

export default router;
```

---

## 💡 Autoevaluación

> [!QUIZ]
> ¿Cuál es la ventaja de enviar el token JWT dentro de una cookie configurada con la opción `httpOnly: true`?
> - [ ] Permite que el token se guarde automáticamente en la base de datos MySQL.
> - [x] Evita que scripts maliciosos ejecutados en el navegador (ataques XSS) puedan leer o robar el token mediante `document.cookie`.
> - [ ] Permite que la sesión nunca expire.
>
> **Explicación**: La directiva `httpOnly` le prohíbe expresamente al navegador acceder al contenido de la cookie desde JavaScript en el cliente, bloqueando los vectores de ataque de robo de identidad.

---

## 🛠️ Ejercicio Práctico Integrador: Logout

**Objetivo**: Crear la ruta `POST /api/auth/logout` que limpie la cookie `access_token`.

<details class="exercise-solution">
<summary>💡 Ver solución paso a paso</summary>

<div class="solution-content">

```javascript
router.post('/logout', (req, res) => {
  res.clearCookie('access_token');
  res.json({
    success: true,
    data: { mensaje: 'Sesión cerrada exitosamente.' }
  });
});
```

</div>
</details>

---

## 🏆 Resumen del Curso Express y APIs REST

¡Felicidades por completar el curso de **Express y APIs REST**!
Ahora dominas la creación de servicios backend seguros y de nivel profesional:
- Servidores HTTP y Middlewares en **Express Core**.
- Arquitectura limpia en 4 capas (**Routes, Controllers, Services, Models**).
- Validación de entradas con **Zod** y manejo global de errores.
- Conexión resiliente a bases de datos con **Connection Pools**.
- Autenticación segura con **Bcrypt, JWT, Cookies httpOnly y RBAC**.

¡Estás listo para el curso de **React Esencial**!
