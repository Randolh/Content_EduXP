# Lección 2: Crear tu primera app React con Vite

En esta lección aprenderás **exclusivamente a inicializar un proyecto con Vite** desde la terminal.

---

## 1. Crear el Proyecto con Vite

1. Abre tu terminal e ingresa el siguiente comando:
   ```bash
   npx create-vite mi-app --template react
   ```
2. Entra a la carpeta recién creada:
   ```bash
   cd mi-app
   ```
3. Instala las librerías necesarias:
   ```bash
   npm install
   ```
4. Inicia el servidor de desarrollo local:
   ```bash
   npm run dev
   ```

Abre el enlace impreso en la terminal (ejemplo: `http://localhost:5173`) en tu navegador para ver la página de bienvenida de React.

---

## Autoevaluación

> [!QUIZ]
> ¿Qué comando inicia el servidor de desarrollo local de Vite para ver tu app en el navegador?
> - [ ] `npm start react`
> - [x] `npm run dev`
> - [ ] `node main.js`
>
> **Explicación**: `npm run dev` arranca el servidor ultrarrápido de desarrollo de Vite.

---

## Ejercicio Práctico

Crea un proyecto llamado `mi-primer-react` con `npx create-vite mi-primer-react --template react`, instala sus dependencias con `npm install` y ejecútalo con `npm run dev`.
