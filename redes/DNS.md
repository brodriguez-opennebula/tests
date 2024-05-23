# DNS

- Domain name system: resolución de nombres de dominio.
- Se puede considerar una "traducción" (resolución) de nombres a IPs...
- ... y viceversa (reverse DNS)
- Dos tipos de servidor
  - Authoritative: Resuelve de manera final. Por ejemplo, el servidor de .com es autoritativo 
  - Recursive: Pasa la consulta a otro servidor (cachea las entradas). Buscaría la entrada global
- Puertos 53 UDP y TCP
  - 53 UDP para las peticiones de resolución
  - 53 TCP para la replicación entre servidores
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
    .org --> .duckdns
    .duckdns --> exampledomain
    .duckdns --> midominiopersonal
    .es --> .segsocial
```

- Software:
  - bind: es el "estándar"
  - otros: unbound, knot, dnsmasq (recursive, sirve más como caché)

## Dynamic DNS

Hay varios servidores de DNS gratuitos que permiten registrar una máquina en su dominio. 
Funcionan haciendo una petición (con token), detectan la IP que la hace (o permiten decir cuál es)  y la agregan automáticamente. Tardan un tiempo en propagar la actualización a los root dns (siempre se dice "un par de horas")

El más sencillo es https://www.duckdns.org/ , permite 5 dominios `.duckdns.org` gratis. La petición sería `https://www.duckdns.org/update?domains=[DOMINIO]&token=[TOKEN]&ip=` (autodetecta la IP con la que se sale fuera o deja ponerle una).

OJO, con esto se llega al router! Luego hace falta abrir (redirigir) puertos en el router para poder entrar dentro de la máquina que haga falta.

