# 2. DDL: CREATE DATABASE, Tipos de Datos y Restricciones (PK/FK)

El lenguaje SQL se divide en subconjuntos de instrucciones especializadas. En esta leccion nos enfocaremos en **DDL (Data Definition Language)**, el conjunto de comandos dedicados a definir y alterar la estructura del esquema de datos (`CREATE`, `ALTER`, `DROP`).

---

## Objetivos de la Leccion
- Seleccionar los tipos de datos apropiados en MySQL 8.x para optimizar el almacenamiento en disco.
- Definir restricciones de integridad: `NOT NULL`, `UNIQUE`, `AUTO_INCREMENT`, `DEFAULT`, `CHECK`.
- Establecer Claves Primarias y Claves Foraneas con politicas de borrado y actualizacion (`ON DELETE`, `ON UPDATE`).
- Modificar esquemas de tablas activas mediante sentencias `ALTER TABLE`.

---

## Tipos de Datos Fundamentales en MySQL 8.x

| Tipo de Dato | Descripcion | Uso Recomendado |
| :--- | :--- | :--- |
| `INT` / `BIGINT` | Enteros de 4 bytes (hasta 2 mil millones) o de 8 bytes. | Identificadores autonumericos, cantidades enteras. |
| `DECIMAL(M,D)` | Punto fijo de alta precision (M = digitos totales, D = decimales). | **Dinero, transacciones financieras y contabilidad**. |
| `VARCHAR(N)` | Cadena de longitud variable con limite maximo de `N` caracteres. | Nombres, titulos, correos electronicos, URLs. |
| `TEXT` | Cadena de longitud extensa fuera de fila (hasta 64KB). | Descripciones largas, cuerpos de articulos. |
| `DATETIME` | Fecha y hora absoluta (`YYYY-MM-DD HH:MM:SS`). | Marcas de tiempo de auditoria, fechas de registro. |
| `JSON` | Almacenamiento nativo de documentos JSON con validacion de sintaxis. | Metadatos semidirigidos, payloads de APIs externas. |

---

## Creacion de Tablas con Integridad Referencial

A continuacion se implementa un esquema formal con tablas normalizadas para categorias y productos:

```sql
CREATE DATABASE IF NOT EXISTS tienda_online;
USE tienda_online;

-- 1. Tabla Padre: categorias
CREATE TABLE IF NOT EXISTS categorias (
    categoria_id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50) NOT NULL UNIQUE,
    descripcion TEXT,
    fecha_creacion DATETIME DEFAULT CURRENT_TIMESTAMP
) ENGINE=InnoDB;

-- 2. Tabla Hija: productos
CREATE TABLE IF NOT EXISTS productos (
    producto_id INT AUTO_INCREMENT,
    codigo_sku VARCHAR(30) NOT NULL UNIQUE,
    nombre VARCHAR(120) NOT NULL,
    precio DECIMAL(10,2) NOT NULL DEFAULT 0.00,
    existencias INT NOT NULL DEFAULT 0,
    categoria_id INT,
    
    -- Definicion de Llave Primaria
    PRIMARY KEY (producto_id),
    
    -- Restriccion CHECK para impedir precios negativos (MySQL 8.0.16+)
    CONSTRAINT chk_precio_positivo CHECK (precio >= 0.00),
    
    -- Definicion formal de Llave Foranea
    CONSTRAINT fk_productos_categorias
        FOREIGN KEY (categoria_id) 
        REFERENCES categorias(categoria_id)
        ON DELETE SET NULL
        ON UPDATE CASCADE
) ENGINE=InnoDB;
```

> [!NOTE]
> La politica `ON DELETE SET NULL` asegura que si una categoria es eliminada, los productos vinculados no se destruyan, sino que su columna `categoria_id` pase a valor `NULL`, evitando inconsistencias de datos.

---

## Modificacion Estructural (`ALTER TABLE`)

```sql
-- Anadir una columna nueva
ALTER TABLE productos 
ADD COLUMN codigo_barras VARCHAR(50) AFTER codigo_sku;

-- Modificar la dimension o tipo de una columna
ALTER TABLE productos 
MODIFY COLUMN nombre VARCHAR(150) NOT NULL;

-- Remover una columna
ALTER TABLE productos 
DROP COLUMN codigo_barras;
```

---

## Ejercicio Practico

Escribe el script SQL DDL para modelar una tabla `clientes` que contenga:
- `cliente_id`: Clave primaria entera autonumerica.
- `dni_cuit`: Identificador fiscal unico de longitud fija `VARCHAR(20)` y `NOT NULL`.
- `email`: Correo electronico unico y obligatorio.
- `fecha_alta`: Marca temporal con valor por defecto de la fecha del sistema (`CURRENT_TIMESTAMP`).
