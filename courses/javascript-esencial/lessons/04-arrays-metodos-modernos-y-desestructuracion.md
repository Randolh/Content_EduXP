# 4. Metodos Modernos de Arrays (map, filter, reduce) y Destructuring

La manipulacion de colecciones en JavaScript contemporaneo se orienta hacia el paradigma funcional inmutable. En esta leccion exploraras metodos de orden superior (`map`, `filter`, `reduce`), desestructuracion y las funciones inmutables de ES2023+.

---

## Objetivos de la Leccion
- Aplicar desestructuracion (Destructuring) y operador Spread en colecciones y objetos.
- Dominar los metodos funcionales iterativos: `map`, `filter`, `reduce`, `find`, `some`, `every`.
- Utilizar metodos inmutables recientes estandarizados en ES2023+: `toSorted()`, `toReversed()`, `toSpliced()`, `with()`.
- Evitar mutaciones accidentales en estructuras compartidas en memoria.

---

## Desestructuracion (Destructuring) y Operador Spread

```javascript
// 1. Destructuring de Arreglos
const coordenadasGPS = [19.4326, -99.1332, 2240];
const [latitud, longitud, altitud = 0] = coordenadasGPS;

// 2. Destructuring de Objetos y renombrado
const servicioConfig = { host: "10.0.0.1", port: 5432, timeout: 5000 };
const { host, port: puertoConexion } = servicioConfig;

// 3. Operador Spread (...) para clonacion inmutable superficial (Shallow Copy)
const listaOriginal = [1, 2, 3];
const listaExtendida = [...listaOriginal, 4, 5];
```

---

## Metodos Funcionales: `map`, `filter` y `reduce`

### 1. `map()`: Mapeo Proporcional 1 a 1
Genera un nuevo arreglo del mismo tamano aplicando una transformacion pura sobre cada elemento:
```javascript
const productos = [
    { id: "P1", nombre: "Monitor 27", precio: 300 },
    { id: "P2", nombre: "Teclado Mecanico", precio: 80 },
    { id: "P3", nombre: "Mouse Optico", precio: 35 }
];

const nombresMayusculas = productos.map(item => item.nombre.toUpperCase());
```

### 2. `filter()`: Seleccion por Criterio Booleano
Retorna un nuevo arreglo compuesto unicamente por los elementos que satisfacen el predicado:
```javascript
const articulosPremium = productos.filter(item => item.precio >= 80);
```

### 3. `reduce()`: Acumulacion Dimensional a un Unico Valor
Permite condensar un arreglo en cualquier entidad de salida (un numero, un objeto estructurado, o un mapa agrupador):
```javascript
const valorTotalInventario = productos.reduce((acumulador, item) => {
    return acumulador + item.precio;
}, 0); // 0 es el acumulador inicial

console.log(`Valoracion total: $${valorTotalInventario}`); // $415
```

---

## Metodos Inmutables de ES2023+ (`toSorted`, `toReversed`, `with`)

Historicamente, invocar `.sort()` o `.reverse()` sobre un arreglo mutaba el arreglo original en memoria, generando efectos secundarios peligrosos en aplicaciones concurrentes.  
El estandar ES2023 introdujo sus contrapartes inmutables oficiales:

```javascript
const metricas = [45, 12, 89, 3, 27];

// toSorted(): Retorna una nueva copia ordenada sin mutar la original
const ordenadas = metricas.toSorted((a, b) => a - b);
console.log(metricas);   // [45, 12, 89, 3, 27] (Intacto)
console.log(ordenadas);  // [3, 12, 27, 45, 89]

// toReversed(): Retorna una nueva copia invertida
const invertidas = metricas.toReversed();

// with(indice, nuevoValor): Retorna una copia sustituyendo el indice indicado
const actualizadas = metricas.with(0, 999);
console.log(actualizadas); // [999, 12, 89, 3, 27]
```

---

## Ejercicio Practico

Dado el siguiente conjunto de transacciones:
```javascript
const registros = [
    { categoria: "servidores", costo: 1500, region: "us-east" },
    { categoria: "almacenamiento", costo: 400, region: "eu-west" },
    { categoria: "servidores", costo: 2300, region: "eu-west" },
    { categoria: "redes", costo: 600, region: "us-east" }
];
```
Utiliza `reduce()` para generar un objeto consolidado que totalice el gasto agrupado por `categoria`:  
`{ servidores: 3800, almacenamiento: 400, redes: 600 }`.
