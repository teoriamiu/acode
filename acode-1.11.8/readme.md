# Acode - Code Editor for Android

<p align="center">
  <img src='res/logo_1.png' width='250'>
</p>

[![](https://img.shields.io/endpoint?logo=telegram&label=Acode&style=flat&url=https%3A%2F%2Facode.app%2Fapi%2Ftelegram-members-count)](https://t.me/foxdebug_acode) [![](https://dcbadge.vercel.app/api/server/vVxVWYUAWD?style=flat)](https://discord.gg/vVxVWYUAWD)

## • Overview


Welcome to Acode Editor - a powerful and versatile code editing tool designed specifically for Android devices. Whether you're working on HTML, CSS, JavaScript, or other programming languages, Acode empowers you to code on-the-go with confidence.

## • Features

- Edit and create websites, and instantly preview them in a browser.
- Seamlessly modify source files for various languages like Python, Java, JavaScript, and more.
- Built-in javascript console
- Enjoy multi-language editing support with easy management tools.
- Enjoy a large collections of community plugins to enhance your coding experience.

## • Installation

You can get Acode Editor from popular platforms:

[<img src="https://play.google.com/intl/en_us/badges/images/generic/en-play-badge.png" alt="Get it on Google Play" height="60">](https://play.google.com/store/apps/details?id=com.foxdebug.acodefree) [<img src="https://fdroid.gitlab.io/artwork/badge/get-it-on.png" alt="Get it on F-Droid" height="60"/>](https://www.f-droid.org/packages/com.foxdebug.acode/)

## • Project Structure

<pre>
Acode/
|
|- src/   - Core code and language files
|
|- www/   - Public documents, compiled files, and HTML templates
|
|- utils/ - CLI tools for building, string manipulation, and more
</pre>

## • Multi-language Support

Enhance Acode's capabilities by adding new languages easily. Just create a file with the language code (e.g., en-us for English) in [`src/lang/`](https://github.com/Acode-Foundation/Acode/tree/main/src/lang) and include it in [`src/lib/lang.js`](https://github.com/Acode-Foundation/Acode/blob/main/src/lib/lang.js). Manage strings across languages effortlessly using utility commands:

```shell
pnpm run lang add
pnpm run lang remove
pnpm run lang search
pnpm run lang update
```

## • Contributing & Building the Application

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed instructions.

### 🚀 Guía de Compilación Nativa en Termux (aarch64)

Para compilar Acode directamente en un dispositivo Android usando Termux, sigue estos pasos optimizados:

#### 1. Requisitos Previos
Asegúrate de tener instalados los paquetes esenciales en Termux:
```shell
pkg install gradle
# Recomendado: pnpm para una gestión de paquetes más rápida
npm install -g pnpm
```

#### 2. Configuración del Entorno
Exporta las rutas necesarias (ajustadas a tu sistema):
```shell
cat <<EOF >> ~/.zshrc
export JAVA_HOME=/data/data/com.termux/files/usr/lib/jvm/java-21-openjdk
export ANDROID_HOME=$HOME/android-sdk
export PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin:$ANDROID_HOME/platform-tools:$ANDROID_HOME/build-tools/36.0.0
export GRADLE_USER_HOME=$HOME/.gradle
export GRADLE_OPTS="-Dandroid.aapt2FromMaven=false"
EOF
```

#### 3. Instalación de Dependencias
```shell
# 1. 📂 Entra al directorio específico del proyecto acode
cd acode-termux-base/acode-1.11.18 && \

# 2. 📁 Crea la carpeta de plataformas si no existe para evitar errores de ruta
mkdir -p platforms && \

# 3. 📦 Instala todas las dependencias del proyecto usando pnpm
pnpm install && \

# 4. 🤖 Añade la plataforma Android versión 14.0.1 sin guardarla en el manifiesto
npx cordova platform add android@14.0.1 --nosave && \

# 5. 🔨 Ejecuta el script de construcción para generar el proyecto final
pnpm run build
```

#### 4. El Parche de AAPT2 (Solución Crítica de Arquitectura)
Gradle descarga versiones x86_64 de `aapt2` que fallan en Termux. Este script inyecta el binario nativo de tu SDK en la caché de Gradle:

> **Nota:** Si es tu primera vez compilando, ejecuta primero `pnpm run build` y deja que falle. Esto forzará a Gradle a descargar las herramientas necesarias para que el script pueda encontrarlas y parchearlas.

```shell
# 1. Localiza el binario nativo en el SDK
NATIVE_AAPT2=$ANDROID_HOME/build-tools/36.0.0/aapt2

# 2. Parchear tanto archivos JAR como binarios extraídos en la caché
echo "Aplicando parches de AAPT2..."
find $GRADLE_USER_HOME/caches -name "aapt2-*-linux.jar" | while read jar; do
  echo "Parcheando JAR: $jar"
  cp $NATIVE_AAPT2 ./aapt2
  zip -f "$jar" aapt2
  rm aapt2
done

find $GRADLE_USER_HOME/caches -name "aapt2" -type f | while read binary; do
  # Solo parchear si no es el binario nativo del SDK
  if [[ "$binary" != *"$ANDROID_HOME"* ]]; then
    echo "Reemplazando binario extraído en: $binary"
    cp $NATIVE_AAPT2 "$binary"
  fi
done
```

#### 5. Compilación Final
```shell
pnpm run build
```

El APK generado estará en:
`platforms/android/app/build/outputs/apk/debug/app-debug.apk`

El APK generado se encontrará en:
`platforms/android/app/build/outputs/apk/debug/app-debug.apk`

---

## • Contributors

<a href="https://github.com/Acode-Foundation/Acode/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=Acode-Foundation/Acode" />
</a>

## • Developing a Plugin for Acode

For comprehensive documentation on creating plugins for Acode Editor, visit the [repository](https://github.com/Acode-Foundation/acode-plugin).

For plugin development information, refer to: [Acode Plugin Documentation](https://docs.acode.app/)

## Star History

<a href="https://star-history.com/#Acode-Foundation/Acode&Date">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=Acode-Foundation/Acode&type=Date&theme=dark" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=Acode-Foundation/Acode&type=Date" />
   <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=Acode-Foundation/Acode&type=Date" />
 </picture>
</a>
