# Lección 6: Pseudo-clases Modernas: `:has()`, `:is()` y `:where()`

En esta lección aprenderás a utilizar las pseudo-clases de CSS moderno más innovadoras, incluyendo el selector relacional del padre `:has()` (conocido como el "selector de padre"), `:is()` y `:where()`.

---

## 1. La Revolución de CSS: `:has()` (El Selector Relacional del Padre)

Históricamente, CSS solo permitía seleccionar hacia abajo en la jerarquía del DOM (hijos o hermanos posteriores). La pseudo-clase `:has()` permite estilizar un elemento en función de si **contiene a un elemento hijo específico** o cumple una condición.

### Casos de Uso Potentes con `:has()`:

```css
/* 1. Estilizar una tarjeta completa si contiene una imagen en su interior */
.card:has(img) {
  grid-template-rows: 200px 1fr;
}

/* 2. Estilizar un contenedor de formulario si tiene un campo inválido */
.form-group:has(input:invalid) {
  border-left: 4px solid #ef4444;
}

/* 3. Cambiar el tema del body si un checkbox modal está activado */
body:has(#menu-toggle:checked) {
  overflow: hidden; /* Evita el scroll cuando el menú está abierto */
}
```

---

## 2. Reducción de Redundancia: `:is()` y `:where()`

Permiten agrupar múltiples selectores en uno solo para simplificar el código.

### Sintaxis Comparativa:

```css
/* CSS Tradicional Largo */
header h1, header h2, header h3,
footer h1, footer h2, footer h3 {
  font-family: 'Outfit', sans-serif;
}

/* Con la pseudo-clase :is() */
:is(header, footer) :is(h1, h2, h3) {
  font-family: 'Outfit', sans-serif;
}
```

### Diferencia Clave entre `:is()` y `:where()`:
- `:is()`: Adopta la especificidad del selector más pesado de su lista.
- `:where()`: **Tiene especificidad CERO `(0,0,0,0)`**. Es ideal para librerías o resets donde quieres que los estilos sean extremadamente fáciles de sobrescribir.

---

## 3. Pseudo-elementos Útiles: `::before`, `::after` y `::selection`

Los pseudo-elementos crean elementos cosméticos sin añadir HTML innecesario:

```css
/* Añadir un distintivo cosmético a los enlaces externos */
a[href^="https://"]::after {
  content: " ↗";
  font-size: 0.8em;
  color: #64748b;
}

/* Personalizar el color de resaltado al seleccionar texto con el ratón */
::selection {
  background-color: #3b82f6;
  color: #ffffff;
}
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué capacidad revolucionaria introdujo la pseudo-clase `:has()` en CSS?
> - [ ] Permite descargar fuentes tipográficas desde servidores externos sin usar HTML.
> - [x] Permite seleccionar y estilizar un elemento padre en función de sus hijos o elementos contenidos.
> - [ ] Convierte código CSS en JavaScript dinámico.
>
> **Explicación**: `:has()` evalúa si un elemento contiene ciertos hijos o estados, permitiendo seleccionar padres.

---

## 🛠️ Ejercicio Práctico: Tarjeta de Producto con Badge Nativo con `:has()`

**Objetivo**: Aplicar un estilo especial a un contenedor de producto solo si tiene un elemento de descuento `.badge-sale` dentro.

**Instrucciones**:
1. Escribe la regla `.product-card`.
2. Utiliza `:has(.badge-sale)` para añadir un borde destacado de color de oferta `#f59e0b`.

<details class="exercise-solution">
<summary>💡 Ver solución explicada paso a paso</summary>

<div class="solution-content">

```css
.product-card {
  padding: 16px;
  background: white;
  border: 1px solid #e2e8f0;

  /* Aplica solo a las tarjetas que contengan un badge de oferta */
  &:has(.badge-sale) {
    border: 2px solid #f59e0b;
    box-shadow: 0 4px 12px rgba(245, 158, 11, 0.15);
  }
}
```

**Explicación**: El navegador examina el interior de cada `.product-card`. Si encuentra `.badge-sale`, aplica automáticamente el borde naranja sin necesidad de clases adicionales en el padre.
</div>
</details>
