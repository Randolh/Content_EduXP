# Lección 2: Instalación de Node.js y tu Primer Script (console.log)

En esta lección aprenderás **exclusivamente a verificar la instalación de Node.js** y ejecutar tu primer script por consola.

---

## 1. Verificación e Instalación

1. Descarga la versión **LTS** desde [nodejs.org](https://nodejs.org).
2. Abre la terminal y comprueba la versión:
   ```bash
   node -v
   ```

---

## 2. Ejecutar tu Primer Script

1. Crea un archivo llamado `app.js`.
2. Escribe una línea de código:
   ```javascript
   console.log("¡Hola desde Node.js!");
   ```
3. Ejecuta el archivo en la terminal escribiendo:
   ```bash
   node app.js
   ```

Verás el mensaje impreso directamente en tu consola.

---

## Autoevaluación

> [!QUIZ]
> ¿Qué comando de consola se usa para ejecutar un archivo de JavaScript llamado `servidor.js` con Node.js?
> - [ ] `run servidor.js`
> - [x] `node servidor.js`
> - [ ] `npm start servidor.js`
>
> **Explicación**: El comando `node <nombre-archivo.js>` inicia el motor V8 y ejecuta el script especificado.

---

## Ejercicio Práctico

Crea un archivo `saludo.js`, escribe `console.log("Mi primer script en Node.js funciona")` y ejecútalo desde tu terminal con `node saludo.js`.
