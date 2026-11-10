# 03-instalacion-proxmox

## Objetivo

## Procedimiento


Para Proxmox virtualizado

    Abrir VirtualBox en tu equipo y registrar su version.
    Crear una VM Linux de 64 bits para Proxmox con CPU, RAM y VDI del diseno.
    Reservar recursos para el sistema anfitrion; no usar toda su RAM para la VM.
    Configurar los adaptadores NAT y solo-anfitrion conforme al diseno local.
    Con la VM apagada, habilitar virtualizacion anidada si esta disponible y necesitas VMs KVM internas; comprobar luego su funcionamiento real.
    Montar la ISO autorizada e instalar Proxmox dentro del VDI, no sobre el host.
    Configurar IP de gestion, hostname y DNS; abrir el panel desde el navegador del mismo equipo anfitrion.
    Desplegar srv-aso y cli-linux dentro de Proxmox, no como dos VMs independientes de VirtualBox. Documentar la alternativa LXC si KVM anidado no esta disponible.





## Comandos usados

```bash
hostnamectl   
ip -br addr    
pveversion df -h
nano /etc/network/interfaces
ifreload
```

## Evidencias

    Captura del panel Proxmox.
    Captura de red y almacenamiento.
    Salida de:

hostnamectl   
ip -br addr    
pveversion df -h  

https://private-user-images.githubusercontent.com/265017921/700687226-8f18f28a-8b67-436c-a03c-8eb8c1b43cb6.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3OTQzMDA4OTgsIm5iZiI6MTc5NDMwMDU5OCwicGF0aCI6Ii8yNjUwMTc5MjEvNzAwNjg3MjI2LThmMThmMjhhLThiNjctNDM2Yy1hMDNjLThlYjhjMWI0M2NiNi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYxMTEwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MTExMFQwODQ5NThaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT04NGI3ZTkxZDE5MDBmZTJkMzJmNzgwYzE1NGUwZTExMjJlY2MyM2Y0MTI1NTE1YWUxY2ViODFkOTJjNzAwN2E2JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZyZXNwb25zZS1jb250ZW50LXR5cGU9aW1hZ2UlMkZwbmcifQ.bb_dMDbaLqsjoFKscoq78HygCwu41XzHbEwXnpwei1A

## Conclusion

Hemos instalado proxmox correctamente con la configuracion de red que habiamos organizado previamente

[Volver al indice](../README.md)
