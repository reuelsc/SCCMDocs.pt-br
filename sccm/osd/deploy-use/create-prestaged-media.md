---
title: "Criar mídia pré-configurada"
titleSuffix: Configuration Manager
description: "Crie mídia em pré-teste no System Center Configuration Manager para simplificar a implantação do Windows em vários cenários."
ms.custom: na
ms.date: 04/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff6e7267-302a-4563-815e-cdc0d1a4b60f
caps.latest.revision: "12"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 4b10aab0674e4066b399c636ecf2226ae109260e
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="create-prestaged-media-with-system-center-configuration-manager"></a>Criar mídia pré-configurada com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A mídia pré-testada no System Center Configuration Manager é um arquivo em formato WIM (Windows Imaging) que pode ser instalado em um computador bare-metal pelo fabricante ou em um centro de preparo corporativo que não está conectado ao ambiente do Configuration Manager.  
A mídia em pré-teste contém a imagem de inicialização usada para iniciar o computador de destino e a imagem do sistema operacional aplicada ao computador de destino. Também é possível especificar aplicativos, pacotes e pacotes de driver para incluir como parte da mídia pré-configurada. A sequência de tarefas que implanta o sistema operacional não está incluída na mídia. A mídia pré-testada é aplicada à unidade de disco rígido de um novo computador antes do computador ser enviado ao usuário final. Use mídia pré-testada para os seguintes cenários de implantação de sistema operacional:  

-   [Criar uma imagem de um OEM na fábrica ou em um repositório local](../../osd/deploy-use/create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

-   [Instalar uma nova versão do Windows em um novo computador (sem sistema operacional)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Implantar o Windows to Go](deploy-windows-to-go.md)  

 Quando o computador é iniciado pela primeira vez depois de a mídia pré-configurada ter sido aplicada, o computador é iniciado com o Windows PE e conecta-se a um ponto de gerenciamento para localizar a sequência de tarefas que conclui o processo de implantação de sistema operacional. Você pode especificar aplicativos, pacotes e pacotes de driver para incluir como parte da mídia pré-testada. Quando você implanta uma sequência de tarefa que utiliza mídia pré-testada, o assistente verifica o cache de sequência de tarefas local quanto a conteúdo válido primeiro, e se o conteúdo não puder ser localizado ou não for revisado, o assistente baixa o conteúdo do ponto de distribuição.  

##  <a name="BKMK_CreatePrestagedMedia"></a> Como criar mídia em pré-teste  
 Antes de criar a mídia pré-testada usando o Assistente para Criar Mídia de Sequência de Tarefas, verifique se as seguintes condições foram atendidas:  

|Tarefa|Descrição|  
|----------|-----------------|  
|Imagem de inicialização|Considere o seguinte sobre a imagem de inicialização que você usará na sequência de tarefas para implantar o sistema operacional:<br /><br /> -   A arquitetura da imagem de inicialização deve ser apropriada para a arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode iniciar e executar uma imagem de inicialização x86 ou x64. No entanto, um computador de destino x86 pode iniciar e executar apenas uma imagem de inicialização x86.<br />-   Verifique se a imagem de inicialização contém os drivers de rede e armazenamento em massa necessários para provisionar o computador de destino.|  
|Criar uma sequência de tarefas para implantar um sistema operacional|Como parte da mídia pré-testada, você deve especificar a sequência de tarefas para implantar o sistema operacional.<br /><br /> -   Para ver as etapas para criar uma nova sequência de tarefas, consulte [Criar uma sequência de tarefas para instalar um sistema operacional](../../osd/deploy-use/create-a-task-sequence-to-install-an-operating-system.md).<br />-   Para obter mais informações sobre sequências de tarefas, consulte [Gerenciar sequências de tarefas para automatizar tarefas](../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md).|  
|Distribuir todo o conteúdo associado à sequência de tarefas|Você deve distribuir todo o conteúdo exigido pela sequência de tarefas para pelo menos um ponto de distribuição. Isso inclui a imagem de inicialização, a imagem do sistema operacional e outros arquivos associados. O assistente reúne as informações do ponto de distribuição quando ele cria a mídia autônoma. Você deve ter direitos de acesso de **Leitura** à biblioteca de conteúdo no ponto de distribuição.  Para obter detalhes, consulte [Sobre a biblioteca de conteúdo](../../core/plan-design/hierarchy/the-content-library.md).|  
|Disco rígido no computador de destino|O disco rígido do computador de destino deve ser formatado antes que a mídia pré-configurada seja preparada no disco rígido do computador. Se o disco rígido não estiver formatado quando a mídia for aplicada, a sequência de tarefas que implanta o sistema operacional falhará quando tentar iniciar o computador de destino.|  

> [!NOTE]  
>  O Assistente para Criar Mídia de Sequência de Tarefas define a seguinte condição de variável de sequência de tarefas na mídia: **_SMSTSMediaType = OEMMedia**. Você pode usar essa condição em toda a sequência de tarefas.  

 Use o procedimento a seguir para criar mídia em pré-teste.  

#### <a name="to-create-prestaged-media"></a>Para criar mídia em pré-teste  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Sequências de Tarefas**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Mídia de Sequência de Tarefas** para iniciar o Assistente para Criar Mídia de Sequência de Tarefas.  

4.  Na página **Selecionar o Tipo de Mídia** , especifique as informações a seguir e clique em **Próximo**.  

    -   Selecione **Mídia em pré-teste**.  

    -   Opcionalmente, se você quiser permitir que o sistema operacional seja implantado sem exigir a entrada do usuário, selecione **Permitir implantação autônoma do sistema operacional**. Quando você seleciona essa opção, o usuário não precisa inserir informações de configuração de rede nem sequências de tarefas opcionais. No entanto, ainda será solicitada ao usuário uma senha, se a mídia estiver configurada para proteção por senha.  

5.  Na página **Gerenciamento de Mídia** , especifique as informações a seguir e clique em **Próximo**.  

    -   Selecione **Mídia dinâmica** se quiser permitir que um ponto de gerenciamento redirecione a mídia para outro ponto de gerenciamento, baseado no local do cliente nos limites do site.  

    -   Selecione **Mídia de site** se quiser que a mídia tenha contato apenas com o ponto de gerenciamento especificado.  

6.  Na página **Propriedades de mídia**  , especifique as informações a seguir e clique em **Próximo**.  

    -   **Criado por**: especifique quem criou a mídia.  

    -   **Versão**: especifique o número de versão da mídia.  

    -   **Comentário**: especifique uma descrição exclusiva da finalidade da mídia.  

    -   **Arquivo de mídia**: especifique o nome e o caminho dos arquivos de saída. O assistente grava os arquivos de saída nesse local. Por exemplo: **\\\nomedoservidor\pasta\arquivodesaída.wim**  

7.  Na página **Segurança** , especifique as informações a seguir e clique em **Próximo**.  

    -   Marque a caixa de seleção **Habilitar suporte a computadores desconhecidos** para permitir que a mídia implante um sistema operacional em um computador não gerenciado pelo Configuration Manager. Não há registro desses computadores no banco de dados do Configuration Manager.  Para obter mais informações, consulte [Preparar implantações de computador desconhecido](../get-started/prepare-for-unknown-computer-deployments.md).  

    -   Marque a caixa de seleção **Proteger mídia com senha** e digite uma senha forte como auxílio para proteger a mídia contra o acesso não autorizado. Quando você especificar uma senha, o usuário deverá fornecer essa senha para usar a mídia em pré-teste.  

        > [!IMPORTANT]  
        >  Como prática recomendada de segurança, atribua sempre uma senha para ajudar a proteger a mídia em pré-teste.  

    -   Para comunicações HTTP, selecione **Criar certificado de mídia autoassinado**e especifique as datas de início e vencimento do certificado.  

    -   Para comunicações HTTPS, selecione **Importar certificado PKI**e especifique o certificado a ser importado e a respectiva senha.  

         Para obter mais informações sobre o certificado de cliente que é usado para imagens de inicialização, consulte [Requisitos do certificado PKI](../../core/plan-design/network/pki-certificate-requirements.md).  

    -   **Afinidade de Dispositivo de Usuário**: para dar suporte ao gerenciamento centrado no usuário no Configuration Manager, especifique como você quer que a mídia associe usuários ao computador de destino. Para obter mais informações sobre como a implantação de sistema operacional dá suporte à afinidade de dispositivo de usuário, consulte [Associar usuários a um computador de destino](../get-started/associate-users-with-a-destination-computer.md).  

        -   Especifique **Permitir afinidade de dispositivo de usuário com aprovação automática** se você quiser que a mídia associe automaticamente os usuários ao computador de destino. Essa funcionalidade é baseada nas ações da sequência de tarefas que implanta o sistema operacional. Nesse cenário, a sequência de tarefas cria uma relação entre os usuários especificados e o computador de destino quando implanta o sistema operacional no computador de destino.  

        -   Especifique **Permitir afinidade de dispositivo de usuário pendente de aprovação de administrador** se você quiser que a mídia associe os usuários ao computador de destino após a aprovação ser concedida. Essa funcionalidade é baseada no escopo da sequência de tarefas que implanta o sistema operacional. Neste cenário, a sequência de tarefas cria uma relação entre os usuários especificados e o computador de destino, mas aguarda a aprovação de um usuário administrativo antes da implantação do sistema operacional.  

        -   Especifique **Não permitir afinidade de dispositivo de usuário** se você quiser que a mídia associe os usuários ao computador de destino. Neste cenário, a sequência de tarefas não associa os usuários ao computador de destino quando implanta o sistema operacional.  

8.  Na página **Sequência de Tarefas** , especifique a sequência de tarefas que será executada no computador de destino. O conteúdo referenciado pela sequência de tarefas é exibido em **Esta sequência de tarefas faz referência ao seguinte conteúdo**. Verifique o conteúdo e clique em **Avançar**.  

9. Na página **Imagem de inicialização** , especifique as informações a seguir e clique em **Próximo**.  

    > [!IMPORTANT]  
    >  A arquitetura da imagem de inicialização distribuída deve ser apropriada para a arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode iniciar e executar uma imagem de inicialização x86 ou x64. No entanto, um computador de destino x86 pode iniciar e executar apenas uma imagem de inicialização x86.  

    -   Na caixa **Imagem de inicialização** , especifique a imagem de inicialização para iniciar o computador de destino. Para obter mais informações, consulte [Gerenciar imagens de inicialização](../get-started/manage-boot-images.md).  

    -   Na caixa **Ponto de distribuição** , especifique o ponto de distribuição onde a imagem de inicialização reside. O assistente recupera a imagem de inicialização do ponto de distribuição e a grava na mídia.  

        > [!NOTE]  
        >  É necessário ter direitos de acesso de **leitura** à biblioteca de conteúdo no ponto de distribuição. Para mais informações, consulte [Sobre a biblioteca de conteúdo](../../core/plan-design/hierarchy/the-content-library.md).  

    -   Se você selecionou **Mídia de site** na página **Gerenciamento de Mídia** do assistente, na caixa **Ponto de gerenciamento** , especifique um ponto de gerenciamento de um site primário.  

    -   Se você selecionou **Mídia dinâmica** na página **Gerenciamento de Mídia** do assistente, na caixa **Pontos de gerenciamento associados** , especifique os pontos de gerenciamento do site primário a ser usados e uma ordem de prioridade para a comunicação inicial.  

10. Na página **Imagens** , especifique as informações a seguir e clique em **Próximo**.  

    -   Na caixa **Pacote da imagem** , especifique a imagem do sistema operacional. Para obter mais informações, consulte [Gerenciar imagens do sistema operacional](../get-started/manage-operating-system-images.md).  

    -   Se o pacote contiver várias imagens de sistemas operacionais, na caixa **Índice de imagens** , especifique a imagem a ser implantada.  

    -   Na caixa **Ponto de distribuição** , especifique o ponto de distribuição onde o pacote da imagem do sistema operacional reside. O assistente recupera a imagem do sistema operacional do ponto de distribuição e a grava na mídia.  

11. Na página **Personalização** , especifique as informações a seguir e clique em **Próxima**.  

    -   Especifique as variáveis que a sequência de tarefas usa para implantar o sistema operacional.  

    -   Especifique os comandos prestart que deseja executar antes de executar a sequência de tarefas. Os comandos prestart são um script ou um executável que podem interagir com o usuário no Windows PE antes da execução da sequência de tarefas para instalar o sistema operacional. Para obter mais informações sobre comandos prestart para mídia, consulte [Comandos prestart para mídia de sequência de tarefas](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        >  Durante a criação de mídia de sequência de tarefas, a sequência de tarefas grava a ID do pacote e a linha de comando prestart, que inclui o valor de quaisquer variáveis de sequência de tarefas, no arquivo de log CreateTSMedia.log no computador que executa o console do Configuration Manager. Você poderá analisar esse arquivo de log para verificar o valor das variáveis de sequência de tarefas.  

12. Conclua o assistente.  

## <a name="next-steps"></a>Próximas etapas
[Cenários para implantar sistemas operacionais corporativos](scenarios-to-deploy-enterprise-operating-systems.md)
