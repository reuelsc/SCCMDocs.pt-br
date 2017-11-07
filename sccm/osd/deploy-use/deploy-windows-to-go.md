---
title: Implantar o Windows to Go
titleSuffix: Configuration Manager
description: "Saiba como provisionar o Windows To Go no System Center Configuration Manager para criar um espaço de trabalho do Windows To Go que é inicializado de uma unidade externa."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8eed50f5-80a4-422e-8aa6-a7ccb2171475
caps.latest.revision: "8"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 91e3fa4aba93dc3012fe1e702f50c4f9438a69e8
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="deploy-windows-to-go-with-system-center-configuration-manager"></a>Implantar o Windows to Go com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico fornece as etapas para provisionar o Windows To Go no System Center Configuration Manager. O Windows To Go é um recurso para empresas do Windows 8 que permite a criação de um espaço de trabalho do Windows To Go que pode ser inicializado a partir de uma unidade conectada por USB em computadores que atendem aos requisitos de certificação do Windows 7 ou do Windows 8, independentemente do sistema operacional em execução no computador. Os espaços de trabalho do Windows To Go podem usar a mesma imagem que as empresas usam para seus desktops e laptops e podem ser gerenciados da mesma forma.  

 Para obter mais informações sobre o Windows To Go, consulte [Visão geral do recurso Windows To Go](http://go.microsoft.com/fwlink/p/?LinkId=263433).  

## <a name="provision-windows-to-go"></a>Provisionar o Windows To Go  
 O Windows To Go é um sistema operacional armazenado em uma unidade externa conectada por USB. Você pode provisionar a unidade do Windows To Go basicamente da mesma forma que provisiona outras implantações de sistema operacional. No entanto, como o Windows To Go é desenvolvido para ser uma solução centrada no usuário e altamente móvel, você deve adotar uma abordagem ligeiramente diferente para provisionar essas unidades.  

 Em um nível superior, o Windows To Go é uma implantação de duas fases que permite configurar o dispositivo com Windows To Go e o conteúdo de pré-teste para a implantação do sistema operacional. É possível conseguir isso com o mínimo de impacto para o usuário e limitar o tempo de inatividade para o computador do usuário. Depois de pré-configurar o computador, é necessário concluir o processo de provisionamento para garantir que o computador esteja pronto para o usuário. O processo de provisionamento é similar ao processo de implantação de sistema operacional atual. O fluxo de trabalho geral para o conteúdo de pré-teste e provisionar o Windows To Go está listado abaixo:  

1.  [Pré-requisitos para provisionar o Windows To Go](#BKMK_Prereqs)  

2.  [Criar mídia pré-configurada](#BKMK_CreatePrestagedMedia)  

3.  [Criar um pacote do Windows To Go Creator](#BKMK_CreatePackage)  

4.  [Atualizar a sequência de tarefas para habilitar o BitLocker para o Windows To Go](#BKMK_UpdateTaskSequence)  

5.  [Implantar o pacote do Windows To Go Creator e a sequência de tarefas](#BKMK_Deployments)  

6.  [O usuário executa o Windows To Go Creator](#BKMK_UserExperience)  

7.  [O Configuration Manager configura e prepara a unidade do Windows To Go](#BKMK_ConfigureStageDrive)  

8.  [O usuário faz logon no Windows 8](#BKMK_UserLogsIn)  

###  <a name="BKMK_Prereqs"></a> Pré-requisitos para provisionar o Windows To Go  
 Antes de provisionar o Windows To Go, é necessário concluir o seguinte no Configuration Manager:  

-   **Distribuir uma imagem de inicialização para um ponto de distribuição**  

     Antes de criar uma mídia em pré-teste, é necessário distribuir a imagem de inicialização para um ponto de distribuição.  

    > [!NOTE]  
    >  As imagens de inicialização são usadas para instalar o sistema operacional nos computadores de destino em seu ambiente do Configuration Manager. Elas contêm uma versão do Windows PE que instala o sistema operacional, bem como todos os drivers de dispositivo adicionais necessários. O Configuration Manager fornece duas imagens de inicialização: uma para dar suporte a plataformas x86 e outra para dar suporte a plataformas x64. Você também pode criar suas próprias imagens de inicialização. Para obter mais informações, consulte [Gerenciar imagens de inicialização](../get-started/manage-boot-images.md).  

-   **Distribuir a imagem do sistema operacional Windows 8 para um ponto de distribuição**  

     Antes de criar uma mídia em pré-teste, é necessário distribuir a imagem do sistema operacional Windows 8 para um ponto de distribuição.  

    > [!NOTE]  
    >  As imagens do sistema operacional são arquivos em formato .WIM e representam uma coleção compactada de arquivos e pastas de referência necessários para instalar e configurar com êxito um sistema operacional em um computador. Para obter mais informações, consulte [Gerenciar imagens do sistema operacional](../get-started/manage-operating-system-images.md).  

-   **Criar uma sequência de tarefas para implantar o Windows 8**  

     É necessário criar uma sequência de tarefas para uma implantação do Windows 8 que você irá referenciar ao criar mídia em pré-teste. Para obter mais informações, consulte [Gerenciar sequências de tarefas para automatizar tarefas](manage-task-sequences-to-automate-tasks.md).  

###  <a name="BKMK_CreatePrestagedMedia"></a> Criar mídia pré-configurada  
 A mídia em pré-teste contém a imagem de inicialização usada para iniciar o computador de destino e a imagem do sistema operacional aplicada ao computador de destino. O computador provisionado com média em pré-teste pode ser iniciado usando a imagem de inicialização. Em seguida, o computador pode executar uma sequência de tarefas de implantação de sistema operacional existente para instalar uma implantação de sistema operacional completa. A sequência de tarefas que implanta o sistema operacional não está incluída na mídia.  

 É possível adicionar conteúdo, como aplicativos e drivers de dispositivo, além da imagem do sistema operacional e da imagem de inicialização durante a fase de pré-configuração. Isso reduz o tempo que demora para implantar um sistema operacional e reduz o tráfego de rede porque o conteúdo já está na unidade.  

 Use o procedimento a seguir para criar a mídia em pré-teste.  

#### <a name="to-create-prestaged-media"></a>Para criar mídia em pré-teste  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Sequências de Tarefas**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Mídia de Sequência de Tarefas** para iniciar o Assistente para Criar Mídia de Sequência de Tarefas.  

4.  Na página **Selecionar o Tipo de Mídia** , especifique as informações a seguir e clique em **Próximo**.  

    -   Selecione **Mídia em pré-teste**.  

    -   Selecione **Permitir implantação autônoma do sistema operacional** para iniciar a implantação do Windows To Go sem a interação do usuário.  

        > [!IMPORTANT]  
        >  Quando você usa essa opção com a variável personalizada SMSTSPreferredAdvertID (configurada posteriormente neste procedimento), nenhuma interação do usuário é necessária e o computador iniciará automaticamente a implantação do Windows To Go quando detectar uma unidade do Windows To Go. O usuário ainda deverá digitar uma senha se a mídia estiver configurada para proteção por senha. Se você usar a configuração **Permitir implantação autônoma do sistema operacional** sem configurar a variável SMSTSPreferredAdvertID, ocorrerá um erro quando você implantar a sequência de tarefas.  

5.  Na página **Gerenciamento de Mídia** , especifique as informações a seguir e clique em **Próximo**.  

    -   Selecione **Mídia dinâmica** se quiser permitir que um ponto de gerenciamento redirecione a mídia para outro ponto de gerenciamento, baseado no local do cliente nos limites do site.  

    -   Selecione **Mídia de site** se quiser que a mídia tenha contato apenas com o ponto de gerenciamento especificado.  

6.  Na página **Propriedades de mídia**  , especifique as informações a seguir e clique em **Próximo**.  

    -   **Criado por**: especifique quem criou a mídia.  

    -   **Versão**: especifique o número de versão da mídia.  

    -   **Comentário**: especifique uma descrição exclusiva da finalidade da mídia.  

    -   **Arquivo de mídia**: especifique o nome e o caminho dos arquivos de saída. O assistente grava os arquivos de saída nesse local. Por exemplo: **\\\nomedoservidor\pasta\arquivodesaída.wim**  

7.  Na página **Segurança** , especifique as informações a seguir e clique em **Próximo**.  

    -   Selecione **Habilitar suporte a computadores desconhecidos** para permitir que a mídia implante um sistema operacional em um computador não gerenciado pelo Configuration Manager. Não há registro desses computadores no banco de dados do Configuration Manager. Computadores desconhecidos incluem:  

        -   Um computador no qual o cliente do Configuration Manager não está instalado  

        -   Um computador que não foi importado para o Configuration Manager  

        -   Um computador não descoberto pelo Configuration Manager  

    -   Selecione **Proteger mídia com senha** e digite uma senha forte para ajudar a proteger a mídia contra o acesso não autorizado. Quando você especificar uma senha, o usuário deverá fornecer essa senha para usar a mídia em pré-teste.  

        > [!IMPORTANT]  
        >  Como prática recomendada de segurança, atribua sempre uma senha para ajudar a proteger a mídia em pré-teste.  

        > [!NOTE]  
        >  Quando você protege a mídia em pré-teste com uma senha, o usuário deve digitá-la mesmo quando a mídia estiver configurada com a opção **Permitir implantação autônoma do sistema operacional** .  

    -   Para comunicações HTTP, selecione **Criar certificado de mídia autoassinado**e especifique as datas de início e vencimento do certificado.  

    -   Para comunicações HTTPS, selecione **Importar certificado PKI**e especifique o certificado a ser importado e a respectiva senha.  

         Para obter mais informações sobre o certificado de cliente que é usado para imagens de inicialização, consulte [Requisitos do certificado PKI](../../core/plan-design/network/pki-certificate-requirements.md).  

    -   **Afinidade de Dispositivo de Usuário**: para dar suporte ao gerenciamento centrado no usuário no Configuration Manager, especifique como você quer que a mídia associe usuários ao computador de destino. Para obter mais informações sobre como a implantação de sistema operacional dá suporte à afinidade de dispositivo de usuário, consulte [Associar usuários a um computador de destino](../get-started/associate-users-with-a-destination-computer.md).  

        -   Especifique **Permitir afinidade de dispositivo de usuário com aprovação automática** se você quiser que a mídia associe automaticamente os usuários ao computador de destino. Essa funcionalidade é baseada nas ações da sequência de tarefas que implanta o sistema operacional. Nesse cenário, a sequência de tarefas cria uma relação entre os usuários especificados e o computador de destino quando implanta o sistema operacional no computador de destino.  

        -   Especifique **Permitir afinidade de dispositivo de usuário pendente de aprovação de administrador** se você quiser que a mídia associe os usuários ao computador de destino após a aprovação ser concedida. Essa funcionalidade é baseada no escopo da sequência de tarefas que implanta o sistema operacional. Neste cenário, a sequência de tarefas cria uma relação entre os usuários especificados e o computador de destino, mas aguarda a aprovação de um usuário administrativo antes da implantação do sistema operacional.  

        -   Especifique **Não permitir afinidade de dispositivo de usuário** se você quiser que a mídia associe os usuários ao computador de destino. Neste cenário, a sequência de tarefas não associa os usuários ao computador de destino quando implanta o sistema operacional.  

8.  Na página **Sequência de Tarefas** , especifique a sequência de tarefas do Windows 8 criada na seção anterior.  

9. Na página **Imagem de inicialização** , especifique as informações a seguir e clique em **Próximo**.  

    > [!IMPORTANT]  
    >  A arquitetura da imagem de inicialização distribuída deve ser apropriada para a arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode iniciar e executar uma imagem de inicialização x86 ou x64. No entanto, um computador de destino x86 pode iniciar e executar apenas uma imagem de inicialização x86. Para os computadores certificados pelo Windows 8 no modo EFI, é preciso usar uma imagem de inicialização x64.  

    -   **Imagem de inicialização**: especifique a imagem de inicialização para iniciar o computador de destino.  

    -   **Ponto de distribuição**: especifique o ponto de distribuição que hospeda a imagem de inicialização. O assistente recupera a imagem de inicialização do ponto de distribuição e a grava na mídia.  

        > [!NOTE]  
        >  O usuário administrativo deve ter direitos de acesso para **Ler** o conteúdo da imagem de inicialização no ponto de distribuição. Para mais informações, consulte [Gerenciar contas para acessar o conteúdo](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).  

    -   Se você selecionar **Mídia de site** na página **Gerenciamento de Mídia** desse assistente, na caixa **Ponto de gerenciamento** , especifique um ponto de gerenciamento de um site primário.  

    -   Se você selecionar **Mídia dinâmica** na página **Gerenciamento de Mídia** do assistente, na caixa **Pontos de gerenciamento associados** , especifique os pontos de gerenciamento do site primário a serem usados e uma ordem de prioridade para as comunicações iniciais.  

10. Na página **Imagens** , especifique as informações a seguir e clique em **Próximo**.  

    -   **Pacote de imagem**: especifique o pacote que contém a imagem do sistema operacional Windows 8.  

    -   **Índice de imagem**: especifique a imagem a ser implantada se o pacote contiver várias imagens de sistemas operacionais.  

    -   **Ponto de distribuição**: especifique o ponto de distribuição que hospeda o pacote da imagem do sistema operacional. O assistente recupera a imagem do sistema operacional do ponto de distribuição e a grava na mídia.  

        > [!NOTE]  
        >  O usuário administrativo deve ter direitos de acesso para **Ler** o conteúdo da imagem do sistema operacional no ponto de distribuição. Para mais informações, consulte [Gerenciar contas para acessar o conteúdo](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).  

11. Na página **Selecionar Aplicativo** , selecione o conteúdo do aplicativo a ser incluído no arquivo de mídia e clique em **Próximo**.  

12. Na página **Selecionar Pacote** , selecione o conteúdo do pacote adicional a ser incluído no arquivo de mídia e clique em **Próximo**.  

13. Na página **Selecionar Pacote** , selecione o conteúdo do pacote de drivers a ser incluído no arquivo de mídia e clique em **Próximo**.  

14. Na página **Pontos de Distribuição** , selecione um ou mais pontos de distribuição que possuem o conteúdo exigido pela sequência de tarefas e clique em **Próximo**.  

15. Na página **Personalização** , especifique as informações a seguir e clique em **Próxima**.  

    -   **Variáveis**: especifique as variáveis que a sequência de tarefas usa para implantar o sistema operacional. Para o Windows To Go, use a variável SMSTSPreferredAdvertID para selecionar automaticamente a disposição do Windows To Go usando o seguinte formato:  

         SMSTSPreferredAdvertID = {*IDImplantação*}, onde IDImplantação corresponde à ID de implantação associada à sequência de tarefas que você usa para concluir o processo de provisionamento para a unidade do Windows To Go.  

        > [!TIP]  
        >  Ao usar essa variável com uma sequência de tarefas que está configurada para executar de forma autônoma (configurada anteriormente neste procedimento), nenhuma interação do usuário é necessária e o computador inicia automaticamente a implantação do Windows To Go quando detecta uma unidade do Windows To Go. O usuário ainda deverá digitar uma senha se a mídia estiver configurada para proteção por senha.  

    -   **Comandos prestart**: especifique os comandos prestart que deseja executar antes de executar a sequência de tarefas. Os comandos prestart podem ser um script ou executável que podem interagir com o usuário no Windows PE antes da execução da sequência de tarefas para instalar o sistema operacional. Configure o seguinte para a implantação do Windows To Go:  

        -   **OSDBitLockerPIN**: o BitLocker para Windows To Go requer uma senha. Defina a variável **OSDBitLockerPIN** como parte de um comando prestart para definir a senha do BitLocker para a unidade do Windows To Go.  

            > [!WARNING]  
            >  Após habilitar o BitLocker para a senha, o usuário deverá inserir a senha a cada vez que o computador for inicializado para a unidade do Windows To Go.  

        -   **SMSTSUDAUsers**: especifica o usuário principal do computador de destino. Use essa variável para coletar o nome de usuário, que pode ser usado para associar o usuário e o dispositivo. Para mais informações, consulte [Associar usuários a um computador de destino](../get-started/associate-users-with-a-destination-computer.md).  

            > [!TIP]  
            >  Para recuperar o nome de usuário, você pode criar uma caixa de entrada como parte do comando prestart, pedir ao usuário para inserir seu nome de usuário e definir a variável com o valor. Por exemplo, você pode adicionar as seguintes linhas no arquivo de script do comando prestart:  
            >   
            >  `UserID = inputbox("Enter Username" ,"Enter your username:","",400,0)`  
            >   
            >  `env("SMSTSUDAUsers") = UserID`  

         Para obter mais informações sobre como criar um arquivo de script para ser usado como comando prestart, consulte [Comandos prestart para mídia de sequência de tarefas](../understand/prestart-commands-for-task-sequence-media.md).  

16. Conclua o assistente.  

    > [!NOTE]  
    >  Pode levar um longo período de tempo para que o assistente conclua o arquivo de mídia em pré-teste.  

###  <a name="BKMK_CreatePackage"></a> Criar um pacote do Windows To Go Creator  
 Como parte da implantação do Windows To Go, é necessário criar um pacote para implantar o arquivo de mídia em pré-teste. O pacote deve incluir a ferramenta que configura a unidade do Windows To Go e extrai a mídia em pré-teste na unidade. Use o procedimento a seguir para criar o pacote do Windows To Go.  

#### <a name="to-create-the-windows-to-go-creator-package"></a>Para criar o pacote do Windows To Go Creator  

1.  No servidor que hospeda os arquivos do pacote do Windows To Go Creator, crie uma pasta de origem para os arquivos de origem do pacote.  

    > [!NOTE]  
    >  A conta de computador do servidor do site deve ter direitos de acesso de **Leitura** para a pasta de origem.  

2.  Copie o arquivo de mídia em pré-teste criado na seção [Create prestaged media](#BKMK_CreatePrestagedMedia) na pasta de origem do pacote.  

3.  Copie a ferramenta Windows To Go Creator (WTGCreator.exe) na pasta de origem do pacote. A ferramenta do criador está disponível em qualquer servidor do site primário no seguinte local: <*ConfigMgrInstallationFolder*>\OSD\Tools\WTG\Creator.  

4.  Crie um pacote e um programa usando o Assistente para Criar Pacote e Programa.  

5.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

6.  No espaço de trabalho **Biblioteca de Software** , expanda o **Gerenciamento de Aplicativos**e clique em **Pacotes**.  

7.  Na guia **Início** , no grupo **Criar** , clique em **Criar Pacote**.  

8.  Na página **Pacote** , especifique o nome e a descrição do pacote. Por exemplo, digite **Windows To Go** para o nome do pacote e especifique **Package to configure a Windows To Go drive using System Center Configuration Manager** para a descrição do pacote.  

9. Selecione **Este pacote contém arquivos de origem**, especifique o caminho para a pasta de origem do pacote criada na etapa 1 e clique em **Próximo**.  

10. Na página **Tipo de Programa** , selecione **Programa padrão**e clique em **Próximo**.  

11. Na página **Programa padrão** , especifique o seguinte:  

    -   **Nome**: especifique o nome do programa. Por exemplo, digite **Creator** para o nome do programa.  

    -   **Linha de Comando**: digite **WTGCreator.exe /wim:PrestageName.wim**, onde PrestageName corresponde ao nome do arquivo em pré-teste criado e copiado na pasta de origem do pacote do pacote do Windows To Go Creator.  

         Ou então, você pode adicionar as seguintes opções:  

        -   **enableBootRedirect**: opção de linha de comando para alterar as opções de inicialização do Windows To Go para permitir o redirecionamento de inicialização. Ao usar essa opção, o computador será inicializado a partir da USB sem ter que alterar a ordem de inicialização no firmware do computador ou, então, peça para o usuário selecionar uma entre as opções da lista disponível durante a inicialização. Se uma unidade do Windows To Go for detectada, o computador será inicializado a partir dessa unidade.  

    -   **Executar**: especifique **Normal** para executar o programa com base nos padrões do sistema e do programa.  

    -   **O programa pode ser executado**: especifique se o programa pode ser executado somente quando um usuário fizer logon.  

    -   **Modo de execução**: especifique se o programa será executado com as permissões de usuários registrados ou com permissões administrativas. O Windows To Go Creator requer permissões elevadas para ser executado.  

    -   Selecione **Permitir que os usuários exibam e interajam com o programa de instalação**e clique em **Próximo**.  

12. Na página Requisitos, especifique o seguinte:  

    -   **Requisitos de plataforma**: selecione as plataformas aplicáveis do Windows 8 para permitir o provisionamento.  

    -   **Espaço em disco estimado**: especifique o tamanho da pasta de origem do pacote para o Windows To Go Creator.  

    -   **Tempo de execução máximo permitido (minutos):**especifica o tempo máximo que o programa está previsto para ser executado no computador do cliente. Por padrão, esse valor é definido como 120 minutos.  

        > [!IMPORTANT]  
        >  Se você estiver usando janelas de manutenção para a coleção em que esse programa é executado, poderá ocorrer um conflito se o **Tempo de execução máximo permitido** for maior do que o tempo da janela de manutenção agendada. Se o tempo de execução máximo for definido como **Desconhecido**, ele será iniciado durante a janela de manutenção, mas continuará sendo executado até que seja concluído ou que ocorra uma falha após a janela de manutenção ser fechada. Se você definir o tempo de execução máximo para um período específico (não definido como Desconhecido) que exceda a duração de qualquer janela de manutenção disponível, esse programa não será executado.  

        > [!NOTE]  
        >  Se o valor for definido como **Desconhecido**, o Configuration Manager definirá o tempo de execução máximo permitido para 12 horas (720 minutos).  

        > [!NOTE]  
        >  Se o tempo de execução máximo (definido pelo usuário ou como o valor padrão) for excedido, o Configuration Manager interromperá o programa se **Executar com direitos administrativos** for selecionado e **Permitir que os usuários exibam e interajam com o programa de instalação** não estiver selecionado na página **Programa Padrão**.  

     Clique em **Próximo** e conclua o assistente.  

###  <a name="BKMK_UpdateTaskSequence"></a> Atualizar a sequência de tarefas para habilitar o BitLocker para o Windows To Go  
 O Windows To Go habilita o BitLocker em uma unidade inicializável externa sem o uso do TPM. Portanto, é necessário usar uma ferramenta separada para configurar o BitLocker na unidade do Windows To Go. Para habilitar o BitLocker, é necessário adicionar uma ação para a sequência de tarefas após a etapa **Instalação do Windows e do ConfigMgr** .  

> [!NOTE]  
>  O BitLocker para Windows To Go requer uma senha. Na etapa [Create prestaged media](#BKMK_CreatePrestagedMedia) , você define a senha como parte de um comando prestart usando a variável OSDBitLockerPIN.  

 Use o procedimento a seguir para atualizar a sequência de tarefas do Windows 8 para habilitar o BitLocker para o Windows To Go.  

#### <a name="to-update-the-windows-8-task-sequence-to-enable-bitlocker"></a>Para atualizar a sequência de tarefas do Windows 8 para habilitar o BitLocker  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda o **Gerenciamento de Aplicativos**e clique em **Pacotes**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Pacote**.  

4.  Na página **Pacote** , especifique o nome e a descrição do pacote. Por exemplo, digite **BitLocker for Windows To Go** para o nome do pacote e especifique **Package to update BitLocker for Windows To Go** para a descrição do pacote.  

5.  Selecione **Este pacote contém arquivos de origem**, especifique o local da ferramenta BitLocker para o Windows To Go e clique em **Próximo**. A ferramenta BitLocker está disponível em qualquer servidor do site primário do Configuration Manager no seguinte local: <*ConfigMgrInstallationFolder*>\OSD\Tools\WTG\BitLocker\  

6.  Na página **Tipo de Programa** , selecione **Não criar um programa**.  

7.  Clique em **Próximo** e conclua o assistente.  

8.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

9. No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Sequências de Tarefas**.  

10. Selecione a sequência de tarefas do Windows 8 a que você faz referência na mídia em pré-teste.  

11. Na guia **Início** , no grupo **Sequência de Tarefas** , clique em **Editar**.  

12. Clique na etapa **Instalação do Windows e do ConfigMgr** , clique em **Adicionar**, **Geral**e clique em **Executar linha de comando**. A etapa Executar linha de comando é adicionada após a etapa Instalação do Windows e do ConfigMgr.  

13. Na guia **Propriedades** da etapa **Executar linha de comando** , adicione o seguinte:  

    1.  **Nome**: especifique um nome para a linha de comando, como **Enable BitLocker for Windows To Go**.  

    2.  **Linha de comando**: i386\osdbitlocker_wtg.exe /Enable /pwd: < *Nenhum&#124;AD*>  

         Parâmetros:  

        -   /pwd:<Nenhum&#124;AD> – Especifique o modo de recuperação de senha do BitLocker. Para esse parâmetro é necessário usar o /Habilitar parâmetro está na linha de comando.  

             Selecione **AD** para configurar a Criptografia de Unidade de Disco BitLocker para fazer backup das informações de recuperação das unidades protegidas pelo BitLocker para os AD DS (Serviços de Domínio Active Directory). O backup das senhas de recuperação de uma unidade protegida pelo BitLocker permite aos usuários administrativos recuperarem a unidade se ela for bloqueada. Isso garante que os dados criptografados pertencentes à empresa sempre possam ser acessados por usuários autorizados. Ao especificar **Nenhum**, o usuário é responsável por manter uma cópia da senha ou da chave de recuperação. Se o usuário perder essas informações ou não descriptografar a unidade antes de sair da organização, os usuários administrativos não conseguirão acessar facilmente a unidade.  

        -   /wait:<TRUE&#124;FALSE> – Especifique se a sequência de tarefas aguardará o término da criptografia antes de ser concluída.  

    3.  Selecione **Pacote**e especifique o pacote criado no início deste procedimento.  

    4.  Na guia **Opções** , adicione as seguintes condições:  

        -   Condição = Variável de sequência de tarefas  

        -   Variável = _SMSTSWTG  

        -   Condição = Igual a  

        -   Valor = Verdadeiro  

    > [!NOTE]  
    >  A etapa **Habilitar BitLocker** , que provavelmente está após a etapa de nova linha de comando, não é usada para habilitar o BitLocker para o Windows To Go. No entanto, você pode manter essa etapa na sequência de tarefas para implantações do Windows 8 que não usem uma unidade do Windows To Go.  

###  <a name="BKMK_Deployments"></a> Implantar o pacote do Windows To Go Creator e a sequência de tarefas  
 O Windows To Go é um processo de implantação híbrida. Portanto, é necessário implantar o pacote do Windows To Go Creator e a sequência de tarefas do Windows 8. Use os procedimentos a seguir para concluir o processo de implantação.  

#### <a name="to-deploy-the-windows-to-go-creator-package"></a>Para implantar o pacote do Windows To Go Creator  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda o **Gerenciamento de Aplicativos**e clique em **Pacotes**.  

3.  Selecione o pacote do Windows To Go criado na etapa [Criar um pacote do Windows To Go Creator](#BKMK_CreatePackage) .  

4.  Na guia **Início** , no grupo **Implantação** , clique em **Implantar**.  

5.  Na página **Geral** , especifique as seguintes configurações:  

    1.  **Software**: verifique se o pacote do Windows To Go é está selecionado.  

    2.  **Coleção**: clique em **Procurar** para selecionar a coleção na qual deseja implantar o pacote do Windows To Go.  

    3.  **Usar grupos de pontos de distribuição padrão associados a esta coleção**: selecione esta opção se quiser armazenar o conteúdo pacote no grupo de pontos de distribuição padrão das coleções. Se você não tiver associado a coleção selecionada a um grupo de ponto de distribuição, essa opção estará indisponível.  

6.  Na página **Conteúdo** , clique em **Adicionar** e selecione os pontos de distribuição ou grupos de pontos de distribuição nos quais deseja implantar o conteúdo associado a este pacote e este programa.  

7.  Na página **Configurações de Implantação** , selecione **Disponível** para o tipo de implantação e clique em **Próximo**.  

8.  No **Agendamento**, configure quando este pacote e este programa serão implantados ou ficarão disponíveis para dispositivos clientes.  

     As opções dessa página irão diferir dependendo se a ação de implantação for definida como **Disponível** ou **Obrigatória**.  

9. No **Agendamento**, defina as seguintes configurações e clique em **Próximo**.  

    1.  **Agendar quando essa implantação estará disponível**: especifique a data e a hora em que o pacote e o programa estarão disponíveis para serem executados no computador de destino. Ao selecionar **UTC**, essa configuração garante que o pacote e o programa estejam disponíveis para vários computadores de destino ao mesmo tempo em vez em momentos diferentes, de acordo com a hora local dos computadores de destino.  

    2.  **Agendar quando esta implantação expirará**: especifique a data e a hora em que o pacote e o programa expiram no computador de destino. Ao selecionar **UTC**, essa configuração garante que a sequência de tarefas expire em vários computadores de destino ao mesmo tempo, e não em momentos diferentes, de acordo com a hora local dos computadores de destino.  

10. Na página **Experiência do Usuário** do assistente, especifique as seguintes informações:  

    -   **Instalação de software**: permite que o software seja instalado fora de qualquer janela de manutenção configurada.  

    -   **Reinicialização do sistema (se necessário para conclusão da instalação)**: permite que um dispositivo seja reiniciado fora das janelas de manutenção configuradas quando exigido pela instalação do software.  

    -   **Dispositivos incorporados**ao implantar pacotes e programas em dispositivos com Windows Embedded habilitados para filtro de gravação, você pode especificar para instalar os pacotes e programas em sobreposição temporária e confirmar as alterações posteriormente, ou confirmar as alterações na data limite da instalação ou durante uma janela de manutenção. Ao confirmar as alterações na data limite da instalação ou durante uma janela de manutenção, é necessário reinicializar. Dessa forma, as alterações permanecem no dispositivo.  

11. Na página **Pontos de Distribuição** , especifique as seguintes informações:  

    -   **Opções de implantação** : especifique **Baixar conteúdo do ponto de distribuição e executar localmente**.  

    -   **Permitir que os clientes compartilhem conteúdo com outros clientes na mesma sub-rede**: selecione esta opção para reduzir a carga na rede, permitindo que os clientes baixem conteúdo de outros clientes na rede que tenham baixado e armazenado o conteúdo em cache. Essa opção utiliza o Windows BranchCache e pode ser usada em computadores que executam o Windows Vista SP2 e posterior.  

    -   **Permitir que os clientes usem um local de origem de fallback para o conteúdo**: especificar a permissão para que clientes façam o fallback e usem o ponto de distribuição não preferencial como o local de origem para conteúdo, quando este não estiver disponível em um ponto de distribuição preferencial.  

12. Conclua o assistente.  

#### <a name="to-deploy-the-windows-8-task-sequence"></a>Para implantar a sequência de tarefas do Windows 8  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Sequências de Tarefas**.  

3.  Selecione a sequência de tarefas do Windows 8 que você criou na etapa [Prerequisites to provision Windows To Go](#BKMK_Prereqs) .  

4.  Na guia **Início** , no grupo **Implantação** , clique em **Implantar**.  

5.  Na página **Geral** , especifique as seguintes configurações:  

    1.  **Sequência de tarefas**: verifique se a sequência de tarefas do Windows 8 está selecionada.  

    2.  **Coleção**: clique em **Procurar** para selecionar a coleção que inclui todos os dispositivos para os quais um usuário pode provisionar o Windows To Go.  

        > [!IMPORTANT]  
        >  Se a mídia em pré-teste que você criou na seção [Create prestaged media](#BKMK_CreatePrestagedMedia) utiliza a variável SMSTSPreferredAdvertID, você pode implantar a sequência de tarefas na coleção de **Todos os Sistemas** e especificar a configuração do **Windows PE somente (oculto)** na página **Conteúdo** . Como a sequência de tarefas está oculta, ela só estará disponível para a mídia.  

    3.  **Usar grupos de pontos de distribuição padrão associados a esta coleção**: selecione esta opção se quiser armazenar o conteúdo pacote no grupo de pontos de distribuição padrão das coleções. Se você não tiver associado a coleção selecionada a um grupo de ponto de distribuição, essa opção estará indisponível.  

6.  Na página **Configurações de Implantação** , defina as seguintes configurações e clique em **Avançar**.  

    -   **Finalidade**: selecione **Disponível**. Ao implantar uma sequência de tarefas para um usuário, ele visualiza a sequência de tarefas publicada no catálogo de aplicativos e pode solicitá-la sob demanda. Se você implanta a sequência de tarefas em um dispositivo, o usuário a visualizará no Centro de Software e pode instalá-la sob demanda.  

    -   **Tornar disponível para o seguinte**: especifique se a sequência de tarefas está disponível para clientes do Configuration Manager, mídia ou PXE.  

        > [!IMPORTANT]  
        >  Use a configuração **Somente mídia e PXE (oculto)** para implantações automatizadas de sequência de tarefas. Selecione **Permitir implantação autônoma do sistema operacional** e defina a variável SMSTSPreferredAdvertID como parte da mídia em pré-teste para que o computador inicialize automaticamente para a implantação do Windows To Go sem interação do usuário quando ele detectar uma unidade WIndows To Go. Para obter mais informações sobre essas configurações de mídia em pré-teste, consulte a seção [Create prestaged media](#BKMK_CreatePrestagedMedia) .  

7.  Na página de **Agendamento** , defina as seguintes configurações e clique em **Avançar**.  

    1.  **Agendar quando essa implantação estará disponível**: especifique a data e a hora em que a sequência de tarefas estará disponível para ser executada no computador de destino. Ao selecionar **UTC**, essa configuração garante que a sequência de tarefas esteja disponível para vários computadores de destino ao mesmo tempo, e não em momentos diferentes, de acordo com a hora local dos computadores de destino.  

    2.  **Agendar quando essa implantação expirará**: especifique a data e a hora em que a sequência de tarefas expirará no computador de destino. Ao selecionar **UTC**, essa configuração garante que a sequência de tarefas expire em vários computadores de destino ao mesmo tempo, e não em momentos diferentes, de acordo com a hora local dos computadores de destino.  

8.  Na página **Experiência do Usuário** , especifique as seguintes informações:  

    -   **Mostrar andamento da sequência de tarefas**: especifique se o cliente do Configuration Manager exibe o andamento da sequência de tarefas.  

    -   **Instalação de software**: especifique se o usuário tem permissão para instalar software fora de uma janela de manutenção configurada após a hora agendada.  

    -   **Reinicialização do sistema (se necessário para conclusão da instalação)**: permite que um dispositivo seja reiniciado fora das janelas de manutenção configuradas quando exigido pela instalação do software.  

    -   **Dispositivos incorporados**ao implantar pacotes e programas em dispositivos com Windows Embedded habilitados para filtro de gravação, você pode especificar para instalar os pacotes e programas em sobreposição temporária e confirmar as alterações posteriormente, ou confirmar as alterações na data limite da instalação ou durante uma janela de manutenção. Ao confirmar as alterações na data limite da instalação ou durante uma janela de manutenção, é necessário reinicializar. Dessa forma, as alterações permanecem no dispositivo.  

    -   **Clientes baseados na internet**: especifique se a sequência de tarefas pode ser executada em um cliente baseado em Internet. Não há suporte para operações que instalam o software, como um sistema operacional, com essa configuração. Use esta opção somente para as sequências de tarefas baseadas em script genérico que executam operações no sistema operacional padrão.  

9. Na página **Alertas** , especifique as configurações de alerta que você deseja para esta sequência de tarefas e clique em **Próximo**.  

10. Na página **Pontos de Distribuição** , especifique as seguintes informações e clique em **Próximo**.  

    -   **Opções de implantação**: selecione **Baixar conteúdo localmente quando necessário, executando a sequência de tarefas**.  

    -   **Quando não houver nenhum ponto de distribuição local disponível, use um ponto de distribuição remoto**: especifique se os clientes podem usar pontos de distribuição que estão em redes lentas ou não confiáveis para baixar o conteúdo exigido pela sequência de tarefas.  

    -   **Permitir que os clientes usem um local de origem de fallback para o conteúdo**:
        - *Nas versões anteriores à 1610*, você pode marcar a caixa de seleção Permitir local de origem de fallback para conteúdo para permitir que clientes fora desses grupos de limites façam fallback e usem o ponto de distribuição como um local de origem para conteúdo quando nenhum outro ponto de distribuição estiver disponível.
        - *Começando da versão 1610*, não é mais possível configurar a opção **Permitir local de origem de fallback para conteúdo**.  Em vez disso, você configura as relações entre grupos de limite que determinam quando um cliente pode iniciar a pesquisa de uma localização de fonte de conteúdo válida em grupos de limite adicionais. 

11. Conclua o assistente.  

###  <a name="BKMK_UserExperience"></a> O usuário executa o Windows To Go Creator  
 Após implantar o pacote do Windows To Go e a sequência de tarefas do Windows 8, o Windows To Go Creator está disponível ao usuário. O usuário pode ir para o catálogo de software, ou Centro de Software se o Windows To Go Creator tiver sido implantado em dispositivos e executar o programa do Windows To Go Creator. Depois que o pacote de criador é baixado, um ícone intermitente é exibido na barra de tarefas. Quando o usuário clica no ícone, uma caixa de seleção é exibida para o usuário selecionar a unidade do Windows To Go para provisionamento (a menos que a opção de linhas de comando/drive esteja em uso). Se a unidade não atender aos requisitos do Windows To Go ou se não tiver espaço em disco suficiente para instalar a imagem, o programa do criador exibe uma mensagem de erro. O usuário pode verificar a unidade e a imagem que será aplicada a partir da página de confirmação. Na medida em que o criador configura e pré-configura o conteúdo da unidade do Windows To Go, ele exibe uma caixa de diálogo de progresso. Depois que a pré-configuração estiver concluída, o criador exibe um aviso para reiniciar o computador para inicializar a unidade do Windows To Go.  

> [!NOTE]  
>  Se você não habilitou o redirecionamento de inicialização como parte da linha de comando do programa do criador na seção [Create a Windows To Go Creator package](#BKMK_CreatePackage) , o usuário poderá ser solicitado para reinicializar manualmente a unidade do Windows To Go sempre que o sistema for reiniciado.  

###  <a name="BKMK_ConfigureStageDrive"></a> O Configuration Manager configura e prepara a unidade do Windows To Go  
 Depois que o computador for reiniciado para a unidade do Windows To Go, a unidade será inicializada no Windows PE e se conectará ao ponto de gerenciamento para obter a política para concluir a implantação de sistema operacional. O Configuration Manager configura e prepara a unidade. Depois que o Configuration Manager pré-configura a unidade, o usuário pode reiniciar o computador para finalizar o processo de provisionamento (como unir-se a um domínio ou instalar aplicativos). Esse processo é o mesmo para qualquer mídia em pré-teste.  

###  <a name="BKMK_UserLogsIn"></a> O usuário faz logon no Windows 8  
 Após o Configuration Manager concluir o processo de provisionamento e a tela de bloqueio do Windows 8 ser exibida, o usuário pode fazer logon no sistema operacional.  
