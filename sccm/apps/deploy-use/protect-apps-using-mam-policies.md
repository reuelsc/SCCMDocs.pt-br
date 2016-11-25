---
title: "Proteger aplicativos usando políticas de gerenciamento de aplicativos móveis | System Center Configuration Manager"
description: "Modifique a funcionalidade dos aplicativos que você implanta para que eles cumpram as políticas de conformidade e segurança da empresa."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 309b7936-a5ca-45c5-8bef-10424eb2e091
caps.latest.revision: 13
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: dfbf6b2001e3259abb7246ab463682b0ead4f4e8


---
# <a name="protect-apps-using-mobile-application-management-policies-in-system-center-configuration-manager"></a>Proteger aplicativos usando políticas de gerenciamento de aplicativos móveis no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As políticas de gerenciamento de aplicativos do System Center Configuration Manager permitem modificar a funcionalidade dos aplicativos implantados para ajudar a alinhá-los com as políticas de conformidade e segurança de sua empresa. Por exemplo, você pode restringir as operações de recortar, copiar e colar em um aplicativo restrito, ou configurar um aplicativo para abrir todos os links da Web dentro de um navegador gerenciado. As políticas de gerenciamento de aplicativos dão suporte a:  

-   Dispositivos que executam o Android 4 e posterior.  

-   Dispositivos que executam o iOS 7 e posterior.  

Além dos dispositivos gerenciados, políticas de gerenciamento de aplicativo móvel podem ser usadas para proteger aplicativos em dispositivos que não são gerenciados pelo Intune. Usando essa nova funcionalidade, você pode aplicar políticas de gerenciamento de aplicativo móvel para aplicativos conectados aos serviços do Office 365. Isso não tem suporte em aplicativos que se conectam ao Exchange ou SharePoint local.  
Para usar essa nova funcionalidade, você deve usar o portal de visualização do Azure. Os seguintes tópicos podem ajudá-lo a começar:  
-   [Introdução às políticas de gerenciamento de aplicativo móvel no Portal do Azure](https://technet.microsoft.com/library/mt627830.aspx)  
-   [Criar e implantar políticas de gerenciamento de aplicativo móvel com o Microsoft Intune](https://technet.microsoft.com/library/mt627829.aspx)  

Ao contrário dos itens de configuração e das linhas de base no Configuration Manager, uma política de gerenciamento de aplicativos não é implantada diretamente. Em vez disso, associe a política ao tipo de implantação do aplicativo que deseja restringir. Quando o tipo de implantação do aplicativo estiver implantado e instalado nos dispositivos, as configurações especificadas entrarão em vigor.  

Para aplicar restrições a um aplicativo, este deve incorporar o SDK (Software Development Kit ) do Aplicativo o Microsoft Intune. Há dois métodos de obter esse tipo de aplicativo:  

-   **Usar um aplicativo gerenciado por política** (Android e iOS): tem o SDK do aplicativo inserido. Para adicionar este tipo de aplicativo, especifique um link para o aplicativo de uma loja de aplicativos, como a iTunes Store ou o Google Play. Nenhum processamento adicional é necessário para este tipo de aplicativo. Para obter uma lista dos aplicativos gerenciados pela política que estão disponíveis para dispositivos iOS e Android, veja [Aplicativos gerenciados para políticas de gerenciamento de aplicativos móveis do Microsoft Intune](https://technet.microsoft.com/en-us/library/dn708489.aspx).  

-   **Usar um aplicativo "encapsulado"** – (Android e iOS): aplicativos que são empacotados novamente para incluir o SDK do aplicativo usando a **Ferramenta de disposição de aplicativos do Microsoft Intune**. Normalmente, essa ferramenta é usada para processar aplicativos da empresa criados internamente. Ele não pode ser usado para processar aplicativos que foram baixados da loja de aplicativos. Veja [Preparar aplicativos do iOS para o gerenciamento de aplicativos móveis com a Ferramenta de Encapsulamento de Aplicativos do Microsoft Intune](https://technet.microsoft.com/en-us/library/dn878028.aspx) e [Preparar aplicativos do Android para o gerenciamento de aplicativos móveis com a Ferramenta de Encapsulamento de Aplicativos do Microsoft Intune](https://technet.microsoft.com/en-us/library/mt147413.aspx).  

## <a name="create-and-deploy-an-app-with-a-mobile-application-management-policy"></a>Criar e implantar um aplicativo com uma política de gerenciamento de aplicativos móveis  
  
##  <a name="step-1-obtain-the-link-to-a-policy-managed-app-or-create-a-wrapped-app"></a>Etapa 1: obter o link para um aplicativo gerenciado por política ou criar um aplicativo encapsulado  

-   **Para obter um link para um aplicativo gerenciado por política** - Na loja de aplicativos, encontre e anote a URL do aplicativo gerenciado que você deseja implantar.  

     Por exemplo, a URL do Microsoft Word para aplicativo do iPad é **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**  

-   **Para criar um aplicativo encapsulado** – use as informações nos tópicos [Preparar aplicativos do iOS para o gerenciamento de aplicativos móveis com a Ferramenta de Encapsulamento de Aplicativos do Microsoft Intune](https://technet.microsoft.com/en-us/library/dn878028.aspx) e [Preparar aplicativos do Android para o gerenciamento de aplicativos móveis com a Ferramenta de Encapsulamento de Aplicativos do Microsoft Intune](https://technet.microsoft.com/en-us/library/mt147413.aspx) para criar um aplicativo encapsulado.  

     A ferramenta cria um aplicativo processado e um arquivo de manifesto associado. Você usará esses arquivos ao criar um aplicativo do Configuration Manager que contém o aplicativo.  

##  <a name="step-2-create-a-configuration-manager-application-that-contains-an-app"></a>Etapa 2: criar um aplicativo do Configuration Manager contendo um aplicativo  
 O procedimento para criar o aplicativo do Configuration Manager é diferente, dependendo se você estiver usando um aplicativo gerenciado por política (link externo) ou um aplicativo que foi criado com a Ferramenta de Encapsulamento de Aplicativos do Microsoft App para iOS (pacote do aplicativo para iOS). Use um dos procedimentos a seguir para criar o aplicativo do Configuration Manager.  

1.  No console do Configuration Manager, clique em **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Aplicativo** para abrir o Assistente para Criar Aplicativos.  

4.  Na página **Geral** , selecione **Detectar automaticamente informações sobre este aplicativo em arquivos de instalação**.  

5.  Na lista suspensa **Tipo**, selecione **Pacote de aplicativo para iOS (arquivo \*.ipa)**.  

6.  Clique em **Procurar** para selecionar o pacote de aplicativo que você quer importar e clique em **Próximo**.  

7.  Na página **Informações Gerais** , insira o texto descritivo e as informações sobre categoria que você quer que os usuários vejam no portal da empresa.  

8.  Conclua o assistente.  

 O novo aplicativo é exibido no nó **Aplicativos** do espaço de trabalho **Biblioteca de Software** .  
  
### <a name="create-an-application-containing-a-link-to-a-policy-managed-app"></a>Criar um aplicativo que contém um link para um aplicativo gerenciado pela política  
  
1.  No console do Configuration Manager, clique em **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.  
  
3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Aplicativo** para abrir o Assistente para Criar Aplicativos.  

4.  Na página **Geral** , selecione **Detectar automaticamente informações sobre este aplicativo em arquivos de instalação**.  

5.  Na lista suspensa **Tipo** , selecione uma das seguintes opções:  

    -   Para iOS: **pacote do aplicativo para iOS da App Store**  

    -   Para Android: **pacote do aplicativo para Android no Google Play**  

6.  Digite a URL para o aplicativo (da etapa 1) e clique em **Próximo**.  

7.  Na página **Informações Gerais** , insira o texto descritivo e as informações sobre categoria que você quer que os usuários vejam no portal da empresa.  

8.  Conclua o assistente.  

 O novo aplicativo é exibido no nó **Aplicativos** do espaço de trabalho **Biblioteca de Software** .  

##  <a name="step-3-create-an-application-management-policy"></a>Etapa 3: criar uma política de gerenciamento de aplicativos  
 Em seguida, crie uma política de gerenciamento de aplicativos que você associará ao aplicativo. É possível criar uma política geral ou de navegador gerenciado.  
  
1.  No console do Configuration Manager, clique em **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Políticas de Gerenciamento de Aplicativos**.  
3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Política de Gerenciamento de Aplicativos**.  

4.  Na página **Geral** , digite o nome e a descrição da política e clique em **Próximo**.  

5.  Na página **Tipo de Política** , selecione a plataforma e o tipo de política para esta política e clique em **Próximo**. Os seguintes tipos de política estão disponíveis:  

    -   **Geral**: o tipo de política Geral permite modificar a funcionalidade dos aplicativos implantados para ajudar a alinhá-los com as políticas de conformidade e segurança de sua empresa. Por exemplo, é possível restringir as operações de recortar, copiar e colar em um aplicativo restrito.  

    -   **Navegador Gerenciado**: configure para permitir ou bloquear o navegador gerenciado de abrir uma lista de URLs. O tipo de política do Managed Browser permite modificar a funcionalidade do aplicativo Intune Managed Browser. Este é um navegador da Web que permite gerenciar as ações que podem ser executadas pelos usuários, incluindo os sites que eles podem visitar e como os links para o conteúdo dentro do navegador serão abertos. Saiba mais sobre o  [aplicativo de Navegador Gerenciado do Intune para iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) e [o aplicativo de Navegador Gerenciado do Intune para Android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).  

6.  Na página **Política do iOS** ou **Política do Android** , configure os seguintes valores, conforme necessário, e clique em **Próximo**. As opções podem variar dependendo do tipo de dispositivo para o qual você está configurando a política.  

|Valor|Mais informações|  
|-----------|----------------------|  
|**Restringir o conteúdo da web a ser exibido em um navegador gerenciado corporativo**|Quando essa configuração for habilitada, todos os links no aplicativo serão abertos no navegador gerenciado. Você precisa ter implantado o aplicativo em dispositivos para que essa opção funcione.|  
|**Impedir backups do Android** ou **Impedir backups do iTunes e iCloud**|Desabilita o backup de todas as informações do aplicativo.|  
|**Permitir que o aplicativo transfira dados para outros aplicativos**|Especifica os aplicativos para os quais esse aplicativo pode enviar dados. Você pode optar por não permitir a transferência de dados para qualquer aplicativo, permitir somente a transferência para outros aplicativos restritos ou para permitir a transferência para qualquer aplicativo.<br /><br /> Para dispositivos iOS, para evitar a transferência de documentos entre os aplicativos gerenciados e não gerenciados, você precisa também configurar e implantar uma política de segurança de dispositivo móvel que desabilite a configuração **Permitir documentos gerenciados em outros aplicativos não gerenciados**.<br /><br /> Se você optar por permitir a transferência apenas para outros aplicativos restritos, os visualizadores de imagens e PDF do Intune (se implantados) serão usados para abrir o conteúdo dos respectivos tipos.|  
|**Permitir que o aplicativo receba dados de outros aplicativos**|Especifica os aplicativos dos quais este aplicativo pode receber dados. Você pode optar por não permitir a transferência de dados de qualquer aplicativo, permitir somente a transferência de outros aplicativos restritos ou permitir a transferência de qualquer aplicativo.|  
|**Impedir "Salvar como"**|Desabilita o uso da opção **Salvar como** em qualquer aplicativo que use essa política.|  
|**Restringir recortar, copiar e colar com outros aplicativos**|Especifica como as operações recortar, copiar e colar podem ser usadas com o aplicativo. Escolha:<br /><br /> **Bloqueado** – Não permite as operações recortar, copiar e colar entre este aplicativo e outros aplicativos.<br /><br /> **Aplicativos gerenciados por política** – Permite operações de recortar, copiar e colar somente entre este aplicativo e outros aplicativos restritos.<br /><br /> **Aplicativos gerenciados por política com Colar em** – Permite a transferência de dados copiados ou recortados deste aplicativo somente para outros aplicativos restritos. Permitir a transferência de dados recortados ou copiados de qualquer aplicativo para este aplicativo.<br /><br /> **Qualquer aplicativo** – Sem restrições para operações de recortar, copiar e colar deste ou para este aplicativo.|  
|**Solicitar PIN simples para acesso**|Requer que o usuário insira um número PIN que ele especificar para usar o aplicativo. O usuário será solicitado a configurar isso na primeira vez em que executar o aplicativo.|  
|**Número de tentativas antes da redefinição do PIN**|Especifique o número de tentativas de entrada do PIN que podem ser feitas antes que o usuário precise redefinir o PIN.|  
|**Exigir credenciais corporativas para acesso**|Requer que o usuário insira suas informações de logon corporativo antes de acessar o aplicativo.|  
|**Exigir conformidade do dispositivo com a política corporativa para acesso**|Permite que o aplicativo seja usado somente quando o dispositivo não está desbloqueado ou modificado.|  
|**Verificar novamente os requisitos de acesso após (minutos)**|No campo **Tempo Limite** , especifique o período de tempo antes que os requisitos de acesso para o aplicativo sejam verificados novamente após o aplicativo ser iniciado.<br /><br /> No campo **Período de carência offline** , se o dispositivo estiver offline, especifique o período de tempo antes que os requisitos de acesso do aplicativo sejam verificados novamente.|  
|**Criptografar dados do aplicativo**|Especifica que todos os dados associados ao aplicativo sejam criptografados, inclusive dados armazenados externamente, como em cartões SD.<br /><br /> **Criptografia para iOS**<br /><br /> Para aplicativos associados a uma política de gerenciamento de aplicativos móveis do Configuration Manager, os dados são criptografados em repouso com a criptografia no nível do dispositivo fornecida pelo sistema operacional. Isso é habilitado pela política de PIN do dispositivo que deve ser definida com o administrador de TI. Quando um PIN for solicitado, os dados serão criptografados segundo as configurações na política de gerenciamento de aplicativos móveis. Conforme indicado na documentação da Apple, [os módulos usados pelo iOS 7 têm a certificação FIPS 140-2](http://support.apple.com/en-us/HT202739).<br /><br /> **Criptografia para Android**<br /><br /> Para aplicativos associados a uma política de gerenciamento de aplicativos móveis do Configuration Manager, a criptografia é fornecida pela Microsoft. Os dados são criptografados de forma síncrona durante operações de E/S de arquivos, de acordo com a configuração na política de gerenciamento de aplicativos móveis. Aplicativos gerenciados no Android usam a criptografia AES-128 no modo CBC utilizando as bibliotecas de criptografia da plataforma. O método de criptografia não tem certificação FIPS 140-2. O conteúdo no armazenamento do dispositivo sempre será criptografado.|  
    |**Bloquear captura de tela** (somente para dispositivos Android)|Especifica que as funcionalidades de captura de tela do dispositivo sejam bloqueadas durante o uso do aplicativo.|  

7.  Na página **Managed Browser** , selecione se o navegador gerenciado tem permissão para abrir somente URLs na lista ou selecione para impedir que o navegador gerenciado abra as URLs na lista, gerencie as URLs na lista e clique em **Próximo**.  

    > [!WARNING]  
    >  Para mais informações, consulte [Gerenciar o acesso à Internet usando políticas do Managed Browser](../../apps/deploy-use/manage-internet-access-using-managed-browser-policies.md).  
  
8.  Conclua o assistente.  

 A nova política é exibida no nó **Políticas de Gerenciamento de Aplicativos** no espaço de trabalho **Biblioteca de Software** .  

##  <a name="step-4-associate-the-application-management-policy-with-a-deployment-type"></a>Etapa 4: associar a política de gerenciamento de aplicativos a um tipo de implantação  
 
 Quando um tipo de implantação é criado para um aplicativo que exige uma política de gerenciamento de aplicativos, o Configuration Manager reconhecerá que uma política de gerenciamento de aplicativos deve ser vinculada a este tipo de implantação quando o aplicativo associado é implantado e solicitará que você associe uma política de gerenciamento de aplicativos. Para o Managed Browser, você precisará associar uma política Geral e uma política do Managed Browser. Para mais informações, consulte [Criar aplicativos](../../apps/deploy-use/create-applications.md).  
  
> [!IMPORTANT]  
>  Se o aplicativo já estiver implantado, a implantação para o novo tipo de implantação falhará até que essa associação seja feita. É possível fazer a associação nas **Propriedades** do aplicativo, na guia **Gerenciamento de Aplicativos** .  

> [!IMPORTANT]  
>  Para dispositivos que executam sistemas operacionais anteriores ao iOS 7.1, as políticas associadas não serão removidas quando o aplicativo for desinstalado.  
>   
>  Se o dispositivo tiver seu registro no Configuration Manager cancelado, as políticas não serão removidas dos aplicativos. Os aplicativos que tinham políticas aplicadas manterão as configurações de política, mesmo depois que o aplicativo é desinstalado e reinstalado.  

##  <a name="step-5-monitor-the-app-deployment"></a>Etapa 5: Monitorar a implantação do aplicativo  
 Depois de criar e implantar um aplicativo associado a uma política de gerenciamento de aplicativos móveis, é possível monitorar o aplicativo e resolver conflitos de política.  
  
1.  No console do Configuration Manager, clique em **Biblioteca de Software** > **Visão Geral** > **Implantações**.  
  
3.  Selecione a implantação e na guia **Início** , clique em **Propriedades**.  

4.  No painel de detalhes da implantação, clique em **Políticas de Gerenciamento de Aplicativos** em **Objetos Relacionados**.  

 Para obter mais informações sobre como monitorar aplicativos, consulte [Monitorar aplicativos](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

##  <a name="how-policy-conflicts-are-resolved"></a>Como os conflitos de política são resolvidos  
 Quando houver um conflito de política de gerenciamento de aplicativo móvel na primeira implantação para o usuário ou dispositivo, o valor da configuração específica em conflito será removido da política implantada para o aplicativo e ele usará um valor de conflito interno.  

 Quando houver um conflito de política de gerenciamento de aplicativo móvel em implantações posteriores ao aplicativo ou usuário, o valor da configuração específica em conflito não será atualizado na política de gerenciamento de aplicativos móveis implantada para o aplicativo e ele usará o valor existente para essa configuração.  

 Em casos em que o dispositivo ou usuário receber duas políticas conflitantes, o comportamento a seguir se aplicará:  

-   Se já tiver sido implantada uma política para o dispositivo, as configurações de política existentes não serão substituídas.  

-   Se nenhuma política tiver sido implantada no dispositivo e duas configurações conflitantes forem implantadas, a configuração padrão integrada no dispositivo será usada.  

##  <a name="available-policy-managed-apps"></a>Aplicativos gerenciados por política disponíveis  
 Para obter uma lista dos aplicativos gerenciados pela política que estão disponíveis para dispositivos iOS e Android, consulte [Parceiros de aplicativo do Microsoft Intune](https://www.microsoft.com/en-us/cloud-platform/microsoft-intune-partners).  



<!--HONumber=Nov16_HO1-->


