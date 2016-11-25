---
title: Configurar registro de dispositivos | MDM local | System Center Configuration Manager
description: "Conceda permissão aos usuários para registrarem seus dispositivos para o Gerenciamento de Dispositivo Móvel Local no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ffaea91-1379-4b86-9953-b25e152f56a9
caps.latest.revision: 10
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: ddbb5648002adb8cf9249febb23797ee71d8a026


---
# <a name="set-up-device-enrollment-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Configurar o registro de dispositivo para o gerenciamento de dispositivo móvel local no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Permitir que os usuários registrem seus próprios dispositivos no Gerenciamento de Dispositivo Móvel Local do System Center Configuration Manager requer conceder a eles permissão para fazer isso. Para conceder aos usuários permissão para registrar dispositivos, execute as tarefas a seguir.

-   [Crie um perfil de registro que permite que os usuários registrem os dispositivos modernos](#bkmk_createProf)  

-   [Configurar definições de cliente adicionais para dispositivos registrados](#bkmk_addClient)  

-   [Permitir que os usuários recebam o perfil de registro de dispositivo moderno](#bkmk_enableUsers)  

-   [Armazenar o certificado raiz em dispositivos que serão registrados](#bkmk_storeCert)  

##  <a name="a-namebkmkcreateprofa-create-an-enrollment-profile-that-allows-users-to-enroll-modern-devices"></a><a name="bkmk_createProf"></a> Crie um perfil de registro que permite que os usuários registrem os dispositivos modernos  
 Para enviar as configurações necessárias por push para permitir que os usuários registrem os dispositivos modernos, você pode adicionar um novo perfil de registro para as configurações padrão, que é aplicado em todos os usuários descobertos no site do Configuration Manager.  

1.  No console do Configuration Manager, clique em **Administração** > **Visão Geral** > **Configurações do Cliente**, abra **Configurações do Cliente Padrão** e selecione **Registro**.  

2.  Em Configurações do Dispositivo, especifique o intervalo de sondagem para dispositivos modernos.  

3.  Em Configurações de Usuário, selecione **Sim** para **Permitir que os usuários registrem os dispositivos modernos**.  

4.  Ao lado do **Perfil de registro de dispositivo moderno**, clique em **Definir perfil...** e em **Criar...**  

5.  Em Criar Perfil de Registro, digite um nome para o perfil de registro e escolha o código do site de gerenciamento que deseja que os usuários com o perfil de registro usem. Clique em **OK** várias vezes para sair da página Configurações Padrão.  

> [!NOTE]  
>  Se você deseja implantar o perfil de registro para um subconjunto de usuários descobertos, você pode usar uma coleção de usuários e criar configurações personalizadas para implantar nessa coleção. Para obter informações sobre como criar configurações personalizadas do cliente, veja [How to configure client settings in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md)  

##  <a name="a-namebkmkaddclienta-set-up-additional-client-settings-for-enrolled-devices"></a><a name="bkmk_addClient"></a> Configurar definições de cliente adicionais para dispositivos registrados  
 Além de configurar o perfil de registro para dispositivos modernos, você pode configurar definições de cliente adicionais para configurar dispositivos quando eles estiverem registrados.  Para obter informações sobre como definir configurações do cliente, veja [Como definir as configurações do cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

 Nem todas as configurações do cliente estão disponíveis para o Gerenciamento de Dispositivo Móvel Local. O branch atual do Configuration Manager dá suporte às seguintes configurações de cliente para o Gerenciamento de Dispositivo Móvel Local:  

-   Registro: essas configurações especificam o perfil de registro de dispositivos gerenciados. Para obter mais informações sobre como configurar um perfil de registro, consulte [Criar um perfil de registro que permite que os usuários registrem os dispositivos modernos](#bkmk_createProf).  

-   Política do cliente: essas configurações especificam a frequência para baixar a política do cliente no dispositivo. Você também pode habilitar as configurações para segmentar usuários com a sondagem da política. Para obter mais informações sobre as configurações de políticas do cliente, consulte [Sobre as configurações do cliente no System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

-   Implantação de software: essa configuração define o intervalo para avaliar os dispositivos do cliente para implantações de software. Para obter mais informações sobre as configurações de implantação de software, consulte a seção Implantação de Software em [Sobre as configurações do cliente no System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md)  

    > [!NOTE]  
    >  Para o Gerenciamento de Dispositivo Móvel Local, as configurações de implantação de software podem ser usadas somente como configurações padrão do cliente. As configurações de implantação de software não podem ser usadas com configurações personalizadas do cliente no branch atual do Configuration Manager.  

##  <a name="a-namebkmkenableusersa-enable-users-to-receive-the-modern-device-enrollment-profile"></a><a name="bkmk_enableUsers"></a> Permitir que os usuários recebam o perfil de registro de dispositivo moderno  
 Para que os usuários recebam as configurações do cliente modificadas com o perfil de registro para o Gerenciamento de Dispositivo Móvel Local, eles devem ser descobertos por meio do método de descoberta do Active Directory. Para se certificar de que todas as pessoas que precisam do perfil de registro vão obtê-lo, execute a descoberta de usuários do Active Directory. Para obter instruções sobre como descobrir usuários, veja [Run discovery for System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md).  

##  <a name="a-namebkmkstorecerta-store-the-root-certificate-on-devices-to-be-enrolled"></a><a name="bkmk_storeCert"></a> Armazenar o certificado raiz em dispositivos que serão registrados  
 Os usuários com dispositivos que ingressaram no domínio provavelmente já terão o certificado raiz necessário para a comunicação confiável com os servidores que hospedam as funções do sistema de site porque a raiz foi emitida como parte do processo de domínio associado com o Active Directory. Os computadores e dispositivos móveis não associados ao domínio terão o certificado raiz instalado manualmente no dispositivo para permitir que o registro ocorra. Esses dispositivos não terão o certificado raiz necessário automaticamente.  

 O arquivo de certificado exportado deve ser fornecido para o dispositivo para instalação manual. Isso pode ser feito usando email, OneDrive, cartão SD, pen drive USB ou qualquer método que funcione melhor para suas necessidades.  

 O certificado raiz que você deseja usar nos dispositivos é aquele que você exportou em [Exportar o certificado com a mesma raiz do certificado do servidor Web](../../mdm/get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert).  

1.  No dispositivo a ser registrado, localize o arquivo do certificado raiz e clique duas vezes nele.  

2.  Na janela Certificado, clique em **Instalar Certificado...**  

3.  No Assistente para Importação de Certificados, selecione o **Computador Local**e clique em **Avançar**.  

4.  Na janela Controle de Conta de Usuário, clique em **Sim**.  

5.  Selecione **Colocar todos os certificados no repositório a seguir**e clique em **Procurar**.  

6.  Clique em **Autoridades de Certificação Raiz Confiáveis**, clique em **OK**e, em seguida, clique em **Avançar**.  

7.  Clique em **Finalizar**.  



<!--HONumber=Nov16_HO1-->


