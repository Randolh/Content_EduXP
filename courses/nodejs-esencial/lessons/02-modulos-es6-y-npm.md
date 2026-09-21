# Lección 2: ES Modules, package.json y Ecosistema NPM

Para construir aplicaciones modulares y escalables en Node.js es fundamental organizar el código en múltiples archivos y aprovechar las miles de librerías disponibles en el ecosistema **NPM** (Node Package Manager). En esta lección aprenderás a configurar el soporte estándar de **ES Modules** (`import`/`export`) y a administrar tu archivo `package.json`.

---

## 1. Configuración del Proyecto y `package.json`

El archivo `package.json` es el manifiesto de cualquier proyecto Node.js. Contiene los metadatos del proyecto, la lista de dependencias instaladas y los comandos de ejecución (scripts).

### Paso 1: Inicializar un proyecto Node.js
Ejecuta el siguiente comando en tu terminal para crear un `package.json` por defecto:

```bash
mkdir mi-proyecto-node
cd mi-proyecto-node
npm init -y
```

### Paso 2: Activar ES Modules (`"type": "module"`)
Por defecto, Node.js utiliza el sistema legacy CommonJS (`require`/`module.exports`). Para utilizar la sintaxis moderna estándar de JavaScript de ES6 (`import`/`export`), debes agregar `"type": "module"` en tu `package.json`:

```json
{
  "name": "mi-proyecto-node",
  "version": "1.0.0",
  "type": "module",
  "main": "src/index.js",
  "scripts": {
    "start": "node src/index.js",
    "dev": "node --watch src/index.js"
  }
}
```

> [!NOTE]
> La bandera nativa `--watch` incluida en Node.js (v18.11+) reinicia automáticamente el servidor cada vez que guardas cambios en un archivo de tu código fuente, haciendo innecesarias herramientas externas como `nodemon`.

---

## 2. Sistema de Módulos: `import` y `export`

Los ES Modules permiten exportar e importar funciones, clases o variables entre archivos de forma limpia.

### A. Exportaciones Nombradas (Named Exports)

```javascript
// math.js - Exportación de funciones
export const sumar = (a, b) => a + b;
export const restar = (a, b) => a - b;
export const PI = 3.14159;
```

```javascript
// index.js - Importación nombrada (requiere extensión .js)
import { sumar, restar, PI } from './math.js';

console.log(`Suma: ${sumar(10, 5)}`);
console.log(`Constante PI: ${PI}`);
```

### B. Exportación por Defecto (Default Export)

```javascript
// logger.js - Exportación por defecto
export default function logMensaje(mensaje) {
  const timestamp = new Date().toISOString();
  console.log(`[${timestamp}] INFO: ${mensaje}`);
}
```

```javascript
// index.js - Importación por defecto (puedes asignarle cualquier nombre)
import logger from './logger.js';

logger('Iniciando servicios del sistema...');
```

> [!WARNING]
> Al importar archivos locales en Node.js con ES Modules, es obligatorio incluir siempre la extensión `.js` en la ruta (ej. `./math.js`), de lo contrario Node.js lanzará un error de tipo `ERR_MODULE_NOT_FOUND`.

---

## 3. Instalación de Dependencias con NPM

NPM te permite instalar librerías de terceros publicadas en la comunidad.

```bash
# Instalación de una dependencia de producción
npm install dotenv

# Instalación de una dependencia de desarrollo
npm install -D prettier
```

Esto actualizará tu `package.json` registrando las librerías en las secciones `"dependencies"` y `"devDependencies"`, y creará la carpeta `node_modules/`.

---

## 💡 Autoevaluación

> [!QUIZ]
> ¿Qué propiedad debes agregar en `package.json` para habilitar el uso nativo de `import` y `export` en Node.js?
> - [ ] `"modules": true`
> - [x] `"type": "module"`
> - [ ] `"syntax": "es6"`
>
> **Explicación**: La clave `"type": "module"` le indica a Node.js que interprete todos los archivos `.js` de ese directorio como módulos ES6 estándar.

---

## 🛠️ Ejercicio Práctico: Calculadora Modular

**Objetivo**: Crear un módulo de utilidades matemáticas e importarlo en tu script principal.

**Instrucciones**:
1. Crea una carpeta `src/`.
2. Crea el archivo `src/utils.js` que exporte una función `multiplicar(a, b)` y una función `dividir(a, b)`.
3. En `src/index.js`, importa las funciones y ejecuta operaciones de prueba capturando errores al dividir entre cero.

<details class="exercise-solution">
<summary>💡 Ver solución paso a paso</summary>

<div class="solution-content">

```javascript
// src/utils.js
export function multiplicar(a, b) {
  return a * b;
}

export function dividir(a, b) {
  if (b === 0) {
    throw new Error('No se puede dividir entre cero.');
  }
  return a / b;
}
```

```javascript
// src/index.js
import { multiplicar, dividir } from './utils.js';

try {
  console.log('Multiplicación 6 x 7:', multiplicar(6, 7));
  console.log('División 20 / 4:', dividir(20, 4));
  console.log('División 10 / 0:', dividir(10, 0));
} catch (error) {
  console.error('❌ Error capturado:', error.message);
}
```

Ejecuta el script con:
```bash
npm run start
```

</div>
</details>

---

## 📌 Resumen

- `package.json` gestiona las dependencias y scripts de tu proyecto.
- `"type": "module"` habilita los **ES Modules** modernos (`import`/`export`).
- Recuerda añadir siempre la extensión `.js` al importar módulos locales.
- En la siguiente lección aprenderás a interactuar con el sistema de archivos del sistema operativo usando `fs/promises` y `path`.
