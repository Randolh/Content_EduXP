# Lección 7: Unir Ramas de Desarrollo (git merge)

En esta lección aprenderás a **unir o fusionar los cambios** de una rama secundaria hacia la rama principal mediante `git merge`.

---

## 1. Fusionar Cambios (`git merge`)

Cuando terminaste una funcionalidad en una rama y comprobaste que todo funciona, debes traer esos cambios a `main`:

1. Cambia primero a la rama principal:
   ```bash
   git switch main
   ```
2. Ejecuta el comando de fusión indicando la rama que quieres unir:
   ```bash
   git merge prueba-estilos
   ```

Los cambios que hiciste en `prueba-estilos` ahora formarán parte de `main`.

---

## Autoevaluación

> [!QUIZ]
> Antes de ejecutar `git merge mi-rama`, ¿en qué rama debes estar posicionado?
> - [ ] En la rama `mi-rama`.
> - [x] En la rama destino (por ejemplo `main`) que va a recibir los cambios.
> - [ ] Da igual en qué rama estés.
>
> **Explicación**: `git merge` trae los cambios desde otra rama hacia la rama activa donde estás parado.

---

## Ejercicio Práctico

1. Estando en `prueba-estilos`, crea un archivo `estilos.css` y haz un commit.
2. Vuelve a `main` con `git switch main`.
3. Une la rama ejecutando `git merge prueba-estilos`.
