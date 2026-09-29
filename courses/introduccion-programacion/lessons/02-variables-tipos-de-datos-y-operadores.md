# 2. Gestion de Memoria, Tipos de Datos y Operadores

Todo programa en ejecucion requiere almacenar y manipular informacion en la memoria volatil (RAM). Para gestionar estos datos con seguridad y eficiencia, los lenguajes de programacion establecen el concepto de variables, constantes y clasificaciones de tipos de datos.

---

## Objetivos de la Leccion
- Comprender como se representan las variables y constantes en la memoria del computador.
- Clasificar los tipos de datos primitivos universales: enteros, flotantes, cadenas y booleanos.
- Aplicar operadores aritmeticos, de asignacion, relacionales y logicos respetando su precedencia.
- Evitar conversiones de tipo implicitas que provoquen perdidas de precision.

---

## Variables y Constantes en Memoria

Una **variable** es un espacio reservado en la memoria RAM identificado por un nombre simbolico (identificador) que almacena un valor susceptible de modificarse durante la ejecucion del programa.

Una **constante**, por el contrario, representa un valor inmutable asignado en tiempo de definicion que permanece inalterable a lo largo de todo el ciclo de vida del proceso.

```text
Memoria RAM Fisica:
Direccion Hexadecimal | Identificador | Tipo de Dato | Valor Asignado
0x00A1F020            | tasaIVA       | Constante    | 0.16
0x00A1F028            | stockActual   | Variable     | 145
0x00A1F030            | nombreCliente | Variable     | "Marta Lopez"
```

### Reglas de Nomenclatura Profesional
- Utilizar nombres semanticamente claros y representativos de la entidad almacenada.
- Evitar identificadores genericos de una sola letra como `x`, `tmp`, `a`.
- Adherirse a convenciones estandares de la industria como `camelCase` (`saldoDisponible`) o `snake_case` (`saldo_disponible`).

---

## Tipos de Datos Primitivos

| Categoria | Denominacion Tecnica | Espacio Tipico | Rango o Dominio de Valores |
| :--- | :--- | :--- | :--- |
| **Entero** | `Integer` / `int` | 32 o 64 bits | Numeros sin parte decimal (`-2147483648` a `2147483647`). |
| **Flotante / Decimal** | `Float` / `Double` | 32 o 64 bits | Numeros reales con precision fraccional (`3.141592`, `-0.005`). |
| **Cadena de Texto** | `String` | Variable | Secuencia contigua de caracteres alfanumericos (`"Codigo Fuente"`). |
| **Caracter Unico** | `Char` | 8 o 16 bits | Un solo simbolo Unicode/ASCII (`'A'`, `'#'`, `'9'`). |
| **Booleano** | `Boolean` / `bool` | 1 byte / 1 bit | Valor de logica binaria: `Verdadero` (`true`) o `Falso` (`false`). |

> [!WARNING]
> **Incompatibilidad de Tipos:**  
> Un error recurrente en principiantes es confundir el valor numerico `50` con la representacion textual `"50"`. Si intentas sumar `"50" + "50"` en lenguajes como JavaScript o Python obtendras `"5050"` (concatenacion) en vez de `100` (adicion aritmetica).

---

## Precedencia y Jerarquia de Operadores

Al evaluar expresiones complejas, el motor de ejecucion aplica un orden estricto de evaluacion denominado **precedencia de operadores**:

```text
Mayor Prioridad:
1. Parentesis: ( ... )
2. Potenciacion y Radicacion: ^, **
3. Multiplicacion, Division y Modulo: *, /, %
4. Suma y Resta: +, -
5. Comparaciones Relacionales: >, <, >=, <=, ==, !=
6. Operadores Logicos: NO (NOT), Y (AND), O (OR)
Menor Prioridad
```

### Operadores Aritmeticos y de Resto
```text
Suma:             total = subtotal + envio
Resta:            ganancia = ingreso - costo
Multiplicacion:   area = base * altura
Division Real:    promedio = sumaTotal / cantidadElementos
Modulo (Resto):   residuo = dividendo % divisor
```

El operador de modulo (`%` o `mod`) retorna el residuo exacto de una division entera. Es esencial para determinar si un numero es par (`numero % 2 == 0`) o para calcular ciclos repetitivos.

---

## Operadores Relacionales y Tablas de Verdad

Los operadores de comparacion devuelven obligatoriamente un resultado de tipo booleano:

```text
Igualdad:         x == y   (Verdadero si x e y tienen el mismo valor)
Desigualdad:      x != y   (Verdadero si x e y difieren)
Mayor / Menor:    x > y, x < y
Mayor o Igual:    x >= y
```

### Combinacion con Operadores Logicos
- **Conjuncion (Y / AND):** Requiere que **ambas** premisas sean verdaderas.
- **Disyuncion (O / OR):** Requiere que **al menos una** de las premisas sea verdadera.
- **Negacion (NO / NOT):** Invierte el estado logico actual.

```text
Premisa A | Premisa B | (A Y B) | (A O B) | NO(A)
-------------------------------------------------
V         | V         | V       | V       | F
V         | F         | F       | V       | F
F         | V         | F       | V       | V
F         | F         | F       | F       | V
```

---

## Ejercicio Practico de Evaluacion

Evalua formalmente el resultado booleano (`Verdadero` o `Falso`) de la siguiente expresion:

```text
a = 15
b = 20
c = 5
resultado = ((a * 2) > b) Y ((b % c == 0) O (a + c == 18))
```
Escribe el desglose paso a paso de cada operacion elemental antes de emitir el veredicto final.
