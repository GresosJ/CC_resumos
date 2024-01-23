# Capitulo 4 - Segurança de Redes

## Propriedades de uma comunicação segura

 - **Confidencialidade**: só o emissor e o rector indicado devem "perceber" o conteúdo das mensagens;
 - **Autenticação**: emissor e recetor pretendem confirmar a identidade um do outro;
 - **Integridade da mensagem**: emissor e recetor querem garantir que a mensagem não foi alterada (no percurso pela rede, antes do envio ou depois da receção) sem que tal posa ser imediatamente detetado;
 - **Não repudio**: evidencias que impeçam intervenientes de negar comunicação;
 - **Acesso e Disponibilidade**: serviços devem estar acessiveis e com disponibilidade para os seus utilizadores;

## Criptografia
**Criptografia de chave simetrica**: emissor e recetor usam a *mesma* chave;

**Criptografia de chave pública**: uma chave para cifrar (publica) outra para decifrar (privada);

### Criptografia de chave simetrica
A criptografia de chave simétrica envolve o uso de uma única chave compartilhada entre remetente e destinatário para cifrar e decifrar mensagens. Ambas as partes utilizam a mesma chave para garantir a confidencialidade dos dados, exigindo um método seguro de compartilhamento dessa chave.

![Criptografia de chave simetrica](img/Chavesimetrica.png)

### Criptografia de chave publica
A criptografia de chave pública utiliza um par de chaves: uma pública, conhecida por todos, e outra privada, mantida em segredo. Mensagens cifradas com a chave pública só podem ser decifradas pela chave privada correspondente, fornecendo um método seguro para comunicação confidencial e autenticação.

![Criptografia de chave publica](img/Chavepublica.png)