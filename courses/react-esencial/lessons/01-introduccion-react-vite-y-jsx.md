# Lección 1: Introducción a React, Setup con Vite y Sintaxis JSX

**React** es la librería de JavaScript más popular del mundo para construir interfaces de usuario dinámicas y reactivas basadas en **Componentes**. En esta lección aprenderás a inicializar un proyecto ultrasrápido con **Vite** y comprenderás la sintaxis declarativa de **JSX**.

---

## 1. Inicializar un Proyecto React con Vite

**Vite** es la herramienta estándar moderna para empaquetar aplicaciones frontend. Ofrece arranque instantáneo y reemplazo de módulos en caliente (HMR).

### Paso 1: Crear la aplicación con Vite

```bash
npx create-vite mi-app-react --template react
cd mi-app-react
npm install
npm run dev
```

### Estructura de Carpetas Generada:

```text
mi-app-react/
├── index.html              <-- Punto de entrada HTML del DOM
├── package.json
├── vite.config.js          <-- Configuración del servidor Vite
└── src/
    ├── main.jsx            <-- Renderizado inicial con ReactDOM
    ├── App.jsx             <-- Componente principal de la aplicación
    └── index.css           <-- Estilos globales
```

---

## 2. ¿Qué es JSX?

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

## 💡 Autoevaluación

> [!QUIZ]
> ¿Cómo se insertan variables o expresiones evaluables de JavaScript dentro de la sintaxis de marcado JSX?
> - [ ] Utilizando corchetes `[variable]`
> - [x] Encerrando la expresión dentro de llaves `{variable}`
> - [ ] Utilizando la sintaxis `{{variable}}`
>
> **Explicación**: Todo lo que coloques dentro de `{}` en JSX será interpretado como código JavaScript dinámico.

---

## 🛠️ Ejercicio Práctico: Renderizado de Listas en JSX

**Objetivo**: Renderizar dinámicamente un arreglo de tecnologías usando la función `.map()` con la propiedad `key`.

<details class="exercise-solution">
<summary>💡 Ver solución paso a paso</summary>

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

## 📌 Resumen

- **Vite** es la herramienta recomendada para crear y desarrollar aplicaciones React.
- **JSX** fusiona HTML y JavaScript de forma declarativa.
- Usa llaves `{}` para renderizar variables y `.map()` para listas (recordando pasar una prop `key` única).
- En la siguiente lección aprenderás a crear **Componentes Funcionales**, enviar datos con **Props** y gestionar el estado local con **useState**.
