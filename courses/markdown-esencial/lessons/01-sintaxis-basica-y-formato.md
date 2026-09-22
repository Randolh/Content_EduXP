# Lección 1: Sintaxis Básica de Markdown: Encabezados, Listas, Enlaces e Imágenes

Bienvenido al curso de **Markdown Esencial**. Markdown es el lenguaje de marcado ligero más popular en la industria del software. Creado por John Gruber y Aaron Swartz en 2004, te permite escribir documentos con formato enriquecido utilizando texto plano fácil de leer y escribir.

---

## 1. Preparación del Entorno de Redacción y Herramientas

Aunque puedes redactar Markdown en cualquier bloc de notas, utilizar un entorno optimizado mejora enormemente la productividad y la visualización en tiempo real.

### A. Editores Recomendados

1. **Visual Studio Code (Gratuito y Recomendado):**
   * Editor estándar de la industria. Permite editar y visualizar Markdown simultáneamente en paneles divididos.
   * **Atajo para Vista Previa en VS Code:** `Ctrl + Shift + V` (Windows/Linux) o `Cmd + Shift + V` (macOS).
   * **Vista previa lado a lado:** `Ctrl + K V` o `Cmd + K V`.

2. **Editores WYSIWYG Dedicados:**
   * **Typora / MarkText / Obsidian:** Editores que renderizan la sintaxis visualmente a medida que escribes.

### B. Extensiones Recomendadas para VS Code

* **Markdown All in One:** Añade atajos de teclado (`Ctrl + B` para negrita, `Ctrl + I` para cursiva), tabla de contenidos automática y autocompletado.
* **Markdown Preview Enhanced:** Proporciona un visor de vista previa avanzado con soporte para matematicas KaTeX, diagramas e integración exportable a PDF/HTML.
* **markdownlint:** Valida las reglas de estilo y buenas prácticas de redacción semántica en tu documento.

---

## 2. Encabezados y Formato de Texto

### Encabezados (Headings)
Los encabezados se crean utilizando el símbolo de almohadilla (`#`). La cantidad de `#` determina el nivel semántico del encabezado (de `<h1>` a `<h6>`).

```markdown
# Encabezado Nivel 1 (Título Principal)
## Encabezado Nivel 2 (Sección principal)
### Encabezado Nivel 3 (Subsección)
#### Encabezado Nivel 4
```

### Formato de Texto (Énfasis)
Puedes aplicar estilos visuales a las palabras utilizando asteriscos (`*`) o guiones bajos (`_`):

* **Negrita:** `**texto en negrita**` o `__texto en negrita__`
* *Cursiva:* `*texto en cursiva*` o `_texto en cursiva_`
* ***Negrita y Cursiva:*** `***texto combinado***`
* ~~Tachado:~~ `~~texto tachado~~`

> [!NOTE]
> Procura dejar un espacio en blanco después de cada `#` en los encabezados para asegurar la compatibilidad con todos los analizadores de Markdown.

---

## 3. Listas Ordenadas y No Ordenadas

### Listas No Ordenadas (Viñetas)
Utiliza asteriscos (`*`), guiones (`-`) o signos más (`+`):

```markdown
* Elemento 1
* Elemento 2
  * Sub-elemento anidado (2 espacios de sangría)
  * Otro sub-elemento
```

### Listas Ordenadas (Numeradas)
Utiliza números seguidos de un punto:

```markdown
1. Primer paso
2. Segundo paso
3. Tercer paso
```

---

## 4. Enlaces e Imágenes

La sintaxis para enlaces e imágenes es muy similar. La clave está en los corchetes `[]` para el texto visible y los paréntesis `()` para la URL.

### Enlaces (Links)
`[Texto del enlace](https://direccion-web.com)`

Ejemplo:
`Visita la plataforma [EduXP](https://eduxp.com) para aprender tecnología.`

### Imágenes
`![Texto alternativo (alt)](https://direccion-imagen.com/foto.png)`

Ejemplo:
`![Logo de Markdown](https://markdown-here.com/img/icon256.png)`

> [!TIP]
> La diferencia entre un enlace y una imagen es el signo de exclamación `!` al inicio de la imagen.

---

## Autoevaluación

> [!QUIZ]
> ¿Cuál es el atajo de teclado en VS Code para abrir la vista previa de Markdown al lado de tu archivo de edición?
> - [ ] `Ctrl + Alt + Del`
> - [x] `Ctrl + K V` (o `Cmd + K V` en Mac)
> - [ ] `F5`
>
> **Explicación**: El comando de teclado `Ctrl + K V` abre un panel lateral adyacente que renderiza los cambios de Markdown en tiempo real mientras escribes.

---

## Ejercicio Práctico: Tu Primer Documento Markdown

**Objetivo**: Probar tu entorno de redacción y crear un archivo de presentación personal estructurado en Markdown.

**Instrucciones**:
1. Abre tu editor de código (VS Code) y abre la vista previa en paralelo.
2. Crea un archivo llamado `perfil.md`.
3. Añade un título principal (H1) con tu nombre.
4. Agrega una sección de biografía breve con texto en negrita y cursiva.
5. Crea una lista no ordenada de tus tecnologías favoritas.
6. Incluye un enlace a tu perfil de GitHub o sitio web.

<details class="exercise-solution">
<summary>Ver solución paso a paso</summary>

<div class="solution-content">

```markdown
# Perfil de Desarrollador: Ana Martínez

¡Hola! Soy **desarrolladora web Fullstack** apasionada por el *código limpio* y la *arquitectura de software*.

## Mis Tecnologías Favoritas:
* JavaScript / TypeScript
* React y Next.js
* Node.js y Express
* Git y GitHub

---

Puedes revisar mis proyectos en mi [Perfil de GitHub](https://github.com/anamartinez).
```

</div>
</details>
