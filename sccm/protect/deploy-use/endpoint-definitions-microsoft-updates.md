---
title: "Definições de malware do Endpoint Protection do compartilhamento de rede | System Center Configuration Manager"
description: "Saiba como habilitar o download de definições de malware do Endpoint Protection do Microsoft Updates para o Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 23c19256f3f38d44c57e5d3d25b36ceb023f3214


---

# <a name="enable-endpoint-protection-malware-definitions-to-download-from-microsoft-updates-for-configuration-manager"></a>Habilitar o download das definições de malware do Endpoint Protection do Microsoft Updates para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


 Quando você seleciona para baixar atualizações de definições do Microsoft Update, os clientes verificarão o site do Microsoft Update no intervalo definido na seção **Atualizações de definições** da caixa de diálogo de política antimalware.

 Esse método pode ser útil quando o cliente não tem conectividade com o site do Configuration Manager ou quando você deseja que os usuários possam iniciar atualizações de definições.

> [!IMPORTANT]
>  Os clientes devem ter acesso ao Microsoft Update na Internet para poder usar esse método para baixar as atualizações de definições.

## <a name="using-the-microsoft-malware-protection-center-to-download-definitions"></a>Usando o Centro de Proteção contra Malware da Microsoft para baixar definições
 Você pode configurar clientes para baixar atualizações de definições do Centro de Proteção contra Malware da Microsoft. Essa opção é usada pelos clientes do Endpoint Protection para baixar as atualizações de definições caso não seja possível baixar atualizações de outra fonte. Esse método de atualização pode ser útil quando há um problema com sua infraestrutura do Configuration Manager que impede a distribuição de atualizações.

> [!IMPORTANT]
>  Os clientes devem ter acesso ao Microsoft Update na Internet para poder usar esse método para baixar as atualizações de definições.


> [!div class="button"]
[Próxima etapa >](endpoint-antimalware-policies.md)

> [!div class="button"]
[Voltar >](endpoint-configure-alerts.md)



<!--HONumber=Nov16_HO1-->


