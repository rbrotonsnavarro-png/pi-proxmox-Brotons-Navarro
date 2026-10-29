# 03-instalacion-proxmox

## Objetivo

## Procedimiento
9. Fase 3. Instalacion de Proxmox

Para Proxmox virtualizado

    Abre VirtualBox en tu equipo y registra su version.
    Crea una VM Linux de 64 bits para Proxmox con CPU, RAM y VDI del diseno.
    Reserva recursos para el sistema anfitrion; no uses toda su RAM para la VM.
    Configura los adaptadores NAT y solo-anfitrion conforme al diseno local.
    Con la VM apagada, habilita virtualizacion anidada si esta disponible y necesitas VMs KVM internas; comprueba luego su funcionamiento real.
    Monta la ISO autorizada e instala Proxmox dentro del VDI, no sobre el host.
    Configura IP de gestion, hostname y DNS; abre el panel desde el navegador del mismo equipo anfitrion.
    Despliega srv-aso y cli-linux dentro de Proxmox, no como dos VMs independientes de VirtualBox. Documenta la alternativa LXC si KVM anidado no esta disponible.

Evidencias:

    Captura del panel Proxmox.
    Captura de red y almacenamiento.
    Salida de:

hostnamectl   
ip -br addr    
pveversion df -h  

## Comandos usados

```bash

```

## Evidencias

## Incidencias

## Conclusion

[Volver al indice](../README.md)
