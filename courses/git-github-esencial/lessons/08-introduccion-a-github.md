# Lección 8: Conectar tu Repositorio con GitHub (git push)

En esta lección final aprenderás **qué es GitHub** y cómo enviar los commits de tu computadora a la nube mediante `git push`.

---

## 1. ¿Qué es GitHub?

Mientras que **Git** es la herramienta que corre en tu computadora, **GitHub** es una página web que almacena y respalda tus repositorios en la nube. Te permite tener copias de seguridad y compartir tu código con el mundo.

---

## 2. Enviar Cambios a GitHub (`git push`)

Una vez creado tu repositorio en la página de GitHub:

1. Vinculas la dirección web del servidor con el nombre de alias `origin`:
   ```bash
   git remote add origin https://github.com/tu-usuario/mi-proyecto.git
   ```
2. Envías tus commits locales a la nube:
   ```bash
   git push -u origin main
   ```

¡Felicidades! Tu código ahora está respaldado de forma segura en GitHub.

---

## Autoevaluación

> [!QUIZ]
> ¿Qué comando se utiliza para enviar los commits de tu repositorio local hacia GitHub?
> - [ ] `git pull`
> - [x] `git push`
> - [ ] `git upload`
>
> **Explicación**: `git push` empuja las confirmaciones locales al servidor remoto.

---

## Ejercicio Práctico Final

Crea una cuenta gratuita en [github.com](https://github.com), crea un repositorio nuevo vacío y sigue las instrucciones para vincular tu repositorio local con `git remote add origin` y enviar tus cambios con `git push`.
