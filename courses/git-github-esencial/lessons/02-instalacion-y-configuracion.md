# Lección 2: Instalación de Git y Configuración Inicial (git config)

En esta lección aprenderás **exclusivamente a instalar Git** en tu sistema operativo y a configurar tu nombre y correo electrónico.

---

## 1. Instalación de Git

Descarga e instala Git según tu sistema:
* **Windows:** Descarga el instalador desde [git-scm.com](https://git-scm.com).
* **Mac:** Abre la terminal y escribe `git --version`. Si no está instalado, te guiará para instalarlo.
* **Linux:** Abre la consola y ejecuta `sudo apt install git`.

Para comprobar que se instaló correctamente, abre la terminal y escribe:
```bash
git --version
```

---

## 2. Configurar tu Identidad (`git config`)

Git necesita saber quién realiza cada cambio. Configura tu nombre y correo con estos dos comandos:

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu_correo@ejemplo.com"
```

> [!NOTE]
> Utiliza el mismo correo electrónico con el que te registrarás más adelante en GitHub.

---

## Autoevaluación

> [!QUIZ]
> ¿Qué comando debes ejecutar para verificar qué versión de Git tienes instalada?
> - [ ] `git start`
> - [x] `git --version`
> - [ ] `git help install`
>
> **Explicación**: `git --version` muestra la versión instalada en tu sistema.

---

## Ejercicio Práctico

Abre tu terminal, configura tu nombre y correo globalmente, y luego ejecuta `git config --list` para verificar que tus datos se hayan guardado.
