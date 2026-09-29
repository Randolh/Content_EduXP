# 3. Condicionales, Bucles y Structural Pattern Matching (match/case)

El control de flujo en Python combina estructuras clasicas con innovaciones modernas del lenguaje, como la sintaxis de **Structural Pattern Matching (`match/case`)** estandarizada a partir de Python 3.10.

---

## Objetivos de la Leccion
- Evaluar condiciones logicas con `if`, `elif` y `else`.
- Implementar expresiones condicionales de una sola linea (Operador Ternario).
- Utilizar bucles `for` avanzados con funciones generadoras `range()`, `enumerate()` y `zip()`.
- Dominar el bucle `while` y las clausulas de control `break`, `continue` y `else`.
- Aplicar Structural Pattern Matching para descomponer estructuras complejas de datos.

---

## Evaluacion Condicional Moderna

```python
nivel_riesgo: str
puntuacion_crediticia: int = 740

if puntuacion_crediticia >= 750:
    nivel_riesgo = "Bajo"
elif puntuacion_crediticia >= 650:
    nivel_riesgo = "Moderado"
elif puntuacion_crediticia >= 500:
    nivel_riesgo = "Alto"
else:
    nivel_riesgo = "Critico"

print(f"Clasificacion de riesgo: {nivel_riesgo}")
```

### Expresion Condicional (Operador Ternario)
Sintaxis: `valor_si_verdadero if condicion else valor_si_falso`

```python
estado_usuario = "Activo" if token_valido else "Bloqueado"
```

---

## Iteraciones Deterministas con `for`

En Python, el bucle `for` es un bucle iterador que recorre secuencias u objetos iterables:

```python
# 1. Secuencia numerica con range(inicio, fin, paso)
for i in range(10, 50, 10):
    print(f"Indice: {i}")

# 2. enumerate() para obtener posicion y valor simultaneamente
servidores = ["srv-prod-01", "srv-prod-02", "srv-backup-01"]
for indice, host in enumerate(servidores, start=1):
    print(f"Nodo {indice}: {host}")

# 3. zip() para iterar multiples colecciones en paralelo
usuarios = ["admin", "developer", "tester"]
puertos = [8080, 3000, 5000]
for u, p in zip(usuarios, puertos):
    print(f"Servicio {u} asignado en puerto TCP {p}")
```

---

## El Bucle `while` y la Clausula `else`

En Python, tanto `for` como `while` admiten un bloque `else` opcional. El bloque `else` se ejecuta **solamente si el bucle finalizo de forma natural** sin haber sido interrumpido por un `break`:

```python
intentos = 0
autenticado = False

while intentos < 3:
    clave = input("Credencial de acceso: ")
    if clave == "claveSecreta2026":
        autenticado = True
        print("Acceso verificado.")
        break
    intentos += 1
else:
    # Se ejecuta solo si se agotaron los 3 intentos sin break
    print("Alerta de seguridad: Superado el limite maximo de reintentos.")
```

---

## Structural Pattern Matching (`match/case`)

`match/case` permite evaluar tanto el valor como la forma y estructura interna de los datos, sustituyendo complejas cadenas de `isinstance()` o comparaciones anidadas.

### 1. Evaluacion de Patrones y Comprobacion de Guardias (`if`)
```python
def procesar_respuesta_api(evento: dict) -> None:
    match evento:
        case {"status": 200, "data": list() as registros}:
            print(f"Exito: Se procesaron {len(registros)} registros devueltos.")
        case {"status": 404}:
            print("Error: El recurso solicitado no existe en la base de datos.")
        case {"status": int(codigo), "error": str(mensaje)} if codigo >= 500:
            print(f"Falla de Servidor [{codigo}]: {mensaje}")
        case _:
            print("Estructura de respuesta no documentada.")

procesar_respuesta_api({"status": 200, "data": ["item1", "item2"]})
procesar_respuesta_api({"status": 503, "error": "Servicio en mantenimiento"})
```

### 2. Desempaquetado de Tuplas de Comandos
```python
comando = ("TRANSFERIR", 5000.0, "CUENTA-A", "CUENTA-B")

match comando:
    case ("SALDO", cuenta):
        print(f"Consultando balance de: {cuenta}")
    case ("TRANSFERIR", float(monto), origen, destino) if monto > 0:
        print(f"Transferencia de ${monto:,.2f} desde {origen} hacia {destino}.")
    case _:
        print("Comando de operacion invalido.")
```

---

## Ejercicio Practico

Construye un script `analizador_paquetes.py` que simule la recepcion de tuplas de telemetria de una red de sensores. Cada tupla tendra el formato `(id_sensor, tipo_sensor, lectura, estado)`.  
Utiliza `match/case` para:
- Detectar si el sensor es `"TEMPERATURA"` y su lectura supera `75.0`, imprimiendo alerta de sobrecalentamiento.
- Detectar si el estado es `"ERROR"`, imprimiendo aviso de sustitucion de hardware.
- Registrar el caso por defecto como telemetria ordinaria.
