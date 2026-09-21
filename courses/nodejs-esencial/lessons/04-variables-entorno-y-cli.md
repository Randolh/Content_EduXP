# Lección 4: Variables de Entorno, `dotenv` y Scripts CLI de Consola

¡Felicitaciones por llegar a la lección final del curso de **Node.js Fundamentos**! En esta lección aprenderás dos conceptos cruciales para el desarrollo profesional de software: la protección de datos sensibles (claves, puertos y credenciales) utilizando **variables de entorno** y la creación de herramientas de línea de comandos (**CLI**) mediante `process.argv`.

---

## 1. Manejo de Variables de Entorno y `dotenv`

Nunca debes escribir credenciales secretas (como contraseñas de bases de datos o claves API) directamente en el código fuente. Las **variables de entorno** permiten configurar el comportamiento del servidor dependiendo del entorno donde se ejecute (desarrollo, pruebas o producción).

### Paso 1: Instalar `dotenv`
```bash
npm install dotenv
```

### Paso 2: Crear el archivo `.env` en la raíz del proyecto
Crea un archivo oculto `.env`:

```env
PORT=4000
NODE_ENV=development
API_SECRET_KEY=clave_super_secreta_123
```

> [!WARNING]
> Añade siempre el archivo `.env` a tu `.gitignore` para asegurarte de nunca subir contraseñas o datos sensibles a repositorios públicos de GitHub.

### Paso 3: Cargar las variables en tu aplicación
```javascript
import dotenv from 'dotenv';

// Cargar las variables declaradas en .env a process.env
dotenv.config();

const puerto = process.env.PORT || 3000;
const ambiente = process.env.NODE_ENV || 'production';

console.log(`🚀 Servidor configurado en el puerto ${puerto} [Entorno: ${ambiente}]`);
```

---

## 2. Lectura de Argumentos de Línea de Comandos (`process.argv`)

Cuando ejecutas un script desde la terminal enviándole parámetros adicionales:

```bash
node cli.js --buscar "producto"
```

Node.js expone esos argumentos en el arreglo global `process.argv`:

* `process.argv[0]`: Ruta absoluta del ejecutable de Node.js.
* `process.argv[1]`: Ruta absoluta de tu archivo script (`cli.js`).
* `process.argv[2...]`: Todos los parámetros adicionales ingresados por el usuario.

### Ejemplo de Procesamiento de Argumentos:

```javascript
// cli.js
const argumentos = process.argv.slice(2);

if (argumentos.length === 0) {
  console.log('⚠️ Por favor ingresa una acción. Ejemplo: node cli.js --saludar Alexis');
  process.exit(1);
}

const comando = argumentos[0];
const valor = argumentos[1] || 'Invitado';

if (comando === '--saludar') {
  console.log(`👋 ¡Hola, ${valor}! Bienvenido a la herramienta CLI.`);
} else {
  console.log(`❌ Comando no reconocido: ${comando}`);
}
```

---

## 💡 Autoevaluación

> [!QUIZ]
> ¿Qué objeto global de Node.js contiene el mapa con todas las variables de entorno disponibles en el sistema?
> - [ ] `process.variables`
> - [x] `process.env`
> - [ ] `global.env`
>
> **Explicación**: El objeto `process.env` almacena todas las claves y valores definidos en el entorno del sistema operativo y en el archivo `.env` tras llamar a `dotenv.config()`.

---

## 🛠️ Ejercicio Final Integrador del Curso: Herramienta CLI de Análisis JSON

**Objetivo**: Construir una herramienta de línea de comandos que lea un archivo JSON del disco duro e imprima estadísticas del contenido.

**Instrucciones**:
1. El script debe ejecutarse como `node analizar.js ruta/al/archivo.json`.
2. Debe validar si se proporcionó la ruta del archivo.
3. Si el archivo existe y es válido, debe imprimir cuántos elementos contiene el arreglo principal.

<details class="exercise-solution">
<summary>💡 Ver solución completa del proyecto</summary>

<div class="solution-content">

```javascript
// analizar.js
import fs from 'node:fs/promises';
import path from 'node:path';
import dotenv from 'dotenv';

dotenv.config();

async function ejecutarAnalisis() {
  const argumentos = process.argv.slice(2);
  const nombreArchivo = argumentos[0];

  if (!nombreArchivo) {
    console.error('❌ Error: Debe especificar la ruta del archivo JSON.');
    console.log('Uso: node analizar.js <nombre-archivo.json>');
    process.exit(1);
  }

  const rutaAbsoluta = path.join(process.cwd(), nombreArchivo);

  try {
    const contenido = await fs.readFile(rutaAbsoluta, 'utf-8');
    const datos = JSON.parse(contenido);

    console.log('====================================');
    console.log(`📊 REPORTE DE ANÁLISIS: ${nombreArchivo}`);
    console.log('====================================');

    if (Array.isArray(datos)) {
      console.log(`✅ El archivo contiene un Arreglo de ${datos.length} elementos.`);
    } else if (typeof datos === 'object') {
      console.log(`✅ El archivo contiene un Objeto con ${Object.keys(datos).length} propiedades.`);
    }

  } catch (error) {
    console.error(`❌ Error al procesar '${nombreArchivo}':`, error.message);
  }
}

ejecutarAnalisis();
```

Prueba la herramienta ejecutando:
```bash
node analizar.js package.json
```

</div>
</details>

---

## 🏆 Resumen del Curso Node.js Esencial

¡Felicidades! Has completado el curso de **Node.js Esencial**. Ahora dominas:
- La arquitectura asíncrona del **Event Loop**.
- El sistema de módulos modernos **ES6** (`import`/`export`) y `package.json`.
- La manipulación segura del sistema de archivos con `fs/promises` y `path`.
- La configuración con `dotenv` y el desarrollo de utilidades CLI.

¡Estás listo para continuar con el siguiente curso: **Creación de APIs REST con Express y Bases de Datos**!
