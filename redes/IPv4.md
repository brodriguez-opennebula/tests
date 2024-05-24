# IP v4

- Internet protocol: Capa 3 del modelo OSI y/o UNIX
- Se encarga de mover info entre redes
- Asigna una dirección lógica (dirección IP) de 32 bits. Sí, la de toda la vida
- Las direcciones IPs tienen dos partes:
  - RED: conjunto de máquinas
  - HOST: Máquina

## Máscara de red
La máscara de red define cuántos bits de los 32 son significativos para la red, y el resto, para el host
Se hace una AND bit a bit entre la máscara y la dirección para saber qué es qué 

Definición "de estar por casa":
- Pensar en binario (32 bits)
- Es, en vocabulario técnico, _un chorro de unos_. Se puede escribir de dos maneras:
  - Forma canónica: 10000000.0.0.0 = 128.0.0.0 ; 11111111.11111111.11111111.0 = 255.255.255.0
  - Forma CIDR: 10000000.0.0.0 = /1 ; 11111111.11111111.11111111.0 = /24 
La forma CIDR es más corta y hace que parezca que sabes más (una máscara barraveinticuatro, una máscara barradieciséis)

_IMPORTANTE_: 
- La primera dirección de cada red (ACABA EN 0) se utiliza para identificar TODA la red
- La última dirección de cada red (ACABA EN 1) se utiliza para identificar a TODOS los hosts (broadcast)

Por ejemplo, la red doméstica estándar:
Dirección 192.168.1.16/24 -> `11000000.10101000.00000001.00010000`
- Máscara de red: 255.255.255.0 -> `11111111.11111111.11111111.0`

Hacemos la AND:
```
IP ADDRESS: 11000000.10101000.00000001.00010000
NETMASK   : 11111111.11111111.11111111.00000000
            ---------------------------XXXXXXXX -> Todo lo que hay antes del 1 es red
NETWORK   : 11000000.10101000.00000001.00000000 -> Dirección de la red
BROADCAST : 11000000.10101000.00000001.11111111 -> Dirección de TODOS los hosts (broadcast)
```

Si pasamos de binario a decimal tenemos:

```
IP ADDRESS: 192.168.001.016
NETMASK   : 255.255.255.000
            ---.---.---.XXX 
NETWORK   : 192.168.001.000 -> Dirección de la red
BROADCAST : 192.168.001.255 -> Dirección de TODOS los hosts (broadcast)
```

### Tamaño de la red

Cuando definimos la red con una máscara de tamaño `/M` tenemos un número máximo de hosts real `(2^(32-M))-2`.
El 2 son las direcciones de red y de broadcast, esos no se pueden usar (por tanto, una máscara `/31` es absolutamente inútil)
En el ejemplo anterior: `(2^(32-24))-2 = 255-2 = 253 hosts`. Ese es el número máximo de hosts que se pueden tener
en la típica red estándar de casa.

### Rangos de red privados

Hay rangos de red privados para tamaños estándar de máscara:

Clase A: Máscara /8. Desde `10.0.0.0/8` hasta `10.255.255.255/8`
Clase B: Máscara /16. Desde `172.16.0.0/12` hasta `172.31.255.255/12`
Clase C: Máscara /24. Desde `192.168.0.0/24` hasta `192.168.255.255/24` -> Aquí es donde están la gran mayoría de routers domésticos

## Formato del paquete

`https://upload.wikimedia.org/wikipedia/commons/6/60/IPv4_Packet-en.svg`
