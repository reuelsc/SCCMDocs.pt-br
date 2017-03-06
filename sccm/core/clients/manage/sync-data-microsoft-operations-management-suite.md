---
title: "Sincronização de dados | Microsoft Docs | Microsoft Operations Management Suite "
description: Sincronizar dados do System Center Configuration Manager com o Microsoft Operations Management Suite.
ms.custom: na
ms.date: 10/13/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
caps.latest.revision: 9
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 0d8944bef9578a41b529a2d53b5a4d0094eaa21c
ms.lasthandoff: 12/16/2016

---
# <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite"></a>Sincronizar dados do Configuration Manager com o Microsoft Operations Management Suite

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

É possível usar o Conector do Microsoft OMS (Operations Management Suite) para sincronizar dados como suas coleções do System Center Configuration Manager com o OMS. Isso torna dados de sua implantação do Configuration Manager visíveis no OMS.

## <a name="add-an-oms-connection-to-configuration-manager"></a>Adicionar uma conexão do OMS ao Configuration Manager

Para adicionar uma conexão do OMS, seu ambiente do Configuration Manager deve configurar primeiro um [ponto de conexão de serviço](../../../core/servers/deploy/configure/about-the-service-connection-point.md) em um [modo online](https://azure.microsoft.com/en-us/documentation/articles/resource-group-create-service-principal-portal/). Quando você adiciona uma conexão do OMS ao seu ambiente, ele também instalará o Microsoft Monitoring Agent no computador que executa essa função de sistema de sites.
1.  No espaço de trabalho **Administração**, selecione **Conector OMS**. Na faixa de opções, clique em "Criar conexão com o Operations Management Suite". Isso abre o **Assistente de Conexão com o Operation Management Suite**. Selecione **Avançar**.
2.  Na tela **Geral**, confirme que você tem as seguintes informações e selecione **Avançar**.

    * Registrou o Configuration Manager como uma ferramenta de gerenciamento "Aplicativo Web e/ou API Web" e que você tem a [ID de cliente desse registro](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
    * Criou uma chave de cliente para a ferramenta de gerenciamento registrada no Azure Active Directory.
    * No Portal de gerenciamento do Azure, forneceu o aplicativo Web registrado com permissão para acessar o OMS, conforme descrito em [Fornecer o Configuration Manager com permissões para OMS](https://azure.microsoft.com/en-us/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms).

3.  Na tela **Azure Active Directory**, defina as configurações de conexão do OMS, fornecendo seu **Locatário**, sua **ID do cliente** e sua **Chave secreta do cliente** e, em seguida, selecione **Avançar**.
4.  Na tela **Configuração de Conexão do OMS**, forneça as suas configurações de conexão preenchendo sua **assinatura do Azure**, **grupo de recursos do Azure** e **espaço de trabalho do Operations Management Suite**.
5.  Verifique suas configurações de conexão na tela **Resumo** e, em seguida, selecione **Avançar**. A tela **Andamento** mostrará o status da conexão e, em seguida, clique em **Concluir**.

> [!NOTE]
> É necessário conectar o OMS no site de nível superior na sua hierarquia. Se você conectar o OMS a um site primário autônomo e, em seguida, adicionar um site de administração central ao seu ambiente, será necessário excluir e recriar a conexão do OMS dentro da nova hierarquia.

Depois de vincular o Configuration Manager ao OMS, será possível adicionar ou remover coleções e exibir as propriedades da conexão do OMS.

## <a name="viewing-microsoft-operations-management-suite-connection-properties-in-configuration-manager"></a>Exibindo propriedades de conexão do Microsoft Operations Management Suite no Configuration Manager

1.  Navegue até **Serviços em Nuvem**, em seguida, selecione **Conector OMS** para abrir a página **Propriedades de Conexão do OMS**.
2.  Nessa página, há duas guias:
  * A guia **Azure Active Directory Azure** mostra seu **Locatário**, sua **ID do cliente**, a **Expiração da Chave Secreta do Cliente** e permite que você **Verifique** se sua **Chave Secreta do Cliente** expirou.
  * A guia **Propriedades de Conexão do OMS** mostra sua **Assinatura do Azure**, **grupo de recursos do Azure**, **Espaço de Trabalho do Operations Management Suite** e uma lista de **Coleções de dispositivos para os quais o Operations Management Suite pode obter dados**. Use os botões **Adicionar** e **Remover** para modificar quais coleções são permitidas.

