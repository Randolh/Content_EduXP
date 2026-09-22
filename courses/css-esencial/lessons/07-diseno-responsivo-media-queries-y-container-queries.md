# Lección 7: Responsive Design, Funciones (`clamp`) y Container Queries

En esta lección aprenderás las técnicas modernas para adaptar interfaces a cualquier dispositivo: estrategia **Mobile-First**, la función matemática fluida `clamp()` y la revolucionaria API **Container Queries (`@container`)**.

---

## 1. Estrategia Mobile-First y Media Queries

El enfoque **Mobile-First** consiste en escribir primero los estilos base para teléfonos móviles sin media queries y usar `@media (min-width: ...)` para agregar capas de complejidad en pantallas más grandes.

```css
/* Estilos Base para Pantallas Móviles */
.sidebar {
  display: none;
}

/* Tablet (Monitores pequeños en adelante) */
@media (min-width: 768px) {
  .sidebar {
    display: block;
    width: 200px;
  }
}

/* Escritorio Grandes (Monitores HD) */
@media (min-width: 1024px) {
  .sidebar {
    width: 280px;
  }
}
```

---

## 2. Tipografía y Espaciados Fluidos con `clamp()`

La función `clamp(Mínimo, Ideal, Máximo)` permite escalar dinámicamente un valor entre un límite inferior y uno superior en función del ancho del viewport, eliminando múltiples media queries:

```css
h1 {
  /* El tamaño será de mínimo 1.8rem, crecerá fluidamente a un 4% de la pantalla y nunca superará los 3.2rem */
  font-size: clamp(1.8rem, 4vw, 3.2rem);
  padding: clamp(12px, 2vw, 32px);
}
```

---

## 3. La Nueva Era: Container Queries (`@container`)

Las **Media Queries** tradicionales responden únicamente al tamaño de la pantalla completa (`viewport`). Sin embargo, en arquitecturas compuestas por componentes reusables (como una tarjeta), el componente debe adaptarse al **ancho de su contenedor padre**, no de la pantalla.

Ahí es donde entran las **Container Queries**:

### 1. Definir el Contenedor:
```css
.card-wrapper {
  container-type: inline-size;
  container-name: card-container;
}
```

### 2. Escribir Reglas Basadas en el Ancho del Padre:
```css
.product-card {
  display: flex;
  flex-direction: column; /* En contenedores estrechos, alineación vertical */
}

/* Cuando el contenedor PADRE mida 400px o más (sin importar la pantalla) */
@container card-container (min-width: 400px) {
  .product-card {
    flex-direction: row;  /* Cambia automáticamente a layout horizontal */
    align-items: center;
  }
}
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué ventaja fundamental ofrecen las Container Queries (`@container`) en comparación con las Media Queries tradicionales (`@media`)?
> - [ ] Permiten cambiar el color de las fuentes tipográficas según la hora del día.
> - [x] Permiten que un componente adapte su diseño en función del tamaño de su contenedor padre inmediato, en lugar del viewport de la pantalla completa.
> - [ ] Eliminan la necesidad de utilizar etiquetas HTML.
>
> **Explicación**: Container Queries independizan el diseño de un componente de la resolución de la pantalla.

---

## 🛠️ Ejercicio Práctico: Título Fluido con `clamp()`

**Objetivo**: Aplicar un tamaño de fuente dinámico y fluido a un título principal `<h1>` utilizando la función `clamp()`.

**Instrucciones**:
1. Escribe la regla para la clase `.hero-title`.
2. Utiliza `font-size: clamp(2rem, 5vw, 4rem)`.
3. Aplica un margen inferior fluido con `margin-bottom: clamp(16px, 3vw, 40px)`.

<details class="exercise-solution">
<summary>💡 Ver solución explicada paso a paso</summary>

<div class="solution-content">

```css
.hero-title {
  font-size: clamp(2rem, 5vw, 4rem);
  margin-bottom: clamp(16px, 3vw, 40px);
  color: #0f172a;
  line-height: 1.2;
}
```

**Explicación**: El texto cambiará de tamaño suavemente según el viewport: en móviles medirá 2rem, en pantallas intermedias 5vw y en monitores gigantes se detendrá exactamente en 4rem.
</div>
</details>
