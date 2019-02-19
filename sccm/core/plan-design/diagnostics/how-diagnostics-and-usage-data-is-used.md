---
title: Uso de dados de diagnóstico
titleSuffix: Configuration Manager
description: Saiba mais sobre como a Microsoft usa os dados de diagnóstico e de uso que o System Center Configuration Manager coleta.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 404c68f954828dffe2bb9aed9dc59800aff83110
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120769"
---
# <a name="how-diagnostics-and-usage-data-is-used-for-system-center-configuration-manager"></a>Como os dados de diagnóstico e de uso são usados para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os dados de diagnóstico e uso coletados pelo System Center Configuration Manager fornecem à Microsoft comentários quase imediatos sobre como o produto está funcionando e são usados para ajustar atualizações futuras. Também podemos ver os dados de configuração, o que nos ajuda a projetar e testar as configurações que estão em produção. Por exemplo:  

-   As versões do Windows Server que são usadas pelos servidores do site  

-   Os pacotes de idiomas instalados  

-   O delta do esquema do SQL em relação ao padrão do produto  

Esses dados ajudam a equipe de engenharia a planejar testes futuros para garantir a melhor experiência para as configurações mais comuns. Como as atualizações do Configuration Manager são lançadas em um ritmo mais rápido (para dar um suporte melhor às tecnologias móveis como o Windows 10 e o Microsoft Intune), esses dados são cruciais para se ajustar e se adaptar rapidamente.  

Igualmente importante é como os dados de diagnóstico e de uso não são usados. A Microsoft não usa esses dados para:  

-   Auditorias de licenciamento, como comparação de uso do cliente em relação a contratos de licença  

-   Auditoria de produtos sem suporte  

-   Anúncios com base nos dados disponíveis, como uso de recursos ou localização geográfica (fuso horário)  

##  <a name="bkmk_improve"></a> Exemplos de como os dados de diagnóstico e de uso aprimoram o produto  
A Microsoft usa os dados disponíveis para melhorar o produto. A seguir estão alguns exemplos:  

-   **Suporte revisado para sistemas operacionais de servidor antigos:**  

     O suporte inicial oferecido pelo branch atual do System Center Configuration Manager limitou a linha do tempo de suporte para o Windows Server 2008 R2. Depois de examinar os dados de uso de clientes que tinham atualizado para o branch atual do Configuration Manager, identificamos a necessidade de revisar e estender essa linha do tempo para dar suporte aos clientes que ainda usam esse sistema operacional de servidor para hospedar servidores de site e funções do sistema de sites.  

-   **Aprimoramento das verificações de pré-requisito:**  

     Com base nos dados de uso, aprimoramos as verificações de pré-requisito para instalação de uma atualização a fim de remover regras obsoletas, considerar casos adicionais e, em alguns casos, autocorrigir alguns problemas.  
