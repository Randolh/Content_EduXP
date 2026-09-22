# Lección 8: Variables de Entorno y tu primer Script Bash (.sh)

En esta lección aprenderás a declarar variables, consultar Variables de Entorno globales y escribir tu primer **Script ejecutable en Bash (`.sh`)**.

---

## 1. Variables en Bash

Para asignar una variable en Bash **no se deben incluir espacios** alrededor del signo igual `=`. Para leer el valor de la variable se antepone el signo `$`.

```bash
# Asignación de variables locales
NOMBRE="EduXP"
VERSION=1.0

# Lectura de la variable
echo "Bienvenido a $NOMBRE versión $VERSION"

# Variables de Entorno globales
export ENTORNO="produccion"
echo $PATH
```

---

## 2. Creación de tu primer Script Bash (`mi_script.sh`)

Un script de Bash es un archivo de texto plano que comienza obligatoriamente con la línea **`#!/bin/bash`** (Shebang), indicándole al sistema qué intérprete debe usar para ejecutar las instrucciones.

Crea el archivo `hola.sh`:

```bash
#!/bin/bash

# Este es mi primer script de automatización
USUARIO=$(whoami)
FECHA=$(date +%Y-%m-%d)

echo "=========================================="
echo " Hola $USUARIO, reporte generado el $FECHA"
echo "=========================================="
```

Para hacerlo ejecutable y correrlo:

```bash
# 1. Otorgar permisos de ejecución
chmod +x hola.sh

# 2. Ejecutar el script
./hola.sh
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué función cumple la primera línea `#!/bin/bash` (Shebang) en un script ejecutable de Bash?
> - [ ] Es un comentario decorativo.
> - [x] Indica al sistema operativo la ruta absoluta del intérprete que debe procesar las líneas de código del script.
> - [ ] Borra las variables del sistema.
>
> **Explicación**: El `#!` (Shebang) especifica el binario del sistema (como `/bin/bash` o `/usr/bin/env bash`) encargado de interpretar y ejecutar la secuencia de comandos.

---

## Ejercicio Práctico

Crea un script `saludo.sh` que defina una variable `CURSO="Bash"`, imprima un mensaje usando la variable y dale permisos `chmod +x saludo.sh` para ejecutarlo con `./saludo.sh`.
