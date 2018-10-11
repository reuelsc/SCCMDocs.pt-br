---
title: Instalar pontos de distribuição na nuvem
titleSuffix: Configuration Manager
description: Use estas etapas para configurar um ponto de distribuição na nuvem no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ef8bfead4bb73871f990a455aef87971413701ba
ms.sourcegitcommit: 2badee2b63ae63687795250e298f463474063100
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/14/2018
ms.locfileid: "45601102"
---
# <a name="install-a-cloud-distribution-point-for-configuration-manager"></a>Instalar um ponto de distribuição na nuvem do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo detalha as etapas para instalar um ponto de distribuição na nuvem do Configuration Manager no Microsoft Azure. Ele inclui as seguintes seções:
- [Antes de começar](#bkmk_before) 
- [Configurar](#bkmk_setup)
- [Configurar o DNS](#bkmk_dns)
- [Configurar o proxy do servidor do site](#bkmk_proxy)
- [Distribuir conteúdo e configurar clientes](#bkmk_client)
- [Gerenciar e monitorar](#bkmk_monitor)
- [Modificar](#bkmk_modify)
- [Solução de problemas avançada](#bkmk_tshoot) 



## <a name="bkmk_before"></a> Antes de começar

Comece lendo o artigo [Usar um ponto de distribuição na nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point). Esse artigo ajuda você a planejar e projetar seus pontos de distribuição na nuvem. 

Use a seguinte lista de verificação para verificar se você tem as informações e os pré-requisitos necessários para criar um ponto de distribuição na nuvem:  

- O servidor do site consegue se conectar ao Azure. Se a rede usa um proxy, [configure a função do sistema de sites](#bkmk_proxy).  

- O **ambiente do Azure** a ser usado. Por exemplo, a Nuvem Pública do Azure ou a Nuvem do Azure US Government.  

- Começando na versão 1806 e *recomendado*, se você planeja usar a **implantação do Azure Resource Manager**, é necessário atender aos seguintes requisitos:<!--1322209-->  

    - Integração com o [Azure Active Directory](/sccm/core/servers/deploy/configure/azure-services-wizard) para **Gerenciamento de Nuvem**. A descoberta de usuário do Azure AD não é necessária.  

    - A **ID da assinatura** do Azure.  

    - O **grupo de recursos** do Azure.  

    - Um **conta do administrador de assinatura** precisa entrar durante a execução do assistente.  

- Se você planeja usar a **implantação de serviço clássico** do Azure, é necessário atender ao seguintes requisitos:  

    - A **ID da assinatura** do Azure.  

    - Um **certificado de gerenciamento** do Azure, exportado como arquivo CER e também PFX. Um administrador de assinatura do Azure precisa adicionar o certificado de gerenciamento .CER à assinatura no [portal do Azure](https://portal.azure.com).  

- Um **certificado de autenticação de servidor**, exportado como um arquivo .PFX.  

- Um **nome do serviço** global exclusivo para o ponto de distribuição na nuvem.  

    > [!TIP]  
    > Antes de solicitar o certificado de autenticação de servidor que usa esse nome de serviço, confirme se o nome de domínio do Azure desejado é exclusivo. Por exemplo, *WallaceFalls.CloudApp.Net*. Faça logon no [portal do Microsoft Azure](https://portal.azure.com). Clique em **Criar um recurso**, selecione a categoria **Computação** e, em seguida, clique em **Serviço de Nuvem**. No campo **Nome DNS**, digite o prefixo desejado, por exemplo, *WallaceFalls*. A interface reflete se o nome de domínio está disponível ou se já está em uso por outro serviço. Não crie o serviço no portal. Use esse processo apenas para verificar a disponibilidade do nome.  
 
- A **região** do Azure para essa implantação.  



##  <a name="bkmk_setup"></a> Configurar   

Execute este procedimento no site para hospedar esse ponto de distribuição na nuvem de acordo com seu [design](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_topology).  

1.  No console do Configuration Manager, acesse o espaço de trabalho **Administração**, expanda **Serviços de Nuvem** e selecione **Pontos de Distribuição na Nuvem**. Na faixa de opções, clique em **Criar Ponto de Distribuição em Nuvem**.  

2.  Na página **Geral** do Assistente para Criar Ponto de Distribuição em Nuvem, configure:  

    a. Especifique primeiro o **ambiente do Azure**.  

    b. Escolha o método de implantação do Azure e, em seguida, defina as configurações associadas.  

       - **Implantação do Azure Resource Manager** (começando na versão 1806, e *recomendado*): clique em **Entrar** para autenticar com uma conta do administrador da assinatura do Azure. O assistente popula automaticamente os campos restantes com as informações armazenadas durante o pré-requisito de integração do Azure AD. Se você tem várias assinaturas, selecione a **ID da Assinatura** da assinatura que deseja usar.  

       - **Implantação de serviço clássico** (e no Configuration Manager versão 1802 e anteriores): insira sua **ID da assinatura** do Azure. Em seguida, clique em **Procurar** e selecione o arquivo .PFX do certificado de gerenciamento do Azure.  

3.  Clique em **Avançar**. Aguarde enquanto o site testa a conexão com o Azure.  

4.  Na página **Geral**, especifique as seguintes configurações e clique em **Avançar**:  

    - **Região**: selecione a região do Azure em que você deseja criar o ponto de distribuição na nuvem.  

    - **Grupo de Recursos** (somente no método de implantação do Azure Resource Manager)  

        - **Usar existente**: selecione um grupo de recursos existente na lista suspensa.  

        - **Criar**: insira o nome do novo grupo de recursos a ser criado em sua assinatura do Azure.  

    - **Site primário**: selecione o site primário para distribuir conteúdo a esse ponto de distribuição.

    - **Arquivo de certificado**: clique em **Procurar** e selecione o arquivo PFX do certificado de autenticação de servidor desse ponto de distribuição na nuvem. O nome comum desse certificado popula os campos obrigatórios **FQDN do serviço** e **Nome do serviço**.  

        > [!NOTE]  
        > O certificado de autenticação de servidor do ponto de distribuição na nuvem permite o uso de caracteres curinga. Se você usar um certificado curinga, substitua o asterisco (*) no campo **FQDN do serviço** pelo nome do host desejado para o serviço.  

5. Na página **Alertas**, configure as cotas de armazenamento, cotas de transferência e com qual percentual dessas cotas que você deseja que o Configuration Manager gere alertas. Clique em **Avançar**.  

6. Conclua o assistente.  


### <a name="monitor-installation"></a>Monitorar a instalação  

O site começa a criar um serviço hospedado para o ponto de distribuição na nuvem. Depois de fechar o assistente, monitore o progresso da instalação do ponto de distribuição na nuvem no console do Configuration Manager. Monitore também o arquivo **CloudMgr.log** no servidor do site primário. Se necessário, monitore o provisionamento do serviço de nuvem no portal do Azure.  

> [!NOTE]  
>  Pode levar até 30 minutos para provisionar um novo ponto de distribuição no Azure. O arquivo **CloudMgr.log** repete a seguinte mensagem de erro até que a conta de armazenamento esteja provisionada:  
> `Waiting for check if container exists. Will check again in 10 seconds`  
> Depois que a conta de armazenamento é provisionada, o serviço é criado e configurado.  


### <a name="verify-installation"></a>Verificar a instalação

Verifique se a instalação de ponto de distribuição na nuvem foi concluída, usando os seguintes métodos:  

- No console do Configuration Manager, acesse o espaço de trabalho **Administração**. Expanda **Serviços de Nuvem** e selecione o nó **Pontos de Distribuição na Nuvem**. Localize o novo ponto de distribuição na nuvem na lista. A coluna Status deve ser **Pronto**.  

- No console do Configuration Manager, acesse o espaço de trabalho **Monitoramento**. Expanda **Status do Sistema** e selecione o nó **Status do Componente**. Exiba todas as mensagens do componente **SMS_CLOUD_SERVICES_MANAGER** e procure a ID da mensagem de status **9409**.  

- Se necessário, acesse o portal do Azure. A **Implantação** do ponto de distribuição na nuvem exibe o status **Pronto**.  



##  <a name="bkmk_dns"></a> Configurar o DNS  

Para que os clientes possam usar o ponto de distribuição na nuvem, eles precisam ser capazes de resolver o nome do ponto de distribuição na nuvem para um endereço IP gerenciado pelo Azure. O ponto de gerenciamento fornece a eles o **FQDN do serviço** do ponto de distribuição na nuvem. O ponto de distribuição na nuvem existe no Azure como o **Nome do serviço**. Veja esses valores na guia **Configurações** das propriedades do ponto de distribuição na nuvem. 

> [!Note]  
> O nó **Pontos de Distribuição na Nuvem** no console inclui uma coluna chamada **Nome do Serviço**, mas que, na verdade, mostra o valor **FQDN do Serviço**. Para ver os dois valores, abra as **Propriedades** do ponto de distribuição na nuvem e mude para a guia **Configurações**.  

<!-- Remove based on feedback from RoYork
If you issue the server authentication certificate from your PKI, you may directly specify the Azure **Service name**. For example, `WallaceFalls.cloudapp.net`. When you specify this certificate in the Create Cloud Distribution Point Wizard, both the **Service FQDN** and **Service name** properties are the same. In this scenario, you don't need to configure DNS. The name that clients receive from the management point is the same name as the service in Azure.  
-->

O nome comum do certificado de autenticação de servidor deve incluir o seu nome de domínio. Esse nome é necessário quando você compra um certificado de um provedor público. Ele é recomendado quando você emite esse certificado de sua PKI. Por exemplo, `WallaceFalls.contoso.com`. Quando você especifica esse certificado no Assistente para Criar Ponto de Distribuição em Nuvem, o nome comum popula a propriedade **FQDN do Serviço** (`WallaceFalls.contoso.com`). O **Nome do serviço** usa o mesmo nome do host (`WallaceFalls`) e acrescenta-o ao nome de domínio do Azure, `cloudapp.net`. Nesse cenário, os clientes precisam resolver o **FQDN do serviço** (`WallaceFalls.contoso.com`) do seu domínio para o **Nome do serviço** (`WallaceFalls.cloudapp.net`) do Azure. Crie um alias do CNAME para mapear esses nomes.


### <a name="create-cname-alias"></a>Criar um alias do CNAME

Crie um CNAME (registro de nome canônico) no DNS público, para a Internet, da sua organização. Esse registro cria um alias para a propriedade **FQDN do Serviço** do ponto de distribuição na nuvem que os clientes recebem, como o **Nome do Serviço** do Azure. Por exemplo, crie um registro CNAME de `WallaceFalls.contoso.com` para `WallaceFalls.cloudapp.net`.  


### <a name="client-name-resolution-process"></a>Processo de resolução de nomes de cliente

O processo a seguir mostra como um cliente resolve o nome do ponto de distribuição na nuvem:  

1. O cliente recebe o **FQDN do Serviço** do ponto de distribuição na nuvem na lista de fontes de conteúdo. Por exemplo, `WallaceFalls.contoso.com`.  

2. Ele consulta o DNS, que resolve o FQDN do serviço usando o alias do CNAME para o **Nome do serviço** do Azure. Por exemplo, `WallaceFalls.cloudapp.net`.  

3. Ele consulta o DNS novamente, que resolve o nome do serviço do Azure para o endereço IP público do Azure.   

4. O cliente usa esse endereço IP para iniciar a comunicação com o ponto de distribuição na nuvem.   

5. O ponto de distribuição na nuvem apresenta o certificado de autenticação de servidor ao cliente. O cliente usa a cadeia confiável do certificado para validação.  



## <a name="bkmk_proxy"></a> Configurar o proxy do servidor do site  

O servidor do site primário que gerencia o ponto de distribuição na nuvem precisa se comunicar com o Azure. Se a organização usa um servidor proxy para controlar o acesso à Internet, configure o servidor do site primário para usar esse proxy.   

Para obter mais informações, confira [Suporte ao servidor proxy](/sccm/core/plan-design/network/proxy-server-support).  



## <a name="bkmk_client"></a> Distribuir conteúdo e configurar clientes

Distribua o conteúdo ao ponto de distribuição na nuvem da mesma forma que você faria com um ponto de distribuição local. O ponto de gerenciamento não inclui o ponto de distribuição na nuvem na lista de locais de conteúdo, a menos que ele tenha o conteúdo que os clientes solicitam. Para obter mais informações, confira [Distribuir e gerenciar o conteúdo](/sccm/core/servers/deploy/configure/deploy-and-manage-content). 

Gerencie um ponto de distribuição na nuvem da mesma forma que você faria com um ponto de distribuição local. Essas ações incluem atribuí-lo a um grupo de pontos de distribuição e gerenciar pacotes de conteúdo. Para obter mais informações, consulte [Instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points).

As configurações padrão do cliente o habilitam automaticamente para usar pontos de distribuição na nuvem. Controle o acesso a todos os pontos de distribuição na nuvem em sua hierarquia com a seguinte configuração do cliente:  

   - No grupo **Configurações de Nuvem**, modifique a configuração **Permitir acesso aos pontos de distribuição na nuvem**.  

       - Por padrão, essa configuração é definida como **Sim**.  

       - Modifique e implante essa configuração para usuários e dispositivos.  



## <a name="bkmk_monitor"></a> Gerenciar e monitorar  

Monitore o conteúdo que você distribui para um ponto de distribuição na nuvem da mesma forma que você faria com um ponto de distribuição local. Para obter mais informações, confira [Monitorar conteúdo](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed). 

### <a name="bkmk_alerts"></a> Alertas  

O Configuration Manager verifica periodicamente o serviço do Azure. Se o serviço não está ativo ou se há problemas de certificado ou de assinatura, o Configuration Manager emite um alerta. 

Configure limites para a quantidade de dados que você deseja armazenar no ponto de distribuição na nuvem e para a quantidade de dados que os clientes baixam do ponto de distribuição. Use alertas para esses limites para ajudá-lo a decidir quando parar ou excluir o serviço de nuvem, ajustar o conteúdo que você armazena no ponto de distribuição na nuvem ou modificar quais clientes podem usar o serviço. 

- **Limite de alerta de armazenamento**: o limite de alerta de armazenamento define um limite superior em GB para a quantidade de dados ou o conteúdo que você deseja armazenar no ponto de distribuição na nuvem. Por padrão, esse limite é 2.000 GB. O Configuration Manager gera alertas de aviso e críticos quando o espaço livre restante atinge o nível especificado. Por padrão, esses alertas ocorrem em 50% e 90% do limite.  

- **Limite de alerta de transferência mensal**: esse limite ajuda a monitorar a quantidade de conteúdo que você transfere do ponto de distribuição aos clientes em um período de 30 dias. Por padrão, esse limite é 10.000 GB. O site gera alertas de aviso e críticos quando as transferências atingem os valores que você definiu. Por padrão, esses alertas ocorrem em 50% e 90% do limite.  

    > [!IMPORTANT]  
    >  O Configuration Manager monitora a transferência de dados, mas não interrompe a transferência de dados que está além do limite de alerta de transferência especificado.  

Especifique limites para cada ponto de distribuição na nuvem durante a instalação ou use a guia **Alertas** das propriedades do ponto de distribuição na nuvem.  

> [!NOTE]  
>  Os alertas de um ponto de distribuição na nuvem dependem das estatísticas de uso do Azure, que podem levar 24 horas para ficar disponíveis. Para obter mais informações sobre a Análise de Armazenamento do Azure, confira [Análise de Armazenamento](https://docs.microsoft.com/rest/api/storageservices/storage-analytics).  

Em um ciclo de hora em hora, o site primário que monitora o ponto de distribuição na nuvem baixa dados de transação do Azure. Ele armazena esses dados de transação no arquivo `CloudDP-<ServiceName>.log` no servidor do site. O Configuration Manager avalia essas informações em relação às cotas de armazenamento e transferência de cada ponto de distribuição na nuvem. Quando a transferência de dados atingir ou exceder o volume especificado para avisos ou alertas críticos, o Configuration Manager gerará o alerta apropriado.  

> [!WARNING]  
>  Como o site baixa informações sobre transferências de dados do Azure a cada hora, o uso pode exceder um limite de aviso ou crítico antes que o Configuration Manager possa acessar os dados e emitir um alerta.  



## <a name="bkmk_modify"></a> Modificar

Exiba informações de alto nível sobre o ponto de distribuição no nó **Pontos de Distribuição na Nuvem** em **Serviços de Nuvem** no espaço de trabalho **Administração** do console do Configuration Manager. Selecione um ponto de distribuição e clique em **Propriedades** para ver mais detalhes.  

Quando você edita as propriedades de um ponto de distribuição de nuvem, as seguintes guias incluem configurações a serem editadas:  

#### <a name="settings"></a>Configurações  

- **Descrição**  

- **Arquivo de certificado**: antes que o certificado de autenticação de servidor expire, emita um novo certificado com o mesmo nome comum. Em seguida, adicione o novo certificado aqui para que o serviço comece a usá-lo. Se o certificado expirar, os clientes não poderão confiar no serviço e usá-lo.  

#### <a name="alerts"></a>Alertas
Ajuste os limites de dados para alertas de armazenamento e de transferência mensal.  

#### <a name="content"></a>Conteúdo
Gerencie o conteúdo da mesma maneira que você faria com um ponto de distribuição local.  


### <a name="redeploy-the-service"></a>Reimplantar o serviço

Alterações mais significativas, como as seguintes configurações, exigem a reimplantação do serviço:
- Método de implantação clássico no Azure Resource Manager
- Assinaturas
- Nome do serviço
- Privado para a PKI pública
- Região do Azure

Começando na versão 1806, para usar o método de implantação do Azure Resource Manager quando houver um ponto de distribuição na nuvem existente no método de implantação clássico, será necessário implantar um novo ponto de distribuição na nuvem. Há duas opções:

- Caso deseje reutilizar o mesmo nome de serviço:  

    1. Primeiro, exclua o ponto de distribuição na nuvem clássico. Se não houver outro ponto de distribuição na nuvem, os clientes não poderão obter o conteúdo.  

    2. Crie um ponto de distribuição na nuvem usando uma implantação do Gerenciador de Recursos. Reutilize o mesmo certificado de autenticação de servidor.  

    3. Distribua o conteúdo do pacote de software necessário para o novo ponto de distribuição na nuvem.  

- Caso deseje usar um novo nome de serviço:  

    1. Crie um ponto de distribuição na nuvem usando uma implantação do Gerenciador de Recursos. Use um novo certificado de autenticação de servidor.  

    2. Distribua o conteúdo do pacote de software necessário para o novo ponto de distribuição na nuvem.  

    3. Exclua o ponto de distribuição na nuvem clássico.

> [!Tip]  
> Para determinar o modelo de implantação atual de um ponto de distribuição de nuvem:<!--SCCMDocs issue #611-->  
> 1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e selecione o nó **Pontos de Distribuição na Nuvem**.  
> 2. Adicione o atributo **Modelo de Implantação** como uma coluna à exibição de lista. Para uma implantação do Resource Manager, esse atributo é **Azure Resource Manager**.  


### <a name="stop-or-start-the-cloud-service-on-demand"></a>Interromper ou iniciar o serviço de nuvem sob demanda

Pare um ponto de distribuição na nuvem a qualquer momento no console do Configuration Manager. Essa ação impede imediatamente que os clientes baixem mais conteúdo do serviço. Reinicie o serviço de nuvem no console do Configuration Manager para restaurar o acesso dos clientes. Por exemplo, é possível parar um serviço de nuvem quando ele atingir um limite de dados.  

Quando você para um ponto de distribuição na nuvem, o serviço de nuvem não exclui o conteúdo da conta de armazenamento. Ele também não impede que o servidor do site transfira mais conteúdo ao ponto de distribuição na nuvem. O ponto de gerenciamento ainda retorna o ponto de distribuição na nuvem aos clientes como uma fonte de conteúdo válida. 

Use o procedimento a seguir para parar um ponto de distribuição na nuvem:  

1. No console do Configuration Manager, acesse o espaço de trabalho **Administração**. Expanda **Serviços de Nuvem** e selecione o nó **Pontos de Distribuição na Nuvem**.  

2. Selecione o ponto de distribuição na nuvem. Para parar o serviço de nuvem que é executado no Azure, clique em **Parar serviço** na faixa de opções.  

3. Clique em **Iniciar serviço** para reiniciar o ponto de distribuição na nuvem.  


### <a name="delete-a-cloud-distribution-point"></a>Excluir um ponto de distribuição na nuvem

Para desinstalar um ponto de distribuição na nuvem, selecione o ponto de distribuição no console do Configuration Manager e, em seguida, selecione **Excluir**.  

Quando um ponto de distribuição na nuvem é excluído de uma hierarquia, o Configuration Manager remove o conteúdo do serviço de nuvem no Azure. 

A remoção manual de componentes no Azure faz com que o sistema fique divergente. Esse estado deixa informações órfãs e comportamentos inesperados podem ocorrer.



## <a name="bkmk_tshoot"></a> Solução de problemas avançada

Se você precisar coletar logs de diagnóstico das VMs do Azure para ajudar a solucionar problemas com seu ponto de distribuição na nuvem, use o seguinte exemplo do PowerShell para habilitar a extensão de diagnóstico de serviço para a assinatura:<!--514275-->  

``` PowerShell
# Change these variables for your Azure environment. The current values are provided as examples. You can find the values for these from the Azure portal.
$storage_name="4780E38368358502‬‭23C071" # The name of the storage account that goes with the CloudDP
$key="3jSyvMssuTyAyj5jWHKtf2bV5JF^aDN%z%2g*RImGK8R4vcu3PE07!P7CKTbZhT1Sxd3l^t69R8Cpsdl1xhlhZtl" # The storage access key from the Storage Account view
$service_name="4780E38368358502‬‭23C071" # The name of the cloud service for the CloudDP, which for a Cloud DP is the same as the storage name
$azureSubscriptionName="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription name the tenant is using 
$subscriptionId="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription ID the tenant is using 

# This variable is the path to the config file on the local computer.
$public_config="F:\PowerShellDiagFile\diagnostics.wadcfgx"

# These variables are for the Azure management certificate. Install it in the Current User certificate store on the system running this script. 
$thumbprint="dac9024f54d8f6df94935fb1732638ca6ad77c13" # The thumbprint of the Azure management certificate 
$mycert = Get-Item cert:\\CurrentUser\My\$thumbprint

Set-AzureSubscription -SubscriptionName $azureSubscriptionName -SubscriptionId $subscriptionId -Certificate $mycert

Select-AzureSubscription $azureSubscriptionName

Set-AzureServiceDiagnosticsExtension -StorageAccountName $storage_name -StorageAccountKey $key -DiagnosticsConfigurationPath $public_config –ServiceName $service_name -Slot 'Production' -Verbose
```


A seguir há um exemplo do arquivo **diagnostics.wadcfgx** referenciado na variável **public_config** no script do PowerShell acima. Para obter mais informações, confira [Esquema de configuração de extensão de Diagnóstico do Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics-schema).  

``` XML
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
      <Directories scheduledTransferPeriod="PT1M">
        <IISLogs containerName ="wad-iis-logfiles" />
        <FailedRequestLogs containerName ="wad-failedrequestlogs" />
      </Directories>
      <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Application!*" />
      </WindowsEventLog>
      <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Information" />
      <CrashDumps dumpType="Full">
        <CrashDumpConfiguration processName="WaAppAgent.exe" />
        <CrashDumpConfiguration processName="WaIISHost.exe" />
        <CrashDumpConfiguration processName="WindowsAzureGuestAgent.exe" />
        <CrashDumpConfiguration processName="WaWorkerHost.exe" />
        <CrashDumpConfiguration processName="DiagnosticsAgent.exe" />
        <CrashDumpConfiguration processName="w3wp.exe" />
      </CrashDumps>
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      </PerformanceCounters>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```

