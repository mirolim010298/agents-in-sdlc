---
title: "Exercício 4 - Monitoramento e gerenciamento de agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Nos últimos exercícios, você pediu ao agente GitHub Copilot na nuvem que assumisse três tarefas diferentes para melhorar a experiência do usuário e adicionar funcionalidades. Embora o agente na nuvem tenha sido criado para trabalhar de forma assíncrona e autônoma, ainda é importante monitorar essas tarefas.

Há várias ferramentas para gerenciar as tarefas atribuídas ao agente na nuvem, incluindo a [página de agentes][agents-page] no GitHub.com. Nesse painel de controle, você vê todas as tarefas do agente com pull requests (PRs) abertos. Você pode explorar as operações realizadas e até orientar uma sessão em andamento.

Nesta lição, você vai:

- explorar a página de agentes para monitorar as tarefas do agente na nuvem.
- orientar uma sessão em andamento e solicitar funcionalidade adicional.

## Cenário

Depois de atribuir ao agente a criação do modo de alto contraste, a equipe percebeu que seria um bom momento para adicionar também um modo claro. Como o trabalho já envolvia atualizar o estilo do site e adicionar uma funcionalidade de alternância, pareceu lógico incluir esse recurso. Você orientará o agente para garantir que ele adicione o modo claro junto com o modo de alto contraste.

## Revise as tarefas do agente GitHub Copilot na nuvem

Vamos verificar o status atual de todas as tarefas atribuídas ao agente GitHub Copilot na nuvem.

1. Acesse a [página de agentes do Copilot](https://github.com/copilot/agents).
2. Observe a lista de tarefas no painel principal e no painel esquerdo. Você deverá ver as tarefas atribuídas ao Copilot, incluindo:
    - Atualizar a documentação da base de código.
    - Gerar APIs para modificar jogos.
    - Adicionar um modo de alto contraste ao site.
3. Selecione uma das tarefas em andamento. Revise as operações realizadas pelo Copilot, que podem incluir:
    - Obter o código do repositório.
    - Criar o ambiente de trabalho do Copilot.
    - Configurar servidores MCP.
    - Executar várias etapas para concluir a tarefa atribuída.

> [!NOTE]
> As etapas listadas variam conforme o estado do trabalho do Copilot e a abordagem usada.

4. Observe também o painel de pull requests (PRs) exibido à direita. Ele permite ver o PR e os arquivos alterados para monitoramento adicional.

## Oriente o agente na nuvem

Agora que você viu as tarefas em andamento, vamos pedir ao Copilot que inclua uma opção de modo claro enquanto trabalha no modo de alto contraste.

1. Selecione a sessão referente à adição do modo de alto contraste. O título exato varia conforme o nome usado pelo Copilot e o estado atual do trabalho.

    ![Sessão de acessibilidade no painel de controle](../../../_images/ex6-accessibility-session.png)

2. Acompanhe a sessão por alguns minutos, até que ela indique que a configuração foi concluída e o trabalho começou. Você saberá que isso aconteceu quando vir mensagens semelhantes às mostradas abaixo.
3. Na caixa de diálogo **Steer active session while Copilot is working**, adicione o prompt:

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![Tarefa do agente na nuvem na página de agentes, com a caixa de diálogo para orientar uma sessão ativa do Copilot destacada](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pressione <kbd>Enter</kbd> para enviar o prompt.
5. Observe como o Copilot confirma o recebimento do prompt e o inclui no fluxo de trabalho.

## Deixe o Copilot trabalhar

Como antes, o Copilot começará a trabalhar na tarefa atualizada! Depois de concluir a etapa em andamento no momento em que você enviou a mensagem, ele incorporará a nova solicitação ao fluxo de trabalho.

Como esse processo levará alguns minutos, é uma boa hora para fazer uma pausa e refletir sobre tudo o que você aprendeu e explorou até agora.

## Resumo e próximos passos

Esta lição apresentou a página de agentes do Copilot, o painel central para monitorar e orientar as tarefas do agente GitHub Copilot na nuvem. Nesse painel, você pode acompanhar todas as tarefas ativas e concluídas, revisar o trabalho e redirecionar tarefas em andamento para ajustar o escopo ou fornecer orientações adicionais.

Você explorou estes conceitos:

- explorou o painel de controle e a página de agentes para monitorar as tarefas do agente na nuvem.
- redirecionou uma sessão em andamento para solicitar funcionalidade adicional.

Enquanto o Copilot conclui o trabalho nos recursos de acessibilidade, vamos [iterar sobre os pull requests criados pelo Copilot][next-lesson].

## Recursos

- [Página de agentes do Copilot][agents-page]
- [Sobre agentes personalizados][custom-agents]

---

| [← Lição anterior: Agentes personalizados][previous-lesson] | [Próxima lição: Iterar sobre o trabalho do Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
