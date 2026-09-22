# Lección 4: Agrupación, Detalle y Nuevas APIs: `<dialog>` y Popover

En esta lección aprenderás a utilizar etiquetas para contenido agrupado (`<figure>`, `<details>`) y explorarás las APIs nativas más recientes de HTML5: los modales con `<dialog>` y los desplegables con el atributo `popover`.

---

## 1. Contenido Agrupado: `<figure>` y `<figcaption>`

Para vincular imágenes, ilustraciones, diagramas o extractos de código con una leyenda descriptiva:

```html
<figure>
  <img src="diagrama-html5.png" alt="Esquema del árbol DOM en HTML5">
  <figcaption>Figura 1.1: Representación de la estructura del árbol DOM en el navegador.</figcaption>
</figure>
```

---

## 2. Acordeones Nativos sin JavaScript: `<details>` y `<summary>`

HTML5 incluye un widget desplegable o acordeón nativo que no requiere código JavaScript para abrirse o cerrarse:

```html
<details>
  <summary>¿Qué requisitos necesito para aprender HTML5?</summary>
  <p>Únicamente un navegador actualizado y un editor de texto como VS Code.</p>
</details>
```

> [!TIP]
> Puedes añadir el atributo `open` (`<details open>`) si deseas que el acordeón aparezca abierto por defecto al cargar la página.

---

## 3. Ventanas Modales Nativas con `<dialog>`

El elemento `<dialog>` representa una caja de diálogo o ventana modal interactiva nativa.

```html
<!-- Botón para abrir el modal vía JavaScript -->
<button onclick="document.getElementById('mi-modal').showModal()">Abrir Modal</button>

<!-- Ventana Modal HTML5 -->
<dialog id="mi-modal">
  <h2>Términos y Condiciones</h2>
  <p>Por favor acepta nuestras políticas de privacidad para continuar.</p>
  
  <form method="dialog">
    <button>Aceptar y Cerrar</button>
  </form>
</dialog>
```

- `.showModal()`: Abre el diálogo como un modal flotante con un fondo oscuro por defecto (`::backdrop`).
- `<form method="dialog">`: Al enviar un formulario dentro de un diálogo con este método, el modal se cierra automáticamente sin recargar la página.

---

## 4. La Nueva API Nativa `popover`

HTML5 ha incorporado el atributo `popover`, permitiendo crear menús desplegables, tooltips y ventanas flotantes sin una sola línea de JavaScript.

```html
<!-- Botón activador conectado por ID -->
<button popovertarget="mi-popover">Ver Información Rápida</button>

<!-- Elemento Popover -->
<div id="mi-popover" popover>
  <h3>Notificación</h3>
  <p>¡Este mensaje flota sobre el contenido gracias al atributo popover nativo de HTML5!</p>
</div>
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué elemento de HTML5 permite crear un acordeón desplegable interactivo sin necesidad de escribir código JavaScript?
> - [ ] El atributo `popover`.
> - [x] La combinación de los elementos `<details>` y `<summary>`.
> - [ ] El elemento `<dialog>` con el atributo `open`.
>
> **Explicación**: `<details>` y `<summary>` integran funcionalidad nativa de despliegue en el navegador.

---

## 🛠️ Ejercicio Práctico: Modal de Confirmación

**Objetivo**: Implementar una ventana de diálogo modal nativa utilizando la etiqueta `<dialog>`.

**Instrucciones**:
1. Escribe un elemento `<dialog>` con el atributo `id="modal-confirm"`.
2. Dentro del diálogo, añade un encabezado `<h3>Confirmar Suscripción</h3>` y un formulario con `method="dialog"`.
3. Añade dos botones en el formulario: uno para cancelar y uno para confirmar.

<details class="exercise-solution">
<summary>💡 Ver solución explicada paso a paso</summary>

<div class="solution-content">

```html
<dialog id="modal-confirm">
  <h3>Confirmar Suscripción</h3>
  <p>¿Deseas recibir noticias y actualizaciones semanales en tu correo?</p>
  
  <form method="dialog">
    <button value="cancel">Cancelar</button>
    <button value="confirm">Confirmar</button>
  </form>
</dialog>
```

**Explicación**: El elemento `<dialog>` encierra la caja modal, y el formulario con `method="dialog"` permite cerrar el modal devolviendo el valor del botón presionado al evento de cierre.
</div>
</details>
