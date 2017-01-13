---
title: Preparar para instalar sites | Microsoft Docs
description: "Leia esses detalhes para economizar tempo durante a instalação de vários sites e evitar erros."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 0534d1eb587cb01f35d811d72ddfe6ceb07e5b7c

---
# <a name="prepare-to-install-system-center-configuration-manager-sites"></a>Preparar para instalar sites do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para se preparar para uma implantação bem-sucedida de um ou mais sites do System Center Configuration Manager, familiarize-se com os detalhes neste artigo. Essas etapas podem economizar tempo durante a instalação de vários sites e ajudar a evitar erros que podem resultar na necessidade de reinstalar um ou mais sites.
 > [!TIP]
 >  Os cenários a seguir são semelhantes a, mas diferentes da instalação de um site da Branch Atual do System Center Configuration Manager:
 > -  **Atualizar**: instale o System Center Configuration Manager para **atualizar** do System Center 2012 Configuration Manager, confira [Atualização para o System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md)
 > -  **Atualizar**: use as atualizações no console para instalar uma nova **versão de atualização** para um site do System Center Configuration Manager existente, confira [Updates for System Center Configuration Manager](../../../../core/servers/manage/updates.md) (Atualizações para o System Center Configuration Manager)
 > -  **Migrar**: para **migrar dados** de outra hierarquia do Configuration Manager para a hierarquia atual do System Center Configuration Manager, confira [Planning for migration to System Center Configuration Manager](../../../../core/migration/planning-for-migration.md) (Planejando a migração para o System Center Configuration Manager)



## <a name="a-namebkmkoptionsa-options-for-installing-different-types-of-sites"></a><a name="bkmk_options"></a> Opções de instalação de diferentes tipos de sites
Quando você instala um novo Configuration Manager, a versão dos arquivos de origem que você pode usar depende da versão dos sites que já estão na hierarquia (caso haja) e os métodos de instalação disponíveis dependem do tipo de site que deseja instalar.  

Antes de instalar sites, certifique-se de planejar sua hierarquia e entender o tipo de site que você deseja instalar. Para obter mais informações, confira [Design a hierarchy of sites](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md) (Criar uma hierarquia de sites).


### <a name="first-site"></a>Primeiro site
O primeiro site que você instalará para uma hierarquia será um site primário autônomo ou um site de administração central.

**Mídia de instalação**: para instalar um site de administração central ou um site primário autônomo como o primeiro site em uma nova hierarquia, você deve [usar uma versão de linha de base](../../../../core/servers/manage/updates.md#bkmk_Baselines) do Configuration Manager. Não instale o primeiro site de uma nova hierarquia usando arquivos de origem atualizados da [pasta CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) de nenhum site.

**Método de instalação**: você pode instalar qualquer tipo de site usando o [Assistente de Instalação do Configuration Manager](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md) ou pode configurar um script para usar com uma [instalação de linha de comando com scripts](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).


### <a name="additional-sites"></a>Sites adicionais
Depois de instalar o site inicial, você pode adicionar sites adicionais a qualquer momento. As opções a seguir existem para incluir sites adicionais (até os [limites com suporte](../../../../core/plan-design/configs/size-and-scale-numbers.md)):

Site que você tem          |Sites adicionais que você pode instalar  
---------                   |---------
Site de administração central |   Instale um site primário filho            
Site primário filho          |   Instale um site secundário        
Site primário autônomo    |   Instale um site secundário<br />Expanda o site primário, o que converte o site primário autônomo em um site primário filho

**Mídia de instalação**: quando você instala um site de administração central para expandir em um site primário autônomo ou instala um novo site primário filho em uma hierarquia existente, você deve usar a mídia de instalação (arquivos de origem) que corresponde à versão do site ou sites existentes.
> [!IMPORTANT]
> Se você tiver instalado atualizações no console que alteraram a versão dos sites instalados anteriormente, não use a mídia de instalação original. Em vez disso, use os arquivos de origem da [pasta CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) de um site atualizado.  O Configuration Manager exige que você use arquivos de origem que correspondam à versão do site existente ao qual seu novo site se conectará.


Um site secundário deve ser instalado de dentro do console do Configuration Manager e, portanto, sempre é instalado usando arquivos de origem do site primário pai.

**Método de instalação**: o método usado para instalar sites adicionais depende do tipo de site que você deseja instalar.
-   **Adicionando um site de administração central**:  
Você pode usar o Assistente de Instalação do Configuration Manager ou uma linha de comando com script para instalar o novo site de administração central como um site pai para o site primário autônomo existente.  Para obter mais informações, confira [Expandir um site primário autônomo](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand).
-   **Instalando um site primário filho**:  
Você pode usar o Assistente de Instalação do Configuration Manager ou uma instalação de linha de comando para adicionar um site primário filho abaixo do site de administração central.
-   **Adicionando um site secundário**:   
Use o console do Configuration Manager para instalar um site secundário como um site filho abaixo do site primário. Não há suporte para outros métodos para sites secundários.



## <a name="a-namebkmktasksa--common-tasks-to-complete-before-starting-an-install"></a><a name="bkmk_tasks"></a> Tarefas comuns para concluir antes de iniciar uma instalação
-   Entender a topologia da hierarquia que você usará para a implantação    
     (confira [Design a hierarchy of sites for System Center Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md) (Criar uma hierarquia dos sites para o System Center Configuration Manager))  

-   Preparar e configurar servidores individuais para atender aos pré-requisitos e configurações com suporte para uso com o Configuration Manager (confira [Site and site system prerequisites](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Pré-requisitos do site e sistema de sites))  

-   Instalar e configurar o SQL Server para hospedar o banco de dados do site (confira    
    [Support for SQL Server versions for System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md) (Suporte para versões do SQL Server para o System Center Configuration Manager)  

-   Preparar o ambiente de rede para dar suporte ao Configuration Manager (confira [Configurar firewalls, portas e domínios para preparar para o Configuration Manager](/sccm/core/plan-design/network/configure-firewalls-ports-domains))  

-   Se você for usar um PKI, preparar sua infraestrutura e certificados (confira [Requisitos de certificado PKI para o Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md))

-   Instalar as últimas atualizações de segurança nos computadores que você usará como servidores de site ou servidores de sistema de sites e, quando necessário, reiniciá-los.



## <a name="a-namebkmksitecodesa--about-site-names-and-site-codes"></a><a name="bkmk_sitecodes"></a> Sobre nomes de site e códigos de site
Códigos e nomes de site são usados para identificar e gerenciar os sites em uma hierarquia do Configuration Manager. No console do Configuration Manager, o código e o nome do site são exibidos no formato &lt;código do site\> - &lt;nome do site\>. Todo código do site que você utiliza na hierarquia deve ser exclusivo. Se o esquema do Active Directory for estendido para o Configuration Manager e os sites estiverem publicando dados, os códigos do site usados dentro de uma floresta do Active Directory deverão ser exclusivos, mesmo se forem usados em uma hierarquia do Configuration Manager diferente, ou se forem usados em instalações anteriores do Configuration Manager. Certifique-se de planejar seus códigos e nomes de site antes de implantar a hierarquia.

### <a name="specify-a-site-code-and-site-name"></a>Especificar um código do site e um nome de site
Durante a Instalação do Configuration Manager, um código e um nome do site são solicitados para o site de administração central e para cada instalação de site primário e secundário. O código do site deve identificar exclusivamente cada site na hierarquia. Como o código do site é usado em nomes de pastas, nunca use os nomes a seguir para o código do site, que incluem nomes reservados do Windows e do Configuration Manager:
  -  AUX
  -  CON
  -  NUL
  -  PRN
  -  SMS

> [!NOTE]
> A Instalação do Configuration Manager não verifica se o código do site especificado ainda não está em uso.



Para inserir o código do site durante a Instalação do Configuration Manager, você deve inserir três caracteres alfanuméricos. Somente as letras de A a Z, números de 0 a 9, ou combinações dos dois são permitidos ao especificar códigos de site. A sequência de letras ou números não tem efeito sobre a comunicação entre sites. Por exemplo, não é necessário nomear um site primário ABC e um local secundário DEF.

O nome do site é um identificador de nome amigável para o site. Use somente caracteres padrão de A a Z, a - z, 0 a 9, e o hífen (-) em nomes de site.
> [!IMPORTANT]
> A alteração do código ou do nome do site após a instalação não é suportada.

### <a name="reuse-a-site-code"></a>Reutilizar um código do site
Os códigos do site não poderão ser usados mais de uma vez em uma hierarquia do Configuration Manager para um site de administração central ou sites primários, mesmo se o site original e o código do site tiverem sido desinstalados. Se você reutiliza um código do site, corre o risco de ter conflitos de ID de objeto na hierarquia. Será possível reutilizar o código do site para um site secundário se esse site secundário e o código do site não estiverem mais em uso na hierarquia do Configuration Manager ou na floresta do Active Directory.


## <a name="limits-and-restrictions-for-installed-sites"></a>Limites e restrições para sites instalados
Antes de instalar sites, compreenda as seguintes limitações que se aplicam para sites e hierarquias:
-   Após a conclusão da instalação, você não poderá alterar as seguintes propriedades do site sem desinstalá-lo e, em seguida, reinstalá-lo com os novos valores:  
    -   O diretório de instalação dos arquivos de programa  
    -   Código do site  
    -   Descrição do site  
-   Quando a hierarquia inclui um site de administração central:  
    -   O Configuration Manager não dá suporte para a movimentação de um site primário filho para fora de uma hierarquia para criar um site primário autônomo ou para anexá-lo a uma hierarquia diferente. Em vez disso, desinstale o site primário filho e, em seguida, reinstale-o como um novo site primário autônomo ou filho do site de administração central de uma hierarquia diferente.  


## <a name="a-namebkmkoptionalstepsa--optional-steps-to-run-before-starting-setup"></a><a name="bkmk_optionalsteps"></a> Etapas opcionais para executar antes de iniciar a instalação
**Você pode executar manualmente o [Downloader de Instalação](../../../../core/servers/deploy/install/setup-downloader.md)** para baixar os arquivos de instalação atualizados para o Configuration Manager.

Quando o computador no qual você executará a instalação não estiver conectado à Internet ou se você pretende instalar vários servidores do site, considere usar o Downloader de Instalação para baixar as atualizações necessárias para os arquivos de instalação:

-  Por padrão, a instalação se conectará à Internet para baixar os arquivos de instalação atualizados
-  Por padrão, os arquivos são armazenados em uma pasta chamada Redist
-  Você pode direcionar a instalação para um local na rede em que você armazenou anteriormente uma cópia desses arquivos


**Você pode executar manualmente o [Verificador de Pré-requisitos](../../../../core/servers/deploy/install/prerequisite-checker.md)** para identificar e corrigir problemas antes de executar a instalação. Antes de iniciar a instalação de um site e antes de instalar uma função de sistema de sites em um servidor, você pode executar o Verificador de Pré-requisitos para garantir que o computador atenda aos requisitos para hospedar o site ou a função de sistema de sites.
 -  Por padrão, a instalação executará o verificador de pré-requisitos.
 -  Se houver erros, a instalação será interrompida até o problema ser corrigido.


**Identifique portas opcionais** a serem usadas para os sistemas de sites e clientes.
 -  Por padrão, clientes e sistemas de sites usam portas predefinidas para se comunicar.
 -  Durante a instalação, você pode configurar portas alternativas.
 -  Para mais informações, confira [Ports used in System Center Configuration Manager](../../../../core/plan-design/hierarchy/ports.md) (Portas usadas no System Center Configuration Manager)



<!--HONumber=Dec16_HO3-->


