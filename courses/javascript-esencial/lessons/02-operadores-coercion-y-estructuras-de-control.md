# 2. Operadores Estrictos, Coercion, Nullish Coalescing y Control de Flujo

La conversion automatica de tipos (coercion) en JavaScript es una fuente comun de comportamientos imprevistos si no se gestiona con disciplina tecnica. En esta leccion aprenderas a escribir evaluaciones estrictas y a utilizar los operadores contemporaneos `??` y `?.`.

---

## Objetivos de la Leccion
- Comprender la diferencia fundamental entre igualdad debil (`==`) e igualdad estricta (`===`).
- Identificar los seis valores catalogados como falsy en la norma ECMAScript.
- Utilizar el operador de fusion nula (`??`) frente al operador OR logico (`||`).
- Aplicar encadenamiento opcional (`?.`) para navegar estructuras de objetos profundas con seguridad.

---

## Comparacion Debil (`==`) vs Comparacion Estricta (`===`)

- **`==` (Igualdad Coercitiva):** Fuerza a ambos operandos a convertirse a un tipo comun antes de comparar. Produce resultados contra-intuitivos:
  ```javascript
  console.log(0 == false);        // true
  console.log("" == false);       // true
  console.log("   " == 0);        // true
  console.log(null == undefined); // true
  ```
- **`===` (Igualdad Estricta):** Compara tanto el tipo de dato como el contenido sin aplicar transformaciones:
  ```javascript
  console.log(0 === false);        // false (number !== boolean)
  console.log("" === false);       // false (string !== boolean)
  console.log(null === undefined); // false (object !== undefined)
  ```

> [!WARNING]
> **Estandar de Ingenieria:**  
> Utiliza de forma exclusiva `===` y `!==`. El uso de `==` introduce vulnerabilidades logicas en sistemas comerciales.

---

## Valores Falsy en JavaScript

Al evaluar una condicion booleana, cualquier expresion se evalua como verdad (truthy) o falsedad (falsy). Unicamente existen **6 valores Falsy primitivos**:
1. `false`
2. `0`, `-0`, `0n`
3. `""` (cadena de longitud cero)
4. `null`
5. `undefined`
6. `NaN` (Not-a-Number)

Cualquier otro elemento, incluyendo arreglos vacios `[]` u objetos vacios `{}`, evalua siempre a **Truthy**.

---

## El Operador Nullish Coalescing (`??`)

El operador tradicional OR (`||`) devuelve el operando derecho si el izquierdo es cualquier valor falsy. Esto causa fallas si el valor valido deseado es el numero `0` o una cadena vacia:

```javascript
const configuracionUsuario = {
    volumenAudio: 0,
    tiempoEspera: null
};

// Problema con OR logico (||):
const volumen1 = configuracionUsuario.volumenAudio || 50; 
console.log(volumen1); // 50 (Invalido: sobreescribio el 0 deseado)

// Solucion con Nullish Coalescing (??):
// Solo evalua la derecha si la izquierda es estrictamente null o undefined
const volumen2 = configuracionUsuario.volumenAudio ?? 50;
console.log(volumen2); // 0 (Correcto: respeto el valor cero)

const espera = configuracionUsuario.tiempoEspera ?? 3000;
console.log(espera);   // 3000 (Correcto: reemplazo null)
```

---

## Encadenamiento Opcional (`?.`)

Evita excepciones fatales de tipo `TypeError: Cannot read properties of undefined` al consultar propiedades en objetos complejos devueltos por APIs externas:

```javascript
const respuestaServicio = {
    codigo: 200,
    payload: {
        usuario: {
            id: 994,
            perfil: {
                correo: "admin@eduxp.org"
            }
        }
    }
};

// Sin encadenamiento opcional, si 'perfil' no existiera, el codigo fallaria fatalmente:
const correo = respuestaServicio?.payload?.usuario?.perfil?.correo ?? "sin_correo@dominio.com";
console.log(correo);

// Invocacion opcional de metodos:
const resultadoMetodo = respuestaServicio.procesarDatos?.(); // Retorna undefined sin arrojar excepcion
```

---

## Ejercicio Practico

Escribe una funcion llamada `obtenerPuertoServidor(config)` que reciba un objeto de configuracion.  
- Debe extraer la propiedad anidada `config.server.network.port`.  
- Si no esta definida o es `null`, debe asignar por defecto `8080`.  
- Si el objeto de configuracion recibido es `null` o `undefined`, debe retornar `8080` sin generar errores en consola.
