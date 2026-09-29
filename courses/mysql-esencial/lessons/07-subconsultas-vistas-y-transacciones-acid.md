# 7. Subconsultas, Vistas (CREATE VIEW), Transacciones ACID y Proyecto Final

En esta leccion final de MySQL 8.x abordaras las tecnicas avanzadas de bases de datos: **Subconsultas anidadas**, **Vistas logicas** para encapsular consultas analiticas, y el control de **Transacciones ACID** para garantizar la integridad contable del sistema.

---

## Objetivos de la Leccion
- Escribir subconsultas escalares y correlacionadas en las clausulas `WHERE` y `FROM`.
- Crear, consultar y mantener Vistas virtuales (`CREATE VIEW`).
- Comprender el estandar ACID (Atomicidad, Consistencia, Aislamiento, Durabilidad).
- Controlar transacciones mediante `START TRANSACTION`, `COMMIT` y `ROLLBACK`.
- Implementar el esquema de base de datos relacional del Proyecto Final Integrador.

---

## Subconsultas (Subqueries)

Una subconsulta es una sentencia `SELECT` anidada dentro de otra consulta SQL principal:

```sql
USE tienda_online;

-- Subconsulta Escalar en WHERE:
-- Obtener todos los productos cuyo precio sea superior al precio promedio general del catalogo
SELECT codigo_sku, nombre, precio 
FROM productos 
WHERE precio > (
    SELECT AVG(precio) FROM productos
)
ORDER BY precio DESC;
```

---

## Vistas de Base de Datos (`CREATE VIEW`)

Una **Vista** es una tabla virtual definida a partir del resultado de una consulta SQL predefinida. No duplica los datos en disco, pero simplifica la arquitectura permitiendo consultar reportes complejos con la misma sintaxis de una tabla tradicional:

```sql
-- 1. Definicion de la vista de catalogo detallado
CREATE OR REPLACE VIEW v_reporte_catalogo AS
SELECT 
    p.producto_id,
    p.codigo_sku,
    p.nombre AS producto,
    p.precio,
    p.existencias,
    c.nombre AS categoria,
    (p.precio * p.existencias) AS valor_inventario
FROM productos p
LEFT JOIN categorias c ON p.categoria_id = c.categoria_id;

-- 2. Consumo simple de la vista como si fuera una tabla fisica
SELECT * FROM v_reporte_catalogo 
WHERE valor_inventario >= 1000.00;
```

---

## Transacciones ACID (`COMMIT` / `ROLLBACK`)

Una **Transaccion** es una unidad de trabajo logica indivisible. Se rige por las propiedades **ACID**:
- **Atomicidad (A):** Todas las operaciones se completan con exito o ninguna tiene efecto.
- **Consistencia (C):** La base de datos pasa de un estado valido a otro estado valido.
- **Aislamiento (I):** Las operaciones concurrentes no interfieren entre si.
- **Durabilidad (D):** Los cambios confirmados sobreviven a fallos del sistema o de corriente electrica.

### Ejemplo: Transferencia de Fondos Financiera Segura
```sql
-- Iniciar bloque de transaccion
START TRANSACTION;

-- Paso 1: Debitar fondos de la cuenta origen
UPDATE cuentas_bancarias 
SET saldo = saldo - 500.00 
WHERE cuenta_id = 101 AND saldo >= 500.00;

-- Paso 2: Acreditar fondos a la cuenta destino
UPDATE cuentas_bancarias 
SET saldo = saldo + 500.00 
WHERE cuenta_id = 202;

-- Confirmar permanentemente la transaccion si no hubo ningun error:
COMMIT;

-- Si se detecto una anomalia o falla en la red, se revierte todo:
-- ROLLBACK;
```

---

## Proyecto Final Integrador: Esquema Comercial E-Commerce

A continuacion se presenta el script SQL completo que implementa el diseno relacional, insercion de datos, vistas y transacciones para una plataforma de comercio electronico:

```sql
-- 1. Creacion y seleccion del esquema
CREATE DATABASE IF NOT EXISTS eduxp_ecommerce;
USE eduxp_ecommerce;

-- 2. Tabla Clientes
CREATE TABLE IF NOT EXISTS clientes (
    cliente_id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    email VARCHAR(120) NOT NULL UNIQUE,
    fecha_alta DATETIME DEFAULT CURRENT_TIMESTAMP
) ENGINE=InnoDB;

-- 3. Tabla Pedidos
CREATE TABLE IF NOT EXISTS pedidos (
    pedido_id INT AUTO_INCREMENT PRIMARY KEY,
    cliente_id INT NOT NULL,
    monto_total DECIMAL(10,2) NOT NULL,
    estado VARCHAR(20) NOT NULL DEFAULT 'COMPLETADO',
    fecha DATETIME DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT fk_pedidos_clientes 
        FOREIGN KEY (cliente_id) REFERENCES clientes(cliente_id)
        ON DELETE RESTRICT
        ON UPDATE CASCADE
) ENGINE=InnoDB;

-- 4. Insercion de datos maestros
INSERT INTO clientes (nombre, email) VALUES
('Mariana Ortiz', 'mariana@eduxp.org'),
('Julian Castro', 'julian@eduxp.org'),
('Lorena Rivas', 'lorena@eduxp.org');

-- 5. Transaccion controlada para procesar una compra
START TRANSACTION;

INSERT INTO pedidos (cliente_id, monto_total, estado)
VALUES (1, 350.50, 'COMPLETADO');

COMMIT;

-- 6. Creacion de Vista Analitica de Facturacion por Cliente
CREATE OR REPLACE VIEW v_resumen_ventas_clientes AS
SELECT 
    c.cliente_id,
    c.nombre AS nombre_cliente,
    c.email,
    COUNT(p.pedido_id) AS total_pedidos_realizados,
    COALESCE(SUM(p.monto_total), 0.00) AS total_gastado
FROM clientes c
LEFT JOIN pedidos p ON c.cliente_id = p.cliente_id
GROUP BY c.cliente_id, c.nombre, c.email;

-- 7. Consulta final de auditoria
SELECT * FROM v_resumen_ventas_clientes 
ORDER BY total_gastado DESC;
```

---

## Conclusiones del Curso
Has completado con exito el curso **MySQL 8.x y Bases de Datos Relacionales desde Cero**. Ya dominas la definicion formal de esquemas, la manipulacion masiva de registros, la ejecucion de consultas relacionales multitabla y la administracion de transacciones transaccionales seguras.
