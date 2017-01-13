---
title: "Gerenciar dados de configuração | Microsoft Docs"
description: "Depois de criar itens de configuração e linhas de base no System Center Configuration Manager, você poderá usar outros comandos para executar várias ações."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b48c693c-d2b0-4707-a5dd-fe92172c49fe
caps.latest.revision: 7
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f9e939d871e95a3248d8e5d96cb73063a81fd5cf
ms.openlocfilehash: 1a6084834384e695b49a71fe23833049c86f8dbc


---
# <a name="manage-configuration-data-in-system-center-configuration-manager"></a>Gerenciar dados de configuração no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Depois de criar itens e linhas de base de configuração no System Center Configuration Manager, outros comandos estarão disponíveis para ajudar a executar várias ações.  

## <a name="manage-configuration-items"></a>Gerenciar itens de configuração  

-   No espaço de trabalho **Ativos e Conformidade**, expanda **Configurações de Conformidade** > **Itens de Configuração**, selecione o item de configuração a ser gerenciado e uma tarefa de gerenciamento.  

|Tarefa de gerenciamento|Detalhes|  
|---------------------|-------------|  
|**Criar Item de Configuração Filho**|Abre o **Assistente para Criar Item de Configuração Filho** , em que é possível criar um item de configuração filho do item de configuração selecionado.<br /><br /> Não é possível criar um item de configuração filho por meio de um item de configuração de dispositivo móvel.<br /><br /> Para ver os detalhes, consulte [Como criar itens de configuração filho](../../compliance/deploy-use/create-child-configuration-items.md).|  
|**Histórico de Revisão**|Abre a caixa de diálogo **Histórico de Revisão do Item de Configuração** , em que é possível exibir e gerenciar as revisões anteriores do item de configuração selecionado.|  
|**Exibir definição XML**|Exibe o arquivo de definição XML para o item de configuração selecionado em uma nova janela. Essas informações podem ser úteis quando você desejar criar dados de configuração manualmente.|  
|**Exportarar**|Exporta um item de configuração em um formato de arquivo de gabinete (.cab), desde que ele tenha sido criado nesse site. Você pode importá-lo para o mesmo site ou outro site do Configuration Manager. Os dados de configuração são convertidos no resumo DCM.|  
|**Copiar**|Cria uma cópia do item de configuração selecionado com um nome que você especificar. O novo item de configuração não mantém nenhuma relação com o item de configuração original. Isso significa que o item de configuração duplicado não continua herdando as informações de configuração do item de configuração original.|  
|**Excluir**|Abre a caixa de diálogo **Excluir Item de Configuração** , em que é possível examinar todas as referências a esse item de configuração.<br /><br /> É necessário remover todas as referências a um item de configuração antes de excluir o item de configuração.|  

## <a name="manage-configuration-baselines"></a>Gerenciar linhas de base de configuração  

-   No espaço de trabalho **Ativos e Conformidade**, expanda **Configurações de Conformidade** > **Linhas de Base de Configuração**, selecione a linha de base de configuração a ser gerenciada e uma tarefa de gerenciamento.  


|Tarefa de gerenciamento|Detalhes|  
|---------------------|-------------|  
|**Mostrar Membros**|Exibe todos os itens de configuração que são referenciados pela linha de base de configuração.|  
|**Resumo do agendamento**|Configura o agendamento pelo qual os dados mostrados no nó **Linhas de Base de Configuração** do console do Configuration Manager são atualizados com as informações mais recentes do banco de dados do site.|  
|**Executar o resumo**|O resumo faz com que os dados do nó **Linhas de Base de Configuração** sejam atualizadas com os dados mais recentes do banco de dados do site. Esta ação pode levar vários minutos para concluir. Talvez você precise clicar em **Atualizar** antes de poder ver os dados mais recentes no console.|  
|**Exibir definição XML**|Exibe o arquivo de definição XML para a linha de base de configuração selecionada em uma nova janela. Essas informações podem ser úteis quando você desejar criar dados de configuração manualmente.|  
|**Habilitar**|Habilita uma linha de base de configuração para o monitoramento de conformidade.|  
|**Desabilitar**|Desabilita uma linha de base de configuração para que ela não seja avaliada quanto à conformidade em computadores cliente. As linhas de base de configuração que fazem referência a esta linha de base de configuração também serão desabilitadas.|  
|**Exportarar**|Exporta uma linha de base de configuração em um formato de arquivo de gabinete (.cab), desde que ela tenha sido criada nesse site. Você pode importá-lo para o mesmo site ou outro site do Configuration Manager. Os dados de configuração são convertidos no resumo DCM.<br /><br /> Para obter informações sobre como importar dados de configuração, veja [Importar dados da configuração](../../compliance/deploy-use/import-configuration-data.md).|  
|**Copiar**|Cria uma cópia da linha de base de configuração selecionada com um nome que você especificar. A nova linha de base de configuração não mantém nenhuma relação com a linha de base de configuração original.|  
|**Excluir**|Abre a caixa de diálogo **Excluir Linha de Base de Configuração** , em que é possível examinar todas as referências a essa linha de base de configuração.<br /><br /> É necessário remover todas as referências a uma linha de base de configuração antes de excluir a linha de base de configuração.|  
|**Implantar**|Abre a caixa de diálogo **Implantar Linha de Base de Configuração** , em que você é possível implantar uma ou mais linhas de base de configuração em dispositivos de sua hierarquia.<br /><br /> Para ver os detalhes, consulte [Implantar linhas de base de configuração](../../compliance/deploy-use/deploy-configuration-baselines.md).|  



<!--HONumber=Dec16_HO3-->


