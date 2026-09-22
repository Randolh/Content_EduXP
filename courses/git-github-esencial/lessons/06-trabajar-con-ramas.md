# Lección 6: Trabajar con Ramas (git branch y git switch)

En esta lección aprenderás **qué es una rama (branch)** y cómo crearla para experimentar sin arruinar tu código principal.

---

## 1. ¿Qué es una Rama?

Una rama te permite crear una línea paralela de desarrollo. Es como hacer un borrador: puedes probar cosas nuevas y si funcionan las unes al código principal, y si no, simplemente borras la rama.

* La rama principal por defecto se llama `main`.

---

## 2. Comandos para Ramas

```bash
# Ver en qué rama estás parado
git branch

# Crear una nueva rama llamada 'nueva-idea' y cambiarte a ella
git switch -c nueva-idea

# Volver a la rama principal
git switch main
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué ventaja tiene trabajar en una rama secundaria en lugar de la rama `main`?
> - [ ] Permite que el código se ejecute más rápido.
> - [x] Te permite hacer pruebas y cambios sin afectar la versión estable del proyecto.
> - [ ] Elimina la necesidad de hacer commits.
>
> **Explicación**: Las ramas aíslan las nuevas características para mantener estable el código principal.

---

## Ejercicio Práctico

Crea una rama llamada `prueba-estilos` con el comando `git switch -c prueba-estilos` y verifica con `git branch` que estés posicionado en ella.
