---
title: Implantar clientes do Mac
titleSuffix: Configuration Manager
description: Saiba como implantar clientes em computadores Mac no Configuration Manager.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e686f9cdbece2ceb652ecd2e0f3c6d5eca420caf
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67677828"
---
# <a name="how-to-deploy-clients-to-macs"></a>Como implantar clientes em Mac

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo descreve como implantar e manter o cliente do Configuration Manager em computadores Mac. Para saber mais sobre o que você precisa configurar antes de implantar clientes em computadores Mac, consulte [Preparar para implantar o software cliente em Macs](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients).

Quando instala um novo cliente para computadores Mac, talvez você também precise instalar atualizações do Configuration Manager para refletir as novas informações de cliente no console do Configuration Manager.

Nesses procedimentos, há duas opções para instalar certificados de cliente. Leia mais sobre os certificados de cliente para Macs no [Preparar para implantar o software cliente em Macs](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#certificate-requirements).  

- Usar o registro do Configuration Manager usando a [ferramenta CMEnroll](#bkmk_enroll). O processo de registro não dá suporte para a renovação automática de certificados. Registre novamente o computador Mac antes que o certificado instalado expire.    

- [Usar um método de solicitação e de instalação de certificado independente do Configuration Manager](#bkmk_external).  

> [!IMPORTANT]  
> Para implantar o cliente em dispositivos que executam o macOS Sierra, configure corretamente o **Nome da entidade** do certificado do ponto de gerenciamento. Por exemplo, use o FQDN do servidor do ponto de gerenciamento.



## <a name="configure-client-settings"></a>Definir as configurações do cliente  

Use as [configurações padrão do cliente](/sccm/core/clients/deploy/about-client-settings) para configurar o registro de computadores Mac. Não é possível usar configurações personalizadas do cliente. Para solicitar e instalar o certificado, o cliente do Configuration Manager para Mac requer as configurações padrão do cliente.  

1. No console do Configuration Manager, acesse o workspace **Administração**. Selecione o nó **Configurações do Cliente** e, em seguida, selecione **Configurações do Cliente Padrão**.  

2. Na guia **Página Inicial** da faixa de opções, no grupo **Propriedades**, escolha **Propriedades**.  

3. Selecione a seção **Registro** e defina as seguintes configurações a seguir:  

    1. **Permitir que os usuários registrem dispositivos móveis e computadores Mac**: **Sim**  

    2. **Perfil de registro:** Escolha **Definir Perfil**.  

4. Na caixa de diálogo **Perfil de Registro do Dispositivo Móvel** escolha **Criar**.  

5. Na caixa de diálogo **Criar Perfil de Registro**, insira um nome para esse perfil de registro. Em seguida, configure o **Código do site de gerenciamento**. Selecione o site primário do Configuration Manager que contém os pontos de gerenciamento para esses computadores Mac.  

    > [!NOTE]  
    >  Caso não consiga selecionar o site, verifique se você configurou pelo menos um ponto de gerenciamento no site para dar suporte a dispositivos móveis.  

6. Escolha **Adicionar**.  

7. Na janela **Adicionar Autoridade de Certificação para Dispositivos Móveis**, selecione o servidor da autoridade de certificação que emite certificados para computadores Mac.  

8. Na caixa de diálogo **Criar Perfil de Registro**, selecione o modelo de certificado do computador Mac que você criou anteriormente.  

9. Selecione **OK** para fechar a caixa de diálogo **Perfil de Registro** e a caixa de diálogo **Configurações do Cliente Padrão**.  

    > [!TIP]  
    > Se desejar alterar o intervalo da política do cliente use o **Intervalo de sondagem da política do cliente** no grupo de configuração do cliente **Política do Cliente**.  

Na próxima vez que os dispositivos baixam a política do cliente, o Configuration Manager aplica essas configurações para todos os usuários. Para iniciar a recuperação de política para um cliente individual, confira [Iniciar a recuperação de política para um cliente do Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  

Além das configurações do cliente de registro, verifique se você definiu as seguintes configurações do dispositivo do cliente:  

- **Inventário de hardware**: Habilite e defina este recurso se você desejar coletar inventário de hardware dos computadores cliente Mac e Windows. Para obter informações, confira [Como estender o inventário de hardware](/sccm/core/clients/manage/inventory/extend-hardware-inventory).  

- **Configurações de conformidade**: Habilite e configure este recurso se desejar avaliar e corrigir configurações em computadores cliente Mac e Windows. Para obter mais informações, consulte [Planejar e definir configurações de conformidade](/sccm/compliance/plan-design/plan-for-and-configure-compliance-settings).  

Para obter mais informações, consulte [Como definir as configurações de cliente](/sccm/core/clients/deploy/configure-client-settings).  



## <a name="bkmk_download"></a> Baixe o cliente Mac  

1. Baixe o pacote de arquivo do cliente Mac OS X do [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=47719). Salve **ConfigmgrMacClient.msi** para um computador que execute o Windows. Esse arquivo não é fornecido na mídia de instalação do Configuration Manager.  

2. Execute o instalador no computador Windows. Extraia o pacote do cliente Mac, **Macclient.dmg**, para uma pasta no disco local. O caminho padrão é `C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client`.  

3. Copie o arquivo **Macclient.dmg** para uma pasta no computador Mac.  

4. No computador Mac, execute **Macclient.dmg** para extrair os arquivos para uma pasta no disco local.  

5. Na pasta, verifique se ele contém os seguintes arquivos: 

    - **Ccmsetup**: Instala o cliente do Configuration Manager nos seus computadores Mac usando **CMClient.pkg**  

    - **CMDiagnostics**: Coleta informações de diagnóstico relacionadas ao cliente do Configuration Manager em seus computadores Mac  

    - **CMUninstall**: Desinstala o cliente de seus computadores Mac  

    - **CMAppUtil**: Converte pacotes de aplicativos da Apple em um formato que possa ser implantado como um aplicativo do Configuration Manager  

    - **CMEnroll**: Solicita e instala o certificado do cliente em um computador Mac para que você possa instalar o cliente do Configuration Manager  



## <a name="bkmk_enroll"></a> Registrar o cliente Mac  

Registre clientes individuais com o [Assistente de registro de computador Mac](#enroll-the-client-with-the-mac-computer-enrollment-wizard).

Para automatizar o registro para muitos clientes, use a [Ferramenta CMEnroll](#client-and-certificate-automation-with-cmenroll).   


### <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>Registrar o cliente com o assistente de registro de computador Mac  

1. Depois de instalar do cliente, o assistente de registro de computador é aberto. Para iniciar manualmente o assistente, selecione **Registrar** da página de preferências do **Configuration Manager**.  

2. Na segunda página do assistente, forneça as seguintes informações:  

   - **Nome de usuário**: O nome de usuário pode estar nos seguintes formatos:  

     - `domain\name`. Por exemplo: `contoso\mnorth`  

     - `user@domain`. Por exemplo: `mnorth@contoso.com`  

         > [!IMPORTANT]  
         >  Quando você usa um endereço de email para popular o campo **Nome de usuário**, o Configuration Manager popula automaticamente o campo **Nome do servidor**. Ele usa o nome padrão do servidor de ponto proxy do registro e o nome de domínio do endereço de email. Se esses nomes não corresponderem ao nome do servidor do ponto proxy do registro, corrija o **Nome do servidor** durante o registro.  

       O nome de usuário e a senha correspondente devem corresponder a uma conta de usuário do Active Directory que tenha permissões de **Leitura** e **Registro** no modelo de certificado do cliente Mac.  

   - **Nome do servidor**: O nome do servidor do ponto proxy do registro.  


### <a name="client-and-certificate-automation-with-cmenroll"></a>Automação de cliente e certificado com o CMEnroll  

Use este procedimento para automação da instalação do cliente e solicitação de registro de certificados de cliente com a ferramenta CMEnroll. Para executar a ferramenta, você precisa ter uma conta de usuário do Active Directory.

1. No computador Mac, navegue até a pasta em que você extraiu o conteúdo do arquivo **Macclient.dmg**.  

2. Insira o seguinte comando: `sudo ./ccmsetup`  

3. Aguarde até que você veja a mensagem **Instalação concluída** . Embora o instalador exiba uma mensagem para que você reinicie agora, não reinicie e passe para a etapa seguinte.  

4. Na pasta **Ferramentas** no computador Mac, digite o seguinte comando: `sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u '<user_name>'`  

    Após a instalação do cliente, o assistente de Registro de Computador Mac é aberto para ajudá-lo a registrar o computador Mac. Para obter mais informações, confira [Registrar o cliente usando o Assistente de registro de computador Mac](#bkmk_enroll).  

     Exemplo: Se o nome do servidor do ponto proxy do registro for **server02.contoso.com** e você conceder permissões **contoso\mnorth** para o modelo de certificado do cliente Mac, digite o seguinte comando: `sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'`  

    > [!NOTE]  
    > Se o nome de usuário incluir qualquer um dos seguintes caracteres, o registro falhará: `<>"+=,`. Use um certificado fora de banda com um nome de usuário que não inclua esses caracteres.  
    >  
    > Para uma experiência de usuário perfeita, planeje as etapas de instalação. Assim, os usuários só precisam fornecer seu nome de usuário e senha.  

5. Digite a senha para a conta de usuário do Active Directory. Quando você inserir esse comando, ele solicitará as duas senhas. A primeira senha é para a conta de superusuário executar o comando. O segundo prompt destina-se à conta de usuário do Active Directory. Os prompts parecem idênticos, portanto certifique-se de especificá-los na sequência correta.  

6. Aguarde até que você veja a mensagem **Registrado com êxito** .  

7. Para limitar o certificado registrado ao Configuration Manager, no computador Mac, abra uma janela do terminal e faça as seguintes alterações:  

    1. Digite o comando `sudo /Applications/Utilities/Keychain Access.app/Contents/MacOS/Keychain Access`  

    2. Na janela **Acesso de Conjunto de Chaves** na seção **Conjuntos de chaves**, escolha **Sistema**. Em seguida, na seção **Categoria**, escolha **Chaves**.  

    3. Expanda as chaves para exibir os certificados do cliente. Localize o certificado com uma chave privada que você instalou e abra essa chave.  

    4. Na guia **Controle de Acesso**, escolha **Confirmar antes de permitir acesso**.  

    5. Navegue até **/Library/Application Support/Microsoft/CCM**, selecione **CCMClient** e escolha **Adicionar**.  

    6. Escolha **Salvar Alterações** e feche a caixa de diálogo **Acesso ao Conjunto de Chaves**.  

8. Reinicie o computador Mac.  

Para verificar se a instalação do cliente teve êxito, abra o item **Configuration Manager** nas **Preferências do Sistema** no computador Mac. Também atualize e exiba a coleção **Todos os Sistemas** no console do Configuration Manager. Confirme que o computador Mac aparece nessa coleção como um cliente gerenciado.  

> [!TIP]  
> Para ajudar a solucionar problemas de cliente Mac, use a ferramenta **CMDiagnostics** incluída com o pacote do cliente Mac. Use-a para coletar as seguintes informações de diagnóstico:  
>   
> - Uma lista de processos em execução  
> - A versão do sistema operacional Mac OS X  
> - Relatórios de falha do Mac OS X relacionados ao cliente do Configuration Manager, incluindo **CCM\*.crash** e **System Preference.crash**.  
> - O arquivo da BOM (Lista de Materiais) e o arquivo da lista de propriedades (.plist) criados pela instalação do cliente do Configuration Manager.  
> - O conteúdo da pasta **/Library/Application Support/Microsoft/CCM/Logs**.  
>   
> As informações coletadas pelo CmDiagnostics são adicionadas a um arquivo zip que é salvo na área de trabalho do computador e tem o nome de `cmdiag-<hostname>-<datetime>.zip`



## <a name="bkmk_external"></a> Gerenciar certificados externos ao Configuration Manager

Você pode usar um método de solicitação e de instalação de certificado independente do Configuration Manager. Use o mesmo processo geral, mas inclua as seguintes etapas adicionais: 

- Quando você instala o cliente do Configuration Manager, use as opções **MP** e **SubjectName** da linha de comando. Insira o seguinte comando: `sudo ./ccmsetup -MP <management point internet FQDN> -SubjectName <certificate subject name>`. O nome da entidade do certificado diferencia maiúsculas de minúsculas, por isso digite-o exatamente como ele aparece nos detalhes do certificado.  

     Exemplo: O FQDN de Internet do ponto de gerenciamento é **server03.contoso.com**. O certificado do cliente Mac tem o FQDN **mac12.contoso.com** como nome comum na entidade do certificado. Use o seguinte comando: `sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com`  

- Se tiver mais de um certificado contendo o mesmo valor de entidade, especifique o número de série do certificado a usar para o cliente do Configuration Manager. Use o seguinte comando: `sudo defaults write com.microsoft.ccmclient SerialNumber -data "<serial number>"`.  

     Por exemplo: `sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"`  



## <a name="renew-the-mac-client-certificate"></a>Renovar o certificado do cliente Mac  

Este procedimento remove o SMSID. O cliente do Configuration Manager para Mac requer uma nova ID para usar um certificado novo ou renovado.  

> [!IMPORTANT]  
> Após substituir o SMSID do cliente e excluir o recurso antigo do console do Configuration Manager, você também exclui todo o histórico armazenado do cliente. Por exemplo, o histórico de inventário de hardware desse cliente.  


1. Crie e popule uma coleção de dispositivos para os computadores Mac que devem renovar os certificados do computador.  

2. No workspace **Ativos e Conformidade**, inicie o **Assistente de Criação de Item de Configuração**.  

3. Na página **Geral** do assistente, especifique as seguintes informações:  

    - **Nome**: **Remover SMSID para Mac**  

    - **Tipo**: **Mac OS X**  

4. Na página **Plataformas com Suporte**, selecione todas as versões do Mac OS X.  

5. Na página **Configurações**, selecione **Nova**. Na janela **Criar Configuração**, especifique as seguintes informações:  

    - **Nome**: **Remover SMSID para Mac**  

    - **Tipo de configuração**: **script**  

    - **Tipo de dados**: **Cadeia de caracteres**  

6. Na janela **Criar Configuração**, para **Script de descoberta**, selecione **Adicionar script**. Essa ação especifica um script para descobrir computadores Mac configurados com um SMSID.  

7. Na janela **Editar Script de Descoberta**, insira o seguinte script de shell:  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8. Escolha **OK** para fechar a janela **Editar Script de Descoberta**.  

9. Na janela **Criar Configuração**, para **Script de correção (opcional)** , escolha **Adicionar script**. Essa ação especifica um script para remover o SMSID quando ele é encontrado em computadores Mac.  

10. Na janela **Criar Script de Correção**, insira o seguinte script de shell:  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Escolha **OK** para fechar a janela **Criar Script de Correção**.  

12. Na página **Regras de Conformidade**, escolha **Nova**. Na janela **Criar Regra**, especifique as seguintes informações:  

    - **Nome**: **Remover SMSID para Mac**  

    - **Configuração selecionada**: Escolha **Procurar** e, em seguida, selecione o script de descoberta que você especificou anteriormente.  

    - No campo **os seguintes valores**: **O par domínio/padrão (com.microsoft.ccmclient, SMSID) não existe**.  

    - Habilite a opção **Executar o script de correção especificado quando esta configuração não está em conformidade**.  

13. Conclua o assistente.  

14. Crie uma linha de base de configuração que contenha este item de configuração. Implante a linha de base na coleção de destino.  

     Para obter mais informações, confira [Como criar linhas de base de configuração](/sccm/compliance/deploy-use/create-configuration-baselines).  

15. Após instalar um novo certificado em computadores Mac cujo SMSID foi removido, execute o comando a seguir para configurar o cliente para usar o novo certificado:  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <subject_name_of_new_certificate>  
    ```  



## <a name="see-also"></a>Consulte também

[Planejar a implantação de cliente em computadores Mac](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients)

[Manter os clientes Mac](/sccm/core/clients/manage/maintain-mac-clients)
