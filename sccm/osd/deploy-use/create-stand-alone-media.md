---
title: "Criar mídia autônoma com o System Center Configuration Manager | Microsoft Docs"
description: "Use uma mídia autônoma para implantar o sistema operacional em um computador sem uma conexão com a rede ou com um site do Configuration Manager."
ms.custom: na
ms.date: 12/21/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
caps.latest.revision: 21
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: ee7f69bd65152deffb2456d9807e1e8fee8802ec
ms.openlocfilehash: 708525604c3f40cf75b5408c3666193186b7cf50
ms.lasthandoff: 03/07/2017


---
# <a name="create-stand-alone-media-with-system-center-configuration-manager"></a>Criar mídia autônoma com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A mídia autônoma no Configuration Manager contém tudo o que é necessário para implantar o sistema operacional em um computador sem uma conexão com um site Configuration Manager e sem usar a rede. Use a mídia autônoma nos seguintes cenários de implantação de sistema operacional:  

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar uma nova versão do Windows em um novo computador (sem sistema operacional)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Atualizar o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md)  

 A mídia autônoma inclui a sequência de tarefas que automatiza as etapas para instalar o sistema operacional e qualquer outro conteúdo necessário, inclusive a imagem de inicialização, imagem do sistema operacional e drivers de dispositivo. Como tudo o que é necessário para implantar o sistema operacional é armazenado na mídia autônoma, o espaço em disco necessário para mídia autônoma é significativamente maior do que o espaço em disco necessário para outros tipos de mídia. Quando você cria mídia autônoma em um site de administração central, o cliente recupera seu código de site atribuído do Active Directory. A mídia autônoma criada em sites filho atribuirá automaticamente ao cliente o código desse site.  

##  <a name="BKMK_CreateStandAloneMedia"></a> Criar mídia autônoma  
 Antes de criar mídia autônoma usando o Assistente para criação de mídia de sequência de tarefas, certifique-se de que as seguintes condições forem atendidas:  

### <a name="create-a-task-sequence-to-deploy-an-operating-system"></a>Criar uma sequência de tarefas para implantar um sistema operacional
Como parte da mídia autônoma, você deve especificar a sequência de tarefas para implantar um sistema operacional. Para ver as etapas para criar uma nova sequência de tarefas, consulte [Criar uma sequência de tarefas para instalar um sistema operacional no System Center Configuration Manager](create-a-task-sequence-to-install-an-operating-system.md).

Não há suporte para as seguintes ações na mídia autônoma:
- A etapa Aplicação automática de drivers na sequência de tarefas. Não há suporte para aplicação automática de drivers de dispositivo do catálogo de driver, mas você pode escolher a etapa Aplicar pacote de driver para tornar um conjunto especificado de drivers disponíveis para instalação do Windows.
- A etapa de Baixar Conteúdo do Pacote na sequência de tarefas. As informações do ponto de gerenciamento não estão disponíveis na mídia autônoma, portanto, a etapa falhará ao tentar enumerar locais de conteúdo.
- Instalação de atualizações de software.
- Instalação do software antes de implantar o sistema operacional.
- Sequência de tarefas para implantações que não são de sistema operacional.
- Associação dos usuários ao computador de destino para dar suporte à afinidade de dispositivo do usuário.
- O pacote dinâmico é instalado por meio da tarefa Instalar pacotes.
- O aplicativo dinâmico é instalado por meio da tarefa Instalar aplicativo.

Se a sequência de tarefas para implantar um sistema operacional incluir a etapa [Instalar Pacote](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) e você criar a mídia autônoma em um site de administração central, poderá ocorrer um erro. O site de administração central não possui as políticas de configuração de cliente necessárias para habilitar o agente de distribuição de software durante a execução da sequência de tarefas. O erro a seguir pode aparecer no arquivo CreateTsMedia.log:<br /><br /> “Falha no método WMI SMS_TaskSequencePackage.GetClientConfigPolicies (0x80041001)”<br /><br /> Para mídia autônoma que inclui uma etapa **Instalar Pacote**, é necessário criar a mídia autônoma em um site primário que contém o agente de distribuição de software habilitado ou adicionar uma etapa [Executar Linha de Comando](../understand/task-sequence-steps.md#BKMK_RunCommandLine) após a etapa [Configurar Windows e ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) e antes da primeira etapa **Instalar Pacote** na sequência de tarefas. A etapa **Executar linha de comando** executa como um comando WMIC para habilitar o agente de distribuição de software antes da primeira etapa de Instalar pacote ser executada. Você pode usar o seguinte em sua etapa de sequência de tarefas de **Executar linha de comando** :<br /><br />
```
WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE
```

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuir todo o conteúdo associado à sequência de tarefas
Você deve distribuir todo o conteúdo exigido pela sequência de tarefas para pelo menos um ponto de distribuição. Isso inclui a imagem de inicialização, a imagem do sistema operacional e outros arquivos associados. O assistente reúne as informações do ponto de distribuição quando ele cria a mídia autônoma. Você precisa ter direitos de acesso de **Leitura** à biblioteca de conteúdo no ponto de distribuição.  Para obter detalhes, consulte [Distribuir o conteúdo referenciado por uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS).

### <a name="prepare-the-removable-usb-drive"></a>Preparar a unidade USB removível
*Para uma unidade USB removível:*

Se você pretende usar uma unidade USB removível, a unidade USB deve ser conectada ao computador no qual o assistente é executado e a unidade USB deve ser detectável pelo Windows como um dispositivo de remoção. O assistente grava diretamente na unidade USB ao criar a mídia. A mídia autônoma usa um sistema de arquivos FAT32. Não é possível criar uma mídia autônoma em uma unidade flash USB cujo conteúdo contém um arquivo de tamanho superior a 4 GB.

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

    -   Opcionalmente, se você quiser permitir que o sistema operacional seja implantado sem exigir a entrada do usuário, selecione **Permitir implantação autônoma do sistema operacional**. Quando você seleciona essa opção, o usuário não precisa inserir informações de configuração de rede nem sequências de tarefas opcionais. No entanto, ainda será solicitada ao usuário uma senha, se a mídia estiver configurada para proteção por senha.  

5.  Na página **Tipo de Mídia** , especifique se a mídia é uma unidade flash ou um conjunto de CD/DVD e clique em configurar o seguinte:  

    > [!IMPORTANT]  
    >  A mídia autônoma usa um sistema de arquivos FAT32. Não é possível criar uma mídia autônoma em uma unidade flash USB cujo conteúdo contém um arquivo de tamanho superior a 4 GB.  

    -   Se você selecionar a **Unidade flash USB**, especifique a unidade na qual deseja armazenar o conteúdo.  

    -   Caso selecione **Conjunto de CD/DVD**, especifique a capacidade da mídia, o nome e o caminho dos arquivos de saída. O assistente grava os arquivos de saída nesse local. Por exemplo: **\\\nomedoservidor\pasta\arquivodesaida.iso**  

         Se a capacidade da mídia for muito pequena para armazenar todo o conteúdo, vários arquivos são criados e você deve armazenar o conteúdo em vários CDs ou DVDs. Se várias mídias forem necessárias, o Configuration Manager adicionará um número de sequência ao nome de cada arquivo de saída criado. Além disso, se você implantar um aplicativo juntamente com o sistema operacional e o aplicativo não couber em uma única mídia, o Configuration Manager armazenará o aplicativo em várias mídias. Quando a mídia autônoma é executada, o Configuration Manager solicita ao usuário a próxima mídia, na qual o aplicativo está armazenado.  

        > [!IMPORTANT]  
        >  Se você selecionar uma imagem .iso existente, o Assistente de Mídia de Sequência de Tarefas excluirá essa imagem da unidade ou do compartilhamento assim que você prosseguir para a próxima página do assistente. A imagem existente será excluída mesmo se você cancelar o assistente.  

     Clique em **Avançar**.  

6.  Na página **Segurança** , insira uma senha forte para ajudar a proteger a mídia e clique em **Próxima**. Se você especificar uma senha, ela será necessária para usar a mídia.  

    > [!IMPORTANT]  
    >  Na mídia autônoma, somente as etapas da sequência de tarefas e suas variáveis são criptografadas. O conteúdo restante da mídia não é criptografado, portanto não inclua nenhuma informação confidencial nos scripts da sequência de tarefas. Armazene e implemente todas as informações confidenciais usando as variáveis da sequência de tarefas.  

7.  Na página **CD/DVD Autônomo** , especifique a sequência de tarefas que implanta o sistema operacional e clique em **Próxima**. Escolha **Detectar dependências de aplicativos associadas e adicioná-las a esta mídia** para adicionar conteúdo à mídia autônoma para dependências de aplicativos.
> [!TIP]
> Se você não vir as dependências de aplicativo esperadas, cancele a seleção e selecione novamente a configuração **Detectar dependências de aplicativos associadas e adicioná-las a esta mídia** para atualizar a lista.

O assistente permite que você selecione apenas as sequências de tarefas associadas a uma imagem de inicialização.  

8.  Na página **Pontos de Distribuição** , especifique o ponto de distribuição que tem o conteúdo exigido pela sequência de tarefas e clique em **Próximo**.  

     O Configuration Manager vai exibir apenas pontos de distribuição que tenham o conteúdo. Você deve distribuir todo o conteúdo associado à sequência de tarefas (imagem de inicialização, imagem do sistema operacional, etc.) para, pelo menos, um ponto de distribuição antes que possa continuar. Após distribuir o conteúdo, você pode reiniciar o assistente ou remover os pontos de distribuição que já selecionou nessa página, ir para a página anterior e voltar para a página **Pontos de distribuição** para atualizar a lista de pontos de distribuição. Para obter mais informações sobre como distribuir conteúdo, consulte [Distribuir o conteúdo referenciado por uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS). Para obter mais informações sobre pontos de distribuição e gerenciamento de conteúdo, consulte [Gerenciar conteúdo e infraestrutura de conteúdo do System Center Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    > [!NOTE]  
    >  É necessário ter direitos de acesso de **Leitura** à biblioteca de conteúdo nos pontos de distribuição.  

9. Na página **Personalização** , especifique as informações a seguir e clique em **Próxima**.  

    -   Especifique as variáveis que a sequência de tarefas usa para implantar o sistema operacional.  

    -   Especifique quaisquer comandos prestart que deseja executar antes da sequência de tarefas. Os comandos prestart são um script ou um executável que podem interagir com o usuário no Windows PE antes da execução da sequência de tarefas para instalar o sistema operacional. Para obter mais informações sobre comandos prestart para mídia, consulte [Comandos prestart para mídia de sequência de tarefas no System Center Configuration Manager](../understand/prestart-commands-for-task-sequence-media.md).  

         Opcionalmente, selecione **Arquivos no comando prestart** para incluir quaisquer arquivos necessários no comando prestart.  

        > [!TIP]  
        >  Durante a criação de mídia de sequência de tarefas, a sequência de tarefas grava a ID do pacote e a linha de comando prestart, que inclui o valor de quaisquer variáveis de sequência de tarefas, no arquivo de log CreateTSMedia.log no computador que executa o console do Configuration Manager. Você poderá analisar esse arquivo de log para verificar o valor das variáveis de sequência de tarefas.  

10. Conclua o assistente.  

 Os arquivos de mídia autônoma (.iso) são criados na pasta de destino. Se tiver selecionado **CD/DVD Autônomo**, agora você poderá copiar os arquivos de saída para um conjunto de CDs ou DVDs.  

##  <a name="BKMK_StandAloneMediaTSExample"></a> Exemplo de sequência de tarefas para mídia autônoma  
 Use a tabela a seguir como um guia que você crie uma sequência de tarefas para implantar um sistema operacional usando mídia autônoma. A tabela ajudará você a decidir a sequência geral de etapas da sequência de tarefas e como organizar e estruturar essas etapas de sequência de tarefas em grupos lógicos. A sequência de tarefas que você criar pode variar do que esse exemplo e pode conter mais ou menos etapas da sequência de tarefas e grupos.  

> [!NOTE]  
>  Você sempre deve usar o Assistente de mídia de sequência de tarefas para criar mídia autônoma.  

|Grupo de sequências de tarefas ou etapa|Descrição|  
|---------------------------------|-----------------|  
|Captura de arquivos e configurações - **(novo grupo de sequências de tarefas)**|Crie um grupo de sequências de tarefas. Um grupo de sequências de tarefas mantém etapas da sequência de tarefas semelhantes juntas para melhor organização e controle de erro.|  
|Capturar Configurações do Windows|Use essa etapa de sequência de tarefas para identificar as configurações do Microsoft Windows que são capturadas do sistema operacional existente no computador de destino antes de fazer uma nova imagem. Você pode capturar o nome do computador, usuário e informações organizacionais e as configurações de fuso horário.|  
|Capturar Configurações da Rede|Use essa etapa de sequência de tarefas para capturar as configurações de rede do computador que recebe a sequência de tarefas. Você pode capturar a associação de grupo de trabalho ou domínio do computador e informações de configuração de adaptador de rede.|  
|Capturar arquivos de usuário e configurações - **(nova tarefa sequência subgrupo)**|Crie um grupo de sequências de tarefas dentro de um grupo de sequências de tarefas. Esse subgrupo contém as etapas necessárias para capturar dados de estado do usuário do sistema operacional existente no computador de destino antes de fazer uma nova imagem. Semelhante para o grupo inicial que você adicionou, esse subgrupo mantém controlam semelhante etapas da sequência de tarefas para o erro e melhor organização.|  
|Definir Local estado local|Use essa etapa de sequência de tarefas para especificar um local usando a variável de sequência de tarefas de caminho protegido. O estado do usuário é armazenado em um diretório protegido no disco rígido.|  
|Capturar Estado do Usuário|Use essa etapa de sequência de tarefas para capturar os arquivos de usuário e configurações que você deseja migrar para o novo sistema operacional.|  
|Instalar o sistema operacional - **(novo grupo de sequências de tarefas)**|Crie outro grupo de subpropriedades de sequência de tarefas. Esse subgrupo contém as etapas necessárias para instalar o sistema operacional.|  
|Reinicialize no Windows PE ou o disco rígido|Use essa etapa de sequência de tarefas para especificar opções de reinicialização do computador que recebe essa sequência de tarefas. Esta etapa exibirá uma mensagem para o usuário indicando que o computador será reiniciado para que a instalação possa continuar.<br /><br /> Esta etapa usa somente leitura **_SMSTSInWinPE** variável de sequência de tarefas. Se o valor for igual a **false** continuará a etapa de sequência de tarefas.|  
|Aplicar Sistema Operacional|Use essa etapa de sequência de tarefas para instalar a imagem do sistema operacional no computador de destino. Esta etapa exclui todos os arquivos nesse volume (com exceção de arquivos de controle específicos do Configuration Manager) e aplica todas as imagens de volume contidas no arquivo WIM para o volume de disco sequencial correspondente. Você também pode especificar um arquivo de resposta **sysprep** para configurar qual partição de disco usar para a instalação.|  
|Aplicar as Configurações do Windows|Use essa etapa de sequência de tarefas para configurar as informações de configuração de configurações do Windows no computador de destino. Você pode aplicar as configurações do windows são usuários e informações organizacionais, informações de chave de produto ou licença, fuso horário e a senha de administrador local.|  
|Aplicar Configurações de Rede|Use essa etapa de sequência de tarefas para especificar as informações de configuração de rede ou grupo de trabalho do computador de destino. Você também pode especificar se o computador usa um servidor DHCP ou você pode atribuir estaticamente as informações de endereço IP.|  
|Aplicar pacote de driver|Use essa etapa de sequência de tarefas para disponibilizar todos os drivers de dispositivo em um pacote de driver para uso pela instalação do Windows. Todos os drivers de dispositivo necessários devem estar contidos na mídia autônoma.|  
|Configurar o sistema operacional - **(novo grupo de sequências de tarefas)**|Crie outro grupo de subpropriedades de sequência de tarefas. Esse subgrupo contém as etapas necessárias para instalar o cliente do Configuration Manager.|  
|Instalar Windows e ConfigMgr|Use essa etapa de sequência de tarefas para instalar o software cliente do Configuration Manager. O Configuration Manager instala e registra o GUID do cliente do Configuration Manager. Você pode atribuir os parâmetros necessários para a instalação na janela **Propriedades de instalação** .|  
|Restaurar arquivos e configurações - **(novo grupo de sequências de tarefas)**|Crie outro grupo de subpropriedades de sequência de tarefas. Esse subgrupo contém as etapas necessárias para restaurar o estado do usuário.|  
|Restaurar Estado do Usuário|Use essa etapa de sequência de tarefas para iniciar a USMT (Ferramenta de Migração do Usuário) para restaurar o estado e as configurações do usuário que foram capturadas da ação Capturar Estado do Usuário para o computador de destino.|  

