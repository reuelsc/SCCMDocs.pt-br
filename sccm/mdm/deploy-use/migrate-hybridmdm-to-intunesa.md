---
title: "Migrar usuários e dispositivos do MDM híbrido para o Intune autônomo"
titleSuffix: Configuration Manager
description: "Saiba como migrar usuários e dispositivos do MDM híbrido para o Intune no Azure."
keywords: 
author: dougeby
manager: angrobe
ms.date: 09/12/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: 1dd696ce-3e46-4dfa-a76d-592fe0f0320e
ms.openlocfilehash: a6e430248fdeedd310087c9a32c6d69ca1864a09
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
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

<!--
The following provides a typical workflow for migrating users from hybrid MDM to Intune standalone:
1.  Admin runs the Microsoft Intune Data Importer Tool, selecting which objects and assignments to import. Selected objects are imported into Intune standalone.
    1. Some objects cannot be imported because they contain settings the tool does not understand or setting that are not available in Intune standalone.
    2. Assignments are migrated. However, only if the collection an object was targeted to is based on a single Active Directory (AD) security group and the same group exists in Azure Active Directory (AAD).
    > [!Note]    
    > If you want, you can skip this step and create the objects that you want directly in Intune in the Azure portal without running the Intune Data Importer Tool. 
2.  Admin logs into the Intune on Azure portal
    1. Creates any additional objects required for their organization that were not imported by the Microsoft Intune Data Importer tool.
    2. Creates any required AAD groups and makes any additional assignments for each object to AAD groups.
    3. Installs the NDES connector on an on-premises server if using SCEP or PFX certificate deployment.
    4. Installs the Exchange connector on an on-premises server if using conditional access. 
3.  Admin ensures that all existing Intune users in their organization have an Intune license assigned to them using AAD or the Office administrator portal.
4.  Admin selects some test users to migrate to Intune standalone and removes them from the collection associated with the Intune subscription in Configuration Manager.
5.  Once removed from the collection, the user and all devices are managed by Intune in the Azure portal. Remaining users and devices continue to be managed by hybrid mobile device management in Configuration Manager. 
6.  Admin validates that things are working as expected on the device and moves more users to Intune standalone by removing them from the collection associated with the Intune subscription in Configuration Manager.
7.  Once the admin is comfortable with the functionality in Intune standalone, they can move the rest of their users and devices by switching their MDM authority to Intune standalone. This can be done by removing the Intune subscription from SCCM and choosing to change the MDM authority. Tenant level policies will be automatically migrated to Intune standalone, all objects and assignments in Intune standalone will remain, and devices will not be required to re-enroll.
-->