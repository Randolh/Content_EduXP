# Lección 10: Proyecto Integrador: Dashboard Responsivo en CSS Puro

¡Felicidades por llegar a la lección final del curso! En este proyecto integrador construirás la hoja de estilos completa en **CSS Puro Sin Frameworks** para un **Dashboard / Landing Page Responsiva**, integrando todo el arsenal del CSS moderno.

---

## 🎯 Objetivos del Proyecto

Debes escribir un archivo `styles.css` 100% estándar que incorpore:

1. **Modern Reset & Cascade Layers**: Estructura de capas `@layer reset, base, layout, components;`.
2. **Sistema de Temas con Variables (`:root`)**: Propiedades personalizadas para colores, tipografías, sombras y radios con soporte claro/oscuro.
3. **Layout Híbrido Flexbox + CSS Grid**: Estructuración del marco del dashboard con CSS Grid y barras/componentes internos con Flexbox.
4. **Rejilla de Tarjetas Autoadaptable**: Galería de métricas con `repeat(auto-fit, minmax(240px, 1fr))`.
5. **Componentes Modernos**: Uso de CSS Nesting nativo, pseudo-clases relacionales `:has()`, funciones fluidas `clamp()` y micro-interacciones animadas con `transition`.

---

## 📋 Especificaciones y Requisitos

```text
styles.css
├── @layer reset
├── @layer base (:root variables y tema)
├── @layer layout (Grid principal del Dashboard: Sidebar + Main Content)
└── @layer components
    ├── .stats-grid (CSS Grid auto-fit)
    ├── .card (Nesting + :has() + transition)
    └── .btn (Estilos interactivos)
```

---

## 🛠️ Solución Modelo del Proyecto Integrador

<details class="exercise-solution">
<summary>💡 Ver solución completa del Proyecto Integrador CSS</summary>

<div class="solution-content">

```css
/* ==========================================================================
   Proyecto Integrador: EduXP Dashboard CSS Moderno
   ========================================================================== */

/* 1. Declaración de Capas en la Cascada */
@layer reset, base, layout, components;

/* Capa 1: Modern Reset CSS */
@layer reset {
  *, *::before, *::after {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    min-height: 100vh;
    line-height: 1.5;
  }

  img {
    display: block;
    max-width: 100%;
  }
}

/* Capa 2: Variables y Estilos Base */
@layer base {
  :root {
    --bg-main: #f8fafc;
    --bg-surface: #ffffff;
    --text-primary: #0f172a;
    --text-muted: #64748b;
    --brand-color: #2563eb;
    --brand-accent: #8b5cf6;
    --border-color: #e2e8f0;
    --radius-lg: 12px;
    --shadow-sm: 0 1px 3px rgba(0, 0, 0, 0.1);
    --shadow-md: 0 4px 12px rgba(0, 0, 0, 0.08);
  }

  @media (prefers-color-scheme: dark) {
    :root {
      --bg-main: #0f172a;
      --bg-surface: #1e293b;
      --text-primary: #f8fafc;
      --text-muted: #94a3b8;
      --border-color: #334155;
    }
  }

  body {
    background-color: var(--bg-main);
    color: var(--text-primary);
    font-family: system-ui, -apple-system, sans-serif;
  }

  h1 {
    font-size: clamp(1.5rem, 3vw, 2.5rem);
  }
}

/* Capa 3: Layout del Dashboard */
@layer layout {
  .dashboard-container {
    display: grid;
    grid-template-columns: 1fr; /* Columna única en móviles */
    min-height: 100vh;

    @media (min-width: 768px) {
      grid-template-columns: 260px 1fr; /* Sidebar + Contenido en escritorio */
    }
  }

  .sidebar {
    background-color: var(--bg-surface);
    border-right: 1px solid var(--border-color);
    padding: 24px;
    display: flex;
    flex-direction: column;
    gap: 16px;
  }

  .main-content {
    padding: clamp(16px, 3vw, 32px);
    display: flex;
    flex-direction: column;
    gap: 24px;
  }
}

/* Capa 4: Componentes del Dashboard */
@layer components {
  /* Rejilla de métricas responsiva sin media queries */
  .stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 20px;
  }

  /* Componente de Tarjeta con Nesting y Pseudo-clases relacionales */
  .stat-card {
    background-color: var(--bg-surface);
    padding: 20px;
    border-radius: var(--radius-lg);
    border: 1px solid var(--border-color);
    box-shadow: var(--shadow-sm);
    transition: transform 0.2s ease, box-shadow 0.2s ease;

    &:hover {
      transform: translateY(-3px);
      box-shadow: var(--shadow-md);
    }

    /* Si la tarjeta incluye una alerta de tendencia positiva */
    &:has(.trend-up) {
      border-left: 4px solid #22c55e;
    }

    .card-title {
      font-size: 0.9rem;
      color: var(--text-muted);
      margin-bottom: 8px;
    }

    .card-value {
      font-size: 1.8rem;
      font-weight: 700;
    }
  }

  /* Botón con Variables y Micro-interacción */
  .btn-primary {
    background-color: var(--brand-color);
    color: #ffffff;
    padding: 10px 20px;
    border-radius: 8px;
    border: none;
    font-weight: 600;
    cursor: pointer;
    transition: background-color 0.2s ease, transform 0.1s ease;

    &:hover {
      background-color: color-mix(in srgb, var(--brand-color) 85%, black);
    }

    &:active {
      transform: scale(0.98);
    }
  }
}
```

</div>
</details>

---

## 🎓 ¡Felicidades!
Has completado con éxito el curso **CSS Moderno Sin Frameworks**. ¡Ahora dominas el estándar nativo de CSS para crear maquetas web rápidas, fluidas, escalables y profesionales!
