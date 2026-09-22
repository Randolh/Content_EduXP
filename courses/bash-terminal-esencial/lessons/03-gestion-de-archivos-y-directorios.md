# Lección 3: Crear, Copiar, Mover y Eliminar (mkdir, cp, mv, rm)

En esta lección aprenderás a administrar archivos y carpetas desde la terminal de forma rápida y eficiente.

---

## 1. Crear Directorios y Archivos

```bash
# Crear una carpeta nueva
mkdir mi_proyecto

# Crear carpetas anidadas de forma recursiva
mkdir -p proyectos/javascript/app

# Crear un archivo vacío (o actualizar su fecha de modificación)
touch notas.txt
```

---

## 2. Copiar, Mover y Renombrar

```bash
# Copiar un archivo
cp notas.txt notas_backup.txt

# Copiar un directorio entero y su contenido (modo recursivo -r)
cp -r mi_proyecto mi_proyecto_copia

# Mover un archivo a otra carpeta
mv notas.txt mi_proyecto/

# Renombrar un archivo (el comando mv también sirve para renombrar)
mv notas_backup.txt notas_v1.txt
```

---

## 3. Eliminar Elementos

```bash
# Eliminar un archivo
rm notas_v1.txt

# Eliminar una carpeta vacía
rmdir carpeta_vacia

# Eliminar un directorio con todo su contenido (modo recursivo y forzado)
rm -rf mi_proyecto_copia
```

> ⚠️ **Precaución**: `rm` elimina archivos inmediatamente **sin enviarlos a la papelera de reciclaje**. Usa `rm -rf` con precaución.

---

## Autoevaluación

> [!QUIZ]
> ¿Qué bandera debemos añadir al comando `cp` para copiar un directorio entero junto con todas sus subcarpetas?
> - [ ] `-f`
> - [x] `-r` (recursivo)
> - [ ] `-p`
>
> **Explicación**: La opción `-r` o `-R` (recursiva) le indica al comando que debe procesar el directorio objetivo y todos sus subdirectorios y archivos internos.

---

## Ejercicio Práctico

Crea una carpeta llamada `prueba_bash`, crea un archivo `demo.txt` dentro de ella, y luego renómbralo a `ejemplo.txt`.
