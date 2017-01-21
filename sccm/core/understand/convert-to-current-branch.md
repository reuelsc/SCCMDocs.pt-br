---
title: "Atualizar o Branch de Manutenção em Longo Prazo para o Branch Atual | Microsoft Docs"
description: "Saiba como converter um site do Branch de Manutenção em Longo Prazo em um site do Branch Atual."
ms.custom: na
ms.date: 10/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec5b54cf-62b7-4ed1-9bb3-e8c63b9641c8
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 37fa8da8b4acc3f22c9c435206eedde58d2754f0

---


# <a name="upgrade-the-long-term-servicing-branch-to-the-current-branch"></a>Atualizar o Branch de Manutenção em Longo Prazo para o Branch Atual

*Aplica-se a: System Center Configuration Manager (Branch de Manutenção em Longo Prazo)*

Use este tópico para saber como atualizar (converter) um site e uma hierarquia que executa o LTSB (Branch de Manutenção em Longo Prazo) do Configuration Manager para o Branch Atual.

Quando você tiver um contrato do Software Assurance (ou direitos de licenciamento semelhantes) que concede a você direitos de uso do Branch Atual, será possível converter a sua instalação do LTSB no Branch Atual.  Essa é uma conversão unidirecional, pois não há suporte para converter um site do Branch Atual no LTSB.

Se você tiver vários sites, só precisará converter o site da camada superior da sua hierarquia. Depois que o site da camada superior for convertido:
- Os sites primários filho serão convertidos automaticamente.
-   Será necessário atualizar manualmente os sites secundários de dentro do console do Configuration Manager.

## <a name="run-setup-to-convert"></a>Executar instalação para converter
No site de camada superior da sua hierarquia, é possível executar a instalação do Configuration Manager na mídia de linha de base de qualificação e selecionar **Manutenção do Site**.  Em seguida, quando a página de licenciamento aparecer, selecione a opção para o Branch Atual e conclua o assistente.

Quando concluído, seu site é convertido no Branch Atual, e os recursos anteriormente indisponíveis estarão disponíveis para uso.

> [!NOTE]  
> A mídia de linha de base de qualificação é uma mídia que tem uma versão igual ou posterior à da sua instalação LTSB.

Por exemplo, como o LTSB se baseia na versão 1606, você não pode usar a mídia 1511 de linha de base para converter no Branch Atual. Em vez disso, execute a instalação com a mesma mídia de linha de base versão 1606 usada para instalar o site LTSB e escolha a opção de licenciamento para o Branch Atual.  Como alternativa, se uma linha de base mais recente do Branch Atual tiver sido lançada, será possível executar a instalação dessa mídia de linha de base.

Para ver uma lista de versões de linha de base, consulte **Versões de linha de base e atualização** em [Updates for Configuration Manager (Atualizações para o Configuration Manager)](/sccm/core/servers/manage/updates).

## <a name="use-the-configuration-manager-console-to-convert"></a>Usar o console do Configuration Manager para converter
Se seu site executar o LTSB, será possível usar a opção a seguir no console do Configuration Manager para converter no Branch Atual:

 1. No console, vá para **Administração** > **Configuração do Site** > **Sites** e abra **Configurações de Hierarquia**.  
 2. Selecione a opção de converter para o Branch Atual e, em seguida, clique em **Aplicar**.  

Quando concluído, seu site é convertido no Branch Atual, e os recursos anteriormente indisponíveis estarão disponíveis para uso.



<!--HONumber=Dec16_HO3-->


