# Instalación de OPNSense

## Objetivos

- Instalar OPNSense en una máquina virtual.
- Configurar OPNSense para que funcione como firewall.

## Pre-requisitos

- Tener instalado VirtualBox.

## Actividades

- Descargar la imagen de OPNSense desde la página oficial.
  - [OPNSense](https://opnsense.org/download/).
- Crear una máquina virtual en VirtualBox.
- Configurar la máquina virtual con las características necesarias.
- Instalar OPNSense en la máquina virtual.
- Configurar OPNSense para que funcione como firewall.

## Descargar la imagen de OPNSense

Para descargar la imagen de OPNSense, se debe acceder a la página oficial de OPNSense y descargar la imagen de la versión deseada.

- [OPNSense](https://opnsense.org/download/).

Para la instalación de OPNSense, se recomienda descargar la versión `AMD64` de la imagen para la versión del Sistema operativo del `host` y la siguiente configuración:

![alt text](image-32.png)

Siguiendo la descarga se obtiene un archivo `.iso` que se usará para instalar OPNSense en la máquina virtual.

## Crear una máquina virtual en VirtualBox

Para crear una máquina virtual en VirtualBox, se realizaron los siguientes pasos:

- Abrir VirtualBox.

- Seleccionar la opción Nueva en la pantalla de inicio.

- Configurar la máquina virtual con los siguientes parámetros:
  - Nombre: `OPNSense`.
  - ISO Image: `opnsense-22.1.1-amd64.iso`, este es el archivo `.iso` que se descargó anteriormente.
  - Tipo: `BSD`.
  - Versión: `FreeBSD (64-bit)`.

![alt text](image.png)

- Configurar la memoria RAM de la máquina virtual.
  - Memoria: `2048 MB`, este es el requerimiento mínimo.
  - Procesadores: `2`, el requerimiento mínimo para una máquina virtual.

![alt text](image-1.png)

- Configurar el disco duro de la máquina virtual.
  - Tipo de archivo: `VDI (VirtualBox Disk Image)`.
  - Almacenamiento: `Dinámico asignado`.
  - Tamaño: `10 GB`, este es el requerimiento mínimo.

![alt text](image-2.png)

- Validar la configuración de la máquina virtual y seleccionar la opción `Crear`.

![alt text](image-3.png)

- Una vez creada la máquina virtual, seleccionar la opción `Configurar`.

- Configurar los adaptadores de red en la sección `Sistema`.
  - Boot Order: Seleccionar `CD/DVD-ROM` para que inicie desde el `.iso` de OPNSense y `HDD` para que inicie desde el disco duro.

![alt text](image-5.png)

- En la sección `Display`, configurar los recursos de display (Opcional).
  - Memoria de video: `64 MB`.

![alt text](image-7.png)

- Configurar los adaptadores de red en la sección `Red`.
  - Adaptador 1: `Adaptador Puente`, este adaptador será la conexión con el exterior(Internet).
    - Nombre: `wlp3s0`, este el nombre de la interfaz de red del `host`, puede ser la conexi[on de red **ethernet** o **wifi** y el nombre puede diferir según el sistema operativo.
  - Adaptador 2: `Red interna`, este adaptador será la conexión para las máquinas virtuales internamente.
    - Nombre: `intnet`.

![alt text](image-8.png)

![alt text](image-9.png)

- Validar la configuración de la máquina virtual y seleccionar la opción `OK`.

- Seleccionar `Iniciar`.

- Una vez iniciada la máquina virtual, se inicia la instalación de OPNSense y el primer paso es presionar cualquier tecla para asignar las interfaces de red. Estas interfaces se asignan de la siguiente manera:
  - `em0`: Adaptador 1 que será la conexión con el exterior (WAN).
  - `em1`: Adaptador 2 que será la conexión con las máquinas virtuales internamente (LAN).

- La instalación preguntará por las sigueintes configuraciones:
  - Configuración de LAGGs: `n`.
  - Configuración de VLANs: `n`.
  - WAN interface: `em0`.
  - LAN interface: `em1`.
  - interfáz opcional: ``.

- Después de asignar las interfaces de red, se valida y se confirma la configuración.

![alt text](image-11.png)

- Con esta primera confiración se inicia la instalación de OPNSense y se pueden ver las interfaces seleccionadas, en este caso `em0` y `em1`, así como un prompt para iniciar sesión. Para esto se configuran de forma automática dos usuarios `root` e `installer`, con las contraseñas `opnsense` y `opnsense`, respectivamente.

- Para proceder con la instalación se debe inciar sesión con el usuario `installer` y la contraseña `opnsense`.

![alt text](image-14.png)

- Esto inicia la instalación de OPNSense y se debe seleccionar la opción `Continuar con el teclado por defecto`.

![alt text](image-15.png)

- Seleccionar la opción `Instalar UFS`.

![alt text](image-16.png)

- Seleccionar la opción `ada0`, este es el disco duro de la máquina virtual donde se instalará OPNSense.

![alt text](image-17.png)

- Una vez seleccionado el disco duro, se confirma la instalación y se procede con la instalación de OPNSense.

![alt text](image-20.png)

- Después de la instalación, se debe cambiar la contraseña del usuario `root`, estas credenciales serán utilizadas para acceder a la interfaz web de OPNSense, así que es importante recordarlas.

![alt text](image-21.png)

- Después de cambiar la contraseña, se completa la instalación de OPNSense y se reinicia la máquina virtual.

![alt text](image-22.png)

- Esto es el proceso de instalación, pero una vez la maquina virtual se reinicie, debemos apagarla, quitar el `.iso` de OPNSense en la `Configuración` del Sistema y encenderla de nuevo. Esto se hace para que al iniciar de nuevo la máquina virtual, inicie desde el disco duro y no desde el `.iso`.

![alt text](image-23.png)

- Después de haber instalado OPNSense, e iniciada la máquina virtual, se debe configurar OPNSense para que funcione como firewall.

## Configurar las interfaces de OPNSense

Para configurar OPNSense, se deben seguir los siguientes pasos:

- Se inicia sesión en la terminal de OPNSense con las credenciales del usuario `root` y la contraseña configurada en la instalación.

- Se debe configurar las interfaces de red de OPNSense, para esto se debe seleccionar la opción `2`.

![alt text](image-24.png)

- Esta opción muestra las interfaces de red disponibles. En este caso, se deben configurar las interfaces `em0` y `em1`.

- Se debe configurar la interfaz WAN, en este caso `em0`, con las siguientes configuraciones:
  - DHCP: `none`.
  - IPv4: `192.168.1.100`, esta es la ip estática de la interfaz WAN y como se conectará a la red local.
  - IPv4 subnet: `24`, este es el rango de ip que se asignará a la red local.
  - IPv4 gateway: `192.168.1.1`, este es el gateway del router de la red local.
  - IPv4 name server: `1.1.1.1`, este es el DNS de Cloudflare que nos permitirá resolver nombres de dominio.
  - DHCP IPv6: `n`.
  - IPv6: ``.

![alt text](image-25.png)

![alt text](image-26.png)

- Se debe configurar la interfaz LAN, en este caso `em1`, con las siguientes configuraciones:
  - IPv4: `192.168.0.1`, esta es la ip estática de la interfaz LAN y como se conectará a las máquinas virtuales internamente, esta ip debe ser diferente a la ip de la interfaz WAN.
  - IPv4 subnet: `24`, este es el rango de ip que se asignará a las máquinas virtuales internamente.
  - IPv4 Gateway: `none`, no se asigna un gateway a la interfaz LAN ya que esta será la puerta de enlace de la red WAN.
  - DHCP IPv6: `n`.
  - IPv6: ``.
  - DHCP: `y`, se habilita el servidor DHCP para asignar ip a las máquinas virtuales internamente.
    - Rango de ip: `192.168.0.10` a `192.168.0.254`, este es el rango de ip que se asignará a las máquinas virtuales internamente, es decir, puede haber hasta 244 máquinas virtuales en la red interna.
  - Selecionamos `n` para las demás opciones.

![alt text](image-27.png)

![alt text](image-28.png)

- Después de configurar las interfaces de red, se guarda la configuración y regresa al menú principal. Ahora se muestran las interfaces de red configuradas y el URL de acceso a la interfaz web de OPNSense, en este caso es `https://192.168.0.1`.

![alt text](image-29.png)

- Con esto se ha configurado OPNSense para que funcione como firewall, para ver la configuración de OPNSense en la interfaz web, por favor ir al siguiente enlace [OPNSense Configuration](./opnSenseConfiguration.md).

## Recursos

- [OPNSense Guide](https://opnsense.org/users/get-started/).
