# Lección 3: Probando tu servidor con Clientes HTTP (Thunder Client)

En esta lección aprenderás **exclusivamente a probar tus URLs** usando una herramienta cliente HTTP como la extensión **Thunder Client** para VS Code.

---

## 1. ¿Por qué necesitas un Cliente HTTP?

El navegador web solo puede realizar peticiones sencillas de tipo `GET` escribiendo una URL. Sin embargo, cuando construyes una API REST, necesitas probar el envío de datos con `POST`, `PUT` o `DELETE`.

---

## 2. Instalación de Thunder Client en VS Code

1. Abre la sección de Extensiones en VS Code (`Ctrl + Shift + X`).
2. Busca **Thunder Client** e instálalo.
3. Verás un nuevo icono de rayo ⚡ en la barra lateral izquierda.
4. Presiona **New Request**, escribe `http://localhost:3000/` y haz clic en **Send**.

Recibirás la respuesta en formato de texto o JSON al instante.

---

## Autoevaluación

> [!QUIZ]
> ¿Para qué se utiliza un cliente HTTP como Thunder Client o Postman?
> - [ ] Para compilar el código JavaScript.
> - [x] Para enviar peticiones de prueba (GET, POST, etc.) a tu servidor backend y revisar la respuesta.
> - [ ] Para formatear archivos HTML.
>
> **Explicación**: Los clientes HTTP simulan llamadas desde aplicaciones web o móviles a tus rutas backend.

---

## Ejercicio Práctico

Abre Thunder Client, envía una petición `GET` a `http://localhost:3000/` con tu servidor en ejecución y verifica que el código de estado devuelto sea `200 OK`.
