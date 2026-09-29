# 4. Estructuras de Repeticion y Control de Ciclos

La automatizacion de tareas computacionales a gran escala depende de la capacidad de ejecutar un conjunto de instrucciones de manera repetitiva hasta que se satisfaga una condicion de terminacion especifica. En esta leccion exploraras los bucles deterministas e indeterministas.

---

## Objetivos de la Leccion
- Comprender la semantica y el ciclo de vida de una estructura de control iterativa.
- Dominar el bucle condicional de pre-verificacion (`Mientras / While`).
- Dominar el bucle contador determinista (`Para / For`).
- Identificar y prevenir bucles infinitos y fugas de recursos.
- Utilizar tecnicas de acumulacion, conteo y banderas de estado (Flags).

---

## Clasificacion de Estructuras Iterativas

Existen dos grandes familias de ciclos en ciencias de la computacion:

1. **Ciclos Indeterministas:** Aquellos en los que no se conoce con anticipacion el numero exacto de iteraciones, ya que dependen del estado del sistema, eventos de red o entradas del usuario (ejemplo: leer registros de un archivo hasta llegar al fin del fichero). Se implementan con `Mientras` (*While*).
2. **Ciclos Deterministas:** Aquellos en los que el numero exacto de repeticiones esta prefijado o depende de la dimension de una coleccion de datos finita. Se implementan con `Para` (*For*).

---

## El Bucle `Mientras` (*While*)

El bucle `Mientras` verifica la condicion logica **antes** de ingresar a cada iteracion. Si la condicion inicial es falsa, el cuerpo del bucle jamas se ejecuta.

```text
Algoritmo SimulacionDescargaArchivo
    Definir bytesTransferidos Como Entero
    Definir bytesTotales Como Entero
    Definir paquete Como Entero
    
    bytesTransferidos = 0
    bytesTotales = 1000
    paquete = 250
    
    Mientras bytesTransferidos < bytesTotales Hacer
        bytesTransferidos = bytesTransferidos + paquete
        Escribir "Progreso: ", bytesTransferidos, " / ", bytesTotales, " bytes."
    FinMientras
    
    Escribir "Descarga de archivo completada satisfactoriamente."
FinAlgoritmo
```

> [!WARNING]
> **Riesgo de Bucle Infinito:**  
> Si dentro del cuerpo del ciclo no se modifica ninguna variable que forme parte de la condicion de corte, el bucle se ejecutara indefinidamente, consumiendo el 100% del procesador hasta que el sistema operativo mate el proceso.

---

## El Bucle `Para` (*For*)

La estructura `Para` abstrae y empaqueta en una sola linea los tres componentes criticos de una iteracion controlada por contador:
1. **Inicializacion:** Define la variable de control y su valor de partida.
2. **Condicion de Limite:** Limite superior o inferior que debe alcanzar el contador.
3. **Paso de Incremento:** Magnitud en la que avanza el contador tras cada vuelta (positivo o negativo).

```text
Algoritmo CalculoFactorial
    Definir numero, i Como Entero
    Definir factorial Como Entero
    
    numero = 6
    factorial = 1
    
    Escribir "Calculando el factorial de: ", numero
    
    // Iteracion determinista desde 1 hasta numero
    Para i Desde 1 Hasta numero Con Paso 1 Hacer
        factorial = factorial * i
        Escribir "Paso ", i, ": factorial acumulado = ", factorial
    FinPara
    
    Escribir "Resultado final: ", numero, "! = ", factorial
FinAlgoritmo
```

---

## Patrones de Diseno en Iteraciones

### 1. Variables Contadoras
Variables enteras que incrementan en un valor constante para registrar ocurrencias de eventos:
```text
contadorErrores = contadorErrores + 1
```

### 2. Variables Acumuladoras
Variables numericas que suman valores dinamicos provenientes de distintas iteraciones:
```text
saldoAcumulado = saldoAcumulado + transaccionActual
```

### 3. Banderas Centinela (Flags)
Variables booleanas que alteran su valor para senalizar que un evento critico ocurrio y provocar la salida del ciclo:
```text
Definir encontrado Como Booleano
encontrado = Falso

Mientras (indice < totalRegistros) Y (encontrado == Falso) Hacer
    Si lista[indice] == claveBuscada Entonces
        encontrado = Verdadero
    FinSi
    indice = indice + 1
FinMientras
```

---

## Ejercicio Practico

Disena en pseudocodigo un algoritmo que solicite al usuario una serie de numeros enteros positivos uno por uno:
1. El usuario indicara que termino de ingresar datos introduciendo un `-1` (valor centinela de escape).
2. El algoritmo debe calcular e imprimir:
   - La cantidad total de numeros validos ingresados.
   - El promedio aritmetico de todos los numeros.
   - El numero maximo y el numero minimo ingresado durante la sesion.
