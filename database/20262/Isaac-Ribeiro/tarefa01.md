# Tarefa 01 - Conceitos de BD, ACID e SGBD

## Q1. O que é um Banco de Dados e o que é um SGBD? Exemplos.

Um **Banco de Dados (BD)** é um conjunto organizado de dados relacionados entre si,
armazenados de forma estruturada para representar informações sobre um domínio do
mundo real. O objetivo é permitir que
esses dados sejam armazenados, consultados, atualizados e compartilhados de forma
eficiente e confiável.

Um **Sistema Gerenciador de Banco de Dados (SGBD)** é o software responsável por
criar, manter e controlar o acesso ao banco de dados. Ele fica entre as aplicações
e os dados propriamente ditos, oferecendo funcionalidades como: definição da
estrutura dos dados (schema), linguagens de consulta (ex.: SQL), controle de
concorrência, segurança, backup/recuperação e garantia das propriedades ACID.

**Exemplos:**

| Exemplo de uso do Banco de Dados | SGBD utilizado |
|---|---|
| Banco de dados de um e-commerce | PostgreSQL, MySQL |
| Banco de dados de uma rede social | MongoDB (NoSQL) |
| Sistema bancário | Oracle Database, SQL Server |
| Aplicativo mobile local | SQLite |
| Cache/sessões de alta performance | Redis |

## Q2. Principais problemas de usar Sistemas de Arquivos para armazenar dados

Antes dos SGBDs, os dados eram armazenados diretamente em arquivos manipulados por
programas. Isso trazia vários problemas, entre eles:

- **Redundância e inconsistência de dados**: o mesmo dado pode ser repetido em
  vários arquivos por aplicações diferentes; se um for atualizado e outro não,
  os dados ficam inconsistentes.
- **Dificuldade de acesso aos dados**: qualquer nova forma de consulta exige
  escrever um novo programa específico.
- **Isolamento dos dados**: os dados ficam espalhados em arquivos com formatos
  diferentes, dificultando integração.
- **Problemas de integridade**: regras de negócio (ex.: "saldo não pode ser
  negativo") precisam ser codificadas manualmente em cada programa, sem garantia
  centralizada.
- **Problemas de atomicidade em falhas**: se o sistema falhar no meio de uma
  operação, não há garantia de que o arquivo fique em um estado consistente.
- **Anomalias de acesso concorrente**: quando múltiplos usuários/programas
  acessam o mesmo arquivo ao mesmo tempo, podem ocorrer condições de corrida e
  sobrescrita de dados.
- **Problemas de segurança**: é difícil definir permissões refinadas (quem pode
  ler/escrever o quê) apenas com permissões de arquivos do sistema operacional.

## Q3. Propriedades ACID (com exemplo de transferência bancária)

Considere uma transferência de R$100 da **Conta A** para a **Conta B**.

### Atomicidade
A transação é tratada como uma unidade indivisível: ou todas as suas operações
são executadas, ou nenhuma é. Na transferência, isso significa debitar da Conta A
**e** creditar na Conta B. As duas ações acontecem juntas ou nenhuma acontece.

*Sem atomicidade*: se o sistema falhar depois do débito e antes do crédito, o
dinheiro "desaparece". Sai da Conta A mas nunca chega à Conta B.

### Consistência
A transação leva o banco de dados de um estado válido para outro estado válido,
respeitando todas as regras/restrições definidas (saldo não pode ficar negativo,
soma total do dinheiro no sistema deve se manter, etc.).

*Sem consistência*: uma transferência poderia deixar o saldo de uma conta negativo
além do limite permitido, ou fazer com que o total de dinheiro do banco "aumente"
ou "diminua" sem explicação, violando as regras de negócio.

### Isolamento
Transações concorrentes não devem interferir umas nas outras; o resultado deve
ser equivalente a executá-las em alguma ordem sequencial. Se duas transferências
envolvendo a Conta A acontecem ao mesmo tempo, uma não deve enxergar um estado
"parcial" da outra.

*Sem isolamento*: dois débitos simultâneos na mesma conta poderiam ler o mesmo
saldo inicial antes de qualquer atualização e ambos descontarem o valor a partir
do saldo antigo, fazendo a conta perder menos dinheiro do que deveria (ou permitir
saldo negativo indevido).

### Durabilidade
Uma vez que a transação é confirmada, suas alterações persistem mesmo em
caso de falhas subsequentes.

*Sem durabilidade*: o sistema poderia confirmar a transferência para o cliente,
mas, se o servidor reiniciasse logo depois, o crédito na Conta B poderia ser
perdido, mesmo o cliente tendo recebido a confirmação de sucesso.