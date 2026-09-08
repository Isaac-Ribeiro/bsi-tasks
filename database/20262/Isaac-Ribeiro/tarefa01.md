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