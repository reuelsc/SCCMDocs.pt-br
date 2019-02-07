---
title: MDM híbrido com o Microsoft Intune
titleSuffix: Configuration Manager
description: Saiba mais sobre o MDM (gerenciamento de dispositivos móveis) híbrido com o Configuration Manager e o Microsoft Intune.
ms.date: 01/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a744463aa82951d68125c0d17d88ba5e8a1f2703
ms.sourcegitcommit: 33e066aceaf321add1031df00e552e942c8351a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2019
ms.locfileid: "55764405"
---
# <a name="hybrid-mdm-with-configuration-manager-and-microsoft-intune"></a>MDM híbrido com o Configuration Manager e o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

> [!Important]  
> O gerenciamento híbrido de dispositivos móveis é um [recurso preterido](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures) desde 14 de agosto de 2018.
> <!--Intune feature 2683117-->  
> Desde o lançamento no Azure há mais de um ano, o Intune adicionou centenas de novos recursos de serviço solicitados pelo cliente e líderes de mercado. Agora, ele oferece muito mais recursos do que os oferecidos pelo gerenciamento de dispositivos móveis híbrido (MDM). O Intune no Azure oferece uma experiência administrativa mais integrada e simplificada para suas necessidades de mobilidade corporativa.
> 
> Como resultado, a maioria dos clientes escolhe o Intune no Azure ao invés do MDM híbrido. A quantidade de clientes que usa o MDM híbrido continua a diminuir à medida que mais clientes migram para a nuvem. Portanto, em 1º de setembro de 2019, a Microsoft aposentará a oferta de serviço do MDM híbrido. Planeje sua [migração para o Intune no Azure](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa) para suas necessidades de MDM. 
> 
> Essa alteração não afeta o Configuration Manager local ou o [cogerenciamento para dispositivos Windows 10](/sccm/comanage/overview). Se você não tiver certeza se está usando o MDM híbrido, acesse o espaço de trabalho **Administração** do console do Configuration Manager, expanda **Serviços de Nuvem** e clique em **Assinaturas do Microsoft Intune**. Se você tiver uma assinatura do Microsoft Intune definida, seu locatário está configurado para o MDM híbrido.
> 
> **Como isso me afeta?**
> 
> - A Microsoft oferecerá suporte para o seu uso de MDM híbrido até o próximo ano. O recurso continuará recebendo as principais correções de bugs. A Microsoft oferecerá suporte à funcionalidade existente em novas versões do sistema operacional, como o registro no iOS 12. Não haverá novos recursos para o MDM híbrido.  
> 
> - Se você migrar para o Intune no Azure antes do final da oferta do MDM híbrido, não deverá haver impacto para o usuário final.  
> 
> - O licenciamento continua o mesmo. As licenças do Intune no Azure estão inclusas no MDM híbrido.  
> 
> - O recurso MDM local no Configuration Manager não é preterido. A partir do Configuration Manager versão 1810, você pode usar o MDM local sem uma conexão do Intune. Para obter mais informações, consulte [Intune uma conexão não é mais necessário para novas implantações de MDM local](/sccm/core/plan-design/changes/whats-new-in-version-1810#bkmk_opmdm). 
> 
> - O recurso de acesso condicional no local do Configuration Manager também é preterido com o MDM híbrido. Se você usar o acesso condicional em dispositivos gerenciados com o cliente do Configuration Manager, para certificar-se de que eles ainda estão protegidos, primeiro habilite o acesso condicional no Intune para os dispositivos antes de migrar. Habilitar o cogerenciamento no Configuration Manager, mover a carga de trabalho de política de conformidade para o Intune e, em seguida, concluir a migração do Intune híbrido para Intune autônomo. Para obter mais informações, consulte [acesso condicional com o cogerenciamento](https://docs.microsoft.com/sccm/comanage/quickstart-conditional-access). 
> 
> - No dia 1º de setembro de 2019, todos os dispositivos com MDM híbrido restantes deixarão de receber políticas, aplicativos ou atualizações de segurança.  
> 
> **O que preciso fazer para me preparar para essa alteração?**
> 
> - Comece a planejar sua migração para o MDM pelo console do ConfigMgr para o Azure. Muitos clientes, incluindo a TI da Microsoft, passaram por este processo. Para saber mais, confira este [estudo de caso da Microsoft](https://aka.ms/Intune_MSFT).  
> 
> - Revise as seguintes ferramentas e documentação para simplificar o processo de migração do MDM híbrido para o Intune no Azure:  
>     - [Importar dados do Configuration Manager para o Microsoft Intune](/sccm/mdm/deploy-use/migrate-import-data)  
>     - [Migrar usuários e dispositivos do MDM híbrido para o Intune autônomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)  
> 
> - Entre em contato com seu parceiro registrado ou com o FastTrack para obter assistência. O [FastTrack for Microsoft 365](https://aka.ms/hybrid_fasttrack) pode ajudar na migração do MDM híbrido para o Intune no Azure. 
> 
> Para saber mais, confira [a postagem no blog de suporte do Intune](https://aka.ms/hybrid_notification).



Com o recurso de gerenciamento de dispositivos móveis (MDM) híbrido do Configuration Manager, gerencie dispositivos iOS, Windows e Android. Todas as tarefas de gerenciamento são tratadas no console do Configuration Manager, em que você executa o restante de suas tarefas de gerenciamento de forma diretamente integrada ao serviço online do Microsoft Intune pela Internet. Use o Configuration Manager para permitir que os usuários acessem recursos da empresa em seus dispositivos de maneira segura e gerenciada. Usando o gerenciamento de dispositivos, você protege os dados da empresa enquanto permite que os usuários registrem dispositivos pessoais ou da empresa para acessar dados da empresa. 

Este artigo pressupõe que você usa o Configuration Manager para gerenciar computadores. Também pressupõe que você esteja interessado em ampliar o console do Configuration Manager com o Intune para gerenciar dispositivos móveis. 



## <a name="capabilities"></a>Capacidades

O MDM híbrido oferece suporte aos seguintes recursos de gerenciamento em dispositivos:

-   Desativar e apagar dispositivos  

-   Definir configurações de conformidade, como senhas, segurança, roaming, criptografia e comunicação sem fio  

-   Implantar aplicativos de LOB (linha de negócios) em dispositivos  

-   Implantar aplicativos em dispositivos que se conectam à Windows Store, Windows Phone Store, App Store ou Google Play  

-   Coletar inventário de hardware  

-   Coletar inventário de software usando relatórios internos  

Para ler sobre os novos recursos que estão disponíveis para o MDM híbrido, consulte [What's new in hybrid mobile device management](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management) (O que há de novo no gerenciamento de dispositivo móvel híbrido).



## <a name="hybrid-mdm-enrollment"></a>Registro no MDM híbrido

Para colocar dispositivos no gerenciamento híbrido, esses dispositivos devem estar registrados no serviço. A forma como os dispositivos são registrados depende do tipo de dispositivo, da propriedade e do nível de gerenciamento necessário.

- **"Traga seu próprio dispositivo" (BYOD)**: Os usuários registram seus telefones pessoais, tablets ou PCs  

- **Dispositivo corporativo (COD)**: Habilitar cenários de gerenciamento como apagamento remoto, dispositivos compartilhados ou afinidade de usuário para um dispositivo  

- Se usar o [Exchange ActiveSync](/sccm/mdm/plan-design/device-enrollment-methods#mobile-device-management-with-exchange-activesync-and-configuration-manager), seja localmente ou hospedado na nuvem, você poderá habilitar o gerenciamento simples do Intune sem o registro. Computadores Windows também podem ser gerenciados usando o [Software cliente do Intune](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune).
