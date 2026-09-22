# Lección 11: Renderizado de Listas y la importancia de la Prop key

En esta lección aprenderás a renderizar colecciones de datos dinámicas iterando arreglos con `.map()` y entendiendo por qué la propiedad `key` es fundamental para el algoritmo de reconciliación de React.

---

## 1. Iterando Arreglos con `.map()`

Para transformar un arreglo de datos en una lista de elementos JSX, usamos el método de orden superior `.map()` de JavaScript.

```jsx
export default function ListaFrutas() {
  const frutas = [
    { id: 101, nombre: 'Manzana', precio: 1.5 },
    { id: 102, nombre: 'Plátano', precio: 0.8 },
    { id: 103, nombre: 'Naranja', precio: 1.2 }
  ];

  return (
    <ul>
      {frutas.map((fruta) => (
        <li key={fruta.id}>
          {fruta.nombre} - ${fruta.precio}
        </li>
      ))}
    </ul>
  );
}
```

---

## 2. ¿Por qué es obligatoria la prop `key`?

La prop `key` le brinda a React una identidad única para cada elemento de la lista. 

- **¿Qué sucede sin `key`?** React no puede identificar qué elementos cambiaron, se agregaron o eliminaron, lo que causa re-renderizados ineficientes o errores de estado en la UI.
- **Regla de oro**: La `key` debe ser un identificador único e invariable (como un `id` de base de datos). Evita usar el índice de la lista `(item, index) => ...` si la lista puede cambiar de orden o eliminarse elementos.

---

## Autoevaluación

> [!QUIZ]
> ¿Cuál es la mejor opción para asignar la propiedad `key` al iterar una lista en React?
> - [ ] Usar `Math.random()` en cada renderizado.
> - [x] Usar un identificador único y persistente proveniente de los datos (como un `id`).
> - [ ] No poner la prop `key`.
>
> **Explicación**: El atributo `key` debe ser único y constante a lo largo del tiempo para que React pueda rastrear qué elementos han cambiado correctamente en el Virtual DOM.

---

## Ejercicio Práctico

Dado un arreglo `const productos = [{ id: 'a', nombre: 'Teclado' }, { id: 'b', nombre: 'Mouse' }]`, renderiza una lista ordenada `<ol>` mostrando el nombre de cada producto asegurando la propiedad `key` correcta.
