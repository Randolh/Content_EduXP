# Lección 6: Tablas Semánticas y Estructuras de Datos

En esta lección aprenderás a construir tablas de datos accesibles y semánticas en HTML5 utilizando etiquetas como `<caption>`, `<thead>`, `<tbody>`, `<tfoot>`, `<th>` y los atributos `scope`, `colspan` y `rowspan`.

---

## 1. ¿Cuándo debemos usar Tablas en HTML5?

> [!WARNING]
> Las tablas deben usarse **exclusivamente para mostrar datos tabulares** (precios, horarios, datos estadísticos, comparativas). **Nunca** utilices tablas para maquetar el diseño visual de tu sitio web.

---

## 2. Estructura Semántica Completa de una Tabla

Una tabla accesible consta de tres partes principales (`<thead>`, `<tbody>`, `<tfoot>`) y una leyenda descriptiva (`<caption>`):

```html
<table>
  <caption>Comparativa de Planes de Suscripción EduXP</caption>
  
  <thead>
    <tr>
      <th scope="col">Plan</th>
      <th scope="col">Lecciones</th>
      <th scope="col">Precio Mensual</th>
    </tr>
  </thead>
  
  <tbody>
    <tr>
      <th scope="row">Gratuito</th>
      <td>Acceso a 5 lecciones</td>
      <td>$0</td>
    </tr>
    <tr>
      <th scope="row">PRO</th>
      <td>Acceso Ilimitado</td>
      <td>$15</td>
    </tr>
  </tbody>

  <tfoot>
    <tr>
      <td colspan="2">Todos los precios incluyen impuestos.</td>
      <td>USD</td>
    </tr>
  </tfoot>
</table>
```

---

## 3. Atributos Fundamentales para Accesibilidad y Combinación

### Atributo `scope` (Accesibilidad)
El atributo `scope` indica a los lectores de pantalla a qué grupo de celdas pertenece una celda de encabezado (`<th>`):
- `scope="col"`: El encabezado aplica a toda la **columna**.
- `scope="row"`: El encabezado aplica a toda la **fila**.

### Atributos `colspan` y `rowspan`
- `colspan="2"`: Hace que una celda se expanda abarcando 2 columnas horizontales.
- `rowspan="2"`: Hace que una celda se expanda abarcando 2 filas verticales.

---

## Autoevaluación

> [!QUIZ]
> ¿Cuál es la función del atributo `scope="col"` en un elemento `<th>`?
> - [ ] Definir el color de fondo de la celda de la columna.
> - [x] Indicar a los lectores de pantalla que esa celda es el encabezado de toda la columna vertical.
> - [ ] Fusionar dos columnas adyacentes.
>
> **Explicación**: El atributo `scope` es clave para la accesibilidad WAI-ARIA en tablas, asociando el encabezado con sus datos en la columna.

---

## 🛠️ Ejercicio Práctico: Tabla de Horario de Cursos

**Objetivo**: Construir una tabla semántica con título descriptivo y encabezados de columna.

**Instrucciones**:
1. Escribe el elemento `<table>` con un `<caption>` titulado `"Horario de Clases Semanales"`.
2. Define un `<thead>` con encabezados para `"Día"`, `"Módulo"` y `"Duración"`. Usa `scope="col"`.
3. Completa el `<tbody>` con dos filas de datos.

<details class="exercise-solution">
<summary>💡 Ver solución explicada paso a paso</summary>

<div class="solution-content">

```html
<table>
  <caption>Horario de Clases Semanales</caption>
  <thead>
    <tr>
      <th scope="col">Día</th>
      <th scope="col">Módulo</th>
      <th scope="col">Duración</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Lunes</th>
      <td>HTML5 Semántico</td>
      <td>2 Horas</td>
    </tr>
    <tr>
      <th scope="row">Miércoles</th>
      <td>CSS3 Moderno</td>
      <td>2 Horas</td>
    </tr>
  </tbody>
</table>
```

**Explicación**: La estructura separa el encabezado en `<thead>` del contenido en `<tbody>`, garantizando accesibilidad mediante los atributos `scope`.
</div>
</details>
