---
title: Recursos no Technical Preview 1602
titleSuffix: Configuration Manager
description: "Saiba mais sobre os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1602."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b9265d1-b461-47f8-b7ef-885da0fdd969
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.openlocfilehash: e0514df0a043a269c3705ff8e869000071f984c0
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="capabilities-in-technical-preview-1602-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1602 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1602. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview. Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de um technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos em um technical preview.  

 Veja a seguir os novos recursos que você pode experimentar nesta versão.  

##  <a name="BKMK_MDM"></a> Melhorias no gerenciamento de dispositivo móvel  

### <a name="ios-activation-lock"></a>Bloqueio de Ativação do iOS  
 O System Center Configuration Manager pode ajudar a gerenciar o Bloqueio de Ativação do iOS, um recurso do aplicativo Buscar meu iPhone para dispositivos iOS 7.1 e posteriores. O Bloqueio de Ativação é habilitado automaticamente quando o aplicativo Buscar meu iPhone for usado em um dispositivo. Depois que ele for habilitado, a ID da Apple e a senha do usuário deverão ser inseridas antes que qualquer pessoa possa:  

-   Desligar o Buscar meu iPhone  

-   Apagar o dispositivo  

-   Reativar o dispositivo  

 O Configuration Manager pode solicitar o status do Bloqueio de Ativação de dispositivos supervisionados e não supervisionados que executam o iOS 7.1 e posterior. Para dispositivos supervisionados, o Intune pode recuperar o código de bypass de Bloqueio de Ativação e emiti-lo diretamente para o dispositivo.  

 Para ver os detalhes, consulte [Ajudar a proteger dispositivos iOS com bypass de Bloqueio de Ativação para o Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock)  

##  <a name="BKMK_SC1601"></a> Melhorias no Centro de Software na versão 1602  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Atualizar a política de computador e de usuário do computador no Centro de Software  
 Uma nova opção, **Política de Sincronização**, foi adicionada à página **Opções** > **Manutenção do Computador** do Centro de Software, o que faz com que o computador atualize sua política de computador e de usuário do Configuration Manager.  

##  <a name="BKMK_Win10Servicing"></a> Melhorias no Serviço do Windows 10  
 Na Technical Preview 1602, adicionamos as seguintes melhorias ao Serviço do Windows 10:  

-   Novas opções de filtro para Planos de Serviço.  Agora é possível filtrar por **Idioma**, **Obrigatório** e **Título**. Somente as atualizações que atendem aos critérios especificados serão adicionadas à implantação associada.  

-   Ao selecionar a classificação **Atualizações** para a sincronização das atualizações de software, é exibida uma caixa de diálogo de aviso para informá-lo que o [hotfix 3095113](https://support.microsoft.com/kb/3095113) do WSUS é necessário para sincronizar com êxito as atualizações de software e para que o Serviço do Windows 10 funcione corretamente.  No diálogo, é possível ir para o artigo da base de dados de conhecimento do hotfix.  

-   As atualizações do Windows 10 disponíveis agora são exibidas apenas no nó **Manutenção do Windows 10** \ **Todas as Atualizações do Windows 10** do console do Configuration Manager. Essas atualizações não são mais exibidas no nó **Atualizações de Software** \ **Todas as Atualizações de Software**.  

-   Os usuários finais que iniciam um pacote de Atualização do Windows 10 veem um diálogo que informará que estão atualizando seus sistemas operacionais.  
