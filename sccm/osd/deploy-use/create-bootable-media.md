---
title: Criar mídia inicializável
titleSuffix: Configuration Manager
description: Mídias inicializáveis no Configuration Manager facilitam a instalação de uma nova versão do Windows ou substituir um computador e transferir as configurações.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d3b2ce474488ebf02c3a3c4a82def91d706b6bfc
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351016"
---
# <a name="create-bootable-media-with-system-center-configuration-manager"></a>Criar uma mídia inicializável com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Mídias inicializáveis no Configuration Manager contém a imagem de inicialização, comandos prestart opcionais e arquivos associados, além dos arquivos do Configuration Manager. Use mídia pré-testada para os seguintes cenários de implantação de sistema operacional:  

-   [Instalar uma nova versão do Windows em um novo computador (sem sistema operacional)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Substituir um computador existente e transferir configurações](replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="BKMK_CreateBootableMedia"></a> Criar mídia inicializável  
 Quando você inicializa a mídia inicializável, o computador de destino é iniciado, conecta-se à rede e recupera a sequência de tarefas especificada, a imagem do sistema operacional e qualquer outro conteúdo necessário da rede. Como a sequência de tarefa não está na mídia, você pode alterar a sequência de tarefas ou o conteúdo sem precisar recriar a mídia. Os pacotes em mídia inicializável não são criptografados. Você deve tomar as medidas de segurança apropriadas, como adicionar uma senha à mídia, para verificar se o conteúdo do pacote está protegido contra usuários não autorizados.  

 Antes de criar mídia inicializável usando o Assistente para Criar Mídia de Sequência de Tarefas, verifique se as seguintes condições foram atendidas:  

|Tarefa|Descrição|  
|----------|-----------------|  
|Imagem de inicialização|Considere o seguinte sobre a imagem de inicialização que você usará na sequência de tarefas para implantar o sistema operacional:<br /><br /> -   A arquitetura da imagem de inicialização deve ser apropriada para a arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode iniciar e executar uma imagem de inicialização x86 ou x64. No entanto, um computador de destino x86 pode iniciar e executar apenas uma imagem de inicialização x86.<br />-   Verifique se a imagem de inicialização contém os drivers de rede e armazenamento em massa necessários para provisionar o computador de destino.|  
|Criar uma sequência de tarefas para implantar um sistema operacional|Como parte da mídia inicializável, você deve especificar a sequência de tarefas para implantar o sistema operacional. Para ver as etapas para criar uma nova sequência de tarefas, consulte [Criar uma sequência de tarefas para instalar um sistema operacional](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md).|  
|Distribuir todo o conteúdo associado à sequência de tarefas|Você deve distribuir todo o conteúdo exigido pela sequência de tarefas para pelo menos um ponto de distribuição. Isso inclui a imagem de inicialização e outros arquivos de pré-inicialização associados. O assistente reúne as informações do ponto de distribuição quando ele cria a mídia inicializável. Você precisa ter direitos de acesso de **Leitura** à biblioteca de conteúdo no ponto de distribuição.  Para obter detalhes, consulte [Sobre a biblioteca de conteúdo](../../core/plan-design/hierarchy/the-content-library.md).|  
|Preparar a unidade USB removível|Para uma unidade USB removível:<br /><br /> Se você pretende usar uma unidade USB removível, a unidade USB deve ser conectada ao computador no qual o assistente é executado e a unidade USB deve ser detectável pelo Windows como um dispositivo de remoção. O assistente grava diretamente na unidade USB ao criar a mídia. A mídia autônoma usa um sistema de arquivos FAT32. Não é possível criar uma mídia autônoma em uma unidade flash USB cujo conteúdo contém um arquivo de tamanho superior a 4 GB.|  
|Criar uma pasta de saída|Para um conjunto de CD/DVD:<br /><br /> Para executar o Assistente para Criar Mídia de Sequência de Tarefas para criar mídia para um conjunto de CD ou DVD, é preciso criar uma pasta para os arquivos de saída criados pelo assistente. A mídia criada para um conjunto de CD ou DVD é gravada como arquivos .iso diretamente na pasta.|  

 Use o procedimento a seguir para criar mídia inicializável.  

### <a name="to-create-bootable-media"></a>Para criar mídia inicializável  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Sequências de Tarefas**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Mídia de Sequência de Tarefas** para iniciar o Assistente para Criar Mídia de Sequência de Tarefas.  

4.  Na página **Selecionar o Tipo de Mídia** , especifique as opções a seguir e clique em **Próximo**.  

    -   Selecione **Mídia inicializável**.  

    -   Opcionalmente, se você quiser permitir que o sistema operacional seja implantado sem a necessidade de entrada do usuário, selecione **Permitir implantação autônoma do sistema operacional**.  

        > [!IMPORTANT]  
        >  Quando você seleciona essa opção, o usuário não precisa inserir informações de configuração de rede nem sequências de tarefas opcionais. No entanto, ainda será solicitada ao usuário uma senha, se a mídia estiver configurada para proteção por senha.  

5.  Na página **Gerenciamento de Mídia** , especifique uma das seguintes opções e clique em **Próximo**.  

    -   Selecione **Mídia dinâmica** se quiser permitir que um ponto de gerenciamento redirecione a mídia para outro ponto de gerenciamento, baseado no local do cliente nos limites do site.  

    -   Selecione **Mídia de site** se quiser que a mídia tenha contato apenas com o ponto de gerenciamento especificado.  

6.  Na página **Tipo de Mídia** , especifique se a mídia é uma unidade flash ou um conjunto de CD/DVD e clique em configurar o seguinte:  

    > [!IMPORTANT]  
    >  A mídia autônoma usa um sistema de arquivos FAT32. Não é possível criar uma mídia autônoma em uma unidade flash USB cujo conteúdo contém um arquivo de tamanho superior a 4 GB.  

    -   Se você selecionar a **Unidade flash USB**, especifique a unidade na qual deseja armazenar o conteúdo.  

    -   Caso selecione **Conjunto de CD/DVD**, especifique a capacidade da mídia, o nome e o caminho dos arquivos de saída. O assistente grava os arquivos de saída nesse local. Por exemplo: **\\\nomedoservidor\pasta\arquivodesaida.iso**  

         Se a capacidade da mídia for muito pequena para armazenar todo o conteúdo, vários arquivos são criados e você deve armazenar o conteúdo em vários CDs ou DVDs. Se várias mídias forem necessárias, o Configuration Manager adicionará um número de sequência ao nome de cada arquivo de saída criado. Além disso, se você implantar um aplicativo juntamente com o sistema operacional e o aplicativo não couber em uma única mídia, o Configuration Manager armazenará o aplicativo em várias mídias. Quando a mídia autônoma é executada, o Configuration Manager solicita ao usuário a próxima mídia, na qual o aplicativo está armazenado.  

        > [!IMPORTANT]  
        >  Se você selecionar uma imagem .iso existente, o Assistente de Mídia de Sequência de Tarefas excluirá essa imagem da unidade ou do compartilhamento assim que você prosseguir para a próxima página do assistente. A imagem existente será excluída mesmo se você cancelar o assistente.  

     Clique em **Avançar**.  

7.  Na página **Segurança** , especifique as opções a seguir e clique em **Próximo**.  

    -   Marque a caixa de seleção **Habilitar suporte a computadores desconhecidos** para permitir que a mídia implante um sistema operacional em um computador não gerenciado pelo Configuration Manager. Não há registro desses computadores no banco de dados do Configuration Manager.  

         Computadores desconhecidos incluem:  

        -   Um computador no qual o cliente do Configuration Manager não está instalado  

        -   Um computador que não foi importado para o Configuration Manager  

        -   Um computador não descoberto pelo Configuration Manager  

    -   Marque a caixa de seleção **Proteger mídia com senha** e digite uma senha forte como auxílio para proteger a mídia contra o acesso não autorizado. Quando você especificar uma senha, o usuário deverá fornecer essa senha para usar a mídia inicializável.  

        > [!IMPORTANT]  
        >  Como prática recomendada de segurança, atribua sempre uma senha para ajudar a proteger a mídia inicializável.  

    -   Para comunicações HTTP, selecione **Criar certificado de mídia autoassinado**e especifique as datas de início e vencimento do certificado.  

    -   Para comunicações HTTPS, selecione **Importar certificado PKI**e especifique o certificado a ser importado e a respectiva senha.  

         Para obter mais informações sobre o certificado de cliente que é usado para imagens de inicialização, consulte [Requisitos do certificado PKI](../../core/plan-design/network/pki-certificate-requirements.md).  

    -   **Afinidade de Dispositivo de Usuário**: para dar suporte ao gerenciamento centrado no usuário no Configuration Manager, especifique como você quer que a mídia associe usuários ao computador de destino. Para obter mais informações sobre como a implantação de sistema operacional dá suporte à afinidade de dispositivo de usuário, consulte [Associar usuários a um computador de destino](../get-started/associate-users-with-a-destination-computer.md).  

        -   Especifique **Permitir afinidade de dispositivo de usuário com aprovação automática** se você quiser que a mídia associe automaticamente os usuários ao computador de destino. Essa funcionalidade é baseada nas ações da sequência de tarefas que implanta o sistema operacional. Nesse cenário, a sequência de tarefas cria uma relação entre os usuários especificados e o computador de destino quando implanta o sistema operacional no computador de destino.  

        -   Especifique **Permitir afinidade de dispositivo de usuário pendente de aprovação de administrador** se você quiser que a mídia associe os usuários ao computador de destino após a aprovação ser concedida. Essa funcionalidade é baseada no escopo da sequência de tarefas que implanta o sistema operacional.  Neste cenário, a sequência de tarefas cria uma relação entre os usuários especificados e o computador de destino, mas aguarda a aprovação de um usuário administrativo antes da implantação do sistema operacional.  

        -   Especifique **Não permitir afinidade de dispositivo de usuário** se você quiser que a mídia associe os usuários ao computador de destino. Neste cenário, a sequência de tarefas não associa os usuários ao computador de destino quando implanta o sistema operacional.  

8.  Na página **Imagem de inicialização** , especifique as opções a seguir e clique em **Próximo**.  

    > [!IMPORTANT]  
    >  A arquitetura da imagem de inicialização distribuída deve ser apropriada para a arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode iniciar e executar uma imagem de inicialização x86 ou x64. No entanto, um computador de destino x86 pode iniciar e executar apenas uma imagem de inicialização x86.  

    -   Na caixa **Imagem de inicialização** , especifique a imagem de inicialização para iniciar o computador de destino.  

    -   Na caixa **Ponto de distribuição** , especifique o ponto de distribuição onde a imagem de inicialização reside. O assistente recupera a imagem de inicialização do ponto de distribuição e a grava na mídia.  

        > [!NOTE]  
        >  É necessário ter direitos de acesso de **Leitura** à biblioteca de conteúdo no ponto de distribuição.  

    -   Se você criar uma mídia inicializável baseada em site na página **Gerenciamento de Mídia** do assistente, especifique um ponto de gerenciamento de um site primário na caixa **Ponto de gerenciamento** .  

    -   Se você criar uma mídia inicializável dinâmica na página **Gerenciamento de Mídia** do assistente, especifique os pontos de gerenciamento do site primário a serem usados e uma ordem de prioridade para as comunicações iniciais em **Pontos de gerenciamento associados**.  

9. Na página **Personalização** , especifique as seguintes opções e clique em **Próximo**.  

    -   Especifique as variáveis que a sequência de tarefas usa para implantar o sistema operacional.  

    -   Especifique os comandos prestart que deseja executar antes de executar a sequência de tarefas. Os comandos prestart são um script ou um executável que podem interagir com o usuário no Windows PE antes da execução da sequência de tarefas para instalar o sistema operacional. Para mais informações, consulte [Comandos prestart para mídia de sequência de tarefas](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        >  Durante a criação de mídia de sequência de tarefas, a sequência de tarefas grava a ID do pacote e a linha de comando prestart, que inclui o valor de quaisquer variáveis de sequência de tarefas, no arquivo de log CreateTSMedia.log no computador que executa o console do Configuration Manager. Você poderá analisar esse arquivo de log para verificar o valor das variáveis de sequência de tarefas.  

         Opcionalmente, marque a caixa de seleção **Arquivos no comando prestart** para incluir quaisquer arquivos necessários no comando prestart.  

10. Conclua o assistente.  

## <a name="create-bootable-media-on-a-usb-drive-from-a-network-share"></a>Criar uma mídia inicializável em uma unidade USB de um compartilhamento de rede
As informações nesta seção ajudam a criar mídia inicializável em uma unidade flash USB quando a unidade flash não está conectada ao computador que executa o console do Configuration Manager. Para criar a mídia inicializável na unidade USB, você pode criar uma mídia de inicialização de sequência de tarefas, montar o ISO e transferir os arquivos do ISO para a unidade USB.

1. [Criar a mídia de inicialização de sequência de tarefas](#to-create-task-boobable-media). Na página **Tipo de mídia**, selecione **Conjunto de CD/DVD**. O assistente grava os arquivos de saída no local que você especificar. Por exemplo: **\\\nomedoservidor\pasta\arquivodesaida.iso**.  
2. Preparar a unidade USB removível. A unidade deve estar formatada, vazia e inicializável.
3. Monte o ISO do local de compartilhamento e transfira os arquivos do ISO para a unidade USB.

## <a name="next-steps"></a>Próximas etapas  
[Use a mídia inicializável para implantar o Windows na rede](use-bootable-media-to-deploy-windows-over-the-network.md)  
