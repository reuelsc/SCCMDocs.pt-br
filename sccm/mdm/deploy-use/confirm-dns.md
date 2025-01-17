---
title: Confirmar requisitos de nome de domínio
titleSuffix: Configuration Manager
description: Confirme requisitos de nome de domínio usando o System Center Configuration Manager.
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 522c2e82-20eb-4f38-859b-d55640b24e32
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0e80a001153012763f56686df66ab7c6fcbf9b88
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62288195"
---
# <a name="confirm-domain-name-requirements-with-system-center-configuration-manager-and-microsoft-intune"></a>Confirmar requisitos de nome de domínio com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Se for necessário, execute as seguintes etapas para satisfazer quaisquer dependências externas para o Configuration Manager:

1. Cada usuário deve ter uma licença do Intune atribuída para registrar dispositivos. Para associar as licenças do Intune aos usuários, cada usuário deve ter um nome UPN que possa ser publicamente resolvido (por exemplo, johndoe@contoso.com) ou uma ID de logon alternativa configurada no Azure Active Directory. A configuração de uma ID de logon alternativa permite que os usuários se conectem com um endereço de email, por exemplo, mesmo se seu UPN está em um formato de NetBIOS (por exemplo, CONTOSO\johndoe).

   - Se sua empresa usa UPNs resolvíveis publicamente (ou seja, johndoe@contoso.com), nenhuma configuração adicional é necessária.
   - Se sua empresa usa um UPN não resolvível (ou seja, CONTOSO\johndoe), você deve [configurar uma ID alternativa no Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#pages-under-the-section-sync).

2. Implante e configure os Serviços de Federação do Active Directory (AD FS). (Opcional)

    Quando você configura logon único, seus usuários podem se conectar com as credenciais corporativas deles para acessar os serviços no Intune.

    Para mais informações, consulte os seguintes tópicos:
   -   [Preparar-se para o logon único](http://go.microsoft.com/fwlink/?LinkID=271124)
   -   [Planejar e implantar o AD FS 2.0 para uso com logon único](http://go.microsoft.com/fwlink/?LinkID=271125)

3. Implantar e configurar a sincronização de diretório.

    A sincronização de diretório permite que você popule o Intune com contas de usuário sincronizadas. As contas de usuários sincronizadas e os grupos de segurança são adicionados ao Intune. A falha ao habilitar a Sincronização de Diretório é uma causa comum de os dispositivos não poderem ser registrados na configuração do MDM do Configuration Manager com o Microsoft Intune.

    Para mais informações, consulte [Integração de diretório](http://go.microsoft.com/fwlink/?LinkID=271120) na biblioteca de documentação do Active Directory.

4. Opcional, mas não recomendado: Se você não estiver usando os serviços de Federação do Active Directory, redefina as senhas dos usuários Online da Microsoft.

    Se você não estiver usando o AD FS, você deve definir uma senha online da Microsoft para cada usuário.

> [!div class="button"]
> [< Etapa anterior](create-mdm-collection.md)  [Próxima etapa >](configure-intune-subscription.md)
