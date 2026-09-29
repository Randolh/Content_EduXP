# 2. Tipos de Datos, Modificadores, Operadores y f-strings

Python posee un sistema de tipado dinamico, fuerte y reflexivo. Esto significa que las variables no requieren una declaracion de tipo obligatoria para compilar, pero cada objeto en memoria conoce su tipo exacto y el interprete no permite conversiones invalidas o ambiguas en tiempo de ejecucion.

---

## Objetivos de la Leccion
- Dominar los tipos de datos primitivos nativos: `int`, `float`, `bool`, `str` y `NoneType`.
- Entender el concepto de inmutabilidad en los objetos primitivos de Python.
- Aplicar transformaciones explicitas de tipo (Casting).
- Utilizar f-strings modernas con formateo numerico, alineacion y depuracion inline.

---

## Tipos de Datos Primitivos e Inmutabilidad

En Python, **todo es un objeto**, incluyendo numeros y cadenas. Los tipos primitivos son **inmutables**: una vez instanciados en memoria, su valor no se puede mutar; reasignar una variable significa crear un nuevo objeto y apuntar la referencia a el.

```python
# 1. Enteros (int) de precision arbitraria (sin desbordamiento de buffer)
total_registros: int = 150000000000000000000

# 2. Decimales de punto flotante de 64 bits (float)
tasa_interes: float = 0.0575

# 3. Cadenas de caracteres inmutables (str) en Unicode
titulo_modulo: str = "Ingenieria de Software"

# 4. Logica Booleana (bool: subclase de int donde True == 1 y False == 0)
servicio_activo: bool = True

# 5. Ausencia formal de valor (NoneType)
resultado_consulta: None = None
```

Podemos inspeccionar la identidad unica del objeto en memoria con `id()` y su tipo con `type()`:
```python
x = 100
print(type(x))  # <class 'int'>
print(id(x))    # Direccion de memoria unica
```

---

## Conversion Explicita de Tipos (Type Casting)

La funcion `input()` captura datos de consola siempre como `str`. Para efectuar calculos aritmeticos, es obligatorio realizar el cast explicito:

```python
entrada_usuario = input("Ingrese el precio base: ")

# Casting seguro
try:
    precio_base = float(entrada_usuario)
    cantidad = int(input("Ingrese la cantidad: "))
    total = precio_base * cantidad
    print(f"Total calculado: {total}")
except ValueError as e:
    print(f"Error de conversion numerica: {e}")
```

---

## Interpolacion Avanzada con f-strings (Python 3.12+)

Las cadenas literales prefijadas con `f` (formato) evaluan expresiones dentro de llaves `{}` y permiten modificadores de formato de alto rendimiento:

### 1. Precision Decimal y Formateo Monetario
```python
subtotal = 145920.8492
iva = 0.16

# Limitar a dos cifras decimales con separador de miles por comas
print(f"Subtotal: ${subtotal:,.2f}")      # $145,920.85
print(f"IVA aplicado: {iva:.1%}")          # 16.0%
```

### 2. Alineacion y Relleno de Columnas
Ideal para formatear reportes tabulares de consola sin dependencias externas:
```python
producto_a = "Servidor Web"
producto_b = "Firewall"
precio_a = 1200.0
precio_b = 450.5

print(f"{producto_a:<20} | ${precio_a:>10.2f}")
print(f"{producto_b:<20} | ${precio_b:>10.2f}")
```

### 3. Autodepuracion con el Modificador `=`
Al anadir `=` tras la expresion, Python imprime el texto de la expresion y su valor evaluado:
```python
ancho = 50
alto = 20
print(f"{ancho=}, {alto=}, {ancho * alto=}")
# Salida: ancho=50, alto=20, ancho * alto=1000
```

---

## Operadores Aritmeticos y de Bits

| Operador | Denominacion | Ejemplo | Resultado |
| :--- | :--- | :--- | :--- |
| `+` | Adicion | `10 + 4` | `14` |
| `-` | Sustraccion | `10 - 4` | `6` |
| `*` | Multiplicacion | `10 * 4` | `40` |
| `/` | Division flotante | `10 / 4` | `2.5` |
| `//` | Division entera (trunca) | `10 // 4` | `2` |
| `%` | Modulo (resto entero) | `10 % 4` | `2` |
| `**` | Exponenciacion | `2 ** 8` | `256` |

---

## Ejercicio Practico

Crea un script llamado `calculo_amortizacion.py` que solicite:
- El capital inicial del prestamo (float).
- La tasa de interes anual en porcentaje (float).
- El plazo en anos (int).

El programa debe calcular el interes simple y el total acumulado a pagar, e imprimir un resumen alineado a la derecha con separador de miles y dos cifras decimales.
