# Lección 5: Estado Global con Context API (`CartContext` y Estado Compartido)

Cuando una aplicación crece, pasar props a través de múltiples niveles de componentes anidados (**Prop Drilling**) se vuelve tedioso e ineficiente. En esta lección aprenderás a utilizar **Context API** (`createContext` y `useContext`) para crear un estado global compartido (ej. un Carrito de Compras) accesible desde cualquier componente de tu aplicación.

---

## 1. El Problema del Prop Drilling vs Context API

```text
Sin Context API (Prop Drilling):
[ App ] ──(props)──► [ Navbar ] ──(props)──► [ UserAvatar ]

Con Context API (Estado Global):
[ App (ContextProvider) ] ──► [ UserAvatar (useContext) ]
```

**Context API** permite inyectar datos globales en el árbol de componentes sin necesidad de pasar props manualmente por los componentes intermedios.

---

## 2. Creación del Proveedor del Carrito (`CartContext.jsx`)

Crearemos un contexto para el carrito de compras con persistencia local en el navegador (`localStorage`).

```jsx
// src/context/CartContext.jsx
import { createContext, useContext, useState, useEffect } from 'react';

// 1. Crear el Contexto
const CartContext = createContext();

// 2. Crear el Proveedor (Provider Component)
export function CartProvider({ children }) {
  // Cargar carrito inicial desde localStorage si existe
  const [cart, setCart] = useState(() => {
    const savedCart = localStorage.getItem('eduxp_cart');
    return savedCart ? JSON.parse(savedCart) : [];
  });

  // Guardar en localStorage cada vez que el carrito cambie
  useEffect(() => {
    localStorage.setItem('eduxp_cart', JSON.stringify(cart));
  }, [cart]);

  // Función para agregar un producto al carrito
  const addToCart = (product) => {
    setCart((prevCart) => {
      const itemExistente = prevCart.find(item => item.id === product.id);
      if (itemExistente) {
        return prevCart.map(item =>
          item.id === product.id
            ? { ...item, cantidad: item.cantidad + 1 }
            : item
        );
      }
      return [...prevCart, { ...product, cantidad: 1 }];
    });
  };

  // Función para eliminar un producto
  const removeFromCart = (id) => {
    setCart(prevCart => prevCart.filter(item => item.id !== id));
  };

  // Función para vaciar el carrito
  const clearCart = () => setCart([]);

  // Calcular total acumulado de items
  const totalItems = cart.reduce((acc, item) => acc + item.cantidad, 0);
  const totalPrecio = cart.reduce((acc, item) => acc + (item.precio * item.cantidad), 0);

  return (
    <CartContext.Provider value={{
      cart,
      addToCart,
      removeFromCart,
      clearCart,
      totalItems,
      totalPrecio
    }}>
      {children}
    </CartContext.Provider>
  );
}

// 3. Custom Hook para consumir el contexto fácilmente
export function useCart() {
  const context = useContext(CartContext);
  if (!context) {
    throw new Error('useCart debe ser utilizado dentro de un CartProvider');
  }
  return context;
}
```

---

## 3. Consumo del Estado Global en Componentes

### A. Botón de Agregar en la Tarjeta de Producto (`ProductoItem.jsx`)

```jsx
import { useCart } from '../context/CartContext.jsx';

export default function ProductoItem({ producto }) {
  const { addToCart } = useCart();

  return (
    <div className="card">
      <h4>{producto.nombre}</h4>
      <p>${producto.precio}</p>
      <button onClick={() => addToCart(producto)}>
        🛒 Agregar al Carrito
      </button>
    </div>
  );
}
```

### B. Badge del Carrito en el Header (`Navbar.jsx`)

```jsx
import { useCart } from '../context/CartContext.jsx';

export default function Navbar() {
  const { totalItems } = useCart();

  return (
    <header className="navbar">
      <h1>EduXP Store</h1>
      <div className="cart-badge">
        🛒 Carrito <span>({totalItems})</span>
      </div>
    </header>
  );
}
```

---

## 💡 Autoevaluación

> [!QUIZ]
> ¿Qué función cumple la envolvente `<CartProvider>` dentro de la aplicación de React?
> - [ ] Compila el código de JSX a JavaScript puro en tiempo de ejecución.
> - [x] Proveer el objeto de estado global y sus métodos modificadores a cualquier componente descendiente en el árbol de React.
> - [ ] Conectarse directamente a la base de datos MySQL del servidor.
>
> **Explicación**: Todos los componentes ubicados dentro de `<CartProvider>` pueden suscribirse a los cambios del contexto usando el Hook `useCart()`.

---

## 🛠️ Ejercicio Práctico: Botón Vaciar Carrito

**Objetivo**: Consumir la función `clearCart` en el componente del Drawer del carrito.

<details class="exercise-solution">
<summary>💡 Ver solución paso a paso</summary>

<div class="solution-content">

```jsx
import { useCart } from '../context/CartContext.jsx';

export default function ResumenCarrito() {
  const { cart, removeFromCart, clearCart, totalPrecio } = useCart();

  return (
    <div>
      <h3>Tu Carrito</h3>
      {cart.map(item => (
        <div key={item.id}>
          <span>{item.nombre} x {item.cantidad} (${item.precio * item.cantidad})</span>
          <button onClick={() => removeFromCart(item.id)}>Eliminar</button>
        </div>
      ))}
      
      <h4>Total: ${totalPrecio.toFixed(2)}</h4>
      {cart.length > 0 && (
        <button onClick={clearCart} className="btn-danger">Vaciar Carrito</button>
      )}
    </div>
  );
}
```

</div>
</details>

---

## 📌 Resumen

- **Context API** resuelve el problema de Prop Drilling en React.
- `createContext` define la estructura del contexto.
- `CartProvider` almacena la lógica del estado y envuelve la aplicación.
- `useContext` (o tu Custom Hook `useCart`) permite a cualquier componente acceder al estado global.
- En la lección final aprenderás a implementar **Autenticación Global** y configurar el **Proxy de Vite** para integrar tu frontend React con la API Express.
