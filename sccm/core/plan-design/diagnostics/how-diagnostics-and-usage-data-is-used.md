---
title: "Uso dos dados de diagnóstico | Microsoft Docs"
description: "Saiba mais sobre como a Microsoft usa os dados de diagnóstico e de uso que o System Center Configuration Manager coleta."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: aa0ee7544e348025a80d32b4a816de6dbec31d7f


---
# <a name="how-diagnostics-and-usage-data-is-used-for-system-center-configuration-manager"></a>Como os dados de diagnóstico e de uso são usados para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os dados de diagnóstico e de uso coletados para o System Center Configuration Manager fornecem à Microsoft comentários quase imediatos sobre como o produto está funcionando (ou se não funciona) e são usados para ajustar atualizações futuras. Também podemos ver os dados de configuração, o que nos ajuda a projetar e testar as configurações que estão em produção. Por exemplo:  

-   As versões do Windows Server que são usadas pelos servidores do site  

-   Os pacotes de idiomas instalados  

-   O delta do esquema do SQL em relação ao padrão do produto  

Esses dados ajudam a equipe de engenharia a planejar testes futuros para garantir a melhor experiência para as configurações mais comuns. Como as atualizações do Configuration Manager são lançadas em um ritmo mais rápido (para dar um suporte melhor e mais ágil às tecnologias móveis como o Windows 10 e o Microsoft Intune), esses dados são cruciais para se ajustar e se adaptar rapidamente.  

Igualmente importante é como os dados de diagnóstico e de uso não são usados. A Microsoft não usa esses dados para:  

-   Auditorias de licenciamento, como comparação de uso do cliente em relação a contratos de licença  

-   Auditoria de produtos sem suporte  

-   Anúncios com base nos dados disponíveis, como uso de recursos ou localização geográfica (fuso horário)  

##  <a name="a-namebkmkimprovea-examples-of-how-diagnostics-and-usage-data-is-improving-the-product"></a><a name="bkmk_improve"></a> Exemplos de como os dados de diagnóstico e de uso estão aprimorando o produto  
A Microsoft usa os dados disponíveis para melhorar o produto. Veja a seguir alguns exemplos de como isso é feito:  

-   **Suporte revisado para sistemas operacionais de servidor antigos:**  

     O suporte inicial oferecido pelo branch atual do System Center Configuration Manager incluía um limite para a linha do tempo de suporte para o Windows Server 2008 R2. Depois de examinar os dados de uso de clientes que tinham atualizado para o branch atual do Configuration Manager, identificamos a necessidade de revisar e estender essa linha do tempo para dar suporte ao grande número de clientes que ainda usam esse sistema operacional de servidor para hospedar servidores do site e funções do sistema de sites.  

-   **Aprimoramento das verificações de pré-requisito:**  

     Com base nos dados de uso, aprimoramos as verificações de pré-requisito para instalação de uma atualização a fim de remover regras obsoletas, considerar casos adicionais e, em alguns casos, autocorrigir alguns problemas.  



<!--HONumber=Dec16_HO3-->


