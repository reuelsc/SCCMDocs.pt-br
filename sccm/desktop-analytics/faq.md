---
title: Perguntas frequentes sobre análise de desktop
titleSuffix: Configuration Manager
description: Perguntas frequentes sobre o desktop Analytics.
ms.date: 07/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3a1760e0039280e686e716d8cf876813083d544c
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68340172"
---
# <a name="desktop-analytics-faq"></a>Perguntas frequentes sobre o desktop Analytics

> [!Note]  
> Essas informações se relacionam a um serviço de visualização que pode ser substancialmente modificado antes de ser lançada comercialmente. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

## <a name="prerequisites"></a>Pré-requisitos 

### <a name="can-i-use-desktop-analytics-with-intune-managed-devices"></a>Posso usar a análise de desktops com dispositivos gerenciados pelo Intune? 

A grande maioria dos clientes que podem se beneficiar do fluxo de trabalho de análise de desktops usa Configuration Manager para implantar o Windows. Sabemos que os clientes do Intune adoram as informações adicionais dos dados de análise, e estamos trabalhando em maneiras de compartilhar informações com eles também.

## <a name="windows-upgrade"></a>Atualização do Windows

### <a name="can-i-upgrade-windows-and-change-architecture"></a>Posso atualizar o Windows e alterar a arquitetura?

O desktop Analytics foi projetado para oferecer o melhor suporte a atualizações in-loco. As atualizações in-loco não dão suporte a migrações de 32 bits para a arquitetura de 64 bits. Se você precisar migrar computadores nesse cenário, use o cenário de atualização. As informações de análise de desktop ainda são valiosas nesse cenário, mas você pode ignorar diretrizes específicas de atualização.

Para saber mais, confira [Atualizar um computador existente com uma nova versão do Windows](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows).

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>Posso mudar de BIOS para UEFI ao atualizar o Windows?

Sim. Para obter mais informações, consulte [converter do BIOS para UEFI durante uma atualização in-loco](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>Posso usar a análise de desktops com o Windows 10 LTSC?

Embora você possa usar o desktop Analytics para auxiliar na atualização de dispositivos do canal de manutenção de longo prazo do Windows 10 (LTSC) para o canal semianual do Windows 10, o desktop Analytics não dá suporte a atualizações para o Windows 10 LTSC. Esse canal do Windows 10 não se destina a uso amplo e não recebe atualizações de recursos, portanto, não é um destino com suporte com análise de desktops. Para obter mais informações, consulte [visão geral do Windows como um serviço](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).

### <a name="can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal"></a>Posso reduzir a quantidade de tempo que leva para que os dados sejam atualizados no meu portal de análise de área de trabalho?

Há dois tipos de dados no portal do desktop Analytics: Dados do administrador e dados de diagnóstico. Para atualizar os dados do administrador sob demanda, abra o submenu de moeda de dados e selecione **aplicar alterações**. Essa ação dispara imediatamente uma única atualização de qualquer alteração de administrador pendente em seus espaços de trabalho. As alterações se propagam e estão geralmente disponíveis em até 15-60 minutos. O tempo depende do tamanho do seu espaço de trabalho e do escopo de alterações pendentes. Você pode solicitar uma atualização de dados sob demanda até seis vezes em um período de 24 horas. 

Todos os dados são atualizados automaticamente uma vez por dia, mesmo que você não solicite uma atualização de dados sob demanda. Não há como disparar uma atualização sob demanda de dados de diagnóstico. Para obter mais informações sobre os diferentes tipos de dados na análise de desktops, consulte [latência de dados](/sccm/desktop-analytics/troubleshooting#data-latency).

## <a name="privacy"></a>Privacidade

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>A análise de desktop pode ser usada sem uma conexão direta de cliente com o serviço Microsoft Gerenciamento de Dados?

Não, o serviço inteiro é alimentado pelos dados de diagnóstico do Windows, o que exige que os dispositivos tenham essa conectividade direta.

### <a name="can-i-choose-the-data-center-location"></a>Posso escolher o local do data center?

Para Log Analytics do Azure: Sim, quando você configura o desktop Analytics e cria o espaço de trabalho Log Analytics.

Para o serviço de Gerenciamento de Dados da Microsoft e o armazenamento do Azure de análise: Não, esses dois serviços são hospedados no Estados Unidos.

### <a name="where-is-my-organizations-data-stored"></a>Onde os dados da minha organização são armazenados?

Os dados de diagnóstico do Windows de seus computadores são criptografados, enviados e processados em data centers seguros gerenciados pela Microsoft localizados no Estados Unidos. Em seguida, nossa análise dos dados relacionados ao desktop Analytics é fornecida por meio da solução de análise de desktop na portal do Azure. Há suporte para análise de desktop em todas as regiões do Azure. A seleção de uma região internacional do Azure não impede que dados de diagnóstico sejam enviados e processados nos data centers seguros da Microsoft nos EUA.

## <a name="other"></a>Outros

### <a name="can-i-use-desktop-analytics-for-my-office-365-proplus-upgrades"></a>Posso usar a análise de desktops para atualizações do Office 365 ProPlus?

Não, a análise de desktops se concentra no Windows. A Microsoft desenvolveu a análise de desktops em uma colaboração próxima com vários clientes. Por meio do programa de visualização, os comentários dos clientes foram sobre como a análise de desktop melhorou sua capacidade de gerenciar com segurança as implantações do Windows. Eles também nos disseram que queriam que o [office 365 ProPlus Readiness](/sccm/sum/deploy-use/office-365-dashboard#bkmk_o365_readiness) esteja mais bem integrado às ferramentas de gerenciamento do office no Configuration Manager e no Intune. A Microsoft continuará a fazer investimentos nessas áreas, ao mesmo tempo em que se concentra em cenários do Windows na análise de desktops.
