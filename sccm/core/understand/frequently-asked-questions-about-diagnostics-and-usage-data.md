---
title: Perguntas frequentes sobre dados de uso e diagnóstico
titleSuffix: Configuration Manager
description: Encontre as perguntas frequentes sobre dados de diagnóstico e de uso do System Center Configuration Manager.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b4174c68d5a6ccd31355d976b7830b6d09f39d91
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32339869"
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Perguntas frequentes sobre dados de diagnóstico e de uso do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo fornece respostas para perguntas frequentes sobre dados de uso e diagnóstico no Configuration Manager.

## <a name="faqs"></a>Perguntas frequentes

###  <a name="bkmk_off"></a> Como desativo a telemetria?  
A telemetria não pode ser desabilitada. No entanto, você pode escolher o nível de dados coletados pela telemetria. Para ajudar a gerenciar quando os dados de telemetria são enviados, use o ponto de conexão de serviço no modo offline.

O ramificação atual do Configuration Manager precisa ser atualizado regularmente para dar suporte a novas versões do Windows 10 e do Microsoft Intune. A Microsoft requer pelo menos o nível básico de dados de uso e diagnóstico. Esses dados são usados para manter o produto atualizado, melhorar a experiência de atualização e melhorar a qualidade e a segurança do produto.

###  <a name="bkmk_retention"></a> Qual é o período de retenção de dados?  
 Os dados de uso e diagnóstico são armazenados por um ano.  

###  <a name="bkmk_update"></a> Os dados de diagnóstico e de uso são enviados na instalação ou atualização do produto?  
 Não. Os dados de diagnóstico e de uso são enviados apenas depois que o site estiver instalado e funcionando.  

###  <a name="bkmk_frequency"></a> Com que frequência os dados são enviados?  
 Os procedimentos armazenados do SQL são executados a cada sete dias a partir da data em que o site é instalado. No modo online, o ponto de conexão de serviço é configurado para carregar os dados depois que as consultas são executadas. No modo offline, o administrador usa a ferramenta de conexão de serviço para carregar os dados. (Os dados não estarão disponíveis para uso offline antes dos sete dias contados a partir de quando o site for instalado.)  

###  <a name="bkmk_network"></a> Os dados podem ser usados para formar um mapa de rede?  
 Conforme mostrado na descrição dos níveis de dados de uso e diagnóstico, os detalhes do site incluem informações de fuso horário de cada site. Isso pode fornecer informações sobre a localização geográfica geral e a dispersão global de sites em uma hierarquia. Esses dados não incluem nenhum detalhe de rede, como endereços IP ou informações geográficas mais detalhadas. Para obter mais informações, confira a lista de [artigos de dados de uso e diagnóstico](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data#articles) e encontre os níveis de coleta de dados de uso e diagnóstico da versão que você está usando.


###  <a name="bkmk_tables"></a> Você pode ver dados em tabelas personalizadas?  
 Não. O Configuration Manager coleta dados de uso e diagnóstico por meio de procedimentos armazenados do SQL. Esses procedimentos armazenados são executados nas tabelas padrão do produto no banco de dados. Todas essas tabelas do SQL são prefixadas com **TEL_**. Como parte da consulta de detecção do esquema SQL, todos os nomes de tabela apresentam hash para comparação com os padrões conhecidos. Esse comportamento determina que existem tabelas personalizadas no banco de dados. A presença de tabelas personalizadas informa que o esquema de banco de dados é estendido do padrão. Ele não inclui nenhum dos dados armazenados nessas tabelas.  

###  <a name="bkmk_databases"></a> Você vê nomes de outros bancos de dados ou dados em outros bancos de dados? 
 Não. Os procedimentos armazenados para coletar dados são limitados ao banco de dados do site.  

### <a name="bkmk_gdpr"></a> O Configuration Manager está sujeito ao GDPR (Regulamento Geral sobre a Proteção de Dados)?
 Não. O Configuration Manager não está sujeito à supervisão do GDPR. Ele é um produto local que você implanta, gerencia e opera diretamente. Os dados de uso e diagnóstico que a Microsoft coleta melhoram a experiência de instalação, a qualidade e a segurança das versões futuras. Esses dados estão sujeitos à supervisão do GDPR. Nenhum dado de EUII (informação de identificação de usuário final) nem de EUPI (identificadores de pseudônimos de usuário final) é coletado e transmitido à Microsoft. Para obter mais informações sobre o GDPR, confira o [Microsoft Trust Center sobre GDPR](https://microsoft.com/gdpr). Para obter mais informações sobre dados do Configuration Manager, confira [Dados de uso e diagnóstico](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).


## <a name="see-also"></a>Consulte também  
 [Dados de diagnóstico e de uso](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)
