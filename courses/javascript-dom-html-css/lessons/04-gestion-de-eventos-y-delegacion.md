# 4. Escuchadores de Eventos (addEventListener) y Delegacion de Eventos

Los **Eventos** representan senales emitidas por el navegador para notificar que una interaccion o cambio de estado ha tenido lugar (clics, pulsaciones de teclas, redimensionamiento, scroll). En esta leccion exploraras el ciclo de propagacion de eventos y la arquitectura de **Delegacion de Eventos**.

---

## Objetivos de la Leccion
- Registrar eventos mediante `addEventListener()` y procesar el objeto `Event`.
- Comprender el flujo de propagacion: Fases de Captura, Objetivo y Burbujeo (Bubbling).
- Cancelar acciones nativas con `preventDefault()` y detener propagacion con `stopPropagation()`.
- Implementar el patron arquitectonico de **Delegacion de Eventos** sobre elementos dinamicos.

---

## Escuchadores de Eventos (`addEventListener`)

El metodo `addEventListener` vincula una funcion controladora (Event Handler) a un evento especifico sin sobreescribir escuchadores previos:

```javascript
const botonGuardar = document.querySelector("#btn-guardar");

botonGuardar.addEventListener("click", (event) => {
    console.log("Tipo de evento:", event.type);          // "click"
    console.log("Elemento emisor:", event.target);        // <button id="btn-guardar">
    console.log("Elemento receptor:", event.currentTarget);
    console.log("Coordenadas pantalla:", event.clientX, event.clientY);
});
```

---

## Propagacion de Eventos: Burbujeo (Event Bubbling)

Cuando un evento ocurre sobre un elemento hijo, viaja a traves de tres etapas:
1. **Fase de Captura:** El evento desciende desde `window` y `document` hasta el elemento objetivo.
2. **Fase de Objetivo:** El evento alcanza el nodo exacto que recibio la interaccion.
3. **Fase de Burbujeo (Bubbling):** El evento asciende secuencialmente desde el elemento hijo pasando por todos sus nodos contenedores padres hasta llegar a la raiz.

```text
Flujo de Burbujeo:
[ document ]         ▲
     │               │ (El evento asciende de forma natural)
[ <section> ]        │
     │               │
[ <ul> ]             │
     │               │
[ <button> ] ────────┘  <-- Clic original del usuario
```

### Control de Comportamientos
```javascript
// Prevenir la recarga predeterminada al hacer submit o al presionar enlaces:
event.preventDefault();

// Detener que el evento continue ascendiendo hacia los padres:
event.stopPropagation();
```

---

## Arquitectura de Delegacion de Eventos

Cuando tienes una lista con cientos de elementos o elementos que se crean dinamicamente en tiempo de ejecucion, agregar un `addEventListener` individual a cada elemento consume memoria innecesaria y fallara con los nuevos elementos creados a futuro.

La **Delegacion de Eventos** aprovecha el burbujeo colocando **un solo escuchador en el contenedor padre** y verificando que elemento hijo disparo la accion mediante `event.target` o `event.target.closest()`:

```html
<ul id="lista-inventario">
  <li data-id="101">Item 1 <button class="btn-borrar">Eliminar</button></li>
  <li data-id="102">Item 2 <button class="btn-borrar">Eliminar</button></li>
</ul>
```

```javascript
// UN SOLO escuchador de eventos para toda la lista:
const listaContenedor = document.querySelector("#lista-inventario");

listaContenedor.addEventListener("click", (event) => {
    // Comprobar si el clic impacto en un boton con la clase btn-borrar
    if (event.target.classList.contains("btn-borrar")) {
        // Localizar el ancestro <li> mas cercano con .closest()
        const filaElemento = event.target.closest("li");
        const idRegistro = filaElemento.dataset.id;
        
        console.log(`Eliminando registro ID: ${idRegistro}`);
        filaElemento.remove();
    }
});
```

> [!TIP]
> La Delegacion de Eventos es la tecnica mas eficiente en interfaces ricas: reduce el uso de memoria RAM, simplifica la limpieza de listeners y maneja nodos generados por AJAX o fetch de forma automatica.

---

## Ejercicio Practico

Construye una lista dinamica de compras:
1. Registra un solo escuchador de eventos sobre el contenedor `<ul>`.
2. Cada `<li>` tendra un boton para marcar como "Completado" y otro para "Eliminar".
3. Implementa la logica completa en el manejador del padre utilizando `event.target.closest()`.
