---
title: Criar perfis de certificado PFX | Microsoft Docs
description: "Saiba como usar arquivos PFX no System Center Configuration Manager para gerar certificados específicos do usuário que dão suporte à troca de dados criptografados."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0185ab18-663d-468a-ba54-4f3f232fd4d2
caps.latest.revision: 5
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 36c20af00e5a83be7038c3a0c01a33c546011427


---
# <a name="how-to-create-pfx-certificate-profiles-in-system-center-configuration-manager"></a>Como criar perfis de certificado PFX no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


O System Center Configuration Manager permite provisionar arquivos de troca de informações pessoais (.pfx) para dispositivos do usuário. Os arquivos PFX podem ser usados para gerar certificados específicos do usuário para dar suporte à troca de dados criptografados. Os certificados PFX podem ser criados no Configuration Manager ou importados. Com o System Center Configuration Manager, os certificados PFX, sejam novos ou importados, podem ser implantados em dispositivos iOS, Android e em dispositivos com Windows 10. Estes arquivos podem ser implantados em vários dispositivos para dar suporte à comunicação de PKI baseada no usuário.  

> [!TIP]  
>  Um tutorial passo a passo que descreve esse processo está disponível em [Como criar e implantar perfis de certificado PFX no Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx).  

## <a name="create-and-deploy-personal-information-exchange-pfx-certificate-profiles"></a>Criar e implantar perfis de certificado PFX (Troca de Informações Pessoais)  

#### <a name="how-to-create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Como criar e implantar um perfil de certificado PFX (Troca de Informações Pessoais)  

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



<!--HONumber=Dec16_HO3-->


