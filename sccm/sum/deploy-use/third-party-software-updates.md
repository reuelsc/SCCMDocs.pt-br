---
title: Habilitar atualizações de terceiros
titleSuffix: Configuration Manager
description: Habilitar as atualizações de terceiros no Configuration Manager
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 946b0f74-0794-4e8f-a6af-9737d877179b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3c31b950ef59147f6f3f46c1cba7780b7789948c
ms.sourcegitcommit: 4b7812b505e80f79fc90dfa8a6db06eea79a3550
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2018
ms.locfileid: "42584590"
---
# <a name="enable-third-party-updates"></a>Habilitar atualizações de terceiros 

*Aplica-se a: System Center Configuration Manager versão 1806*

Da versão 1806 em diante, o nó **Catálogos de Atualização de Software de Terceiros** no console do Configuration Manager permite que você assine catálogos de terceiros, publique suas atualizações em seu SUP (ponto de atualização de software) e, em seguida, implante-as nos clientes.  <!--1357605, 1352101, 1358714-->



## <a name="prerequisites"></a>Pré-requisitos 
- Espaço em disco suficiente no ponto de atualização de software de nível superior, a pasta WSUSContent, para armazenar o conteúdo binário de origem para atualizações de software de terceiros.
    - A quantidade de armazenamento necessário varia de acordo com o fornecedor, os tipos de atualizações e as atualizações específicas que você publica para implantação.
    - Se você precisar mover a pasta WSUSContent para outra unidade com mais espaço livre, leia a postagem no blog [How to change the location where WSUS stores updates locally](https://blogs.technet.microsoft.com/sus/2008/05/19/wsus-how-to-change-the-location-where-wsus-stores-updates-locally/) (Como alterar o local em que o WSUS armazena as atualizações localmente).
- O serviço de sincronização de atualização de software de terceiros requer acesso à Internet.
    - Para obter a lista de catálogos de parceiros, download.microsoft.com pela porta HTTPS 443 é necessário. 
    -  Acesso à Internet a todos os catálogos de produtos de terceiros e os arquivos de conteúdo de atualização. Portas adicionais diferente de 443 podem ser necessárias.
    - Atualizações de terceiros usam as mesmas configurações de proxy que SUP.

## <a name="additional-requirements-when-the-sup-is-remote-from-the-top-level-site-server"></a>Requisitos adicionais quando SUP é remoto do servidor do site de nível superior 

1. SSL deverá ser habilitado no SUP quando ele for remoto. 
    - [Configurar SSL no WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#bkmk_2.5.ConfigSSL)
        - Quando você configura SSL no WSUS, observe alguns dos serviços Web e os diretórios virtuais são sempre HTTP, e não HTTPS. 
        - O Configuration Manager baixa o conteúdo de terceiros para pacotes de atualização de software do seu diretório de conteúdo do WSUS por HTTP.   
    - [Configurar SSL no SUP](../get-started/install-a-software-update-point.md#configure-ssl-communications-to-wsus)

2. Para permitir a criação do certificado autoassinados do WSUS: 
   - O Registro remoto deve ser habilitado no servidor SUP.
   -  A **conta de conexão de servidor do WSUS** deve ter permissões de registro remoto no servidor WSUS/SUP. 


3. Crie a seguinte chave do Registro no servidor do site do Configuration Manager: 
    - `HKLM\Software\Microsoft\Update Services\Server\Setup`, crie um novo DWORD chamado **EnableSelfSignedCertificates** com um valor de `1`. 

4. Para habilitar a instalação do certificado nos repositórios de Fornecedores Confiáveis e de Raiz Confiável no servidor SUP remoto:
   - A **conta de conexão de servidor do WSUS** deve ter permissões de administração remota no servidor SUP.

    Se esse item não for possível, exporte o certificado do repositório WSUS do computador local para os repositórios de Fornecedor Confiável e de Raiz confiável. 

> [!NOTE] 
>A **conta de conexão do servidor do WSUS** pode ser identificada exibindo a guia **Configurações de Proxy e Conta** nas propriedades de função do Sistema de Sites do SUP. Se uma conta não for especificada, a conta do computador do servidor do site será usada.

## <a name="enable-third-party-updates-on-the-sup"></a>Habilitar atualizações de terceiros no SUP
Se você habilitar essa opção, poderá assinar os catálogos de atualizações de terceiros no console do Configuration Manager. Em seguida, poderá publicar essas atualizações no WSUS e implantá-las para os clientes. Execute as seguintes etapas uma vez por hierarquia para habilitar e configurar o recurso a ser usado. As etapas talvez precisem ser executadas novamente se você nunca substituir o servidor do WSUS do SUP de nível superior. 

1. No console do Configuration Manager, acesse o espaço de trabalho **Administração**. Expanda **Configuração do Site** e selecione o nó **Sites**.
2. Selecione o site de nível superior na hierarquia. Na faixa de opções, clique em **Configurar Componentes do Site** e selecione **Ponto de Atualização de Software**.
3. Mude para a guia **Atualizações de Terceiros**. Selecione a opção **Habilitar atualizações de software de terceiros**.

    ![Captura de tela de propriedades do SUP de atualizações de terceiros](media/third-party-sup-properties.PNG)


## <a name="configure-the-wsus-signing-certificate"></a>Configurar o certificado de autenticação do WSUS
Você precisará decidir se deseja que o Configuration Manager gerencie automaticamente o certificado de autenticação do WSUS de terceiros ou se precisa configurar manualmente o certificado. 

### <a name="automatically-manage-the-wsus-signing-certificate"></a>Gerenciar automaticamente o certificado de autenticação do WSUS
Se você não tiver um requisito para usar certificados PKI, poderá optar por gerenciar automaticamente os certificados de autenticação para atualizações de terceiros. O gerenciamento de certificados do WSUS é feito como parte do ciclo de sincronização e é registrado em log em `wsyncmgr.log`. 

1. No console do Configuration Manager, acesse o espaço de trabalho **Administração**. Expanda **Configuração do Site** e selecione o nó **Sites**.
2. Selecione o site de nível superior na hierarquia. Na faixa de opções, clique em **Configurar Componentes do Site** e selecione **Ponto de Atualização de Software**.
3. Mude para a guia **Atualizações de Terceiros**. Selecione a opção **Configuration Manager gerencia o certificado**. 
4. Um novo certificado do tipo **Assinatura do WSUS de Terceiros** é criado no nó **Certificados** em **Segurança** no espaço de trabalho **Administração**.  

### <a name="manually-manage-the-wsus-signing-certificate"></a>Gerenciar manualmente o certificado de autenticação do WSUS
Se você precisar configurar manualmente o certificado, por exemplo, houver necessidade de usar um certificado PKI, use o [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server) ou outra ferramenta para isso.  

1. Configure o certificado de autenticação usando o [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server).
2. No console do Configuration Manager, acesse o espaço de trabalho **Administração**. Expanda **Configuração do Site** e selecione o nó **Sites**.
3. Selecione o site de nível superior na hierarquia. Na faixa de opções, clique em **Configurar Componentes do Site** e selecione **Ponto de Atualização de Software**.
4. Mude para a guia **Atualizações de Terceiros**. Selecione a opção **Gerenciar o certificado manualmente**.


## <a name="enable-third-party-updates-on-the-clients"></a>Habilite atualizações de terceiros nos clientes
Habilite atualizações de terceiros em clientes nas configurações do cliente. A configuração define a política de agente do Windows Update para [Permitir atualizações assinadas para um local do serviço Microsoft Update na intranet](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates#BKMK_comp3). Essa configuração do cliente também instala o certificado de autenticação do WSUS para o repositório Fornecedores Confiáveis no cliente. O registro em log do gerenciamento de certificado é visto em `updatesdeployment.log` nos clientes.  Execute estas etapas para cada configuração personalizada do cliente que você deseja usar para atualizações de terceiros. Para obter mais informações, leia o artigo [Sobre as configurações do cliente](/sccm/core/clients/deploy/about-client-settings#Enable-third-party-software-updates).

1. No console do Configuration Manager, vá até o espaço de trabalho **Administração** e selecione o nó **Configurações do Cliente**.
2. Selecione uma configuração personalizada de cliente existente ou crie uma nova. 
3. Selecione a guia **Atualizações de Software** no lado esquerdo. Se você não tiver essa guia, verifique se a caixa **Atualizações de Software** está habilitada.
4. Defina **Habilitar atualizações de software de terceiros** como **Sim**. 


## <a name="add-a-custom-catalog"></a>Adicionar um catálogo personalizado
*Catálogos de parceiros* são catálogos de fornecedores de software que têm suas informações já registradas com a Microsoft. Com os catálogos de parceiros, você pode assiná-los sem precisar especificar nenhuma informação adicional. Os catálogos que você adicionar são chamados *catálogos personalizados*. Você pode adicionar um catálogo personalizado de um fornecedor de atualização de terceiros ao Configuration Manager. Catálogos personalizados devem usar https e as atualizações devem ser assinadas digitalmente. 

1. Vá para o espaço de trabalho **Biblioteca de Atualizações de Software**, expanda **Atualizações de software** e selecione o nó **Catálogos de Atualizações de Software de Terceiros**. 
   
     ![Captura de tela de nó de atualizações de terceiros](media/third-party-updates-node.PNG)
2. Clique em **Adicionar Catálogo Personalizado** na faixa de opções. 

     ![Catálogo personalizado para adicionar atualizações de terceiros](media/third-party-updates-custom-catalog.png)
1. Na página **Geral**, especifique os itens a seguir: 
    - **URL de download**: um endereço HTTPS válido do catálogo personalizado.
    - **Publicador**: o nome da organização que publica o catálogo. 
    - **Nome**: o nome do catálogo a ser exibido no Console do Configuration Manager. 
    - **Descrição**: uma descrição do catálogo. 
    - **URL de suporte** (opcional): um endereço HTTPS válido de um site para obter ajuda com o catálogo. 
    - **Contatar Suporte** (opcional): informações de contato para obter ajuda com o catálogo. 
2. Clique em **Avançar** para examinar o resumo de catálogo e continuar com o preenchimento do **Assistente de Catálogo Personalizado de Atualizações de Software de Produtos de Terceiros**.


## <a name="subscribe-to-a-third-party-catalog-and-sync-updates"></a>Assine um catálogo de terceiros e sincronize as atualizações
Quando você assina um catálogo de terceiros no console do Configuration Manager, os metadados para cada atualização no catálogo são sincronizados com os servidores do WSUS para seu SUPs. A sincronização dos metadados permite que os clientes determinem se alguma das atualizações é aplicável. Execute as seguintes etapas para cada catálogo de terceiros que você deseja assinar:  

1. No console do Configuration Manager, acesse o espaço de trabalho **Biblioteca de Software**. Expanda **Atualizações de Software** e selecione o nó **Catálogos de Atualização de Software de Terceiros**.  
2. Selecione o catálogo a ser assinado e clique em **Assinar Catálogo** na faixa de opções. 
    ![Catálogo personalizado para adicionar atualizações de terceiros](media/third-party-updates-subscribe.png)
1. Examine e aprove o certificado do catálogo.  
    >[!NOTE]
    
    > Quando você assina um catálogo de atualizações de software de terceiros, o certificado que você examina e aprova no assistente é adicionado ao site. Esse certificado é do tipo **Catálogo de Atualizações de Software de Terceiros**. Você pode gerenciá-lo por meio do nó **Certificados** em **Segurança** no espaço de trabalho **Administração**.  
2. Conclua o assistente. Após a assinatura inicial, o download do catálogo deverá ser iniciado em alguns minutos. 
    - O catálogo é sincronizado automaticamente a cada sete dias.
    - Clique em **Sincronizar agora** na faixa de opções para forçar uma sincronização.
3. Depois de baixar o catálogo, os metadados do produto precisam ser sincronizados do banco de dados do WSUS com o banco de dados do Configuration Manager. [Inicie manualmente a sincronização de atualizações de software](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) para sincronizar as informações do produto.
4. Depois que as informações do produto estiverem sincronizadas, [Configure o SUP para sincronizar o produto desejado](../get-started/configure-classifications-and-products.md#to-configure-classifications-and-products-to-synchronize) no Configuration Manager.  
5. [Inicie manualmente a sincronização de atualizações de software](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) para sincronizar as atualizações do produto novo no Configuration Manager.  
6. Quando a sincronização for concluída, você poderá ver as atualizações de terceiros no nó **Todas as Atualizações**. Essas atualizações são publicadas como atualizações **somente de metadados** até você optar por publicá-las. 
     - O ícone com a seta azul representa uma atualização de software somente de metadados. ![Ícone de atualização de software somente de metadados](media/MetadataOnly.png)


## <a name="publish-and-deploy-third-party-software-updates"></a>Publicar e implantar atualizações de software de terceiros 
Depois que as atualizações de terceiros estiverem no nó **Todas as Atualizações**, você pode escolher quais atualizações devem ser publicadas para a implantação. Quando você publica uma atualização, os arquivos binários são baixados do fornecedor e colocados no diretório WSUSContent no SUP de nível superior. 

1. No console do Configuration Manager, acesse o espaço de trabalho **Biblioteca de Software**. Expanda **Atualizações de Software** e selecione o nó **Todas as Atualizações de Software**.
2. Clique em **Adicionar Critérios** para filtrar a lista de atualizações. Por exemplo, adicione **Fornecedor** para **HP**. para exibir todas as atualizações da HP.  
3. Selecione as atualizações exigidas pela sua organização. Clique **Publicar Conteúdo de Atualização de Software de Terceiros**.
    - Essa ação baixa os binários de atualização do fornecedor e, em seguida, armazena-as na pasta WSUSContent no ponto de atualização de software de nível superior. 
4. [Inicie manualmente a sincronização de atualizações de software](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) para alterar o estado das atualizações publicadas de somente metadados para atualizações implantáveis com conteúdo. 
    >[!NOTE]
    >Quando você publicar o conteúdo de atualização de software de terceiros, todos os certificados usados para assinar o conteúdo serão adicionados ao site. Esses certificados são do tipo **Conteúdo de Atualizações de Software de Terceiros**. Você pode gerenciá-los por meio do nó **Certificados** em **Segurança** no espaço de trabalho **Administração**.  

5. Examine o progresso no SMS_ISVUPDATES_SYNCAGENT.log. O log está localizado no ponto de atualização de software de nível superior na pasta Logs do sistema de sites.
6. Implante as atualizações usando o processo [Implantar atualizações de software](../deploy-use/deploy-software-updates.md). 
7. Na página **Locais de Download** do **Assistente para Implantar Atualizações de Software**, selecione a opção padrão para **Baixar atualizações de software da Internet**. Nesse cenário, o conteúdo já está publicado no ponto de atualização de software, que é usado para baixar o conteúdo do pacote de implantação.
8. Os clientes precisarão executar uma verificação e avaliar as atualizações antes que você possa ver os resultados de conformidade.  Você pode disparar esse ciclo manualmente usando o painel de controle do Configuration Manager em um cliente executando a ação **Ciclo de Verificação de Atualizações de Software**.


## <a name="monitoring-progress-of-third-party-software-updates"></a>Monitorando o andamento das atualizações de software de terceiros 

A sincronização de atualizações de software de terceiros é tratada pelo componente SMS_ISVUPDATES_SYNCAGENT no ponto de atualização de software padrão de nível superior. Você pode exibir as mensagens de status desse componente ou consultar um status mais detalhado no SMS_ISVUPDATES_SYNCAGENT.log. Esse log está no ponto de atualização de software de nível superior na pasta de logs do sistema do site. Por padrão, esse caminho é C:\Arquivos de Programas\Microsoft Configuration Manager\Logs. Para obter mais informações sobre como monitorar o processo geral de gerenciamento de atualizações de software, veja [Monitorar atualizações de software](../deploy-use/monitor-software-updates.md) 

## <a name="known-issues"></a>Problemas conhecidos

- O computador em que o console está sendo executado é usada para baixar as atualizações do WSUS e adicioná-las ao pacote de atualizações. O certificado de autenticação do WSUS deve ser confiável no computador do console. Se não for, você poderá ter problemas com a verificação de assinatura durante o download de atualizações de terceiros. 
- O serviço de sincronização de atualização de software de terceiros não consegue publicar conteúdo para atualizações somente de metadados adicionadas ao WSUS por outro aplicativo, ferramenta ou script, como SCUP. A ação **Publicar conteúdo de atualização de software de terceiros** falha nessas atualizações. Se você precisar implantar atualizações de terceiros que ainda não sejam compatíveis com esse recurso, use o processo existente por completo para implantar essas atualizações.  
-  O Configuration Manager tem uma nova versão para o formato de arquivo cab do catálogo. A nova versão inclui os certificados para os arquivos binários do fornecedor. Esses certificados são adicionados ao nó **Certificados** em **Segurança** no espaço de trabalho **Administração** depois que você aprova o catálogo de confiança.  
     - Você ainda pode usar a versão mais antiga do arquivo cab do catálogo, desde que a URL de download seja https e as atualizações sejam assinadas. A publicação do conteúdo falhará porque os certificados para os binários não estão no arquivo cab e já aprovados. Você pode contornar esse problema localizando o certificado no nó **Certificados**, desbloqueá-lo e, em seguida, publicar a atualização novamente. Se você estiver publicando várias atualizações assinadas com diferentes certificados, precisará desbloquear cada certificado usado.
     - Para obter mais informações, veja as mensagens de status 11523 e 11524 na tabela de mensagem de status a seguir.
-  Quando o serviço de sincronização de atualização de software de terceiros no ponto de atualização de nível superior precisa de um servidor proxy para acesso à Internet, as verificações de assinatura digital podem falhar. Para atenuar esse problema, defina as configurações de proxy de WinHTTP no sistema do site. Para saber mais, confira [Comandos Netsh para WinHTTP](https://go.microsoft.com/fwlink/p/?linkid=199086).

## <a name="status-messages"></a>Mensagens de status

| MessageID       | Severidade           | Descrição | Causa possível| Possível solução
| ------------- |-------------| -----|----|----|
| 11516     | Erro |Falha ao publicar o conteúdo para atualizar a "ID de Atualização" porque o conteúdo não assinado.  Somente o conteúdo com assinaturas válidas pode ser publicado.  |O Configuration Manager não permite que atualizações não assinadas sejam publicadas.| Publica a atualização de maneira alternativa. </br></br>Veja se uma atualização assinada está disponível do fornecedor.|
| 11523  | Aviso |  O catálogo de "X" não inclui certificados de assinatura de conteúdo, tentativas de publicar o conteúdo para atualização desse catálogo poderão não obter sucesso até que os certificados de assinatura do conteúdo sejam adicionados e aprovados. | Essa mensagem pode ocorrer quando você importa um catálogo que está usando uma versão mais antiga do formato de arquivo cab.|Entre em contato com o provedor do catálogo para obter um catálogo atualizado que inclua os certificados de assinatura de conteúdo. </br> </br> Os certificados para os binários não estão incluídos no arquivo cab, de modo que a publicação do conteúdo cab falhará. Você pode contornar esse problema localizando o certificado no nó **Certificados**, desbloqueá-lo e, em seguida, publicar a atualização novamente. Se você estiver publicando várias atualizações assinadas com diferentes certificados, precisará desbloquear cada certificado usado.|
| 11524| Erro  | Falha ao publicar a "ID" de atualização devido à ausência de metadados de atualização. | A atualização pode ter sido sincronizada com o WSUS fora do Configuration Manager.| Sincronize a atualização com o Configuration Manager antes de tentar publicar seu conteúdo.  </br> </br>Se uma ferramenta externa tiver sido usada para publicar a atualização como **Somente metadados**, use a mesma ferramenta para publicar o conteúdo da atualização.|



## <a name="working-with-third-party-updates-video"></a>Como trabalhar com vídeo de atualizações de terceiros
<iframe width="560" height="315" src="https://www.youtube.com/embed/ai8rLCLtuTI?rel=0" frameborder="0" allowfullscreen></iframe>



## <a name="next-step"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Implantar atualizações de software](./deploy-software-updates.md)
