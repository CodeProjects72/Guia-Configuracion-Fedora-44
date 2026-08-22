# Fedora Post-Install

Guía de configuración y puesta a punto de Fedora después de una instalación limpia.

---

## 01 · Optimización de DNF

### Configuración inicial

Editar la configuración de DNF:

```bash
sudo nano /etc/dnf/dnf.conf
```

Añadir:

```ini
fastestmirror=true
max_parallel_downloads=10
deltarpm=true
```

---

## 02 · Actualización del sistema

Actualizar el sistema antes de comenzar con la instalación de paquetes:

```bash
sudo dnf update && sudo dnf upgrade -y
```

---

## 03 · Paquetes multimedia

Instalar codecs, reproductores, herramientas de compresión y utilidades multimedia:

```bash
sudo dnf install -y xz bzip2 unrar p7zip lbzip2 arj lzma lzop cpio webp-pixbuf-loader java unar file-roller xine-lib-extras xine-lib-extras-freeworld gstreamer1-plugins-base-tools vlc libdvdread libdvdnav lsdvd gstreamer1-vaapi libva-utils ImageMagick
```

### GStreamer

Instalar los plugins y codecs adicionales:

```bash
sudo dnf install -y gstreamer1-plugins-{bad-*,good-*,base} gstreamer1-plugin-openh264 gstreamer1-libav --exclude=gstreamer1-plugins-bad-free-devel
```

---

## 04 · Herramientas básicas

Instalar las herramientas esenciales:

```bash
sudo dnf install -y wget curl git
```

---

## 05 · ZSH

### Instalación

Instalar ZSH y las dependencias necesarias:

```bash
sudo dnf install -y git zsh util-linux-user
```

### Oh My Zsh

Clonar el repositorio:

```bash
git clone https://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
```

Crear la configuración:

```bash
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
```

Crear una copia de seguridad:

```bash
cp ~/.zshrc ~/.zshrc.orig
```

### Shell predeterminado

Cambiar el shell del usuario a ZSH:

```bash
sudo chsh -s /bin/zsh nombre-de-usuario
```

Cerrar y volver a abrir la terminal.

---

## 06 · Powerlevel10k

### Instalación

Clonar Powerlevel10k:

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/.oh-my-zsh/custom/themes/powerlevel10k
```

### Configuración

Añadir Powerlevel10k a `.zshrc`:

```bash
echo 'source ~/.oh-my-zsh/custom/themes/powerlevel10k/powerlevel10k.zsh-theme' >> ~/.zshrc
```

Reiniciar ZSH:

```bash
exec zsh
```

Al iniciar aparecerá el asistente de configuración de Powerlevel10k.

---

## 07 · ZSH para Root

Para utilizar ZSH con la cuenta `root`, repetir los mismos pasos de instalación de ZSH, Oh My Zsh y Powerlevel10k desde la cuenta de root.

La configuración de `root` es independiente de la configuración del usuario normal.

---

## 08 · Temas e iconos

### Bibata Cursor

Habilitar el repositorio:

```bash
sudo dnf copr enable peterwu/rendezvous
```

Instalar los cursores:

```bash
sudo dnf install -y bibata-cursor-themes
```

### Layan GTK Theme

Instalar las dependencias:

```bash
sudo dnf install -y gtk-murrine-engine gtk2-engines
```

Clonar el repositorio:

```bash
git clone https://github.com/vinceliuice/Layan-gtk-theme.git
```

Entrar en el directorio:

```bash
cd Layan-gtk-theme
```

Ejecutar el instalador:

```bash
./install.sh
```

---

## 09 · VirtualBox

### Repositorio de Oracle

Descargar el repositorio:

```bash
sudo wget https://download.virtualbox.org/virtualbox/rpm/fedora/virtualbox.repo -P /etc/yum.repos.d/
```

### Dependencias

Instalar las dependencias necesarias:

```bash
sudo dnf install -y kernel-devel kernel-headers dkms elfutils-libelf-devel make gcc
```

### Instalación

Instalar VirtualBox:

```bash
sudo dnf install -y VirtualBox-7.2
```

### Grupo `vboxusers`

Añadir el usuario actual al grupo:

```bash
sudo usermod -aG vboxusers $USER
```

---

## 10 · Reinicio

Reiniciar el sistema para aplicar los cambios:

```bash
sudo reboot
```

---

## Referencias

- [Oh My Zsh](https://github.com/robbyrussell/oh-my-zsh)
- [Powerlevel10k](https://github.com/romkatv/powerlevel10k)
- [Layan GTK Theme](https://github.com/vinceliuice/Layan-gtk-theme)
- [VirtualBox](https://www.virtualbox.org/)
