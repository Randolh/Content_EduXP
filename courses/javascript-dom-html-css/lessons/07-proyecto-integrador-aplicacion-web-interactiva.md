# 7. Desarrollo de una Aplicacion SPA Completa y Proyecto Final

En esta leccion final integraras todos los conocimientos adquiridos a lo largo del curso para construir una aplicacion web interactiva completa: **Gestor de Tareas y Proyectos SPA**, implementada con HTML5 semantico, CSS3 moderno y JavaScript DOM puro.

---

## Objetivos de la Leccion
- Modularizar el estado global reactivo de una aplicacion Single Page Application (SPA).
- Implementar una funcion de renderizado optimizada mediante `DocumentFragment`.
- Gestionar acciones del usuario mediante **Delegacion de Eventos**.
- Garantizar la persistencia de datos en `localStorage` con gestion de errores.

---

## Maquetacion HTML5 Semantica y CSS3 Base (`index.html`)

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>EduXP Task Manager SPA</title>
  <style>
    :root {
      --bg-principal: #0b1120;
      --bg-tarjeta: #1e293b;
      --color-texto: #f8fafc;
      --color-acento: #0284c7;
      --color-peligro: #ef4444;
      --color-borde: #334155;
    }
    body {
      font-family: system-ui, -apple-system, sans-serif;
      background-color: var(--bg-principal);
      color: var(--color-texto);
      margin: 0;
      padding: 2rem 1rem;
      display: flex;
      justify-content: center;
    }
    .contenedor-app {
      width: 100%;
      max-width: 600px;
      background: var(--bg-tarjeta);
      border: 1px solid var(--color-borde);
      border-radius: 12px;
      padding: 2rem;
      box-shadow: 0 10px 25px rgba(0,0,0,0.5);
    }
    h1 {
      margin-top: 0;
      font-size: 1.5rem;
      border-bottom: 1px solid var(--color-borde);
      padding-bottom: 1rem;
    }
    form {
      display: flex;
      gap: 0.5rem;
      margin-bottom: 1.5rem;
    }
    input[type="text"] {
      flex: 1;
      padding: 0.75rem 1rem;
      background: var(--bg-principal);
      border: 1px solid var(--color-borde);
      border-radius: 6px;
      color: var(--color-texto);
      font-size: 1rem;
    }
    button.btn-primario {
      background: var(--color-acento);
      color: white;
      border: none;
      padding: 0.75rem 1.25rem;
      border-radius: 6px;
      cursor: pointer;
      font-weight: 600;
    }
    ul.lista-tareas {
      list-style: none;
      padding: 0;
      margin: 0;
    }
    li.item-tarea {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0.75rem 1rem;
      background: var(--bg-principal);
      border: 1px solid var(--color-borde);
      border-radius: 6px;
      margin-bottom: 0.5rem;
    }
    li.item-tarea.completada span {
      text-decoration: line-through;
      color: #94a3b8;
    }
    .acciones-tarea button {
      background: transparent;
      border: 1px solid var(--color-borde);
      color: var(--color-texto);
      padding: 0.25rem 0.5rem;
      border-radius: 4px;
      cursor: pointer;
      margin-left: 0.25rem;
    }
    .acciones-tarea button.btn-eliminar {
      border-color: var(--color-peligro);
      color: var(--color-peligro);
    }
  </style>
</head>
<body>
  <div class="contenedor-app">
    <h1>Gestor de Tareas y Operaciones SPA</h1>
    <form id="formulario-tareas">
      <input type="text" id="input-tarea" placeholder="Describa la tarea a registrar..." required />
      <button type="submit" class="btn-primario">Agregar</button>
    </form>
    <ul id="contenedor-lista" class="lista-tareas"></ul>
  </div>
  <script src="app.js"></script>
</body>
</html>
```

---

## Logica JavaScript (`app.js`)

```javascript
// 1. ESTADO GLOBAL DE LA APLICACION
const CLAVE_STORAGE = "eduxp_spa_tareas";

const cargarEstadoInicial = () => {
    try {
        const datos = localStorage.getItem(CLAVE_STORAGE);
        return datos ? JSON.parse(datos) : [
            { id: 1, descripcion: "Dominar manipulacion nativa del DOM", completada: true },
            { id: 2, descripcion: "Construir aplicacion interactiva sin frameworks", completada: false }
        ];
    } catch (e) {
        console.error("Error al cargar localStorage:", e);
        return [];
    }
};

let estadoTareas = cargarEstadoInicial();

// 2. REFERENCIAS A ELEMENTOS DEL DOM
const formulario = document.querySelector("#formulario-tareas");
const inputTexto = document.querySelector("#input-tarea");
const listaContenedor = document.querySelector("#contenedor-lista");

// 3. PERSISTENCIA
const guardarEnStorage = () => {
    localStorage.setItem(CLAVE_STORAGE, JSON.stringify(estadoTareas));
};

// 4. RENDERIZADO OPTIMIZADO CON DOCUMENTFRAGMENT
const renderizar = () => {
    listaContenedor.innerHTML = "";
    const fragmento = document.createDocumentFragment();

    estadoTareas.forEach(tarea => {
        const li = document.createElement("li");
        li.classList.add("item-tarea");
        if (tarea.completada) li.classList.add("completada");
        li.dataset.id = tarea.id;

        const span = document.createElement("span");
        span.textContent = tarea.descripcion;

        const divAcciones = document.createElement("div");
        divAcciones.classList.add("acciones-tarea");

        const btnEstado = document.createElement("button");
        btnEstado.textContent = tarea.completada ? "Reabrir" : "Completar";
        btnEstado.classList.add("btn-toggle");

        const btnBorrar = document.createElement("button");
        btnBorrar.textContent = "Eliminar";
        btnBorrar.classList.add("btn-eliminar");

        divAcciones.append(btnEstado, btnBorrar);
        li.append(span, divAcciones);
        fragmento.append(li);
    });

    listaContenedor.append(fragmento);
};

// 5. REGISTRO DE EVENTO SUBMIT (CREACION)
formulario.addEventListener("submit", (e) => {
    e.preventDefault();
    const texto = inputTexto.value.trim();
    if (!texto) return;

    const nuevaTarea = {
        id: Date.now(),
        descripcion: texto,
        completada: false
    };

    estadoTareas.push(nuevaTarea);
    guardarEnStorage();
    renderizar();
    inputTexto.value = "";
});

// 6. DELEGACION DE EVENTOS EN EL PADRE (MUTACION Y BORRADO)
listaContenedor.addEventListener("click", (e) => {
    const itemLi = e.target.closest("li.item-tarea");
    if (!itemLi) return;

    const idTarea = Number(itemLi.dataset.id);

    if (e.target.classList.contains("btn-eliminar")) {
        estadoTareas = estadoTareas.filter(t => t.id !== idTarea);
    } else if (e.target.classList.contains("btn-toggle")) {
        estadoTareas = estadoTareas.map(t => 
            t.id === idTarea ? { ...t, completada: !t.completada } : t
        );
    }

    guardarEnStorage();
    renderizar();
});

// Inicializacion inicial de render
renderizar();
```

---

## Conclusiones del Curso
Has completado el curso **JavaScript DOM, Eventos y Aplicaciones Web Interactivas con HTML5 y CSS3**. Ahora dominas la arquitectura de interfaces dinamicas nativas, la sincronizacion con almacenamiento local y las mejores practicas de rendimiento web.
