---
title: Criar perfis de certificado PFX | Microsoft Docs
description: "Saiba como usar arquivos PFX no System Center Configuration Manager para gerar certificados específicos do usuário que dão suporte à troca de dados criptografados."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: eddecee8886296fb6132d7477afebbfc7fd280d1
ms.lasthandoff: 03/06/2017


---
# <a name="how-to-create-pfx-certificate-profiles-in-system-center-configuration-manager"></a>Como criar perfis de certificado PFX no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os perfis de certificado funcionam com os Serviços de Certificados do Active Directory e com a função Serviço de Registro de Dispositivo de Rede para provisionar certificados de autenticação para os dispositivos gerenciados para que os usuários possam acessar perfeitamente os recursos da empresa. Por exemplo, você pode criar e implantar perfis de certificado para fornecer os certificados necessários para que os usuários iniciem conexões VPN e sem fio.

[Perfis de certificado](../../protect/deploy-use/introduction-to-certificate-profiles.md) fornece informações gerais sobre como criar e configurar perfis de certificado. Este tópico destaca algumas informações específicas sobre perfis de certificado relacionados ao gerenciamento de dispositivos móveis.

- Os perfis de certificado fornecem registro e renovação de uma AC (autoridade de certificação) corporativa para dispositivos que executam iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop e Mobile e Android. Esses certificados podem ser usados para conexões Wi-Fi e VPN.

-  Para implantar perfis de certificado que usam o SCEP, você deve instalar um módulo de política para NDES em um servidor que executa o Windows Server 2012 R2 com a função de Serviços de Certificados do Active Directory, e um NDES operacional que possa ser acessado pelos dispositivos que exigem os certificados. Para dispositivos registrados pelo Microsoft Intune, isso requer que o NDES esteja acessível pela Internet, por exemplo, em uma sub-rede filtrada (também conhecida como DMZ).

-  O Configuration Manager dá suporte à implantação de certificados em repositórios de certificado diferentes, dependendo dos requisitos, do tipo de dispositivo e do sistema operacional. Os seguintes dispositivos e sistemas operacionais têm suporte:
 -   Windows RT 8.1  
 -   Windows 8.1  
 -   Windows Phone 8.1  
 -   Windows 10 Desktop e Mobile  
 -   iOS  
 -   Android  
 > [!IMPORTANT]  
 >  Para implantar perfis em dispositivos Android, iOS, Windows Phone e em dispositivos registrados Windows 8.1 ou posteriores, esses dispositivos devem ser [registrados no Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).   

- Para outros pré-requisitos, confira [Pré-requisitos de perfil de certificado](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

## <a name="pfx-certificate-profiles"></a>Perfis de certificado PFX
O System Center Configuration Manager permite provisionar arquivos de troca de informações pessoais (.pfx) para dispositivos do usuário. Os arquivos PFX podem ser usados para gerar certificados específicos do usuário para dar suporte à troca de dados criptografados. Os certificados PFX podem ser criados no Configuration Manager ou importados. Com o System Center Configuration Manager, os certificados PFX, sejam novos ou importados, podem ser implantados em dispositivos iOS, Android e em dispositivos com Windows 10. Estes arquivos podem ser implantados em vários dispositivos para dar suporte à comunicação de PKI baseada no usuário.  

> [!TIP]  
>  Um tutorial passo a passo que descreve esse processo está disponível em [Como criar e implantar perfis de certificado PFX no Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx).  

### <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Criar e implantar um perfil de certificado PFX (Troca de Informações Pessoais)  

1.  No console do System Center Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , expanda **Configurações de Conformidade**, expanda **Acesso ao Recurso da Empresa**e clique em **Perfis de Certificado**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Perfil Certificado**. O Assistente para **Criar Perfil de Certificado** é aberto.  

4.  Na página **Geral** do Assistente para **Criar Perfil de Certificado** , especifique as seguintes informações:  

    -   **Nome**: insira um nome exclusivo para o perfil de certificado. Você pode usar no máximo 256 caracteres.  

    -   **Descrição**: forneça uma descrição que ofereça uma visão geral do perfil de certificado e outras informações relevantes que ajudem a identificá-lo no console do System Center Configuration Manager. Você pode usar no máximo 256 caracteres.  

    -   **Especifique o tipo de perfil de certificado que deseja criar**: escolha um dos seguintes tipos de perfil de certificado:  

        -   **Certificado de AC confiável**: selecione este tipo de perfil de certificado se desejar implantar uma AC (autoridade de certificação) raiz confiável ou intermediar o certificado da AC para formar uma cadeia de confiança de certificados para quando o usuário, ou dispositivo, precisar autenticar outro dispositivo. Por exemplo, o dispositivo pode ser um servidor RADIUS ou VPN (rede virtual privada). Você também deve configurar um perfil de certificado de autoridade de certificação confiável antes de criar um perfil de certificado SCEP. Neste caso, o certificado de autoridade de certificação confiável tem que ser o certificado confiável raiz da AC que emitirá o certificado para o usuário ou dispositivo.  

        -   **Configurações do protocolo SCEP**: selecione este tipo de perfil de certificado se desejar solicitar um certificado para um usuário ou dispositivo usando o protocolo SCEP e o serviço de função de Serviço de Registro de Dispositivo de Rede.  

        -   **Troca de Informações Pessoais – Configurações PKCS #12 (PFX) – Importar**: selecione esta opção para importar um certificado PFX.  

5.  Na janela **Propriedades do Certificado** do assistente **Criar Perfil de Certificado** , especifique o local onde o certificado PFX será armazenado nos dispositivos de destino.  

    -   **Instalar em um TPM (Trusted Platform Module), se houver**  

    -   **Instalar em um TPM (Trusted Platform Module); caso contrário, ocorrerá uma falha**  

    -   **Instalar o Provedor de Armazenamento de Chaves de Software**  

     Clique em **Avançar**.  

6.  Na janela **Plataformas com Suporte** do assistente para **Criar Perfil de Certificado** , especifique quais sistemas operacionais ou plataformas podem receber o arquivo PFX importado.  

    -   **Windows 10**  

    -   **iPhone**  

    -   **iPad**  

    -   **Android**  

7.  Clique em **Próximo**, examine a página **Resumo** e feche o assistente.  

8.  O perfil de certificado que contém o arquivo PFX agora está disponível do espaço de trabalho **Perfis de Certificado** . No console do **Ativos e Conformidade** , vá para **Configurações de Conformidade** > **Acesso ao Recurso da Empresa** > **Perfis de Certificado** e clique com o botão direito do mouse para implantar o novo certificado nas coleções de Usuários.  

9. Usando o SDK para Windows 8.1 disponível no Centro de Download ([http://go.microsoft.com/fwlink/?LinkId=613525](http://go.microsoft.com/fwlink/?LinkId=613525), implante um Script para Criar PFX. O Script para Criar PFX adicionado no Configuration Manager 2012 SP2 adiciona uma classe SMS_ClientPfxCertificate ao SDK. Esta classe inclui os seguintes métodos:  

    -   ImportForUser  

    -   DeleteForUser  

     Exemplo de script:  

    ```  
    $EncryptedPfxBlob = "<blob>"  
    $Password = "abc"  
    $ProfileName = "PFX_Profile_Name"  
    $UserName = "ComputerName\Administrator"  

    #New pfx  
    $WMIConnection = ([WMIClass]"\\nksccm\root\SMS\Site_MDM:SMS_ClientPfxCertificate")  
        $NewEntry = $WMIConnection.psbase.GetMethodParameters("ImportForUser")  
        $NewEntry.EncryptedPfxBlob = $EncryptedPfxBlob  
        $NewEntry.Password = $Password  
        $NewEntry.ProfileName = $ProfileName  
        $NewEntry.UserName = $UserName  
    $Resource = $WMIConnection.psbase.InvokeMethod("ImportForUser",$NewEntry,$null)  

    ```  

     As seguintes variáveis de script devem ser modificadas para o seu script:  

    -   <blob\> = O blob com criptografia PFX base64  

    -   $Password = A senha do arquivo PFX  

    -   $ProfileName = O nome do perfil PFX  

    -   ComputerName = nome do computador host  

### <a name="see-also"></a>Consulte também
[Criar um novo perfil de certificado](../../protect/deploy-use/create-certificate-profiles.md#create-a-new-certificate-profile) orienta você pelo Assistente para criar perfil de certificado.

[Implantar Wi-Fi, VPN, email e perfis de certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) para obter informações sobre como implantar perfis de certificado.

