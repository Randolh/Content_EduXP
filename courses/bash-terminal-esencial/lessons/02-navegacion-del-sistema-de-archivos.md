# Lección 2: Navegación del Sistema de Archivos (pwd, ls, cd)

En esta lección aprenderás a moverte con fluidez a través de los directorios de tu equipo utilizando los comandos de navegación esenciales.

---

## 1. Dónde estás y qué hay a tu alrededor

- **`pwd` (Print Working Directory)**: Muestra la ruta absoluta del directorio donde te encuentras actualmente.
- **`ls` (List)**: Lista los archivos y carpetas del directorio actual.

```bash
# Mostrar ruta actual
pwd

# Listar archivos visibles
ls

# Listar con detalles (permisos, tamaño, fecha de modificación)
ls -l

# Listar todos los archivos (incluyendo archivos ocultos que inician con .)
ls -la
```

---

## 2. Cambiar de Directorio con `cd`

- **Ruta Absoluta**: Especifica la ruta completa desde la raíz `/` (ej. `cd /home/usuario/Documentos`).
- **Ruta Relativa**: Especifica la ruta a partir de tu ubicación actual (ej. `cd Documentos`).

```bash
# Entrar a una carpeta
cd Documentos

# Regresar al directorio padre (subir un nivel)
cd ..

# Ir directamente a tu directorio personal (Home)
cd ~

# Regresar al directorio anterior donde estabas
cd -
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué símbolo representa tu directorio personal de usuario (Home) en la terminal?
> - [ ] `..`
> - [x] `~` (virgulilla / tilde)
> - [ ] `/`
>
> **Explicación**: El carácter `~` es un acceso directo universal al directorio home del usuario actual (ej. `/home/randolh` o `/Users/randolh`).

---

## Ejercicio Práctico

Ejecuta `pwd`, luego navega a tu directorio home con `cd ~` y lista todos los archivos ocultos usando `ls -la`.
