---
title: "Avaliar em um ambiente de laboratório"
titleSuffix: Configuration Manager
description: "Crie um ambiente de laboratório para avaliar o System Center Configuration Manager para uso em sua organização."
ms.custom: na
ms.date: 2/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
caps.latest.revision: "25"
caps.handback.revision: "0"
author: brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 8649f6686adad908b7806d22983aaf20171609ba
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>Avaliar o System Center Configuration Manager compilando seu próprio ambiente de laboratório

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 Saiba como criar um ambiente de laboratório para avaliar o System Center Configuration Manager para uso em sua organização.  

 O System Center Configuration Manager é uma ferramenta poderosa e complexa para gerenciar usuários, dispositivos e software. É recomendável avaliar completamente o System Center Configuration Manager antes da implantação completa, para que seja possível unir o entendimento conceitual com exercícios práticos.  

 Este guia destina-se principalmente a administradores que estão avaliando o uso do Configuration Manager em ambientes corporativos:  

-   Administradores que desejam uma solução para gerenciar totalmente computadores, servidores e dispositivos móveis  

-   Administradores em setores de alta segurança que exigem a segurança do gerenciamento de dispositivo local com a flexibilidade do gerenciamento de dispositivo baseado em nuvem  

-   Administradores que desejam gerenciar o escalonamento vertical de sua arquitetura de servidor local  

## <a name="what-this-lab-does"></a>O que esse laboratório faz  
 A meta principal de criar esse ambiente de laboratório é fornecer a você o conhecimento geral para começar a trabalhar com o Configuration Manager e para aprimorar a compreensão do Configuration Manager. Você acompanhará um assembly acelerado da versão atual do Configuration Manager, usando dois servidores:  

-   Um que hospeda o Active Directory, o controlador de domínio e o servidor DNS  

-   Um que hospeda o Configuration Manager e todos os componentes do SQL Server associados  

Computadores cliente são instalados no Hyper-V. O laboratório em si também pode ser executado como um sistema totalmente virtualizado em um único servidor.  

## <a name="what-this-lab-does-not-do"></a>O que este laboratório não faz  
 Este laboratório não levará você por todos os cenários do Configuration Manager. Ele não foi projetado para ser imediatamente migrado para um ambiente ativo.  

 Ao compilar este laboratório, você terá um ambiente funcional para trabalhar. Porém, esse ambiente não será otimizado para fatores como o desempenho do sistema, gerenciamento de espaço em disco e armazenamento do SQL Server.  

##  <a name="BKMK_EvalRec"></a> Leitura recomendada antes de criar o laboratório  
 Há uma grande quantidade de conteúdo disponível na [Documentação do System Center Configuration Manager](http://docs.microsoft.com/sccm/). É recomendável que você leia os tópicos a seguir desta biblioteca antes de começar a criar o laboratório:  

-   Conheça os conceitos básicos do console do Configuration Manager, portais do usuário final e cenários de exemplo na [Introdução ao System Center Configuration Manager](../../core/understand/introduction.md).  

-   Saiba mais sobre os recursos de gerenciamento primário do Configuration Manager em [Recursos e funcionalidades do System Center Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md).  

-   Reforce seu conhecimento com os [Conceitos básicos do System Center Configuration Manager](../../core/understand/fundamentals.md).  

-   Aprenda a importância de funções de segurança em [Conceitos básicos da administração baseada em funções para o System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   Saiba mais sobre gerenciamento de conteúdo em [Conceitos de gerenciamento de conteúdo](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   Saiba como dar suporte às operações diárias com êxito durante toda a sua implantação em [Entender como os clientes encontram serviços e recursos do site para o System Center Configuration Manager](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  
