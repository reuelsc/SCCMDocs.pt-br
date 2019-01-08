---
title: Preparar o cache par do Windows PE para reduzir o tráfego da WAN
titleSuffix: Configuration Manager
description: O Cache Par do Windows PE funciona no Windows PE para obter o conteúdo de um par local e minimizar o tráfego da WAN quando não há nenhum ponto de distribuição local.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 6c64f276-b88c-4b1e-8073-331876a03038
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 804b21733422bd654764f2199fe33d184d54cce4
ms.sourcegitcommit: d021f82e4bc35a8e9b5d291bf779ce52b4f47eb8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53656468"
---
# <a name="prepare-windows-pe-peer-cache-to-reduce-wan-traffic-in-system-center-configuration-manager"></a>Preparar o cache par do Windows PE para reduzir o tráfego da WAN no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Ao implantar um novo sistema operacional no System Center Configuration Manager, os computadores que executam a sequência de tarefas podem usar o Cache Par do Windows PE para obter o conteúdo de um par local (uma fonte de cache par), em vez de baixar o conteúdo de um ponto de distribuição. Isso ajuda a minimizar o tráfego de WAN (rede de longa distância) em cenários de filial em que não há nenhum ponto de distribuição local.  

 O Cache par do Windows PE é semelhante ao [Windows BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#bkmk_branchcache), mas funciona no Windows PE (Ambiente de Pré-Instalação do Windows). Os seguintes termos são usados para descrever os clientes que usam o Cache par do Windows PE:  

-   Um **cliente de cache de sistemas pares** é um computador configurado para usar o Cache de sistemas pares do Windows PE.  

-   Uma **fonte de cache de sistemas pares** é um cliente configurado para o cache de sistemas pares e que disponibiliza o conteúdo para outros clientes de cache de sistemas pares que solicitam esse conteúdo.  

Use as seções a seguir para gerenciar o Cache Par.

##  <a name="BKMK_PeerCacheObjects"></a> Objetos armazenados em uma fonte de cache par  
 Uma sequência de tarefas configuradas para usar o Cache par do Windows PE pode obter os seguintes objetos de conteúdo durante a execução no Windows PE:  

- Imagem do sistema operacional  

- Pacote de Drivers  

- Pacotes e programas (Quando o cliente continua executando a sequência de tarefas no sistema operacional completo, o cliente receberá o conteúdo de uma fonte de cache par se a sequência de tarefas foi originalmente configurada para o cache par durante a execução no Windows PE.)  

- Imagens de inicialização adicionais  

  Os seguintes objetos de conteúdo nunca transferem usando cache par. Em vez disso, eles são transferidos de um ponto de distribuição ou pelo Windows BranchCache se você tiver configurado o Windows BranchCache em seu ambiente:  

- Aplicativos  

- Atualizações de software  

##  <a name="BKMK_PeerCacheWork"></a> Como funciona o cache par no Windows PE?  
 Considere um cenário com uma filial que não tem um ponto de distribuição, mas que tem vários clientes habilitados para usar o Cache par do Windows PE. Você implanta a sequência de tarefas configurada para usar cache par para vários clientes que estão configurados para ser parte da fonte de cache par. O primeiro cliente a executar a sequência de tarefas transmite uma solicitação para uma associação com o conteúdo. Ele não encontra uma, então obtém o conteúdo do ponto de distribuição na WAN. O cliente instala a nova imagem e armazena o conteúdo em seu cache do cliente do Configuration Manager para que possa funcionar como uma fonte de cache par para outros clientes. Quando o próximo cliente executa a sequência de tarefas, ele transmite uma solicitação na sub-rede para uma fonte de cache de sistemas pares, e esse primeiro cliente responde e disponibiliza o conteúdo armazenado em cache.  

##  <a name="BKMK_PeerCacheDetermine"></a> Determinar quais clientes serão parte da fonte de Cache par do Windows PE  
 Para ajudar você a determinar quais computadores serão selecionados como uma fonte de Cache par do Windows PE, há várias coisas que você deve considerar:  

-   A fonte de Cache par do Windows PE deve ser um computador desktop que está sempre ligado e disponível para clientes de cache par.  

-   O Cache par do Windows PE tem um tamanho de cache de cliente suficiente para armazenar as imagens.  

##  <a name="BKMK_PeerCacheRequirements"></a> Requisitos para um cliente usar uma fonte de Cache par do Windows PE  
 Para os clientes usarem uma fonte de Cache par do Windows PE, eles devem atender aos seguintes requisitos:  

-   O cliente do Configuration Manager deve estar habilitado para se comunicar entre as seguintes portas em sua rede:  

    -   Porta da difusão de rede inicial para encontrar uma fonte de cache par. Por padrão, essa porta é a 8004.  

    -   Porta para download de conteúdo de uma fonte de cache par (HTTP e HTTPS): Por padrão, essa porta é a 8003.  

        > [!TIP]  
        >  Os clientes usarão HTTPS para baixar o conteúdo quando ele estiver disponível. No entanto, o mesmo número da porta será usado para HTTP ou HTTPS.  

-   [Configurar o cache de cliente para clientes do Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_ClientCache) nos clientes para garantir que eles têm espaço suficiente para manter e armazenar as imagens de implantação. O Cache par do Windows PE não afeta a configuração ou o comportamento do cache do cliente.  

-   As opções de implantação para a implantação de sequência de tarefas devem ser configuradas como Baixar conteúdo localmente quando necessário por sequência de tarefas.  

##  <a name="BKMK_PeerCacheConfigure"></a> Configurar o Cache par do Windows PE  
 Você pode usar os métodos a seguir para provisionar um cliente com o conteúdo de cache par para que ele possa servir como uma fonte de cache par:  

- Um cliente de cache de sistemas pares que não possa encontrar uma fonte de cache de sistemas pares com o conteúdo a baixará de um ponto de distribuição.  Se o cliente recebe configurações do cliente que permitem que o cache de sistemas pares e a sequência de tarefas são configuradas para preservar o conteúdo em cache, o cliente torna-se uma fonte de cache de sistemas pares.  

- Um cliente de cache de sistemas pares pode obter o conteúdo de outro cliente de cache de sistemas pares (uma fonte de cache de sistemas pares).  Como o cliente está configurado para o cache de sistemas pares, quando ele executa uma sequência de tarefas configurada para preservar o conteúdo em cache, o cliente torna-se uma fonte de cache de sistemas pares.  

- Um cliente executa uma sequência de tarefas que inclui a etapa opcional, [Download Package Content](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent), que é usada para pré-configurar o conteúdo relevante que é incluído na sequência de tarefas de Cache par do Windows PE. Ao usar este método:  

  -   O cliente não precisa instalar a imagem que está sendo implantada.  

  -   Além da opção **Baixar Conteúdo do Pacote** , a sequência de tarefas também deve usar a opção **cache de cliente do Configuration Manager** . Use esta opção para armazenar o conteúdo no cache dos clientes para que o cliente possa agir como uma fonte de cache de sistemas pares para outros clientes de cache de sistemas pares.  

  Os procedimentos a seguir ajudarão você a configurar o Cache de sistemas pares do Windows PE em clientes e configurar as sequências de tarefas que dão suporte ao cache de sistemas pares.  

### <a name="to-configure-the-windows-pe-peer-cache-source-computers"></a>Para configurar os computadores de origem do Cache par do Windows PE  

1. No console do Configuration Manager, navegue até **Administração** > **Configurações do Cliente** e crie novas **Configurações Personalizadas do Dispositivo Cliente** ou edite um objeto de configurações existente. Você também pode configurar isso para o objeto **Configurações Padrão do Cliente** .  

   > [!TIP]  
   >  Use um objeto de configurações personalizadas para gerenciar quais clientes recebem esta configuração. Por exemplo, talvez você deseje evitar essa configuração nos laptops dos usuários que estejam frequentemente em movimento. Um sistema altamente móvel pode ser uma fonte inadequada para fornecer conteúdo para outros clientes de cache de sistemas pares.  
   >   
   >  Lembre-se também de que quando você definir essa configuração como parte das **Configurações do Cliente Padrão**, a configuração se aplicará a todos os clientes em seu ambiente.  

2. Em **Configurações do Cache do Cliente**, defina **Permitir que o cliente do Configuration Manager no SO completo compartilhe conteúdo** como **Sim**.  

   -   Por padrão, somente o HTTP está habilitado. Se desejar permitir que os clientes baixem conteúdo por HTTPS, defina **Habilitar HTTPS para a comunicação ponto a ponto do cliente** como **Sim**.  

   -   Por padrão, a porta para difusões é definida como 8004 e a porta para downloads de conteúdo é definida como 8003. É possível alterar os dois.  

3. Salvar e implantar as configurações do cliente para os clientes que você selecionar uma fonte de cache par.  

   Depois que um dispositivo for configurado com este objeto de configurações, o dispositivo estará configurado para agir como uma fonte de cache de sistemas pares. Estas configurações devem ser implantadas em clientes potenciais de cache de sistemas pares para configurar as portas e os protocolos necessários.  

###  <a name="BKMK_PeerCacheConfigureTS"></a> Configurar uma sequência de tarefas para o Cache par do Windows PE  
 Ao configurar a sequência de tarefas, use as seguintes variáveis de sequência de tarefas como Variáveis da Coleção na coleção em que a sequência de tarefas será implantada:  

- **SMSTSPeerDownload**  

   Valor:  TRUE  

   Isso permite que o cliente use o Cache de sistemas pares do Windows PE.  

- **SMSTSPeerRequestPort**  

   Valor: <Número da porta\>  

   Quando você não usar a porta padrão configurada nas Configurações do Cliente (8004), será preciso configurar essa variável com um valor personalizado da porta de rede a ser usada para a difusão inicial.  

- **SMSTSPreserveContent**  

   Valor: TRUE  

   Isso sinaliza o conteúdo na sequência de tarefas a ser mantido no cache do cliente do Configuration Manager após a implantação. Isso é diferente de usar SMSTSPersisContent, que apenas preserva o conteúdo durante a sequência de tarefas e usa o cache da sequência de tarefas, e não o cache do cliente do Configuration Manager.  

  Para saber mais, confira [Variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables).  

###  <a name="BKMK_PeerCacheValidate"></a> Validar o sucesso do uso de Cache par do Windows PE  
 Depois de usar o Cache par do Windows PE para implantar e instalar uma sequência de tarefas, é possível confirmar se o cache par foi usado com êxito no processo ao exibir o **smsts.log** no cliente que executou a sequência de tarefas.  

 No log, encontre uma entrada semelhante à seguinte, em que <*SourceServerName*> identifica o computador por meio do qual o cliente obteve o conteúdo. Este computador deve ser uma fonte de cache de sistemas pares e não um servidor de ponto de distribuição. Outros detalhes podem variar de acordo com seu ambiente e configurações locais.  

-   *<![LOG[Arquivo baixado de http:// <SourceServerName\>:8003/SCCM_BranchCache$/SS10000C/sccm?/install.wim to C:\\_SMSTaskSequence\Packages\SS10000C\install.wim ]LOG]!><time="14:24:33.329+420" date="06-26-2015" component="ApplyOperatingSystem" context="" type="1" thread="1256" file="downloadcontent.cpp:1626">*  
