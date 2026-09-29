# 3. Funciones, Arrow Functions, Parametros Rest y Closures

En JavaScript, las funciones son **ciudadanos de primera clase** (*First-Class Citizens*): pueden asignarse a variables, pasarse como argumentos a otras funciones (callbacks) y retornarse desde funciones. En esta leccion exploraras el enlace de contexto de las Arrow Functions y el concepto de **Closures**.

---

## Objetivos de la Leccion
- Diferenciar entre funciones declarativas tradicionales y funciones expresadas.
- Dominar la sintaxis y el enlace lexico del identificador `this` en Arrow Functions.
- Utilizar el operador Rest (`...`) y parametros con valores predeterminados.
- Comprender la clausura lexica (Closure) y su uso en encapsulamiento y estado privado.

---

## Declaracion vs Expresion de Funciones

```javascript
// 1. Declaracion de Funcion (Sujeta a Hoisting en su ambito)
function calcularImpuesto(monto, tasa = 0.16) {
    return monto * tasa;
}

// 2. Expresion de Funcion (Asignada a una constante, no sufre Hoisting ambiguo)
const calcularDescuento = function(monto, porcentaje) {
    return monto * (porcentaje / 100);
};
```

---

## Arrow Functions (Funciones Flecha)

Introducidas en ES6, las Arrow Functions simplifican la escritura de funciones anonimas y de orden superior:

```javascript
// Sintaxis estandar con bloque
const multiplicar = (a, b) => {
    return a * b;
};

// Retorno implicito de una sola expresion
const duplicar = valor => valor * 2;

// Retorno de un objeto literal (requiere envolver entre parentesis para no confundir con bloque)
const crearPuntoCartesiano = (x, y) => ({ ejeX: x, ejeY: y });
```

### Enlace Lexico de `this`
A diferencia de las funciones tradicionales declaradas con `function` que redefinen su propio `this` segun la forma de invocacion, las Arrow Functions **no poseen su propio contexto `this`**: heredan el `this` del ambito donde fueron declaradas (Lexical Scoping).

---

## Parametros Rest y Parametros por Defecto

El operador Rest (`...`) condensa multiples argumentos individuales en un arreglo formal:

```javascript
const registrarTransacciones = (codigoCliente, ...montos) => {
    console.log(`Cliente: ${codigoCliente}`);
    console.log(`Total de operaciones recibidas: ${montos.length}`);
    const balanceTotal = montos.reduce((acc, curr) => acc + curr, 0);
    return balanceTotal;
};

const total = registrarTransacciones("CLI-4401", 120.5, 45.0, 310.0, 99.9);
console.log(`Balance resultante: $${total}`);
```

---

## Clausuras Lexicas (Closures)

Un **Closure** es la combinacion de una funcion y el entorno lexico en el cual dicha funcion fue declarada. Permite que una funcion interna mantenga acceso permanente a las variables de su funcion externa contenedora, incluso despues de que la funcion externa haya finalizado su ejecucion y salido de la pila de llamadas.

```javascript
function crearGeneradorIds(prefijoModulo) {
    let consecutivo = 0; // Variable privada protegida en el closure

    return {
        siguiente: () => {
            consecutivo += 1;
            return `${prefijoModulo}-${consecutivo.toString().padStart(4, "0")}`;
        },
        consultarActual: () => consecutivo,
        reiniciar: () => {
            consecutivo = 0;
        }
    };
}

const generadorFacturas = crearGeneradorIds("FAC");

console.log(generadorFacturas.siguiente()); // "FAC-0001"
console.log(generadorFacturas.siguiente()); // "FAC-0002"
console.log(generadorFacturas.siguiente()); // "FAC-0003"
// La variable 'consecutivo' es totalmente inaccesible desde el ambito exterior
```

> [!NOTE]
> Los Closures son la base tecnologica del encapsulamiento modular en JavaScript y explican el funcionamiento interno de los Hooks en frameworks como React (`useState`).

---

## Ejercicio Practico

Escribe una funcion constructora mediante Closures llamada `crearLimitadorTasa(limiteMaximo)`:
- Debe mantener un contador interno de peticiones permitidas.
- Debe retornar una funcion `ejecutar(accion)`.
- Si las ejecuciones acumuladas superan `limiteMaximo`, debe rechazar la llamada imprimiendo `"Tasa de solicitudes excedida"`; de lo contrario, debe invocar la funcion `accion` y registrar el incremento.
