# 1. Fundamentos de la Programacion, Algoritmos y Abstraccion

El desarrollo de software profesional no consiste unicamente en memorizar palabras clave de un lenguaje especifico, sino en cultivar la capacidad de analizar problemas del mundo real y traducirlos en secuencias precisas de instrucciones ejecutables por una computadora.

---

## Objetivos de la Leccion
- Comprender la arquitectura funcional de un programa y el rol del procesador y la memoria.
- Definir con precision que es un algoritmo e identificar sus cuatro propiedades fundamentales.
- Aplicar tecnicas de descomposicion y abstraccion para resolver problemas.
- Representar algoritmos mediante pseudocodigo formal y diagramas de flujo.

---

## Que es la Programacion

Una computadora es un dispositivo electronico digital de alta velocidad disenado para ejecutar operaciones logicas y aritmeticas basicas. Carece de sentido comun, intuicion y criterio de decision propio; unicamente procesa las directrices exactas que recibe.

> [!NOTE]
> **Definicion Tecnica:**  
> Programar es el acto formal de estructurar, escribir, probar, depurar y mantener el codigo fuente de un programa informatico a traves de un lenguaje formal con reglas sintacticas y semanticas definidas.

El flujo de procesamiento clasico consta de tres etapas:
1. **Entrada (Input):** Datos suministrados por el usuario, sensores o archivos de disco.
2. **Procesamiento:** Transformaciones logicas y aritmeticas realizadas por el procesador (CPU) en la memoria RAM.
3. **Salida (Output):** Informacion procesada presentada al usuario, transmitida por red o guardada en disco.

---

## Propiedades Fundamentales de un Algoritmo

Para que una serie de instrucciones califique formalmente como algoritmo en ciencias de la computacion, debe cumplir obligatoriamente con los siguientes requisitos:

| Propiedad | Definicion | Relevancia Tecnica |
| :--- | :--- | :--- |
| **Finitud** | Debe tener un punto de terminacion claro tras un numero discreto y contable de pasos. | Evita ciclos de ejecucion perpetuos que agotan los recursos del sistema. |
| **Precision** | Cada paso individual debe estar libre de ambiguedad y claramente especificado. | Garantiza que cualquier interpretador o procesador ejecute la misma accion exacta. |
| **Determinismo** | Si se procesan las mismas entradas en diferentes instancias, se debe generar siempre el mismo resultado. | Asegura la repetibilidad y verificabilidad de las pruebas de software. |
| **Eficiencia** | Los pasos deben requerir una cantidad razonable y finita de tiempo y memoria. | Permite que el sistema escale a grandes volumenes de procesamiento. |

---

## Metodologia de Abstraccion y Descomposicion

Cuando un ingeniero de software se enfrenta a un requerimiento complejo (por ejemplo, calcular impuestos internacionales o procesar imagenes satelitales), aplica dos principios cardinales:

1. **Descomposicion modular:** Dividir el problema global en subproblemas mas pequenos e independientes (Divide y Venceras).
2. **Abstraccion:** Aislar los detalles superficiales o irrelevantes y concentrarse unicamente en los datos y operaciones criticas.

### Ejemplo Practico: Calculo de Tarifa de Peaje Autopista
Un problema que parece amplio se descompone en:
- Subproblema A: Identificar el tipo de vehiculo (motocicleta, automovil, transporte pesado).
- Subproblema B: Evaluar la hora del trayecto (tarifa estandar vs tarifa hora punta).
- Subproblema C: Comprobar el medio de pago (dispositivo electronico TAG con descuento vs efectivo).
- Subproblema D: Totalizar el importe y emitir el ticket.

---

## Representacion mediante Pseudocodigo

El pseudocodigo es una convencion estructurada que utiliza construcciones logicas similares a los lenguajes de alto nivel (como asignaciones, condicionales y bucles) expresadas en un lenguaje legible para el ser humano.

```text
Algoritmo ControlAccesoEdificio
    // Declaracion explicita de tipos de datos
    Definir edad Como Entero
    Definir tienePaseElectronico Como Booleano
    
    Escribir "Ingrese la edad del visitante:"
    Leer edad
    Escribir "El visitante posee pase valido? (Verdadero/Falso):"
    Leer tienePaseElectronico
    
    Si (edad >= 18) Y (tienePaseElectronico == Verdadero) Entonces
        Escribir "Acceso autorizado: Apertura de torniquete."
    Sino
        Escribir "Acceso denegado: Proceda a la recepcion central."
    FinSi
FinAlgoritmo
```

> [!TIP]
> **Recomendacion de Diseno:**  
> Nunca comiences a codificar directamente en un lenguaje de programacion sin haber estructurado previamente el flujo logico en papel o pseudocodigo. El 80% de los fallos de diseno ocurren por falta de planificacion algoritmica.

---

## Ejercicio Practico de Autoevaluacion

Elabora en tu cuaderno o editor el pseudocodigo para un algoritmo denominado `CalculoCalificacionFinal`:
1. Debe solicitar tres notas parciales de un estudiante (rango de 0 a 100).
2. La nota 1 pondera el 30%, la nota 2 pondera el 30% y la nota 3 pondera el 40%.
3. Si el promedio final ponderado es igual o mayor a 70, imprime "Aprobado"; de lo contrario imprime "Reprobado".
