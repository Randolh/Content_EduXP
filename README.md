# EduXP Content Repository

Repositorio oficial de contenidos educativos y catálogo maestro de cursos para la plataforma **EduXP**. Este repositorio contiene las lecciones en Markdown, la configuración estructurada de cada curso y el índice principal consumido dinámicamente por la plataforma web.

---

## Estructura del Repositorio

```text
Content_EduXP_git/
├── README.md                      # Documentación principal del repositorio
├── courses.json                   # Registro maestro del catálogo de cursos
├── CURSO_SPEC.md                  # Especificación técnica del estándar EduXP Spec v1.0
├── GUIA_CREACION_CURSOS.md        # Guía paso a paso para creadores de cursos
└── courses/                       # Contenido individual de los cursos
    ├── nodejs-esencial/           # Curso: Node.js Fundamentos
    │   ├── course.json            # Manifiesto y temario del curso
    │   └── lessons/               # Lecciones en formato Markdown (.md)
    ├── express-api-rest/          # Curso: Creación de APIs REST con Express
    │   ├── course.json
    │   └── lessons/
    └── react-esencial/            # Curso: React Esencial con Vite
        ├── course.json
        └── lessons/
```

---

## Catálogo de Cursos Disponibles

El archivo maestro [`courses.json`](file:///home/randolh/Documents/Content_EduXP_git/courses.json) define el catálogo visible en la plataforma. A continuación se detalla la oferta académica actual en la carpeta [`courses/`](file:///home/randolh/Documents/Content_EduXP_git/courses):

### 1. Node.js Fundamentos: JavaScript en el Servidor
* **ID / Slug:** `nodejs-esencial`
* **Categoría:** `backend` | **Nivel:** `Principiante` | **Duración:** `3 Horas` | **Lecciones:** `4`
* **Tecnologías:** `Node.js`, `JavaScript`, `NPM`, `Event Loop`, `CLI`
* **Proyecto Integrador:** Analizador de Archivos y Generador de Reportes CLI
* **Directorio:** [`courses/nodejs-esencial`](file:///home/randolh/Documents/Content_EduXP_git/courses/nodejs-esencial)
* **Lecciones:**
  1. [`01-introduccion-y-event-loop.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/nodejs-esencial/lessons/01-introduccion-y-event-loop.md)
  2. [`02-modulos-es6-y-npm.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/nodejs-esencial/lessons/02-modulos-es6-y-npm.md)
  3. [`03-sistema-de-archivos-fs-path.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/nodejs-esencial/lessons/03-sistema-de-archivos-fs-path.md)
  4. [`04-variables-entorno-y-cli.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/nodejs-esencial/lessons/04-variables-entorno-y-cli.md)

---

### 2. Creación de APIs REST con Express y Bases de Datos
* **ID / Slug:** `express-api-rest`
* **Categoría:** `api` | **Nivel:** `Intermedio` | **Duración:** `5 Horas` | **Lecciones:** `5`
* **Tecnologías:** `Express`, `API REST`, `Node.js`, `Zod`, `JWT`, `Bcrypt`, `MySQL`, `SQLite`
* **Proyecto Integrador:** API RESTful Profesional de Gestión y Autenticación de Usuarios
* **Directorio:** [`courses/express-api-rest`](file:///home/randolh/Documents/Content_EduXP_git/courses/express-api-rest)
* **Lecciones:**
  1. [`01-fundamentos-express-y-middlewares.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/express-api-rest/lessons/01-fundamentos-express-y-middlewares.md)
  2. [`02-arquitectura-modular-en-capas.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/express-api-rest/lessons/02-arquitectura-modular-en-capas.md)
  3. [`03-validacion-de-datos-con-zod.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/express-api-rest/lessons/03-validacion-de-datos-con-zod.md)
  4. [`04-persistencia-con-bases-de-datos.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/express-api-rest/lessons/04-persistencia-con-bases-de-datos.md)
  5. [`05-autenticacion-jwt-bcrypt-y-rbac.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/express-api-rest/lessons/05-autenticacion-jwt-bcrypt-y-rbac.md)

---

### 3. React Esencial: Desarrollo Frontend Moderno con Vite
* **ID / Slug:** `react-esencial`
* **Categoría:** `frontend` | **Nivel:** `Principiante - Intermedio` | **Duración:** `6 Horas` | **Lecciones:** `6`
* **Tecnologías:** `React`, `Vite`, `JavaScript`, `JSX`, `Hooks`, `Context API`
* **Proyecto Integrador:** Aplicación Web Fullstack e-Commerce con Carrito y Autenticación
* **Directorio:** [`courses/react-esencial`](file:///home/randolh/Documents/Content_EduXP_git/courses/react-esencial)
* **Lecciones:**
  1. [`01-introduccion-react-vite-y-jsx.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/react-esencial/lessons/01-introduccion-react-vite-y-jsx.md)
  2. [`02-componentes-props-y-usestate.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/react-esencial/lessons/02-componentes-props-y-usestate.md)
  3. [`03-useeffect-y-consumo-de-apis-rest.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/react-esencial/lessons/03-useeffect-y-consumo-de-apis-rest.md)
  4. [`04-componentes-ui-y-formularios.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/react-esencial/lessons/04-componentes-ui-y-formularios.md)
  5. [`05-estado-global-con-usecontext.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/react-esencial/lessons/05-estado-global-con-usecontext.md)
  6. [`06-autenticacion-y-integracion-fullstack.md`](file:///home/randolh/Documents/Content_EduXP_git/courses/react-esencial/lessons/06-autenticacion-y-integracion-fullstack.md)

---

## Especificaciones Técnicas y Documentación

Para obtener más detalles sobre el estándar de estructuración e integración con EduXP, puedes consultar las siguientes guías del repositorio:

* **Especificación Técnica (EduXP Spec v1.0):** [`CURSO_SPEC.md`](file:///home/randolh/Documents/Content_EduXP_git/CURSO_SPEC.md)
  * Esquemas JSON de `courses.json` y `course.json`.
  * Reglas para metadatos, lecciones en Markdown e integración frontend.
* **Guía para Creadores de Cursos:** [`GUIA_CREACION_CURSOS.md`](file:///home/randolh/Documents/Content_EduXP_git/GUIA_CREACION_CURSOS.md)
  * Instrucciones paso a paso para añadir nuevas lecciones y cursos al catálogo.

---

## Cómo Añadir un Nuevo Curso

1. **Crear el directorio del curso:** Crea una nueva carpeta en `courses/<slug-del-curso>/`.
2. **Definir el manifiesto:** Crea `courses/<slug-del-curso>/course.json` especificando el título, descripción, autor y la lista de lecciones.
3. **Escribir las lecciones:** Añade los archivos Markdown dentro de `courses/<slug-del-curso>/lessons/`.
4. **Actualizar el registro maestro:** Añade los metadatos del nuevo curso a [`courses.json`](file:///home/randolh/Documents/Content_EduXP_git/courses.json).
