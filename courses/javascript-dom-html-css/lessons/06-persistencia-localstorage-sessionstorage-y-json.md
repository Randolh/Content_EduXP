# 6. Persistencia Web: LocalStorage, SessionStorage y JSON

Para garantizar que el estado de una aplicacion web (preferencias de configuracion, temas oscuros, carritos de compra o listas de tareas) sobreviva a recargas de pagina o cierres del navegador, los estandares web proporcionan la API de **Web Storage**.

---

## Objetivos de la Leccion
- Comprender las caracteristicas y diferencias entre `localStorage` y `sessionStorage`.
- Almacenar, recuperar y purgar datos con `setItem`, `getItem`, `removeItem` y `clear`.
- Serializar estructuras de datos complejas mediante `JSON.stringify()` y `JSON.parse()`.
- Controlar excepciones de almacenamiento y cuotas maximas del navegador.

---

## `localStorage` vs `sessionStorage`

| Caracteristica | `localStorage` | `sessionStorage` |
| :--- | :--- | :--- |
| **Persistencia** | Indefinida (persiste tras reiniciar el equipo o navegador). | Temporal (se purga al cerrar la pestana actual). |
| **Capacidad Aprox.** | 5MB a 10MB por origen. | ~5MB por pestana y origen. |
| **Ambito de Acceso** | Mismo protocolo, dominio y puerto (Mismo Origen). | Exclusivo para la pestana que lo genero. |
| **Tipo de Almacenamiento** | **Exclusivamente cadenas de texto (Strings)**. | **Exclusivamente cadenas de texto (Strings)**. |

---

## Operaciones de Almacenamiento

```javascript
// 1. Almacenar valores simples
localStorage.setItem("tema_visual", "modo_oscuro");
localStorage.setItem("idioma_interfaz", "es-ES");

// 2. Recuperar valores (Retorna null si la clave no existe)
const tema = localStorage.getItem("tema_visual");
console.log(`Tema recuperado: ${tema}`); // "modo_oscuro"

// 3. Eliminar una clave especifica
localStorage.removeItem("idioma_interfaz");

// 4. Limpiar todo el almacenamiento local del dominio actual
// localStorage.clear();
```

---

## Serializacion de Objetos Complejos con JSON

Dado que Web Storage solo admite cadenas de texto plano, intentar almacenar un objeto directamente provocara que el motor lo convierta a la cadena literal `"[object Object]"`, destruyendo la informacion.

Para solucionarlo, serializamos a formato JSON:

```javascript
const perfilSesion = {
    usuarioId: 1045,
    nombre: "Andrea Rios",
    roles: ["editor", "revisor"],
    preferencias: {
        notificacionesEmail: true,
        articulosPorPagina: 25
    }
};

// 1. SERIALIZACION: De Objeto a Cadena de Texto JSON
const jsonCadena = JSON.stringify(perfilSesion);
localStorage.setItem("sesion_activa", jsonCadena);

// 2. DESERIALIZACION: De Cadena de Texto JSON a Objeto JavaScript
const datosRecuperados = localStorage.getItem("sesion_activa");

let objetoPerfil = null;
if (datosRecuperados) {
    try {
        objetoPerfil = JSON.parse(datosRecuperados);
        console.log(`Bienvenido de nuevo, ${objetoPerfil.nombre}`);
    } catch (error) {
        console.error("Fallo al reconstruir datos desde JSON:", error);
    }
}
```

> [!WARNING]
> **Privacidad y Seguridad en LocalStorage:**  
> Nunca guardes contraseñas en texto plano ni tokens altamente sensibles (como claves maestras de pago) en `localStorage`, ya que cualquier script inyectado mediante vulnerabilidades XSS en tu sitio puede leer `localStorage` en su totalidad.

---

## Ejercicio Practico

Crea un script que almacene una lista de notas `[{ id: 1, texto: "Comprar cables" }]` en `localStorage`:
1. Implementa una funcion `guardarNotas(notas)` que serialize a JSON.
2. Implementa una funcion `cargarNotas()` que devuelva el arreglo parseado o un arreglo vacio `[]` si la clave no existe.
3. Prueba agregar una nota nueva y verificar la persistencia recargando la pagina.
