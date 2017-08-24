---
title: "Pré-requisitos para perfis de email | Microsoft Docs"
description: "Saiba mais sobre os perfis de email no System Center Configuration Manager e suas dependências externas e dependências dentro do produto."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dccf0b73-43bd-4545-8914-114168ebad36
caps.latest.revision: "5"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 451317db1d7aab888c03d1a099b9ce25311e06d0
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="email-profile-prerequisites"></a>Pré-requisitos para perfis de email

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os perfis de email no System Center Configuration Manager têm dependências externas e dependências dentro do produto.  

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Permissões de segurança específicas devem ser concedidas para gerenciar perfis de email|Você deve ter as seguintes permissões de segurança para gerenciar configurações de acesso aos recursos da empresa, como perfis de email:<br /><br /> ‑ Para exibir e gerenciar alertas e relatórios para perfis de email: permissões para **Criar**, **Excluir**, **Modificar**, **Modificar Relatório**, **Ler** e **Executar Relatório** para o objeto **Alertas**.<br /><br /> ‑ Para criar e gerenciar perfis de certificado: permissões para **Criar Política**, **Modificar Relatório**, **Ler** e **Executar Relatório** para o objeto **Perfil de Certificado**.<br /><br /> ‑ Para gerenciar implantações de perfil de email: permissões para **Implantar Políticas de Configuração**, **Modificar Alerta de Status do Cliente**, **Ler** e **Ler Recurso** para o objeto **Coleção**.<br /><br /> ‑ Para gerenciar todas as políticas de configuração: permissões **Criar**, **Excluir**, **Modificar**, **Ler** e **Definir Escopo de Segurança** para o objeto **Política de Configuração**.<br /><br /> ‑ Para executar consultas relacionadas aos perfis de email: permissão para **Ler** para o objeto **Consulta**.<br /><br /> ‑ Para exibir as informações de perfis de certificado no console do System Center Configuration Manager: permissão para **Ler** o objeto **Site**.<br /><br /> ‑ Para exibir mensagens de status para perfis de email: permissão para **Ler** para o objeto **Mensagens de Status**.<br /><br /> ‑ Para criar e gerenciar perfis de email: permissões para **Criar Política**, **Modificar Relatório**, **Ler** e **Executar Relatório** para o objeto **Perfil de Provisionamento de Comunicação**.<br /><br /> A função de segurança do **Gerente de Acesso de Recurso da Empresa** inclui essas permissões que são necessárias para gerenciar os perfis de email no System Center Configuration Manager. Para mais informações, consulte [Configurar segurança no System Center Configuration Manager](../../core/plan-design/security/configure-security.md).|  
|Atributo mail no active directory|Se você deseja gerar o endereço de email de usuários em um perfil de email usando o endereço SMTP primário do usuário, a descoberta de usuário do System Center Configuration Manager deve ser configurada para descobrir o atributo **mail** do Active Directory (isso é configurado por padrão).|  

## <a name="external-dependencies"></a>Dependências externas  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Atributo mail no active directory|Se você deseja gerar os endereços de email de usuários em um perfil de email usando o endereço de SMTP primário do usuário, esse endereço deve existir no atributo **mail** no Active Directory.<br /><br /> Para obter mais informações, consulte a documentação do Windows Server.|
