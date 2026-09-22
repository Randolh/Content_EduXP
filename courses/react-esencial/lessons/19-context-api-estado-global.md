# Lección 19: Gestión de Estado Global con Context API

En esta lección aprenderás a solucionar el problema del ***Prop Drilling*** (pasar props manualmente a través de múltiples niveles de componentes anidados) creando un estado global nativo con la **Context API** y el Hook `useContext`.

---

## 1. Creación del Contexto y Provider

Creamos un contexto que almacenará el estado global y envolveremos los componentes que necesiten acceder a él.

```jsx
import { createContext, useContext, useState } from 'react';

// 1. Crear el Contexto
const TemaContext = createContext();

// 2. Componente Provider que envuelve la app
export function TemaProvider({ children }) {
  const [tema, setTema] = useState('claro');

  const alternarTema = () => {
    setTema((prev) => (prev === 'claro' ? 'oscuro' : 'claro'));
  };

  return (
    <TemaContext.Provider value={{ tema, alternarTema }}>
      {children}
    </TemaContext.Provider>
  );
}

// 3. Custom Hook conveniente para consumir el contexto
export function useTema() {
  return useContext(TemaContext);
}
```

---

## 2. Consumo del Estado Global en Componentes Hijos

Cualquier componente ubicado dentro del `<TemaProvider>` puede consumir el valor directamente sin recibir props intermedias:

```jsx
function BotonCambiarTema() {
  const { tema, alternarTema } = useTema();

  return (
    <button onClick={alternarTema}>
      Tema actual: {tema === 'claro' ? '☀️ Claro' : '🌙 Oscuro'}
    </button>
  );
}

export default function AppConEstadoGlobal() {
  return (
    <TemaProvider>
      <div className="main-layout">
        <h1>Mi Aplicación con Estado Global</h1>
        <BotonCambiarTema />
      </div>
    </TemaProvider>
  );
}
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué problema técnico resuelve la Context API en React?
> - [ ] Acelera las peticiones HTTP.
> - [x] Evita el *Prop Drilling*, permitiendo compartir datos con componentes profundos sin pasar props por cada nivel intermedio.
> - [ ] Reemplaza el uso de JSX.
>
> **Explicación**: La Context API crea un canal directo de comunicación entre un Provider (proveedor) y cualquier componente hijo que utilice `useContext`.

---

## Ejercicio Práctico

Crea un `CarritoContext` que provea un arreglo `items` y una función `agregarAlCarrito(producto)`.
