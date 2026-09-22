# Lección 4: Tu primer Componente Funcional

En esta lección aprenderás **exclusivamente a crear un nuevo componente** como una función de JavaScript.

---

## 1. Crear un Componente Funcional

Un componente en React es simplemente una función que retorna marcado JSX y cuyo nombre comienza con una letra **Mayúscula**.

```jsx
// src/BotonApretar.jsx
export default function BotonApretar() {
  return (
    <button className="mi-boton">
      ¡Haz clic aquí!
    </button>
  );
}
```

Luego puedes usar tu nuevo componente en `App.jsx` como si fuera una etiqueta HTML propia: `<BotonApretar />`.

---

## Autoevaluación

> [!QUIZ]
> ¿Con qué tipo de letra debe comenzar OBLIGATORIAMENTE el nombre de un componente de React?
> - [ ] Con minúscula.
> - [x] Con Mayúscula.
> - [ ] Con un número.
>
> **Explicación**: React distingue los componentes propios de las etiquetas HTML estándar (como `<div>` o `<button>`) porque los componentes inician siempre con letra mayúscula (ej. `<MiComponente />`).

---

## Ejercicio Práctico

Crea un archivo `src/Encabezado.jsx` que devuelva un componente `<header>` con un título, e impórtalo dentro de `src/App.jsx`.
