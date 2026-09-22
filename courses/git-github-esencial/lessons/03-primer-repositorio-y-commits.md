# Lección 3: Tu Primer Repositorio (git init, add y commit)

En esta lección aprenderás a **inicializar un repositorio** y guardar tu primer punto de control (commit).

---

## 1. Inicializar un Repositorio (`git init`)

Un repositorio es la carpeta que Git estará vigilando. Para activarlo:

```bash
mkdir mi-proyecto
cd mi-proyecto
git init
```

---

## 2. Guardar Cambios (`git add` y `git commit`)

Guardar una versión requiere 2 pasos:

1. **Preparar los archivos (`git add`):** Seleccionas qué archivos formarán la foto.
   ```bash
   git add index.html
   ```
2. **Guardar la foto (`git commit`):** Registras los cambios con un mensaje explicativo.
   ```bash
   git commit -m "Mi primer commit"
   ```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué comando convierte una carpeta común en un repositorio de Git?
> - [ ] `git start`
> - [x] `git init`
> - [ ] `git new`
>
> **Explicación**: `git init` crea la carpeta oculta `.git` que almacena todo el historial del proyecto.

---

## Ejercicio Práctico

Crea una carpeta `mi-web`, inicializa Git con `git init`, crea un archivo `hola.txt` y guárdalo en el historial ejecutando `git add hola.txt` y `git commit -m "Agregar hola.txt"`.
