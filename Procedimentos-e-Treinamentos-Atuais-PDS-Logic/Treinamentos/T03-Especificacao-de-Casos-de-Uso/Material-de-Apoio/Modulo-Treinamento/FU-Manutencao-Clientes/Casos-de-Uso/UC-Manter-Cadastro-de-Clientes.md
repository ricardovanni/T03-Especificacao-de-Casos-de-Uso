![Cabecalho](../../../ReadMe-Anexos/Cabecalho.png)

[Home](../../../ReadMe.md) :: [Módulo Treinamento](../../Modulo-Treinamento.md) :: [FU-Manter Cadastro de Clientes](../FU-Manter-Cadastro-de-Clientes.md) :: [UC-Manter Cadastro de Clientes](UC-Manter-Cadastro-de-Clientes.md)

# Caso de Uso: Manter Cadastro de Clientes

| **[UC]**                | Manter Cadastro de Clientes                                                                                                                                                                                                          |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Objetivo**            | Manter as informações cadastrais do cliente, possibilitando inclusão de novos cliente e atualização cadastral dos clientes existentes. Não sendo possível a remoção definitiva de um cadastro, apenas seu arquivamento (inativação). |
| **Ator Principal**      | Auxiliar de Cadastro                                                                                                                                                                                                                 |
| **Atores Secundários**  | Gerente de Contas                                                                                                                                                                                                                    |
| **Fluxo Principal**     | [PR: Incluir Cliente](#pr-incluir-cliente)                                                                                                                                                                                           |
| **Fluxos Alternativos** | [AL01: Consultar Cliente](#al01-consultar-cliente)                                                                                                                                                                                   |
|                         | [AL02: Alterar Cliente](#al02-alterar-cliente)                                                                                                                                                                                       |
|                         | [AL03: Inativar Cliente](#al03-inativar-cliente)                                                                                                                                                                                     |
|                         | [AL04: Aprovar Cadastro de Cliente](#al04-aprovar-cadastro-de-cliente)                                                                                                                                                               |
| **Fluxos de Exceção**   | [EX01: Auxiliar de Cadastro não preenche todas as informações obrigatórias](#ex01-auxiliar-de-cadastro-n-o-preenche-todas-as-informa-es-obrigat-rias)                                                                                |
|                         | [EX02: Auxiliar de Cadastro não informa os filtros para pesquisar](#ex02-auxiliar-de-cadastro-n-o-informa-os-filtros-para-pesquisar)                                                                                                 |
|                         | [EX03: Não foram encontrados clientes com filtros informados](#ex03-n-o-foram-encontrados-clientes-com-filtros-informados)                                                                                                           |
|                         | [EX04: Situação cadastral do cliente é INATIVA](#ex04-situa-o-cadastral-do-cliente-inativa).                                                                                                                                         |
|                         | [EX05: Situação cadastral do cliente é INATIVO ou APROVADO](#ex05-situa-o-cadastral-do-cliente-inativo-ou-aprovado)                                                                                                                  |
|                         | [EX06: Gerente de Contas não informa os dados necessários para Aprovar um Cadastro](#)                                                                                                                                               |
|                         | [EX07: Gerente de Contas não informa Login/Senha para Aprovar um Cadastro](#ex07-gerente-de-contas-n-o-informa-login-senha-para-aprovar-um-cadastro)                                                                                 |
|                         | [EX08: Gerente de Contas não confirma a Aprovação](#ex08-gerente-de-contas-n-o-confirma-a-aprova-o)                                                                                                                                  |


## PR: Incluir Cliente

1. **Auxiliar de Cadastro** seleciona opção de _Cadastro de Clientes_ no sistema.
2. **Sistema** apresenta o formulário _Cadastro e Manutenção de Clientes_.
3. **Auxiliar de Cadastro** seleciona opção de _Cadastrar Novo Cliente_ no sistema [[AL01](#al01-consultar-cliente)].
4. **Sistema** solicita as informações para cadastro de novos clientes, cf: [RN-Campos Cadastro Clientes](../Regras-de-Negocios/RN-Campos-Cadastro-Clientes.md).
5. **Auxiliar de Cadastro** preenche todas as informações obrigatórias e opcionalmente as não obrigatórias [[EX01](#ex01-auxiliar-de-cadastro-n-o-preenche-todas-as-informa-es-obrigat-rias)].
6. **Auxiliar de Cadastro** aciona comando para gravar as informações.
4. **Sistema** atualiza a situação cadastral do cliente para NOVO, cf: [RN-Situação Cadastral Cliente](../Regras-de-Negocios/RN-Situacao-Cadastral-Cliente.md)
7. **Sistema** grava as informações.
8. **Fim do caso de Uso**

## Fluxos Alternativos

### AL01: Consultar Cliente

Fluxo executado para consultar clientes já cadastrados, acionado quando o **Auxiliar de Cadastro** seleciona a opção _Buscar Cliente_.

1. **Auxiliar de Cadastro** seleciona a opção _Buscar Cliente_.
2. **Sistema** apresenta os filtros de pesquisa:
  - Nome
  - CPF
3. **Auxiliar de Cadastro** informa os filtros de pesquisa e aciona o comando para pesquisar os clientes [[EX02](#ex02-auxiliar-de-cadastro-n-o-informa-os-filtros-para-pesquisar)]
4. **Sistema** pesquisa pelos clientes na base de dados conforme os filtros informados e apresenta os resultados [[EX03](#ex03-n-o-foram-encontrados-clientes-com-filtros-informados)]
5. **Auxiliar de Cadastro** apenas consulta (visualiza) os dados do cliente sem alterá-los [[AL02](#al02-alterar-cliente)] [[AL03](#al03-inativar-cliente)] [[AL04](#al04-aprovar-cadastro-de-cliente)]
6. **Sistema** retorna ao passo 3 do fluxo [[PR](#pr-incluir-cliente)]

### AL02: Alterar Cliente

Fluxo executado para alterar um cliente já cadastrado, acionado quando o **Auxiliar de Cadastro** altera algum dado do Cliente após pesquisá-lo pelo fluxo [[AL01](#al01-consultar-cliente)].

1. **Auxiliar de Cadastro** altera as informações do cliente conforme desejar, garantindo que todos os campos obrigatórios estão preechidos [[EX01](#ex01-auxiliar-de-cadastro-n-o-preenche-todas-as-informa-es-obrigat-rias)].
2. **Auxiliar de Cadastro** aciona comando para gravar as informações.
3. **Sistema** grava as informações atualizadas do cliente.
4. **Sistema** atualiza a situação cadastral do cliente para ALTERADO, cf: [RN-Situação Cadastral Cliente](../Regras-de-Negocios/RN-Situacao-Cadastral-Cliente.md)
6. **Sistema** retorna ao passo 3 do fluxo [[PR](#pr-incluir-cliente)]

### AL03: Inativar Cliente

Fluxo executado para inativar um cliente cadastrado, o que irá interromper o fornecimento de serviços ao mesmo. Acionado quando o **Auxiliar de Cadastro** aciona o comando _Inativar_  após pesquisá-lo pelo fluxo [[AL01](#al01-consultar-cliente)].

1. **Auxiliar de Cadastro** realiza a consulta de um cliente cujo status é NOVO, ALTERADO ou APROVADO [[EX04](#ex04-situa-o-cadastral-do-cliente-inativa)]
1. **Auxiliar de Cadastro** aciona o comando _Inativar_.
4. **Sistema** atualiza a situação cadastral do cliente para INATIVO, cf: [RN-Situação Cadastral Cliente](../Regras-de-Negocios/RN-Situacao-Cadastral-Cliente.md)
6. **Sistema** retorna ao passo 3 do fluxo [[PR](#pr-incluir-cliente)]

### AL04: Aprovar Cadastro de Cliente

Fluxo executado pelo **Gerente de Contas** para aprovação de cliente recém cadastrado, ou cujo cadastro foi alterado. Acionado após a pequisa de um cliente com situação NOVO ou ALTERADO pelo fluxo: [[AL01](#al01-consultar-cliente)].

1. **Gerente de Contas** realiza a consulta de um cliente cujo status é NOVO ou ALTERADO [[EX05](#ex05-situa-o-cadastral-do-cliente-inativo-ou-aprovado)]
2. **Gerente de Contas** informa os dados para aprovação
  - Plano do Clientes (Premium ou Básico)
  - Código da Conta Contábil (para efeitos de balancete/DRE)
3. **Gerente de Contas** aciona o comando para aprovar o cadastro.
4. **Sistema** solicita o código de usuário e senha do **Gerente de Contas**
5. **Gerente de Contas** informa sua identificação (login e senha) [[EX07](#ex07-gerente-de-contas-n-o-informa-login-senha-para-aprovar-um-cadastro)] [[EX08](#ex08-gerente-de-contas-n-o-confirma-a-aprova-o)].
4. **Sistema** atualiza a situação cadastral do cliente para APROVADPO, cf: [RN-Situação Cadastral Cliente](../Regras-de-Negocios/RN-Situacao-Cadastral-Cliente.md)
6. **Sistema** retorna ao passo 3 do fluxo [[PR](#pr-incluir-cliente)]


## Fluxos de Exceção

### EX01: Auxiliar de Cadastro não preenche todas as informações obrigatórias

Exceção quando **Auxiliar de Cadastro** não preenche todas as informações obrigatórias.

1. **Sistema** exibe mensagem: _"* 'nome-do-campo' Obrigatório."_ em cada campo obrigatório não informado.
2. **Sistema** retorna ao passo 5 do fluxo [[PR](#pr-incluir-cliente)]

### EX02: Auxiliar de Cadastro não informa os filtros para pesquisar

Exceção quando **Auxiliar de Cadastro** não informa os filtros de pesquisa e aciona o comando para pesquisar clientes.

1. **Sistema** exibe mensagem: _"Informe ao menos um filtro  para consulta."_.
2. **Sistema** retorna ao passo 2 do fluxo [[AL01](#al01-consultar-cliente)]

### EX03: Não foram encontrados clientes com filtros informados

Exceção quando não há clientes cadastrados com os filros informados pelo **Auxiliar de Cadastro** na consulta de clientes.

1. **Sistema** exibe mensagem: _"Não foram encontrados clientes com os filtros informados."_.
2. **Sistema** retorna ao passo 2 do fluxo [[AL01](#al01-consultar-cliente)]

### EX04: Situação cadastral do cliente é INATIVA

Exceção quando o **Auxiliar de Cadastro** busca por um cliente cuja situação cadastral é INATIVO, cf: [RN-Situação Cadastral Cliente](../Regras-de-Negocios/RN-Situacao-Cadastral-Cliente.md).

1. **Sistema** não disponibiliza opção de comando para _Arquivar_
2. **Sistema** retorna ao passo 5 do fluxo [[AL01](#al01-consultar-cliente)]


### EX05: Situação cadastral do cliente é INATIVO ou APROVADO

Exceção quando o **Gerente de Contas** busca por um cliente cuja situação cadastral é INATIVO ou APROVADO, cf: [RN-Situação Cadastral Cliente](../Regras-de-Negocios/RN-Situacao-Cadastral-Cliente.md), o que impossibilita sua aprovação.

1. **Sistema** não disponibiliza opção de comando para _Aprovar_
2. **Sistema** retorna ao passo 5 do fluxo [[AL01](#al01-consultar-cliente)]

### EX06: Gerente de Contas não informa os dados necessários para Aprovar um Cadastro

Exceção quando o **Gerente de Contas** não informa os dados necessários para Aprovar um Cadastro cf: [RN-Aprovação Cadastro Clientes](../Regras-de-Negocios/RN-Aprovacao-Cadastro-Clientes.md), o que impossibilita sua aprovação.

1. **Sistema** exibe mensagem: _"* 'nome-do-campo' Obrigatório."_ em cada campo não informado.
2. **Sistema** retorna ao passo 2 do fluxo [[AL04](#al04-aprovar-cadastro-de-cliente)]


### EX07: Gerente de Contas não informa Login/Senha para Aprovar um Cadastro

Exceção quando o **Gerente de Contas** não informa seu Login e Senha para aprovação do cadastro

1. **Sistema** exibe mensagem: _"Informe o Login e a Senha para Aprovação do Cadastro do Cliente"_.
2. **Sistema** retorna ao passo 2 do fluxo [[AL04](#al04-aprovar-cadastro-de-cliente)]

### EX08: Gerente de Contas não confirma a Aprovação

Exceção quando o **Gerente de Contas** se recusa a aprovar o cadastro do cliente, acionando opção "Recusar".

1. **Sistema** exibe mensagem: _"Cadastro Não Aprovado."_.
2. **Sistema** retorna ao passo 2 do fluxo [[AL04](#al04-aprovar-cadastro-de-cliente)]


_[Sobre o Portal de Documentação](../../../About/About.md)_

![Rodape](../../../ReadMe-Anexos/Rodape.png)
