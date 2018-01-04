![Cabecalho](../../../ReadMe-Anexos/Cabecalho.png)

[Home](../../../ReadMe.md) :: [Módulo Treinamento](../../Modulo-Treinamento.md) :: [FU-Integração Financeira de Clientes](../FU-Integracao-Financeira-Clientes.md) :: [UC-Inativar Cliente por Atraso de Pagamento](UC-Inativar-Cliente-por-Atraso-de-Pagamento.md)

# Caso de Uso: Inativar Cliente por Atraso de Pagamento


| **[UC]**                | Inativar Cliente por Atraso de Pagamento                                                                                                                                                                                                                                  |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Objetivo**            | Permite inativar um cliente de qualquer plano (**Básico** ou **Premium**) por atraso de pagamento das últimas faturas em conformidade com [RN-Inativação de Clientes por Atraso de Pagamento](../Regras-de-Negocios/RN-Inativacao-de-Clientes-por-Atraso-de-Pagamento.md) |
| **Ator Principal**      | Analista Financeiro                                                                                                                                                                                                                                                       |
| **Atores Secundários**  | Gerente de Contas                                                                                                                                                                                                                                                         |
| **Fluxo Principal**     | [PR: Inativar Cliente Básico](#pr-inativar-cliente-b-sico)                                                                                                                                                                                                                |
| **Fluxos Alternativos** | [AL01: Inativar Cliente Premium](#al01-inativar-cliente-premium)                                                                                                                                                                                                          |
| **Fluxos de Exceção**   | [EX01: Não há clientes passíveis de inativação](#ex01-n-o-h-clientes-pass-veis-de-inativa-o)                                                                                                                                                                              |
|                         | [EX02: Analista Financeiro não seleciona um cliente](#ex02-analista-financeiro-n-o-seleciona-um-cliente)                                                                                                                                                                  |
|                         | [EX03: Ocorreu um erro interno no sistema durante a inativação](#ex03-ocorreu-um-erro-interno-no-sistema-durante-a-inativa-o)                                                                                                                                             |
|                         | [EX04: Gerente de Contas não informa Login/Senha](#ex04-gerente-de-contas-n-o-informa-login-senha)                                                                                                                                                                        |
|                         | [EX05: Gerente de Contas não confirma a inativação](#ex05-gerente-de-contas-n-o-confirma-a-inativa-o)                                                                                                                                                                     |



## PR: Inativar Cliente Básico

1. **Analista Financeiro** seleciona opção de _Inativar Cliente por Atraso de Pagamento_ [1] no Sistema.
2. **Sistema** apresenta o formulário _Inativação de Clientes_ [2].
3. **Analista Financeiro** seleciona opção para pesquisar clientes passíveis de inativação.
4. **Sistema** obtém na base de dados os clientes passíveis de inativação, cf: [RN-Inativação de Clientes por Atraso de Pagamento](../Regras-de-Negocios/RN-Inativacao-de-Clientes-por-Atraso-de-Pagamento.md) [[EX01](#ex01-n-o-h-clientes-pass-veis-de-inativa-o)]
5. **Sistema** apresenta a listagem dos clientes passíveis de inativação com: [3]
  - Nome
  - Plano (cf: [RN-Planos de Clientes](../Regras-de-Negocios/RN-Planos-de-Clientes.md))
  - Número de meses em atraso
6. **Analista Financeiro** seleciona um cliente **básico** cf: [RN-Planos de Clientes](RN-Planos-de-Clientes.md) [3] [[AL01](#al01-inativar-cliente-premium)] [[EX02](#ex02-analista-financeiro-n-o-seleciona-um-cliente)] [4].
7. **Analista Financeiro** aciona opção para inativar o cliente.
8. **Sistema** registra a inativação cessando o fornecimento de serviços a este cliente. [[EX03](#ex03-ocorreu-um-erro-interno-no-sistema-durante-a-inativa-o)]
9. **Fim do Caso de Uso** [5]

_Notas:_

1. "Inativar Cliente por Atraso de Pagamento" é a **opção** que o sistema oferece ao Atendente. Isto pode ser acessado através de uma entrada de menu, um comando de teclado, um botão em uma barra de comandos, tanto faz. O caso de uso **não deve entrar** no detalhe técnico de **como** esta funcionalidade é acessada, pois fica desacoplado da GUI.

2. No passo 2, "Inativação de Clientes" é o título do formulário que irá aparecer. Quando necessário indicar uma tela ou formulário mencione o título da mesma, para que o leitor saiba identificá-la quando acessar o sistema. Como o caso de uso descreve a **comunicação entre os atores**, os **termos em comum** desta comunicação devem estar claros para ambos.

3. Veja que não está sendo mencionado **como** o sistema apresenta a listagem nem **como** o usuário seleciona o cliente. Isto é detalhe gráfico da GUI. Pode ser que o sistema apresente uma lista drop-down, pode ser um combo-box, pode ser uma tabela.
**Caso de uso X GUI**:  quanto menos detalhes de GUI forem mencionados no caso de uso, menor a necessidade de alteração no mesmo quando algum ajuste puramente visual for realizado.

4. **Pontos de Acesso à Fluxos Alternativos:**
Deve ficar claro no caso de uso quando um fluxo qualquer tiver algum passo que possa levar à um caminho alternativo (fluxo alternativo). Atente para a notação utilizada.

5. Encerre o caso de uso com a sentença: "**Fim do Caso de Uso**".

## Fluxos Alternativos

### AL01: Inativar Cliente Premium

1. **Analista Financeiro** seleciona um cliente **Preminum** cf: [RN-Planos de Clientes](RN-Planos-de-Clientes.md) [[EX02](#ex02-analista-financeiro-n-o-seleciona-um-cliente)] [1]
2. **Sistema** solicita confirmação pelo **Gerente de Contas**
3. **Gerente de Contas** informa sua identificação (login e senha) e aciona comando para aprovar [[EX04](#ex04-gerente-de-contas-n-o-informa-login-senha)] [[EX05](#ex05-gerente-de-contas-n-o-confirma-a-inativa-o)]
4. **Analista Financeiro** aciona opção para inativar o cliente.
5. **Sistema** confirma que o **Gerente de Contas** possui permissão para inativação de clientes **premium** [[EX06](#ex06)] [2]
6. **Sistema** registra a inativação cessando o fornecimento de serviços a este cliente [[EX03](#ex03-ocorreu-um-erro-interno-no-sistema-durante-a-inativa-o)].
7. **Sistema** retorna ao passo 2 do [[PR](#pr-inativar-cliente-b-sico)]


_Notas:_

1. O primeiro passo indica qual a condição (opção) tomada pelo ator que alterou o caminho do caso de uso.
2. Os passos devem assumir sempre uma posição de sucesso (possui permissão), as falhas são tratados na exceção.
3. Todos os fluxos devem indicar no seu último passo para onde o sistema guiará o ator principal:
- Se a interação irá se encerrar: X. Fim do Caso de Uso.
- Ou se o Ator será guiado de volta para o fluxo original: X. **Sistema** continua no passo 8 do fluxo [[PR](#)]


## Fluxos de Exceção

### EX01: Não há clientes passíveis de inativação

Exceção quando não há clientes na base de dados passíveis de inativação segundo a regra [RN-Inativação de Clientes por Atraso de Pagamento](../Regras-de-Negocios/RN-Inativacao-de-Clientes-por-Atraso-de-Pagamento.md).

1. **Sistema** exibe mensagem: _"Não foram encontrados clientes para inativação"_.
2. **Sistema** retorna ao passo 2 do [[PR](#pr-inativar-cliente-b-sico)]

### EX02: Analista Financeiro não seleciona um cliente

Exceção quando **Analista Financeiro** não indica o cliente para inativação.

1. **Sistema** exibe mensagem: _"Selecione o cliente para inativação"_.
2. **Sistema** retorna ao passo 5 do [[PR](#pr-inativar-cliente-b-sico)]

### EX03: Ocorreu um erro interno no sistema durante a inativação

Exceção quando algum **erro interno** inesperado ocorreu no sistema e a operação não foi efetivada.

1. **Sistema** estorna qualquer operação parcialmente executada.
2. **Sistema** exibe uma mensagem com detalhes do erro e com orientações de como solicitar suporte técnico.
3. **Sistema** retorna ao passo 7 do [[PR](#pr-inativar-cliente-b-sico)] ou ao passo 5 do [[AL01](#al01-inativar-cliente-premium)]


### EX04: Gerente de Contas não informa Login/Senha

Exceção quando o **Gerente de Contas** não informa seu Login e Senha e aciona opção para aprovar a inativação.

1. **Sistema** exibe mensagem: _"Informe o Login e a Senha para aprovação de Inativação de cliente PREMIUM"_.
3. **Sistema** retorna ao passo 2 do [[AL01](#al01-inativar-cliente-premium)]

### EX05: Gerente de Contas não confirma a inativação

Exceção quando o **Gerente de Contas** se recusa a aprovar a inativação do cliente, acionando opção "Recusar".

1. **Sistema** exibe mensagem: _"Inativação de cliente PREMIUM não aprovada."_.
3. **Sistema** retorna ao passo 2 do [[AL01](#al01-inativar-cliente-premium)]


### EX06: Gerente de Contas não possui permissão para inativação

Exceção quando o **Gerente de Contas** aprova a inativação do cliente, porém o **Sistema** identifica que ele não possui permissão para tal, cf. [RN-Inativação de Clientes por Atraso de Pagamento](../Regras-de-Negocios/RN-Inativacao-de-Clientes-por-Atraso-de-Pagamento.md).

1. **Sistema** NÃO confirma que o **Gerente de Contas** possui permissão para inativação de clientes **premium**
2. **Sistema** exibe mensagem: _"Falha ao inativar cliente PREMIUM: (nome-do-Gerente-de-Contas) não possui permissão: (código-da-permissão)."_.
3. **Sistema** retorna ao passo 2 do fluxo alternativo [[AL01](#al01-inativar-cliente-premium)]


_[Sobre o Portal de Documentação](../../../About/About.md)_

![Rodape](../../../ReadMe-Anexos/Rodape.png)
