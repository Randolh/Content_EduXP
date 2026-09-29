# 6. Asincronia, Event Loop, Promesas y Async/Await

JavaScript es un lenguaje de **hilo unico** (*Single-Threaded*). Para ejecutar tareas bloqueantes y costosas de entrada/salida (como consultas de red o acceso a disco) sin congelar la interfaz de usuario o el servidor, el entorno utiliza una arquitectura asincrona no bloqueante coordinada por el **Event Loop**.

---

## Objetivos de la Leccion
- Comprender el ciclo de operacion del Event Loop, Microtask Queue y Macrotask Queue.
- Conocer la anatomia de una Promesa (`Promise`) y sus tres estados formales.
- Utilizar la sintaxis `async` / `await` con captura de errores mediante `try` / `catch`.
- Ejecutar concurrencia estructurada mediante `Promise.all()` y `Promise.allSettled()`.

---

## La Arquitectura del Event Loop

El motor V8 ejecuta las instrucciones sincronas directamente en el Call Stack. Cuando encuentra una operacion asincrona (como `fetch` o `setTimeout`), la delega a las APIs del entorno (navegador o Node.js) y continua inmediatamente con la siguiente instruccion.

Al concluir la tarea en segundo plano, su callback se encola en:
1. **Microtask Queue:** Promesas (`.then`, `await`), `queueMicrotask()`. Poseen prioridad absoluta de ejecucion.
2. **Macrotask Queue:** `setTimeout()`, `setInterval()`, eventos I/O.

```text
Flujo del Event Loop:
[ Call Stack ] (Se vacia la ejecucion sincrona)
      ▲
      │ (El Event Loop transfiere funciones si el stack esta vacio)
[ Microtask Queue ] (Prioridad 1: Promesas / Await)
[ Macrotask Queue ] (Prioridad 2: Timers / IO)
```

---

## El Objeto `Promise`

Una Promesa es un objeto formal que representa la terminacion o fracaso eventual de una operacion asincrona:
- **Pending (Pendiente):** Estado inicial no resuelto.
- **Fulfilled (Cumplida):** La operacion finalizo exitosamente (`resolve()`).
- **Rejected (Rechazada):** La operacion fallo con un error (`reject()`).

```javascript
const consultarServicio = (endpoint) => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            const exito = true;
            if (exito) {
                resolve({ codigo: 200, datos: "Respuesta de " + endpoint });
            } else {
                reject(new Error("Fallo de conexion de red."));
            }
        }, 1000);
    });
};
```

---

## Sintaxis Moderna: `async` / `await`

La combinacion de `async` y `await` (ES2017) transforma el codigo asincrono en una estructura legible y secuencial, eliminando la necesidad de encadenamientos extensos de `.then()`:

```javascript
async function procesarDatosRemotos() {
    try {
        console.log("Iniciando solicitud asincrona...");
        
        // Peticion HTTP utilizando fetch nativo
        const respuesta = await fetch("https://jsonplaceholder.typicode.com/posts/1");
        
        if (!respuesta.ok) {
            throw new Error(`Error en respuesta HTTP: Estado ${respuesta.status}`);
        }

        const datosJSON = await respuesta.json();
        console.log("Datos obtenidos:", datosJSON.title);

    } catch (error) {
        console.error("Fallo durante el procesamiento asincrono:", error.message);
    } finally {
        console.log("Pipeline asincrono finalizado.");
    }
}

procesarDatosRemotos();
```

---

## Concurrencia con `Promise.all` y `Promise.allSettled`

Cuando requieres consultar multiples servicios independientes, encadenar llamadas `await` consecutivas introduce latencias acumulativas innecesarias. Para procesarlas en paralelo:

```javascript
async function cargarDashboardAnalitico() {
    try {
        // Ejecucion concurrente paralela de 3 peticiones
        const promesas = [
            fetch("/api/usuarios").then(r => r.json()),
            fetch("/api/ventas").then(r => r.json()),
            fetch("/api/servidores").then(r => r.json())
        ];

        // Promise.all falla inmediatamente si una sola promesa es rechazada
        const [usuarios, ventas, servidores] = await Promise.all(promesas);
        console.log("Dashboard cargado en paralelo.");

    } catch (error) {
        console.error("Fallo critico en una de las fuentes:", error);
    }
}
```

> [!TIP]
> Si deseas que todas las peticiones concluyan sin importar si algunas fallaron, utiliza **`Promise.allSettled()`**, la cual retorna el estado individual de cada operacion (`status: 'fulfilled' | 'rejected'`).

---

## Ejercicio Practico

Escribe una funcion asincrona llamada `ejecutarConReintentos(fnAsincrona, maxReintentos, retardoMs)`:
- Debe intentar ejecutar `fnAsincrona()`.
- Si la funcion falla arrojando un error, debe esperar `retardoMs` y volver a intentar.
- Debe detenerse y retornar el resultado exitoso o arrojar el error final tras agotar `maxReintentos`.
