---
title: Criar um ponto de conexão de serviço
titleSuffix: Configuration Manager
description: Crie um ponto de conexão de serviço usando o System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 617abb22-d22f-41fb-a76b-1c4259e419d2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d0ce47e9ade73d76e99aa5c0d4e5581c713a847a
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62224821"
---
# <a name="create-a-service-connection-point-with-system-center-configuration-manager-and-microsoft-intune"></a>Criar um ponto de conexão de serviço com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Depois de criar a assinatura, é possível instalar a função do sistema de sites do ponto de conexão de serviço que permite que você se conecte ao serviço do Intune. Esta função do sistema de sites enviará por push as configurações e os aplicativos ao serviço do Intune.

 O ponto de conexão de serviço envia as configurações e informações da implantação de software para o Configuration Manager e recupera mensagens de status e inventário dos dispositivos móveis. O serviço Configuration Manager age como um gateway que se comunica com dispositivos móveis e armazena configurações.

> [!NOTE]
>  A função do sistema de sites do ponto de conexão de serviço só pode ser instalada em um site de administração central ou em um site primário autônomo. O ponto de conexão de serviço deve ter acesso à Internet.


## <a name="configure-the-service-connection-point-role"></a>Configurar a função do ponto de conexão de serviço

1.  No console do Configuration Manager, clique em **Administração**.

2.  No workspace **Administração**, expanda **Configuração de Site** e, em seguida, clique em **Funções de Servidores e do Sistema de Sites**.

3.  Adicione a função do **Ponto de conexão de serviço** a um servidor do sistema de sites novo ou existente usando a etapa associada:

    -   Novo servidor do sistema de site: No **Home** guia da **Create** , clique em **criar servidor do sistema de Site** para iniciar o Assistente para criação de servidor de sistema de Site.

    -   Servidor do sistema de site existente: Clique no servidor no qual você deseja instalar a função de ponto de conexão de serviço. Em seguida, na guia **Início** , no grupo **Servidor** , clique em **Adicionar Funções do Sistema de Site** para iniciar o Assistente para Adicionar Funções do Sistema de Site.

4.  Na página **Seleção de Função do Sistema** , selecione **Ponto de conexão de serviço**e clique em **Avançar**.
![Criar um ponto de conexão de serviço](../media/mdm-service-connection-point.png)

* Conclua o assistente.

## <a name="how-does-the-service-connection-point-authenticate-with-the-microsoft-intune-service"></a>Como o ponto de conexão de serviço é autenticado no serviço do Microsoft Intune?
 O ponto de conexão de serviço estende o Configuration Manager estabelecendo uma conexão com o serviço Intune baseado em nuvem, que gerencia dispositivos móveis pela Internet. O ponto de conexão de serviço é autenticado no serviço Intune da seguinte maneira:

1.  Ao criar uma assinatura do Intune no console do Configuration Manager, o administrador do Configuration Manager é autenticado pela conexão ao Azure Active Directory, que é redirecionada para o respectivo servidor ADFS para solicitar o nome de usuário e a senha. Em seguida, o Intune emite um certificado para o locatário.

2.  O certificado da etapa 1 é instalado na função do site do ponto de conexão de serviço e é usado para autenticar e autorizar toda a comunicação adicional com o serviço do Microsoft Intune.

> [!div class="button"]
> [< Etapa anterior](terms-and-conditions.md)  [Próxima etapa >](enable-platform-enrollment.md)
