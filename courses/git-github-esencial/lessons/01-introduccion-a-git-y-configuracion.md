# Lección 1: Introducción a Git, Configuración Global y Estados del Repositorio

Bienvenido al curso de **Git y GitHub**. En esta primera lección aprenderás qué es un sistema de control de versiones distribuido, cómo instalar y preparar tu entorno de trabajo en Windows, macOS o Linux, cómo configurar tus credenciales globales y cómo mover archivos entre los tres estados fundamentales de un repositorio local.

---

## 1. ¿Qué es el Control de Versiones y por qué usar Git?

Un **Sistema de Control de Versiones (VCS)** es una herramienta que registra los cambios realizados en un conjunto de archivos a lo largo del tiempo. Esto te permite:

* Revertir archivos o proyectos enteros a estados anteriores.
* Comparar cambios a lo largo del tiempo.
* Identificar quién introdujo una modificación o un error.
* Trabajar en paralelo con múltiples desarrolladores sin sobrescribir el trabajo de otros.

**Git** es un VCS **distribuido** creado por Linus Torvalds en 2005. A diferencia de los sistemas centralizados (como Subversion), cada desarrollador tiene una copia completa y local de todo el historial del repositorio en su propia máquina.

```text
[ Mi Máquina (Copia completa del historial) ] ◄── Sync ──► [ Servidor GitHub (Copia remota) ]
```

> [!NOTE]
> Git funciona completamente sin conexión a Internet. Solo necesitas conexión a red cuando vas a sincronizar tu trabajo con un servidor remoto como GitHub.

---

## 2. Instalación de Git y Preparación del Entorno

Antes de comenzar a rastrear tus proyectos, debes verificar o instalar Git en tu sistema operativo:

### A. Instalación según tu Sistema Operativo

1. **Windows:**
   * Descarga el instalador desde [git-scm.com](https://git-scm.com/download/win).
   * Al instalar, asegúrate de mantener marcada la opción de instalar **Git Bash** (una terminal basada en UNIX ideal para ejecutar comandos de Git).

2. **macOS:**
   * Abre la terminal y ejecuta `git --version`. Si no está instalado, macOS te solicitará instalar las **Xcode Command Line Tools**.
   * O puedes instalarlo mediante Homebrew: `brew install git`.

3. **Linux (Ubuntu / Debian / Fedora):**
   ```bash
   # Debian / Ubuntu
   sudo apt update && sudo apt install -y git
   
   # Fedora
   sudo dnf install git
   ```

### B. Verificación de la Instalación

Abre tu consola de comandos o Git Bash y verifica que Git responda correctamente:

```bash
git --version
# Ejemplo de salida: git version 2.43.0
```

---

## 3. Configuración Inicial de Git (`git config`)

Antes de realizar tu primer commit, debes identificarte en Git con tu nombre y correo electrónico. Estos datos quedarán grabados de forma permanente en cada cambio que realices.

Abre tu terminal y ejecuta los siguientes comandos:

```bash
# Configurar tu nombre global
git config --global user.name "Tu Nombre"

# Configurar tu correo electrónico (mismo correo de GitHub)
git config --global user.email "tu_email@ejemplo.com"

# Definir 'main' como el nombre predeterminado de la rama principal
git config --global init.defaultBranch main

# Verificar la configuración actual
git config --list
```

---

## 4. Los 3 Estados de Git

Para dominar Git debes comprender los tres estados en los que puede estar cualquier archivo dentro de tu proyecto:

1. **Working Directory (Directorio de Trabajo):** La carpeta local donde estás editando tus archivos.
2. **Staging Area (Área de Preparación / Index):** Un área intermedia donde preparas los cambios que formarán parte de la próxima "fotografía" o commit.
3. **Repository / Git Directory (.git):** La base de datos donde Git almacena de forma permanente las capturas fijas de tu proyecto.

```text
[ Working Directory ]  ── (git add) ──►  [ Staging Area ]  ── (git commit) ──►  [ Git Repository (.git) ]
```

### Comandos Clave del Flujo Local:

* `git init`: Inicializa un nuevo repositorio Git en el directorio actual (crea la carpeta oculta `.git`).
* `git status`: Muestra el estado actual de los archivos (modificados, en staging o no rastreados).
* `git add <archivo>`: Mueve cambios del Working Directory al Staging Area.
* `git commit -m "Mensaje"`: Guarda los cambios preparados en el Staging Area permanentemente en el historial.

---

## Autoevaluación

> [!QUIZ]
> ¿Cuál es el propósito del Staging Area en Git?
> - [ ] Subir automáticamente el código al servidor remoto de GitHub.
> - [x] Funcionar como una zona intermedia donde seleccionamos específicamente qué archivos formarán parte del próximo commit.
> - [ ] Comprimir las imágenes del proyecto antes de guardarlas.
>
> **Explicación**: El Staging Area te da control total para decidir exactamente qué modificaciones incluir en una confirmación (commit), permitiendo organizar commits pequeños y atómicos.

---

## Ejercicio Práctico: Tu Primer Repositorio Local

**Objetivo**: Verificar la instalación de Git, inicializar un repositorio local, crear un archivo, añadirlo al Staging Area y realizar tu primer commit.

**Instrucciones**:
1. Verifica tu versión de Git con `git version`.
2. Crea una carpeta llamada `mi-primer-repo` e ingresa a ella desde la terminal.
3. Inicializa el repositorio con `git init`.
4. Crea un archivo `index.html` con un texto simple.
5. Consulta el estado con `git status`.
6. Agrega el archivo al staging area y confirma los cambios con un commit.

<details class="exercise-solution">
<summary>Ver solución paso a paso</summary>

<div class="solution-content">

```bash
# 1. Verificar instalacion
git --version

# 2. Crear carpeta y navegar a ella
mkdir mi-primer-repo
cd mi-primer-repo

# 3. Inicializar repositorio Git
git init

# 4. Crear archivo de prueba
echo "<h1>Hola Mundo con Git</h1>" > index.html

# 5. Verificar estado (aparecerá como Untracked)
git status

# 6. Mover al Staging Area
git add index.html

# 7. Confirmar cambios con un mensaje descriptivo
git commit -m "feat: agregar pagina principal index.html"
```

</div>
</details>
