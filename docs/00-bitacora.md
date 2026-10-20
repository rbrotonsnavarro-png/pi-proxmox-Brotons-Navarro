# Bitacora de sesiones

La bitacora es el registro cronologico del trabajo. Se anade una entrada al final de cada sesion y se conservan las anteriores.

## Sesion 01 - 06/10/2026

- **Objetivo:** iniciar GitHub y la documentacion Markdown.
- **Acciones realizadas:** se creo el repositorio `pi-proxmox-Brotons-Navarro` en GitHub. Se preparo la estructura inicial de carpetas y archivos, se inicializo Git en el directorio local y se configuro el repositorio remoto. Se publico el proyecto en GitHub mediante `git push`.
- **Decisiones y motivos:** se eligio GitHub para almacenar la documentacion y mantener una copia accesible desde distintos ordenadores. Se utilizo Markdown por su sencillez y porque permite documentar el proyecto directamente en el repositorio. Se preparo una estructura separada para documentacion, evidencias, scripts y automatizacion.
- **Pruebas y resultados:** se ejecuto `git push -u origin main` y la operacion finalizo correctamente. GitHub confirmo la publicacion de la rama `main`. Se puede comprobar accediendo al repositorio y revisando los archivos publicados.
- **Documentos o evidencias:** [Ficha inicial](00-ficha-inicial.md), [README del proyecto](../README.md) y [carpeta de evidencias](../evidencias/README.md).
- **Incidencias y solucion o estado pendiente:** al principio hubo problemas de autenticacion y permisos al intentar publicar el repositorio. Se reviso el acceso a GitHub hasta conseguir completar el envio. Queda pendiente comprobar que el profesor tiene acceso al repositorio si este es privado.
- **Siguiente paso:** completar el inventario de hardware, registrar las caracteristicas del equipo y planificar los recursos que se asignaran a Proxmox y a las maquinas virtuales.

## Sesion 02 - 13/10/2026

- **Objetivo:** identificar el hardware disponible y comenzar la planificacion de recursos del proyecto.
- **Acciones realizadas:** se recopilaron las caracteristicas del equipo fisico: procesador Intel Pentium G4560 a 3,50 GHz, 2 nucleos y 4 hilos, 8 GB de RAM DDR4 a 2400 MHz, almacenamiento de aproximadamente 465,8 GB y tarjeta de red Realtek Gigabit Ethernet. Se comenzo a planificar la asignacion de recursos para Proxmox, el servidor `srv-aso`, el cliente `cli-linux` y el almacenamiento de imagenes ISO y copias locales.
- **Decisiones y motivos:** se planteo una distribucion ajustada de los recursos porque el equipo dispone de 8 GB de RAM. Se debe reservar memoria para el hipervisor y evitar asignar a las maquinas virtuales mas recursos de los que permite el equipo.
- **Pruebas y resultados:** se identificaron los componentes principales del equipo y se establecio una planificacion inicial. La asignacion definitiva de CPU, RAM y disco queda pendiente de comprobar durante la preparacion e instalacion del entorno.
- **Documentos o evidencias:** [Inventario de hardware](01-inventario-hardware.md) y [ficha inicial](00-ficha-inicial.md).
- **Incidencias y solucion o estado pendiente:** los 8 GB de RAM limitan la cantidad de memoria que se puede asignar simultaneamente a las maquinas virtuales. Queda pendiente ajustar la distribucion definitiva.
- **Siguiente paso:** completar y revisar el inventario de hardware y preparar la instalacion de Proxmox, verificando los requisitos y la distribucion de recursos.


## Sesion 02 - 13/10/2026

- **Objetivo:** Realizar el diagrama de red
- **Acciones realizadas:** he diseñado un diagrama de red para proxmox con ayuda de los apuntes 
- **Documentos o evidencias:** [Inventario de hardware](02-diagrama-red.md) y [ficha inicial](00-ficha-inicial.md).
- **Siguiente paso:** Instalación del proxmox en la máquina virtual


[Volver al indice](../README.md)
