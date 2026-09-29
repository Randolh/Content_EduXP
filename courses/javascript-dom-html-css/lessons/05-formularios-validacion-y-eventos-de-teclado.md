# 5. Formularios, Evento Submit, Evento Input y Validacion en Vivo

Los formularios representan el canal fundamental de entrada de informacion en la web. En esta leccion aprenderas a capturar eventos de envio con `submit`, procesar datos masivos con la API `FormData` y validar reglas de negocio en tiempo real mediante los eventos `input` y `change`.

---

## Objetivos de la Leccion
- Interceptar el envio de formularios y prevenir la recarga de pagina con `preventDefault()`.
- Capturar y serializar datos mediante la API nativa `new FormData()`.
- Validar campos en tiempo real respondiendo al evento `input`.
- Comunicar estados de error y exito mediante clases CSS y atributos ARIA de accesibilidad.

---

## Captura y Procesamiento de Formularios con `FormData`

```html
<form id="formulario-registro" novalidate>
  <div class="campo-grupo">
    <label for="nombre">Nombre Completo:</label>
    <input type="text" id="nombre" name="nombre" required />
  </div>

  <div class="campo-grupo">
    <label for="correo">Correo Electronico:</label>
    <input type="email" id="correo" name="correo" required />
  </div>

  <div class="campo-grupo">
    <label for="rol">Rol Asignado:</label>
    <select id="rol" name="rol">
      <option value="usuario">Usuario Estandar</option>
      <option value="auditor">Auditor</option>
      <option value="administrador">Administrador</option>
    </select>
  </div>

  <button type="submit">Registrar Usuario</button>
</form>
```

```javascript
const formulario = document.querySelector("#formulario-registro");

formulario.addEventListener("submit", (event) => {
    // 1. Cancelar recarga tradicional de la pagina
    event.preventDefault();

    // 2. Extraer todos los valores de los inputs automaticamente mediante FormData
    const formData = new FormData(formulario);

    // 3. Transformar FormData a un objeto plano JavaScript
    const datosUsuario = Object.fromEntries(formData.entries());

    console.log("Carga util estructurada para enviar a la API:");
    console.log(datosUsuario);
    // Salida: { nombre: "Carlos Perez", correo: "carlos@eduxp.org", rol: "auditor" }

    // 4. Limpieza del formulario tras envio exitoso
    formulario.reset();
});
```

---

## Validacion en Tiempo Real con el Evento `input`

Esperar a que el usuario presione el boton de envio para notificarle un error degrada la experiencia. La validacion interactiva reacciona mientras el usuario escribe:

```javascript
const inputCorreo = document.querySelector("#correo");
const mensajeEstado = document.createElement("span");
mensajeEstado.classList.add("mensaje-feedback");
inputCorreo.after(mensajeEstado);

// El evento 'input' se dispara con cada pulsacion o cambio de caracter
inputCorreo.addEventListener("input", (event) => {
    const valorActual = event.target.value.trim();
    const patronCorreo = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

    if (!patronCorreo.test(valorActual)) {
        inputCorreo.classList.remove("campo-valido");
        inputCorreo.classList.add("campo-invalido");
        mensajeEstado.textContent = "Ingrese una direccion de correo valida.";
        mensajeEstado.style.color = "#ef4444";
    } else {
        inputCorreo.classList.remove("campo-invalido");
        inputCorreo.classList.add("campo-valido");
        mensajeEstado.textContent = "Formato de correo correcto.";
        mensajeEstado.style.color = "#10b981";
    }
});
```

---

## Ejercicio Practico

Implementa un formulario de creacion de contrasenas con un campo `<input type="password">`.  
Escribe un script que reaccione al evento `input` y valide tres criterios simultaneamente:
1. Longitud minima de 8 caracteres.
2. Contiene al menos un digito numerico.
3. Contiene al menos una letra mayuscula.  
Muestra visualmente el estado de cumplimiento de cada regla en una lista debajo del campo.
