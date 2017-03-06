---
title: "Afinidade de usuário para dispositivos híbridos gerenciados no Configuration Manager | Microsoft Docs"
description: "Configurar afinidade de usuário para dispositivos gerenciados no Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5d520a7-e9e5-40ee-91f9-f2684214beb6
caps.latest.revision: 6
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: 74dcc0f4e680893db804956615248b7e1230d2b5
ms.lasthandoff: 12/16/2016

---
# <a name="user-affinity-for-hybrid-managed-devices-in-configuration-manager"></a>Afinidade de usuário para dispositivos híbridos gerenciados no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Ao configurar perfis para dispositivos corporativos, o administrador pode especificar se os dispositivos gerenciados podem ter *afinidade de usuário*, que identifica um usuário específico com o dispositivo.  

##  <a name="a-namebkmkioscpa-managed-devices-with-user-affinity"></a><a name="BKMK_iOSCP"></a> Dispositivos gerenciados com afinidade de usuário  
 Dispositivos configurados com **user affinity** podem instalar e executar o aplicativo de Portal da Empresa para baixar aplicativos e gerenciar dispositivos. Assim que os usuários receberem seus dispositivos, eles deverão concluir várias etapas adicionais a fim de completar o Assistente de Configuração e instalar o aplicativo de Portal da Empresa.  

#### <a name="how-to-enroll-ios-devices-with-user-affinity"></a>Como registrar dispositivos iOS com afinidade de usuário  

1.  Quando os usuários ligarem seus dispositivos pela primeira vez, receberão uma solicitação para concluir o Assistente de Configuração. O perfil de registro pode especificar a solicitação de credenciais durante a instalação. Os usuários devem usar as credenciais (ou seja, o nome pessoal exclusivo ou UPN) associadas à assinatura do Intune.  

2.  Durante a configuração, será solicitado que os usuários informem uma ID Apple. É necessário fornecer uma ID Apple para que o dispositivo seja instalado no Portal da Empresa. Os usuários também podem fornecer uma ID Apple depois da conclusão na instalação nas **Configuração** do iOS.  

3.  Após a conclusão da configuração, o dispositivo iOS deve instalar o aplicativo Portal da Empresa por meio da App Store, por exemplo, [aplicativo Portal da Empresa](https://itunes.apple.com/us/app/id719171358).  

4.  Agora, o usuário pode fazer logon no Portal da Empresa com o UPN usado durante a configuração do dispositivo.  

5.  Após o logon, o usuário recebe uma solicitação para registrar seu dispositivo. A primeira etapa é **Identificar o dispositivo**. O aplicativo apresenta uma lista de dispositivos iOS que foram registrados pela empresa e atribuídos à conta do Intune do usuário final. Escolha o dispositivo correspondente.  

     Se o dispositivo ainda não tiver sido registrado pela empresa, selecione "novo dispositivo" para continuar com o fluxo de registro padrão.  

6.  Na próxima tela, o usuário deverá confirmar o número de série do novo dispositivo. O usuário pode tocar no link "confirmar o Número de Série" para iniciar o aplicativo de Configurações para verificar o número de série. Em seguida, o usuário deve inserir os quatro últimos caracteres do número de série no aplicativo Portal da Empresa.  

     Essa etapa verifica se o dispositivo é o dispositivo corporativo registrado no Intune. Se o número de série no dispositivo não corresponder, o dispositivo incorreto terá sido selecionado. Volte para a tela anterior e selecione um dispositivo diferente.  

7.  Após a verificação do número de série, o aplicativo Portal da Empresa redirecionará para o site do Portal da Empresa a fim de finalizar o registro e solicitará que o usuário retorne ao aplicativo.  

8.  O registro está concluído. Agora você pode usar este dispositivo com o conjunto completo de recursos.  

##  <a name="a-namebkmknouaa-managed-devices-without-user-affinity"></a><a name="BKMK_noUA"></a> Dispositivos gerenciados sem afinidade de usuário  
 Dispositivos configurados com **no user affinity** não têm suporte no Portal da Empresa e não devem instalar o aplicativo. O Portal da Empresa se destina a usuários com credenciais corporativas e que precisam de acesso aos recursos corporativos personalizados (por exemplo, email). O dispositivo registrado sem **afinidade do usuário** não deve ter uma entrada de usuário dedicada. Quiosque, ponto de venda (PDV) ou dispositivos de utilitário compartilhados são casos de uso comuns de dispositivos registrados sem afinidade de usuário. Se a afinidade de usuário for necessária, certifique-se de que o perfil de registro do dispositivo tenha a opção **Afinidade de Usuário** selecionada antes de registrar o dispositivo. Para alterar o status de afinidade em um dispositivo, você deverá desativar e registrar novamente o dispositivo.

