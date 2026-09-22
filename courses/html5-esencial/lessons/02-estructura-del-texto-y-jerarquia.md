# Lección 2: Jerarquía de Texto, Listas y Formateo Semántico

En esta lección aprenderás a darle estructura lógica y significado al texto mediante encabezados jerárquicos, párrafos, listas y etiquetas de formato semántico.

---

## 1. Encabezados Jerárquicos (`<h1>` a `<h6>`)

HTML5 proporciona 6 niveles de encabezados para indicar la importancia jerárquica del contenido:

```html
<h1>Título Principal de la Página (Único por documento)</h1>
<h2>Sección Principal</h2>
<h3>Subsección de Nivel 3</h3>
<h4>Subsección de Nivel 4</h4>
```

> [!WARNING]
> Nunca uses encabezados para cambiar el tamaño de letra por razones de diseño visual. Utiliza encabezados **únicamente para estructurar el árbol jerárquico del documento**. Debe existir solo **un `<h1>` por página** para un SEO óptimo.

---

## 2. Párrafos y Saltos de Línea (`<p>`, `<br>`, `<hr>`)

- `<p>`: Encapsula párrafos de texto.
- `<br>`: Fuerza un salto de línea dentro de un párrafo (usar con moderación, ej. en poesía o direcciones).
- `<hr>`: Representa un cambio temático o separación semántica entre párrafos (regla horizontal).

---

## 3. Listas: Ordenadas, Desordenadas y de Definición

HTML5 ofrece tres tipos fundamentales de listas:

### Lista Desordenada (`<ul>` y `<li>`)
Para elementos donde el orden numérico no importa (ej. tecnologías, viñetas):
```html
<ul>
  <li>HTML5</li>
  <li>CSS3</li>
  <li>JavaScript</li>
</ul>
```

### Lista Ordenada (`<ol>` y `<li>`)
Para secuencias paso a paso o rankings:
```html
<ol>
  <li>Descargar el editor de código.</li>
  <li>Crear el archivo index.html.</li>
  <li>Abrir el archivo en el navegador.</li>
</ol>
```

### Lista de Definición (`<dl>`, `<dt>`, `<dd>`)
Ideal para glosarios, listas clave-valor o preguntas frecuentes:
```html
<dl>
  <dt>HTML</dt>
  <dd>Lenguaje de marcado para estructurar la web.</dd>
  <dt>CSS</dt>
  <dd>Lenguaje de hojas de estilo para la presentación visual.</dd>
</dl>
```

---

## 4. Formateo Semántico de Texto

En HTML5, las etiquetas de texto no solo cambian la apariencia, sino que expresan la **intención del mensaje**:

- `<strong>`: Representa **importancia o urgencia** (los navegadores lo muestran en negrita).
- `<em>`: Representa **énfasis verbal** o tono (los navegadores lo muestran en cursiva).
- `<mark>`: Representa texto **destacado o resaltado** por relevancia contextual.
- `<code>`: Representa un fragmento corto de código informático.
- `<time datetime="2026-09-22">`: Representa una fecha o tiempo legible por máquinas y buscadores.

```html
<p>La entrega es <mark>obligatoria</mark> antes del <time datetime="2026-10-01">1 de octubre</time>.</p>
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué etiqueta debe utilizarse para resaltar un término debido a su importancia o gravedad en el contenido?
> - [ ] La etiqueta `<b>` porque pone el texto en negrita.
> - [x] La etiqueta `<strong>` porque aporta significado de importancia alta a los lectores de pantalla y buscadores.
> - [ ] La etiqueta `<i>` porque inclina las letras.
>
> **Explicación**: `<strong>` aporta semántica de alta relevancia e importancia, mientras que `<b>` solo aplica estilo visual sin valor semántico.

---

## 🛠️ Ejercicio Práctico: Glosario Técnico Semántico

**Objetivo**: Construir la sección de un artículo técnico utilizando la jerarquía de encabezados, listas y formateo semántico.

**Instrucciones**:
1. Crea un encabezado secundario `<h2>` titulado `"Glosario de Desarrollo Web"`.
2. Utiliza una lista de definición (`<dl>`) con dos términos: `"W3C"` y `"WHATWG"`.
3. Dentro de las definiciones (`<dd>`), utiliza `<strong>` y `<em>` para resaltar acrónimos e importancia.

<details class="exercise-solution">
<summary>💡 Ver solución explicada paso a paso</summary>

<div class="solution-content">

```html
<h2>Glosario de Desarrollo Web</h2>

<dl>
  <dt><strong>W3C</strong></dt>
  <dd>World Wide Web Consortium: Organización que estandarizó versiones previas de HTML y recomendaciones web.</dd>
  
  <dt><strong>WHATWG</strong></dt>
  <dd>Web Hypertext Application Technology Working Group: Comunidad que mantiene el estándar vivo <em>HTML Living Standard</em>.</dd>
</dl>
```

**Explicación**: La estructura utiliza `<dl>`, `<dt>` y `<dd>` para vincular términos con sus explicaciones, aprovechando `<strong>` y `<em>` para dar valor semántico.
</div>
</details>
