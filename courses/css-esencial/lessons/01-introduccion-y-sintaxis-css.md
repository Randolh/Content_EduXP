# Lección 1: Reglas, Selectores, Especificidad y Cascada

¡Bienvenido al curso de **CSS Moderno Sin Frameworks**! En esta lección aprenderás cómo funciona el motor de estilos de los navegadores web: la sintaxis de las reglas CSS, los tipos de selectores, el algoritmo de la **Cascada** y el cálculo de la **Especificidad**.

---

## 1. Anatoma de una Regla CSS

**CSS** (*Cascading Style Sheets*) define la presentación visual de los elementos HTML. Una regla CSS consta de un selector y un bloque de declaraciones (propiedades y valores):

```css
/* Selector { Propiedad: Valor; } */
.btn-primary {
  background-color: #2563eb;
  color: #ffffff;
  padding: 10px 20px;
  border-radius: 6px;
}
```

---

## 2. Tipos de Selectores Básicos

1. **Selector de Elemento/Etiqueta**: Aplica a todas las etiquetas coincidentes.
   ```css
   h1 { color: #1e293b; }
   ```
2. **Selector de Clase (`.`)**: Reutilizable en múltiples elementos HTML.
   ```css
   .card { background: #f8fafc; }
   ```
3. **Selector de ID (`#`)**: Aplica a un elemento único con ese ID.
   ```css
   #header-principal { background: #0f172a; }
   ```
4. **Selector de Atributo**: Selecciona elementos según sus atributos.
   ```css
   input[type="email"] { border-color: #3b82f6; }
   ```

---

## 3. Entendiendo la Cascada y la Especificidad

Cuando dos o más reglas CSS aplican estilos contradictorios al mismo elemento, el navegador resuelve el conflicto mediante la **Cascada** y el cálculo de la **Especificidad**.

### La Jerarquía de Especificidad (De mayor a menor peso):

```text
 Estilos Inline (style="...")  ──►  1, 0, 0, 0 (Peso más alto)
 Selectores de ID (#header)    ──►  0, 1, 0, 0
 Clases/Atributos (.btn, [type])──►  0, 0, 1, 0
 Etiquetas/Elementos (p, div) ──►  0, 0, 0, 1
 Selector Universal (*)        ──►  0, 0, 0, 0 (Peso más bajo)
```

### Ejemplo de Conflicto:

```html
<button id="btn-submit" class="btn btn-primary" style="color: yellow;">Enviar</button>
```

```css
button { color: red; }           /* (0, 0, 0, 1) */
.btn-primary { color: green; }   /* (0, 0, 1, 0) */
#btn-submit { color: blue; }     /* (0, 1, 0, 0) */
```

> **Resultado Visual**: El botón tendrá el color `yellow` debido al estilo inline (o `blue` si no hubiera estilo inline). El ID vence a las clases y las clases vencen a las etiquetas.

> [!WARNING]
> Evita a toda costa utilizar `!important` (ej. `color: red !important;`) para resolver problemas de especificidad. El mal uso de `!important` rompe la cascada y dificulta el mantenimiento del código.

---

## Autoevaluación

> [!QUIZ]
> Si un elemento HTML recibe estilos de un selector de clase `.card` y de un selector de ID `#card-info`, ¿cuál regla prevalecerá?
> - [ ] Prevalecerá `.card` porque las clases son más modernas.
> - [x] Prevalecerá `#card-info` porque los selectores de ID poseen mayor peso de especificidad.
> - [ ] El navegador mostrará un error sintáctico.
>
> **Explicación**: Los selectores de ID tienen una especificidad (0,1,0,0) superior a los de clase (0,0,1,0).

---

## 🛠️ Ejercicio Práctico: Cálculo de Especificidad

**Objetivo**: Ordenar tres reglas CSS en función de cuál aplicará efectivamente los estilos al elemento.

**Instrucciones**:
Dado el siguiente código HTML:
```html
<p id="destacado" class="texto-importante aviso">Texto de prueba</p>
```
Y las reglas CSS:
```css
/* Regla A */
.aviso { color: blue; }

/* Regla B */
p.texto-importante { color: green; }

/* Regla C */
#destacado { color: purple; }
```
¿Cuál será el color final del texto y por qué?

<details class="exercise-solution">
<summary>💡 Ver solución explicada paso a paso</summary>

<div class="solution-content">

**Color Final**: `purple`.

**Explicación por Especificidad**:
- Regla A (`.aviso`): (0, 0, 1, 0)
- Regla B (`p.texto-importante`): 1 etiqueta + 1 clase = (0, 0, 1, 1)
- Regla C (`#destacado`): 1 ID = (0, 1, 0, 0)

La Regla C tiene el peso más alto debido al selector de ID `#destacado`.
</div>
</details>
