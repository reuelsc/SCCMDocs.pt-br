---
title: Sobre as extensões do SCAP (Protocolo de Automação do Conteúdo de Segurança)
titleSuffix: System Center Configuration Manager
description: Saiba mais sobre as extensões do SCAP (Protocolo de Automação do Conteúdo de Segurança)
ms.custom: na
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a315489d-5e12-46d6-903e-3a35235b72c5
caps.latest.revision: 1
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: fc986e2175583124377ccb7c080df4b219ea8df0
ms.sourcegitcommit: 27da4be015f1496b7b89ebddb517a2685f1ecf74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="about-the-security-content-automation-protocol-scap-extensions"></a>Sobre as extensões do SCAP (Protocolo de Automação de Conteúdo de Segurança)

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

> [!Tip]  
> Esse recurso foi introduzido pela primeira vez na versão Technical Preview 1803 como um [recurso de pré-lançamento](/sccm/core/servers/manage/pre-release-features). Esta versão de pré-lançamento das extensões do SCAP pode ser instalada em todas as versões compatíveis no momento do branch atual do Configuration Manager e o LTSB 1606. O arquivo de instalação está localizado em cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi a partir da Technical Preview 1803. 

As Extensões do SCAP para o Microsoft System Center Configuration Manager ajudam você a analisar e avaliar seu ambiente de rede para fins de conformidade com o SCAP (Protocolo de Automação do Conteúdo de Segurança). O SCAP é definido e mantido pelo NIST (National Institute of Standards and Technology) dos EUA.

As Extensões do SCAP para Microsoft System Center Configuration Manager usam o recurso Configurações de conformidade no Microsoft System Center Configuration Manager para verificar os computadores em seu ambiente e documentar seu nível de conformidade com o mandato da USGCB (Linha de Base de Configuração do Governo dos Estados Unidos).

As extensões permitem que o Configuration Manager consuma fluxos de dados do SCAP (Security Content Automation Protocol), avalie sistemas quanto à conformidade e gere resultados de relatório no formato SCAP. Sua organização pode usar a infraestrutura existente do Configuration Manager para ajudar a garantir que os computadores gerenciados atendam a este requisito de conformidade federal e gerem os relatórios do USGCB de requisito para o NIST (National Institute of Standards and Technology) e o OMB (Bureau de Gerenciamento e Orçamento) dos EUA.

Este guia fornece informações para ajudá-lo a instalar, configurar e executar as Extensões do SCAP em sua infraestrutura do System Center Configuration Manager.



# <a name="what39s-new-in-scap-extensions-prerelease-for-microsoft-system-center-configuration-manager"></a>Novidades no pré-lançamento das Extensões do SCAP para Microsoft System Center Configuration Manager

Use esta seção para conhecer as novidades na versão mais recente.

Pré-lançamento de extensões do SCAP para o System Center Configuration Manager:

- Inclui uma extensão do Console do Configuration Manager que dá suporte completo à conversão de Conteúdo do SCAP para linhas de base de configurações de conformidade para o branch atual do System Center Configuration Manager
- Dá suporte ao SCAP versão 1.2 e é compatível com o SCAP versões 1.1 e 1.0.


  - Dá suporte ao XCCDF (Extensible Configuration Checklist Description Format) versão 1.2.
  - Dá suporte ao OVAL (Open Vulnerability and Assessment Language) versões até 5.10.
  - Dá suporte à geração de relatórios ARF (Asset Reporting Format) 1.1
  - Dá suporte ao CPE (Common Platform Enumeration) 2.3
  - Dá suporte ao CVE (Common Vulnerabilities and Exposures)
  - Dá suporte ao CCE (Common Configuration Enumeration) versão 5
  - Dá suporte à USGCB Internet Explorer 8, USGCB Windows 7 e à USGCB do Firewall do Windows 7.

- Inclui um Assistente de interface do usuário para importar o conteúdo do SCAP 1.2/1.1/1.0 e OVAL para conversão em linhas de base de configuração.


  - Permite a seleção de Fluxos de dados de origem do SCAP e parâmetros de comparação e perfis do XCCDF para conversão.

- Inclui um Assistente de interface do usuário para exportar os resultados da avaliação de configuração para o relatório em formato XML do SCAP


  - Exibe o arquivo de origem, o fluxo de dados do SCAP, o parâmetro de comparação XCCDF e o perfil do XCCDF usado para gerar a linha de base.
  - Dá suporte à geração de relatórios LASR (Cyberscope Lightweight Asset Summary Results).

- Dá suporte à geração de relatórios do SCAP com base na implantação de linha de base de configuração. Inclui um novo painel para visualizar a conformidade do cliente, bem como conformidade da regra do XCCDF. O painel dá suporte ao detalhamento para relatórios mais avançados em que é possível pesquisar e filtrar.
- Melhora o desempenho de vários tipos de que itens de configuração convertidos de testes OVAL, permitindo que a avaliação mais rápida.

- Corrige diversos problemas encontrados no conteúdo do Windows 10 DESA v1r3.

# <a name="scap-extensions-for-microsoft-system-center-configuration-manager-deployment-process"></a>Extensões do SCAP para o processo de implantação do Microsoft System Center Configuration Manager

Este guia descreve como analisar, avaliar e emitir relatórios sobre a conformidade com o SCAP usando as Extensões do SCAP para o Microsoft System Center Configuration Manager. Veja um breve resumo dos procedimentos que você seguirá:

- Prepare a infraestrutura de pré-requisito para usufruir as extensões.
- Instalar e configurar as Extensões do SCAP para o Microsoft System Center Configuration Manager
- Baixe, instale e configure os arquivos de fluxo de dados do SCAP da [NVD](http://nvd.nist.gov) (National Vulnerability Database).
- Converta e importe os arquivos de fluxo de dados do SCAP diretamente para uma linha de base de configurações de conformidade do System Center Configuration Manager usando o Assistente de Importação **ou** por meio de um arquivo de gabinete (.cab) usando a ferramenta de linha de comando Microsoft.Sces.ScapToDcm.exe.
- Exporte resultados de conformidade para o formato do SCAP usando o Assistente de Exportação ou a ferramenta de linha de comando Microsoft.Sces.DcmToScap.exe.

# <a name="terms"></a>Termos

**ID do OVAL:** um identificador para uma definição de OVAL específica que está em conformidade com o formato para as IDs de OVAL.

**Fluxo de dados de resultado do SCAP:** um pacote de componentes do SCAP, junto com os mapeamentos de referências entre componentes do SCAP, que armazenam o conteúdo de saída (resultado).

**Fluxo de dados de origem do SCAP:** um pacote de componentes do SCAP, junto com os mapeamentos de referências entre componentes do SCAP, que armazenam o conteúdo de entrada (origem).

# <a name="prepare-the-prerequisite-infrastructure"></a>Preparar a infraestrutura de pré-requisito

Certifique-se de que os seguintes requisitos de software e hardware são atendidos para usufruir as Extensões do SCAP para o Microsoft System Center Configuration Manager.

## <a name="software-requirements"></a>Requisitos de software

Para instalar, configurar e executar as Extensões do SCAP para o Microsoft System Center Configuration Manager, você precisa de um computador com o seguinte software:

- Uma [versão compatível](/sccm/core/servers/manage/current-branch-versions-supported) do console de branch atual do System Center Configuration Manager.
- Um sistema operacional compatível com o console do System Center Configuration Manager. Para obter uma lista de sistemas operacionais compatíveis, consulte o artigo [Sistemas operacionais com suporte para consoles do System Center Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-consoles).

Além do computador que executa as extensões do SCAP, você precisará também dos seguintes itens:

- Uma infraestrutura de branch atual do System Center Configuration Manager. Para obter mais informações sobre os requisitos para uma implantação do Configuration Manager, veja o artigo [Configurações compatíveis para o Configuration Manager](/sccm/core/plan-design/configs/supported-configurations).

Os computadores que você deseja avaliar quanto à conformidade do SCAP precisam das seguintes configurações e software:

- O componente Gerenciamento de Conformidade e Configurações habilitado no cliente do Configuration Manager.
- Windows PowerShell 2.0 ou superior.
- A política de execução do PowerShell do Configuration Manager definida como **Ignorar**. Para obter mais informações, consulte o artigo [Política de execução do PowerShell](/sccm/core/clients/deploy/about-client-settings#computer-agent).
- Um dos seguintes sistemas operacionais
  - Versão da liberação do Windows 7 ou SP1, 32 ou 64 bits
  - Windows 10 32 bits ou 64 bits
  - Windows Server 2012 R2

## <a name="hardware-requirements"></a>Requisitos de hardware

Os requisitos mínimos do sistema são fornecidos aqui:

[Planejando as configurações de hardware para o Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware)



## <a name="accessibility-features"></a>Recursos de acessibilidade

As Extensões do SCAP para o System Center Configuration Manager incluem ferramentas de linha de comando do Windows que podem usufruir os recursos e as ferramentas de acessibilidade no Windows.

- Os parâmetros de linha de comando são documentados neste guia do usuário para Microsoft.Sces.ScapToDcm.exe e Microsoft.Sces.DcmToScap.exe.
- -help e -? imprimirão o uso da ferramenta na tela, em que ela estará disponível para leitores de tela e outras tecnologias de assistência.
- [Acessibilidade](http://windows.microsoft.com/windows/help/accessibility) do Windows

As Extensões do SCAP também utilizam os recursos do System Center Configuration Manager.  O Configuration Manager inclui recursos que tornam o produto mais acessível para pessoas com deficiências.

- [Recursos de acessibilidade no System Center Configuration Manager](/sccm/core/understand/accessibility-features)

Para informações gerais sobre produtos e serviços de acessibilidade da Microsoft, visite o site da Web [Microsoft Accessibility](http://go.microsoft.com/fwlink/p/?LinkId=9212).

## <a name="next-step"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Instalar e configurar as Extensões do SCAP](/sccm/compliance/plan-design/scap/install-configure-scap)
