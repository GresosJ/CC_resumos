# Capitulo 2 - HTTP

## Como funciona?
HTTP é um protocolo de aplicação que roda sobre o protocolo de transporte TCP. O HTTP define a estrutura das mensagens trocadas entre o cliente e o servidor, bem como ações que devem ser tomadas por ambos os lados. O HTTP é um protocolo sem estado, ou seja, não mantém informações sobre as requisições anteriores. Cada requisição é tratada de forma independente, sem relação com as requisições anteriores. O HTTP é um protocolo orientado a transações, ou seja, cada requisição/resposta é tratada como uma transação independente.

### HTTP - Não persistente
 - Só pode ser enviado no máximo um objeto web por cada conexão TCP;
 - O HTTP 1.0 utiliza o HTTP não persistente;
 - Minimo de 2 RTT/objeto;
 - Exige mais recursos do S.O;
 - Alguns browsers abrem várias conexões TCP em paralelo para pedirem vários objetos referidos no mesmo objeto;

### HTTP - Persistente
 - Podem ser enviados múltiplos objeyos web por cada ligação estabelecida entre o cliente e o servidor;
 - O HTTP 1.1 utiliza, por defeito, o HTTP persistente;
 - Servidor mantém conexão TCP aberta;
 - Com ou sem estrtégia de pipelining;

| Sem Pipelining | Com Pipelining |
|:---:|:---:|
| O cliente envia um novo pedido apenas quando recebe a responta ao anterior | Modo por defeito no HTTP/1.1 |
| No cenario mais otimista consome-se um RTT por cada objeto | O cliente envia os pedidos assim que os encontrar no objeto referenciador |
|  | No cenario mais otimista consome-se um RTT para todos os objetos |