---
title: Windows Autopilot com cogerenciamento
titleSuffix: Configuration Manager
description: Use o Windows Autopilot com cogerenciamento no Configuration Manager para simplificar o conjunto de backup de novos dispositivos Windows 10.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e3e3c97f-5945-49ab-a622-9f6fe6b9737e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4c9867b7ea59b435bd1fd344dd0bf4aa67a2be21
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754562"
---
# <a name="windows-autopilot-with-co-management"></a>Windows Autopilot com cogerenciamento

Receber um novo dispositivo Windows 10 é empolgante. No entanto, pode levar tempo para configurar todos os seus aplicativos e configurações de modo que você possa ser produtivo. Cogerenciamento resolve esse problema com o Windows Autopilot de provisionamento de dispositivos.

Piloto automático fornece uma experiência simplificada para você e seus usuários nas seguintes situações:
- Configurar e pré-configurar novos dispositivos Windows 10  
- Redefinir, reciclar e recuperar os dispositivos existentes  

Piloto automático reduz o tempo, recursos e complexidade associada à implantação, gerenciamento e desativar dispositivos. Ao mesmo tempo, a experiência para seus usuários é simplificada e fácil da primeira inicialização.

Windows Autopilot dá suporte a vários cenários, todos os quais são maximizados com cogerenciamento:

- Os usuários podem trazer suas próprias implantações de novos dispositivos ao Active Directory com o ingresso no Azure AD híbrido ou o Azure Active Directory (AD do Azure)  

- Você pode configurar a implantação automática de novas implantações de dispositivo ao Azure AD para dispositivos compartilhados e quiosques  

- Com o Windows Autopilot para dispositivos existentes, use o Configuration Manager para migrar um dispositivo existente do Windows 7 e o Active Directory para Windows 10 e o Azure AD  

No vídeo a seguir, Danny Guillory do gerente de programa sênior e gerente de programa principal Andrew McMurray abordam em demonstração do Windows Autopilot com cogerenciamento:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Windows-Autopilot-with-Co-Management/player]



## <a name="benefits"></a>Benefícios

Quando você usa o cogerenciamento e Autopilot juntos, você certifique-se de que novos dispositivos entrar em sua rede acabam no mesmo estado de gerenciamento. Nessa configuração, os dispositivos estão registrados no Intune e têm um cliente do Configuration Manager.  Ele permite que você use o novo modelo de provisionamento do Windows 10 e ajuda a eliminar a necessidade de criar, manter e atualizar as imagens do sistema operacional personalizadas. 

Em todos esses cenários, você pode automaticamente [habilitar o cogerenciamento](/sccm/comanage/how-to-prepare-win10) pelo Intune. Essa automação ajuda com o processo de provisionamento e para o gerenciamento contínuo do dispositivo.

Com o Autopilot, você não precisa se preocupar sobre drivers e imagens. Concentre-se sobre o provisionamento de dispositivos por esse processo automatizado usando o Intune e Configuration Manager por meio de cogerenciamento.


Eis aqui como usar o cogerenciamento e Autopilot juntos pode ajudar você no momento:

#### <a name="reduce-time-costs-and-complexity"></a>Reduzir tempo, os custos e complexidade
Windows Autopilot usa a versão otimizada de OEM do Windows 10 é pré-instalado no dispositivo. Essa configuração salva as organizações o esforço de manutenção de imagens personalizadas e os drivers para cada modelo do dispositivo em uso. Em vez de refazer a imagem do dispositivo, transforme a instalação existente do Windows 10 em um estado "pronto para os negócios". Ele aplica as configurações e políticas, instala aplicativos e altera a edição do Windows 10. Por exemplo, atualização do Windows 10 Pro para Windows 10 Enterprise para que você pode dar suporte a recursos avançados.

#### <a name="improve-the-user-experience"></a>Melhorar a experiência do usuário
A melhor experiência de usuário faz com que o mínimo de interrupções e ajuda a voltar a se concentrar em seu trabalho. Windows Autopilot oferece uma abordagem simples para ajudar os usuários a configurar rapidamente com apenas alguns cliques e suas credenciais do AD do Azure. Para muitas organizações com um campo grande de funcionários remotos, use o Windows Autopilot para novos dispositivos são enviados diretamente do fabricante.

#### <a name="use-autopilot-and-configuration-manager-to-migrate-existing-windows-7-devices-to-windows-10"></a>Usar o Autopilot e o Configuration Manager para migrar os dispositivos existentes do Windows 7 para Windows 10
Com o Windows Autopilot para dispositivos existentes, você cria um arquivo de configuração e implantá-lo com uma sequência de tarefas do Configuration Manager. Esse processo migra facilmente os dispositivos existentes do Windows 7 para Windows 10. Você usa uma imagem de assinatura Windows 10 no Configuration Manager e, em seguida, aplicá-lo para o dispositivo do Windows 7 existente com a configuração de piloto automático. Quando o usuário inicia o dispositivo, eles usam o processo de integração controlada pelo usuário do Autopilot.

Aqui estão as etapas de piloto automático para dispositivos existentes:

![Visão geral do processo para o Windows Autopilot para dispositivos existentes](media/autopilot-for-existing-devices.png)

1. Implantar política de grupo para redirecionar pastas conhecidas para o OneDrive
2. Gerar arquivo de configuração do Autopilot
3. Implantar a sequência de tarefas para atualizar para o Windows 10
4. Computador com Windows 10 percorre Autopilot na primeira inicialização

#### <a name="modernizing-device-provisioning-for-all-types-of-workers"></a>Modernizando o provisionamento do dispositivo para todos os tipos de trabalhos
Com o Autopilot, agora você pode fornecer uma implantação de sistema operacional viva-voz unmanned de dispositivos ou dispositivos compartilhados usando o modo de implantação automática. Essa configuração atende às necessidades de todos os tipos diferentes de trabalhadores. Além disso, a função Reset do Windows Autopilot torna-se de que o reprovisionamento de um dispositivo a um novo usuário é simples e fácil. Esse processo simplifica o que sempre foi uma tarefa difícil quando você tem sazonais ou contrato de trabalhadores. 



## <a name="case-study"></a>Estudo de caso

A empresa de frete rail e logística alemão Shenker DB usa o Autopilot para aumentar a produtividade dos funcionários e liberar suas equipes de TI trabalhar nas tarefas diárias de suporte. Shenker foi movido para fora de geração de imagens tradicional e substituímos por provisionamento por meio da nuvem. Agora que usar o Azure AD – join e o Intune para que novos dispositivos em funcionamento rapidamente. 

Em vez de ter seu tempo de resíduos de trabalhadores remotos viajar para um local com serviços de TI, Shenker agora usa o Windows Autopilot. Eles são fornecidos seu hardware de trabalhadores diretamente do fabricante para seu escritório local. O trabalhador conecta o novo dispositivo à internet e entram com suas credenciais do AD do Azure. O dispositivo, em seguida, conecta-se aos aplicativos e serviços que Schenker atribui do departamento de TI para o perfil do usuário individual.

Para obter mais informações, consulte [centraliza a firma de logística Global IT, une os funcionários com o espaço de trabalho digital modernos](https://customers.microsoft.com/story/db-schenker-travel-transportation-windows-10).



## <a name="value-proposition"></a>Proposta de valor

Crie satisfação em sua organização, criando uma melhor experiência de usuário para seus usuários. Use o Windows Autopilot para reduzir os custos. Libere tempo para se concentrar em outros projetos para direcionar mais valor e o impacto para sua organização.



## <a name="configure"></a>Configurar

Para obter mais informações, consulte [dispositivos do Windows registrar no Intune usando o Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot).

