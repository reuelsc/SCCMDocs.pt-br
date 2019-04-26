---
title: Configurações do Windows Hello para Empresas
titleSuffix: Configuration Manager
description: Saiba como integrar o Windows Hello para Empresas com o Configuration Manager.
ms.date: 12/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: c0593c07-5dd7-4d23-a0d8-d30165f49ef7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 71f853034133e2ec73a4d8e606c2e0c0c94841a4
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62227576"
---
# <a name="windows-hello-for-business-settings-in-configuration-manager-hybrid"></a>Windows Hello para empresas no Configuration Manager (híbrido)

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Configuration Manager permite a integração com o Windows Hello para empresas (anteriormente Microsoft Passport para Windows), que é um método de logon alternativo para dispositivos Windows 10. O Hello para Empresas usa o Active Directory ou uma conta do Azure Active Directory para substituir uma senha, cartão inteligente ou cartão inteligente virtual. O Hello para Empresas permite que você use um **gesto de usuário** para logon, em vez de uma senha. O gesto do usuário pode ser um PIN simples, uma autenticação biométrica ou um dispositivo externo, como um leitor de impressão digital.  

> [!Important]  
> A partir de dezembro de 2017, Windows Hello para empresas no Configuration Manager é um [recurso preterido](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Implantação do Windows Server 2016 autoridade do Active Directory Federation Services registro (RA ADFS) é mais simples, proporciona uma melhor experiência de usuário e tem uma experiência de registro de certificado mais determinista. Para obter mais informações, confira [Windows Hello para Empresas](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification).  


O Configuration Manager integra-se com o Windows Hello para Empresas de duas maneiras:  

- É possível usar o Configuration Manager para controlar quais gestos os usuários podem e não podem usar para se conectar.  

- Você pode armazenar certificados de autenticação no KSP (provedor de armazenamento de chaves) do Windows Hello para Empresas. Para obter mais informações, consulte [Certificate profiles (Perfis de Certificado)](create-pfx-certificate-profiles.md).  

- É possível implantar as políticas do Windows Hello para Empresas em dispositivos Windows 10 ingressados em domínio que executam o cliente do Configuration Manager. Essa configuração é descrita em [Configurar o Windows Hello para Empresas em dispositivos Windows 10 ingressados em domínio](/sccm/protect/deploy-use/windows-hello-for-business-settings#configure-windows-hello-for-business-on-domain-joined-windows-10-devices). Quando você estiver usando o Configuration Manager com o Intune (híbrido), será possível definir essas configurações em dispositivos Windows 10 e Windows 10 Mobile, mas não em dispositivos ingressados em domínio que executam o cliente do Configuration Manager.   

Para obter informações gerais sobre como configurar o Windows Hello para empresas, consulte [Windows Hello para empresas no Configuration Manager](/sccm/protect/deploy-use/windows-hello-for-business-settings).



## <a name="configure-windows-hello-for-business-settings-hybrid"></a>Configurar o Windows Hello para Empresas (híbrido)  

1. No console do Configuration Manager, clique em **Administração** > **Serviços em Nuvem** > **Assinaturas do Microsoft Intune**.  

2. Na lista, selecione sua assinatura do Microsoft Intune e, em seguida, na guia **Início** , no grupo **Assinatura** , clique em **Configurar plataformas** > **Windows (MDM)**.  

3. Na guia **Windows Hello para Empresas** da caixa de diálogo **Propriedades de assinatura do Microsoft Intune** , escolha um dos seguintes valores que afetarão todos os dispositivos Windows 10 e Windows 10 Mobile registrados:  

   - **Desabilitar Windows Hello para Empresas em dispositivos registrados** ou **Habilitar Windows Hello para Empresas em dispositivos registrados** - habilita ou desabilita o uso do Windows Hello para Empresas em todos os dispositivos Windows 10 e Windows 10 Mobile registrados.  

   - **Usar um Trusted Platform Module (TPM)** – um chip do TPM (Trusted Platform Module) fornece uma camada adicional de segurança de dados. Selecione uma das seguintes opções:  

     -   **Necessário** (padrão) - somente dispositivos com um TPM acessível podem provisionar o Windows Hello para Empresas.  

     -   **Preferenciais** - Primeira tentativa para usar dispositivos em um TPM. Se não estiver disponível, eles podem usar criptografia de software  

   - **Exigir comprimento mínimo de PIN** – especifique o número mínimo de caracteres necessários para o PIN do Windows Hello para Empresas. Você deve usar pelo menos quatro caracteres (o valor padrão são seis caracteres).  

   - **Exigir comprimento máximo de PIN** – especifique o número máximo de caracteres permitidos para o PIN do Windows Hello para Empresas. Você pode usar até 127 caracteres.  

   - **Exigir letras minúsculas no PIN** – especifica se letras minúsculas devem ser usadas no PIN do Windows Hello para Empresas. Escolha:  

     -   **Permitido** - Os usuários podem usar caracteres minúsculos em seu PIN.  

     -   **Necessário** - Os usuários devem incluir pelo menos um caractere minúsculo no PIN.  

     -   **Não permitido** (padrão) - Os usuários não devem usar caracteres minúsculos em seu PIN.  

   - **Exigir letras maiúsculas no PIN** – especifica se letras maiúsculas devem ser usadas no PIN do Windows Hello para Empresas. Escolha:  

     -   **Permitido** - Os usuários podem usar caracteres maiúsculos em seu PIN.  

     -   **Necessário** - Os usuários devem incluir pelo menos um caractere maiúsculo no PIN.  

     -   **Não permitido** (padrão) - Os usuários não devem usar caracteres maiúsculos no PIN.  

   - **Exigir caracteres especiais** – especifica o uso de caracteres especiais no PIN. Escolha:  

     - **Permitido** - Os usuários podem usar caracteres especiais em seu PIN.  

     - **Necessário** - Os usuários devem incluir pelo menos um caractere especial em seu PIN.  

     - **Não permitido** (padrão) - Os usuários não devem usar caracteres especiais no PIN (este também é o comportamento se a configuração não estiver configurada).  

       Caracteres especiais incluem: **! " # $ % & ' ( ) \* + , - . / : ; < = > ? @ [ \ ] ^ _ ` { &#124; } ~**.  

   - **Exigir a expiração do PIN (dias)** – especifica o número de dias antes da alteração obrigatória do PIN do dispositivo. O padrão é 41 dias.  

   - **Evitar a reutilização de PINs anteriores** – use essa configuração para restringir a reutilização de PINs usados anteriormente. O padrão determina que os últimos cinco PINS usados não podem ser reutilizados.  

   - **Habilitar gestos biométricos** – permite a autenticação biométrica, como reconhecimento facial ou impressão digital, como uma alternativa a um PIN do Windows Hello para Empresas. Os usuários ainda devem configurar um PIN de trabalho no caso de falha de autenticação biométrica.  

      Se definido como **Habilitado**, o Windows Hello para Empresas permite autenticação biométrica.  Se definido como **Desabilitado**, o Windows Hello para Empresas impede a autenticação biométrica (para todos os tipos de conta).  

   - **Usar antifalsificação avançada, quando disponível** – define se a antifalsificação avançada é usada em dispositivos que são compatíveis com ela.  

      Se definido como **Habilitado**, o Windows exige que todos os usuários usem a antifalsificação para recursos faciais quando há suporte.  

   - **Usar Remote Passport** – se essa opção for definida como **Habilitada**, os usuários poderão usar o Hello para Empresas para servir como um dispositivo portátil complementar para autenticação de computador desktop. O computador desktop deve ser associado ao Azure Active Directory e o dispositivo complementar deve ser configurado com um PIN do Windows Hello para Empresas.  

4. Ao terminar, clique em **OK**.  



## <a name="see-also"></a>Consulte também  

[Proteger a infraestrutura de dados e do site](/sccm/protect/understand/protect-data-and-site-infrastructure)

[Windows Hello para Empresas](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)  
