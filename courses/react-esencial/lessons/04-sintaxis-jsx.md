# Lección 3: Introducción a JSX: Mezclando HTML y JavaScript

En esta lección aprenderás **exclusivamente qué es JSX** y cómo insertar variables de JavaScript dentro de tu marcado entre llaves `{}`.

---

## 1. ¿Qué es JSX?

**JSX** permite escribir código que parece HTML directamente dentro de archivos JavaScript.

Para mostrar el valor de una variable de JavaScript en pantalla, la encierras entre llaves `{}`:

```jsx
export default function App() {
  const nombre = "Alexis";
  const edad = 25;

  return (
    <div>
      <h1>Hola, {nombre}</h1>
      <p>Tienes {edad} años.</p>
    </div>
  );
}
```

> [!NOTE]
> En JSX usas `className` en lugar de `class` para asignar clases de CSS a los elementos.

---

## Autoevaluación

> [!QUIZ]
> ¿Qué símbolo se utiliza en JSX para evaluar una variable de JavaScript dentro del HTML?
> - [ ] Corchetes `[variable]`
> - [x] Llaves `{variable}`
> - [ ] Signos de pesos `$variable`
>
> **Explicación**: Las llaves `{}` le indican a React que ejecute la expresión JavaScript contenida.

---

## Ejercicio Práctico

Abre `src/App.jsx`, crea una variable `const curso = "React Esencial"` y muéstrala dentro de una etiqueta `<h2>{curso}</h2>`.
