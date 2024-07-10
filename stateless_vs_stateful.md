# Stateless versus Statefull

* Statefull - A aplicação, o banco de dados, o store, o backup, etc ficam no mesmo servidor (disco).

  * Positivo: deburação de codigo mais simples, dados centralizados, geralmente só requer um DNS, comunicação via barramento, monitoração.
  * negativo: escalonamento dificil e só vertical, menor resiliencia, maior complexidade de aplicação, deploy dificuldado.

* Stateless - A aplicação, o banco de dados, o store, o backup, etc ficam em servidor (disco) diferentes. Não armazena estado do sistema.
  * Positivo: facil escalonamento horizontal, aplicação imutavel, Maior resiliencia, menor complexidade de implemntação, manutenção mais simples, eficiencia do deploy e entrega.
  * negativo: repetição de dados, requer complementos, comunicação via rede, monitoração.
