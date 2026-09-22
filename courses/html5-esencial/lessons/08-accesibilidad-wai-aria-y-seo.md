# Lección 8: Accesibilidad Web (WAI-ARIA) y SEO Semántico

En esta lección aprenderás las mejores prácticas de **accesibilidad web (a11y)**, el uso responsable de atributos **WAI-ARIA** y la optimización para motores de búsqueda (**SEO técnico**) mediante marcado HTML5.

---

## 1. Fundamentos de Accesibilidad Web (a11y)

Un sitio web accesible garantiza que todas las personas, independientemente de sus capacidades físicas o cognitivas o de las tecnologías de asistencia que utilicen (como lectores de pantalla NVDA, JAWS o VoiceOver), puedan navegar y comprender el contenido.

### Reglas de Oro de Accesibilidad en HTML5:
1. **Contraste y Jerarquía**: Respetar el orden jerárquico único de encabezados (`<h1>` -> `<h2>` -> `<h3>`).
2. **Textos Alternativos**: Proveer descripciones `alt` útiles en imágenes que transmitan información.
3. **Navegación por Teclado**: Asegurar que todos los elementos interactivos puedan recibir foco mediante la tecla `Tab`.

---

## 2. Atributos WAI-ARIA (`aria-*`)

**WAI-ARIA** (*Web Accessibility Initiative - Accessible Rich Internet Applications*) complementa al HTML cuando la semántica nativa no es suficiente para comunicar estados dinámicos a lectores de pantalla.

> [!IMPORTANT]
> **Primera Regla de ARIA**: Si puedes utilizar un elemento o atributo HTML5 nativo que ya tenga la semántica requerida (como `<button>`, `<dialog>` o `<nav>`), **NO utilices ARIA**.

### Atributos ARIA Más Utilizados:

- `aria-label`: Proporciona una etiqueta de texto invisible cuando el elemento no tiene texto visible (ej. un botón que solo tiene un icono).
  ```html
  <button aria-label="Cerrar ventana modal">&times;</button>
  ```
- `aria-expanded="true|false"`: Comunica a un lector de pantalla si un menú o desplegable está abierto o cerrado.
  ```html
  <button aria-expanded="false" aria-controls="menu-desplegable">Menú</button>
  ```
- `aria-hidden="true"`: Oculta elementos puramente decorativos para que los lectores de pantalla los ignoren.
  ```html
  <span aria-hidden="true">🚀</span>
  ```

---

## 3. SEO Semántico y Meta Etiquetas Open Graph

El marcado semántico es la columna vertebral del posicionamiento orgánico en motores de búsqueda (SEO):

```html
<head>
  <!-- Descripción corta para el snippet de Google -->
  <meta name="description" content="Aprende HTML5 y desarrollo web profesional con el curso esencial de EduXP.">
  
  <!-- Meta etiquetas Open Graph para redes sociales (Facebook, LinkedIn, X) -->
  <meta property="og:title" content="Curso de HTML5 Moderno y Semántico">
  <meta property="og:description" content="Domina las etiquetas semánticas, accesibilidad y SEO en HTML5.">
  <meta property="og:image" content="https://eduxp.dev/assets/html5-cover.jpg">
  <meta property="og:type" content="website">
</head>
```

---

## Autoevaluación

> [!QUIZ]
> Según la primera regla de WAI-ARIA, ¿cuándo se deben agregar roles y atributos ARIA personalizados?
> - [ ] Siempre, en todas las etiquetas HTML5 de la página.
> - [x] Solo cuando la semántica nativa de HTML5 sea insuficiente para comunicar la función o estado a tecnologías de asistencia.
> - [ ] Únicamente en elementos `<div>` y `<span>`.
>
> **Explicación**: El estándar indica priorizar siempre los elementos semánticos nativos de HTML5 antes de recurrir a atributos ARIA.

---

## 🛠️ Ejercicio Práctico: Botón de Icono Accesible

**Objetivo**: Hacer que un botón de interfaz basado únicamente en un icono sea 100% accesible para personas con discapacidad visual.

**Instrucciones**:
1. Escribe un elemento `<button>`.
2. Dentro del botón, coloca un icono decorativo o caracter `🔍`.
3. Aplica `aria-label="Buscar en el catálogo"` al botón.
4. Aplica `aria-hidden="true"` al icono interior.

<details class="exercise-solution">
<summary>💡 Ver solución explicada paso a paso</summary>

<div class="solution-content">

```html
<button type="button" aria-label="Buscar en el catálogo">
  <span aria-hidden="true">🔍</span>
</button>
```

**Explicación**: El lector de pantalla ignorará el símbolo `🔍` gracias a `aria-hidden="true"` y leerá claramente `"Buscar en el catálogo"` indicado en `aria-label`.
</div>
</details>
