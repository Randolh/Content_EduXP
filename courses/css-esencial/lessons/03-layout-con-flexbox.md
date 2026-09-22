# Lección 3: Layouts Unidimensionales con Flexbox

En esta lección aprenderás a dominar **Flexible Box Layout (Flexbox)**, el módulo de CSS diseñado para alinear, distribuir y organizar elementos en una sola dimensión (fila o columna).

---

## 1. El Contenedor Flex y los Ejes (Main & Cross Axis)

Al aplicar `display: flex` a un elemento padre, este se convierte en un **Contenedor Flex** y sus hijos inmediatos en **Flex Items**.

```text
                  Eje Principal (Main Axis)
       ──────────────────────────────────────────────►
   ┌───┬───────────────────────────────────────────┐
E  │   │  Flex Item 1   Flex Item 2   Flex Item 3  │
j  │ C │ ┌────────────┐ ┌────────────┐ ┌──────────┐ │
e  │ r │ │            │ │            │ │          │ │
   │ o │ └────────────┘ └────────────┘ └──────────┘ │
S  │ s │                                           │
e  │ s │                                           │
c  ▼   └───────────────────────────────────────────┘
```

---

## 2. Propiedades Principales del Contenedor Flex

### `flex-direction`
Establece la dirección del eje principal:
- `row` (Por defecto): De izquierda a derecha en fila.
- `column`: De arriba a abajo en columna.
- `row-reverse` / `column-reverse`: Invierte la dirección.

### `justify-content` (Alineación en el Eje Principal)
Distribuye el espacio sobrante a lo largo del eje principal:
- `flex-start` / `flex-end`: Al inicio o al final.
- `center`: Centrado perfecto.
- `space-between`: Espacio igual **entre** elementos (sin espacio en los bordes).
- `space-around` / `space-evenly`: Espaciado uniforme distribuido alrededor.

### `align-items` (Alineación en el Eje Secundario)
Controla la alineación perpendicular:
- `stretch` (Por defecto): Estira los items para llenar el contenedor.
- `center`: Centra los items verticalmente.
- `flex-start` / `flex-end`: Alinea al inicio o al final.

### `flex-wrap` y `gap`
- `flex-wrap: wrap`: Permite que los ítems salten a una nueva línea si no caben.
- `gap: 16px`: Define la separación exacta entre filas y columnas flex sin usar márgenes.

---

## 3. Propiedades de los Hijos (`Flex Items`)

- `flex-grow: 1`: Determina cuánto puede crecer un elemento si hay espacio disponible.
- `flex-shrink: 1`: Determina cuánto se puede encoger si falta espacio.
- `flex-basis: 200px`: Define el tamaño base inicial antes de distribuir el espacio.
- `flex: 1`: Atajo (*shorthand*) para `flex-grow flex-shrink flex-basis`.

### El Famoso Centrado Perfecto con Flexbox:

```css
.card-container {
  display: flex;
  justify-content: center; /* Centrado horizontal */
  align-items: center;     /* Centrado vertical */
  min-height: 100vh;
}
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué combinación de propiedades Flexbox logra centrar un elemento hijo tanto horizontal como verticalmente dentro de su contenedor?
> - [ ] `flex-direction: center; flex-wrap: wrap;`
> - [x] `justify-content: center; align-items: center;`
> - [ ] `align-content: space-between; gap: 0;`
>
> **Explicación**: `justify-content: center` centra en el eje principal y `align-items: center` en el eje cruzado.

---

## 🛠️ Ejercicio Práctico: Barra de Navegación Flexbox

**Objetivo**: Crear una barra de navegación accesible con el logotipo a la izquierda y los enlaces agrupados a la derecha.

**Instrucciones**:
1. Crea un contenedor `.navbar` con `display: flex`.
2. Utiliza `justify-content: space-between` y `align-items: center`.
3. Añade un espacio `gap: 20px` entre los enlaces de navegación.

<details class="exercise-solution">
<summary>💡 Ver solución explicada paso a paso</summary>

<div class="solution-content">

```css
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 32px;
  background-color: #0f172a;
  color: #ffffff;
}

.nav-links {
  display: flex;
  gap: 20px;
  list-style: none;
}
```

**Explicación**: `justify-content: space-between` empuja el logotipo a un extremo y la lista de enlaces al otro, mientras que `.nav-links` usa Flexbox secundario con `gap` para separar los items.
</div>
</details>
