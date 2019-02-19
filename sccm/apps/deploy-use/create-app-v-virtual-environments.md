---
title: Criar um ambiente virtual do App-V
titleSuffix: Configuration Manager
description: Crie ambientes virtuais com o Microsoft Application Virtualization para que os aplicativos possam compartilhar dados entre si.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2becf31d807f0854bf6ab9d4eb58adf84d8ab7e6
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56135755"
---
# <a name="create-app-v-virtual-environments-in-system-center-configuration-manager"></a>Criar ambientes virtuais App-V no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Em um ambiente virtual do Microsoft App-V (Application Virtualization) no System Center Configuration Manager (Configuration Manager), os aplicativos virtuais implantados podem compartilhar o mesmo sistema de arquivos e Registro em computadores clientes Windows. Ao contrário dos aplicativos virtuais padrão, esses aplicativos podem compartilhar dados entre si. Os ambientes virtuais são criados ou modificados em computadores cliente quando o aplicativo é instalado ou quando os clientes avaliam em seguida seus aplicativos instalados. Você pode ordenar esses aplicativos para que, caso vários aplicativos tentem modificar um sistema de arquivo ou um valor de Registro, o aplicativo de ordem superior tenha prioridade.  

> [!IMPORTANT]  
>  Não confie em ambientes virtuais do App-V para fornecer proteção de segurança, como contra malware.  

 Use o procedimento a seguir para criar um ambiente virtual do App-V no Configuration Manager.  

## <a name="create-an-app-v-virtual-environment"></a>Criar um ambiente virtual do App-V  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativo** > **Ambientes Virtuais do App-V**.  

3.  Na guia **Início**, no grupo **Criar**, escolha **Criar Ambiente Virtual**.  

4.  Na caixa de diálogo **Criar Ambiente Virtual**, insira as seguintes informações:  

    -   **Nome**.  Insira um nome exclusivo para o ambiente virtual (no máximo 128 caracteres).  

    -   **Descrição**. (Opcional) Insira uma descrição para o ambiente virtual.  

5.  Para adicionar um novo tipo de implantação no ambiente virtual, escolha **Adicionar**. Você deve adicionar pelo menos um tipo de implantação.  

6.  Na caixa de diálogo **Adicionar Aplicativos**, especifique o **Nome do grupo** (no máximo 128 caracteres). Você usará esse nome para referir-se ao grupo de aplicativos que adicionará ao ambiente virtual.  

7.  Escolha **Adicionar**, selecione os aplicativos do App-V 5 e os tipos de implantação que deseja adicionar ao grupo e, em seguida, escolha **OK**.  

8.  Na caixa de diálogo **Adicionar Aplicativos**, você poderá selecionar **Aumentar Ordem** ou **Diminuir Ordem** para especificar qual aplicativo terá prioridade se diversos aplicativos tentarem modificar as configurações do sistema de arquivos ou do Registro no mesmo ambiente virtual.  

9. Para retornar à caixa de diálogo **Criar Ambiente Virtual**, escolha **OK**.  

10. Ao terminar a adição de grupos, escolha **OK** para criar o ambiente virtual. O novo ambiente virtual é exibido no nó **Ambientes Virtuais do App-V** do console do Configuration Manager. Você pode monitorar o status dos seus ambientes virtuais usando o relatório Status do ambiente virtual do App-V.  

    > [!NOTE]  
    >  O ambiente virtual será adicionado ou modificado nos computadores clientes quando o aplicativo for instalado ou quando o cliente fizer a próxima avaliação dos aplicativos instalados.  
