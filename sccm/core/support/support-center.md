---
title: Centro de Suporte
titleSuffix: Configuration Manager
description: Solucionar problemas de clientes do Configuration Manager com o Centro de Suporte.
ms.date: 01/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c631197d-7daa-4faa-9e22-980cd6d604c2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 828edc3c90b4dd93f4d86772b863816bbc8c9130
ms.sourcegitcommit: 013ca76d5a3c07306de7b5bfd985b0289d1be599
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2019
ms.locfileid: "55482411"
---
# <a name="support-center-for-configuration-manager"></a>Centro de Suporte do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

<!--1357489--> Da versão 1810 em diante, use o Centro de Suporte para solução de problemas do cliente, exibição de log em tempo real ou captura do estado de um computador de cliente do Configuration Manager para análise posterior. O Centro de Suporte é uma ferramenta única para consolidação das diversas ferramentas de solução de problemas do administrador. 



## <a name="about"></a>Sobre o 

O Centro de Suporte tem como objetivo reduzir os desafios e as frustrações ao solucionar problemas de computadores cliente do Configuration Manager. Anteriormente, ao trabalhar com o suporte para corrigir um problema com clientes do Configuration Manager, você precisa coletar manualmente os arquivos de log e outras informações para ajudar a solucionar o problema. Era muito fácil esquecer acidentalmente um arquivo de log crucial, causando problemas adicionais para você e para a equipe de suporte com que você estava trabalhando.

Use o Centro de Suporte para simplificar a experiência de suporte. Ele permite que você:

 - Crie um pacote de solução de problemas (arquivo .zip) que contém os arquivos de log do cliente do Configuration Manager. Em seguida, você tem um único arquivo para enviar à equipe de suporte.  

 - Exibir arquivos de log do cliente do Configuration Manager, certificados, configurações de Registro, despejos de depuração, políticas do cliente.  

 - Diagnóstico em tempo real de inventário (substitui ContentSpy), política (substitui PolicySpy) e cache do cliente.  


### <a name="support-center-viewer"></a>Visualizador do Centro de Suporte

O Centro de Suporte inclui Visualizador do Centro de Suporte, uma ferramenta que o pessoal de suporte usa para abrir o pacote de arquivos que você cria usando o Centro de Suporte. O coletor de dados do Centro de Suporte coleta e agrupa os logs de diagnóstico de um cliente do Configuration Manager local ou remoto. Para exibir pacotes do coletor de dados, use o aplicativo visualizador.


### <a name="support-center-log-file-viewer"></a>Visualizador de arquivos de log do Centro de Suporte

O Centro de Suporte inclui um visualizador de logs moderno. Essa ferramenta substitui o CMTrace. O OneTrace fornece uma interface personalizável com suporte para guias e janelas encaixáveis. Ele tem uma camada de apresentação rápida e pode carregar arquivos de log grandes em segundos.


### <a name="powershell-cmdlets"></a>Cmdlets do PowerShell

O Centro de Suporte também inclui [cmdlets do Windows PowerShell](https://go.microsoft.com/fwlink/?linkid=397830). Use esses cmdlets para criar uma conexão remota com outro cliente do Configuration Manager, configurar as opções de coleta de dados e iniciar a coleta de dados.



## <a name="prerequisites"></a>Pré-requisitos

Instale os seguintes componentes no servidor ou computador cliente no qual você instala o Centro de Suporte:

- Uma versão de sistema operacional com suporte do Configuration Manager. Para obter mais informações, confira [Versões do sistema operacional com suporte para clientes](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices). O Centro de Suporte não dá suporte a dispositivos móveis.  

- O .NET framework 4.5.2 é necessário no computador em que você executa o Centro de Suporte e seus componentes.  



## <a name="install"></a>Instalar o

Localize o instalador do Centro de Suporte no servidor do site no seguinte caminho: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`.

Após a instalação, localize os itens a seguir no menu Iniciar no grupo do **Microsoft System Center**:  
- Centro de Suporte (ConfigMgrSupportCenter.exe)  
- Visualizador de Arquivos de Log do Centro de Suporte (CMLogViewer.exe)  
- Visualizador do Centro de Suporte (ConfigMgrSupportCenterViewer.exe)  



## <a name="known-issues"></a>Problemas conhecidos 

#### <a name="remote-connections-must-include-computer-name-or-domain-as-part-of-the-user-name"></a>Conexões remotas devem incluir o nome do computador ou domínio como parte do nome de usuário
Se você se conectar a um cliente remoto do Centro de Suporte, deverá fornecer o nome do computador ou o nome de domínio da conta de usuário ao estabelecer a conexão. Se você usar um nome do computador ou nome de domínio abreviado (como `.\administrator`), a conexão será bem-sucedida, mas o Centro de Suporte não coletará dados do cliente. 

Para evitar esse problema, use os seguintes formatos de nome de usuário para se conectar a um cliente remoto: 
- `ComputerName\UserName`  
- `DomainName\UserName`  

#### <a name="scripted-server-message-block-connections-to-remote-clients-might-require-removal"></a>Conexões de protocolo SMB com clientes remotos podem necessitar de remoção
Ao conectar-se a clientes remotos usando o cmdlet [New-CMMachineConnection](https://go.microsoft.com/fwlink/p/?linkid=390542) do PowerShell, o Centro de suporte cria uma conexão de protocolo SMB de mensagem do servidor para cada cliente remoto. Ele retém essas conexões depois de você concluir a coleta de dados. Para evitar exceder o número máximo de conexões remotas para o Windows, use o comando `net use` para ver o conjunto ativo de conexões remotas. Em seguida, desabilite todas as conexões desnecessárias usando o comando a seguir: `net use <connection_name> /d` 
em que `<connection_name>` é o nome da conexão remota.

#### <a name="application-deployment-evaluation-cycle-request-isnt-sent-correctly-to-remote-machines"></a>A solicitação de ciclo de avaliação de implantação de aplicativos não é enviada de maneira correta para computadores remotos
<!--2849356--> No Centro de Suporte, se você selecionar **Avaliação de implantação de aplicativo** na ação **gatilho Invocar** na guia **Conteúdo**, essa ação iniciará uma tarefa que avaliará os aplicativos implantados. Se você estiver conectado a um cliente local, tanto as implantações de aplicativos de computador quanto as de usuário serão avaliadas. No entanto, se você estiver conectado a um cliente remoto, apenas as implantações de aplicativos de computador serão avaliadas.


## <a name="next-steps"></a>Próximas etapas

[Início rápido do Centro de Suporte](/sccm/core/support/support-center-quickstart)
