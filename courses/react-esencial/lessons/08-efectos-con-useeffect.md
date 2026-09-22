# Lección 8: Introducción a Efectos Secundarios con useEffect

En esta lección final aprenderás **qué es el Hook `useEffect`** y cómo ejecutar código cuando el componente aparece en pantalla por primera vez.

---

## 1. El Hook `useEffect`

`useEffect` sirve para realizar acciones secundarias, como pedir datos a un servidor o cambiar el título de la pestaña del navegador.

```jsx
import { useState, useEffect } from 'react';

export default function MiEfecto() {
  const [mensaje, setMensaje] = useState('Cargando...');

  useEffect(() => {
    // Este código se ejecuta una sola vez cuando el componente se dibuja
    console.log("El componente ha aparecido en pantalla");
    setMensaje("¡Bienvenido a la aplicación!");
  }, []); // El arreglo vacío [] indica que solo se ejecute al montar el componente

  return <h1>{mensaje}</h1>;
}
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué indica colocar un arreglo vacío `[]` al final del Hook `useEffect`?
> - [ ] Que el efecto nunca se ejecutará.
> - [x] Que el efecto se ejecutará únicamente 1 vez cuando el componente se monte por primera vez en pantalla.
> - [ ] Que provocará un bucle infinito.
>
> **Explicación**: El arreglo de dependencias vacío `[]` le dice a React que no depende de ninguna variable cambiante y solo debe correr en la carga inicial.

---

## Ejercicio Práctico Final

Crea un componente que al cargarse use `useEffect` para cambiar el título de la pestaña del navegador a `"Página lista"` ejecutando `document.title = "Página lista"`.
