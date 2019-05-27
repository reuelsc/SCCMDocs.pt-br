---
title: Criar mídia em pré-teste
titleSuffix: Configuration Manager
description: Use uma mídia em pré-teste no Configuration Manager para simplificar a implantação do Windows em vários cenários.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ff6e7267-302a-4563-815e-cdc0d1a4b60f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8cba7fff1ec7144abfa5f92c25c73d36d5d7c749
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65082786"
---
# <a name="create-prestaged-media"></a>Criar mídia em pré-teste

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A mídia em pré-teste no Configuration Manager é um arquivo WIM (Imagem do Windows). Ela pode ser instalada em um computador sem sistema operacional pelo fabricante ou no seu centro de preparo que não esteja conectado ao ambiente de produção do Configuration Manager. A mídia em pré-teste contém a imagem de inicialização usada para iniciar o computador de destino e a imagem do SO aplicada ao computador de destino. Também é possível especificar aplicativos, pacotes e pacotes de driver para incluir como parte da mídia em pré-teste. A sequência de tarefas que implanta o SO não está incluída na mídia. A mídia em pré-teste é aplicada à unidade de disco rígido de um novo computador antes do computador ser enviado ao usuário final.

Use a mídia em pré-teste para os seguintes cenários de implantação de SO:  

- [Criar uma imagem de um OEM na fábrica ou em um repositório local](/sccm/osd/deploy-use/create-an-image-for-an-oem-in-factory-or-a-local-depot)  

- [Instalar uma nova versão do Windows em um novo computador (sem sistema operacional)](/sccm/osd/deploy-use/install-new-windows-version-new-computer-bare-metal)  

- [Implantar o Windows to Go](/sccm/osd/deploy-use/deploy-windows-to-go)  


## <a name="usage"></a>Uso

Quando o computador é iniciado pela primeira vez após a aplicação da mídia em pré-teste, ele é iniciado no Windows PE. O computador se conecta a um ponto de gerenciamento para localizar a sequência de tarefas que conclui o processo de implantação do SO. Quando você implanta uma sequência de tarefas que usa uma mídia em pré-teste, primeiro o cliente verifica o cache de sequência de tarefas local em busca de conteúdo válido. Se o conteúdo não for encontrado ou se tiver sido revisado, o cliente baixará o conteúdo de um ponto de distribuição ou par.  


## <a name="prerequisites"></a>Pré-requisitos

Antes de criar uma mídia em pré-teste usando o Assistente para Criar Mídia de Sequência de Tarefas, verifique se todas as condições foram atendidas.

### <a name="boot-image"></a>Imagem de inicialização

Considere os seguintes pontos sobre a imagem de inicialização usada na sequência de tarefas para implantar o SO:

- A arquitetura da imagem de inicialização deve ser apropriada para a arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode iniciar e executar uma imagem de inicialização x86 ou x64. No entanto, um computador de destino x86 pode iniciar e executar apenas uma imagem de inicialização x86.
- Certifique-se de que a imagem de inicialização contenha os drivers de rede e de armazenamento necessários para provisionar o computador de destino.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Criar uma sequência de tarefas para implantar um SO

Como parte da mídia em pré-teste, especifique a sequência de tarefas para implantar o SO. Para saber mais, confira [Criar uma sequência de tarefas para instalar um SO](/sccm/osd/deploy-use/create-a-task-sequence-to-install-an-operating-system).

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuir todo o conteúdo associado à sequência de tarefas

Distribua todo o conteúdo exigido pela sequência de tarefas para pelo menos um ponto de distribuição. Esse conteúdo inclui a imagem de inicialização, a imagem do SO e outros arquivos associados. O assistente reúne o conteúdo do ponto de distribuição ao criar a mídia em pré-teste.

Sua conta de usuário precisa pelo menos de direitos de acesso de **Leitura** à biblioteca de conteúdo nesse ponto de distribuição. Para obter mais informações, consulte [Distribuir conteúdo](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).

### <a name="hard-drive-on-the-destination-computer"></a>Disco rígido no computador de destino

O disco rígido do computador de destino deve ser formatado antes que a mídia em pré-teste seja aplicada a ele. Se o disco rígido não estiver formatado quando a mídia for aplicada, a sequência de tarefas que implanta o SO falhará quando tenta iniciar o computador de destino.

> [!NOTE]  
> O Assistente para Criar Mídia de Sequência de Tarefas define a seguinte condição de variável de sequência de tarefas na mídia: **_SMSTSMediaType = OEMMedia**. Você pode usar essa mesma condição na sua sequência de tarefas.  


## <a name="process"></a>Processar

1. No console do Configuration Manager, acesse o espaço de trabalho **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione o nó **Sequências de Tarefas**.  

2. Na guia **Início** da faixa de opções, no grupo **Criar**, selecione **Criar Mídia de Sequência de Tarefas**. Essa ação inicia o Assistente para Criar Mídia de Sequência de Tarefas.  

3. Na página **Selecionar o Tipo de Mídia**, especifique as seguintes opções:  

    - Selecione **Mídia em pré-teste**.  

    - Opcionalmente, se quiser permitir que o SO seja implantado sem exigir a entrada do usuário, selecione **Permitir implantação autônoma do sistema operacional**.  

        > [!IMPORTANT]  
        > Quando você seleciona essa opção, o usuário não recebe uma solicitação para fornecer informações de configuração da rede ou sequências de tarefas opcionais. Se você configurar a mídia para proteção por senha, o usuário ainda será solicitado a fornecer uma senha.  

4. Na página **Gerenciamento de Mídia**, especifique uma das seguintes opções:  

    - **Mídia dinâmica**: permite que um ponto de gerenciamento redirecione a mídia para outro ponto de gerenciamento, com base na localização do cliente nos limites do site.  

    - **Mídia de site**: a mídia contata apenas o ponto de gerenciamento especificado.  

5. Na página **Propriedades da Mídia**, especifique as seguintes informações:  

    - **Criado por**: especifique quem criou a mídia.  

    - **Versão**: especifique o número de versão da mídia.  

    - **Comentário**: especifique uma descrição exclusiva da finalidade da mídia.  

    - **Arquivo de mídia**: especifique o nome e o caminho dos arquivos de saída. O assistente grava os arquivos de saída nesse local. Por exemplo: `\\servername\folder\outputfile.wim`  

    - **Pasta de preparo**<!--1359388-->: o processo de criação da mídia pode exigir muito espaço em disco temporário. Por padrão, essa localização é semelhante ao seguinte caminho: `%UserProfile%\AppData\Local\Temp`. A partir da versão 1902, para fornecer maior flexibilidade quando se trata de armazenar esses arquivos temporários, altere esse valor para outra unidade e caminho.  

6. Na página **Segurança**, especifique as seguintes opções:  

    - **Habilitar suporte a computadores desconhecidos**: permite que a mídia implante um SO em um computador que não seja gerenciado pelo Configuration Manager. Não há registro desses computadores no banco de dados do Configuration Manager. Para obter mais informações, consulte [Preparar implantações de computador desconhecido](/sccm/osd/get-started/prepare-for-unknown-computer-deployments).  

    - **Proteger mídia com senha**: insira uma senha forte para ajudar a proteger a mídia contra acesso não autorizado. Quando você especificar uma senha, o usuário deverá fornecer essa senha para usar a mídia em pré-teste.  

        > [!IMPORTANT]  
        > Como prática recomendada de segurança, atribua sempre uma senha para ajudar a proteger a mídia em pré-teste.  

    - Para comunicações HTTP, selecione **Criar certificado de mídia autoassinado**. Em seguida, especifique a data de início e de vencimento do certificado.  

    - Para comunicações HTTPS, selecione **Importar certificado PKI**. Em seguida, especifique o certificado a ser importado e sua senha.  

        Para saber mais sobre este certificado de cliente usado por imagens de inicialização, confira [Requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

    - **Afinidade de dispositivo de usuário**: para dar suporte ao gerenciamento voltado ao usuário no Configuration Manager, especifique como você deseja que a mídia associe usuários ao computador de destino. Para saber mais sobre como a implantação do SO dá suporte à afinidade de dispositivo de usuário, confira [Associar usuários a um computador de destino](/sccm/osd/get-started/associate-users-with-a-destination-computer).  

        - **Permitir afinidade de dispositivo de usuário com aprovação automática**: a mídia associa automaticamente os usuários ao computador de destino. Essa funcionalidade se baseia nas ações da sequência de tarefas que implanta o SO. Nesse cenário, a sequência de tarefas cria um relacionamento entre os usuários especificados e o computador de destino ao implantar o SO nesse computador.  

        - **Permitir afinidade de dispositivo de usuário pendente de aprovação de administrador**: a mídia associa os usuários ao computador de destino depois que uma aprovação é concedida. Essa funcionalidade se baseia no escopo da sequência de tarefas que implanta o SO. Nesse cenário, a sequência de tarefas cria um relacionamento entre os usuários especificados e o computador de destino, mas aguarda a aprovação de um usuário administrativo antes que o SO seja implantado.  

        - **Não permitir afinidade de dispositivo de usuário**: a mídia não associa usuários ao computador de destino. Nesse cenário, a sequência de tarefas não associa usuários ao computador de destino quando implanta o SO.  

7. Na página **Sequência de Tarefas**, selecione a sequência de tarefas que é executada no computador de destino. Verifique a lista de conteúdo consultada pela sequência de tarefas.  

    - **Detectar dependências de aplicativos associados e adicioná-las a esta mídia**: também adicione conteúdo à mídia para dependências de aplicativos.  

        > [!TIP]  
        > Se você não vir as dependências de aplicativo esperadas, desmarque e depois selecione novamente essa opção para atualizar a lista.  

8. Na página **Imagem de inicialização**, especifique as seguintes opções:  

    > [!IMPORTANT]  
    > A arquitetura da imagem de inicialização que você distribuir deve ser apropriada para a arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode iniciar e executar uma imagem de inicialização x86 ou x64. No entanto, um computador de destino x86 pode iniciar e executar apenas uma imagem de inicialização x86.  

    - **Imagem de inicialização**: selecione a imagem de inicialização para iniciar o computador de destino.  

    - **Ponto de distribuição**: selecione o ponto de distribuição que possui a imagem de inicialização. O assistente recupera a imagem de inicialização do ponto de distribuição e a grava na mídia.  

        > [!NOTE]  
        > Sua conta de usuário precisa pelo menos de permissões de **Leitura** à biblioteca de conteúdo no ponto de distribuição.  

    - **Ponto de gerenciamento**: somente para *mídia de site*, selecione um ponto de gerenciamento de um site primário.  

    - **Pontos de gerenciamento associado:**: somente para *mídia dinâmica*, selecione os pontos de gerenciamento do site primário a serem usados e uma ordem de prioridade para a comunicação inicial.  

9. Na página **Imagens**, especifique as seguintes opções:  

    - **Pacote de imagens**: especifique a imagem do SO a ser usada. Para obter mais informações, confira [Gerenciar imagens do sistema operacional](/sccm/osd/get-started/manage-operating-system-images).  

    - **Índice de imagens**: se o pacote contiver várias imagens do SO, especifique o índice da imagem a ser implantada.  

    - **Ponto de distribuição**: especifique o ponto de distribuição que contém o pacote de imagens do SO. O assistente obtém a imagem do SO do ponto de distribuição e a grava na mídia.  

10. Na página **Selecionar Aplicativo**, selecione aplicativos adicionais para inclusão no arquivo de mídia em pré-teste.  

11. Na página **Selecionar Pacote**, selecione pacotes adicionais para inclusão no arquivo de mídia em pré-teste.  

12. Na página **Selecionar Pacote de Driver**, selecione pacotes de driver adicionais para inclusão no arquivo de mídia em pré-teste.  

13. Na página **Pontos de Distribuição**, selecione um ou mais pontos de distribuição dos quais obter conteúdo.  

    O Configuration Manager exibe apenas pontos de distribuição que tenham conteúdo. Distribua todo o conteúdo associado à sequência de tarefas para pelo menos um ponto de distribuição antes de continuar. Após distribuir o conteúdo, atualize a lista de pontos de distribuição. Remova os pontos de distribuição que já foram selecionados nessa página, vá para a página anterior e volte para a página **Pontos de Distribuição**. Como alternativa, reinicie o assistente. Para obter mais informações, consulte [Distribuir o conteúdo referenciado por uma sequência de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DistributeTS) e [Gerenciar conteúdo e infraestrutura de conteúdo](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  

14. Na página **Personalização**, especifique as seguintes opções:  

    - Adicione quaisquer variáveis usadas pela sequência de tarefas.  

    - **Habilitar comando prestart**: especifique qualquer comando prestart que você queira executar antes da execução da sequência de tarefas. Comandos prestart são um script ou executável que pode interagir com o usuário no Windows PE antes da execução da sequência de tarefas. Para mais informações, consulte [Comandos prestart para mídia de sequência de tarefas](/sccm/osd/understand/prestart-commands-for-task-sequence-media).  

        > [!TIP]  
        > Durante a criação da mídia, a sequência de tarefas grava o ID do pacote e a linha do comando prestart, incluindo o valor de qualquer variável de sequência de tarefas, no arquivo **CreateTSMedia.log** no computador que executa o console do Configuration Manager. Você poderá analisar esse arquivo de log para verificar o valor das variáveis de sequência de tarefas.  

        Se o comando prestart exigir algum conteúdo, selecione a opção **Incluir arquivos no comando prestart**.  

15. Conclua o assistente.  


## <a name="next-steps"></a>Próximas etapas

[Criar uma imagem de um OEM na fábrica ou em um repositório local](/sccm/osd/deploy-use/create-an-image-for-an-oem-in-factory-or-a-local-depot)
