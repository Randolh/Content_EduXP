# Lección 5: El Gestor de Paquetes NPM y package.json

En esta lección aprenderás **exclusivamente qué es NPM** y cómo inicializar el manifiesto de tu proyecto `package.json`.

---

## 1. ¿Qué es NPM y `package.json`?

**NPM** (Node Package Manager) es la librería de paquetes y dependencias de código abierto más grande del mundo.

Para convertir una carpeta en un proyecto oficial de Node.js, ejecutas:

```bash
npm init -y
```

Esto generará el archivo `package.json`, que guardará la información de tu proyecto y las librerías externas que instales más adelante.

---

## Autoevaluación

> [!QUIZ]
> ¿Qué comando genera automáticamente un archivo `package.json` con configuraciones por defecto?
> - [ ] `node init`
> - [x] `npm init -y`
> - [ ] `npm start`
>
> **Explicación**: El parámetro `-y` responde "sí" automáticamente a todas las preguntas iniciales.

---

## Ejercicio Práctico

En una carpeta nueva, ejecuta `npm init -y` y abre el archivo `package.json` en VS Code para revisar sus campos (`name`, `version`, `scripts`).
