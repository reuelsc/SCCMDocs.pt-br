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
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0bae054d3daa5aea8e343fef05aa4578221f17b6
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62226820"
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
  * Condição: Nível de risco máximo de proteção de ameaças de dispositivo.
  * Valor: O valor pode ser um dos seguintes:
    * **Nenhum (protegido)**: Este é o mais seguro. Isso significa que o dispositivo não pode ter quaisquer ameaças. Se qualquer nível de ameaças for encontrado, o dispositivo será avaliado como não compatível.
    * **Baixa**: O dispositivo será avaliado como compatível se apenas ameaças de nível baixo estiverem presentes. Qualquer ameaça superior coloca o dispositivo em um status de não compatível.
    * **Médio**: O dispositivo será avaliado como compatível se as ameaças encontradas no dispositivo forem de nível baixo ou médio. Se forem detectadas ameaças de nível alto, o dispositivo será determinado como não compatível.
    * **Alta**: Este é o menos seguro. Essencialmente, essa opção permite todos os níveis de risco, e talvez seja útil somente se você estiver usando esta solução para fins de relatório.

Se você criar políticas de acesso condicional para o Office 365 e outros serviços, a avaliação de compatibilidade acima será levada em consideração e os dispositivos incompatíveis serão impedidos de acessar recursos da empresa até que a ameaça seja resolvida.

O status de proteção contra ameaça do dispositivo é exibido no nó **Segurança** no workspace **Monitoramento**.
Um resumo do status com vários níveis de ameaça será exibido em um gráfico visual. Clique nas seções específicas do gráfico para ver mais informações, como o número de dispositivos indicados como não compatíveis pela plataforma, e os erros relatados.
Você também pode ver o status individual do dispositivo no workspace **Ativos e conformidade**, em **Dispositivos**.  Você pode adicionar as colunas **Conformidade do dispositivo contra ameaça** e **Nível de ameaça do dispositivo** para ver o status.  Essas colunas não são exibidas por padrão.
