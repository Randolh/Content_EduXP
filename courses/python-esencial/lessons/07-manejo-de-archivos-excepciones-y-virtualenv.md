# 7. Excepciones, Persistencia JSON, venv y Proyecto Integrador

En esta leccion final de Python Moderno aprenderas a controlar fallos imprevistos mediante el sistema de **Excepciones**, guardar y cargar estructuras de datos en formato **JSON** utilizando gestores de contexto, administrar dependencias aisladas con **entornos virtuales (`venv`)** y consolidaras la aplicacion del **Proyecto Integrador**.

---

## Objetivos de la Leccion
- Implementar bloques de captura de errores con `try`, `except`, `else` y `finally`.
- Manipular rutas de forma agnostica con `pathlib.Path`.
- Leer y serializar datos estructurados mediante el modulo nativo `json`.
- Aislar entornos de librerias con `python -m venv` y gestionar `requirements.txt`.
- Construir la aplicacion CLI del Proyecto Final del curso.

---

## Control de Excepciones Profesional

Una excepcion es un objeto que representa una condicion anormal que interrumpe el flujo normal del programa:

```python
def dividir_valores(a: float, b: float) -> float:
    try:
        resultado = a / b
    except ZeroDivisionError:
        print("Error matematico: Division por cero no admitida.")
        raise
    except TypeError as e:
        print(f"Error de tipos incompatibles: {e}")
        return 0.0
    else:
        # Se ejecuta UNICAMENTE si NO hubo excepcion
        print("Operacion efectuada satisfactoriamente.")
        return resultado
    finally:
        # Se ejecuta SIEMPRE (ideal para cerrar descriptores de archivo o conexiones)
        print("Bloque de finalizacion ejecutado.")
```

---

## Persistencia con `pathlib` y `json`

La libreria `pathlib` proporciona una interfaz orientada a objetos para interactuar con el sistema de archivos independientemente de si el sistema operativo es Windows, Linux o macOS:

```python
import json
from pathlib import Path

# Definicion agnostica de ruta
ruta_archivo = Path("datos_almacen") / "inventario.json"
ruta_archivo.parent.mkdir(parents=True, exist_ok=True)

catalogo = [
    {"codigo": "SRV-01", "nombre": "Servidor Rack 1U", "precio": 2400.0, "stock": 4},
    {"codigo": "SW-24", "nombre": "Switch Gestionable 24P", "precio": 380.5, "stock": 15}
]

# Serializacion a JSON en disco con Context Manager (with)
with open(ruta_archivo, "w", encoding="utf-8") as f:
    json.dump(catalogo, f, indent=4, ensure_ascii=False)

# Deserializacion desde disco
if ruta_archivo.exists():
    with open(ruta_archivo, "r", encoding="utf-8") as f:
        datos_recuperados = json.load(f)
        print(f"Registros cargados desde el archivo: {len(datos_recuperados)}")
```

---

## Gestion de Entornos Virtuales (`venv`)

Un **entorno virtual** es un directorio aislado que contiene su propio binario ejecutable de Python y sus propias carpetas de librerias `site-packages`. Permite instalar dependencias sin requerir permisos de administrador (`root`) y previene colisiones de versiones entre distintos proyectos.

### 1. Creacion del Entorno Virtual
En la raiz de tu proyecto:
```bash
python -m venv .venv
```

### 2. Activacion del Entorno
- **Linux y macOS (Bash/Zsh):**
  ```bash
  source .venv/bin/activate
  ```
- **Windows (PowerShell):**
  ```powershell
  .\.venv\Scripts\Activate.ps1
  ```
El prompt de la terminal mostrara el prefijo `(.venv)`.

### 3. Registro y Replicacion de Dependencias
```bash
# Exportar librerias instaladas
pip freeze > requirements.txt

# Instalar librerias en otro entorno de trabajo
pip install -r requirements.txt
```

---

## Proyecto Final Integrador: PyManager CLI

A continuacion se presenta la implementacion completa del sistema modular de gestion de inventario que integra clases, dataclasses, persistencia JSON y match/case:

```python
# pymanager.py
import json
import sys
from dataclasses import dataclass, asdict
from pathlib import Path

@dataclass
class Articulo:
    codigo: str
    descripcion: str
    precio_unitario: float
    existencias: int

class InventarioManager:
    def __init__(self, ruta_archivo: str = "inventario_db.json") -> None:
        self.archivo: Path = Path(ruta_archivo)
        self.articulos: dict[str, Articulo] = self._cargar_datos()

    def _cargar_datos(self) -> dict[str, Articulo]:
        if not self.archivo.exists():
            return {}
        try:
            with open(self.archivo, "r", encoding="utf-8") as f:
                data = json.load(f)
                return {item["codigo"]: Articulo(**item) for item in data}
        except (json.JSONDecodeError, IOError) as err:
            print(f"Advertencia al leer base de datos: {err}")
            return {}

    def guardar_datos(self) -> None:
        lista_datos = [asdict(art) for art in self.articulos.values()]
        with open(self.archivo, "w", encoding="utf-8") as f:
            json.dump(lista_datos, f, indent=2, ensure_ascii=False)

    def registrar_articulo(self, art: Articulo) -> None:
        self.articulos[art.codigo] = art
        self.guardar_datos()
        print(f"Registro exitoso: {art.descripcion} ({art.codigo}) guardado.")

    def listar_inventario(self) -> None:
        if not self.articulos:
            print("El inventario actual no contiene registros.")
            return
        print(f"\n{'CODIGO':<10} | {'DESCRIPCION':<30} | {'PRECIO':>10} | {'STOCK':>6}")
        print("-" * 65)
        for a in self.articulos.values():
            print(f"{a.codigo:<10} | {a.descripcion:<30} | ${a.precio_unitario:>9.2f} | {a.existencias:>6}")

def main() -> None:
    gestor = InventarioManager()
    
    while True:
        print("\n=== SISTEMA PYMANAGER CLI ===")
        print("1. Listar articulos")
        print("2. Registrar nuevo articulo")
        print("3. Salir")
        
        opcion = input("Seleccione operacion [1-3]: ").strip()
        
        match opcion:
            case "1":
                gestor.listar_inventario()
            case "2":
                try:
                    cod = input("Codigo SKU: ").strip().upper()
                    desc = input("Descripcion: ").strip()
                    prec = float(input("Precio unitario: "))
                    stock = int(input("Existencias iniciales: "))
                    gestor.registrar_articulo(Articulo(cod, desc, prec, stock))
                except ValueError:
                    print("Error: Los valores de precio y existencias deben ser numericos.")
            case "3":
                print("Cerrando aplicacion de inventario.")
                sys.exit(0)
            case _:
                print("Opcion invalida. Intente nuevamente.")

if __name__ == "__main__":
    main()
```

---

## Conclusiones del Curso
Has completado el curso **Python 3.12+ Moderno: De Cero a Desarrollo Profesional**. Ya dominas la sintaxis actual, el control de errores, la persistencia en disco y los estandares de desarrollo backend.
