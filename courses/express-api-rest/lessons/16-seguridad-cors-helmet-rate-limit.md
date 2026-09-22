# Lección 16: Seguridad y Buenas Prácticas (CORS, Helmet, Rate Limit)

En esta lección aprenderás a blindar tu servidor Express contra vulnerabilidades web comunes configurando **CORS**, encabezados de seguridad con **Helmet** y limitación de tasa de peticiones con **Express-Rate-Limit**.

---

## 1. Módulos de Seguridad Esenciales

1. **`cors`**: Controla qué dominios frontend (orígenes) están autorizados para consumir tu API REST.
2. **`helmet`**: Configura automáticamente encabezados HTTP de seguridad para proteger la app contra vulnerabilidades como XSS, Clickjacking y MIME-sniffing.
3. **`express-rate-limit`**: Previene ataques de fuerza bruta y denegación de servicio (DoS) limitando la cantidad de peticiones que un mismo IP puede realizar en un intervalo de tiempo.

---

## 2. Configuración en un Servidor Express

```javascript
import express from 'express';
import cors from 'cors';
import helmet from 'helmet';
import rateLimit from 'express-rate-limit';

const app = express();

// 1. Helmet para encabezados HTTP seguros
app.use(helmet());

// 2. CORS restringido a tu dominio frontend
app.use(cors({
  origin: ['http://localhost:5173', 'https://midominio.com'],
  methods: ['GET', 'POST', 'PUT', 'DELETE'],
  credentials: true
}));

// 3. Limitador de Peticiones (Rate Limit)
const authLimiter = rateLimit({
  windowMs: 15 * 60 * 1000, // Ventana de 15 minutos
  max: 5, // Máximo 5 peticiones por IP por ventana
  message: { error: 'Demasiados intentos de inicio de sesión. Intenta de nuevo en 15 minutos.' }
});

app.use(express.json());

// Aplicar rate limit únicamente en rutas sensibles como Login
app.post('/api/auth/login', authLimiter, (req, res) => {
  res.json({ mensaje: 'Intento de login procesado' });
});
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué vulnerabilidad ayuda a mitigar la librería `express-rate-limit`?
> - [ ] Inyección de código SQL.
> - [x] Ataques de fuerza bruta en contraseñas y sobrecarga por denegación de servicio (DoS).
> - [ ] Errores de sintaxis en el archivo package.json.
>
> **Explicación**: Al bloquear las IP que exceden un umbral razonable de peticiones en un lapso de tiempo, `express-rate-limit` impide que scripts automatizados intenten adivinar contraseñas infinitamente.

---

## Ejercicio Práctico

Configura el paquete `cors` para permitir peticiones únicamente desde el origen `http://localhost:3000`.
