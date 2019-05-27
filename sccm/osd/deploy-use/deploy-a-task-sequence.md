---
title: Implantar uma sequência de tarefas
titleSuffix: Configuration Manager
description: Use essas informações para implantar uma sequência de tarefas nos computadores de uma coleção.
ms.date: 05/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: b2abcdb0-72e0-4c70-a4b8-7827480ba5b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18179301fc6edcc9148e8bff353a5e14c1b0f210
ms.sourcegitcommit: ab9f2a7fb7ea3a0c65808fce2975ab25a670281f
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65613024"
---
# <a name="deploy-a-task-sequence"></a>Implantar uma sequência de tarefas

Depois de criar uma sequência de tarefas e distribuir o conteúdo referenciado, implante-a em uma coleção de dispositivos. Essa ação permite que a sequência de tarefas seja executada em um dispositivo. Uma sequência de tarefas implementada pode ser executada automaticamente ou quando instalada por um usuário do dispositivo.

> [!WARNING]  
> Você pode gerenciar o comportamento de implantações de sequência de tarefas de alto risco. Uma implantação de alto risco é uma implantação que é instalada automaticamente e que tem o potencial de causar resultados indesejados. Por exemplo, uma sequência de tarefas que tem uma finalidade **Obrigatória** que implanta um sistema operacional é considerada uma implantação de alto risco. Para obter mais informações, consulte [Configurações para gerenciar implantações de alto risco](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments).  


## <a name="process"></a>Processar

Use o procedimento a seguir para implantar uma sequência de tarefas para computadores em uma coleção.  

> [!NOTE]  
> As mensagens de status para a implantação de sequência de tarefas são exibidas na janela de mensagem no site primário, mas não são exibidas no site de administração central.  

1. No console do Configuration Manager, acesse o espaço de trabalho **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione o nó **Sequências de Tarefas**.  

2. Na lista **Sequência de Tarefas** , selecione a sequência de tarefas a implantar.  

3. Na guia **Início** da faixa de opções, no grupo **Implantação**, selecione **Implantar**.  

    > [!NOTE]  
    > Se **Implantar** não estiver disponível, a sequência de tarefas terá uma referência que não será válida. Corrija a referência e, em seguida, tente implantar a sequência de tarefas novamente.  

4. Na página **Geral**, especifique as seguintes informações.  

    - **Sequência de tarefas**: especifique a sequência de tarefas para implantação. Por padrão, essa caixa exibe a sequência de tarefas selecionada.  

    - **Coleção**: selecione a coleção que contém os computadores que executarão a sequência de tarefas.  

        Não implante uma sequência de tarefas que instala um sistema operacional em coleções inadequadas, como uma coleção de todos os servidores de data center. A coleção selecionada precisa conter somente os computadores que você quer que executem a sequência de tarefas.  

        Para saber mais sobre implantações de alto risco, confira [Implantações de alto risco](#bkmk_high-risk).

    - **Usar grupos de pontos de distribuição padrão associados a esta coleção**: armazene o conteúdo da sequência de tarefas no grupo de pontos de distribuição padrão da coleção. Se você não tiver associado a coleção selecionada a um grupo de pontos de distribuição, essa opção estará desabilitada.  

    - **Distribuir o conteúdo automaticamente para dependências**: se o conteúdo referenciado tiver dependências, o site também enviará o conteúdo dependente aos pontos de distribuição.  

    - **Conteúdo pré-baixado para esta sequência de tarefas**: saiba mais em [Configurar o conteúdo de armazenamento prévio em cache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  

    - **Selecionar Modelo de Implantação**: começando no Configuration Manager versão 1802,<!--1357391--> você pode salvar e especificar um modelo de implantação para uma sequência de tarefas.  

        > [!IMPORTANT]  
        > No Gerenciador de Configurações versão 1802, alguns itens não são salvos no modelo.  <!--510610--> Certifique-se de aplicar os seguintes itens ao executar o assistente de implementação:  
        >
        > - Instalação do Software
        > - Agendamento
        > - Pré-baixar conteúdo

    - **Comentários (opcional)**: especifique informações adicionais que descrevem essa implantação da sequência de tarefas.  

5. Na página **Configurações da implantação**, especifique as seguintes informações:  

    - **Finalidade**: na lista suspensa, escolha uma das seguintes opções:  

        - **Disponível**: o usuário vê a sequência de tarefas no Centro de Software e poderá instalá-la sob demanda.  

        - **Obrigatório**: o Gerenciador de Configurações executará automaticamente a sequência de tarefas de acordo com a agenda configurada. Se a sequência de tarefas não estiver oculta, um usuário ainda poderá acompanhar seu status de implantação. Eles também podem usar o Centro de Software para instalar a sequência de tarefas antes do prazo.  

        > [!NOTE]
        > Se vários usuários estiverem conectados ao dispositivo, as implantações de pacote e sequência de tarefas talvez não sejam exibidas no Centro de Software.  

    - **Disponibilizar para o seguinte**: especifique se a sequência de tarefas está disponível para um dos tipos a seguir:  

        - Somente clientes do Gerenciador de Configurações  
        - Clientes do Configuration Manager, mídia e PXE  
        - Somente mídia e PXE  
        - Somente mídia e PXE (oculto)  

        > [!IMPORTANT]  
        > Use a configuração **Somente mídia e PXE (oculto)** para implantações automatizadas de sequência de tarefas. Para que o computador seja inicializado automaticamente para a implantação sem a interação do usuário, selecione **Permitir implantação autônoma de sistema operacional** e defina a variável **SMSTSPreferredAdvertID** como parte da mídia. Para saber mais sobre variáveis de sequência de tarefas, confira [Variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables#SMSTSPreferredAdvertID).  

    - **Enviar pacotes de ativação**: se a implantação for **Obrigatória** e você selecionar essa opção, o site enviará um pacote de ativação aos computadores antes que o cliente execute a implantação. Esse pacote ativa os computadores na hora limite da instalação. Antes de usar essa opção, os computadores e as redes devem ser configurados para Wake On LAN. Para obter mais informações, confira [Planejar como ativar clientes](/sccm/core/clients/deploy/plan/plan-wake-up-clients).  

    - **Permitir que os clientes com um plano de Internet limitado baixem o conteúdo após a data limite da instalação, o que pode incorrer em custos adicionais**: essa opção está disponível somente para implantações **Obrigatórias**. Quando você tem um sequência de tarefas personalizada que instala um aplicativo, mas não implanta um sistema operacional, pode especificar se permite que os clientes baixem conteúdo após o prazo de instalação quando usarem conexões de Internet limitada. Às vezes, os provedores de Internet cobram pela quantidade de dados que você usa quando está em uma conexão de Internet limitada.  

        > [!NOTE]  
        > Embora o uso de um plano de Internet limitado possa funcionar para sequências de tarefas que não implantam um sistema operacional, não há suporte para esse recurso.  

6. Na página **Agendamento**, especifique as seguintes informações:  

    > [!IMPORTANT]  
    > Quando um cliente do Windows PE é iniciado pelo PXE ou pela mídia de inicialização, ele não avalia agendas de implantação. Essas agendas incluem os horários de início, expiração e prazo. Somente configure agendamentos em implantações em clientes que iniciam com o sistema operacional Windows completo. Considere usar outros métodos, como janelas de manutenção, para controlar as sequências de tarefas ativas implantadas nos clientes que iniciam por meio do Windows PE.  

    - **Agendar quando essa implantação estará disponível**: especifique a data e a hora em que a sequência de tarefas estará disponível para ser executada no computador de destino. Quando você seleciona a opção **UTC**, a sequência de tarefas está disponível para vários computadores ao mesmo tempo. Caso contrário, a implantação ficará disponível em momentos diferentes, acordo com a hora local em cada computador.  

        Se a hora de início for anterior à hora exigida, o cliente baixará o conteúdo da sequência de tarefas na hora de início.  

    - **Agendar quando essa implantação expirará**: especifique a data e a hora em que a sequência de tarefas expirará no computador de destino. Quando você selecionar a opção **UTC**, a sequência de tarefas expira em vários computadores de destino ao mesmo tempo. Caso contrário, a implantação expira em momentos diferentes, acordo com a hora local em cada computador.  

    - **Agendamento da atribuição**: para uma implantação **Obrigatória**, especifique quando o cliente executa a sequência de tarefas. Você pode adicionar vários agendamentos. O agendamento da atribuição pode ter uma das seguintes configurações:  

        - Data e hora específicas  
        - Padrão de recorrência mensal, semanal ou personalizado  
        - O mais breve possível  
        - Eventos de logon ou logoff  

        > [!NOTE]  
        > Se você agendar uma hora de início para uma implantação obrigatória anterior à data e hora de disponibilização da sequência de tarefas, o cliente do Gerenciador de Configurações baixará o conteúdo na hora de início atribuída. Esse comportamento ocorre mesmo que você tenha agendado a sequência de tarefas para estar disponível em um momento posterior.<!--SCCMDocs issue 777-->  

    - **Executar comportamento novamente**: especifique quando a sequência de tarefas precisar ser executada novamente. Selecione uma das seguintes opções:  

        - **Nunca executar novamente o programa implantado**: se o cliente executou a sequência de tarefas anteriormente, ele não a executará novamente. A sequência de tarefas não será executada novamente, mesmo se ela falhar originalmente ou se os arquivos da sequência de tarefas forem alterados.  

        - **Sempre executar novamente o programa**: a sequência de tarefas sempre executa novamente no cliente quando a implantação é agendada. Executa novamente mesmo se a sequência de tarefas já tiver sido executada com êxito. Essa configuração é útil quando você usa implantações recorrentes nas quais a sequência de tarefas é atualizada regularmente.  

            > [!IMPORTANT]  
            > Essa opção é habilitada por padrão. No entanto, ela não tem efeito até que você atribua uma implantação obrigatória. O usuário sempre pode executar novamente as implantações disponíveis.  

        - **Executar novamente se a tentativa anterior falhar**: a sequência de tarefas será executada novamente quando a implantação for agendada e somente se houver falha na execução anterior. Essa configuração é útil para implantações obrigatórias. Se a última tentativa de execução não for bem-sucedida, uma nova tentativa será feita de acordo com o agendamento de atribuição.  

        - **Executar novamente se a tentativa anterior tiver êxito**: a sequência de tarefas será executada novamente somente se a execução anterior tiver êxito no cliente. Essa configuração é útil ao usar implantações recorrentes nas quais a sequência de tarefas é atualizada regularmente, e cada atualização requer que a atualização anterior esteja instalada com êxito.  

        > [!NOTE]  
        > Um usuário pode executar novamente uma implantação de sequência de tarefas disponível. Antes de implantar uma sequência de tarefas disponível em um ambiente de produção, teste o que acontece se um usuário executar várias vezes a sequência de tarefas.  

7. Na página **Experiência do Usuário** , especifique as seguintes informações:  

    - **Permitir que o usuário execute o programa de forma independente das atribuições**: especifique se um usuário pode executar uma implantação obrigatória fora do agendamento da atribuição. Essa opção está sempre habilitada para as implantações disponíveis.  

    - **Mostrar andamento da sequência de tarefas**: especifique se o cliente do Configuration Manager exibe o andamento da sequência de tarefas.  

    - **Instalação de software**: especifique se o usuário tem permissão para instalar um software fora de uma janela de manutenção configurada após a hora agendada.  

    - **Reinicialização do sistema (se necessário para conclusão da instalação)**: especifique se o usuário tem permissão para reiniciar o computador após uma instalação de software fora de uma janela de manutenção configurada após a hora de atribuição.  

    - **Tratamento de filtro de gravação para dispositivos Windows Embedded com filtro de gravação**: essa configuração controla o comportamento da instalação em dispositivos Windows Embedded habilitados com um filtro de gravação. Escolha a opção para confirmar as alterações na data limite da instalação ou durante uma janela de manutenção. Quando você seleciona essa opção, a reinicialização é necessária e as alterações permanecem no dispositivo. Caso contrário, o aplicativo é instalado na sobreposição temporária e confirmado mais tarde. Ao implantar uma sequência de tarefas em um dispositivo Windows Embedded, verifique se o dispositivo é membro de uma coleção com uma janela de manutenção configurada.  

    - **Permitir que a sequência de tarefas seja executada para um cliente na Internet**: especifique se a sequência de tarefas tem permissão para ser executada em um cliente baseado na Internet. Não há suporte para operações que instalam o software, como um sistema operacional, nessa configuração. Use essa opção somente para sequências de tarefas baseadas em script genérico que executam operações no sistema operacional padrão.  

        - A partir da versão 1802, essa configuração é compatível com implantações de uma sequência de tarefas de atualização in-loco do Windows 10 para clientes baseados na Internet por meio do gateway de gerenciamento de nuvem. Para obter mais informações, consulte [Implantar a atualização in-loco do Windows 10 por meio do CMG](#deploy-windows-10-in-place-upgrade-via-cmg).  

8. Na página **Alertas**, especifique as configurações de alerta desejadas para essa implantação de sequência de tarefas.  

9. Na página **Pontos de Distribuição** , especifique as seguintes informações:  

    - **Opções de implantação**: especifique uma das seguintes opções:  

        > [!NOTE]  
        > Ao usar o multicast para implantar um sistema operacional, baixe o conteúdo nos computadores de destino conforme o necessário ou antes da execução da sequência de tarefas.  

        - **Baixar o conteúdo localmente quando necessário executando a sequência de tarefas**: especifique que os clientes baixam conteúdo do ponto de distribuição conforme exigido pela sequência de tarefas. O cliente inicia a sequência de tarefas. Quando uma etapa na sequência de tarefas exigir o conteúdo, ele será baixado antes da execução da etapa.  

        - **Baixar todo o conteúdo localmente antes de iniciar a sequência de tarefas**: especifique que os clientes baixam todo conteúdo do ponto de distribuição antes da execução da sequência de tarefas. Se a sequência de tarefas for disponibilizada para implantações de PXE e de mídia de inicialização na página **Configurações de implantação**, essa opção não aparecerá.  

        - **Acessar conteúdo diretamente de um ponto de distribuição quando for exigido pela sequência de tarefas em execução**: especifique que os clientes executam o conteúdo do ponto de distribuição. Essa opção só é disponibilizada quando todos os pacotes associados à sequência de tarefas estiverem habilitados para usar um compartilhamento de pacotes no ponto de distribuição. Para habilitar o conteúdo a usar um compartilhamento de pacotes, consulte a guia **Acesso a Dados** nas **Propriedades** de cada pacote.  

            > [!IMPORTANT]  
            > Para maior segurança, selecione as opções para **Baixar conteúdo localmente quando necessário, executando a sequência de tarefas** ou **Baixar todo o conteúdo localmente antes de iniciar a sequência de tarefas**. Quando você seleciona uma dessas opções, o Configuration Manager faz o hash do pacote para garantir sua integridade. Quando você seleciona a opção **Acessar conteúdo diretamente de um ponto de distribuição quando necessário, executando a sequência de tarefas**, o Configuration Manager não verifica o hash do pacote antes de executar o programa especificado. Como o site não pode garantir a integridade do pacote, é possível que usuários com direitos administrativos alterem ou adulterem o conteúdo do pacote.  

    - **Quando não houver um ponto de distribuição local disponível, use um ponto de distribuição remoto**: especifique se os clientes podem usar pontos de distribuição de um grupo de limite vizinho para baixar o conteúdo exigido pela sequência de tarefas.  

    - **Permitir que os clientes usem pontos de distribuição do grupo de limites do site padrão**: especifique se os clientes devem baixar o conteúdo de um ponto de distribuição no grupo de limites do site padrão, quando o conteúdo não estiver disponível em um ponto de distribuição nos grupos de limites atuais ou vizinhos.  

        > [!Note]  
        > Da versão 1810 em diante, quando um dispositivo executa uma sequência de tarefas e precisa adquirir conteúdo, ele usa comportamentos de grupo de limites semelhantes ao cliente do Configuration Manager. Para obter mais informações, confira [Suporte de sequência de tarefas para grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgr-osd).<!--1359025-->  

10. Começando no Configuration Manager 1802, na guia **Resumo**, selecione **Salvar como Modelo** para salvar as configurações para reutilização. Forneça um nome para o modelo e selecione as configurações a serem salvas.  

11. Conclua o assistente.  


## <a name="deploy-windows-10-in-place-upgrade-via-cmg"></a>Implantar a atualização in-loco do Windows 10 por meio do CMG

<!-- 1357149 -->
A partir da versão 1802, a sequência de tarefas de atualização in-loco do Windows 10 é compatível com a implantação de clientes baseados na Internet gerenciados por meio do [CMG](/sccm/core/clients/manage/plan-cloud-management-gateway) (gateway de gerenciamento de nuvem). Essa capacidade proporciona aos usuários remotos uma atualização mais fácil para o Windows 10 sem a necessidade de se conectar à intranet.

Certifique-se de que todo o conteúdo referenciado pela sequência de tarefas de upgrade in-loco seja distribuído para um [ponto de distribuição da nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point). Caso contrário, os dispositivos não podem executar a sequência da tarefas.

Ao implantar uma sequência de tarefas de upgrade, use as seguintes configurações:

- **Permitir que a sequência de tarefas seja executada para o cliente na Internet**, na guia Experiência do Usuário da implantação.  

- **Baixar todo o conteúdo localmente antes de iniciar a sequência de tarefas**, na guia Pontos de Distribuição da implantação. Outras opções, como **Baixar conteúdo localmente quando necessário, executando a sequência de tarefas**, não funcionam neste cenário. O mecanismo de sequência de tarefas atualmente não consegue obter conteúdo de um ponto de distribuição da nuvem. O cliente do Configuration Manager deve baixar o conteúdo a partir do ponto de distribuição da nuvem antes de iniciar a sequência de tarefas.  

- (*Opcional*) **Conteúdo pré-baixado para esta sequência de tarefas**, na guia Geral da implantação. Para saber mais, confira [Configurar o conteúdo de armazenamento prévio em cache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  


## <a name="bkmk_high-risk"></a> Implantações de alto risco

Ao executar uma implantação de alto risco, como um sistema operacional, a janela **Selecionar Coleção** exibe somente as coleções personalizadas que atendem às configurações de verificação da implantação definidas nas propriedades do site. As implantações de alto risco sempre estão limitadas às coleções personalizadas criadas e à coleção interna de **Computadores desconhecidos** . Ao criar uma implantação de alto risco, não é possível selecionar uma coleção interna como **Todos os Sistemas**. Para ver todas as coleções personalizadas que contêm menos clientes que o tamanho máximo configurado, desabilite a opção para **Ocultar coleções com uma contagem de membros maior que a configuração de tamanho mínimo do site**. Para obter mais informações, consulte [Configurações para gerenciar implantações de alto risco](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments).  

As configurações de verificação de implantação baseiam-se na associação atual da coleção. Depois de implantar a sequência de tarefas, o Gerenciador de Configurações não reavalia a associação à coleção quanto às configurações de implantação de alto risco.  

Por exemplo, suponhamos que você defina **Tamanho padrão** como 100 e o **Tamanho máximo** como 1000. Ao criar uma implantação de alto risco, a janela **Selecionar Coleção** exibe somente as coleções que contêm menos de 100 clientes. Se você desmarcar a configuração **Ocultar coleções com uma contagem de membros maior que a configuração mínima de tamanho do site**, a janela exibirá coleções que contêm menos de 1.000 clientes.  

Ao selecionar uma coleção que contém uma função de site, o seguinte comportamento se aplica:  

- Se a coleção contiver um servidor do sistema de sites e você definiu as configurações de verificação da implantação para bloquear coleções com servidores do sistema de sites, ocorrerá um erro. Você não poderá continuar criando a implantação.  

- Se um dos critérios a seguir se aplicar, o Assistente de Implantação de Software exibirá um aviso de alto risco. Para continuar, você precisa concordar em criar uma implantação de alto risco. O site gera uma mensagem de status de auditoria.  

    - Se a coleção contiver um servidor do sistema de sites e você definiu as configurações de verificação da implantação para alertar sobre coleções com servidores do sistema de sites  

    - Se a coleção exceder o valor do tamanho padrão

    - Se a coleção contiver um servidor  


## <a name="see-also"></a>Consulte também

[Gerenciar sequências de tarefas para automatizar tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks)
