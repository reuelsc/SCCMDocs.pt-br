---
title: Implantar o conteúdo
titleSuffix: Configuration Manager
description: Depois de instalar os pontos de distribuição para o System Center Configuration Manager, eis como você pode começar a implantar o conteúdo para eles.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d50dcca0-4419-449d-a487-73abcadf328f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c6a2a69047a8fee5ab0c1f4f0f13197178334f05
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="deploy-and-manage-content-for-system-center-configuration-manager"></a>Implantar e gerenciar o conteúdo para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Depois de instalar os pontos de distribuição para o System Center Configuration Manager, você pode começar a implantar o conteúdo para eles. Normalmente, o conteúdo é transferido para os pontos de distribuição pela rede, mas há outras opções para levar o conteúdo para os pontos de distribuição. Depois que o conteúdo é transferido para um ponto de distribuição, você pode atualizar, redistribuir, remover e validar esse conteúdo nos pontos de distribuição.  

##  <a name="bkmk_distribute"></a> Distribuir conteúdo  
 Em geral, você distribui o conteúdo para pontos de distribuição para que ele esteja disponível para computadores cliente. (A exceção é quando você usa distribuição de conteúdo sob demanda para uma implantação específica.)  Ao distribuir conteúdo, o Configuration Manager armazena os arquivos de conteúdo em um pacote e depois distribui o pacote para o ponto de distribuição. Os tipos de conteúdo que você pode distribuir incluem:  

-   Tipos de implantação de aplicativos  

-   Pacotes  

-   Pacotes de implantação  

-   Pacotes de driver  

-   Imagens do sistema operacional  

-   Instaladores de sistema operacional  

-   Imagens de inicialização  

-   Sequências de tarefas  

Ao criar um pacote que contém arquivos de origem, como um tipo de implantação do aplicativo ou um pacote de implantação, o site no qual o pacote é criado se torna o proprietário do site para a fonte de conteúdo do pacote. O Configuration Manager copia os arquivos de origem do caminho do arquivo de origem especificado para o objeto na biblioteca de conteúdo no servidor do site que tem a fonte de conteúdo do pacote.  Em seguida, o Configuration Manager replica as informações para sites adicionais. (Confira [A biblioteca de conteúdo](../../../../core/plan-design/hierarchy/the-content-library.md) para obter mais informações sobre isso.)  

Use o procedimento a seguir para distribuir o conteúdo para pontos de distribuição.  

#### <a name="to-distribute-content-on-distribution-points"></a>Para distribuir conteúdo em pontos de distribuição  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , selecione uma das seguintes etapas para o tipo de conteúdo que você quer distribuir:  

    -   **Aplicativos**: expanda **Gerenciamento de Aplicativos** > **Aplicativos** e selecione os aplicativos que você quer distribuir.  

    -   **Pacotes**: expanda **Gerenciamento de Aplicativos** >  **Pacotes** e selecione os pacotes que você quer distribuir.  

    -   **Pacotes de Implantação**: expanda **Atualizações do Software** >  **Pacotes de Implantação** e selecione os pacotes de implantação que você quer distribuir.  

    -   **Pacotes de Driver**: expanda **Sistemas Operacionais** >  **Pacotes de Driver** e selecione os pacotes de driver que você quer distribuir.  

    -   **Imagens do Sistema Operacional**: expanda **Sistemas Operacionais** >  **Imagens do Sistema Operacional** e selecione as imagens do sistema operacional que você quer distribuir.  

    -   **Instaladores do Sistema Operacional**: expanda **Sistemas Operacionais** > **Instaladores do Sistema Operacional** e selecione os instaladores do sistema operacional que deseja distribuir.  

    -   **Imagens de Inicialização**: expanda **Sistemas Operacionais** >  **Imagens de Inicialização** e selecione as imagens de inicialização que deseja distribuir.  

    -   **Sequência de Tarefas**: expanda **Sistemas Operacionais** >  **Sequências de Tarefas** e selecione a sequência de tarefas que deseja distribuir. Embora as sequências de tarefas não tenham o conteúdo, elas têm dependências de conteúdo associadas que são distribuídas.  

        > [!NOTE]  
        >  Se você modificar a sequência de tarefas, deverá redistribuir o conteúdo.  

3.  Na guia **Início** , no grupo **Implantação** , clique em **Distribuir Conteúdo**. O Assistente para Distribuir Conteúdo é aberto.  

4.  Na página **Geral**, verifique se o conteúdo listado é o conteúdo que você quer distribuir, escolha se você quer que o Configuration Manager detecte as dependências de conteúdo associadas ao conteúdo selecionado, adicione as dependências à distribuição e clique em **Próximo**.  

    > [!NOTE]  
    >  Você tem a opção de definir a configuração **Detectar dependências de conteúdo associadas e adicioná-las a esta distribuição** somente para o tipo de conteúdo do aplicativo. O Configuration Manager define automaticamente esta configuração para sequências de tarefas e ela não pode ser modificada.  

5.  Na guia **Conteúdo** , se exibida, verifique se o conteúdo listado é o conteúdo que você quer distribuir e clique em **Próximo**.  

    > [!NOTE]  
    >  A página **Conteúdo** só é exibida quando a configuração **Detectar dependências de conteúdo associado e adicioná-las a essa distribuição** é selecionada na página **Geral** do assistente.  

6.  Na página **Destino do Conteúdo** , clique em **Adicionar**, escolha uma destas opções e siga a etapa associada:  

    -   **Coleções**: selecione **Coleções de Usuários** ou **Coleções de Dispositivos**, clique na coleção associada a um ou mais grupos de pontos de distribuição, e clique em **OK**.  

        > [!NOTE]  
        >  Somente as coleções associadas a um grupo de pontos de distribuição são exibidas. Para mais informações sobre como associar coleções a grupos de pontos de distribuição, confira [Manage distribution point groups](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) (Gerenciar grupos de pontos de distribuição) no tópico [Install and configure distribution points for System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) (Instalar e configurar pontos de distribuição para o System Center Configuration Manager).  

    -   **Ponto de Distribuição**: selecione um ponto de distribuição existente e clique em **OK**. Os pontos de distribuição que já receberam o conteúdo não são exibidos.  

    -   **Grupo de Pontos de Distribuição**: selecione um grupo de pontos de distribuição existente e clique em **OK**. Os grupos de pontos de distribuição que já receberam o conteúdo não são exibidos.  

    Ao terminar de adicionar destinos de conteúdo, clique em **Próximo**.  

7.  Na página **Resumo** , verifique as configurações de distribuição antes de prosseguir. Para distribuir o conteúdo aos destinos selecionados, clique em **Próximo**.  

8.  A página **Andamento** exibe o andamento da distribuição.  

9. A página **Confirmação** mostra se o conteúdo foi atribuído com êxito aos pontos. Para monitorar a distribuição de conteúdo, confira [Monitorar o conteúdo que você distribuiu com o System Center Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

##  <a name="bkmk_prestage"></a> Usar conteúdo pré-teste  
 Você pode pré-configurar os arquivos de conteúdo para aplicativos e tipos de pacote:  

-   No console do Configuration Manager, você seleciona o conteúdo de que precisa e usa o **Assistente para Criar Arquivo de Conteúdo Pré-Teste** para criar um arquivo de conteúdo pré-teste e compactado que contenha arquivos e metadados associados ao conteúdo selecionado.  

-   Você pode importar manualmente o conteúdo em um servidor de site, site secundário ou ponto de distribuição.  

-   Quando você importa o arquivo de conteúdo de pré-teste em um servidor do site, os arquivos de conteúdo são adicionados à biblioteca de conteúdo no servidor do site, e em seguida registrados no banco de dados do servidor do site.  

-   Quando você importa o arquivo de conteúdo de pré-teste em um ponto de distribuição, os arquivos de conteúdo são adicionados à biblioteca de conteúdo no ponto de distribuição, e uma mensagem de status é enviada ao servidor do site informando que o conteúdo está disponível no ponto de distribuição.  

**Limitações e considerações para o conteúdo pré-teste:**  

-   **Quando o ponto de distribuição estiver localizado no servidor do site**, não habilite o ponto de distribuição para conteúdo pré-teste. Em vez disso, use o procedimento em [Como pré-testar conteúdo no ponto de distribuição em um servidor do site](#bkmk_dpsiteserver).  

-   **Quando o ponto de distribuição estiver configurado como ponto de distribuição de recepção**, não habilite o ponto de distribuição para conteúdo pré-teste. A configuração do conteúdo de pré-teste para um ponto de distribuição substitui a configuração do ponto de distribuição de recepção. Um ponto de distribuição de recepção configurado para conteúdo de pré-teste não extrai conteúdo de ponto de distribuição de origem e não recebe conteúdo do servidor do site.  

-   **Para você poder pré-configurar conteúdo para o ponto de distribuição, a biblioteca de conteúdo deve ser criada no ponto de distribuição**. Distribua conteúdo pela rede ao menos uma vez antes de pré-configurar conteúdo para o ponto de distribuição.  

-   **Quando você pré-configura conteúdo para um pacote com um longo caminho de origem** (por exemplo, mais de 140 caracteres), a ferramenta de linha de comando Extrair Conteúdo pode falhar em extrair com sucesso, para a biblioteca de conteúdo, o conteúdo daquele pacote.  

Para informações sobre quando pré-configurar os arquivos de conteúdo, confira *Conteúdo pré-teste* no tópico [Gerenciar a largura de banda de rede para o gerenciamento de conteúdo](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).  

Use as seções a seguir para pré-configurar o conteúdo.  

###  <a name="BKMK_CreatePrestagedContentFile"></a> Etapa 1: Criar um arquivo de conteúdo pré-teste  
 Você pode criar um arquivo de conteúdo pré-teste, compactado, que contenha os arquivos e metadados associados para o conteúdo selecionado no console do Configuration Manager. Use o procedimento a seguir para criar um arquivo de conteúdo de pré-teste.  

##### <a name="to-create-a-prestaged-content-file"></a>Para criar um arquivo de conteúdo de pré-teste  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , selecione uma das seguintes etapas para o tipo de conteúdo que você quer pré-configurar:  

    -   **Aplicativos**: Expanda **Gerenciamento de Aplicativos**, clique em **Aplicativos**, e selecione os aplicativos que você quer pré-configurar.  

    -   **Pacotes**: Expanda **Gerenciamento de Aplicativos**, clique em **Pacotes**, e selecione os pacotes que você quer pré-configurar.  

    -   **Pacotes de Driver**: Expanda **Sistemas Operacionais**, clique em **Pacotes de Driver**, e selecione os pacotes de driver que você quer pré-configurar.  

    -   **Imagens do Sistema Operacional**: Expanda **Sistemas Operacionais**, clique em **Imagens do Sistema Operacional**, e selecione as imagens do sistema operacional que você quer pré-configurar.  

    -   **Instaladores de Sistema Operacional**: Expanda **Sistemas Operacionais**, clique em **Instaladores de Sistema Operacional**, e selecione os instaladores de sistema operacional que você quer pré-configurar.  

    -   **Imagens de Inicialização**: Expanda **Sistemas Operacionais**, clique em **Imagens de Inicialização**, e selecione as imagens de inicialização que você quer pré-configurar.  

    -   **Sequências de Tarefas**: expanda **Sistemas Operacionais**, clique em **Sequências de Tarefas**e selecione a sequência de tarefas que você quer criar um pré-teste.  

3.  Na guia **Início** , no grupo **Implantação** , clique em **Criar Arquivo de Conteúdo de Pré-Teste**. O Assistente para Criar Arquivo de Conteúdo de Pré-Teste é aberto.  

    > [!NOTE]  
    >  **Para aplicativos:** na guia **Início**, no grupo **Aplicativo**, clique em **Criar Arquivo de Conteúdo Pré-teste**.  
    >   
    >  **Para pacotes:** na guia **Início**, no grupo &lt;*NomedoPacote*>, clique em **Criar Arquivo de Conteúdo Pré-teste**.  

4.  Na página **Geral** , clique em **Procurar**, escolha o local para o arquivo de conteúdo de pré-teste, determine um nome para o arquivo e clique em **Salvar**. Use esse arquivo de conteúdo de pré-teste em servidores de site primário, servidores de site secundário ou pontos de distribuição, para importar o conteúdo e os metadados.  

5.  Para aplicativos, selecione **Exportar todas as dependências** para que o Configuration Manager detecte e adicione as dependências associadas ao aplicativo ao arquivo de conteúdo pré-teste. Por padrão, essa configuração está selecionada.  

6.  Em **Comentários do administrador**, insira comentários opcionais sobre o arquivo de conteúdo de pré-teste e clique em **Próximo**.  

7.  Na página **Conteúdo** , verifique se o conteúdo listado é o conteúdo que você quer adicionar ao arquivo de conteúdo de pré-teste e clique em **Próximo**.  

8.  Na página **Locais de Conteúdo** , especifique os pontos de distribuição dos quais você quer recuperar os arquivos de conteúdo para o arquivo de conteúdo de pré-teste. Você pode selecionar mais de um ponto de distribuição para recuperar o conteúdo. Os pontos de distribuição são listados na seção Locais de conteúdo. A coluna **Conteúdo** exibe quantos dos pacotes ou aplicativos selecionados estão disponíveis em cada ponto de distribuição. O Configuration Manager começa pelo primeiro ponto de distribuição na lista para recuperar o conteúdo selecionado e depois segue para baixo na lista, a fim de recuperar o conteúdo restante necessário para o arquivo de conteúdo pré-teste. Clique em **Mover para Cima** ou **Mover para Baixo** para alterar a ordem de prioridade dos pontos de distribuição. Quando os pontos de distribuição da lista não contêm todo o conteúdo selecionado, você deve adicionar à lista pontos de distribuição que têm o conteúdo ou sair do assistente, distribuir o conteúdo por pelo menos um ponto de distribuição e reiniciar o assistente.  

9. Na página **Resumo** , confirme os detalhes. Você pode voltar às páginas anteriores e fazer alterações. Clique em **Próximo** para criar o arquivo de conteúdo de pré-teste.  

10. A página **Andamento** exibe o conteúdo que está sendo adicionado ao arquivo de conteúdo de pré-teste.  

11. Na página **Conclusão** , verifique se o arquivo de conteúdo pré-configurado foi criado com sucesso, e clique em **Fechar**.  

###  <a name="BKMK_AssignContentToDistributionPoint"></a> Etapa 2: Atribuir o conteúdo a pontos de distribuição  
 Depois que você pré-configurar o arquivo de conteúdo, atribua o conteúdo a pontos de distribuição.  

> [!NOTE]  
>  Quando você usa um arquivo de conteúdo pré-configurado para recuperar a biblioteca de conteúdo em um servidor do site, e não precisa pré-configurar arquivos de conteúdo em um ponto de distribuição, você pode ignorar esse procedimento.  

 Use o procedimento a seguir para atribuir o conteúdo do arquivo de conteúdo pré-configurado a pontos de distribuição.  

> [!IMPORTANT]  
>  Verifique se os pontos de distribuição que você quer pré-configurar são configurados como pontos de distribuição pré-testados ou se o conteúdo é distribuído para os pontos de distribuição usando a rede.  

##### <a name="to-assign-the-content-to-distribution-points"></a>Para atribuir o conteúdo a pontos de distribuição  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , selecione uma das seguintes etapas para o tipo de conteúdo que você quer selecionar ao criar arquivo de conteúdo pré-configurado:  

    -   **Aplicativos**: Expanda **Gerenciamento de Aplicativo**, clique em **Aplicativos**, e selecione os aplicativos pré-configurados.  

    -   **Pacotes**: Expanda **Gerenciamento de Aplicativo**, clique em **Pacotes**, e selecione os pacotes pré-configurados.  

    -   **Pacotes de Implantação**: Expanda **Atualizações do Software**, clique em **Pacotes de Implantação**, e selecione os pacotes de implantação pré-configurados.  

    -   **Pacotes de Driver**: Expanda **Sistemas Operacionais**, clique em **Pacotes de Driver**, e selecione os pacotes de driver pré-configurados.  

    -   **Imagens do Sistema Operacional**: Expanda **Sistemas Operacionais**, clique em **Imagens do Sistema Operacional**, e selecione as imagens do sistema operacional pré-configuradas.  

    -   **Instaladores de Sistema Operacional**: Expanda **Sistemas Operacionais**, clique em **Instaladores de Sistema Operacional**, e selecione os instaladores de sistema operacional pré-configurados.  

    -   **Imagens de Inicialização**: Expanda **Sistemas Operacionais**, clique em **Imagens de Inicialização**, e selecione as imagens de inicialização pré-configuradas.  

3.  Na guia **Início** , no grupo **Implantação** , clique em **Distribuir Conteúdo**. O Assistente para Distribuir Conteúdo é aberto.  

4.  Na página **Geral**, verifique se o conteúdo listado é o conteúdo que você pré-configurou e escolha se você quer que o Configuration Manager detecte as dependências de conteúdo associadas ao conteúdo selecionado, adicione as dependências à distribuição e clique em **Próximo**.  

    > [!NOTE]  
    >  Você tem a opção de definir a configuração **Detectar dependências de conteúdo associadas e adicioná-las a esta distribuição** somente para o tipo de conteúdo do aplicativo. O Configuration Manager define automaticamente esta configuração para sequências de tarefas e ela não pode ser modificada.  

5.  Na página **Conteúdo** , verifique se o conteúdo listado é o conteúdo que você quer distribuir e clique em **Próximo**.  

    > [!NOTE]  
    >  A página **Conteúdo** só é exibida quando a configuração **Detectar dependências de conteúdo associado e adicioná-las a essa distribuição** é selecionada na página **Geral** do assistente.  

6.  Na página **Destino de Conteúdo** , clique em **Adicionar**, escolha uma das seguintes opções que inclui os pontos de distribuição a serem pré-configurados e siga a etapa associada:  

    -   **Coleções**: selecione **Coleções de Usuários** ou **Coleções de Dispositivos**, clique na coleção associada a um ou mais grupos de pontos de distribuição, e clique em **OK**.  

        > [!NOTE]  
        >  Somente as coleções associadas a um grupo de pontos de distribuição são exibidas.  Para mais informações, confira [Manage distribution point groups](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) (Gerenciar grupos de pontos de distribuição) no tópico [Install and configure distribution points for System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) (Instalar e configurar pontos de distribuição para o System Center Configuration Manager).  

    -   **Ponto de Distribuição**: selecione um ponto de distribuição existente e clique em **OK**. Os pontos de distribuição que já receberam o conteúdo não são exibidos.  

    -   **Grupo de Pontos de Distribuição**: selecione um grupo de pontos de distribuição existente e clique em **OK**. Os grupos de pontos de distribuição que já receberam o conteúdo não são exibidos.  

    Ao terminar de adicionar destinos de conteúdo, clique em **Próximo**.  

7.  Na página **Resumo** , verifique as configurações de distribuição antes de prosseguir. Para distribuir o conteúdo aos destinos selecionados, clique em **Próximo**.  

8.  A página **Andamento** exibe o andamento da distribuição.  

9. A página **Confirmação** mostra se o conteúdo foi atribuído com êxito aos pontos de distribuição. Para monitorar a distribuição de conteúdo, confira [Monitorar o conteúdo que você distribuiu com o System Center Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

###  <a name="BKMK_ExportContentFromPrestagedContentFile"></a> Etapa 3: Extrair o conteúdo do arquivo de conteúdo pré-teste  
 Após criar o arquivo de conteúdo de pré-teste e atribuir o conteúdo a pontos de distribuição, você pode extrair os arquivos de conteúdo para a biblioteca de conteúdo em um servidor do site ou ponto de distribuição. Normalmente, você já copiou o arquivo de conteúdo de pré-teste em uma unidade portátil, como uma unidade USB, ou gravou o conteúdo em uma mídia, como um DVD, e já o tem disponível no local do servidor do site ou no ponto de distribuição que requer o conteúdo.  

 Use o procedimento a seguir para exportar manualmente os arquivos de conteúdo do arquivo de conteúdo de pré-teste usando a ferramenta de linha de comando Extrair Conteúdo.  

> [!IMPORTANT]  
>  Ao executar a ferramenta de linha de comando Extrair Conteúdo, ela cria um arquivo temporário enquanto cria o arquivo de conteúdo de pré-teste. Em seguida, o arquivo é copiado na pasta de destino e o arquivo temporário é excluído. Você deve ter espaço suficiente em disco para o arquivo temporário para que o processo não falhe. O arquivo temporário é criado no seguinte local:  
>   
>  -   O arquivo temporário é criado na mesma pasta que você especifica como a pasta de destino para o arquivo de conteúdo de pré-teste.  

> [!IMPORTANT]  
>  O usuário que executa a ferramenta de linha de comando Extrair Conteúdo deve ter direitos de **Administrador** no computador do qual você está extraindo o conteúdo pré-teste.  

##### <a name="to-extract-the-content-files-from-the-prestaged-content-file"></a>Para extrair os arquivos de conteúdo do arquivo de conteúdo de pré-teste  

1.  Copie o arquivo de conteúdo de pré-teste no computador do qual você deseja extrair o conteúdo.  

2.  Copie a ferramenta de linha de comando Extrair Conteúdo do &lt;*ConfigMgrInstallationPath*>\bin\\&lt;*plataforma*> para o computador do qual você deseja extrair o arquivo de conteúdo pré-teste.  

3.  Abra o prompt de comando e navegue até a pasta local do arquivo de conteúdo de pré-teste e da ferramenta Extrair Conteúdo.  

    > [!NOTE]  
    >  Você pode extrair um ou mais arquivos de conteúdo de pré-teste em um site de servidor, servidor do site secundário ou ponto de distribuição.  

4.  Digite **extractcontent /P:**&lt;*PrestagedFileLocation*>**\\**&lt;*PrestagedFileName*> **/S** para importar um único arquivo.  

     Digite **extractcontent /P:**&lt;*PrestagedFileLocation*> **/S** para importar todos os arquivos pré-configurados na pasta especificada.  

     Por exemplo, digite **extractcontent /P:D:\PrestagedFiles\MyPrestagedFile.pkgx /S** em que `D:\PrestagedFiles\` é o PrestagedFileLocation, `MyPrestagedFile.pkgx` é o nome do arquivo pré-teste e o `/S` informa ao Configuration Manager para extrair somente arquivos de conteúdo que são mais novos do que os que estão atualmente no ponto de distribuição.  

     Quando você extrai o arquivo de conteúdo de pré-teste em um servidor do site, os arquivos de conteúdo são adicionados à biblioteca de conteúdo no servidor do site, e em seguida a disponibilidade do conteúdo é registrada no banco de dados do servidor do site. Ao exportar o arquivo de conteúdo de pré-teste em um ponto de distribuição, os arquivos de conteúdo são adicionados à biblioteca de conteúdo no ponto de distribuição, o ponto de distribuição envia uma mensagem de status ao servidor do site primário pai, e em seguida a disponibilidade do conteúdo é registrada no banco de dados do site.  

    > [!IMPORTANT]  
    >  No cenário a seguir, você deve atualizar o conteúdo que você extraiu do arquivo de conteúdo de pré-teste quando o conteúdo é atualizado para uma nova versão:  
    >   
    >  1.  Você cria um arquivo de conteúdo de pré-teste para a versão 1 de um pacote.  
    >  2.  Você atualiza os arquivos de origem para o pacote com a versão 2.  
    >  3.  Você extrai o arquivo de conteúdo de pré-teste (versão 1 do pacote) em um ponto de distribuição.  
    >   
    > O Configuration Manager não distribui automaticamente a versão 2 do pacote para o ponto de distribuição. Você deve criar um arquivo de conteúdo de pré-teste que contém a nova versão do arquivo e, em seguida, extrair o conteúdo, atualizar o ponto de distribuição para distribuir os arquivos que foram alterados ou redistribuir todos os arquivos no pacote.  

###  <a name="bkmk_dpsiteserver"></a> Como pré-testar conteúdo no ponto de distribuição em um servidor do site  
 Quando houver um ponto de distribuição instalado em um servidor do site, use o procedimento a seguir para pré-configurar com êxito o conteúdo. Isso ocorre porque os arquivos de conteúdo já estão na biblioteca de conteúdo.  

 Quando o ponto de distribuição não estiver habilitado para pré-configurar o conteúdo, ou quando o ponto de distribuição não estiver localizado em um servidor do site, confira a seção [Usar conteúdo pré-teste](#bkmk_prestage) nesse tópico.  

##### <a name="to-prestage-content-on-distribution-points-located-on-a-site-server"></a>Para pré-configurar conteúdo nos pontos de distribuição localizados em um servidor do site  

1.  Siga as seguintes etapas para verificar se o ponto de distribuição não está habilitado para o conteúdo pré-configurado.  

    1.  No console do Configuration Manager, clique em **Administração**.  

    2.  No espaço de trabalho **Administração** , clique em **Pontos de Distribuição**, e então selecione o ponto de distribuição localizado no servidor do site.  

    3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

    4.  Na guia **Geral** , verifique se a caixa de seleção **Habilitar este ponto de distribuição para conteúdo pré-configurado** não está selecionada.  

2.  Crie o arquivo de conteúdo pré-testado usando a seção [Etapa 1: Criar um arquivo de conteúdo pré-teste](#BKMK_CreatePrestagedContentFile) nesse tópico.  

3.  Atribua o conteúdo ao ponto de distribuição usando a seção [Etapa 2: Atribuir o conteúdo a pontos de distribuição](#BKMK_AssignContentToDistributionPoint) neste tópico.  

4.  No servidor do site, extraia o conteúdo do arquivo de conteúdo pré-teste usando a seção [Etapa 3: Extrair o conteúdo do arquivo de conteúdo pré-teste](#BKMK_ExportContentFromPrestagedContentFile) neste tópico.  

    > [!NOTE]  
    >  Quando o ponto de distribuição estiver em um site secundário, aguarde pelo menos 10 minutos e, então, usando um console do Configuration Manager que está conectado a um site primário pai, atribua o conteúdo ao ponto de distribuição no site secundário.  

##  <a name="bkmk_manage"></a> Gerenciar o conteúdo que você distribuiu  
 Você tem as seguintes opções para gerenciar o conteúdo:  
 - [Atualizar conteúdo](#update-content)
 - [Redistribuir o conteúdo](#redistribute-content)
 - [Remover conteúdo](#remove-content)
 - [Validar o conteúdo](#validate-content)

### <a name="update-content"></a>Atualizar conteúdo
Quando o local do arquivo de origem para uma implantação é atualizado adicionando novos arquivos ou substitui arquivos existentes pode uma versão mais nova, é possível atualizar os arquivos de conteúdo em pontos de distribuição usando a ação **Atualizar Pontos de Distribuição** ou **Atualizar Conteúdo**:  
-   Os arquivos de conteúdo são copiados do caminho do arquivo de origem para a biblioteca de conteúdo no site que tem a fonte de conteúdo do pacote  
-   A versão do pacote é incrementada  
-   Cada instância da biblioteca de conteúdo em servidores do site e no ponto de distribuição é atualizada apenas com os arquivos alterados  

> [!WARNING]  
>  A versão do pacote de aplicativos é sempre 1. Ao atualizar o conteúdo para um tipo de implantação de aplicativo, o Configuration Manager cria uma nova ID de conteúdo para o tipo de implantação e o pacote faz referência à nova ID de conteúdo.  

#### <a name="to-update-content-on-distribution-points"></a>Para atualizar conteúdo em pontos de distribuição  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , selecione uma das seguintes etapas para o tipo de conteúdo que você quer distribuir:  

    -   **Aplicativos**: expanda **Gerenciamento de Aplicativos** > **Aplicativos** e selecione os aplicativos que você quer distribuir. Clique na guia **Tipos de Implantação** e selecione o tipo de implantação que você quer atualizar.  

    -   **Pacotes**: expanda **Gerenciamento de Aplicativos** > **Pacotes** e selecione os pacotes que deseja atualizar.  

    -   **Pacotes de Implantação**: expanda **Atualizações do Software** > **Pacotes de Implantação** e selecione os pacotes de implantação que deseja atualizar.  

    -   **Pacotes de Driver**: expanda **Sistemas Operacionais** > **Pacotes de Driver** e selecione os pacotes de driver que deseja atualizar.  

    -   **Imagens do Sistema Operacional**: expanda **Sistemas Operacionais** > **Imagens do Sistema Operacional** e selecione as imagens do sistema operacional que deseja atualizar.  

    -   **Instaladores do Sistema Operacional**: expanda **Sistemas Operacionais** > **Instaladores do Sistema Operacional** e selecione os instaladores do sistema operacional que deseja atualizar.  

    -   **Imagens de Inicialização**: expanda **Sistemas Operacionais** >  **Imagens de Inicialização** e selecione as imagens de inicialização que deseja atualizar.  

3.  Na guia **Início** , no grupo **Implantação** , clique em **Atualizar Pontos de Distribuição**e em **OK** para confirmar que você quer atualizar o conteúdo.  

    > [!NOTE]  
    >  Para atualizar o conteúdo de aplicativos, clique na guia **Tipos de Implantação** , clique com o botão direito no tipo de implantação, clique em **Atualizar Conteúdo**e em **OK** para confirmar que você quer atualizar o conteúdo.  

    > [!NOTE]  
    >  Quando você atualiza o conteúdo de imagens de inicialização, o Assistente para Gerenciar Pontos de Distribuição é aberto. Revise as informações na página **Resumo** e conclua o assistente para atualizar o conteúdo.  

### <a name="redistribute-content"></a>Redistribuir o conteúdo
Você pode redistribuir um pacote para copiar todos os arquivos de conteúdo do pacote para pontos de distribuição ou grupos de pontos de distribuição e, assim, substituir os arquivos existentes.  

 Use essa operação para reparar arquivos de conteúdo do pacote ou reenviar o conteúdo quando a distribuição inicial falha. Você pode redistribuir um pacote de:  

-   Propriedades do pacote  
-   Propriedades do ponto de distribuição  
-   Propriedades do grupo de pontos de distribuição.  


#### <a name="to-redistribute-content-from-package-properties"></a>Para redistribuir o conteúdo nas propriedades do pacote  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , selecione uma das seguintes etapas para o tipo de conteúdo que você quer distribuir:  

    -   **Aplicativos**: expanda **Gerenciamento de Aplicativos** >  **Aplicativos** e selecione o aplicativo que deseja redistribuir.  

    -   **Pacotes**: expanda **Gerenciamento de Aplicativos** > **Pacotes** e selecione o pacote que deseja redistribuir.  

    -   **Pacotes de Implantação**: expanda **Atualizações do Software** >  **Pacotes de Implantação** e selecione o pacote de implantação que deseja redistribuir.  

    -   **Pacotes de Driver**: expanda **Sistemas Operacionais** > **Pacotes de Driver** e selecione o pacote de driver que deseja redistribuir.  

    -   **Imagens do Sistema Operacional**: expanda **Sistemas Operacionais** > **Imagens do Sistema Operacional** e selecione a imagem do sistema operacional que deseja redistribuir.  

    -   **Instaladores do Sistema Operacional**: expanda **Sistemas Operacionais** > **Instaladores do Sistema Operacional** e selecione o instalador do sistema operacional que deseja redistribuir.  

    -   **Imagens de Inicialização**: expanda **Sistemas Operacionais** >  **Imagens de Inicialização** e selecione a imagem de inicialização que deseja redistribuir.  

3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Clique na guia **Locais de Conteúdo** , selecione o ponto de distribuição ou grupo de pontos de distribuição nos quais você quer redistribuir o conteúdo, clique em **Redistribuir**, e depois clique em **OK**.  

#### <a name="to-redistribute-content-from-distribution-point-properties"></a>Para redistribuir o conteúdo das propriedades do ponto de distribuição  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , clique em **Pontos de Distribuição**, depois selecione o ponto de distribuição no qual você quer redistribuir o conteúdo.  

3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Clique na guia **Conteúdo** , selecione o conteúdo a ser redistribuído, clique em **Redistribuir**, e depois clique em **OK**.  

#### <a name="to-redistribute-content-from-distribution-point-group-properties"></a>Para redistribuir o conteúdo das propriedades do grupo de pontos de distribuição  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , clique em **Grupos de Pontos de Distribuição**, depois selecione o grupo de pontos de distribuição no qual você quer redistribuir o conteúdo.  

3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Clique na guia **Conteúdo** , selecione o conteúdo a ser redistribuído, clique em **Redistribuir**, e depois clique em **OK**.  

    > [!IMPORTANT]  
    >  O conteúdo do pacote é redistribuído para todos os pontos de distribuição do grupo.  


#### <a name="use-the-sdk-to-force-replication-of-content"></a>Usar o SDK para forçar a replicação de conteúdo
Você pode usar o método de classe do WMI (Instrumentação de Gerenciamento do Windows) **RetryContentReplication** do SDK do Configuration Manager para forçar o Gerenciador de Distribuição a copiar conteúdo do local de origem para a biblioteca de conteúdo.  

Somente use esse método para forçar a replicação quando precisar redistribuir o conteúdo após haver problemas com a replicação de conteúdo normal (normalmente confirmada pelo uso do nó Monitoramento do console).   

Para obter mais informações sobre essa opção de SDK, consulte [RetryContentReplication Method in Class SMS_CM_UpdatePackages](https://msdn.microsoft.com/library/mt762092(CMSDK.16).aspx) (Método RetryContentReplication na classe SMS_CM_UpdatePackages) no MSDN.Microsoft.com.

### <a name="remove-content"></a>Remover conteúdo
Quando você não precisa mais de conteúdo em seus pontos de distribuição, pode remover os arquivos de conteúdo desses pontos.  

-   Propriedades do pacote  
-   Propriedades do ponto de distribuição  
-   Propriedades do grupo de pontos de distribuição.  

Porém, quando o conteúdo é associado a outro pacote que foi distribuído para o mesmo ponto de distribuição, não é possível remover o conteúdo.  

#### <a name="to-remove-package-content-files-from-distribution-points"></a>Para remover arquivos de conteúdo de pacote de pontos de distribuição  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , selecione uma das seguintes etapas para o tipo de conteúdo que você quer excluir:  

    -   **Aplicativos**: expanda **Gerenciamento de Aplicativos** > **Aplicativos** e selecione o aplicativo que deseja remover.  

    -   **Pacotes**: expanda **Gerenciamento de Aplicativos** > **Pacotes** e selecione o pacote que deseja remover.  

    -   **Pacotes de Implantação**: expanda **Atualizações do Software** > **Pacotes de Implantação** e selecione o pacote de implantação que deseja remover.  

    -   **Pacotes de Driver**: expanda **Sistemas Operacionais** > **Pacotes de Driver** e selecione o pacote de driver que deseja remover.  

    -   **Imagens do Sistema Operacional**: expanda **Sistemas Operacionais** > **Imagens do Sistema Operacional** e selecione a imagem do sistema operacional que deseja remover.  

    -   **Instaladores do Sistema Operacional**: expanda **Sistemas Operacionais** > **Instaladores do Sistema Operacional** e selecione o instalador do sistema operacional que deseja remover.  

    -   **Imagens de Inicialização**: expanda **Sistemas Operacionais** > **Imagens de Inicialização** e selecione a imagem de inicialização que deseja remover.  

3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Clique na guia **Locais de Conteúdo** , selecione o ponto de distribuição ou grupo de pontos de distribuição dos quais você quer remover o conteúdo, clique em **Remover**, e depois clique em **OK**.  

#### <a name="to-remove-package-content-from-distribution-point-properties"></a>Para remover o conteúdo do pacote das propriedades do ponto de distribuição  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , clique em **Pontos de Distribuição**, depois selecione o ponto de distribuição no qual você quer excluir o conteúdo.  

3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Clique na guia **Conteúdo** , selecione o conteúdo a ser removido, clique em **Remover**, e depois clique em **OK**.  

#### <a name="to-remove-content-from-distribution-point-group-properties"></a>Para remover o conteúdo das propriedades do grupo de pontos de distribuição  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , clique em **Grupos de Pontos de Distribuição**, depois selecione o grupo de pontos de distribuição do qual você quer remover o conteúdo.  

3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Clique na guia **Conteúdo** , selecione o conteúdo a ser removido, clique em **Remover**, e depois clique em **OK**.  


### <a name="validate-content"></a>Validar o conteúdo
O processo de validação de conteúdo verifica a integridade dos arquivos de conteúdo nos pontos de distribuição. É possível habilitar a validação de conteúdo em um agendamento ou então iniciar manualmente a validação de conteúdo a partir das propriedades dos pontos de distribuição e pacotes.  

 Quando o processo de validação de conteúdo começa, o Configuration Manager verifica os arquivos de conteúdo em pontos de distribuição e, se o hash do arquivo não é esperado para os arquivos no ponto de distribuição, o Configuration Manager cria uma mensagem de status que você pode examinar no espaço de trabalho **Monitoramento**.  

 Para mais informações sobre como configurar o agendamento de validação de conteúdo, confira [Distribution point configurations](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs) (Configurações do ponto de distribuição) no tópico [Install and configure distribution points for System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) (Instalar e configurar pontos de distribuição para o System Center Configuration Manager).  


#### <a name="to-initiate-content-validation-for-all-content-on-a-distribution-point"></a>Para iniciar a validação de conteúdo de todo o conteúdo em um ponto de distribuição  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , clique em **Pontos de Distribuição**e selecione o ponto de distribuição no qual você quer validar o conteúdo.  

3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Na guia **Conteúdo** , selecione o pacote no qual você quer validar o conteúdo, clique em **Validar**, **OK**e em **OK**. O processo de validação de conteúdo é iniciado para o pacote no ponto de distribuição.  

5.  Para exibir os resultados do processo de validação de conteúdo, no espaço de trabalho **Monitoramento** , expanda **Status da Distribuição**e clique no nó **Status do Conteúdo** . O conteúdo de cada tipo de pacote (por exemplo, aplicativo, pacote de atualização de software e imagem de inicialização) é exibido. Para mais informações sobre o monitoramento do status do conteúdo, confira [Monitorar o conteúdo que você distribuiu com o System Center Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

#### <a name="to-initiate-content-validation-for-a-package"></a>Para iniciar a validação de conteúdo para um pacote  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , selecione uma das seguintes etapas para o tipo de conteúdo que você quer validar:  

    -   **Aplicativos**: expanda **Gerenciamento de Aplicativos** > **Aplicativos** e selecione o aplicativo que deseja validar.  

    -   **Pacotes**: expanda **Gerenciamento de Aplicativos** > **Pacotes** e selecione o pacote que deseja validar.  

    -   **Pacotes de Implantação**: expanda **Atualizações do Software** > **Pacotes de Implantação** e selecione o pacote de implantação que deseja validar.  

    -   **Pacotes de Driver**: expanda **Sistemas Operacionais** > **Pacotes de Driver** e selecione o pacote de driver que deseja validar.  

    -   **Imagens do Sistema Operacional**: expanda **Sistemas Operacionais** > **Imagens do Sistema Operacional** e selecione a imagem do sistema operacional que deseja validar.  

    -   **Instaladores do Sistema Operacional**: expanda **Sistemas Operacionais** >  **Instaladores do Sistema Operacional** e selecione o instalador do sistema operacional que deseja validar.  

    -   **Imagens de Inicialização**: expanda **Sistemas Operacionais** > **Imagens de Inicialização** e selecione a imagem de inicialização que deseja pré-configurar.  

3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Na guia **Locais de Conteúdo** , selecione o ponto de distribuição ou grupo de pontos de distribuição no qual você quer validar o conteúdo, clique em **Validar**, **OK**e em **OK**. O processo de validação de conteúdo é iniciado para o conteúdo no ponto de distribuição ou grupo de pontos de distribuição selecionado.  

5.  Para exibir os resultados do processo de validação de conteúdo, no espaço de trabalho **Monitoramento** , expanda **Status da Distribuição**e clique no nó **Status do Conteúdo** . O conteúdo de cada tipo de pacote (por exemplo, aplicativo, pacote de atualização de software e imagem de inicialização) é exibido. Para mais informações sobre o monitoramento do status do conteúdo, confira [Monitorar o conteúdo que você distribuiu com o System Center Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  
