# Lección 12: Consumo de APIs REST con fetch y async/await

En esta lección aprenderás a conectar tu aplicación de React con servidores externos consumiendo APIs REST mediante `fetch` y manejando los tres estados esenciales de una petición: **Cargando (`loading`)**, **Error (`error`)** y **Datos (`data`)**.

---

## 1. El Patrón de Carga de Datos en `useEffect`

Para hacer peticiones HTTP al montar un componente, usamos `useEffect` combinando estados locales para la interfaz de usuario.

```jsx
import { useState, useEffect } from 'react';

export default function ListaUsuarios() {
  const [usuarios, setUsuarios] = useState([]);
  const [cargando, setCargando] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function obtenerUsuarios() {
      try {
        const respuesta = await fetch('https://jsonplaceholder.typicode.com/users');
        if (!respuesta.ok) {
          throw new Error('Error al obtener la información');
        }
        const datos = await respuesta.json();
        setUsuarios(datos);
      } catch (err) {
        setError(err.message);
      } finally {
        setCargando(false);
      }
    }

    obtenerUsuarios();
  }, []);

  if (cargando) return <p>⌛ Cargando usuarios...</p>;
  if (error) return <p className="error">❌ Error: {error}</p>;

  return (
    <ul>
      {usuarios.map((u) => (
        <li key={u.id}>{u.name} - {u.email}</li>
      ))}
    </ul>
  );
}
```

---

## Autoevaluación

> [!QUIZ]
> ¿Por qué no debemos pasar una función `async` directamente a `useEffect(async () => {...})`?
> - [ ] Porque JavaScript lanza un error de sintaxis inmediatamente.
> - [x] Porque `useEffect` espera que la función retorne una función de limpieza (cleanup function) o nada, pero las funciones `async` siempre retornan una Promesa.
> - [ ] Porque las peticiones HTTP están prohibidas en React.
>
> **Explicación**: `useEffect` reserva el valor retornado para la función de limpieza (cleanup). Si le pasas una función `async`, esta devuelve una Promesa, lo cual interfiere con la arquitectura interna de React. La solución es definir una función `async` auxiliar dentro del efecto.

---

## Ejercicio Práctico

Escribe un componente `PerfilPokemon` que use `useEffect` para hacer un `fetch` a `https://pokeapi.co/api/v2/pokemon/ditto` y muestre el nombre del pokémon y su peso en pantalla.
