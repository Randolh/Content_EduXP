# Lección 5: Pasar información entre componentes con Props

En esta lección aprenderás **exclusivamente a usar Props** para enviar información desde un componente padre hacia un componente hijo.

---

## 1. ¿Qué son las Props?

Las **Props** (Propiedades) son como los parámetros que le pasas a una función. Le permiten a un mismo componente mostrar información diferente según los datos que reciba.

### Componente Hijo (`TarjetaUsuario.jsx`):
```jsx
export default function TarjetaUsuario(props) {
  return (
    <div className="tarjeta">
      <h3>Usuario: {props.nombre}</h3>
      <p>Rol: {props.rol}</p>
    </div>
  );
}
```

### Componente Padre (`App.jsx`):
```jsx
import TarjetaUsuario from './TarjetaUsuario';

export default function App() {
  return (
    <div>
      <TarjetaUsuario nombre="Ana" rol="Administrador" />
      <TarjetaUsuario nombre="Carlos" rol="Estudiante" />
    </div>
  );
}
```

---

## Autoevaluación

> [!QUIZ]
> ¿Para qué sirven las Props en React?
> - [ ] Para instalar librerías externas.
> - [x] Para pasar datos e información de un componente padre a un componente hijo.
> - [ ] Para conectar el servidor con la base de datos.
>
> **Explicación**: Las Props son el mecanismo de comunicación unidireccional entre componentes en React.

---

## Ejercicio Práctico

Crea un componente `Producto(props)` que reciba `props.titulo` y `props.precio`, e instáncialo dos veces desde `App.jsx` con productos y precios diferentes.
