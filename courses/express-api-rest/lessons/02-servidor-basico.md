# Lección 2: Instalación de Express y tu primer Servidor HTTP

En esta lección aprenderás **exclusivamente a instalar Express** en tu proyecto y poner a escuchar tu primer servidor en el puerto 3000.

---

## 1. Instalación y Código del Servidor

1. En una carpeta nueva, inicializa el proyecto:
   ```bash
   npm init -y
   npm install express
   ```

2. Crea el archivo `server.js`:
   ```javascript
   import express from 'express';

   const app = express();
   const PORT = 3000;

   // Ruta principal de bienvenida
   app.get('/', (req, res) => {
     res.send('¡Hola! Servidor Express en funcionamiento.');
   });

   // Iniciar el servidor
   app.listen(PORT, () => {
     console.log(`Servidor listo en http://localhost:${PORT}`);
   });
   ```

3. Ejecuta el servidor en la consola:
   ```bash
   node server.js
   ```

Abre tu navegador en `http://localhost:3000` para ver el mensaje.

---

## Autoevaluación

> [!QUIZ]
> ¿Qué método de Express se utiliza para poner al servidor a escuchar peticiones en un puerto determinado?
> - [ ] `app.start()`
> - [x] `app.listen()`
> - [ ] `app.run()`
>
> **Explicación**: `app.listen(PUERTO)` vincula el servidor al puerto de red especificado.

---

## Ejercicio Práctico

Crea un servidor en `server.js` que escuche en el puerto `4000` y responda `"Mi primera API REST"` al acceder a la raíz `/`.
