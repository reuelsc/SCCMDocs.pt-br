---
title: Upgrade Readiness | System Center Configuration Manager
description: "Integre o Upgrade Readiness com o Configuration Manager. Acessar dados de compatibilidade de atualização no seu console de administração. Dispositivos de destino para atualização ou correção."
keywords: 
author: brenduns
ms.author: brenduns
manager: angerobe
ms.date: 3/1/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
translationtype: Human Translation
ms.sourcegitcommit: 460089ce58910b68eb0a613bce0166754850844b
ms.openlocfilehash: 9361c66228cf54eb1daf8138cd03fc8f6139f48d
ms.lasthandoff: 03/01/2017


---

# <a name="integrate-upgrade-readiness-with-system-center-configuration-manager"></a>Integrar o Upgrade Readiness com o System Center Configuration Manager
O Upgrade Readiness (anteriormente Upgrade Analytics) permite que você avalie e analise a preparação e a compatibilidade do dispositivo com o Windows 10 para permitir atualizações mais fáceis e estáveis. Integre o Upgrade Readiness ao Configuration Manager para acessar dados de compatibilidade de atualização de cliente no console de administração do Configuration Manager. Você então poderá direcionar os aplicativos para atualização ou correção da lista de dispositivos.

O Upgrade Readiness é uma solução no OMS (Microsoft Operations Management Suite). Você pode ler mais sobre o Upgrade Readiness em [Get started with Upgrade Readiness](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness) (Introdução ao Upgrade Readiness).

## <a name="configure-clients"></a>Configurar clientes

Há várias etapas de configuração que você precisa realizar para garantir que os clientes possam fornecer dados para o Upgrade Readiness:

-  Defina as configurações de telemetria do cliente, conforme descrito em [Configurar telemetria do Windows em sua organização](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization).
-  Instalar os KBs descritos na seção *Deploy the compatibility update and related KBs* (Implantar a atualização de compatibilidade e KBs relacionados) de [Get started with Upgrade Readiness](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness) (Introdução ao Upgrade Readiness).

    > [!NOTE]
    > Você pode baixar um script para automatizar muitas das tarefas de instalação do cliente. Consulte a seção *Run the Upgrade Readiness deployment script* (Executar o script de implantação do Upgrade Readiness) de [Get started with Upgrade Readiness](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness) (Introdução ao Upgrade Readiness) para obter informações sobre o script.

## <a name="create-a-connection-to-upgrade-readiness"></a>Criar uma conexão com o Upgrade Readiness

### <a name="prerequisites"></a>Pré-requisitos

- Para adicionar a conexão, seu ambiente do Configuration Manager deve configurar primeiro um [ponto de conexão de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point) em um [modo online](https://azure.microsoft.com/en-us/documentation/articles/resource-group-create-service-principal-portal/). Quando você adiciona a conexão ao seu ambiente, ele também instalará o Microsoft Monitoring Agent no computador que executa essa função de sistema de sites.
- Registre o Configuration Manager como uma ferramenta de gerenciamento "Aplicativo Web e/ou API Web" e obtenha a [ID do cliente desse registro](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
- Crie uma chave de cliente para a ferramenta de gerenciamento registrada no Azure Active Directory.
- No Portal de Gerenciamento do Azure, forneça o aplicativo Web registrado com permissão para acessar o OMS, conforme descrito em [Fornecer ao Configuration Manager as permissões para OMS](https://azure.microsoft.com/en-us/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms).

    > [!IMPORTANT]
    > Ao configurar a permissão para acessar o OMS, certifique-se de escolher a função **Colaborador** e atribua a ela permissões para o grupo de recursos do aplicativo registrado.

### <a name="create-the-connection"></a>Criar a conexão

1.  No console do Configuration Manager, escolha **Administração** > **Serviços de Nuvem** > **Upgrade Readiness Connector (Conector do Upgrade Readiness)** > **Create Connection to Upgrade Readiness (Criar Conexão com o Upgrade Readiness)** para iniciar o **Add Upgrade Readiness Connection wizard (Assistente para Adicionar Conexão com o Upgrade Readiness)**.
3.  Na tela **Azure Active Directory**, forneça o **Locatário**, a **ID do cliente** e a **Chave de Segredo do Cliente** e, em seguida, selecione **Avançar**.
4.  Na tela **Upgrade Readiness**, forneça as suas configurações de conexão preenchendo sua **Assinatura do Azure**, **Grupo de recursos do Azure** e **Espaço de trabalho do Operations Management Suite**.
5.  Verifique suas configurações de conexão na tela **Resumo** e, em seguida, selecione **Avançar**.

    > [!NOTE]
    > É necessário conectar o Upgrade Readiness ao site de nível superior na sua hierarquia. Se você conectar o Upgrade Readiness a um site primário autônomo e, em seguida, adicionar um site de administração central ao seu ambiente, será necessário excluir e recriar a conexão do OMS dentro da nova hierarquia.

### <a name="complete-upgrade-readiness-tasks"></a>Concluir tarefas do Upgrade Readiness  

Depois de criar a conexão no Configuration Manager, realize essas tarefas, conforme descrito em [Get started with Upgrade Readiness](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness) (Introdução ao Upgrade Readiness).  

1. Adicione o serviço do UpgradeReadiness ao espaço de trabalho do OMS.  
2. Gerar uma ID comercial.  
3. Assine o Upgrade Readiness.   

## <a name="use-the-upgrade-readiness-deployment-script"></a>Usar o script de implantação do Upgrade Readiness  

Você pode automatizar muitas das tarefas do Upgrade Readiness e solucionar problemas de compartilhamento com o **script de implantação do Upgrade Readiness** da Microsoft.  
O script de implantação do Upgrade Readiness faz o seguinte:  

- Define as chaves de ID comercial + CommercialDataOptIn + RequestAllAppraiserVersions.  
- Verifica se computadores de usuário podem enviar dados à Microsoft.  
- Verifica se o computador tem uma reinicialização pendente.   
- Verifica se a versão mais recente do pacote 10.0.x da KB está instalada (requer 10.0.14913 ou versões posteriores).  
- Se habilitado, ativará o modo detalhado para solução de problemas.  
- Inicia a coleta de dados de telemetria que a Microsoft precisa para avaliar a preparação para a atualização da sua organização.  
- Se habilitado, exibirá o progresso do script em uma janela cmd, fornecendo visibilidade de problemas (sucesso ou falha para cada etapa) e/ou gravará no arquivo de log.  

### <a name="to-run-the-upgrade-readiness-deployment-script"></a>Para executar o script de implantação do Upgrade Readiness:  

1. Baixe o [script de implantação do Upgrade Readiness](https://go.microsoft.com/fwlink/?LinkID=822966&clcid=0x409) e extraia UpgradeReadiness.zip. Os arquivos na pasta **Diagnóstico** só serão necessários se você planejar executar o script no modo de solução de problemas.  
2. Edite esses parâmetros em RunConfig.bat:  
- Local de armazenamento para informações de log. Exemplo: %SystemDrive%\URDiagnostics. Você pode armazenar informações de log em um compartilhamento de arquivo remoto ou em um diretório local. Se o script for impedido de criar o arquivo de log para o caminho especificado, ele criará os arquivos de log na unidade com o diretório do Windows.  
- Chave da ID comercial.  
- Por padrão, o script envia informações de log para o console e o arquivo de log. Para alterar o comportamento padrão, use uma das seguintes opções:  
    - logMode = log 0 somente para console  
    - logMode = log 1 para arquivo e console  
    - logMode = log 2 somente para arquivo  
    - Para solucionar o problema, defina **isVerboseLogging** como **$true** para gerar informações de log que podem ajudar a diagnosticar problemas. Por padrão, **isVerboseLogging** é definido como **$false**. Certifique-se de que a pasta Diagnóstico está instalada no mesmo diretório que o script para usar esse modo.  
    - Notifique os usuários se eles precisarem reinicializar seus computadores. Por padrão, isso é definido como desativado.  

3. Após terminar de editar os parâmetros em RunConfig.bat, execute o script como um administrador.  


## <a name="view-microsoft-upgrade-readiness-properties-in-configuration-manager"></a>Exibir propriedades do Microsoft Upgrade Readiness no Configuration Manager  

1.  No console do Configuration Manager, navegue até **Serviços de Nuvem** e, em seguida, escolha **Conector OMS** para abrir a página **Propriedades de Conexão do OMS**.  

2.  Nessa página, há duas guias:
  * A guia **Azure Active Directory Azure** mostra seu **Locatário**, sua **ID do cliente**, a **Expiração da Chave Secreta do Cliente** e permite que você **Verifique** se sua **Chave Secreta do Cliente** expirou.
  * A guia **Upgrade Readiness** mostra sua **Assinatura do Azure**, **Grupo de recursos do Azure** e **Espaço de trabalho do Operations Management Suite**.

## <a name="view-and-use-the-upgrade-information"></a>Exibir e usar as informações de atualização

Após a integração do Upgrade Readiness ao Configuration Manager, você poderá exibir a análise de preparação para atualização de seus clientes e, em seguida, executar a ação.

1. No console do Configuration Manager, escolha **Monitoramento** > **Visão Geral** > **Upgrade Readiness**.
2. Examine os dados, que inclui o estado de preparação para atualização e a porcentagem de dispositivos do Windows que estão comunicando telemetria.
3. Você pode filtrar o painel para exibir dados para dispositivos em coleções específicas.
4. Você poderá exibir os dispositivos em um estado de prontidão específico e criar uma coleção dinâmica deles para que você possa atualizar os dispositivos, se estiverem prontos, ou tomar medidas para colocá-los em um estado de prontidão.

