# Lección 5: Custom Properties (Variables) y CSS Nesting Nativo

En esta lección aprenderás dos de las características modernas más potentes de CSS que eliminan la necesidad de preprocesadores como SASS: las **Custom Properties (Variables CSS)** y el **CSS Nesting (Anidamiento Nativo)**.

---

## 1. Custom Properties (Variables CSS Nativas)

Las variables CSS permiten reutilizar valores (colores, espaciados, fuentes) en todo tu documento. A diferencia de las variables de SASS, las Custom Properties son **reactivas en tiempo de ejecución**, responden a la cascada y pueden actualizarse dinámicamente con JavaScript o pseudo-clases.

### Declaración y Uso:

```css
/* Scope Global en el pseudo-elemento raíz :root */
:root {
  --primary-color: #2563eb;
  --secondary-color: #0f172a;
  --bg-card: #ffffff;
  --padding-base: 16px;
  --radius-md: 8px;
}

/* Consumo mediante la función var() */
.card {
  background-color: var(--bg-card);
  padding: var(--padding-base);
  border-radius: var(--radius-md);
  border: 1px solid var(--primary-color);
}
```

### Cambio de Tema Claro / Oscuro con Variables:

```css
/* Sobrescribir variables según la preferencia del sistema */
@media (prefers-color-scheme: dark) {
  :root {
    --bg-card: #1e293b;
    --secondary-color: #f8fafc;
  }
}
```

---

## 2. CSS Nesting Nativo (Sin SASS ni Build Tools)

Todos los navegadores modernos soportan **CSS Nesting nativo**, permitiendo anidar reglas CSS dentro de otras para reflejar la jerarquía HTML de forma más limpia:

### Sintaxis Nativa en CSS Moderno:

```css
/* CSS Tradicional plano */
.card {
  background: white;
}
.card .card-title {
  font-size: 1.5rem;
}
.card:hover {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

/* CSS Nesting Nativo Moderno */
.card {
  background: white;

  /* Selector descendiente anidado */
  .card-title {
    font-size: 1.5rem;
  }

  /* Pseudo-clase vinculada al elemento padre mediante & */
  &:hover {
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  }

  /* Modificador o elemento anidado */
  &.card-active {
    border-color: var(--primary-color);
  }
}
```

> [!NOTE]
> El símbolo ampersand (`&`) hace referencia explícita al selector padre inmediato en el anidamiento.

---

## Autoevaluación

> [!QUIZ]
> ¿Qué diferencia principal existe entre las variables CSS nativas (`var(--mi-var)`) y las variables de preprocesadores como SASS (`$mi-var`)?
> - [ ] Las variables CSS nativas solo aceptan colores hex.
> - [x] Las variables CSS nativas son dinámicas, residen en el DOM y responden al tema del usuario en tiempo de ejecución.
> - [ ] Las variables de SASS funcionan sin servidor y las CSS nativas no.
>
> **Explicación**: Las Custom Properties de CSS existen vivas en el navegador y pueden cambiar con JavaScript o Media Queries.

---

## 🛠️ Ejercicio Práctico: Componente Card con Nesting y Variables

**Objetivo**: Construir el selector de una tarjeta interactiva utilizando variables de color en `:root` y Nesting nativo.

**Instrucciones**:
1. Declara la variable `--accent-color: #8b5cf6` en `:root`.
2. Crea la regla `.product-card`.
3. Anida la regla `&:hover` para aplicar un borde con `var(--accent-color)`.
4. Anida la regla `.btn-buy` dentro de `.product-card`.

<details class="exercise-solution">
<summary>💡 Ver solución explicada paso a paso</summary>

<div class="solution-content">

```css
:root {
  --accent-color: #8b5cf6;
  --text-dark: #1f2937;
}

.product-card {
  background: #ffffff;
  padding: 20px;
  border: 2px solid transparent;

  &:hover {
    border-color: var(--accent-color);
  }

  .btn-buy {
    background-color: var(--accent-color);
    color: white;
    padding: 10px 16px;
    border: none;
  }
}
```

**Explicación**: Las variables gestionan los temas de color y el Nesting nativo agrupa los estilos de `.product-card`, su estado `:hover` y su botón hijo en un único bloque limpio.
</div>
</details>
