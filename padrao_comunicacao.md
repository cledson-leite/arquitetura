# Padrões de comunicação e Transação

## Pub - Sub

### *one to many*

Um produtor escreve uma mensagem, envia para o topico no broker que distribuir para todos os escritos lerem.

* Publica a mesma mensagem em diversos escritos
* Multiplos consumitores recebem a mesma mensagem
* Ajuda no desacoplamento de serviços
* Muito usado para notificações

## Queue

### *many to one*

Um ou mais produtores escreve uma ou varias mensagens, envia para a fila no broker e um consumidor ouvi ( busca ) essas nesnsagens. Caso aja dois consumidores para a mesma fila, eles concorem entre si qual mensagen um recebe e o outro não.

* Apenas um consumidor procesa cada mensagem
* Mantem historico se necessario
* Disaster Discovery
* Ordenação se necessario (FIFO)
* Ajuda no desacoplamento de serviços

## Messaging Fanout Pattern

### *junção do Pub/sSub com Queue*

Um  produtor escreve uma mensagem, envia para um topico no broker, o topico envia essa mensagem para uma ou mais filas escritas no topico, um consumidor de cada fila ouve (busca) essa mensagem.
Vantagens:

* Tira complexidade do fluxo da aplicação
* Tem um backlog e pode ser processado o que não foi consumido
* Paraleliza a execução de mensagens otimizando o tempo
* Escalabilidade apenas do que realmente precisa ser "quae em tempo real"
* Desaclopa serviços
* Melhora a integração e/o comunicação entre serviços

Desvantagens:

* Gera custos
* Precisa de matiridade na observabilidade
* Mais uma habilidade e/ou ferramenta externa para o projeto

## Saga - Coreagraphy Pattern

### *fluxo do caminho da mensagem descentralizado e sem visão completa da jornada*

Cada aplicação tem suas regras de fluxo que define qual o porximo passo sera dado. Todas a plicações devem esta em sicronia ( coreografada ) com qual passo será dado apos receber e processar a mensagem.

Vantagens:

* Autonomia completa pois cada time só sabe as regras do proximo passo
* Escabilidade já que são independentes
* Não tem um unico ponto de falha
* Deploy tem um raio de impacto menor

Desvantagens:

* Cada serviço tem um punhado de regras de fluxo junto com regras de negocio
* Cada serviço conhese apenas sua origem e seu destino e não tem uma visao completa do negocio
* Complexidade de manutenção pois está descentralizado
* Dificil observabilidade e investigação

## Saga - Orchestration Pattern

### *fluxo do caminho da mensagem centralizado e com visão completa da jornada*

A aplicação envia a transação para um orquestrator que inicia o fluxo enviado mensagem especifica para cada serviço e esperando sua resposta para seguir o proximo passo.

Vantagens:

* Reduz complexibilidade
* Observabilidade, monitoramento e rastreo
* Entendimento do fluxo de negocio

Desvantagens:

* Unico ponto de falha
* Ter um time exclusivo para o orquestrator com visão do fluxo completo

## Api Composition Pattern

### *Um agregador de chamadas APIs  de varias outras aplicações*

Um serviço recebe um chamada de api, decodifica qual apis é necessaria para ter a resposta para aquela chamda inicial e gerencia essas chamadas a cada api necessaria.

Vantagens:

* Redux complexibilidade para o front
* Gera abstração do backend
* Menor tempo de latencia
* reduz a necessidade de sobrecarga de comunicação
* Simplificação de segurança
* Pode conter regras de negocio especificas

desvantagens:

* Unico ponto de falha
* Exclusividade de um time para esse serviço
* Novas habilidade e/ou mais um passo paar entregar
