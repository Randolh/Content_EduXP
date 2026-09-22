# Lección 7: Formularios HTML5, Inputs Modernos y Validación Nativa

En esta lección aprenderás a construir formularios interactivos y accesibles con la amplia variedad de tipos de `<input>` que ofrece HTML5 y sus potentes atributos de **validación nativa sin JavaScript**.

---

## 1. La Estructura de un Formulario Accessible

Un formulario bien construido siempre vincula cada control con su etiqueta `<label>` mediante el atributo `for` e `id`:

```html
<form action="/enviar-datos" method="POST">
  <div>
    <label for="nombre-usuario">Nombre Completo:</label>
    <input type="text" id="nombre-usuario" name="nombre" required>
  </div>
  
  <button type="submit">Enviar Registro</button>
</form>
```

---

## 2. Tipos de Input Modernos en HTML5

HTML5 incluye múltiples tipos de entrada especializados que despliegan teclados optimizados en teléfonos móviles y validaciones integradas:

```html
<!-- Correo electrónico (Valida formato de email) -->
<input type="email" name="correo" required>

<!-- Número de teléfono (Despliega teclado numérico en móvil) -->
<input type="tel" name="telefono" placeholder="+52 555 123 4567">

<!-- Selector de Fecha nativo -->
<input type="date" name="fecha_nacimiento" min="1900-01-01" max="2026-12-31">

<!-- Rango o Slider -->
<input type="range" name="satisfaccion" min="1" max="10" step="1">

<!-- Selector de Color -->
<input type="color" name="color_favorito" value="#3b82f6">

<!-- Búsqueda -->
<input type="search" name="q" placeholder="Buscar lección...">
```

---

## 3. Listas de Autocompletado con `<datalist>`

HTML5 permite ofrecer sugerencias de autocompletado en un campo de texto simple sin librerías externas:

```html
<label for="pais">País de Residencia:</label>
<input type="text" id="pais" name="pais" list="lista-paises">

<datalist id="lista-paises">
  <option value="Argentina">
  <option value="Colombia">
  <option value="España">
  <option value="México">
  <option value="Perú">
</datalist>
```

---

## 4. Atributos de Validación Nativa en HTML5

Puedes impedir el envío de formularios con datos incorrectos utilizando atributos nativos:

- `required`: Hace que el campo sea obligatorio.
- `minlength="3"` / `maxlength="50"`: Controla la cantidad mínima y máxima de caracteres.
- `min="18"` / `max="99"`: Limita valores numéricos o de fechas.
- `pattern="[A-Za-z]{3,}"`: Aplica expresiones regulares (Regex) nativas para validar el formato.

```html
<input 
  type="text" 
  name="codigo_postal" 
  pattern="[0-9]{5}" 
  title="El código postal debe constar de exactamente 5 dígitos numéricos" 
  required
>
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué ventaja ofrece utilizar el tipo `<input type="email">` en lugar de un simple `<input type="text">`?
> - [ ] Cambia automáticamente el color del texto a azul.
> - [x] Valida automáticamente el formato de correo en el navegador y muestra la tecla '@' en teclados móviles.
> - [ ] Envía el formulario directamente a la bandeja de entrada del usuario.
>
> **Explicación**: `<input type="email">` provee validación nativa y optimiza la experiencia UX en dispositivos táctiles.

---

## 🛠️ Ejercicio Práctico: Formulario de Contacto Completo

**Objetivo**: Crear un formulario de contacto con validaciones nativas en HTML5.

**Instrucciones**:
1. Escribe la etiqueta `<form>`.
2. Incluye un campo obligatorio para el nombre (`type="text"`, `minlength="3"`).
3. Incluye un campo obligatorio para el correo (`type="email"`).
4. Incluye un campo opcional para la fecha de consulta (`type="date"`).
5. Incluye un `<textarea>` para el mensaje (`required`).
6. Añade un `<button type="submit">Enviar Mensaje</button>`.

<details class="exercise-solution">
<summary>💡 Ver solución explicada paso a paso</summary>

<div class="solution-content">

```html
<form action="/contacto" method="POST">
  <div>
    <label for="nombre">Nombre Completo:</label>
    <input type="text" id="nombre" name="nombre" minlength="3" required>
  </div>

  <div>
    <label for="email">Correo Electrónico:</label>
    <input type="email" id="email" name="email" required>
  </div>

  <div>
    <label for="fecha">Fecha preferida de contacto:</label>
    <input type="date" id="fecha" name="fecha">
  </div>

  <div>
    <label for="mensaje">Mensaje:</label>
    <textarea id="mensaje" name="mensaje" rows="4" required></textarea>
  </div>

  <button type="submit">Enviar Mensaje</button>
</form>
```

**Explicación**: El formulario asocia etiquetas `<label>` con campos mediante `for` e `id`, y aplica validaciones como `required`, `minlength` y tipos de input específicos.
</div>
</details>
