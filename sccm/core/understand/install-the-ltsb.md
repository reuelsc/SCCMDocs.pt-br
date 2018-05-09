---
title: 'Instalar um site usando a mídia de linha de base 1606 '
titleSuffix: Configuration Manager
description: Instalar ou atualizar para o LTSB para System Center Configuration Manager.
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f4f9a5fd-f573-4b99-ad93-b2c76812e922
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e0a4369e9c302c687f15b29b0daafbf4329e22a5
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="install-and-upgrade-with-the-version-1606-baseline-media-for-system-center-configuration-manager"></a>Instalar e atualizar com uma mídia de linha de base da versão 1606 para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual), (Branch de Manutenção de Longo Prazo)*

Quando você executa a Configuração da mídia de linha de base da versão 1606 para o Configuration Manager, é possível instalar o Branch de Manutenção em Longo Prazo ou o Branch Atual do System Center Configuration Manager.

A mídia de linha de base está disponível em DVD como parte da versão do Microsoft System Center 2016 ou do System Center Configuration Manager (Branch Atual e Branch de Manutenção em Longo Prazo 1606). Para saber mais sobre a mídia de linha de base, confira [Baseline and update versions](/sccm/core/servers/manage/updates#baseline-and-udpate-versions) (Versões de linha de base e atualização).


Quando você usa a mídia de linha de base da versão 1606, o site que você instala ou para o qual atualiza é:
- Um *site do Branch Atual* que é equivalente a um site que foi instalado pela primeira vez usando a mídia de linha de base da 1511 e então atualizado para a versão 1606 e com o pacote cumulativo de atualizações do hotfix da 1606 – KB3186654.
-   Um *site do LTSB* que é equivalente ao site do Branch Atual que executa a versão 1606 com o pacote cumulativo de atualizações do hotfix da 1606 – KB3186654. A mídia de linha de base já inclui o pacote cumulativo de atualizações do hotfix.  Mas o LTSB não dá suporte a todos os recursos ou funcionalidades disponíveis com o Branch Atual, conforme detalhado em [Introdução ao Branch de Manutenção em Longo Prazo do System Center Configuration Manager](introduction-to-the-ltsb.md).

Se você não estiver familiarizado com os diferentes branches do System Center Configuration Manager, confira [Qual branch do Configuration Manager devo usar](which-branch-should-i-use.md).




## <a name="changes-to-setup-with-the-1606-baseline-media"></a>Alterações na instalação com a mídia de linha de base da 1606
A mídia de linha de base da 1606 apresenta as seguintes alterações na Instalação do Configuration Manager.

### <a name="branch-and-edition"></a>Branch e edição
Quando você executar a Instalação, será apresentada uma página de licenciamento na qual é possível pode selecionar o branch do Configuration Manager que você deseja instalar. Você pode escolher o Branch Atual ou o LTSB como uma instalação licenciada ou pode escolher a Edição de Avaliação do Branch Atual como uma instalação não licenciada.

Para mais informações, consulte [Licenciamento e branches do System Center Configuration Manager](learn-more-editions.md).

### <a name="software-assurance-expiration"></a>Término do Software Assurance
Durante a Instalação, você tem a opção de inserir o valor da **Data de validade do Software Assurance**. Esse é um valor opcional que você pode especificar como um lembrete conveniente.

> [!NOTE]
> A Microsoft não valida a data de validade inserida e não usará essa data para validação da licença.  No entanto, você pode usá-la como um lembrete da data de vencimento. Isso é útil porque o Configuration Manager verifica periodicamente se há novas atualizações de software oferecidas online. O status de licença do Software Assurance deve estar atualizado para que você esteja qualificado para usar essas atualizações adicionais.    

- Você pode especificar o valor da data na página **Chave do Produto (Product Key)** do Assistente de Instalação ao executar a Instalação da mídia de linha de base da versão 1606 do System Center Configuration Manager.
- Você também pode especificar essa data selecionando **Propriedades de Configurações de Hierarquia** > **Licenciamento** no console do Configuration Manager.

Para obter mais informações, confira "Contratos do Software Assurance" em [Licenciamento e branches para o System Center Configuration Manager](learn-more-editions.md).


### <a name="additional-pre-upgrade-configurations"></a>Configurações adicionais de pré-atualização
Antes de iniciar uma atualização do System Center 2012 Configuration Manager para o LTSB, você deve realizar as etapas adicionais a seguir como parte da lista de verificação pré-atualização.  
Desinstalar as funções do sistema de sites que não têm suporte pelo LTSB:
- Ponto de sincronização do Asset Intelligence
- Conector do Microsoft Intune
- Pontos de distribuição baseados em nuvem

Para mais informações, confira [Atualização para o System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).


### <a name="new-scripted-installation-options"></a>Novas opções de instalação com scripts
A mídia de linha de base da versão 1606 dá suporte a uma nova chave de arquivo de script autônomo para instalações com scripts de um novo site de nível superior. Isso se aplica à instalação de um novo site primário autônomo ou à adição de um site de administração central como parte de um cenário de expansão do site.

Ao usar um script autônomo para instalar uma ramificação licenciada, é necessário adicionar a seção, os nomes de chave e valores a seguir na seção de Opções do seu script. Você não precisa usar esses valores para instalar com script a Edição de avaliação do Branch Atual:  

 **SABranchOptions**
-   **Nome da chave: SAActive**
  - Valores: 0 ou 1.  
  - Detalhes: 0 instala uma Edição de Avaliação não licenciada do Branch Atual e 1 instala uma edição licenciada.   

- **CurrentBranch**
  - Valores: 0 ou 1.  
  - Detalhes: 0 instala o Branch de Manutenção em Longo Prazo e 1 instala o Branch Atual.  

Por exemplo, para instalar uma edição do Branch Atual, você usaria:

  **Nome da chave: SABranchOptions**
   -    **SAActive = 1**
   - **CurrentBranch = 1**


> [!IMPORTANT]  
> O **SABranchOptions** funciona apenas com a Instalação da mídia de linha de base. Ele não se aplica quando você executa a Instalação da pasta CD.Latest de um site instalado anteriormente usando a mídia de linha de base da versão 1606.
>
> O **SABranchOptions** não se aplica a atualizações com script do System Center 2012 Configuration Manager e sempre resulta no Branch Atual.

Para mais informações, confira [Use a command line to install System Center Configuration Manager sites](/sccm/core/servers/deploy/install/use-a-command-line-to-install-sites) (Usar uma linha de comando para instalar sites do System Center Configuration Manager).


## <a name="install-a-new-site"></a>Instalar um novo site
Ao usar a mídia de linha de base da 1606 para instalar um novo site de qualquer um dos branches, use os procedimentos de planejamento, preparo e instalação de site documentados no tópico [Installing System Center Configuration Manager sites](/sccm/core/servers/deploy/install/installing-sites) (Instalando sites do System Center Configuration Manager) com a adição das seguintes considerações para a Instalação:

- Durante a Instalação, você deve escolher o branch do Configuration Manager que deseja instalar e pode especificar os detalhes do contrato do Software Assurance.
- Todos os sites na mesma hierarquia devem executar o mesmo branch. Não há suporte para ter uma hierarquia com uma combinação do LTSB e do Branch Atual em sites diferentes.
-   Nova instalação com scripts. Para obter mais informações, consulte "Novas opções de instalação com scripts" anteriormente neste artigo.

## <a name="expand-a-stand-alone-primary-site"></a>Expandir um site primário autônomo
Você pode expandir um site primário autônomo que executa o LTSB.  O processo não é diferente daquele usado para um site de Branch Atual com uma limitação:

- Ao instalar o novo site de administração central, você deve usar a Instalação da mídia de origem original usada para instalar o site LTSB. Não há suporte para executar a Instalação da pasta CD.Latest para esse cenário.

Para obter mais informações sobre a expansão de um site, confira "Expandir um site primário autônomo" em [Instalar um site usando o Assistente de Instalação](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).

## <a name="upgrade-from-system-center-2012-configuration-manager"></a>Atualizar do System Center 2012 Configuration Manager
Ao atualizar do System Center 2012 Configuration Manager, use o planejamento, preparo e procedimentos de site conforme documentado no tópico [Atualização para o System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager), mas com as seguintes alterações:

**Atualização para o Branch Atual:**
- Durante a Instalação, você deve escolher o Branch Atual e pode especificar detalhes para o contrato do Software Assurance.
-   Nova instalação com scripts. Para obter mais informações, consulte "Novas opções de instalação com scripts" anteriormente neste artigo.

**Atualização para o LTSB:**  
- Etapas adicionais para seguir na lista de verificação de pré-atualização.
- Durante a Instalação, você deve escolher o LTSB e pode especificar detalhes para o contrato do Software Assurance.
- Apenas é possível atualizar sites que executam o System Center 2012 Configuration Manager com Service Pack 1, o System Center 2012 Configuration Manager com Service Pack 2, o System Center 2012 R2 Configuration Manager com Service Pack 1 ou o System Center 2012 R2 Configuration Manager sem service pack.

### <a name="in-place-upgrade-paths-for-the-1606-baseline-media"></a>Caminhos de atualização in-loco para a mídia de linha de base da 1606
Você pode usar a mídia de linha de base da 1606 para atualizar o seguinte para uma edição licenciada do System Center Configuration Manager:
- System Center 2012 R2 Configuration Manager com Service Pack 1
- System Center 2012 R2 Configuration Manager sem Service Pack (Isso requer o uso da mídia de linha de base para a versão 1606 que foi lançada novamente em 15 de dezembro de 2016).
- System Center 2012 Configuration Manager com Service Pack 2
- System Center 2012 Configuration Manager com Service Pack 1 (requer o uso da mídia de linha de base da versão 1606 que foi lançada em 15 de dezembro de 2016).


Você também pode usar essa mídia para atualizar uma Edição de Avaliação do Branch Atual não licenciada para uma versão totalmente licenciada do Branch Atual.

Esta mídia não dá suporte à atualização de:
- Outras versões do System Center 2012 Configuration Manager.
- Configuration Manager 2007 ou anterior.
- Uma instalação de versão Release Candidate do System Center Configuration Manager.

## <a name="about-the-cdlatest-folder-and-the-ltsb"></a>Sobre a pasta CD.Latest e o LTSB
A seguir estão as limitações para o uso da mídia que o Configuration Manager cria na pasta CD.Latest no servidor do site. Esses limites se aplicam a sites que executam o LTSB:

A mídia na pasta CD.Latest tem suporte para:
- Recuperação de site.
- Manutenção do site.
- Instalação de sites primários filho adicionais.

A mídia na pasta CD.Latest não tem suporte para:  
- Instalação de um site de administração central como parte de um cenário de expansão do site.

Para obter mais informações, veja [a pasta CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder).

## <a name="backup-recovery-and-site-maintenance-for-the-ltsb"></a>Backup, recuperação e manutenção do site para o LTSB
Para fazer backup, recuperar ou executar a manutenção do site em um site que executa o LTSB, use as diretrizes e os procedimentos de [Backup e recuperação para o System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).  

Use a Instalação do Configuration Manager da pasta CD.Latest do backup do seu site do LTSB.
