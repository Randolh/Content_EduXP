# 4. DQL: SELECT, WHERE, Operadores, LIKE, ORDER BY y LIMIT

**DQL (Data Query Language)** es el componente de SQL orientado a la recuperacion, transformacion y filtrado de datos almacenados mediante la sentencia `SELECT`.

---

## Objetivos de la Leccion
- Estructurar consultas de proyeccion de columnas mediante `SELECT` y alias (`AS`).
- Aplicar filtros relacionales y logicos en la clausula `WHERE`.
- Realizar busquedas de patrones de cadenas con el operador `LIKE` y comodines (`%`, `_`).
- Ordenar conjuntos de resultados con `ORDER BY` y paginar registros mediante `LIMIT` y `OFFSET`.

---

## Proyeccion de Columnas y Alias (`SELECT ... FROM`)

```sql
USE tienda_online;

-- 1. Proyeccion de columnas explicitas y alias para nombrar columnas de salida
SELECT 
    producto_id AS id,
    nombre AS producto,
    precio AS precio_unitario,
    (precio * existencias) AS valor_inventario_total
FROM productos;
```

---

## Filtrado de Registros con `WHERE`

La clausula `WHERE` evalua un predicado booleano sobre cada fila individual antes de proyectar la salida:

```sql
-- 1. Rango numerico inclusivo con BETWEEN
SELECT nombre, precio, existencias 
FROM productos 
WHERE precio BETWEEN 50.00 AND 500.00;

-- 2. Comparacion contra conjunto discreto con IN
SELECT nombre, categoria_id 
FROM productos 
WHERE categoria_id IN (1, 2, 4);

-- 3. Busqueda de subcadenas con LIKE y comodines
-- '%' representa 0 o mas caracteres arbitrarios
-- '_' representa exactamente un solo caracter
SELECT * FROM productos 
WHERE nombre LIKE 'Laptop%';   -- Inicia con 'Laptop'

SELECT * FROM productos 
WHERE nombre LIKE '%Gigabit%';  -- Contiene 'Gigabit' en cualquier posicion

-- 4. Comprobacion de valores nulos (IS NULL / IS NOT NULL)
SELECT * FROM productos 
WHERE categoria_id IS NULL;
```

---

## Ordenamiento y Paginacion de Resultados

### 1. Ordenamiento Jerarquico (`ORDER BY`)
Permite ordenar los resultados por una o varias columnas de forma ascendente (`ASC`, por defecto) o descendente (`DESC`):
```sql
SELECT nombre, precio, existencias 
FROM productos 
WHERE existencias > 0
ORDER BY precio DESC, nombre ASC;
```

### 2. Paginacion para Aplicaciones Web (`LIMIT` y `OFFSET`)
Permite limitar el volumen de datos transferidos por red para mostrar resultados paginados en el cliente:
```sql
-- Pagina 1: Obtener los primeros 10 registros
SELECT producto_id, nombre, precio 
FROM productos 
ORDER BY producto_id ASC 
LIMIT 10;

-- Pagina 2: Desplazar 10 registros (OFFSET 10) y recuperar los siguientes 10
SELECT producto_id, nombre, precio 
FROM productos 
ORDER BY producto_id ASC 
LIMIT 10 OFFSET 10;
```

---

## Ejercicio Practico

Escribe una consulta SQL que devuelva los 5 productos mas costosos del catalogo:
- Solo deben considerarse productos que tengan inventario disponible (`existencias > 0`).
- No deben incluirse productos cuyo nombre comience con la palabra `"Cable"`.
- Debes proyectar el nombre del producto y su precio formateado con alias `precio_venta`.
