# 3. Limites del Enfoque por Capas en Proyectos Medianos y Grandes

Aunque la Arquitectura por Capas representa un avance gigantesco frente a no tener estructura, en aplicaciones medianas y grandes (mas de 20-30 entidades y multiples desarrolladores) comienza a exhibir **fricciones estructurales severas**. En esta leccion exploraras por que y cuando este enfoque empieza a fallar.

---

## Objetivos de la Leccion
- Analizar el antipatron conocido como **Shotgun Surgery** (Cirugia de Escopeta).
- Identificar cuellos de botella de mantenimiento en directorios masivos horizontales.
- Evaluar el impacto del enfoque por capas en la colaboracion de equipos multidisciplinarios.
- Comprender por que la transicion a microservicios se complica bajo una estructura estrictamente por capas.

---

## El Fenomeno "Shotgun Surgery"

En diseno de software, **Shotgun Surgery** ocurre cuando una modificacion puntual sobre una sola funcionalidad de negocio obliga al desarrollador a tocar una gran cantidad de archivos distribuidos a lo largo y ancho de todo el arbol del proyecto:

```text
Agregar un solo campo a "Pagos" en Arquitectura por Capas:
Modificacion requerida:
  ├── src/routes/payments.routes.js        <-- Archivo 1
  ├── src/controllers/payments.controller.js <-- Archivo 2
  ├── src/services/payments.service.js     <-- Archivo 3
  ├── src/repositories/payments.repository.js <-- Archivo 4
  └── src/models/payment.model.js          <-- Archivo 5
```

En lugar de trabajar en un unico lugar cohesivo, el desarrollador salta constantemente entre 5 directorios diferentes (`/routes`, `/controllers`, `/services`, `/repositories`, `/models`). Conforme la aplicacion crece a 50 tablas, cada carpeta contiene decenas de ficheros que no guardan relacion entre si mas alla de su clasificacion tecnica.

---

## Problemas de Escalabilidad del Enfoque por Capas

### 1. Baja Cohesion Espacial
La carpeta `src/controllers/` almacena simultaneamente `auth.controller.js`, `cart.controller.js`, `shipping.controller.js`, `billing.controller.js`. Estos archivos no tienen nada que ver conceptualmente entre si; simplemente comparten la caracteristica tecnica de recibir `req` y `res`. Los elementos que cambian juntos no estan agrupados juntos.

### 2. Conflictos de Fusion en Git (Merge Conflicts)
En equipos de desarrollo donde 5 o 10 ingenieros trabajan en paralelo:
- El Desarrollador A trabaja en la funcionalidad de `Usuarios`.
- El Desarrollador B trabaja en la funcionalidad de `Facturas`.
- Ambos deben registrar sus endpoints en un archivo central compartido `src/routes/index.js` y en la configuracion global de modelos.  
El resultado son colisiones de merge recurrentes en los archivos centrales de coordinacion.

### 3. Falsa Sensacion de Desacoplamiento
A menudo los servicios de una capa comienzan a llamarse mutuamente de forma cruzada sin reglas claras:  
`OrderService` importa `UserService`, que a su vez importa `NotificationService`, que a su vez importa `OrderService`, provocando **dependencias circulares** que bloquean la inicializacion del interprete de Node.js.

---

## Comparativa de Escala

| Dimension de Analisis | Aplicacion Pequena (1-5 entidades) | Aplicacion Mediana/Grande (20+ entidades) |
| :--- | :--- | :--- |
| **Navegacion en el Editor** | Agil y comoda. | Difusa; carpetas con decenas de archivos dispersos. |
| **Incorporacion (Onboarding) de Desarrolladores** | Inmediata (patron clasico facil de entender). | Lenta; el desarrollador debe mapear todo el arbol para entender una sola funcionalidad. |
| **Impacto de Eliminar una Caracteristica** | Bajo. | Alto riesgo; borrar una funcion exige cazar archivos en 5 o 6 directorios. |
| **Transicion a Microservicios** | Rara vez necesaria. | Sumamente costosa; los componentes de un dominio estan desmembrados horizontalmente. |

> [!WARNING]
> Si la carpeta `/services` de tu proyecto Express tiene mas de 25 archivos y los desarrolladores necesitan abrir 6 pestañas en VS Code en extremos opuestos del proyecto para alterar una sola regla comercial, tu arquitectura por capas ha alcanzado su techo de escalabilidad.

---

## Ejercicio de Reflexion

Imagina que tu empresa decide extraer el subsistema de `Facturacion` de tu API monolitica para convertirlo en un microservicio independiente:
- ¿Que tan facil seria extraerlo si todos los archivos de Facturacion estan dispersos en `routes/`, `controllers/`, `services/`, `models/` y `validators/`?
- ¿Que cambiaria si todo el subsistema residiera en una carpeta autonoma `src/modules/invoicing/`?
