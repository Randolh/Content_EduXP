# Lección 4: Módulos en Node.js (import y export)

En esta lección aprenderás **exclusivamente a dividir tu código en varios archivos** usando la sintaxis moderna de ES Modules (`import` y `export`).

---

## 1. Exportar e Importar Funciones

Dividir el código en archivos pequeños mantiene tu proyecto organizado.

### Archivo 1: `matematica.js` (Exporta una función)
```javascript
export function sumar(a, b) {
  return a + b;
}
```

### Archivo 2: `main.js` (Importa la función)
```javascript
import { sumar } from './matematica.js';

console.log("Resultado:", sumar(5, 10));
```

> [!NOTE]
> Para usar `import` y `export`, debes asegurarte de colocar `"type": "module"` en tu archivo `package.json`.

---

## Autoevaluación

> [!QUIZ]
> ¿Qué palabra clave se usa para compartir una función desde un archivo hacia otros módulos?
> - [ ] `send`
> - [x] `export`
> - [ ] `share`
>
> **Explicación**: `export` expone variables o funciones para que puedan ser consumidas con `import`.

---

## Ejercicio Práctico

Crea un archivo `saludos.js` que exporte la función `obtenerSaludo(nombre)` y consumela en un archivo `index.js`.
