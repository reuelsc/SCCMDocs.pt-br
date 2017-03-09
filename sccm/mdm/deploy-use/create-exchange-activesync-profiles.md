---
title: Criar perfis de email do Exchange ActiveSync | Microsoft Docs
description: Saiba como criar e configurar perfis de email no System Center Configuration Manager que funcionam com o Microsoft Intune.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 120442be-179e-450c-a0c4-284046895da3
caps.latest.revision: 4
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 1cbe1d8f34b0a7482232488e907190a7a9cadf30
ms.lasthandoff: 03/06/2017


---

# <a name="exchange-activesync-email-profiles-in-system-center-configuration-manager"></a>Perfis de email do Exchange ActiveSync no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os perfis de email funcionam com o Microsoft Intune para permitir que você provisione dispositivos com restrições e perfis de email usando o Exchange ActiveSync. Isso permite que os usuários acessem email corporativo em seus dispositivos com uma configuração mínima exigida de sua parte.  

 Você pode configurar os seguintes tipos de dispositivo com perfis de email:  

-   Dispositivos que executam o Windows Phone 8  

-   Dispositivos que executam o Windows Phone 8.1  

-   Dispositivos que executam o Windows 10 Mobile  

-   Dispositivos IPhone que executam o iOS 5, iOS 6, iOS 7 e iOS 8  

-   Dispositivos IPad que executam o iOS 5, iOS 6, iOS 7 e iOS 8  

> [!IMPORTANT]  
>  Para implantar perfis em dispositivos iOS, Android Samsung KNOX Standard, Windows Phone e Windows 8.1 ou Windows 10, esses dispositivos devem ser registrados no Intune. Para obter informações sobre como registrar seus dispositivos, veja [Gerenciar dispositivos móveis com o Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).  

 Além de configurar uma conta de email no dispositivo, você também pode configurar as configurações de sincronização de contatos, calendários e tarefas.  

 Ao criar um perfil de email, você pode incluir uma grande variedade de configurações de segurança, inclusive certificados de identidade, criptografia e assinatura que foram provisionados usando os perfis de certificado do System Center Configuration Manager. Para obter mais informações sobre perfis de certificado, consulte [Perfis de certificado do System Center Configuration Manager](introduction-to-certificate-profiles.md).    


## <a name="create-a-new-exchange-activesync-email-profile"></a>Criar um novo perfil de email do Exchange ActiveSync  

Iniciar o Assistente de Criação de Perfil de Email do Exchange ActiveSync  

1.  No console do System Center Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , expanda **Configurações de Conformidade**, expanda **Acesso aos Recursos da Empresa**e clique em **Perfis de email**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar perfil do Exchange ActiveSync**.

4.  Siga as instruções no assistente   

### <a name="to-configure-exchange-activesync-settings-for-the-exchange-activesync-email-profile"></a>Para definir as configurações do Exchange ActiveSync para o perfil de email do Exchange ActiveSync  

1.  Na página **Exchange ActiveSync** do Assistente de criação de perfil de email do Exchange ActiveSync, especifique as seguintes informações:  

    -   **Host do Exchange ActiveSync:** especifique o nome de host do Exchange Server de sua empresa que hospeda os serviços do Exchange ActiveSync.  

    -   **Nome da conta:** especifique o nome de exibição para a conta de email que será exibido aos usuários em seus dispositivos.  

    -   **Nome de usuário da conta:** selecione como o nome de usuário da conta de email é configurado nos dispositivos cliente. Você pode selecionar uma das seguintes opções na lista suspensa:  

        -   **Nome Principal do usuário** usa o nome principal de usuário completo para fazer logon no Exchange.  

        -   Usar**sAMAccountName**   

        -   **Endereço SMTP primário** usa o endereço SMTP principal de usuários para fazer logon no Exchange.  

    -   **Endereço de email:** selecione como o endereço de email do usuário em cada dispositivo cliente é gerado. Você pode selecionar uma das seguintes opções na lista suspensa:  

        -   **Endereço SMTP primário** usa o endereço SMTP principal de usuários para fazer logon no Exchange.  

        -   **Nome Principal do usuário** usa o nome principal de usuário completo como o endereço de email.  

    -   **Domínio da conta:** escolha uma das seguintes opções:  

        -   **Obter do Active Directory**  

        -   **Personalizado**  

         Esse campo só é aplicável se **sAMAccountName** for selecionado na lista suspensa **Nome de usuário da conta** .  

    -   **Método de autenticação:** escolha um dos seguintes métodos de autenticação que serão usados para autenticar a conexão com o Exchange ActiveSync:  

        -   **Certificados** um certificado de identidade será usado para autenticar a conexão do Exchange ActiveSync.  

        -   **Nome de usuário e senha** o usuário do dispositivo deve fornecer uma senha para se conectar ao Exchange ActiveSync (o nome de usuário é configurado como parte do perfil de email).  

    -   **Certificado de identidade:** clique em **Selecionar** e selecione um certificado a ser usado para a identidade.  

        > [!NOTE]  
        >  Antes de selecionar o certificado de identidade, primeiro você deve configurá-lo como um perfil de certificado de protocolo de registro de certificado simples (SCEP). Para obter mais informações sobre perfis de certificado, consulte [Perfis de certificado do System Center Configuration Manager](introduction-to-certificate-profiles.md).  

         Essa opção só estará disponível se você selecionou **Certificados** em **Método de autenticação**.  

    -   **Usar S/MIME** envia emails de saída usando criptografia S/MIME. Essa opção é aplicável somente a dispositivos iOS.  

    -   **Certificados de criptografia:** clique em **Selecionar** e selecione um certificado a ser usado para a criptografia. Essa opção é aplicável somente a dispositivos iOS.  

        > [!NOTE]  
        >  Antes de selecionar o certificado de criptografia, primeiro você deve configurá-lo como um perfil de certificado de protocolo de registro de certificado simples (SCEP). Para obter mais informações sobre perfis de certificado, consulte [Perfis de certificado do System Center Configuration Manager](introduction-to-certificate-profiles.md).  

         Essa opção só estará disponível se você selecionou **Usar S/MIME**.  

    -   **Certificados de autenticação:** clique em **Selecionar** e selecione um certificado a ser usado para a assinatura. Essa opção é aplicável somente a dispositivos iOS.  

        > [!NOTE]  
        >  Antes de selecionar o certificado de assinatura, primeiro você deve configurá-lo como um perfil de certificado de protocolo de registro de certificado simples (SCEP). Para obter mais informações sobre perfis de certificado, consulte [Perfis de certificado do System Center Configuration Manager](introduction-to-certificate-profiles.md).  

         Essa opção só estará disponível se você selecionou **Usar S/MIME**.  

###   <a name="configure-synchronization-settings-for-the-exchange-activesync-email-profile"></a>Defina configurações de sincronização para o perfil de email do Exchange ActiveSync.  

1.  Na página **Definir configurações de sincronização** do Assistente de criação de perfil de email do Exchange ActiveSync, especifique as seguintes informações:  

    -   **Agendamento:** selecione o agendamento pelo qual os dispositivos sincronizarão os dados do Exchange Server. Essa opção é aplicável somente a dispositivos Windows Phone. Escolha:  

        -   **Não configurado** uma agenda de sincronização não é imposta. Isso permite aos usuários configurar suas próprias agendas de sincronização.  

        -   **Enquanto as mensagens chegam** dados como emails e itens de calendário serão sincronizados automaticamente quando chegam.  

        -   **15 minutos** dados como emails e itens de calendário serão automaticamente sincronizados a cada 15 minutos.  

        -   **30 minutos** Dados como emails e itens de calendário serão automaticamente sincronizados a cada 30 minutos.  

        -   **60 minutos** Dados como emails e itens de calendário serão automaticamente sincronizados a cada 60 minutos.  

        -   **Manual** a sincronização deve ser iniciada manualmente pelo usuário do dispositivo.  

    -   **Número de dias de email a ser sincronizado:** na lista suspensa, selecione o número de dias de email que deseja sincronizar. Selecione uma das seguintes opções:  

        -   **Não configurado** a configuração não é imposta. Isso permite que os usuários configurem como o email é baixado para o seu dispositivo.  

        -   **Ilimitado** sincroniza todas as mensagens disponíveis.  

        -   **1 dia**  

        -   **3 dias**  

        -   **1 semana**  

        -   **2 semanas**  

        -   **1 mês**  

    -   **Permitir que as mensagens sejam movidas para outras contas de email** Selecione esta opção para permitir que os usuários movam mensagens de email entre contas diferentes que podem estar configuradas em seu dispositivo. Essa opção é aplicável somente a dispositivos iOS.  

    -   **Permitir envio de email por meio de aplicativos de terceiros** Selecione esta opção para permitir que os usuários enviem e-mails de certos aplicativos de email não padrão, de terceiros. Essa opção é aplicável somente a dispositivos iOS.  

    -   **Sincronizar endereços de email usados recentemente** Selecione esta opção para sincronizar a lista de endereços de email usados recentemente no dispositivo. Essa opção é aplicável somente a dispositivos iOS.  

    -   **Usar SSL** Selecione esta opção para usar comunicação Secure Sockets Layer (SSL) ao enviar emails, recebendo emails e se comunicar com o Exchange Server.  

    -   **Tipo de conteúdo para sincronizar:** selecione os tipos de conteúdo que deseja sincronizar com dispositivos. Essa opção é aplicável somente a dispositivos Windows Phone. Escolha:  

        -   **Email**  

        -   **Contatos**  

        -   **Calendário**  

        -   **Tarefas**  

###  <a name="specify-supported-platforms-for-the-exchange-activesync-email-profile"></a>Especificar as plataformas com suporte para o perfil de email do Exchange ActiveSync.  

1.  Na página **Plataformas com Suporte** do Assistente de criação de perfil de email do Exchange ActiveSync, selecione os sistemas operacionais nos quais o perfil de email será instalado ou clique em **Selecionar todos** para instalar o perfil de email em todos os sistemas operacionais disponíveis.  

2.  Conclua o assistente.

Para obter informações sobre como implantar perfis de email do Exchange ActiveSync, consulte [Como implantar perfis no System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).  

