---
title: Importar dados de configuração
titleSuffix: Configuration Manager
description: Importe dados de configuração se tiver contido em um formato de arquivo de gabinete e atender ao esquema de Linguagem de Modelagem de Serviço com suporte.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 309b9a09-a611-4ba2-90ab-dde51582cf87
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2a779f80f42439fe6526c05d7027c22fb191e41e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32332103"
---
# <a name="import-configuration-data-with-system-center-configuration-manager"></a>Importar dados de configuração com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Além de criar linhas de base de configuração e itens de configuração no console do System Center Configuration Manager, você poderá importar dados de configuração se eles estiverem em um formato de arquivo de gabinete (.cab) e seguirem o esquema SML (Linguagem de Modelagem de Serviço) com suporte. Você pode importar dados de configuração de:  

-   Dados de configuração de prática recomendada (Pacotes de Configuração) baixados no site da Microsoft ou em outros sites de fornecedores de software.  

-   Dados de configuração exportados do System Center 2012 Configuration Manager e posterior.  

-   Dados de configuração que foram criados externamente e que estão em conformidade com o esquema SML.  

 Para obter um exemplo de Pacote de Configuração que vai ajudá-lo a gerenciar a conformidade de funções de servidor do site do System Center 2012 Configuration Manager, veja o [Pacote de Configuração do System Center 2012 Configuration Manager](http://www.microsoft.com/en-us/download/details.aspx?id=30710&WT.mc_id=rss_alldownloads_all).  

Quando você importa uma linha de base de configuração, alguns ou todos os itens de configuração que são referenciados na linha de base de configuração também podem ser incluídos no arquivo de gabinete. Durante o processo de importação, o Configuration Manager verifica se todos os itens de configuração que são referenciados na linha de base de configuração também estão incluídos no arquivo de gabinete ou se já existem no site do Configuration Manager. O processo de importação falhará se você tentar importar uma linha de base de configuração que faz referência aos dados de configuração que o Configuration Manager não pode localizar.  

Entre outros cenários em que o processo de importação pode falhar estão os seguintes:  

-   Os dados de configuração fazem referência a dados de configuração que o Configuration Manager não pode localizar, seja em seu banco de dados ou no próprio arquivo de gabinete.  

-   Os dados de configuração já estão presentes no banco de dados do Configuration Manager com o mesmo nome e a mesma versão de dados de configuração, mas a versão do conteúdo é diferente.  

-   Os dados de configuração já estão presentes no banco de dados do Configuration Manager com a mesma versão do conteúdo, mas o cálculo de hash as identifica como sendo diferentes.  

-   Uma versão mais recente dos dados de configuração com o mesmo nome já está presente no banco de dados do Configuration Manager ou foi excluída dele recentemente.  

-   Em uma hierarquia do Configuration Manager de vários sites, os dados de configuração foram originalmente importados de um site pai. É necessário atualizá-los no mesmo site e não em um site filho.  

### <a name="import-configuration-data"></a>Importar dados de configuração  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Itens de Configurações** ou **Linhas de Base de Configuração**
2.  Na guia **Início**, no grupo **Criar**, clique em **Importar Dados de Configuração**.  
3.  Na página **Selecionar Arquivos** do **Assistente para Importar dados de Configuração**, clique em **Adicionar**e, na caixa de diálogo **Abrir** , selecione os arquivos .cab que deseja importar.  
4.  Marque a caixa de seleção **Criar uma nova cópia dos itens de configuração e das linhas de base de configuração importadas** se desejar que os dados de configuração importados sejam editáveis no console do Configuration Manager.  
5.  Na página **Resumo**, examine as ações a serem executadas e conclua o assistente.  

Os dados de configuração importados são exibidos no nó **Configurações de Conformidade** do espaço de trabalho **Ativos e Conformidade**.  
