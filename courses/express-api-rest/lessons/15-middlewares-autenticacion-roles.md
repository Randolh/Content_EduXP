# Lección 15: Protección de Rutas y Control de Acceso por Roles (RBAC)

En esta lección aprenderás a modularizar tus middlewares de autenticación y a construir un sistema de **Control de Acceso Basado en Roles (Role-Based Access Control - RBAC)**.

---

## 1. Middleware de Autenticación (`requireAuth`)

Aislamos la lógica de verificación de tokens en un middleware reutilizable que adjunta los datos del usuario a la propiedad `req.user`.

```javascript
import jwt from 'jsonwebtoken';

const JWT_SECRET = process.env.JWT_SECRET || 'secreto_desarrollo';

export function requireAuth(req, res, next) {
  const authHeader = req.headers.authorization;

  if (!authHeader || !authHeader.startsWith('Bearer ')) {
    return res.status(401).json({ error: 'Acceso denegado: Token no proporcionado' });
  }

  const token = authHeader.split(' ')[1];

  try {
    const usuarioDecodificado = jwt.verify(token, JWT_SECRET);
    req.user = usuarioDecodificado; // Adjunta los datos al objeto de petición
    next(); // Permite el paso al siguiente controlador
  } catch (error) {
    return res.status(403).json({ error: 'Token inválido o expirado' });
  }
}
```

---

## 2. Middleware de Autorización por Roles (`requireRole`)

Garantiza que únicamente los usuarios que posean ciertos roles permitidos puedan acceder a endpoints críticos (ej. eliminar usuarios, modificar catálogo).

```javascript
export function requireRole(...rolesPermitidos) {
  return (req, res, next) => {
    if (!req.user) {
      return res.status(401).json({ error: 'No autenticado' });
    }

    if (!rolesPermitidos.includes(req.user.role)) {
      return res.status(403).json({ 
        error: `Acceso prohibido: Se requiere rol [${rolesPermitidos.join(', ')}]` 
      });
    }

    next();
  };
}

// Ejemplo de Aplicación en Endpoints
app.get('/api/panel-usuario', requireAuth, (req, res) => {
  res.json({ mensaje: `Hola ${req.user.email}` });
});

app.delete('/api/productos/:id', requireAuth, requireRole('admin', 'superadmin'), (req, res) => {
  res.json({ mensaje: 'Producto eliminado por administrador' });
});
```

---

## Autoevaluación

> [!QUIZ]
> ¿Cuál es la diferencia conceptual entre **Autenticación** y **Autorización**?
> - [ ] Autenticación es para bases de datos y Autorización para HTML.
> - [x] Autenticación verifica **quién eres** (identidad) y Autorización verifica **qué tienes permiso de hacer** (permisos/roles).
> - [ ] Ambas palabras significan exactamente lo mismo.
>
> **Explicación**: Autenticación responde a "¿Eres quien dices ser?" (ej. login válido). Autorización responde a "¿Tienes permisos para realizar esta acción?" (ej. ¿eres Admin?).

---

## Ejercicio Práctico

Crea un middleware `requireAdmin` que utilice `requireRole('admin')` para proteger la ruta `POST /api/categorias`.
