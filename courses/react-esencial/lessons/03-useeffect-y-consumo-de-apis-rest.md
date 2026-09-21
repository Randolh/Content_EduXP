# Lección 3: Efectos Secundarios con `useEffect` y Consumo de APIs REST (`fetch`)

Las aplicaciones del mundo real necesitan cargar información desde un servidor backend o API de terceros. En esta lección aprenderás a utilizar el Hook **useEffect** para sincronizar tus componentes con sistemas externos y realizar peticiones HTTP asíncronas de forma limpia.

---

## 1. El Hook `useEffect` y su Arreglo de Dependencias

`useEffect` permite ejecutar código secundario en momentos específicos del ciclo de vida del componente (al montarse en pantalla, al actualizarse o al desmontarse).

```jsx
import { useEffect } from 'react';

useEffect(() => {
  // Código que se ejecuta tras el renderizado
  console.log('Componente montado en la pantalla');

  return () => {
    // Función de limpieza (Cleanup) opcional (ej. al desmontar)
    console.log('Componente desmontado');
  };
}, []); // <- Arreglo de dependencias
```

### Comportamiento según el Arreglo de Dependencias:
1. `[]` (Arreglo vacío): Se ejecuta **una sola vez** al montarse el componente. Ideal para peticiones HTTP iniciales.
2. `[variable]`: Se ejecuta al montarse y **cada vez que `variable` cambie de valor**.
3. *Sin arreglo*: Se ejecuta en **cada renderizado** del componente (¡usar con precaución!).

---

## 2. Consumo de una API REST con `fetch()` y Estados de Carga

Al realizar peticiones de red asíncronas, siempre debes gestionar 3 estados en la interfaz:
1. **Datos (`data`)**: La información recibida de la API.
2. **Cargando (`loading`)**: `true` mientras se espera la respuesta HTTP.
3. **Error (`error`)**: Captura de excepciones si la conexión o la API fallan.

### Componente `ListaProductos.jsx`

```jsx
import { useState, useEffect } from 'react';

export default function ListaProductos() {
  const [productos, setProductos] = useState([]);
  const [cargando, setCargando] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    // Definición de función asíncrona dentro de useEffect
    const obtenerProductos = async () => {
      try {
        setCargando(true);
        const respuesta = await fetch('/api/productos');
        
        if (!respuesta.ok) {
          throw new Error(`Error de servidor: ${respuesta.status}`);
        }

        const resultado = await respuesta.json();
        setProductos(resultado.data || []);
      } catch (err) {
        setError(err.message);
      } finally {
        setCargando(false);
      }
    };

    obtenerProductos();
  }, []); // Se ejecuta 1 sola vez al cargar la página

  if (cargando) return <div className="spinner">⏳ Cargando productos desde el servidor...</div>;
  if (error) return <div className="error-banner">❌ Error al cargar productos: {error}</div>;

  return (
    <div className="grid-productos">
      {productos.map(p => (
        <div key={p.id} className="card-producto">
          <h4>{p.nombre}</h4>
          <p>${p.precio}</p>
        </div>
      ))}
    </div>
  );
}
```

---

## 💡 Autoevaluación

> [!QUIZ]
> ¿Por qué es fundamental incluir un arreglo de dependencias vacío `[]` al realizar una petición `fetch` dentro de `useEffect`?
> - [ ] Para obligar a React a reintentar la petición si falla.
> - [x] Para asegurar que la petición a la API se ejecute únicamente una sola vez cuando el componente se monta en la pantalla, evitando bucles infinitos de peticiones HTTP.
> - [ ] Porque de lo contrario el navegador bloquea la petición por politicas de CORS.
>
> **Explicación**: Si no pasas el arreglo de dependencias `[]`, cada `setProductos` disparará un re-renderizado que volverá a ejecutar el `useEffect`, creando un bucle infinito que saturará el servidor.

---

## 🛠️ Ejercicio Práctico: Filtro de Búsqueda Asíncrono por Categoría

**Objetivo**: Re-ejecutar la petición a la API cuando cambie el estado de la categoría seleccionada en un selector `<select>`.

<details class="exercise-solution">
<summary>💡 Ver solución paso a paso</summary>

<div class="solution-content">

```jsx
import { useState, useEffect } from 'react';

export default function FiltroProductos() {
  const [categoria, setCategoria] = useState('todas');
  const [items, setItems] = useState([]);

  useEffect(() => {
    async function cargarPorCategoria() {
      const url = categoria === 'todas' 
        ? '/api/productos' 
        : `/api/productos?categoria=${categoria}`;
      
      const res = await fetch(url);
      const json = await res.json();
      setItems(json.data || []);
    }

    cargarPorCategoria();
  }, [categoria]); // <- Se re-ejecuta cada vez que cambia el estado 'categoria'

  return (
    <div>
      <select value={categoria} onChange={(e) => setCategoria(e.target.value)}>
        <option value="todas">Todas las categorías</option>
        <option value="electronica">Electrónica</option>
        <option value="ropa">Ropa</option>
      </select>

      <p>Resultados cargados: {items.length}</p>
    </div>
  );
}
```

</div>
</details>

---

## 📌 Resumen

- **`useEffect`** administra los efectos secundarios en React.
- Controla el ciclo de vida con el **arreglo de dependencias**.
- Maneja siempre los tres estados al consumir APIs: `data`, `loading` y `error`.
- En la siguiente lección aprenderás a construir componentes de UI avanzados (Modales, Drawers) y **Formularios Controlados**.
