# Lección 13: Seguridad de Credenciales con Hashing (bcryptjs)

En esta lección aprenderás por qué **nunca se deben almacenar contraseñas en texto plano** y cómo aplicar algoritmos de hashing unidireccionales con la librería `bcryptjs`.

---

## 1. ¿Qué es Hashing y por qué no es lo mismo que Encriptación?

- **Encriptación (Bidireccional)**: Transforma un texto usando una clave y se puede desencriptar para obtener el texto original.
- **Hashing (Unidireccional)**: Transforma un texto en una cadena irreversible (hash). No existe un método para "des-hashear" la contraseña. Para verificarla, se calcula el hash del intento del usuario y se compara con el hash almacenado.

---

## 2. Uso de `bcryptjs` en Express

Instalamos con `npm install bcryptjs`.

```javascript
import bcrypt from 'bcryptjs';

// 1. Crear el Hash al Registrar un Usuario
async function registrarUsuario(passwordEnTextoPlano) {
  const saltRounds = 10; // Número de rondas de complejidad (Salt)
  const passwordHash = await bcrypt.hash(passwordEnTextoPlano, saltRounds);
  
  console.log('Password original:', passwordEnTextoPlano);
  console.log('Password Hash guardado en BD:', passwordHash);
  return passwordHash;
}

// 2. Verificar la Contraseña al Iniciar Sesión (Login)
async function verificarLogin(passwordIngresada, passwordHashBD) {
  // Compara el texto plano con el hash guardado de forma segura
  const esCorrecta = await bcrypt.compare(passwordIngresada, passwordHashBD);
  return esCorrecta; // Retorna true o false
}
```

---

## Autoevaluación

> [!QUIZ]
> ¿Por qué es fundamental usar una "Sal" (`salt`) al generar un hash de contraseña con `bcrypt`?
> - [ ] Para comprimir el tamaño de la contraseña.
> - [x] Para asegurar que dos usuarios con la misma contraseña tengan hashes completamente diferentes, protegiendo contra ataques de Tablas Arcoíris (Rainbow Tables).
> - [ ] Para acelerar la velocidad del servidor.
>
> **Explicación**: El `salt` agrega una secuencia aleatoria antes del proceso de hash, evitando que contraseñas idénticas generen hashes iguales.

---

## Ejercicio Práctico

Escribe una función de autenticación `validarCredenciales(inputPass, dbPassHash)` que use `bcrypt.compare` y devuelva un mensaje de éxito o error.
