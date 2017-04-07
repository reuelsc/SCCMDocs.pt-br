---
title: Criar perfis de certificado PFX | Microsoft Docs
description: "Saiba como usar arquivos PFX no System Center Configuration Manager para gerar certificados específicos do usuário que dão suporte à troca de dados criptografados."
ms.custom: na
ms.date: 03/30/2017
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
ms.sourcegitcommit: 3b1451edaed69a972551bd060293839aa11ec8b2
ms.openlocfilehash: 2495cef2442706b343bac6d510946c1226b64cfc
ms.lasthandoff: 03/28/2017


---
# <a name="how-to-create-pfx-certificate-profiles-in-system-center-configuration-manager"></a>Como criar perfis de certificado PFX no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os perfis de certificado funcionam com os Serviços de Certificados do Active Directory e com a função Serviço de Registro de Dispositivo de Rede para provisionar certificados de autenticação para os dispositivos gerenciados para que os usuários possam acessar perfeitamente os recursos da empresa. Por exemplo, você pode criar e implantar perfis de certificado para fornecer os certificados necessários para que os usuários iniciem conexões VPN e sem fio.

[Perfis de certificado](../../protect/deploy-use/introduction-to-certificate-profiles.md) fornece informações gerais sobre como criar e configurar perfis de certificado. Este tópico destaca algumas informações específicas sobre perfis de certificado relacionados aos certificados PFX.

-  O Configuration Manager dá suporte à implantação de certificados em repositórios de certificado diferentes, dependendo dos requisitos, do tipo de dispositivo e do sistema operacional. Os dispositivos a seguir têm suporte quando eles são registrados com o Intune:

 -   iOS  

- Para outros pré-requisitos, confira [Pré-requisitos de perfil de certificado](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

## <a name="pfx-certificate-profiles"></a>Perfis de certificado PFX
O System Center Configuration Manager permite provisionar arquivos de troca de informações pessoais (.pfx) para dispositivos do usuário. Os arquivos PFX podem ser usados para gerar certificados específicos do usuário para dar suporte à troca de dados criptografados. Os certificados PFX podem ser criados no Configuration Manager ou importados.

> [!TIP]  
>  Um tutorial passo a passo que descreve esse processo está disponível em [Como criar e implantar perfis de certificado PFX no Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx).  

## <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Criar e implantar um perfil de certificado PFX (Troca de Informações Pessoais)  

### <a name="get-started"></a>Introdução

1.  No console do System Center Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , expanda **Configurações de Conformidade**, expanda **Acesso ao Recurso da Empresa**e clique em **Perfis de Certificado**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Perfil Certificado**.

4.  Na página **Geral** do Assistente para **Criar Perfil de Certificado** , especifique as seguintes informações:  

    -   **Nome**: insira um nome exclusivo para o perfil de certificado. Você pode usar no máximo 256 caracteres.  

    -   **Descrição**: forneça uma descrição que ofereça uma visão geral do perfil de certificado e outras informações relevantes que ajudem a identificá-lo no console do System Center Configuration Manager. Você pode usar no máximo 256 caracteres.  

    -   **Especifique o tipo de perfil de certificado que deseja criar**: para certificados PFX, escolha um desses:  

        -   **Troca de Informações Pessoais – Configurações PKCS #12 (PFX) – Importar**: selecione esta opção para importar um certificado PFX.  
        -   **Troca de Informações Pessoais – Configurações PKCS #12 (PFX) – Criar**: selecione esta opção para criar um novo certificado PFX.

### <a name="import-a-pfx-certificate"></a>Importar um certificado PFX

Para importar um certificado PFX, você precisará do SDK do Configuration Manager. Todos os certificados que você importar para um usuário serão implantados em todos os dispositivos em que o usuário se registra.

1. Na página **Certificado PFX** do **Assistente Criar Perfil de Certificado**, especifique o local onde o certificado PFX será armazenado nos dispositivos nos quais você o implantará:
    -     **Instalar em um TPM (Trusted Platform Module), se houver**  
    -   **Instalar em um TPM (Trusted Platform Module); caso contrário, ocorrerá uma falha** 
    -   **Instalar para o Windows Hello para Empresas, caso contrário, falhará** 
    -   **Instalar o Provedor de Armazenamento de Chaves de Software** 
2. Clique em **Avançar**. 
3. Na página **Plataformas Suportadas** do assistente, escolha as plataformas de dispositivo nas quais este certificado será instalado e clique em **Avançar**.
4. Usando o SDK para Windows 8.1 disponível no Centro de Download ([http://go.microsoft.com/fwlink/?LinkId=613525](http://go.microsoft.com/fwlink/?LinkId=613525), implante um Script para Criar PFX. O Script para Criar PFX adicionado no Configuration Manager 2012 SP2 adiciona uma classe SMS_ClientPfxCertificate ao SDK. Esta classe inclui os seguintes métodos:  

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

   -   blob\ = The PFX base64-encrypted blob  
   -   $Password = A senha do arquivo PFX  
   -   $ProfileName = O nome do perfil PFX  
   -   ComputerName = nome do computador host   

### <a name="create-a-new-pfx-certificate"></a>Criar um novo certificado PFX

Quando você cria e implanta um certificado PFX, o mesmo certificado será instalado em todos os dispositivos em que o usuário se registra.

1. Na página **Plataformas Suportadas** do assistente, escolha as plataformas de dispositivo nas quais este certificado será instalado e clique em **Avançar**.
2. Na página **Autoridades de Certificação** do assistente, configure o seguinte:
    - **Site primário** - selecione o site primário do Configuration Manager do qual você deseja selecionar uma autoridade de certificação.
    - **Autoridades de certificação** - depois de selecionar um site primário, selecione a autoridade de certificação que você deseja na lista e clique em **Avançar**.
3. Na página **Certificado PFX** do assistente, configure os seguintes valores:
    - **Limite de renovação (%)**: especifique o percentual do tempo de vida do certificado restante antes da renovação das solicitações de dispositivo do certificado.
    - **Nome do modelo de certificado**: clique em **Procurar** para selecionar o nome de um modelo de certificado que foi adicionado a uma AC emissora. Para procurar pelos modelos de certificado, a conta de usuário que você estiver usando para executar o console do Configuration Manager deve ter permissão de **Leitura** para o modelo de certificado. Alternativamente, digite o nome do modelo de certificado. 
    - **Formato de nome da entidade**: na lista, selecione o modo como o Configuration Manager cria automaticamente o nome da entidade na solicitação de certificado. Se o certificado for para um usuário, você também pode incluir o endereço de email do usuário no nome da entidade. Escolha **Nome comum** ou **Nome totalmente diferenciado**.
    - **Nome alternativo da entidade**: especifique como o Configuration Manager criará automaticamente os valores para o SAN (nome alternativo da entidade) na solicitação de certificado. Se tiver selecionado um tipo de certificado de usuário, por exemplo, você pode incluir o UPN no nome alternativo da entidade. Escolha:
        - **Endereço de email** 
        - **UPN (Nome UPN)** 
    - **Período de validade do certificado** - 
    - **Provedor de armazenamento de chave do Windows** (exibido somente se você selecionou Windows como uma plataforma com suporte) - 
        -     **Instalar em um TPM (Trusted Platform Module), se houver**  
        -   **Instalar em um TPM (Trusted Platform Module); caso contrário, ocorrerá uma falha** 
        -   **Instalar para o Windows Hello para Empresas, caso contrário, falhará** 
        -   **Instalar o Provedor de Armazenamento de Chaves de Software** 
4. Clique em **Avançar**.

### <a name="finish-up"></a>Concluir

1.  Clique em **Próximo**, examine a página **Resumo** e feche o assistente.  
2.  O perfil de certificado que contém o arquivo PFX agora está disponível do espaço de trabalho **Perfis de Certificado** . 
3.  Para implantar o perfil, no espaço de trabalho **Ativos e Conformidade**, abra **Configurações de Conformidade** > **Acesso ao Recurso da Empresa** > **Perfis de Certificado**, clique com o botão direito no certificado desejado e clique em **Implantar**. 



## <a name="see-also"></a>Consulte também
[Criar um novo perfil de certificado](../../protect/deploy-use/create-certificate-profiles.md#create-a-new-certificate-profile) orienta você pelo Assistente para criar perfil de certificado.

[Implantar Wi-Fi, VPN, email e perfis de certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) para obter informações sobre como implantar perfis de certificado.
