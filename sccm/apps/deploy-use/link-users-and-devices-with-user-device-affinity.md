---
title: "Vincular usuários e dispositivos com a afinidade de dispositivo de usuário | System Center Configuration Manager"
description: "Vincule usuários e dispositivos à afinidade de dispositivo de usuário e implante aplicativos automaticamente para todos os dispositivos associados a um usuário."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b30b0d5-722d-4d4b-9ed7-5a43de315461
caps.latest.revision: 7
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: bb918eb5f7a69cad47de761a3e95e92926524e3a


---
# <a name="link-users-and-devices-with-user-device-affinity-in-system-center-configuration-manager"></a>Vincular usuários e dispositivos com a afinidade de dispositivo de usuário no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A afinidade de dispositivo de usuário no System Center Configuration Manager associa um usuário a um ou mais dispositivos. Isso pode eliminar a necessidade de conhecer os nomes dos dispositivos de um usuário a fim de implantar um aplicativo nesse usuário. Em vez de implantar o aplicativo em todos os dispositivos do usuário, implante o aplicativo no usuário. Em seguida, a afinidade de dispositivo de usuário garante automaticamente que o aplicativo seja instalado em todos os dispositivos que estão associados a esse usuário.  

 Você pode definir dispositivos primários que normalmente são os dispositivos que os usuários usam diariamente para realizar seu trabalho. Ao criar uma afinidade entre um usuário e um dispositivo, você obtém mais opções de implantação de aplicativo. Por exemplo, se um usuário precisa do Microsoft Office Visio, você pode instalá-lo no dispositivo primário do usuário usando uma implantação do Windows Installer. No entanto, em um dispositivo que não é o primário, você pode implantar o Microsoft Office Visio como um aplicativo virtual. Também é possível usar a afinidade de dispositivo de usuário para pré-implantar o software em um dispositivo do usuário quando o usuário não estiver conectado. Quando o usuário se conectar, o aplicativo já estará instalado e pronto para ser executado.  

 Você deve gerenciar as informações de afinidade de dispositivo de usuário nos computadores. A afinidade de dispositivo de usuário é gerenciada automaticamente pelo Configuration Manager para os dispositivos móveis que ele registra.  

## <a name="manually-configure-user-device-affinity"></a>Configurar manualmente a afinidade de dispositivo de usuário  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Dispositivos**.  

3.  Selecione um dispositivo da lista. Na guia **Início** , no grupo **Dispositivo** , clique em **Editar Usuários Primários**.  

4.  Na caixa de diálogo **Editar Usuários Primários** , procure e selecione os usuários a adicionar como usuários primários para o dispositivo selecionado e clique em **Adicionar**.  

    > [!NOTE]  
    >  A lista **Usuários Primários** exibe os usuários que já são usuários primários desse dispositivo e o método pelo qual a relação usuário-dispositivo foi atribuída.  

## <a name="configure-primary-devices-for-a-user"></a>Configurar dispositivos primários de um usuário  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Usuários**.  

3.  Selecione um usuário da lista. Na guia **Dispositivo** , clique em **Editar Dispositivos Primários**.  

4.  Na caixa de diálogo **Editar Dispositivos Primários** , procure e selecione os dispositivos a adicionar como dispositivos primários para o usuário selecionado e clique em **Adicionar**.  

    > [!NOTE]  
    >  A lista **Dispositivos Primários** exibe os dispositivos que já são configurados como dispositivos primários desse usuário e o método pelo qual a relação usuário-dispositivo foi atribuída.  

## <a name="automatically-create-user-device-affinities-windows-pcs-only"></a>Criar afinidades de dispositivo de usuário automaticamente (somente PCs com Windows)  
 O Configuration Manager lê os dados sobre logons do usuário no log de Eventos do Windows. Para poder criar automaticamente as afinidades de dispositivo, é necessário habilitar as duas configurações a seguir da política de segurança local em computadores cliente para armazenar eventos de logon no log de Eventos do Windows.  

-   **Eventos de logon de conta de auditoria**  

-   **Eventos de logon de auditoria**  

 Você pode usar a política de grupo do Windows para definir essas configurações.  

> [!IMPORTANT]  
>  Se um erro fizer com que o log de Eventos do Windows gere um grande número de entradas, isso poderá resultar na criação de um novo log de eventos. Se isso ocorrer, os eventos do logon existentes poderão ficar indisponíveis para o Configuration Manager.  
>   
>  Tenha cuidado ao implementar **Eventos de logon de conta de auditoria** e **Eventos de logon de auditoria** no Windows XP. Por padrão, a política de retenção é de 7 dias e é provável que esses eventos completarão o Log de Eventos de Segurança. Os usuários padrão não poderão fazer logon se o log de eventos estiver cheio. Para evitar o problema, defina também a política **Método de Retenção** do log de segurança como **Substituir eventos quando necessário**. Para permitir dados suficientes para afinidade de dispositivo de usuário, defina também a política Tamanho máximo do log de segurança com um valor razoável, como 5-20 MB.  

### <a name="configure-the-site-to-automatically-create-user-device-affinities"></a>Configurar o site para automaticamente criar afinidades de dispositivo de usuário  

1.  No console do Configuration Manager, clique em **Administração** > **Configurações do Cliente**.  

3.  Para modificar as configurações do cliente, selecione **Configurações do Cliente Padrão**, na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**. Para criar configurações personalizadas do agente cliente, selecione o nó **Configurações do Cliente** , na guia **Início** , no grupo **Criar** , clique em **Criar Configurações Personalizadas do Dispositivo do Cliente**.  

    > [!NOTE]  
    >  Se você modificar as configurações do cliente padrão, elas serão implantadas em todos os computadores na hierarquia. Para obter mais informações sobre configurações de cliente, consulte [Como definir as configurações do cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

4.  Para a configuração de cliente **Afinidade de Usuário e Dispositivo**, defina o seguinte:  

    -   **Limite de afinidade de dispositivo de usuário (minutos)** - Especifique a quantidade de minutos antes da criação da afinidade de dispositivo de usuário.  

    -   **Limite de afinidade de dispositivo de usuário (dias)** – Especifique a quantidade de dias durante os quais o uso baseado no limite de afinidade é medido.  

    -   **Configurar automaticamente a afinidade de dispositivo de usuário por meio de dados de uso** – Na lista suspensa, selecione **Verdadeiro** para habilitar o site para criar automaticamente afinidades de dispositivo de usuário. Se você selecionar **False**, será necessário aprovar todas as atribuições de afinidade de dispositivo de usuário.  

    > [!TIP]  
    >  **Exemplo:** se **Limite de afinidade de dispositivo de usuário (minutos)** é especificado como **60** minutos e **Limite de afinidade de dispositivo de usuário (dias)** é especificado como **5** dias, o usuário deve usar o dispositivo por, pelo menos, 60 minutos em um período de 5 dias para criar automaticamente uma afinidade de dispositivo de usuário.  
   
Feita a criação de afinidade de dispositivo de usuário automática, o Configuration Manager continua a monitorar os limites de afinidade de dispositivo de usuário. Se a atividade do usuário para o dispositivo estiver abaixo dos limites configurados, a afinidade de dispositivo de usuário será removida. Configure o **Limite de afinidade de dispositivo de usuário (dias)** com o valor mínimo de **7** dias para evitar situações em que a afinidade de dispositivo de usuário configurada automaticamente seja perdida enquanto o usuário não estiver conectado, por exemplo, durante o fim de semana.  

## <a name="import-user-device-affinities-from-a-file"></a>Importar afinidades de dispositivo de usuário de um arquivo  
 É possível importar um arquivo que contém as afinidades de dispositivo de usuário para permitir que você crie muitas relações de uma só vez. Para esse procedimento, é necessário que os dispositivos de entidade tenham sido descobertos e que existam como recursos no banco de dados do Configuration Manager, caso contrário, esse procedimento falhará.  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Usuários** ou **Dispositivos**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Importar Afinidade de Dispositivo de Usuário**.  

4.  Na página **Escolher Mapeamento** do **Assistente de Importação de Afinidade de Dispositivo de Usuário**, especifique as seguintes informações:  

    -   **Nome do arquivo** – Especifique um arquivo CSV (valores separados por vírgula) que contém uma lista de usuários e dispositivos entre os quais se deseja criar uma afinidade. Nesse arquivo, cada par de dispositivo-e-usuário deve estar em uma linha diferente e separado por uma vírgula. Use o formato *<Domínio\>\\<nome de usuário\>*,*<nome NetBIOS do dispositivo\>*.  

    -   **Este arquivo tem títulos de coluna para fins de referência** – Se o arquivo CSV tem uma linha de cabeçalho da linha superior, selecione essa opção e a linha de cabeçalho será ignorada após a importação.  

5.  Se o arquivo que está sendo importado contém mais de dois itens em cada linha, você pode usar **Coluna** e **Atribuir** para especificar quais colunas representam usuários e dispositivos e quais colunas devem ser ignoradas durante a importação.  

6.  Clique em **Próximo** e conclua o **Assistente de Importação de Afinidade de Dispositivo de Usuário**.  

## <a name="let-end-users-create-a-user-device-affinity"></a>Permitir que os usuários finais criem uma afinidade de dispositivo de usuário  
 Use estes procedimentos para permitir que os usuários criem sua própria afinidade de dispositivo de usuário no Centro de Software.  

### <a name="configure-the-site-to-allow-user-created-user-device-affinity-requests"></a>Configurar o site para permitir solicitações de afinidade de dispositivo de usuário criadas pelo usuário  

1.  No console do Configuration Manager, clique em **Administração** > **Configurações do Cliente**.  

3.  Para modificar as configurações do cliente, selecione **Configurações do Cliente Padrão**, na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**. Para criar configurações personalizadas do agente cliente, selecione o nó **Configurações do Cliente** , na guia **Início** , no grupo **Criar** , clique em **Criar Configurações Personalizadas do Usuário**.  

    > [!NOTE]  
    >  Se você modificar as configurações do cliente padrão, elas serão implantadas em todos os computadores na hierarquia. Para obter mais informações sobre como definir configurações do cliente, veja [Definir configurações do cliente](../../core/clients/deploy/configure-client-settings.md).  

4.  Selecione a configuração do cliente **Afinidade de Dispositivo e de Usuário** e, na lista suspensa **Permitir que o usuário defina seus dispositivos primários** , selecione **True**.  

### <a name="configure-a-user-device-affinity"></a>Configurar uma afinidade de dispositivo de usuário  

1.  No Catálogo de Aplicativos, clique em **Meus Sistemas**.  

2.  Habilite a opção **Uso regularmente este computador para trabalho**.  

## <a name="manage-user-device-affinity-requests-from-users"></a>Gerenciar solicitações de afinidade de dispositivo de usuário dos usuários  
 Quando a configuração do cliente **Configurar automaticamente a afinidade de dispositivo de usuário por meio de dados de uso** está definida como **False**, é necessário aprovar todas as atribuições de afinidade de dispositivo de usuário.  

### <a name="approve-or-reject-a-user-device-affinity-request"></a>Aprovar ou rejeitar uma atribuição de afinidade de dispositivo de usuário  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , selecione a coleção de usuário ou dispositivo para a qual você deseja gerenciar as solicitações de afinidade.  

3.  Na guia **Início** , no grupo **Coleção** , clique em **Gerenciar Solicitações de Afinidade**.  

4.  Na caixa de diálogo **Gerenciar Solicitações de Afinidade de Dispositivo de Usuário** , selecione uma solicitação de afinidade e clique em **Aprovar** ou **Rejeitar**.  



<!--HONumber=Nov16_HO1-->


