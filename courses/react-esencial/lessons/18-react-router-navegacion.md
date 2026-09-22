# Lección 18: Navegación Multi-página con React Router v6

En esta lección aprenderás a convertir tu aplicación cliente en una Single Page Application (SPA) con soporte para múltiples URLs y vistas usando la librería oficial **React Router v6**.

---

## 1. Configuración Básica de Rutas

Instalamos React Router ejecutando `npm install react-router-dom` y envolvemos la aplicación con `<BrowserRouter>`.

```jsx
import { BrowserRouter, Routes, Route, Link, useParams, useNavigate } from 'react-router-dom';

// Componentes de Página
function Inicio() {
  return <h2>🏠 Página Principal</h2>;
}

function DetalleProducto() {
  const { id } = useParams(); // Lee parámetros dinámicos de la URL (/producto/42)
  const navigate = useNavigate();

  return (
    <div>
      <h2>📦 Detalle del Producto #{id}</h2>
      <button onClick={() => navigate('/')}>Volver al Inicio</button>
    </div>
  );
}

export default function AppRouter() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">Inicio</Link> | <Link to="/producto/101">Ver Producto 101</Link>
      </nav>

      <Routes>
        <Route path="/" element={<Inicio />} />
        <Route path="/producto/:id" element={<DetalleProducto />} />
        <Route path="*" element={<h2>404 - Página no encontrada</h2>} />
      </Routes>
    </BrowserRouter>
  );
}
```

---

## 2. Elementos Clave de React Router

- **`<Link to="...">`**: Reemplaza las etiquetas `<a href="...">` tradicionales para evitar recargar la página.
- **`useParams()`**: Extrae variables dinámicas especificadas en el path con dos puntos (`:id`, `:category`).
- **`useNavigate()`**: Permite redirigir al usuario programáticamente desde código (ej. tras iniciar sesión o completar una compra).

---

## Autoevaluación

> [!QUIZ]
> ¿Por qué usamos `<Link to="/contacto">` en lugar de `<a href="/contacto">` al navegar en React Router?
> - [ ] Para dar estilos CSS automáticamente.
> - [x] Porque `<Link>` intercepta la navegación para cambiar la URL sin recargar la página completa en el navegador.
> - [ ] Porque `<a href>` no funciona en JavaScript.
>
> **Explicación**: El componente `<Link>` evita la recarga total del navegador (full page reload), manteniendo vivo el estado JavaScript de la SPA.

---

## Ejercicio Práctico

Define una ruta `/usuario/:username` que lea el parámetro mediante `useParams()` y muestre en pantalla un mensaje personalizado de bienvenida: `"Bienvenido, [username]"`.
