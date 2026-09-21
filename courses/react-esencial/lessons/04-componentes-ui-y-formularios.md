# Lección 4: Formularios Controlados, Modales y Componentes de UI

Para permitir que los usuarios interactúen con nuestra aplicación (crear productos, actualizar datos, abrir ventanas emergentes), debemos manejar los eventos de entrada de usuario. En esta lección aprenderás a implementar **Formularios Controlados** y a estructurar componentes de interfaz reutilizables como **Modales y Drawers**.

---

## 1. Formularios Controlados en React

En un **Formulario Controlado**, React es la "única fuente de la verdad". El valor de cada elemento de entrada (`<input>`, `<select>`, `<textarea>`) está vinculado directamente a un estado de `useState`, y cada pulsación de tecla actualiza dicho estado.

```jsx
import { useState } from 'react';

export default function FormularioCrearProducto({ onGuardar }) {
  const [formData, setFormData] = useState({
    nombre: '',
    precio: '',
    categoria: 'frontend'
  });

  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData(prev => ({
      ...prev,
      [name]: value
    }));
  };

  const handleSubmit = (e) => {
    e.preventDefault(); // Prevenir recarga por defecto de la página
    
    if (!formData.nombre.trim() || Number(formData.precio) <= 0) {
      alert('Por favor completa todos los campos correctamente.');
      return;
    }

    onGuardar(formData);
    setFormData({ nombre: '', precio: '', categoria: 'frontend' }); // Limpiar formulario
  };

  return (
    <form onSubmit={handleSubmit} className="form-box">
      <h3>Crear Nuevo Producto</h3>

      <div className="form-group">
        <label>Nombre del Producto:</label>
        <input 
          type="text"
          name="nombre"
          value={formData.nombre}
          onChange={handleChange}
          placeholder="Ej. Teclado Gamer"
        />
      </div>

      <div className="form-group">
        <label>Precio ($):</label>
        <input 
          type="number"
          name="precio"
          value={formData.precio}
          onChange={handleChange}
          placeholder="99.99"
        />
      </div>

      <button type="submit" className="btn btn-primary">Guardar Producto</button>
    </form>
  );
}
```

---

## 2. Componente de UI Reutilizable: Modal Dialog

Un **Modal** se renderiza condicionalmente dependiendo de un estado booleano (`isOpen`).

```jsx
// Componente Modal Reutilizable
export default function Modal({ isOpen, onClose, titulo, children }) {
  if (!isOpen) return null; // Si no está abierto, no renderiza nada en el DOM

  return (
    <div className="modal-overlay" onClick={onClose}>
      <div className="modal-content" onClick={(e) => e.stopPropagation()}>
        <div className="modal-header">
          <h3>{titulo}</h3>
          <button className="btn-close" onClick={onClose}>&times;</button>
        </div>
        <div className="modal-body">
          {children}
        </div>
      </div>
    </div>
  );
}
```

### Uso del Modal en `App.jsx`:

```jsx
import { useState } from 'react';
import Modal from './Modal.jsx';
import FormularioCrearProducto from './FormularioCrearProducto.jsx';

export default function App() {
  const [modalAbierto, setModalAbierto] = useState(false);

  return (
    <div>
      <button onClick={() => setModalAbierto(true)}>+ Agregar Producto</button>

      <Modal 
        isOpen={modalAbierto} 
        onClose={() => setModalAbierto(false)}
        titulo="Nuevo Producto"
      >
        <FormularioCrearProducto 
          onGuardar={(datos) => {
            console.log('Datos guardados:', datos);
            setModalAbierto(false);
          }} 
        />
      </Modal>
    </div>
  );
}
```

---

## 💡 Autoevaluación

> [!QUIZ]
> ¿Por qué es necesario ejecutar `e.preventDefault()` dentro de la función asignada al evento `onSubmit` de un formulario en React?
> - [ ] Para reiniciar los valores del formulario a cero automáticamente.
> - [x] Para evitar que el navegador ejecute su comportamiento por defecto de enviar una petición HTTP completa y recargar toda la página web.
> - [ ] Para habilitar la validación automática de campos requeridos HTML5.
>
> **Explicación**: En aplicaciones Single Page Application (SPA) con React, procesamos la información asíncronamente con JavaScript sin refrescar la ventana del navegador.

---

## 🛠️ Ejercicio Práctico: Componente Drawer Lateral (Carrito/Menú)

**Objetivo**: Crear un componente de Drawer (menú o carrito deslizante) que aparezca desde el lateral derecho.

<details class="exercise-solution">
<summary>💡 Ver solución paso a paso</summary>

<div class="solution-content">

```jsx
export default function Drawer({ isOpen, onClose, children }) {
  return (
    <aside className={`drawer ${isOpen ? 'drawer-open' : ''}`}>
      <div className="drawer-header">
        <h4>Tu Carrito de Compras</h4>
        <button onClick={onClose}>Cerrar ✕</button>
      </div>
      <div className="drawer-body">
        {children}
      </div>
    </aside>
  );
}
```

</div>
</details>

---

## 📌 Resumen

- Los **Formularios Controlados** enlazan las entradas HTML con estados de React mediante `value` y `onChange`.
- Evita recargar la página llamando a `e.preventDefault()`.
- Los componentes de UI como **Modales y Drawers** se controlan con estados booleanos (`isOpen`).
- En la siguiente lección aprenderás a compartir estados entre múltiples componentes sin prop-drilling usando **Context API**.
