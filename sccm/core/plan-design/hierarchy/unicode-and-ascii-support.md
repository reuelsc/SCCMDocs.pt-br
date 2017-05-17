---
title: Suporte a Unicode e ASCII | Microsoft Docs
description: Saiba mais sobre o suporte para caracteres ASCII e Unicode em objetos do System Center Configuration Manager.
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bdec799-905f-48bc-aed5-2d92134739e8
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: b35e747c8c297d61bb549b9767c4318f51e5fdb4
ms.openlocfilehash: 18f1c64c1f27001a0fdfbab4236d09a5bc279272
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017


---
# <a name="unicode-and-ascii-support-in-system-center-configuration-manager"></a>Suporte a Unicode e ASCII no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager cria a maioria dos objetos usando caracteres Unicode. No entanto, vários objetos dão suporte apenas aos caracteres ASCII, ou têm outras limitações.  

 As seções a seguir listam os objetos que usam caracteres somente do conjunto de caracteres ASCII, ou que possuem limitações adicionais.  

-   [Objetos que usam caracteres ASCII](#BKMK_ASCIIchar)  

-   [Limitações adicionais](#BKMK_OtherCharLimitations)  

-   [Objetos do Configuration Manager que não são localizados](#BKMK_LangNonLocalize)  

##  <a name="BKMK_ASCIIchar"></a> Objetos que usam caracteres ASCII  
 O Configuration Manager dá suporte ao conjunto de caracteres ASCII somente quando os seguintes objetos são criados:  

-   Código do site  

-   Todos os nomes do computador do servidor do sistema de site  

-   As seguintes contas do Configuration Manager:  

    > [!NOTE]  
    >  Estas contas dão suporte aos caracteres ASCII e RUS em um site executado em russo.  

    -   Conta de instalação do cliente por push  

    -   Conta de publicação de referência de estado de integridade  

    -   Conta de consulta de referências de estado de integridade  

    -   Conta de conexão do banco de dados do ponto de gerenciamento  

    -   Conta de acesso à rede  

    -   Conta de acesso ao pacote  

    -   Conta do remetente padrão  

    -   Conta de instalação do sistema de sites  

    -   Conta da conexão do ponto de atualização do software  

    -   Conta do servidor proxy do ponto de atualização do software  

    > [!NOTE]  
    >  As contas que você especificar para a administração baseada em funções oferecerão suporte para Unicode.  
    >   
    >  A conta do ponto do Reporting Services dá suporte a Unicode, exceto aos caracteres RUS.  

-   FQDN (nome de domínio totalmente qualificado) para servidores do site e sistemas de sites  

-   Caminho de instalação para o Configuration Manager  

-   Nomes de instância do SQL Server  

-   O caminho para as seguintes funções do sistema de site:  

    -   Ponto de serviços Web do Catálogo de Aplicativos  

    -   Ponto de sites da Web do catálogo de aplicativos  

    -   Ponto de registro  

    -   Ponto proxy do registro  

    -   Ponto do Reporting Services  

    -   Ponto de migração de estado  

-   O caminho para as seguintes pastas:  

    -   A pasta que armazena dados de migração de estado do cliente  

    -   A pasta que contém os relatórios do Configuration Manager  

    -   A pasta que armazena o backup do Configuration Manager  

    -   A pasta que armazena os arquivos de origem de instalação para a instalação do site  

    -   A pasta que armazena os downloads de pré-requisitos para uso pela instalação  

-   O caminho para os seguintes objetos:  

    -   Site da Web do IIS  

    -   Caminho de instalação de aplicativo virtual  

    -   Nome do aplicativo virtual  

-   Os seguintes objetos para AMT e gerenciamento fora da banda:  

    -   O FQDN do computador baseado em AMT  

    -   O nome do computador baseado em AMT  

    -   O nome NetBIOS do domínio  

    -   O nome do perfil sem fio e SSID  

    -   O nome da autoridade de certificação raiz confiável  

    -   O nome da AC (autoridade de certificação) e nomes de modelo  

    -   O nome do arquivo e o caminho para o arquivo de imagem de redirecionamento de IDE  

    -   O conteúdo do armazenamento de dados AMT  

-   Nomes do arquivo ISO da mídia de inicialização  

##  <a name="BKMK_OtherCharLimitations"></a> Limitações adicionais  
 Estas são as limitações adicionais para conjuntos de caracteres e versões de idioma com suporte:  

-   O Configuration Manager não dá suporte à alteração de localidade do computador do servidor de site.  

-   Uma AC (autoridade de certificação) corporativa não oferece suporte a nomes de computador cliente que usam DBCS (conjunto de caracteres de dois bytes). Os nomes de computador cliente que você pode usar são restritos pela limitação PKI do conjunto de caracteres IA5. Além disso, o Configuration Manager não dá suporte a valores de nome de entidade e de AC que usam DBCS.  

##  <a name="BKMK_LangNonLocalize"></a> Objetos do Configuration Manager que não são localizados  
 O banco de dados do Configuration Manager dá suporte a Unicode para a maioria dos objetos que ele armazena e, quando possível, exibe essas informações no idioma do sistema operacional que corresponde à localidade de um computador. Para a interface de cliente ou o console do Configuration Manager exibir informações no idioma do sistema operacional do computador, a localidade do computador deve corresponder ao idioma do cliente ou servidor que você instala em um site.  

 No entanto, diversos objetos do Configuration Manager não dão suporte a Unicode, e são armazenados no banco de dados usando ASCII, ou têm limitações de idioma adicionais. Essas informações são sempre exibidas usando o conjunto de caracteres ASCII ou no idioma em uso quando o objeto foi criado.  

