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

