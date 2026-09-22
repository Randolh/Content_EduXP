# Lección 9: Cascade Layers (`@layer`) y Modern Reset CSS

En esta lección aprenderás a organizar proyectos de CSS a gran escala eliminando las guerras de especificidad mediante la nueva característica estándar de **Cascade Layers (`@layer`)** y aplicando un **Modern Reset CSS**.

---

## 1. El Reseteo CSS Moderno (Modern Reset)

Los navegadores aplican estilos por defecto (márgenes en body, tamaños en h1, etc.) que varían entre Chrome, Firefox y Safari. Un **Modern Reset** normaliza estas diferencias de forma limpia:

```css
/* Modern Reset CSS Base */
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html {
  color-scheme: light dark;
  font-family: system-ui, -apple-system, sans-serif;
  line-height: 1.5;
}

body {
  min-height: 100vh;
  text-rendering: optimizeSpeed;
}

img, picture, video, svg {
  display: block;
  max-width: 100%;
}

input, button, textarea, select {
  font: inherit;
}
```

---

## 2. Cascade Layers (`@layer`)

Históricamente, para sobrescribir los estilos de una librería o reset se requerían selectores largos con alta especificidad. Con **Cascade Layers**, puedes ordenar explícitamente qué capas de código tienen prioridad sobre otras, **independientemente del peso del selector**.

### Declaración de Capas y Orden de Prioridad:

```css
/* 1. Declarar el orden de precedencia (la última capa definida TIENE LA MAYOR PRIORIDAD) */
@layer reset, base, components, utilities;

/* Capa 1: Reset inicial */
@layer reset {
  button {
    background: transparent;
    border: none;
  }
}

/* Capa 2: Componentes del sitio */
@layer components {
  .btn-submit {
    background-color: #2563eb;
    color: white;
    padding: 10px 20px;
  }
}

/* Capa 3: Utilidades */
@layer utilities {
  .text-center { text-align: center; }
  .hidden { display: none !important; }
}
```

- En este ejemplo, los estilos dentro de `@layer components` o `@layer utilities` **siempre vencerán** a los de `@layer reset`, incluso si `@layer reset` usara un selector con ID (`#btn`).

---

## 3. La Función `color-mix()` de CSS Moderno

CSS nativo ahora permite mezclar colores directamente en la hoja de estilos sin herramientas externas:

```css
:root {
  --brand-color: #3b82f6;
  /* Mezcla un 20% de blanco con un 80% de brand-color para crear una variante clara */
  --brand-light: color-mix(in srgb, var(--brand-color) 80%, white);
  /* Mezcla un 10% de negro para una variante oscura */
  --brand-dark: color-mix(in srgb, var(--brand-color) 90%, black);
}
```

---

## Autoevaluación

> [!QUIZ]
> En la declaración `@layer reset, base, components;`, ¿cuál capa de estilos posee la mayor prioridad en la cascada?
> - [ ] La capa `@layer reset` por ser la primera.
> - [x] La capa `@layer components` por ser la última capa declarada en la lista.
> - [ ] Todas las capas tienen exactamente la misma prioridad.
>
> **Explicación**: En Cascade Layers, las capas declaradas al final de la lista tienen mayor prioridad sobre las anteriores.

---

## 🛠️ Ejercicio Práctico: Estructurar Capas de Código con `@layer`

**Objetivo**: Organizar los estilos de un proyecto separando la capa base de la capa de componentes.

**Instrucciones**:
1. Declara las capas `@layer base, components;`.
2. En `@layer base`, asigna a `body` un fondo claro `background-color: #f8fafc`.
3. En `@layer components`, crea la regla `.card` con `background-color: #ffffff`.

<details class="exercise-solution">
<summary>💡 Ver solución explicada paso a paso</summary>

<div class="solution-content">

```css
@layer base, components;

@layer base {
  body {
    background-color: #f8fafc;
    color: #0f172a;
    font-family: system-ui, sans-serif;
  }
}

@layer components {
  .card {
    background-color: #ffffff;
    border-radius: 12px;
    padding: 24px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
  }
}
```

**Explicación**: Las capas quedan aisladas lógicamente. Los componentes en `@layer components` prevalecen limpiamente sobre las reglas globales de `@layer base`.
</div>
</details>
