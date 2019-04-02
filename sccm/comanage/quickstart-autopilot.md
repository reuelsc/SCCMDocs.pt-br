---
title: Windows Autopilot com cogerenciamento
titleSuffix: Configuration Manager
description: Use o Windows Autopilot com cogerenciamento no Configuration Manager para simplificar a configuração de novos dispositivos Windows 10.
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e3e3c97f-5945-49ab-a622-9f6fe6b9737e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28710b925444d681a161eff184b845a1cdd430b1
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56838745"
---
# <a name="windows-autopilot-with-co-management"></a>Windows Autopilot com cogerenciamento

Receber um novo dispositivo Windows 10 é empolgante. No entanto, pode levar um tempo para configurar todos os seus aplicativos e definir as configurações de modo que você possa ser produtivo. O cogerenciamento resolve esse problema de provisionamento de dispositivos com o Windows Autopilot.

O Autopilot fornece uma experiência simplificada para você e seus usuários nas seguintes situações:
- Configurar e pré-configurar novos dispositivos Windows 10  
- Redefinir, reciclar e recuperar dispositivos existentes  

O Autopilot reduz o tempo, os recursos e a complexidade associados à implantação, ao gerenciamento e à desativação de dispositivos. Ao mesmo tempo, a experiência para seus usuários é simplificada e fácil desde a primeira inicialização.

O Windows Autopilot oferece suporte a vários cenários, todos maximizados com o cogerenciamento:

- Os usuários podem trazer suas próprias implantações de novos dispositivos ao Active Directory com o ingresso no Azure AD híbrido ou no Azure Active Directory (Azure AD)  

- É possível configurar a autoimplantação de novas implantações de dispositivo no Azure AD para dispositivos compartilhados e quiosques  

- Com o Windows Autopilot para dispositivos existentes, use o Configuration Manager para migrar um dispositivo do Windows 7 e do Active Directory para o Windows 10 e o Azure AD  

No vídeo a seguir, o gerente de programas sênior Danny Guillory e o gerente de programas principal Andrew McMurray discutem e demonstram o Windows Autopilot com o cogerenciamento:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Windows-Autopilot-with-Co-Management/player]



## <a name="benefits"></a>Benefícios

Quando você usa o cogerenciamento e o Autopilot juntos, garante que novos dispositivos que entram em sua rede acabem no mesmo estado de gerenciamento. Nessa configuração, os dispositivos estão inscritos no Intune e têm um cliente do Configuration Manager.  Ele permite usar o novo modelo de provisionamento do Windows 10 e ajuda a eliminar a necessidade de criar, manter e atualizar imagens do sistema operacional personalizadas. 

Em todos esses cenários, você pode [habilitar o cogerenciamento](/sccm/comanage/how-to-prepare-win10) automaticamente pelo Intune. Essa automação ajuda no processo de provisionamento e no gerenciamento contínuo do dispositivo.

Com o Autopilot, você não precisa se preocupar com drivers e imagens. Concentre-se no provisionamento de dispositivos por esse processo automatizado usando o Intune e o Configuration Manager com cogerenciamento.


Veja como o uso do cogerenciamento e do Autopilot juntos pode ajudar você agora mesmo:

#### <a name="reduce-time-costs-and-complexity"></a>Reduzir tempo, custos e complexidade
O Windows Autopilot usa a versão otimizada para OEM do Windows 10 pré-instalada no dispositivo. Essa configuração poupa as organizações do esforço de ter que fazer a manutenção de imagens personalizadas e drivers para cada modelo de dispositivo em uso. Em vez de refazer a imagem do dispositivo, transforme a instalação existente do Windows 10 em um estado “pronto para os negócios”. Ele aplica as configurações e políticas, instala aplicativos e altera a edição do Windows 10. Por exemplo, a atualização do Windows 10 Pro para Windows 10 Enterprise para que você possa ter recursos avançados.

#### <a name="improve-the-user-experience"></a>Melhorar a experiência do usuário
Uma experiência melhor para os usuários causa menos interrupções e os ajuda a se concentrar no trabalho. O Windows Autopilot oferece uma abordagem simples para ajudar os usuários a fazerem a configuração rapidamente, com apenas alguns cliques e suas credenciais do Azure AD. Muitas organizações com um número grande de funcionários remotos podem usar o Autopilot do Windows para enviar novos dispositivos diretamente do fabricante.

#### <a name="use-autopilot-and-configuration-manager-to-migrate-existing-windows-7-devices-to-windows-10"></a>Usar o Autopilot e o Configuration Manager para migrar os dispositivos existentes do Windows 7 para Windows 10
Com o Windows Autopilot para dispositivos existentes, você cria um arquivo de configuração e implanta-o com uma sequência de tarefas do Configuration Manager. Esse processo migra facilmente os dispositivos existentes do Windows 7 para Windows 10. Use uma imagem característica do Windows 10 no Configuration Manager e, em seguida, aplique-a no dispositivo Windows 7 com a configuração do Autopilot. Quando o usuário inicia o dispositivo, utiliza o processo de integração controlada pelo usuário do Autopilot.

Estas são as etapas do Autopilot para dispositivos existentes:

![Visão geral do processo do Windows Autopilot para dispositivos existentes](media/autopilot-for-existing-devices.png)

1. Implantar política de grupo para redirecionar pastas conhecidas para o OneDrive
2. Gerar arquivo de configuração do Autopilot
3. Implantar a sequência de tarefas para atualizar para o Windows 10
4. Computador com Windows 10 é submetido ao Autopilot na primeira inicialização

#### <a name="modernizing-device-provisioning-for-all-types-of-workers"></a>Modernizar o provisionamento de dispositivos para todos os tipos de funcionários
Com o Autopilot, agora é possível fornecer uma implantação de sistema operacional não assistida para dispositivos automatizados ou dispositivos compartilhados usando o modo de autoimplantação. Essa configuração atende às necessidades de diferentes tipos de funcionários. Além disso, a função Reiniciar do Windows Autopilot garante que o reprovisionamento de um dispositivo para um novo usuário seja simples e fácil. Esse processo simplifica o que sempre foi uma tarefa difícil quando você tem funcionários sazonais ou contratados. 



## <a name="case-study"></a>Estudo de caso

A empresa alemã de logística e transporte ferroviário DB Schenker usa o Autopilot para aumentar a produtividade dos funcionários e liberar suas equipes de TI das tarefas diárias de suporte. A Shenker deixou de lado a imagem tradicional e a substituiu pelo provisionamento por nuvem. Agora eles usam o ingresso no Azure AD e o Intune para colocar novos dispositivos em funcionamento rapidamente. 

Ao invés de fazer seus funcionários remotos perderem tempo com viagens para um local com serviços de TI, a Shenker agora usa o Windows Autopilot. Eles enviam hardware aos funcionários diretamente do fabricante para o escritório de campo local. O funcionário conecta o novo dispositivo à Internet e entra com suas credenciais do Azure AD. O dispositivo se conecta aos aplicativos e serviços que o departamento de TI da Schenker atribui ao perfil individual do usuário.

Para saber mais, confira [Empresa de logística global centraliza a TI, unindo os funcionários com o local de trabalho digital moderno](https://customers.microsoft.com/story/db-schenker-travel-transportation-windows-10).



## <a name="value-proposition"></a>Proposta de valor

Crie satisfação em sua empresa proporcionando uma experiência melhor para seus usuários. Use o Windows Autopilot para diminuir os custos. Libere seu tempo para se concentrar em outros projetos, a fim de gerar mais valor e impacto para sua organização.



## <a name="configure"></a>Configurar

Para obter mais informações, confira os seguintes artigos:

[Usar o Intune para criar perfis do Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot)

Sequência de tarefas do [Windows Autopilot para dispositivos existentes](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices)

