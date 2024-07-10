# Arquiteturas

## Three Tier Architecture

arquitetura em tres camadas: Presentation - Aplication - Data
Cada camada pode ser escalada independetemente, o sistema pode lidar com aumentos de carga escalando apenas a camada que afetada.
Facil de operar, monitorar e debugar.
Cada camada pode ser protegida de forma independente.
Facil de testar e reutilizar codigos.
Geralmente monolitica e atende a sistemas menos complexos.

## Monolito versus Monolito Modular

* Monolito - todo o sistema em um unico codigo ( servidor/ porta ).
* Modular - um sistemas com modulos separados em varios servidor/ porta com comunicação em rede.

PS.: Modular é diferente de microserviço.

## Microserviço

Monolito/Modular sempre opera o mesmo banco de dado ou mesmo contexto. No modular um moculo atualiza o db e o outro ler o db e faz a ação.
No microserviço o frontend conversa com um barramento (bff, gateway, broker, etc..). Cada serviço é independente entre si inclusive com a persitencia em em banco de dado proprio. Cada microserviço realiza sua operação e comunica ao barramento seu resultado e o barramento comunica ao outro microserviço ou o proprio microserviço comunica diretamente ao outro microserviço porém sem contato entre os dbs.

## Container archtecture

cada servidor tem um ou mais container da aplicação que roda em seu proprio ambiente ( dependencias, versões, etc). Tudo controlado por um painel de controle ( servidor que gerencia a movimentação, monitora a usabilidade e capacitadade e balancea os acesso e processo).

* vantagens: portabilidade, eficiencia de recursos, isolamento, escabilidade, deploy e rollback facilidado, organização.

* desvantagens: gestão complicada, dificil monitoramento e logging, ruido dos vizinhos, custos, complexidade de rede, requisitos de microserviços.

## Serveless architecture

Divide os microserviços em funções independentes que não precisar gerenciar um servidor (sem servidor) apenas um sistema tercerizado ( SaaS ) que processe cada um das funções solicitada e gerencie seu proprio servidor que sera armazenada a função em si.

* vantagens: eficiencia de recurso, escabilidade automatica, observabilidade, abstração de recursos de infra, rapido e simples deploy, foco no codigo/negocio, custo.

* desvantagens: complexidade arquitetonica, limitações de tempo e quantidade, observabilidade, falta de custominização, tempo de inicialização, vendor lock-in, custo.
