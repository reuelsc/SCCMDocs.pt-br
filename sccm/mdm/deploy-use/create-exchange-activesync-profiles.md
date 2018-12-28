---
title: Criar perfis de email do Exchange ActiveSync
titleSuffix: Configuration Manager
description: Saiba como criar e configurar perfis de email no System Center Configuration Manager que funcionam com o Microsoft Intune.
ms.date: 07/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 120442be-179e-450c-a0c4-284046895da3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: decd16a03a0381718ada3e4c977d10c159c6be25
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417057"
---
# <a name="exchange-activesync-email-profiles-in-system-center-configuration-manager"></a>Perfis de email do Exchange ActiveSync no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch atual)*

Usando o Microsoft Intune e o Exchange ActiveSync, você pode configurar dispositivos com restrições e perfis de email. Isso permite que os usuários acessem o email corporativo em seus dispositivos com uma configuração mínima exigida de sua parte.  

 Você pode configurar os seguintes tipos de dispositivo com perfis de email:  

- Windows 10
- Windows Phone 8.1
- iPhones que executam o iOS 9 e posterior 
- iPads que executam o iOS 9 e posterior 
- Samsung KNOX Standard (4 e posterior)
- Android for Work

Para implantar perfis de email nos dispositivos, você deve registrar os dispositivos no Intune. Para obter informações sobre como registrar seus dispositivos, veja [Gerenciar dispositivos móveis com o Microsoft Intune](https://technet.microsoft.com/library/dn646962.aspx).

> [!NOTE]
> O Intune fornece dois perfis de email do Android for Work, um para o aplicativo de email Gmail e outro para o aplicativo de email Nine Work. Esses aplicativos estão disponíveis no Google Play Store e dão suporte às conexões com o Exchange. Para habilitar a conectividade de email, implante esses aplicativos de email nos dispositivos de seus usuários e, em seguida, crie e implante o perfil apropriado. Os aplicativos de email, como Nine Work, podem não ser gratuitos. Examine os detalhes de licenciamento do aplicativo ou entre em contato com a empresa do aplicativo se tiver dúvidas.

 Além de configurar uma conta de email no dispositivo, você também pode definir as configurações de sincronização para os contatos, calendários e tarefas.  

 Ao criar um perfil de email, você pode incluir várias configurações de segurança. Essas configurações incluem os certificados de identidade, criptografia e assinatura que foram configurados usando os perfis de certificado do System Center Configuration Manager. Para obter mais informações sobre perfis de certificado, consulte [Perfis de certificado do System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles.md).    

## <a name="create-an-exchange-activesync-email-profile"></a>Criar um perfil de email do Exchange ActiveSync  

Para criar um perfil, use o Assistente para Criar Perfil de Email do Exchange ActiveSync. 

1. No console do Configuration Manager, escolha **Ativos e Conformidade**.  

2. No workspace **Ativos e Conformidade**, expanda **Configurações de Conformidade**, expanda **Acesso aos Recursos da Empresa**e escolha **Perfis de Email**.  

3. Na guia **Início**, no grupo **Criar**, escolha **Criar Perfil de Email do Exchange ActiveSync** para iniciar o assistente.

4. Na página **Geral** do assistente, configure o seguinte:

   - **Nome**. Forneça um nome descritivo para o perfil de email.

   - **Descrição**. Opcionalmente, forneça uma descrição para o perfil de email que ajudará a identificá-lo no console do Configuration Manager.

   - **Este perfil de email é para o Android for Work**. Escolha esta opção se você implantar o perfil de email para os dispositivos Android for Work somente. Se marcar esta caixa, a página do assistente de **Plataformas Suportadas** não será exibida. Apenas perfis de email do Android for Work são configurados.

5. Na página **Exchange ActiveSync** do assistente, especifique as seguintes informações:  

   - **Host do Exchange ActiveSync**. Especifique o nome de host do servidor Exchange da empresa que hospeda os serviços do Exchange ActiveSync.  

   - **Nome da conta**. Especifique o nome de exibição para a conta de email, como será exibido para os usuários em seus dispositivos.  

   - **Nome de usuário da conta**. Escolha como o nome de usuário da conta de email é configurado nos dispositivos cliente. Você pode escolher uma das seguintes opções na lista suspensa:  

     -   **Nome Principal do Usuário**. Use o nome principal do usuário completo para entrar no Exchange.  

     -   **AccountName**. Use o nome da conta de usuário completo no Active Directory.

     -   **Endereço SMTP Primário**. Use o endereço SMTP primário do usuário para entrar no Exchange.  

   - **Endereço de email**. Escolha como o endereço de email do usuário em cada dispositivo cliente é gerado. Você pode escolher uma das seguintes opções na lista suspensa:  

     -   **Endereço SMTP Primário**. Use o endereço SMTP primário do usuário para entrar no Exchange.  

     -   **Nome Principal do Usuário**. Use o nome principal do usuário completo como o endereço de email.  

   - **Domínio da conta**. Selecione uma das seguintes opções:  

     - **Obter do Active Directory**  

     - **Personalizado**  

       Esse campo só será aplicável se **sAMAccountName** for selecionado na lista suspensa **Nome de usuário da conta**.  

   - **Método de autenticação**. Escolha um dos seguintes métodos de autenticação que serão usados para autenticar a conexão com o Exchange ActiveSync:  

     -   **Certificados**. Um certificado de identidade será usado para autenticar a conexão do Exchange ActiveSync.  

     -   **Nome de usuário e Senha**. O usuário do dispositivo deve fornecer uma senha para conectar o Exchange ActiveSync. (O nome de usuário é configurado como parte do perfil de email.)  

   - **Certificado de identidade**. Escolha **Selecionar**, em seguida, escolha um certificado a ser usado para a identidade.  

      Os certificados de identidade devem ser certificados SCEP; não é possível usar um certificado PFX.  Para saber mais, confira [Perfis de certificado no System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

      Essa opção só estará disponível se você escolheu **Certificados** no **Método de autenticação**.  

   - **Use S/MIME**. Envie um email de saída usando a criptografia S/MIME. Essa opção é aplicável somente a dispositivos iOS. Escolha dentre as seguintes opções:

     - **Certificados de assinatura**.  Escolha **Selecionar**, depois, escolha um perfil de certificado para usar para criptografia.  

       O perfil pode ser um certificado SCEP ou PFX.  No entanto, se a assinatura e a criptografia forem usadas, você deverá selecionar os perfis de certificado PFX para *assinatura e criptografia*.

     - **Certificados de criptografia**. Escolha **Selecionar**, em seguida, escolha um certificado a usar para a criptografia. Você só pode escolher um certificado PFX para usar como um certificado de criptografia.

     - Para criptografar todas as mensagens em dispositivos iOS, marque a caixa de seleção **Exigir criptografia**.    

       Você deve criar perfis de certificado antes de poder escolhê-los aqui.  Para saber mais, confira [Perfis de certificado no System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

## <a name="configure-synchronization-settings-for-the-exchange-activesync-email-profile"></a>Defina as configurações de sincronização para o perfil de email do Exchange ActiveSync  

Na página **Definir configurações de sincronização** do Assistente de criação de perfil de email do Exchange ActiveSync, especifique as seguintes informações:  

-   **Agendamento**. Escolha a agenda pela qual os dispositivos sincronizarão os dados do Exchange Server. Essa opção é aplicável somente a dispositivos Windows Phone. Escolha:  

    -   **Não Configurado**. Uma agenda de sincronização não é imposta. Isso permite que os usuários configurem sua própria agenda de sincronização.  

    -   **Quando as mensagens chegam**. Dados como emails e itens de calendário serão sincronizados automaticamente quando chegarem.  

    -   **15 minutos**. Dados como emails e itens de calendário serão sincronizados automaticamente a cada 15 minutos.  

    -   **30 minutos**. Dados como emails e itens de calendário serão sincronizados automaticamente a cada 30 minutos.  

    -   **60 minutos**. Dados como emails e itens de calendário serão sincronizados automaticamente a cada 60 minutos.  

    -   **Manual**. O usuário do dispositivo deve iniciar a sincronização manualmente.  

-   **Número de dias de email para sincronizar**. Na lista suspensa, escolha o número de dias de email que você deseja sincronizar. Selecione uma das seguintes opções:  

    -   **Não Configurado**. A configuração não é imposta. Isso permite que os usuários configurem quanto email é baixado para seu dispositivo.  

    -   **Ilimitado**. Sincronize todos os emails disponíveis.  

    -   **1 dia**  

    -   **3 dias**  

    -   **1 semana**  

    -   **2 semanas**  

    -   **1 mês**  

-   **Permita que as mensagens sejam movidas para outras contas de email**. Escolha esta opção para permitir que os usuários movam mensagens de email entre as diferentes contas configuradas em seu dispositivo. Essa opção é aplicável somente a dispositivos iOS.  

-   **Permita que um email seja enviado de aplicativos de terceiros**. Escolha esta opção para permitir que os usuários enviem email de certos aplicativos de email não padrão de terceiros. Essa opção é aplicável somente a dispositivos iOS.  

-   **Sincronize os endereços de email usados recentemente**. Escolha esta opção para sincronizar a lista de endereços de email usados recentemente no dispositivo. Essa opção é aplicável somente a dispositivos iOS.  

-   **Use SSL**. Escolha esta opção para usar a comunicação Secure Sockets Layer (SSL) para enviar emails, receber emails e comunicar-se com o Exchange Server.  

-   **Tipo de conteúdo a sincronizar**. Escolha os tipos de conteúdo que você deseja sincronizar com os dispositivos. Essa opção é aplicável somente a dispositivos Windows Phone. Escolha:  

    -   **Email**  

    -   **Contatos**  

    -   **Calendário**  

    -   **Tarefas**  

## <a name="specify-supported-platforms-for-the-exchange-activesync-email-profile"></a>Especificar as plataformas com suporte para o perfil de email do Exchange ActiveSync  

1.  Na página **Plataformas Suportadas** do Assistente para Criar Perfil de Email do Exchange ActiveSync, escolha os sistemas operacionais nos quais o perfil de email será instalado. Ou escolha **Selecionar tudo** para instalar o perfil de email em todos os sistemas operacionais disponíveis.  

2.  Conclua o assistente.

Para obter informações sobre como implantar perfis de email do Exchange ActiveSync, consulte [Como implantar perfis no System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).  
