# Lección 11: Revertir commits de forma segura con git revert

En esta lección aprenderás a deshacer los efectos de un commit anterior en repositorios públicos o compartidos de manera segura usando **`git revert`**.

---

## 1. ¿Por qué usar `git revert` en lugar de `git reset` en GitHub?

- **`git reset`** sobrescribe y reescribe el historial de commits. Si ya publicaste los commits en GitHub (`git push`), usar `reset` romperá el historial para tus compañeros de equipo.
- **`git revert`** no altera el pasado. En su lugar, analiza los cambios de un commit problemático y genera un **nuevo commit inverso** que deshace exactamente esas modificaciones.

```bash
# Revertir un commit específico mediante su hash
git revert a1b2c3d

# Revertir el último commit realizado
git revert HEAD
```

Al ejecutar el comando, Git abrirá tu editor de texto por defecto para ingresar el mensaje del nuevo commit de reversión (ej. `Revert "Agregar función con bug"`).

---

## Autoevaluación

> [!QUIZ]
> ¿Por qué `git revert` es la opción recomendada para deshacer un commit que ya fue subido a GitHub con `git push`?
> - [ ] Porque `git revert` elimina la cuenta de GitHub si hay errores.
> - [x] Porque crea un nuevo commit en lugar de borrar el historial pasado, evitando conflictos con otros colaboradores.
> - [ ] Porque es el único comando que funciona sin internet.
>
> **Explicación**: `git revert` preserva la integridad del historial público agregando un commit seguro que revierte los cambios deseados.

---

## Ejercicio Práctico

Identifica el hash del último commit con `git log --oneline` y ejecuta `git revert HEAD` para generar un commit inverso que deshaga los últimos cambios de forma segura.
