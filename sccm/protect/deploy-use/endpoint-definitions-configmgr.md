---
title: Definições de malware do Endpoint Protection
titleSuffix: Configuration Manager
description: Saiba como configurar as atualizações do software do Configuration Manager para fornecer atualizações de definição para os computadores cliente.
ms.date: 10/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3b9c4027-a98b-406b-935c-ccabcfe713df
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 976a6b149175b817ea7039faf1f909a73f2b514d
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500535"
---
#  <a name="using-configuration-manager-software-updates-to-deliver-definition-updates"></a>Usando as atualizações de Software do Configuration Manager para fornecer atualizações de definições

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


 Você pode configurar as atualizações do software do Configuration Manager para fornecer atualizações de definição para os computadores cliente. Isso é feito ao configurar regras de implantação automática. Antes de começar a criar regras de implantação automática, verifique se você configurou as atualizações de software do Configuration Manager. Para mais informações, consulte [Introdução às atualizações de software no System Center Configuration Manager](/sccm/sum/understand/software-updates-introduction).

> [!NOTE]
>  Esse procedimento é somente para os itens que devem ser configurados especificamente para o Endpoint Protection. Para obter mais informações sobre o Assistente para Criar Regra de Implantação Automática, consulte [Implantar atualizações de software automaticamente](/sccm/sum/deploy-use/automatically-deploy-software-updates).

## <a name="to-configure-an-automatic-deployment-rule-to-deliver-definition-updates"></a>Para configurar uma regra de implantação automática para fornecer atualizações de definições

1. No console do Configuration Manager, clique em **Biblioteca de Software**.

2. No workspace **Biblioteca de Software**, expanda **Atualizações de Software** e clique em **Regras de Implantação Automática**.

3. Na guia **Início** , no grupo **Criar** , clique em **Criar Regra de Implantação Automática**.

4. Na página **Geral** do **Assistente para Criar Regra de Implantação Automática**, especifique as seguintes informações:

   -   **Nome**: digite um nome exclusivo para a regra de implantação automática.

   -   **Coleção**: selecione a coleção de computadores cliente na qual você deseja implantar atualizações de definições.

       > [!NOTE]
       >  Você não pode implantar atualizações de definições em uma coleção de usuários.

5. Clique em **Adicionar a um Grupo de Atualizações de Software existente**.

6. Verifique se a caixa de seleção  **Habilitar a implantação após esta regra ser executada** está marcada e clique em **Avançar**.

7. Na página **Configurações de Implantação** do assistente, na lista **Nível de detalhe**, selecione **Somente mensagens de erro** e clique em **Avançar**.

   > [!NOTE]
   >  Selecionar **Somente mensagens de erro** reduzirá o número de mensagens de estado retornadas pela implantação da definição. Essa configuração ajuda a reduzir o uso de processamento da CPU nos servidores do Configuration Manager.

8. Na lista **Filtros de propriedade** , marque a caixa de seleção **Classificação da Atualização** .

9. Na lista **Critérios de pesquisa**, clique em **<itens para localizar\>**. Na caixa de diálogo **Critérios de Pesquisa** , na lista **Especificar o valor de pesquisa** , selecione **Atualizações de Definições**.

10. Clique em **OK** para fechar a caixa de diálogo **Critérios de Pesquisa** .

11. Na lista **Filtros de propriedade** , marque a caixa de seleção **Produto** .

12. Na lista **Critérios de pesquisa**, clique em **<itens para localizar\>**. Na caixa de diálogo **Critérios de Pesquisa** , na lista **Especificar o valor de pesquisa** , selecione **Forefront Endpoint Protection 2010** para Windows 8.1 e versões anteriores ou **Windows Defender** para Windows 10 e versões posteriores.

13. Clique em **OK** para fechar a caixa de diálogo **Critérios de Pesquisa** e clique em **Avançar**.

14. Opcionalmente, você pode filtrar as atualizações substituídas.   Para fazer isso:
    1.  Na lista **Filtros de propriedade** , marque a caixa de seleção **Substituído** .
    2.  Na lista **Critérios de pesquisa**, clique em **<itens para localizar\>**. Na caixa de diálogo **Critérios de Pesquisa** , na lista **Especificar o valor de pesquisa** , selecione **Não**.  <br><br>

15. Clique em **OK** para fechar a caixa de diálogo **Critérios de Pesquisa** e clique em **Avançar**.

16. Na página **Agendamento de Avaliação** do assistente, selecione **Habilitar a execução da regra em um agendamento**e configure o agendamento no qual deseja baixar atualizações de definições. No mínimo, defina que a regra seja executada duas horas depois de cada sincronização de ponto de atualização de software. Clique em **Avançar**.

17. Na página **Agendamento da Implantação** , defina as seguintes configurações:

    -   **Tempo base em**: selecione **UTC** se desejar que todos os clientes na hierarquia instalem as definições mais recentes ao mesmo tempo. O tempo de instalação real varia em uma janela de duas horas. Essa configuração é uma prática recomendada.

    -   **Tempo disponível do software**: especifique o tempo disponível para a implantação criada por essa regra. A hora especificada deve ser pelo menos uma hora depois que a regra de implantação automática é executada. Isso ajuda a garantir que o conteúdo tenha tempo suficiente para replicar os pontos de distribuição na hierarquia. Algumas atualizações de definições também podem incluir atualizações de mecanismos antimalware, as quais podem levar mais tempo para alcançar os pontos de distribuição.

    -   **Prazo de instalação**: selecione **O mais breve possível**.

        > [!NOTE]
        >  Os prazos de atualização de software variam durante um período de duas horas para impedir que todos os clientes solicitem uma atualização ao mesmo tempo.

18. Clique em **Avançar**.

19. Na página **Experiência do Usuário** do assistente, na lista **Notificações do usuário** , selecione **Ocultar no Centro de Software e todas as notificações**.   Isso garante que as atualizações de definições instalem silenciosamente. Clique em **Avançar**.

20. Na página **Alertas** do assistente, você não precisa configurar nenhum alerta. O Endpoint Protection no Configuration Manager gera todos os alertas que podem ser necessários. Clique em **Avançar**.

21. Na página **Pacote de Implantação** do assistente, selecione um pacote de implantação existente ou crie um novo pacote de implantação para conter os arquivos de atualização de software associados à regra.

    > [!NOTE]
    >  Considere colocar as atualizações de definições em um pacote que não contenha outras atualizações de software. Essa estratégia mantém o tamanho do pacote de atualização de definição menor, o que permite que ele seja replicado para os pontos de distribuição mais rapidamente.

22. Se criar um novo pacote, na página **Pontos de Distribuição** do assistente, selecione um ou mais pontos de distribuição para os quais o conteúdo do pacote serão copiados e clique em **Avançar**.

23. Na página **Local de Download** do assistente, selecione **Baixar atualizações de software da Internet**e clique em **Avançar**.

24. Na página **Seleção do Idioma** do assistente, selecione cada versão do idioma das atualizações a serem baixadas e clique em **Avançar**.

25. Na página **Configurações de Download** do assistente, selecione o comportamento de download das atualizações de software necessárias e clique em **Avançar**.

26. Na página **Resumo** do assistente, examine as configurações e clique em **Avançar**.

26. Conclua o Assistente para Criar de Regra de Implantação Automática.

27. Verifique se a nova regra é exibida no nó **Regras de Implantação Automática** do console do Configuration Manager.


> [!div class="button"]
> [Próxima etapa >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Voltar >](endpoint-configure-alerts.md)
