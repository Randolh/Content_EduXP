# Lección 2: Modelo de Caja (Box Model) y la propiedad Display

En esta lección aprenderás cómo los navegadores representan visualmente cada elemento HTML como una caja rectangular mediante el **Box Model** y cómo controlar su comportamiento con `box-sizing` y `display`.

---

## 1. Las 4 Capas del Modelo de Caja (Box Model)

Todo elemento HTML renderizado en la pantalla consta de 4 áreas concéntricas:

```text
┌─────────────────────────────────────────┐
│               MARGIN                    │
│   ┌─────────────────────────────────┐   │
│   │           BORDER                │   │
│   │   ┌─────────────────────────┐   │   │
│   │   │        PADDING          │   │   │
│   │   │   ┌─────────────────┐   │   │   │
│   │   │   │     CONTENT     │   │   │   │
│   │   │   │  (width x height)│   │   │   │
│   │   │   └─────────────────┘   │   │   │
│   │   └─────────────────────────┘   │   │
│   └─────────────────────────────────┘   │
└─────────────────────────────────────────┘
```

1. **Content (Contenido)**: El texto, imágenes o elementos anidados. Su tamaño está dado por `width` y `height`.
2. **Padding (Relleno interno)**: El espacio transparente entre el contenido y el borde.
3. **Border (Borde)**: La línea o marco que rodea el padding.
4. **Margin (Margen externo)**: El espacio transparente exterior que separa la caja de otros elementos adyacentes.

---

## 2. El Reseteo Indispensable: `box-sizing: border-box`

Por defecto en el estándar antiguo (`content-box`), si asignas `width: 200px` y `padding: 20px` a un elemento, el ancho total resultante en pantalla será de **240px** (`200 + 20 + 20`). Esto solía romper los diseños responsivos.

Con `box-sizing: border-box`, el valor de `width` incluye el contenido, el padding y el borde dentro de los 200px especificados.

```css
/* Aplicar el modelo border-box globalmente en todo proyecto moderno */
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
```

---

## 3. La Propiedad `display`

La propiedad `display` determina el comportamiento de la caja en el flujo del documento:

- `display: block`: Ocupa el **100% del ancho disponible** de su contenedor y fuerza un salto de línea antes y después (ej. `<div>`, `<p>`, `<h1>`). Acepta `width`, `height`, `margin` y `padding`.
- `display: inline`: Solo ocupa el ancho estricto de su contenido y fluye en la misma línea (ej. `<span>`, `<a>`, `<strong>`). **Ignora** los valores de `width` y `height` y los márgenes verticales.
- `display: inline-block`: Fluye horizontalmente en la misma línea como un elemento inline, pero **sí respeta** los valores de `width`, `height`, `margin` y `padding`.
- `display: none`: Remueve completamente el elemento del árbol visual y del flujo de la página.

---

## Autoevaluación

> [!QUIZ]
> ¿Por qué es una buena práctica aplicar `box-sizing: border-box` al inicio de un proyecto CSS?
> - [ ] Porque elimina los bordes de todas las imágenes.
> - [x] Porque asegura que el `width` y `height` indicados incluyan el padding y el borde, evitando cálculos inesperados.
> - [ ] Porque convierte todos los elementos inline en elementos de bloque.
>
> **Explicación**: `border-box` hace que las dimensiones indicadas sean exactas e incluyan el relleno interno y bordes.

---

## 🛠️ Ejercicio Práctico: Tarjeta con Border-Box

**Objetivo**: Construir una tarjeta de contenido fijando un ancho total exacto de 300px con relleno de 20px y borde de 2px.

**Instrucciones**:
1. Crea una regla CSS para la clase `.card-box`.
2. Aplica `box-sizing: border-box`.
3. Asigna `width: 300px`, `padding: 20px`, `border: 2px solid #2563eb` y `margin: 15px`.

<details class="exercise-solution">
<summary>💡 Ver solución explicada paso a paso</summary>

<div class="solution-content">

```css
.card-box {
  box-sizing: border-box;
  width: 300px;
  padding: 20px;
  border: 2px solid #2563eb;
  margin: 15px;
  background-color: #f8fafc;
}
```

**Explicación**: Al utilizar `border-box`, el ancho total visible en el navegador será de **exactamente 300px**, distribuyendo internamente el padding y el borde sin deformar el contenedor.
</div>
</details>
