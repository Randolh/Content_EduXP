# Lección 1: Introducción a Node.js y la Arquitectura No Bloqueante

¡Bienvenido al inicio de tu camino en el desarrollo backend con **Node.js**! En esta lección comprenderás qué es Node.js, cómo preparar tu entorno de desarrollo, cómo instalarlo en cualquier sistema operativo y cómo su modelo de Entradas/Salidas (I/O) no bloqueante impulsado por el **Event Loop** le permite procesar miles de peticiones simultáneas con alto rendimiento.

---

## 1. ¿Qué es Node.js?

Node.js es un entorno de ejecución de JavaScript de código abierto y multiplataforma construido sobre el motor **V8 de Google Chrome**. Fue creado por Ryan Dahl en 2009 para resolver el problema de la concurrencia en servidores tradicionales.

A diferencia de entornos multitarea tradicionales (como PHP con Apache o Java con Tomcat) que crean un hilo de ejecución por cada petición de usuario, Node.js utiliza un **único hilo principal** (Single Thread) apoyado por un bucle de eventos (**Event Loop**) asíncrono.

```text
[ Cliente HTTP 1 ] ──┐
[ Cliente HTTP 2 ] ──┼──► [ Event Loop (Hilo Único) ] ──► [ Worker Pool / Sistema OS ]
[ Cliente HTTP 3 ] ──┘                                        (Operaciones pesadas/DB)
```

> [!NOTE]
> Node.js **no es un lenguaje de programación ni un framework**, es un entorno de ejecución (Runtime) que permite correr JavaScript directamente en tu sistema operativo (servidores, computadores personales, IoT).

---

## 2. Instalación de Node.js y Preparación del Entorno

Antes de comenzar a programar, debes instalar Node.js y preparar tu editor de código.

### A. Descarga e Instalación

1. **Windows y macOS:**
   * Visita la página oficial [nodejs.org](https://nodejs.org).
   * Descarga la versión **LTS (Long Term Support)** recomendada para la mayoría de usuarios.
   * Ejecuta el instalador siguiendo los pasos predeterminados.

2. **Linux (Ubuntu/Debian):**
   ```bash
   # Actualizar índices de paquetes e instalar Node.js y NPM
   sudo apt update
   sudo apt install -y nodejs npm
   ```

3. **Uso de NVM (Node Version Manager) - Recomendado para desarrolladores:**
   ```bash
   # Instalar NVM en macOS/Linux
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
   
   # Instalar y activar la versión LTS más reciente
   nvm install --lts
   nvm use --lts
   ```

### B. Verificación de la Instalación

Abre tu terminal (PowerShell, Git Bash o Consola de Linux/macOS) y ejecuta los siguientes comandos para verificar la instalación:

```bash
# Verificar versión de Node.js (debe ser v18.x o superior)
node -v

# Verificar versión del gestor de paquetes NPM
npm -v
```

### C. Editor de Código Recomendado (Visual Studio Code)

Se recomienda utilizar **Visual Studio Code (VS Code)** con las siguientes extensiones recomendadas:
* **ESLint:** Detección de errores de código en tiempo real.
* **Prettier:** Formateo automático de código.
* **JavaScript (ES6) code snippets:** Atajos para acelerar la escritura de código.

---

## 3. Bloqueante (Síncrono) vs No Bloqueante (Asíncrono)

En la programación **síncrona (bloqueante)**, la ejecución del código se detiene en cada operación pesada (como leer un archivo del disco o consultar una base de datos) hasta obtener una respuesta.

En la programación **asíncrona (no bloqueante)**, Node.js delega la tarea pesada al sistema operativo y continúa inmediatamente procesando otras líneas de código o atendiendo a nuevos usuarios.

### Ejemplo de Código Asíncrono en JavaScript:

```javascript
console.log('1. Inicio del proceso');

// Operación asíncrona simulada con temporizador
setTimeout(() => {
  console.log('2. Operación asíncrona completada (Callback)');
}, 2000);

console.log('3. Fin del script principal');
```

**Salida en consola:**
```text
1. Inicio del proceso
3. Fin del script principal
2. Operación asíncrona completada (Callback)
```

> [!TIP]
> Observa cómo la instrucción 3 se ejecuta antes que la instrucción 2. Mientras el temporizador esperaba 2 segundos, el hilo principal no se congeló y continuó la ejecución.

---

## 4. ¿Cómo funciona el Event Loop?

El **Event Loop** supervisa constantemente la cola de tareas asíncronas (**Callback Queue**) y la pila de ejecución (**Call Stack**). Su regla de oro es:

1. Si la pila de ejecución está vacía, toma el primer evento pendiente de la cola.
2. Envía la función asociada a la pila de ejecución para procesarla.
3. Repite el proceso indefinidamente mientras el programa siga en ejecución.

---

## Autoevaluación

> [!QUIZ]
> ¿Cuál es la versión recomendada de Node.js para descargar desde nodejs.org al configurar un entorno de producción o aprendizaje estable?
> - [ ] La versión Current (Con las últimas características experimentales).
> - [x] La versión LTS (Long Term Support), que garantiza estabilidad y soporte extendido.
> - [ ] No es necesario descargar Node.js, viene integrado en el navegador.
>
> **Explicación**: La versión LTS es la más estable y probada por la comunidad, ideal para evitar incompatibilidades en proyectos y cursos.

---

## Ejercicio Práctico: Experimentando la Asincronía

**Objetivo**: Verificar tu instalación ejecutando un script en JavaScript que demuestre la diferencia entre ejecución secuencial y operaciones asíncronas con `setTimeout`.

**Instrucciones**:
1. Crea un archivo llamado `asincronia.js`.
2. Simula una consulta a una base de datos que tarda 1.5 segundos en responder.
3. Imprime mensajes antes, durante y después del llamado asíncrono.
4. Ejecuta el archivo desde la consola con `node asincronia.js`.

<details class="exercise-solution">
<summary>Ver solución paso a paso</summary>

<div class="solution-content">

```javascript
// asincronia.js

function consultarBaseDeDatos() {
  console.log('⏳ Solicitando datos a la base de datos...');
  
  setTimeout(() => {
    console.log('✅ Datos recibidos: { usuario: "Alexis", rol: "Admin" }');
  }, 1500);
}

console.log('🚀 Servidor iniciado...');
consultarBaseDeDatos();
console.log('⚡ Servidor listo para recibir nuevas peticiones...');
```

**Ejecución en consola**:
```bash
node asincronia.js
```

**Explicación**: El mensaje de "Servidor listo..." aparece inmediatamente después de iniciar la consulta a la base de datos, demostrando que Node.js no se bloquea esperando la respuesta de 1.5 segundos.

</div>
</details>

---

## Resumen

- Node.js requiere instalar el entorno de ejecución desde **nodejs.org** o mediante **NVM**.
- Se verifica la instalación mediante los comandos `node -v` y `npm -v`.
- Node.js ejecuta JavaScript fuera del navegador mediante el motor **V8** con arquitectura de **hilo único e I/O no bloqueante**.
- En la siguiente lección aprenderás sobre el sistema de módulos moderno (**ES Modules**) y el gestor de paquetes **NPM**.
