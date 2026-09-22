# Lección 4: Consultar el Estado y Cambios (git status)

En esta lección aprenderás **exclusivamente a revisar el estado de tu proyecto** usando `git status`.

---

## 1. El Comando `git status`

En cualquier momento puedes preguntarle a Git en qué estado están tus archivos:

```bash
git status
```

Git te dirá:
* **Untracked (No rastreados):** Archivos nuevos que Git aún no conoce.
* **Changes not staged:** Archivos modificados que aún no has preparado con `git add`.
* **Changes to be committed:** Archivos listos en el Staging Area esperando el `git commit`.

---

## Autoevaluación

> [!QUIZ]
> ¿Qué comando debes usar para saber si tienes archivos pendientes por guardar en un commit?
> - [ ] `git check`
> - [x] `git status`
> - [ ] `git list`
>
> **Explicación**: `git status` te da un reporte del estado de todos los archivos del directorio de trabajo.

---

## Ejercicio Práctico

En tu repositorio de prueba, modifica el archivo `hola.txt` agregando una línea de texto nueva. Ejecuta `git status` para observar cómo Git identifica que el archivo ha cambiado.
