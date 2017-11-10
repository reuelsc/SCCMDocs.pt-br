---
title: "Definições de malware do Endpoint Protection do compartilhamento de rede"
titleSuffix: Configuration Manager
description: "Aprenda como baixar manualmente as atualizações de definições mais recentes da Microsoft e configurar os clientes para baixar essas definições."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ddef4d2a-f481-4020-9ddd-9cca5f9795cb
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 3487238d7fdcd6e152bd5f578b20fb3fb5690978
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-a-network-share-for-configuration-manager"></a>Habilitar o download das definições de malware do Endpoint Protection de um compartilhamento de rede para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 Você pode baixar manualmente as atualizações de definições mais recentes da Microsoft e configurar os clientes para baixar essas definições de uma pasta compartilhada na rede. Os usuários também podem iniciar as atualizações de definições quando você usa essa origem de atualização.

> [!NOTE]
>  Os clientes devem ter acesso de leitura à pasta compartilhada para poder baixar as atualizações de definições.

 Para obter mais informações sobre como baixar as atualizações de definições e de mecanismos para armazenar no compartilhamento de arquivos, consulte [Instalar o software antimalware e antispyware mais recente da Microsoft](http://www.microsoft.com/security/portal/Definitions/HowToForeFront.aspx).

## <a name="to-configure-definition-downloads-from-a-file-share"></a>Para configurar downloads de definições de um compartilhamento de arquivo

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.

2.  No espaço de trabalho **Ativos e Conformidade** , expanda **Endpoint Protection**e clique em **Políticas Antimalware**.

3.  Abra a página de propriedades da **Política Antimalware Padrão** ou crie uma nova política antimalware. Para obter mais informações sobre como criar políticas antimalware, consulte [Como criar e implantar políticas antimalware para o Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md).

4.  Na seção **Atualizações de definições** da caixa de diálogo Propriedades antimalware, clique em **Definir Origem**.

5.  Na caixa de diálogo **Configurar Origens de Atualização de Definição** , selecione **Atualizações de compartilhamentos de arquivo UNC**.

6.  Clique em **OK** para fechar a caixa de diálogo **Configurar Origens de Atualização de Definição** .

7.  Clique em **Definir Caminhos**. Na caixa de diálogo **Configurar Caminhos UNC de Atualização de Definição** , adicione um ou mais caminhos UNC ao local dos arquivos das atualizações de definições em um compartilhamento de rede.

8.  Clique em **OK** para fechar a caixa de diálogo **Configurar Caminhos UNC de Atualização de Definição** .


> [!div class="button"]
[Próxima etapa >](endpoint-antimalware-policies.md)

> [!div class="button"]
[Voltar >](endpoint-configure-alerts.md)
