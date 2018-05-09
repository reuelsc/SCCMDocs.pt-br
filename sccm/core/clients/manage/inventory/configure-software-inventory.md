---
title: Configurar o inventário de software
titleSuffix: Configuration Manager
description: Configurar o inventário de software e excluir pastas do inventário de software no Configuration Manager.
ms.date: 01/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 346ff3254f4c1833f49bf256cbf5ad0c489d77e0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>Como configurar o inventário de software no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este procedimento define as configurações padrão do cliente para o inventário de software e se aplica a todos os computadores na hierarquia. Caso deseje aplicar essas configurações somente a alguns computadores, crie uma configuração de cliente de dispositivo personalizada e atribua-a a uma coleção. Para obter mais informações sobre como criar configurações personalizadas de dispositivo, consulte [Como configurar as definições de cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).   

## <a name="to-configure-software-inventory"></a>Para configurar o inventário de software  

1.  No console do Configuration Manager, clique em **Administração** > **Configurações do Cliente****Configurações do Cliente Padrão**.  

4.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

5.  Na caixa de diálogo **Configurações Padrão**, escolha **Inventário de Software**.  

6.  Na lista **Configurações do Dispositivo** , configure os seguintes valores:  

    -   **Habilitar inventário de software em clientes** – Na lista suspensa, selecione **Verdadeiro**.  

    -   **Programar agendamento do inventário de software e da coleção de arquivos** – Configura o intervalo no qual os clientes coletam inventário de software e arquivos.   

7.  Defina as configurações do cliente necessárias. A seção [Inventário de software](../../../../core/clients/deploy/about-client-settings.md#software-inventory) do artigo [Sobre as configurações do cliente no System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md) apresenta uma lista das configurações do cliente.  

 Os computadores cliente serão definidos com essas configurações durante o próximo download da política do cliente. Para iniciar a recuperação de política para um cliente individual, veja [Como gerenciar clientes no System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

 > [!TIP]  
        >   O código de erro 80041006 em inventoryprovider.log significa que a memória do provedor WMI é insuficiente. Ou seja, foi atingido o limite de cota de memória para um provedor e o provedor de inventário não pode continuar.
Nesse caso, o agente de inventário cria um relatório com 0 entrada e, portanto, nenhum item de inventário é relatado. <br/>
Uma possível solução para esse erro seria reduzir o escopo da coleta de inventário de software. Em circunstâncias em que o erro ocorre depois de limitar o escopo de inventário, o aumento da propriedade [MemoryPerHost](https://blogs.technet.microsoft.com/askperf/2008/09/16/memory-and-handle-quotas-in-the-wmi-provider-service/) definida na classe [_ProviderHostQuotaConfiguration](https://msdn.microsoft.com/library/aa394671) pode fornecer uma solução.

<!--SMS.480648 include WMI Out of memory tip -->


## <a name="to-exclude-folders-from-software-inventory"></a>Para excluir pastas do inventário de software  

1.  Usando o Notepad.exe, crie um arquivo vazio chamado **Skpswi.dat**.  

2.  Clique com o botão direito do mouse no arquivo **Skpswi.dat** e clique em **Propriedades**. Nas propriedades do arquivo Skpswi.dat, selecione o atributo **Hidden** .  

3.  Coloque o arquivo **Skpswi.dat** na raiz de cada estrutura de pasta ou da unidade de disco rígido do cliente que você deseja excluir do inventário de software.  

> [!NOTE]  
>  O inventário de software não realizará o inventário da unidade do cliente novamente, a menos que esse arquivo seja excluído da unidade no computador cliente.