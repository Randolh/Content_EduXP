# Lección 14: Manipulación del DOM y Referencias Mutables con useRef

En esta lección aprenderás a utilizar el Hook `useRef` para dos casos de uso fundamentales: acceder directamente a elementos del DOM de HTML y guardar valores persistentes que **no provocan re-renderizados** al cambiar.

---

## 1. El Hook `useRef`

`useRef` retorna un objeto mutable cuya propiedad `.current` persiste durante todo el ciclo de vida del componente.

### Caso de uso 1: Acceso Directo al DOM (Foco de un Input)

```jsx
import { useRef } from 'react';

export default function InputConFoco() {
  const inputRef = useRef(null);

  const darFoco = () => {
    // Acceso directo al nodo HTML del DOM
    inputRef.current.focus();
    inputRef.current.style.border = '2px solid cyan';
  };

  return (
    <div>
      <input ref={inputRef} type="text" placeholder="Escribe aquí..." />
      <button onClick={darFoco}>Enfocar Input</button>
    </div>
  );
}
```

### Caso de uso 2: Guardar Valores Mutables sin Re-renderizar (Cronómetro / Timers)

A diferencia de `useState`, modificar `ref.current` **no provoca que el componente se vuelva a renderizar**.

```jsx
import { useRef } from 'react';

export default function ContadorRenders() {
  const contadorRef = useRef(0);

  const incrementarSinRender = () => {
    contadorRef.current += 1;
    console.log(`Clics totales (sin re-render): ${contadorRef.current}`);
  };

  return <button onClick={incrementarSinRender}>Contar Clics en Consola</button>;
}
```

---

## Autoevaluación

> [!QUIZ]
> ¿Cuál es la diferencia principal entre `useState` y `useRef` al actualizar su valor?
> - [ ] `useState` es solo para números y `useRef` para objetos.
> - [x] Actualizar `useState` desencadena un re-renderizado de la interfaz, mientras que modificar `.current` en `useRef` no re-renderiza el componente.
> - [ ] `useRef` borra su valor cuando el componente se actualiza.
>
> **Explicación**: `useRef` es ideal para almacenar referencias al DOM o guardar contadores/intervalos en segundo plano sin forzar a React a actualizar la UI en pantalla.

---

## Ejercicio Práctico

Crea un componente con un campo de texto y un botón "Limpiar". Al presionar el botón, debes limpiar el contenido del input y devolverle el foco automáticamente usando `useRef`.
