---
title: Criar aplicativos de computador Mac
titleSuffix: Configuration Manager
description: Veja quais considerações você deverá levar em conta ao criar e implantar aplicativos para computadores Mac.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: ab1aecdd-d943-44f5-b0a9-e8fe7439e5d6
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 41ec97899d8f959298b3f62ff4a86837b04af461
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140908"
---
# <a name="create-mac-computer-applications-with-system-center-configuration-manager"></a>Criar aplicativos de computador Mac com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Lembre-se das seguintes considerações ao criar e implantar aplicativos para computadores Mac.  

> [!IMPORTANT]  
>  Os procedimentos deste tópico abrangem informações sobre a implantação de aplicativos em computadores Mac nos quais você instalou o cliente do Configuration Manager. Computadores Mac registrados no Microsoft Intune não dão suporte à implantação de aplicativos.  

## <a name="general-considerations"></a>Considerações gerais  
 É possível usar o System Center Configuration Manager para implantar aplicativos em computadores Mac que executam o cliente Mac do Configuration Manager. As etapas para implantar o software em computadores Mac são semelhantes às etapas para implantar o software em computadores Windows. No entanto, antes de criar e implantar aplicativos para computadores Mac gerenciados pelo Configuration Manager, considere o seguinte:  

-   Antes de implantar pacotes de aplicativos Mac em computadores Mac, será necessário usar a ferramenta **CMAppUtil** em um computador Mac para converter esses aplicativos em um formato que possa ser lido pelo Configuration Manager.  

-   O Configuration Manager não dá suporte a implantação de aplicativos Mac em usuários. Em vez disso, essas implantações devem ser em um dispositivo. Da mesma forma, para implantações de aplicativos Mac, o Configuration Manager não dá suporte à opção **Pré-implantar software no dispositivo primário do usuário** na página **Configurações de Implantação** do **Assistente de Implantação de Software**.  

-   Os aplicativos Mac dão suporte para implantações simuladas.  

-   Você não pode implantar aplicativos em computadores Mac com a finalidade de **Disponível**.  

-   Não há suporte para a opção de enviar pacotes de ativação ao implantar o software em computadores Mac.  

-   Os computadores Mac não dão suporte para BITS (Serviço de Transferência Inteligente em Segundo Plano) para fazer o download de conteúdo do aplicativo. Se o download de um aplicativo falhar, ele será reiniciado.  

-   O Configuration Manager não dá suporte a condições globais quando você cria tipos de implantação para computadores Mac.  

## <a name="steps-to-create-and-deploy-an-application"></a>Etapas para criar e implantar um aplicativo  
 A tabela a seguir fornece as etapas, os detalhes e as informações para criar e implantar aplicativos para computadores Mac.  


|                                         Etapa                                          |                                                                                                             Detalhes                                                                                                              |
|---------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|            **Etapa 1**: Preparar aplicativos Mac para o Configuration Manager             | Antes de criar aplicativos do Configuration Manager por meio dos pacotes de software Mac, é necessário usar a ferramenta **CMAppUtil** em um computador Mac para converter o software Mac em um arquivo <strong>.cmmac</strong> do Configuration Manager. |
| **Etapa 2**: Criar um aplicativo do Configuration Manager que contém o software do Mac |                                                                       Use o **Assistente para Criar Aplicativo** para criar um aplicativo para o software do Mac.                                                                       |
|             **Etapa 3**: Criar um tipo de implantação para o aplicativo Mac              |                                                              Esta etapa é necessária somente se você não importou automaticamente essas informações do aplicativo.                                                               |
|                        **Etapa 4**: Implantar o aplicativo Mac                         |                                                                          Use o **Assistente de Implantação de Software** para implantar o aplicativo em computadores Mac.                                                                          |
|               **Etapa 5**: Monitorar a implantação do aplicativo Mac               |                                                                                 Monitore o sucesso das implantações de aplicativos em computadores Mac.                                                                                 |

## <a name="supplemental-procedures-to-create-and-deploy-applications-for-mac-computers"></a>Procedimentos complementares para criar e implantar aplicativos para computadores Mac  
 Use os procedimentos a seguir criar e implantar aplicativos para computadores Mac gerenciados pelo Configuration Manager.  

###  <a name="step-1-prepare-mac-applications-for-configuration-manager"></a>Etapa 1: Preparar aplicativos Mac para o Configuration Manager  
 O processo para a criação e implantação de aplicativos do Configuration Manager em computadores Mac é semelhante ao processo de implantação para computadores Windows. No entanto, antes de criar aplicativos do Configuration Manager que contenham tipos de implantação do Mac, é necessário preparar os aplicativos usando a ferramenta **CMAppUtil**. Essa ferramenta é baixada com os arquivos de instalação do cliente Mac. A ferramenta **CMAppUtil** pode coletar informações sobre o aplicativo, que incluem dados de detecção dos seguintes pacotes do Mac:  

-   Imagem de disco da Apple (.dmg)  

-   Arquivo do pacote meta (.mpkg)  

-   Pacote do Mac OS X Installer (.pkg)  

-   Aplicativo do Mac OS X (.app)  

Depois que ele coleta informações do aplicativo, a **CMAppUtil** cria um arquivo com a extensão **.cmmac**. Este arquivo contém os arquivos de instalação para o software do Mac e informações sobre métodos de detecção que podem ser usados para avaliar se o aplicativo já está instalado. O**CMAppUtil** também pode processar arquivos do **.dmg** que contêm vários aplicativos Mac e criar diferentes tipos de implantação para cada aplicativo.  

1.  Copie o pacote e instalação do software do Mac para a pasta no computador Mac onde você extraiu o conteúdo do arquivo **macclient.dmg** que foi baixado do Centro de Download da Microsoft.  

2.  No mesmo computador Mac, abra uma janela do terminal e navegue até a paste onde você extraiu o conteúdo do arquivo **macclient.dmg** .  

3.  Navegue até a pasta **Ferramentas** e digite o seguinte comando de linha de comando:  

     **./CMAppUtil** *<propriedades\>*  

     Por exemplo, digamos que você deseja converter o conteúdo de um arquivo de imagem de disco da Apple chamado **MySoftware.dmg** que está armazenado na pasta da área de trabalho do usuário em um arquivo **cmmac** na mesma pasta. Você também deseja criar arquivos **cmmac** para todos os aplicativos que são encontrados no arquivo de imagem de disco. Para fazer isso, use a seguinte linha de comando:  

     **./CMApputil –c /Users/** *<Nome de usuário\>* **/Desktop/MySoftware.dmg -o /Users/** *<Nome de usuário\>* **/Desktop -a**  

    > [!NOTE]  
    >  O nome do aplicativo não pode ter mais de 128 caracteres.  

     Para configurar opções para a **CMAppUtil**, use as propriedades da linha de comando na seguinte tabela:  

    |Propriedade|Mais informações|  
    |--------------|----------------------|  
    |**-h**|Exibe as propriedades de linha de comando disponíveis.|  
    |**-r**|Produz o **detection.xml** do arquivo **.cmmac** fornecido para **stdout**. A saída contém os parâmetros de detecção e a versão da **CMAppUtil** usada para criar o arquivo **.cmmac** .|  
    |**-c**|Especifica o arquivo de origem a ser convertido.|  
    |**-o**|Especifica o caminho de saída em conjunto com a propriedade -c.|  
    |**-a**|Cria automaticamente os arquivos .cmmac em conjunto com a propriedade -c para todos os aplicativos e pacotes no arquivo de imagem de disco.|  
    |**-s**|Ignora a geração do **detection.xml** se nenhum parâmetro de detecção for encontrado e força a criação do arquivo **.cmmac** sem o arquivo **detection.xml** .|  
    |**-v**|Exibe saída mais detalhada da ferramenta **CMAppUtil** junto com informações de diagnóstico.|  

4.  Verifique se o arquivo **.cmmac** foi criado na pasta de saída que você especificou.  

###  <a name="create-a-configuration-manager-application-that-contains-the-mac-software"></a>Criar um aplicativo do Configuration Manager que contém o software do Mac  

Use o procedimento a seguir para ajudar a criar um aplicativo para computadores Mac gerenciados pelo Configuration Manager.  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.  

3.  Na guia **Início**, no grupo **Criar**, escolha **Criar Aplicativo**.  

4.  Na página **Geral** do **Assistente para Criar Aplicativo**, selecione **Detectar automaticamente informações sobre este aplicativo em arquivos de instalação**.  

    > [!NOTE]  
    >  Se você mesmo deseja especificar informações sobre o aplicativo, selecione **Especificar manualmente as informações do aplicativo**. Para obter mais informações sobre como especificar as informações manualmente, consulte [Como criar aplicativos com o System Center Configuration Manager](../../apps/deploy-use/create-applications.md).  

5.  Na lista suspensa **Tipo** , selecione **Mac OS X**.  

6.  No campo **Local**, especifique o caminho UNC no formato *\\\\<servidor\>\\<compartilhamento\>\\<nomedoarquivo\>* para o arquivo de instalação do aplicativo Mac (arquivo **.cmmac**) que detectará as informações do aplicativo. Como alternativa, escolha **Procurar** para procurar e especificar o local do arquivo de instalação.  

    > [!NOTE]  
    >  É necessário ter acesso ao caminho UNC que contém o aplicativo.  

7.  Escolha **Próxima**.  

8.  Na página **Importar informações** do **Assistente para Criar Aplicativo**, examine as informações que foram importadas. Se necessário, você pode escolher **Anterior** para voltar e corrigir os erros. Escolha **Avançar** para continuar.  

9. Na página **Informações Gerais** do **Assistente para Criar Aplicativo**, especifique informações sobre o aplicativo, tais como nome do aplicativo, comentários, versão e uma referência opcional para ajudar a fazer referência ao aplicativo no console do Configuration Manager.  

    > [!NOTE]  
    >  Algumas das informações do aplicativo já podem estar nesta página se foram obtidas previamente dos arquivos de instalação do aplicativo.  

10. Escolha **Avançar**, examine as informações do aplicativo na página **Resumo** e conclua o **Assistente para Criar Aplicativo**.  

11. O novo aplicativo é exibido no nó **Aplicativos** do console do Configuration Manager.  

###  <a name="step-3-create-a-deployment-type-for-the-mac-application"></a>Etapa 3: Criar um tipo de implantação para o aplicativo Mac  
 Use o procedimento a seguir para ajudar a criar um tipo de implantação para computadores Mac gerenciados pelo Configuration Manager.  

> [!NOTE]  
>  Se você importou automaticamente as informações sobre o aplicativo no **Assistente para Criar Aplicativo**, um tipo de implantação para o aplicativo já pode ter sido criado.  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.  

3.  Selecione um aplicativo. Em seguida, na guia **Início**, no grupo **Aplicativo**, escolha **Criar Tipo de Implantação** para criar um novo tipo de implantação para esse aplicativo.  

    > [!NOTE]  
    >  Você também pode iniciar o **Assistente para Criar Tipo de Implantação** no **Assistente para Criar Aplicativo** e na guia **Tipos de Implantação** da caixa de diálogo **Propriedades** do *<nome do aplicativo\>*.  

4.  Na página **Geral** do **Assistente para Criar Tipo de Implantação**, na lista suspensa **Tipo**, selecione **Mac OS X**.  

5.  No campo **Local**, especifique o caminho UNC no formato \\\\<servidor\>\\<compartilhamento\>\\<nomedoarquivo\> para o arquivo de instalação do aplicativo (arquivo **.cmmac**). Como alternativa, escolha **Procurar** para procurar e especificar o local do arquivo de instalação.  

    > [!NOTE]  
    >  É necessário ter acesso ao caminho UNC que contém o aplicativo.  

6.  Escolha **Próxima**.  

7.  Na página **Importar informações** do **Assistente para Criar Tipo de Implantação**, revise as informações que foram importadas. Se necessário, escolha **Anterior** para voltar e corrigir os erros. Escolha **Avançar** para continuar.  

8.  Na página **Informações gerais** do **Assistente para criar tipo de implantação**, especifique informações sobre o aplicativo, como nome do aplicativo, comentários e os idiomas em que o tipo de implantação está disponível.  

    > [!NOTE]  
    >  Algumas das informações do tipo de implantação já podem estar nesta página se foram obtidas previamente dos arquivos de instalação do aplicativo.  

9. Escolha **Próxima**.  

10. Na página **Requisitos** do **Assistente para Criar Tipo de Implantação**, você pode especificar as condições que devem ser atendidas antes que o tipo de implantação seja instalado em computadores Mac.  

11. Escolha **Adicionar** para abrir a caixa de diálogo **Criar Requisito** e adicionar um novo requisito.  

    > [!NOTE]  
    >  Você também pode adicionar novos requisitos na guia **Requisitos** da caixa de diálogo **Propriedades** do *<nome do tipo de implantação\>*.  

12. Na lista suspensa **Categoria** , selecione que esse requisito é para um dispositivo.  

13. Na lista suspensa **Condição**, selecione a condição que você deseja usar para avaliar se o computador Mac atende aos requisitos de instalação. O conteúdo desta lista varia dependendo da categoria selecionada.  

14. Na lista suspensa **Operador**, escolha o operador que será usado para comparar a condição selecionada com o valor especificado para avaliar se o usuário ou o dispositivo atende aos requisitos de instalação. Os operadores disponíveis variam dependendo da condição selecionada.  

15. No campo **Valor**, especifique os valores que serão usados com a condição selecionada e o operador, para avaliar se o usuário ou o dispositivo atende aos requisitos de instalação. Os valores disponíveis variam dependendo da condição e do operador que você selecionar.

16. Escolha **OK** para salvar a regra de requisito e fechar a caixa de diálogo **Criar Requisito**.  

17. Na página **Requisitos** do **Assistente para Criar Tipo de Implantação**, escolha **Avançar**.  

18. Na página **Resumo** do **Assistente para Criar Tipo de Implantação**, revise as ações a serem tomadas pelo assistente.  Se necessário, escolha **Anterior** para voltar e alterar o tipo de implantação. Escolha **Avançar** para criar o tipo de implantação.  

19. Após a conclusão da página **Andamento**, veja as ações que foram tomadas e escolha **Fechar** para concluir o **Assistente para Criar Tipo de Implantação**.  

20. Se tiver iniciado esse assistente no **Assistente para Criar Aplicativo**, você retornará para a página **Tipos de Implantação**.  

###  <a name="deploy-the-mac-application"></a>Implantar o aplicativo Mac  
 As etapas para implantar um aplicativo em computadores Mac são as mesmas que as etapas para implantar um aplicativo em computadores Windows, exceto pelas seguintes diferenças:  

-   Não há suporte para a implantação de aplicativos em usuários.  

-   As implantações com uma finalidade **Disponível** não têm suporte.  

-   Não há suporte para a opção **Pré-implantar software no dispositivo primário do usuário** na página **Configurações de Implantação** do **Assistente de Implantação de Software**.  

-   Como nos computadores Mac não há suporte para o Centro de Software, a configuração **Notificações do Usuário** na página **Experiência do Usuário** do **Assistente de Implantação de Software** é ignorada.  

-   Não há suporte para a opção de enviar pacotes de ativação ao implantar o software em computadores Mac.  

> [!NOTE]  
>  Você pode criar uma coleção que contenha somente computadores Mac. Para isso, crie uma coleção que usa uma regra de consulta e use o exemplo de consulta WQL no tópico [Como criar consultas](../../core/servers/manage/create-queries.md).  

 Para obter informações, confira [Deploy applications](../../apps/deploy-use/deploy-applications.md) (Implantar aplicativos).  

###  <a name="step-5-monitor-the-deployment-of-the-mac-application"></a>Etapa 5: Monitorar a implantação do aplicativo Mac  
 Você pode usar o mesmo processo para monitorar implantações de aplicativo em computadores Mac que você usaria para monitorar implantações de aplicativo em computadores Windows.  

 Para obter mais informações, consulte [Monitor applications (Monitorar aplicativos)](/sccm/apps/deploy-use/monitor-applications-from-the-console).  
