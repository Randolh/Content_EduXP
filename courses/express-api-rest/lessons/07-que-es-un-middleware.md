# Lección 7: ¿Qué es un Middleware en Express?

En esta lección aprenderás **qué es un Middleware** y cómo funciona la función `next()`.

---

## 1. El Concepto de Middleware

Un **Middleware** es una función intermedia que se ejecuta **antes** de que tu petición llegue a la ruta final.

Tiene 3 parámetros: `(req, res, next)`.

```javascript
// Middleware logger de consola
app.use((req, res, next) => {
  console.log(`Petición recibida en URL: ${req.url}`);
  
  // ¡OBLIGATORIO! Llama a next() para dar paso a la siguiente función
  next();
});
```

> [!WARNING]
> Si no ejecutas `next()`, la petición del cliente se quedará colgada esperando respuesta.

---

## Autoevaluación

> [!QUIZ]
> ¿Qué función debes llamar obligatoriamente al final de un middleware para permitir que la petición continúe su camino?
> - [ ] `res.continue()`
> - [x] `next()`
> - [ ] `app.forward()`
>
> **Explicación**: `next()` le indica a Express que pase el control al siguiente middleware o handler de la cadena.

---

## Ejercicio Práctico

Crea un middleware que imprima la hora actual con `new Date().toLocaleTimeString()` en cada petición que reciba el servidor.
