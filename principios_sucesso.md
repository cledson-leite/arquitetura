# Principios de sucesso na arquiteura de softwares

1- Planejamento de Capacidade:

    Previção de demanda e planejamentod e capacidade. Estar pronto para momentos de pico. Entregar no mesmo tempo de resposta independente do trafego.

2- Segurança:

    Criptografias, normals, certificados, OWASP, protocolos seguros, mecanismo contra DDoS, XSS e outros.

3- Observabilidade:

    Ter metricas, alarmes, logs e trace de todo fluxo de usuario, mensagem, request e etc.

4- Otimização de custos:

    Depende de todos os outros pilares, porém quão frugal voce estar.

5- Release Engeneering:

    Ter capacidade de atualizar ambientes produtivos com o minimo de impacto possivel. Ter testes automatizados.

6- Operações:

    Como todas as outras habilidades devem ser usadas sem comprometera eficiencia das operações. MTTR, automações, paniel de controles, etc.

7- Confiabilidade:

    Capacidade de estar acima do SLA de posibilidades, ser resiliente, estrategia de backup/restore, estrategis de disaster recovery.

## Ciclo de mudanças de uma arquitetura

1- Avaliação  do "AS_IS":

* Entender as necessidades  do negocio
* Entender o planejamento futuro do negocio
* Entender sobre a arquitetura e como estar resolvendoa necessidade do negocio
* Identifiar Pain Points (incidentes, tempo de entrega, conversas)
* Coletar data Points

2- Definição do "TO_BE":

* Com todos os data points em mãos, identifique o real problema do negocio
* Criar alternativas de "TO_BE" usando boas particas
* Fortaleza com casos de sucesso existentes

3- Execução da Prova de conceitos (PoC):

* Execute uma PoC focado no problema que voce quer resolver
* Se vcoe quer validar seu modelo de arquitetura precisa escrever o codigo com as melhores praticas

4- Testes:

* Execute todos os teste possiveis para validar sua arquitetura
* Se sua arquiteura faz 1000 TPS não considere sucesso se sua poc fizer 1000 TPS

5- Migração oficial:

* Criar plano de migração
* Converter PoC em Produto minimo viavel (MVP)
* Coletar indicadores de sucesso e confirma-los
* Se posivel migra em pequenas levas
* Publica casos de sucesso ou fracasos
