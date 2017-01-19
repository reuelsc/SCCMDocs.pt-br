---

title: Configurar o Endpoint Protection | Microsoft Docs
description: "Saiba como selecionar e configurar os métodos com o Endpoint Protection no System Center Configuration Manager para manter as definições antimalware atualizadas nos computadores cliente."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 537dd2a7-4e44-4877-b8dd-5e1499407f8d
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 9085a4daed409eeff4c95e5c467f123d0a38147a



---

#  <a name="configure-definition-updates-for-endpoint-protection"></a>Configurar atualizações de definição para o Endpoint Protection  

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 Com o Endpoint Protection no System Center Configuration Manager, você pode usar qualquer um dos vários métodos disponíveis para manter as definições antimalware atualizadas nos computadores cliente em sua hierarquia. As informações neste tópico podem ajudá-lo a selecionar e configurar esses métodos.

 Para atualizar as definições antimalware, você pode usar um ou mais dos seguintes métodos:

-   [Atualizações distribuídas do Configuration Manager](endpoint-definitions-configmgr.md) – Esse método usa as atualizações de software do Configuration Manager para fornecer atualizações de mecanismos e definições aos computadores na sua hierarquia.

-   [Atualizações distribuídas do WSUS (Windows Server Update Services)](endpoint-definitions-wsus.md) – Esse método usa sua infraestrutura do WSUS para fornecer atualizações de definições e de mecanismos aos computadores.

-   [Atualizações distribuídas do Microsoft Update](endpoint-definitions-microsoft-updates.md) – Esse método permite que os computadores se conectem diretamente ao Microsoft Update para baixar atualizações de definições e de mecanismos. Esse método pode ser útil para computadores que não estão frequentemente conectados à rede comercial.

-   [Atualizações distribuídas por meio do Centro de Proteção contra Malware da Microsoft](endpoint-definitions-protection-center.md) – Esse método baixará atualizações de definições por meio do Centro de Proteção contra Malware da Microsoft.

-   [Atualizações de compartilhamentos de arquivo UNC](endpoint-definitions-network.md) – Com esse método, você pode salvar as atualizações de definições e de mecanismos mais recentes em um compartilhamento na rede. Os clientes podem acessar a rede para instalar as atualizações.

 Você pode configurar várias origens de atualização de definição e controlar a ordem em que elas são avaliadas e aplicadas. Isso é feito na caixa de diálogo **Configurar Origens de Atualização de Definição** quando você cria uma política antimalware.

> [!IMPORTANT]
>  Para computadores Windows 10, você deve configurar o Endpoint Protection para atualizar as definições de malware para o Windows Defender.

## <a name="how-to-configure-definition-update-sources"></a>Como configurar origens de atualização de definição
 Use o procedimento a seguir para configurar origens de atualização de definição a serem usadas para cada política antimalware.

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.

2.  No espaço de trabalho **Ativos e Conformidade** , expanda **Endpoint Protection**e clique em **Políticas Antimalware**.

3.  Abra a página de propriedades da **Política Antimalware Padrão** ou crie uma nova política antimalware. Para obter mais informações sobre como criar políticas antimalware, consulte [Como criar e implantar políticas antimalware para o Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md).

4.  Na seção **Atualizações de definições** da caixa de diálogo Propriedades antimalware, clique em **Definir Origem**.

5.  Na caixa de diálogo **Configurar Origens de Atualização de Definição** , selecione as origens a serem usadas para as atualizações de definições. Você pode clicar em **Para Cima** ou **Para Baixo** para modificar a ordem na qual as origens são usadas.

6.  Clique em **OK** para fechar a caixa de diálogo **Configurar Origens de Atualização de Definição** .

## <a name="configure-endpoint-protection-definitions"></a>Configurar as definições do Endpoint Protection

-   [Atualizações distribuídas do Configuration Manager](endpoint-definitions-configmgr.md) – Esse método usa as atualizações de software do Configuration Manager para fornecer atualizações de mecanismos e definições aos computadores na sua hierarquia.

-   [Atualizações distribuídas do WSUS (Windows Server Update Services)](endpoint-definitions-wsus.md) – Esse método usa sua infraestrutura do WSUS para fornecer atualizações de definições e de mecanismos aos computadores.

-   [Atualizações distribuídas do Microsoft Update](endpoint-definitions-microsoft-updates.md) – Esse método permite que os computadores se conectem diretamente ao Microsoft Update para baixar atualizações de definições e de mecanismos. Esse método pode ser útil para computadores que não estão frequentemente conectados à rede comercial.

-   Atualizações distribuídas por meio do Centro de Proteção contra Malware da Microsoft – Esse método baixará atualizações de definições por meio do Centro de Proteção contra Malware da Microsoft.

-   [Atualizações de compartilhamentos de arquivo UNC](endpoint-definitions-network.md) – Com esse método, você pode salvar as atualizações de definições e de mecanismos mais recentes em um compartilhamento na rede. Os clientes podem acessar a rede para instalar as atualizações.



<!--HONumber=Dec16_HO3-->

