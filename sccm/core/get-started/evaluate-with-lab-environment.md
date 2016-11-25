---
title: "Avaliar o System Center Configuration Manager compilando seu próprio ambiente de laboratório"
description: "Crie um ambiente de laboratório para avaliar o System Center Configuration Manager para uso em sua organização."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
caps.latest.revision: 25
caps.handback.revision: 0
author: brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 363e6a929b72e027d5fff7584905fb552dc695b0


---
# <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>Avaliar o System Center Configuration Manager compilando seu próprio ambiente de laboratório

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Saiba como criar um ambiente de laboratório para avaliar o System Center Configuration Manager para uso em sua organização.  

## <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>Avaliar o System Center Configuration Manager ao compilar seu próprio ambiente de laboratório  
 O System Center Configuration Manager é uma ferramenta poderosa e complexa para gerenciar usuários, dispositivos e software. Recomendamos que você realize uma avaliação total do System Center Configuration Manager antes da implantação completa, para que seja possível unir o entendimento conceitual com exercícios práticos.  

 Este guia destina-se principalmente a administradores que avaliam o uso do Configuration Manager em ambientes corporativos.  

-   Administradores que buscam uma solução para gerenciar por completo computadores, servidores e dispositivos móveis  

-   Administradores em setores de alta segurança que exigem a segurança do gerenciamento de dispositivo local com a flexibilidade do gerenciamento de dispositivo baseado em nuvem  

-   Administradores que buscam gerenciar o escalonamento vertical de sua arquitetura de servidor local  

### <a name="what-this-lab-does"></a>O que esse laboratório faz  
 O principal objetivo de criar esse ambiente é fornecer o conhecimento geral para começar a trabalhar com o Configuration Manager, bem como aprimorar seu entendimento do Configuration Manager na prática. Para isso, você acompanhará um assembly acelerado da versão atual do Configuration Manager, usando dois servidores:  

-   Um que hospeda o Active Directory, o Controlador de Domínio e o servidor DNS  

-   E um segundo, que hospeda o Configuration Manager e todos os componentes do SQL Server de associados.  

-   Computadores cliente são instalados no Hyper-V. O laboratório em si também pode ser executado como um sistema totalmente virtualizado em um único servidor.  

### <a name="what-this-lab-does-not-do"></a>O que este laboratório não faz  
 Este laboratório não apresentará todos os cenários do Configuration Manager e não foi projetado para ser migrado imediatamente para um ambiente ativo.  

 Ao compilar este laboratório, você terá um ambiente funcional para trabalhar. No entanto, esse ambiente não será otimizado em relação ao desempenho do sistema, gerenciamento de espaço em disco, armazenamento do SQL Server, etc.  

###  <a name="a-namebkmkevalreca-recommended-reading-prior-to-beginning-the-lab"></a><a name="BKMK_EvalRec"></a> Leitura recomendada antes de começar o laboratório  
 Há uma grande quantidade de conteúdo disponível na [Documentação do System Center Configuration Manager](http://docs.microsoft.com/sccm/). Foi incluída abaixo uma seleção de tópicos desta biblioteca, cuja leitura é recomendada antes de começar estes exercícios, para todos os administradores que trabalham em laboratórios.  

-   Conheça os conceitos básicos do console do Configuration Manager, portais do usuário final e cenários de exemplo na [Introdução ao System Center Configuration Manager](../../core/understand/introduction.md)  

-   Saiba mais sobre os recursos de gerenciamento primário do Configuration Manager em [Recursos e funcionalidades do System Center Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md)  

-   Reforce seu conhecimento com os [Conceitos básicos do System Center Configuration Manager](../../core/understand/fundamentals.md)  

-   Aprenda a importância de funções de segurança em [Conceitos básicos da administração baseada em funções para o System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md)  

-   Conhecer esses [Conceitos de gerenciamento de conteúdo](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_Concepts) pode fornecer conceitos específicos relacionados ao gerenciamento de conteúdo  

-   [Entenda como os clientes encontram serviços e recursos do site para o System Center Configuration Manager](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) para dar suporte às operações diárias com êxito durante toda a sua implantação  



<!--HONumber=Nov16_HO1-->


