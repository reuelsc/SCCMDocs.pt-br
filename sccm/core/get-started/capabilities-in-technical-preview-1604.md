---
title: Funcionalidades no Technical Preview 1604 do Configuration Manager
description: "Saiba mais sobre os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1604."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 684a5559-9e6e-469b-86ae-e768e9f0c9ac
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5d08d1f9ccd995d544c3c21c4af52ede73343077
ms.openlocfilehash: d36de897e6407ec7431d4dbe24ad04423aee2ca1

---
# <a name="capabilities-in-technical-preview-1604-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1604 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1604. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview.      Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de um technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos em um technical preview.  

 Veja a seguir os novos recursos que você pode experimentar nesta versão.  

##  <a name="a-namebkmkwindowsvppa-manage-volume-purchased-apps-from-the-windows-store-for-business"></a><a name="BKMK_WindowsVPP"></a> Gerenciar aplicativos adquiridos por volume da Windows Store para Empresas  
 Na [Windows Store para Empresas](https://www.microsoft.com/en-us/business-store), é possível encontrar e adquirir aplicativos para sua organização, individualmente ou por volume. Ao conectar a loja ao Configuration Manager, é possível gerenciar aplicativos adquiridos por volume no console do Configuration Manager, por exemplo:  

-   É possível sincronizar a lista de aplicativos adquiridos com o Configuration Manager  

-   Os aplicativos que são sincronizados aparecem no console do Configuration Manager e você pode implantá-los como qualquer outro aplicativo  

-   É possível acompanhar quantas licenças estão disponíveis e quantas estão sendo usadas no console do Configuration Manager  

### <a name="try-it-out"></a>Experimente!  

##### <a name="scenario-1-set-up-windows-store-for-business-synchronization"></a>Cenário 1: Configurar a sincronização da Windows Store para Empresas  

1.  No Azure Active Directory, registre o Configuration Manager como uma ferramenta de gerenciamento de "Aplicativo Web e/ou API da Web". Isso fornecerá uma ID de cliente que você precisará mais tarde.  

    1.  No nó **Active Directory** de [https://manage.windowsazure.com](https://manage.windowsazure.com), selecione seu Azure Active Directory e clique em **Aplicativos** > **Adicionar**.  

    2.  Clique em **Adicionar um aplicativo que minha organização esteja desenvolvendo**.  

    3.  Insira um nome para o aplicativo, selecione **Aplicativo Web** e/ou **API da Web** e clique na seta Avançar.  

    4.  Insira a mesma URL para **URL de Entrada** e **URI da ID do Aplicativo**.  A URL pode ser qualquer uma e não precisa ser resolvida para um endereço real. Por exemplo, você pode inserir **https://&lt;seudomínio\>/sccm**.  

    5.  Conclua o assistente.  

2.  No Azure Active Directory, crie uma chave de cliente para a ferramenta de gerenciamento registrada.  

    1.  Realce o aplicativo que você acabou de criar e clique em **Configurar**.  

    2.  Em **Chaves**, escolha uma duração na lista e clique em **Salvar**.  Isso criará uma nova chave de cliente.  Não saia dessa página até que você tenha carregado com êxito a Windows Store para Empresas no Configuration Manager.  

3.  Na Windows Store para Empresas, configure o Configuration Manager como a ferramenta de gerenciamento da loja.  

    1.  Abra [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) e se conecte, se solicitado.  

    2.  Aceite os termos de uso, se necessário.  

    3.  Em **Ferramentas de Gerenciamento**, clique em **Adicionar uma ferramenta de gerenciamento**.  

    4.  Em **Pesquisar a ferramenta por nome**, digite o nome do aplicativo que você criou anteriormente no AAD e clique em **Adicionar**.  

    5.  Clique em **Ativar** ao lado do aplicativo que você acabou de importar.  

    6.  No assistente **Exibir Aplicativos Licenciados Offline**, clique em **Sim** se quiser permitir que aplicativos licenciados offline sejam comprados.  

4.  Compre pelo menos um aplicativo da Windows Store para Empresas.  

5.  No espaço de trabalho **Administração** do console do Configuration Manager, expanda **Serviços de Nuvem** e clique em **Windows Store para Empresas**.  

6.  Na guia **Início**, no grupo **Criar**, clique em **Adicionar Conta da Windows Store para Empresas**.  

7.  Adicione a ID de locatário, a id de cliente e a chave de cliente do Azure Active Directory e conclua o assistente.  

8.  Quando terminar, você verá a conta configurada na lista **Contas da Windows Store para Empresas** no console do Configuration Manager.  

##### <a name="scenario-2-create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-offline-licensed-app"></a>Cenário 2: Criar e implantar um aplicativo do Configuration Manager por meio de um aplicativo licenciado offline da Windows Store para Empresas  

1.  No espaço de trabalho **Biblioteca de Software** do console do Configuration Manager, expanda **Gerenciamento de Aplicativos** e clique em **Informações sobre Licença para Aplicativos da Loja**.  

2.  A lista **Aplicativos comprados na Windows Store para Empresas** mostra uma lista de aplicativos que foram sincronizados da loja. Escolha o aplicativo que deseja implantar e, na guia **Início**, no grupo **Criar**, clique em **Criar Aplicativo**.  

3.  É criado um aplicativo do Configuration Manager contendo o aplicativo da Windows Store para Empresas. Em seguida, é possível implantar e monitorar o aplicativo, como você faria com qualquer outro aplicativo do Configuration Manager.  

##  <a name="a-namebkmkpfwa-improvements-to-microsoft-passport-for-work-management"></a><a name="BKMK_PFW"></a> Melhorias no gerenciamento do Microsoft Passport for Work  
 Agora, é possível implantar políticas do Passport for Work em dispositivos Windows 10 ingressados no domínio e gerenciados pelo cliente do Configuration Manager.  

##  <a name="a-namebkmkswitchsupa-option-for-clients-to-switch-to-a-new-software-update-point"></a><a name="bkmk_switchsup"></a> Opção para clientes alternarem para um novo ponto de atualização de software  
 No Technical Preview 1604, você pode habilitar a opção para clientes do Configuration Manager mudarem para um novo ponto de atualização de software quando houver problemas com o ponto de atualização de software ativo. Para essa opção, você deve ter vários pontos de atualização de software disponíveis em um site primário. Habilite essa opção em uma coleção de dispositivos e, uma vez habilitada, os clientes na coleção procurarão por outro ponto de atualização de software na próxima verificação, quando o cliente não conseguir se conectar com êxito ao ponto de atualização de software ativo. Dependendo de suas definições de configuração do WSUS (classificações de atualização, produtos etc.), mudar para um novo ponto de atualização de software gerará tráfego de rede adicional. Portanto, você deve usar essa opção apenas quando for necessário.  

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>Para habilitar a opção de alternar pontos de atualização de software  

1.  No console do Configuration Manager, vá até **Ativos e Conformidade > Visão Geral > Coleções de Dispositivos**.  

2.  Na guia **Início** , no grupo **Coleção** , clique em **Notificação do Cliente**e em **Alternar para o próximo ponto de atualização de software**.  

> [!NOTE]  
>  Essa opção só está disponível em sites que possuem vários pontos de atualização de software.  

##  <a name="a-namebkmkpeercachea-client-settings-to-manage-client-cache-settings-and-client-peer-cache"></a><a name="bkmk_peercache"></a> Definições do cliente para gerenciar Configurações de Cache do Cliente e Cache de Mesmo Nível do cliente  
 A versão de visualização 1604 introduz duas novas configurações de cliente de dispositivo que afetam o uso de um cache do cliente. Ambas podem ser usadas individualmente, mas são configuradas na mesma folha de propriedades para configurações do cliente e se combinam para ajudar você a gerenciar a implantação de conteúdo em seus clientes em locais remotos.  

-   A primeira é o **Cache Par do cliente**, uma solução interna do Configuration Manager para clientes compartilharem conteúdo com outros clientes diretamente do cache local. Para clientes do Cache de Mesmo Nível compartilharem conteúdo, eles devem ser membros do mesmo grupo de limites. O Cache Par não substitui o uso de outras soluções como o BranchCache, mas trabalha lado a lado para fornecer a você mais opções para estender as soluções tradicionais de implantação de conteúdo, como os pontos de distribuição.  

     Depois de implantar configurações do cliente que habilitam o Cache Par para uma coleção, os membros dessa coleção podem atuar como uma fonte de conteúdo par para outros clientes em seu grupo de limites.  O cliente que opera como fonte de conteúdo par enviará uma lista do conteúdo disponível que ele armazenou em cache para seu ponto de gerenciamento. Depois, quando o próximo cliente do grupo de limites solicitar o conteúdo, a fonte de cache par será oferecida como uma fonte de conteúdo potencial em conjunto com todos os pontos de distribuição que estiverem configurados para serem rápidos. O cliente seleciona uma fonte de conteúdo aleatória desse pool combinado de fontes de conteúdo. Os clientes buscarão conteúdo de um ponto de distribuição configurado para ser lento apenas quando não houver pontos de distribuição rápidos ou fontes de cache par presentes no grupo de limites.  

-   A segunda nova configuração permite que você **gerencie o tamanho do cache** nos clientes. Você pode configurar o cache para ter um tamanho máximo em megabytes e um tamanho máximo como um percentual do espaço na unidade do cliente.  O cliente impõe a configuração que for atingida primeiro.  

Para ajudar você a entender o uso do Cache Par do cliente, exiba o painel **Fontes de Dados do Cliente**. No console, vá para **Monitoramento > Status do Cliente > Fontes de Dados do Cliente**. Aqui você pode escolher um período de tempo para aplicar ao painel. Em seguida, na exibição, escolha o grupo de limites ou o pacote do qual quer ver informações. Ao exibir as informações, você pode passar o mouse sobre a superfície para ver mais detalhes sobre conteúdo ou as origens da política.  

 Também é possível usar um novo relatório, **Fontes de Dados do Cliente — Resumo**, para exibir um resumo das fontes de dados do cliente de cada grupo de limites.   
**Requisitos para usar o Cache Par:**  

-   É necessário configurar seu site com uma **Conta de Acesso à Rede** que tenha **Controle Total** da pasta de cache em cada cliente. Por padrão, a pasta é **%windir%\ccmcache**  

-   Os clientes poderão transferir conteúdo usando o Cache de Mesmo Nível apenas quando eles forem membros do mesmo grupo de limites.  

#### <a name="to-configure-client-peer-cache-client-settings"></a>Para definir as configurações do cliente do Cache Par  

1.  As configurações são definidas na mesma página de configurações do cliente. No console do Configuration Manager, vá até **Administração > Configurações do Cliente** e abra o objeto de configurações do cliente do dispositivo que deseja usar. Também é possível alterar o objeto de Configurações Padrão do Cliente.  

2.  Na lista de configurações disponíveis, selecione **Configurações de Cache do Cliente**.  

3.  Para gerenciar o tamanho do cache, defina **Configurar o tamanho do cache do cliente** como **Sim**. Em seguida, configure o tamanho máximo do cache tanto em megabytes e quanto em um percentual do espaço da unidade do cliente.  

4.  Para habilitar os clientes a participarem o Cache Par de clientes, defina **Habilitar cliente do Configuration Manager em um SO completo para compartilhar conteúdo** como **Sim**. Em seguida, você pode configurar as portas usadas pelos clientes, incluindo se elas serão HTTP ou HTTPS.  

### <a name="try-it-out"></a>Experimente!  
 Tente concluir as seguintes tarefas e depois use as informações dos comentários perto da parte superior deste tópico para nos contar como foi:  

1.  Modifique as configurações de cliente para especificar um novo tamanho para o cache do cliente e confirme essa configuração em um cliente.  

2.  Use as configurações de cliente para configurar vários clientes para usar o Cache Par  

3.  Implante conteúdo nos clientes de modo que alguns, ou a maioria dos clientes, o obtenham de outro cliente usando o Cache Par.  Você pode confirmar a fonte do conteúdo usada exibindo o novo painel.  

    > [!NOTE]  
    >  Para concluir essa tarefa com a visualização técnica e um único ponto de distribuição, configure o ponto de distribuição para ser lento para o local de rede de todos os seus clientes. Em seguida, distribua o conteúdo para um único cliente.  Depois que esse cliente estiver com o conteúdo, distribua o conteúdo aos clientes adicionais que devem localizar pares locais para usar como uma fonte de conteúdo antes de usar o ponto de distribuição que é considerado lento no local do cliente.  

##  <a name="a-namebkmkpassporta-support-for-passport-for-work-as-a-ksp"></a><a name="bkmk_passport"></a> Suporte ao Passport for Work como um KSP  
 O System Center Configuration Manager permite a integração ao Microsoft Passport for Work, que é um método de entrada alternativo que usa o Active Directory ou uma conta do Azure Active Directory para substituir uma senha, um cartão inteligente ou um cartão inteligente virtual.  
O Passport permite que você use um gesto de usuário para logon, em vez de uma senha. Um gesto do usuário pode ser um PIN simples, uma autenticação biométrica, como o Windows Hello, ou um dispositivo externo, como um leitor de impressão digital.  

-   Você pode usar o Configuration Manager para controlar quais gestos os usuários podem e não podem usar no logon e para configurar os requisitos de complexidade do PIN.  

-   Você pode armazenar certificados de autenticação no Passport for Work para o KPS (provedor de armazenamento de chaves).  

Quando um usuário cria um PIN do Passport, o Windows envia uma notificação que o Configuration Manager escuta.  Isso permite que o Configuration Manager reconheça rapidamente quais usuários criaram um PIN do Passport. O Configuration Manager também poderá emitir novos certificados para esses usuários se o Passport for usado como o Provedor de Armazenamento de Chaves em um perfil de certificado.  

##  <a name="a-namebkmkonpremdhaa-on-premises-device-health-attestation"></a><a name="bkmk_onpremdha"></a> Atestado de integridade do dispositivo local  
 O atestado de integridade para dispositivos Windows 10 agora podem ser configurados para comunicação usando a infraestrutura local.  Os administradores podem especificar se o relatório é gerado pelos recursos locais ou na nuvem.  Se **local** for escolhido para o relatório de atestado de integridade, um URI poderá ser especificado para o dispositivo. Isso permite que os PCs cliente sem acesso à Internet habilitem e gerenciem dispositivos usando o atestado de integridade.  

#### <a name="enable-health-attestation-for-on-premises-devices"></a>Habilitar atestado de integridade para dispositivos no local  

1.  No console do Configuration Manager, navegue para **Administração** > **Visão Geral** > **Configurações do cliente**e defina **Usar Serviço de Atestado de Integridade local** como **Sim**.  

2.  Especifique a **URL do Serviço de Atestado de Integridade local**e clique em **OK**.  

Para testar, configure o Serviço de Atesto de Integridade local usando as configurações do agente cliente.  

##  <a name="a-namebkmksmarta-smartlock-setting-for-android-devices"></a><a name="BKMK_Smart"></a> Configuração do SmartLock para dispositivos Android  
 Uma nova configuração, **Permitir SmartLock e outros agentes de confiança**, foi adicionada ao item de configuração **Android e Samsung KNOX**, que permite controlar o recurso SmartLock em dispositivos Android compatíveis. Essa capacidade do telefone, às vezes conhecida como agentes de confiança, permite desabilitar ou ignorar a senha da tela de bloqueio do dispositivo se o dispositivo estiver em um local confiável, como quando ele está conectado a um dispositivo Bluetooth específico, ou quando ele está perto de uma marca NFC. Você pode usar essa configuração para impedir que os usuários finais configurem o SmartLock.  



<!--HONumber=Jan17_HO4-->


