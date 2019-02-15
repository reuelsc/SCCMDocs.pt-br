---
title: Segurança e privacidade do perfil de Wi-Fi e VPN
titleSuffix: Configuration Manager
description: Saiba mais sobre as práticas recomendadas de segurança para gerenciar perfis de Wi-Fi e VPN para dispositivos no System Center Configuration Manager.
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: be81ff80f0da01916e2ec21a8ba1c7fe48fb8062
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142316"
---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Segurança e privacidade de perfis Wi-Fi e VPN no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

##  <a name="security-best-practices-for-wi-fi--and-vpn-profiles"></a>Práticas recomendadas de segurança para perfis de Wi-Fi e VPN  
 Use as seguintes práticas recomendadas de segurança ao gerenciar perfis de Wi-Fi e VPN para dispositivos.  

|Prática recomendada de segurança|Mais informações|  
|----------------------------|----------------------|  
|Sempre que possível, escolha as opções mais seguras para as quais sua infraestrutura de Wi-Fi e VPN e sistemas operacionais cliente podem dar suporte.|Os perfis de Wi-Fi e VPN fornecem um método conveniente para distribuir e gerenciar de maneira centralizada as configurações de Wi-Fi e VPN que já têm suporte dos dispositivos. O Configuration Manager não adiciona a funcionalidade de Wi-Fi ou VPN.<br /><br /> Identifique, implemente e siga as práticas recomendadas de segurança que foram sugeridas para os dispositivos e a infraestrutura.|  

## <a name="privacy-information-for-wi-fi-profiles"></a>Informações de privacidade para perfis Wi-Fi  
 Você pode usar perfis Wi-Fi e VPN para configurar os dispositivos cliente que se conectam a servidores Wi-Fi e VPN e avaliar se esses dispositivos são compatíveis depois que os perfis forem aplicados. O ponto de gerenciamento envia informações de conformidade ao servidor do site, e essas informações são armazenadas no banco de dados do site. As informações são criptografadas quando os dispositivos as enviam para o ponto de gerenciamento, mas não são armazenadas em formato criptografado no banco de dados do site. O banco de dados mantém as informações até que a tarefa de manutenção de site **Excluir Dados Antigos de Gerenciamento da Configuração** as exclua. O intervalo de exclusão padrão é de 90 dias, mas você pode alterá-lo. As informações de conformidade não são enviadas à Microsoft.  

 Por padrão, os dispositivos não avaliam os perfis Wi-Fi e VPN. Além disso, você deve configurar os perfis e implantá-los nos usuários.  

 Antes de configurar os perfis Wi-Fi e VPN, considere seus requisitos de privacidade.  
