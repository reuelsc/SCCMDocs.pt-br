---
title: Licenciamento e filiais
titleSuffix: Configuration Manager
description: Saiba mais sobre os requisitos de licenciamento das opções de instalação disponíveis com o Configuration Manager
ms.date: 06/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 495b87ae-41a4-49ba-abe2-d4f7d22ac0d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 02c0839bf7587fa9ee1421bf7035e31a3ca59cd1
ms.sourcegitcommit: a6a6507e01d819217208cfcea483ce9a2744583d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2019
ms.locfileid: "66748095"
---
# <a name="licensing-and-branches-for-system-center-configuration-manager"></a>Licenciamento e branches do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual), (Branch de Manutenção de Longo Prazo)*

Use este artigo para saber mais sobre os requisitos de licenciamento para as opções de instalação disponíveis com o System Center Configuration Manager. Essas opções de instalação incluem os seguintes branches:

- Branch atual
- LTSB (Branch de Manutenção de Longo Prazo)
- Instalação de avaliação do branch atual
- Branch de technical preview

## <a name="licensing-overview"></a>Visão geral do licenciamento

Os clientes com SA (Software Assurance) ativo para as licenças do System Center Configuration Manager ou com direitos de assinatura equivalentes a partir de 1º de outubro de 2016 têm direito de usar a versão 1606, de outubro de 2016, do System Center Configuration Manager. Clientes que adquiriram direitos do System Center Configuration Manager em ou após 1º de outubro de 2016 encontrarão duas opções licenciadas durante a instalação: Branch Atual e LTSB (Branch de Manutenção de Longo Prazo).

Para obter os termos e condições completos dos produtos que você compra por meio dos programas de Licenciamento por volume da Microsoft, confira [Documentação e termos de licenciamento](https://go.microsoft.com/fwlink/?LinkId=800052).


## <a name="licensed-branches"></a>Branches licenciados

Este artigo faz referência ao contrato de Software Assurance ou aos direitos de assinatura equivalentes. Este contrato de licenciamento da Microsoft concede direitos para instalar e usar o Configuration Manager.

### <a name="current-branch"></a>Branch atual

O branch atual requer um contrato de Software Assurance ativo (ou direitos equivalentes) para o Configuration Manager. Para obter mais informações, confira [Branch Atual e o Software Assurance](#software-assurance-and-the-current-branch).

Este branch tem suporte para uso em ambientes de produção que desejam receber atualizações regulares de qualidade e de recursos da Microsoft. Ele fornece acesso para usar todos os recursos e aprimoramentos.

A partir da versão 1710, cada versão de atualização permanece com suporte por 18 meses a partir da data de lançamento de disponibilidade geral. Para mais informações, consulte [Suporte para versões do branch atual do System Center Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).

### <a name="long-term-servicing-branch-ltsb"></a>LTSB (Branch de Manutenção de Longo Prazo)

O LTSB requer um contrato atual do Software Assurance com a Microsoft desde 1º de outubro de 2016. Para obter mais informações, consulte o [Software Assurance e o LTSB](#software-assurance-and-the-ltsb).

Este branch tem suporte para o uso em ambientes de produção. É destinado a uso por clientes que deixaram seus direitos de SA (Software Assurance) ou direitos de assinatura equivalentes do Configuration Manager vencerem depois de 1º de outubro de 2016. Este branch é limitado em comparação ao Branch Atual.

Atualizações de segurança críticas do Configuration Manager são disponibilizadas para este branch, mas nenhum novo recurso está disponível.

### <a name="evaluation-installation-of-the-current-branch"></a>Instalação de avaliação do branch atual

A versão de avaliação não requer um contrato do Software Assurance com a Microsoft. As [instalações de avaliação](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) são sempre o branch atual e você pode usá-las por 180 dias.

É possível atualizar a instalação de avaliação para uma instalação completa do branch atual. Não é possível atualizar uma instalação de avaliação para o branch de manutenção de longo prazo.

### <a name="technical-preview-branch"></a>Branch de technical preview

O [branch de technical preview](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) também está disponível. Esse branch é um build limitado do Configuration Manager que permite que você experimente os novos recursos. O technical preview é instalado, usando mídia diferente das versões licenciadas. Para obter mais informações, consulte [Technical Preview](/sccm/core/get-started/technical-preview).


## <a name="software-assurance-agreements"></a>Contratos de Software Assurance

O status do Software Assurance em suas licenças do System Center Configuration Manager ou em direitos de assinatura equivalentes em ou após 1º de outubro de 2016 determina o branch que você pode instalar e usar.

### <a name="software-assurance-and-the-current-branch"></a>Software Assurance e o branch atual

Os direitos para usar o branch atual do Configuration Manager podem ser fornecidos por:

- **System Center:** os clientes com SA ativo do System Center Standard ou licenças de datacenter podem instalar e usar a opção do branch atual do Configuration Manager.

- **System Center Configuration Manager:** os clientes com SA ativo para as licenças do System Center Configuration Manager ou com direitos de assinatura equivalentes podem instalar e usar a opção do branch atual do Configuration Manager.

Se tiver um SA ativo para licenças do System Center Configuration Manager ou direitos de assinatura equivalentes a partir de 1º de outubro de 2016, você:

- Pode instalar e usar o branch atual.
- Se permitir que o SA ou a assinatura expirem, você precisará desinstalar o branch atual.

### <a name="software-assurance-and-the-ltsb"></a>Software Assurance e o LTSB

Se tiver um SA ativo para licenças do System Center Configuration Manager ou direitos de assinatura equivalentes a partir de 1º de outubro de 2016, você:

- pode instalar e usar o LTSB. Clientes que têm direitos perpétuos do System Center Configuration Manager ou que permitirem que a assinatura do SA expire podem instalar a versão do LTSB do Configuration Manager que for atual no momento em que a licença expirar.

O LTSB se baseia na versão 1606 do branch atual e tem as seguintes limitações:

- Não há suporte para converter um branch atual para o LTSB. Se tiver um site do branch atual, instale o LTSB como um novo site.  

- O LTSB não dá suporte a todos os recursos do branch atual. Para obter mais informações, confira [Introdução ao branch de manutenção de longo prazo](introduction-to-the-ltsb.md). Essas limitações incluem um conjunto limitado de recursos, opções de atualização limitadas e um ciclo de vida de suporte de produto separado.  

### <a name="software-assurance-expiration-date"></a>Data de validade do Software Assurance

Começando com a versão de outubro de 2016 da mídia de linha de base da versão 1606 do Configuration Manager, você pode especificar a data de validade do contrato do Software Assurance. A **data de expiração do Software Assurance** é um valor opcional como um lembrete conveniente. Adicione-a ao executar a instalação do Configuration Manager ou posterior no console do Configuration Manager.

> [!NOTE]
> A Microsoft não valida a data de validade especificada e não usa essa data para validação da licença. Use-a como um lembrete da data de vencimento. Este valor é útil quando o Configuration Manager verifica periodicamente as novas atualizações de software oferecidas online. O status de licença do Software Assurance deve estar atualizado para estar qualificado para usar essas atualizações adicionais.

#### <a name="to-specify-the-software-assurance-expiration-date"></a>Para especificar a data de validade do Software Assurance

- Ao executar a instalação da mídia do Configuration Manager, especifique o valor na página **Chave do produto** do Assistente de instalação.

- No console do Configuration Manager, nas **Configurações de Hierarquia**, especifique o valor na guia **Licenciamento**.


## <a name="licensing-resources"></a>Recursos de licenciamento

Para saber mais sobre os detalhes do licenciamento de produtos, use os links a seguir.

### <a name="microsoft-volume-licensing-service-center-vlsc"></a>VLSC (Centro de Serviços de Licenciamento por Volume) da Microsoft

- [Visão geral do VLSC](https://www.microsoft.com/Licensing/existing-customer/vlsc-training-and-resources.aspx)

- [Termos do Produto do Licenciamento por Volume da Microsoft](https://go.microsoft.com/fwlink/?LinkId=800052)

- Os clientes de licença de volume podem obter um resumo das suas licenças no [Centro de serviços de licença de volume](https://www.microsoft.com/Licensing/servicecenter/default.aspx). Vá para o menu **Licenças** e selecione **Resumo de licenças**.

### <a name="vlsc-videos"></a>Vídeos sobre o VLSC

- Para vídeos de treinamento sobre como funciona o VLSC, acesse [Recursos e treinamento do Centro de Serviços de Licença de Volume da Microsoft](https://www.microsoft.com/licensing/existing-customer/vlsc-training-and-resources) e selecione **Vídeos de instruções**.

- [Onde procurar seu contrato de Software Assurance ativado](https://www.microsoft.com/showcase/video.aspx?uuid=fe1846cb-1d26-49fc-b064-57b25dcc31a0) (começando em 43 segundos)  

- [Como obter as permissões do VLSC](https://www.microsoft.com/showcase/video.aspx?uuid=ac4ed1ca-d0a9-43cd-89fa-74ccb555dec4). Você pode delegar permissões de leitura e gravação no VLSC para outras pessoas de sua organização.
