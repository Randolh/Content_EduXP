# Lección 6: Autenticación Global (`AuthProvider`), Vite Proxy e Integración Fullstack

¡Felicitaciones por llegar a la lección final del curso de **React Esencial**! En esta sesión integradora aprenderás a conectar tu cliente frontend React con la API REST de Express desarrollada en el curso backend, utilizando un **Proxy de desarrollo en Vite** y creando un sistema de **Autenticación Global** con `AuthContext`.

---

## 1. Configuración del Proxy de Desarrollo en Vite (`vite.config.js`)

Para evitar problemas de políticas de origen cruzado (**CORS**) y evitar escribir la URL completa `http://localhost:5000` en cada `fetch()`, configuramos el proxy en `vite.config.js`:

```javascript
// vite.config.js
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';

export default defineConfig({
  plugins: [react()],
  server: {
    port: 3000,
    proxy: {
      // Redirige peticiones /api -> http://localhost:5000/api
      '/api': {
        target: 'http://localhost:5000',
        changeOrigin: true,
        secure: false
      }
    }
  }
});
```

Ahora en tus componentes React basta con escribir `fetch('/api/productos')` y Vite redirigirá transparente la solicitud hacia el servidor Express en el puerto 5000.

---

## 2. Proveedor de Autenticación Global (`AuthContext.jsx`)

Crearemos un contexto de autenticación que gestione el estado del usuario logueado (`user`), el token y las operaciones de Login y Logout.

```jsx
// src/context/AuthContext.jsx
import { createContext, useContext, useState, useEffect } from 'react';

const AuthContext = createContext();

export function AuthProvider({ children }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  // Verificar si hay sesión activa al cargar la aplicación
  useEffect(() => {
    async function verificarSesion() {
      try {
        const res = await fetch('/api/auth/perfil');
        if (res.ok) {
          const json = await res.json();
          setUser(json.data.usuario);
        }
      } catch (err) {
        console.log('No hay sesión activa.');
      } finally {
        setLoading(false);
      }
    }

    verificarSesion();
  }, []);

  // Función de Login
  const login = async (email, password) => {
    const res = await fetch('/api/auth/login', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ email, password })
    });

    const json = await res.json();

    if (!res.ok) {
      throw new Error(json.error?.message || 'Error en autenticación');
    }

    setUser(json.data.usuario);
    return json.data.usuario;
  };

  // Función de Logout
  const logout = async () => {
    await fetch('/api/auth/logout', { method: 'POST' });
    setUser(null);
  };

  return (
    <AuthContext.Provider value={{
      user,
      isAuthenticated: !!user,
      loading,
      login,
      logout
    }}>
      {children}
    </AuthContext.Provider>
  );
}

export function useAuth() {
  const context = useContext(AuthContext);
  if (!context) {
    throw new Error('useAuth debe ser utilizado dentro de AuthProvider');
  }
  return context;
}
```

---

## 3. Formulario de Iniciar Sesión (`LoginForm.jsx`)

```jsx
import { useState } from 'react';
import { useAuth } from '../context/AuthContext.jsx';

export default function LoginForm() {
  const { login } = useAuth();
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [error, setError] = useState('');

  const handleSubmit = async (e) => {
    e.preventDefault();
    setError('');

    try {
      await login(email, password);
      alert('¡Bienvenido!');
    } catch (err) {
      setError(err.message);
    }
  };

  return (
    <form onSubmit={handleSubmit} className="form-auth">
      <h2>Iniciar Sesión</h2>
      {error && <div className="alert-error">{error}</div>}

      <input 
        type="email" 
        placeholder="Correo electrónico"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
        required
      />

      <input 
        type="password" 
        placeholder="Contraseña"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
        required
      />

      <button type="submit">Ingresar</button>
    </form>
  );
}
```

---

## 4. Ensamblado Fullstack en `src/main.jsx`

Envolvemos la aplicación completa con los dos proveedores globales (`AuthProvider` y `CartProvider`):

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App.jsx';
import { AuthProvider } from './context/AuthContext.jsx';
import { CartProvider } from './context/CartContext.jsx';
import './index.css';

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <AuthProvider>
      <CartProvider>
        <App />
      </CartProvider>
    </AuthProvider>
  </React.StrictMode>
);
```

---

## 💡 Autoevaluación

> [!QUIZ]
> ¿Cuál es el beneficio de configurar la propiedad `server.proxy` en `vite.config.js` durante el desarrollo?
> - [ ] Permite que React compile los componentes más rápido.
> - [x] Redirige automáticamente las llamadas relativas `/api/*` hacia el servidor backend Express evitando bloqueos de CORS sin hardcodear URLs absolutas.
> - [ ] Genera automáticamente el token JWT en el cliente.
>
> **Explicación**: El servidor de desarrollo de Vite actúa como intermediario entre el navegador y tu API REST en Express durante la etapa de desarrollo local.

---

## 🛠️ Ejercicio Final Integrador del Curso

**Objetivo**: Renderizar el botón de "Cerrar Sesión" si el usuario está autenticado, o el botón de "Iniciar Sesión" si es un visitante anónimo.

<details class="exercise-solution">
<summary>💡 Ver solución paso a paso</summary>

<div class="solution-content">

```jsx
import { useAuth } from './context/AuthContext.jsx';

export default function UserMenu() {
  const { user, isAuthenticated, logout } = useAuth();

  if (!isAuthenticated) {
    return <button className="btn-primary">Iniciar Sesión</button>;
  }

  return (
    <div className="user-profile">
      <span>Hola, {user.nombre} ({user.rol})</span>
      <button onClick={logout} className="btn-secondary">Cerrar Sesión</button>
    </div>
  );
}
```

</div>
</details>

---

## 🏆 Resumen Final del Curso React Esencial

¡Felicidades por completar la ruta completa de desarrollo Fullstack!
A lo largo de este curso de **React Esencial** has aprendido a:
- Configurar proyectos modernos ultra rápidos con **Vite**.
- Escribir sintaxis declarativa limpia en **JSX**.
- Modularizar tu aplicación en **Componentes Funcionales** reutilizables con **Props**.
- Controlar la reactividad y eventos con **useState** y **useEffect**.
- Crear formularios controlados y componentes de UI como **Modales y Drawers**.
- Administrar el estado global con **Context API** (`CartContext` y `AuthContext`).
- Conectar tu frontend React con un backend Express mediante **Vite Proxy** y **fetch**.
