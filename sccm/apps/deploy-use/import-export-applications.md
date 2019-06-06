---
title: Importar e exportar aplicativos
titleSuffix: Configuration Manager
description: Saiba como importar e exportar aplicativos no Configuration Manager para compartilhar entre hierarquias separadas.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: dba00e54-9d5b-4f6b-916d-ead48c66e288
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 02bb394de4f3bb947bdc2669a830167089c42311
ms.sourcegitcommit: 3f43fa8462bf39b2c18b90a11a384d199c2822d8
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66411005"
---
# <a name="import-and-export-applications"></a>Importar e exportar aplicativos

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use o Configuration Manager para importar e exportar aplicativos entre duas hierarquias. Por exemplo, copie um aplicativo de um ambiente de teste para um ambiente de produção.

## <a name="export"></a>Exportar

1. No console do Configuration Manager, selecione o nó **Aplicativos**. No grupo Criar da faixa de opções, escolha **Exportar Aplicativo**.
1. Na tela **Geral**, insira o caminho para um novo arquivo zip no qual exportar. Opcionalmente, especifique se deve exportar *dependências, relações de substituição, condições e ambientes virtuais*, bem como *conteúdo para os aplicativos e as dependências selecionados*.  Insira os comentários do administrador, se desejado, e selecione **Avançar**.
1. Verifique se o aplicativo e todas as dependências estão listadas na página **Objetos Relacionados** e selecione **Avançar**.
1. Na página Resumo, selecione **Avançar**.
1. Quando o processo for concluído, ele criará o arquivo ZIP e você poderá fechar o assistente.

> [!IMPORTANT]
> Se você pretende copiar este aplicativo para outro ambiente, pegue arquivo zip e a pasta que o acompanha. O arquivo zip deve existir no mesmo diretório que a pasta criada.

## <a name="import"></a>Importar

> [!NOTE]
> Você pode importar apenas os aplicativos de caminhos UNC, mas não pode importar diretamente do seu disco local.

1. No console do Configuration Manager, selecione o nó **Aplicativos**. No grupo Criar da faixa de opções, escolha **Importar Aplicativo**.
1. Escolha o arquivo zip que você deseja importar e selecione **Avançar**.
1. A janela Conteúdo do Arquivo mostra o que acontece quando você importa o aplicativo. Selecione **Avançar**.
1. Examine a tela de resumo e selecione **Avançar**.
1. Feche o assistente. O aplicativo agora está disponível no site.

## <a name="see-also"></a>Consulte também
 
Automatize a importação e exportação de aplicativos usando o PowerShell.

* [Import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication)
* [Export-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/export-cmapplication)
