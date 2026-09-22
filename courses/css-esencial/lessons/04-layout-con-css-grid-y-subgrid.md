# Lección 4: Layouts Bidimensionales con CSS Grid y Subgrid

En esta lección aprenderás a construir maquetas bidimensionales complejas (filas y columnas simultáneas) utilizando **CSS Grid**, las unidades fraccionales (`fr`), la función `auto-fit` / `minmax()` y la nueva especificación **Subgrid**.

---

## 1. Fundamentos de CSS Grid (Filas y Columnas)

Para activar el sistema de cuadrícula bidimensional, asigna `display: grid`:

```css
.grid-container {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr; /* 3 columnas (unidad fraccional) */
  grid-template-rows: auto 1fr auto;
  gap: 20px;                         /* Espacio entre celdas */
}
```

- La unidad `fr` (*fraction*) representa una fracción del espacio libre disponible en el contenedor Grid.

---

## 2. Grids Autoadaptables sin Media Queries (`auto-fit` + `minmax`)

Puedes crear rejillas de tarjetas completamente responsivas que se acomodan solas según el tamaño de la pantalla sin escribir una sola media query:

```css
.card-grid {
  display: grid;
  /* Crea tantas columnas de mínimo 250px como quepan */
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 24px;
}
```

- `repeat()`: Repite el patrón de columnas.
- `auto-fit`: Ajusta el número de columnas automáticamente estirando las existentes.
- `minmax(250px, 1fr)`: Garantiza que ninguna columna mida menos de 250px, pero permite crecer libremente si hay espacio sobrante.

---

## 3. Maquetación Basada en Áreas (`grid-template-areas`)

Permite maquetar el layout visual mediante un mapa conceptual de cadenas de texto:

```css
.layout-page {
  display: grid;
  grid-template-columns: 250px 1fr;
  grid-template-rows: auto 1fr auto;
  grid-template-areas:
    "header header"
    "sidebar content"
    "footer footer";
  min-height: 100vh;
}

header { grid-area: header; }
aside  { grid-area: sidebar; }
main   { grid-area: content; }
footer { grid-area: footer; }
```

---

## 4. La Nueva Especificación: Subgrid (`grid-template-columns: subgrid`)

Anteriormente, los elementos hijos anidados dentro de una celda Grid perdían la alineación con la cuadrícula del padre. Con **Subgrid**, un elemento hijo puede adoptar directamente las líneas de columna o fila de su contenedor abuelo:

```css
.card-item {
  grid-row: span 3;           /* Ocupa 3 filas del Grid padre */
  display: grid;
  grid-template-rows: subgrid; /* Hereda las líneas exactas del padre */
}
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué logra la regla `grid-template-columns: repeat(auto-fit, minmax(200px, 1fr))`?
> - [ ] Crea exactamente 200 columnas fijas de 1px cada una.
> - [x] Crea un layout fluido de tarjetas que se adapta automáticamente al ancho de la pantalla sin requerir Media Queries.
> - [ ] Limita el número de elementos a solo 200 items por fila.
>
> **Explicación**: `auto-fit` combinado con `minmax()` recalcula dinámicamente el número y ancho de las columnas.

---

## 🛠️ Ejercicio Práctico: Galería Fluid Responsive con CSS Grid

**Objetivo**: Construir una rejilla de tarjetas que adapte sus columnas automáticamente manteniendo un tamaño mínimo de 280px.

**Instrucciones**:
1. Define la clase `.gallery-grid`.
2. Asigna `display: grid`.
3. Utiliza `grid-template-columns` con `repeat()`, `auto-fit` y `minmax(280px, 1fr)`.
4. Asigna un espaciado `gap: 20px`.

<details class="exercise-solution">
<summary>💡 Ver solución explicada paso a paso</summary>

<div class="solution-content">

```css
.gallery-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;
  padding: 20px;
}
```

**Explicación**: En un monitor 4K mostrará múltiples columnas de 280px+; en una tablet mostrará 2 o 3 columnas y en un teléfono móvil se colapsará automáticamente a 1 sola columna.
</div>
</details>
