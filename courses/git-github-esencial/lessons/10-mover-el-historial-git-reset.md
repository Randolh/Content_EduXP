# Lección 10: Mover el historial con git reset (--soft, --mixed, --hard)

En esta lección aprenderás a rebobinar el puntero de tu rama activa a un commit pasado utilizando el comando **`git reset`** y entendiendo la diferencia crucial entre sus tres modos principales.

---

## 1. Modos de `git reset`

El comando `git reset <commit-hash>` desplaza el puntero `HEAD` hacia atrás en el historial. La forma en que trata los cambios dependera de la bandera utilizada:

### 1. `git reset --soft <commit-hash>`
Mueve el puntero al commit indicado. **Conserva todos los cambios posteriores** colocándolos directamente en el Área de Preparación (Staging Area). Ideal si deseas rehacer el mensaje de un commit o agrupar varios commits en uno solo.

### 2. `git reset --mixed <commit-hash>` (Modo por Defecto)
Mueve el puntero al commit indicado y **remueve los cambios del Staging Area**, manteniéndolos como modificaciones no guardadas en tu directorio de trabajo.

### 3. `git reset --hard <commit-hash>`
⚠️ **Peligro**: Mueve el puntero al commit indicado y **destruye de forma permanente** todas las modificaciones y commits posteriores tanto del Staging Area como del directorio de trabajo.

```bash
# Ejemplo: Rebobinar 1 commit manteniendo los cambios en Staging
git reset --soft HEAD~1

# Ejemplo: Rebobinar a un commit específico borrando todo cambio posterior
git reset --hard a1b2c3d
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué sucede al ejecutar `git reset --soft HEAD~1`?
> - [ ] Se borran todos los archivos del proyecto.
> - [x] Se deshace el último commit pero se conservan las modificaciones preparadas en el Staging Area listas para hacer un nuevo commit.
> - [ ] Se envía el código a GitHub.
>
> **Explicación**: El modo `--soft` mueve el puntero de la rama al commit anterior sin tocar los archivos modificados, dejándolos listos en staging.

---

## Ejercicio Práctico

Crea un commit de prueba, luego usa `git reset --soft HEAD~1` y verifica con `git status` que los archivos continuen en el Staging Area.
