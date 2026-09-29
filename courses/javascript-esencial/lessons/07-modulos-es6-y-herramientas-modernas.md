# 7. Modulos ESM (import/export) y Proyecto Integrador

En esta leccion final de JavaScript Moderno exploraras la arquitectura de **Modulos ECMAScript (ESM)**, el estandar oficial para encapsular, reutilizar y estructurar proyectos de gran escala, y consolidaras el **Proyecto Integrador** del curso.

---

## Objetivos de la Leccion
- Comprender el estandar oficial de modulos ESM frente a formatos legados (CommonJS).
- Dominar exportaciones e importaciones nombradas (`export`) y por defecto (`export default`).
- Configurar soporte nativo de modulos en el navegador y en Node.js.
- Desarrollar la libreria modular del Proyecto Final Integrador.

---

## Modulos ECMAScript (ESM)

Un modulo es un archivo JavaScript aislado que se ejecuta en su propio ambito lexico estricto (`"use strict"` activado por defecto) y expone unicamente aquellos identificadores designados explicitamente mediante `export`.

### 1. Exportaciones Nombradas
Permiten exportar multiples funciones, clases o constantes desde un mismo archivo:
```javascript
// lib/calculo.js
export const TASA_BASE = 0.12;

export function calcularInteres(monto, meses) {
    return monto * TASA_BASE * (meses / 12);
}

export class GestorFinanzas {
    // Definicion de la clase
}
```

```javascript
// app.js
import { TASA_BASE, calcularInteres } from './lib/calculo.js';

console.log(`Tasa base: ${TASA_BASE}`);
```

### 2. Exportacion por Defecto (Default Export)
Representa la entidad principal que representa el modulo:
```javascript
// services/ClienteHTTP.js
export default class ClienteHTTP {
    async get(url) {
        const res = await fetch(url);
        return res.json();
    }
}
```

```javascript
// app.js
import ClienteHTTP from './services/ClienteHTTP.js';
```

---

## Configuracion de ESM en Navegadores y Node.js

### En HTML5 (Navegador)
El elemento `<script>` requiere el atributo `type="module"`:
```html
<script type="module" src="./src/index.js"></script>
```

### En Node.js (`package.json`)
Declara la clave `"type": "module"` en la raiz de tu `package.json` para permitir la sintaxis `import/export` en archivos `.js`:
```json
{
  "name": "eduxp-js-moderno",
  "type": "module"
}
```

---

## Proyecto Final Integrador: Motor de Pipeline Asincrono de Datos

El siguiente modulo completo en JavaScript ES2024+ demuestra la integracion de clases, metodos funcionales inmutables, asincronia robusta y arquitectura ESM:

```javascript
// src/services/TransformadorPipeline.js
export class TransformadorPipeline {
    #filtros = [];
    #transformadores = [];

    anadirFiltro(predicado) {
        this.#filtros.push(predicado);
        return this; // Permite patron Fluent API
    }

    anadirMapeo(transformacion) {
        this.#transformadores.push(transformacion);
        return this;
    }

    procesarColeccion(coleccion = []) {
        // Filtrado inmutable encadenado
        const datosFiltrados = coleccion.filter(item => 
            this.#filtros.every(filtro => filtro(item))
        );

        // Mapeo transformador encadenado
        return datosFiltrados.map(item => 
            this.#transformadores.reduce((acc, fn) => fn(acc), item)
        );
    }
}

export const servicioDatosRemotos = {
    async obtenerTransacciones() {
        return new Promise((resolve) => {
            setTimeout(() => {
                resolve([
                    { id: "T101", concepto: "Servidores Cloud", monto: 1200, activo: true },
                    { id: "T102", concepto: "Licencia Base Datos", monto: 450, activo: false },
                    { id: "T103", concepto: "Servicio Backup", monto: 310, activo: true },
                    { id: "T104", concepto: "Balanceador Carga", monto: 800, activo: true }
                ]);
            }, 800);
        });
    }
};
```

```javascript
// src/index.js
import { TransformadorPipeline, servicioDatosRemotos } from './services/TransformadorPipeline.js';

async function ejecutarApp() {
    console.log("=== EJECUTANDO MOTOR DE PIPELINE ASINCRONO ES2024+ ===");
    
    try {
        const datosBrutos = await servicioDatosRemotos.obtenerTransacciones();
        console.log(`Transacciones recuperadas de la fuente: ${datosBrutos.length}`);

        const pipeline = new TransformadorPipeline();
        
        // Configuracion declarativa de filtros y transformaciones
        pipeline
            .anadirFiltro(t => t.activo === true)
            .anadirFiltro(t => t.monto >= 400)
            .anadirMapeo(t => ({
                identificador: t.id,
                detalle: t.concepto.toUpperCase(),
                costoUSD: t.monto,
                costoConIVA: Number((t.monto * 1.16).toFixed(2))
            }));

        const resultados = pipeline.procesarColeccion(datosBrutos);
        
        console.log("Resultados procesados mediante pipeline inmutable:");
        console.table(resultados);

    } catch (err) {
        console.error("Fallo critico en la ejecucion del pipeline:", err.message);
    }
}

ejecutarApp();
```

---

## Conclusiones del Curso
Has completado el curso **JavaScript Moderno ES2024+: Fundamentos y Motor de Ejecucion**. Ya posees el dominio tecnico de la sintaxis contemporanea, la asincronia no bloqueante y la modularizacion profesional para construir aplicaciones web de alto rendimiento.
