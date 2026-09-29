# 5. Funciones, Parametros, Retorno y Ambito de Variables

A medida que un sistema de software escala superando miles de lineas de codigo, escribir secuencias monoliticas continuas genera deudas tecnicas inmanejables. La solucion universal es la **modularizacion funcional**, regida por el principio de diseno **DRY (Don't Repeat Yourself)**.

---

## Objetivos de la Leccion
- Comprender la arquitectura de subrutinas, procedimientos y funciones.
- Diferenciar con precision entre parametros formales y argumentos reales.
- Dominar el flujo de control mediante la sentencia de retorno (`Retornar / Return`).
- Analizar el ciclo de vida y alcance de variables (Scope Local vs Scope Global).
- Comprender el modelo de pila de llamadas (Call Stack).

---

## Concepto de Funcion

Una **Funcion** es un modulo autonomo de codigo disenado para ejecutar una tarea delimitada y coherente. Posee una firma o interfaz formal de comunicacion compuesta por:
- Un **Nombre Identificador** representativo de la accion efectuada.
- Una **Lista de Parametros** que actuan como entradas de datos.
- Un **Tipo de Retorno** que especifica el dato resultante que devuelve al invocador.

```text
                    ┌─────────────────────────────────┐
  Argumentos        │         Funcion Modulo          │       Valor
 ──────────►        │     CalcularInteresCompuesto    │    ──────────►
 (P, r, n, t)       │   Resultado = P * (1 + r/n)^nt  │     Retornado
                    └─────────────────────────────────┘
```

---

## Parametros vs Argumentos

- **Parametros Formales:** Son los identificadores de variables declarados en la cabecera o definicion de la funcion. Actuan como contenedores temporales a la espera de valores.
- **Argumentos Reales:** Son los valores concretos, literales o referencias pasados a la funcion en el punto exacto de la invocacion (Call Site).

```text
// Definicion de la funcion modular
Funcion CalcularDescuentoMayorista(montoVenta, porcentajeDescuento)
    Definir rebaja Como Real
    rebaja = montoVenta * (porcentajeDescuento / 100.0)
    Retornar rebaja
FinFuncion

// Codigo principal
Algoritmo Principal
    Definir totalOriginal, ahorroRealizado Como Real
    totalOriginal = 4500.00
    
    // Llamada con argumentos reales
    ahorroRealizado = CalcularDescuentoMayorista(totalOriginal, 15.0)
    
    Escribir "Monto descontado: $", ahorroRealizado
    Escribir "Total neto a liquidar: $", (totalOriginal - ahorroRealizado)
FinAlgoritmo
```

---

## Ambito de Variables (Scope) y Ciclo de Vida

El **Scope** o ambito delimita la zona del codigo fuente donde una variable es visible, valida y accesible:

| Ambito | Localizacion | Ciclo de Vida en Memoria |
| :--- | :--- | :--- |
| **Local (Stack)** | Declarada dentro de una funcion o bloque especifico. | Nace al entrar a la funcion y es destruida inmediatamente al retornar. |
| **Global** | Declarada en el nivel superior del archivo o modulo. | Permanece cargada en memoria durante toda la ejecucion del proceso. |

> [!WARNING]
> **Riesgo del Estado Global:**  
> El uso indiscriminado de variables globales dificulta el rastreo de errores, rompe el encapsulamiento y causa colisiones de nombres. La regla arquitectonica consiste en pasar datos como parametros y recibir resultados por retorno.

---

## Pila de Llamadas (Call Stack)

Cuando una funcion `FuncionA()` invoca a `FuncionB()`, el procesador pausa la ejecucion de `FuncionA()`, guarda la direccion de retorno y las variables locales en una estructura de pila LIFO (*Last In, First Out*) denominada **Call Stack**, y salta a ejecutar `FuncionB()`. Al concluir `FuncionB()`, la pila se desapila (*Pop*) y `FuncionA()` reanuda su operacion.

```text
[ Call Stack en ejecucion anidada ]
┌──────────────────────────────────────┐
│ Marco 3: CalcularRaizCuadrada()      │  <-- Funcion en ejecucion actual
├──────────────────────────────────────┤
│ Marco 2: CalcularHipotenusa()        │  <-- En espera de retorno
├──────────────────────────────────────┤
│ Marco 1: AlgoritmoPrincipal()        │  <-- En espera de retorno
└──────────────────────────────────────┘
```

---

## Ejercicio Practico

Escribe en pseudocodigo un sistema que contenga tres funciones modulares:
1. `EsPrimo(numero)`: Retorna `Verdadero` si el numero entero recibido es primo y `Falso` si no lo es.
2. `CalcularPotencia(base, exponente)`: Calcula el resultado sin usar operadores especiales de potencia, utilizando un bucle `Para`.
3. `CalcularDistanciaEuclidiana(x1, y1, x2, y2)`: Utiliza las funciones anteriores o formulas basicas para retornar la distancia entre dos puntos cartesianos.
