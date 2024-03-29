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

![Tabela de Encaminhamento](img/TabelaEncam.png)

**Tipos de Algoritmos**:
Os algoritmos de encaminhamento podem gerir a informação de duas formas distintas:
 - **Global**:
   - Todos os encaminhadores têm um conhecimento completo da topologia e custo das ligações;
   - Algoritmos de estado das ligações (*Link State-LS*);

 - **Descentralizada**:
   - Os encaminhadores só conhcem os vizinhos a que estão fisicamente/logicamente ligados e o custo das ligações respetivas;
   - O processo de computação é iterativo, havendo troca de informação entre vizinhos;
   - Algoritmos de vetor de distância (*Distance Vector-DV*);

## Algoritmo Link State (LS)

Todos os nós da topologia espalham pela rede informação sobre o estado das suas ligações de forma a construirem a base de dados topologica (usando um metodo de inundação fiavel - **Reliable Flooding**):
 - Inicialmente necessitam de coonhecer apenas os seus vizinhos diretos, para quem enviam a identificação de todos os outros seus vizinhos, bem como o custo das ligações respetivas;
 - Um nó/encaminhador ao receber esta informação atualiza a sua base de dados topológica e reenvia a informação para todos os seus vizinhos;
 - Ao fim de algum tempo todos os nós possuem um conhecimento completo da topologia e dos custos de todas as ligações.

Com esta informação, em cada nó/encaminhador, é executado um algoritmo de descoberta dos caminhos de custo mínimo, normalmente o algoritmo de *Dijkstra*.

![Tabela do Link State](img/TabelaLS.png)

### Escalabilidade e Oscilações
 - Esforço/Complexidade do algoritmo para N nós da rede é O(N2), portanto, a implementação dos algoritmos LS têm alguns problemas de escalabilidade;
 - Na presença de métricas assimétricas que espelham o estado da rede (por exemplo, se a métrica refletir a carga nas ligações) o cálculo da melhor rota sofre oscilações (ver exemplo abaixo em que a métrica reflete a quantidade de dados transmitidos).

![Escalabilidade e Oscilações do LS](img/IssueLS.png)

## Algoritmo Distance Vector (DV)

Ao contrario dos algoritmos LS, os algoritmos DV não usam informação global, são distribuidos, iterativos e assincronos:
 - Cada nó recebe informação de encaminhamento de algum dos seus vizinhos diretos, recalcula a tabela de encaminhamento e envia essa informação de encaminhamento de volta;
 - O processo continua até que não haja informação de encaminhamento a ser trocada entre nós vizinhos, i.e., até que a informação de encaminhamento convirja;
 - Não exige que os nós estejam sincronizados uns com os outros em relação à topologia completa da rede.

### Equação de Bellman-Ford
Seja c(x,v) o custo do caminho entre x e v adjacentes e Vx o grupo de todos os nós vizinhos/adjacentes a x, então o custo do melhor caminho de x para y (ou a rota de custo mínimo entre o nó x e o nó y) é dado por:

dx(y) = min { c(x,v) + dv(y) }, para todos os v em Vx

Sabendo que:
 - N’ é o grupo de todos os nós da rede e que x є N’
 - Vx é o grupo de nós adjacentes/vizinhos de x
 - O nó x conhece o custo para todos os seus vizinhos Cx  - { c(x,v) }, v є Vx
 - O custo do melhor caminho de x para y é dado por dx(y)  - min { c(x,v) + dv(y) }, y є N’, v є Vx
 - Seja o custo do melhor caminho de x para y expresso por Dx(y), y є N’
 - O nó x mantém um vetor de distâncias próprio expresso por DVx  - { Dx(y) }, y є N’
 - O nó x também mantém os vetores de distâncias dos seus vizinhos DVv  - { Dv(y) }, y є N’, v є Vx
 - Cada nó x envia periodicamente a sua estimativa DVx a todos os seus vizinhos
 - Quando um nó x recebe um novo DVv de um dos seus vizinhos atualiza o seu próprio vetor DVx
 - Em condições normais, a estimativa de Dx(y) converge para o valor de dx(y) ao fim de algum tempo
 - A troca contínua dos DV mantém a convergência

![Tabela do Distance Vector](img/TabelaDV.png)

### Problemas do DV
 - **Contagem ao infinito**: o algoritmo DV não consegue distinguir entre uma rota inexistente e uma rota com custo infinito;
 - **Oscilações**: o algoritmo DV pode sofrer de oscilações quando as métricas são assimétricas (por exemplo, se a métrica refletir a carga nas ligações);
 - **Partição da rede**: o algoritmo DV não consegue lidar com partições da rede.

Para isso existem duas técnicas:
 - **Split Horizon**: Se Y aprendeu rota para X com Z, nunca ensina essa rota a Z!
 - **Poison Reverse**: Se Y aprendeu rota para X com Z, então “mente” a Z anunciando que o custo da sua rota para X é igual a infinito!

O "Split Horizon" é uma técnica de roteamento que impede um roteador de anunciar informações de rota de volta à interface de onde as aprendeu. Isso evita loops na rede. Já o "Poison Reverse" ocorre quando um roteador informa ao vizinho que a rota para um destino é inalcançável, atribuindo um custo infinito. Ambas as práticas visam evitar loops em redes de roteamento dinâmico.

## Reflexões finais comparativas – LS vs DV

 - **Sobrecarga introduzida pela mensagens de controlo**:
   - Nos algoritmos LS todos os nós necessitam de conhecer o custo de todas as ligações, por isso, sempre que o custo de uma ligação muda, uma mensagem com o novo custo tem que ser enviada para todos os nós para que todos conheçam a nova topologia;
   - Nos algoritmos DV a mudança do custo de uma ligação só provoca o envio de mensagens se resultar na mudança da tabela de encaminhamento.
 - **Convergência**:
   - Os algoritmos LS convergem mais depressa mas, com alguns tipos de métricas dinâmicas estão sujeitos a oscilações;
   - Os algoritmos DV convergem lentamente, podem apresentar ciclos enquanto não convergem, e é necessário incluir mecanismos para resolver o problema dos loops de eventuais contagens até ao infinito.
 - **Robutez**:
   - Nos algoritmos LS, cada encaminhador calcula a sua tabela de encaminhamento usando a base de dados topológica, de forma independente dos outros encaminhadores. Isso confere a este tipo de algoritmos uma robustez maior.
   - Nos algoritmos DV, se algum encaminhador estiver a calcular mal a sua tabela de encaminhamento, os erros cometidos vão-se propagar aos outros encaminhadores da topologia.
 - **Recursos computacionais**:
   - Os algoritmos LS são mais exigentes do que os algoritmos DV, quer em termos de memória (base de dados topológica vs tabela de distâncias), quer em termos de capacidade de processamento.