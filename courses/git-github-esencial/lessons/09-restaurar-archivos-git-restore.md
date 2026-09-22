# Lección 9: Deshacer cambios locales con git restore

En esta lección aprenderás a utilizar el comando moderno **`git restore`** para descartar modificaciones sin confirmar en tu directorio de trabajo o remover archivos del área de preparación (staging).

---

## 1. Descartar cambios en el Directorio de Trabajo

Si modificaste un archivo localmente pero deseas regresar a la versión del último commit descartando tus cambios no guardados en Git:

```bash
# Restaurar un archivo específico al último commit guardado
git restore index.html

# Restaurar todos los archivos modificados en el directorio actual
git restore .
```

> ⚠️ **Atención**: Descartar cambios locales no guardados con `git restore` borra de forma permanente las modificaciones no confirmadas.

---

## 2. Sacar archivos del Área de Preparación (Staging Area)

Si agregaste accidentalmente un archivo al área de preparación usando `git add`, puedes "desprepararlo" (unstage) usando la opción `--staged`:

```bash
# Sacar un archivo del área de preparación sin perder tus modificaciones locales
git restore --staged config.json
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué comando debes usar para quitar un archivo del Staging Area (`git add`) manteniendo tus cambios intactos en el código fuente?
> - [ ] `git restore index.html`
> - [x] `git restore --staged index.html`
> - [ ] `git commit --delete`
>
> **Explicación**: El parámetro `--staged` le indica a Git que solo debe remover el archivo del área de preparación previa al commit, conservando el contenido del archivo en tu disco local.

---

## Ejercicio Práctico

Modifica un archivo `app.js`, agrégalo a staging con `git add app.js`, y luego ejecuta `git restore --staged app.js` verificando el estado con `git status`.
