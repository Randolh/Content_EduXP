# Lección 5: Enlaces, Imágenes Responsivas (`<picture>`) y Multimedia

En esta lección aprenderás a conectar páginas mediante hipervínculos, optimizar imágenes para rendimiento web y utilizar las etiquetas nativas `<picture>`, `<audio>` y `<video>`.

---

## 1. Hipervínculos (`<a>`) y Atributos de Seguridad

La etiqueta `<a>` (*anchor*) crea enlaces navegables:

```html
<!-- Enlace a sitio externo en una pestaña nueva -->
<a href="https://eduxp.dev" target="_blank" rel="noopener noreferrer">
  Visitar EduXP
</a>

<!-- Enlace de descarga de archivo -->
<a href="guia.pdf" download="Guia_HTML5.pdf">Descargar Guía PDF</a>
```

> [!WARNING]
> Al utilizar `target="_blank"` para abrir enlaces en pestañas nuevas, **siempre** incluye `rel="noopener noreferrer"` para proteger tu aplicación contra ataques de suplantación de pestaña (*tabnabbing*).

---

## 2. Imágenes Optimizadas (`<img>`) y Carga Diferida

```html
<img 
  src="html5-banner.webp" 
  alt="Banner ilustrativo con el logo de HTML5" 
  width="800" 
  height="400" 
  loading="lazy"
>
```

- `alt`: Descripción textual imprescindible para accesibilidad y SEO.
- `width` y `height`: Evitan el parpadeo de diseño (*Cumulative Layout Shift - CLS*) al reservar espacio antes de que la imagen cargue.
- `loading="lazy"`: Habilita la carga diferida nativa. La imagen solo se descarga cuando el usuario se desplaza cerca de ella.

---

## 3. Imágenes Responsivas con `<picture>`

La etiqueta `<picture>` permite ofrecer distintos formatos (como WebP o AVIF) o diferentes tamaños de imagen según el dispositivo o la pantalla del usuario:

```html
<picture>
  <!-- Para dispositivos móviles (pantallas pequeñas) -->
  <source media="(max-width: 600px)" srcset="banner-mobile.webp">
  <!-- Formato moderno AVIF para pantallas grandes -->
  <source srcset="banner-desktop.avif" type="image/avif">
  <!-- Imagen por defecto (Fallback) -->
  <img src="banner-desktop.jpg" alt="Banner promocional de EduXP">
</picture>
```

---

## 4. Multimedia Nativa: `<video>` y `<audio>`

HTML5 permite reproducir contenido multimedia sin necesidad de plugins externos (como Flash):

### Reproductor de Video
```html
<video controls poster="portada.jpg" width="640">
  <source src="clase-html5.mp4" type="video/mp4">
  <source src="clase-html5.webm" type="video/webm">
  Tu navegador no soporta el reproductor de video HTML5.
</video>
```

### Reproductor de Audio
```html
<audio controls preload="metadata">
  <source src="podcast-episodio1.mp3" type="audio/mpeg">
  Tu navegador no soporta el elemento de audio HTML5.
</audio>
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué atributo de la etiqueta `<img>` le indica al navegador que no descargue la imagen hasta que el usuario haga scroll cerca de ella?
> - [ ] `async="true"`
> - [x] `loading="lazy"`
> - [ ] `defer="true"`
>
> **Explicación**: `loading="lazy"` habilita la carga perezosa diferida nativa del navegador para optimizar el rendimiento.

---

## 🛠️ Ejercicio Práctico: Galería Responsiva con `<picture>`

**Objetivo**: Crear una imagen adaptativa que cargue una versión ligera en teléfonos y una versión de alta resolución en escritorio.

**Instrucciones**:
1. Escribe un elemento `<picture>`.
2. Incluye un `<source>` con la regla `media="(max-width: 768px)"` apuntando a `foto-movil.jpg`.
3. Agrega la etiqueta `<img>` por defecto apuntando a `foto-escritorio.jpg` con el atributo `loading="lazy"` y un texto alternativo semántico `alt`.

<details class="exercise-solution">
<summary>💡 Ver solución explicada paso a paso</summary>

<div class="solution-content">

```html
<picture>
  <source media="(max-width: 768px)" srcset="foto-movil.jpg">
  <img src="foto-escritorio.jpg" alt="Fotografía del equipo de desarrollo trabajando en oficina" loading="lazy">
</picture>
```

**Explicación**: El navegador evaluará la media query `(max-width: 768px)` y cargará `foto-movil.jpg` en pantallas pequeñas, mientras que usará la imagen por defecto en monitores grandes.
</div>
</div>
</details>
