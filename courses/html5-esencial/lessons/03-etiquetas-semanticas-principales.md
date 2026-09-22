# Lección 3: Etiquetas Semánticas de Estructura Principales

En esta lección aprenderás a reemplazar el antiguo uso indiscriminado de `<div>` por **etiquetas semánticas de estructura HTML5** para dar un significado claro a cada bloque de tu página web.

---

## 1. ¿Por qué es crucial el HTML Semántico?

Antes de HTML5, las páginas web se maquetaban con contenedores genéricos como `<div id="header">`, `<div id="nav">` o `<div id="footer">`. 

El **HTML Semántico** introduce etiquetas con nombres con significado propio. Sus beneficios principales son:
1. **Accesibilidad (a11y)**: Permite que los lectores de pantalla y tecnologías de asistencia para personas con discapacidad visual naveguen fácilmente por zonas del sitio (landmarks).
2. **SEO (Optimización en Buscadores)**: Ayuda a Google y Bing a indexar correctamente cuál es el contenido principal y cuál es secundario.
3. **Mantenibilidad de Código**: Hace que el código sea limpio y fácil de leer para otros desarrolladores.

---

## 2. Mapa Semántico de una Página Web en HTML5

```text
┌─────────────────────────────────────────────────────────┐
│                        <header>                         │
│  ┌───────────────────────────────────────────────────┐  │
│  │                        <nav>                      │  │
│  └───────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘
┌───────────────────────────────────────┬─────────────────┐
│                <main>                 │     <aside>     │
│  ┌─────────────────────────────────┐  │ (Barra lateral, │
│  │            <article>            │  │   publicidad,   │
│  │  ┌───────────────────────────┐  │  │   enlaces)      │
│  │  │         <section>         │  │  │                 │
│  │  └───────────────────────────┘  │  │                 │
│  └─────────────────────────────────┘  │                 │
└───────────────────────────────────────┴─────────────────┘
┌─────────────────────────────────────────────────────────┐
│                        <footer>                         │
└─────────────────────────────────────────────────────────┘
```

---

## 3. Las Etiquetas Semánticas Estructurales Explicadas

### `<header>`
Representa la cabecera del documento o de una sección. Suele contener el logo, el título principal y la navegación principal.

### `<nav>`
Representa un bloque de **enlaces de navegación principal** (menús de navegación, barras superiores, listas de enlaces de navegación interna).

### `<main>`
Representa el **contenido central e independiente del documento**. Solo debe haber **un `<main>` visible por página** y no debe contener elementos repetitivos entre páginas (como logos o pie de página).

### `<article>`
Representa una unidad de contenido **autónoma e independiente** que tendría sentido por sí sola si se distribuyera fuera del sitio (ej. un post de blog, una noticia, un comentario o una tarjeta de producto).

### `<section>`
Representa una **agrupación temática de contenido** relacionada dentro de un documento o artículo. Generalmente debe incluir su propio encabezado (`<h2>`-`<h6>`).

### `<aside>`
Representa contenido secundario o complementario tangencial al contenido principal (barras laterales, enlaces relacionados, anuncios, biografías del autor).

### `<footer>`
Representa el pie de página del documento o sección. Suele contener avisos de copyright, políticas de privacidad, enlaces de contacto y redes sociales.

---

## Ejemplo Completo de Maquetación Semántica

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Blog Dev - EduXP</title>
</head>
<body>

  <header>
    <h1>DevBlog EduXP</h1>
    <nav>
      <ul>
        <li><a href="#inicio">Inicio</a></li>
        <li><a href="#articulos">Artículos</a></li>
        <li><a href="#contacto">Contacto</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <section id="articulos">
      <h2>Últimas Publicaciones</h2>
      
      <article>
        <h3>Novedades en HTML5 Living Standard</h3>
        <p>Publicado el <time datetime="2026-09-22">22 de septiembre de 2026</time>.</p>
        <p>El estándar vivo de la HTML sigue añadiendo capacidades increíbles como la Popover API...</p>
      </article>
    </section>
  </main>

  <aside>
    <h3>Sobre el Autor</h3>
    <p>Apasionado del desarrollo frontend y los estándares web.</p>
  </aside>

  <footer>
    <p>&copy; 2026 EduXP. Todos los derechos reservados.</p>
  </footer>

</body>
</html>
```

---

## Autoevaluación

> [!QUIZ]
> ¿Cuál es la etiqueta adecuada para encerrar la publicación de una entrada de blog completa e independiente?
> - [ ] `<section>` porque es una sección de la página.
> - [x] `<article>` porque representa contenido autónomo reutilizable por sí solo.
> - [ ] `<div>` con la clase `"blog-post"`.
>
> **Explicación**: `<article>` es la etiqueta semántica diseñada para elementos autónomos e independientes como noticias, posts o tarjetas de producto.

---

## 🛠️ Ejercicio Práctico: Estructurar la Portada de una Tienda

**Objetivo**: Reemplazar una estructura genérica basada en `<div>` por las etiquetas semánticas HTML5 adecuadas.

**Instrucciones**:
1. Crea un encabezado con `<header>` y un menú dentro de `<nav>`.
2. Define un área principal con `<main>`.
3. Dentro de `<main>`, añade una sección `<section>` con dos artículos `<article>` que representen dos productos.
4. Finaliza con un `<footer>`.

<details class="exercise-solution">
<summary>💡 Ver solución explicada paso a paso</summary>

<div class="solution-content">

```html
<header>
  <h1>Tienda EduXP</h1>
  <nav>
    <a href="#productos">Productos</a> | <a href="#ofertas">Ofertas</a>
  </nav>
</header>

<main>
  <section id="productos">
    <h2>Catálogo Destacado</h2>
    
    <article>
      <h3>Teclado Mecánico RGB</h3>
      <p>Precio: $49.99</p>
    </article>

    <article>
      <h3>Monitor 4K 27"</h3>
      <p>Precio: $299.99</p>
    </article>
  </section>
</main>

<footer>
  <p>&copy; 2026 Tienda EduXP</p>
</footer>
```

**Explicación**: Cada elemento cumple su propósito semántico: `<header>` para la cabecera, `<nav>` para el menú, `<main>` para el catálogo, `<section>` para agruparlo y `<article>` para cada producto individual.
</div>
</details>
