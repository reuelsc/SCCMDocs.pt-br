---
title: Perguntas Frequentes para análise da área de trabalho
titleSuffix: Configuration Manager
description: Perguntas frequentes para análise de área de trabalho.
ms.date: 04/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4596923f9a6a42ad98dc17257b22925ad0bc5eed
ms.sourcegitcommit: 9af73f5c1b93f6ccaea3e6a096f75a5fecd65c2f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2019
ms.locfileid: "64562443"
---
# <a name="desktop-analytics-faq"></a>Perguntas frequentes sobre análise de área de trabalho

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

## <a name="windows-upgrade"></a>Atualização do Windows

### <a name="can-i-upgrade-windows-and-change-architecture"></a>É possível atualizar o Windows e alterar a arquitetura?

Análise da área de trabalho foi projetado para melhor atualizações in-loco de suporte. Atualizações in-loco não dão suporte a migrações de arquitetura de 32 bits para 64 bits. Se você precisar migrar computadores nesse cenário, use o cenário de atualização. Insights de análise da área de trabalho ainda são valiosos nesse cenário, mas você pode ignorar as diretrizes específicas da atualização.

Para saber mais, confira [Atualizar um computador existente com uma nova versão do Windows](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows).

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>Posso alterar de BIOS para UEFI durante a atualização do Windows?

Sim. Para obter mais informações, consulte [converter de BIOS para UEFI durante uma atualização in loco](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>Pode usar análise da área de trabalho com Windows 10 LTSC?

Embora você possa usar a análise de área de trabalho para ajudá-lo com a atualização de dispositivos do Windows 10 em longo prazo de manutenção LTSC (canal) para o canal semestral do Windows 10, análise de área de trabalho não dá suporte a atualizações para Windows 10 LTSC. Esse canal do Windows 10 não é destinado para uso amplo e não recebe atualizações do recurso, portanto, não é um destino com suporte com a análise de área de trabalho. Para obter mais informações, consulte [Windows como uma visão geral do serviço](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).

## <a name="privacy"></a>Privacidade

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>Análise de área de trabalho podem ser usado sem uma conexão direta do cliente ao serviço de gerenciamento de dados da Microsoft?

Não, o serviço inteiro é alimentado por dados de diagnóstico em Windows, que exige que os dispositivos possuem essa conectividade direta.

### <a name="can-i-choose-the-data-center-location"></a>Posso escolher o local do data center?

Para o Azure Log Analytics: Sim, quando você configurar a análise de área de trabalho e cria o espaço de trabalho do Log Analytics.

Para o serviço de gerenciamento de dados da Microsoft e análise de armazenamento do Azure: Não, esses dois serviços são hospedados nos Estados Unidos.

### <a name="where-is-my-organizations-data-stored"></a>Onde estão armazenados os dados da minha organização?

Dados de diagnóstico do Windows em seus computadores são criptografados, enviados para e processados em centros de dados segura gerenciada pela Microsoft localizados nos Estados Unidos. Nossa análise dos dados relacionados à análise de área de trabalho, em seguida, é fornecida a você por meio da solução de análise de área de trabalho no portal do Azure. Análise da área de trabalho é compatível com todas as regiões do Azure. Selecionar uma região do Azure internacional não impede que dados de diagnóstico que estão sendo enviados e processados em centros de dados seguros da Microsoft nos Estados Unidos.
