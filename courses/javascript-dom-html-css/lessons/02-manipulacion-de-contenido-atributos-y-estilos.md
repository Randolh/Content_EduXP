# 2. Manipulacion de Texto, Atributos, classList y Estilos Dinamicos

Una vez seleccionados los nodos del DOM, el siguiente paso fundamental es alterar su contenido, gestionar clases CSS para coordinar el aspecto visual, y leer o actualizar atributos personalizados sin comprometer la seguridad de la aplicacion.

---

## Objetivos de la Leccion
- Diferenciar entre `textContent`, `innerText` e `innerHTML` evaluando riesgos de seguridad XSS.
- Manipular clases CSS de alto rendimiento con la API `classList` (`add`, `remove`, `toggle`, `contains`).
- Consultar y definir atributos HTML personalizados mediante la API `dataset` (`data-*`).
- Actualizar variables nativas de CSS (Custom Properties) desde JavaScript.

---

## Modificacion de Contenido: `textContent` vs `innerHTML`

```javascript
const panel = document.querySelector("#panel-informativo");

// 1. textContent (RECOMENDADO PARA CADENAS DE TEXTO)
// Trata todo el valor como texto plano.
// Es seguro contra vulnerabilidades de Cross-Site Scripting (XSS).
panel.textContent = "El estado del servicio es: Operativo.";

// 2. innerHTML (SOLO PARA FRAGMENTOS HTML CONTROLADOS)
// Interpreta etiquetas y entidades HTML.
// NUNCA concatenes entradas no saneadas del usuario aqui.
panel.innerHTML = `
    <div class="alerta-box">
        <h3>Notificacion del Sistema</h3>
        <p>Los datos han sido sincronizados.</p>
    </div>
`;
```

> [!WARNING]
> **Vulnerabilidad de Cross-Site Scripting (XSS):**  
> Si asignas datos recibidos de un formulario o query string directamente a `innerHTML` (ej: `panel.innerHTML = inputUsuario;`), un atacante podria inyectar codigo `<script>` o etiquetas `<img>` maliciosas y comprometer la sesion de los usuarios.

---

## Gestion de Clases con `classList`

La mejor practica arquitectonica consiste en definir las reglas visuales dentro de tu archivo CSS y utilizar JavaScript unicamente para alternar clases de estado en los elementos del DOM:

```javascript
const botonMenu = document.querySelector("#btn-toggle-menu");
const barraLateral = document.querySelector("#sidebar");

// 1. Anadir una o varias clases
barraLateral.classList.add("activo", "sombra-elevada");

// 2. Remover clases
barraLateral.classList.remove("oculto");

// 3. Alternar estado (Si existe la remueve; si no existe la anade)
botonMenu.addEventListener("click", () => {
    barraLateral.classList.toggle("colapsado");
});

// 4. Verificar presencia de clase (Retorna valor booleano)
const estaAbierto = barraLateral.classList.contains("activo");
console.log(`Estado de barra lateral: ${estaAbierto}`);
```

---

## Atributos Personalizados con `dataset`

Los atributos de datos de HTML5 (`data-*`) permiten almacenar informacion en los nodos que JavaScript puede leer o mutar comodamente mediante la propiedad `.dataset`:

```html
<article 
  id="tarjeta-45" 
  class="tarjeta-producto" 
  data-producto-id="4590" 
  data-categoria-origen="hardware"
  data-requiere-envio="true">
  Tarjeta de Red Gigabit
</article>
```

```javascript
const tarjeta = document.querySelector("#tarjeta-45");

// Los nombres 'data-producto-id' se transforman automaticamente a camelCase:
const idProducto = tarjeta.dataset.productoId;           // "4590"
const categoria = tarjeta.dataset.categoriaOrigen;       // "hardware"
const envio = tarjeta.dataset.requiereEnvio === "true";  // Conversion a booleano

// Modificar o agregar un nuevo atributo de datos en tiempo real:
tarjeta.dataset.estadoStock = "disponible";
```

---

## Mutacion Dinamica de Variables CSS (`Custom Properties`)

En lugar de definir estilos individuales inline (`elemento.style.color = "red"`), la tecnica moderna consiste en alterar variables CSS globales definidas en `:root`:

```javascript
// Modificar la paleta de colores del tema en tiempo real
document.documentElement.style.setProperty("--color-primario", "#0284c7");
document.documentElement.style.setProperty("--espaciado-base", "1.5rem");
```

---

## Ejercicio Practico

Crea un contenedor `<div id="caja-noticia" class="noticia"></div>` y un boton.  
Escribe un script en JavaScript que al presionar el boton:
1. Verifique si el contenedor tiene la clase `noticia-destacada`.
2. Si no la tiene, anada la clase y modifique el `dataset.leido` a `"true"`.
3. Actualice el `textContent` indicando: `"Noticia leida y archivada"`.
