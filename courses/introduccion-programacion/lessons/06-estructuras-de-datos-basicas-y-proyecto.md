# 6. Arreglos Indexados y Proyecto Integrador de Logica

Hasta el momento hemos procesado variables atomicas que unicamente retienen un valor individual. En la industria del software es indispensable manipular listas masivas de registros (usuarios de una base de datos, precios bursatiles, coordenadas de navegacion). En esta leccion aprenderas a manipular **Arreglos Unidimensionales (Arrays)** y consolidaras el curso en un **Proyecto Integrador**.

---

## Objetivos de la Leccion
- Comprender la distribucion contigua de un arreglo en la memoria RAM.
- Acceder, mutar y leer elementos mediante indices numericos (Zero-Indexed).
- Implementar algoritmos clasicos de busqueda lineal y calculo de estadisticas sobre arreglos.
- Desarrollar la arquitectura integral del Proyecto Final del curso.

---

## Anatomia de un Arreglo (Array)

Un **Arreglo** o Vector es una coleccion estructurada y secuencial de elementos de un mismo tipo de dato almacenados en posiciones contiguas de memoria.

Cada casillero individual se direcciona mediante un **Indice numerico**. En los estandares informaticos contemporaneos se utiliza la convencion de **indexacion base cero** (*0-indexed*):

```text
Arreglo: medicionesSensores (Tamano = 5)
Direccion:   0x100      0x104      0x108      0x10C      0x110
Indice:       [0]        [1]        [2]        [3]        [4]
Valor:       24.5       26.1       22.8       25.0       28.4
```

### Operaciones Fundamentales sobre Arreglos
```text
Algoritmo ManipulacionArreglos
    Definir temperaturas Como Real[5]
    Definir i Como Entero
    
    // Escritura en posiciones especificas
    temperaturas[0] = 24.5
    temperaturas[1] = 26.1
    temperaturas[2] = 22.8
    temperaturas[3] = 25.0
    temperaturas[4] = 28.4
    
    // Lectura e impresion con ciclo Para
    Para i Desde 0 Hasta 4 Con Paso 1 Hacer
        Escribir "Sensor [", i, "]: ", temperaturas[i], " C"
    FinPara
FinAlgoritmo
```

---

## Algoritmo de Busqueda Lineal

Uno de los algoritmos basicos de colecciones consiste en recorrer secuencialmente el arreglo comparando cada posicion con un elemento de interes:

```text
Funcion BuscarRegistro(arregloDatos, dimension, elementoBuscado)
    Definir i Como Entero
    Para i Desde 0 Hasta (dimension - 1) Con Paso 1 Hacer
        Si arregloDatos[i] == elementoBuscado Entonces
            Retornar i // Retorna el indice donde lo encontro
        FinSi
    FinPara
    Retornar -1 // Retorna -1 si no existe en la coleccion
FinFuncion
```

---

## Proyecto Final Integrador: Sistema de Analisis Financiero y Ventas

A continuacion se presenta la especificacion y el algoritmo completo que integra variables, tipos de datos primitivos, validaciones condicionales, ciclos repetitivos, arreglos y funciones modulares:

```text
// Modulo de validacion de comisiones
Funcion CalcularComision(montoVenta, rendimientoPorcentaje)
    Si rendimientoPorcentaje >= 100.0 Entonces
        Retornar montoVenta * 0.12 // 12% por cumplimiento total
    Sino Si rendimientoPorcentaje >= 80.0 Entonces
        Retornar montoVenta * 0.08 // 8% por cumplimiento parcial
    Sino
        Retornar montoVenta * 0.02 // 2% comision base
    FinSi
FinFuncion

// Modulo de calculo de promedio
Funcion CalcularPromedio(ventas, cantidad)
    Definir suma Como Real
    Definir i Como Entero
    suma = 0.0
    Para i Desde 0 Hasta (cantidad - 1) Hacer
        suma = suma + ventas[i]
    FinPara
    Retornar suma / cantidad
FinFuncion

Algoritmo SistemaFinancieroComercial
    // Definicion de constantes y variables
    Definir LIMITE_MESES Como Entero
    LIMITE_MESES = 6
    
    Definir historicoVentas Como Real[6]
    Definir metaMensual, totalAnual, promedio, ventaPico Como Real
    Definir i, mesPico Como Entero
    
    metaMensual = 10000.00
    totalAnual = 0.00
    ventaPico = -1.0
    mesPico = 0
    
    Escribir "=== SISTEMA DE CONSOLIDACION COMERCIAL SEMESTRAL ==="
    
    // Captura de datos estructurada con ciclo Para
    Para i Desde 0 Hasta (LIMITE_MESES - 1) Con Paso 1 Hacer
        Escribir "Ingrese las ventas netas del Mes ", (i + 1), ":"
        Leer historicoVentas[i]
        
        // Acumular total
        totalAnual = totalAnual + historicoVentas[i]
        
        // Rastrear el mes de mayor venta
        Si historicoVentas[i] > ventaPico Entonces
            ventaPico = historicoVentas[i]
            mesPico = i + 1
        FinSi
    FinPara
    
    // Invocacion de funciones modulares
    promedio = CalcularPromedio(historicoVentas, LIMITE_MESES)
    
    Escribir "---------------------------------------------------"
    Escribir "Reporte Consolidado:"
    Escribir "Volumen Total Semestral: $", totalAnual
    Escribir "Promedio Mensual Obtenido: $", promedio
    Escribir "Mes con mayor rendimiento: Mes ", mesPico, " ($", ventaPico, ")"
    
    // Evaluacion del cumplimiento de metas
    Si promedio >= metaMensual Entonces
        Escribir "Dictamen: Cumplimiento de meta semestral alcanzado."
    Sino
        Escribir "Dictamen: Rendimiento inferior a la meta prevista."
    FinSi
    Escribir "---------------------------------------------------"
FinAlgoritmo
```

---

## Conclusiones del Curso
Has completado con exito el curso **Introduccion a la Programacion y Pensamiento Algoritmico**. Dominas los fundamentos teoricos y practicos que rigen cualquier lenguaje moderno como Python, JavaScript o SQL.
