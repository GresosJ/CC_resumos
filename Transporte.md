# Capitulo 1 - Nível de Transporte

Os serviços e protocolos de transporte são responsaveis por estabelecer uma conexão lógica entre aplicações executadas em sistemas terminais diferentes. Esses protocolos são executados nos sistemas terminais, onde o emissor divide a mensagem gerada pela aplicação em segmentos, que são transmitidos á camada de rede. No lado do receptor, os diferentes segmentos são reunidos para formar a mensagem original, que é então entregue à aplicação correspondente. Na Internet, dois dos principais protocolos de transporte são o TCP (Transmission Control Protocol) e o UDP (User Datagram Protocol). O TCP oferece uma comunicação confiável e orientada à conexão, enquanto o UDP proporciona uma comunicação mais rápida, porém menos confiável e sem a necessidade de estabelecer uma conexão prévia.

## Multiplexação e Demultiplexação

![Multiplexação e Desmultiplexação](img/multi.png)

 - Desmultiplexagem é efetuada pelo sistema terminal destino ao receber um datagrama IP.
 - Cada datagrama contem um segemento TCP ou UDP.
 - Cada segmento possui a identificação da porta de origem e da porta destino.
 - O sistema terminal usa os endereços IP e os numeros de porta para encaminhar o segmento para o socket correto.

## Protocolo UDP - User Datagram Protocol

Funções do UDP:
 - Protocolo de transporte fim-a-fim não confiável;
 - Orientado ao datagrama;
 - Atua como uma interface da aplicação com o IP para multiplexar e desmultiplexar tráfego;
 - Usa o conceito de porta/número de porta;
 - Utilizado em situações que não justificam o TCP, ou quando as aplicações querem controlar o fluxo de dados e gerir erros de transmissão diretamente;
 
![UDP](img/desUDP.png)

Uma aplicação pode escolher o UDO devido a vários motivos:

 - **Maior controle sobre o envio dos dados:** A aplicação tem autonomia para decidir quando e como enviar ou reenviar dados, sem depender do protocolo de transporte.

 - **Fuga ao controle de congestão do TCP:** UDP não está sujeito às regras rigorosas de controle de congestão do TCP, permitindo à aplicação determinar a taxa de envio de dados.

 - **Controle sobre o tamanho dos dados enviados:** A aplicação decide a quantidade de bytes a enviar em cada transmissão.

 - **Ausência de estabelecimento e terminação de conexão:** Não é necessário criar ou encerrar uma conexão antes da transmissão de dados, acelerando a comunicação.

 - **Ausência de manutenção de informação de estado por conexão:** Não é preciso manter informações de estado por conexão, simplificando o processo.

 - **Menor overhead por pacote:** O cabeçalho UDP é mais leve, com apenas 8 bytes, reduzindo a sobrecarga em comparação com o TCP.


## Protocolo TCP - Transmission Control Protocol

Funções do TCP:
 - Protocolo de transporte fim-a-fim confiável;
 - Orientado à conexão;
 - Cada conexão é identificada por um par de sockets;
 - Uma conexao é um circuito virtual entre portas de aplicações;
 - Multiplexa os dados de várias aplicações através de numero de porta;
 - Efetua controlo de erros, controlo de fluxo e controlo de congestão;

| Ação            | Emissor (Aplicação)               | Camada de Rede | Recetor (Aplicação)                |
|-----------------|-----------------------------------|-----------------|------------------------------------|
| Iniciar         | Aplicação A                       | -               | Aplicação B                        |
| Segmentação     | Aplicação A divide a mensagem      | -               |                                    |
|                 | em segmentos e envia para a        |                 |                                    |
|                 | camada de rede                      |                 |                                    |
| Transmissão     | Camada de Rede envia os segmentos | -               |                                    |
| Receção         | -                                 | Camada de Rede | Recebe os segmentos da camada de   |
|                 |                                   |                 | rede e os entrega à aplicação B    |
| Reagrupamento   | -                                 |                 | Aplicação B reagrupa os segmentos  |
|                 |                                   |                 | para reconstruir a mensagem        |