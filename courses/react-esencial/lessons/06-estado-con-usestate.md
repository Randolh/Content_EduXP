# Lección 6: Manejo de Estado Local con el Hook useState

En esta lección aprenderás **exclusivamente a hacer componentes interactivos** usando el Hook `useState`.

---

## 1. ¿Qué es el Estado (State)?

A diferencia de las variables normales que no redibujan la pantalla cuando cambian, el **Estado** es memoria interna que, al modificarse, actualiza automáticamente lo que el usuario ve en el navegador.

```jsx
import { useState } from 'react';

export default function Contador() {
  // Crear estado 'contador' iniciando en 0
  const [contador, setContador] = useState(0);

  return (
    <div>
      <p>Has hecho clic {contador} veces</p>
      <button onClick={() => setContador(contador + 1)}>
        Aumentar
      </button>
    </div>
  );
}
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué función se debe llamar para actualizar el valor del estado y hacer que React vuelva a renderizar el componente?
> - [ ] La variable de lectura directamente (ej. `contador = 5`).
> - [x] La función modificadora devuelta por `useState` (ej. `setContador(5)`).
> - [ ] `window.location.reload()`.
>
> **Explicación**: Solo llamando a la función actualizadora (ej. `setContador`) React se entera de que el estado cambió y refresca la interfaz.

---

## Ejercicio Práctico

Crea un componente `BotonMeGusta` que tenga un estado `const [likes, setLikes] = useState(0)` y aumente la cuenta al hacer clic.
