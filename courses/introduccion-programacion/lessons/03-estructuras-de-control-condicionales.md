# 3. Toma de Decisiones y Estructuras Condicionales

Un programa secuencial que ejecuta ciegamente una lista fija de instrucciones es insuficiente para procesar la complejidad de los sistemas de informacion reales. Las estructuras condicionales permiten bifurcar el flujo de ejecucion segun el cumplimiento de criterios logicos evaluados en tiempo de ejecucion.

---

## Objetivos de la Leccion
- Comprender el flujo de control condicional y su representacion en arboles de decision.
- Implementar condicionales simples (`Si`), dobles (`Si / Sino`) y encadenados (`Si / Sino Si / Sino`).
- Dominar la estructura de seleccion multiple (`Segun / Switch`).
- Aplicar el principio de retorno temprano (Early Return) para reducir la complejidad ciclomatica.

---

## Mecanica de Bifurcacion de Flujo

Una estructura condicional evalua una expresion booleana. Si el resultado es `Verdadero`, el procesador salta a la direccion de memoria correspondiente al bloque designado; si es `Falso`, omite dicho bloque o ejecuta una rama alternativa.

```text
                         [ Expresion Logica ]
                                  │
                       ¿Evalua a Verdadero?
                      ┌───────────┴───────────┐
               [ Si ] │                       │ [ No ]
                      ▼                       ▼
            ┌───────────────────┐   ┌───────────────────┐
            │ Bloque Afirmativo │   │  Bloque Negativo  │
            └─────────┬─────────┘   └─────────┬─────────┘
                      │                       │
                      └───────────┬───────────┘
                                  ▼
                        [ Siguiente Sentencia ]
```

---

## Tipos de Estructuras Condicionales

### 1. Condicional Simple
Aplica una mutacion o efecto secundario unicamente si la condicion se satisface.

```text
Si saldoCuenta < costoTransaccion Entonces
    Escribir "Error: Fondos insuficientes para debitar operacion."
FinSi
```

### 2. Condicional Doble
Garantiza que uno y solo uno de los dos caminos excluyentes se ejecutara.

```text
Si temperaturaSensor > 85.0 Entonces
    ActivarSistemaRefrigeracion()
Sino
    MantenerModoReposo()
FinSi
```

### 3. Condicional Multiple Encadenado
Permite evaluar jerarquias de rangos continuos de manera secuencial:

```text
Algoritmo TarificacionConsumoElectrico
    Definir consumoKWh Como Real
    Definir tarifaAplicada Como Real
    
    Escribir "Ingrese los kilovatios consumidos en el periodo:"
    Leer consumoKWh
    
    Si consumoKWh <= 150 Entonces
        tarifaAplicada = consumoKWh * 0.10
    Sino Si consumoKWh <= 300 Entonces
        tarifaAplicada = (150 * 0.10) + ((consumoKWh - 150) * 0.15)
    Sino Si consumoKWh <= 500 Entonces
        tarifaAplicada = (150 * 0.10) + (150 * 0.15) + ((consumoKWh - 300) * 0.22)
    Sino
        tarifaAplicada = (150 * 0.10) + (150 * 0.15) + (200 * 0.22) + ((consumoKWh - 500) * 0.35)
    FinSi
    
    Escribir "Total a liquidar por servicio electrico: $", tarifaAplicada
FinAlgoritmo
```

---

## Estructura de Seleccion Multiple (`Segun / Switch`)

Cuando una variable individual debe compararse contra un conjunto discreto y cerrado de valores equivalentes (como estados de una maquina de estados o codigos de operacion), el encadenamiento de multiples `Sino Si` degrada la legibilidad. La estructura `Segun` optimiza este escenario:

```text
Algoritmo EnrutadorSolicitudes
    Definir codigoProtocolo Como Entero
    codigoProtocolo = 200
    
    Segun codigoProtocolo Hacer
        200:
            Escribir "HTTP 200: Peticion procesada con exito."
        201:
            Escribir "HTTP 201: Recurso creado satisfactoriamente."
        400:
            Escribir "HTTP 400: Solicitud malformada o parametros invalidos."
        401, 403:
            Escribir "HTTP 401/403: No autorizado o privilegios insuficientes."
        404:
            Escribir "HTTP 404: El recurso solicitado no existe en el servidor."
        500:
            Escribir "HTTP 500: Falla interna no controlada en el servidor."
        De Otro Modo:
            Escribir "Codigo de respuesta no clasificado en la norma."
    FinSegun
FinAlgoritmo
```

> [!NOTE]
> La clausula `De Otro Modo` (o `default` en lenguajes de produccion) actua como caso de escape obligatorio para interceptar cualquier valor fuera del dominio anticipado.

---

## Buenas Practicas: Evitar la Anidacion Profunda

El fenomeno conocido como **"Arrow Anti-Pattern"** o piramide de anidacion ocurre cuando se introducen condicionales anidados dentro de condicionales a mas de 3 o 4 niveles de profundidad:

```text
// Diseno Deficiente (Ilegible):
Si condicionA Entonces
    Si condicionB Entonces
        Si condicionC Entonces
            EjecutarAccion()
        FinSi
    FinSi
FinSi

// Diseno Profesional (Aplanado mediante Operador Logico):
Si condicionA Y condicionB Y condicionC Entonces
    EjecutarAccion()
FinSi
```

---

## Ejercicio Practico

Escribe en pseudocodigo la logica de validacion para el otorgamiento de un prestamo hipotecario con las siguientes reglas:
1. El solicitante debe tener entre 21 y 65 anos de edad.
2. Su antiguedad laboral debe ser mayor o igual a 2 anos.
3. La cuota mensual proyectada del credito no puede superar el 35% de su ingreso mensual neto.
4. Si cumple los 3 criterios, imprimir "Credito Pre-Aprobado"; de lo contrario, indicar especificamente que criterio no se satisfizo.
