---
title: Gerenciador de Conversão de Pacotes
titleSuffix: Configuration Manager
description: Saiba mais sobre o Gerenciador de Conversão de Pacotes para converter pacotes em aplicativos no Configuration Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f053fa73-c553-4522-a6b9-f885f23fe57c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7057084ba976408f189a0d4fbb96f176bc0c6656
ms.sourcegitcommit: 759098de944b8f7d5eedfc2bae2cb9a6ba15276f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43297191"
---
# <a name="package-conversion-manager"></a>Gerenciador de Conversão de Pacotes

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

<!--1357861-->

A partir da versão 1806, o Gerenciador de Conversão de Pacotes ajuda a converter pacotes legados do Configuration Manager em aplicativos. Os aplicativos apresentam benefícios adicionais, como dependências, regras de requisitos, métodos de detecção e afinidade de dispositivo de usuário.

> [!Note]  
> Nesta versão do Configuration Manager, o Gerenciador de Conversão de Pacotes é um recurso de pré-lançamento. Para habilitá-lo, veja [Recursos de pré-lançamento](/sccm/core/servers/manage/pre-release-features).  

Um aplicativo do Configuration Manager contém arquivos e programas que você implementa em dispositivos clientes. No entanto, diferentemente dos pacotes e programas legados, um aplicativo fornece funcionalidade adicional centrada no usuário. Por exemplo, um aplicativo pode conter tipos de implantação para uma instalação local de um pacote de software, um pacote de aplicativos virtuais ou uma versão do aplicativo para dispositivos móveis.

Para obter mais informações, consulte os seguintes artigos: 
- [Introdução ao gerenciamento de aplicativos](/sccm/apps/understand/introduction-to-application-management)  
- [Pacotes e programas](/sccm/apps/deploy-use/packages-and-programs)  

> [!Important]  
> Se você já tiver instalado uma versão mais antiga do Gerenciador de Conversão de Pacotes, desinstale-a antes de atualizar seu site. Essa versão integrada não requer a instalação, mas pode entrar em conflito com as versões existentes.  

Essa versão integrada do Gerenciador de Conversão de Pacotes funciona em pacotes no branch atual do Configuration Manager. Não é uma ferramenta autônoma. Se você tiver pacotes e programas em uma versão mais antiga do Configuration Manager, primeiro migre os pacotes para o seu branch atual. Para saber mais, confira [Migrar dados entre hierarquias](/sccm/core/migration/migrate-data-between-hierarchies).



## <a name="planning"></a>Planejamento

Antes de começar a converter pacotes em aplicativos, primeiro desenvolva um plano. O processo a seguir é um exemplo de plano:

- [Definir um plano de conversão de pacote detalhado](#bkmk_define)  

- [Selecionar e preparar pacotes para conversão](#bkmk_prepare)  

- [Selecionar pacotes de teste](#bkmk_test)  

- [Analisar, investigar e converter pacotes](#bkmk_analyze)  

- [Testar e implantar os aplicativos](#bkmk_deploy)  


### <a name="bkmk_define"></a> Definir um plano de conversão de pacote detalhado

Esta seção descreve dois exemplos de planos de conversão de pacote:  

- [Um ambiente de teste de alta utilização de recursos](#bkmk_define-high): você tem um ambiente de teste com recursos, permissões e arquitetura para replicar por completo seu ambiente de produção.  

- [Um ambiente de teste de recursos limitados](#bkmk_define-limited): você não tem um ambiente de teste que duplica totalmente o seu ambiente de produção.  

Ajuste esses planos conforme necessário para outros problemas específicos do seu ambiente.

#### <a name="bkmk_define-high"></a> Exemplo de plano para um ambiente de teste de alta utilização de recursos

Seu ambiente de teste possui recursos, permissões e arquitetura semelhantes ao seu ambiente de produção. Use o ambiente de teste para analisar e converter com eficiência todos os seus pacotes e, em seguida, testar todos os seus aplicativos do Configuration Manager. Depois de concluir esse trabalho, transfira-o para o ambiente de produção. 

Seu plano de conversão de pacote pode ser semelhante às seguintes etapas:  

1.  Selecione os pacotes que você deseja converter.  

2.  Migre os pacotes para conversão em seu ambiente de teste.  

3.  Prepare os pacotes para conversão.  

4.  Selecione pacotes de teste.  

5.  Analise, investigue e converta os pacotes de teste.  

6.  Teste os aplicativos convertidos.  

7.  Analise e converta os pacotes restantes (não usados para teste).  

8.  Exporte os aplicativos a partir do ambiente de teste. Importe-os para o seu ambiente de produção.  

#### <a name="bkmk_define-limited"></a> Exemplo de plano para um ambiente de teste de recursos limitados

Seu ambiente de teste não possui recursos, permissões e arquitetura semelhantes ao seu ambiente de produção. Você não pode analisar, testar e converter todos os seus pacotes. Nesse cenário, apenas analise, investigue, converta e teste seus pacotes de teste. Em seguida, migre os pacotes restantes para o ambiente de produção para analisar e convertê-los. 

Seu plano de conversão de pacote pode ser semelhante às seguintes etapas:

1.  Selecione os pacotes que você deseja converter.  

2.  Selecione pacotes de teste.  

3.  Migre os pacotes de teste em seu ambiente de teste.  

4.  Prepare os pacotes de teste para conversão.  

5.  Analise, investigue e converta os pacotes de teste.  

6.  Teste os aplicativos convertidos.  

7.  Exporte os aplicativos de teste a partir do ambiente de teste. Em seguida, importe-os para o seu ambiente de produção.  

8.  Migre os pacotes restantes no ambiente de produção e prepare-os para conversão.  

9.  Analise, investigue e converta os pacotes restantes no ambiente de produção.  

10. Libere os aplicativos restantes para o ambiente de produção.  


### <a name="bkmk_prepare"></a> Selecionar e preparar pacotes para conversão

#### <a name="bkmk_prepare-select"></a> Selecione os pacotes que deseja converter

Nem todos os pacotes são adequados para serem convertidos em aplicativos. Antes de começar a converter pacotes, identifique os pacotes que não serão convertidos. 

Os melhores tipos de pacote para conversão em aplicativos são aqueles que contêm software voltado ao usuário como, por exemplo:  

 - Arquivos do Windows Installer (.msi e .msu)  

 - Programas do Microsoft Application Virtualization (App-V)  

 - Arquivos executáveis ​​do Windows (.exe)  

Os tipos de pacote que são melhor mantidos como pacotes e não convertidos em aplicativos incluem:

 - Ferramentas de manutenção do sistema. Por exemplo, scripts ou utilitários de backup.  

 - Não há suporte para pacotes de software.

> [!Tip]  
> Depois de identificar os pacotes que não são apropriados para conversão em aplicativos, mova-os para uma pasta separada no console do Configuration Manager. Para criar uma pasta de pacote no console do Configuration Manager:  
> - Clique com o botão direito do mouse no nó **Pacotes**.  
> - Selecione **Pastas** e, em seguida, selecione **Criar pasta**.  
> - Insira o nome da pasta, por exemplo `Not Converted`.  
> - Clique em **OK**.  

#### <a name="prepare-the-packages-for-conversion"></a>Preparar os pacotes para conversão

Para cada pacote que desejar converter, verifique se ele atende às seguintes condições:  

 - O local dos arquivos de origem é um caminho UNC completo, por exemplo `\\Server\Share\File`.  

 - Os arquivos do Windows Installer usam apenas um código de produto exclusivo.  


### <a name="bkmk_test"></a> Selecionar pacotes de teste

Se possível, seu grupo de pacotes de teste deve incluir pacotes que atendam aos seguintes critérios:  

 - Pelo menos um pacote de teste com um estado de preparação de **Automático**.  

 - Pelo menos um pacote de teste com um estado de preparação de **Manual**.  

Idealmente, seus pacotes de teste devem ser pacotes principais, por exemplo:  

 - Pacotes que você conhece bem.  

 - Os pacotes que são os mais importantes para sua organização.  

 - Pacotes que você pode testar com mais facilidade.  

Identifique os pacotes apropriados para o teste. Em seguida, mova-os para uma pasta separada no console do Configuration Manager.


### <a name="bkmk_analyze"></a> Analisar, investigar e converter pacotes

#### <a name="analyze-packages"></a>Analisar pacotes

Para analisar um pacote individual ou um pequeno grupo, use o Gerenciador de Conversão de Pacotes integrado no console do Configuration Manager. Para saber mais, confira [Como analisar e converter pacotes](/sccm/apps/pcm/how-to-analyze-and-convert).  

> [!NOTE]  
> Confira o nó **Status de Conversão de Pacote** no espaço de trabalho **Monitoramento**. Ele exibe informações resumidas sobre os processos de análise e conversão.  

#### <a name="investigate-analysis-results"></a>Investigar resultados da análise

Depois de analisar os pacotes de teste, investigue os pacotes com um estado de preparação de **Manual** ou **Erro**. Determine as razões pelas quais eles têm esse estado. Entre algumas das razões comuns para um estado de preparação de **Manual** ou **Erro** estão:

 - O pacote não contém as informações necessárias para criar um método de detecção em um tipo de implantação de aplicativo.  

 - O pacote não contém as informações necessárias para converter as coleções em requisitos e condições globais.  

 - O pacote contém mais de um programa.  

 - O pacote depende de outro pacote que não foi convertido em um aplicativo.  

Para saber mais, use os seguintes recursos:  

- Revise as mensagens de erro e as correções em [Referência técnica para as mensagens de erro do Gerenciador de Conversão de Pacotes](/sccm/apps/pcm/error-messages)  

- Examinar o arquivo de log **PCMTrace.log**  

- [Solução de problemas do Gerenciador de Conversão de Pacotes](/sccm/apps/pcm/troubleshoot-pcm)  

#### <a name="convert-the-packages"></a>Converter os pacotes

Para saber mais sobre como converter pacotes, confira [Como analisar e converter pacotes](/sccm/apps/pcm/how-to-analyze-and-convert).

> [!NOTE]  
> Confira o nó **Status de Conversão de Pacote** no espaço de trabalho **Monitoramento**. Ele exibe informações resumidas sobre os processos de análise e conversão.  


### <a name="bkmk_deploy"></a> Testar e implantar os aplicativos

Teste os aplicativos em seu ambiente de teste ou ambiente de produção, de acordo com seu plano de conversão detalhado do pacote.



## <a name="recommendations"></a>Recomendações

- Use o nó **Status de Conversão de Pacote** no espaço de trabalho **Monitoramento**. Ele exibe informações resumidas sobre os processos de análise e conversão.  

- Investigue os programas em seus pacotes (conhecidos como wrappers). Use o plug-in do Gerenciador de Conversão de Pacotes para converter suas funções na funcionalidade equivalente do Configuration Manager.  

- Lembre-se de testar por completo cada aplicativo convertido antes de implantá-lo em um ambiente de produção.  



## <a name="next-steps"></a>Próximas etapas

[Como analisar e converter pacotes](/sccm/apps/pcm/how-to-analyze-and-convert)