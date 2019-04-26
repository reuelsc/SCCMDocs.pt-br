---
title: Migrar recursos do MDM híbrido para o Intune autônomo
titleSuffix: Configuration Manager
description: Saiba como migrar usuários e dispositivos do MDM híbrido para o Intune no Azure.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/14/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 1dd696ce-3e46-4dfa-a76d-592fe0f0320e
ms.collection: M365-identity-device-management
ms.openlocfilehash: e2b62362bfcc9a76e407e9c0124306f83ac4a782
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62282078"
---
# <a name="migrate-hybrid-mdm-users-and-devices-to-intune-standalone"></a>Migrar usuários e dispositivos do MDM híbrido para o Intune autônomo

*Aplica-se a: System Center Configuration Manager (Branch Atual)*    

Este artigo aborda a migração do MDM híbrido para uma experiência somente na nuvem usando o Intune no Azure. 

> [!Important]  
> O gerenciamento híbrido de dispositivos móveis é um [recurso preterido](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures) desde 14 de agosto de 2018. Para saber mais, confira [O que é o MDM híbrido](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  


Inicie a migração para o Intune autônomo usando uma abordagem em fases. Com essa abordagem, você testa um pequeno subconjunto de usuários e dispositivos, enquanto a maioria de seus usuários e dispositivos ainda é gerenciada com o MDM híbrido. Depois de verificar a funcionalidade do Intune, inicie a migração de mais recursos para o Intune.    

Para obter mais informações, consulte os seguintes artigos:    
  
1.  [Importar dados do Configuration Manager para o Microsoft Intune](migrate-import-data.md)   

    A ferramenta Importador de Dados do Intune:  

    - Coleta dados sobre os objetos que você seleciona na hierarquia do Configuration Manager  

    - Fornece detalhes sobre os objetos que você pode selecionar para importação   

    - Fornece informações sobre o motivo pelo qual alguns objetos não podem ser importados  

    - Possibilita importar objetos selecionados em seu locatário do Microsoft Intune  

    Esta etapa é opcional. Você pode economizar tempo automatizando o processo de recriar objetos do Configuration Manager para o Intune.  

2.  [Preparar o Intune para migração de usuário](migrate-prepare-intune.md)    

    - Validar objetos importados do Configuration Manager  

    - Criar novos objetos  

    - Crie grupos do Azure AD e atribua objetos a esses grupos  

    - Instale conectores NDES e Exchange  

    Quando você concluir as etapas e iniciar a migração para o Intune autônomo, não há nenhum impacto significativo para seus usuários.   

3.  [Alterar a autoridade de MDM para usuários específicos (autoridade de MDM mista)](migrate-mixed-authority.md)    

    Configure uma autoridade de MDM mista no mesmo locatário. Selecione alguns usuários para serem gerenciados no Intune, enquanto continua gerenciando todos os outros dispositivos com o MDM híbrido. Teste se o recurso do Intune está funcionando em um pequeno subconjunto de usuários de dispositivos antes de iniciar a migração de usuários adicionais.   

4.  [Alterar sua autoridade de MDM para o Intune autônomo](change-mdm-authority.md)     

    Altere sua autoridade de MDM no nível do locatário do Configuration Manager para o Intune. Todos os usuários e dispositivos restantes são migrados para o Intune autônomo. Depois de testar completamente os recursos do Intune na etapa anterior e migrar a maioria ou todos os seus usuários, altere a autoridade do MDM no nível do locatário.



## <a name="request-assistance"></a>Solicitar assistência
<!--Intune bug 2339232-->
Para solicitar assistência do programa Microsoft FastTrack, começar acessando [FastTrack para o Microsoft 365](https://fasttrack.microsoft.com/microsoft365/capabilities?view=security).

1. Clique em "Entrar" e insira sua ID da organização.  

2. Vá até o Painel e siga as instruções para acessar o formulário **Solicitação de assistência**.    

3. A Microsoft revisa sua solicitação e a encaminha para a equipe apropriada para atender às suas necessidades e elegibilidade específicas.  

Neste painel você encontra as práticas recomendadas, as ferramentas e os recursos dos especialistas do FastTrack para fazer a sua experiência com o Microsoft Cloud ser ideal.

