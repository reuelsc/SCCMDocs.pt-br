---
title: Solucionar problemas de implantações de aplicativo
titleSuffix: Configuration Manager
description: Dicas para solucionar problemas de implantação de aplicativos no System Center Configuration Manager
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4e8b46a3-3e11-475f-a4d7-6bf9ddf14145
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 75dcf2d4ae69c2181fecde0c04359faa46753e88
ms.sourcegitcommit: 3f43fa8462bf39b2c18b90a11a384d199c2822d8
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66411015"
---
# <a name="troubleshoot-application-deployments"></a>Solucionar problemas de implantação do aplicativo

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Problemas típicos com implantações de aplicativos se enquadram em uma das seguintes categorias:

- Falhas de download do aplicativo

- Conformidade de implantação do aplicativo parada em 0%

Se você tiver qualquer um desses problemas, este artigo fornecerá algumas etapas que você pode usar para solucionar problemas.


## <a name="download-failures"></a>Falhas de download

As falhas de download do aplicativo incluem os seguintes problemas:

- O cliente está parado baixando um aplicativo

- O cliente falha ao baixar o conteúdo do aplicativo

- O cliente fica parado em 0% ao baixar o aplicativo

A primeira coisa a ser verificada ao enfrentar falhas de download de aplicativo é se há limites grupos de limites ausentes ou configurados incorretamente. Por exemplo, se o cliente estiver na intranet e não configurado para o gerenciamento de clientes apenas da Internet, seu local de rede deverá estar em um limite configurado. Também deve haver um grupo de limites atribuído a esse limite para o cliente baixar o conteúdo. Para obter mais informações, confira [Definir limites e grupos de limites do site](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups).

Se você não puder configurar um limite para um cliente ou se um grupo de limites específico não puder ser um membro de outro grupo de limites:

1. No console do Configuration Manager, abra as propriedades do **Tipo de Implantação**.  

1. Alterne para a guia **Conteúdo**.

1. Na seção para usar um ponto de distribuição de um grupo de limites vizinho ou o grupo de limites de site padrão, altere as **Opções de implantação** para **Baixar conteúdo do ponto de distribuição e executar localmente**. (Por padrão, essa configuração é **Não baixar conteúdo**.)

Se o cliente não puder baixar o conteúdo do aplicativo, verifique se que ele é distribuído para um ponto de distribuição. Para verificar essa configuração, use os recursos no console para monitorar a distribuição do conteúdo para os pontos de distribuição. Para obter mais informações, consulte [Monitorar o conteúdo que você distribuiu](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed).  


## <a name="compliance-stuck-at-0"></a>Conformidade parada a 0%

Quando a conformidade da implantação do aplicativo é 0%, verifique o status de implantação para o aplicativo no workspace **Monitoramento** no nó **Implantações**.

- **Em andamento**: o cliente pode estar parado no [download de conteúdo](#download-failures)

- **Erro**: para obter mais informações sobre como solucionar esse problema, veja a postagem no blog: [Tips and Tricks: How to Take Action on Assets That Report a Failed Deployment](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/Tips-and-Tricks-How-to-Take-Action-on-Assets-That-Report-a/ba-p/273019) (Dicas e truques: como agir nos ativos que relatam uma implantação com falha)

- **Desconhecido**: esse status geralmente significa que o cliente não recebeu a política. Atualize manualmente a política do cliente para ver se o cliente a recebe. Para obter mais informações, confira [Iniciar recuperação de política para um cliente do Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).
  
Se essas ações não resolverem o problema, verifique o status do cliente. Pode haver um problema subjacente mais profundo com o cliente. Para obter mais informações, consulte [Como monitorar clientes](/sccm/core/clients/manage/monitor-clients).


## <a name="next-steps"></a>Próximas etapas

- [Monitorar aplicativos](/sccm/apps/deploy-use/monitor-applications-from-the-console)
- [Implantar aplicativos](/sccm/apps/deploy-use/deploy-applications)
- [Tarefas de gerenciamento de aplicativos](/sccm/apps/deploy-use/management-tasks-applications)
