# Guia-Configuracion-Fedora-44Fedora Post-Install

Configuración y software recomendado después de una instalación limpia de Fedora.

Editar el archivo de configuración:

sudo nano /etc/dnf/dnf.conf

Añadir:

fastestmirror=true
max_parallel_downloads=10
deltarpm=true

🔄 Actualizar el sistema
sudo dnf update && sudo dnf upgrade -y

🎬 Paquetes multimedia

Instalar codecs, reproductores, herramientas de compresión y utilidades multimedia:

sudo dnf install -y xz bzip2 unrar p7zip lbzip2 arj lzma lzop cpio webp-pixbuf-loader java unar file-roller xine-lib-extras xine-lib-extras-freeworld gstreamer1-plugins-base-tools vlc libdvdread libdvdnav lsdvd gstreamer1-vaapi libva-utils ImageMagick

GStreamer
sudo dnf install -y gstreamer1-plugins-{bad-*,good-*,base} gstreamer1-plugin-openh264 gstreamer1-libav --exclude=gstreamer1-plugins-bad-free-devel

🛠️ Herramientas básicas
sudo dnf install -y wget curl git

🐚 ZSH
Instalación
sudo dnf install -y git zsh util-linux-user

Oh My Zsh
git clone https://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh


Crear la configuración:

cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc


Crear una copia de seguridad:

cp ~/.zshrc ~/.zshrc.orig

Establecer ZSH como shell predeterminado

Cambiar nombre-de-usuario por el usuario correspondiente:

sudo chsh -s /bin/zsh nombre-de-usuario


Cerrar y volver a abrir la terminal.

✨ Powerlevel10k

Instalar Powerlevel10k:

git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/.oh-my-zsh/custom/themes/powerlevel10k


Activar el tema:

echo 'source ~/.oh-my-zsh/custom/themes/powerlevel10k/powerlevel10k.zsh-theme' >> ~/.zshrc


Reiniciar ZSH:

exec zsh


Al iniciar aparecerá el asistente de configuración de Powerlevel10k.

👑 ZSH para root

Para utilizar ZSH con root, repetir la instalación de Oh My Zsh y Powerlevel10k desde la cuenta de root.

La configuración de root es independiente de la configuración del usuario normal.

🎨 Temas e iconos
Cursor — Bibata

Habilitar el repositorio:

sudo dnf copr enable peterwu/rendezvous


Instalar:

sudo dnf install -y bibata-cursor-themes

Tema GTK — Layan

Instalar dependencias:

sudo dnf install -y gtk-murrine-engine gtk2-engines


Clonar el repositorio:

git clone https://github.com/vinceliuice/Layan-gtk-theme.git


Entrar en el directorio:

cd Layan-gtk-theme


Ejecutar el instalador:

./install.sh

📦 VirtualBox
Repositorio de Oracle
sudo wget https://download.virtualbox.org/virtualbox/rpm/fedora/virtualbox.repo -P /etc/yum.repos.d/

Dependencias
sudo dnf install -y kernel-devel kernel-headers dkms elfutils-libelf-devel make gcc

Instalación
sudo dnf install -y VirtualBox-7.2

Grupo vboxusers

Añadir el usuario actual al grupo:

sudo usermod -aG vboxusers $USER

🔁 Reiniciar

Después de completar la instalación:

sudo reboot

✅ Checklist
 Optimización de DNF
 Actualización del sistema
 Codecs y multimedia
 Herramientas básicas
 ZSH
 Oh My Zsh
 Powerlevel10k
 Tema Layan
 Cursores Bibata
 VirtualBox
📌 Notas

Esta guía está pensada para una instalación limpia de Fedora y sirve como referencia para preparar rápidamente el entorno de trabajo.

Aviso: Algunos paquetes y repositorios pueden variar según la versión de Fedora utilizada.
