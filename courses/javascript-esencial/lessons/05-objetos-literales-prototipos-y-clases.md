# 5. Objetos Literales, Optional Chaining y Clases ES6+

En JavaScript, los objetos son estructuras dinamicas clave-valor respaldadas por un sistema de herencia prototipica. A partir de ES6 y revisiones subsiguientes (ES2022+), el lenguaje formalizo la sintaxis de clases con caracteristicas avanzadas como **campos privados nativos (`#`)**.

---

## Objetivos de la Leccion
- Manipular objetos literales, metodos concisos y propiedades calculadas.
- Comprender la cadena de prototipos (`[[Prototype]]` / `__proto__`).
- Definir clases orientadas a objetos con constructores y metodos estaticos.
- Proteger el estado interno mediante campos privados (`#`) estandarizados en ES2022.

---

## Objetos Literales y Sintaxis Mejorada

```javascript
const prefijoAmbiente = "entorno";

const servidorConfig = {
    nombre: "Worker-Node-01",
    // Propiedad con nombre computado dinamicamente
    [`${prefijoAmbiente}_actual`]: "produccion",
    
    // Metodo conciso
    describir() {
        return `Host: ${this.nombre} (${this.entorno_actual})`;
    }
};

console.log(servidorConfig.describir());
```

---

## Clases ES6 y Enlace Prototipico

La declaracion `class` en JavaScript es una abstraccion sintactica construida sobre la herencia prototipica nativa, proporcionando una interfaz limpia y estructurada:

```javascript
class DispositivoRed {
    constructor(direccionMAC, fabricante) {
        this.direccionMAC = direccionMAC;
        this.fabricante = fabricante;
        this.conectado = false;
    }

    establecerConexion() {
        this.conectado = true;
        console.log(`Dispositivo [${this.direccionMAC}] conectado a la red.`);
    }

    // Metodo estatico (pertenece a la clase, no a las instancias)
    static validarMAC(mac) {
        const regexMAC = /^([0-9A-Fa-f]{2}[:-]){5}([0-9A-Fa-f]{2})$/;
        return regexMAC.test(mac);
    }
}
```

---

## Campos y Metodos Privados con `#` (ES2022+)

Con anterioridad a ES2022, la comunidad recurria a convenciones informales con guion bajo (`_saldo`) o closures para simular privacidad.  
El estandar ECMAScript actual provee aislamiento estricto de bajo nivel mediante el prefijo `#`:

```javascript
class CuentaSegura {
    // Declaracion obligatoria de campos privados con #
    #balance = 0;
    #claveSecreta;

    constructor(titular, depositoInicial, clave) {
        this.titular = titular;
        this.#balance = depositoInicial;
        this.#claveSecreta = clave;
    }

    // Metodo publico de interaccion
    debitar(monto, claveEntrada) {
        if (claveEntrada !== this.#claveSecreta) {
            throw new Error("Violacion de seguridad: Credencial invalida.");
        }
        if (monto > this.#balance) {
            throw new Error("Operacion declinada: Fondos insuficientes.");
        }
        this.#balance -= monto;
        return this.#balance;
    }

    // Getter controlado
    get saldoDisponible() {
        return this.#balance;
    }
}

const miCuenta = new CuentaSegura("Esteban Morales", 5000, "pin_9921");
console.log(miCuenta.saldoDisponible); // 5000
// miCuenta.#balance = 0; // SyntaxError: Private field '#balance' must be declared in an enclosing class
```

---

## Herencia con `extends` y `super()`

```javascript
class SwitchEthernet extends DispositivoRed {
    constructor(direccionMAC, fabricante, cantidadPuertos) {
        super(direccionMAC, fabricante); // Invocacion obligatoria al constructor padre
        this.cantidadPuertos = cantidadPuertos;
    }

    establecerConexion() {
        super.establecerConexion(); // Ejecucion de logica base
        console.log(`Puertos activos: ${this.cantidadPuertos}`);
    }
}
```

---

## Ejercicio Practico

Crea una clase llamada `ManejadorSesion` con un campo privado `#tokenAcceso` y un campo publico `usuario`.
1. El constructor debe inicializar ambos datos.
2. Implementa un metodo `validarToken(tokenComparar)` que retorne un booleano sin exponer el valor de `#tokenAcceso`.
3. Comprueba que el campo privado no pueda ser leido ni sobreescrito desde el exterior.
