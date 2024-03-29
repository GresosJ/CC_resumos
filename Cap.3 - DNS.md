# Capitulo 3 - DNS

 - Base de dados distribuida implementada numa hierarquia de servidores de nomes;
 - Protocolo da camada de aplicação;

**TLD - Top-Level Domain Servers**
 - Responsaveis por .com, .org, .net, .edu, etc e todos os dominios de topo dos paises .pt, .uk, .fr, etc;

**Servidores DNS autoritativos**
 - Servidores DNS das organizações com autoridade sobre dominio de nomes local e sobre mapeamentos nomes->endereço;
 - Podem conter base de dados original ou copias oficiais da mesma;

**Servidor de nomes local**
 - Pode pertencer á hierarquia;
 - Cada ISP (ISP residencial, empresas, universidades) têm um;
 - Quando um host formula uma interrogação DNS, ele deve ser sempre dirigida ao seu servidor DNS local;
 - Funciona como um proxy, redirecionando a query para a gierarquia quando necessário, designa-se forwarder;
 - Faz caching;

## Resolução de um nome
**Modo iterativo**: servidor contactado responde com o nome do proximo servidor a contactar;

![Modo iterativo](img/ModoIterativo.png)

**Modo recursivo**: coloca o fardo da resolução no servidor de nomes contactado;

![Modo recursivo](img/ModoRecursivo.png)

## DNS resource records (RR)
Formato RR: (name, value, type, ttl)

Type  - A :
 - *name* é o nome de um host:
 - *value* é o endereço IP do host;

Type  - MX :
 - *name* é o nome de um domínio;
 - *value* é o nome do servidor de email associado;

Type  - NS :
 - *name* é o nome de um domínio;
 - *value* é o nome do host do servidor DNS autoritativo para o dominio;

Type  - CNAME :
 - *name* é um alias (nome alternativo) para outro nome canónico, www.dn.pt é na realidade dn.sapot.pt;
 - *value* é o nome canónico (real);

## Protocolo DNS
Duas mensagens (query e reply) exatamente com o mesmo formato;

![Protocolo DNS](img/DNSProtocol.png)