# Lección 17: Optimización de Rendimiento con useMemo y useCallback

En esta lección aprenderás a prevenir cálculos innecesarios y re-renderizados costosos mediante los Hooks de optimización de React: **`useMemo`** y **`useCallback`**.

---

## 1. Memorización de Valores Calculados con `useMemo`

`useMemo` almacena en caché el resultado de un cálculo pesado entre renderizados, volviendo a ejecutar la función únicamente cuando alguna de sus dependencias cambia.

```jsx
import { useState, useMemo } from 'react';

export default function FiltroNumeros() {
  const [numeros] = useState([10, 25, 40, 55, 70, 85, 100]);
  const [limite, setLimite] = useState(50);
  const [temaOscuro, setTemaOscuro] = useState(false);

  // Solo se recorta el arreglo cuando 'limite' o 'numeros' cambian
  const numerosFiltrados = useMemo(() => {
    console.log('Filtrando números pesados...');
    return numeros.filter((n) => n > limite);
  }, [numeros, limite]);

  return (
    <div style={{ background: temaOscuro ? '#333' : '#fff', color: temaOscuro ? '#fff' : '#000' }}>
      <button onClick={() => setTemaOscuro(!temaOscuro)}>Cambiar Tema</button>
      <input
        type="number"
        value={limite}
        onChange={(e) => setLimite(Number(e.target.value))}
      />
      <p>Números mayores a {limite}: {numerosFiltrados.join(', ')}</p>
    </div>
  );
}
```

---

## 2. Memorización de Funciones con `useCallback`

`useCallback` memoriza la **definición de una función** para asegurar que mantenga exactamente la misma referencia en memoria entre renderizados.

```jsx
import { useState, useCallback } from 'react';

export default function Padre() {
  const [contador, setContador] = useState(0);

  // Mantiene la referencia de la función a menos que cambien sus dependencias
  const manejarEliminar = useCallback((id) => {
    console.log(`Eliminando elemento con id: ${id}`);
  }, []);

  return (
    <div>
      <button onClick={() => setContador(contador + 1)}>Re-renderizar ({contador})</button>
    </div>
  );
}
```

---

## Autoevaluación

> [!QUIZ]
> ¿Cuál es la diferencia principal entre `useMemo` y `useCallback`?
> - [ ] `useMemo` se usa en componentes de clase y `useCallback` en componentes funcionales.
> - [x] `useMemo` devuelve y almacena en caché el **resultado calculado** de una función, mientras que `useCallback` almacena la **definición de la función en sí**.
> - [ ] Ninguna, hacen exactamente lo mismo.
>
> **Explicación**: `useMemo(() => fn(), [deps])` memoriza un valor retornado. `useCallback(fn, [deps])` memoriza la instancia de la función `fn`.

---

## Ejercicio Práctico

Utiliza `useMemo` para memorizar la suma total de un arreglo de compras `[12.5, 45.0, 8.99]` de forma que no se re-calcule si cambia un estado de visibilidad secundario.
