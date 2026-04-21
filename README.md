# Acode - Code Editor for Android

<p align="center">
  <img src='res/logo_1.png' width='250'>
</p>

[![]([https://img.shields.io/endpoint?logo=telegram&label=Acode&style=flat&url=https%3A%2F%2Facode.app%2Fapi%2Ftelegram-members-count)](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSCJZ8ZszBvHEgfE3pBcXkcGF29EhAHPsA6pNUC9ZK2MpeEZJab1sAI9eFS&s=10)](https://t.me/foxdebug_acode) [![](https://dcbadge.vercel.app/api/server/vVxVWYUAWD?style=flat)](https://discord.gg/vVxVWYUAWD)

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
# 1. 📂 Habilita el acceso a las carpetas del almacenamiento interno del teléfono
termux-setup-storage && \

# 2. 🔄 Sincroniza el índice de paquetes con los servidores oficiales
pkg update -y && \

# 3. 🆙 Sube de versión los paquetes instalados aceptando configuraciones nuevas automáticamente
pkg upgrade -y -o Dpkg::Options::="--force-confnew" && \

# 4. 🐙 Instala GitHub CLI para gestionar repositorios desde la terminal
pkg install gh -y && \

# 5. 🐚 Instala el shell Zsh como alternativa avanzada a Bash
pkg install zsh -y && \

# 6. 🌿 Instala Git para el control de versiones de tus proyectos
pkg install git -y && \

# 7. 🟢 Instala el entorno Node.js para ejecutar JavaScript
pkg install nodejs -y && \

# 8. 📦 Instala pnpm globalmente para una gestión de paquetes más rápida y eficiente
npm install -g pnpm && \

# 9. 🐘 Instala Gradle para la automatización y compilación de proyectos (como Android)
pkg install gradle -y && \

# 10. 🤐 Instala Zip para comprimir y empaquetar archivos desde la terminal
pkg install zip -y && \

# 11. 🪄 Instala Oh My Zsh de forma automatizada y desatendida
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended && \

# 12. 💡 Clona el plugin de sugerencias automáticas (Autosuggestions)
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions && \

# 13. 🎨 Clona el plugin de resaltado de sintaxis (Syntax Highlighting)
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting && \

# 14. ⚙️ Configura los plugins dentro del archivo .zshrc automáticamente
sed -i 's/plugins=(git)/plugins=(git zsh-autosuggestions zsh-syntax-highlighting)/' ~/.zshrc && \

# 15. 🤫 Elimina el mensaje de bienvenida de Termux (Hush Login)
touch ~/.hushlogin && \

# 16. 🏁 Cambia el shell por defecto a Zsh y reinicia la sesión reemplazando el proceso
chsh -s zsh && exec zsh
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
