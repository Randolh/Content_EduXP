# Lección 9: Proyecto Final Integrador: Script de Automatización Bash

¡Felicitaciones por llegar a la lección final! En este proyecto integrador pondrás a prueba todo lo aprendido en el curso construyendo un **Script de Automatización e Inspección de Sistema en Bash** (`limpiador_y_reporte.sh`).

---

## 📋 Descripción del Proyecto

Construirás una herramienta de consola interactiva en Bash que realice las siguientes tareas automáticamente:
1. Verificar que el usuario tenga permisos adecuados de ejecución.
2. Crear un directorio de respaldo (`backup_reportes/`).
3. Escanear archivos `.log` o `.tmp` en una carpeta seleccionada, moverlos a la carpeta de respaldo o eliminarlos.
4. Generar un archivo de texto con el resumen de uso de disco y estado de memoria del sistema (`reporte_sistema.txt`).

---

## 💻 Código de Referencia para el Proyecto (`automatizar.sh`)

```bash
#!/bin/bash

# ==============================================================================
# PROYECTO FINAL: SCRIPT DE AUTOMATIZACIÓN Y REPORTE DE SISTEMA - EDUXP
# ==============================================================================

FECHA=$(date +"%Y-%m-%d_%H-%M-%S")
DIRECTORIO_BACKUP="./respaldo_$FECHA"
LOG_REPORTE="$DIRECTORIO_BACKUP/reporte_ejecucion.log"

echo "🚀 Iniciando proceso de automatización..."

# 1. Crear el directorio de respaldo
mkdir -p "$DIRECTORIO_BACKUP"
echo "[OK] Directorio creado: $DIRECTORIO_BACKUP" > "$LOG_REPORTE"

# 2. Copiar archivos de texto o configuración importantes
if [ -d "./src" ]; then
    echo "📦 Respaldando directorio src..." | tee -a "$LOG_REPORTE"
    cp -r ./src "$DIRECTORIO_BACKUP/"
fi

# 3. Generar reporte de información del sistema
echo "" >> "$LOG_REPORTE"
echo "==========================================" >> "$LOG_REPORTE"
echo " REPORTE DE SISTEMA ($FECHA)" >> "$LOG_REPORTE"
echo " Usuario actual: $(whoami)" >> "$LOG_REPORTE"
echo " Directorio actual: $(pwd)" >> "$LOG_REPORTE"
echo "==========================================" >> "$LOG_REPORTE"

# 4. Imprimir resumen en consola usando tuberías (pipes)
cat "$LOG_REPORTE"

echo "--------------------------------------------------"
echo "✅ Proceso finalizado exitosamente. Respaldo guardado en $DIRECTORIO_BACKUP"
```

---

## 🛠️ Instrucciones de Ejecución

1. Guarda el código en un archivo llamado `automatizar.sh`.
2. Otorga permisos de ejecución ejecutando:
   ```bash
   chmod +x automatizar.sh
   ```
3. Ejecuta el script desde tu consola:
   ```bash
   ./automatizar.sh
   ```

---

## 🏆 Criterios de Evaluación

1. **Estructura Correcta**: Inclusión obligatoria del Shebang `#!/bin/bash` al inicio del archivo.
2. **Permisos Ejecutables**: Uso correcto de `chmod +x`.
3. **Flujo de Salida**: Redirección correcta de mensajes a archivos de reporte (`>` y `>>`).
4. **Comandos de Consola**: Inclusión de comandos aprendidos (`mkdir`, `cp`, `whoami`, `date`, `cat`).

¡Felicidades! Has completado el curso de **Terminal y Bash Esencial** y ahora posees las herramientas para automatizar cualquier flujo de trabajo en la consola.
