# Padrões de armazenamento de dados

## Change Data Capture (CDC) Pattern

### *Uma mudança de um sistema é capturado e adicionado ou atualizado em outro alvo*

A requisição de alterar o banco de dado acessa o banco ao receber o retorno encia uma mensagem para fila que é consumida pelos conectores dos bancos de dados que precisa ser atualilzado.

Vantagens:

* Baixa Latencia de propagação
* Retira a garantia de consistencia do codigo
* Simplifica a replicação

Desvantagem:

* Eventual Consisten
* Limitação de compatibilidade
* Mais uma habilidade e/ou ferramenta

## Transition Outbox Pattern

### *Como garantir atomicamente consistencia entre dois destinos*

Ao transacionar um dado no banco primeiro se criar um tabela transitoria que salva esse dado e fica esperando uma ordem para tranferi-lo para tabela permanete, caso essa ordem não chegue em X tempo essa transação é cancelada e o dado removido sem tranferir para o permanente.

Vantagem:

* Garante atomicidade em duas base de dados
* Evita regsitro desnecessario no banco principal
* Mais simple que event sourcing

Desvantagem:

* Dublicidade de dados dobrando o espaço de banco de dados

## CQRS - Command Query Responsability Segregation

### *Separação fisica entre comandos que modificam o banco de dados da requecisão que apenas ler o dados*

O comando de alteração do DB e processado e após finalizar envia uma mensagem para o db de requisições atualizando o mesmo.
Ao receber um requisição de leitura chega deve ser lido do db de requisição.

Vantagens:

* Evita concorencia entre escrever e ler
* Otimiza tempo de resposta
* Resiliencia

 Desvantagens:

* Custo
* Eventual Consistency

## Database Sharding Pattern

### *Divide dados em varios bancos para melhorar perfomarce e escabilidade, distribuindo a carga entre serviços*

O comando de alteração da base é recebido. Esses dados recebe um hash limitado entre 0 e 100 (porcentagem de balanceamento) depois é enviado para um mapping que determina em qual db aquele dado pertende e por ultimo altera o db correspondente. No caso de um depe atingir seu limite e for necessario redividir se chama um serviço de painel de controle determina qual tamanho deve dividir, cria um novo db e envia para o mapping a nova divisão dos db. Ja a requisição de leitura ja vai direto para o db que foi apontado.

Vantagens:

* Microgerenciamento de acesso por tabelas
* Delegação de regra para dividir e conquistar
* Melhora na peformance
* Redução do impacto do "raio de exploção"
* Escalabilidade horizontal nos DBs

Desvantagens:

* Pode limitar o crescimento de novos dados
* Manutenções e alterações complexa
* Possibilidade de remanejamento de dados na manutenção
* Manter um consitent hash para facilitar o mapeamentodas tabelas ou dbs

## Cache Aside Pattern

### *Carrega dados no cache sob demanda: se ausente, busca no db, depois colaca no cache e retorna*

A requisição de leitura primeiro é lançado no cache, caso ache retorna e não chama o db. Caso não encontre, chama o banco de dado, a resposda desse é colocado em cache e depois retorna. Na segunda chamada ira encontra-lo no cache.
