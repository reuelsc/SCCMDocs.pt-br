---
title: Criar perfis de certificado PFX importando detalhes do certificado | Microsoft Docs
description: "Saiba como usar arquivos PFX no System Center Configuration Manager para gerar certificados específicos do usuário que dão suporte à troca de dados criptografados."
ms.custom: na
ms.date: 04/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
caps.latest.revision: "5"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: c8346d04c7cd9761291824f5d30f09fab9acbcf9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-pfx-certificate-profiles-by-importing-certificate-details"></a>Como criar perfis de certificado PFX importando detalhes do certificado

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Aqui, você aprende a criar um perfil de certificado importando as credenciais de certificados externos.  

[Perfis de certificado](../../protect/deploy-use/introduction-to-certificate-profiles.md) fornecem informações gerais sobre como criar e configurar perfis de certificado. Este tópico destaca algumas informações específicas sobre perfis de certificado relacionados aos certificados PFX.

-  O Configuration Manager tem vários repositórios de certificado apropriados para diferentes dispositivos e sistemas operacionais.  Elas incluem:

 -   iOS e MacOS/OSX
 -   Android e Android for Work
 -   Windows 10, incluindo Windows 10 Mobile.

Para saber mais, confira [Pré-requisitos para perfis de certificado](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

## <a name="pfx-certificate-profiles"></a>Perfis de certificado PFX
O System Center Configuration Manager permite que você importe credenciais de certificado e provisione arquivos .pfx (troca de informações pessoais) para dispositivos do usuário. Os arquivos PFX podem ser usados para gerar certificados específicos do usuário para dar suporte à troca de dados criptografados.

> [!TIP]  
>  Um tutorial passo a passo que descreve esse processo está disponível em [Como criar e implantar perfis de certificado PFX no Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx).  

## <a name="create-import-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Criar, importar e implantar um perfil de certificado PFX (Troca de Informações Pessoais)  

### <a name="get-started"></a>Introdução

1.  No console do System Center Configuration Manager, clique em **Ativos e Conformidade**.  
2.  No espaço de trabalho **Ativos e Conformidade** , expanda **Configurações de Conformidade**, expanda **Acesso ao Recurso da Empresa**e clique em **Perfis de Certificado**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Perfil Certificado**.

4.  Na página **Geral** do Assistente para **Criar Perfil de Certificado** , especifique as seguintes informações:  

    -   **Nome**: insira um nome exclusivo para o perfil de certificado. Você pode usar no máximo 256 caracteres.  

    -   **Descrição**: forneça uma descrição que ofereça uma visão geral do perfil de certificado e outras informações relevantes que ajudem a identificá-lo no console do System Center Configuration Manager. Você pode usar no máximo 256 caracteres.  

    -   **Especifique o tipo de perfil de certificado que deseja criar**: para certificados PFX, escolha uma das opções a seguir:  

        -   **Configurações de Troca de Informações Pessoais PKCS #12 (PFX) – Importar**: cria um perfil de certificado importando programaticamente as informações de certificados existentes.  

        -   **Configurações de Troca de Informações Pessoais – PKCS #12 (PFX) – Criar**: cria um perfil de certificado PFX usando as credenciais fornecidas por uma autoridade de certificação.  Para saber mais, confira [Como criar perfis de certificado PFX usando uma autoridade de certificação](../../mdm/deploy-use/create-pfx-certificate-profiles.md).


### <a name="create-a-pfx-certificate-profile-for-the-imported-credentials"></a>Criar um perfil de certificado PFX para as credenciais importadas

Para importar um certificado PFX, use o SDK do Configuration Manager para implantar um script Criar PFX. 

Certificados importados são posteriormente implantados em dispositivos registrados.

1. Na página **Certificado de PFX** do **Assistente para Criar Perfil de Certificado**, especifique onde o provedor de armazenamento de chave do dispositivo:
    -   **Instalar em um TPM (Trusted Platform Module), se houver**  
    -   **Instalar em um TPM (Trusted Platform Module); caso contrário, ocorrerá uma falha** 
    -   **Instalar para o Windows Hello para Empresas, caso contrário, falhará** 
    -   **Instalar o Provedor de Armazenamento de Chaves de Software** 
2. Clique em **Avançar**. 
3. Na página **Plataformas com Suporte** do assistente, escolha as plataformas de dispositivo com suporte e clique em **Avançar**.

### <a name="finish-the-profile"></a>Concluir o perfil

1.  Clique em **Próximo**, examine a página **Resumo** e feche o assistente.  
2.  O perfil de certificado que contém o arquivo PFX agora está disponível do espaço de trabalho **Perfis de Certificado** . 
3.  Para implantar o perfil, no espaço de trabalho **Ativos e Conformidade**, abra **Configurações de Conformidade** > **Acesso ao Recurso da Empresa** > **Perfis de Certificado**, clique com o botão direito no certificado desejado e clique em **Implantar**. 

### <a name="deploy-a-create-pfx-script"></a>Implantar um script Criar PFX

Use o [SDK do Configuration Manager](http://go.microsoft.com/fwlink/?LinkId=613525) para implantar um script Criar PFX. 

O Script para Criar PFX adicionado no Configuration Manager 2012 SP2 adiciona uma classe SMS_ClientPfxCertificate ao SDK. Esta classe inclui os seguintes métodos:  

    -   `ImportForUser`  

    -   `DeleteForUser`  

O exemplo a seguir importa as credenciais para um perfil de certificado PFX.

``` powershell
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

Para usar este exemplo, atualize as variáveis de script a seguir:  

   -   **blob**\ – O blob PFX criptografado em base64  
   -   **$Password** – A senha do arquivo PFX  
   -   **$ProfileName** – O nome do perfil PFX  
   -   **ComputerName** – nome do computador host   

## <a name="see-also"></a>Consulte também
[Criar um novo perfil de certificado](../../protect/deploy-use/create-certificate-profiles.md) orienta você pelo Assistente para criar perfil de certificado.

[Como criar perfis de certificado PFX importando detalhes do certificado](../../mdm/deploy-use/create-pfx-certificate-profiles.md)

[Implantar Wi-Fi, VPN, email e perfis de certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) descreve como implantar perfis de certificado.