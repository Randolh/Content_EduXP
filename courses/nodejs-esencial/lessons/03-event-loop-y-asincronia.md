# Lección 3: Entendiendo la Ejecución Asíncrona (Event Loop)

En esta lección aprenderás **cómo Node.js ejecuta código asíncrono** sin congelar el programa.

---

## 1. Asincronía con `setTimeout`

A diferencia de otros lenguajes que esperan a que una tarea larga termine antes de continuar, Node.js no se bloquea.

Prueba este código:

```javascript
console.log("1. Inicio");

setTimeout(() => {
  console.log("2. Tarea asíncrona completada (después de 1 segundo)");
}, 1000);

console.log("3. Fin");
```

**Salida en pantalla:**
```text
1. Inicio
3. Fin
2. Tarea asíncrona completada
```

Node.js continuó ejecutando el punto 3 mientras el temporizador esperaba en segundo plano.

---

## Autoevaluación

> [!QUIZ]
> ¿Por qué el mensaje "3. Fin" aparece antes que "2. Tarea asíncrona completada"?
> - [ ] Porque hubo un error en el código.
> - [x] Porque Node.js delega la espera en segundo plano y no congela la ejecución del script principal.
> - [ ] Porque `setTimeout` invierte el orden de las líneas.
>
> **Explicación**: El modelo no bloqueante permite seguir procesando instrucciones mientras se espera la finalización del evento diferido.

---

## Ejercicio Práctico

Escribe un archivo `temporizador.js` con dos mensajes `console.log` inmediatos y un `setTimeout` de 2000 ms en el medio para experimentar el comportamiento asíncrono.
