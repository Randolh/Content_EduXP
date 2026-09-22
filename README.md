# EduXP Content Repository

Repositorio oficial de contenidos educativos y catálogo maestro de cursos para la plataforma **EduXP**. Este repositorio contiene las lecciones en Markdown diseñadas con una metodología paso a paso para principiantes (un concepto práctico por lección), la configuración estructurada de cada curso y el índice principal consumido dinámicamente por la plataforma web.

---

## Estructura del Repositorio

```text
Content_EduXP_git/
├── README.md                      # Documentación principal del repositorio
├── courses.json                   # Registro maestro del catálogo de cursos
└── courses/                       # Contenido individual de los cursos
    ├── nodejs-esencial/           # Curso: Node.js Fundamentos Paso a Paso (7 lecciones)
    │   ├── course.json            # Manifiesto y temario del curso
    │   └── lessons/               # Lecciones en formato Markdown (.md)
    ├── express-api-rest/          # Curso: APIs REST con Express Paso a Paso (8 lecciones)
    │   ├── course.json
    │   └── lessons/
    ├── react-esencial/            # Curso: React Esencial Paso a Paso con Vite (8 lecciones)
    │   ├── course.json
    │   └── lessons/
    ├── git-github-esencial/       # Curso: Git y GitHub Paso a Paso (8 lecciones)
    │   ├── course.json
    │   └── lessons/
    └── markdown-esencial/         # Curso: Markdown Esencial Paso a Paso (8 lecciones)
        ├── course.json
        └── lessons/
```

---

## Catálogo de Cursos Disponibles

El archivo maestro [`courses.json`](file:///home/randolh/Documents/Content_EduXP_git/courses.json) define el catálogo visible en la plataforma. A continuación se detalla la oferta académica adaptada para principiantes en la carpeta [`courses/`](file:///home/randolh/Documents/Content_EduXP_git/courses):

### 1. Node.js Fundamentos Paso a Paso
* **ID / Slug:** `nodejs-esencial`
* **Categoría:** `backend` | **Nivel:** `Principiante` | **Duración:** `3 Horas` | **Lecciones:** `7`
* **Directorio:** [`courses/nodejs-esencial`](file:///home/randolh/Documents/Content_EduXP_git/courses/nodejs-esencial)
* **Lecciones:**
  1. [`01-que-es-nodejs.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/nodejs-esencial/lessons/01-que-es-nodejs.md)
  2. [`02-instalacion-y-primer-script.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/nodejs-esencial/lessons/02-instalacion-y-primer-script.md)
  3. [`03-event-loop-y-asincronia.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/nodejs-esencial/lessons/03-event-loop-y-asincronia.md)
  4. [`04-modulos-en-nodejs.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/nodejs-esencial/lessons/04-modulos-en-nodejs.md)
  5. [`05-npm-y-package-json.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/nodejs-esencial/lessons/05-npm-y-package-json.md)
  6. [`06-sistema-de-archivos-fs.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/nodejs-esencial/lessons/06-sistema-de-archivos-fs.md)
  7. [`07-variables-entorno-dotenv.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/nodejs-esencial/lessons/07-variables-entorno-dotenv.md)

---

### 2. APIs REST con Express Paso a Paso
* **ID / Slug:** `express-api-rest`
* **Categoría:** `api` | **Nivel:** `Principiante` | **Duración:** `4 Horas` | **Lecciones:** `8`
* **Directorio:** [`courses/express-api-rest`](file:///home/randolh/Documents/Content_EduXP_git/courses/express-api-rest)
* **Lecciones:**
  1. [`01-que-es-express.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/express-api-rest/lessons/01-que-es-express.md)
  2. [`02-servidor-basico.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/express-api-rest/lessons/02-servidor-basico.md)
  3. [`03-clientes-http-pruebas.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/express-api-rest/lessons/03-clientes-http-pruebas.md)
  4. [`04-metodos-http.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/express-api-rest/lessons/04-metodos-http.md)
  5. [`05-parametros-de-ruta.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/express-api-rest/lessons/05-parametros-de-ruta.md)
  6. [`06-procesar-datos-json.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/express-api-rest/lessons/06-procesar-datos-json.md)
  7. [`07-que-es-un-middleware.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/express-api-rest/lessons/07-que-es-un-middleware.md)
  8. [`08-rutas-y-controladores.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/express-api-rest/lessons/08-rutas-y-controladores.md)

---

### 3. React Esencial Paso a Paso con Vite
* **ID / Slug:** `react-esencial`
* **Categoría:** `frontend` | **Nivel:** `Principiante` | **Duración:** `5 Horas` | **Lecciones:** `8`
* **Directorio:** [`courses/react-esencial`](file:///home/randolh/Documents/Content_EduXP_git/courses/react-esencial)
* **Lecciones:**
  1. [`01-que-es-react.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/react-esencial/lessons/01-que-es-react.md)
  2. [`02-crear-proyecto-vite.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/react-esencial/lessons/02-crear-proyecto-vite.md)
  3. [`03-sintaxis-jsx.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/react-esencial/lessons/03-sintaxis-jsx.md)
  4. [`04-primer-componente.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/react-esencial/lessons/04-primer-componente.md)
  5. [`05-propiedades-props.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/react-esencial/lessons/05-propiedades-props.md)
  6. [`06-estado-con-usestate.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/react-esencial/lessons/06-estado-con-usestate.md)
  7. [`07-eventos-en-react.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/react-esencial/lessons/07-eventos-en-react.md)
  8. [`08-efectos-con-useeffect.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/react-esencial/lessons/08-efectos-con-useeffect.md)

---

### 4. Git y GitHub: Paso a Paso para Principiantes
* **ID / Slug:** `git-github-esencial`
* **Categoría:** `tools` | **Nivel:** `Principiante` | **Duración:** `4 Horas` | **Lecciones:** `8`
* **Directorio:** [`courses/git-github-esencial`](file:///home/randolh/Documents/Content_EduXP_git/courses/git-github-esencial)
* **Lecciones:**
  1. [`01-que-es-git.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/git-github-esencial/lessons/01-que-es-git.md)
  2. [`02-instalacion-y-configuracion.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/git-github-esencial/lessons/02-instalacion-y-configuracion.md)
  3. [`03-primer-repositorio-y-commits.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/git-github-esencial/lessons/03-primer-repositorio-y-commits.md)
  4. [`04-estado-y-diferencias.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/git-github-esencial/lessons/04-estado-y-diferencias.md)
  5. [`05-historial-de-cambios.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/git-github-esencial/lessons/05-historial-de-cambios.md)
  6. [`06-trabajar-con-ramas.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/git-github-esencial/lessons/06-trabajar-con-ramas.md)
  7. [`07-fusionar-ramas.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/git-github-esencial/lessons/07-fusionar-ramas.md)
  8. [`08-introduccion-a-github.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/git-github-esencial/lessons/08-introduccion-a-github.md)

---

### 5. Markdown Esencial: Documentación Paso a Paso
* **ID / Slug:** `markdown-esencial`
* **Categoría:** `tools` | **Nivel:** `Principiante` | **Duración:** `3 Horas` | **Lecciones:** `8`
* **Directorio:** [`courses/markdown-esencial`](file:///home/randolh/Documents/Content_EduXP_git/courses/markdown-esencial)
* **Lecciones:**
  1. [`01-introduccion-y-editores.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/markdown-esencial/lessons/01-introduccion-y-editores.md)
  2. [`02-encabezados-y-titulos.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/markdown-esencial/lessons/02-encabezados-y-titulos.md)
  3. [`03-formato-de-texto-negrita-cursiva.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/markdown-esencial/lessons/03-formato-de-texto-negrita-cursiva.md)
  4. [`04-listas-ordenadas-y-no-ordenadas.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/markdown-esencial/lessons/04-listas-ordenadas-y-no-ordenadas.md)
  5. [`05-enlaces-e-imagenes.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/markdown-esencial/lessons/05-enlaces-e-imagenes.md)
  6. [`06-bloques-de-codigo.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/markdown-esencial/lessons/06-bloques-de-codigo.md)
  7. [`07-tablas-y-alineacion.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/markdown-esencial/lessons/07-tablas-y-alineacion.md)
  8. [`08-readmes-profesionales.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/markdown-esencial/lessons/08-readmes-profesionales.md)

---

## Cómo Añadir un Nuevo Curso

1. **Crear el directorio del curso:** Crea una nueva carpeta en `courses/<slug-del-curso>/`.
2. **Definir el manifiesto:** Crea `courses/<slug-del-curso>/course.json` especificando el título, descripción, autor y la lista de lecciones.
3. **Escribir las lecciones:** Añade los archivos Markdown dentro de `courses/<slug-del-curso>/lessons/` siguiendo la regla de un solo concepto práctico por lección.
4. **Actualizar el registro maestro:** Añade los metadatos del nuevo curso a [`courses.json`](file:///home/randolh/Documents/Content_EduXP_git/courses.json).
