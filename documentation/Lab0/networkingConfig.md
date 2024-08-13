# Laboratorio de pruebas

En este primer reto, el fin es crear un laboratorio de pruebas.

## Creación del laboratorio de pruebas

### Objetivos

Configurar una red de 3 computadores dentro del `hypervisor Virtualbox`.

### Actividades

- Crear una red aislada de la red local en la que se encuentra la máquina `host`.
- Instalar 4 máquinas virtuales:
  - [OPNSense](https://opnsense.org/)
    - Firewall con IP fija.
  - [Kali Linux](https://www.kali.org/get-kali/)
    - Red con IP fija.
  - [Kali-urple](https://www.kali.org/get-kali/)
    - Blue con IP fija.
  - [Metasploitable2](https://sourceforge.net/projects/metasploitable/files/Metasploitable2/)
    - VbD sin IP fija.

### Instalacion de Virtualbox

Para instalar Virtualbox, se debe descargar el instalador desde la página oficial [Virtualbox](https://www.virtualbox.org/).
Esta instalación se debe realizar en la máquina `host`, en particular, este manual se realizó en una máquina con sistema operativo `Pop!_OS 22.04 LTS x86_64`.

- Descargar el instalador de Virtualbox de la página oficial.
  - [Virtualbox](https://www.virtualbox.org/wiki/Linux_Downloads).
- Ejecutar el instalador.
  - `sudo dpkg -i ~/Downloads/virtualbox-6.1_6.1.32-149290_Ubuntu_bionic_amd64.deb`.
- Seguir las instrucciones del instalador.
  - Ejecutar `sudo apt install -f` si hay dependencias que no están instaladas en la máquina `host`.
- Si el sistema lo requiere, Reiniciar la máquina `host`.

### Instalación de OPNSense

Para realizar la instalación de OPNSense, sigue las instrucciones en [OPNSense Installation](./opnSense/opnSenseInstallation.md).

### Configuración de OPNSense

Para realizar la configuración de OPNSense, sigue las instrucciones en [OPNSense Configuration](./opnSense/opnSenseConfiguration.md).

### Instalación de Kali Linux y Kali-purple

Para realizar la instalación de Kali Linux, incluyendo Kali-Purple, sigue las instrucciones en [Kali Linux Installation](./kaliLinux/kaliLinuxInstallation.md).

### Configuración de Kali Linux y Kali-purple

Para realizar la configuración de Kali Linux y Kali-purple, sigue las instrucciones en [Kali Linux Configuration](./kaliLinux/kaliLinuxConfiguration.md).

### Instalación de Metasploitable2

Para realizar la instalación de Metasploitable2, sigue las instrucciones en [Metasploitable Installation](./metasploitable/metasploitableInstallation.md).
