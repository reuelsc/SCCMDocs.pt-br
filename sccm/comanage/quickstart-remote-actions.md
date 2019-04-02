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
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754575"
---
# <a name="remote-actions-with-co-management"></a>Ações remotas com o cogerenciamento

Você precisa se certificar de que todos os dispositivos gerenciados estejam acessíveis, independentemente de onde estejam, sempre que se conectem. Você também precisa fornecer a cada usuário tudo o que eles precisam para se manterem produtivos, protegendo os aplicativos e dados. Com as ações de dispositivo compatíveis com Intune, é possível resolver remotamente essas funções críticas.

No vídeo a seguir, a gerente de programas principal Heidi Cheng e o gerente de programas sênior Danny Guillory discutem e demonstram ações remotas com o cogerenciamento:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Co-Management-to-Execute-Remote-Actions/player]



## <a name="benefits"></a>Benefícios

As ações de dispositivo remoto oferecem controles de gerenciamento no dispositivo sem interferir nos dados pessoais. Essas ações de dispositivo remoto permitem: 
- Excluir dados da empresa em dispositivos perdidos ou roubados  
- Renomear um dispositivo  
- Reiniciar um dispositivo  
- Examinar o inventário de dispositivo  
- Controlar um dispositivo remotamente  
- Apagar aplicativos OEM pré-instalados com uma reinicialização Novo início  
- Fazer uma redefinição de fábrica em qualquer dispositivo Windows 10  

Essas funções são uma maneira simples e importante de proteger dados corporativos nesses dispositivos, no email ou no OneDrive.

Para saber mais sobre essas ações, confira [Ações remotas disponíveis](#available-remote-actions). 



## <a name="case-studies"></a>Estudos de caso

A empresa de consultoria global Avanade usa regularmente as ações remotas para gerenciar os dispositivos usados pelos seus 30.000 funcionários. Em uma [postagem recente no blog](https://www.microsoft.com/microsoft-365/blog/2018/02/07/the-future-is-on-the-other-side-of-this-bridge/), o CIO da Avanade fez esta observação:

> *Nosso benefício imediato de ter a funcionalidade do Intune foi a capacidade de redefinir remotamente o Windows em um computador. Isso é importante para nós em relação a computadores perdidos ou roubados, o que é mais comum em nossa força de trabalho altamente móvel.*
> *Essa é uma funcionalidade que, de outra forma, seria criada e mantida em um pacote personalizado do ConfigMgr.*

Para saber mais sobre como usar essas ações remotas, confira [Ações do dispositivo disponíveis](https://docs.microsoft.com/intune/device-management#available-device-actions).


## <a name="value-proposition"></a>Proposta de valor

Quando um dispositivo do Configuration Manager é cogerenciado, ele adiciona imediatamente essas funções que o Configuration Manager não tem nativamente. Agora você agora pode realizar qualquer ação remota compatível com o Intune. 

Com o cogerenciamento, os dispositivos do Configuration Manager agora são como qualquer outro dispositivo gerenciado pelo Intune. Por exemplo, eles têm uma presença completa na nuvem, e você pode entrar em contato com eles desde que tenham acesso à Internet. É possível realizar todas essas ações sem seguir nenhuma etapa adicional além da permissão do cogerenciamento.

Como o processo de inscrição automática é transparente para o usuário, não há nenhum impacto sobre a produtividade. O usuário não precisa executar nenhuma ação.


### <a name="available-remote-actions"></a>Ações remotas disponíveis

Use essas ações remotas do Intune depois de [habilitar o cogerenciamento](/sccm/comanage/how-to-enable) no Configuration Manager.

#### <a name="remove-devices"></a>Remover dispositivos
- **Desativar**: essa ação remove dados e aplicativos gerenciados (quando aplicável), configurações e perfis de email atribuídos a esse dispositivo. O dispositivo é removido do gerenciamento do Intune. Esse processo ocorre na próxima vez em que o dispositivo faz check-in e recebe a ação remota de desativação. A função Desativar deixa os dados pessoais do usuário no dispositivo.  

- **Apagar**: essa ação restaura um dispositivo para as configurações padrão de fábrica. Se você escolher a opção **Manter o estado do registro e a conta de usuário**, os dados de usuário são mantidos. Caso contrário, a unidade é apagada com segurança.  

- **Excluir**: Se você quiser remover dispositivos do Intune no portal do Azure, exclua-os pelo painel de dispositivo específico. Na próxima vez que o dispositivo fizer check-in, ele removerá os dados organizacionais armazenados nele.  

Para saber mais, confira [Remover dispositivos usando as ações para apagar, desativar ou cancelar o registro do dispositivo manualmente](https://docs.microsoft.com/intune/devices-wipe).

#### <a name="selective-wipe"></a>Limpeza seletiva
<!--SCCMDocs issue 973-->
Quando você escolhe uma **Limpeza seletiva de aplicativo**, ela remove os dados corporativos de aplicativos sem remover dados pessoais. Use essa ação quando um dispositivo for relatado como perdido ou roubado. 

Para saber mais, confira [Como apagar apenas dados corporativos dos aplicativos gerenciados pelo Intune](https://docs.microsoft.com/intune/apps-selective-wipe).

#### <a name="sync"></a>Sincronizar
A ação de dispositivo **Sincronizar** força o dispositivo selecionado a fazer check-in no Intune imediatamente. Quando um dispositivo faz check-in, ele recebe imediatamente as ações ou políticas pendentes atribuídas a ele.

Esse recurso pode ajudá-lo a validar e a solucionar problemas das políticas que você atribuiu, imediatamente, sem precisar esperar o próximo check-in agendado.

Para saber mais, confira [Sincronizar dispositivos com o Intune para obter as políticas e ações mais recentes](https://docs.microsoft.com/intune/device-sync).

#### <a name="restart"></a>Reiniciar
A ação de dispositivo **Reiniciar** faz com que o dispositivo escolhido seja reiniciado. Essa ação é útil quando há uma reinicialização pendente, mas o usuário não está disponível para fazê-la.

Para saber mais, confira [Reiniciar dispositivos remotamente com o Intune](https://docs.microsoft.com/intune/device-restart).

#### <a name="fresh-start"></a>Novo início
A ação de dispositivo **Novo início** remove os aplicativos instalados em um dispositivo que executa Windows 10, versão 1703 ou posterior. O Novo início ajuda a remover aplicativos OEM pré-instalados que normalmente são instalados com um novo dispositivo.

Se você optar por não manter os dados de usuário, o dispositivo será restaurado para seu estado original. Isso cancela o registro no Azure AD e no MDM.

Se você tiver padrões predeterminados sobre quais aplicativos devem estar no dispositivo, essa ação eliminará aqueles que não atendam aos seus critérios.

Para saber mais, confira [Usar o Novo início para redefinir dispositivos Windows 10 com o Intune](https://docs.microsoft.com/intune/device-fresh-start). 

#### <a name="remote-control"></a>Controle remoto
Os dispositivos gerenciados pelo Intune podem ser administrados remotamente usando o [TeamViewer](https://www.teamviewer.com/). O TeamViewer é um programa de terceiros que você adquire separadamente.

Para saber mais, confira [Usar o TeamViewer para administrar remotamente os dispositivos do Intune](https://docs.microsoft.com/intune/device-profile-android-teamviewer). 



## <a name="configure"></a>Configurar

Além do controle remoto via TeamViewer, para começar a usar essas ações remotas de dispositivos no Intune, nenhuma configuração adicional é necessária após você [habilitar o cogerenciamento](/sccm/comanage/how-to-enable).

Para saber mais sobre como usar o TeamViewer para controle remoto, confira [Usar o TeamViewer para administrar remotamente os dispositivos do Intune](https://docs.microsoft.com/intune/device-profile-android-teamviewer). 

