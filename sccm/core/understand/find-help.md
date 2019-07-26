---
title: Encontrar ajuda
titleSuffix: Configuration Manager
description: Localize recursos para informações adicionais sobre o Configuration Manager.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 86810629-cf2a-43e8-86a2-847444119fc1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: be9fd76105685a283931bc298e534a6a8f6683d8
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68340271"
---
# <a name="find-help-for-using-configuration-manager"></a>Localizar ajuda para usar o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo fornece as seguintes seções com vários recursos para encontrar ajuda para o uso do Configuration Manager:  

- [Documentação do produto](#bkmk_Info)  

- [Compartilhamento de comentários sobre o produto](#product-feedback)  

- [Siga o blog da equipe do Configuration Manager](#BKMK_ProductGroupBlog)  

- [Opções de suporte e recursos da comunidade](#BKMK_SupportOptions)  

Para obter ajuda com a acessibilidade de produto, veja [Recursos de acessibilidade](/sccm/core/understand/accessibility-features).  



##  <a name="bkmk_Info"></a> Documentação do produto  

Para acessar a documentação mais recente do produto, comece no [índice da biblioteca](https://docs.microsoft.com/sccm/).  

<a name="BKMK_SearchTips"></a>  

Para obter dicas de pesquisa, fornecer comentários e obter mais informações sobre como usar a documentação do produto, veja [Como usar os documentos](/sccm/core/understand/use-docs).  



<a name="product-feedback"></a>

## <a name="BKMK_1806Feedback"></a> Comentários sobre o produto da versão 1806 em diante

Do Configuration Manager versão 1806 em diante, você pode enviar comentários sobre o produto diretamente do console. Se você precisar anexar logs, use o [Hub de Comentários](#BKMK_FeedbackHub). É possível fazer o seguinte: <!--1357542-->

- **Enviar um sorriso**: enviar comentários sobre o que você gostou.
- **Enviar um rosto triste**: enviar comentários sobre o que você não gostou.
- **Enviar uma sugestão**: leva você para o [site UserVoice](https://configurationmanager.uservoice.com/) para compartilhar sua ideia.

  ![Enviar comentários no Configuration Manager 1806](media/1806-send-a-smile.png)


### <a name="send-a-smile"></a>Envie um Smiley

Para enviar comentários sobre algo que você gostou, siga as instruções abaixo: 
1. No canto superior direito do console, clique no smiley. 
2. No menu suspenso, selecione **Enviar um Smiley**.
3. Use a caixa de texto para explicar do que você gostou. 
4. Escolha se você gostaria de compartilhar seu endereço de email e uma captura de tela. 
5. Clique em **Enviar Comentários**
     - Se você não tiver conectividade com a Internet, clique em **Salvar** na parte inferior. Siga as instruções na seção [Enviar comentários que você salvou para envio posterior](#BKMK_NoInternet) para enviá-los à Microsoft. 

![Enviar formulário de comentários no Configuration Manager 1806](media/1806-feedback-form.png)


### <a name="send-a-frown"></a>Enviar um rosto triste

Para enviar comentários sobre algo de que você não gostou, siga as instruções abaixo:

1. No canto superior direito do console, clique no smiley. 
2. No menu suspenso, selecione **Enviar um rosto triste**.
3. Use a caixa de texto para explicar do que você não gostou. 
4. Escolha se você gostaria de compartilhar seu endereço de email e uma captura de tela. 
5. Clique em **Enviar Comentários**
     - Se você não tiver conectividade com a Internet, clique em **Salvar** na parte inferior. Siga as instruções na seção [Enviar comentários que você salvou para envio posterior](#BKMK_NoInternet) para enviá-los à Microsoft.  

### <a name="send-a-suggestion"></a>Enviar uma sugestão

Quando você **enviar uma sugestão**, será direcionado para [UserVoice](https://configurationmanager.uservoice.com/), um site de terceiros, para compartilhar sua ideia. A equipe de produto do Configuration Manager usa os seguintes valores de status do UserVoice:

- **Observado**: entendemos a solicitação e ela faz sentido. Nós a adicionamos à nossa lista de pendências.
- **Planejado**: começamos a codificação para esse recurso e esperamos que ele apareça em um build de visualização técnica dentro dos próximos meses.
- **Iniciado**: o recurso agora está em uma visualização técnica. Confira e envie seus comentários. Avise-nos se o recurso está no caminho certo ou não. Insira comentários adicionais na seção de comentários da solicitação original para as outras pessoas verem e comentarem. Leremos e usaremos os comentários para tentar melhorar o recurso.
- **Concluído**: a primeira versão do recurso está em um build de produção. Esse status não significa que concluímos totalmente o trabalho com o recurso e não o melhoraremos mais. Mas isso significa que a v1 dos recursos está em um build de produção e você pode começar a usá-los de fato. Estamos marcando como concluído porque:
  - Queremos informar a você que o recurso está pronto para produção.
  - Queremos devolver seus votos do UserVoice para que você possa usá-los em outros itens.
  - Você pode fazer novas Solicitações de Alteração de Design para esse recurso para nos ajudar a saber qual é a próxima melhoria mais importante para esse recurso.

### <a name="information-sent-with-feedback"></a>Informações enviadas com comentários

Quando você **enviar um smiley** ou **enviar um rosto triste**, as informações a seguir serão enviadas com os comentários:

- Informações do build do sistema operacional
- ID da hierarquia do Configuration Manager
- Informações de build do produto
- Informações de idioma
- Identificador de dispositivo 
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SQMClient:MachineId



### <a name="BKMK_NoInternet"></a> Enviar comentários que você salvou para envio posterior

1. Clique em **Salvar** na parte inferior da janela **Fazer comentários**. 
2. Salve o arquivo .zip. Se o computador local não tiver acesso à Internet, copie o arquivo para um computador conectado à Internet. 
3. Se necessário, copie a pasta UploadOfflineFeedback localizada em `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\`
    - Para obter mais informações sobre a pasta cd.latest, veja [A pasta CD.Latest](../servers/manage/the-cd.latest-folder.md)

4. Em um computador conectado à Internet, abra um prompt de comando. 
5. Execute o seguinte comando: `UploadOfflineFeedback.exe -f c:\folder\location_of.zip`
    
    - Opcionalmente, você pode especificar os seguintes parâmetros:
        -  `-t, --timeout` Tempo limite em segundos para enviar os dados. 0 é ilimitado. O padrão é 30.
        - `-s --silent` Nenhum registro em log no console (não é possível combinar com --verbose)
        - `-v, --verbose` Gera registro em log detalhado no console (não é possível combinar com -silent)
        - `--help` Exibe a tela de ajuda

## <a name="bkmk_feedbackid"></a> Confirmação de comentários do console

<!--3556010-->
Começando na versão 1902, quando você envia comentários por meio do console do Configuration Manager ou de UploadOfflineFeedback.exe, ele mostra uma mensagem de confirmação. Essa mensagem inclui uma **ID dos comentários**, que você pode fornecer à Microsoft como um identificador de acompanhamento.

- Para copiar a **ID do comentário**, selecione o ícone de cópia ao lado da ID ou use as teclas de atalho **CTRL** + **C**.
  - Essa ID não é armazenada no computador, portanto, copie-a antes de fechar a janela.
- Clicar em **Não mostrar esta mensagem novamente** suprimirá a caixa de diálogo e impedirá que ela apareça no futuro.

   ![Confirmação do comentário do console no Configuration Manager 1902](media/1902-feedback-id-example.png)
- A ferramenta de comando **UploadOfflineFeedback** grava a **FeedbackID** no console, a menos que -s ou --silent seja usado.

  ![Confirmação do comentário de UploadOfflineFeedback.exe no Configuration Manager 1902](media/1902-offline-feedback-id-example.png)

##  <a name="BKMK_FeedbackHub"></a> Comentários sobre o produto para as versões 1802 e anteriores

Relate defeitos do produto potenciais por meio do [aplicativo hub de comentários](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) interno do Windows 10. Ao **Adicionar novos comentários**, selecione a categoria **Enterprise Management** e, em seguida, escolha uma das seguintes subcategorias:
- Cliente do Configuration Manager
- Console do Configuration Manager
- Implantação de sistema operacional do Configuration Manager
- Configuration Manager Server

Continue usando a [página UserVoice](https://configurationmanager.uservoice.com/) para votar em ideias de novos recursos no Configuration Manager. A equipe de produto do Configuration Manager usa os seguintes valores de status do UserVoice:

- **Observado**: entendemos a solicitação e ela faz sentido. Nós a adicionamos à nossa lista de pendências.
- **Planejado**: começamos a codificação para esse recurso e esperamos que ele apareça em um build de visualização técnica dentro dos próximos meses.
- **Iniciado**: o recurso agora está em uma visualização técnica. Confira e envie seus comentários. Avise-nos se o recurso está no caminho certo ou não. Insira comentários adicionais na seção de comentários da solicitação original para as outras pessoas verem e comentarem. Leremos e usaremos os comentários para tentar melhorar o recurso.
- **Concluído**: a primeira versão do recurso está em um build de produção. Esse status não significa que concluímos totalmente o trabalho com o recurso e não o melhoraremos mais. Mas isso significa que a v1 dos recursos está em um build de produção e você pode começar a usá-los de fato. Estamos marcando como concluído porque:
  - Queremos informar a você que o recurso está pronto para produção.
  - Queremos devolver seus votos do UserVoice para que você possa usá-los em outros itens.
  - Você pode fazer novas Solicitações de Alteração de Design para esse recurso para nos ajudar a saber qual é a próxima melhoria mais importante para esse recurso.

##  <a name="BKMK_ProductGroupBlog"></a> Blog da equipe do Configuration Manager  

As equipes de engenharia e parceiros do Configuration Manager usam o [blog do Enterprise Mobility + Security](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager) para fornecer informações técnicas e outras novidades sobre o Configuration Manager e as tecnologias relacionadas. Nossas postagens no blog complementam as informações de suporte e documentação do produto.  


##  <a name="BKMK_SupportOptions"></a> Opções de suporte e recursos da comunidade  

Os links a seguir fornecem informações sobre as opções de suporte e os recursos da comunidade:  

-   [Suporte da Microsoft](https://aka.ms/cmcbsupport)  

-   [Comunidade do Configuration Manager: Guia de sobrevivência do System Center Configuration Manager (Branch Atual)](https://social.technet.microsoft.com/wiki/contents/articles/33035.system-center-configuration-manager-current-branch-survival-guide.aspx )  

-   [Página de fóruns do Configuration Manager](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)  
    <!-- NOTE: the above URL requires "en-US" for the category to work -->
