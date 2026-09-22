# Lección 7: Eventos y Formularios Básicos (onClick y onChange)

En esta lección aprenderás **exclusivamente a capturar lo que el usuario escribe** en un campo de texto usando `onChange`.

---

## 1. Capturar Texto con `onChange`

Para leer lo que el usuario teclea en una casilla `<input>`:

```jsx
import { useState } from 'react';

export default function FormularioNombre() {
  const [nombre, setNombre] = useState('');

  return (
    <div>
      <input 
        type="text" 
        value={nombre} 
        onChange={(e) => setNombre(e.target.value)} 
        placeholder="Escribe tu nombre"
      />
      <p>Tu nombre es: {nombre}</p>
    </div>
  );
}
```

La propiedad `e.target.value` obtiene la letra o texto recién ingresado.

---

## Autoevaluación

> [!QUIZ]
> ¿Qué propiedad del evento `e` contiene el valor actualizado que el usuario escribió en una casilla `<input>`?
> - [ ] `e.text`
> - [x] `e.target.value`
> - [ ] `e.input.data`
>
> **Explicación**: `e.target` hace referencia al elemento del DOM (el input) y `.value` a su contenido de texto.

---

## Ejercicio Práctico

Crea un componente con un campo de texto `<input>` que guarde un comentario en el estado y lo muestre debajo en tiempo real.
