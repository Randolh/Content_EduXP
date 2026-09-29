# 4. Listas, Tuplas, Diccionarios y Comprensiones (List Comprehensions)

La manipulacion eficiente de datos en Python se sustenta en sus cuatro estructuras nativas principales: **Listas**, **Tuplas**, **Diccionarios** y **Conjuntos**. En esta leccion exploraras sus garantias de rendimiento y las tecnicas funcionales de comprension.

---

## Objetivos de la Leccion
- Dominar listas dinamicas, operaciones de agregacion, remocion y corte (Slicing).
- Utilizar tuplas inmutables y desempaquetado estructurado.
- Manipular diccionarios clave-valor y metodos de extraccion segura (`get`, `setdefault`).
- Escribir comprensiones de listas y diccionarios de alto rendimiento y bajo consumo de memoria.

---

## Listas (`list`): Secuencias Mutables y Dinamicas

Una lista en Python es un arreglo dinamico redimensionable que almacena punteros a objetos en memoria:

```python
servicios: list[str] = ["auth", "database", "gateway", "billing"]

# Operaciones mutables
servicios.append("analytics")           # Insercion O(1) al final
servicios.insert(1, "cache")            # Insercion O(n) en posicion 1
servicios.remove("database")            # Remocion O(n) por valor
elemento_removido = servicios.pop()     # Extraccion O(1) del ultimo elemento
```

### Tecnicas de Slicing (Rebanado)
Sintaxis: `coleccion[inicio:fin:paso]`
```python
datos = [10, 20, 30, 40, 50, 60, 70, 80, 90]

print(datos[2:6])      # Indices del 2 al 5: [30, 40, 50, 60]
print(datos[:3])       # Tres primeros elementos: [10, 20, 30]
print(datos[5:])       # Del indice 5 hasta el final
print(datos[::2])      # Saltos de dos en dos
print(datos[::-1])     # Inversion completa de la lista
```

---

## Tuplas (`tuple`): Inmutabilidad y Eficiencia

Las tuplas son secuencias ordenadas de tamano fijo e inmutables. Consumen menos memoria RAM que las listas y son seguras frente a mutaciones accidentales:

```python
coordenada: tuple[float, float] = (19.4326, -99.1332)

# Desempaquetado multiple estructurado (Tuple Unpacking)
latitud, longitud = coordenada
print(f"Latitud: {latitud}, Longitud: {longitud}")
```

---

## Diccionarios (`dict`): Tablas Hash Clave-Valor

Los diccionarios implementan tablas hash con busqueda en tiempo constante promedio O(1). A partir de Python 3.7+, conservan formalmente el orden de insercion de las claves:

```python
configuracion_db: dict[str, any] = {
    "host": "localhost",
    "port": 5432,
    "database": "eduxp_core",
    "ssl_enabled": True
}

# Acceso seguro con .get() previniendo KeyError
puerto = configuracion_db.get("port", 3306) # Retorna 3306 si 'port' no existiera

# Iteracion limpia sobre items (clave, valor)
for clave, valor in configuracion_db.items():
    print(f"Parametro {clave}: {valor}")
```

---

## Comprensiones de Listas y Diccionarios

Las comprensiones permiten crear nuevas estructuras a partir de secuencias existentes mediante una sintaxis declarativa concisa ejecutada a nivel de lenguaje C interno:

### 1. List Comprehensions
Sintaxis: `[expresion for elemento in iterable if condicion]`

```python
valores_brutos = [12, -5, 45, 0, 18, -3, 60, 9]

# Filtrar positivos y multiplicar por el factor 1.15 en una sola expresion
valores_procesados = [round(v * 1.15, 2) for v in valores_brutos if v > 0]
print(valores_procesados) # [13.8, 51.75, 20.7, 69.0, 10.35]
```

### 2. Dict Comprehensions
Sintaxis: `{clave: valor for elemento in iterable if condicion}`

```python
nombres = ["juan", "maria", "alberto", "teresa"]
longitudes = {nombre.capitalize(): len(nombre) for nombre in nombres if len(nombre) > 4}
print(longitudes) # {'Maria': 5, 'Alberto': 7, 'Teresa': 6}
```

---

## Ejercicio Practico

Dado el siguiente registro de metricas:
```python
lecturas_red = [
    {"ip": "192.168.1.1", "latencia_ms": 12, "estado": "OK"},
    {"ip": "192.168.1.2", "latencia_ms": 140, "estado": "SLOW"},
    {"ip": "192.168.1.3", "latencia_ms": 8, "estado": "OK"},
    {"ip": "192.168.1.4", "latencia_ms": 310, "estado": "CRITICAL"}
]
```
Utiliza una **List Comprehension** para generar una lista que contenga unicamente las direcciones IP de aquellos nodos cuyo estado no sea `"OK"`.
