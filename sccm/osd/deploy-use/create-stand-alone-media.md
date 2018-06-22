---
title: Criar mídia autônoma
titleSuffix: Configuration Manager
description: Use uma mídia autônoma para implantar o sistema operacional em um computador sem uma conexão de rede.
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35dd110c2566dab945bb0701e113becb3412d65c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351931"
---
# <a name="create-stand-alone-media-with-system-center-configuration-manager"></a>Criar mídia autônoma com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A mídia autônoma no Configuration Manager contém tudo o que é necessário para implantar o sistema operacional em um computador sem uma conexão de rede. Use a mídia autônoma nos seguintes cenários de implantação de sistema operacional:  

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar uma nova versão do Windows em um novo computador (sem sistema operacional)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Atualizar o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md)  

A mídia autônoma inclui a sequência de tarefas que automatiza as etapas para instalar o sistema operacional e todos os demais conteúdos necessários. Esse conteúdo inclui a imagem de inicialização, a imagem do sistema operacional e os drivers de dispositivo. Como a mídia autônoma armazena tudo para implantar o sistema operacional, é necessário mais espaço em disco do que para outros tipos de mídia. Quando você cria mídia autônoma em um site de administração central, o cliente recupera seu código do site atribuído do Active Directory. A mídia autônoma criada em sites filho atribui automaticamente o código desse site ao cliente.  

##  <a name="BKMK_CreateStandAloneMedia"></a> Criar mídia autônoma  
Antes de criar mídia autônoma usando o Assistente para criação de mídia de sequência de tarefas, certifique-se de que as seguintes condições forem atendidas:  

### <a name="create-a-task-sequence-to-deploy-an-operating-system"></a>Criar uma sequência de tarefas para implantar um sistema operacional
Como parte da mídia autônoma, você deve especificar a sequência de tarefas para implantar um sistema operacional. Para ver as etapas para criar uma nova sequência de tarefas, consulte [Criar uma sequência de tarefas para instalar um sistema operacional no System Center Configuration Manager](create-a-task-sequence-to-install-an-operating-system.md).

Não há suporte para as seguintes ações na mídia autônoma:
- A etapa **Aplicação Automática de Drivers** na sequência de tarefas. A mídia autônoma não é compatível com a aplicação automática de drivers de dispositivo do catálogo de drivers. Use a etapa **Aplicar Pacote de Driver** para tornar um conjunto especificado de drivers disponível para Instalação do Windows.
- A etapa **Baixar Conteúdo do Pacote** na sequência de tarefas. As informações do ponto de gerenciamento não estão disponíveis na mídia autônoma, portanto, a etapa falha ao tentar enumerar locais de conteúdo.
- Instalação de atualizações de software.
- Instalação do software antes de implantar o sistema operacional.
- Sequência de tarefas para implantações que não são de sistema operacional.
- Associação dos usuários ao computador de destino para dar suporte à afinidade de dispositivo do usuário.
- O pacote dinâmico é instalado por meio da tarefa **Instalar Pacotes**.
- O aplicativo dinâmico é instalado por meio da tarefa **Instalar Aplicativo**.

> [!NOTE]    
> Poderá ocorrer um erro se a sequência de tarefas incluir a etapa [Instalar Pacote](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) e você criar a mídia autônoma em um site de administração central. O site de administração central não tem as políticas de configuração de cliente necessárias. Essas políticas são necessárias para habilitar o agente de distribuição de software durante a execução da sequência de tarefas. O erro a seguir pode aparecer no arquivo CreateTsMedia.log:    
>     
> `WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)`    
> 
> Para mídia autônoma que inclui uma etapa **Instalar Pacote**, crie a mídia autônoma em um site primário que tem o agente de distribuição de software habilitado. 
>
> Como alternativa, adicione uma etapa [Executar Linha de Comando](../understand/task-sequence-steps.md#BKMK_RunCommandLine) após a etapa [Instalar o Windows e o ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) e antes da primeira etapa **Instalar o Pacote** na sequência de tarefas. A etapa **Executar Linha de Comando** executa o seguinte comando WMIC para habilitar o agente de distribuição de software antes da primeira etapa Instalar Pacote:    
>    
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`


> [!IMPORTANT]    
> Não selecione a configuração **Usar pacote de cliente de pré-produção quando disponível** na etapa da sequência de tarefas **Instalar o Windows e o ConfigMgr** para mídia autônoma. A mídia autônoma não é compatível com o uso dessa configuração. Para obter mais informações sobre essa configuração, consulte [Instalar o Windows e o ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr).


### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuir todo o conteúdo associado à sequência de tarefas
Distribua todo o conteúdo exigido pela sequência de tarefas para pelo menos um ponto de distribuição. Esse conteúdo inclui a imagem de inicialização, a imagem do sistema operacional e outros arquivos associados. O assistente reúne as informações do ponto de distribuição quando ele cria a mídia autônoma. Você precisa ter direitos de acesso de **Leitura** à biblioteca de conteúdo no ponto de distribuição. Para obter mais informações, consulte [Distribuir o conteúdo referenciado por uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS).

### <a name="prepare-the-removable-usb-drive"></a>Preparar a unidade USB removível
*Para uma unidade USB removível:*

Se você estiver usando uma unidade USB removível, conecte a unidade USB ao computador em que o assistente é executado. A unidade USB precisa ser detectável pelo Windows como um dispositivo removível. O assistente grava diretamente na unidade USB ao criar a mídia. A mídia autônoma usa um sistema de arquivos FAT32. Não é possível criar uma mídia autônoma em uma unidade flash USB cujo conteúdo contém um arquivo de tamanho superior a 4 GB.

### <a name="create-an-output-folder"></a>Criar uma pasta de saída
*Para um conjunto de CD/DVD:*

Para executar o Assistente para Criar Mídia de Sequência de Tarefas para criar mídia para um conjunto de CD ou DVD, é preciso criar uma pasta para os arquivos de saída criados pelo assistente. A mídia criada para um conjunto de CD ou DVD é gravada como arquivos .iso diretamente na pasta.


 Use o procedimento a seguir para criar mídia autônoma para uma unidade USB removível ou um aparelho de CD/DVD.  

## <a name="to-create-stand-alone-media"></a>Para criar mídia autônoma  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Sequências de Tarefas**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Mídia de Sequência de Tarefas** para iniciar o Assistente para Criar Mídia de Sequência de Tarefas.  

4.  Na página **Selecionar o Tipo de Mídia** , especifique as opções a seguir e clique em **Próximo**.  

    -   Selecione **Mídia autônoma**.  

    -   Opcionalmente, se você quiser permitir que o sistema operacional seja implantado sem exigir a entrada do usuário, selecione **Permitir implantação autônoma do sistema operacional**. Quando você seleciona essa opção, o usuário não precisa inserir informações de configuração de rede nem sequências de tarefas opcionais. Se a mídia estiver configurada para proteção de senha, o usuário ainda receberá uma solicitação de senha.  

5.  Na página **Tipo de Mídia**, especifique se a mídia é uma unidade USB removível ou um conjunto de CD/DVD:  

    > [!IMPORTANT]  
    >  Por padrão, a mídia autônoma usa um sistema de arquivos FAT32. Não é possível criar uma mídia autônoma em uma unidade USB removível cujo conteúdo inclui um arquivo de tamanho superior a 4 GB.  

    -   Ao selecionar a **Unidade USB removível**, especifique a unidade na qual você deseja armazenar o conteúdo.  

        - **Formatar a unidade USB removível (FAT32) e torná-la inicializável**: por padrão, permita que o Configuration Manager prepare a unidade USB. Muitos dispositivos UEFI mais recentes requerem uma partição FAT32 inicializável. No entanto, esse formato também limita o tamanho dos arquivos e a capacidade geral da unidade. Se você já tiver formatado e configurado a unidade removível, desabilite essa opção. 

    -   Caso selecione **Conjunto de CD/DVD**, especifique a capacidade da mídia, o nome e o caminho dos arquivos de saída. O assistente grava os arquivos de saída nesse local. Por exemplo: **\\\nomedoservidor\pasta\arquivodesaida.iso**  

         Se a capacidade da mídia for muito pequena para armazenar todo o conteúdo, vários arquivos são criados e você deve armazenar o conteúdo em vários CDs ou DVDs. Se várias mídias forem necessárias, o Configuration Manager adicionará um número de sequência ao nome de cada arquivo de saída criado. Além disso, se você implantar um aplicativo juntamente com o sistema operacional e o aplicativo não couber em uma única mídia, o Configuration Manager armazenará o aplicativo em várias mídias. Quando a mídia autônoma é executada, o Configuration Manager solicita ao usuário a próxima mídia, na qual o aplicativo está armazenado.   

         > [!IMPORTANT]  
         >  Se você selecionar uma imagem .iso existente, o Assistente de Mídia de Sequência de Tarefas excluirá essa imagem da unidade ou do compartilhamento assim que você prosseguir para a próxima página do assistente. A imagem existente será excluída mesmo se você cancelar o assistente.  

     Clique em **Avançar**.  

6.  Na página **Segurança**, escolha entre as seguintes configurações e clique em **Avançar**:
    - **Proteger mídia com senha**: insira uma senha forte para ajudar a proteger a mídia. Se você especificar uma senha, ela será necessária para usar a mídia.  

        > [!IMPORTANT]  
        >  Na mídia autônoma, somente as etapas da sequência de tarefas e suas variáveis são criptografadas. O conteúdo restante da mídia não é criptografado, portanto não inclua nenhuma informação confidencial nos scripts da sequência de tarefas. Armazene e implemente todas as informações confidenciais usando as variáveis da sequência de tarefas.  

    - **Selecione um intervalo de datas válido para essa mídia autônoma** (a partir da versão 1702): defina datas de início e vencimento opcionais na mídia. Essas configurações estão desabilitadas por padrão. As datas são comparadas com a hora do sistema no computador antes de a mídia autônoma ser executada. Quando a hora do sistema for anterior à hora de início ou posterior à hora de expiração, a mídia autônoma não será iniciada. Essas opções também estão disponíveis usando o cmdlet New-CMStandaloneMedia PowerShell.
7.  Na página **CD/DVD Autônomo** , especifique a sequência de tarefas que implanta o sistema operacional e clique em **Próxima**. Para adicionar conteúdo à mídia autônoma para dependências de aplicativos, escolha **Detectar dependências de aplicativos associados e adicioná-los a esta mídia**.
    > [!TIP]
    > Se você não vir as dependências de aplicativo esperadas, cancele a seleção e selecione novamente a configuração **Detectar dependências de aplicativos associadas e adicioná-las a esta mídia** para atualizar a lista.

    O assistente permite que você selecione apenas as sequências de tarefas associadas a uma imagem de inicialização.  

8. Na página **Selecionar Aplicativo** (disponível a partir da versão 1702), especifique o conteúdo do aplicativo a ser incluído como parte do arquivo de mídia e clique em **Avançar**.
9. Na página **Selecionar Pacote** (disponível a partir da versão 1702), especifique o conteúdo do pacote a ser incluído como parte do arquivo de mídia e clique em **Avançar**.
10. Na página **Selecionar Pacote do Driver** (disponível a partir da versão 1702), especifique o conteúdo do pacote do driver a ser incluído como parte do arquivo de mídia e clique em **Avançar**.
11.  Na página **Pontos de Distribuição**, especifique os pontos de distribuição que tem o conteúdo exigido e clique em **Avançar**.  

     O Configuration Manager exibe apenas pontos de distribuição que tenham conteúdo. Distribua todo o conteúdo associado à sequência de tarefas para pelo menos um ponto de distribuição antes de continuar. Após distribuir o conteúdo, atualize a lista de pontos de distribuição. Remova os pontos de distribuição que já foram selecionados nessa página, vá para a página anterior e volte para a página **Pontos de Distribuição**. Como alternativa, reinicie o assistente. Para obter mais informações, consulte [Distribuir o conteúdo referenciado por uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS) e [Gerenciar conteúdo e infraestrutura de conteúdo](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    > [!NOTE]  
    >  É necessário ter direitos de acesso de **Leitura** à biblioteca de conteúdo nos pontos de distribuição.  

12. Na página **Personalização** , especifique as informações a seguir e clique em **Próxima**.  

    -   Especifique as variáveis que a sequência de tarefas usa para implantar o sistema operacional.  

    -   Especifique quaisquer comandos prestart que deseja executar antes da sequência de tarefas. Os comandos prestart são um script ou um executável que é executado no Windows PE antes de iniciar a sequência de tarefas. Para mais informações, consulte [Comandos prestart para mídia de sequência de tarefas](../understand/prestart-commands-for-task-sequence-media.md).  

         Opcionalmente, selecione **Arquivos no comando prestart** para incluir quaisquer arquivos necessários no comando prestart.  

        > [!TIP]  
        >  Durante a criação de mídia da sequência de tarefas, o Configuration Manager grava a ID do pacote e a linha de comando prestart, para o arquivo **CreateTSMedia.log** no computador que executa o console do Configuration Manager. Essa saída inclui o valor para quaisquer variáveis de sequência de tarefas. Examine este arquivo de log para verificar o valor das variáveis da sequência de tarefas.  

13. Conclua o assistente.  

 Os arquivos de mídia autônoma (.iso) são criados na pasta de destino. Se tiver selecionado **CD/DVD Autônomo**, agora você poderá copiar os arquivos de saída para um conjunto de CDs ou DVDs.  

##  <a name="BKMK_StandAloneMediaTSExample"></a> Exemplo de sequência de tarefas para mídia autônoma  
 Para criar uma sequência de tarefas para implantar um sistema operacional usando mídia autônoma, use a tabela a seguir como um guia. A tabela ajuda você a decidir a sequência geral de etapas de sequência de tarefas. Ela também ajuda a organizar e estruturar as etapas de sequência de tarefas em grupos lógicos. A sequência de tarefas que você criar pode variar do que esse exemplo e pode conter mais ou menos etapas da sequência de tarefas e grupos.  

> [!NOTE]  
>  Você sempre deve usar o Assistente de mídia de sequência de tarefas para criar mídia autônoma.  

|Grupo de sequências de tarefas ou etapa|Descrição|  
|---------------------------------|-----------------|  
|Captura de arquivos e configurações - **(novo grupo de sequências de tarefas)**|Crie um grupo de sequências de tarefas. Um grupo de sequências de tarefas mantém etapas da sequência de tarefas semelhantes juntas para melhor organização e controle de erro.|  
|Capturar Configurações do Windows|Use essa etapa de sequência de tarefas para capturar as configurações do Windows do computador de destino antes de criar uma nova imagem. Capture o nome do computador, usuário e informações organizacionais e as configurações de fuso horário.|  
|Capturar configurações da rede|Use essa etapa de sequência de tarefas para capturar as configurações de rede do computador que recebe a sequência de tarefas. Você pode capturar a associação de grupo de trabalho ou domínio do computador e informações de configuração de adaptador de rede.|  
|Capturar Arquivos e Configurações do Usuário ‑ **(Novo Subgrupo de Sequências de Tarefas)**|Crie um grupo de sequências de tarefas dentro de um grupo de sequências de tarefas. Esse subgrupo contém as etapas para capturar dados de estado do usuário do computador de destino antes de fazer uma nova imagem. Semelhante ao grupo inicial que você adicionou, esse subgrupo mantém etapas semelhantes da sequência de tarefas juntas para melhorar a organização e o controle de erros.|  
|Definir Local estado local|Use essa etapa de sequência de tarefas para especificar um local usando a variável de sequência de tarefas de caminho protegido. O estado do usuário é armazenado em um diretório protegido no disco rígido.|  
|Capturar Estado do Usuário|Use essa etapa de sequência de tarefas para capturar os arquivos de usuário e configurações que você deseja migrar para o novo sistema operacional.|  
|Instalar o sistema operacional - **(novo grupo de sequências de tarefas)**|Crie outro subgrupo de sequências de tarefas. Esse subgrupo contém as etapas necessárias para instalar o sistema operacional.|  
|Reinicialize no Windows PE ou o disco rígido|Use essa etapa de sequência de tarefas para especificar opções de reinicialização do computador que recebe essa sequência de tarefas. Esta etapa exibe uma mensagem para o usuário indicando que o computador está reiniciando para continuar a instalação.<br /><br /> Esta etapa usa a variável de sequência de tarefas **_SMSTSInWinPE** de somente leitura. Se o valor associado for igual a **false**, a etapa da sequência de tarefas continuará.|  
|Aplicar Sistema Operacional|Use essa etapa de sequência de tarefas para instalar a imagem do sistema operacional no computador de destino. Esta etapa exclui todos os arquivos no volume, com exceção de arquivos de controle específicos do Configuration Manager. Em seguida, ela aplica todas as imagens de volume contidas no arquivo WIM ao volume de disco sequencial correspondente. Você também pode especificar um arquivo de resposta **sysprep** para configurar qual partição de disco usar para a instalação.|  
|Aplicar as Configurações do Windows|Use essa etapa de sequência de tarefas para configurar as informações de configuração de configurações do Windows no computador de destino. Essas configurações incluem informações dos usuários e organizacionais, informações de chave de produto ou licença, fuso horário e a senha de administrador local.|  
|Aplicar Configurações de Rede|Use essa etapa de sequência de tarefas para especificar as informações de configuração de rede ou grupo de trabalho do computador de destino. Você também pode especificar se o computador usa um servidor DHCP ou você pode atribuir estaticamente as informações de endereço IP.|  
|Aplicar pacote de driver|Use essa etapa de sequência de tarefas para disponibilizar todos os drivers de dispositivo em um pacote de driver para uso pela instalação do Windows. Todos os drivers de dispositivo necessários devem estar contidos na mídia autônoma.|  
|Configurar o sistema operacional - **(novo grupo de sequências de tarefas)**|Crie outro subgrupo de sequências de tarefas. Esse subgrupo contém as etapas necessárias para instalar o cliente do Configuration Manager.|  
|Instalar Windows e ConfigMgr|Use essa etapa de sequência de tarefas para instalar o software cliente do Configuration Manager. O Configuration Manager instala e registra o GUID do cliente do Configuration Manager. Você pode atribuir os parâmetros necessários para a instalação na janela **Propriedades de instalação** .|  
|Restaurar arquivos e configurações - **(novo grupo de sequências de tarefas)**|Crie outro subgrupo de sequências de tarefas. Esse subgrupo contém as etapas necessárias para restaurar o estado do usuário.|  
|Restaurar Estado do Usuário|Use essa etapa de sequência de tarefas para iniciar a USMT (Ferramenta de Migração do Usuário Windows). A USMT restaura o estado e configurações do usuário capturadas anteriormente com a etapa Capturar Estado do Usuário para o computador de destino.|  
