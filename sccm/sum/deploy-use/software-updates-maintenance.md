---
title: Manutenção de atualizações de software
titleSuffix: Configuration Manager
description: Para manter as atualizações no Configuration Manager, você pode agendar a tarefa de limpeza do WSUS ou executá-la manualmente.
author: aczechowski
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3a44643870234a08169db1d55cc834e4ca5fcbb5
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385483"
---
# <a name="software-updates-maintenance"></a>Manutenção de atualizações de software

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode agendar e executar tarefas de limpeza do WSUS no console do Configuration Manager usando as propriedades do Componente de Ponto de Atualização de Software. Quando você seleciona para executar a tarefa de limpeza do WSUS pela primeira vez, ela será executada depois da próxima sincronização de atualizações de software.  

## <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>Para agendar e executar o trabalho de limpeza do WSUS 
Agende o trabalho de limpeza do WSUS executando as seguintes etapas:   

1.  No console do Configuration Manager, navegue até **Administração** > **Visão Geral** > **Configuração de Site** > **Sites**. 
2. Selecione o site sobre a hierarquia do Configuration Manager. 

3.  Clique em **Configurar componentes do Site** no grupo **Configurações** e, em seguida, clique em **Ponto de atualização de Software** para abrir as propriedades do componente do Ponto de atualização de Software.  

4. Examine o **comportamento de Substituição**. Modifique o comportamento se necessário. 
![captura de tela do comportamento de substituição](media/sccm-supersedence-behavior.PNG)

5.  Clique na guia **Regras de Substituição** e selecione **Executar o assistente de limpeza do WSUS**. Na versão 1806, a opção é renomeada como **Executar limpeza do WSUS após a sincronização**. 
 
6. Clique em **OK** (clique em **Fechar** se você estiver executando a versão 1806).

## <a name="wsus-cleanup-behavior-in-version-1802-and-earlier"></a>Comportamento de limpeza do WSUS na versão 1802 e anteriores
Antes da versão 1806 do Configuration Manager, a opção de limpeza do WSUS executa o item a seguir: 
- A opção **Atualizações expiradas** do assistente de limpeza do WSUS no servidor do WSUS do site de nível superior somente. 
![Captura de tela de limpeza de atualização expirada do WSUS](media/wsus-cleanup-expired.PNG)

-  Uma limpeza de itens de configuração de atualização de software no banco de dados do Configuration Manager ocorre a cada sete dias e remove atualizações desnecessárias do console. 
   - Essa limpeza não removerá as atualizações expiradas do console do Configuration Manager se elas estiverem implantadas no momento. 

Manutenção adicional ainda é necessária no banco de dados do WSUS nível superior e em todos os outros bancos de dados do WSUS no ambiente. Para obter mais informações e instruções, leia a postagem no blog [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://blogs.technet.microsoft.com/configurationmgr/2016/01/26/the-complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maintenance/) (O guia completo para manutenção do Microsoft WSUS e do Configuration Manager SUP). 


## <a name="wsus-cleanup-behavior-starting-in-version-1806"></a>Comportamento de limpeza do WSUS começando na versão 1806
Da versão 1806 em diante, a opção de limpeza do WSUS ocorre após cada sincronização e realiza a limpeza dos itens a seguir: <!--1357898 -->
- A opção **Atualizações expiradas** para servidores do WSUS em sites primários e CAS.
    - Servidores do WSUS para sites secundários não executam a limpeza do WSUS para atualizações expiradas. 
- O Configuration Manager cria uma lista de atualizações substituídas de seu banco de dados. A lista baseia-se no comportamento de substituição nas propriedades do componente de Ponto de Atualização de Software. 
    - Os itens de configuração de atualização que atendem aos critérios de comportamento de substituição estão expirados no console do Configuration Manager.
    - As atualizações são recusadas no WSUS para sites primários e CAS, mas não para sites secundários.
- Uma limpeza de itens de configuração de atualização de software no banco de dados do Configuration Manager ocorre a cada sete dias e remove atualizações desnecessárias do console. 
    - Essa limpeza não removerá as atualizações expiradas do console do Configuration Manager se elas estiverem implantadas no momento. 

> [!NOTE]
> A informação de "Meses de espera antes que uma atualização substituída expire" se baseia na data de criação da atualização substituta. Por exemplo, se você usar dois meses para essa configuração, atualizações que foram substituídas serão recusadas no WSUS e expiradas no Configuration Manager quando a atualização substituta tiver dois meses. 

Toda a Manutenção do WSUS precisa ser executada manualmente em bancos de dados WSUS do site secundário. As seguintes opções do **Assistente de Limpeza do Servidor WSUS** não são executadas em sites primários e CAS:

- Atualizações não utilizadas e revisões de atualização
- Computadores que não estão entrando em contato com o servidor
- Arquivos de atualização desnecessários

 Para obter mais informações e instruções, leia a postagem no blog [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://blogs.technet.microsoft.com/configurationmgr/2016/01/26/the-complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maintenance/) (O guia completo para manutenção do Microsoft WSUS e do Configuration Manager SUP). 

## <a name="updates-cleanup-log-entries"></a>Entradas de log de limpeza de atualizações
 
Você pode verificar essa limpeza examinando o wSyncMgr. log para as seguintes entradas: 
  - O declínio de atualizações substituídas no WSUS está concluído quando você vê esta entrada de log: `Cleanup processed <number> total updates and declined <number>`
  - A limpeza do WSUS está sendo iniciada quando você vê esta entrada: `Calling WSUS Cleanup.`
  - A limpeza do WSUS para atualizações expiradas é concluída quando você vê esta entrada: `Successfully completed WSUS Cleanup.`
  - A limpeza dos itens de configuração de atualizações expiradas do Configuration Manager está iniciando quando você vê esta entrada: `Deleting old expired updates...`
  - A limpeza dos itens de configuração de atualizações expiradas do Configuration Manager está concluída quando você vê esta entrada: `Deleted <number> expired updates total`
