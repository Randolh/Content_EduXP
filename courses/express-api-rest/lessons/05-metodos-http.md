# Lección 4: Entendiendo los Métodos HTTP (GET, POST, PUT, DELETE)

En esta lección aprenderás **qué significa cada método HTTP** en una arquitectura de API REST.

---

## 1. Los 4 Métodos HTTP Principales

Una API REST utiliza verbos estándar para saber qué acción realizar sobre los datos:

* **`GET` (Leer):** Solicita información al servidor (ej. obtener lista de productos).
* **`POST` (Crear):** Envía datos nuevos para registrar un recurso (ej. crear nuevo usuario).
* **`PUT` (Actualizar):** Modifica un elemento existente (ej. cambiar precio de un producto).
* **`DELETE` (Eliminar):** Borra un recurso del sistema.

```javascript
app.get('/api/usuarios', (req, res) => res.send('Listar usuarios'));
app.post('/api/usuarios', (req, res) => res.send('Crear usuario'));
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué método HTTP debe utilizarse cuando un usuario envía un formulario para registrarse por primera vez?
> - [ ] `GET`
> - [x] `POST`
> - [ ] `DELETE`
>
> **Explicación**: El verbo `POST` se utiliza para la creación de nuevos recursos en el backend.

---

## Ejercicio Práctico

Agrega a tu servidor una ruta `app.post('/api/tareas', ...)` que responda con la frase `"Tarea creada"` y pruébala seleccionando `POST` en Thunder Client.
