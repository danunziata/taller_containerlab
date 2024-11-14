# Taller Containerlab

## Fundamentos

### Containerlab

#### ¿Qué es Containerlab?
Containerlab es una herramienta de código abierto que facilita la creación y gestión de laboratorios de redes usando contenedores Docker o Podman. Fue creada con el objetivo de simplificar la replicación y gestión de laboratorios de redes mediante la infraestructura como código (IaC). Containerlab permite levantar y configurar topologías de red en un entorno controlado, ideal para desarrollo, pruebas y emulaciones.

#### ¿Para qué sirve Containerlab?
Containerlab permite a los ingenieros de redes y desarrolladores:

- Montar topologías de red complejas en pocos minutos.
- Simular redes en contenedores y crear escenarios de pruebas de redes.
- Crear y probar configuraciones de routers, switches y otros dispositivos de red sin requerir hardware físico.
- Utilizar Infraestructura como Código (IaC) para definir topologías y configuraciones, lo que facilita la replicación, el versionamiento y la colaboración.


### Network Operating System (NOS)

Un sistema operativo de red (Network Operating System, NOS) es un software diseñado para conectar y gestionar múltiples dispositivos y computadoras en una red, permitiendo el intercambio eficiente de recursos entre ellos. Su función principal es asegurar que las interacciones y operaciones entre todos los dispositivos y servicios de la red se realicen de manera efectiva.
Algunas de las funciones que nos provee este tipo de software son:
- Crear y administrar cuentas de usuarios en la red
- Controlar el a acceso de recursos en lared
- Proveer Servicios de comunicación entre los dispositivos y la red
- Monitorear la red
- Configurar y Administrar los recursos en la red.

#### NOS de referencia basados en Linux

- [FRRouting](https://frrouting.org/)
- [OpenBGPD](https://www.openbgpd.org/)
- [Nokia Service Router Linux](https://www.nokia.com/networks/ip-networks/service-router-linux-NOS/)


## Instalación de Containerlab

### Instalar Docker
```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

### Instalar containerlab
```bash
curl -sL https://containerlab.dev/setup | sudo -E bash -s "all"
```

## Comandos básicos de Containerlab

### Iniciar topología
```bash
containerlab deploy -t topology.yml
```

### Destruir topología
```bash
containerlab destroy -t topology.yml
```

### Visualizar topología
```bash
containerlab graph -t topology.yml
```

# Referencias

- https://containerlab.dev/
- https://www.docker.com/
- https://frrouting.org/
- https://www.nokia.com/networks/ip-networks/service-router-linux-NOS/
- https://www.openbgpd.org/
- https://github.com/wbitt/Network-MultiTool
- https://www.kali.org/
- https://github.com/ernestosv73/ipv6seclab
- https://github.com/alejo-guevara/ipv6-workshop

</br>
<p align="center"><strong>Laboratorio de Redes - Facultad de Ingeniería - UNRC</strong></p>