# Lección 7: Variables de Entorno y Configuración (dotenv)

En esta lección final aprenderás **qué son las variables de entorno** y cómo guardar datos sensibles como contraseñas en archivos `.env`.

---

## 1. Archivo `.env` y el paquete `dotenv`

Nunca debes colocar contraseñas o claves secretas escritas directamente en tu código fuente. En su lugar, se guardan en un archivo oculto llamado `.env`:

### 1. Crear el archivo `.env`:
```text
PUERTO=3000
CLAVE_SECRETA=mi_super_secreto_123
```

### 2. Acceder desde Node.js (`process.env`):
```javascript
import 'dotenv/config';

console.log("El puerto configurado es:", process.env.PUERTO);
```

---

## Autoevaluación

> [!QUIZ]
> ¿En qué objeto global de Node.js se almacenan las variables de entorno cargadas?
> - [ ] `window.env`
> - [x] `process.env`
> - [ ] `global.variables`
>
> **Explicación**: `process.env` contiene todas las variables de entorno activas en el proceso actual de Node.js.

---

## Ejercicio Práctico Final

Instala la librería dotenv ejecutando `npm install dotenv`, crea un archivo `.env` con la variable `NOMBRE_APP="EduXP CLI"` e imprímela por pantalla importando `dotenv/config`.
