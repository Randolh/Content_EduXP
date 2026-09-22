# Lección 20: Carga bajo demanda con React.lazy y Suspense

En esta lección aprenderás a reducir el tamaño del paquete JavaScript inicial (bundle size) dividiendo tu código en fragmentos menores con **Code Splitting**, cargando componentes únicamente cuando se necesitan con **`React.lazy`** y **`<Suspense>`**.

---

## 1. Importación Dinámica y Suspense

Por defecto, Vite / Webpack empaqueta todo el código del proyecto en un solo archivo. Con `React.lazy`, un componente pesado se descarga del servidor solo al momento de renderizarse en pantalla.

```jsx
import { lazy, Suspense, useState } from 'react';

// Carga perezosa (Lazy Import)
const GraficoEstadisticas = lazy(() => import('./GraficoEstadisticas'));

export default function Dashboard() {
  const [mostrarGrafico, setMostrarGrafico] = useState(false);

  return (
    <div>
      <h2>Panel Principal</h2>
      <button onClick={() => setMostrarGrafico(true)}>Cargar Gráfico Pesado</button>

      {mostrarGrafico && (
        /* Suspense muestra un fallback (Loader) mientras descarga el componente por red */
        <Suspense fallback={<p>⌛ Descargando módulo del gráfico...</p>}>
          <GraficoEstadisticas />
        </Suspense>
      )}
    </div>
  );
}
```

---

## Autoevaluación

> [!QUIZ]
> ¿Para qué sirve la propiedad `fallback` del componente `<Suspense>`?
> - [ ] Para especificar qué hacer en caso de un error de red.
> - [x] Para mostrar un componente de carga (spinner o skeleton) mientras se descarga el código del componente lazy.
> - [ ] Para definir una ruta alternativa.
>
> **Explicación**: `fallback` recibe cualquier elemento JSX que se mostrará temporalmente en pantalla mientras el código del componente asíncrono se descarga por red.

---

## Ejercicio Práctico

Configura el componente `<Suspense>` envolviendo una vista de administración importada con `lazy(() => import('./AdminPanel'))`.
