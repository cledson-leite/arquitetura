# Conceitos Importantes

## Api Gateway Pattern

gerencia rotas, valida contratos, agrega serviços, balancea carga, autentica e autoriza, throttling, logging, tracing, manubulação de errors, tranformação de string, estrategia de deploy, integrar com ferramentas de segurança, reduz consumo do backend preventivo ( 4xx, DDoS), cache.

## Load Balancing Pattern

### Algoritmos de Load Balancing

Round Robin: Distribui as solicitações de maneira sequencial entre os servidores disponíveis.

Least Connections: Direciona as novas solicitações ao servidor com o menor número de conexões ativas.

Hashing: Utiliza um hash da solicitação (por exemplo, IP do cliente) para determinar o servidor que atenderá à solicitação.

Weighted Round Robin: Similar ao Round Robin, mas atribui um peso a cada servidor, distribuindo mais solicitações para servidores mais poderosos.

## EDA - Event Drive Arquitecture

* sync - fluxo de requisição - processamento - resposta feita em cascada onde o processo fica parado a espera da resposta. Tempo de processo é a soma de todos os tempos das etapas mais a latencia.

* async - fluxo de rquisição - processo - resposta feita em paralelo e com pub-sub. Onde o processo recebe uma resposta de recbimento, o processo é feito e envia uma nova mensagem de resposta final. O Tempo de processamento é dividido, a requisição recebe resposta instantanea e a finalização do porcesso leva seu tempo sem impactar no porcesso como um todo.

## Strong Consistency versus Eventual Consitency

* strong - neste modelo, qualquer operação de leitura retorna o resultado mais recenteda operação de escrita. Geralmente o tempo de escrita é maior, pois todas as partições são escritas de formas SYNC.

* eventual - Neste modelo, a resposta de leitura será o retorno persistido no destino da operação. Podendo ser uma versão mais antiga. Geralmente o tempo de operação de escrita é menor, pois só uma partição e atualizada e as outras acontecem de forma ASYNC.

## ACID

* Atomicidade: tudo ou nada. É a caacidade de uma transação que possui N escritores, somente realizar o commit quanto o ultimo escritor finalizar o processo.Ex. Se uma transação transferi 100 reais da conat A para conta B, garante que as duas ações ( debitar de A e credita em B) ocorram completamente ou nenhuma delas.
* Consistencia: a transação deve ser consitente de acordo com seus atribudo e tipos, seguinto as regras. Ex. Se uma conta não pode ter saldo negativo, qualquer transação que tente retirar mais dinheiro que o disponivelserá rejeitada mantendo o banco de dados consistente.
* Isolamento: transações concorrentes são isoladas umas das outras. Ex. dois cliente compram o mesmo produto online ao mesmo tempo. O isolamento garante que cada transação ocorra separatamente, evitando que ambos comprem o ultimo item ao mesmo tempo.
* Durabilidade: após o commit, o dado estará consistente e permanentemente armazenado e disponivel onde deve estar. Ex. após um pedido ser confirmado em um e-commerce, ele é gravado no banco de dados permanentemente, garantido que o pedido não será perdido mesmo que ocorra uma falha no sistema.

## Single Tenant versus Mult Tenant

* Single Tenat:
  * positivo: cliente tem recurso deticado apenas para ele, nada é dividido e é completamente isolado, não precisa se perocupar com Neighbor Noise, personalização por cliente, manutenção mais segura.
  * negativo: manutenção mais demorada, alto custo, necessidade de controles. monitoramento e configuração personalizada.

* Multi Tenat:
  * positivo: recuros compartilhados e isolado a nivel de aplicação, custo otimizado.
  * negativo: manutenção gera impacto em varios clientes, Neighbor Noise,complexo escalonamento para um unico cliente, dificil, isolamento de acesso e personalização.

## Streaming versus Messaging

* Messaging: envio de mensagem entre serviços de forma assincrona com mensagens independentes. Usa os padrões Pub-Sub e Queue. Garante a entrega em diversos niveis incluindo "no minimo uma vez", "no maximo uma vez" ou "exatamente uma vez". É usado em comunicação de microsserviços, em processos assincronos e em negocios baseados em eventos.

* Stream: transmição continua de dados, processados em tempo real como um fluxo. Uma comunicação continua e sequencial, com dados frequentemente dependentes de eventos anteriores. Usa o padrão de streams de dados continuo ( topicos ) com foco menor em garantias de entrega e mais em processo continuo. Usa em monitoramento em tempo real, analise de logs, processamento de eventos de sensores em IoT e sistemas de recomentações em tempo real.

## Consistem Hashing

 Distribui dados uniformemente entre servidores, facilidando a escabilidade.

## Shuffle Sharding

Aumenta a resiliencia dos dados disponibilizando-os em N shards, porém embaralhados.
