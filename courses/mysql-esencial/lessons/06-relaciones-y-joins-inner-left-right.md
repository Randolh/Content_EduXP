# 6. Uniones Multitabla: INNER JOIN, LEFT JOIN y RIGHT JOIN

La virtud principal del modelo relacional es la capacidad de normalizar los esquemas dividiendo la informacion en tablas independientes y recomponer los datos en tiempo de consulta mediante las operaciones de **JOIN**. En esta leccion exploraras el algebra relacional aplicada a consultas multitabla.

---

## Objetivos de la Leccion
- Comprender la teoria de conjuntos detras de las operaciones de union relacional.
- Implementar uniones internas exactas con `INNER JOIN`.
- Preservar registros sin correspondencia mediante `LEFT JOIN` y `RIGHT JOIN`.
- Detectar registros huerfanos mediante combinaciones de `LEFT JOIN` y clausulas `IS NULL`.
- Construir consultas complejas que enlazan tres o mas tablas relacionadas.

---

## Clasificacion de Uniones Relacionales

```text
       INNER JOIN                     LEFT JOIN                    RIGHT JOIN
    ┌───────┬───────┐              ┌───────┬───────┐            ┌───────┬───────┐
    │       │///////│              │///////│///////│            │       │///////│
    │ Tabla │///////│ Tabla        │ Tabla │///////│ Tabla      │ Tabla │///////│ Tabla
    │   A   │///////│   B          │   A   │///////│   B        │   A   │///////│   B  
    │       │///////│              │///////│///////│            │       │///////│
    └───────┴───────┘              └───────┴───────┘            └───────┴───────┘
  Coincidencias en ambas         Todos los de A + coinc.      Todos los de B + coinc.
```

---

## 1. `INNER JOIN` (Interseccion Exacta)

Devuelve unicamente las filas que tienen una coincidencia valida en ambas tablas unidas por la condicion relacional `ON`:

```sql
USE tienda_online;

SELECT 
    p.producto_id,
    p.codigo_sku,
    p.nombre AS producto,
    p.precio,
    c.nombre AS categoria
FROM productos p
INNER JOIN categorias c ON p.categoria_id = c.categoria_id;
```

---

## 2. `LEFT JOIN` (Inclusion de la Tabla Izquierda)

Devuelve **todas las filas de la tabla izquierda** (`FROM productos`), y si no existe coincidencia en la tabla derecha (`categorias`), rellena las columnas de la derecha con valores `NULL`:

```sql
-- Listar TODOS los productos, incluso si no tienen categoria asignada (categoria_id es NULL)
SELECT 
    p.nombre AS producto,
    p.precio,
    COALESCE(c.nombre, 'Sin Categoria') AS categoria
FROM productos p
LEFT JOIN categorias c ON p.categoria_id = c.categoria_id;
```

### Patron de Deteccion de Huerfanos (Anti-Join)
Podemos identificar registros que no tienen ninguna relacion en la tabla hija filtrando por `WHERE b.pk IS NULL`:

```sql
-- Encontrar categorias que NO tienen ningun producto asociado en catalogo
SELECT c.categoria_id, c.nombre AS categoria_vacia
FROM categorias c
LEFT JOIN productos p ON c.categoria_id = p.categoria_id
WHERE p.producto_id IS NULL;
```

---

## 3. Uniones Multitabla Encadenadas

En aplicaciones de comercio electronico vinculamos clientes, pedidos y productos a traves de tablas intermedias normalizadas:

```sql
SELECT 
    o.orden_id,
    cli.nombre AS nombre_cliente,
    cli.email,
    p.nombre AS producto_comprado,
    o.total,
    o.fecha
FROM ordenes o
INNER JOIN clientes cli ON o.cliente_id = cli.cliente_id
INNER JOIN productos p ON o.producto_id = p.producto_id
ORDER BY o.fecha DESC;
```

---

## Ejercicio Practico

Escribe una consulta SQL multitabla que:
1. Realice un `INNER JOIN` entre la tabla `categorias` y la tabla `productos`.
2. Calcule la cantidad de articulos y el valor total del inventario (`SUM(precio * existencias)`) por cada nombre de categoria.
3. Ordene los resultados de mayor a menor valor total de inventario.
