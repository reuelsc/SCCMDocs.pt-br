---
title: "Configurações do Windows Hello para Empresas | Microsoft Docs"
description: Saiba como integrar o Windows Hello para Empresas com o System Center Configuration Manager.
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
caps.latest.revision: 17
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 699b79b68440b61904a9053e5004318a2a248bfd
ms.openlocfilehash: 75def95561feb35f2f060f0daa72291983324d4f
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017


---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>Windows Hello para Empresas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager permite que você se integre com o Windows Hello para Empresas (anteriormente conhecida como Microsoft Passport para Windows), um método de entrada alternativo para dispositivos Windows 10. O Hello para Empresas usa o Active Directory ou uma conta do Azure Active Directory para substituir uma senha, cartão inteligente ou cartão inteligente virtual.  

O Hello para Empresas permite que você use um **gesto de usuário** para logon, em vez de uma senha. O gesto do usuário pode ser um PIN simples, uma autenticação biométrica ou um dispositivo externo, como um leitor de impressão digital.

[Saiba mais sobre o Windows Hello para empresas](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification)

 O Configuration Manager integra-se com o Windows Hello para Empresas de duas maneiras:  

-   É possível usar o Configuration Manager para controlar quais gestos os usuários podem e não podem usar para se conectar.  

-   Você pode armazenar certificados de autenticação no KSP (provedor de armazenamento de chaves) do Windows Hello para Empresas. Para obter mais informações, consulte [Certificate profiles (Perfis de Certificado)](introduction-to-certificate-profiles.md).  

- É possível implantar as políticas do Windows Hello para Empresas em dispositivos Windows 10 ingressados em domínio que executam o cliente do Configuration Manager. Essa configuração é descrita em [Configurar o Windows Hello para Empresas em dispositivos Windows 10 ingressados em domínio](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices) abaixo. Quando você estiver usando o Configuration Manager com o Intune (híbrido), será possível definir essas configurações em dispositivos Windows 10 e Windows 10 Mobile, mas não em dispositivos ingressados em domínio que executam o cliente do Configuration Manager. Confira [Definir configurações do Windows Hello para empresas (híbrido)](../../mdm/deploy-use/windows-hello-for-business-settings.md) para saber mais.

## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>Configurar o Windows Hello para Empresas em dispositivos Windows 10 ingressados em domínio
É possível controlar as configurações do Windows Hello para Empresas em dispositivos Windows 10 ingressados em domínio de três maneiras:

- É possível criar e implantar um Perfil do Windows Hello para Empresas. Essa é a abordagem recomendada.
- É possível usar uma política de grupo.  
- É possível usar um script do PowerShell.

Observe que, além dessa configuração, também é necessário implantar um perfil de certificado, conforme descrito em [Configurar um perfil de certificado](#configure-a-certificate-profile).

## <a name="configure-a-windows-hello-for-business-profile"></a>Configurar um perfil para o Windows Hello para empresas  

No console do Configuration Manager, em **Acesso ao Recurso da Empresa**, clique com o botão direito do mouse em **Perfil do Windows Hello para Empresas** e escolha **Novo** para iniciar o assistente de perfil. Forneça as configurações solicitadas pelo assistente, reveja-as e confirme-as na última página e clique em **Fechar**. Aqui está um exemplo de como será a aparência de suas configurações:  

![Configurações do Windows Hello para Empresas](../media/Hello-for-Business-settings.png)

## <a name="configure-windows-hello-for-business-with-group-policy-in-active-directory"></a>Configurar o Windows Hello para Empresas com a Política de Grupo no Active Directory  

É possível usar uma Política de Grupo do Active Directory para configurar seus dispositivos Windows 10 ingressados em domínio para provisionar a um usuário as credenciais do Microsoft Hello para Empresas quando um usuário faz logon no Windows:

1.  Em um computador Windows Server, abra o Gerenciador do Servidor e navegue até **Ferramentas** > **Gerenciamento de Política de Grupo**.    

2.  Na caixa de diálogo **Gerenciamento de Política de Grupo** , expanda o domínio no qual você deseja habilitar o ingresso automático.    

3.  Clique com o botão direito do mouse em **Objetos de Política de Grupo**e, em seguida, clique em **Novo**.  

4.  Na caixa de diálogo **Novo GPO**, digite um nome para o novo objeto de Política de Grupo, como **Habilitar o Windows Hello para Empresas** e, em seguida, clique em **OK**.  

5.  No nó **Objetos de Política de Grupo** , clique com o botão direito do mouse no objeto que você acabou de criar e, em seguida, clique em **Editar**.  

6.  Na caixa de diálogo **Editor de Gerenciamento de Política de Grupo**, navegue até **Configuração do Computador** > **Políticas** > **Modelos Administrativos** > **Componentes do Windows** > **Windows Hello para Empresas**.  

7.  Clique com o botão direito do mouse em **Habilitar Windows Hello para Empresas**  e, em seguida, clique em **Editar**.   

8.  Selecione **Habilitado**, clique em **Aplicar**e, em seguida, clique em **OK**.

Agora você pode vincular o objeto de Política de Grupo que você acabou de criar em um local de sua escolha. Por exemplo:    

   Uma UO (Unidade Organizacional) específica no AD, em que os computadores que ingressaram no domínio do Windows 10 serão localizados.    

   Um grupo de segurança específico com computadores que ingressaram no domínio do Windows 10 que serão automaticamente registrados com o AD do Azure.    

## <a name="configure-windows-hello-for-business-by-deploying-a-powershell-script-with-configuration-manager"></a>Configurar o Windows Hello para Empresas implantando um script do PowerShell com o Configuration Manager    
É possível criar e implantar o seguinte script do PowerShell usando o gerenciamento de aplicativos do Configuration Manager.    

**powershell.exe -ExecutionPolicy Bypass -NoLogo -NoProfile -Command "& {New-ItemProperty "HKLM:\Software\Policies\Microsoft\PassportForWork" -Name "Enabled" -Value 1 -PropertyType "DWord" -Force}" ** 

Para obter mais informações sobre o gerenciamento de aplicativos do Configuration Manager, consulte [Introdução ao gerenciamento de aplicativos no System Center Configuration Manager](/sccm/apps/understand/introduction-to-application-management).  

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>Configure um perfil de certificado para registrar o certificado de registro do Windows Hello para Empresas no Configuration Manager  
 Se quiser usar o logon baseado no certificado do Windows Hello para Empresas, ou Microsoft Hello, configure o seguinte:  

-   Um perfil de certificado do Configuration Manager.  

-   No perfil de certificado, selecione um modelo que usa o logon do cartão inteligente EKU.  

-    Se você pretende armazenar perfis de certificado no contêiner de chaves do Windows Hello para Empresas, e o perfil de certificado usa o EKU de **Logon de Cartão Inteligente**, deverá configurar as seguintes permissões para registro de chave para garantir que o certificado seja validado corretamente.
Você primeiro deverá ter criado o **Administradores de Chave** e adicionado a esse grupo todos os computadores do ponto de gerenciamento do Configuration Manager como membros.

    1.    Faça logon em um controlador de domínio ou estações de trabalho de gerenciamento com o Administrador de Domínio ou credenciais equivalentes.
    2.    Abra **usuários e computadores do Active Directory**.
    3.    No painel de navegação, clique com o botão direito no seu nome de domínio e, em seguida, clique em **Propriedades**.
    4.    Na guia **Segurança** da caixa de diálogo *<domain name>* **Propriedades**, clique em **Avançado**. Se a guia **Segurança** não for exibida, ative **Recursos Avançados** do menu **Exibição** de **Usuários e Computadores do Active Directory**.
    5.    Clique em **Adicionar**.
    6.    Na caixa de diálogo **Entrada de Permissão para** *<domain name>*, clique em **Selecionar uma entidade**.
    7.    Na caixa de diálogo **Selecionar Usuário, Computador, Conta de Serviço ou Grupo**, digite **Administradores de Chave** na caixa de texto **Insira o nome do objeto para selecionar**.  Clique em **OK**.
    8.    Da lista **Aplica-se a**, selecione **Objetos do Usuário Descendente**.
    9.    Role até a parte inferior da página e clique em **Limpar tudo**.
    10.    Na seção **Propriedades**, selecione **Ler msDS-KeyCredentialLink**.
    11.    Clique em **OK** três vezes para concluir a tarefa.


 Para obter mais informações, consulte [Certificate profiles (Perfis de Certificado)](introduction-to-certificate-profiles.md).  





