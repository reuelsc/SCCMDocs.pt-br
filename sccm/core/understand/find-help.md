---
title: Encontrar ajuda
titleSuffix: Configuration Manager
description: Localize recursos para informações adicionais sobre o Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 86810629-cf2a-43e8-86a2-847444119fc1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f9c4b9bdbd67e26962a4de3ff66643f071339795
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56139469"
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


### <a name="information-sent-with-feedback"></a>Informações enviadas com comentários
 
   - Informações do build do sistema operacional
   - ID da hierarquia do Configuration Manager
   - Informações de build do produto
   - Informações de idioma
   - Identificador de dispositivo 
       - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SQMClient:MachineId


### <a name="BKMK_NoInternet"></a> Enviar comentários que você salvou para envio posterior

1. Clique em **Salvar** na parte inferior da janela **Fazer comentários**. 
2. Salve o arquivo .zip. Se o computador local não tiver acesso à Internet, copie o arquivo para um computador conectado à Internet. 
3. Se necessário, copie UploadOfflineFeedback.exe, localizado em `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe`
    - Para obter mais informações sobre a pasta cd.latest, veja [A pasta CD.Latest](../servers/manage/the-cd.latest-folder.md)

4. Em um computador conectado à Internet, abra um prompt de comando. 
5. Execute o seguinte comando: `UploadOfflineFeedback.exe -f c:\folder\location_of.zip`
    
    - Opcionalmente, você pode especificar o seguinte:
        -  `-t, --timeout` Tempo limite em segundos para enviar os dados. 0 é ilimitado. O padrão é 30.
        - `-s --silent` Nenhum registro em log no console (não é possível combinar com --verbose)
        - `-v, --verbose` Gera registro em log detalhado no console (não é possível combinar com -silent)
        - `--help` Exibe a tela de ajuda



##  <a name="BKMK_FeedbackHub"></a> Comentários sobre o produto para as versões 1802 e anteriores

Relate defeitos do produto potenciais por meio do [aplicativo hub de comentários](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) interno do Windows 10. Ao **Adicionar novos comentários**, selecione a categoria **Enterprise Management** e, em seguida, escolha uma das seguintes subcategorias:
 - Cliente do Gerenciador de Configurações
 - Console do Configuration Manager
 - Implantação de sistema operacional do Configuration Manager
 - Configuration Manager Server

Continue usando a [página UserVoice](https://configurationmanager.uservoice.com/) para votar em ideias de novos recursos no Configuration Manager.


##  <a name="BKMK_ProductGroupBlog"></a> Blog da equipe do Configuration Manager  

As equipes de engenharia e parceiros do Configuration Manager usam o [blog do Enterprise Mobility + Security](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager) para fornecer informações técnicas e outras novidades sobre o Configuration Manager e as tecnologias relacionadas. Nossas postagens no blog complementam as informações de suporte e documentação do produto.  


##  <a name="BKMK_SupportOptions"></a> Opções de suporte e recursos da comunidade  

Os links a seguir fornecem informações sobre as opções de suporte e os recursos da comunidade:  

-   [Suporte da Microsoft](https://aka.ms/cmcbsupport)  

-   [Comunidade do Configuration Manager: Guia de sobrevivência do System Center Configuration Manager (Branch Atual)](https://social.technet.microsoft.com/wiki/contents/articles/33035.system-center-configuration-manager-current-branch-survival-guide.aspx )  

-   [Página de fóruns do Configuration Manager](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)  
    <!-- NOTE: the above URL requires "en-US" for the category to work -->
