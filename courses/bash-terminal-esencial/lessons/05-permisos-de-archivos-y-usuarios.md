# Lección 5: Permisos de Archivos y Usuarios (chmod, chown, sudo)

En esta lección aprenderás cómo funciona el sistema de seguridad y permisos de POSIX/Linux para controlar la lectura, escritura y ejecución de archivos.

---

## 1. Entendiendo la Estructura de Permisos (`ls -l`)

Al ejecutar `ls -l`, verás una cadena de 10 caracteres como `-rwxr-xr--`:

- El 1º carácter es el tipo (`-` archivo, `d` directorio).
- Los caracteres 2-4 son permisos del **Propietario (User - u)**.
- Los caracteres 5-7 son permisos del **Grupo (Group - g)**.
- Los caracteres 8-10 son permisos de **Otros usuarios (Others - o)**.

Tipos de permisos:
- `r` (Read / Lectura - valor octal 4)
- `w` (Write / Escritura - valor octal 2)
- `x` (Execute / Ejecución - valor octal 1)

---

## 2. Modificar Permisos con `chmod`

```bash
# Otorgar permiso de ejecución al propietario
chmod u+x script.sh

# Otorgar permiso de ejecución a todos los usuarios
chmod +x script.sh

# Notación Octal (755: rwx para usuario, r-x para grupo, r-x para otros)
chmod 755 script.sh

# Notación Octal (600: rw- solo para el propietario - ideal para llaves SSH privadas)
chmod 600 id_rsa
```

---

## 3. Superusuario (`sudo`) y Cambio de Propietario (`chown`)

- **`sudo` (SuperUser DO)**: Ejecuta un comando con privilegios de administrador (root).
- **`chown` (Change Owner)**: Cambia el usuario o grupo propietario de un archivo.

```bash
# Cambiar el propietario de un archivo
sudo chown usuario:grupo archivo.txt
```

---

## Autoevaluación

> [!QUIZ]
> ¿Qué representa el código octal `755` al ejecutar `chmod 755 mi_script.sh`?
> - [ ] Lectura para todos y nada más.
> - [x] El propietario tiene todos los permisos (`7` = r+w+x), mientras que el grupo y otros tienen lectura y ejecución (`5` = r+x).
> - [ ] Borra el archivo del sistema.
>
> **Explicación**: `7` representa 4(r) + 2(w) + 1(x) = 7. `5` representa 4(r) + 0(w) + 1(x) = 5.

---

## Ejercicio Práctico

Crea un archivo `script.sh`, consulta sus permisos iniciales con `ls -l script.sh` y agrégale permisos de ejecución con `chmod +x script.sh`.
