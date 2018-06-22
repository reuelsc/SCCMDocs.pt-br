---
title: Gerenciar pacotes de atualização de sistema operacional
titleSuffix: Configuration Manager
description: Saiba como gerenciar pacotes de atualização do sistema operacional com o System Center Configuration Manager.
ms.date: 12/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e323fa8df7d8ae88d6526a5d1777ceb8fa27c2de
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32353140"
---
# <a name="manage-operating-system-upgrade-packages-with-system-center-configuration-manager"></a>Gerenciar pacotes de atualização do sistema operacional com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Um pacote de atualização no System Center Configuration Manager contém os arquivos de origem da Instalação do Windows que são usados para atualizar um sistema operacional existente em um computador. Use as seções a seguir para gerenciar pacotes de atualização do sistema operacional no Configuration Manager.

##  <a name="BKMK_AddOSUpgradePkgs"></a> Adicionar pacotes de atualização do sistema operacional no Gerenciador de Configurações  
 Antes de usar um pacote de atualização do sistema operacional, você deve adicionar o pacote a um site do Configuration Manager. Use o procedimento a seguir para adicionar um pacote de atualização do sistema operacional a um site.  

#### <a name="to-add-an-operating-system-upgrade-package"></a>Para adicionar um pacote de atualização do sistema operacional  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Pacotes de atualização do Sistema Operacional**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Adicionar Pacote de Atualização do Sistema Operacional** para iniciar o Assistente para Adicionar Atualização do Sistema Operacional.  

4.  Na página **Fonte de Dados** , especifique o caminho de rede dos arquivos de origem de instalação do pacote de atualização do sistema operacional. Por exemplo, especifique o UNC **\\\server\path** em que os arquivos de origem de instalação estão localizados.  

    > [!NOTE]  
    >  Os arquivos de origem de instalação contêm Setup.exe e outros arquivos e pastas para instalar o sistema operacional.  

    > [!IMPORTANT]  
    >  Limite o acesso aos arquivos de origem da instalação para impedir violações indesejadas.  

5.  Na página **Geral** , especifique as seguintes informações e clique em **Próximo**. Essa informação é útil para fins de identificação quando você adiciona vários instaladores do sistema operacional.  

    -   **Nome**: Especifique o nome do instalador do sistema operacional.  

    -   **Versão**: Especifique a versão do instalador do sistema operacional.  

    -   **Comentário**: Especifique uma breve descrição do instalador do sistema operacional.  

6.  Conclua o assistente.  

 Agora você pode distribuir um instalador do sistema operacional para os pontos de distribuição que são acessados pelas sequências de tarefas de implantação.  

##  <a name="BKMK_DistributeBootImages"></a> Distribuir imagens do sistema operacional para um ponto de distribuição  
 Imagens do sistema operacional são distribuídas para os pontos de distribuição da mesma forma que outros conteúdos são distribuídos. Na maioria dos casos, você deve distribuir a imagem do sistema operacional para pelo menos um ponto de distribuição antes de implantar o sistema operacional. Para as etapas para distribuir uma imagem do sistema operacional, consulte [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

##  <a name="BKMK_OSUpgradePkgApplyUpdates"></a> Aplicar atualizações de software a um pacote de atualização do sistema operacional  
 A partir do Configuration Manager versão 1602, você pode aplicar novas atualizações de software à imagem do sistema operacional em seu pacote de atualização do sistema operacional. Antes de aplicar as atualizações de software a um pacote de atualização, sua infraestrutura de atualizações de software deve estar em funcionamento, você deve ter sincronizado com êxito as atualizações de software e deve ter baixado as atualizações de software para a biblioteca de conteúdo no servidor do site. Para mais informações, consulte [Implantar atualizações de software](../../sum/deploy-use/deploy-software-updates.md).  

 Você pode aplicar as atualizações de software a um pacote de atualização em um agendamento especificado. No cronograma que você especificar, o Configuration Manager aplica as atualizações de software que você selecionar no pacote de atualização do sistema operacional e, opcionalmente, distribui o pacote de atualização atualizado para os pontos de distribuição. As informações sobre o pacote de atualização do sistema operacional são armazenadas no banco de dados do site, incluindo as atualizações de software que foram aplicadas no momento da importação. As atualizações de software que foram aplicadas ao pacote de atualização desde que ela foi inicialmente adicionada também são armazenadas no banco de dados do site. Ao iniciar o assistente para aplicar as atualizações de software ao pacote de atualização do sistema operacional, o assistente recupera uma lista de atualizações de software aplicáveis que ainda não foram aplicadas ao pacote de atualização para que você a selecione. O Configuration Manager copia as atualizações de software da biblioteca de conteúdo no servidor do site e aplica as atualizações de software ao pacote de atualização do sistema operacional.  

 Use o procedimento a seguir para aplicar as atualizações de software a um pacote de atualização do sistema operacional.  

#### <a name="to-apply-software-updates-to-an-operating-system-upgrade-package"></a>Para aplicar atualizações de software a um pacote de atualização do sistema operacional  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Pacotes de atualização do Sistema Operacional**.  

3.  Selecione o pacote de atualização do sistema operacional ao qual deseja aplicar as atualizações de software.  

4.  Na guia **Início** , no grupo **Pacotes de Atualização do Sistema Operacional** , clique em **Agendar Atualizações** para iniciar o assistente.  

5.  Na página **Escolher Atualizações** , especifique as seguintes atualizações de software para aplicar à imagem do sistema operacional e clique em **Próximo**.  

6.  Na página **Definir Agendamento** , especifique as seguintes configurações e clique em **Próximo**.  

    1.  **Agendamento**: especifique o agendamento para quando as atualizações de software devem ser aplicadas à imagem do sistema operacional.  

    2.  **Continuar se houver erro**: selecione essa opção para continuar a aplicar as atualizações de software à imagem em caso de erro.  

    3.  **Distribuir a imagem para os pontos de distribuição**: selecione essa opção para atualizar a imagem do sistema operacional nos pontos de distribuição após as atualizações de software serem aplicadas.  

7.  Na página **Resumo** , verifique as seguintes informações e clique em **Próximo**.  

8.  Na página **Conclusão** , verifique se as atualizações de software foram aplicadas com êxito à imagem do sistema operacional.  
