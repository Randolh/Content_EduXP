# Lección 10: Renderizado Condicional en React

En esta lección aprenderás cómo mostrar u ocultar elementos del DOM en función del estado de tu aplicación utilizando los patrones más comunes de renderizado condicional.

---

## 1. Métodos de Renderizado Condicional

En React puedes tomar decisiones en el renderizado usando sintaxis de JavaScript estándar:

1. **Operador Ternario (`condicion ? verdadero : falso`)**: Ideal para alternar entre dos vistas o componentes.
2. **Operador Lógico AND (`condicion && elemento`)**: Ideal para mostrar algo solo si la condición es verdadera.
3. **Sentencia `if / else` dentro de la función**: Util para retornar vistas completamente diferentes (ej. pantalla de carga vs. contenido final).

```jsx
import { useState } from 'react';

export default function PanelUsuario() {
  const [isLoggedIn, setIsLoggedIn] = useState(false);
  const [hasUnreadMessages, setHasUnreadMessages] = useState(true);

  return (
    <div className="card">
      <h2>Estado de Sesión</h2>

      {/* Operador Ternario */}
      {isLoggedIn ? (
        <button onClick={() => setIsLoggedIn(false)}>Cerrar Sesión</button>
      ) : (
        <button onClick={() => setIsLoggedIn(true)}>Iniciar Sesión</button>
      )}

      {/* Operador Lógico && */}
      {isLoggedIn && hasUnreadMessages && (
        <p className="badge">📩 Tienes mensajes sin leer</p>
      )}
    </div>
  );
}
```

---

## Autoevaluación

> [!QUIZ]
> En la sintaxis `{esModoOscuro && <TemaOscuro />}`, ¿qué ocurre cuando `esModoOscuro` es `false`?
> - [ ] Se renderiza `<TemaOscuro />` de todas formas.
> - [x] React no renderiza nada en esa posición (retorna `false` que no produce HTML).
> - [ ] Se genera un error de compilación.
>
> **Explicación**: El operador `&&` evalúa el lado derecho solo si el lado izquierdo es verdadero. Si es falso, la expresión evalúa a `false`, lo cual React ignora en el renderizado.

---

## Ejercicio Práctico

Crea un componente `BotonLikes` que tenga un estado `liked` (booleano). Si es `true`, debe mostrar `"❤️ Te gusta esto"`, y si es `false`, debe mostrar `"🤍 Dar Like"`.
