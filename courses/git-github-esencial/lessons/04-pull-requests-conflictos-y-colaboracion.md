# Lección 4: Pull Requests, Resolución de Conflictos y Buenas Prácticas

En esta lección final dominarás el trabajo colaborativo en equipo mediante **Forks**, **Pull Requests (PR)**, revisiones de código en GitHub y el manejo profesional de **conflictos de fusión** (merge conflicts).

---

## 1. Flujo de Colaboración con Pull Requests

Un **Pull Request (PR)** es una solicitud que haces a los mantenedores de un repositorio para integrar tus cambios de una rama secundaria hacia la rama principal.

### Flujo Estándar de Trabajo en Equipo:

1. **Crear una rama de trabajo:** `git switch -c feature/nueva-vista`
2. **Realizar commits pequeños y claros:** `git commit -m "feat: agregar formulario"`
3. **Subir la rama a GitHub:** `git push origin feature/nueva-vista`
4. **Abrir el Pull Request:** Entrar a GitHub y presionar "Compare & Pull Request".
5. **Revisión de código (Code Review):** Los compañeros comentan, aprueban o piden correcciones.
6. **Fusión (Merge PR):** El código se integra a `main` mediante la interfaz de GitHub.

```text
[ Tu Rama Local ] ──► [ Push a GitHub ] ──► [ Pull Request ] ──► [ Review & Merge a Main ]
```

---

## 2. Resolución de Conflictos de Fusión (Merge Conflicts)

Un **conflicto** ocurre cuando dos desarrolladores modifican **la misma línea del mismo archivo** en dos ramas distintas, o cuando uno borra un archivo que el otro editó. Git no puede decidir automáticamente qué cambio conservar y solicita intervención humana.

```text
<<<<<<< HEAD (Tu cambio en la rama actual)
const puerto = 3000;
=======
const puerto = 8080;
>>>>>>> feature/servidor (Cambio entrante de la otra rama)
```

### Pasos para Resolver un Conflicto:

1. Identifica los archivos en conflicto utilizando `git status`.
2. Abre los archivos marcados y decide qué código mantener, eliminando los marcadores `<<<<<<<`, `=======` y `>>>>>>>`.
3. Guarda el archivo corregido.
4. Prepara el archivo con `git add <archivo-corregido>`.
5. Finaliza la fusión con `git commit`.

> [!TIP]
> Los editores modernos como **VS Code** muestran botones interactivos (*Accept Current Change*, *Accept Incoming Change*, *Accept Both*) para resolver conflictos con un solo clic.

---

## 3. Convención de Mensajes de Commit (Conventional Commits)

Mantener un historial de cambios legible es fundamental para proyectos profesionales. Se recomienda utilizar el estándar de **Conventional Commits**:

* `feat: ...` : Una nueva característica o funcionalidad.
* `fix: ...` : Corrección de un error o bug.
* `docs: ...` : Cambios en la documentación (README, comentarios).
* `refactor: ...` : Reestructuración de código sin cambiar su comportamiento.
* `test: ...` : Adición o modificación de pruebas unitarias.

---

## Autoevaluación

> [!QUIZ]
> ¿Qué debes hacer inmediatamente después de editar un archivo para resolver las marcas de conflicto (`<<<<<<<`, `=======`, `>>>>>>>`)?
> - [ ] Borrar el directorio `.git` y clonar el repositorio de nuevo.
> - [x] Marcar el archivo como resuelto con `git add` y concluir la fusión ejecutando `git commit`.
> - [ ] Ejecutar `git push --force` inmediatamente para sobrescribir GitHub.
>
> **Explicación**: El comando `git add` le indica a Git que el conflicto en ese archivo ha sido resuelto manualmente. Luego, `git commit` registra la confirmación de la fusión.

---

## Ejercicio Práctico: Simulación de Conflicto y Resolución

**Objetivo**: Provocar intencionalmente un conflicto entre dos ramas y resolverlo manualmente.

**Instrucciones**:
1. En `main`, edita la primera línea de `README.md` y haz un commit.
2. Crea una rama `feature/doc-actualizada`, cambia la primera línea de `README.md` a un texto distinto y haz un commit.
3. Intenta fusionar `feature/doc-actualizada` en `main` para generar el conflicto.
4. Abre `README.md`, resuelve el conflicto conservando la mejor versión y completa el commit de fusión.

<details class="exercise-solution">
<summary>Ver solución paso a paso</summary>

<div class="solution-content">

```bash
# 1. Cambiar linea en main
echo "Título de la app en Main" > README.md
git add README.md
git commit -m "docs: actualizar titulo desde main"

# 2. Crear rama secundaria y cambiar la misma linea
git switch -c feature/doc-actualizada
echo "Título de la app en Feature Branch" > README.md
git add README.md
git commit -m "docs: actualizar titulo desde feature branch"

# 3. Regresar a main e intentar fusionar (generara conflicto)
git switch main
git merge feature/doc-actualizada

# 4. Editar README.md manualmente para dejar la version final deseada:
# "Título Profesional de la Aplicación (Resuelto)"

# 5. Marcar conflicto resuelto y finalizar merge
git add README.md
git commit -m "fix: resolver conflicto de fusion en README.md"
```

</div>
</details>
