# Instalación y configuración de Flet Python en Debian 13

## Aclaración

En el video de YouTube se utilizó **Flet 0.28.3** y **Visual Studio Code** con la extensión oficial de Python, además de las dependencias **git** y **libmpv2**.

## Introducción

Esta guía detalla los pasos para configurar un entorno de desarrollo con Flet en Python, solucionar problemas de dependencias en Debian 13 y generar ejecutables para Linux y Android.

## Instalación y ejecución

**1. Instalar las dependencias:**

```bash
sudo apt install python3-venv python3-pip git libmpv2 -y
```

**2. Redireccionar a libmpv2:**
Debido a que `libmpv1` no está en los repositorios de Debian 13, creamos un enlace simbólico:

```bash
sudo ln -s /usr/lib/x86_64-linux-gnu/libmpv.so.2 /usr/lib/x86_64-linux-gnu/libmpv.so.1
```

**3. Crear una carpeta de prueba y entrar en ella:**

```bash
mkdir prueba
cd prueba
```

**4. Crear el entorno virtual:**

```bash
python3 -m venv .env
```

**5. Activar el entorno:**

```bash
source .env/bin/activate
```

**6. Instalar Flet:**

```bash
pip install flet
```

**7. Crear el proyecto:**

```bash
flet create .
```

**8. Ejecutar el proyecto:**

```bash
flet run
```

Desde aquí puedes empezar a experimentar con `src/main.py`.

---

## Empaquetado

En esta sección, Flet descargará automáticamente **Flutter** y **Java** en la carpeta principal del usuario.

### Debian

**Instalar las dependencias:**

```bash
sudo apt install clang cmake ninja-build pkg-config libgtk-3-dev -y
```

**Crear ejecutable:**

```bash
flet build linux
```

### Android

**Crear APK para todas las arquitecturas:**

```bash
flet build apk
```

**Crear APK para arm64-v8a:**

```bash
flet build apk --flutter-build-args=--target-platform --flutter-build-args=android-arm64
```

**Crear APK para armeabi-v7a:**

```bash
flet build apk --flutter-build-args=--target-platform --flutter-build-args=android-arm
```

---

## Ocultar carpetas

Es muy probable que no quieras visualizar las carpetas creadas por Flet en tu carpeta personal (`$HOME`). Puedes crear un archivo `.hidden` para ocultarlas en el explorador de archivos:

```bash
nano ~/.hidden
```

Agrega lo siguiente dentro del archivo y guarda los cambios:

```text
flutter
java
```
