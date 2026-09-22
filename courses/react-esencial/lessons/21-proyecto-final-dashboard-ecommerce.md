# Lección 21: Proyecto Final Integrador: EduXP Store App

¡Felicitaciones por llegar a la lección final! En esta etapa pondrás a prueba todo lo aprendido en el curso construyendo una aplicación web completa e interactiva: **EduXP Store**, un Dashboard E-Commerce profesional con catálogo dinámico, rutas, filtros, carrito de compras global y persistencia de datos.

---

## 📋 Descripción del Proyecto

Desarrollarás una Single Page Application (SPA) para una tienda en línea moderna que consuma la API pública de productos [FakeStoreAPI](https://fakestoreapi.com/products) o [DummyJSON](https://dummyjson.com/products).

---

## 🎯 Requisitos Técnicos y Funcionalidades

### 1. Arquitectura y Componentes
- Estructura modular de carpetas (`components/`, `context/`, `hooks/`, `pages/`).
- Componentes reutilizables: `Header`, `ProductCard`, `CartItem`, `Spinner`, `Rating`.

### 2. Consumo de API & Custom Hooks
- Implementar un Custom Hook `useProducts()` que obtenga la lista de productos de `https://fakestoreapi.com/products`.
- Controlar estados de interfaz: `loading` (spinner de carga), `error` (mensaje de falla) y `data`.

### 3. Filtros y Búsqueda en Tiempo Real
- Campo de entrada (`input`) para filtrar productos por título en tiempo real.
- Selector (`select`) para filtrar por categoría (ej. electrónica, ropa, joyería).
- Optimización del filtrado usando `useMemo` para prevenir recálculos innecesarios.

### 4. Carrito de Compras Global (Context API + localStorage)
- Crear un `CartContext` que contenga:
  - `cart`: Arreglo de elementos en el carrito.
  - `addToCart(product)`: Agregar producto o incrementar cantidad si ya existe.
  - `removeFromCart(productId)`: Eliminar producto.
  - `clearCart()`: Vaciar carrito.
  - `totalPrice`: Cálculo acumulado del costo total.
- **Persistencia**: Guardar y sincronizar automáticamente el estado del carrito en `localStorage` usando un efecto o Custom Hook `useLocalStorage`.

### 5. Enrutamiento con React Router v6
- `/` (Home): Catálogo principal con buscador y tarjetas de productos.
- `/producto/:id`: Vista de detalle con descripción completa, imagen ampliada y botón de agregar.
- `/carrito`: Vista del resumen de compra con lista de items, totales y botón de Checkout.
- `*`: Página 404 para rutas no existentes.

---

## 💻 Código Base Recomendado para el Carrito (`CartContext.jsx`)

```jsx
import { createContext, useContext, useState, useEffect } from 'react';

const CartContext = createContext();

export function CartProvider({ children }) {
  const [cart, setCart] = useState(() => {
    const saved = localStorage.getItem('eduxp_cart');
    return saved ? JSON.parse(saved) : [];
  });

  useEffect(() => {
    localStorage.setItem('eduxp_cart', JSON.stringify(cart));
  }, [cart]);

  const addToCart = (product) => {
    setCart((prev) => {
      const exists = prev.find((item) => item.id === product.id);
      if (exists) {
        return prev.map((item) =>
          item.id === product.id ? { ...item, quantity: item.quantity + 1 } : item
        );
      }
      return [...prev, { ...product, quantity: 1 }];
    });
  };

  const removeFromCart = (id) => {
    setCart((prev) => prev.filter((item) => item.id !== id));
  };

  const total = cart.reduce((acc, item) => acc + item.price * item.quantity, 0);

  return (
    <CartContext.Provider value={{ cart, addToCart, removeFromCart, total }}>
      {children}
    </CartContext.Provider>
  );
}

export function useCart() {
  return useContext(CartContext);
}
```

---

## 🏆 Criterios de Evaluación y Entrega

1. **Uso correcto de Hooks**: Demostrar manejo fluido de `useState`, `useEffect`, `useContext`, `useMemo` y Custom Hooks.
2. **Navegación Fluida**: Cambiar de ruta sin recarga completa de página.
3. **Persistencia**: Si refrescas el navegador, los elementos agregados al carrito deben conservarse.
4. **Diseño y UX**: Interfaz limpia, responsiva y con retroalimentación visual al usuario durante peticiones asíncronas.

¡Felicidades! Al completar este proyecto habrás creado una aplicación completa con el estándar que exige la industria del desarrollo Frontend con React.
