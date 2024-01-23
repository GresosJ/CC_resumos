# Tabelas de Encaminhamento

**Reenvio (forwarding) num encaminhador**:
 - Utiliza a tabela de reenvio previamente preenchida pelos protocolos de encaminhamento ou pelo administrador;
 - Procura na tabela, para um dado "destino", o "proximo salto" e o "interface de saida";
 - Comuta o pacote pelo interface respetivo, encapsulando-o numa trama de acordo com o tipo de interface;

**Encaminhamento (routing)**:
 - Preenche a tabela de encaminhamento com a(s) melhor(es)  rotas para as redes de destino (classfull) ou para um conjunto de prefixos de endereços (classless);
 - Pode ser um processo manual, feito pelo administrador- encaminhamento estático;
 - Ou, no caso mais comum, um processo automatico resultante da operação de um protocolo de encaminhamento dinâminaco;

## Routers - Plano de Controlo Centralizado/Distribuido

Os roteadores podem ser classificados quanto ao plano de controle em centralizados e distribuídos. Em um plano de controle centralizado, as decisões sobre o encaminhamento de pacotes são tomadas por um único ponto central, conhecido como controlador. Este controlador coordena as informações de roteamento e toma decisões para toda a rede. Já em um plano de controle distribuído, cada roteador individual é responsável por tomar suas próprias decisões de encaminhamento com base nas informações locais disponíveis, resultando em uma abordagem mais descentralizada e adaptável à escala da rede. O modelo escolhido impacta o desempenho, a escalabilidade e a resiliência do sistema de roteamento.

## Algoritmo de Encaminhamento/Routing

Dada uma topologia de rede (um conjunto de encaminhadores com ligações de rede a interligá-los), representável como um grafo com pesos nos arcos/ligações dos seus nós, o objetivo do algoritmo de encaminhamento é determinar um “bom” caminho desde o nó fonte/origem até ao nó destino.

**A topologia de rede é um grafo em que**:
 - Os nos do grafo são os encaminhadores/routers;
 - Os arcos do grafo são as ligações/links da rede;
 - O custo das ligações pode ser estabelecido em função de varios criterios (individualmente ou em conjunto), como por exemplo, o atraso, a capacidade/ritmo nominal, do nivel de congestão, do custo operacional, da distancia, etc.;
 - Um "bom" caminho geralmente significa o caminho que minimiza ou maximiza o seu custo total;

![Tabela de Encaminhamento](TabelaEncam.png)