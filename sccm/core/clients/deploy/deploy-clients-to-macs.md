---
title: "Implantar os clientes Mac | Microsoft Docs"
description: "Saiba como implantar clientes em computadores Mac no System Center Configuration Manager."
ms.custom: na
ms.date: 11/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
caps.latest.revision: 12
author: nbigman
ms.author: nbigman
manager: angrobe

---
# <a name="how-to-deploy-clients-to-macs-in-system-center-configuration-manager"></a>How to deploy clients to Macs in System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico descreve como instalar o cliente do Configuration Manager em computadores Mac.

## <a name="prerequisites-and-preparatory-steps"></a>Pré-requisitos e etapas preparatórias

### <a name="mac-prerequisites"></a>Pré-requisitos do Mac

Antes de instalar o cliente, certifique-se de que os computadores Mac atendem aos pré-requisitos, conforme descrito em [Supported operating systems for Macs](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers) (Sistemas operacionais com suporte para Macs).  

### <a name="certificate-requirements"></a>Requisitos de certificado
A instalação e o gerenciamento do cliente para computadores Mac exigem certificados de PKI (infraestrutura de chave pública). Os certificados PKI protegem a comunicação entre os computadores Mac e o site do Configuration Manager usando autenticação mútua e transferência de dados criptografados. O Configuration Manager pode solicitar e instalar um certificado de cliente do usuário usando os Serviços de Certificados da Microsoft com uma AC (autoridade de certificação) corporativa e as funções do sistema de sites de ponto de registro e ponto proxy do registro do Configuration Manager. Ou você poderá solicitar e instalar um certificado de computador independentemente do Configuration Manager se o certificado atender aos requisitos do Configuration Manager.   
  
Os clientes Mac do Configuration Manager sempre fazem a verificação de revogação de certificado. Diferente dos clientes do Configuration Manager que são executados no Windows, não é possível desabilitar essa função de verificação de CRL (lista de certificados revogados).  
  
Se os clientes Mac não puderem confirmar o status de revogação de um certificado do servidor porque não conseguem localizar a CRL, eles não poderão se conectar com êxito aos sistemas de sites do Configuration Manager, como pontos de gerenciamento e pontos de distribuição. Especialmente para clientes Mac em uma floresta diferente da autoridade de certificação emissora, verifique o design da sua CRL para garantir que os clientes Mac possam localizar e se conectar a um CDP (ponto de distribuição) de CRL para estabelecer conexão com servidores do sistema de site.  

Antes de instalar o cliente do Configuration Manager em um computador Mac, decida como o certificado do cliente será instalado:  

-   Usar o registro do Configuration Manager utilizando a ferramenta CMEnroll e siga as etapas na próxima seção deste tópico. O processo de registro não oferece suporte à renovação automática de certificados, portanto, é necessário registrar novamente os computadores Mac antes de o certificado instalado expirar.  

-   Usar um método de solicitação e instalação do certificado que é independente do Configuration Manager. Para esse método de instalação, consulte a seção [Use a certificate request and installation method that is independent from Configuration Manager](#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager) neste tópico.  

Para obter mais informações sobre o requisito de certificado do cliente Mac e outros certificados PKI necessários para dar suporte a computadores Mac, consulte [Requisitos de certificado PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

Os clientes Mac são atribuídos automaticamente ao site do Configuration Manager que os gerencia. Os clientes Mac são instalados como clientes somente de Internet, mesmo se a comunicação for restrita à intranet. Essa configuração de cliente significa que eles se comunicarão com as funções de sistema de site (pontos de gerenciamento e de distribuição) em seus sites atribuídos quando você configurar essas funções do sistema de site para permitir conexões de clientes por meio da Internet. Os computadores Mac não se comunicam com as funções do sistema de site fora do site atribuído.  

> [!IMPORTANT]  
>  O cliente Mac do Configuration Manager não pode ser usado para se conectar a um ponto de gerenciamento configurado para usar uma [réplica de banco de dados](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  


### <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Implantar um certificado do servidor Web nos servidores do sistema de sites  
Caso os sistemas de sites ainda não tenham um certificado do servidor Web, implante um nos computadores que têm as funções de sistema de sites a seguir:  

-   Ponto de gerenciamento  

-   Ponto de distribuição  

-   Ponto de registro  

-   Ponto proxy do registro  

O Certificado do servidor Web deve conter o FQDN de Internet especificado nas propriedades de sistema de site. O servidor não precisa ser acessível pela Internet para dar suporte a computadores Mac. Se você não precisa de gerenciamento de clientes baseado na Internet, pode especificar o valor de FQDN de intranet para o FQDN de Internet.  

Especifique o valor do FQDN de Internet do sistema de sites no certificado do servidor Web para o ponto de gerenciamento, o ponto de distribuição e o ponto proxy do registro. 

Para ver um exemplo de implantação que cria e instala esse certificado do servidor Web, consulte [Implantando o certificado do servidor Web para sistemas de sites que executam IIS](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  

 

### <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>Implantar um certificado de autenticação de cliente nos servidores do sistema de sites  
 Caso esses sistemas de sites não o tenham, implante um certificado de autenticação de cliente nos seguintes computadores que hospedam as seguintes funções de sistema de sites:  

-   Ponto de gerenciamento  

-   Ponto de distribuição  

 Para ver um exemplo de implantação que cria e instala o certificado do cliente para pontos de gerenciamento, consulte [Implantando o certificado do cliente para computadores com Windows](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)  

 Para ver um exemplo de implantação que cria e instala o certificado do cliente para pontos de distribuição, consulte [Implantando o certificado do cliente para pontos de distribuição](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

### <a name="prepare-the-client-certificate-template-for-macs"></a>Preparar o modelo de certificado do cliente para Macs  

> [!NOTE]  
>  Para executar a ferramenta de registro do Configuration Manager, é necessário ter uma conta de usuário do Active Directory.  

 O modelo de certificado deve ter permissões de **Leitura** e **Registro** para a conta de usuário que registrará o certificado no computador Mac.  

 Consulte [Implantando o certificado do cliente para computadores Mac](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1).  

### <a name="configure-the-management-point-and-distribution-point"></a>Configurar o ponto de gerenciamento e o ponto de distribuição  
 Configure os pontos de gerenciamento para as seguintes opções:  

-   HTTPS  

-   Permitir conexões do cliente por meio da Internet. Esse valor de configuração é necessário para gerenciar computadores Mac. No entanto, isso não significa que os servidores do sistema de site devem ser acessíveis pela Internet.  

-   Permitir que dispositivos móveis e computadores Mac usem este ponto de gerenciamento  

 Embora não sejam necessários pontos de distribuição para a instalação do cliente, você deverá configurar pontos de distribuição para permitir conexões de clientes por meio da Internet se desejar implantar software nesses computadores após o cliente ser instalado.  

 
##### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>Para configurar pontos de gerenciamento e pontos de distribuição para dar suporte a Mac  

Antes de iniciar esse procedimento, verifique se o servidor de sistema de site que executa o ponto de gerenciamento e o ponto de distribuição está configurado com um FQDN de Internet. Se esses servidores não derem suporte ao gerenciamento de clientes baseado na Internet, você poderá especificar o FQDN de intranet como o valor de FQDN de Internet. 

As funções de sistema de sites devem estar em um site primário.  


1.  No console do Configuration Manager, escolha **Administração** > **Configuração do Site** > **Funções de Servidores e Sistema de Site** e escolha o servidor com as funções do sistema de site corretas.  

3.  No painel de detalhes, clique com o botão direito do mouse no **Ponto de gerenciamento**, escolha **Propriedades de Função** e, na caixa de diálogo **Propriedades do Ponto de Gerenciamento**, configure as opções a seguir:  

    1.  Escolha **HTTPS**.  

    2.  Escolha **Permitir conexões de cliente apenas de Internet** ou **Permitir conexões de cliente de intranet e Internet**. Essas opções exigem um FQDN de Internet ou de intranet.  

    3.  Escolha **Permitir que dispositivos móveis e computadores Mac usem este ponto de gerenciamento**.  

4.  No painel de detalhes, clique com o botão direito do mouse em **Ponto de distribuição**, escolha **Propriedades de Função** e, na caixa de diálogo **Propriedades do Ponto de Distribuição**, configure as opções a seguir:  

    -   Escolha **HTTPS**.  

    -   Escolha **Permitir conexões de cliente apenas de Internet** ou **Permitir conexões de cliente de intranet e Internet**. Essas opções exigem um FQDN de Internet ou de intranet.  

    -   Escolha **Importar certificado**, navegue até o arquivo do certificado do ponto de distribuição do cliente exportado e especifique a senha.  

5.  Repita as etapas de 2 a 4 para todos os pontos de gerenciamento e de distribuição nos sites primários que você usará com Macs.  

### <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Configurar o ponto proxy do registro e o ponto de registro  
 É necessário instalar ambas as funções de sistema de site no mesmo site, mas não é necessário instalá-las no mesmo servidor de sistema de site ou na mesma floresta do Active Directory.  

 Para obter mais informações e considerações sobre o posicionamento de funções de sistema de sites, consulte [Funções de sistema de sites](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) em [Planejar funções e servidores do sistema de sites para o System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).  

 Estes procedimentos configuram as funções do sistema de site para oferecer suporte a computadores Mac. Escolha um desses procedimentos dependendo se você instalará um novo servidor do sistema de site para oferecer suporte a computadores Mac ou se usará um servidor do sistema de site existente:  

-   [Novo servidor do sistema de sites](#new-site-system-server)  

-   [Servidor do sistema de sites existente](#existing-site-system-server)  

####  <a name="new-site-system-server"></a>Novo servidor do sistema de site  

1.  No console do Configuration Manager, escolha **Administração** >  **Configuração do Site** > **Funções de Servidores e Sistema de Site**  

3.  Na guia **Início**, no grupo **Criar**, escolha **Criar Servidor do Sistema de Site**.  

4.  Na página **Geral**, especifique as configurações gerais do sistema de sites.  Não se esqueça de especificar um valor para o FQDN de Internet. Se o servidor não puder ser acessado pela Internet, use o FQDN de intranet.  

5.  Na página **Seleção de Função do Sistema**, selecione **Ponto proxy do registro** e **Ponto de registro** na lista de funções disponíveis.  

6.  Na página **Ponto Proxy do Registro**, examine as configurações e faça as alterações necessárias.  

7.  Na página **Configurações do Ponto de Registro**, examine as configurações e faça as alterações necessárias. Em seguida, conclua o assistente.  

#### <a name="existing-site-system-server"></a>Servidor do sistema de site existente  

1.  No console do Configuration Manager, escolha **Administração** >  **Configuração do Site** > **Funções de Servidores e Sistema de Site** e escolha o servidor que deseja usar para dar suporte a Macs.  

3.  Na guia **Início**, no grupo **Criar**, escolha **Adicionar Funções do Sistema de Site**.  

4.  Na página **Geral** , especifique as configurações gerais para o sistema de site e clique em **Próximo**. Não se esqueça de especificar um valor para o FQDN de Internet. Se o servidor não puder ser acessado pela Internet, use o FQDN de intranet.   

5.  Na página **Seleção de Função do Sistema**, escolha **Ponto proxy do registro** e **Ponto de registro** na lista de funções disponíveis.  

6.  Na página **Ponto Proxy do Registro**, examine as configurações e faça as alterações necessárias.  

7.  Na página **Configurações do Ponto de Registro**, examine as configurações e faça as alterações necessárias. Em seguida, conclua o assistente.  

### <a name="optional-install-the-reporting-services-point"></a>Opcional: instalar o ponto do Reporting Services  
 Instale o ponto do Reporting Services se desejar executar relatórios para Macs.  

 Para obter mais informações sobre como instalar e configurar o ponto do Reporting Services, consulte [Configurando relatórios no System Center Configuration Manager](../../../core/servers/manage/configuring-reporting.md).  


##  <a name="install-and-configure-the-client-for-macs"></a>Instalar e configurar o cliente para Macs  


### <a name="configure-client-settings-for-enrollment"></a>Defina as configurações do cliente para o registro  
 É necessário usar as configurações de cliente padrão para configurar o registro para computadores Mac; não é possível usar configurações de cliente personalizadas.  

 Para obter mais informações sobre configurações do cliente, consulte [About client settings in System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md).  

 Isso é necessário para que o Configuration Manager solicite e instale o certificado no Mac.  

#### <a name="to-configure-the-default-client-settings-for-configuration-manager-to-enroll-certificates-for-macs"></a>Para definir as configurações de cliente padrão para o Configuration Manager registrar certificados para Mac  

1.  No console do Configuration Manager, escolha **Administração** >  **Configurações do Cliente** > **Configurações do Cliente Padrão**.  

4.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

5.  Selecione a seção **Registro** e defina essas configurações:  

    1.  **Permitir que os usuários registrem dispositivos móveis e computadores Mac: Sim**  

    2.  **Perfil de registro:** escolha **Definir Perfil**.  

6.  Na caixa de diálogo **Perfil de Registro do Dispositivo Móvel** escolha **Criar**.  

7.  Na caixa de diálogo **Criar Perfil de Registro** , insira um nome para esse perfil de registro e configure o **Código do site de gerenciamento**. Selecione o site primário do Configuration Manager que contém os pontos de gerenciamento que gerenciarão os computadores Mac.  

    > [!NOTE]  
    >  Caso não consiga selecionar o site, verifique se pelo menos um ponto de gerenciamento no site está configurado para dar suporte a dispositivos móveis.  

8.  Escolha **Adicionar**.  

9. Na caixa de diálogo **Adicionar Autoridade de Certificação para Dispositivos Móveis**, selecione o servidor da AC (autoridade de certificação) que emitirá certificados para computadores Mac.  

10. Na caixa de diálogo **Criar Perfil de Registro**, selecione o modelo de certificado do computador Mac criado na Etapa 3.  

11. Clique em **OK** para fechar a caixa de diálogo **Perfil de Registro** e a caixa de diálogo **Configurações do Cliente Padrão**.  

    > [!TIP]  
    >  Se desejar alterar o intervalo da política do cliente use a configuração do cliente **Intervalo de sondagem da política do cliente** no grupo de configuração do cliente **Política do Cliente** .  

 Todos os usuários serão configurados com essas definições na próxima vez que baixarem a política do cliente. Para iniciar a recuperação de política para um cliente individual, consulte [Iniciar a recuperação de política para um cliente do Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  

 Além das configurações do cliente de registro, defina as seguintes configurações do dispositivo do cliente do Configuration Manager:  

-   **Inventário de hardware**: habilite e configure isso se desejar coletar inventário de hardware dos computadores cliente Mac e Windows. Para obter mais informações, consulte [Como estender o inventário de hardware no System Center Configuration Manager](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

-   **Configurações de conformidade**: habilite e configure isso se desejar avaliar e corrigir configurações em computadores cliente Mac e Windows. Para obter mais informações, consulte [Planejar e definir configurações de conformidade](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

> [!NOTE]  
>  Para obter mais informações sobre as configurações do cliente do Configuration Manager, consulte [Como definir as configurações do cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).  

### <a name="download-the-client-source-files-for-macs"></a>Baixar os arquivos de origem do cliente para Mac  
 Baixe e instale os seguintes programas antes de instalar e gerenciar o cliente do Configuration Manager em computadores Mac:  

-   **Ccmsetup**: use este aplicativo para instalar o cliente do Configuration Manager nos seus computadores Mac.  

-   **CMDiagnostics**: use esta ferramenta para coletar informações de diagnóstico relacionadas ao cliente do Configuration Manager em seus computadores Mac.  

-   **CMUninstall**: use esta ferramenta para desinstalar o cliente do Configuration Manager de seus computadores Mac.  

-   **CMAppUtil**: use esta ferramenta para converter pacotes de aplicativos da Apple em um formato que possa ser implantado como um aplicativo do Configuration Manager.  

-   **CMEnroll**: use esta ferramenta para solicitar e instalar o certificado do cliente em um computador Mac para que você possa instalar o cliente do Configuration Manager.  

> [!IMPORTANT]  
>  Quando instala um novo cliente para computadores Mac, talvez você também precise instalar atualizações do Configuration Manager para refletir as novas informações de cliente no console do Configuration Manager.  

##### <a name="to-download-and-install-the-mac-os-x-client-files"></a>Para baixar e instalar os arquivos do cliente Mac OS X  

1.  Baixe o pacote de arquivos do cliente Mac OS X, **ConfigmgrMacClient.msi**e salve-o em um computador que executa o Windows.  

     Esse arquivo não é fornecido na mídia de instalação do Configuration Manager. Você pode baixar o arquivo do [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

2.  No computador Windows, execute o arquivo **ConfigmgrMacClient.msi** que você acabou de baixar para extrair o pacote do cliente Mac Macclient.dmg para uma pasta no disco local (por padrão **C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client\\**).  

3.  Copie o arquivo Macclient.dmg para uma pasta no computador Mac.  

4.  No computador Mac, execute o arquivo Macclient.dmg para extrair os arquivos para uma pasta no disco local.  

5.  Na pasta, verifique se os arquivos Ccmsetup e CMClient.pkg foram extraídos e se uma pasta chamada Ferramentas foi criada e contém as ferramentas CMDiagnostics, CMUninstall, CMAppUtil e CMEnroll.  

### <a name="install-the-client-and-then-enroll-the-client-certificate-on-the-mac"></a>Instalar o cliente e registrar o certificado do cliente no computador Mac  
 Este procedimento instala o cliente e usa a ferramenta CMEnroll para solicitar e instalar o certificado do cliente para um computador Mac, para que seja possível gerenciar esse computador usando o Configuration Manager.  

 Você pode registrar o cliente usando o Assistente de Registro de Computador Mac sem precisar usar a ferramenta CMEnroll, conforme descrito em [Registrar o cliente usando o Assistente de Registro de Computador Mac](#enroll-the-client-by-using-the-mac-computer-enrollment-wizard)  

#### <a name="to-install-the-client-and-enroll-the-certificate-by-using-the-cmenroll-tool"></a>Para instalar o cliente e registrar o certificado usando a ferramenta de CMEnroll  

1.  No computador Mac, navegue até a pasta em que você extraiu o conteúdo do arquivo Macclient.dmg.  

2.  Digite a seguinte linha de comando: **sudo ./ccmsetup**  

3.  Aguarde até que você veja a mensagem **Instalação concluída** . Embora o instalador exiba uma mensagem para que você reinicie agora, não reinicie, e passe para a etapa seguinte.  

4.  Na pasta Ferramentas no computador Mac, digite o seguinte: **sudo ./CMEnroll -s &lt;nome_servidor_proxy_registro> -ignorecertchainvalidation -u &lt;'nome de usuário'>**  

    Após a instalação do cliente, o assistente de Registro de Computador Mac é aberto para ajudá-lo a registrar o computador Mac. Para registrar o cliente por esse método, consulte [To enroll the client by using the Mac Computer Enrollment Wizard](#BKMK_EnrollR2) neste tópico.  

5. Digite a senha para a conta de usuário do Active Directory.  Quando você digitar esse comando, serão solicitadas duas senhas: o primeiro prompt destina-se à conta de superusuário para executar o comando. O segundo prompt destina-se à conta de usuário do Active Directory. Os prompts parecem idênticos, portanto certifique-se de especificá-los na sequência correta.  

    O nome de usuário pode estar nos seguintes formatos:  

    -   'domínio\nome’. Por exemplo: 'contoso\mnorth'  

    -   'user@domain'. Por exemplo: 'mnorth@contoso.com'  

     O nome de usuário e a senha correspondente devem ser compatíveis com uma conta de usuário do Active Directory com permissões de Leitura e Registro no modelo de certificado do cliente Mac.  

     Exemplo: se o nome do servidor do ponto proxy do registro for **server02.contoso.com** e um nome de usuário **contoso\mnorth** tiver recebido permissões para o modelo de certificado do cliente Mac, digite o seguinte: **sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'**  

    > [!NOTE]  
    >  Se o nome de usuário contiver os caracteres **&lt;>"+=,**, o registro falhará. Para corrigir esse problema, obtenha um certificado fora de banda com um nome de usuário que não contenha esses caracteres.  
    >  
    >  Para uma experiência melhor do usuário, você pode e escrever as etapas e os comandos de instalação para que os usuários só precisem fornecer o nome de usuário a senha.  

5.  Aguarde até que você veja a mensagem **Registrado com êxito** .  

6.  Para limitar o certificado registrado ao Configuration Manager, no computador Mac, abra uma janela do terminal e faça as seguintes alterações:  

    a.  Digite o comando **sudo /Aplicativos/Utilitários/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  Na caixa de diálogo **Acesso ao Conjunto de Chaves**, na seção **Conjuntos de Chaves**, escolha **Sistema** e, na seção **Categoria**, escolha **Chaves**.  

    c.  Expanda as chaves para exibir os certificados do cliente. Quando você tiver identificado o certificado com uma chave privada recém-instalada, clique duas vezes na chave.  

    d.  Na guia **Controle de Acesso**, escolha **Confirmar antes de permitir acesso**.  

    e.  Navegue até **/Library/Application Support/Microsoft/CCM**, selecione **CCMClient** e escolha **Adicionar**.  

    f.  Escolha **Salvar Alterações** e feche a caixa de diálogo **Acesso ao Conjunto de Chaves**.  

7.  Reinicie o computador Mac.  

 Verifique se a instalação do cliente teve êxito abrindo o item **Configuration Manager** nas **Preferências do Sistema** no computador Mac. Você também pode atualizar e exibir a coleção **Todos os Sistemas** para confirmar se os computadores Mac agora aparecem nessa coleção como um cliente gerenciado.  

> [!TIP]  
>  Para ajudar a solucionar quaisquer problemas com o cliente Mac, você pode usar o programa CMDiagnostics incluído no pacote do cliente Mac OS X para coletar as seguintes informações de diagnóstico:  
>   
>  -   Uma lista de processos em execução  
> -   A versão do sistema operacional Mac OS X  
> -   Relatórios de falha do Mac OS X relacionados ao cliente do Configuration Manager, incluindo **CCM\*.crash** e **System Preference.crash**.  
> -   O arquivo da BOM (Lista de Materiais) e o arquivo da lista de propriedades (.plist) criados pela instalação do cliente do Configuration Manager.  
> -   O conteúdo da pasta /Library/Application Support/Microsoft/CCM/Logs.  
>   
>  As informações coletadas por CmDiagnostics são adicionadas a um arquivo zip que é salvo na área de trabalho do computador e que tem o nome cmdiag-*<nome do host\>***-***<data e hora\>*.zip.  

####  <a name="enroll-the-client-by-using-the-mac-computer-enrollment-wizard"></a>Registrar o cliente usando o Assistente de Registro de Computador Mac  

1.  Depois de concluir a instalação do cliente, o Assistente de Registro de Computador é aberto. Se o assistente não abrir, ou se você o fechar acidentalmente, clique em **Registrar** na página de preferências do **Configuration Manager** para abri-lo.  

2.  Na segunda página do assistente, especifique as seguintes informações:  

    -   **Nome de usuário** - O nome de usuário pode estar nos seguintes formatos:  

        -   'domínio\nome’. Por exemplo: 'contoso\mnorth'  

        -   'user@domain'. Por exemplo: 'mnorth@contoso.com'  

            > [!IMPORTANT]  
            >  Quando você usa um endereço de email para popular o campo **Nome de usuário**, o Configuration Manager usa automaticamente o nome de domínio do endereço de email e o nome padrão do servidor do ponto proxy do registro para popular o campo **Nome do servidor**. Se o nome de domínio e o nome do servidor não corresponderem ao nome do servidor do ponto proxy do registro, você deverá avisar aos usuários sobre o nome correto a usar, de modo que eles possam digitá-lo ao registrar seus computadores Mac.  

         O nome de usuário e a senha correspondente devem ser compatíveis com uma conta de usuário do Active Directory com permissões de Leitura e Registro no modelo de certificado do cliente Mac.  

    -   **Senha** – insira uma senha correspondente ao nome de usuário especificado.  

    -   **Nome do servidor** – insira o nome do servidor do ponto proxy do registro.  

3.  Clique em **Próximo** para continuar e, em seguida, conclua o assistente.  

## <a name="maintenance-tasks-for-mac-clients"></a>Tarefas de manutenção para clientes Mac

###  <a name="uninstalling-the-mac-client"></a>Desinstalando o cliente Mac  

1.  Em um computador Mac, abra uma janela do terminal e navegue até a pasta em que você extraiu o conteúdo do arquivo macclient.dmg baixado.  

2.  Navegue até a pasta Ferramentas e digite a seguinte linha de comando:  

     **./CMUninstall -c**  

    > [!NOTE]  
    >  A propriedade **-c** instrui a desinstalação do cliente a também remover os logs de falha do cliente e os arquivos de log. Isso é opcional, mas também é uma prática recomendada para ajudar a evitar confusão se você reinstalar o cliente posteriormente.  

3.  Se necessário, remova manualmente o certificado de autenticação de cliente que o Configuration Manager estava usando ou revogue-o. CMUnistall não remove nem revoga esse certificado.  

###  <a name="renewing-the-mac-client-certificate"></a>Renovando o certificado do cliente Mac  
 Use um dos seguintes métodos para renovar o certificado de cliente Mac:  

-   [Assistente de renovação de certificado](#renew-certificate-wizard)  

-   [Renovar o certificado manualmente](#renew-certificate-manually)  

####  <a name="renew-certificate-wizard"></a>Assistente de renovação de certificado  

1.  Configure os seguintes valores como *cadeias de caracteres* no arquivo ccmclient.plist que controla quando o Assistente de renovação de certificado é aberto:  

    -   **RenewalPeriod1** – especifica, em segundos, o primeiro período de renovação em que os usuários podem renovar o certificado. O valor padrão é 3.888.000 segundos (45 dias). Não configure nenhum valor menor que 300, uma vez que o período será revertido ao padrão. 


    -   **RenewalPeriod2** – especifica, em segundos, o segundo período de renovação em que os usuários podem renovar o certificado. O valor padrão é 259.200 segundos (3 dias). Se esse valor estiver configurado e for maior ou igual a 300 segundos e menor ou igual a **RenewalPeriod1**, o valor será usado. Se **RenewalPeriod1** for maior que 3 dias, um valor de 3 dias será usado para **RenewalPeriod2**.  Se **RenewalPeriod1** for menor que 3 dias, **RenewalPeriod2** será definido como o mesmo valor de **RenewalPeriod1**.  

    -   **RenewalReminderInterval1** – especifica, em segundos, a frequência em que o Assistente de Renovação de Certificado será exibido para os usuários durante o primeiro período de renovação. O valor padrão é 86.400 segundos (1 dia). Se **RenewalReminderInterval1** for maior que 300 segundos e menor que o valor configurado para **RenewalPeriod1**, então será usado o valor configurado. Caso contrário, será usado o valor padrão de 1 dia.  

    -   **RenewalReminderInterval2** – especifica, em segundos, a frequência em que o Assistente de Renovação de Certificado será exibido para os usuários durante o segundo período de renovação. O valor padrão é de 28.800 segundos (8 dias). Se **RenewalReminderInterval2** for maior que 300 segundos, menor ou igual a **RenewalReminderInterval1** e menor ou igual a **RenewalPeriod2**, o valor configurado será usado. Caso contrário, será usado um valor de 8 horas.  

     **Exemplo:** se os valores forem deixados como seus padrões, 45 dias antes do vencimento do certificado, o assistente será aberto a cada 24 horas.  No prazo de até 3 dias do vencimento do certificado, o assistente será aberto a cada 8 horas.  

     **Exemplo:** use a seguinte linha de comando, ou um script, para definir o primeiro período de renovação para 20 dias.  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2.  Quando o Assistente de renovação de certificado é aberto, os campos **Nome do usuário** e **Nome do servidor** serão, normalmente, populados previamente e o usuário só precisará inserir a senha para renovar o certificado.  

    > [!NOTE]  
    >  Se o assistente não abrir, ou se você o fechar acidentalmente, clique em **Renovar** na página de preferências do **Configuration Manager** para abri-lo.  

####  <a name="renewing-the-mac-client-certificate-manually"></a>Renovando o certificado do cliente Mac manualmente  
 Um período de validade típico para o certificado do cliente Mac é de 1 ano. O Configuration Manager não renova automaticamente o certificado do usuário solicitado durante o registro, por isso você precisa usar o procedimento a seguir para renovar o certificado manualmente.  

> [!IMPORTANT]  
>  Se o certificado expirar, você deverá desinstalar, reinstalar e registrar novamente o cliente Mac.  

 Este procedimento remove o SMSID, que é necessário para solicitar um novo certificado para o mesmo computador Mac. Quando você remove e substitui o SMSID do cliente, todo o histórico armazenado do cliente, como o inventário, é excluído depois que você excluir o cliente do console do Configuration Manager.  

1.  Crie e popule uma coleção de dispositivos para os computadores Mac que devem renovar os certificados de usuário.  

    > [!WARNING]  
    >  O Configuration Manager não monitora o período de validade do certificado registrado para computadores Mac. É necessário monitorá-lo independentemente do Configuration Manager para identificar os computadores Mac a serem adicionados a essa coleção.  

2.  No espaço de trabalho **Ativos e Conformidade** , inicie o **Assistente de Criação de Item de Configuração**.  

3.  Na página **Geral** do assistente, especifique as seguintes informações:  

    -   **Nome:remover SMSID para Mac**  

    -   **Tipo:Mac OS X**  

4.  Na página **Plataforma com suporte** do assistente, verifique se todas as versões do Mac OS X foram selecionadas.  

5.  Na página **Configurações** do assistente, escolha **Novo** e, na caixa de diálogo **Criar Configuração**, especifique as seguintes informações:  

    -   **Nome:remover SMSID para Mac**  

    -   **Tipo de configuração:script**  

    -   **Tipo de dados:cadeia de caracteres**  

6.  Na caixa de diálogo **Criar Configuração**, para **Script de descoberta**, escolha **Adicionar script** para especificar um script que descobre computadores Mac com um SMSID configurado.  

7.  Na caixa de diálogo **Editar Script de Descoberta** , insira o seguinte Script de Shell:  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Escolha **OK** para fechar a caixa de diálogo **Editar Script de Descoberta**.  

9. Na caixa de diálogo **Criar Configuração**, para **Script de correção (opcional)**, escolha **Adicionar script** para especificar um script que remove o SMSID quando ele é encontrado em computadores Mac.  

10. Na caixa de diálogo **Criar Script de Correção** , insira o seguinte Script de Shell:  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Escolha **OK** para fechar a caixa de diálogo **Criar Script de Correção**.  

12. Na página do assistente **Regras de Conformidade** , clique em **Novo**e na caixa de diálogo **Criar Regra** , especifique as seguintes informações:  

    -   **Nome:remover SMSID para Mac**  

    -   **Configuração selecionada:** escolha **Procurar** e selecione o script de descoberta especificado anteriormente.  

    -   Em **os seguintes valores** digite **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**.  

    -   Habilite a opção **Executar o script de correção especificado quando esta configuração não for compatível**.  

13. Conclua o Assistente de Criação de Item de Configuração.  

14. Crie uma linha de base de configuração que contenha o item de configuração que você acabou de criar e implante-a na coleção de dispositivos criada na etapa 1.  

     Para obter mais informações sobre como criar e implantar linhas de base de configuração, consulte [Como criar linhas de base de configuração no System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md) e [Como implantar linhas de base de configuração no System Center Configuration Manager](../../../compliance/deploy-use/deploy-configuration-baselines.md).  

15. Em computadores Mac com o SMSID removido, execute o seguinte comando para instalar um novo certificado:  

    ```  
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     Quando solicitado, digite a senha da conta do superusuário para executar o comando e a senha da conta de usuário do Active Directory.  

16. Para limitar o certificado registrado ao Configuration Manager, no computador Mac, abra uma janela do terminal e faça as seguintes alterações:  

    a.  Digite o comando **sudo /Aplicativos/Utilitários/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  No diálogo **Acesso ao Conjunto de Chaves**, na seção **Conjuntos de Chaves**, escolha **Sistema** e, na seção **Categoria**, escolha **Chaves**.  

    c.  Expanda as chaves para exibir os certificados do cliente. Quando você tiver identificado o certificado com uma chave privada recém-instalada, clique duas vezes na chave.  

    d.  Na guia **Controle de Acesso**, escolha **Confirmar antes de permitir acesso**.  

    e.  Navegue até **/Library/Application Support/Microsoft/CCM**, selecione **CCMClient** e escolha **Adicionar**.  

    f.  Escolha **Salvar Alterações** e feche a caixa de diálogo **Acesso ao Conjunto de Chaves**.  

17. Reinicie o computador Mac.  

##  <a name="use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager"></a>Usar uma solicitação de certificado e o método de instalação que é independente do Configuration Manager  
 Quando você não usa o registro do Configuration Manager, mas, em vez disso, solicita e instala o certificado do cliente independentemente do Configuration Manager, as etapas de configuração são um pouco diferentes

Comece executando *apenas* essas etapas:

a. [Implantar um certificado do servidor Web nos servidores do sistema de sites](#deploy-a-web-server-certificate-to-site-system-servers)

b. [Implantar um certificado de autenticação de cliente nos servidores do sistema de sites](#deploy-a-client-authentication-certificate-to-site-system-servers)

c. [Configurar o ponto de gerenciamento e o ponto de distribuição](#configure-the-management-point-and-distribution-point)

d. [Opcional: instalar o ponto do Reporting Services](#optional:-install-the-reporting-services-point)

e. [Baixar os arquivos de origem do cliente para Mac](#download-the-client-source-files-forMacs).  
  

#### <a name="to-install-the-client-certificate-independently-from-configuration-manager-and-install-the-client"></a>Para instalar o certificado do cliente independente do Configuration Manager e instalar o cliente  

1.  Para instalar o certificado do cliente independentemente do Configuration Manager, use as instruções que acompanham o método de implantação do certificado escolhido para solicitar e instalar o certificado do cliente em um computador Mac.  

2.  Navegue até a pasta onde você extraiu o conteúdo do arquivo macclient.dmg baixado do Centro de Download da Microsoft.  

3.  Digite a seguinte linha de comando: **sudo ./ccmsetup -MP <FQDN da Internet do ponto de gerenciamento\> -SubjectName <valor da entidade do certificado\>**.  O valor da entidade do certificado diferencia maiúsculas de minúsculas, por isso digite-o exatamente como ele aparece nos detalhes do certificado.  

     Exemplo: se o FQDN da Internet nas propriedades do sistema de sites for **server03.contoso.com** e o certificado do cliente Mac tiver o FQDN **mac12.contoso.com** como nome comum na entidade do certificado, digite: **sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com**  

4.  Aguarde até ver a mensagem **Instalação concluída** e reinicie o computador Mac.  

5.  Para verificar se esse certificado é acessível para o Configuration Manager, no computador Mac, abra uma janela do terminal e faça essas alterações:  

    a.  Digite o comando **sudo /Aplicativos/Utilitários/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  Na caixa de diálogo **Acesso ao Conjunto de Chaves**, na seção **Conjuntos de Chaves**, escolha **Sistema** e, na seção **Categoria**, escolha **Chaves**.  

    c.  Expanda as chaves para exibir os certificados do cliente. Quando você tiver identificado o certificado com uma chave privada recém-instalada, clique duas vezes na chave.  

    d.  Na guia **Controle de Acesso**, escolha **Confirmar antes de permitir acesso**.  

    e.  Navegue até **/Library/Application Support/Microsoft/CCM**, selecione **CCMClient** e escolha **Adicionar**.  

    f.  Escolha **Salvar Alterações** e feche a caixa de diálogo **Acesso ao Conjunto de Chaves**.  

6.  Se tiver mais de um certificado contendo o mesmo valor de entidade, especifique o número de série do certificado para identificar o certificado que deseja usar para o cliente do Configuration Manager. Para fazer isso, use o seguinte comando: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<número de série\>"**.  

     Por exemplo: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

 Verifique se a instalação do cliente teve êxito abrindo o item **Configuration Manager** nas **Preferências do Sistema** no Mac. Você também pode atualizar e exibir a coleção **Todos os Sistemas** para confirmar se o Mac agora aparece nessa coleção como um cliente gerenciado.  

### <a name="renewing-the-mac-client-certificate"></a>Renovando o certificado do cliente Mac  
 Use o procedimento a seguir antes de renovar o certificado do computador em computadores Mac.  

 Este procedimento remove o SMSID, que é necessário para que o cliente use um certificado novo ou renovado no computador Mac.  

> [!IMPORTANT]  
>  Quando você remove e substitui o SMSID do cliente, todo o histórico armazenado do cliente, como o inventário, é excluído depois que você excluir o cliente do console do Configuration Manager.  

#### <a name="to-renew-the-mac-client-certificate"></a>Para renovar o certificado do cliente Mac  

1.  Crie e popule uma coleção de dispositivos para os computadores Mac que devem renovar os certificados do computador.  

2.  No espaço de trabalho **Ativos e Conformidade** , inicie o **Assistente de Criação de Item de Configuração**.  

3.  Na página **Geral** do assistente, especifique as seguintes informações:  

    -   **Nome:remover SMSID para Mac**  

    -   **Tipo:Mac OS X**  

4.  Na página **Plataforma com suporte** do assistente, verifique se todas as versões do Mac OS X foram selecionadas.  

5.  Na página **Configurações** do assistente, clique em **Novo** e na caixa de diálogo **Criar Configuração** , especifique as seguintes informações:  

    -   **Nome:remover SMSID para Mac**  

    -   **Tipo de configuração:script**  

    -   **Tipo de dados:cadeia de caracteres**  

6.  Na caixa de diálogo **Criar Configuração** , para **Script de descoberta**, clique em **Adicionar script** para especificar um script que descobre computadores Mac com um SMSID configurado.  

7.  Na caixa de diálogo **Editar Script de Descoberta** , insira o seguinte Script de Shell:  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Escolha **OK** para fechar a caixa de diálogo **Editar Script de Descoberta**.  

9. Na caixa de diálogo **Criar Configuração**, para **Script de correção (opcional)**, escolha **Adicionar script** para especificar um script que remove o SMSID quando ele é encontrado em computadores Mac.  

10. Na caixa de diálogo **Criar Script de Correção** , insira o seguinte Script de Shell:  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Escolha **OK** para fechar a caixa de diálogo **Criar Script de Correção**.  

12. Na página do assistente **Regras de Conformidade**, escolha **Novo** e, na caixa de diálogo **Criar Regra**, especifique as seguintes informações:  

    -   **Nome:remover SMSID para Mac**  

    -   **Configuração selecionada:** escolha **Procurar** e selecione o script de descoberta especificado anteriormente.  

    -   Em **os seguintes valores** digite **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**.  

    -   Habilite a opção **Executar o script de correção especificado quando esta configuração não for compatível**.  

13. Conclua o Assistente de Criação de Item de Configuração.  

14. Crie uma linha de base de configuração que contenha o item de configuração criado recentemente e implante-a na coleção de dispositivos criada na etapa 1.  

     Para obter mais informações sobre como criar e implantar linhas de base de configuração, consulte [Como criar linhas de base de configuração no System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md).  

15. Após instalar um novo certificado em computadores Mac que tiveram o SMSID removido, execute o comando a seguir para configurar o cliente para usar o novo certificado:  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <Subject_Name_of_New_Certificate>  
    ```  

16. Se tiver mais de um certificado contendo o mesmo valor de entidade, especifique o número de série do certificado para identificar o certificado que deseja usar para o cliente do Configuration Manager. Para fazer isso, use o seguinte comando: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<número de série\>"**.  

     Por exemplo: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

17. Reinicie o Mac.  


<!--HONumber=Dec16_HO3-->


