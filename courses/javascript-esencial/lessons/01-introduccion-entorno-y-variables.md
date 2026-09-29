# 1. Motor V8, Entorno de Ejecucion, let, const y Tipos Primitivos

JavaScript es el lenguaje de programacion que gobierna la Web. Aunque comenzo como un lenguaje de scripting para navegadores, hoy en dia se ejecuta en servidores de alta concurrencia (Node.js, Deno, Bun) y dispositivos diversos gracias a compiladores Just-In-Time (JIT) como el motor V8 de Google.

---

## Objetivos de la Leccion
- Comprender como opera el motor V8 mediante el Call Stack y el Memory Heap.
- Conocer la diferencia entre el ambito de bloque de `let`/`const` y el ambito de funcion de `var`.
- Comprender el fenomeno de la Zona Muerta Temporal (Temporal Dead Zone - TDZ).
- Identificar los siete tipos de datos primitivos inmutables y el tipo Objeto.

---

## Arquitectura del Motor V8

El motor V8 compila el codigo JavaScript directamente a instrucciones de maquina optimizadas en tiempo de ejecucion:
- **Memory Heap:** Espacio de memoria no estructurado donde se almacenan objetos, arreglos y variables complejas.
- **Call Stack (Pila de Llamadas):** Estructura LIFO que registra en que punto del programa nos encontramos y gestiona los contextos de ejecucion.

```text
Entorno de Ejecucion JavaScript:
┌────────────────────────────────────────────────────────┐
│                      Motor V8                          │
│   ┌─────────────────────┐    ┌─────────────────────┐   │
│   │     Memory Heap     │    │   Call Stack (Pila) │   │
│   │ [Objetos / Memoria] │    │  [ Contexto Actual] │   │
│   │                     │    │  [ Contexto Global] │   │
│   └─────────────────────┘    └─────────────────────┘   │
└────────────────────────────────────────────────────────┘
```

---

## Declaracion de Variables: `const`, `let` y Obsolescencia de `var`

En el estandar moderno de ECMAScript se descarta por completo el uso de `var` debido a sus efectos secundarios indeseados (hoisting permisivo y falta de ambito de bloque).

| Criterio | `const` | `let` | `var` (Obsoleto) |
| :--- | :--- | :--- | :--- |
| **Ambito (Scope)** | Bloque `{}` | Bloque `{}` | Funcion o Global |
| **Reasignacion** | No permitida | Permitida | Permitida |
| **Redeclaracion** | No permitida | No permitida | Permitida (Riesgoso) |
| **Hoisting** | Temporal Dead Zone (TDZ) | Temporal Dead Zone (TDZ) | Elevacion inicial con `undefined` |

```javascript
// Demostracion del Ambito de Bloque:
if (true) {
    const configuracion = "Modo_Estricto";
    let contador = 1;
    var fugaVariable = "Visible fuera del bloque";
}

// console.log(configuracion); // ReferenceError: configuracion is not defined
// console.log(contador);      // ReferenceError: contador is not defined
console.log(fugaVariable);     // Imprime el valor (Comportamiento problematico de var)
```

> [!NOTE]
> **Regla de Diseno Profesional:**  
> Declara todas tus variables con `const` por defecto. Si el valor necesita ser reasignado debido al flujo del algoritmo (por ejemplo, un acumulador en un bucle), utiliza `let`. Nunca emplees `var`.

---

## Tipos de Datos Primitivos en JavaScript

JavaScript cuenta con 7 tipos primitivos inmutables:

```javascript
// 1. String (Cadenas en UTF-16)
const usuario = "Valeria Gomez";

// 2. Number (Punto flotante IEEE 754 de 64 bits para enteros y decimales)
const puerto = 8080;
const tasa = 0.05;

// 3. BigInt (Para enteros de precision arbitraria superior a 2^53 - 1)
const idUniversal = 9007199254740995n;

// 4. Boolean (true o false)
const esProduccion = false;

// 5. Undefined (Variable declarada pero sin asignacion explicita)
let respuestaServicio;
console.log(respuestaServicio); // undefined

// 6. Null (Representacion deliberada de ausencia de objeto o valor)
const sesionExpirada = null;

// 7. Symbol (Identificador unico e inmutable para propiedades de objetos)
const clavePrivada = Symbol("id_interno");

// Inspeccion de tipos:
console.log(typeof usuario);        // "string"
console.log(typeof puerto);         // "number"
console.log(typeof idUniversal);    // "bigint"
console.log(typeof sesionExpirada); // "object" (Peculiaridad historica de la norma original)
```

---

## Ejercicio Practico

Abre la consola de Node.js o las herramientas de desarrollador del navegador e implementa:
1. Una constante con un objeto `{ id: 1, nombre: "Laptop" }`. Comprueba que aunque la variable es `const`, sus propiedades internas pueden ser mutadas.
2. Utiliza `Object.freeze()` sobre el objeto anterior y verifica que ocurre al intentar mutar una de sus propiedades en modo estricto (`"use strict";`).
