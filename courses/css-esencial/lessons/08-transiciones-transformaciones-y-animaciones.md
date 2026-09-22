# Lección 8: Transiciones, Transformaciones 2D/3D y `@keyframes`

En esta lección aprenderás a darle vida a la interfaz de usuario mediante **Transiciones CSS**, transformaciones geométricas (`transform`) y animaciones complejas personalizadas con `@keyframes`.

---

## 1. Transiciones Suaves (`transition`)

Las transiciones permiten interpolar cambios de propiedades CSS suavemente en lugar de ocurrir de forma instantánea:

```css
.btn {
  background-color: #2563eb;
  color: white;
  padding: 12px 24px;
  border-radius: 8px;
  /* Transicionar propiedad, duración, función de tiempo */
  transition: background-color 0.3s ease, transform 0.2s ease;
}

.btn:hover {
  background-color: #1d4ed8;
  transform: translateY(-3px); /* Eleva ligeramente el botón */
}
```

- Propiedades óptimas para animar: `opacity` y `transform` (utilizan aceleración por hardware GPU y no provocan *reflow*).

---

## 2. Transformaciones 2D y 3D (`transform`)

Permiten alterar la posición, rotación, escala o inclinación de un elemento:

- `translate(x, y)`: Mueve el elemento en los ejes X e Y.
- `scale(1.1)`: Aumenta o disminuye el tamaño (1.1 = 110%).
- `rotate(45deg)`: Rota el elemento en grados.
- `perspective(500px) rotateY(180deg)`: Efectos 3D como voltear una tarjeta.

```css
.card-flip {
  transition: transform 0.6s ease;
  transform-style: preserve-3d;
}

.card-flip:hover {
  transform: rotateY(180deg);
}
```

---

## 3. Animaciones Complejas con `@keyframes`

Las animaciones permiten crear secuencias multinivel con múltiples fotogramas clave (*keyframes*):

```css
/* 1. Definición del Keyframe */
@keyframes pulseGlow {
  0% {
    transform: scale(1);
    box-shadow: 0 0 0 0 rgba(37, 99, 235, 0.4);
  }
  50% {
    transform: scale(1.05);
    box-shadow: 0 0 0 12px rgba(37, 99, 235, 0);
  }
  100% {
    transform: scale(1);
    box-shadow: 0 0 0 0 rgba(37, 99, 235, 0);
  }
}

/* 2. Asignación al elemento */
.badge-live {
  /* nombre duración función-de-tiempo repetición */
  animation: pulseGlow 2s infinite ease-in-out;
}
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué dos propiedades CSS son las más recomendadas para animar debido a su alto rendimiento al ejecutarse directamente en la tarjeta gráfica (GPU)?
> - [ ] `width` y `height`.
> - [x] `transform` y `opacity`.
> - [ ] `margin-top` y `padding-left`.
>
> **Explicación**: `transform` y `opacity` son procesadas por la GPU sin forzar el recalculado del layout (*reflow*) en el procesador principal.

---

## 🛠️ Ejercicio Práctico: Botón Interactivo con Elevación y Sombra

**Objetivo**: Crear la animación interactiva de un botón al pasar el cursor (`:hover`) utilizando `transition` y `transform`.

**Instrucciones**:
1. Crea la clase `.btn-animated`.
2. Aplica `transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1)`.
3. En el estado `&:hover`, aplica `transform: translateY(-4px) scale(1.02)` y una sombra `box-shadow: 0 8px 20px rgba(0,0,0,0.15)`.

<details class="exercise-solution">
<summary>💡 Ver solución explicada paso a paso</summary>

<div class="solution-content">

```css
.btn-animated {
  background-color: #0f172a;
  color: #ffffff;
  padding: 14px 28px;
  border-radius: 8px;
  border: none;
  cursor: pointer;
  transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1), box-shadow 0.3s ease;

  &:hover {
    transform: translateY(-4px) scale(1.02);
    box-shadow: 0 8px 20px rgba(15, 23, 42, 0.25);
  }

  &:active {
    transform: translateY(-1px) scale(0.99);
  }
}
```

**Explicación**: La transición suaviza el cambio de elevación con `translateY` y escala al pasar sobre el botón, creando una experiencia táctil fluida.
</div>
</details>
