---
title: "Proteger aplicativos usando políticas de gerenciamento de aplicativo móvel | Microsoft Docs"
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
ms.sourcegitcommit: 946c8f8185fa6a8f0aded8e615b491d8ae454379
ms.openlocfilehash: 8d437af550a5790949085605f26189d88e094d03


---
# <a name="protect-apps-using-mobile-application-management-policies-in-system-center-configuration-manager"></a>Proteger aplicativos usando políticas de gerenciamento de aplicativos móveis no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As políticas de gerenciamento de aplicativos do System Center Configuration Manager permitem modificar a funcionalidade dos aplicativos implantados para ajudar a alinhá-los com as políticas de conformidade e segurança de sua empresa. Por exemplo, você pode restringir as operações de recortar, copiar e colar em um aplicativo restrito, ou configurar um aplicativo para abrir todas as URLs dentro de um navegador gerenciado. As políticas de gerenciamento de aplicativos dão suporte a:  

-   Dispositivos que executam o Android 4 e posterior.  

-   Dispositivos que executam o iOS 7 e posterior.  

Você também pode usar políticas de gerenciamento de aplicativo móvel para proteger aplicativos em dispositivos que não são gerenciados pelo Intune. Usando essa nova funcionalidade, você pode aplicar políticas de gerenciamento de aplicativo móvel para aplicativos que se conectam aos serviços do Office 365. Isso não tem suporte para aplicativos que se conectam ao Exchange ou SharePoint local.  

Para usar essa nova funcionalidade, você precisa usar a Versão Prévia do Portal do Azure. Os seguintes tópicos podem ajudá-lo a começar:  
-   [Introdução às políticas de gerenciamento de aplicativo móvel no Portal do Azure](https://technet.microsoft.com/library/mt627830.aspx)  
-   [Criar e implantar políticas de gerenciamento de aplicativo móvel com o Microsoft Intune](https://technet.microsoft.com/library/mt627829.aspx)  

 Você não implanta uma política de gerenciamento de aplicativos diretamente como você faria com itens de configuração e linhas de base no Configuration Manager. Em vez disso, associe a política ao tipo de implantação do aplicativo que deseja restringir. Quando o tipo de implantação do aplicativo estiver implantado e instalado nos dispositivos, as configurações especificadas entrarão em vigor.  

Para aplicar restrições a um aplicativo, este deve incorporar o SDK (Software Development Kit ) do Aplicativo o Microsoft Intune. Há dois métodos de obter esse tipo de aplicativo:  

-   **Usar um aplicativo gerenciado por política** (Android e iOS): esses aplicativos têm o SDK do aplicativo inserido. Para adicionar este tipo de aplicativo, especifique um link para o aplicativo de uma loja de aplicativos, como a iTunes Store ou o Google Play. Nenhum processamento adicional é necessário para este tipo de aplicativo. Para obter uma lista dos aplicativos gerenciados pela política que estão disponíveis para dispositivos iOS e Android, veja [Aplicativos gerenciados para políticas de gerenciamento de aplicativos móveis do Microsoft Intune](https://technet.microsoft.com/en-us/library/dn708489.aspx).  

-   **Usar um aplicativo "encapsulado"** (Android e iOS): esses aplicativos são empacotados novamente para incluir o SDK do aplicativo usando a **Ferramenta de Encapsulamento de Aplicativos do Microsoft Intune**. Normalmente, essa ferramenta é usada para processar aplicativos da empresa criados internamente. Ele não pode ser usado para processar aplicativos que foram baixados da loja de aplicativos. Consulte os artigos a seguir para obter mais informações:
    - [Preparar aplicativos iOS para gerenciamento de aplicativos móveis com a Ferramenta de Encapsulamento de Aplicativos do Microsoft Intune](https://technet.microsoft.com/en-us/library/dn878028.aspx)

    - [Preparar aplicativos Android para o gerenciamento de aplicativos móveis com a Ferramenta de Encapsulamento de Aplicativos do Microsoft Intune](https://technet.microsoft.com/en-us/library/mt147413.aspx)  

## <a name="create-and-deploy-an-app-with-a-mobile-application-management-policy"></a>Criar e implantar um aplicativo com uma política de gerenciamento de aplicativos móveis  

##  <a name="step-1-obtain-the-link-to-a-policy-managed-app-or-create-a-wrapped-app"></a>Etapa 1: obter o link para um aplicativo gerenciado por política ou criar um aplicativo encapsulado  

-   **Para obter um link para um aplicativo gerenciado por política**: na loja de aplicativos, encontre e anote a URL do aplicativo gerenciado por política que você deseja implantar.  

     Por exemplo, a URL do Microsoft Word para aplicativo do iPad é **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**  

-   **Para criar um aplicativo encapsulado**: use as informações nos tópicos [Preparar aplicativos iOS para gerenciamento de aplicativos móveis com a Ferramenta de Encapsulamento de Aplicativos do Microsoft Intune](https://technet.microsoft.com/en-us/library/dn878028.aspx) e [Preparar aplicativos Android para o gerenciamento de aplicativos móveis com a Ferramenta de Encapsulamento de Aplicativos do Microsoft Intune](https://technet.microsoft.com/en-us/library/mt147413.aspx) para criar um aplicativo encapsulado.  

     A ferramenta cria um aplicativo processado e um arquivo de manifesto associado. Esses arquivos são usados ao criar um aplicativo do Configuration Manager que contém o aplicativo.  

##  <a name="step-2-create-a-configuration-manager-application-that-contains-an-app"></a>Etapa 2: criar um aplicativo do Configuration Manager contendo um aplicativo  
 O procedimento para criar o aplicativo do Configuration Manager é diferente, dependendo se você estiver usando um aplicativo gerenciado por política (link externo) ou um aplicativo que foi criado com a Ferramenta de Encapsulamento de Aplicativos do Microsoft App para iOS (pacote do aplicativo para iOS). Use um dos procedimentos a seguir para criar o aplicativo do Configuration Manager.  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.  

3.  Na guia **Início**, no grupo **Criar**, escolha **Criar Aplicativo** para abrir o Assistente para **Criar Aplicativos**.  

4.  Na página **Geral** , selecione **Detectar automaticamente informações sobre este aplicativo em arquivos de instalação**.  

5.  Na lista suspensa **Tipo**, selecione **Pacote de aplicativo para iOS (arquivo \*.ipa)**.  

6.  Escolha **Procurar** para selecionar o pacote do aplicativo que você deseja importar e escolha **Avançar**.  

7.  Na página **Informações Gerais** , insira o texto descritivo e as informações sobre categoria que você quer que os usuários vejam no portal da empresa.  

8.  Conclua o assistente.  

 O novo aplicativo é exibido no nó **Aplicativos** do espaço de trabalho **Biblioteca de Software** .  

### <a name="create-an-application-that-contains-a-link-to-a-policy-managed-app"></a>Criar um aplicativo que contém um link para um aplicativo gerenciado por política  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.  

3.  Na guia **Início**, no grupo **Criar**, escolha **Criar Aplicativo** para abrir o Assistente para **Criar Aplicativos**.  

4.  Na página **Geral** , selecione **Detectar automaticamente informações sobre este aplicativo em arquivos de instalação**.  

5.  Na lista suspensa **Tipo** , selecione uma das seguintes opções:  

    -   Para iOS: **pacote do aplicativo para iOS da App Store**  

    -   Para Android: **pacote do aplicativo para Android no Google Play**  

6.  Digite a URL para o aplicativo (da etapa 1) e escolha **Avançar**.  

7.  Na página **Informações Gerais** , insira o texto descritivo e as informações sobre categoria que você quer que os usuários vejam no portal da empresa.  

8.  Conclua o assistente.  

 O novo aplicativo é exibido no nó **Aplicativos** do espaço de trabalho **Biblioteca de Software** .  

##  <a name="step-3-create-an-application-management-policy"></a>Etapa 3: criar uma política de gerenciamento de aplicativos  
 Em seguida, crie uma política de gerenciamento de aplicativos que você associará ao aplicativo. É possível criar uma política geral ou de navegador gerenciado.  

1)  No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Políticas de Gerenciamento de Aplicativos**.  

2)  Na guia **Início**, no grupo **Criar**, escolha **Criar Política de Gerenciamento de Aplicativos**.  

3)  Na página **Geral**, insira o nome e a descrição da política e escolha **Avançar**.  

4)  Na página **Tipo de Política**, selecione a plataforma e o tipo de política para esta política e escolha **Avançar**. Os seguintes tipos de política estão disponíveis:  

-   **Geral**: o tipo de política Geral permite modificar a funcionalidade dos aplicativos implantados para ajudar a alinhá-los com as políticas de conformidade e segurança de sua empresa. Por exemplo, é possível restringir as operações de recortar, copiar e colar em um aplicativo restrito.  

-   **Managed Browser**: a política Managed Browser permite que você decida se deseja permitir ou bloquear o navegador gerenciado de abrir uma lista de URLs. O tipo de política do Managed Browser permite modificar a funcionalidade do aplicativo Intune Managed Browser. Este é um navegador da Web que permite gerenciar as ações que podem ser executadas pelos usuários, incluindo os sites que eles podem visitar e como os links para o conteúdo dentro do navegador serão abertos. Saiba mais sobre o  [aplicativo de Navegador Gerenciado do Intune para iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) e [o aplicativo de Navegador Gerenciado do Intune para Android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).

5)  Na página **Política do iOS** ou **Política do Android**, configure os seguintes valores, conforme necessário, e escolha **Avançar**. As opções podem variar dependendo do tipo de dispositivo para o qual você está configurando a política.  

|Valor|Mais informações|  
|-----------|----------------------|  
|**Restringir o conteúdo da web a ser exibido em um navegador gerenciado corporativo**|Permite que todos os links no aplicativo abram no Managed Browser. Você precisa ter implantado o aplicativo em dispositivos para que essa opção funcione.|  
|**Impedir backups do Android** ou **Impedir backups do iTunes e iCloud**|Desabilita o backup de todas as informações do aplicativo.|  
|**Permitir que o aplicativo transfira dados para outros aplicativos**|Especifica os aplicativos para os quais esse aplicativo pode enviar dados. Você pode optar por não permitir a transferência de dados para qualquer aplicativo, permitir somente a transferência para outros aplicativos restritos ou permitir a transferência para qualquer aplicativo.<br /><br /> Para dispositivos iOS, para evitar a transferência de documentos entre os aplicativos gerenciados e não gerenciados, você precisa também configurar e implantar uma política de segurança de dispositivo móvel que desabilite a configuração **Permitir documentos gerenciados em outros aplicativos não gerenciados**.<br /><br /> Se você optar por permitir a transferência apenas para outros aplicativos restritos, os visualizadores de imagens e PDF do Intune (se implantados) serão usados para abrir o conteúdo dos respectivos tipos.|  
|**Permitir que o aplicativo receba dados de outros aplicativos**|Especifica os aplicativos dos quais este aplicativo pode receber dados. Você pode optar por não permitir a transferência de dados de qualquer aplicativo, permitir somente a transferência de outros aplicativos restritos ou permitir a transferência de qualquer aplicativo.|  
|**Impedir "Salvar como"**|Desabilita o uso da opção **Salvar Como** em qualquer aplicativo que use essa política.|  
|**Restringir recortar, copiar e colar com outros aplicativos**|Especifica como as operações recortar, copiar e colar podem ser usadas com o aplicativo. Escolha:<br /><br /> **Bloqueado** – Não permite as operações recortar, copiar e colar entre este aplicativo e outros aplicativos.<br /><br /> **Aplicativos Gerenciados por Política** – Permite operações de recortar, copiar e colar somente entre este aplicativo e outros aplicativos restritos.<br /><br /> **Aplicativos Gerenciados por Política com Colar Em** – Permite que os dados recortados ou copiados desse aplicativo sejam colados apenas em outros aplicativos restritos. Permite que os dados recortados ou copiados de qualquer aplicativo sejam colados nesse aplicativo.<br /><br /> **Qualquer Aplicativo** – Sem restrições para operações de recortar, copiar e colar deste ou para este aplicativo.|  
|**Solicitar PIN simples para acesso**|Requer que o usuário insira um PIN que ele especifica para usar o aplicativo. É solicitado que o usuário configure isso na primeira vez em que executar o aplicativo.|  
|**Número de tentativas antes da redefinição do PIN**|Especifica o número de tentativas de entrada do PIN que podem ser feitas antes que o usuário tenha de redefinir o PIN.|  
|**Exigir credenciais corporativas para acesso**|Requer que o usuário insira suas informações de entrada corporativas antes de acessar o aplicativo.|  
|**Exigir conformidade do dispositivo com a política corporativa para acesso**|Permite que o aplicativo seja usado somente quando o dispositivo não está com jailbreak ou com raiz.|  
|**Verificar novamente os requisitos de acesso após (minutos)**|Especifica o período antes que os requisitos de acesso para o aplicativo sejam verificados novamente após o aplicativo ser iniciado (no campo **Tempo Limite**).<br /><br /> No campo **Período de carência offline**, se o dispositivo estiver offline, especificará o período de tempo antes que os requisitos de acesso do aplicativo sejam verificados novamente.|  
|**Criptografar dados do aplicativo**|Especifica que todos os dados associados ao aplicativo são criptografados, inclusive dados armazenados externamente, como dados armazenados em cartões SD.<br /><br /> **Criptografia para iOS**<br /><br /> Para aplicativos associados a uma política de gerenciamento de aplicativo móvel do Configuration Manager, os dados são criptografados em repouso com a criptografia no nível do dispositivo fornecida pelo sistema operacional. Isso é habilitado pela política de PIN do dispositivo que deve ser definida pelo administrador de TI. Quando um PIN é solicitado, os dados são criptografados segundo as configurações na política de gerenciamento de aplicativo móvel. Conforme indicado na documentação da Apple, [os módulos usados pelo iOS 7 têm a certificação FIPS 140-2](http://support.apple.com/en-us/HT202739).<br /><br /> **Criptografia para Android**<br /><br /> Para aplicativos associados a uma política de gerenciamento de aplicativos móveis do Configuration Manager, a criptografia é fornecida pela Microsoft. Os dados são criptografados de forma síncrona durante operações de E/S de arquivos, de acordo com a configuração na política de gerenciamento de aplicativos móveis. Aplicativos gerenciados no Android usam a criptografia AES-128 no modo CBC utilizando as bibliotecas de criptografia da plataforma. O método de criptografia não tem certificação FIPS 140-2. O conteúdo no armazenamento do dispositivo sempre é criptografado.|  
    |**Bloquear captura de tela** (somente para dispositivos Android)|Especifica que as funcionalidades de captura de tela do dispositivo sejam bloqueadas durante o uso do aplicativo.|  

6)  Na página **Managed Browser**, selecione se o navegador gerenciado tem permissão para abrir somente URLs na lista ou para impedir que o navegador gerenciado abra as URLs na lista e escolha **Avançar**.  
Para mais informações, consulte [Gerenciar o acesso à Internet usando políticas do Managed Browser](../../apps/deploy-use/manage-internet-access-using-managed-browser-policies.md).  

7)  Conclua o assistente.  

 A nova política é exibida no nó **Políticas de Gerenciamento de Aplicativos** no espaço de trabalho **Biblioteca de Software** .  

##  <a name="step-4-associate-the-application-management-policy-with-a-deployment-type"></a>Etapa 4: associar a política de gerenciamento de aplicativos a um tipo de implantação  

 Quando um tipo de implantação é criado para um aplicativo que requer uma política de gerenciamento de aplicativos, o Configuration Manager reconhece isso e solicita que você associe uma política de gerenciamento de aplicativo. Para o Managed Browser, você precisa associar uma política Geral e uma política do Managed Browser. Para mais informações, consulte [Criar aplicativos](../../apps/deploy-use/create-applications.md).  

> [!IMPORTANT]  
>  Se o aplicativo já estiver implantado, a implantação para o novo tipo de implantação falhará até que essa associação seja feita. É possível fazer a associação nas **Propriedades** do aplicativo, na guia **Gerenciamento de Aplicativos** .  

> [!IMPORTANT]  
>  Para dispositivos que executam sistemas operacionais anteriores ao iOS 7.1, as políticas associadas não são removidas quando o aplicativo é desinstalado.  
>   
>  Se o dispositivo tiver seu registro no Configuration Manager cancelado, as políticas não serão removidas dos aplicativos. Os aplicativos que tinham políticas aplicadas mantêm as configurações de política, mesmo depois que o aplicativo é desinstalado e reinstalado.  

##  <a name="step-5-monitor-the-app-deployment"></a>Etapa 5: Monitorar a implantação do aplicativo  
 Depois de criar e implantar um aplicativo associado a uma política de gerenciamento de aplicativo móvel, é possível monitorar o aplicativo e resolver conflitos de política.  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Visão Geral** > **Implantações**.  

3.  Selecione a implantação que você criou. Em seguida, na guia **Início**, escolha **Propriedades**.  

4.  No painel de detalhes da implantação, em **Objetos Relacionados**, escolha **Políticas de Gerenciamento de Aplicativos**.  

 Para obter mais informações sobre como monitorar aplicativos, consulte [Monitorar aplicativos](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

##  <a name="learn-how-policy-conflicts-are-resolved"></a>Saiba como os conflitos de política são resolvidos  
 Quando há um conflito de política de gerenciamento de aplicativo móvel na primeira implantação para o usuário ou dispositivo, o valor da configuração específica em conflito é removido da política implantada para o aplicativo. Em seguida, o aplicativo usa um valor de conflito interno.  

 Quando há um conflito de política de gerenciamento de aplicativo móvel em implantações posteriores para o aplicativo ou usuário, o valor da configuração específica em conflito não é atualizado na política de gerenciamento de aplicativo móvel implantada para o aplicativo e ele usa o valor existente para essa configuração.  

 Em casos em que o dispositivo ou usuário receber duas políticas conflitantes, o comportamento a seguir se aplicará:  

-   Se uma política já tiver sido implantada para o dispositivo, as configurações de política existentes não serão substituídas.  

-   Se nenhuma política tiver sido implantada ainda no dispositivo e duas configurações conflitantes forem implantadas, a configuração padrão integrada no dispositivo será usada.  

##  <a name="see-a-list-of-available-policy-managed-apps"></a>Veja uma lista dos aplicativos gerenciados por política disponíveis  
 Para obter uma lista dos aplicativos gerenciados pela política que estão disponíveis para dispositivos iOS e Android, consulte [Parceiros de aplicativo do Microsoft Intune](https://www.microsoft.com/en-us/cloud-platform/microsoft-intune-partners).  



<!--HONumber=Dec16_HO3-->


