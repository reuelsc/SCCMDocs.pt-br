---
title: "Criar mídia de sequência de tarefas com o System Center Configuration Manager"
description: "Crie mídia de sequência de tarefas, como um CD, para implantar um sistema operacional em um computador de destino em seu ambiente do Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
caps.latest.revision: 8
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f00defcdb56e37476ac24d8ce25d1dc5fb2f3260


---
# <a name="create-task-sequence-media-with-system-center-configuration-manager"></a>Criar mídia de sequência de tarefas com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode usar mídia para capturar uma imagem de sistema operacional de um computador de referência ou implantar um sistema operacional em um computador de destino em seu ambiente do System Center Configuration Manager. A mídia que você criar pode ser um conjunto de CD, DVD ou uma unidade flash USB.  

 A mídia é usada muitas vezes para implantar sistemas operacionais em computadores de destino que não têm uma conexão de rede ou que têm uma conexão de baixa largura de banda em seu local do Configuration Manager. No entanto, a mídia de implantação também é usada para iniciar a implantação do sistema operacional fora de um sistema operacional Windows. Esse segundo uso de mídia de implantação é importante às vezes, quando não há sistema operacional no computador de destino, o sistema operacional está em um estado não operacional ou o usuário administrativo deseja fazer a repartição do disco rígido no computador de destino.  

 A mídia de implantação inclui mídia inicializável, mídia autônoma e mídia em pré-teste. O conteúdo da mídia de implantação varia, dependendo do tipo de mídia que você usar. Por exemplo, mídia autônoma contém a sequência de tarefas que implanta o sistema operacional, enquanto outros tipos de mídia recuperam sequências de tarefas do ponto de gerenciamento.  

> [!IMPORTANT]  
>  Para criar uma mídia de sequência de tarefas, é preciso ser um administrador no computador no qual você executa o console do Configuration Manager. Se você não for um administrador, serão solicitadas as credenciais de administrador quando você iniciar o assistente para Criar Mídia de Sequência de Tarefas.  

##  <a name="a-namebkmkplancapturemediaa-capture-media-for-operating-system-images"></a><a name="BKMK_PlanCaptureMedia"></a> Mídia de captura para imagens do sistema operacional  
 Mídia de captura permite que você capture uma imagem do sistema operacional de um computador de referência. A mídia de captura contém a imagem de inicialização que inicia o computador de referência e a sequência de tarefas que captura a imagem do sistema operacional. Para obter informações sobre como criar mídia de captura, consulte [Create capture media with System Center Configuration Manager](create-capture-media.md) (Criar mídia de captura com o System Center Configuration Manager).  

##  <a name="a-namebkmkplanbootablemediaa-bootable-media-operating-system-deployments"></a><a name="BKMK_PlanBootableMedia"></a> Implantações de sistema operacional com mídia inicializável  
 A mídia inicializável contém somente a imagem de inicialização, [comandos prestart](../understand/prestart-commands-for-task-sequence-media.md) opcionais e seus arquivos necessários, bem como binários do Configuration Manager. Quando o computador de destino é iniciado, conecta-se à rede e recupera a sequência de tarefas, a imagem do sistema operacional e qualquer outro conteúdo necessário da rede. Como a sequência de tarefa não está na mídia, você pode alterar a sequência de tarefas ou o conteúdo sem precisar recriar a mídia.  

> [!IMPORTANT]  
>  Os pacotes em mídia inicializável não são criptografados. O usuário administrativo deve tomar as medidas de segurança apropriadas, como adicionar uma senha à mídia, verificar se o conteúdo do pacote está protegido contra usuários não autorizados.  

 Para obter informações sobre como criar a mídia inicializável, veja [Criar mídia inicializável](create-bootable-media.md).  

##  <a name="a-namebkmkplanprestagedmediaa-prestaged-media-operating-system-deployments"></a><a name="BKMK_PlanPrestagedMedia"></a> Implantações de sistema operacional com mídia pré-configurada  
 Mídia pré-testada permite que você pré-teste a mídia inicializável e uma imagem de sistema operacional em um disco rígido para o processo de provisionamento. A mídia pré-testada é um arquivo em formato WIM (Windows Imaging) que pode ser instalado em um computador bare-metal pelo fabricante ou em um centro de preparo corporativo que não está conectado ao ambiente do Configuration Manager.  

 A mídia em pré-teste contém a imagem de inicialização usada para iniciar o computador de destino e a imagem do sistema operacional aplicada ao computador de destino. Também é possível especificar aplicativos, pacotes e pacotes de driver para incluir como parte da mídia pré-configurada. A sequência de tarefas que implanta o sistema operacional não está incluída na mídia. Ao implantar uma sequência de tarefas que utiliza a mídia pré-configurada, o cliente primeiro verifica se há conteúdo válido no cache local da sequência de tarefas e, caso o conteúdo não possa ser localizado ou não foi revisado, o cliente baixa o conteúdo do ponto de distribuição.  

 A mídia pré-testada é aplicada à unidade de disco rígido de um novo computador antes do computador ser enviado ao usuário final. Quando o computador inicia pela primeira vez, após a mídia pré-testada ter sido aplicada, o computador inicia o Windows PE e conecta-se a um ponto de gerenciamento para localizar a sequência de tarefas que conclui o processo de implantação do sistema operacional.  

> [!IMPORTANT]  
>  Os pacotes em mídia pré-testada não são criptografados. O usuário administrativo deve tomar as medidas de segurança apropriadas, como adicionar uma senha à mídia, verificar se o conteúdo do pacote está protegido contra usuários não autorizados.  

 Para obter informações sobre como criar uma mídia pré-configurada, consulte [Criar mídia pré-configurada](create-prestaged-media.md).  

##  <a name="a-namebkmkplanstandalonemediaa-stand-alone-media-operating-system-deployments"></a><a name="BKMK_PlanStandaloneMedia"></a> Implantações de sistema operacional com mídia autônoma  
 Mídia autônoma contém tudo o que é necessário para implantar o sistema operacional. Isso inclui a sequência de tarefas e qualquer outro conteúdo necessário. Como tudo o que é necessário para implantar o sistema operacional é armazenado na mídia autônoma, o espaço em disco necessário para mídia autônoma é significativamente maior do que o espaço em disco necessário para outros tipos de mídia.  

 Para mais informações sobre como criar mídia autônoma, consulte [Criar mídia autônoma](create-stand-alone-media.md).  

## <a name="media-considerations-when-using-site-systems-configured-for-https"></a>Considerações sobre mídia ao usar sistemas de sites configurados para HTTPS  
 Quando seu ponto de gerenciamento e pontos de distribuição são configurados para usar comunicação HTTPS, você deve criar mídia de inicialização e mídia em pré-teste no site primário, não no site de administração central. Além disso, considere o seguinte para ajudá-lo a determinar se deseja configurar a mídia como dinâmica ou com base no site:  

-   Para configurar a mídia como mídia dinâmica, todos os sites primários devem ter autoridade de certificação raiz do site por meio do qual você criou a mídia. Você pode importar a autoridade de certificação raiz para todos os sites primários na sua hierarquia.  

-   Quando sites primários na hierarquia do Configuration Manager usam autoridades de certificação raízes diferentes, você deve usar mídia baseada em site em cada site.  



<!--HONumber=Nov16_HO1-->


