# Padrões de Resiliencia, Escalabilidade e Infraestrutura

## Circuit Breaker Pattern

### *previni falha em cascata, isolando serviços problematicos para manter a estabilidade do sistema*

Fecha a chamadas para um serviço que esta quebrado e continua o processo com os demais serviços com um retorno padrão deste serviço quebrado. Em x tempos ele começa a enviar novas memsagens em pequenas escala para ver se esta funcionando, caso esteja, volta ao fluxo normal, caso não votar a fechar e esperar x tempo.

Vantagens:

* Aumento de resiliencia e estabilidade
* Evita efeito domino
* Não precisa pelo timeout do serviço para conyinuar o porcesso
* Pode retornar um cache statle ou mensagem de erro para esse serviço
* Evita tentativa que será frustada

Desvantagens:

* Mais uma camada de complexibilidade
* Exige um monitoramento eficiente e granulado
