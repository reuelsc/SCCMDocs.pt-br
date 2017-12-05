---
title: Recursos no Technical Preview 1601
titleSuffix: Configuration Manager
description: "Saiba mais sobre os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1601."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aae1cf2f-2c04-4f68-a03a-f4a925433c09
caps.latest.revision: "7"
author: erikje
ms.author: erikje
manager: angrobe
robots: noindex,nofollow
ms.openlocfilehash: 70efb483ac15ba14497b884ed753032e8e48a4b5
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="capabilities-in-technical-preview-1601-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1601 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1601. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview.      Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de um technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos em um technical preview.  

 **Problemas conhecidos nesse Technical Preview:**  

-   quando você gerencia **Opções de Atualização do Cliente** para promover um cliente de pré-produção para produção, o texto da caixa de seleção exibe uma versão de cliente zero (0) em vez do número real de build do cliente. A versão correta do cliente de pré-produção é mostrada na superfície acima dessa opção e é a versão do cliente que é promovida para a produção quando você seleciona essa opção.  

-   Ao atualizar para o Technical Preview 1601 e escolher testar o cliente do Configuration Manager em uma coleção de pré-produção, o pacote do cliente para a coleção não será atualizado. Esse problema é apenas na Technical Preview 1601.  

     Para contornar esse problema, siga uma destas etapas:  

    -   Execute o seguinte script SQL no banco de dados do site primário:  

        ```  
        DECLARE @PilotingPkgID NVARCHAR(8)  

        SELECT @PilotingPkgID = PilotingPackageID FROM ClientDeploymentSettings  

        MERGE INTO PkgServers_G AS T  
        USING (  
            SELECT @PilotingPkgID AS PkgID, NALPath, SiteCode, SiteName, SourceSite, RefreshTrigger, UpdateMask, [Action]  
            FROM PkgServers_G WHERE PkgID IN (SELECT UpgradePackageID FROM ClientDeploymentSettings)  
            ) AS S  
        ON T.PkgID = S.PkgID and T.NALPath = S.NALPath  

        WHEN NOT MATCHED THEN  
            INSERT (PkgID, NALPATH, SiteCode, SiteName, SourceSite, LastRefresh, RefreshTrigger, UpdateMask, [Action])  
            VALUES (S.PkgID, S.NALPath, S.SiteCode, S.SiteName, S.SourceSite, GetUTCDate(), S.RefreshTrigger, S.UpdateMask, S.[Action])  
        ;  

        ```  

    -   Adicione uma nova função do sistema de sites de ponto de distribuição ao seu site de laboratório. O novo ponto de distribuição atualizará a coleção de pré-produção com o novo pacote do cliente.  

**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  

##  <a name="bkmk_hybrid1"></a> Melhorias para a integração do Microsoft Intune  
Na Visualização técnica 1601, adicionamos suporte para os seguintes recursos:  

### <a name="improvements-to-conditional-access"></a>Aprimoramentos ao acesso condicional  

-   **Suporte a acesso condicional para PCs gerenciados pelo System Center Configuration Manager**  

     Agora você pode definir políticas de acesso condicional para PCs gerenciados pelo System Center Configuration Manager, as quais exigirão que os PCs estejam em conformidade com a política de conformidade para acessar os serviços do Exchange Online e do SharePoint Online.  Com essa nova funcionalidade, você também pode registrar PCs com o AD do Azure por meio da política de conformidade e monitorar e informar sobre o registro do AD do Azure.  

    > [!NOTE]  
    >  O Acesso Condicional ainda não tem suporte no Windows 10.  

    A seguir, os pré-requisitos para usar esse recurso:  

    -   Assinatura Azure Active Directory Premium e sincronização do AD FS.  

    -   Uma assinatura do Microsoft Intune. A assinatura do Microsoft Intune deve ser configurada no console do Configuration Manager.  

    -   [Pré-requisitos para registro automático do Azure AD](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    Para usar a opção, você deve criar uma política de conformidade no Configuration Manager com regras específicas descritas abaixo e definir uma política de acesso condicional no console do Intune.  Além disso, para garantir que apenas PCs compatíveis tenham permissão de acesso, você deve definir o requisito de PC do Windows para a opção **Os dispositivos devem ser compatíveis**. A seguir, as regras de política compatíveis que se aplicam a PCs gerenciados pelo System Center Configuration Manager.  

    -   **Requer registro no Azure Active Directory:** essa regra verifica se o dispositivo do usuário é o local de trabalho associado ao Azure AD; se não, o dispositivo será registrado automaticamente no Azure AD. O registro automático só tem suporte no Windows 8.1. Para PCs com Windows 7, implante um MSI para realizar o registro automático. Para mais informações, consulte [aqui](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    -   **Todas as atualizações necessárias instaladas com um prazo superior a determinado número de dias:** essa regra verifica se o dispositivo do usuário tem todas as atualizações necessárias (especificadas na regra **Atualizações automáticas necessárias**) dentro do prazo e período de carência especificado por você e instala automaticamente as atualizações necessárias.  

    -   **Exigir criptografia de unidade de disco BitLocker:** essa é uma verificação para ver se a unidade principal (por exemplo, C:\\) no dispositivo é criptografada pelo BitLocker. Se a criptografia Bitlocker não estiver habilitada no dispositivo primário, o acesso aos serviços de email e do SharePoint será bloqueado.  

    -   **Exigir Antimalware:** essa é uma verificação para ver se o software antimalware (somente System Center Endpoint Protection ou Windows Defender) está habilitado e em execução.  
         Se não estiver habilitado, o acesso aos serviços de email e do SharePoint estará bloqueado.  

    Usuários finais bloqueados por falta de conformidade verão informações de conformidade no Centro de Software do SCCM e iniciarão uma nova avaliação de política quando problemas de conformidade forem corrigidos.  

-   **Acesso condicional com o Serviço de atestado de integridade** Agora você pode restringir o acesso a email e aos serviços 0365 com base na integridade dos dispositivos, conforme relatado pelo Serviço de atestado de integridade.  Além disso, os dispositivos gerenciados pelo Intune são incluídos nos relatórios de integridade do dispositivo.  

    Uma nova regra de conformidade foi adicionada ao console do Configuration Manager, permitindo que você especifique se os dispositivos devem ter o acesso permitido ou bloqueado com base em seu status de integridade.  Para criar essa regra, abra o assistente **Criar Política de Conformidade** e adicione uma nova regra.  Selecione **Informado como íntegro pelo Serviço de Atestado de Integridade** para a condição e defina o valor como **Verdadeiro**.  Isso assegurará que somente dispositivos informados como íntegros tenham acesso aos recursos da empresa. Para obter detalhes sobre o Serviço de atestado de integridade e como a integridade dos dispositivos é informada no Intune, veja [Atestado de Integridade do Dispositivo](#bkmk_devicehealth).  

-   **Novas configurações de política de conformidade:** as novas configurações de política de conformidade ajudam a melhorar a segurança e a proteção em dispositivos usados para acessar serviços de email e do SharePoint da empresa:  

    -   **Requer atualizações automáticas:** você pode precisar de dispositivos com Windows 8.1 ou posterior para permitir a instalação automática de atualizações e também especificar a classe da atualizações instaladas.  Você pode optar por: instalar somente atualizações marcadas como importantes ou instalar todas as atualizações recomendadas.  

         Para criar uma regra para atualizações automáticas, abra o assistente **Criar Política de Conformidade** e adicione uma nova regra.  Selecione **Classificação mínima das atualizações necessárias** como a condição e defina o valor para um dos valores disponíveis: **Nenhum**, **Recomendado** e **Importante**.  

        -   **Nenhum:** as atualização não são instaladas automaticamente.  

        -   **Recomendado:** todas as atualizações recomendadas são instaladas  

        -   **Importante:** somente atualizações classificadas como importantes são instaladas.  

    -   **Exigir uma senha para desbloquear dispositivos móveis:** quando essa configuração é definida como **Sim**, os usuários finais devem digitar uma senha antes que possam acessar seu dispositivo.  

         Para criar uma regra de senha para desbloquear dispositivos móveis, abra o assistente **Criar Política de Conformidade** e adicione uma nova regra. Selecione **Exigir uma senha para desbloquear um dispositivo ocioso** como a condição e defina o valor como **Verdadeiro**.  

    -   **Minutos de inatividade antes que a senha seja exigida:** especifica o tempo ocioso antes que o usuário precise digitar novamente sua senha.  

         Para criar essa regra, abra o assistente **Criar Política de Conformidade** e adicione uma nova regra. **Selecione os Minutos de inatividade antes que a senha seja exigida** como a condição e defina o valor para uma das opções disponíveis: 1 minuto, 5 minutos, 15 minutos, 30 minutos, 1 hora.  

-   **Substituição de regra padrão – Sempre permitir que dispositivos registrados e compatíveis acessem o Exchange no local:**  

     Quando você marca essa opção, os dispositivos registrados no Intune e compatíveis com as políticas de conformidade têm permissão para acessar o Exchange no local. Essa regra substitui a Regra padrão, o que significa que mesmo que você defina a Regra padrão para bloquear o acesso ou colocar na quarentena, dispositivos registrados e compatíveis ainda poderão acessar o Exchange no local.  
     Use essa configuração quando desejar que dispositivos registrados e compatíveis sempre tenham acesso ao email por meio do Exchange no local.  

     Há suporte para isso nas seguintes plataformas: Windows Phone 8 e posterior, iOS 6 e posterior. Android 4.0 e posterior, Samsung KNOX Standard 4.0 e posterior.  

     Para usar essa opção, vá para a página **Geral** do assistente **Configurar Política de Acesso Condicional** para o Exchange no local.  

##  <a name="bkmk_clientStatus"></a> Status online do cliente  
Começando com o technical preview 1601, você pode identificar rapidamente se um cliente está online ou offline no console do Configuration Manager. Com colunas e ícones atualizados nas listas de dispositivos do console, você pode avaliar o status dos clientes em seu ambiente para identificar áreas problemáticas e outras questões que precisam de atenção.  

Um cliente estará online se estiver conectado a uma função de sistema de sites do ponto de gerenciamento do Configuration Manager. Enquanto o ponto de gerenciamento estiver recebendo mensagens de ping do cliente, seu status está online. Se o gerenciamento não receber uma mensagem em 5 minutos, o status do cliente será alterado para offline.  

### <a name="icons-for-client-status"></a>Ícones de status do cliente  

|||  
|-|-|  
|![ícone de status online para clientes](media/online-status-icon.png)|O cliente está online.|  
|![ícone de status offline para clientes](media/offline-status-icon.png)|O cliente está offline.|  
|![ícone de status desconhecido para clientes](media/unknown-status-icon.png)|O status do cliente é desconhecido.|  

### <a name="prerequisites"></a>Pré-requisitos  
 O status do cliente online não tem pré-requisitos. Você pode começar a usá-lo assim que o technical preview 1601 do Configuration Manager estiver instalado.  

### <a name="limitations"></a>Limitações  
 O status online do cliente só está disponível para computadores Windows com o cliente do Configuration Manager instalado. Não há suporte para o status online de cliente para computadores Mac, Linux ou UNIX computador ou dispositivos gerenciados com o Gerenciamento de Dispositivo Móvel local.  

### <a name="to-view-client-online-status"></a>Para exibir status online do cliente  

1.  No console do Configuration Manager, vá até **Ativos e Conformidade > Visão Geral > Dispositivos**.  

2.  Clique com botão direito do mouse no cabeçalho da coluna e, em seguida, clique em um dos campos de status online do cliente para adicioná-lo à exibição do dispositivo. Os campos são  

    -   **Status Online do Dispositivo** indica se o cliente ainda está online ou offline no momento.  

    -   **Última Vez Online** indica quando o status online do cliente foi alterado de offline para online.  

    -   **Última Vez Offline** indica quando o status online do cliente foi alterado de online para offline.  

 Para mostrar alterações recentes no status do cliente, atualize o console.  

##  <a name="bkmk_appmgmt1601"></a> Aprimoramentos no gerenciamento de aplicativos  
 Na Visualização técnica 1601, adicionamos suporte para os seguintes recursos:  

### <a name="manage-volume-purchased-apps-for-ios-devices"></a>Gerenciar aplicativos adquiridos por volume para dispositivos iOS  
 Algumas lojas de aplicativos oferecem a possibilidade de comprar várias licenças para um aplicativo que você deseja executar na empresa. Isso ajuda a reduzir a sobrecarga administrativa de controlar várias cópias de aplicativos adquiridas.  

 Agora, o Configuration Manager ajuda a gerenciar aplicativos comprados por meio de tal programa, importando as informações de licença da loja de aplicativos e acompanhando quantas licenças você usou.  

 Para obter detalhes, consulte [Gerenciar aplicativos adquiridos por meio de um programa de compra por volume com o Configuration Manager](https://technet.microsoft.com/library/mt627954.aspx).  

### <a name="ios---app-configuration-for-applicationsbr-hybrid"></a>iOS – Configuração de aplicativo para aplicativos<br />Híbrido  
 Alguns aplicativos iOS dão suporte à pré-configuração de definições como um servidor ou banco de dados com o qual o aplicativo deve se conectar. Agora, o Configuration Manager dá suporte à implantação de políticas de configuração de aplicativo para o dispositivo que permite que o usuário use o aplicativo imediatamente sem a necessidade de conhecer essas informações. Os desenvolvedores devem habilitar essa funcionalidade em seus aplicativos.  

 Um número limitado de aplicativos liberados publicamente dão suporte no momento a definições pré-configuradas; você também pode ter aplicativos de linhas de negócios desenvolvidos internamente que dão suporte a elas.  

#### <a name="prerequisites-for-this-scenario"></a>Pré-requisitos para esse cenário  

-   Você deve ter adicionado uma assinatura do Microsoft Intune ao Configuration Manager.  

-   Você deve ter adicionado um certificado Apple APNs válido à assinatura do Intune.  

-   Você deve ter implantado um aplicativo iOS que dá suporte à configuração de aplicativo.  

#### <a name="try-it-out"></a>Experimente!  
 Quando os pré-requisitos acima forem atendidos, você deverá criar um aplicativo do Configuration Manager que usa um tipo de implantação de iOS. O aplicativo que você usa deve dar suporte à configuração de aplicativo. Consulte a documentação do fornecedor do aplicativo para saber quais itens específicos (pares de nome/valor), você pode configurar.  

 Em seguida, associe a política de configuração do aplicativo com o tipo de implantação de iOS durante a implantação do aplicativo. Implante também a política por meio do nó **Políticas de Configuração do Aplicativo**, destinado a um aplicativo e uma coleção existentes.  

 Tente concluir as seguintes tarefas e depois use as informações de comentários perto da parte superior deste tópico para nos contar como elas funcionaram:  

-   Se você tiver um aplicativo iOS que dá suporte à configuração de aplicativo, consulte a documentação do fornecedor do aplicativo para descobrir os pares de nome e valor que devem ser especificados para configurar o aplicativo.  

-   Inicie o assistente **Criar Política de Configuração de Aplicativo**. Na página **Política de iOS** do assistente, tente adicionar pares de nome e valor encontrados na documentação do fornecedor do aplicativo ou importar um arquivo XML contendo os valores necessários.  

-   No assistente **Implantar Software**, na página **Política de Configuração de Aplicativo**, associe a política de configuração de aplicativo criada com um tipo compatível de implantação de aplicativos.  

##  <a name="bkmk_compliance1601"></a> Aprimoramentos para configurações de conformidade  
 Na Visualização técnica 1601, adicionamos suporte para os seguintes recursos:  

### <a name="microsoft-edge-browser-settings"></a>Configurações do navegador Microsoft Edge  
 Foram adicionadas novas configurações do navegador Microsoft Edge ao item de configuração do **Windows 8.1 e Windows 10** (as configurações só se aplicam a dispositivos do Windows 10).  

 Para ver as novas configurações, escolha **Microsoft Edge** no item de configuração da página **Configurações do Dispositivo** do assistente **Criar Item de Configuração**.  

 Para mais informações, consulte [Como criar itens de configuração para dispositivos Windows 8.1 e Windows 10 gerenciados sem o cliente do System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="compliance-settings-for-windows-10-team-devices"></a>Configurações de conformidade para os dispositivos do Windows 10 Team  
 Use essas novas configurações de conformidade para configurar dispositivos que executam o Windows 10 Team, como os dispositivos Surface Hub.  

 Para ver as novas configurações, escolha **Windows 10 Team** no item de configuração, página **Configurações do Dispositivo** do assistente **Criar Item de Configuração**.  

 Para mais informações, consulte [Como criar itens de configuração para dispositivos Windows 8.1 e Windows 10 gerenciados sem o cliente do System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="android---kiosk-mode-for-samsung-knox-standardbr-hybrid"></a>Android – Modo de quiosque para Samsung KNOX Standard<br />Híbrido  
 O modo de quiosque permite bloquear um dispositivo para permitir que apenas alguns recursos funcionem. Por exemplo, você pode permitir que um dispositivo execute apenas um aplicativo gerenciado que você especificar ou pode desabilitar os botões de volume em um dispositivo. Essas configurações podem ser usadas para um modelo de demonstração de um dispositivo ou um dispositivo que é dedicado a apenas uma função, como um dispositivo de ponto de venda. Essas configurações não estão disponíveis para dispositivos Samsung KNOX Standard no item de configuração **Windows 8.1 e Windows 10** (as configurações só se aplicam a dispositivos Windows 10).  

 Para ver as novas configurações, escolha **Modo de Quiosque – Samsung KNOX** no item de configuração da página **Configurações do Dispositivo** do assistente **Criar Item de Configuração**.  

 Para mais informações, consulte [Como criar itens de configuração para dispositivos Windows 8.1 e Windows 10 gerenciados sem o cliente do System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  
