---
title: Definições de malware do Endpoint Protection do compartilhamento de rede
titleSuffix: Configuration Manager
description: Aprenda como baixar manualmente as atualizações de definições mais recentes da Microsoft e configurar os clientes para baixar essas definições.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ddef4d2a-f481-4020-9ddd-9cca5f9795cb
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2dbe2c5ecfbf58248f1bc391d39d6e0b86b86bc2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140449"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-a-network-share-for-configuration-manager"></a>Habilitar o download das definições de malware do Endpoint Protection de um compartilhamento de rede para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 Você pode baixar manualmente as atualizações de definições mais recentes da Microsoft e configurar os clientes para baixar essas definições de uma pasta compartilhada na rede. Os usuários também podem iniciar as atualizações de definições quando você usa essa origem de atualização.

> [!NOTE]
>  Os clientes devem ter acesso de leitura à pasta compartilhada para poder baixar as atualizações de definições.

 Para obter mais informações sobre como baixar as atualizações de definições e de mecanismos para armazenar no compartilhamento de arquivos, consulte [Instalar o software antimalware e antispyware mais recente da Microsoft](https://www.microsoft.com/wdsi/definitions).

## <a name="to-configure-definition-downloads-from-a-file-share"></a>Para configurar downloads de definições de um compartilhamento de arquivo

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.

2.  No workspace **Ativos e Conformidade**, expanda **Endpoint Protection** e clique em **Políticas Antimalware**.

3.  Abra a página de propriedades da **Política Antimalware Padrão** ou crie uma nova política antimalware. Para obter mais informações sobre como criar políticas antimalware, consulte [Como criar e implantar políticas antimalware para o Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md).

4.  Na seção **Atualizações de definições** da caixa de diálogo Propriedades antimalware, clique em **Definir Origem**.

5.  Na caixa de diálogo **Configurar Origens de Atualização de Definição** , selecione **Atualizações de compartilhamentos de arquivo UNC**.

6.  Clique em **OK** para fechar a caixa de diálogo **Configurar Origens de Atualização de Definição** .

7.  Clique em **Definir Caminhos**. Na caixa de diálogo **Configurar Caminhos UNC de Atualização de Definição** , adicione um ou mais caminhos UNC ao local dos arquivos das atualizações de definições em um compartilhamento de rede.

8.  Clique em **OK** para fechar a caixa de diálogo **Configurar Caminhos UNC de Atualização de Definição** .


> [!div class="button"]
> [Próxima etapa >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Voltar >](endpoint-configure-alerts.md)
