---
title: "Configurações do Windows Hello para Empresas | Microsoft Docs"
description: Saiba como integrar o Windows Hello para Empresas com o System Center Configuration Manager.
ms.custom: na
ms.date: 10/10/2016
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
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 1f254ee31bae1c3d7b1506e68c40baf78793bf66


---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>Windows Hello para Empresas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager permite que você se integre com o Windows Hello para Empresas (anteriormente conhecida como Microsoft Passport para Windows), um método de entrada alternativo para dispositivos Windows 10. O Hello para Empresas usa o Active Directory ou uma conta do Azure Active Directory para substituir uma senha, cartão inteligente ou cartão inteligente virtual.  

O Hello para Empresas permite que você use um **gesto de usuário** para logon, em vez de uma senha. O gesto do usuário pode ser um PIN simples, uma autenticação biométrica ou um dispositivo externo, como um leitor de impressão digital.  

 O Configuration Manager integra-se com o Windows Hello para Empresas de duas maneiras:  

-   É possível usar o Configuration Manager para controlar quais gestos os usuários podem e não podem usar para se conectar.  

-   Você pode armazenar certificados de autenticação no KSP (provedor de armazenamento de chaves) do Windows Hello para Empresas. Para obter mais informações, consulte [Certificate profiles (Perfis de Certificado)](introduction-to-certificate-profiles.md).  

- É possível implantar as políticas do Windows Hello para Empresas em dispositivos Windows 10 ingressados em domínio que executam o cliente do Configuration Manager. Essa configuração é descrita em [Configurar o Windows Hello para Empresas em dispositivos Windows 10 ingressados em domínio](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices) abaixo. Quando você estiver usando o Configuration Manager com o Intune (híbrido), será possível definir essas configurações em dispositivos Windows 10 e Windows 10 Mobile, mas não em dispositivos ingressados em domínio que executam o cliente do Configuration Manager.   

## <a name="configure-windows-hello-for-business-settings-hybrid"></a>Configurar o Windows Hello para Empresas (híbrido)  

1.  No console do Configuration Manager, clique em **Administração** > **Serviços em Nuvem** > **Assinaturas do Microsoft Intune**.  

3.  Na lista, selecione sua assinatura do Microsoft Intune e, em seguida, na guia **Início** , no grupo **Assinatura** , clique em **Configurar plataformas** > **Windows (MDM)**.  

4.  Na guia **Windows Hello para Empresas** da caixa de diálogo **Propriedades de assinatura do Microsoft Intune** , escolha um dos seguintes valores que afetarão todos os dispositivos Windows 10 e Windows 10 Mobile registrados:  

    -   **Desabilitar Windows Hello para Empresas em dispositivos registrados** ou **Habilitar Windows Hello para Empresas em dispositivos registrados** - habilita ou desabilita o uso do Windows Hello para Empresas em todos os dispositivos Windows 10 e Windows 10 Mobile registrados.  

    -   **Usar um Trusted Platform Module (TPM)** – um chip do TPM (Trusted Platform Module) fornece uma camada adicional de segurança de dados. Selecione uma das seguintes opções:  

        -   **Necessário** (padrão) - somente dispositivos com um TPM acessível podem provisionar o Windows Hello para Empresas.  

        -   **Preferenciais** - Primeira tentativa para usar dispositivos em um TPM. Se não estiver disponível, eles podem usar criptografia de software  

    -   **Exigir comprimento mínimo de PIN** – especifique o número mínimo de caracteres necessários para o PIN do Windows Hello para Empresas. Você deve usar pelo menos quatro caracteres (o valor padrão são seis caracteres).  

    -   **Exigir comprimento máximo de PIN** – especifique o número máximo de caracteres permitidos para o PIN do Windows Hello para Empresas. Você pode usar até 127 caracteres.  

    -   **Exigir letras minúsculas no PIN** – especifica se letras minúsculas devem ser usadas no PIN do Windows Hello para Empresas. Escolha:  

        -   **Permitido** - Os usuários podem usar caracteres minúsculos em seu PIN.  

        -   **Necessário** - Os usuários devem incluir pelo menos um caractere minúsculo no PIN.  

        -   **Não permitido** (padrão) - Os usuários não devem usar caracteres minúsculos em seu PIN.  

    -   **Exigir letras maiúsculas no PIN** – especifica se letras maiúsculas devem ser usadas no PIN do Windows Hello para Empresas. Escolha:  

        -   **Permitido** - Os usuários podem usar caracteres maiúsculos em seu PIN.  

        -   **Necessário** - Os usuários devem incluir pelo menos um caractere maiúsculo no PIN.  

        -   **Não permitido** (padrão) - Os usuários não devem usar caracteres maiúsculos no PIN.  

    -   **Exigir caracteres especiais** – especifica o uso de caracteres especiais no PIN. Escolha:  

        -   **Permitido** - Os usuários podem usar caracteres especiais em seu PIN.  

        -   **Necessário** - Os usuários devem incluir pelo menos um caractere especial em seu PIN.  

        -   **Não permitido** (padrão) - Os usuários não devem usar caracteres especiais no PIN (este também é o comportamento se a configuração não estiver configurada).  

         Os caracteres especiais incluem: **! " # $ % & ' ( ) \* + , - . / : ; < = > ? @ [ \ ] ^ _ ` { &#124; } ~**.  

    -   **Exigir a expiração do PIN (dias)** – especifica o número de dias antes da alteração obrigatória do PIN do dispositivo. O padrão é 41 dias.  

    -   **Evitar a reutilização de PINs anteriores** – use essa configuração para restringir a reutilização de PINs usados anteriormente. O padrão determina que os últimos cinco PINS usados não podem ser reutilizados.  

    -   **Habilitar gestos biométricos** – permite a autenticação biométrica, como reconhecimento facial ou impressão digital, como uma alternativa a um PIN do Windows Hello para Empresas. Os usuários ainda devem configurar um PIN de trabalho no caso de falha de autenticação biométrica.  

         Se definido como **Habilitado**, o Windows Hello para Empresas permite autenticação biométrica.  Se definido como **Desabilitado**, o Windows Hello para Empresas impede a autenticação biométrica (para todos os tipos de conta).  

    -   **Usar antifalsificação avançada, quando disponível** – define se a antifalsificação avançada é usada em dispositivos que são compatíveis com ela.  

         Se definido como **Habilitado**, o Windows exige que todos os usuários usem a antifalsificação para recursos faciais quando há suporte.  

    -   **Usar Remote Passport** – se essa opção for definida como **Habilitada**, os usuários poderão usar o Hello para Empresas para servir como um dispositivo portátil complementar para autenticação de computador desktop. O computador desktop deve ser associado ao Azure Active Directory e o dispositivo complementar deve ser configurado com um PIN do Windows Hello para Empresas.  

5.  Ao terminar, clique em **OK**.  


## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>Configurar o Windows Hello para Empresas em dispositivos Windows 10 ingressados em domínio
É possível controlar as configurações do Windows Hello para Empresas em dispositivos Windows 10 ingressados em domínio de três maneiras:

- É possível criar e implantar um Perfil do Windows Hello para Empresas. Essa é a abordagem recomendada.
- É possível usar uma política de grupo.  
- É possível usar um script do PowerShell.

Observe que, além dessa configuração, também é necessário implantar um perfil de certificado, conforme descrito em [Configurar um perfil de certificado](#configure-a-certificate-profile).

### <a name="recommended-approach----configure-a-windows-hello-for-business-profile"></a>Recomendado abordagem – configurar um perfil do Windows Hello para Empresas  

No console do administração, em **Acesso ao Recurso da Empresa**, clique com o botão direito do mouse em **Perfil do Windows Hello para Empresas** e escolha **Novo** para iniciar o assistente de perfil. Forneça as configurações solicitadas pelo assistente, reveja-as e confirme-as na última página e clique em **Fechar**. Aqui está um exemplo de como será a aparência de suas configurações:  

![Configurações do Windows Hello para Empresas](../media/Hello-for-Business-settings.png)

### <a name="configure-windows-hello-for-business-with-group-policy-in-active-directory"></a>Configurar o Windows Hello para Empresas com a Política de Grupo no Active Directory  

É possível usar uma Política de Grupo do Active Directory para configurar seus dispositivos Windows 10 ingressados em domínio para provisionar a um usuário as credenciais do Microsoft Hello para Empresas quando um usuário faz logon no Windows:

1.  Em um computador Windows Server, abra o Gerenciador do Servidor e navegue até **Ferramentas** > **Gerenciamento de Política de Grupo**.    

2.  Na caixa de diálogo **Gerenciamento de Política de Grupo** , expanda o domínio no qual você deseja habilitar o ingresso automático.    

3.  Clique com o botão direito do mouse em **Objetos de Política de Grupo**e, em seguida, clique em **Novo**.  

4.  Na caixa de diálogo **Novo GPO**, digite um nome para o novo objeto de Política de Grupo, como **Habilitar o Windows Hello para Empresas** e, em seguida, clique em **OK**.  

5.  No nó **Objetos de Política de Grupo** , clique com o botão direito do mouse no objeto que você acabou de criar e, em seguida, clique em **Editar**.  

6.  Na caixa de diálogo **Editor de Gerenciamento de Política de Grupo**, navegue até **Configuração do Computador** > **Políticas** > **Modelos Administrativos** > **Componentes do Windows** > **Windows Hello para Empresas**.  

7.  Clique com o botão direito do mouse em **Habilitar Windows Hello para Empresas ** e, em seguida, clique em **Editar**.   

8.  Selecione **Habilitado**, clique em **Aplicar**e, em seguida, clique em **OK**.

Agora você pode vincular o objeto de Política de Grupo que você acabou de criar em um local de sua escolha. Por exemplo:    

   Uma UO (Unidade Organizacional) específica no AD, em que os computadores que ingressaram no domínio do Windows 10 serão localizados.    

   Um grupo de segurança específico com computadores que ingressaram no domínio do Windows 10 que serão automaticamente registrados com o AD do Azure.    

#### <a name="configure-windows-hello-for-business-by-deploying-a-powershell-script-with-configuration-manager"></a>Configurar o Windows Hello para Empresas implantando um script do PowerShell com o Configuration Manager    
É possível criar e implantar o seguinte script do PowerShell usando o gerenciamento de aplicativos do Configuration Manager.    

```    
powershell.exe -ExecutionPolicy Bypass -NoLogo -NoProfile -Command "& {New-ItemProperty "HKLM:\Software\Policies\Microsoft\PassportForWork" -Name "Enabled" -Value 1 -PropertyType "DWord" -Force}"  
```  

Para obter mais informações sobre o gerenciamento de aplicativos do Configuration Manager, consulte [Introdução ao gerenciamento de aplicativos no System Center Configuration Manager](/sccm/apps/understand/introduction-to-application-management).  

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>Configure um perfil de certificado para registrar o certificado de registro do Windows Hello para Empresas no Configuration Manager  
 Se quiser usar o logon baseado no certificado do Windows Hello para Empresas, ou Microsoft Hello, configure o seguinte:  

-   Um perfil de certificado do Configuration Manager.  

-   No perfil de certificado, selecione um modelo que usa o logon do cartão inteligente EKU.  

 Para obter mais informações, consulte [Certificate profiles (Perfis de Certificado)](introduction-to-certificate-profiles.md).  

### <a name="see-also"></a>Consulte também  
 [Proteger a infraestrutura de dados e do site com o System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md)

 [Gerenciar a verificação de identidade usando o Windows Hello para Empresas](https://technet.microsoft.com/itpro/windows/keep-secure/manage-identity-verification-using-microsoft-passport).  



<!--HONumber=Dec16_HO3-->


