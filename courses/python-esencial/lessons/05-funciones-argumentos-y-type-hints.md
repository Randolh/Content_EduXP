# 5. Funciones con Type Hints, *args, **kwargs y Lambdas

Las funciones son las unidades fundamentales de abstraccion y composicion de software en Python. En esta leccion aprenderas a disenar interfaces funcionales tipadas, desacopladas y conformes a las pautas de arquitectura moderna.

---

## Objetivos de la Leccion
- Definir funciones con la palabra clave `def` documentadas con docstrings (PEP 257).
- Utilizar anotaciones de tipos estaticas (**Type Hints**, PEP 484).
- Manejar argumentos posicionales dinamicos (`*args`) y argumentos de palabras clave (`**kwargs`).
- Definir argumentos exclusivos por posicion o por nombre (Keyword-Only Arguments).
- Implementar funciones lambda para operaciones de orden superior.

---

## Funciones Tipadas con Type Hints

A partir de Python 3.5+, las anotaciones de tipos no alteran la ejecucion en tiempo de ejecucion, pero permiten verificacion estatica con herramientas como `mypy` y autocompletado avanzado en Visual Studio Code:

```python
def calcular_tasa_efectiva(
    capital: float, 
    tasa_nominal: float, 
    periodos: int = 12
) -> float:
    """Calcula la tasa de interes efectiva anualizada.
    
    Args:
        capital: Monto original de la inversion.
        tasa_nominal: Tasa porcentual anual (ej. 0.15 para 15%).
        periodos: Cantidad de capitalizaciones en el ano fiscal.
        
    Returns:
        Monto final acumulado tras el periodo de inversion.
    """
    if capital <= 0 or periodos <= 0:
        raise ValueError("Parametros de capital y periodos deben ser estrictamente positivos.")
    return capital * ((1 + (tasa_nominal / periodos)) ** periodos)
```

---

## Argumentos Flexibles: `*args` y `**kwargs`

### 1. `*args` (Argumentos Posicionales Arbitrarios)
Empaqueta un numero indeterminado de parametros posicionales adicionales en una **Tupla**:
```python
def consolidar_totales(categoria: str, *montos: float) -> str:
    total: float = sum(montos)
    return f"Categoria {categoria}: Total consolidado = ${total:,.2f}"

print(consolidar_totales("Infraestructura", 1500.0, 3200.5, 450.0))
```

### 2. `**kwargs` (Argumentos Nombrados Arbitrarios)
Empaqueta argumentos nombrados adicionales en un **Diccionario**:
```python
def registrar_evento_auditoria(usuario: str, accion: str, **metadatos: any) -> None:
    print(f"AUDITORIA: Usuario '{usuario}' ejecuto accion '{accion}'")
    for k, v in metadatos.items():
        print(f"  Detalle [{k}]: {v}")

registrar_evento_auditoria(
    "admin_root", 
    "ACTUALIZAR_PARAMETROS", 
    ip="10.0.0.15", 
    modulo="facturacion", 
    intento=1
)
```

---

## Argumentos Nombrados Obligatorios (Keyword-Only)

Utilizando el caracter `*` solitario en la firma de la funcion, forzamos al invocador a nombrar explicitamente los argumentos que le suceden, evitando errores de pasaje por posicion:

```python
def conectar_servicio(host: str, puerto: int, *, timeout: int = 30, ssl: bool = True) -> None:
    print(f"Conectando a {host}:{puerto} (Timeout={timeout}s, SSL={ssl})")

# Invocacion correcta:
conectar_servicio("api.eduxp.org", 443, timeout=60, ssl=True)

# Invocacion incorrecta (Generara TypeError):
# conectar_servicio("api.eduxp.org", 443, 60, True)
```

---

## Expresiones Lambda y Funciones de Orden Superior

Una expresion `lambda` es una funcion anonima reducida a una unica expresion de evaluacion:

```python
# Ordenar un catalogo de servicios por tiempo de respuesta
servidores = [
    {"nodo": "us-east", "ping_ms": 45},
    {"nodo": "eu-central", "ping_ms": 120},
    {"nodo": "sa-brazil", "ping_ms": 18}
]

# Ordenamiento con funcion lambda como criterio de seleccion
servidores_ordenados = sorted(servidores, key=lambda s: s["ping_ms"])

for s in servidores_ordenados:
    print(f"{s['nodo']}: {s['ping_ms']} ms")
```

---

## Ejercicio Practico

Escribe una funcion tipada llamada `filtrar_registros(datos: list[dict], *, clave_filtro: str, umbral: float) -> list[dict]`:
1. Debe recibir una lista de diccionarios.
2. Debe filtrar y retornar unicamente aquellos diccionarios donde el valor de `clave_filtro` sea estrictamente mayor al `umbral`.
3. Debe incluir docstring detallado con formato PEP 257.
