# 5. Funciones de Agregacion (COUNT, SUM, AVG) y GROUP BY / HAVING

En el diseno de sistemas de gestion empresarial y tableros analiticos es imprescindible calcular metricas cuantitativas globales: total de ingresos, medias salariales o conteo de ordenes por region. En esta leccion exploraras las **Funciones de Agregacion** y la clausula **`GROUP BY`**.

---

## Objetivos de la Leccion
- Utilizar funciones de agregacion estandar: `COUNT()`, `SUM()`, `AVG()`, `MIN()` y `MAX()`.
- Colapsar conjuntos de datos en grupos coherentes con `GROUP BY`.
- Comprender la diferencia fundamental entre el filtrado de filas individuales con `WHERE` y el filtrado de grupos consolidados con `HAVING`.

---

## Funciones de Agregacion Escalares

Las funciones de agregacion procesan una columna a traves de multiples filas y devuelven un unico valor resumido:

```sql
USE tienda_online;

SELECT 
    COUNT(*) AS total_filas_catalogo,
    COUNT(categoria_id) AS productos_con_categoria,
    SUM(existencias) AS stock_total_unidades,
    ROUND(AVG(precio), 2) AS precio_promedio_general,
    MIN(precio) AS precio_mas_bajo,
    MAX(precio) AS precio_mas_alto
FROM productos;
```

> [!NOTE]
> `COUNT(*)` cuenta todas las filas devueltas (incluyendo aquellas con campos nulos), mientras que `COUNT(columna)` cuenta unicamente las filas donde dicha columna no sea `NULL`.

---

## Agrupacion de Datos (`GROUP BY`)

La clausula `GROUP BY` agrupa filas que comparten valores identicos en una o mas columnas, permitiendo aplicar las funciones de agregacion sobre cada subconjunto:

```sql
-- Calcular la cantidad de articulos y el precio medio por cada categoria
SELECT 
    categoria_id,
    COUNT(*) AS total_articulos,
    SUM(existencias) AS existencias_totales,
    ROUND(AVG(precio), 2) AS precio_promedio
FROM productos
GROUP BY categoria_id;
```

---

## Filtrado de Grupos: `WHERE` vs `HAVING`

Uno de los errores conceptuales mas frecuentes en SQL es intentar filtrar metricas acumuladas en la clausula `WHERE`. La jerarquia de ejecucion del motor SQL establece un orden estricto:

```text
Orden de Ejecucion del Motor SQL:
1. FROM / JOIN
2. WHERE           <-- Filtra filas individuales ANTES de agrupar
3. GROUP BY        <-- Agrupa las filas restantes
4. HAVING          <-- Filtra los grupos resultantes
5. SELECT          <-- Proyecta las columnas
6. ORDER BY        <-- Ordena el conjunto final
7. LIMIT           <-- Limita la salida
```

```sql
-- Consulta Analitica:
-- Obtener aquellas categorias donde el precio promedio sea mayor a $100,
-- considerando unicamente productos que tengan existencias mayores a cero:

SELECT 
    categoria_id,
    COUNT(*) AS cantidad_productos,
    ROUND(AVG(precio), 2) AS promedio_precio
FROM productos
WHERE existencias > 0         -- Paso 1: Filtra filas individuales
GROUP BY categoria_id         -- Paso 2: Agrupa por categoria
HAVING AVG(precio) > 100.00   -- Paso 3: Filtra los grupos calculados
ORDER BY promedio_precio DESC;
```

---

## Ejercicio Practico

Dada una tabla de transacciones de ventas con campos `cliente_id`, `monto_total` y `metodo_pago`:  
Escribe una consulta que agrupe por `cliente_id` y muestre unicamente aquellos clientes que hayan acumulado mas de 3 compras y cuyo gasto total (`SUM(monto_total)`) sea estrictamente superior a `$1,000.00`.
