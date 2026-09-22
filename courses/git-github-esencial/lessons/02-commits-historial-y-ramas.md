# Lección 2: Commits, Historial (git log), Ramas y Fusiones Básicas

En esta lección aprenderás a inspeccionar la historia de tu proyecto mediante `git log` y a utilizar **ramas (branches)** para desarrollar nuevas funcionalidades de forma aislada sin afectar el código de producción.

---

## 1. Inspeccionando el Historial con `git log`

Cada vez que realizas un commit, Git genera un identificador único SHA-1 (un hash de 40 caracteres hexadecimales) que identifica esa instantánea exacta en el tiempo.

Para consultar el historial de confirmaciones de tu proyecto utiliza:

```bash
# Historial completo detallado
git log

# Historial resumido en una línea por commit
git log --oneline

# Historial gráfico con ramas y etiquetas
git log --oneline --graph --all
```

> [!TIP]
> Puedes utilizar `git diff` para ver los cambios exactos (línea por línea) introducidos entre el directorio de trabajo y el último commit o entre dos commits diferentes.

---

## 2. ¿Qué son las Ramas (Branches)?

Una **rama** en Git representa una línea independiente de desarrollo. Pensar en ramas es como pensar en universos paralelos: puedes experimentar libremente en una rama sin alterar la rama principal (`main`).

```text
       (feature/login) ──► [ Commit B1 ] ──► [ Commit B2 ]
                                              
(main) ──► [ Commit A1 ] ─────────────────────────► [ Commit A2 ]
```

### Comandos Esenciales para Ramas:

```bash
# Listar ramas existentes (* indica la rama activa)
git branch

# Crear una nueva rama
git branch feature/contacto

# Cambiar a la nueva rama
git switch feature/contacto
# (o el comando clásico: git checkout feature/contacto)

# Crear y cambiar a la rama en un solo paso
git switch -c feature/login

# Eliminar una rama local una vez fusionada
git branch -d feature/contacto
```

---

## 3. Fusión de Ramas (`git merge`)

Cuando terminas de desarrollar una característica en una rama secundaria y has verificado que funciona correctamente, debes integrar esos cambios en la rama principal (`main`).

1. Cambia a la rama destino (`main`).
2. Ejecuta el comando `git merge` indicando el nombre de la rama origen.

```bash
# Cambiar a la rama principal
git switch main

# Fusionar la rama de la funcionalidad
git merge feature/login
```

Existen dos tipos principales de fusiones:
* **Fast-Forward Merge:** Ocurre cuando la rama principal no ha recibido commits adicionales desde que se creó la rama secundaria. Git simplemente avanza el puntero.
* **Recursive / 3-Way Merge:** Ocurre cuando ambas ramas han avanzado con nuevos commits de forma independiente. Git crea un "Commit de Fusión" (Merge Commit) para unificar ambas líneas.

---

## Autoevaluación

> [!QUIZ]
> ¿Qué comando te permite crear una nueva rama llamada `feature/carrito` y cambiar a ella inmediatamente en una sola instrucción?
> - [ ] `git branch feature/carrito --switch`
> - [x] `git switch -c feature/carrito`
> - [ ] `git commit -b feature/carrito`
>
> **Explicación**: El comando `git switch -c <nombre-rama>` (o `git checkout -b <nombre-rama>`) crea la nueva rama y posiciona la cabeza de trabajo (HEAD) en ella automáticamente.

---

## Ejercicio Práctico: Creando y Fusionando Ramas

**Objetivo**: Crear una rama para una nueva funcionalidad, realizar cambios en ella y fusionarla en la rama `main`.

**Instrucciones**:
1. En tu repositorio, crea una rama llamada `feature/estilos`.
2. Cambia a esa rama y crea un archivo `styles.css`.
3. Haz un commit registrando el archivo CSS.
4. Regresa a `main` y fusiona la rama `feature/estilos`.

<details class="exercise-solution">
<summary>Ver solución paso a paso</summary>

<div class="solution-content">

```bash
# 1. Crear y cambiar a la rama feature/estilos
git switch -c feature/estilos

# 2. Crear archivo CSS
echo "body { background-color: #f4f4f4; font-family: sans-serif; }" > styles.css

# 3. Guardar en el historial de la rama
git add styles.css
git commit -m "feat: agregar estilos basicos css"

# 4. Volver a la rama principal
git switch main

# 5. Fusionar los cambios en main
git merge feature/estilos

# 6. Eliminar la rama que ya fue integrada
git branch -d feature/estilos
```

</div>
</details>
