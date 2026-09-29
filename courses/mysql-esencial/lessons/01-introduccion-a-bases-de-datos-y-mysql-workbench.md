# 1. Modelo Relacional, RDBMS, Instalacion de MySQL 8.x y Workbench

Las bases de datos relacionales constituyen la infraestructura estandar para el almacenamiento confiable y consistente de informacion en el desarrollo backend. En este curso aprenderas a modelar, consultar y administrar bases de datos relacionales utilizando **MySQL 8.x**, el motor de bases de datos de codigo abierto mas extendido en la industria.

---

## Objetivos de la Leccion
- Comprender el concepto de Sistema de Gestion de Bases de Datos Relacionales (RDBMS).
- Identificar los componentes de un esquema: Tablas, Filas (Tuplas), Columnas (Atributos), PK y FK.
- Instalar MySQL Server 8.x y configurar clientes de conexion grafica (MySQL Workbench) y por terminal (CLI).
- Ejecutar comandos basicos de administracion y diagnostico de instancias.

---

## El Modelo Relacional de Bases de Datos

El modelo relacional organiza la informacion en **Tablas bidimensionales** conectadas entre si mediante llaves de relacion:

```text
Estructura Relacional Basica:
 ┌─────────────────────────────────────────────────────────────┐
 │                      Tabla: clientes                        │
 ├───────────┬──────────────────┬──────────────────────────────┤
 │ cliente_id│ nombre           │ email                        │
 ├───────────┼──────────────────┼──────────────────────────────┤
 │     1     │ Carlos Rivera    │ carlos@eduxp.org             │
 └─────┬─────┴──────────────────┴──────────────────────────────┘
       │ (Clave Primaria / PK)
       │
       │ (Clave Foranea / FK)
       ▼
 ┌─────────────────────────────────────────────────────────────┐
 │                      Tabla: ordenes                         │
 ├───────────┬───────────┬────────────┬────────────────────────┤
 │ orden_id  │ cliente_id│ fecha      │ total                  │
 ├───────────┼───────────┼────────────┼────────────────────────┤
 │   1001    │     1     │ 2026-09-29 │ $250.00                │
 └───────────┴───────────┴────────────┴────────────────────────┘
```

### Conceptos Clave
- **Clave Primaria (`PRIMARY KEY` / PK):** Identificador unico que garantiza que ninguna fila este duplicada. No puede contener valores nulos.
- **Clave Foranea (`FOREIGN KEY` / FK):** Columna en una tabla hija que apunta a la Clave Primaria de una tabla padre, asegurando la **Integridad Referencial**.

---

## Proceso de Instalacion de MySQL 8.x

### Instalacion en Windows
1. Descarga el paquete instalador completo desde dev.mysql.com.
2. Selecciona los componentes: `MySQL Server 8.0/8.x` y `MySQL Workbench`.
3. Configura el metodo de autenticacion con contrasena cifrada estandar (caching_sha2_password) y asigna la clave del superusuario `root`.

### Instalacion en Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install mysql-server mysql-workbench -y
sudo mysql_secure_installation
```

---

## Conexion y Primeras Sentencias en la Consola

Inicia sesion en el cliente de terminal:
```bash
mysql -u root -p
```

### Diagnostico Inicial en SQL
```sql
-- 1. Listar las bases de datos registradas en la instancia
SHOW DATABASES;

-- 2. Crear una base de datos de pruebas
CREATE DATABASE eduxp_demo;

-- 3. Seleccionar la base de datos de trabajo activa
USE eduxp_demo;

-- 4. Consultar la version exacta del motor y el usuario en sesion
SELECT VERSION(), USER();
```

---

## Ejercicio Practico

Abre tu conexion a MySQL (mediante Workbench o CLI) y ejecuta las siguientes verificaciones:
1. Inspecciona el motor de almacenamiento por defecto ejecutando `SHOW ENGINES;` y comprueba que `InnoDB` este marcado como `DEFAULT`.
2. Crea una base de datos denominada `laboratorio_sql` y confirma su existencia en el listado de `SHOW DATABASES;`.
