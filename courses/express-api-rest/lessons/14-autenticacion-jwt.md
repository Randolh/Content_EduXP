# Lección 14: Autenticación Basada en Tokens con JSON Web Tokens (JWT)

En esta lección aprenderás a implementar el estándar de la industria para autenticación sin estado en APIs REST: **JSON Web Tokens (JWT)**.

---

## 1. Estructura de un JSON Web Token

Un JWT es una cadena codificada dividida en 3 partes separadas por puntos (`Header.Payload.Signature`):

1. **Header (Encabezado)**: Algoritmo de firma utilizado.
2. **Payload (Carga Útil)**: Información del usuario (`id`, `email`, `role`, expiración).
3. **Signature (Firma)**: Cifrado criptográfico generado con la clave secreta del servidor.

---

## 2. Generación y Verificación de Tokens

Instalamos la librería con `npm install jsonwebtoken`.

```javascript
import express from 'express';
import jwt from 'jsonwebtoken';

const app = express();
app.use(express.json());

const JWT_SECRET = 'clave_secreta_super_segura_123';

// 1. Endpoint de Login (Firma del Token)
app.post('/api/auth/login', (req, res) => {
  const { email, password } = req.body;

  // Supongamos que verificamos la contraseña con bcrypt y es válida...
  const usuarioBD = { id: 42, email: email, role: 'admin' };

  // Firmar y emitir el JWT (expira en 2 horas)
  const token = jwt.sign(
    { id: usuarioBD.id, email: usuarioBD.email, role: usuarioBD.role },
    JWT_SECRET,
    { expiresIn: '2h' }
  );

  res.json({ mensaje: 'Login exitoso', token });
});

// 2. Verificación del Token en un Endpoint Privado
app.get('/api/perfil', (req, res) => {
  const authHeader = req.headers.authorization;

  if (!authHeader || !authHeader.startsWith('Bearer ')) {
    return res.status(401).json({ error: 'Acceso no autorizado: Token ausente' });
  }

  const token = authHeader.split(' ')[1]; // Extrae el token eliminando 'Bearer '

  try {
    const payload = jwt.verify(token, JWT_SECRET);
    res.json({ mensaje: 'Perfil consultado', usuario: payload });
  } catch (error) {
    return res.status(403).json({ error: 'Token inválido o expirado' });
  }
});
```

---

## Autoevaluación

> [!QUIZ]
> ¿Dónde se envía habitualmente el token JWT en una petición HTTP cliente a una API REST?
> - [ ] En los parámetros de la URL.
> - [x] En el encabezado `Authorization` con el prefijo `Bearer <token>`.
> - [ ] En el cuerpo de todas las peticiones `GET`.
>
> **Explicación**: El estándar de la industria especifica que los tokens de autenticación se transmiten mediante el encabezado HTTP `Authorization: Bearer <token>`.

---

## Ejercicio Práctico

Genera un token JWT que contenga el `id` del usuario y expire en `15m` (15 minutos).
