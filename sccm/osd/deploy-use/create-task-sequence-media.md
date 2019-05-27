---
title: Criar mídia de sequência de tarefas
titleSuffix: Configuration Manager
description: Crie uma mídia de sequência de tarefas para implantar um SO em um computador de destino no seu ambiente do Configuration Manager.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 101cee8ed63cacfc41481b2df69b42e1760d8837
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65082810"
---
# <a name="create-task-sequence-media"></a>Criar mídia de sequência de tarefas

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode usar a mídia para capturar uma imagem do SO de um computador de referência ou para implantar um SO em um computador de destino no seu ambiente do Configuration Manager. A mídia que você criar pode ser um conjunto de CD, DVD ou uma unidade flash USB.  

A mídia é usada principalmente para implantar sistemas operacionais em computadores de destino que não tenham uma conexão de rede ou que tenham uma conexão de baixa largura de banda com o seu site do Configuration Manager. No entanto, você também pode usar mídia para iniciar uma implantação de SO fora de um SO Windows existente. Esse método é útil quando não há um SO, quando o SO não está funcionando ou se você deseja reparticionar o disco rígido.  

A mídia de implantação inclui mídia inicializável, mídia autônoma e mídia em pré-teste. O conteúdo da mídia varia dependendo do tipo de mídia usado. Por exemplo, a mídia autônoma contém a sequência de tarefas que implanta o SO. Outros tipos de mídia recuperam sequências de tarefas do ponto de gerenciamento.  

> [!IMPORTANT]  
> Para criar uma mídia de sequência de tarefas, você deve ser administrador no computador em que executa o console do Configuration Manager. Se você não for administrador, receberá um prompt para inserir credenciais de administrador ao iniciar o Assistente para Criar Mídia de Sequência de Tarefas.  


## <a name="BKMK_PlanCaptureMedia"></a> Mídia de captura

A mídia de captura permite capturar uma imagem do sistema operacional em um computador de referência. A mídia de captura contém a imagem de inicialização que inicia o computador de referência e a sequência de tarefas que captura a imagem do SO.

Para saber mais sobre como criar a mídia de captura, confira [Criar mídia de captura](/sccm/osd/deploy-use/create-capture-media).  


## <a name="BKMK_PlanBootableMedia"></a> Mídia inicializável

A mídia inicializável contém os seguintes componentes:

- A imagem de inicialização
- [Comandos prestart](/sccm/osd/understand/prestart-commands-for-task-sequence-media) opcionais e seus arquivos necessários
- Binários do Configuration Manager

Quando o computador de destino é iniciado, ele se conecta à rede e recupera a sequência de tarefas, a imagem do SO e qualquer outro conteúdo necessário da rede. Como a sequência de tarefas não está na mídia, você pode alterar a sequência de tarefas ou o conteúdo sem ter que recriar a mídia.  

> [!IMPORTANT]  
> Os pacotes em uma mídia inicializável não são criptografados. Tome medidas de segurança apropriadas, como adicionar uma senha à mídia, para garantir que o conteúdo do pacote fique protegido contra usuários não autorizados.  

Para saber mais sobre como criar uma mídia inicializável, confira [Criar mídia inicializável](/sccm/osd/deploy-use/create-bootable-media).  


## <a name="BKMK_PlanPrestagedMedia"></a> Mídia em pré-teste

A mídia em pré-teste aplicar uma mídia inicializável e uma imagem do SO a um disco rígido antes do processo de provisionamento. A mídia em pré-teste é um arquivo de imagem do Windows (WIM). Ela pode ser instalada em um computador sem sistema operacional pelo fabricante ou no seu centro de preparo que não esteja conectado ao ambiente de produção do Configuration Manager.  

A mídia em pré-teste contém a imagem de inicialização usada para iniciar o computador de destino e a imagem do SO aplicada ao computador de destino. Também é possível especificar aplicativos, pacotes e pacotes de driver para incluir como parte da mídia em pré-teste. A sequência de tarefas que implanta o SO não está incluída na mídia. Quando você implanta uma sequência de tarefas que usa uma mídia em pré-teste, primeiro o cliente verifica o cache de sequência de tarefas local em busca de conteúdo válido. Se o conteúdo não for encontrado ou se tiver sido revisado, o cliente baixará o conteúdo de um ponto de distribuição ou par.  

A mídia em pré-teste é aplicada à unidade de disco rígido de um novo computador antes do computador ser enviado ao usuário final. Quando o computador é iniciado pela primeira vez após a aplicação da mídia em pré-teste, ele é iniciado no Windows PE. O computador se conecta a um ponto de gerenciamento para localizar a sequência de tarefas que conclui o processo de implantação do SO.  

> [!IMPORTANT]  
> Os pacotes na mídia em pré-teste não são criptografados. Tome medidas de segurança apropriadas, como adicionar uma senha à mídia, para garantir que o conteúdo do pacote fique protegido contra usuários não autorizados.  

Para saber mais sobre como criar uma em pré-teste, confira [Criar mídia em pré-teste](/sccm/osd/deploy-use/create-prestaged-media).  


## <a name="BKMK_PlanStandaloneMedia"></a> Mídia autônoma

A mídia autônoma contém tudo o que é necessário para implantar o SO. Esse conteúdo inclui a sequência de tarefas e qualquer outro conteúdo necessário. Como tudo o que é necessário para implantar o SO está armazenado na mídia autônoma, o espaço em disco necessário para a mídia autônoma é maior do que para outros tipos de mídia.  

Para saber mais sobre como criar uma mídia autônoma, confira [Criar mídia autônoma](/sccm/osd/deploy-use/create-stand-alone-media).  


## <a name="considerations-when-using-https"></a>Considerações ao usar o HTTPS

Quando você configurar seus pontos de gerenciamento e pontos de distribuição para usar HTTPS, crie a mídia de inicialização e a mídia em pré-teste em um site primário, e não no site de administração central. Além disso, considere o seguinte ponto para ajudá-lo a determinar se a mídia deve ser configurada como dinâmica ou baseada em site:  

- Para configurar a mídia como dinâmica, todos os sites primários devem ter a autoridade de certificação raiz (CA) do site no qual você criou essa mídia. Você pode importar a autoridade de certificação raiz para todos os sites primários na sua hierarquia.  

- Quando sites primários na hierarquia do Configuration Manager usam autoridades de certificação raízes diferentes, você deve usar mídia baseada em site em cada site.  
