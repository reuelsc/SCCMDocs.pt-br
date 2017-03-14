---
title: "Habilitar a regra de proteção de dispositivo na política de conformidade | System Center Configuration Manager"
description: "Habilite a regra de proteção contra ameaças móveis na política de conformidade do dispositivo."
ms.custom: na
ms.date: 12/9/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 020f43e8-738e-4a82-91be-27b10cda9665
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 498b8c02dbf1391e6331c8b9ad7b6ef0fdef22d0
ms.openlocfilehash: 319289c9b211935ba10cb6d3da386ffed3c0153e
ms.lasthandoff: 02/23/2017


---
# <a name="create-a-lookout-device-threat-protection-rule"></a>Criar uma regra de proteção contra ameaças do dispositivo do Lookout

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

## <a name="before-you-begin"></a>Antes de começar

O Intune com a proteção contra ameaças móveis, Lookout, oferece a capacidade de detectar ameaças móveis e fazer uma avaliação de risco no dispositivo. Você pode criar uma regra de política de conformidade no Configuration Manager a fim de incluir a avaliação de risco e determinar se o dispositivo está em conformidade. Em seguida, você pode usar a política de acesso condicional para permitir ou bloquear o acesso ao Exchange, ao SharePoint e a outros serviços com base na conformidade do dispositivo.

Para que a detecção de ameaças ao dispositivo do Lookout influencie a política de conformidade do dispositivo:

-   A regra **Proteção contra Ameaças ao Dispositivo** deve ser habilitada na política de conformidade.

-   A página **Status do Lookout** no **Console de administrador do Intune** deve aparecer como **Ativa**. Consulte o tópico [Habilitar a conexão MTP do Lookout no Intune](https://docs.microsoft.com/sccm/protect/deploy-use/enable-lookout-connection-in-intune) para obter mais detalhes e instruções sobre como ativar a integração do Lookout.

Antes de criar a regra de proteção contra ameaça ao dispositivo na política de conformidade, recomendamos que você faça o seguinte:

1.  [Configure sua assinatura com a proteção contra ameaças de dispositivo do Lookout](https://docs.microsoft.com/sccm/protect/deploy-use/set-up-your-subscription-with-lookout)

2.  [Habilite a conexão do Lookout no Intune](https://docs.microsoft.com/sccm/protect/deploy-use/enable-lookout-connection-in-intune)

3.  [Configure o aplicativo Lookout for Work](https://docs.microsoft.com/sccm/protect/deploy-use/configure-and-deploy-lookout-for-work-apps)

>[!NOTE]
>A regra de conformidade é imposta somente após a conclusão da instalação.

## <a name="to-create-a-device-threat-protection-rule"></a>Para criar uma regra de proteção contra ameaças do dispositivo

Como parte da configuração de proteção contra ameaça ao dispositivo do Lookout, no [console do Lookout](https://aad.lookout.com), crie uma política que classifica diversas ameaças nos níveis alto, médio e baixo. Na política de conformidade do Intune, você usará o nível de ameaça para definir o nível máximo de ameaças permitido.

Para criar uma regra de proteção contra ameaças do dispositivo do Lookout:

1.  No console do Configuration Manager, clique no espaço de trabalho **Ativos e Conformidade**.

2.  Nos **Ativos e Conformidade**, expanda **Políticas de Conformidade.**

3.  Clique com o botão direito do mouse em **Políticas de Conformidade** e selecione **Criar Política de Conformidade**.

4.  Insira o nome da política de conformidade e, em seguida, selecione **Regras de conformidade para dispositivos gerenciados sem o cliente do Configuration Manager**.

5.  Selecione as plataformas de sistema operacional que serão provisionadas com a política de conformidade (Android 4.1 e posterior e/ou iOS 8 e posterior).

6.  Na página **Regras**, clique em **Novo** para especificar as regras para um dispositivo em conformidade.

7.  Na página **Adicionar Regra**, defina uma nova regra com as seguintes informações:
    1.  Condição: nível máximo de risco de proteção contra ameaças ao dispositivo.
    
    2.  Valor: o valor pode ser um dos seguintes:
        1.  **Nenhum (protegido)**: este é o mais seguro. Isso significa que o dispositivo não pode ter quaisquer ameaças. Se qualquer nível de ameaças for encontrado, o dispositivo será avaliado como sem conformidade.
        2.  **Baixo**: o dispositivo será avaliado como compatível se houver apenas as ameaças de nível baixo. Qualquer ameaça superior coloca o dispositivo em um status de não compatível.
        3.  **Médio**: o dispositivo é avaliado como compatível se as ameaças encontradas no dispositivo forem de nível baixo ou médio. Se forem detectadas ameaças de nível alto, o dispositivo será determinado como não compatível.
        4.  **Alto**: esse é o menos seguro. Essencialmente, essa opção permite todos os níveis de risco, e talvez seja útil somente se você estiver usando esta solução para fins de relatório.

>[!IMPORTANT]
>Se você criar políticas de acesso condicional para o Office 365 e outros serviços, a avaliação de compatibilidade acima será levada em consideração e os dispositivos incompatíveis serão impedidos de acessar recursos da empresa até que a ameaça seja resolvida.
