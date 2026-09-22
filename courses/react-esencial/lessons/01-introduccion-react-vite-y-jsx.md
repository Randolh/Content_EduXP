# Lección 1: Introducción a React, Setup con Vite y Sintaxis JSX

**React** es la librería de JavaScript más popular del mundo para construir interfaces de usuario dinámicas y reactivas basadas en **Componentes**. En esta lección aprenderás a preparar tu entorno de desarrollo, inicializar un proyecto ultrarrápido con **Vite** y comprenderás la sintaxis declarativa de **JSX**.

---

## 1. Prerrequisitos y Preparación del Entorno

Antes de crear tu primera aplicación React, asegúrate de contar con el siguiente entorno configurado:

### A. Herramientas Requeridas

1. **Node.js (v18.0 o superior):**
   * React y Vite requieren Node.js para ejecutar los comandos de instalación y el servidor de desarrollo local.
   * Verifica la versión en tu terminal con `node -v`. Si no lo tienes, descárgalo desde [nodejs.org](https://nodejs.org).

2. **Gestor de Paquetes (NPM / PNPM / Yarn):**
   * Viene incluido automáticamente con Node.js (`npm -v`).

### B. Extensiones Recomendadas para Visual Studio Code

* **ES7+ React/Redux/React-Native snippets:** Genera plantillas de componentes con atajos como `rafce` (React Arrow Function Component with Export).
* **Auto Rename Tag:** Cambia automáticamente la etiqueta de cierre en JSX al renombrar la de apertura.
* **Prettier - Code Formatter:** Formatea automáticamente el código JSX y CSS al guardar.

### C. Herramientas de Inspección en el Navegador

* **React Developer Tools:** Extensión oficial para Chrome y Firefox que añade los paneles *Components* y *Profiler* a las herramientas de desarrollo del navegador (`F12`).

---

## 2. Inicializar un Proyecto React con Vite

**Vite** es la herramienta estándar moderna para empaquetar aplicaciones frontend. Ofrece arranque instantáneo y reemplazo de módulos en caliente (HMR).

### Paso 1: Crear la aplicación con Vite

Abre tu terminal y ejecuta:

```bash
# Crear proyecto con la plantilla oficial de React
npx create-vite mi-app-react --template react

# Navegar a la carpeta creada
cd mi-app-react

# Instalar dependencias
npm install

# Iniciar servidor de desarrollo local
npm run dev
```

### Estructura de Carpetas Generada:

```text
mi-app-react/
├── index.html              <-- Punto de entrada HTML del DOM
├── package.json            <-- Dependencias del proyecto
├── vite.config.js          <-- Configuración del servidor Vite
└── src/
    ├── main.jsx            <-- Renderizado inicial con ReactDOM
    ├── App.jsx             <-- Componente principal de la aplicación
    └── index.css           <-- Estilos globales
```

---

## 3. ¿Qué es JSX?

**JSX** (JavaScript XML) es una extensión de sintaxis que permite escribir código similar a HTML directamente dentro de archivos JavaScript.

```jsx
// src/App.jsx
export default function App() {
  const titulo = 'Bienvenido a EduXP React Esencial';
  const usuario = { nombre: 'Alexis', esPremium: true };

  return (
    <div className="container">
      <h1>{titulo}</h1>
      <p>Hola, {usuario.nombre}.</p>
      
      {/* Renderizado Condicional con operadores ternarios */}
      {usuario.esPremium ? (
        <span className="badge badge-gold">⭐ Usuario Premium</span>
      ) : (
        <span className="badge">Usuario Estándar</span>
      )}
    </div>
  );
}
```

> [!NOTE]
> Reglas clave de JSX:
> 1. Todas las etiquetas deben cerrarse (`<img />`, `<br />`).
> 2. Se usa `className` en lugar de `class` para clases CSS.
> 3. Las expresiones JavaScript se evalúan encerrándolas entre llaves `{}`.

---

## Autoevaluación

> [!QUIZ]
> ¿Cómo se insertan variables o expresiones evaluables de JavaScript dentro de la sintaxis de marcado JSX?
> - [ ] Utilizando corchetes `[variable]`
> - [x] Encerrando la expresión dentro de llaves `{variable}`
> - [ ] Utilizando la sintaxis `{{variable}}`
>
> **Explicación**: Todo lo que coloques dentro de `{}` en JSX será interpretado como código JavaScript dinámico.

---

## Ejercicio Práctico: Renderizado de Listas en JSX

**Objetivo**: Renderizar dinámicamente un arreglo de tecnologías usando la función `.map()` con la propiedad `key`.

<details class="exercise-solution">
<summary>Ver solución paso a paso</summary>

<div class="solution-content">

```jsx
// src/ListaTecnologias.jsx
export default function ListaTecnologias() {
  const tecnologias = [
    { id: '1', nombre: 'React 18', categoria: 'Frontend' },
    { id: '2', nombre: 'Vite', categoria: 'Bundler' },
    { id: '3', nombre: 'Express', categoria: 'Backend' }
  ];

  return (
    <div>
      <h2>Stack de Tecnologías</h2>
      <ul>
        {tecnologias.map((tech) => (
          <li key={tech.id}>
            <strong>{tech.nombre}</strong> - <em>{tech.categoria}</em>
          </li>
        ))}
      </ul>
    </div>
  );
}
```

</div>
</details>

---

## Resumen

- Se requiere Node.js v18+ y VS Code con extensiones como **ES7+ Snippets** y **React DevTools**.
- **Vite** es la herramienta recomendada para crear y desarrollar aplicaciones React.
- **JSX** fusiona HTML y JavaScript de forma declarativa.
- En la siguiente lección aprenderás a crear **Componentes Funcionales**, enviar datos con **Props** y gestionar el estado local con **useState**.
