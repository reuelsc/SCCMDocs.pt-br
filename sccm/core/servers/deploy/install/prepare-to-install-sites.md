---
title: Preparar para instalar sites
titleSuffix: Configuration Manager
description: Se você planeja instalar vários sites do Configuration Manager, leia essas informações para ajudá-lo a economizar tempo e evitar erros.
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9f07a321ac6f10f5287a88d0df7064920f538ae5
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32341688"
---
# <a name="prepare-to-install-system-center-configuration-manager-sites"></a>Preparar para instalar sites do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para se preparar para uma implantação bem-sucedida de um ou mais sites do System Center Configuration Manager, familiarize-se com os detalhes neste artigo. Essas etapas podem economizar tempo durante a instalação de vários sites e ajudar a evitar erros que podem resultar na necessidade de reinstalar um ou mais sites.

> [!TIP]
> Ao gerenciar a infraestrutura do site e da hierarquia do System Center Configuration Manager, os termos *upgrade*, *atualização* e *instalação* são usados para descrever três conceitos separados. Para saber como cada termo é usado, consulte [About upgrade, update, and install](/sccm/core/understand/upgrade-update-install) (Sobre upgrade, atualização e instalação).

## <a name="bkmk_options"></a> Opções de instalação de diferentes tipos de sites
Quando você instala um novo site do Configuration Manager, a versão dos arquivos de origem que você pode usar depende da versão dos sites que já estão na hierarquia (caso haja). Os métodos de instalação que você pode usar dependem do tipo de site que você deseja instalar.  

Antes de instalar um site, certifique-se de que você planejou sua hierarquia e que entende o tipo de site que deseja instalar. Para obter mais informações, confira [Design a hierarchy of sites](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md) (Criar uma hierarquia de sites).


### <a name="first-site"></a>Primeiro site
O primeiro site que você instalará em uma hierarquia será um site primário autônomo ou um site de administração central.

**Mídia de instalação**: para instalar um site de administração central ou um site primário autônomo como o primeiro site em uma nova hierarquia, você deve [usar uma versão de linha de base](../../../../core/servers/manage/updates.md#bkmk_Baselines) do Configuration Manager. Não instale o primeiro site de uma nova hierarquia usando arquivos de origem atualizados da [pasta CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) de nenhum site.

**Método de instalação**: você pode instalar qualquer tipo de site usando o [Assistente de Instalação do Configuration Manager](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md) ou pode configurar um script para usar com uma [instalação de linha de comando com scripts](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).


### <a name="additional-sites"></a>Sites adicionais
Depois de instalar o site inicial, você pode adicionar mais sites a qualquer momento. Você tem as seguintes opções para adicionar sites (até os [limites com suporte](../../../../core/plan-design/configs/size-and-scale-numbers.md)):

|Site que você tem|Tipo de site adicional que você pode instalar|
|---|---|
|Site de administração central|Site primário filho|
|Site primário filho|Site secundário|
|Site primário autônomo|Site secundário (você pode expandir o site primário, o que converte o site primário autônomo em um site primário filho)|

**Mídia de instalação**: quando você instala um site de administração central para expandir um site primário autônomo ou se instalar um novo site primário filho em uma hierarquia existente, deve usar a mídia de instalação (que contém arquivos de origem) que corresponde à versão do site ou sites existentes.

> [!IMPORTANT]
> Se você tiver instalado atualizações no console que alteraram a versão dos sites instalados anteriormente, não use a mídia de instalação original. Em vez disso, neste cenário, use os arquivos de origem da [pasta CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) de um site atualizado. O Configuration Manager exige que você use arquivos de origem que correspondam à versão do site existente ao qual seu novo site se conectará.

Um site secundário deve ser instalado no console do Configuration Manager. Dessa forma, os sites secundários sempre são instalados usando arquivos de origem do site primário pai.

**Método de instalação**: o método usado para instalar sites adicionais depende do tipo de site que você deseja instalar.
-   **Adicionar um site de administração central**: você pode usar o Assistente de Instalação do Configuration Manager ou uma linha de comando com script para instalar o novo site de administração central como um site pai para o site primário autônomo existente. Para obter mais informações, confira [Expansão de um site primário autônomo](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand).
-   **Adicionar um site primário filho**: você pode usar o Assistente de Instalação do Configuration Manager ou uma instalação de linha de comando para adicionar um site primário filho abaixo do site de administração central.
-   **Adicionar um site secundário**: use o console do Configuration Manager para instalar um site secundário como um site filho abaixo do site primário. Não há suporte para outros métodos para adicionar sites secundários.

## <a name="bkmk_tasks"></a> Tarefas comuns para concluir antes de iniciar uma instalação
-   **Entender a topologia da hierarquia que você usará para a implantação**    
Para obter mais informações, consulte [Criar uma hierarquia de sites para o System Center Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

-   **Preparar e configurar servidores individuais para atender aos pré-requisitos e configurações com suporte para uso com o Configuration Manager**         
Para obter mais informações, consulte [Site and site system prerequisites](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Pré-requisitos de site e sistema de sites).  

-   **Instalar e configurar o SQL Server para hospedar o banco de dados do site**     
Para obter mais informações, consulte [Suporte para versões do SQL Server para o System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   **Preparar o ambiente de rede para dar suporte ao Configuration Manager**      
Para obter mais informações, consulte [Configurar firewalls, portas e domínios para preparar-se para o Configuration Manager](../../../../core/plan-design/network/configure-firewalls-ports-domains.md).  

- **Se você usar uma PKI (Infraestrutura de Chave Pública), prepare sua infraestrutura e certificados**      
Para obter mais informações, consulte [Requisitos de certificado PKI para o Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).

-   **Instalar as últimas atualizações de segurança nos computadores que você usará como servidores de site ou servidores de sistema de sites e, quando necessário, reiniciá-los**

## <a name="bkmk_sitecodes"></a> Sobre nomes de site e códigos de site
Códigos e nomes de site são usados para identificar e gerenciar os sites em uma hierarquia do Configuration Manager. No console do Configuration Manager, o código e o nome do site são exibidos no formato &lt;*código do site*\> - &lt;*nome do site*\>. Todo código do site que você utiliza na hierarquia deve ser exclusivo. Se o esquema do Active Directory for estendido para o Configuration Manager e os sites estiverem publicando dados, os códigos do site usados dentro de uma floresta do Active Directory deverão ser exclusivos, mesmo se forem usados em uma hierarquia do Configuration Manager diferente ou se forem usados em instalações anteriores do Configuration Manager. Certifique-se de planejar seus códigos e nomes de site antes de implantar a hierarquia.

### <a name="specify-a-site-code-and-site-name"></a>Especifique um código do site e um nome de site
Quando você executa a Instalação do Configuration Manager, um código e um nome do site são solicitados para o site de administração central e para cada instalação de site primário e secundário. Um código do site deve identificar exclusivamente cada site na hierarquia. Como o código do site é usado em nomes de pastas, nunca use os nomes a seguir para o código do site, que incluem nomes reservados do Windows e do Configuration Manager:
  -  AUX
  -  CON
  -  NUL
  -  PRN
  -  SMS

> [!NOTE]
> A Instalação do Configuration Manager não verifica se o código do site ainda não está em uso.

Para inserir o código do site quando estiver executando a Instalação do Configuration Manager, você deverá inserir três caracteres alfanuméricos. Somente as letras de *A* a *Z* e os números de *0* a *9*, em qualquer combinação, são permitidos em códigos de site. A sequência de letras ou números não tem efeito sobre a comunicação entre sites. Por exemplo, não é necessário nomear um site primário *ABC* e um local secundário *DEF*.

O nome do site é um identificador de nome amigável para o site. Você pode usar apenas os caracteres de *A* a *Z*, *a* a *z*, *0* a *9* e o hífen (*-*) em nomes de sites.

> [!IMPORTANT]
> Não há suporte para uma alteração do código do site ou do nome do site após instalar o site.

### <a name="reuse-a-site-code"></a>Reutilizar um código do site
Os códigos do site não poderão ser usados mais de uma vez em uma hierarquia do Configuration Manager para um site de administração central ou um site primário, mesmo se o site original e o código do site tiverem sido desinstalados. Se você reutilizar um código do site, correrá o risco de ter conflitos de ID de objeto na hierarquia. Será possível reutilizar o código do site para um site secundário se esse site secundário e o código do site não estiverem mais em uso na hierarquia do Configuration Manager ou na floresta do Active Directory.

## <a name="limits-and-restrictions-for-installed-sites"></a>Limites e restrições para sites instalados
Antes de instalar um site, é importante entender as seguintes limitações que se aplicam aos sites e hierarquias de site:
-   Após executar a Instalação, não é possível alterar as seguintes propriedades do site sem desinstalar o site e reinstalá-lo usando os novos valores:  
  -   Diretório de instalação dos Arquivos de Programas  
  -   Código do site  
  -   Descrição do site  
-   Quando a hierarquia inclui um site de administração central:  
  -   O Configuration Manager não dá suporte para a movimentação de um site primário filho para fora de uma hierarquia para criar um site primário autônomo ou para anexá-lo a uma hierarquia diferente. Em vez disso, desinstale o site primário filho e, em seguida, reinstale-o como um novo site primário autônomo ou como um site filho do site de administração central de uma hierarquia diferente.  


## <a name="bkmk_optionalsteps"></a> Etapas opcionais antes de executar a Instalação
**Executar manualmente [Downloader de Instalação](../../../../core/servers/deploy/install/setup-downloader.md)**

Para baixar os arquivos de Instalação atualizados para o Configuration Manager, você pode executar o Downloader de Instalação. Se o computador no qual você executará a instalação não estiver conectado à Internet ou se você pretende instalar vários servidores do site, considere usar o Downloader de Instalação para baixar as atualizações necessárias para a Instalação. Aqui estão algumas informações adicionais:
-  Por padrão, a instalação se conecta à Internet para baixar os arquivos de Instalação atualizados.
-  Por padrão, os arquivos são armazenados na pasta Redist.
-  Você pode direcionar a instalação para um local na rede em que você armazenou anteriormente uma cópia desses arquivos.

**Executar manualmente o [Verificador de Pré-requisito](../../../../core/servers/deploy/install/prerequisite-checker.md)**

Para identificar e corrigir problemas antes de executar a Instalação para instalar um site e antes de instalar uma função de sistema de sites em um servidor, você pode executar o Verificador de Pré-requisitos. O Verificador de Pré-requisitos ajuda a garantir que o computador atenda aos requisitos para hospedar o site ou função do sistema de sites. Aqui estão algumas informações adicionais:
 -  Por padrão, a Instalação executa o Verificador do Pré-requisitos.
 -  Se houver erros, a Instalação será parada até o problema ser corrigido.

**Identifique portas opcionais**

Você pode identificar portas opcionais para os sistemas de sites e clientes usarem. Aqui estão algumas informações adicionais:
 -  Por padrão, os clientes e sistemas de sites usam portas predefinidas para se comunicar.
 -  Durante a instalação, você pode configurar portas alternativas.

 Para obter mais informações, consulte [Portas usadas no System Center Configuration Manager](../../../../core/plan-design/hierarchy/ports.md).
