---
title: Privacidade de dados de análise da área de trabalho
titleSuffix: Configuration Manager
description: Análise da área de trabalho tem o compromisso de privacidade de dados do cliente
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b5606f15-f589-485c-a599-cdabf1a9e7ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 370bfc26b8a7b6ca0223803a36e765528460d89f
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62258157"
---
# <a name="desktop-analytics-data-privacy"></a>Privacidade de dados de análise da área de trabalho

Análise da área de trabalho está totalmente comprometido com a privacidade de dados do cliente, focalizando esses princípios:

- **Transparência:** Vamos documentar totalmente os eventos de diagnóstico do Windows. Examine-os com as equipes de segurança e conformidade da sua empresa. O Visualizador de dados de diagnóstico do Windows lhe permite visualizar dados de diagnóstico enviados de um determinado dispositivo. Para obter mais informações, consulte [visão geral de Visualizador de dados de diagnóstico](https://docs.microsoft.com/windows/configuration/diagnostic-data-viewer-overview).  

- **Controle:** Você controlar o nível de dados de diagnóstico para compartilhar com a Microsoft. Windows 10, versão 1709, adiciona uma nova política para limitar os dados de diagnóstico avançados para o mínimo exigido pela análise de área de trabalho.  

- **Segurança:** Microsoft protege seus dados com alta segurança e criptografia.  

- **Relação de confiança:** Área de trabalho Analytics é compatível com o Microsoft [declaração de privacidade](https://privacy.microsoft.com/privacystatement) e [termos de serviço Online](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).  



## <a name="diagnostic-data-flow"></a>Fluxo de dados de diagnóstico

A ilustração a seguir mostra dados de diagnóstico como fluxos de dispositivos individuais por meio do serviço de dados de diagnóstico, o armazenamento do Azure Log Analytics e seu espaço de trabalho do Log Analytics:

![Diagrama que ilustra o fluxo de dados de diagnóstico de dispositivos](media/da-data-flow-v1.png)

1. Você entra portal do Azure e integrar a análise de área de trabalho. Crie o aplicativo do Azure AD para se conectar com o Configuration Manager. Ao configurar a análise de área de trabalho, você cria um espaço de trabalho do Log Analytics do Azure no local de sua escolha.  

2. Conectar o Configuration Manager e registrar dispositivos  

    1. Configurar o serviço de nuvem de análise de área de trabalho no Configuration Manager com os detalhes do aplicativo do Azure AD.  

    2. Dentro de 15 minutos, o Configuration Manager sincroniza os planos de implantações e coleções de dispositivos com a análise de área de trabalho. Ele repete esse processo para cada hora.  

    3. Configuration Manager define a ID comercial, o nível de dados de diagnóstico e outras configurações para os dispositivos na coleção de destino. Essa configuração especifica os dispositivos para aparecer no seu espaço de trabalho de análise de área de trabalho.  

    4. Você pode implantar as atualizações de compatibilidade para todos os dispositivos de destino. Opcionalmente, você implanta o analisador de integridade do aplicativo e o Office Readiness Toolkit para um conjunto representativo dos dispositivos. Essas ferramentas fornecem ainda mais insights sobre linha personalizada de aplicativos de negócios e as macros do Office.  

3. Dispositivos enviam dados de diagnóstico para os serviços de gerenciamento de dados de diagnóstico do Microsoft para Windows e Office. Esse serviço é hospedado nos Estados Unidos.  

4. Por dia, a Microsoft produz um instantâneo de insights com foco em TI. Esse instantâneo combina os dados de diagnóstico do Windows e do Office com a sua entrada para os dispositivos registrados. Esse processo ocorre no armazenamento transitório, o que é usado somente pela análise de área de trabalho. O armazenamento transitório é hospedado em data centers da Microsoft nos Estados Unidos. Os instantâneos são separados por ID comercial.  

5. Os instantâneos são copiados para o espaço de trabalho apropriado do Log Analytics do Azure.  

6. Análise da área de trabalho armazena sua entrada no armazenamento do Azure Log Analytics. Essas configurações incluem os planos de implantação e decisões de ativo para atualização e importância.  


<!-- ![Diagram illustrating flow of diagnostic data from devices](media/wa-data-flow-v1.png)

1. Devices send diagnostic data to the Microsoft Diagnostic Data Management service. This service is hosted in the United States.  

2. Set up and enrollment  

    1. You create an Azure Log Analytics workspace when you set up Desktop Analytics. You choose the location and copy the commercial ID. This ID identifies your workspace.  
    
    2. When you connect Configuration Manager to Desktop Analytics, it sets the commercial ID on the devices in your target collection. This configuration specifies the devices to appear in your workspace.  

3. Each day Microsoft produces a "snapshot" of IT-focused insights for each workspace in the Diagnostic Data Management service.  

4. These snapshots are copied to transient storage, which is only used by Desktop Analytics. The transient storage is hosted in Microsoft data centers in the United States. The snapshots are segregated by commercial ID.  

5. The snapshots are then copied to the appropriate Azure Log Analytics workspace.  

6. Desktop Analytics stores your configurations in Analytics Azure storage. These configurations include deployment plans and asset upgrade decisions.  
-->


## <a name="other-resources"></a>Outros recursos

Para obter mais informações sobre os aspectos de privacidade relacionadas, consulte os artigos a seguir:

- [Windows 10 e o GDPR para tomadores de decisões](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Configurar dados de diagnóstico do Windows em sua organização](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

- [Campos e eventos de dados de diagnóstico de avaliador Windows 7, Windows 8 e Windows 8.1](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/appraiser-diagnostic-data-events-and-fields)  

- [Windows 10, versão 1809 básica nível Windows eventos de diagnóstico e campos](https://docs.microsoft.com/windows/privacy/basic-level-windows-diagnostic-events-and-fields-1809)  

- [Windows 10, versão 1709 aprimorada eventos de dados de diagnóstico e os campos usados pela análise de área de trabalho](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)  

- [Visão geral do Visualizador de dados de diagnóstico](https://docs.microsoft.com/windows/privacy/diagnostic-data-viewer-overview)  

- [Termos de licenciamento e documentação](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  

- [Segurança e privacidade em data centers do Microsoft Azure](https://azure.microsoft.com/global-infrastructure/)  

- [Confiança na nuvem confiável](https://azure.microsoft.com/overview/trusted-cloud/)  

- [Central de confiabilidade](https://www.microsoft.com/trustcenter)  



## <a name="faq"></a>Perguntas Frequentes

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>Análise de área de trabalho podem ser usado sem uma conexão direta do cliente ao serviço de gerenciamento de dados da Microsoft?
Não, o serviço inteiro é alimentado por dados de diagnóstico em Windows, que exige que os dispositivos possuem essa conectividade direta.


### <a name="can-i-choose-the-data-center-location"></a>Posso escolher o local do data center?

Para o Azure Log Analytics: Sim, quando você configurar a análise de área de trabalho e cria o espaço de trabalho do Log Analytics.

Para o serviço de gerenciamento de dados da Microsoft e análise de armazenamento do Azure: Não, esses dois serviços são hospedados nos Estados Unidos.

