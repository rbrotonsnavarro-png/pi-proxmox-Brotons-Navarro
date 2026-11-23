# Memoria tecnica: nodo Proxmox individual

La memoria presenta el resultado tecnico por temas. Debe explicar como esta
construido el laboratorio, por que se tomaron las decisiones y con que pruebas
se demostro su funcionamiento. Usa la bitacora como fuente, pero no copies el
diario completo: resume la configuracion final, los resultados y las
limitaciones que sigan abiertas.

## Resumen

En este proyecto se está construyendo un laboratorio de virtualización utilizando Proxmox instalado dentro de una máquina virtual de VirtualBox. El objetivo es disponer de un entorno donde poder crear y administrar máquinas virtuales para realizar prácticas de administración de sistemas operativos y servicios de red.

## Necesidad y objetivos

Necesidad que atiende el laboratorio:

Disponer de un entorno controlado de virtualización donde poder instalar sistemas operativos, configurar servicios y realizar pruebas de administración de sistemas sin tener que modificar directamente el sistema operativo del equipo físico.

Objetivo comprobable 1: instalar Proxmox dentro de VirtualBox y acceder correctamente a su panel de administración mediante el navegador.

Objetivo comprobable 2: configurar las interfaces de red y el direccionamiento para permitir la comunicación entre el nodo Proxmox, el servidor ASO y el cliente Linux.

Objetivo comprobable 3: desplegar máquinas virtuales y configurar servicios de administración de sistemas, comprobando su funcionamiento mediante pruebas de conectividad y acceso.

## Alcance y criterios de aceptacion

El proyecto incluye la instalación de Proxmox VE virtualizado mediante VirtualBox, la configuración de las interfaces de red, la preparación de los almacenamientos y el despliegue de máquinas virtuales para realizar prácticas de ASO.

También se contempla la creación de una plantilla Linux, la instalación de servicios, la automatización de tareas mediante Bash y Ansible y la realización de copias de seguridad.

Quedan fuera del alcance la instalación de Proxmox directamente sobre el equipo físico, la utilización del laboratorio como entorno de producción y la configuración de una infraestructura empresarial completa.

Los criterios de aceptación son:

-Proxmox debe instalarse correctamente y permitir el acceso a su panel web.

-Las interfaces de red deben tener las direcciones IP previstas y permitir la conectividad necesaria.

-Las máquinas virtuales deben poder crearse y arrancar correctamente.

-El servidor y el cliente deben poder comunicarse mediante la red del laboratorio.

-Los servicios instalados deben funcionar y permitir realizar las pruebas previstas.

-Las tareas automatizadas y las copias de seguridad deben poder comprobarse mediante sus respectivas pruebas.

## Modalidad e inventario
El equipo físico analizado dispone de las siguientes características:

Elemento

Características

Procesador

Intel Pentium G4560 a 3,50 GHz

Núcleos e hilos

2 núcleos y 4 hilos

Memoria RAM

8 GB DDR4 a 2400 MHz

Almacenamiento

Disco de aproximadamente 465,8 GB

Tarjeta de red

Realtek Gigabit Ethernet

Placa base

ASUS H110M-K

Gráficos

Intel HD Graphics 610

Arquitectura

x86-64

Virtualización

Intel VT-x

La principal limitación del equipo es la memoria RAM, ya que dispone de solamente 8 GB. Por este motivo, es necesario controlar los recursos asignados a Proxmox y a las máquinas virtuales.

El inventario completo y el estudio de viabilidad se encuentran en:
[Inventario](01-inventario-hardware.md)

## Diseno de red

Se ha diseñado una red utilizando dos adaptadores de red en la máquina virtual de Proxmox. Uno utiliza NAT para proporcionar salida al exterior y el otro utiliza una red solo-anfitrión para la administración y la comunicación entre los equipos del laboratorio.

El direccionamiento utilizado es el siguiente:

Elemento

Interfaz o nombre

Dirección IP

Función

Equipo anfitrión

Host-only

192.168.56.1/24

Administración

Proxmox

vmbr0

10.0.2.15/24

Salida al exterior

Proxmox

vmbr1

192.168.56.10/24

Administración y red interna

Gateway NAT

-

10.0.2.2

Salida al exterior

DNS NAT

-

10.0.2.3

Resolución de nombres

Servidor ASO

srv-aso

192.168.56.24/24

Servicios

Cliente Linux

cli-linux

192.168.56.34/24

Pruebas

El nombre del nodo Proxmox es pve-brotons y el puerto utilizado para acceder al panel de administración es el 8006.

Se ha separado la red de administración de la salida al exterior para mantener una mayor organización y controlar las comunicaciones del laboratorio.

El diseño completo se encuentra en:
[Diagrama y direccionamiento](02-diagrama-red.md)

## Instalacion y configuracion de Proxmox

Se ha instalado Proxmox VE dentro de una máquina virtual de VirtualBox, utilizando una imagen ISO y configurando previamente los adaptadores de red.

Durante la instalación se ha establecido el nombre del nodo pve-brotons y se han configurado las interfaces de red vmbr0 y vmbr1 siguiendo el diseño realizado anteriormente.

También se ha revisado la configuración de los almacenamientos disponibles:

Almacenamiento

Tipo

Capacidad

local

Directorio

30,2 GiB

local-lvm

LVM-Thin

32,7 GiB

El almacenamiento local utiliza el directorio /var/lib/vz, mientras que local-lvm utiliza el grupo de volúmenes pve y el Thin Pool data.

Se ha realizado una segunda instalación siguiendo las indicaciones del profesor para mejorar la configuración inicial. Posteriormente, se ha terminado la configuración base del nodo y se ha comprobado que el entorno se encuentra preparado para continuar con la creación de máquinas virtuales.

Los comandos utilizados para comprobar la configuración han sido:

hostnamectl
ip -br addr
pveversion
df -h
nano /etc/network/interfaces
ifreload

El procedimiento completo y las evidencias se encuentran en:
[Procedimiento](03-instalacion-proxmox.md)

## Plantilla Linux y despliegue

[Plantilla](04-plantilla-linux.md) y [VMs/LXC](05-vms-lxc.md)

## Servicio ASO

[Instalacion y pruebas](06-servicio-aso.md)

## Automatizacion con Bash y Ansible

[Automatizacion](07-automatizacion.md)

## Copias y restauracion

[Procedimiento y validacion](08-copias-restauracion.md)

## Rendimiento y seguridad

[Resultados](09-rendimiento-seguridad.md)

## Incidencias y decisiones

[Bitacora](00-bitacora.md)

## Presupuesto y sostenibilidad

## Conclusiones

## Fuentes y anexos

[Evidencias](../evidencias/README.md) y [volver al indice](../README.md)
