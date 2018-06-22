---
title: Configurar os aplicativos Android for Work com as políticas de configuração
titleSuffix: Configuration Manager
description: Ajude a eliminar problemas de configuração em dispositivos que executam o Android for Work ao implantar políticas de configuração de aplicativo para os usuários antes que eles executem aplicativos.
ms.date: 09/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9126d188-7780-45a4-b21d-7fcf4fad7da2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79ab2548453c84cfff7450574ed46562d7c1a005
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32348174"
---
# <a name="apply-settings-to-android-for-work-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>Aplicar configurações a aplicativos Android for Work com políticas de configuração de aplicativo no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode usar políticas de configuração de aplicativo no System Center Configuration Manager para distribuir configurações que podem ser necessárias quando um usuário executa um aplicativo. Por exemplo, um aplicativo pode exigir que um usuário especifique estes detalhes:
- Um número de porta personalizado
- Configurações de idioma
- Configurações de segurança
- Configurações de identidade visual, como um logotipo da empresa

Se o usuário inserir as configurações incorretamente, a correção poderá sobrecarregar o suporte técnico e a implantação do aplicativo ficará lenta. Para evitar esses problemas, você pode usar políticas de configuração de aplicativo para implantar as configurações necessárias para os usuários antes que eles executem o aplicativo. As configurações são associadas a um usuário automaticamente. O usuário não precisa executar nenhuma ação.
Em vez de implantar as políticas de configuração diretamente para o usuários e dispositivos, você associa uma política a um tipo de implantação ao implantar o aplicativo. As configurações de política são aplicadas sempre que o aplicativo as verifica, normalmente, na primeira vez em que o aplicativo é executado.

As políticas de configuração de aplicativo do Android estão disponíveis somente em dispositivos com Android for Work. As políticas de configuração de aplicativo se aplicam a aplicativos aprovados pela Play for Work Store. Para obter detalhes sobre os aplicativos Android adquiridos por volume, confira [Como implantar aplicativos em dispositivos Android for Work](https://docs.microsoft.com/intune/deploy-use/android-for-work-apps).

Para obter mais informações sobre os tipos de instalação de aplicativos, consulte a [introdução ao gerenciamento de aplicativos](/sccm/apps/understand/introduction-to-application-management).

## <a name="create-an-app-configuration-policy"></a>Criar uma política de configuração do aplicativo

1. No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Políticas de Configuração de Aplicativo**.
2. Na guia **Página Inicial**, no grupo **Políticas de Configuração de Aplicativo**, escolha **Criar Política de Configuração de Aplicativo**.
3. No Assistente para Criar Política de Configuração de Aplicativo, na página **Geral** defina estas informações de política:
  - **Nome**. Insira um nome exclusivo para a política.
  - **Descrição**. (Opcional) Para facilitar a identificação da política, você pode adicionar uma descrição.
  -  **Selecione um tipo de política de configuração**. Especifique a plataforma de destino com a política de configuração de aplicativo: **Política de configuração para os aplicativos do Android for Work**.
  -  **Categorias atribuídas para melhorar a pesquisa e a filtragem**. (Opcional) Para criar e atribuir categorias para a política, escolha **Categorias**. As categorias facilitam a classificação e a localização de itens no console do Configuration Manager.
4. Na página **Política do Android for Work**, escolha como definir as informações da política de configuração:
  - **Especificar pares nome-valor**. Você pode usar essa opção para arquivos de lista de propriedades que não usam aninhamento. Para especificar um par nome e valor:
        1. Para adicionar um novo par JSON, escolha **Novo**.
        2. Na caixa de diálogo **Adicionar Par Nome/Valor**, especifique os seguintes detalhes:
            - **Tipo**. Na lista, selecione o tipo de valor que deseja especificar.
            - **Nome**. Insira o nome da chave de lista de propriedades para o qual deseja especificar um valor.
            - **Valor**. Insira o valor que será aplicado à chave inserida.

  - **Navegue até um arquivo JSON de lista de propriedades**. Use essa opção se você já tiver um arquivo JSON de configuração de aplicativo ou para arquivos mais complexos que usam aninhamento. No campo **Política de configuração de aplicativo**, insira as informações da lista de propriedades no formato JSON correto.
5. Para importar um arquivo JSON que você criou anteriormente, escolha **Selecionar arquivo**.
6. Escolha **Próxima**. Se houver erros no código JSON, corrija-os antes de continuar.
7. Conclua as etapas mostradas no assistente.

A nova política de configuração de aplicativo é mostrada no espaço de trabalho **Biblioteca de Software**, no nó **Políticas de Configuração de Aplicativo**.

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>Associar uma política de configuração de aplicativo a um aplicativo do Gerenciador de Configurações

Para associar uma política de configuração de aplicativo à implantação de um aplicativo Android for Work, implante o aplicativo da maneira normal, usando o procedimento no tópico [Implantar aplicativos](/sccm/apps/deploy-use/deploy-applications).

No Assistente para Implantar Software, na página **Políticas de configuração de aplicativo**, escolha **Novo**. Na caixa de diálogo **Selecionar Política de Configuração de Aplicativo**, escolha um tipo de implantação de aplicativo e a política de configuração de aplicativo à qual deseja associá-lo.
Quando o tipo de implantação for instalado, as definições da política de configuração de aplicativo serão aplicadas automaticamente.
