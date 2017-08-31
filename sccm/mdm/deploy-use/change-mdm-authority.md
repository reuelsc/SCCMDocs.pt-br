---
title: Alterar sua autoridade de MDM | Microsoft Docs
description: "Saiba como alterar a autoridade de MDM do Configuration Manager (híbrido) para o Intune autônomo ou vice-versa."
keywords: 
author: dougeby
manager: angrobe
ms.date: 06/02/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.openlocfilehash: 55f25239dc80641b2f5f7bf1c9d753b146269886
ms.sourcegitcommit: 974fbc4408028c8be28911e5cd646efcf47c7f15
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2017
---
# <a name="change-your-mdm-authority"></a>Alterar sua autoridade de MDM
A partir do Configuration Manager versão 1610, você pode alterar sua autoridade MDM sem precisar entrar em contato com o Suporte da Microsoft e sem a necessidade de cancelar o registro e registrar novamente os dispositivos gerenciados existentes.

## <a name="change-the-mdm-authority-to-intune-standalone"></a>Alterar a autoridade de MDM para o Intune autônomo
Use esta seção para alterar um locatário existente do Microsoft Intune configurado no console do Configuration Manager (híbrido) ao Intune autônomo, sem a necessidade de cancelar o registro e registrar novamente os dispositivos gerenciados existentes.

### <a name="key-considerations"></a>Principais considerações
Depois de alterar para a nova autoridade de MDM, provavelmente haverá um tempo de transição (até oito horas) antes de o dispositivo fazer o check-in e sincronizar com o serviço. Você deve definir as configurações na nova autoridade de MDM (Intune autônomo) para garantir que os dispositivos registrados continuarão a ser gerenciados e protegidos após a alteração. Observe as seguintes considerações:
- Os dispositivos devem se conectar com o serviço após a alteração para que as configurações da nova autoridade de MDM (Intune autônomo) substitua as configurações no dispositivo.
- Depois de alterar a autoridade de MDM, algumas das configurações básicas (como perfis) da autoridade de MDM anterior (híbrido) permanecem no dispositivo por até sete dias. É recomendável que você configure aplicativos e parâmetros (políticas, perfis, aplicativos etc.) na nova autoridade de MDM assim que possível e implante as configurações para os grupos de usuários que contêm usuários que têm dispositivos registrados. Quando um dispositivo se conecta ao serviço após a alteração na autoridade de MDM, ele recebe novas configurações da nova autoridade de MDM. As políticas de destino recentes substituirão as políticas existentes no dispositivo.
- Após você alterar para a nova autoridade de MDM, os dados de conformidade no console de administração do Microsoft Intune poderá levar até uma semana para relatar com precisão. No entanto, os estados de conformidade no Azure Active Directory e no dispositivo serão precisos, então o dispositivo ainda estará protegido.
- Os dispositivos que não têm usuários associados (normalmente quando você tem o Programa de registro de dispositivos iOS ou cenários de registro em massa) não são migrados para a nova autoridade de MDM. Para esses dispositivos, você precisa chamar o suporte para obter assistência para movê-los para a nova autoridade de MDM.

### <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>Preparar para alterar a autoridade de MDM para o Intune autônomo
Examine as informações a seguir para se preparar para a alteração para a autoridade de MDM:
- Você deve ter o Configuration Manager versão 1610 ou superior para que a opção que altera a autoridade de MDM esteja disponível.
- Pode levar até oito horas para um dispositivo se conectar ao serviço depois que você alterar para a nova autoridade de MDM.
- Verifique se todos os usuários que estão sendo gerenciados pelo híbrido têm uma licença do Intune/EMS atribuída a eles antes da alteração na autoridade de MDM. Ter essa licença garante que o usuário e seus dispositivos serão gerenciados pelo Intune autônomo após a alteração na autoridade de MDM. Para saber mais, veja [Atribuir licenças do Intune a suas contas de usuário](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).
- Verifique se a conta de usuário administrador tem uma licença do Intune/EMS atribuída e confirme que a conta de usuário do administrador pode entrar no Intune antes da alteração para a autoridade de MDM. A autoridade de MDM deve exibir **Definir para o Configuration Manager** (locatário híbrido) no console de administração do Microsoft Intune antes da alteração na autoridade de MDM.
- No console do Configuration Manager, remova todas as funções do Gerenciador de registro de dispositivos. Vá para **Administração** > **Serviços de Nuvem** > **Assinaturas do Microsoft Intune**, selecione a assinatura do Microsoft Intune, clique em **Propriedades**, clique na guia **Gerenciador de Registro de Dispositivos** e remova todas as funções do Gerenciador de registro de dispositivos.
- No console doConfiguration Manager, remova as categorias de dispositivo existentes. Vá para **Ativos e Conformidade** > **Visão Geral** > **Coleções de Dispositivos**, escolha **Gerenciar Categorias de Dispositivos** e remova as categorias de dispositivos existentes.
- Não deve haver nenhum impacto perceptível para os usuários finais durante a alteração na autoridade de MDM. 
- Se você estiver usando o Configuration Manager (locatário híbrido) para gerenciar dispositivos iOS antes da alteração na autoridade de MDM, deverá garantir que o mesmo certificado Apple Push Notification Service (APNs) que era usado no Configuration Manager seja renovado e usado para configurar o locatário novamente no Intune autônomo.

    > [!IMPORTANT]  
    > Se um certificado APNs diferente for usado para o Intune autônomo, TODOS os dispositivos iOS registrados anteriormente terão o registro cancelado e você precisará passar pelo processo de registrá-los novamente. Antes de fazer a alteração da autoridade de MDM, verifique se você sabe exatamente qual certificado APNs foi usado para gerenciar os dispositivos iOS no Configuration Manager. Localize o mesmo certificado listado no Apple Push Certificates Portal (https://identity.apple.com), o Portal de Certificados por Push da Apple, e verifique se o usuário cuja ID da Apple usada para criar o certificado APNs original é identificado e está disponível para renovar o mesmo certificado APNs como parte da mudança para a nova autoridade de MDM.  

### <a name="change-the-mdm-authority-to-intune-standalone"></a>Alterar a autoridade de MDM para o Intune autônomo
O processo para alterar a autoridade de MDM para o Intune autônomo inclui as seguintes etapas de alto nível:  
- No console do Configuration Manager, use a opção **Alterar a autoridade de MDM para o Microsoft Intune** para remover a assinatura existente do Microsoft Intune.
- No console de administração do Microsoft Intune, defina a nova autoridade de MDM para **Intune**.
- Configure o certificado de APNs da Apple usando o mesmo certificado de APNs que você renovou.
- No console de administração do Microsoft Intune, configure e implante novas configurações e aplicativos da nova autoridade de MDM (Intune).
- Da próxima vez que o dispositivo se conectar ao serviço, ele sincronizará e receberá as novas configurações da nova autoridade de MDM.

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>Para alterar a autoridade de MDM para o Intune autônomo
1.  No console do Configuration Manager, vá para **Administração** &gt; **Visão Geral** &gt; **Serviços de Nuvem** &gt; **Assinatura do Microsoft Intune** e exclua sua assinatura do Intune.
2.  Selecione **Alterar a autoridade de MDM para o Microsoft Intune** e, em seguida, clique em **Avançar**.

    ![Baixar a solicitação de certificado APNs](/sccm/mdm/deploy-use/media/mdm-change-delete-subscription.png)
3.  Entre no locatário do Intune que você usou originalmente quando definiu a autoridade de MDM no Configuration Manager.
4.  Clique em **Próximo** e conclua o assistente.
5.  A autoridade de MDM agora está redefinida. A assinatura do Intune não deve ser exibida no nó de assinaturas do Microsoft Intune do console do Configuration Manager.
6.  Faça logon para o [Console de administração do Microsoft Intune](http://manage.microsoft.com) usando o mesmo locatário do Intune utilizado antes.
7.  Confirme se a autoridade de MDM foi redefinida e, em seguida, defina a autoridade de MDM como **Microsoft Intune**. Depois de alterar a autoridade de MDM, você a verá refletida no console. Para saber mais, veja [Como definir a autoridade de MDM](https://docs.microsoft.com/en-us/intune/deploy-use/prerequisites-for-enrollment#step-2-set-mdm-authority).
<!-- [Azure portal](https://docs.microsoft.com/en-us/intune-azure/enroll-devices/set-mdm-authority) -->


### <a name="configure-the-apns-certificate"></a>Configurar o certificado APNs
Quando você tiver dispositivos iOS, deverá configurar o certificado APNs no Intune.

#### <a name="to-configure-the-apns-certificate"></a>Para configurar o certificado APNs
1.  Baixar a solicitação de certificado APNs.
    <!--The process is different depending on how you connect to Intune:
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment** &gt; **Apple MDM Push Certificate**, and then select **Download your CSR** to download and save the .csr file locally.   
    <br/>
    **Microsoft Intune administration console**   -->
    No [Console de administração do Microsoft Intune](http://manage.microsoft.com), acesse **Administração** &gt; **Gerenciamento de dispositivo móvel** &gt; **iOS e Mac OS X** &gt; **Carregar um certificado APNs** e escolha **Baixar a solicitação de certificado APNs**. Salve o arquivo (.csr) da solicitação de assinatura do certificado localmente.
    > [!IMPORTANT]    
    > Baixe uma solicitação de assinatura de novo certificado. Não use um arquivo existente ou ocorrerá erro.

    ![Baixar a solicitação de certificado APNs](/sccm/mdm/deploy-use/media/mdm-change-download-apns-certificate.png)

2.  Vá para o [Portal de Certificados de Push da Apple](http://go.microsoft.com/fwlink/?LinkId=269844) e entre com a **mesma** ID da Apple que foi usada anteriormente para criar e renovar o certificado APNs que você usou no Configuration Manager (híbrido).

    ![Página de conexão do Portal de Certificados de Push da Apple](/sccm/mdm/deploy-use/media/mdm-change-apns-portal.png)

3.  Selecione o certificado APNs que você usou no Configuration Manager (híbrido) e, em seguida, clique em **Renovar**.   

    ![Caixa de diálogo Renovar APNs](/sccm/mdm/deploy-use/media/mdm-change-renew-apns.png)

4.  Selecione o arquivo de solicitação de assinatura de certificado APNs (.csr) que você baixou e, em seguida, clique em **Carregar**.

    ![Página de conexão do Portal de Certificados de Push da Apple](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-upload.png)  
5.  Selecione o mesmo APNs e, em seguida, clique em **Baixar**. Baixe o certificado APNs (.pem) e salve o arquivo localmente.  

    ![Página de conexão do Portal de Certificados de Push da Apple](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-download.png)

6.  Carregue o certificado APNs renovado para o locatário do Intune usando a mesma ID da Apple que antes.
<!--The process is different depending on how to connect to Intune:  
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment**  &gt; **Apple MDM Push Certificate**, enter your Apple ID in step 3, select the certificate (.pem) file in step 4, and then click **Upload**.     
    <br/>
    **Microsoft Intune administration console**    -->
    In the [Microsoft Intune administration console](http://manage.microsoft.com), go to **Administration** &gt; **Mobile Device Management** &gt; **iOS and Mac OS X** &gt; **Upload an APNs Certificate**, and then choose **Upload the APNs certificate**. Go to the certificate (.pem) file, choose **Open**, and then enter your **Apple ID**.   

    ![Upload the APNs certificate](/sccm/mdm/deploy-use/media/mdm-change-upload-apns-certificate.png)

### <a name="next-steps"></a>Próximas etapas
Depois de a alteração na autoridade de MDM ser concluída, examine as seguintes etapas:
- Quando o serviço Intune detectar que a autoridade de MDM de um locatário foi alterada, ele enviará uma mensagem de notificação para todos os dispositivos registrados para fazer check-in e sincronizar com o serviço (isso ocorre fora do check-in agendado regularmente). Portanto, depois que a autoridade de MDM para o locatário tiver sido alterada de híbrida para o Intune autônomo, todos os dispositivos que estiverem ligados e online se conectarão ao serviço, receberão a nova autoridade de MDM e serão gerenciados pelo Intune autônomo no futuro. Não haverá interrupção para o gerenciamento e a proteção desses dispositivos.
- Os dispositivos que estiverem desativados ou offline durante (ou logo após) a alteração na autoridade de MDM se conectarão e sincronizarão com o serviço na nova autoridade de MDM quando estiverem ligados e online.  

  Os dispositivos iOS exigem mais tempo para renovar e configurar o certificado APNs. Portanto, os dispositivos iOS não receberão a solicitação de check-in inicial. Mesmo se os dispositivos iOS estiverem ligados e online durante (ou logo após) a alteração na autoridade de MDM, haverá um atraso de até oito horas (dependendo do horário do próximo check-in regular agendado) antes de os dispositivos iOS serem registrados com o serviço sob a nova autoridade de MDM.    

  > [!IMPORTANT]
  > Entre o momento em que você altera a autoridade de MDM e em que o certificado APNs renovado é carregado para a nova autoridade, novos registros de dispositivo e check-in de dispositivo para dispositivos iOS falharão. Portanto, é importante que você analise e carregue o certificado APNs para a nova autoridade assim que possível após a alteração na autoridade de MDM.   

- Os usuários podem alterar rapidamente para a nova autoridade de MDM iniciando manualmente um check-in do dispositivo para o serviço. Os usuários podem fazer isso facilmente pelo aplicativo Portal da Empresa e iniciando uma verificação de conformidade do dispositivo.
- Para validar que as coisas estão funcionando corretamente depois que os dispositivos fizerem check-in e forem sincronizados com o serviço após a alteração na autoridade de MDM, procure os dispositivos no [Console de administração do Microsoft Intune](http://manage.microsoft.com). Os dispositivos que eram gerenciados anteriormente pelo Configuration Manager (híbrido) agora serão exibidos como dispositivos gerenciados.    
- Há um período provisório em que um dispositivo está offline durante a alteração na autoridade de MDM e quando esse dispositivo faz check-in no serviço. Para ajudar a garantir que o dispositivo permaneça protegido e funcional durante esse período provisório, os seguintes itens permanecerão no dispositivo por até sete dias (ou até que o dispositivo se conecte com a nova autoridade de MDM e receba novas configurações que substituirão as existentes):
    - Perfil de email
    - Perfil da VPN
    - Perfil de certificado
    - Perfil de Wi-Fi
    - Perfis de configuração
- Verifique se as novas configurações que se destinam a substituir as configurações existentes têm o mesmo nome que as anteriores para garantir que as configurações antigas sejam substituídas. Caso contrário, os dispositivos podem acabar com políticas e perfis redundantes.
    > [!TIP]   
    > Como prática recomendada, você deve criar todos os parâmetros de gerenciamento e as configurações, além das implantações, logo após a alteração para a autoridade de MDM ser concluída. Isso ajuda a garantir que os dispositivos estejam protegidos e sejam gerenciados ativamente durante o período intermediário.   
-  Depois de alterar a autoridade MDM, execute as etapas a seguir para validar que os novos dispositivos sejam registrados com êxito para a nova autoridade:   
    - Registrar um novo dispositivo
    - Verifique se o dispositivo registrado recentemente aparece no console de administração do Intune.
    - Execute uma ação, como bloqueio remoto, do console de administração para o dispositivo. Se a ação for bem-sucedida, isso significará que o dispositivo está sendo gerenciado pela nova autoridade de MDM.
- Se você tiver problemas com dispositivos específicos, poderá cancelar o registro e registrar novamente os dispositivos para que eles se conectem à nova autoridade e sejam gerenciados o mais rápido possível.

<!-- After the change in MDM authority and devices check in with the service, note the following:      - The updated compliance status of devices will only display in the Azure portal immediately.
- There will be a delay for compliance status of devices to display in the Intune administrative console.-->


## <a name="change-the-mdm-authority-to-configuration-manager-hybrid"></a>Alterar a autoridade de MDM para o Configuration Manager (híbrido)
Use esta seção para alterar um locatário existente do Microsoft Intune configurado do Intune e com a autoridade de MDM definida do **Microsoft Intune** (autônomo) para o **Configuration Manager** (híbrido) sem a necessidade de cancelar o registro e registrar novamente os dispositivos gerenciados existentes.

### <a name="key-considerations"></a>Principais considerações
Depois de alternar para a nova autoridade de MDM, provavelmente haverá tempo de transição (até oito horas) antes de o dispositivo fazer o check-in e sincronizar com o serviço. Será necessário definir as configurações na nova autoridade de MDM (híbrido) para garantir que os dispositivos registrados continuarão a ser gerenciado e protegidos após a alteração. . Observe o seguinte:
- Os dispositivos devem se conectar com o serviço após a alteração para que as configurações da nova autoridade de MDM (Intune autônomo) substitua as configurações no dispositivo.
- Depois de alterar a autoridade de MDM, algumas das configurações básicas (como perfis) da autoridade de MDM anterior (Intune autônomo) permanecem no dispositivo por até 7 dias ou até que o dispositivo se conecte com o serviço pela primeira vez. É recomendável que você configure aplicativos e parâmetros (políticas, perfis, aplicativos etc.) na nova autoridade de MDM (híbrido) assim que possível e implante as configurações para os grupos de usuários que contêm usuários que têm dispositivos registrados. Assim que um dispositivo se conectar ao serviço após a alteração na autoridade de MDM, ele receberá as novas configurações da nova autoridade de MDM e evitará falhas na proteção e no gerenciamento.
- Os dispositivos que não têm usuários associados (normalmente quando você tem o Programa de registro de dispositivos iOS ou cenários de registro em massa) não são migrados para a nova autoridade de MDM. Para esses dispositivos, você precisa chamar o suporte para obter assistência para movê-los para a nova autoridade de MDM.

### <a name="prepare-to-change-the-mdm-authority-to-configuration-manager-hybrid"></a>Preparar para alterar a autoridade de MDM para o Configuration Manager (híbrido)
Examine as informações a seguir para se preparar para a alteração para a autoridade de MDM:
- Você deve ter o Configuration Manager versão 1610 ou superior para que a opção que altera a autoridade de MDM esteja disponível.
- Pode levar até oito horas para um dispositivo se conectar ao serviço depois que você alterar para a nova autoridade de MDM.
- Crie uma coleção de usuário do Configuration Manager com todos os usuários atualmente gerenciados pelo Intune autônomo que será usada quando você configurar a assinatura do Intune no console do Configuration Manager. Isso ajudará a garantir que o usuário e seus dispositivos terão uma licença do Configuration Manager atribuída e serão gerenciados no ambiente híbrido após a alteração para a autoridade de MDM.
- Verifique se o usuário administrador de TI está nesta coleção de usuário também.  
- Antes da alteração, a autoridade de MDM será exibida como **Definida como Microsoft Intune** (autônomo) no console de administração do Intune.
- A autoridade de MDM deve exibir **Definir para o Microsoft Intune** (locatário autônomo) no console de administração do Microsoft Intune antes da alteração na autoridade de MDM.
    > [!NOTE]    
    > Se sua autoridade de MDM exibir **Gerenciado pelo Intune e pelo Office 365**, os dispositivos de MDM gerenciados pelo Office 365 não serão mais gerenciados quando você alterar sua autoridade de MDM para **Configuration Manager** (híbrido). É recomendável que você licencie esses usuários para o Intune ou Enterprise Mobility Suite antes de alterar a autoridade de MDM.   

- No [Console de Administração do Microsoft Intune](http://manage.microsoft.com), remova a função de Gerenciador de Registro de Dispositivos. Para obter detalhes, veja [Excluir um gerenciador de registro de dispositivos do Intune](/intune-classic/deploy-use/enroll-corporate-owned-devices-with-the-device-enrollment-manager-in-microsoft-intune#delete-a-device-enrollment-manager-from-intune).
- Desative os mapeamentos de grupo de dispositivos que estiverem configurados. Para obter detalhes, veja [Categorizar os dispositivos com o mapeamento de grupo de dispositivos no Microsoft Intune](/intune-classic/deploy-use/categorize-devices-with-device-group-mapping-in-microsoft-intune).
- Não deve haver nenhum impacto perceptível para os usuários finais durante a alteração na autoridade de MDM. No entanto, você talvez deva comunicar esta alteração aos usuários para que eles verifiquem se seus dispositivos estão ligados e se eles conseguem se conectar ao serviço logo após a alteração. Isso garantirá que o máximo de dispositivos possível se conectará e se registrará com o serviço por meio da nova autoridade o mais rápido possível.
- Se você estiver usando o Intune autônomo para gerenciar dispositivos iOS antes da alteração na autoridade de MDM, deverá garantir que o mesmo certificado Apple Push Notification Service (APNs) que era usado no Intune seja renovado e usado para configurar o locatário novamente no Configuration Manager (híbrido).    

    > [!IMPORTANT]  
    > Se um certificado APNs diferente for usado para híbrido, TODOS os dispositivos iOS registrados anteriormente terão o registro cancelado e você precisará passar pelo processo de registrá-los novamente. Antes de fazer a alteração da autoridade de MDM, verifique se você sabe exatamente qual certificado APNs foi usado para gerenciar os dispositivos iOS no Intune. Localize o mesmo certificado listado no Apple Push Certificates Portal (https://identity.apple.com), o Portal de Certificados por Push da Apple, e verifique se o usuário cuja ID da Apple usada para criar o certificado APNs original é identificado e está disponível para renovar o mesmo certificado APNs como parte da mudança para a nova autoridade de MDM.  

### <a name="change-the-mdm-authority-to-configuration-manager"></a>Alterar a autoridade de MDM para o Configuration Manager
O processo para alterar a autoridade de MDM para o Configuration Manager (híbrido) inclui as seguintes etapas de alto nível:  
- No console do Configuration Manager, adicione a assinatura do Microsoft Intune.
- Configure o certificado de APNs da Apple usando o mesmo certificado de APNs que você renovou.
- No console do Configuration Manager, configure e implante novas configurações e aplicativos da nova autoridade de MDM (híbrido).
- Da próxima vez que o dispositivo se conectar ao serviço, ele sincronizará e receberá as novas configurações da nova autoridade de MDM.

#### <a name="to-change-the-mdm-authority-to-configuration-manager"></a>Para alterar a autoridade de MDM para o Configuration Manager
1.  No console do Configuration Manager, no espaço de trabalho **Administração** &gt; **Visão Geral** &gt; **Serviços de Nuvem** &gt; **Assinaturas do Microsoft Intune** e selecione para adicionar uma assinatura do Intune.
2.  Entre no locatário do Intune que você usou originalmente quando definiu a autoridade de MDM no Intune e clique em **Avançar**.
3.  Selecione **Alterar minha autoridade do MDM para o Configuration Manager** e clique em **Avançar**.
4.  Selecione a coleção de usuário que conterá todos os usuários que continuarão a ser gerenciados pela nova autoridade de MDM híbrida.
5.  Clique em **Próximo** e conclua o assistente.  
5.  A autoridade de MDM agora é alterada para o **Configuration Manager**.
6.  Faça logon no [Console de administração do Microsoft Intune](http://manage.microsoft.com) usando o mesmo locatário do Intune e confirme que a autoridade de MDM foi alterada para **Definir para o Configuration Manager**.


### <a name="enable-ios-enrollment"></a>Habilitar registro do iOS
Quando você tiver dispositivos iOS, deverá configurar o certificado APNs no Configuration Manager.

#### <a name="to-enable-ios-enrollment-and-configure-the-apns-certificate"></a>Para habilitar o registro do iOS e configurar o certificado APNs

1. **Baixar uma solicitação de assinatura de certificado**

    1.  No console do Configuration Manager, vá para **Administração** &gt; **Serviços de Nuvem** &gt; **Assinaturas do Microsoft Intune** e selecione **Criar solicitação de certificado APNs** para abrir a caixa de diálogo **Solicitar Solicitação de Assinatura de Certificado Apple Push Notification Service**.  
    2.  **Navegue** até o caminho para salvar o novo arquivo de solicitação de assinatura de certificado (.csr). Salve o arquivo (.csr) da solicitação de assinatura do certificado localmente.  
    3.  Clique em **Baixar**. O novo arquivo .csr do Microsoft Intune é baixado e salvo pelo Configuration Manager.   

    > [!IMPORTANT]
    > Você deve baixar uma solicitação de assinatura de novo certificado. Não use um arquivo existente ou ocorrerá erro.  

2.  Vá para o [Portal de Certificados de Push da Apple](http://go.microsoft.com/fwlink/?LinkId=269844) e entre com a **mesma** ID da Apple que foi usada anteriormente para criar e renovar o certificado APNs que você usou no Intune autônomo.

    ![Página de conexão do Portal de Certificados de Push da Apple](/sccm/mdm/deploy-use/media/mdm-change-apns-portal.png)

3.  Selecione o certificado APNs que você usou no Intune autônomo e, em seguida, clique em **Renovar**.   

    ![Caixa de diálogo Renovar APNs](/sccm/mdm/deploy-use/media/mdm-change-renew-apns.png)

4.  Selecione o arquivo de solicitação de assinatura de certificado APNs (.csr) que você baixou e, em seguida, clique em **Carregar**.

    ![Página de conexão do Portal de Certificados de Push da Apple](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-upload.png)  
5.  Selecione o mesmo APNs e, em seguida, clique em **Baixar**. Baixe o certificado APNs (.pem) e salve o arquivo localmente.  

    ![Página de conexão do Portal de Certificados de Push da Apple](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-download.png)

6.  Carregue o certificado APNs renovado para o locatário híbrido usando a mesma ID da Apple que antes.

    1.  No console do Configuration Manager, no espaço de trabalho **Administração** &gt; **Serviços de Nuvem** &gt; **Assinaturas do Microsoft Intune** e escolha **Configurar Plataformas** &gt; **iOS**.  
    2.  Na caixa de diálogo **Propriedades da Assinatura do Microsoft Intune**, selecione a guia **Certificado APNs** e clique para marcar a caixa de seleção **Habilitar registro do iOS e do MAC OS X (MDM)**.  
    3.  Clique em **Procurar**e vá para o arquivo de certificado APNs (.cer) baixado da Apple. O Configuration Manager exibe as informações de certificado APNs. Clique em **OK** para salvar o certificado APNs no Intune.  

        ![Página de propriedades de assinatura do Intune - iOS](/sccm/mdm/deploy-use/media/mdm-change-subscription-properties-ios.png)

### <a name="enable-android-enrollment"></a>Habilitar o registro do Android
1. No console do Configuration Manager, no espaço de trabalho **Administração** &gt; **Serviços de Nuvem** &gt; **Assinaturas do Microsoft Intune** e escolha **Configurar Plataformas** &gt; **Android**.  
2. Selecione **Habilitar registro do Android** e clique em **OK**.

### <a name="enable-windows-enrollment"></a>Habilitar o registro do Windows
1. No console do Configuration Manager, no espaço de trabalho **Administração** &gt; **Serviços de Nuvem** &gt; **Assinaturas do Microsoft Intune** e escolha **Configurar Plataformas** &gt; **Windows**.  
2. Selecione **Habilitar registro do Windows** e clique em **OK**.

### <a name="enable-windows-phone-enrollment"></a>Habilitar registro do Windows Phone
1. No console do Configuration Manager, no espaço de trabalho **Administração** &gt; **Serviços de Nuvem** &gt; **Assinaturas do Microsoft Intune** e escolha **Configurar Plataformas** &gt; **Windows Phone**.  
2. Selecione a plataforma que você deseja habilitar e clique em **OK**.


### <a name="next-steps"></a>Próximas etapas
Depois de a alteração na autoridade de MDM ser concluída, examine as seguintes etapas:
- Quando o serviço Intune detectar que a autoridade de MDM de um locatário foi alterada, ele enviará uma mensagem de notificação para todos os dispositivos registrados para fazer check-in e sincronizar com o serviço (isso ocorre fora do check-in agendado regularmente). Portanto, depois que a autoridade de MDM para o locatário tiver sido alterada de Intune autônomo para híbrida, todos os dispositivos que estiverem ligados e online se conectarão ao serviço, receberão a nova autoridade de MDM e serão gerenciados pelo híbrido no futuro. Não haverá interrupção para o gerenciamento e a proteção desses dispositivos.
- Mesmo para os dispositivos ligados e online durante (ou logo após) a alteração na autoridade de MDM, haverá um atraso de até oito horas (dependendo do horário do próximo check-in regular agendado) antes de os dispositivos serem registrados com o serviço sob a nova autoridade de MDM.    

  > [!IMPORTANT]
  > Entre o momento em que você altera a autoridade de MDM e em que o certificado APNs renovado é carregado para a nova autoridade, novos registros de dispositivo e check-in de dispositivo para dispositivos iOS falharão. Portanto, é importante que você analise e carregue o certificado APNs para a nova autoridade assim que possível após a alteração na autoridade de MDM.

- Os usuários podem alterar rapidamente para a nova autoridade de MDM iniciando manualmente um check-in do dispositivo para o serviço. Os usuários podem fazer isso facilmente pelo aplicativo Portal da Empresa e iniciando uma verificação de conformidade do dispositivo.
- Para validar que as coisas estão funcionando corretamente depois que os dispositivos fizerem check-in e forem sincronizados com o serviço após a alteração na autoridade de MDM, procure os dispositivos no Console do Configuration Manager. Os dispositivos que eram gerenciados anteriormente pelo Intune agora serão exibidos como dispositivos gerenciados no console do Configuration Manager.    
- Há um período provisório em que um dispositivo está offline durante a alteração na autoridade de MDM e quando esse dispositivo faz check-in no serviço. Para ajudar a garantir que o dispositivo permaneça protegido e funcional durante esse período provisório, os seguintes itens permanecerão no dispositivo por até 7 dias (ou até que o dispositivo se conecte com a nova autoridade de MDM e receba novas configurações que substituirão as existentes):
    - Perfil de email
    - Perfil da VPN
    - Perfil de certificado
    - Perfil de Wi-Fi
    - Perfis de configuração
- Após você alterar para a nova autoridade de MDM, os dados de conformidade no console de administração do Microsoft Intune poderá levar até uma semana para relatar com precisão. No entanto, os estados de conformidade no Azure Active Directory e no dispositivo serão precisos, então o dispositivo ainda estará protegido.
- Verifique se as novas configurações que se destinam a substituir as configurações existentes têm o mesmo nome que as anteriores para garantir que as configurações antigas sejam substituídas. Caso contrário, os dispositivos podem acabar com políticas e perfis redundantes.
    > [!TIP]   
    > Como prática recomendada, você deve criar todos os parâmetros de gerenciamento e as configurações, além das implantações, logo após a alteração para a autoridade de MDM ser concluída. Isso ajuda a garantir que os dispositivos estejam protegidos e sejam gerenciados ativamente durante o período intermediário.   
-  Depois de alterar a autoridade MDM, execute as etapas a seguir para validar que os novos dispositivos sejam registrados com êxito para a nova autoridade:   
    - Registrar um novo dispositivo
    - Verifique se o dispositivo registrado recentemente aparece no console do Configuration Manager.
    - Execute uma ação, como bloqueio remoto, do console de administração para o dispositivo. Se a ação for bem-sucedida, isso significará que o dispositivo está sendo gerenciado pela nova autoridade de MDM.
- Se você tiver problemas com dispositivos específicos, poderá cancelar o registro e registrar novamente os dispositivos para que eles se conectem à nova autoridade e sejam gerenciados o mais rápido possível.
