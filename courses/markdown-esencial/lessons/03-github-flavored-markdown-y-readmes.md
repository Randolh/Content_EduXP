# Lección 3: GitHub Flavored Markdown (GFM) y Estructura de READMEs Profesionales

En esta lección final dominarás las extensiones avanzadas de **GitHub Flavored Markdown (GFM)** como alertas decorativas, listas de tareas interactivas y componentes HTML desplegables, así como la estructura estándar de un archivo **README.md** profesional.

---

## 1. Extensiones de GitHub Flavored Markdown (GFM)

GFM es una variante estandarizada de Markdown creada por GitHub que añade características avanzadas para el desarrollo de software.

### Listas de Tareas (Task Lists)
Ideal para dar seguimiento a pendientes en Issues, Pull Requests o tableros de proyectos:

```markdown
- [x] Diseñar el prototipo en Figma
- [x] Configurar la base de datos PostgreSQL
- [ ] Desarrollar la autenticación con JWT
- [ ] Desplegar en producción
```

### Llamadas de Atención / Alertas de GitHub (Callouts)
Permiten resaltar información crítica con colores e iconos integrados:

```markdown
> [!NOTE]
> Información útil o contexto de fondo para el lector.

> [!TIP]
> Consejos de optimización o mejores prácticas recomendadas.

> [!IMPORTANT]
> Requisitos esenciales que el usuario no debe pasar por alto.

> [!WARNING]
> Advertencias sobre cambios drásticos o posibles incompatibilidades.

> [!CAUTION]
> Acciones de alto riesgo que podrían causar pérdida de datos.
```

---

## 2. Elementos HTML Permitidos en Markdown

Markdown permite la combinación con sintaxis HTML pura para lograr efectos avanzados de interfaz:

### Secciones Desplegables (`<details>` y `<summary>`)

```html
<details>
  <summary>Haz clic aquí para ver instrucciones avanzadas</summary>
  <p>Este contenido permanece oculto hasta que el usuario expande la sección.</p>
</details>
```

---

## 3. Anatomía de un README.md Profesional

Un archivo **README.md** es la carta de presentación de cualquier repositorio de código. Debe responder rápidamente a las preguntas: ¿Qué hace este proyecto?, ¿Cómo se instala? y ¿Cómo se usa?

### Estructura Recomendada:

1. **Título e Insignias (Badges):** Nombre del proyecto y estados de build/licencia.
2. **Descripción Concisa:** 2 a 3 oraciones explicando el propósito del proyecto.
3. **Características Principales:** Lista con los puntos fuertes.
4. **Prerrequisitos e Instalación:** Comandos exactos para clonar y ejecutar.
5. **Ejemplos de Uso:** Snippet rápido mostrando cómo funciona.
6. **Licencia y Contribución:** Reglas para que otros participen.

---

## Autoevaluación

> [!QUIZ]
> ¿Cuál es la sintaxis correcta para crear una casilla de verificación marcada (completada) en una lista de tareas en GFM?
> - [ ] `* (x) Tarea completada`
> - [x] `- [x] Tarea completada`
> - [ ] `[check] Tarea completada`
>
> **Explicación**: La sintaxis `- [x]` con la `x` minúscula entre corchetes genera una casilla de verificación marcada en GitHub Flavored Markdown.

---

## Ejercicio Práctico: Plantilla Completa de README.md

**Objetivo**: Construir una plantilla base de README.md utilizando las características de GFM aprendidas.

**Instrucciones**:
1. Crea un archivo `README.md`.
2. Añade un callout del tipo `[!TIP]`.
3. Incluye una lista de tareas de la hoja de ruta del proyecto.
4. Agrega un bloque desplegable `<details>` con comandos de solución de problemas.

<details class="exercise-solution">
<summary>Ver solución paso a paso</summary>

<div class="solution-content">

```markdown
# Sistema de Gestión EduXP

Plataforma educativa interactiva de código abierto para aprender tecnologías web.

> [!TIP]
> Recuerda clonar el repositorio usando la opción `--recursive` para incluir los submódulos.

## Hoja de Ruta (Roadmap)
- [x] Configuración inicial del servidor Express
- [x] Creación del motor de lecciones en Markdown
- [ ] Implementación del sistema de gamificación (XP)
- [ ] Integración de pasarela de pagos

<details>
<summary>Solución de Problemas Frecuentes</summary>

Si encuentras el error `EADDRINUSE`, ejecuta:
`npx kill-port 3000`

</details>
```

</div>
</details>
