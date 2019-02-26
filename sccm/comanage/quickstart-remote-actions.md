---
title: Ações remotas com o cogerenciamento
titleSuffix: Configuration Manager
description: Executar ações remotas do Intune para dispositivos cogerenciados
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4a877bed-f6c4-4048-9421-507dc848af5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4439aa280edaffbb59f8d49ece58e067a729ec91
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754575"
---
# <a name="remote-actions-with-co-management"></a>Ações remotas com o cogerenciamento

Você precisará certificar-se de que todos os dispositivos gerenciados é acessível, independentemente de onde ele está, sempre que ele se conecta. Você também precisará fornecer a cada usuário com tudo o que eles precisam para se manterem produtivos, protegendo os aplicativos e dados. Com as ações de dispositivo com suporte do Intune, você pode resolver remotamente essas funções críticas.

No vídeo a seguir, gerente de programa principal Heidi Cheng e gerente de programa sênior Danny Guillory discutem e ações remotas com cogerenciamento de demonstração:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Co-Management-to-Execute-Remote-Actions/player]



## <a name="benefits"></a>Benefícios

Ações de dispositivo remoto lhe oferece controles de gerenciamento no dispositivo sem interferir nos dados pessoais. Essas ações de dispositivo remoto permite que você: 
- Excluir dados da empresa em dispositivos perdidos ou roubados  
- Renomear um dispositivo  
- Reiniciar um dispositivo  
- Inventário de dispositivo de revisão  
- Controlar remotamente um dispositivo  
- Apagar aplicativos OEM pré-instalados com uma reinicialização novo início  
- Fazer uma redefinição de fábrica em qualquer dispositivo Windows 10  

Essas funções são uma maneira simple e importante para proteger dados corporativos nesses dispositivos, no email ou OneDrive.

Para obter mais informações sobre essas ações, consulte [ações remotas disponíveis](#available-remote-actions). 



## <a name="case-studies"></a>Estudos de caso

A empresa de consultoria global Avanade regularmente usa ações remotas para gerenciar os dispositivos usados pelos seus 30.000 funcionários. Em um [postagem de blog recentes](https://www.microsoft.com/microsoft-365/blog/2018/02/07/the-future-is-on-the-other-side-of-this-bridge/), CIO da Avanade observado:

> *Nosso win imediata de ter a funcionalidade do Intune foi a capacidade de redefinir remotamente o Windows em um computador. Isso é importante para nós de computadores perdidos ou roubados, que é mais comum em nossa força de trabalho altamente móvel. * 
>  *Essa é uma funcionalidade que, caso contrário, teríamos que para criar e manter em um pacote personalizado do ConfigMgr.*

Para obter mais informações sobre como usar essas ações remotas, consulte [ações do dispositivo disponíveis](https://docs.microsoft.com/intune/device-management#available-device-actions).


## <a name="value-proposition"></a>Proposta de valor

Quando um dispositivo do Configuration Manager está gerenciado em conjunto, ele adiciona imediatamente dessas funções que o Configuration Manager não tem nativamente. Agora você agora pode realizar qualquer ação remota que tem suporte pelo Intune. 

Com o cogerenciamento, os dispositivos do Configuration Manager agora estão assim como qualquer outro dispositivo gerenciado pelo Intune. Por exemplo, eles têm uma presença completa na nuvem, e você pode contatá-los, desde que eles têm acesso à internet. Você pode fazer todas essas ações sem realizar nenhuma etapa adicional além de permitir o cogerenciamento.

Como o processo de inscrição automática é transparente para o usuário, não há nenhum impacto sobre a produtividade. O usuário não precisa fazer nada.


### <a name="available-remote-actions"></a>Ações remotas disponíveis

Use essas ações remotas do Intune depois que você [habilitar o cogerenciamento](/sccm/comanage/how-to-enable) no Configuration Manager.

#### <a name="remove-devices"></a>Remover dispositivos
- **Desativar**: Esta ação remove dados e aplicativos gerenciados (quando aplicável), configurações e email perfis que foram atribuídos a esse dispositivo. Em seguida, o dispositivo é removido do gerenciamento do Intune. Esse processo acontece a próxima ação de desativação do tempo o dispositivo fizer check-in e receba o computador remoto. A função desativar deixa os dados pessoais do usuário no dispositivo.  

- **Apagar**: Essa ação restaura um dispositivo para as configurações padrão de fábrica. Se você escolher a opção de **manter o registro de conta de usuário e o estado**, em seguida, os dados de usuário são mantidos. Caso contrário, a unidade é apagada com segurança.  

- **Delete**: Se você quiser remover dispositivos do Intune no portal do Azure, excluí-los a partir do painel de dispositivo específico. Na próxima vez que o dispositivo fizer check-in, ele remove quaisquer dados organizacionais armazenados nele.  

Para obter mais informações, consulte [remover dispositivos usando o apagamento, desativação ou cancelando o registro do dispositivo manualmente](https://docs.microsoft.com/intune/devices-wipe).

#### <a name="selective-wipe"></a>Limpeza seletiva
<!--SCCMDocs issue 973--> Quando você escolhe um **apagamento seletivo do aplicativo**, ele remove os dados de aplicativo da empresa sem remover dados pessoais. Use essa ação quando um dispositivo é relatado como perdido ou roubado. 

Para obter mais informações, consulte [como apagar apenas dados corporativos dos aplicativos gerenciados pelo Intune](https://docs.microsoft.com/intune/apps-selective-wipe).

#### <a name="sync"></a>sincronização
O **sincronização** ação de dispositivo força o dispositivo selecionado a fazer check-in no Intune imediatamente. Quando um dispositivo faz check-in, ele recebe imediatamente as ações pendentes ou políticas que você atribuiu a ele.

Esse recurso pode ajudar a validar imediatamente e solucionar problemas de políticas que você atribuiu, sem aguardar o próximo check-in agendado.

Para obter mais informações, consulte [sincronizar dispositivos para obter as últimas políticas e ações com o Intune](https://docs.microsoft.com/intune/device-sync).

#### <a name="restart"></a>Reiniciar
O **reiniciar** ação do dispositivo faz com que o dispositivo que você optar por reiniciar. Essa ação é útil quando há uma reinicialização pendente, mas o usuário não está disponível para fazê-lo.

Para obter mais informações, consulte [reiniciar dispositivos remotamente com o Intune](https://docs.microsoft.com/intune/device-restart).

#### <a name="fresh-start"></a>Começar do zero
O **novo início** ação do dispositivo remove todos os aplicativos instalados em um dispositivo executando o Windows 10, versão 1703 ou posterior. Novo início ajuda a remover aplicativos (OEM) pré-instalados que normalmente são instalados com um novo dispositivo.

Se você optar por não manter os dados de usuário, o dispositivo restaura para seu estado de out-of-box. Ele cancela o registro do Azure AD e o MDM.

Se você tiver predeterminados padrões sobre quais aplicativos devem ser no dispositivo, essa ação elimina aqueles que não atendem aos seus critérios.

Para obter mais informações, consulte [Use novo início para redefinir dispositivos Windows 10 com o Intune](https://docs.microsoft.com/intune/device-fresh-start). 

#### <a name="remote-control"></a>Controle remoto
Dispositivos gerenciados pelo Intune podem ser administrados remotamente usando o [TeamViewer](https://www.teamviewer.com/). O TeamViewer é um programa de terceiros que você adquira separadamente.

Para obter mais informações, consulte [usar o TeamViewer para administrar remotamente os dispositivos do Intune](https://docs.microsoft.com/intune/device-profile-android-teamviewer). 



## <a name="configure"></a>Configurar

Diferente de controle remoto por meio do TeamViewer, para começar a usar essas ações remotas de dispositivo no Intune, nenhuma configuração adicional é necessária depois que você [habilitar o cogerenciamento](/sccm/comanage/how-to-enable).

Para obter mais informações sobre como usar o TeamViewer para o controle remoto, consulte [usar o TeamViewer para administrar remotamente os dispositivos do Intune](https://docs.microsoft.com/intune/device-profile-android-teamviewer). 

