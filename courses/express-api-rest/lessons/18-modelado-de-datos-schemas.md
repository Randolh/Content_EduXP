# Lección 18: Modelado de Datos y Relaciones Backend

En esta lección aprenderás cómo estructurar **Modelos de Datos y Relaciones** en el backend para representar entidades de dominio reales (como Usuarios, Productos y Órdenes).

---

## 1. El Patrón Modelo (Model Layer)

En una arquitectura limpia (como MVC), la capa de modelo abstrae la estructura de los objetos y las operaciones con la base de datos o almacenamiento.

```javascript
// models/Producto.js - Ejemplo de Esquema conceptual
export class ProductoModel {
  constructor({ id, nombre, precio, stock, categoriaId }) {
    this.id = id;
    this.nombre = nombre;
    this.precio = precio;
    this.stock = stock;
    this.categoriaId = categoriaId;
  }
}
```

---

## 2. Tipos de Relaciones entre Entidades

1. **Uno a Muchos (1:N)**: Un Usuario tiene muchas Órdenes de compra.
2. **Muchos a Muchos (N:M)**: Una Orden de compra contiene muchos Productos, y un Producto pertenece a muchas Órdenes.

```javascript
// Ejemplo de Entidad Relacionada: Orden de Compra
const ordenEjemplo = {
  id: 'ord-1001',
  usuarioId: 42, // Relación con el Usuario
  fecha: '2026-09-22',
  items: [ // Relación N:M representada mediante referencias y cantidades
    { productoId: 101, cantidad: 2, precioUnitario: 99.99 },
    { productoId: 205, cantidad: 1, precioUnitario: 15.00 }
  ],
  total: 214.98,
  estado: 'completado'
};
```

---

## Autoevaluación

> [!QUIZ]
> En un sistema de E-Commerce, ¿qué tipo de relación existe entre la entidad `Usuario` y la entidad `OrdenDeCompra`?
> - [ ] Uno a Uno (1:1).
> - [x] Uno a Muchos (1:N), ya que un solo usuario puede realizar múltiples compras a lo largo del tiempo.
> - [ ] Ninguna relación.
>
> **Explicación**: Un único registro de usuario puede estar asociado a cero, una o múltiples órdenes de compra en el sistema.

---

## Ejercicio Práctico

Diseña el objeto JSON para una entidad `Reseña` que se relacione con un `productoId` y un `usuarioId`, incluyendo una calificación numérica de 1 a 5 y un comentario.
