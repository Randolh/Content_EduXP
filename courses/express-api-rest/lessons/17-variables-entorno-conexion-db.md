# Lección 17: Variables de Entorno y Conexión a Base de Datos (dotenv)

En esta lección aprenderás a gestionar configuraciones sensibles (cadenas de conexión a base de datos, claves secretas, puertos) de forma segura mediante **Variables de Entorno** y el paquete **dotenv**.

---

## 1. El Archivo `.env` y `.gitignore`

Nunca debes incluir claves privadas, tokens o passwords de base de datos en tu código fuente subido a repositorios como GitHub.

Crea un archivo `.env` en la raíz de tu proyecto:

```env
PORT=4000
NODE_ENV=development
JWT_SECRET=super_secreto_clave_99
DATABASE_URL=mongodb+srv://usuario:password@cluster.mongodb.net/eduxp_db
```

Asegúrate de agregar `.env` dentro de tu archivo `.gitignore`:

```text
node_modules/
.env
```

---

## 2. Carga de Variables con `dotenv`

Instalamos con `npm install dotenv`.

```javascript
import 'dotenv/config'; // Carga automáticamente las variables del archivo .env a process.env
import express from 'express';

const app = express();

const PORT = process.env.PORT || 3000;
const DB_URL = process.env.DATABASE_URL;

console.log('Modo de ejecución:', process.env.NODE_ENV);
console.log('Conectando a la base de datos en:', DB_URL);

app.get('/api/health', (req, res) => {
  res.json({ status: 'ok', environment: process.env.NODE_ENV });
});

app.listen(PORT, () => console.log(`Servidor iniciado en puerto ${PORT}`));
```

---

## Autoevaluación

> [!QUIZ]
> ¿Por qué debe agregarse el archivo `.env` al archivo `.gitignore`?
> - [ ] Porque Node.js no puede leer archivos ignorados por Git.
> - [x] Para evitar que las claves secretas y credenciales de base de datos sean publicadas por accidente en repositorios de código públicos.
> - [ ] Para hacer que el servidor inicie más rápido.
>
> **Explicación**: El archivo `.env` contiene información confidencial. Ignorarlo en Git asegura que cada entorno (desarrollo, pruebas, producción) mantenga sus propias credenciales de forma aislada e inalcanzable para terceros.

---

## Ejercicio Práctico

Crea una variable de entorno `API_KEY=12345` en tu `.env` y léela en un endpoint `/api/config` usando `process.env.API_KEY`.
