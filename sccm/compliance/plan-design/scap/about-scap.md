---
title: Extensões SCAP
titleSuffix: Configuration Manager
description: Saiba mais sobre as extensões SCAP (Security Content Automation Protocol) para o Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a315489d-5e12-46d6-903e-3a35235b72c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0cf248704d49f429bf4ca9dc4ea2be375093f92c
ms.sourcegitcommit: 2cc635835709fb8d86cdb63ea34233b36c94d4d8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52258991"
---
# <a name="about-the-security-content-automation-protocol-scap-extensions"></a>Sobre as extensões do SCAP (Protocolo de Automação de Conteúdo de Segurança)

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As extensões SCAP para o Configuration Manager ajudam você a analisar e avaliar seu ambiente de rede em relação à conformidade com o SCAP (Security Content Automation Protocol). O SCAP é definido e mantido pelo NIST (National Institute of Standards and Technology) dos EUA. Para obter mais informações, confira a [visão geral do projeto SCAP](https://csrc.nist.gov/projects/security-content-automation-protocol).

As extensões SCAP para o Configuration Manager usam o recurso de configurações de conformidade para primeiro verificar os computadores em seu ambiente. Em seguida, ele documenta seu nível de conformidade com o USGCB (United States Government Configuration Baseline).

As extensões permitem que o Configuration Manager consuma fluxos de dados SCAP, avalie os sistemas quanto à conformidade e gere resultados de relatório no formato SCAP. Sua organização pode usar a infraestrutura existente do Configuration Manager para ajudar a garantir que os computadores gerenciados atendam a esse requisito de conformidade federal. O Configuration Manager também pode ser usado para gerar os relatórios do USGCB exigidos pelo NIST e o OMB (Gabinete de Gestão e Orçamento).

Este artigo fornece informações para ajudá-lo a instalar, configurar e executar as extensões SCAP em sua infraestrutura do Configuration Manager.



## <a name="whats-new"></a>Novidades

Esta versão das extensões do protocolo SCEP para o Configuration Manager inclui e dá suporte aos seguintes recursos:  

- Uma extensão de console do Configuration Manager, que dá suporte para conversão de conteúdo SCAP nas linhas de base de configurações de conformidade.  

- SCAP versão 1.2, que inclui os seguintes componentes:  

  - XCCDF (Extensible Configuration Checklist Description Format) versão 1.2
  - OVAL (Open Vulnerability and Assessment Language) versões até a 5.10
  - geração de relatórios ARF (Asset Reporting Format) 1.1
  - CPE (Common Platform Enumeration) 2.3
  - CVE (Common Vulnerabilities and Exposures)
  - CCE (Common Configuration Enumeration) versão 5
  - USGCB Internet Explorer 8, USGCB Windows 7 e USGCB do Firewall do Windows 7  

- Compatibilidade com as versões anteriores do SCAP 1.1 e 1.0.  

- Um assistente de console para importar o conteúdo SCAP 1.2/1.1/1.0 e OVAL para conversão em linhas de base de configuração.  

  - Permite a seleção de fluxos de dados de origem SCAP e parâmetros de comparação e perfis XCCDF para conversão.

- Um assistente de console para exportar os resultados da avaliação de configuração para o relatório XML no formato SCAP.  

  - Exibe o arquivo de origem, o fluxo de dados SCAP, o parâmetro de comparação XCCDF e o perfil XCCDF usados para gerar a linha de base.
  - Gera o relatório LASR (Cyberscope Lightweight Asset Summary Results).  

- Gera relatórios do SCAP com base na implantação da linha de base de configuração. Esse componente inclui um novo painel para visualizar a conformidade do cliente e a conformidade com a regra do XCCDF. O painel dá suporte ao detalhamento para relatórios mais avançados em que é possível pesquisar e filtrar.  

- Melhora o desempenho de vários tipos de itens de configuração convertidos de testes OVAL, permitindo uma avaliação mais rápida.  

- Corrige diversos problemas encontrados no conteúdo do Windows 10 DESA v1r3.  



## <a name="terms"></a>Termos

- **ID OVAL:** um identificador para uma definição OVAL específica que está em conformidade com o formato de IDs OVAL.  

- **Fluxo de dados de resultado SCAP:** um pacote de componentes SCAP e os mapeamentos de referências entre os componentes SCAP que armazenam o conteúdo de saída (resultado).  

- **Fluxo de dados de origem SCAP:** um pacote de componentes SCAP e os mapeamentos de referências entre componentes SCAP que armazenam o conteúdo de entrada (fonte).



## <a name="deployment-process"></a>Processo de implantação

Aqui está um resumo do processo geral de implantação:  

- [Preparar a infraestrutura](#bkmk_prepare) para usar as extensões  

- [Instalar e configurar as extensões SCAP](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_install) para o Configuration Manager  

- [Baixar e instalar os arquivos de fluxo de dados SCAP](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_scap-data-stream-files) do NIST  

- Converta e importe os arquivos de fluxo de dados SCAP em uma linha de base de configurações de conformidade do Configuration Manager. Use um dos dois métodos a seguir:   

    - [Processo manual](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_convert-and-import) usando o assistente de importação no console do Configuration Manager  

    - [Processo automatizado](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_auto-convert-and-import) com a ferramenta de linha de comando Microsoft.Sces.ScapToDcm.exe  

- [Implantar](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_deploy) as linhas de base de configuração nas coleções  

- [Monitorar](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_monitor) os dados de conformidade  

- Exporte os resultados de conformidade para o formato SCAP usando um dos dois métodos a seguir:  

    - [Processo manual](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_export) usando o assistente de exportação no console  

    - [Processo automatizado](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_auto-export) usando a ferramenta de linha de comando Microsoft.Sces.DcmToScap.exe  



## <a name="bkmk_prepare"></a> Preparar a infraestrutura

### <a name="software-requirements"></a>Requisitos de software

Para instalar, configurar e executar as extensões SCAP para o Center Configuration Manager, você precisa de um computador com o seguinte software:

- Uma [versão compatível](/sccm/core/servers/manage/current-branch-versions-supported) do console do branch atual do Configuration Manager.  

- Uma versão de sistema operacional compatível com o console do Configuration Manager. Para obter mais informações, confira [Sistemas operacionais com suporte para consoles do Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-consoles).  

Além do computador que executa as extensões SCAP, você também precisa dos seguintes itens:

- Uma infraestrutura do branch atual do Configuration Manager. Para obter mais informações sobre os requisitos para uma implantação do Configuration Manager, veja o artigo [Configurações compatíveis para o Configuration Manager](/sccm/core/plan-design/configs/supported-configurations).  

Os computadores que você deseja avaliar quanto à conformidade do SCAP precisam das seguintes configurações e software:

- O cliente do Configuration Manager.  

- Windows PowerShell 2.0 ou superior.  

- A política de execução do PowerShell do Configuration Manager definida como **Ignorar**. Para obter mais informações, consulte o artigo [Política de execução do PowerShell](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

- Um dos seguintes sistemas operacionais:  
  - Windows 7 SP1, de 32 bits ou 64 bits
  - Windows 10, de 32 bits ou 64 bits
  - Windows Server 2012 R2

### <a name="hardware-requirements"></a>Requisitos de hardware

Para obter mais informações sobre os requisitos mínimos do sistema para o Configuration Manager, confira [Planejando as configurações de hardware do Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware).



## <a name="accessibility-features"></a>Recursos de acessibilidade

As extensões SCAP para o Configuration Manager incluem as ferramentas de linha de comando do Windows. Essas ferramentas permitem aproveitar os recursos e as ferramentas de acessibilidade do Windows.

- Os parâmetros de linha de comando são documentados para Microsoft.Sces.ScapToDcm.exe e Microsoft.Sces.DcmToScap.exe. Para obter mais informações, confira [Parâmetros de linha de comando do Microsoft.Sces.ScapToDcm.exe](/sccm/compliance/plan-design/scap/install-configure-scap#microsoftscesscaptodcmexe-command-line-parameters) e [Parâmetros de linha de comando do Microsoft.Sces.DcmToScap.exe](/sccm/compliance/plan-design/scap/import-scap-compliance-settings#microsoftscesdcmtoscapexe-command-line-parameters).  

- Os parâmetros de linha de comando `-help` e `-?` de cada ferramenta imprimem o uso na tela. Em seguida, esses detalhes de uso ficam disponíveis para os leitores de tela e outras tecnologias adaptativas.  

- Para obter mais informações, confira [Acessibilidade do Windows](http://windows.microsoft.com/windows/help/accessibility).

As extensões SCAP também usam os recursos de acessibilidade do Configuration Manager. Para obter mais informações, confira [Recursos de acessibilidade no Configuration Manager](/sccm/core/understand/accessibility-features).

Para obter mais informações sobre os produtos e serviços de acessibilidade da Microsoft, confira o [site Microsoft Accessibility](http://go.microsoft.com/fwlink/p/?LinkId=9212) (Acessibilidade da Microsoft).



## <a name="next-step"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Instalar e configurar as extensões do SCAP](/sccm/compliance/plan-design/scap/install-configure-scap)
