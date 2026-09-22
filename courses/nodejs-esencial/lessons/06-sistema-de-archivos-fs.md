# Lección 6: Lectura y Escritura de Archivos (fs/promises)

En esta lección aprenderás a **leer y guardar archivos de texto** en tu computadora desde Node.js usando el módulo `fs/promises`.

---

## 1. Escribir y Leer Archivos

Node.js incluye un módulo nativo llamado `fs` (FileSystem).

```javascript
import fs from 'node:fs/promises';

// 1. Guardar texto en un archivo
await fs.writeFile('nota.txt', 'Hola, este texto fue guardado desde Node.js');

// 2. Leer el texto del archivo
const contenido = await fs.readFile('nota.txt', 'utf-8');

console.log("Contenido leído:", contenido);
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué parámetro le indica a `readFile` que convierta los bytes leídos en texto legible en español?
> - [ ] `'binary'`
> - [x] `'utf-8'`
> - [ ] `'html'`
>
> **Explicación**: El formato de codificación `'utf-8'` traduce los datos leídos a texto legible de caracteres universales.

---

## Ejercicio Práctico

Crea un script que guarde la frase `"Lista de compras: Leche, Pan, Café"` en un archivo `compras.txt` y luego lo lea por pantalla.
