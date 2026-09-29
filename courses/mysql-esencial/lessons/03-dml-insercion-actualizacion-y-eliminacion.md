# 3. DML: INSERT INTO, UPDATE, DELETE y TRUNCATE

Una vez disenado el esquema de tablas mediante DDL, utilizaremos **DML (Data Manipulation Language)** para gestionar el ciclo de vida de los registros en la base de datos: insercion, actualizacion puntual y eliminacion de filas.

---

## Objetivos de la Leccion
- Insertar registros individuales y masivos mediante `INSERT INTO`.
- Actualizar filas condicionadas mediante `UPDATE` y la clausula `WHERE`.
- Diferenciar entre la eliminacion selectiva con `DELETE` y el restablecimiento masivo con `TRUNCATE TABLE`.
- Prevenir actualizaciones accidentales de tablas completas.

---

## Insercion de Registros (`INSERT INTO`)

```sql
USE tienda_online;

-- 1. Insercion individual especificando columnas destino
INSERT INTO categorias (nombre, descripcion) 
VALUES ('Informatica', 'Equipos de computo, servidores y periféricos');

-- 2. Insercion multiple en un solo lote atomico (Optimiza escrituras en disco)
INSERT INTO categorias (nombre, descripcion) 
VALUES 
    ('Redes', 'Routers, switches y cableado estructurado'),
    ('Seguridad', 'Camaras IP, grabadores y control de accesos'),
    ('Audio', 'Microfonos, altavoces y mesas de mezcla');

-- 3. Insercion de productos vinculados a categorias existentes (categoria_id 1 = Informatica)
INSERT INTO productos (codigo_sku, nombre, precio, existencias, categoria_id)
VALUES 
    ('SKU-1001', 'Laptop Profesional 16GB', 1450.00, 8, 1),
    ('SKU-1002', 'Teclado Mecanico USB', 65.50, 25, 1),
    ('SKU-2001', 'Switch 24 Puertos Gigabit', 310.00, 12, 2);
```

---

## Actualizacion de Filas (`UPDATE`)

El comando `UPDATE` altera los valores de una o mas columnas en filas existentes:

```sql
-- Actualizar precio y existencias de un producto puntual identificado por SKU
UPDATE productos 
SET precio = 1399.99, existencias = 10 
WHERE codigo_sku = 'SKU-1001';

-- Incrementar el precio en un 8% para todos los productos de la categoria 2 (Redes)
UPDATE productos 
SET precio = precio * 1.08 
WHERE categoria_id = 2;
```

> [!WARNING]
> **Riesgo Critico de Integridad:**  
> Ejecutar un comando `UPDATE productos SET precio = 0.00;` **sin la clausula `WHERE`** sobrescribira el precio de la totalidad de registros de la tabla. Siempre ejecuta un `SELECT` previo con las mismas condiciones para validar que filas seran afectadas.

---

## Eliminacion de Datos: `DELETE` vs `TRUNCATE`

```sql
-- 1. DELETE: Elimina filas que satisfagan el predicado WHERE
DELETE FROM productos 
WHERE codigo_sku = 'SKU-1002';

-- 2. TRUNCATE TABLE: Vacia la tabla por completo y reinicia el contador AUTO_INCREMENT
TRUNCATE TABLE productos;
```

### Tabla Comparativa
| Parametro | `DELETE` | `TRUNCATE` |
| :--- | :--- | :--- |
| **Clasificacion** | DML | DDL |
| **Admite clausula WHERE** | Si (Permite borrado selectivo) | No (Vacia la tabla entera) |
| **Mecanismo Interno** | Elimina fila por fila registrando logs | Destruye y recrea la estructura |
| **Rendimiento** | Lento en millones de filas | Inmediato (O(1)) |
| **Contador AUTO_INCREMENT** | Mantiene el ultimo valor alcanzado | Se restablece a 1 |

---

## Ejercicio Practico

1. Inserta 3 categorias y 4 productos en la base de datos `tienda_online`.
2. Escribe una consulta `UPDATE` que reduzca un 10% el precio de aquellos productos cuyas existencias sean superiores a 20 unidades.
3. Ejecuta una eliminacion segura con `DELETE` para borrar aquellos productos cuyo precio sea menor a `$10.00`.
