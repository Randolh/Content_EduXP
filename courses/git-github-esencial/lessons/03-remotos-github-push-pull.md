# Lección 3: Conexión con GitHub, Remotos (origin), Push y Pull

Hasta este punto has trabajado exclusivamente en tu computadora local. En esta lección aprenderás a vincular tu repositorio local con **GitHub**, respaldar tu código en la nube y mantener sincronizados múltiples entornos mediante los comandos `git push`, `git fetch` y `git pull`.

---

## 1. ¿Qué es GitHub y cómo se conecta con Git?

**GitHub** es una plataforma en la nube que hospeda repositorios Git. Proporciona una interfaz gráfica para revisar código, colaborar con equipos, gestionar proyectos y automatizar despliegues (CI/CD).

```text
[ Repositorio Local (Tu PC) ] ── (git push) ──► [ GitHub (Servidor Remoto) ]
[ Repositorio Local (Tu PC) ] ◄── (git pull) ─── [ GitHub (Servidor Remoto) ]
```

### Conceptos Clave de Remotos:

* **Remote (Remoto):** Una referencia a la dirección URL donde se hospeda la copia remota del repositorio.
* **origin:** El nombre por convención que se le da al remoto principal de un proyecto.

---

## 2. Vincular un Repositorio Local con GitHub (`git remote`)

Una vez creado un repositorio vacío en la plataforma de GitHub, debes vincularlo a tu repositorio local existente:

```bash
# Vincular el repositorio remoto indicando el alias 'origin' y la URL (HTTPS o SSH)
git remote add origin https://github.com/tu-usuario/mi-primer-repo.git

# Verificar los remotos configurados
git remote -v
```

---

## 3. Subir y Descargar Cambios (`push`, `fetch` y `pull`)

### `git push` (Enviar Cambios)
Envía los commits guardados en tu repositorio local al servidor remoto:

```bash
# Subir la rama 'main' al remoto 'origin' por primera vez (-u establece el rastreo)
git push -u origin main

# En llamadas posteriores, solo necesitas ejecutar:
git push
```

### `git fetch` vs `git pull` (Recibir Cambios)
Cuando trabajas con un equipo o desde varias computadoras, el repositorio remoto recibirá nuevos commits:

* **`git fetch`:** Descarga los nuevos commits desde el remoto pero **no modifica** tus archivos locales. Te permite revisar qué cambios hay antes de unirlos.
* **`git pull`:** Descarga los cambios del remoto y realiza un `git merge` **automático** en tu rama local activa (`git pull = git fetch + git merge`).

```bash
# Descargar e integrar cambios remotos en tu rama local activa
git pull origin main
```

> [!WARNING]
> Ejecuta siempre `git pull` antes de comenzar a trabajar cada día para asegurarte de tener la versión más reciente del código de tu equipo.

---

## Autoevaluación

> [!QUIZ]
> ¿Cuál es la diferencia entre `git fetch` y `git pull`?
> - [ ] `git fetch` sube cambios a GitHub y `git pull` los borra del servidor.
> - [x] `git fetch` descarga la información del servidor sin modificar tus archivos locales, mientras que `git pull` descarga y fusiona automáticamente los cambios en tu rama actual.
> - [ ] No hay diferencia, ambos comandos realizan exactamente la misma acción.
>
> **Explicación**: `git fetch` es una operación segura que solo actualiza el historial remoto en tu máquina; `git pull` combina ese historial directamente en tus archivos de trabajo.

---

## Ejercicio Práctico: Conectar y Subir a GitHub

**Objetivo**: Simular el flujo de vinculación remota y publicar tus commits locales en GitHub.

**Instrucciones**:
1. Inspecciona la URL del remoto configurado en tu proyecto.
2. Agrega un archivo `README.md` que describa el proyecto.
3. Haz un commit local.
4. Sube la rama `main` al servidor remoto ficticio o real.

<details class="exercise-solution">
<summary>Ver solución paso a paso</summary>

<div class="solution-content">

```bash
# 1. Crear documentación del proyecto
echo "# Mi Primer Repositorio Git" > README.md
echo "Proyecto de práctica creado en el curso EduXP." >> README.md

# 2. Registrar los cambios localmente
git add README.md
git commit -m "docs: agregar README principal"

# 3. Vincular con GitHub (reemplaza con tu URL real)
git remote add origin https://github.com/usuario/mi-primer-repo.git

# 4. Enviar los cambios al remoto
git push -u origin main
```

</div>
</details>
