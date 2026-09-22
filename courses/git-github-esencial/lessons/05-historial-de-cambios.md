# Lección 5: Inspeccionar el Historial (git log)

En esta lección aprenderás a **consultar el historial de commits** realizados mediante el comando `git log`.

---

## 1. El Comando `git log`

Para ver todas las fotos o versiones guardadas a lo largo del tiempo, ejecuta:

```bash
git log
```

Verás una lista con:
* El código identificador único (Hash SHA) de cada commit.
* El nombre del autor y su correo.
* La fecha y hora exacta en que se guardó.
* El mensaje descriptivo que escribiste.

> [!TIP]
> Si quieres ver el historial de forma más compacta (una sola línea por commit), usa:
> `git log --oneline`

---

## Autoevaluación

> [!QUIZ]
> ¿Qué información te muestra el comando `git log`?
> - [ ] La lista de archivos eliminados de tu disco duro.
> - [x] El historial completo de todos los commits guardados en el proyecto.
> - [ ] El estado de tu conexión a Internet.
>
> **Explicación**: `git log` despliega el registro histórico de confirmaciones.

---

## Ejercicio Práctico

Ejecuta `git log --oneline` en tu repositorio local para ver el resumen de los commits que has realizado hasta el momento.
