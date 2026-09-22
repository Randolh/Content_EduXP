# Lección 2: Preparación del Entorno: Instalación de Node.js, NPM y NPX

En esta lección aprenderás **exclusivamente a instalar Node.js** en tu computadora y a comprender las herramientas **NPM** y **NPX** necesarias para ejecutar los creadores de proyectos de React.

---

## 1. ¿Qué son Node.js, NPM y NPX?

Antes de crear una aplicación en React, necesitas entender tres conceptos clave:

* **Node.js:** El entorno que permite ejecutar JavaScript en tu computadora fuera del navegador.
* **NPM (Node Package Manager):** El gestor de librerías que te permite instalar paquetes de código creados por la comunidad.
* **NPX (Node Package Execute):** Una herramienta incluida con NPM que te permite **ejecutar comandos e instaladores temporales** (como `create-vite` o `create-react-app`) sin tener que instalarlos globalmente en tu disco duro.

---

## 2. Instalación de Node.js (Paso a Paso)

1. Visita el sitio web oficial: [nodejs.org](https://nodejs.org).
2. Descarga la versión **LTS (Long Term Support)** recomendada para la mayoría de usuarios.
3. Abre el archivo ejecutable descargado y completa el asistente presionando "Siguiente" con las opciones por defecto.

---

## 3. Verificación en la Terminal

Abre tu consola de comandos (PowerShell, Git Bash o Terminal de macOS/Linux) y verifica que las tres herramientas estén listas ejecutando:

```bash
# 1. Verificar Node.js
node -v

# 2. Verificar NPM
npm -v

# 3. Verificar NPX
npx -v
```

Si los tres comandos responden mostrando un número de versión (por ejemplo `v18.17.0` o superior), ¡tu entorno está 100% preparado!

---

## Autoevaluación

> [!QUIZ]
> ¿Cuál es la diferencia principal entre el comando `npm` y el comando `npx`?
> - [ ] `npm` es para Mac y `npx` es para Windows.
> - [x] `npm` sirve para instalar y gestionar paquetes permanentemente, mientras que `npx` permite ejecutar instaladores o scripts temporales sin instalarlos globalmente.
> - [ ] `npx` borra todos los archivos de tu proyecto.
>
> **Explicación**: `npx` descarga y ejecuta herramientas de inicialización al instante sin llenar tu disco duro de paquetes globales antiguos.

---

## Ejercicio Práctico

Abre la terminal de tu computadora y ejecuta los tres comandos de verificación (`node -v`, `npm -v`, `npx -v`). Toma nota de las versiones instaladas en tu equipo.
