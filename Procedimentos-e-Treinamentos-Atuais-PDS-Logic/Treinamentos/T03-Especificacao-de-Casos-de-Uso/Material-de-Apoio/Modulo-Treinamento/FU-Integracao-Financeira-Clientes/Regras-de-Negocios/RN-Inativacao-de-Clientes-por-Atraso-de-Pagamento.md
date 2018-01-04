![Cabecalho](../../../ReadMe-Anexos/Cabecalho.png)

[Home](../../../ReadMe.md) :: [Módulo Treinamento](../../Modulo-Treinamento.md) :: [FU-Integração Financeira de Clientes](../FU-Integracao-Financeira-Clientes.md) :: [RN-Inativação de Clientes por Atraso de Pagamento](RN-Inativacao-de-Clientes-por-Atraso-de-Pagamento.md)


# Regra de Negócios: Inativação de Clientes por Atraso de Pagamento

Um cliente pode ser _inativado_, sendo cessado o fornecimento de serviços ao mesmo, se este estiver com 3 (três) ou mais parcelas em atraso.
A inativação deve ser realizada pelo **Analista Financeiro** validado por permissão de acesso à tela destinada à este fim. Caso se trate de um cliente especial, denominado: _premium_, a inativação só poderá ser realizada com aprovação do **Gerente de Contas**, validado por permissão especial.

**Parametrizações:**
- O limite de meses é parametrável pela chave: `sistema.financeiro.meses_em_atraso_para_inativacao`, com valor padrão: 3 (três meses)
- A operação vinculada a permissão para aprovação do Gerente de Contas tem o código: `4.35.193` - Aprovação para Inativação de Cliente Premium

_[Sobre o Portal de Documentação](../../../About/About.md)_

![Rodape](../../../ReadMe-Anexos/Rodape.png)
