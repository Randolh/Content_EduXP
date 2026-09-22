# Lección 9: Proyecto Integrador: Maqueta Web Semántica Accesible

¡Felicidades por llegar a la última lección del curso! En este proyecto integrador pondrás a prueba todo lo aprendido construyendo la plantilla HTML5 completa, semántica y accesible para un **Portal Web / Blog de Tecnología**.

---

## 🎯 Objetivos del Proyecto

Debes maquetar un archivo `index.html` 100% válido según la especificación **HTML5 Living Standard** que incorpore:

1. **Metadatos Técnicos y SEO**: Configuración de `lang="es"`, `viewport`, `charset="UTF-8"`, título y metadatos Open Graph.
2. **Estructura Semántica Profesional**: Uso correcto de `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>` y `<footer>`.
3. **Contenido Enriquecido**: Formateo de texto semántico (`<time>`, `<mark>`, `<strong>`), imágenes responsivas (`<picture>`) y tabla de datos tabulares con `scope`.
4. **Formulario Accesible**: Formulario de contacto con tipos de input modernos (`email`, `date`, `text`), atributos de validación (`required`, `minlength`) y enlaces accesibles (`aria-label`).
5. **Componentes Interactivos Nativos**: Acordeón con `<details>` / `<summary>` o ventana modal con `<dialog>`.

---

## 📋 Especificaciones y Requisitos

```text
index.html
├── <head> (Metadatos charset, viewport, SEO, OG)
└── <body>
    ├── <header>
    │   ├── <h1> DevTech Portal
    │   └── <nav> (Enlaces de navegación)
    ├── <main>
    │   ├── <section id="destacado">
    │   │   └── <article> (Noticia principal con <picture> y <time>)
    │   ├── <section id="articulos">
    │   │   └── <article> (Publicaciones secundarias)
    │   └── <section id="precios">
    │       └── <table> (Tabla comparativa semántica)
    ├── <aside>
    │   ├── Biografía del Autor y <details> de preguntas frecuentes
    ├── <section id="contacto">
    │   └── <form> (Formulario de contacto validado)
    └── <footer> (Derechos de autor y enlaces)
```

---

## 🛠️ Solución Modelo del Proyecto Integrador

<details class="exercise-solution">
<summary>💡 Ver solución completa del Proyecto Integrador HTML5</summary>

<div class="solution-content">

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>DevTech Portal - Novedades de Desarrollo Web</title>
  <meta name="description" content="Portal de noticias y tutoriales sobre HTML5, CSS3 y JavaScript moderno.">
  <meta property="og:title" content="DevTech Portal">
  <meta property="og:type" content="website">
</head>
<body>

  <!-- Cabecera y Navegación Principal -->
  <header>
    <h1>DevTech Portal</h1>
    <nav aria-label="Menú principal">
      <ul>
        <li><a href="#destacado">Noticias</a></li>
        <li><a href="#planes">Planes</a></li>
        <li><a href="#faq">Preguntas</a></li>
        <li><a href="#contacto">Contacto</a></li>
      </ul>
    </nav>
  </header>

  <!-- Contenido Central del Sitio -->
  <main>
    
    <!-- Sección Destacada -->
    <section id="destacado">
      <h2>Noticia Destacada</h2>
      <article>
        <h3>El Futuro de la Web con HTML5 Living Standard</h3>
        <p>Publicado por <address style="display:inline;">Alex Pérez</address> el <time datetime="2026-09-22">22 de septiembre de 2026</time>.</p>
        
        <figure>
          <picture>
            <source media="(max-width: 600px)" srcset="https://via.placeholder.com/400x200">
            <img src="https://via.placeholder.com/800x400" alt="Ilustración de estándares web" loading="lazy">
          </picture>
          <figcaption>Figura 1: Evolución continua de las APIs nativas del navegador.</figcaption>
        </figure>

        <p>La web evoluciona hacia una plataforma con componentes nativos sin necesidad de librerías pesadas...</p>
      </article>
    </section>

    <!-- Sección de Precios Tabular -->
    <section id="planes">
      <h2>Planes de Membresía</h2>
      <table>
        <caption>Comparativa de Beneficios</caption>
        <thead>
          <tr>
            <th scope="col">Plan</th>
            <th scope="col">Acceso</th>
            <th scope="col">Precio</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <th scope="row">Básico</th>
            <td>Artículos públicos</td>
            <td>Gratis</td>
          </tr>
          <tr>
            <th scope="row">PRO</th>
            <td>Cursos y Talleres</td>
            <td>$12 USD / mes</td>
          </tr>
        </tbody>
      </table>
    </section>

  </main>

  <!-- Barra Lateral Secundaria -->
  <aside>
    <h2>Acerca de la Comunidad</h2>
    <p>Somos una plataforma dedicada a la enseñanza de estándares web.</p>

    <!-- Acordeón Nativo de Preguntas Frecuentes -->
    <section id="faq">
      <h3>Preguntas Frecuentes</h3>
      <details>
        <summary>¿Los certificados son gratuitos?</summary>
        <p>Sí, al completar todas las autoevaluaciones y el proyecto integrador.</p>
      </details>
    </section>
  </aside>

  <!-- Formulario de Contacto -->
  <section id="contacto">
    <h2>Boletín y Contacto</h2>
    <form action="/subscribe" method="POST">
      <div>
        <label for="nombre">Nombre Completo:</label>
        <input type="text" id="nombre" name="nombre" minlength="3" required>
      </div>

      <div>
        <label for="email">Correo Electrónico:</label>
        <input type="email" id="email" name="email" required>
      </div>

      <button type="submit">Suscribirse al Boletín</button>
    </form>
  </section>

  <!-- Pie de Página -->
  <footer>
    <p>&copy; 2026 DevTech Portal - EduXP. Todos los derechos reservados.</p>
  </footer>

</body>
</html>
```

</div>
</details>

---

## 🎓 ¡Felicidades!
Has completado con éxito el curso **HTML5 Moderno y Semántico**. ¡Ahora estás listo para dar el siguiente paso y dominar la estilización web avanzada con **CSS Moderno Sin Frameworks**!
