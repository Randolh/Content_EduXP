# Lección 4: Lectura e Inspección de Archivos (cat, head, tail, nano)

En esta lección aprenderás las distintas herramientas que ofrece la consola para leer, examinar y editar el contenido de archivos de texto.

---

## 1. Comandos de Inspección de Texto

```bash
# Muestra todo el contenido del archivo en la consola
cat archivo.txt

# Muestra el contenido paginado (presiona Q para salir)
less archivo_largo.txt

# Muestra únicamente las primeras 10 líneas
head archivo.txt

# Muestra únicamente las primeras 5 líneas
head -n 5 archivo.txt

# Muestra únicamente las últimas 10 líneas (ideal para logs)
tail archivo.log

# Monitorea un archivo de logs en tiempo real a medida que se escriben nuevas líneas
tail -f servidor.log
```

---

## 2. Edición Rápida con Nano

`nano` es un editor de texto por línea de comandos intuitivo disponible por defecto en la mayoría de sistemas Linux.

```bash
nano mi_script.sh
```

- Para guardar cambios en `nano`: presiona `Ctrl + O` y luego `Enter`.
- Para salir de `nano`: presiona `Ctrl + X`.

---

## Autoevaluación

> [!QUIZ]
> ¿Qué comando de terminal es el más adecuado para monitorear un archivo de registros (log) en tiempo real a medida que se producen nuevos eventos?
> - [ ] `cat servidor.log`
> - [x] `tail -f servidor.log`
> - [ ] `head -n 10 servidor.log`
>
> **Explicación**: La opción `-f` (follow) en `tail` mantiene la conexión abierta imprimiendo en pantalla cada nueva línea que se agregue al final del archivo.

---

## Ejercicio Práctico

Usa `nano prueba.txt` para escribir tres líneas de texto, guarda el archivo con `Ctrl+O` y verifica su contenido ejecutando `cat prueba.txt`.
