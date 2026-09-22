# Lección 6: Búsqueda y Filtrado de Texto (grep, find, wildcard)

En esta lección aprenderás a encontrar rápidamente archivos y cadenas de texto dentro de tu sistema usando **`grep`**, **`find`** y caracteres comodín (**wildcards**).

---

## 1. Caracteres Comodín (Wildcards)

- **`*`**: Coincide con cero o más caracteres. (ej. `*.js` selecciona todos los archivos JavaScript).
- **`?`**: Coincide con exactamente un carácter. (ej. `foto?.jpg` coincide con `foto1.jpg`, `fotoA.jpg`).

```bash
# Listar todos los archivos que terminen en .md
ls *.md
```

---

## 2. Filtrado de Contenido en Texto con `grep`

`grep` busca coincidencias de patrones dentro del contenido de uno o varios archivos.

```bash
# Buscar la palabra "error" dentro de un archivo de logs (sensible a mayúsculas)
grep "error" servidor.log

# Buscar la palabra ignorando mayúsculas/minúsculas (insensible -i)
grep -i "error" servidor.log

# Buscar de forma recursiva (-r) en todos los archivos del directorio actual
grep -r "TODO" src/

# Mostrar el número de línea donde ocurrió la coincidencia (-n)
grep -n "puerto" config.js
```

---

## 3. Localizar Archivos con `find`

`find` busca archivos en el árbol de directorios basándose en el nombre, tipo, tamaño o fecha.

```bash
# Buscar archivos por nombre en la carpeta actual
find . -name "*.png"

# Buscar ignorando mayúsculas/minúsculas (-iname)
find . -iname "readme.md"

# Buscar únicamente directorios (-type d)
find . -type d -name "node_modules"
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué bandera debemos usar con `grep` para buscar un texto ignorando si está escrito en mayúsculas o minúsculas?
> - [ ] `-r`
> - [x] `-i` (ignore case)
> - [ ] `-v`
>
> **Explicación**: El parámetro `-i` le indica a `grep` que realice una búsqueda insensible a mayúsculas y minúsculas (case-insensitive).

---

## Ejercicio Práctico

Usa `grep -i "react" package.json` o crea un archivo de texto e inspecciona cuántas veces aparece una palabra usando `grep -n`.
