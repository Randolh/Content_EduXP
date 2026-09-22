# Lección 7: Redirección de Entrada/Salida y Tuberías (|)

En esta lección aprenderás uno de los conceptos más poderosos de la filosofía Unix: **conectar programas individuales mediante redirecciones y tuberías (pipes)**.

---

## 1. Redirección de Entrada y Salida

Por defecto, los comandos reciben datos por `stdin` (teclado) e imprimen en `stdout` (pantalla). Podemos cambiar este comportamiento:

- **`>` (Redireccionar y Sobrescribir)**: Guarda la salida de un comando en un archivo (reemplazando su contenido previo).
- **`>>` (Redireccionar y Anexar)**: Agrega la salida al final del archivo sin borrar su contenido previo.

```bash
# Guardar un mensaje en un archivo (sobrescribe)
echo "Servidor iniciado" > estado.log

# Agregar una nueva línea al final del archivo (anexa)
echo "Conexión a BD establecida" >> estado.log
```

---

## 2. Tuberías (`|` - Pipes)

El operador de tubería `|` toma la **salida producida por el comando de la izquierda** y la convierte en la **entrada del comando de la derecha**.

```bash
# Listar todos los procesos y filtrarlos con grep
ps aux | grep "node"

# Mostrar las últimas 20 líneas de un log y filtrar errores
tail -n 20 servidor.log | grep -i "error"

# Contar cuántos archivos .txt existen en la carpeta
ls -1 *.txt | wc -l
```

---

## Autoevaluación

> [!QUIZ]
> ¿Cuál es la diferencia entre el operador `>` y el operador `>>` al guardar datos en un archivo?
> - [ ] `>` es para lectura y `>>` es para ejecución.
> - [x] `>` sobrescribe todo el contenido anterior del archivo, mientras que `>>` añade la nueva información al final sin borrar nada.
> - [ ] Ambas opciones hacen exactamente lo mismo.
>
> **Explicación**: `>` reinicia el archivo borrando su contenido antes de escribir, mientras que `>>` (append) concatena la nueva información al final.

---

## Ejercicio Práctico

Ejecuta `echo "Línea 1" > salida.txt`, luego `echo "Línea 2" >> salida.txt` y comprueba con `cat salida.txt` que ambas líneas existan.
