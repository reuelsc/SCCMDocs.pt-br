---
title: "Configurar o inventário de software | Microsoft Docs"
description: "Configure o inventário de software e uma pasta de exclusão de inventário no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: cc226259-0e28-410a-94d3-223bdc948818
caps.latest.revision: 4
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 7ba943bee7faf417099cde0388649e4907525738


---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>Como configurar o inventário de software no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

É possível criar um arquivo oculto chamado **Skpswi.dat** e colocá-lo na raiz de um disco rígido do cliente para excluí-lo do inventário de software do System Center Configuration Manager. Você também pode colocar esse arquivo na raiz de qualquer estrutura de pastas que você deseja excluir do inventário de software. Esse procedimento pode ser usado para desabilitar o inventário de software em uma única estação de trabalho ou em um único servidor cliente, como um servidor de arquivos grandes.  

> [!NOTE]  
>  O inventário de software não realizará o inventário da unidade do cliente novamente, a menos que esse arquivo seja excluído da unidade no computador cliente.  

### <a name="to-exclude-folders-from-software-inventory"></a>Para excluir pastas do inventário de software  

1.  Usando o Notepad.exe, crie um arquivo vazio chamado **Skpswi.dat**.  

2.  Clique com o botão direito do mouse no arquivo do **Skpswi.dat** e clique em **Propriedades**. Nas propriedades do arquivo Skpswi.dat, selecione o atributo **Hidden** .  

3.  Coloque o arquivo **Skpswi.dat** na raiz de cada estrutura de pasta ou da unidade de disco rígido do cliente que você deseja excluir do inventário de software.  



<!--HONumber=Dec16_HO3-->


