# 1. Instalacion de Python 3.12+, Entorno en VS Code y Primer Script

Python 3.12+ es el estandar tecnologico actual en areas criticas como desarrollo de servicios web backend, ingenieria de datos, aprendizaje automatico y automatizacion de infraestructuras en la nube. En esta leccion prepararas un entorno de ejecucion limpio y profesional.

---

## Objetivos de la Leccion
- Descargar e instalar Python 3.12 o superior verificando las rutas del PATH del sistema.
- Configurar Visual Studio Code con el interprete oficial y la extension de Microsoft.
- Diferenciar el modo interactivo REPL de la ejecucion de scripts mediante la terminal.
- Comprender las reglas cardinales de sintaxis de Python: sangria formal y comentarios.

---

## Proceso de Instalacion por Plataforma

### Windows 10 / 11
1. Descarga el paquete instalador oficial x64 desde python.org.
2. Ejecuta el instalador con privilegios de administrador.
3. **Requisito critico:** Activa la casilla de verificacion **"Add python.exe to PATH"** antes de presionar el boton de instalacion.
4. Finalizada la instalacion, presiona la opcion "Disable path length limit" para evitar truncamientos de rutas profundas.

### macOS (Homebrew)
En sistemas macOS, utiliza el gestor de paquetes Homebrew para evitar interferir con el interprete base del sistema operativo:
```bash
brew update
brew install python@3.12
```

### Linux (Distribuciones Debian / Ubuntu)
```bash
sudo apt update
sudo apt install python3.12 python3.12-venv python3-pip -y
```

### Verificacion en Consola
Ejecuta en tu terminal el comando de verificacion:
```bash
python --version
# O alternativamente:
python3 --version
```
La salida debe confirmar: `Python 3.12.x` (o version superior).

---

## Consola Interactiva (REPL) vs Scripts de Produccion

### 1. El Interprete Interactivo (REPL)
Al teclear `python` sin argumentos en la consola, accedes a un entorno de lectura, evaluacion e impresion inmediata:
```python
>>> 10 * 5 + 3
53
>>> import sys
>>> sys.version
'3.12.2 (main, Feb 21 2024, 10:00:00)'
>>> exit()
```
El REPL es excelente para comprobar expresiones rapidas o inspeccionar metodos, pero no conserva el codigo.

### 2. Archivos de Codigo Fuente (.py)
Para construir proyectos reales, escribimos archivos de texto plano con extension `.py` codificados en UTF-8.

Crea un archivo denominado `app.py`:
```python
# app.py - Inicializacion de ejecucion formal

def main() -> None:
    print("========================================")
    print("Sistema de Inicializacion Python 3.12+")
    print("========================================")
    
    usuario: str = input("Identificador de usuario: ")
    print(f"Sesion establecida satisfactoriamente para: {usuario}")

if __name__ == "__main__":
    main()
```

Ejecuta el script desde la terminal:
```bash
python app.py
```

---

## Reglas Estructurales de Python

A diferencia de lenguajes de la familia C (Java, C++, JavaScript) que utilizan llaves `{}` para agrupar bloques, Python utiliza **indentacion obligatoria**:
- La convencion estandar oficial (PEP 8) estipula el uso de **4 espacios en blanco** por cada nivel de anidacion.
- Mezclar tabulaciones y espacios provocara un error critico de tipo `TabError: inconsistent use of tabs and spaces in indentation`.

```python
# Ejemplo de indentacion correcta:
if 10 > 5:
    print("Primer nivel de indentacion (4 espacios)")
    if True:
        print("Segundo nivel de indentacion (8 espacios)")
```

---

## Ejercicio Practico

Crea un script llamado `diagnostico_entorno.py` que importe los modulos nativos `sys` y `platform`, e imprima en consola:
1. La version exacta de Python en ejecucion.
2. El sistema operativo anfitrion (nombre de la arquitectura y version del kernel).
3. La ruta absoluta del ejecutable de Python en tu disco duro (`sys.executable`).
