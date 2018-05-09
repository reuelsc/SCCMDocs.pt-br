---
title: Introdução às coleções
titleSuffix: Configuration Manager
description: Veja uma introdução às coleções para usar coleções no System Center Configuration Manager.
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 48a0788d83ffcd7a373f5f73ee675b62508a6d86
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="introduction-to-collections-in-system-center-configuration-manager"></a>Introdução às coleções no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As coleções ajudam você o a organizar recursos em unidades gerenciáveis. Você pode criar coleções para atender às suas necessidades de gerenciamento de cliente e executar operações em vários recursos ao mesmo tempo. 

A maioria das tarefas de gerenciamento depende do uso de uma ou mais coleções. Embora você possa usar a coleção interna de Todos os sistemas, o uso dessa coleção para tarefas de gerenciamento não é uma prática recomendada. Crie coleções personalizadas para identificar mais especificamente os dispositivos ou os usuários para uma tarefa.  

 As coleções internas e personalizadas são exibidas nos nós **Coleções de Usuários** e **Coleções de Dispositivos**, no espaço de trabalho **Ativos e Conformidade**, no console do Configuration Manager.  

 As coleções que você exibiu recentemente aparecem no nó **Usuários** e no nó **Dispositivos**, no espaço de trabalho **Ativos e Conformidade**.  

Aqui estão alguns exemplos do uso de coleção:  

|Operação|Exemplo|  
|---------|-------|  
|Recursos de agrupamento|É possível criar coleções que agrupam os recursos baseados na hierarquia da sua organização.<br /><br /> Por exemplo, é possível criar uma coleção de todos os computadores na UO (Unidade Organizacional) "London Headquarters" do Active Directory. Para obter mais informações sobre como criar esse tipo de coleção, consulte [How to Create Collections in System Center Configuration Manager (Como criar coleções no System Center Configuration Manager)](../../../../core/clients/manage/collections/create-collections.md).<br /><br /> É possível usar essa coleção para operações como: definir configurações do Endpoint Protection, definir configurações de gerenciamento de energia do dispositivo ou instalar o cliente do Configuration Manager.|  
|[Implantação de aplicativo]|Você pode criar uma coleção de todos os computadores que não têm o Microsoft Office 2013 instalado e implantá-lo em todos os computadores nessa coleção.<br /><br /> Você também pode usar os requisitos do aplicativo para executar esta tarefa. Para obter mais informações, consulte [Como criar aplicativos com o System Center Configuration Manager](../../../../apps/deploy-use/create-applications.md).|  
|[Gerenciando as configurações do cliente](../../../../core/clients/deploy/about-client-settings.md)|Embora as configurações padrão do cliente no Configuration Manager sejam aplicáveis a todos os dispositivos e todos os usuários, você pode criar configurações de cliente personalizadas que sejam aplicáveis a uma coleção de dispositivos ou a um conjunto de usuários.<br /><br /> Por exemplo, se desejar que o controle remoto esteja disponível somente para alguns dispositivos, defina as configurações do cliente para permitir o controle remoto e, em seguida, defina as configurações personalizadas do cliente que não permitem o controle remoto e implante-as na coleção de clientes excepcionais. |  
|[Gerenciamento de energia](../power/introduction-to-power-management.md)|Você pode definir configurações de energia específicas por coleção.|  
|[Administração baseada em funções](../../../../core/servers/deploy/configure/configure-role-based-administration.md)|Usar coleções para controlar quais grupos de usuários têm acesso a vários recursos no console do Configuration Manager.|  
|[Janelas de Manutenção](../../../../core/clients/manage/collections/use-maintenance-windows.md)|Com as janelas de manutenção é possível definir um período de tempo no qual várias operações do Configuration Manager podem ser executadas nos membros de uma coleção de dispositivos. |  


## <a name="collection-types-in-configuration-manager"></a>Tipos de coleção no Configuration Manager  
 O Configuration Manager tem coleções internas para operações comuns e você também pode criar coleções personalizadas.   

### <a name="built-in-collections"></a>Coleções internas  
 Por padrão, o Configuration Manager inclui as seguintes coleções, que não podem ser modificadas.  

|**Nome da coleção**|Descrição|  
|-------------------------|-----------------|  
|**Todos os grupos de usuários**|Contém grupos de usuários que são descobertos usando a Descoberta de Grupo de Segurança do Active Directory.|  
|**Todos os Usuários**|Contém os usuários que são descobertos usando a Descoberta de Usuário do Active Directory.|  
|**Todos os usuários e grupos de usuários**|Contém as coleções Todos os Usuários e Todos os Grupos de Usuários. Essa coleção contém o maior escopo dos recursos de grupo de usuário e do usuário.|  
|**Todos os clientes de Desktop e Servidor**|Contém os dispositivos de área de trabalho e servidor que têm o cliente do Configuration Manager instalado. A associação é mantida pela Descoberta de Pulsação.|  
|**Todos os dispositivos móveis**|Contém os dispositivos móveis gerenciados pelo Configuration Manager. A associação é restrita para os dispositivos móveis que são atribuídos a um site ou descobertos pelo conector do Exchange Server com êxito.|  
|**Todos os sistemas**|Contém todos os clientes de Área de Trabalho e de Servidor, todos os dispositivos móveis, a coleção de todos os computadores desconhecidos e todos os dispositivos móveis registrados pelo Microsoft Intune. Essa coleção contém o maior escopo dos recursos de dispositivos.|  
|**Todos os computadores desconhecidos**|Contém registros de computador genérico para várias plataformas de computador. Você pode usar essa coleção para implantar um sistema operacional usando uma sequência de tarefas e a inicialização PXE, a mídia inicializável ou a mídia em pré-configuração.|  

### <a name="custom-collections"></a>Coleções personalizadas  
 Quando você cria uma coleção personalizada no Configuration Manager, a associação da coleção é determinada por uma ou mais regras de coleta, conforme descrito em [Como criar coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md). 

