# DNS

- Domain name system: resolución de nombres de dominio.
- Se puede considerar una "traducción" (resolución) de nombres a IPs...
- ... y viceversa (reverse DNS)
- Puertos 53 UDP y TCP
  - Puerto 53 UDP para las peticiones de resolución
  - Puerto 53 TCP para la replicación entre servidores
- Existen diferentes tipos de entradas/registros (records). Las más relevantes
  - A: Entrada para registros de tipo IPv4
  - AAAA: Entrada para registros de tipo IPv6 
  - CNAME: Alias (puede apuntar a otros registros)
- NO ES SEGURO. Para agregar seguridad existen varios mecanismos
  - DNS over HTTPS
  - DNS over TLS
  - DNS leak: En algunos casos porque el tráfico puede ir por un túnel seguro 
    pero se pueden hacer las peticiones DNS por un canal inseguro

- Funciona de forma jerárquica
``` mermaid
stateDiagram-v2
    [*] --> .com
    [*] --> .org
    [*] --> .es
    .com --> .google
    .google --> mail
    .google --> drive
    .org --> .wikipedia
    .wikipedia --> www
    .wikipedia --> media
    .es --> .segsocial

```

