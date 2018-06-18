---
title: Notas de versão do MDT
description: Entenda as plataformas com suporte, os pré-requisitos e as limitações do Microsoft Deployment Toolkit.
ms.date: 06/04/2018
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 6e32ce6d-585d-4801-a345-ff0f6f2d90ad
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7cb287a17322af8069708268a18d638bd04dddcf
ms.sourcegitcommit: 10b3a571e2a822bbd7b58a25840ee1e6f703a7a2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34814273"
---
# <a name="microsoft-deployment-toolkit-release-notes"></a>Notas de versão do Microsoft Deployment Toolkit  

Este artigo apresenta detalhes sobre a versão mais recente do MDT (Microsoft Deployment Toolkit). Esses detalhes incluem as plataformas com suporte, os pré-requisitos e as limitações. Considera-se que você já tenha familiaridade com os conceitos, os recursos e as funcionalidades da versão do MDT.



## <a name="latest-release"></a>Versão mais recente

O **MDT build 8450** é a versão mais recente disponível no [Centro de Download da Microsoft](https://aka.ms/mdtdownload). 

Essa atualização inicia o suporte ao ADK (Kit de Avaliação e Implantação do Windows) para Windows 10, versão 1709. 

***Atualização***: a partir de maio de 2018, esse build também passará a ser compatível com o Windows 10, versão 1803.

Para obter mais informações, confira a seção [plataformas com suporte](#supported-platforms).


### <a name="significant-changes"></a>Alterações significativas
Aqui está um resumo das alterações significativas nesse build do MDT.

#### <a name="supported-configuration-updates"></a>Atualizações de configuração com suporte
- Windows ADK para Windows 10, versão 1709
- Windows 10, versão 1709
- Configuration Manager, versão 1710

#### <a name="quality-updates"></a>Atualizações de qualidade
Estes são os títulos das correções de bug nesta versão:
- Dependências e licenças do aplicativo de sideload do Win10 não instaladas
- A sequência de tarefas CaptureOnly não permite capturar uma imagem
- Erro recebido ao iniciar uma sequência de tarefas do MDT: valor de DeploymentType "" inválido especificado. A implantação não continuará
- O ZTIMoveStateStore procura a pasta de armazenamento de estado no local errado e, portanto, não consegue movê-la
- O XML contém um erro de digitação simples que causou um comportamento indesejado
- Instalar Funções e Recursos não funciona para o recurso Console de Gerenciamento do IIS do Windows Server 2016
- A pesquisa de imagens do sistema operacional na sequência de tarefas de atualização não funciona quando são usadas pastas
- A ferramenta do MDT provisiona o TPM incorretamente em um estado de funcionalidade reduzida. Para obter mais informações, confira [KB 4018657](https://support.microsoft.com/help/4018657/tpm-is-in-reduced-functionality-mode-after-successful-deployment-of-wi).
- Atualizações na lógica de detecção de tipo de chassi do ZTIGather
- A etapa de atualização do sistema operacional esquece do SetupComplete.cmd, interrompendo as implantações futuras
- Problema de inicialização da UEFI do Windows 10 ADK 1607 e posterior em alguns hardwares
- Inclui os binários de sequência de tarefas atualizados do Configuration Manager



## <a name="supported-platforms"></a>Plataformas com Suporte

As versões do MDT não são mais marcadas com o ano nem com a versão de atualização. Para alinhar melhor aos branches atuais do Windows 10 e do Configuration Manager, e para simplificar a identidade visual e o processo de lançamento, agora ele é chamado simplesmente de **Microsoft Deployment Toolkit**. O número de build é usado para distinguir cada versão. Por exemplo, o build mais recente disponível para download é o 8450.

Ao contrário do Configuration Manager que tem uma agenda de versão predeterminada, o MDT somente lança novas versões conforme a necessidade de dar suporte às novas versões do Windows 10, do Windows ADK ou do branch atual do Configuration Manager. Os problemas conhecidos com esses componentes serão documentados neste artigo conforme o necessário.

Há suporte para as seguintes versões de sistema operacional para implantação com o MDT:
- Windows 10, versão 1803
- Windows 10, versão 1709
- Outras [versões com suporte](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet) do Windows 10
- Windows 8.1
- Windows 7
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2



## <a name="prerequisites"></a>Pré-requisitos

O MDT requer os seguintes componentes, que estão incluídos no Windows:
- Microsoft .NET Framework 4.0
- Windows PowerShell versão 3.0

Use o [Windows ADK para Windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install) mais recente. 

> [!Note]  
> O Windows recomenda o uso do Windows ADK que corresponde à versão do Windows que você está implantando. Por exemplo, use o Windows ADK para Windows 10 versão 1703 quando implantar o Windows 10 versão 1703. Para obter mais informações sobre a compatibilidade de componente do Windows ADK, consulte [Plataformas compatíveis com DISM](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) e [Requisitos de USMT](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1).

Ao integrar o MDT com os cenários de ZTI e UDI do Configuration Manager, use a versão mais recente do branch atual do Configuration Manager.



## <a name="upgrading-mdt"></a>Atualizando o MDT

O processo de instalação do MDT remove todas as instâncias existentes do MDT instaladas no mesmo computador. Os compartilhamentos de implantação, os pontos de distribuição e os bancos de dados existentes são preservados durante esse processo. Eles precisarão ser atualizados quando a instalação for concluída.

A versão atual do MDT permite a atualização das seguintes versões do MDT:
- MDT build 8443

> [!Tip]  
> Crie um backup da infraestrutura existente do MDT antes de tentar uma atualização.

### <a name="lti"></a>LTI
Depois de instalar o MDT, atualize um compartilhamento de implantação existente executando o **Assistente para Abrir Compartilhamento de Implantação** por meio do nó Compartilhamentos de Implantação no Workbench de Implantação. Especifique o caminho para o diretório de compartilhamento de implantação existente e, em seguida, marque a caixa de seleção **Atualizar**. Esse processo também atualiza os compartilhamentos de implantação de rede e os compartilhamentos de implantações de mídia existentes, portanto, esses compartilhamentos devem estar acessíveis. Não execute essa atualização durante a execução de implantações, porque os arquivos em uso podem causar problemas de atualização.

### <a name="zti"></a>ZTI
As sequências de tarefas do MDT existentes presentes no Configuration Manager não são modificadas durante o processo de instalação do MDT. Elas devem continuar a funcionar sem nenhum problema. Não é fornecido nenhum mecanismo para atualizar essas sequências de tarefas. Se você quiser usar algum dos novos recursos do MDT, crie novas sequências de tarefas integradas ao MDT no Configuration Manager.

Quando o processo de atualização for concluído:  

- Execute o **Assistente para Configurar a Integração com o ConfigMgr** após a atualização. Ele registra os novos componentes e instala os modelos de sequência de tarefas ZTI atualizados.  

- Crie um novo pacote **Arquivos do Microsoft Deployment Toolkit** para as novas sequências de tarefas ZTI criadas. Você pode usar o pacote Arquivos do Microsoft Deployment Toolkit existente para as sequências de tarefas ZTI criadas antes da atualização, mas é necessário criar um novo pacote Arquivos do Microsoft Deployment Toolkit para as novas sequências de tarefas ZTI.



<!--
## Known issues
-->



## <a name="frequently-asked-questions"></a>Perguntas frequentes

#### <a name="whats-the-mdt-support-life-cycle"></a>O que é o ciclo de vida de suporte do MDT?  
Para obter mais informações, confira [Ciclo de vida de suporte do Microsoft Deployment Toolkit](https://support.microsoft.com/help/2872000/microsoft-deployment-toolkit-support-life-cycle).

#### <a name="is-this-release-only-supported-with-windows-10-windows-adk-or-configuration-manager-version-x"></a>Esta versão apenas é compatível com o Windows 10, o Windows ADK ou o Configuration Manager versão *X*?
Nós testamos esse build do MDT principalmente com a configuração listada acima. A menos que haja algum problema explícito conhecido, tudo que estiver fora da configuração acima terá uma alta probabilidade de ainda estar funcionando. O seu uso poderá variar porque nós ainda não testamos outras combinações explicitamente.

#### <a name="how-do-i-get-help-with-mdt"></a>Como obter ajuda com o MDT?
Use um dos métodos a seguir para obter ajuda com o MDT (por ordem de prioridade):

1. Postar no [Fórum do MDT](https://social.technet.microsoft.com/Forums/en/home?forum=mdt). Os MVPs e outros usuários na comunidade observam e respondem às postagens no fórum. Essa é provavelmente a maneira mais eficiente de obter ajuda.
2. Contate o Suporte da Microsoft. Abra um caso de suporte e receba ajuda profissional.
3. Se você consegue reproduzir um problema de forma consistente e acredita que ele seja um bug do produto, registre-o no [Hub de Comentários](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) do Windows 10. A equipe do produto investiga tudo o que é relatado. Use a categoria **Gerenciamento Corporativo** e a subcategoria **Implantação do Sistema Operacional** ao preencher os comentários. Essa categorização ajuda a classificar e rotear seus comentários para a equipe do MDT.
     - O Hub de Comentários também pode ser usado para enviar sugestões (solicitações de alteração no design ou DCRs) sobre o produto.
     - Se você já tiver registrado os comentários por meio do Connect, não será necessário registrar novamente no Hub de Comentários.