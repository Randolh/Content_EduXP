# 3. Creacion, Eliminacion de Nodos y Rendimiento con DocumentFragment

En aplicaciones web reactivas es indispensable construir nuevos fragmentos de interfaz en tiempo real (por ejemplo, al renderizar resultados de una busqueda o nuevos elementos de una lista). En esta leccion exploraras metodos de mutacion del DOM y optimizaciones de rendimiento criticas.

---

## Objetivos de la Leccion
- Crear nodos de tipo elemento con `document.createElement()`.
- Insertar nodos de forma segura utilizando `append()`, `prepend()` y `before()`/`after()`.
- Eliminar elementos del DOM mediante el metodo nativo `.remove()`.
- Prevenir operaciones de Reflow y Repaint recurrentes utilizando `DocumentFragment`.

---

## Creacion e Insercion de Nodos en Memoria

```javascript
// 1. Instanciacion del elemento en memoria (Aun no presente en el DOM visible)
const nuevoArticulo = document.createElement("article");

// 2. Configuracion de clases, atributos y estructura
nuevoArticulo.classList.add("tarjeta-informativa");
nuevoArticulo.dataset.prioridad = "alta";

const titulo = document.createElement("h3");
titulo.textContent = "Alerta de Servidor";

const parrafo = document.createElement("p");
parrafo.textContent = "Uso de memoria superior al umbral del 85%.";

// 3. Ensamblaje interno del componente
// append() admite multiples nodos hijos o texto plano de una sola vez
nuevoArticulo.append(titulo, parrafo);

// 4. Insercion final en el DOM visible
const contenedorAlertas = document.querySelector("#contenedor-alertas");
contenedorAlertas.append(nuevoArticulo);    // Inserta al final
// contenedorAlertas.prepend(nuevoArticulo); // Inserta al principio
```

---

## Eliminacion de Nodos

Para remover un elemento de la vista activa:

```javascript
const elementoRemover = document.querySelector("#alerta-obsoleta");

// Metodo estandar contemporaneo:
elementoRemover.remove();
```

---

## Optimizacion de Rendimiento: Reflow, Repaint y `DocumentFragment`

Cada vez que un nodo se inserta directamente en el arbol del DOM visible, el motor del navegador se ve forzado a recalcular la geometria espacial de la pagina (**Reflow**) y redibujar los pixeles en pantalla (**Repaint**).

Si insertas 100 elementos de una lista uno a uno dentro de un bucle `for`, provocaras 100 operaciones consecutivas de Reflow, causando saltos y congelamiento de la interfaz:

```javascript
// MALA PRACTICA (Provoca 50 Reflows continuos):
const lista = document.querySelector("#mi-lista");
for (let i = 0; i < 50; i++) {
    const li = document.createElement("li");
    li.textContent = `Registro ${i}`;
    lista.append(li); // Impacto negativo en el rendimiento
}
```

### Solucion Optima: `DocumentFragment`
Un `DocumentFragment` es un contenedor virtual y ligero que vive exclusivamente en memoria RAM fuera del arbol de renderizado del documento:

```javascript
const lista = document.querySelector("#mi-lista");
const registros = ["Servidor Alpha", "Servidor Beta", "Servidor Gamma", "Servidor Delta"];

// 1. Creacion del fragmento en memoria
const fragmento = document.createDocumentFragment();

registros.forEach(nombreHost => {
    const li = document.createElement("li");
    li.classList.add("item-servidor");
    li.textContent = nombreHost;
    
    // Insercion en el fragmento (Cero impacto de renderizado en el navegador)
    fragmento.append(li);
});

// 2. Insercion UNICA de todos los elementos en el DOM real (Un solo Reflow)
lista.append(fragmento);
```

---

## Ejercicio Practico

Dado un arreglo con 10 nombres de usuarios en formato JSON:
1. Crea un `DocumentFragment`.
2. Itera sobre los datos generando elementos `<div class="tarjeta-usuario">`.
3. Anade a cada tarjeta un nombre y un boton con la clase `.btn-eliminar`.
4. Inserta el fragmento en un contenedor principal `#usuarios-grid` en una sola operacion atomica.
