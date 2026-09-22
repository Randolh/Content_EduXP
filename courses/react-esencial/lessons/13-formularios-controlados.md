# Lección 13: Formularios Controlados y Validaciones

En esta lección aprenderás a construir **Componentes Controlados** en React, donde el estado del componente es la "única fuente de verdad" para los campos de un formulario.

---

## 1. ¿Qué es un Componente Controlado?

En HTML tradicional, los campos `<input>` mantienen su propio estado interno. En React, un input está "controlado" cuando vinculamos su atributo `value` a una variable de estado (`useState`) y actualizamos ese estado en la propiedad `onChange`.

```jsx
import { useState } from 'react';

export default function FormularioRegistro() {
  const [formData, setFormData] = useState({
    nombre: '',
    email: '',
    categoria: 'react'
  });
  const [error, setError] = useState('');

  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData((prev) => ({
      ...prev,
      [name]: value
    }));
  };

  const handleSubmit = (e) => {
    e.preventDefault(); // Previene la recarga del navegador
    if (!formData.nombre.trim()) {
      setError('El nombre es obligatorio');
      return;
    }
    setError('');
    alert(`Registro exitoso para: ${formData.nombre}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      {error && <p className="error">{error}</p>}
      
      <div>
        <label>Nombre:</label>
        <input
          type="text"
          name="nombre"
          value={formData.nombre}
          onChange={handleChange}
        />
      </div>

      <div>
        <label>Email:</label>
        <input
          type="email"
          name="email"
          value={formData.email}
          onChange={handleChange}
        />
      </div>

      <button type="submit">Enviar</button>
    </form>
  );
}
```

---

## Autoevaluación

> [!QUIZ]
> ¿Por qué ejecutamos `e.preventDefault()` en el controlador del evento `onSubmit` de un formulario?
> - [ ] Para borrar los inputs automáticamente.
> - [x] Para evitar que el navegador realice una petición HTTP POST predeterminada y recargue la página completa.
> - [ ] Para deshabilitar el botón de envío.
>
> **Explicación**: `e.preventDefault()` cancela la conducta por defecto del navegador al enviar un formulario en HTML, permitiendo que JavaScript y React procesen la información de forma SPA (Single Page Application).

---

## Ejercicio Práctico

Crea un formulario con un campo `input` de búsqueda. Agrega una validación que no permita enviar el formulario si el texto de búsqueda tiene menos de 3 caracteres.
