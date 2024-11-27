# Laboratorio de seguridad en IPv6

Este laboratorio explora una de las vulnerabilidades más comunes en redes IPv6: NDP Spoofing (Neighbor Discovery Protocol Spoofing). Se utiliza una topología en containerlab que permite simular y analizar este tipo de ataque, así como implementar mecanismos de mitigación.

NDP Spoofing (también conocido como Neighbor Discovery Protocol Spoofing) es un tipo de ataque que explota el protocolo NDP, utilizado en redes IPv6 para tareas como la resolución de direcciones IP a direcciones MAC, la detección de enrutadores, y la configuración automática de direcciones. 

Funciona como un ataque de hombre en el medio (MITM) en donde el atacante se inserta entre dos partes comunicantes creando la posibilidad de que el atacante descarte, lea o modifique los mensajes antes de que lleguen al destinatario previsto.

![ataque de hombre en el medio](img/ataque-MITM.png)

Al igual que en ARP Spoofing, el atacante envía mensajes falsos para engañar a los dispositivos de la red, logrando que asocien una dirección IPv6 legítima con la dirección MAC del atacante. Esto le permite interceptar, manipular o redirigir el tráfico de la red.

En este laboratorio, se demuestra cómo un atacante puede utilizar mensajes de Router Advertisement (RA) para hacerse pasar por un router. De esta manera, el atacante intenta que las víctimas lo configuren como su puerta de enlace predeterminada.
Para mitigar este ataque, se implementa RA-Guard, que bloquea la comunicación no autorizada en capa 2, permitiendo solo al router legítimo enviar paquetes a través de la dirección multicast de enlace local.

## Ejemplo

Este escenario utiliza una topología básica compuesta por dos máquinas Linux, dos routers (SRL y FRR) y un switch, para demostrar la facilidad con la que se pueden ejecutar ataques NDP Spoofing y cómo mitigar dichos ataques utilizando RA-Guard en un router Nokia SRLinux.

#### Clonar repositorio

Clona el repositorio que contiene los archivos necesarios para desplegar la topología:

```bash
git clone https://github.com/ernestosv73/srl03
```

#### Editar la configuracion inicial

1. Edita el archivo de configuración principal:
   - Descomenta las líneas que siguen a **`name: srl03`** para habilitar el uso del bridge en la topología.
2. Cambia la configuración de inicio (**`startup-config`**) del router **srl1** a **srl2.cfg**.

#### Acceso a los nodos Linux

Puedes acceder a las máquinas Linux para realizar las pruebas desde la terminal:

```bash
# PC1 (Kali Linux)
docker exec -it clab-srl02-PC1 /bin/bash
# PC3 (Network-Multitool)
docker exec -it clab-srl02-PC3 /bin/bash
```

#### Acceso al router SRL

Para conectarte al router SRLinux, utiliza SSH con las siguientes credenciales:

```bash
ssh admin@clab-srl02-srl1
password: NokiaSrl1!
```
#### Iniciar el ataque

Desde **PC1**, ejecuta el siguiente comando para realizar un ataque NDP Spoofing:

```bash
# Ejecutamos el NDP Spoofing -> PC1
atk6-fake_router6 eth1 2001:db8:ffff:1::/64
```

Observamos las consecuencias en la PC y router SRLEn **PC3**, verifica las direcciones IPv6 asignadas:

```bash
ifconfig
```

En el router SRLinux, comprueba las rutas afectadas:

```bash
show network-instance route-table
```

#### Implementacion de RA-Guard en el nodo SRL

Mitiga el ataque configurando RA-Guard en el router SRLinux:

```bash
# Ingresamos al modo de configuracion
enter candidate
# Aplicamos la ra guard a nivel de sistema
system ra-guard-policy "Discard all" action discard
# Guardamos los cambios
commit stay
# Aplicamos la ra guard a nivel de interfaz mgmt0
interface mgmt0 subinterface 0 ra-guard policy "Discard All"
# Guardamos los cambios
commit stay
# Volvemos al modo running
enter running
# Volvemos a comprobar las rutas aplicando un nuevo ataque
show network-instance route-table
```

Con las configuraciones de RA-Guard aplicadas, el ataque NDP Spoofing es bloqueado eficazmente. Esto demuestra cómo las políticas de RA-Guard protegen la red al descartar paquetes maliciosos y mantener la integridad del enrutamiento.

