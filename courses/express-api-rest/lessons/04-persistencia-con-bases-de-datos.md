# Lección 4: Persistencia en Base de Datos Relacional (Connection Pool y SQL)

En aplicaciones de producción, la información debe persistir en bases de datos relacionales seguras. En esta lección aprenderás a conectar tu backend Express a una base de datos relacional (como **MySQL** o **SQLite**) utilizando un fondo de conexiones (**Connection Pool**) para optimizar el rendimiento.

---

## 1. Concepto de Connection Pool

Abrir y cerrar una conexión a la base de datos por cada petición HTTP es costoso en términos de CPU y memoria. Un **Connection Pool** mantiene un conjunto de conexiones abiertas y reutilizables en memoria.

```text
[ Peticiones HTTP ] ──► [ Connection Pool (5-10 Conexiones) ] ──► [ Base de Datos ]
```

---

## 2. Configuración del Pool de Conexiones (`src/config/db.js`)

Instalación de drivers para MySQL (o SQLite):

```bash
npm install mysql2
```

### Configuración con `mysql2/promise` (`db.js`)

```javascript
import mysql from 'mysql2/promise';
import dotenv from 'dotenv';

dotenv.config();

// Crear el Pool de conexiones reutilizables
export const dbPool = mysql.createPool({
  host: process.env.DB_HOST || 'localhost',
  user: process.env.DB_USER || 'root',
  password: process.env.DB_PASSWORD || '',
  database: process.env.DB_NAME || 'eduxp_db',
  port: Number(process.env.DB_PORT) || 3306,
  waitForConnections: true,
  connectionLimit: 10,
  queueLimit: 0
});

// Comprobar conexión al arrancar
export async function probarConexionDB() {
  try {
    const conexion = await dbPool.getConnection();
    console.log('✅ Conexión exitosa a la base de datos MySQL.');
    conexion.release(); // Liberar la conexión de vuelta al pool
  } catch (error) {
    console.error('❌ Error de conexión a la Base de Datos:', error.message);
  }
}
```

---

## 3. Integración en la Capa Modelo (`users.model.js`)

Utilizamos consultas preparadas (Placeholders `?`) para prevenir ataques de **Inyección SQL**:

```javascript
import { dbPool } from '../../config/db.js';

export const UsersModel = {
  // Buscar usuario por correo electrónico
  async findByEmail(email) {
    const query = 'SELECT id, nombre, email, password, rol FROM usuarios WHERE email = ?';
    const [rows] = await dbPool.execute(query, [email]);
    return rows[0] || null;
  },

  // Insertar un nuevo usuario
  async create({ nombre, email, password, rol = 'USER' }) {
    const query = `
      INSERT INTO usuarios (nombre, email, password, rol)
      VALUES (?, ?, ?, ?)
    `;
    const [resultado] = await dbPool.execute(query, [nombre, email, password, rol]);
    return { id: resultado.insertId, nombre, email, rol };
  },

  // Listar usuarios sin exponer el hash de contraseña
  async findAll() {
    const query = 'SELECT id, nombre, email, rol, created_at FROM usuarios';
    const [rows] = await dbPool.execute(query);
    return rows;
  }
};
```

> [!WARNING]
> Nunca concatenes variables directamente en sentencias SQL como `SELECT * FROM usuarios WHERE email = '${email}'`. Siempre utiliza sentencias preparadas con signos de interrogación `?` para evitar Inyección SQL.

---

## 💡 Autoevaluación

> [!QUIZ]
> ¿Cuál es la función principal de utilizar la sintaxis de consultas preparadas (`dbPool.execute(sql, [params])`)?
> - [ ] Comprimir las consultas para enviarlas más rápido por la red.
> - [x] Sanitizar los parámetros de entrada previniendo ataques maliciosos de Inyección SQL.
> - [ ] Crear tablas automáticas en la base de datos sin ejecutar migraciones.
>
> **Explicación**: Las consultas preparadas separan la estructura del comando SQL de los datos proporcionados por el usuario, evitando que código malicioso altere la consulta.

---

## 🛠️ Ejercicio Práctico: Implementando `UsersModel.findById`

**Objetivo**: Añadir el método `findById(id)` al modelo de usuarios.

<details class="exercise-solution">
<summary>💡 Ver solución paso a paso</summary>

<div class="solution-content">

```javascript
// Añadir en users.model.js
async findById(id) {
  const query = 'SELECT id, nombre, email, rol FROM usuarios WHERE id = ?';
  const [rows] = await dbPool.execute(query, [id]);
  return rows[0] || null;
}
```

</div>
</details>

---

## 📌 Resumen

- Un **Connection Pool** optimiza el manejo de conexiones a la base de datos.
- Utiliza siempre `dbPool.execute(query, [parametros])` para proteger tu API de **Inyección SQL**.
- Mantén las sentencias SQL aisladas exclusivamente dentro de la capa de **Modelos**.
- En la lección final aprenderás a asegurar tus endpoints mediante **JWT, Bcrypt y Control de Roles (RBAC)**.
