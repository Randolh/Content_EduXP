# Lección 1: ¿Qué es HTML5 y la Estructura Base de un Documento?

¡Bienvenido al curso de **HTML5 Moderno y Semántico**! En esta primera lección aprenderás los fundamentos del lenguaje de marcado estándar de la web y cómo estructurar un archivo HTML5 profesional siguiendo la especificación **HTML Living Standard**.

---

## 1. ¿Qué es HTML5 y el HTML Living Standard?

**HTML** (*HyperText Markup Language*) es el lenguaje estándar utilizado para estructurar y dar significado al contenido de una página web (textos, imágenes, enlaces, formularios, etc.).

A diferencia de versiones antiguas (como HTML 4.01 o XHTML), hoy en día HTML evoluciona constantemente mediante el modelo **HTML Living Standard**, mantenido por la **WHATWG** (Web Hypertext Application Technology Working Group). Esto significa que no habrá un "HTML6", sino un estándar vivo en constante evolución.

---

## 2. La Estructura Base de un Documento HTML5

Todo documento HTML5 válido arranca con la siguiente plantilla mínima indispensable:

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mi Primera Página en HTML5</title>
</head>
<body>
  <h1>¡Hola, Mundo en HTML5!</h1>
  <p>Este es el cuerpo visible de mi sitio web.</p>
</body>
</html>
```

### Desglose de Elementos Clave:

1. `<!DOCTYPE html>`: Declara al navegador que se trata de un documento **HTML5**. Debe ir en la primera línea.
2. `<html lang="es">`: Elemento raíz. El atributo `lang="es"` especifica el idioma principal del contenido (esencial para accesibilidad y motores de búsqueda).
3. `<head>`: Contiene metadatos e instrucciones técnicas que **no se muestran directamente en la pantalla** (título de la pestaña, codificación, enlaces a estilos).
   - `<meta charset="UTF-8">`: Asegura la correcta interpretación de acentos, eñes y caracteres especiales (emojis).
   - `<meta name="viewport" content="width=device-width, initial-scale=1.0">`: Habilita el diseño responsivo en dispositivos móviles.
4. `<body>`: Contiene todo el contenido **visible** que los usuarios ven e interactúan en el navegador.

> [!NOTE]
> En HTML5, los nombres de las etiquetas deben escribirse siempre en **minúsculas** por convención y buena práctica profesional.

> [!TIP]
> En editores como VS Code, puedes generar la estructura básica escribiendo `!` y presionando `Tab` o `Enter`.

---

## Autoevaluación

> [!QUIZ]
> ¿Cuál es la función del elemento `<meta name="viewport" content="width=device-width, initial-scale=1.0">`?
> - [ ] Cambiar el color de fondo de la aplicación en dispositivos móviles.
> - [x] Adaptar el área visible del documento para un renderizado responsivo en pantallas móviles.
> - [ ] Definir el título que aparece en la pestaña del navegador web.
>
> **Explicación**: La meta etiqueta `viewport` le indica al navegador móvil que ajuste el ancho de la página al ancho de la pantalla del dispositivo.

---

## 🛠️ Ejercicio Práctico: Tu Primer Documento HTML5

**Objetivo**: Crear un archivo de documento HTML5 válido con metadatos de codificación y título personalizado.

**Instrucciones**:
1. Escribe la estructura completa de un archivo HTML5.
2. Configura el idioma en español (`es`) y la codificación de caracteres en `UTF-8`.
3. Asigna el título `"Perfil de Desarrollador - EduXP"`.
4. En el `<body>`, añade un encabezado principal con tu nombre y un párrafo corto sobre tus metas en el desarrollo web.

<details class="exercise-solution">
<summary>💡 Ver solución explicada paso a paso</summary>

<div class="solution-content">

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Perfil de Desarrollador - EduXP</title>
</head>
<body>
  <h1>Hola, soy Alex Pérez</h1>
  <p>Estoy aprendiendo HTML5 semántico para construir aplicaciones web accesibles y profesionales.</p>
</body>
</html>
```

**Explicación**: El archivo incluye la declaración `<!DOCTYPE html>`, la etiqueta `<html>` configurada en español, metadatos esenciales en `<head>` y el contenido visible en `<body>`.
</div>
</details>
