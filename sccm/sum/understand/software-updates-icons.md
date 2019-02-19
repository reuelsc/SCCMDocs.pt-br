---
title: Ícones usados para as atualizações de software
titleSuffix: Configuration Manager
description: O console do Configuration Manager contém ícones que indicam um estado para o grupo de atualização de software ou atualização sincronizada.
author: aczechowski
manager: dougeby
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 63c5ef72-5715-4d86-85a2-71beba469fab
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 898eabbb142a5562464950812cbfd057d3d65187
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56128265"
---
# <a name="icons-used-for-software-updates-in-system-center-configuration-manager"></a>Ícones usados para as atualizações de software no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Atualizações de software sincronizadas são exibidas no console do Configuration Manager e a primeira coluna de cada atualização de software contém um ícone que indica um estado específico. Grupos de atualização de software também são representados por um ícone que fornece informações sobre o estado das atualizações de software contidas no grupo. Esta seção fornece informações sobre os ícones de atualização de software e o que cada ícone representa.  

## <a name="icons-for-software-updates"></a>Ícones de atualizações de software  
 Atualizações de software sincronizadas são representadas por um dos ícones a seguir.  

### <a name="normal-icon"></a>Ícone normal  
 ![ícone](../media/Normal.jpg "Ícone normal") O ícone com a seta verde representa uma atualização de software normal.  

 **Descrição:**  

 Atualizações de software normais foram sincronizadas e estão disponíveis para implantação de software.  

 **Problemas operacionais:**  

 não há problemas operacionais.  

### <a name="expired-icon"></a>Ícone expirado  
 ![ícone](../media/Expired.jpg "Ícone expirado") O ícone com um X preto representa uma atualização de software expirada. Você também pode identificar as atualizações de software expiradas analisando a coluna **Expirada** da atualização de software quando ela for exibida no console do Configuration Manager.  

 **Descrição:**  

 Anteriormente, atualizações de software expiradas podiam ser implantadas em computadores cliente, mas após uma atualização de software expirar, novas implantações não podem ser criadas para as atualizações de software. As atualizações de software expiradas são removidas das implantações ativas e não estarão mais disponíveis para os clientes.  

 **Problemas operacionais:**  

 não há problemas operacionais.

### <a name="superseded-icon"></a>Ícone substituído  
 ![ícone](../media/Superseded.jpg "Ícone substituído") O ícone com a estrela amarela representa uma atualização de software substituída. Você também pode identificar atualizações de software substituídas analisando a coluna **Substituída** da atualização de software quando ela for exibida no console do Configuration Manager.  

 **Descrição:**  

 Atualizações de software que foram substituídas por versões mais recentes da atualização de software. Normalmente, uma atualização de software que substitui outra tem uma ou mais das seguintes características:  

- Melhora, aumenta ou acrescenta algo à correção fornecida por uma ou mais atualizações lançadas anteriormente.  

- Melhora a eficiência do pacote de arquivos de atualização de software, que o cliente instala se a atualização for aprovada para instalação. Por exemplo, a atualização de software substituída pode conter arquivos que não são mais relevantes para a correção ou para os sistemas operacionais com suporte pela nova atualização. Sendo assim, esses arquivos não são incluídos no pacote de arquivos da atualização de software de substituição.  

- Atualiza versões mais novas de um produto ou, em outras palavras, que não são mais aplicáveis a versões ou configurações mais antigas de um produto. Atualizações de software também podem substituir outras atualizações de software caso tenham sido feitas modificações para expandir o suporte para idiomas. Por exemplo, uma revisão posterior da atualização de um produto do Microsoft Office pode remover o suporte de um sistema operacional mais antigo, mas adicionar suporte para novos idiomas na versão de atualização de software inicial.  

  Na guia Regras de Substituição nas propriedades do Componente de Ponto de Atualização de Software, você pode especificar como gerenciar atualizações de software substituídas. Para obter mais informações, consulte [Supersedence rules](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules).  

  **Problemas operacionais:**  

  Quando possível, implante a atualização de software de substituição nos computadores cliente em vez da atualização de software substituídas. Você pode exibir uma lista das atualizações de software que substituem a atualização de software na guia **Informações de Substituição** nas propriedades da atualização de software.  

### <a name="invalid-icon"></a>Ícone inválido  
 ![ícone](../media/Invalid.jpg "Ícone inválido") O ícone com um X vermelho representa uma atualização de software inválida.  

 **Descrição:**  

 Atualizações de software inválidas estão em uma implantação ativa, mas, por algum motivo, o conteúdo (arquivos de atualização de software) não está disponível. Veja a seguir cenários em que esse estado pode ocorrer:  

- Você implanta com êxito a atualização de software, mas o arquivo de atualização de software é removido do pacote de implantação e não está mais disponível.  

- Você cria uma implantação de atualização de software em um site e o objeto de implantação é replicado com êxito para um site filho, mas o pacote de implantação não foi replicado com êxito para o site filho.  

  **Problemas operacionais:**  

  Quando o conteúdo está ausente para uma atualização de software, os clientes não conseguem instalar a atualização de software até que o conteúdo fique disponível no ponto de distribuição. Você pode redistribuir o conteúdo para pontos de distribuição usando a ação **Redistribuir** . Quando o conteúdo está ausente para uma atualização de software em uma implantação criada em um site pai, a atualização de software deve ser replicada ou redistribuída para o site filho. Para obter mais informações sobre a redistribuição de conteúdo, consulte [Gerenciar o conteúdo que você distribuiu](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  

### <a name="metadata-only-icon"></a>Ícone somente metadados
 ![ícone](../media/MetadataOnly.png "Ícone somente metadados") O ícone com a seta azul representa uma atualização de software somente de metadados.

 **Descrição:**  

 Atualizações de software somente de metadados estão disponíveis no console do Configuration Manager para relatórios. Você não pode implantar ou baixar atualizações de software somente de metadados porque um arquivo de atualização de software não está associado aos metadados das atualizações de software.  

 **Problemas operacionais:**  

 Atualizações de software somente de metadados estão disponíveis para fins de relatório e não se destinam a implantação de atualização de software.  

## <a name="icons-for-software-update-groups"></a>Ícones de grupos de atualizações de software  
 Grupos de atualizações de software são representadas por um dos ícones a seguir.  

### <a name="normal-icon"></a>Ícone normal  
 ![ícone](../media/Normal.jpg "Ícone normal") O ícone com a seta verde representa um grupo de atualizações de software que contém apenas atualizações de software normais.  

 **Problemas operacionais:**  

 não há problemas operacionais.  

### <a name="expired-icon"></a>Ícone expirado  
 ![ícone](../media/Expired.jpg "Ícone expirado") O ícone com o X preto representa um grupo de atualizações de software que contém uma ou mais atualizações de software expiradas.  

 **Problemas operacionais:**  

 Remova ou substitua atualizações de software expiradas do grupo de atualização de software quando possível.  

### <a name="superseded-icon"></a>Ícone substituído  
 ![ícone](../media/Superseded.jpg "Ícone substituído") O ícone com a estrela amarela representa um grupo de atualizações de software que contém uma ou mais atualizações de software substituídas.  

 **Problemas operacionais:**  

 Substitua a atualização de software substituída no grupo de atualizações de software pela atualização de software substituta quando possível.  

### <a name="invalid-icon"></a>Ícone inválido  
 ![ícone](../media/Invalid.jpg "Ícone inválido") O ícone com o X vermelho representa um grupo de atualizações de software que contém uma ou mais atualizações de software inválidas.  

 **Problemas operacionais:**  

 Quando o conteúdo está ausente para uma atualização de software, os clientes não conseguem instalar a atualização de software até que o conteúdo fique disponível no ponto de distribuição. Você pode redistribuir o conteúdo para pontos de distribuição usando a ação **Redistribuir** . Quando o conteúdo está ausente para uma atualização de software em uma implantação criada em um site pai, a atualização de software precisa ser replicada ou redistribuída para o site filho. Para obter mais informações sobre a redistribuição de conteúdo, consulte [Gerenciar o conteúdo que você distribuiu](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  
