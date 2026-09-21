# Lección 3: Manejo del Sistema de Archivos con `fs/promises` y `path`

Una de las capacidades más poderosas de **Node.js** en comparación con JavaScript en el navegador es la habilidad de interactuar directamente con el sistema de archivos del servidor (crear, leer, editar y eliminar archivos y carpetas). En esta lección aprenderás a utilizar los módulos nativos `node:fs/promises` y `node:path`.

---

## 1. Construcción Segura de Rutas con `node:path`

Los sistemas operativos utilizan diferentes separadores de carpetas (Linux y macOS usan `/`, mientras que Windows usa `\`). El módulo nativo `node:path` resuelve estas diferencias de forma automática.

```javascript
import path from 'node:path';

// Unir carpetas de forma multiplataforma
const rutaArchivo = path.join(process.cwd(), 'datos', 'usuarios.json');

console.log('Ruta absoluta generada:', rutaArchivo);
console.log('Nombre del archivo:', path.basename(rutaArchivo));
console.log('Extensión del archivo:', path.extname(rutaArchivo));
```

> [!TIP]
> Utiliza prefijos como `node:path` y `node:fs` al importar módulos nativos de Node.js. Esto mejora la claridad de la lectura y evita posibles conflictos de nombres con paquetes externos instalados en `node_modules`.

---

## 2. Lectura y Escritura Asíncrona con `node:fs/promises`

El submódulo `node:fs/promises` expone todas las operaciones del sistema de archivos mediante **Promesas**, permitiendo utilizar la sintaxis moderna `async/await`.

### A. Escribir un archivo JSON (`writeFile`)

```javascript
import fs from 'node:fs/promises';
import path from 'node:path';

async function guardarReporte() {
  try {
    const datos = {
      servidor: 'Node-Production-01',
      estado: 'Activo',
      fecha: new Date().toISOString()
    };

    const ruta = path.join(process.cwd(), 'reporte.json');
    
    // Convertir objeto JS a string JSON formateado
    const contenidoJSON = JSON.stringify(datos, null, 2);
    
    await fs.writeFile(ruta, contenidoJSON, 'utf-8');
    console.log('✅ Archivo reporte.json guardado con éxito.');
  } catch (error) {
    console.error('❌ Error al escribir el archivo:', error.message);
  }
}

guardarReporte();
```

### B. Leer y parsear un archivo JSON (`readFile`)

```javascript
import fs from 'node:fs/promises';
import path from 'node:path';

async function cargarReporte() {
  try {
    const ruta = path.join(process.cwd(), 'reporte.json');
    
    // Leer el contenido en formato texto utf-8
    const contenidoTexto = await fs.readFile(ruta, 'utf-8');
    
    // Convertir el texto JSON a objeto JS
    const datosObj = JSON.parse(contenidoTexto);
    
    console.log('📊 Datos leídos del archivo:');
    console.log(`Servidor: ${datosObj.servidor} | Estado: ${datosObj.estado}`);
  } catch (error) {
    console.error('❌ Error al leer el archivo:', error.message);
  }
}

cargarReporte();
```

---

## 3. Verificar Existencia de Directorios y Archivos

Para evitar que tu aplicación falle al intentar leer un archivo que no existe, puedes utilizar `fs.access` o inspeccionar directorios con `fs.mkdir` y `fs.readdir`.

```javascript
async function asegurarDirectorio(nombreCarpeta) {
  const rutaCarpeta = path.join(process.cwd(), nombreCarpeta);
  try {
    // recursive: true evita que falle si la carpeta ya existe
    await fs.mkdir(rutaCarpeta, { recursive: true });
    console.log(`📁 Carpeta '${nombreCarpeta}' lista para usarse.`);
  } catch (error) {
    console.error('Error al crear carpeta:', error.message);
  }
}
```

---

## 💡 Autoevaluación

> [!QUIZ]
> ¿Por qué es una mala práctica concatenar rutas manualmente usando strings como `'carpetas/' + 'archivo.txt'`?
> - [ ] Porque Node.js solo acepta rutas codificadas en formato Base64.
> - [x] Porque los separadores de ruta varían entre sistemas operativos (barra diagonal en Linux/macOS y barra invertida en Windows).
> - [ ] Porque las cadenas de texto no soportan caracteres especiales en nombres de archivo.
>
> **Explicación**: El módulo `node:path` y su método `path.join()` se encargan de utilizar automáticamente el separador correcto según el sistema operativo en el que se esté ejecutando el servidor.

---

## 🛠️ Ejercicio Práctico: Registrador de Logs de Auditoría

**Objetivo**: Crear una función asíncrona que agregue (append) entradas de registro a un archivo `app.log`.

**Instrucciones**:
1. Utiliza `fs.appendFile` del módulo `node:fs/promises`.
2. Cada línea guardada debe incluir la fecha en formato ISO y el mensaje de log.

<details class="exercise-solution">
<summary>💡 Ver solución paso a paso</summary>

<div class="solution-content">

```javascript
import fs from 'node:fs/promises';
import path from 'node:path';

async function registrarLog(nivel, mensaje) {
  const rutaLog = path.join(process.cwd(), 'app.log');
  const timestamp = new Date().toISOString();
  const lineaLog = `[${timestamp}] [${nivel.toUpperCase()}]: ${mensaje}\n`;

  try {
    await fs.appendFile(rutaLog, lineaLog, 'utf-8');
    console.log('📝 Log registrado.');
  } catch (error) {
    console.error('Error al escribir log:', error);
  }
}

// Pruebas
await registrarLog('info', 'Usuario inició sesión exitosamente');
await registrarLog('warn', 'Intento de acceso fallido desde IP 192.168.1.50');
```

</div>
</details>

---

## 📌 Resumen

- Usa siempre `node:path` para construir rutas de archivos compatibles entre Windows, Linux y macOS.
- Utiliza `node:fs/promises` con `async/await` para operaciones no bloqueantes del sistema de archivos.
- `JSON.stringify()` convierte objetos JS a texto JSON para guardar, y `JSON.parse()` revierte el proceso al leer.
- En la siguiente lección aprenderás a gestionar variables de entorno y crear scripts interactivos de consola (CLI).
