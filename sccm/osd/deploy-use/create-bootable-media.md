---
title: Criar mídia inicializável
titleSuffix: Configuration Manager
description: Use uma mídia inicializável no Configuration Manager para instalar uma nova versão do Windows ou substituir um computador.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0b7a68dd6d0bdbc2fa043d552aba13562dc175fc
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65082955"
---
# <a name="create-bootable-media"></a>Criar mídia inicializável

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Mídias inicializáveis no Configuration Manager contém a imagem de inicialização, comandos prestart opcionais e arquivos associados, além dos arquivos do Configuration Manager. Use a mídia em pré-teste para os seguintes cenários de implantação de SO:  

- [Instalar uma nova versão do Windows em um novo computador (sem sistema operacional)](/sccm/osd/deploy-use/install-new-windows-version-new-computer-bare-metal)  

- [Substituir um computador existente e transferir configurações](/sccm/osd/deploy-use/replace-an-existing-computer-and-transfer-settings)  


## <a name="usage"></a>Uso

O processo a seguir ocorre quando você inicializa a mídia inicializável:

1. O computador de destino é iniciado
1. Ele se conecta à rede
1. Ele recupera o seguinte conteúdo do site:
    - A sequência de tarefas especificada
    - Imagem do sistema operacional
    - Qualquer outro conteúdo necessário

Como a sequência de tarefas não está na mídia, você pode alterar a sequência de tarefas ou o conteúdo sem ter que recriar a mídia.

Os pacotes em uma mídia inicializável não são criptografados. Para garantir que o conteúdo do pacote seja protegido contra usuários não autorizados, tome as medidas de segurança apropriadas. Por exemplo, adicione uma senha à mídia.

## <a name="prerequisites"></a>Pré-requisitos

Antes de criar uma mídia inicializável usando o Assistente para Criar Mídia de Sequência de Tarefas, verifique se todas essas condições foram atendidas.

### <a name="boot-image"></a>Imagem de inicialização

Considere os seguintes pontos sobre a imagem de inicialização usada na sequência de tarefas para implantar o SO:

- A arquitetura da imagem de inicialização deve ser apropriada para a arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode iniciar e executar uma imagem de inicialização x86 ou x64. No entanto, um computador de destino x86 pode iniciar e executar apenas uma imagem de inicialização x86.
- Certifique-se de que a imagem de inicialização contenha os drivers de rede e de armazenamento necessários para provisionar o computador de destino.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Criar uma sequência de tarefas para implantar um SO

Como parte da mídia inicializável, especifique a sequência de tarefas para implantar o SO. Para saber mais, confira [Criar uma sequência de tarefas para instalar um SO](/sccm/osd/deploy-use/create-a-task-sequence-to-install-an-operating-system).

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuir todo o conteúdo associado à sequência de tarefas

Distribua todo o conteúdo exigido pela sequência de tarefas para pelo menos um ponto de distribuição. Esse conteúdo inclui a imagem de inicialização e outros arquivos de pré-inicialização associados. O assistente reúne o conteúdo do ponto de distribuição ao criar a mídia inicializável.

Sua conta de usuário precisa pelo menos de direitos de acesso de **Leitura** à biblioteca de conteúdo nesse ponto de distribuição. Para obter mais informações, consulte [Distribuir conteúdo](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Preparar a unidade USB removível

Se estiver usando uma unidade USB removível, conecte-a ao computador em que você executa o Assistente para Criar Mídia de Sequência de Tarefas. A unidade USB deve ser detectável pelo Windows como um dispositivo de remoção. O assistente grava diretamente na unidade USB ao criar a mídia.

### <a name="create-an-output-folder"></a>Criar uma pasta de saída

Antes de executar o Assistente para Criar Mídia de Sequência de Tarefas para criar a mídia para um conjunto de CD ou DVD, crie uma pasta para os arquivos de saída que são gerados. A mídia criada para um conjunto de CD ou DVD é gravada como um arquivo .ISO diretamente na pasta.


## <a name="process"></a>Processar

1. No console do Configuration Manager, acesse o espaço de trabalho **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione o nó **Sequências de Tarefas**.  

2. Na guia **Início** da faixa de opções, no grupo **Criar**, selecione **Criar Mídia de Sequência de Tarefas**. Essa ação inicia o Assistente para Criar Mídia de Sequência de Tarefas.  

3. Na página **Selecionar o Tipo de Mídia**, especifique as seguintes opções:  

    - Selecione **Mídia inicializável**.  

    - Opcionalmente, se quiser permitir que o SO seja implantado sem exigir a entrada do usuário, selecione **Permitir implantação autônoma do sistema operacional**.  

        > [!IMPORTANT]  
        > Quando você seleciona essa opção, o usuário não recebe uma solicitação para fornecer informações de configuração da rede ou sequências de tarefas opcionais. Se você configurar a mídia para proteção por senha, o usuário ainda será solicitado a fornecer uma senha.  

4. Na página **Gerenciamento de Mídia**, especifique uma das seguintes opções:  

    - **Mídia dinâmica**: permite que um ponto de gerenciamento redirecione a mídia para outro ponto de gerenciamento, com base na localização do cliente nos limites do site.  

    - **Mídia de site**: a mídia contata apenas o ponto de gerenciamento especificado.  

5. Na página **Tipo de Mídia**, especifique se a mídia é uma **Unidade USB removível** ou um **Conjunto de CD/DVD**. Em seguida, configure as seguintes opções:  

    > [!IMPORTANT]  
    > A mídia usa um sistema de arquivos FAT32. Você não pode criar uma mídia em uma unidade USB cujo conteúdo inclua um arquivo com mais de 4 GB.  

    - Se você selecionar **Unidade USB removível**, selecione a unidade na qual deseja armazenar o conteúdo.  

        - **Formatar a unidade USB removível (FAT32) e torná-la inicializável**: por padrão, permita que o Configuration Manager prepare a unidade USB. Muitos dispositivos UEFI mais recentes requerem uma partição FAT32 inicializável. No entanto, esse formato também limita o tamanho dos arquivos e a capacidade geral da unidade. Se você já formatou e configurou a unidade de disco removível, desabilite essa opção.

    - Se você selecionar **Conjunto de CD/DVD**, especifique a capacidade da mídia (**Tamanho da mídia**) e o nome e o caminho do arquivo de saída (**Arquivo de mídia**). O assistente grava os arquivos de saída nesse local. Por exemplo: `\\servername\folder\outputfile.iso`  

        Se a capacidade da mídia for muito pequena para armazenar todo o conteúdo, ela criará vários arquivos. Portanto, você precisará armazenar o conteúdo em vários CDs ou DVDs. Quando vários arquivos de mídia são necessários, o Configuration Manager adiciona um número de sequência ao nome de cada arquivo de saída criado.  

        > [!IMPORTANT]  
        > Se você selecionar uma imagem .iso existente, o Assistente de Mídia de Sequência de Tarefas excluirá essa imagem da unidade ou do compartilhamento assim que você prosseguir para a próxima página do assistente. A imagem existente será excluída mesmo se você cancelar o assistente.  

    - **Pasta de preparo**<!--1359388-->: o processo de criação da mídia pode exigir muito espaço em disco temporário. Por padrão, essa localização é semelhante ao seguinte caminho: `%UserProfile%\AppData\Local\Temp`. A partir da versão 1902, para fornecer maior flexibilidade quando se trata de armazenar esses arquivos temporários, altere esse valor para outra unidade e caminho.  

    - **Rótulo de mídia**<!--1359388-->: a partir da versão 1902, adicione um rótulo à mídia de sequência de tarefas. Esse rótulo ajuda a identificar melhor a mídia depois de criá-la. O valor padrão é `Configuration Manager`. Esse campo de texto é exibido nos seguintes locais:  

        - Se você montar um arquivo ISO, o Windows exibirá esse rótulo como o nome da unidade montada  

        - Se você formatar uma unidade USB, ela usará os primeiro 11 caracteres do rótulo como seu nome  

        - O Configuration Manager grava um arquivo de texto chamado `MediaLabel.txt` na raiz da mídia. Por padrão, o arquivo inclui uma única linha de texto: `label=Configuration Manager`. Se você personalizar o rótulo de mídia, essa linha usará o rótulo personalizado, em vez do valor padrão.  

    - **Incluir arquivo autorun.inf na mídia**<!-- 4090666 -->: a partir da versão 1902, o Configuration Manager não adiciona um arquivo autorun.inf por padrão. Normalmente, esse arquivo é bloqueado por produtos antimalware. Para obter mais informações sobre o recurso AutoRun do Windows, confira [Creating an AutoRun-enabled CD-ROM Application](https://docs.microsoft.com/windows/desktop/shell/autoplay) (Criando um aplicativo de CD-ROM habilitado para AutoRun). Se ainda for necessário para o seu cenário, selecione essa opção para incluir o arquivo.  

6. Na página **Segurança**, especifique as seguintes opções:  

    - **Habilitar suporte a computadores desconhecidos**: permite que a mídia implante um SO em um computador que não seja gerenciado pelo Configuration Manager. Não há registro desses computadores no banco de dados do Configuration Manager. Para obter mais informações, consulte [Preparar implantações de computador desconhecido](/sccm/osd/get-started/prepare-for-unknown-computer-deployments).  

    - **Proteger mídia com senha**: insira uma senha forte para ajudar a proteger a mídia contra acesso não autorizado. Quando você especificar uma senha, o usuário deverá fornecer essa senha para usar a mídia inicializável.  

        > [!IMPORTANT]  
        > Como prática recomendada de segurança, atribua sempre uma senha para ajudar a proteger a mídia inicializável.  

    - Para comunicações HTTP, selecione **Criar certificado de mídia autoassinado**. Em seguida, especifique a data de início e de vencimento do certificado.  

    - Para comunicações HTTPS, selecione **Importar certificado PKI**. Em seguida, especifique o certificado a ser importado e sua senha.  

        Para saber mais sobre este certificado de cliente usado por imagens de inicialização, confira [Requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

    - **Afinidade de dispositivo de usuário**: para dar suporte ao gerenciamento voltado ao usuário no Configuration Manager, especifique como você deseja que a mídia associe usuários ao computador de destino. Para saber mais sobre como a implantação do SO dá suporte à afinidade de dispositivo de usuário, confira [Associar usuários a um computador de destino](/sccm/osd/get-started/associate-users-with-a-destination-computer).  

        - **Permitir afinidade de dispositivo de usuário com aprovação automática**: a mídia associa automaticamente os usuários ao computador de destino. Essa funcionalidade se baseia nas ações da sequência de tarefas que implanta o SO. Nesse cenário, a sequência de tarefas cria um relacionamento entre os usuários especificados e o computador de destino ao implantar o SO nesse computador.  

        - **Permitir afinidade de dispositivo de usuário pendente de aprovação de administrador**: a mídia associa os usuários ao computador de destino depois que uma aprovação é concedida. Essa funcionalidade se baseia no escopo da sequência de tarefas que implanta o SO. Nesse cenário, a sequência de tarefas cria um relacionamento entre os usuários especificados e o computador de destino, mas aguarda a aprovação de um usuário administrativo antes que o SO seja implantado.  

        - **Não permitir afinidade de dispositivo de usuário**: a mídia não associa usuários ao computador de destino. Nesse cenário, a sequência de tarefas não associa usuários ao computador de destino quando implanta o SO.  

7. Na página **Imagem de inicialização**, especifique as seguintes opções:  

    > [!IMPORTANT]  
    > A arquitetura da imagem de inicialização que você distribuir deve ser apropriada para a arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode iniciar e executar uma imagem de inicialização x86 ou x64. No entanto, um computador de destino x86 pode iniciar e executar apenas uma imagem de inicialização x86.  

    - **Imagem de inicialização**: selecione a imagem de inicialização para iniciar o computador de destino.  

    - **Ponto de distribuição**: selecione o ponto de distribuição que possui a imagem de inicialização. O assistente recupera a imagem de inicialização do ponto de distribuição e a grava na mídia.  

        > [!NOTE]  
        > Sua conta de usuário precisa pelo menos de permissões de **Leitura** à biblioteca de conteúdo no ponto de distribuição.  

    - **Ponto de gerenciamento**: somente para *mídia de site*, selecione um ponto de gerenciamento de um site primário.  

    - **Pontos de gerenciamento associado:**: somente para *mídia dinâmica*, selecione os pontos de gerenciamento do site primário a serem usados e uma ordem de prioridade para a comunicação inicial.  

8. Na página **Personalização**, especifique as seguintes opções:  

    - Adicione quaisquer variáveis usadas pela sequência de tarefas.  

    - **Habilitar comando prestart**: especifique qualquer comando prestart que você queira executar antes da execução da sequência de tarefas. Comandos prestart são um script ou executável que pode interagir com o usuário no Windows PE antes da execução da sequência de tarefas. Para mais informações, consulte [Comandos prestart para mídia de sequência de tarefas](/sccm/osd/understand/prestart-commands-for-task-sequence-media).  

        > [!TIP]  
        > Durante a criação da mídia, a sequência de tarefas grava o ID do pacote e a linha do comando prestart, incluindo o valor de qualquer variável de sequência de tarefas, no arquivo **CreateTSMedia.log** no computador que executa o console do Configuration Manager. Você poderá analisar esse arquivo de log para verificar o valor das variáveis de sequência de tarefas.  

        Se o comando prestart exigir algum conteúdo, selecione a opção **Incluir arquivos no comando prestart**.  

9. Conclua o assistente.  


## <a name="alternate-method"></a>Método alternativo

Você pode criar uma mídia inicializável em uma unidade USB removível quando a unidade não está conectada ao computador que executa o console do Configuration Manager.

1. [Criar a mídia de inicialização de sequência de tarefas](#process). Na página **Tipo de mídia**, selecione **Conjunto de CD/DVD**. O assistente grava os arquivos de saída no local que você especificar. Por exemplo: `\\servername\folder\outputfile.iso`.  

2. Preparar a unidade USB removível. A unidade deve estar formatada, vazia e inicializável.

3. Monte o ISO do local de compartilhamento e transfira os arquivos do ISO para a unidade USB.


## <a name="next-steps"></a>Próximas etapas

[Use a mídia inicializável para implantar o Windows na rede](/sccm/osd/deploy-use/use-bootable-media-to-deploy-windows-over-the-network)  
