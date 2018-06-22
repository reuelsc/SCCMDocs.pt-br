---
title: Habilitar a regra de proteção de dispositivo na política de conformidade
titleSuffix: Configuration Manager
description: Habilite a regra de proteção contra ameaças móveis na política de conformidade do dispositivo.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 99a5b715-f172-46e1-ac27-ad55bde66d0d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6e102f65baad93bdbdf630649a4639d1092284c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32353038"
---
# <a name="enable-device-threat-protection-rule-in-the-compliance-policy"></a>Habilitar a regra de proteção contra ameaças móveis na política de conformidade

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Intune com a proteção contra ameaças móveis, Lookout, oferece a capacidade de detectar ameaças móveis e fazer uma avaliação de risco no dispositivo. Você pode criar uma regra de política de conformidade no Configuration Manager a fim de incluir a avaliação de risco e determinar se o dispositivo é compatível. Em seguida, você pode usar a política de acesso condicional para permitir ou bloquear o acesso ao Exchange, ao SharePoint e a outros serviços com base na conformidade do dispositivo.

Para que a detecção de ameaças ao dispositivo do Lookout influencie a política de conformidade do dispositivo:

* Habilite a regra **Proteção contra Ameaças ao Dispositivo** na política de conformidade.

* A página **Status do Lookout** no **Console de administrador do Intune** deve aparecer como **Ativa**. Consulte o tópico [Habilitar a conexão MTP do Lookout no Intune](enable-lookout-connection-in-intune.md) para obter mais detalhes e instruções sobre como ativar a integração do Lookout.


Antes de criar a regra de proteção contra ameaças do dispositivo na política de conformidade, recomendamos a [configuração de sua assinatura com a proteção contra ameaças ao dispositivo do Lookout](set-up-your-subscription-with-lookout.md), [habilitação da conexão do Lookout no Intune](enable-lookout-connection-in-intune.md) e [configuração do aplicativo Lookout for work](configure-and-deploy-lookout-for-work-apps.md). A regra de conformidade é imposta somente após a conclusão da instalação.

Para habilitar a regra de proteção contra ameaça ao dispositivo, use uma política de conformidade existente ou crie uma nova.

Como parte da configuração de proteção contra ameaça ao dispositivo do Lookout, no [console do Lookout](https://aad.lookout.com), crie uma política que classifica diversas ameaças nos níveis alto, médio e baixo. Na política de conformidade do Intune, você usará o nível de ameaça para definir o nível máximo de ameaças permitido.

Na página **Regras** do assistente de política de conformidade, defina uma nova regra com as informações a seguir:
  * Condição: nível máximo de risco de proteção contra ameaças ao dispositivo.
  * Valor: o valor pode ser um dos seguintes:
    * **Nenhum (protegido)**: este é o mais seguro. Isso significa que o dispositivo não pode ter quaisquer ameaças. Se qualquer nível de ameaças for encontrado, o dispositivo será avaliado como não compatível.
    * **Baixo**: o dispositivo será avaliado como compatível se houver apenas as ameaças de nível baixo. Qualquer ameaça superior coloca o dispositivo em um status de não compatível.
    * **Médio**: o dispositivo é avaliado como compatível se as ameaças encontradas no dispositivo forem de nível baixo ou médio. Se forem detectadas ameaças de nível alto, o dispositivo será determinado como não compatível.
    * **Alto**: esse é o menos seguro. Essencialmente, essa opção permite todos os níveis de risco, e talvez seja útil somente se você estiver usando esta solução para fins de relatório.

Se você criar políticas de acesso condicional para o Office 365 e outros serviços, a avaliação de compatibilidade acima será levada em consideração e os dispositivos incompatíveis serão impedidos de acessar recursos da empresa até que a ameaça seja resolvida.

O status de proteção contra ameaça do dispositivo é exibido no nó **Segurança** no espaço de trabalho **Monitoramento**.
Um resumo do status com vários níveis de ameaça será exibido em um gráfico visual. Clique nas seções específicas do gráfico para ver mais informações, como o número de dispositivos indicados como não compatíveis pela plataforma, e os erros relatados.
Você também pode ver o status individual do dispositivo no espaço de trabalho **Ativos e conformidade**, em **Dispositivos**.  Você pode adicionar as colunas **Conformidade do dispositivo contra ameaça** e **Nível de ameaça do dispositivo** para ver o status.  Essas colunas não são exibidas por padrão.
