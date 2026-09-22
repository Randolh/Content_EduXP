# Lección 2: Preparación del Entorno Backend: Node.js, NPM y Clientes HTTP

En esta lección aprenderás **exclusivamente a verificar las herramientas backend** y a configurar clientes para realizar peticiones HTTP de prueba.

---

## 1. Verificación de Node.js y NPM

Para trabajar con Express.js, asegúrate de tener instalado **Node.js (v18+)** en tu computadora.

Abre la terminal y ejecuta:

```bash
# Verificar versión de Node.js
node -v

# Verificar versión del gestor de paquetes NPM
npm -v
```

Si no tienes Node.js, descárgalo e instálalo desde [nodejs.org](https://nodejs.org).

---

## 2. Herramientas para Pruebas HTTP (Thunder Client / Postman)

El navegador web solo puede realizar peticiones sencillas de consulta `GET`. Para enviar datos a tu backend con `POST`, `PUT` o `DELETE`, necesitarás un **Cliente HTTP**:

* **Thunder Client (Extensión de VS Code - Recomendada):** Te permite probar tus APIs directamente en el editor sin instalar programas adicionales.
* **Postman o Insomnia:** Aplicaciones de escritorio para inspeccionar respuestas JSON de servidores.

---

## Autoevaluación

> [!QUIZ]
> ¿Por qué es necesario contar con un cliente HTTP como Thunder Client o Postman para desarrollar APIs backend?
> - [ ] Porque sustituye la necesidad de usar Node.js.
> - [x] Porque el navegador normal solo permite hacer peticiones GET escribiendo la URL, mientras que con un cliente HTTP podemos probar envíos POST, PUT y DELETE con objetos JSON.
> - [ ] Porque compila el código de Express.
>
> **Explicación**: Los clientes HTTP simulan todas las operaciones necesarias para probar endpoints backend.

---

## Ejercicio Práctico

Abre VS Code, instala la extensión **Thunder Client** desde la pestaña de extensiones (`Ctrl + Shift + X`) y haz clic en el icono del rayo ⚡ para comprobar que la herramienta de pruebas esté activa.
