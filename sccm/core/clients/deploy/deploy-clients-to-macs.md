---
title: Implantar clientes do Mac
titleSuffix: Configuration Manager
description: Saiba como implantar clientes em computadores Mac no System Center Configuration Manager.
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: aaroncz
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
caps.latest.revision: "12"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 1b7f20a48e0e7219d933c367fb9f0315fc287dfd
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="how-to-deploy-clients-to-macs"></a>How to deploy clients to Macs

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico descreve como implantar e manter o cliente do Configuration Manager em computadores Mac. Para saber mais sobre o que você precisa configurar antes de implantar clientes em computadores Mac, consulte [Preparar para implantar o software cliente em Macs](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients).

Quando instala um novo cliente para computadores Mac, talvez você também precise instalar atualizações do Configuration Manager para refletir as novas informações de cliente no console do Configuration Manager.

Nesses procedimentos, há duas opções para instalar certificados de cliente. Leia mais sobre os certificados de cliente para Macs no [Preparar para implantar o software cliente em Macs](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#certificate-requirements).  

-   Usar o registro do Configuration Manager usando a [ferramenta CMEnroll](#install-the-client-and-then-enroll-the-client-certificate-on-the-mac). O processo de registro não oferece suporte à renovação automática de certificados, portanto, é necessário registrar novamente os computadores Mac antes de o certificado instalado expirar.    

-   [Usar um método de solicitação e de instalação de certificado independente do Configuration Manager](#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager). 

>[!IMPORTANT]
>  Para implantar o cliente em dispositivos com macOS Sierra, o nome da entidade do certificado do ponto de gerenciamento deve estar configurado corretamente, por exemplo, usando o FQDN do servidor de ponto de gerenciamento.


## <a name="configure-client-settings-for-enrollment"></a>Defina as configurações do cliente para o registro  
 É necessário usar as [configurações de cliente padrão](../../../core/clients/deploy/about-client-settings.md) para configurar o registro para computadores Mac; não é possível usar configurações de cliente personalizadas.  

 Isso é necessário para que o Configuration Manager solicite e instale o certificado no Mac.  

### <a name="to-configure-the-default-client-settings-for-configuration-manager-to-enroll-certificates-for-macs"></a>Para definir as configurações de cliente padrão para o Configuration Manager registrar certificados para Mac  

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
    >  Se desejar alterar o intervalo da política do cliente use o **Intervalo de sondagem da política do cliente** no grupo de configuração do cliente **Política do Cliente**.  

 Todos os usuários serão configurados com essas definições na próxima vez que baixarem a política do cliente. Para iniciar a recuperação de política para um cliente individual, consulte [Iniciar a recuperação de política para um cliente do Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  

 Além das configurações do cliente de registro, verifique se você definiu as seguintes configurações do dispositivo do cliente:  

-   **Inventário de hardware**: habilite e configure isso se desejar coletar inventário de hardware dos computadores cliente Mac e Windows. Para obter mais informações, consulte [Como estender o inventário de hardware no System Center Configuration Manager](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

-   **Configurações de conformidade**: habilite e configure isso se desejar avaliar e corrigir configurações em computadores cliente Mac e Windows. Para obter mais informações, consulte [Planejar e definir configurações de conformidade](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

> [!NOTE]  
>  Para obter mais informações sobre as configurações do cliente do Configuration Manager, consulte [Como definir as configurações do cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).  

## <a name="download-the-client-source-files-for-macs"></a>Baixar os arquivos de origem do cliente para Mac  

1.  Baixe o pacote de arquivos do cliente Mac OS X, **ConfigmgrMacClient.msi**e salve-o em um computador que executa o Windows.  

     Esse arquivo não é fornecido na mídia de instalação do Configuration Manager. Você pode baixar o arquivo do [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

2.  No computador Windows, execute **ConfigmgrMacClient.msi** para extrair o pacote Macclient.dmg do cliente Mac para uma pasta no disco local (por padrão **C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client\\**).  

3.  Copie o arquivo Macclient.dmg para uma pasta no computador Mac.  

4.  No computador Mac, execute o arquivo Macclient.dmg para extrair os arquivos para uma pasta no disco local.  

5.  Na pasta, verifique se os arquivos Ccmsetup e CMClient.pkg foram extraídos e se uma pasta chamada Ferramentas foi criada e contém as ferramentas CMDiagnostics, CMUninstall, CMAppUtil e CMEnroll.

    -  **Ccmsetup**: instala o cliente do Configuration Manager nos seus computadores Mac.  

    -   **CMDiagnostics**: coleta informações de diagnóstico relacionadas ao cliente do Configuration Manager em seus computadores Mac.  

    -   **CMUninstall**: desinstala o cliente de seus computadores Mac.  

    -   **CMAppUtil**: converte pacotes de aplicativos da Apple em um formato que possa ser implantado como um aplicativo do Configuration Manager.  

    -   **CMEnroll**: solicita e instala o certificado do cliente em um computador Mac para que você possa instalar o cliente do Configuration Manager.   

## <a name="install-the-client-and-then-enroll-the-client-certificate-on-the-mac"></a>Instalar o cliente e registrar o certificado do cliente no computador Mac  

É possível registrar clientes individuais com o [Assistente de Registro de Computador Mac](#enroll-the-client-with-the-mac-computer-enrollment-wizard).

Para uma automação que habilita o registro de muitos clientes, use a [ferramenta CMEnroll](#client-and-certificate-automation-with-cmenroll).   


###  <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>Registrar o cliente com o Assistente de Registro de Computador Mac  

1.  Depois de concluir a instalação do cliente, o Assistente de Registro de Computador é aberto. Se o assistente não abrir ou se você fechá-lo acidentalmente, clique em **Registrar** na página de preferências do **Configuration Manager** para abri-lo.  

2.  Na segunda página do assistente, forneça:  

    -   **Nome de usuário** - O nome de usuário pode estar nos seguintes formatos:  

        -   'domínio\nome’. Por exemplo: 'contoso\mnorth'  

        -   'user@domain'. Por exemplo: 'mnorth@contoso.com'  

            > [!IMPORTANT]  
            >  Quando você usa um endereço de email para popular o campo **Nome de usuário**, o Configuration Manager usa automaticamente o nome de domínio do endereço de email e o nome padrão do servidor do ponto proxy do registro para popular o campo **Nome do servidor**. Se o nome de domínio e o nome do servidor não corresponderem ao nome do servidor do ponto proxy do registro, diga aos usuários o nome correto a ser usado ao registrar seus computadores Mac.  

         O nome de usuário e a senha correspondente devem ser compatíveis com uma conta de usuário do Active Directory com permissões de Leitura e Registro no modelo de certificado do cliente Mac.  

    -   **Senha** – insira uma senha correspondente ao nome de usuário especificado.  

    -   **Nome do servidor** – insira o nome do servidor do ponto proxy do registro.  


### <a name="client-and-certificate-automation-with-cmenroll"></a>Automação de cliente e certificado com o CMEnroll  

Use este procedimento para automação da instalação do cliente e solicitação de registro de certificados de cliente com a ferramenta CMEnroll. Para executar a ferramenta você precisa ter uma conta de usuário do Active Directory.

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
    >  Se o nome de usuário contiver os caracteres **&lt;>"+=,** o registro falhará. Obtenha um certificado fora de banda com um nome de usuário que não contenha esses caracteres.  
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
>  Para ajudar a solucionar problemas do cliente Mac, você pode usar o programa CMDiagnostics incluído no pacote do cliente Mac OS X para coletar as seguintes informações de diagnóstico:  
>   
>  -   Uma lista de processos em execução  
> -   A versão do sistema operacional Mac OS X  
> -   Relatórios de falha do Mac OS X relacionados ao cliente do Configuration Manager, incluindo **CCM\*.crash** e **System Preference.crash**.  
> -   O arquivo da BOM (Lista de Materiais) e o arquivo da lista de propriedades (.plist) criados pela instalação do cliente do Configuration Manager.  
> -   O conteúdo da pasta /Library/Application Support/Microsoft/CCM/Logs.  
>   
>  As informações coletadas por CmDiagnostics são adicionadas a um arquivo zip, que é salvo na área de trabalho do computador e que tem o nome cmdiag-*<nome do host\>***-***&gt;data e hora\>*.zip.***


##  <a name="use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager"></a>Usar uma solicitação de certificado e o método de instalação que é independente do Configuration Manager  

Primeiro, execute estas tarefas específicas de [Preparar para implantar o software cliente em Macs](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients):

1. [Implantar um certificado do servidor Web nos servidores do sistema de sites](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#deploy-a-web-server-certificate-to-site-system-servers)

2. [Implantar um certificado de autenticação de cliente nos servidores do sistema de sites](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#deploy-a-client-authentication-certificate-to-site-system-servers)

3. [Configurar o ponto de gerenciamento e o ponto de distribuição](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#configure-the-management-point-and-distribution-point)

4. [Opcional: instalar o ponto do Reporting Services](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#install-the-reporting-services-point)

Em seguida, execute estas tarefas:

5. [Baixar os arquivos de origem do cliente para Mac](#download-the-client-source-files-for-macs).  
6. Use as instruções que acompanham o método de implantação do certificado escolhido para solicitar e instalar o certificado do cliente em um computador Mac.  
7.  Navegue até a pasta onde você extraiu o conteúdo do arquivo macclient.dmg baixado do Centro de Download da Microsoft.  

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

## <a name="renewing-the-mac-client-certificate"></a>Renovando o certificado do cliente Mac  
 Use o procedimento a seguir antes de renovar o certificado do computador em computadores Mac.  

 Este procedimento remove o SMSID, que é necessário para que o cliente use um certificado novo ou renovado no computador Mac.  

> [!IMPORTANT]  
>  Quando você remove e substitui o SMSID do cliente, todo o histórico armazenado do cliente, como o inventário, é excluído depois que você excluir o cliente do console do Configuration Manager.  

### <a name="to-renew-the-mac-client-certificate"></a>Para renovar o certificado do cliente Mac  

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

    -   Em **os seguintes valores** digite **O par domínio/padrão (com.microsoft.ccmclient, SMSID) não existe**.  

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

17. Reiniciar.  


## <a name="see-also"></a>Consulte também

[Manter os clientes Mac](/sccm/core/clients/manage/maintain-mac-clients)
