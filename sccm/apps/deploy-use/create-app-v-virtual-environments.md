---
title: Criar ambientes virtuais do App-V | System Center Configuration Manager
description: Crie ambientes virtuais com o Microsoft Application Virtualization para que os aplicativos possam compartilhar dados entre si.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 625ea93d855089f6dbbdcc8368032e61b8a1ba0b


---
# <a name="create-app-v-virtual-environments-in-system-center-configuration-manager"></a>Criar ambientes virtuais App-V no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os ambientes virtuais do Microsoft Application Virtualization (App-V) no System Center Configuration Manager habilitam aplicativos virtuais implantados a compartilhar o mesmo sistema de arquivos e Registro em computadores Windows cliente. Isso significa que, diferentemente dos aplicativos virtuais padrão, esses aplicativos podem compartilhar dados entre si. Os ambientes virtuais são criados ou modificados em computadores cliente quando o aplicativo é instalado ou quando os clientes avaliam em seguida seus aplicativos instalados. Você pode ordenar esses aplicativos para que, caso vários aplicativos tentem modificar um sistema de arquivo ou um valor de Registro, o aplicativo de ordem superior tenha prioridade.  

> [!IMPORTANT]  
>  Não confie em ambientes virtuais do App-V para fornecer proteção de segurança, por exemplo, contra malware.  

 Use o procedimento a seguir para criar ambientes virtuais do App-V no Configuration Manager.  

## <a name="create-an-app-v-virtual-environment"></a>Criar um ambiente virtual do App-V  

1.  No console do Configuration Manager, clique em **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Ambientes Virtuais do App-V**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Ambiente Virtual**.  

4.  Na caixa de diálogo **Criar Ambiente Virtual** , especifique as seguintes informações:  

    -   **Nome** - Especifique um nome exclusivo para o ambiente virtual que tenha, no máximo, 128 caracteres.  

    -   **Descrição** - Opcionalmente, especifique uma descrição para o ambiente virtual.  

5.  Clique em **Adicionar** para adicionar um novo tipo de implantação no ambiente virtual. Você deve adicionar pelo menos um tipo de implantação.  

6.  Na caixa de diálogo **Adicionar Aplicativos** , especifique o **Nome do Grupo** de até 128 caracteres que será usado para se referir a esse grupo de aplicativos adicionado ao ambiente virtual.  

7.  Clique em **Adicionar**, selecione os aplicativos do App-V 5 e os tipos de implantação que você deseja adicionar ao grupo, e clique em **OK**.  

8.  Na caixa de diálogo **Adicionar Aplicativos** , você pode clicar em **Aumentar Ordem** ou **Diminuir Ordem** para especificar qual aplicativo terá prioridade se diversos aplicativos tentarem modificar o sistema de arquivos ou as configurações de Registro no mesmo ambiente virtual.  

9. Clique em **OK** para retornar à caixa de diálogo **Criar Ambiente Virtual** .  

10. Quando tiver terminado de adicionar grupos, clique em **OK** para criar o ambiente virtual. O novo ambiente virtual é exibido no nó **Ambientes Virtuais do App-V** do console do Configuration Manager. É possível monitorar o status de seus ambientes virtuais usando o relatório **Status de Ambiente Virtual do App-V**.  

    > [!NOTE]  
    >  O ambiente virtual será adicionado ou modificado em computadores cliente quando o aplicativo for instalado ou quando o cliente avaliar em seguida seus aplicativos instalados.  



<!--HONumber=Nov16_HO1-->


