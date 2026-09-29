# 1. El Arbol del DOM, Nodos y Seleccion con querySelector

El **Document Object Model (DOM)** es la interfaz de programacion que representa un documento HTML como una estructura jerarquica de objetos en memoria. JavaScript interactua con el DOM para consultar, alterar, agregar o eliminar elementos de la pagina de forma dinamica.

---

## Objetivos de la Leccion
- Comprender la estructura de nodos del DOM (`Document`, `Element`, `Text`, `Comment`).
- Utilizar los metodos modernos de seleccion: `querySelector` y `querySelectorAll`.
- Diferenciar entre una `NodeList` estatica y una `HTMLCollection` viva.
- Transformar listas de nodos en arreglos JavaScript nativos para operaciones avanzadas.

---

## La Jerarquia del Arbol del DOM

Cuando el motor de renderizado del navegador procesa el marcado HTML, genera un arbol de nodos comenzando en la raiz global `window.document`:

```text
                        [ document ]
                             │
                             ▼
                          [ <html> ]
                             │
            ┌────────────────┴────────────────┐
            ▼                                 ▼
        [ <head> ]                        [ <body> ]
            │                                 │
     ┌──────┴──────┐                ┌─────────┴─────────┐
     ▼             ▼                ▼                   ▼
 [ <title> ]   [ <meta> ]       [ <header> ]        [ <main> ]
                                    │                   │
                                [ <h1> ]            [ <section> ]
```

Cada etiqueta representa un nodo de tipo elemento (`Node.ELEMENT_NODE`), el texto interior representa un nodo de texto (`Node.TEXT_NODE`) y los atributos representan metadatos asociados.

---

## Seleccion de Elementos con Selectores CSS

El estandar actual descarta metodos legados como `document.getElementsByTagName` o `document.anchors` en favor de la API de Selectores CSS:

### 1. `document.querySelector(selectorCSS)`
Retorna **el primer elemento** que coincide exactamente con la regla CSS proporcionada, o `null` si no existe coincidencia:

```javascript
// Seleccion por Identificador ID
const encabezadoPrincipal = document.querySelector("#main-header");

// Seleccion por Clase CSS
const tarjetaPrincipal = document.querySelector(".card-item");

// Seleccion por Atributo y Descendencia
const entradaCorreo = document.querySelector("form.login-form input[type='email']");
```

### 2. `document.querySelectorAll(selectorCSS)`
Retorna una coleccion indexada de tipo **`NodeList`** que contiene todos los elementos coincidentes en el orden del documento:

```javascript
const botonesAccion = document.querySelectorAll(".btn-action");

console.log(`Cantidad de botones detectados: ${botonesAccion.length}`);

// NodeList dispone de forma nativa del metodo .forEach:
botonesAccion.forEach((boton, indice) => {
    console.log(`Boton [${indice}]:`, boton.textContent);
});

// Conversion a Array nativo para aplicar map, filter o reduce:
const arregloBotones = Array.from(botonesAccion);
// O alternativamente mediante Spread Operator:
const arregloSpread = [...botonesAccion];
```

---

## Comparativa de Rendimiento y Tipos de Retorno

| Metodo | Retorno | Tipo de Coleccion | Soporta Selectores Complejos |
| :--- | :--- | :--- | :--- |
| `querySelector()` | `Element` o `null` | N/A | Si (Selectores CSS nivel 3/4) |
| `querySelectorAll()` | `NodeList` | Estatica (Snapshot) | Si |
| `getElementById()` | `Element` o `null` | N/A | No (Solo ID exacto) |
| `getElementsByClassName()` | `HTMLCollection` | Viva (Live) | No (Solo nombre de clase) |

> [!NOTE]
> Una coleccion "viva" (`HTMLCollection`) se actualiza automaticamente en memoria si el DOM sufre modificaciones, lo que puede causar ciclos infinitos accidentales si se itera mientras se insertan nodos. Por esta razon, la comunidad prefiere las `NodeList` estaticas generadas por `querySelectorAll`.

---

## Ejercicio Practico

Dada la siguiente estructura HTML:
```html
<ul id="lista-servidores">
  <li class="nodo" data-status="online">Servidor 1</li>
  <li class="nodo" data-status="offline">Servidor 2</li>
  <li class="nodo" data-status="online">Servidor 3</li>
</ul>
```
Escribe el codigo JavaScript para:
1. Seleccionar unicamente los elementos `<li>` que posean el atributo `data-status="online"`.
2. Convertir la lista resultante a un arreglo y mapear una lista con los nombres de texto en mayusculas.
