---

title: Registro de dispositivos em massa | Microsoft Docs | MDM Local
description: "Registre dispositivos em massa de maneira automatizada com o Gerenciamento de Dispositivo Móvel local no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b36f5e4a-2b57-4d18-83f6-197081ac2a0a
caps.latest.revision: 13
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0d6479bcc134103e6005159a8ea295a5f359a436
ms.openlocfilehash: ef68a9f998ea6ff9628e01f6ac622711de68375d


---
# <a name="how-to-bulk-enroll-devices-with-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Como registrar dispositivos em massa com o Gerenciamento de Dispositivo Móvel local no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


O registro em massa no Gerenciamento de Dispositivo Móvel Local do System Center Configuration Manager é uma maneira mais automatizada para registrar dispositivos, quando comparado ao registro de usuário, que exige que os usuários insiram suas credenciais para registrar o dispositivo.  O registro em massa usa um pacote de registro para autenticar o dispositivo durante o registro. O pacote (um arquivo .ppkg) contém um perfil de certificado e, opcionalmente, um perfil de Wi-Fi, caso o dispositivo precise de conectividade de intranet para dar suporte ao registro.  

 > [!NOTE]  
>  O branch atual do Configuration Manager dá suporte ao registro no Gerenciamento de Dispositivo Móvel Local para dispositivos que executam os seguintes sistemas operacionais:  
>   
>  -   Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team \(a partir do Configuration Manager versão 1602\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise

As seguintes tarefas explicam como registrar computadores e dispositivos em massa para o Gerenciamento de Dispositivo Móvel Local:  

-   [Criar um perfil de certificado](#bkmk_createCert)  

-   [Criar um perfil de Wi-Fi](#CreateWifi)  

-   [Criar um perfil de registro](#bkmk_createEnroll)  

-   [Criar um arquivo (ppkg) de pacote de registro](#bkmk_createPpkg)  

-   [Usar o pacote para registrar um dispositivo em massa](#bkmk_getPpkg)  

-   [Verificar o registro do dispositivo](#bkmk_verifyEnroll)  

##  <a name="a-namebkmkcreatecerta-create-a-certificate-profile"></a><a name="bkmk_createCert"></a> Criar um perfil de certificado  
 O principal componente do pacote de registro é um perfil de certificado, que é usado para provisionar automaticamente um certificado raiz confiável no dispositivo que está sendo registrado.  Este certificado raiz é necessário para a comunicação confiável entre os dispositivos e as funções do sistema de sites necessários para o Gerenciamento de Dispositivo Móvel Local. Sem o certificado raiz, o dispositivo não seria confiável em conexões HTTPS entre ele e os servidores que hospedam o ponto de registro, o ponto proxy do registro, o ponto de distribuição e as funções do sistema de sites do ponto de gerenciamento de dispositivos.  

 Como parte da preparação do sistema para o Gerenciamento de Dispositivo Móvel Local, você exporta um certificado raiz que pode ser usado no perfil de certificado do pacote de registro. Para obter instruções sobre como obter o certificado raiz confiável, consulte [Exportar o certificado com a mesma raiz do certificado do servidor Web](../../mdm/get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert).  

 Use o certificado raiz exportado para criar um perfil de certificado. Para obter instruções, consulte [How to create certificate profiles in System Center Configuration Manager (Como criar perfis de certificado no System Center Configuration Manager)](../../protect/deploy-use/create-certificate-profiles.md).  

##  <a name="a-namecreatewifia-create-a-wi-fi-profile"></a><a name="CreateWifi"></a> Criar um perfil de Wi-Fi  
 O outro componente do pacote usado para o registro em massa é um perfil de Wi-Fi. Alguns dispositivos podem não ter a conectividade de rede necessária para dar suporte ao registro até que as configurações de rede sejam provisionadas. Incluir um perfil de Wi-Fi no pacote de registro fornece um meio para estabelecer a conectividade de rede para o dispositivo.  

 Para criar um perfil de Wi-Fi no Configuration Manager, siga as instruções descritas em [How to create Wi-Fi profiles in System Center Configuration Manager (Como criar perfis de Wi-Fi no System Center Configuration Manager)](../../protect/deploy-use/create-wifi-profiles.md).  

> [!IMPORTANT]  
>Tenha os dois problemas a seguir em mente ao criar um perfil de Wi-Fi para registro em massa:
>
> - O branch atual do Configuration Manager só dá suporte às seguintes configurações de segurança Wi-Fi para o Gerenciamento de Dispositivo Móvel Local:  
>   
>   - Tipos de segurança: **WPA2 Enterprise** ou **WPA2 Personal**  
>   - Tipos de criptografia: **AES** ou **TKIP**  
>   - Tipos de EAP: **Cartão Inteligente ou outro certificado** ou **PEAP**  
>
>
> - Embora o Configuration Manager tenha uma configuração de informações do servidor proxy no perfil de Wi-Fi, ele não configura o proxy quando o dispositivo é registrado. Se você precisar configurar um servidor proxy com seus dispositivos registrados, será possível implantar as configurações usando os itens de configuração quando dispositivos forem registrados ou criar o segundo pacote usando a Windows ICD (Designer de Configuração e Imagens) para implantar junto com o pacote de registro em massa.

##  <a name="a-namebkmkcreateenrolla-create-an-enrollment-profile"></a><a name="bkmk_createEnroll"></a> Criar um perfil de registro  
 O perfil de registro permite especificar as configurações necessárias para o registro de dispositivo, incluindo um perfil de certificado que provisionará dinamicamente um certificado raiz confiável no dispositivo e um perfil de Wi-Fi que provisionará as configurações de rede, se necessário.  

 Antes de criar um perfil de registro, verifique se você tem um perfil de certificado e um perfil de Wi-Fi (se necessário) criado. Para obter mais informações, consulte [Criar um perfil de certificado](#bkmk_createCert) e [Criar um perfil de Wi-Fi](#CreateWifi).  

#### <a name="to-create-an-enrollment-profile"></a>Para criar um perfil de registro:  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** >**Visão Geral** >**Todos os Dispositivos Corporativos** >**Windows** >**Perfis de Registro**.  

2.  Clique com o botão direito do mouse em **Perfil de Registro** e clique em **Criar Perfil**.  

3.  No assistente de Criação de Perfil de Registro, insira um nome para o perfil, certifique-se de que **Local** está marcado para **Autoridade de Gerenciamento**e clique em **Avançar**.  

4.  Selecione o código do site e clique em **Avançar**.  

5.  Selecione **Somente Intranet**, selecione os pontos proxy do registro que o dispositivo usará, inicie o processo de registro e clique em **Avançar**.  

6.  Selecione o perfil de certificado que contém o certificado raiz confiável (este é o perfil que você criou em [Create a certificate profile](#bkmk_createCert)) e clique em **Avançar**.  

7.  Selecione o perfil de W-Fi que contém as configurações de rede necessárias para os dispositivos se conectarem à intranet (este é o perfil que você criou em [Create a Wi-Fi profile](#CreateWifi)) e clique em **Avançar**.  

    > [!NOTE]  
    >  Se não estiver usando um perfil de Wi-Fi para o pacote de registro, ignore essa etapa.  

8.  Confirme as configurações do perfil de registro e clique em **Avançar**. Clique em **Fechar** para sair do assistente.  

##  <a name="a-namebkmkcreateppkga-create-an-enrollment-package-ppkg-file"></a><a name="bkmk_createPpkg"></a> Criar um arquivo (ppkg) de pacote de registro  
 O pacote de registro é o arquivo usado para registrar dispositivos em massa para o Gerenciamento de Dispositivo Móvel Local.  Este arquivo deve ser criado com o Configuration Manager. É possível criar tipos semelhantes de pacotes com o Windows ICD (Designer de Configuração e Imagens), mas apenas os pacotes criados no Configuration Manager podem ser usados para registrar dispositivos para o Gerenciamento de Dispositivo Móvel local do início ao fim. Os pacotes criados com o Windows ICD podem fornecer somente o nome UPN necessário para o registro, mas não executam o processo de registro real.  

 O processo para criar o pacote de registro requer o Windows ADK (Kit de Avaliação e Implantação do Windows) para o Windows 10.  No servidor que executa o console do Configuration Manager, certifique-se de ter a versão 1511 do Windows ADK instalada. Para mais informações, consulte a seção [Baixar kits e ferramentas para o Windows 10](https://msdn.microsoft.com/windows/hardware/dn913721.aspx)do ADK  

> [!TIP]  
>  Se você remover um pacote de registro do console do Configuration Manager, ele não poderá ser usado para registrar dispositivos. É possível usar a remoção de pacote como uma maneira de gerenciar pacotes que você não desejar mais usar para o registro em massa de dispositivos.  

#### <a name="to-create-an-enrollment-package-ppkg-file"></a>Para criar um arquivo (ppkg) de pacote de registro:  

1.  Clique com o botão direito do mouse no perfil que acabou de criar (no [Criar um perfil de registro](#bkmk_createEnroll)) e clique em **Exportar**.  

2.  Clique em **Procurar**, encontre um local para salvar o arquivo .ppkg, insira um nome para o pacote e clique em **Salvar**.  

3.  Se desejar proteger o pacote com senha, clique na caixa de seleção ao lado de **Criptografar Pacote**, clique em **Exportar** e aguarde cerca de 10 segundos até que a exportação seja concluída.  

    > [!NOTE]  
    >  Se você criptografou o pacote, o Configuration Manager fornece uma mensagem com a senha descriptografada nele. Lembre-se de salvar as informações de senha, pois você precisará delas para provisionar o pacote nos dispositivos.  

4.  Clique em **OK**.  

##  <a name="a-namebkmkgetppkga-use-the-package-to-bulk-enroll-a-device"></a><a name="bkmk_getPpkg"></a> Usar o pacote para registrar um dispositivo em massa  
 É possível usar o pacote para registrar dispositivos antes ou depois que o dispositivo tiver sido configurado por meio do processo OOBE (tela de apresentação).   O pacote de registro também pode ser incluído como parte de um pacote de provisionamento do OEM (fabricante de equipamento original).  

 O pacote deve ser fisicamente entregue ao dispositivo para ser usado para o registro em massa. É possível entregar o pacote de registro para o dispositivo de várias maneiras, dependendo de suas necessidades, incluindo:  

-   Copiar do sistema de arquivos  

-   Anexar ao email  

-   Copiar em conexão NFC (comunicação a curta distância)  

-   Copiar do cartão de memória  

-   Escanear o código de barras  

-   Copiar de um dispositivo vinculado  

-   Incluir no pacote de provisionamento do OEM  

#### <a name="to-bulk-enroll-a-device"></a>Para registrar um dispositivo em massa:  

1.  No dispositivo a ser registrado, encontre o pacote de registro (usando o Explorador de Arquivos) e clique duas vezes no arquivo .ppkg.  

2.  Clique em **Sim** na mensagem do Controle de Conta de Usuário.  

3.  Na caixa de diálogo que pergunta se o pacote provém de uma fonte confiável, clique em **Sim, adicionar agora**.  

     O processo de registro é iniciado e leva cerca de 5 minutos.  

4.  Abra **Configurações**.  

5.  Clique em  **Contas** > **Acesso Corporativo**. Quando o registro for bem-sucedido, você verá uma conta em **CompanyApps**  

6.  Clique na conta e em **Sincronizar**, o que iniciará o gerenciamento com o Configuration Manager.  

##  <a name="a-namebkmkverifyenrolla-verify-enrollment-of-device"></a><a name="bkmk_verifyEnroll"></a> Verificar o registro do dispositivo  
 É possível verificar se os dispositivos foram registrados com êxito no console do Configuration Manager.  

-   Inicie o console do Configuration Manager.  

-   Clique em **Ativos e Conformidade** > **Visão Geral** > **Dispositivos**. O dispositivo registrado aparecerá na lista.  



<!--HONumber=Dec16_HO3-->


