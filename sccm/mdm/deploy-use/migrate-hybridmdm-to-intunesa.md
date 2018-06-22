---
title: Migrar usuários e dispositivos do MDM híbrido para o Intune autônomo
titleSuffix: Configuration Manager
description: Saiba como migrar usuários e dispositivos do MDM híbrido para o Intune no Azure.
author: aczechowski
manager: dougeby
ms.date: 09/12/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 1dd696ce-3e46-4dfa-a76d-592fe0f0320e
ms.openlocfilehash: 4e2471b06c1767bcf914000d626bb22b6ee2bd6b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32346314"
---
# <a name="migrate-hybrid-mdm-users-and-devices-to-intune-standalone"></a>Migrar usuários e dispositivos do MDM híbrido para o Intune autônomo

*Aplica-se a: System Center Configuration Manager (Branch Atual)*    

Leia este artigo quando você decidir que está pronto para iniciar a migração do MDM híbrido (Intune integrado com o Configuration Manager) para uma experiência somente em nuvem usando o Intune no Azure. Se você ainda não tiver decido, consulte [Escolher entre o Microsoft Intune autônomo e o gerenciamento de dispositivo móvel híbrido com o System Center Configuration Manager](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management). 

Você pode iniciar a migração para o Intune autônomo usando uma abordagem em fases que permite testar um pequeno subconjunto de usuários e dispositivos, enquanto a maioria dos usuários e dispositivos ainda é gerenciada com o MDM híbrido. Depois de verificar a funcionalidade do Intune, você poderá iniciar a migração de mais usuários para o Intune.    

Os tópicos a seguir fornecem as etapas para migrar seus usuários ao Intune autônomo usando uma abordagem em fases.    
  
1.  [Importar dados do Configuration Manager para o Microsoft Intune](migrate-import-data.md)   
    A ferramenta Importador de Dados do Intune coleta dados sobre os objetos que você seleciona na hierarquia do Configuration Manager, fornece detalhes sobre os objetos que você pode selecionar para importação e informações sobre o motivo pelo qual um objeto não pode ser importado e permite importar os objetos selecionados em seu locatário do Microsoft Intune. Embora esta etapa seja opcional, ela pode poupar bastante tempo por automatizar o processo de recriar objetos do Configuration Manager para o Intune. 
2.  [Preparar o Intune para migração de usuários](migrate-prepare-intune.md)    
    Valide os objetos importados do Configuration Manager, crie novos objetos, crie grupos do AAD e faça atribuições de objeto para esses grupos, instale conectores NDES e Exchange, etc. Quando você concluir as etapas e iniciar a migração para o Intune autônomo, o processo deverá ser transparente para os usuários.  
3.  [Alterar a autoridade de MDM para usuários específicos (autoridade de MDM mista)](migrate-mixed-authority.md)    
    Configure uma autoridade de MDM mista no mesmo locatário selecionando alguns usuários a serem gerenciados no Intune enquanto todos os outros dispositivos continuam a ser gerenciados com o MDM híbrido (Intune integrado ao Configuration Manager). Você pode testar se a funcionalidade do Intune está funcionando conforme o esperado nos dispositivos para um pequeno subconjunto de usuários antes de iniciar a migração de usuários adicionais. 
4.  [Alterar sua autoridade de MDM para o Intune autônomo](change-mdm-authority.md)     
    Altere sua autoridade de MDM no nível do locatário do Configuration Manager para o Intune. Todos os usuários e dispositivos restantes são migrados para o Intune autônomo. Você vai alterar a sua autoridade de MDM no nível do locatário depois de testar completamente a funcionalidade do Intune na etapa anterior e migrar a maioria ou todos os usuários.