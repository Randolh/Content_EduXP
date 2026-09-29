# 6. Programacion Orientada a Objetos (POO) y Dataclasses

La Programacion Orientada a Objetos (POO) es un paradigma de desarrollo centrado en estructurar software en torno a entidades coherentes que encapsulan estado (atributos) y comportamiento (metodos). En esta leccion exploraras el estandar contemporaneo en Python.

---

## Objetivos de la Leccion
- Comprender clases, instancias, el metodo constructor `__init__` y el puntero `self`.
- Aplicar encapsulamiento mediante convenciones de visibilidad protegida y privada.
- Definir interfaces de acceso mediante `@property` y `@setter`.
- Implementar metodos magicos (Dunder Methods) como `__str__` y `__repr__`.
- Simplificar modelos de datos utilizando `@dataclass` (PEP 557).

---

## Estructura de una Clase Formal

```python
class ServidorCloud:
    """Representa una instancia de maquina virtual en un proveedor cloud."""
    
    # Atributo de clase (compartido por todas las instancias)
    proveedor: str = "EduXP Cloud Engine"

    def __init__(self, hostname: str, ram_gb: int, vcpus: int) -> None:
        # Atributos de instancia (propios de cada objeto creado)
        self.hostname: str = hostname
        self.ram_gb: int = ram_gb
        self.vcpus: int = vcpus
        self._encendido: bool = False  # Atributo protegido

    def iniciar(self) -> None:
        if not self._encendido:
            self._encendido = True
            print(f"Servidor {self.hostname} encendido con exito.")

    def detener(self) -> None:
        if self._encendido:
            self._encendido = False
            print(f"Servidor {self.hostname} detenido.")

    def __str__(self) -> str:
        estado = "Activo" if self._encendido else "Detenido"
        return f"Host: {self.hostname} ({self.vcpus} vCPUs, {self.ram_gb}GB RAM) - Estado: {estado}"
```

---

## Encapsulamiento con `@property`

En lugar de crear metodos tradicionales `get_saldo()` o `set_saldo()` al estilo Java, Python utiliza el decorador `@property` para exponer atributos con validaciones manteniendo una sintaxis limpia de acceso directo:

```python
class CuentaBancaria:
    def __init__(self, titular: str, saldo_inicial: float) -> None:
        self.titular: str = titular
        self._saldo: float = 0.0
        self.saldo = saldo_inicial  # Invoca al setter

    @property
    def saldo(self) -> float:
        """Getter de lectura controlada."""
        return self._saldo

    @saldo.setter
    def saldo(self, nuevo_monto: float) -> None:
        """Setter con validacion de integridad."""
        if nuevo_monto < 0:
            raise ValueError("El saldo contable no puede ser un valor negativo.")
        self._saldo = nuevo_monto

cuenta = CuentaBancaria("Alejandro Sanchez", 1500.0)
print(f"Saldo actual: ${cuenta.saldo:,.2f}")
cuenta.saldo = 2400.0 # Valida y asigna
```

---

## Modelado Conciso con `@dataclass`

El modulo estandar `dataclasses` (introducido en Python 3.7) genera automaticamente metodos repetitivos como `__init__()`, `__repr__()` y `__eq__()` a partir de definiciones de tipo de atributos:

```python
from dataclasses import dataclass, field
from datetime import datetime

@dataclass
class TransaccionFinanciera:
    id_transaccion: str
    monto: float
    divisa: str = "USD"
    fecha: datetime = field(default_factory=datetime.now)
    aprobada: bool = False

    def procesar(self) -> None:
        if self.monto > 0:
            self.aprobada = True

tx1 = TransaccionFinanciera("TX-8801", 1250.75)
print(tx1)
# Salida automatica: TransaccionFinanciera(id_transaccion='TX-8801', monto=1250.75, divisa='USD', fecha=datetime.datetime(...), aprobada=False)
```

---

## Herencia y Polimorfismo

```python
@dataclass
class UsuarioSistema:
    username: str
    email: str

    def obtener_privilegios(self) -> list[str]:
        return ["lectura_basica"]

@dataclass
class AdministradorSistema(UsuarioSistema):
    departamento: str = "TI"

    # Sobrescritura polimorfica de metodo
    def obtener_privilegios(self) -> list[str]:
        return ["lectura_basica", "escritura", "gestion_usuarios", "auditoria"]
```

---

## Ejercicio Practico

Disena una jerarquia de clases orientada a objetos para un sistema de envios postales:
1. Una `@dataclass` base `Paquete` con atributos `codigo_rastreo`, `peso_kg` y `destino`.
2. Un metodo `calcular_tarifa()` que retorne `$10` base mas `$5` por cada kilogramo de peso.
3. Una subclase `PaqueteInternacional` que anada un atributo `pais_destino` y sobrescriba `calcular_tarifa()` aplicando un arancel adicional del 25% sobre el total.
