---
title: "Vincular usuários e dispositivos com a afinidade de dispositivo de usuário | Microsoft Docs"
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
ms.sourcegitcommit: 6b1393b2a329bcd017dc961366afb09fa7a77899
ms.openlocfilehash: 4e8e677851ad9ae7d027ab685e842a8ff5e35573


---
# <a name="link-users-and-devices-with-user-device-affinity-in-system-center-configuration-manager"></a>Vincular usuários e dispositivos com a afinidade de dispositivo de usuário no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A afinidade de dispositivo de usuário no System Center Configuration Manager (Configuration Manager) associa um usuário a um ou mais dispositivos. Isso pode eliminar a necessidade de saber os nomes dos dispositivos de um usuário a fim de implantar um aplicativo nesse usuário. Em vez de implantar o aplicativo em todos os dispositivos do usuário, implante o aplicativo no usuário. Em seguida, a afinidade de dispositivo de usuário garante automaticamente que o aplicativo seja instalado em todos os dispositivos que estão associados a esse usuário.  

 É possível definir dispositivos primários que normalmente são os dispositivos que os usuários usam diariamente para realizar seu trabalho. Ao criar uma afinidade entre um usuário e um dispositivo, você obtém mais opções de implantação de aplicativo. Por exemplo, se um usuário precisar do Microsoft Visio, será possível instalá-lo no dispositivo primário do usuário usando uma implantação do Windows Installer. No entanto, em um dispositivo que não é o primário, talvez o Visio seja implantado como um aplicativo virtual. Também é possível usar a afinidade de dispositivo de usuário para pré-implantar o software em um dispositivo do usuário quando o usuário não estiver conectado. Quando o usuário se conectar, o aplicativo já estará instalado e pronto para ser executado.  

 Você deve gerenciar as informações de afinidade de dispositivo de usuário nos computadores. O Configuration Manager gerencia automaticamente as afinidades de dispositivo de usuário para os dispositivos móveis que ele registra.  

## <a name="manually-set-up-user-device-affinity"></a>Configurar a afinidade de dispositivo de usuário manualmente  

1.  No console do Configuration Manager, escolha **Ativos e Conformidade** > **Dispositivos**.  

3.  Na lista, selecione um dispositivo. Em seguida, na guia **Início**, no grupo **Dispositivo**, escolha **Editar Usuários Primários**.  

4.  Na caixa de diálogo **Editar Usuários Primários**, pesquise e, em seguida, selecione os usuários a serem adicionados como usuários primários para o dispositivo selecionado. Escolha **Adicionar**.  

    > [!NOTE]  
    > A lista **Usuários Primários** mostra os usuários que já são usuários primários desse dispositivo e o método pelo qual a relação usuário-dispositivo foi atribuída.  

## <a name="set-up-primary-devices-for-a-user"></a>Configurar dispositivos primários para um usuário  

1.  No console do Configuration Manager, escolha **Ativos e Conformidade** > **Usuários**.  

3.  Na lista, selecione um usuário. Em seguida, na guia **Dispositivo**, escolha **Editar Dispositivos Primários**.  

4.  Na caixa de diálogo **Editar Dispositivos Primários**, pesquise e selecione os dispositivos a serem adicionados como dispositivos primários para o usuário selecionado. Escolha **Adicionar**.  

    > [!NOTE]  
    > A lista **Dispositivos Primários** exibe os dispositivos que já estão configurados como dispositivos primários desse usuário e o método pelo qual a relação usuário-dispositivo foi atribuída.  

## <a name="automatically-create-user-device-affinities-windows-pcs-only"></a>Criar afinidades de dispositivo de usuário automaticamente (somente PCs com Windows)  
 O Configuration Manager lê os dados sobre logons do usuário no log de Eventos do Windows. Para criar afinidades de dispositivo de usuário automaticamente, é necessário ativar estas duas opções na política de segurança local nos computadores cliente para armazenar os eventos de logon no log de Eventos do Windows:  

-   **Eventos de logon de conta de auditoria**  
-   **Eventos de logon de auditoria**  

 Para definir essas configurações, use a Política de Grupo do Windows.  

> [!IMPORTANT]  
> Se um erro fizer com que o log de eventos do Windows gere um número elevado de entradas, um novo log de eventos poderá ser criado. Se isso ocorrer, os eventos do logon existentes poderão ficar indisponíveis para o Configuration Manager.  
>   
> Tenha cuidado ao ativar as configurações **Eventos de logon de conta de auditoria** e **Eventos de logon de auditoria** no Windows XP. Por padrão, a política de retenção é de 7 dias e é provável que esses eventos preencherão o log de eventos de segurança. Os usuários padrão não poderão fazer logon se o log de eventos estiver cheio. Para evitar isso, para o log de eventos de segurança, defina o valor do **Método de Retenção** da política como **Substituir eventos quando necessário**. Para ter dados suficientes para a afinidade de dispositivo de usuário, defina também o tamanho do log de eventos de segurança máxima da política com um valor razoável, como 5-20 MB.  

### <a name="set-up-the-site-to-automatically-create-user-device-affinities"></a>Configurar o site para criar afinidades de dispositivo de usuário automaticamente  

1.  No console do Configuration Manager, escolha **Administração** > **Configurações do Cliente**.  

2.  Para modificar as configurações padrão do cliente, selecione **Configurações do Cliente Padrão** e, na guia **Início**, no grupo **Propriedades**, escolha **Propriedades**. Para criar configurações personalizadas do agente cliente, selecione o nó **Configurações do Cliente** e, na guia **Início**, no grupo **Criar**, escolha **Criar Configurações Personalizadas do Dispositivo Cliente**.  

    > [!NOTE]  
    > Se você modificar as configurações do cliente padrão, elas serão implantadas em todos os computadores na hierarquia. Para obter mais informações sobre configurações de cliente, consulte [Como definir as configurações do cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

3.  Para **Afinidade de Usuário e Dispositivo**, defina o seguinte:  

    -   **Limite de afinidade de dispositivo de usuário (minutos)**. Defina o número de minutos de uso do dispositivo antes da criação da afinidade de dispositivo de usuário.  

    -   **Limite de afinidade de dispositivo de usuário (dias)**. Defina o número de dias durante os quais o limite de afinidade baseado em uso é medido.  

    -   **Configurar automaticamente a afinidade de dispositivo de usuário por meio de dados de uso**. Para permitir que o site crie afinidades de dispositivo de usuário automaticamente, na lista suspensa, selecione **Verdadeiro**. Se você selecionar **Falso**, será necessário aprovar todas as atribuições de afinidade de dispositivo de usuário.  

    > [!TIP]  
    > **Exemplo:** se você definir **Limite de afinidade de dispositivo de usuário (minutos)** como **60** minutos e **Limite de afinidade de dispositivo de usuário (dias)** como **5** dias, o usuário deverá usar o dispositivo durante, pelo menos, 60 minutos em um período de 5 dias para criar uma afinidade de dispositivo de usuário automaticamente.  

Feita a criação de afinidade de dispositivo de usuário automática, o Configuration Manager continua a monitorar os limites de afinidade de dispositivo de usuário. Se a atividade do usuário para o dispositivo estiver abaixo dos limites definidos, a afinidade de dispositivo de usuário será removida. Defina o **Limite de afinidade de dispositivo de usuário (dias)** com o valor mínimo de **7** dias, para evitar situações em que a afinidade de dispositivo de usuário configurada automaticamente possa ser perdida enquanto o usuário não estiver conectado, por exemplo, durante o fim de semana.  

## <a name="import-user-device-affinities-from-a-file"></a>Importar afinidades de dispositivo de usuário de um arquivo  
 Para criar várias relações ao mesmo tempo, é possível importar um arquivo que contém os detalhes de várias afinidades de dispositivo de usuário. Para esse procedimento, é necessário que os dispositivos da entidade tenham sido descobertos e existam como recursos no banco de dados do Configuration Manager; caso contrário, o procedimento falhará.  

1.  No console do Configuration Manager, escolha **Ativos e Conformidade** > **Usuários** ou **Dispositivos**.  

2.  Na guia **Início**, no grupo **Criar**, escolha **Importar Afinidade de Dispositivo de Usuário**.  

3.  No Assistente de Importação de Afinidade de Dispositivo de Usuário, na página **Escolher Mapeamento**, defina estas informações:  

    -   **Nome do arquivo**. Especifique um arquivo CSV (valores separados por vírgula) que contém uma lista de usuários e dispositivos entre os quais você deseja criar uma afinidade. Nesse arquivo, cada par dispositivo/usuário deve estar em sua própria linha, com valores separados por uma vírgula. Use este formato: <*Domínio*>&#92;<*nome de usuário*>,<*nome NetBIOS do dispositivo*>.  

    -   **Esse arquivo tem cabeçalhos de coluna para fins de referência**. Se o arquivo .csv tiver um cabeçalho de linha superior, selecione essa opção e a linha de cabeçalho será ignorada durante a importação.  

4.  Se o arquivo que está sendo importado tiver mais de dois itens em cada linha, você poderá usar **Coluna** e **Atribuir** para especificar quais colunas representam os usuários e dispositivos e quais colunas devem ser ignoradas durante a importação.  

5.  Escolha **Avançar** e conclua o Assistente de Importação de Afinidade de Dispositivo de Usuário.  

## <a name="let-users-create-their-own-device-affinities"></a>Permitir que os usuários criem suas próprias afinidades de dispositivo  
 Com os procedimentos a seguir, é possível configurar um usuário para criar sua própria afinidade de dispositivo de usuário no aplicativo Centro de Software.  

### <a name="set-up-the-site-to-allow-user-created-user-device-affinity-requests"></a>Configurar o site para permitir solicitações de afinidade de dispositivo de usuário criadas pelo usuário  

1.  No console do Configuration Manager, escolha **Administração** > **Configurações do Cliente**.  

2.  Para modificar as configurações padrão do cliente, selecione **Configurações do Cliente Padrão** e, na guia **Início**, no grupo **Propriedades**, escolha **Propriedades**. Para criar configurações personalizadas do agente cliente, selecione o nó **Configurações do Cliente** e, na guia **Início**, no grupo **Criar**, escolha **Criar Configurações Personalizadas do Usuário Cliente**.  

    > [!NOTE]  
    > Se você modificar as configurações do cliente padrão, elas serão implantadas em todos os computadores na hierarquia. Para obter mais informações sobre como definir configurações do cliente, veja [Definir configurações do cliente](../../core/clients/deploy/configure-client-settings.md).  

3.  Selecione a configuração do cliente **Afinidade de Dispositivo e de Usuário** e, na lista suspensa **Permitir que o usuário defina seus dispositivos primários** , selecione **True**.  

### <a name="set-up-a-user-device-affinity"></a>Configurar uma afinidade de dispositivo de usuário  

1.  No Catálogo de Aplicativos, escolha **Meus Sistemas**.  

2.  Selecione a opção **Uso regularmente este computador para trabalho**.  

## <a name="manage-user-device-affinity-requests-from-users"></a>Gerenciar solicitações de afinidade de dispositivo de usuário dos usuários  
 Quando a configuração do cliente **Configurar automaticamente a afinidade de dispositivo de usuário por meio de dados de uso** está definida como **False**, é necessário aprovar todas as atribuições de afinidade de dispositivo de usuário.  

### <a name="approve-or-reject-a-user-device-affinity-request"></a>Aprovar ou rejeitar uma atribuição de afinidade de dispositivo de usuário  

1.  No console do Configuration Manager, escolha **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , selecione a coleção de usuário ou dispositivo para a qual você deseja gerenciar as solicitações de afinidade.  

3.  Na guia **Início**, no grupo **Coleção**, escolha **Gerenciar Solicitações de Afinidade**.  

4.  Na caixa de diálogo **Gerenciar Solicitações de Afinidade de Dispositivo de Usuário**, selecione uma solicitação de afinidade e escolha **Aprovar** ou **Rejeitar**.  



<!--HONumber=Dec16_HO3-->


