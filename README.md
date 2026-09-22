# Infraestructura de Red Empresarial - Cisco Packet Tracer

## Descripción

Diseño e implementación de una infraestructura de red empresarial utilizando Cisco Packet Tracer. El proyecto simula la infraestructura de una empresa con diferentes departamentos, segmentación mediante VLANs, enrutamiento inter-VLAN, servicios de red centralizados y controles de acceso entre departamentos.

## Objetivos

* Diseñar una red empresarial segmentada.
* Implementar VLANs para separar los diferentes departamentos.
* Configurar comunicación entre VLANs mediante Router-on-a-Stick.
* Implementar DHCP centralizado para la asignación automática de direcciones IP.
* Implementar servicios DNS y FTP.
* Configurar enlaces troncales entre los dispositivos de red.
* Implementar ACLs para controlar la comunicación entre departamentos.
* Validar la conectividad y funcionamiento de los servicios mediante pruebas.

## Arquitectura de red

La infraestructura está compuesta por:

* 1 router Cisco
* 2 switches Cisco
* 4 departamentos
* 3 servidores
* 1 VLAN dedicada a servidores

### Departamentos

| VLAN | Departamento   | Red               |
| ---: | -------------- | ----------------- |
|   10 | Administración | `192.168.10.0/24` |
|   20 | RR.HH.         | `192.168.20.0/24` |
|   30 | Ventas         | `192.168.30.0/24` |
|   40 | Soporte        | `192.168.40.0/24` |
|   50 | Servidores     | `192.168.50.0/24` |

## Direccionamiento

Cada VLAN utiliza su propia subred IPv4 y tiene como gateway la subinterfaz correspondiente del router.

| VLAN | Gateway        |
| ---: | -------------- |
|   10 | `192.168.10.1` |
|   20 | `192.168.20.1` |
|   30 | `192.168.30.1` |
|   40 | `192.168.40.1` |
|   50 | `192.168.50.1` |

## Servicios implementados

### DHCP

Se implementó un servidor DHCP centralizado en:

`192.168.50.2`

El router utiliza `ip helper-address` para reenviar las solicitudes DHCP de las diferentes VLANs hacia el servidor.

### DNS

Servidor DNS:

`192.168.50.3`

Se configuró el registro:

`ftp.empresa.local → 192.168.50.4`

Esto permite acceder al servidor FTP mediante un nombre en lugar de utilizar directamente su dirección IP.

### FTP

Servidor FTP:

`192.168.50.4`

Se configuró autenticación mediante usuario y contraseña y se verificó el acceso desde los diferentes departamentos.

## Seguridad y control de acceso

Se implementó una ACL extendida para controlar la comunicación entre departamentos.

La política establecida permite:

* Administración → todos los departamentos.
* Soporte → todos los departamentos.
* RR.HH. → Administración, Soporte y Servidores.
* Ventas → Administración, Soporte y Servidores.

Se bloqueó específicamente la comunicación entre:

`RR.HH. ↔ Ventas`

La configuración fue validada mediante pruebas de conectividad.

## Pruebas realizadas

Se realizaron pruebas para verificar el funcionamiento de la infraestructura:

* ✅ Asignación automática de direcciones IP mediante DHCP.
* ✅ Comunicación entre VLANs.
* ✅ Comunicación con la VLAN de servidores.
* ✅ Resolución DNS mediante `nslookup`.
* ✅ Resolución de `ftp.empresa.local`.
* ✅ Acceso al servidor FTP mediante dirección IP.
* ✅ Acceso al servidor FTP mediante nombre DNS.
* ✅ Comunicación entre los departamentos permitidos.
* ✅ Bloqueo de comunicación entre RR.HH. y Ventas.
* ✅ Verificación de enlaces troncales.
* ✅ Verificación de interfaces y subinterfaces del router.

## Tecnologías utilizadas

* Cisco Packet Tracer
* IPv4
* VLAN
* IEEE 802.1Q
* Router-on-a-Stick
* DHCP
* DNS
* FTP
* ACL
* TCP/IP
* Subnetting

## Autor

**Evans Elian Sierra Meliano**

Proyecto desarrollado como práctica de infraestructura de redes y administración de servicios de red.

