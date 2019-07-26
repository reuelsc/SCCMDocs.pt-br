---
title: Definir limites
titleSuffix: Configuration Manager
description: Entenda como definir locais de rede na sua intranet que podem conter dispositivos que você deseja gerenciar.
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7218f467df72d9ea9d9ae7b3e4bb15be3c74bda2
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68338183"
---
# <a name="define-network-locations-as-boundaries-for-system-center-configuration-manager"></a>Definir locais de rede como limites para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os limites do Configuration Manager são locais na sua rede que contêm dispositivos que você deseja gerenciar. O limite em que um dispositivo está é equivalente ao site do Active Directory ou ao endereço IP da rede identificado pelo cliente do Configuration Manager instalado no dispositivo.
- Você pode criar limites individuais manualmente. No entanto, o Configuration Manager não dá suporte à entrada direta de uma super-rede como limite. Em vez disso, use o tipo de limite de intervalo de endereços IP.
- Você pode configurar o método [Descoberta de Florestas do Active Directory](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) para detecção automática e criar limites para cada sub-rede IP e Site do Active Directory detectado. Quando a descoberta de florestas do Active Directory identifica uma super-rede que é atribuída a um site do Active Directory, o Configuration Manager converte a super-rede em um limite de intervalo de endereços IP.  

Não é incomum um dispositivo usar um endereço IP de que o administrador do Configuration Manager não esteja ciente. Quando o local de rede de um dispositivo for incerto, confirme o que o dispositivo reporta como seu local usando o comando **IPCONFIG** no dispositivo.  

Ao criar um limite, ele recebe automaticamente um nome baseado no tipo e no escopo do limite. Não é possível modificar esse nome. Em vez disso, você pode especificar uma descrição para ajudar a identificar o limite no console do Configuration Manager.  

Cada limite está disponível para uso por todos os sites na sua hierarquia. Depois que um limite tiver sido criado, você poderá modificar suas propriedades para fazer o seguinte:  
- Adicionar o limite a um ou mais grupos de limites.  
- Alterar o tipo ou o escopo do limite.  
- Exiba a guia **Sistemas de Sites** de limites para ver quais servidores do sistema de sites (pontos de distribuição, pontos de migração de estado e pontos de gerenciamento) estão associados ao limite.  

## <a name="to-create-a-boundary"></a>Para criar um limite  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** > **Limites**  

2.  Na guia **Início** , no grupo **Criar** , clique em **Criar Boundary**.  

3.  Na guia **Geral** da caixa de diálogo Criar Limite, é possível especificar uma **Descrição** para identificar o limite por um nome amigável ou de referência.  

4.  Selecione um **Tipo** para esse limite:  

    - Se selecionar **Sub-rede IP**, será necessário especificar uma **ID de Sub-rede** para esse limite.  
      > [!TIP]  
      > Você pode especificar a **Rede** e a **Máscara de Sub-rede** para que a **ID de Sub-rede** seja especificada automaticamente. Quando você salva o limite, somente o valor da ID de Sub-rede é salvo.  

    - Se selecionar o **site do Active Directory**, você deverá especificar ou **Procurar** um site do Active Directory na floresta local do servidor do site.  
        
      - Ao especificar um site do Active Directory para um limite, o limite inclui uma sub-rede IP que é um membro de um site do Active Directory. Se a configuração do site do Active Directory mudar no Active Directory, os locais de rede inclusos nesse limite também mudarão.  

      - Limites de site do Active Directory não funcionam para clientes do Azure AD puros. Se eles fizerem roaming local, não se encaixarão em nenhum limite se definido apenas usando Sites do AD.

    - Se selecionar o **Prefixo IPv6**, você deverá especificar um **Prefixo** no formato de prefixo IPv6.  

    - Se selecionar **Intervalo de endereços IP**, será necessário especificar um **Endereço IP Inicial** e um **Endereço IP Final** que inclui parte de uma sub-rede IP ou várias sub-redes IP.    

5.  Clique em **OK** para salvar o novo limite.  

## <a name="to-configure-a-boundary"></a>Para configurar um limite  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** > **Limites**  

2.  Selecione o limite que você deseja modificar.  

3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Na caixa de diálogo **Propriedades** do limite, selecione a guia **Geral** para editar a **Descrição** ou **Tipo** do limite. Você também pode alterar o escopo de um limite editando os locais de rede para o limite. Por exemplo, para um limite de site do Active Directory, você pode especificar um novo nome de site do Active Directory.  

5.  Selecione a guia **Sistemas de Site** para exibir os sistemas de site que estão associados a esse limite. Não é possível alterar essa configuração a partir das propriedades de um limite.  

    > [!TIP]  
    > Para que um servidor do sistema de sites seja listado como um sistema de sites para um limite, ele deve ser associado como um servidor do sistema de sites a pelo menos um grupo de limites que inclui esse limite. Isso é configurado na guia **Referências** de um grupo de limite.  

6.  Selecione a guia **Grupos de Limites** para modificar a associação a um grupo de limites para esse limite:  

    - Para adicionar esse limite a um ou mais grupos de limites, clique em **Adicionar**, marque a caixa de seleção para um ou mais grupos de limites e clique em **OK**.  

    - Para remover esse limite de um grupo de limites, selecione o grupo de limites e clique em **Remover**.  

7.  Clique em **OK** para fechar as propriedades de limite e salvar a configuração.  
