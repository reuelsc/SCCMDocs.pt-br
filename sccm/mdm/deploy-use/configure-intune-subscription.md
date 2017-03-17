---
title: Configurar sua assinatura do Intune usando o System Center Configuration Manager | Microsoft Docs
description: Configure sua assinatura do Intune usando o System Center Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99de8fe7-560e-401a-8ab2-6d87d091be17
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 10cc64ae7e4d91f53201c2896b359e77ef04d32d
ms.lasthandoff: 03/06/2017

---
# <a name="configure-your-intune-subscription-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar sua assinatura do Intune usando o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A assinatura do Intune permite gerenciar dispositivos pela Internet. Isso inclui especificar qual coleção de usuários pode registrar dispositivos e definir informações apresentadas aos usuários. Durante a criação da assinatura do Intune, você também pode adicionar a identidade visual da marca ao portal de empresa do Intune com o logotipo e esquema de cores personalizado de sua empresa.

A assinatura do Intune faz o seguinte:

-   Recupera o certificado que o ponto de conexão de serviço exige para se conectar ao serviço do Intune
-   Define a coleção de usuários que permite que os usuários registrem dispositivos móveis
-   Define e configura as plataformas móveis às quais você deseja dar suporte

> [!IMPORTANT]
>  A criação de uma assinatura do Microsoft Intune no Configuration Manager colocará o ponto de conexão de serviço de seu site no “modo online”. Confira [Sobre o ponto de conexão de serviço no System Center Configuration Manager](../../core/servers/deploy/configure/about-the-service-connection-point.md).

## <a name="to-create-the-microsoft-intune-subscription"></a>Para criar a assinatura do Microsoft Intune

1.  Se ainda não tiver uma, inscreva-se para obter uma conta do Microsoft Intune em [Microsoft Intune](http://go.microsoft.com/fwlink/?LinkID=258216).  Depois de criar sua conta do Intune, você não precisa adicionar nenhum usuário à conta do Intune ou executar configurações adicionais.

2.  No console do Configuration Manager, clique em **Administração**.

3.  No espaço de trabalho **Administração** , expanda **Serviços de Nuvem**e clique em **Assinaturas do Microsoft Intune**. Na guia **Início** , clique em **Adicionar Assinatura do Microsoft Intune**.

![Criar uma assinatura do Intune](../media/mdm-set-intune.png)

4.  Na página **Introdução** do Assistente para Criar Assinatura do Microsoft Intune, examine o texto e clique em **Próximo**.

5.  Na página **Assinatura** , clique em **Entrar** e entre usando sua conta empresarial ou de estudante. Na caixa de diálogo **Definir a autoridade de gerenciamento de dispositivos móveis**, marque a caixa de seleção para gerenciar apenas dispositivos móveis usando o Configuration Manager por meio do console do Configuration Manager. Para continuar sua assinatura, selecione essa opção.

    > [!IMPORTANT]
    >  Após selecionar o Configuration Manager como sua autoridade de gerenciamento, não será possível alterar futuramente a autoridade de gerenciamento para o Microsoft Intune.

6.  Clique nos links de privacidade para revisá-los e clique em **Próximo**.

7.  Na página **Geral** , especifique as seguintes opções e clique em **Próximo**.

  -   **Coleção**: especifique uma coleção de usuários que contém os usuários que registrarão seus dispositivos móveis.

      > [!NOTE]
      >  Se um usuário for removido da coleção, o dispositivo do usuário continuará a ser gerenciado por até 24 horas, quando o registro do usuário for removido do banco de dados de usuários.

  -   **Nome da empresa**: especifique o nome de sua empresa.

  -   **URL da documentação de privacidade**: se você publicar as informações de privacidade da sua empresa em um link acessível pela Internet, forneça um link que os usuários possam acessar pelo portal da empresa, por exemplo, http://www.contoso.com/CP_privacy.html. As informações de privacidade podem esclarecer quais informações os usuários estão compartilhando com sua empresa.

  -   **Esquema de cores do portal da empresa**: opcionalmente, troque a cor azul padrão pela cor dos portais da empresa.

  -   **Código do site do Configuration Manager**: especifica o código de um site primário para gerenciar os dispositivos móveis.

    > [!NOTE]
    >  Alterar o código do site afeta somente os novos registros e não afeta os dispositivos registrados existentes.

8.  Na página **Informações de Contato da Empresa**, especifique as informações de contato da empresa que são exibidas para os usuários em **Contatar TI** no aplicativo do Portal da Empresa. Forneça as informações de contato para a sua empresa e clique em **Próximo**.

9. Na página **Logotipo da Empresa**, você pode escolher se deseja exibir logotipos no portal da empresa e, em seguida, clicar em **Próximo**.

10. Conclua o assistente.

> [!div class="button"]
[< Etapa anterior](confirm-dns.md)  [Próxima etapa >](terms-and-conditions.md)

