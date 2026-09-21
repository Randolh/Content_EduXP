# Lección 2: Componentes Funcionales, Props y Estado Reactivo con `useState`

Los componentes son los bloques de construcción reutilizables de React. En esta lección aprenderás a dividir tu interfaz en componentes, enviarles datos mediante **Props** y hacer que la interfaz responda a las acciones del usuario modificando el estado local con el Hook **useState**.

---

## 1. Componentes Funcionales y Props

Las **Props** (Propiedades) son los argumentos que se le pasan a un componente hijo desde un componente padre para personalizar su apariencia o contenido. Son **de solo lectura (inmutables)**.

### Componente Hijo: `ProductoCard.jsx`

```jsx
// Destructuración de props
export default function ProductoCard({ titulo, precio, destacado = false }) {
  return (
    <div className={`card ${destacado ? 'card-highlight' : ''}`}>
      <h3>{titulo}</h3>
      <p className="precio">${precio.toFixed(2)}</p>
      {destacado && <span className="tag">¡Oferta Especial!</span>}
    </div>
  );
}
```

### Componente Padre: `App.jsx`

```jsx
import ProductoCard from './ProductoCard.jsx';

export default function App() {
  return (
    <main className="catalogo">
      <h2>Catálogo de Productos</h2>
      <ProductoCard titulo="Audífonos Bluetooth" precio={59.99} destacado={true} />
      <ProductoCard titulo="Monitor 4K 27 IPS" precio={299.00} />
    </main>
  );
}
```

---

## 2. El Hook `useState` (Estado Reactivo Local)

El estado es la memoria interna de un componente. Cuando el estado cambia mediante su función actualizadora, React vuelve a renderizar automáticamente el componente en la pantalla.

```jsx
import { useState } from 'react';

export default function Contador() {
  // Declaración del estado: [valorActual, funcionActualizadora]
  const [contador, setContador] = useState(0);

  const incrementar = () => {
    setContador(prev => prev + 1);
  };

  const decrementar = () => {
    if (contador > 0) {
      setContador(prev => prev - 1);
    }
  };

  return (
    <div className="contador-box">
      <h3>Cantidad: {contador}</h3>
      <button onClick={decrementar}>-</button>
      <button onClick={() => setContador(0)}>Reset</button>
      <button onClick={incrementar}>+</button>
    </div>
  );
}
```

> [!WARNING]
> Nunca mutas el estado directamente (ej. `contador = contador + 1`). Siempre debes invocar la función asignada (`setContador(nuevoValor)`).

---

## 💡 Autoevaluación

> [!QUIZ]
> ¿Qué sucede en la pantalla cuando actualizas el estado de un componente llamando a su función `setEstado(...)`?
> - [ ] Se recarga toda la página web del navegador desde el servidor.
> - [x] React vuelve a renderizar únicamente el componente afectado y actualiza el DOM de forma eficiente.
> - [ ] Se borran las Props del componente padre.
>
> **Explicación**: React utiliza un Virtual DOM para comparar la nueva versión del componente con la anterior y aplicar solo los cambios necesarios en el navegador.

---

## 🛠️ Ejercicio Práctico: Botón Me Gusta (Like Button)

**Objetivo**: Crear un componente interactivo que alterne el estado de "Me Gusta" y cuente el total de likes.

<details class="exercise-solution">
<summary>💡 Ver solución paso a paso</summary>

<div class="solution-content">

```jsx
import { useState } from 'react';

export default function BotónLike() {
  const [liked, setLiked] = useState(false);
  const [likesCount, setLikesCount] = useState(42);

  const toggleLike = () => {
    if (liked) {
      setLikesCount(likesCount - 1);
    } else {
      setLikesCount(likesCount + 1);
    }
    setLiked(!liked);
  };

  return (
    <button 
      onClick={toggleLike}
      className={`btn-like ${liked ? 'active' : ''}`}
    >
      {liked ? '❤️ Te gusta' : '🤍 Me gusta'} ({likesCount})
    </button>
  );
}
```

</div>
</details>

---

## 📌 Resumen

- Las **Props** permiten pasar información de padres a hijos (flujo de datos unidireccional).
- **`useState`** almacena y gestiona datos dinámicos que provocan el re-renderizado de la UI.
- Los eventos como `onClick` ejecutan funciones actualizadoras del estado.
- En la siguiente lección aprenderás a manejar efectos secundarios y consumir APIs REST reales con **useEffect**.
