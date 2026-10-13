# Inventario investigado y viabilidad

## 1. Contexto

- **Equipo analizado:** PC del aula.
- **Sistema operativo:** GNU/Linux.
- **Arquitectura:** x86-64.
- **Versión del kernel:** 5.16.0-15-generic.
- **Objetivo:** comprobar si el equipo puede utilizarse para instalar Proxmox VE y ejecutar las máquinas virtuales de la práctica.

## 2. Inventario inicial del hardware

| Elemento | Información obtenida | Observaciones |
|---|---|---|
| CPU | Intel Pentium G4560 a 3,50 GHz | 2 núcleos y 4 hilos |
| RAM | 8 GB DDR4 a 2400 MHz | Capacidad limitada para ejecutar varias máquinas virtuales |
| Almacenamiento | `/dev/sda`, 465,8 GB | La capacidad libre y el modelo del disco están pendientes de comprobar |
| Tarjeta de red | Realtek RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev. 15) | Tarjeta de red Gigabit Ethernet |
| Placa base | ASUS H110M-K | Modelo anotado en el equipo |
| Gráficos | Intel HD Graphics 610 | Gráficos integrados |
| Arquitectura | x86-64 | Compatible con sistemas operativos de 64 bits |
| Virtualización por hardware | VT-x | - |
| Firmware y arranque | Arranca en UEFI | - |

### Información de red observada

- `lo`: interfaz de loopback, con dirección `127.0.0.1/8`. `Unknown`
- `etho`: interfaz cuya dirección anotada parece ser `192.168.122.1/24`, pero  `DOWN`.
- `docker0`: interfaz asociada a Docker, con dirección `172.17.0.1/16`,  `DOWN`.
- `virbr0`: interfaz de red virtual, con dirección anotada `172.18.0.1/16`. `DOWN`



## 3. Viabilidad de instalar Proxmox VE

### ¿El procesador es compatible?

El equipo dispone de un Intel Pentium G4560 de 64 bits. Intel VT-x esté disponible y habilitada en UEFI 

### ¿La memoria RAM es suficiente?

El equipo tiene 8 GB de RAM DDR4 a 2400 MHz. Esta cantidad permite plantear una práctica pequeña con pocas máquinas virtuales, pero limita la memoria disponible para Proxmox VE y los sistemas invitados. Será necesario asignar recursos de forma moderada.

### ¿El almacenamiento y la red son suficientes?

El disco anotado tiene una capacidad de 465,8 GB, por lo que, en principio, ofrece espacio para plantear la práctica. 

El equipo dispone de una tarjeta de red Realtek Gigabit Ethernet. También es necesario verificar la conectividad real de la interfaz de red y su configuración.

## 4. Reparto propuesto de recursos

La siguiente tabla es una propuesta inicial para una práctica pequeña, no una configuración que se haya aplicado al equipo.

| Elemento                         | CPU/vCPU                  | RAM prevista | Disco previsto | Justificación |
| -------------------------------- | ------------------------- | ------------ | -------------- | ------------- |
| Proxmox y sus servicios          | 2 núcleos compartidos     | 2 GB         | 20 GB          | Necesita recursos para el sistema anfitrión y la gestión de las máquinas virtuales. |
| srv-aso                          | 2 vCPU                    | 2 GB         | 20 GB          | Permite realizar prácticas de administración de sistemas y servicios. |
| cli-linux                        | 1 vCPU                    | 1,5 GB       | 16 GB          | Suficiente para tareas básicas de Linux y pruebas de conexión con el servidor. |
| Plantilla, ISOs y copias locales | No aplica                 | No aplica    | 10 GB          | Reserva espacio para imágenes de instalación, plantillas y copias locales. |
| Margen de operacion              | Recursos compartidos      | 2,5 GB       | Resto disponible | Permite absorber variaciones de consumo y deja espacio para futuras necesidades. |

El reparto de RAM suma 8 GB. Por tanto, es una distribución ajustada: si el anfitrión necesita más memoria, habrá que reducir la asignada a las máquinas virtuales o ejecutar menos máquinas simultáneamente.

Los discos virtuales propuestos suman 36 GB, sin contar las ISO, las plantillas ni el espacio que necesite Proxmox VE. Antes de instalar, se debe comprobar el espacio disponible en el disco físico.

## 5. Limitaciones detectadas

| Limitación | Consecuencia | Posible solución |
|---|---|---|
| 8 GB de RAM | Limita el número de máquinas virtuales y la memoria que se les puede asignar | Ejecutar pocas máquinas a la vez y ajustar la RAM |
| Procesador de 2 núcleos y 4 hilos | El rendimiento puede disminuir con varias máquinas virtuales simultáneas | Evitar cargas de trabajo elevadas |

## 6. Componentes críticos

| Componente | Importancia | Estado |
|---|---|---|
| CPU | Debe permitir la virtualización por hardware | Intel Pentium G4560|
| RAM | Debe permitir ejecutar el anfitrión y las máquinas virtuales | 8 GB DDR4 a 2400 MHz |
| Almacenamiento | Debe disponer de espacio suficiente para el sistema y las máquinas virtuales | Disco de 465,8 GB |
| Red | Debe permitir la conectividad necesaria para la práctica | Tarjeta Realtek Gigabit Ethernet|
| Firmware | Debe permitir configurar la virtualización por hardware | - |

## 7. Fuentes técnicas

| Fuente | Información consultada |
|---|---|
| [Requisitos oficiales de Proxmox VE](https://www.proxmox.com/en/products/proxmox-virtual-environment/requirements) | Requisitos de hardware y virtualización |
| [Especificaciones de ASUS H110M-K](https://www.asus.com/motherboards-components/motherboards/prime/h110m-k/techspec/) | Información de la placa base |
| [Lista de procesadores compatibles con ASUS H110M-K](https://www.asus.com/es/supportonly/h110m-k/helpdesk_cpu/) | Compatibilidad del procesador |
| [Manual de VirtualBox](https://www.virtualbox.org/manual/ch10.html) | Información sobre virtualización por hardware |

## 8. Veredicto de viabilidad

**Viabilidad provisional: apto para una práctica pequeña, pendiente de comprobaciones.**

El equipo dispone de un procesador de 64 bits, 8 GB de RAM, un disco de 465,8 GB y una tarjeta de red Gigabit Ethernet. En principio, estas características permiten plantear un entorno de virtualización sencillo.

La memoria RAM es el principal límite para ejecutar varias máquinas virtuales al mismo tiempo. Por ello, se recomienda utilizar una configuración reducida y ajustar los recursos según las necesidades de la práctica.

## 9. Evidencias y revisión

Para completar el inventario, se pueden recoger estas evidencias desde la terminal de GNU/Linux:

```bash
lscpu
free -h
lsblk
df -h
ip -br addr
ip route
```

[Volver al indice](../README.md)
