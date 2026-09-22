# Lección 15: Manejo de Estado Complejo con useReducer

En esta lección aprenderás a utilizar el Hook `useReducer`, una alternativa a `useState` diseñada para gestionar estados complejos que involucran múltiples subvalores o cuando el siguiente estado depende del anterior.

---

## 1. El Patrón Reducer

Un *Reducer* es una función pura que recibe dos argumentos: el **estado actual (`state`)** y una **acción (`action`)**, y retorna un **nuevo estado**.

```jsx
import { useReducer } from 'react';

// 1. Estado inicial
const initialState = { contador: 0, paso: 1 };

// 2. Función Reducer
function contadorReducer(state, action) {
  switch (action.type) {
    case 'INCREMENTAR':
      return { ...state, contador: state.contador + state.paso };
    case 'DECREMENTAR':
      return { ...state, contador: state.contador - state.paso };
    case 'SET_PASO':
      return { ...state, paso: action.payload };
    case 'RESETEAR':
      return initialState;
    default:
      return state;
  }
}

// 3. Componente
export default function ContadorAvanzado() {
  const [state, dispatch] = useReducer(contadorReducer, initialState);

  return (
    <div>
      <h2>Valor: {state.contador}</h2>
      <button onClick={() => dispatch({ type: 'INCREMENTAR' })}>+{state.paso}</button>
      <button onClick={() => dispatch({ type: 'DECREMENTAR' })}>-{state.paso}</button>
      <button onClick={() => dispatch({ type: 'RESETEAR' })}>Reset</button>

      <div>
        <label>Paso: </label>
        <input
          type="number"
          value={state.paso}
          onChange={(e) => dispatch({ type: 'SET_PASO', payload: Number(e.target.value) })}
        />
      </div>
    </div>
  );
}
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué función cumple la llamada `dispatch({ type: 'INCREMENTAR' })` en `useReducer`?
> - [ ] Actualiza el DOM directamente.
> - [x] Envía un objeto de acción a la función reducer para describir qué tipo de cambio se debe realizar.
> - [ ] Elimina el estado actual.
>
> **Explicación**: `dispatch` es el emisor de acciones. La función reducer recibe la acción emitida a través de `dispatch` y calcula el nuevo estado basándose en `action.type` y opcionalmente `action.payload`.

---

## Ejercicio Práctico

Crea un reducer para una lista de tareas que soporte dos acciones: `{ type: 'AGREGAR_TAREA', payload: 'Aprender Reducer' }` y `{ type: 'ELIMINAR_TAREA', payload: id }`.
