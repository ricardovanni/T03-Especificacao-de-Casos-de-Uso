![Cabecalho](../../../ReadMe-Anexos/Cabecalho.png)


[Home](../../../ReadMe.md) :: [Módulo Treinamento](../../Modulo-Treinamento.md) :: [FU-Manter Cadastro de Clientes](../FU-Manter-Cadastro-de-Clientes.md) :: [RN-Situação Cadastral Cliente](RN-Situacao-Cadastral-Cliente.md)

# Regra de Negócios: Situação Cadastral Cliente

Todo cliente mantido no sistema tem sua situação cadastral definida por estas regras:
1. Após ser cadastrado um novo cliente, sua situação é NOVO e este ainda não pode efetuar compras.
2. Uma vez aprovado pelo **Gerente de Contas** sua situação é atualizada para APROVADO. Status que permite realização de compras.
3. Caso algum informação do cliente seja alterada após sua aprovação, sua situação cadastral é marcada com status: ALTERADO e necessita de nova aprovação comercial.
4. Caso algum cliente tenha seu cadastro inativado, este tem seu status marcado com INATIVO e não pode realizar compras.

_[Sobre o Portal de Documentação](../../../About/About.md)_

![Rodape](../../../ReadMe-Anexos/Rodape.png)
