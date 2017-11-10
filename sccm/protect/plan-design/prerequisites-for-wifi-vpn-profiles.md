---
title: "Pré-requisitos de perfis de Wi-Fi e VPN"
titleSuffix: Configuration Manager
description: "Saiba mais sobre as permissões de segurança necessárias para gerenciar perfis de certificado, Wi-Fi e VPN no System Center Configuration Manager."
ms.custom: na
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 9f459ad76768443c218bbc86d75b3f5ae34596b3
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="prerequisites-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Pré-requisitos para perfis Wi-Fi e VPN no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Perfis Wi-Fi e VPN no System Center Configuration Manager têm dependências somente dentro do produto.  

 Você deve ter as seguintes permissões de segurança para gerenciar as configurações de acesso aos recursos da empresa, como perfis de certificado, perfis Wi-Fi e perfis VPN:  

-   Para exibir e gerenciar alertas e relatórios para Wi-Fi e perfis: **Criar**, **Excluir**, **Modificar**, **Modificar Relatório**, **Ler**e **Executar Relatório** para o objeto **Alertas**.  

-   Para criar e gerenciar perfis de certificado: **Criar Política**, **Modificar Relatório**, **Ler**e **Executar Relatório** para o objeto **Perfil de Certificado** .  

-   Para gerenciar implantações de perfil Wi-Fi, de certificado e VPN: **Implantar Políticas de Configuração**, **Modificar Alerta de Status do Cliente**, **Ler**e **Ler Recurso** para o objeto **Coleção** .  

-   Para gerenciar todas as políticas de configuração: **Criar**, **Excluir**, **Modificar**, **Ler**e **Definir Escopo de Segurança** para o objeto **Política de Configuração** .  

-   Para executar consultas relacionadas aos perfis Wi-Fi e VPN: permissão para **Ler** o objeto **Consulta**.  

-   Para exibir as informações de perfis Wi-Fi e VPN no console do System Center Configuration Manager: permissão para **Ler** o objeto **Site**.  

-   Para exibir mensagens de status para perfis Wi-Fi e VPN: permissão para **Ler** o objeto **Mensagens de Status**.  

-   Para criar e modificar o perfil de certificado de autoridade de certificação confiável: **Criar Política**, **Modificar Relatório**, **Ler**e **Executar Relatório** para o objeto **Perfil Certificado de Autoridade de Certificação Confiável** .  

-   Para criar e gerenciar perfis VPN: permissões para **Criar Política**, **Modificar Relatório**, **Ler**e **Executar Relatório** para o objeto **Perfil VPN** .  

-   Para criar e gerenciar perfis Wi-Fi: permissões para **Criar Política**, **Modificar Relatório**, **Ler**e **Executar Relatório** para o objeto **Perfil Wi-Fi** .  

 A função de segurança do **Gerente de Acesso de Recurso da Empresa** inclui essas permissões que são necessárias para gerenciar os perfis Wi-Fi no System Center Configuration Manager. Para mais informações, consulte [Configurar segurança no System Center Configuration Manager](../../core/plan-design/security/configure-security.md).
