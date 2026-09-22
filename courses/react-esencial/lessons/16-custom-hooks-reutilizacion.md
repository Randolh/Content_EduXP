# Lección 16: Creación de Custom Hooks Reutilizables

En esta lección aprenderás a abstraer y reutilizar lógica con estado entre múltiples componentes mediante la creación de tus propios **Custom Hooks** (Hooks Personalizados).

---

## 1. ¿Qué es un Custom Hook?

Un Custom Hook es una función de JavaScript cuyo nombre comienza obligatoriamente con el prefijo **`use`** (ej. `useFetch`, `useLocalStorage`, `useForm`) y que puede llamar a otros Hooks de React dentro de ella.

### Ejemplo: Custom Hook `useFetch`

```jsx
import { useState, useEffect } from 'react';

// 1. Definición del Custom Hook
export function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    setLoading(true);
    fetch(url)
      .then((res) => {
        if (!res.ok) throw new Error('Error HTTP');
        return res.json();
      })
      .then((data) => setData(data))
      .catch((err) => setError(err.message))
      .finally(() => setLoading(false));
  }, [url]);

  return { data, loading, error };
}

// 2. Uso dentro de cualquier Componente
export default function CatalogoProductos() {
  const { data: productos, loading, error } = useFetch('https://fakestoreapi.com/products');

  if (loading) return <p>Cargando catálogo...</p>;
  if (error) return <p>Error: {error}</p>;

  return (
    <div>
      <h2>Catálogo de Productos</h2>
      <ul>
        {productos?.map((p) => (
          <li key={p.id}>{p.title} - ${p.price}</li>
        ))}
      </ul>
    </div>
  );
}
```

---

## Autoevaluación

> [!QUIZ]
> ¿Cuál de los siguientes nombres cumple con la convención estándar para definir un Custom Hook en React?
> - [ ] `obtenerDatosGuardados()`
> - [x] `useLocalStorage()`
> - [ ] `CustomHookEstado()`
>
> **Explicación**: El prefijo `use` en minúscula es una convención obligatoria exigida por el linter de React para identificar que la función contiene llamadas a Hooks internos de React.

---

## Ejercicio Práctico

Crea un Custom Hook llamado `useContador(inicial = 0)` que retorne `{ contador, incrementar, decrementar, resetear }` y pruébalo en un componente.
