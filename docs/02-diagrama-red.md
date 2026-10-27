# 02-diagrama-red

## Objetivo
Diseñar una red de laboratorio para conectar el nodo Proxmox,
el servidor ASO y el cliente Linux de forma controlada.

## 1. Tabla de direccionamiento

| Elemento | Nombre | IP | Función | Recursos |
|---|---|---|---|---|
|Interfaz solo-anfitrión del host| Host-only | 192.168.56.1/24 | Navegador, SSH y Ansible hacia el laboratorio | VM |
| Proxmox Adaptador1 NAT | vmbr0 | 10.0.2.15/24 |   Red exterior | VM |
| Gateway NAT de VirtualBox | - | 10.0.2.2  | Salida al exterior permitido | VM |
| DNS NAT de VirtualBox | - | 10.0.2.3  | Resolución | VM |
| Proxmox Adaptador2 | vmbr1 | 192.168.56.10/24 | Administración y gateway invitados | VM |
| Servidor ASO | srv-aso | 192.168.56.24/24 | Servicio principal | VM |
| Cliente | cli-linux | 192.168.56.34/24 | pruebas | VM |


Nombre del nodo Proxmox: pve-brotons  
Interfaz de gestion: vmbr0  
Bridge de Proxmox: vmbr1  
Red o VLAN de laboratorio: 192.168.56.0/24  
IP del host en la red solo-anfitrión: 192.168.56.1/24.  
IP de administración de Proxmox: 192.168.56.10/24.  
IP del servidor ASO: 192.168.56.24/24.  
IP del cliente Linux: 192.168.56.34/24.  
Gateway de los invitados: 192.168.56.10  
Gateway de la interfaz NAT de Proxmox: 10.0.2.2.  
DNS: 10.0.2.3  
Puertos necesarios: 8006  
Medidas de aislamiento: red solo-anfitrión para la administración y comunicación del laboratorio, con una interfaz NAT separada para la salida exterior  


## 2. Diagrama de red

```mermaid
flowchart TD
    A["Equipo del alumno<br/>LliureX y VirtualBox"]
    B["Red solo-anfitrión<br/>192.168.56.1"]
    C["Proxmox vmbr1<br/>192.168.56.10"]
    D["cli-linux · .34"]
    E["srv-aso · .24"]
    F["Proxmox vmbr0 · 10.0.2.15"]
    G["NAT VirtualBox · 10.0.2.2"]
    H["Salida autorizada del equipo"]

    A --> B
    B --> C

    C --> D
    C -->|Enrutamiento y NAT del nodo| F
    C --> E

    D -->|Samba| E

    F --> G
    G --> H

    classDef nodo fill:#eef0ff,stroke:#7889ff,color:#334155,stroke-width:1px
    class A,B,C,D,E,F,G,H nodo
```


## Conclusion
Esta es la representación teórica del diseño de red

[Volver al indice](../README.md)
