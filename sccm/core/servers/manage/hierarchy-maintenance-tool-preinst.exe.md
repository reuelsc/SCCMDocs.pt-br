---
title: "Ferramenta de Manutenção de Hierarquia | Microsoft Docs"
description: "Entenda o que faz a ferramenta de manutenção de hierarquia e por que você pode usá-la. Inclui referência de opções de linha de comando."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cead6825-6113-4ba5-a381-ac3598dfee86
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: f3ddeaadfb1418aeeaacdca47768600c86b59083
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="hierarchy-maintenance-tool-preinstexe-for-system-center-configuration-manager"></a>Ferramenta de Manutenção de Hierarquia (Preinst.exe) para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A ferramenta de Manutenção de Hierarquia (Preinst.exe) envia os comandos para o Gerenciador de Hierarquia do System Center Configuration Manager enquanto o serviço do Gerenciador de Hierarquia está em execução. A ferramenta de Manutenção de Hierarquia é automaticamente instalada quando você instala um site do Configuration Manager. É possível encontrar o Preinst.exe na pasta compartilhada \\&lt;*NomeDoServidorDoSite*>\SMS_&lt;*CódigoDoSite*\bin\X64\00000409 no servidor do site.  

 É possível usar a ferramenta de Manutenção de Hierarquia nas seguintes situações:  

-   Quando a troca de chaves com segurança é necessária, existem situações nas quais você deve realizar manualmente a troca inicial de chaves públicas entre os sites. Para obter mais informações, consulte [Troca manual de chaves públicas entre sites](#BKMK_ManuallyExchangeKeys) neste tópico.  

-   Para remover trabalhos ativos que são de um site de destino que não está mais disponível.  

-   Para excluir um servidor do site do console do Configuration Manager quando não é possível desinstalar o site usando a Instalação. Por exemplo, se você remover fisicamente um site do Configuration Manager sem antes executar a Instalação para desinstalar o site, as informações do site ainda existirão no banco de dados do site pai, e o site pai continuará tentando se comunicar com o site filho. Para resolver esse problema, é possível executar a ferramenta de Manutenção de Hierarquia e excluir manualmente o site filho do banco de dados do site pai.  

-   Para interromper todos os serviços do Configuration Manager em um site sem precisar interrompê-los individualmente.  

-   Quando você está recuperando um site, pode usar a opção CHILDKEYS para distribuir as chaves públicas de vários sites filho para o site de recuperação.  

Para executar a ferramenta de Manutenção de Hierarquia, o usuário atual deve ter privilégios administrativos no computador local. Além disso, o usuário deve ter explicitamente o direito de segurança de Site - Administrador; não é suficiente o usuário herdar esse direito por ser um membro de um grupo que tenha essa permissão.  

## <a name="hierarchy-maintenance-tool-command-line-options"></a>Opções de linha de comando da ferramenta de Manutenção de Hierarquia  
Quando você usa a ferramenta de Manutenção de Hierarquia, deve executá-la localmente no site de administração central, no site primário, ou no servidor de site secundário.  

Ao executar a ferramenta de Manutenção de Hierarquia, é necessário usar a seguinte sintaxe: preinst.exe /&lt;opção\>. Veja a seguir as opções de linha de comando.  

 **/DELJOB &lt;*CódigoDoSite*>** use esta opção em um site para excluir todos os trabalhos ou comandos do site atual para o site de destino especificado.  

 **/DELSITE &lt;*CódigoDoSiteFilhoASerRemovido*>** use esta opção em um site pai para excluir os dados de sites filho do banco de dados do site pai. Normalmente, você usará essa opção se um computador do servidor do site for encerrado antes que se desinstale o site dele.  

> [!NOTE]  
>  A opção /DELSITE não desinstala o site no computador especificado pelo parâmetro ChildSiteCodeToRemove. Esta opção apenas remove as informações do banco de dados do site do Configuration Manager.  

**/DUMP &lt;*CódigoDoSite*>**: use esta opção no servidor do site local para gravar imagens de controle de site na pasta raiz da unidade na qual o site está instalado. Você pode gravar uma imagem específica de controle de site na pasta ou gravar todos os arquivos de controle de site na hierarquia.  

-   /DUMP &lt;*CódigoDoSite*> grava a imagem de controle de site somente para o site especificado.  

-   /DUMP grava os arquivos de controle de site para todos os sites.  

Uma imagem é uma representação binária do arquivo de controle de site, armazenado no banco de dados do site do Configuration Manager. A imagem do arquivo de controle de site despejada é uma soma da imagem base mais as imagens delta pendentes.  

Depois de despejar uma imagem do arquivo de controle de site com a ferramenta de Manutenção de Hierarquia, o nome do arquivo estará no formato sitectrl_&lt;*CódigoDoSite*>.ct0.  

**/STOPSITE** – use esta opção no servidor do site local para iniciar um ciclo de desligamento para o serviço do Gerenciador de Componentes de Site do Configuration Manager, que redefine parcialmente o site. Quando esse ciclo de desligamento é executado, alguns serviços do Configuration Manager em um servidor do site e seus sistemas de sites remotos são interrompidos. Esses serviços são sinalizados para reinstalação. Como resultado desse ciclo de desligamento, algumas senhas são alteradas automaticamente quando os serviços são reinstalados.  

> [!NOTE]  
>  Se você deseja ver um registro do desligamento, reinstalação, e alteração de senhas para o Gerenciador de Componentes de Site, habilite o log para esse componente antes de usar essa opção de linha de comando.  

Depois de iniciado o ciclo de desligamento, ele prossegue automaticamente, ignorando quaisquer componentes ou computadores que não respondem. Entretanto, se o serviço do Gerenciador de Componentes de Site não puder acessar um sistema de site remoto durante o ciclo de desligamento, os componentes instalados no sistema de site remoto serão reinstalados quando o serviço do Gerenciador de Componentes de Site for reiniciado. Quando reiniciado, o serviço do Gerenciador de Componentes de Site tenta repetidamente a reinstalação de todos os serviços sinalizados para isso, até que tenha sucesso.  

Você pode reiniciar o serviço do Gerenciador de Componentes de Site usando o Gerenciador de Serviços. Depois que for reiniciado, todos os serviços afetados serão desinstalados, reinstalados e reiniciados. Após usar a opção /STOPSITE para iniciar o ciclo de desligamento, não será possível impedir os ciclos de reinstalação depois de o serviço do Gerenciador de Componentes de Site ser reiniciado.  

**/KEYFORPARENT** - use essa opção em um site para distribuir a chave pública do site para um site pai.  

A opção /KEYFORPARENT coloca a chave pública do site no arquivo &lt;*CódigoDoSite*>.CT4 na raiz da unidade dos arquivos de programas. Depois de executar preinst.exe com esta opção, copie manualmente o arquivo &lt;*CódigoDoSite*>.CT4 para a pasta …\Inboxes\hman.box do site pai (não hman.box\pubkey).  

**/KEYFORCHILD** - use essa opção em um site para distribuir a chave pública do site para um site filho.  

A opção /KEYFORCHILD coloca a chave pública do site no arquivo &lt;*CódigoDoSite*>.CT5 na raiz da unidade dos arquivos de programas. Depois de executar preinst.exe com essa opção, copie manualmente o arquivo &lt;*CódigoDoSite*>.CT5 na pasta …\Inboxes\hman.box do site filho (não hman.box\pubkey).  

**/CHILDKEYS** - você pode usar essa opção nos sites filho de um site que você está recuperando. Use essa opção para distribuir chaves públicas de vários sites filho para o site de recuperação.  

A opção /CHILDKEYS coloca a chave do site na qual você executa a opção, e todas as chaves públicas dos sites filho desse site no arquivo &lt;*CódigoDoSite*>.CT6.  

Depois de executar preinst.exe com essa opção, copie manualmente o arquivo &lt;*CódigoDoSite*>.CT6 para a pasta …\Inboxes\hman.box do site de recuperação (não hman.box\pubkey).  

**/PARENTKEYS** - você pode usar essa opção no site pai de um site que você está recuperando. Use essa opção para distribuir chaves públicas de todos os sites pai para o site de recuperação.  

A opção /PARENTKEYS coloca a chave do site na qual você executa a opção e as chaves de cada site pai acima desse site no arquivo &lt;CódigoDoSite\>.CT7.  

Depois de executar preinst.exe com essa opção, copie manualmente o arquivo &lt;*CódigoDoSite*>.CT7 para a pasta …\Inboxes\hman.box do site de recuperação (não hman.box\pubkey).  

##  <a name="BKMK_ManuallyExchangeKeys"></a> Troca manual de chaves públicas entre sites  
Por padrão, a opção **Solicitar troca de chaves com segurança** está habilitada para sites do Configuration Manager. Quando a troca de chave com segurança é necessária, existem duas situações nas quais você deve executar manualmente a troca inicial de chaves entre os sites:  

-   Se o esquema do Active Directory não foi estendido para o Configuration Manager  

-   Os sites do Configuration Manager não estão publicando dados para o Active Directory  

Você pode usar a ferramenta de Manutenção de Hierarquia para exportar as chaves públicas para cada site. Após serem exportados, você deverá trocar manualmente as chaves entre os sites.  

> [!NOTE]  
>  Depois que as chaves públicas forem alteradas manualmente, você poderá examinar o arquivo de log **hman.log** , que registra as alterações de configuração do site e a publicação de informações do site para os Serviços de Domínio Active Directory, no servidor do site pai para verificar se o site primário processou a nova chave pública.  

#### <a name="to-manually-transfer-the-child-site-public-key-to-the-parent-site"></a>Para transferir manualmente a chave pública do site filho para o site pai  

1.  Enquanto conectado ao site filho, abra um prompt de comando e navegue para a localização do **Preinst.exe**.  

2.  Para exportar a chave pública do site filho, digite: **Preinst /keyforparent**  

3.  A opção /keyforparent coloca a chave pública do site filho no arquivo **&lt;código do site\>.CT4** localizado na raiz da unidade do sistema.  

4.  Mova o arquivo **&lt;código do site\>.CT4** para a pasta **&lt;diretório de instalação\>\inboxes\hman.box** do site pai.  

#### <a name="to-manually-transfer-the-parent-site-public-key-to-the-child-site"></a>Para transferir manualmente a chave pública do site pai para o site filho  

1.  Enquanto conectado ao site pai, abra um prompt de comando e navegue para a localização de **Preinst.exe**.  

2.  Digite o seguinte para exportar a chave pública do site pai: **Preinst /keyforchild**.  

3.  A opção /keyforchild coloca a chave pública do site pai no arquivo **&lt;código do site\>.CT5** localizado na raiz da unidade do sistema.  

4.  Mova o arquivo **&lt;código do site\>.CT5** para o diretório **&lt;diretório de instalação\>\inboxes\hman.box** do site filho.  
