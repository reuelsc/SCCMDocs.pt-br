---
title: Configurar o gateway de gerenciamento de nuvem | Microsoft Docs
description: 
author: nbigman
manager: angrobe
ms.author: nbigman
ms.date: 12/14/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
translationtype: Human Translation
ms.sourcegitcommit: 2bcc5d9dde1f1a2d9c33575d6c463e281ac818e8
ms.openlocfilehash: 61b8cd8458718b9a54edb129739c619f947ac380

---

# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Configurar o gateway de gerenciamento de nuvem para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A partir da versão 1610, o processo de configuração do gateway de gerenciamento de nuvem no Configuration Manager inclui as seguintes etapas:

## <a name="step-1-create-a-custom-ssl-certificate"></a>Etapa 1: Criar um certificado SSL personalizado

Você pode criar um certificado SSL personalizado para o gateway de gerenciamento de nuvem da mesma maneira que faria para um ponto de distribuição baseado em nuvem. Siga as instruções para [Implantando o certificado de serviço em pontos de distribuição baseados em nuvem](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012), mas faça estas ações de forma diferente:

-   Ao configurar o novo modelo de certificado, conceda permissões de **Leitura** e **Registro** para o grupo de segurança que você configurou para os servidores do Configuration Manager.

-  Ao solicitar o certificado de servidor Web personalizado, forneça um FQDN para o nome comum do certificado que termine em **cloudapp.net** para usar o gateway de gerenciamento de nuvem na nuvem pública do Azure, ou **usgovcloudapp.net** para a nuvem do Azure Governamental.

## <a name="step-2-export-the-client-certificates-root"></a>Etapa 2: Exportar a raiz do certificado do cliente

A maneira mais fácil de exportar a raiz dos certificados de cliente usados na rede é abrir um certificado do cliente em um dos computadores ingressados no domínio que tenha um e copiá-lo.

> [!NOTE] 
>
> Os certificados de cliente são necessários em qualquer computador que você queira gerenciar com o gateway de gerenciamento de nuvem e no servidor do sistema de sites que hospeda o ponto do conector do gateway de gerenciamento de nuvem. Se você precisar adicionar um certificado do cliente a qualquer uma desses computadores, confira [Implantando o certificado do cliente para computadores Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).

1.  Na janela Executar, digite **mmc** e pressione Executar.

2.  No menu Arquivo, escolha **Adicionar/Remover Snap-in...**.

3.  Na caixa de diálogo Adicionar/Remover Snap-ins, escolha **Certificados** > **Adicionar &gt; **  >  **Conta de computador** > **Avançar** > **Computador Local** > **Concluir**. 

4.  Acesse **Certificados** &gt; **Pessoal** &gt; **Certificados**.

5.  Clique duas vezes no certificado para autenticação do cliente no computador, escolha a guia Caminho de Certificação e clique duas vezes na autoridade raiz (na parte superior do caminho).

6.  Na guia Detalhes, escolha **Copiar para Arquivo...**.

7.  Conclua o Assistente de Exportação de Certificado usando o formato de certificado padrão. Verifique a nota do nome e local do certificado raiz que você criar. Você precisará dele para configurar o gateway de gerenciamento de nuvem em uma [etapa posterior](#step-4-set-up-cloud-management-gateway).

## <a name="step-3-upload-the-management-certificate-to-azure"></a>Etapa 3: Carregar o certificado de gerenciamento no Azure

Um certificado de gerenciamento do Azure é necessário para o Configuration Manager acessar a API do Azure e configurar o gateway de gerenciamento de nuvem. Para obter mais informações e instruções sobre como carregar um certificado de gerenciamento, consulte os artigos a seguir na documentação do Azure:

- [Visão geral sobre certificados para os Serviços de Nuvem do Azure](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)

- [Carregar um Certificado de Gerenciamento de API do Gerenciamento do Azure](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/)

>[!IMPORTANT]
>Certifique-se de copiar a ID da assinatura associada ao certificado de gerenciamento. Você precisará dela para configurar o gateway de gerenciamento de nuvem no console do Configuration Manager na [próxima etapa](#step-4-set-up-cloud-management-gateway).

### <a name="subordinate-ca-certificates-and-azure"></a>Certificados de autoridade de certificação subordinada e o Azure

Se o seu certificado for emitido por uma autoridade de certificação subordinada (subCA), e sua infraestrutura PKI corporativa não estiver na Internet, use este procedimento para carregar o certificado no Azure. 

1. No portal do Azure, depois de configurar um gateway de gerenciamento de nuvem, localize o serviço do gateway de gerenciamento da nuvem e acesse a guia **Certificado**. Carregue seu(s) certificado(s) subCA nesse local. Se você tiver mais de um certificado de subCA, será necessário carregar todos eles. 
2. Após o carregamento do certificado, registre a impressão digital dele. 
3. Adicione a impressão digital ao banco de dados do site usando este script:
    
```

    DIM serviceCName
    DIM subCAThumbprints

    ' Verify arguments
    IF WScript.Arguments.Count <> 2 THEN
    WScript.StdOut.WriteLine "Usage: CScript UpdateSubCAThumbprints.vbs <ServiceCName> <SubCA cert thumbprints, separated by ;>"
    WScript.Quit 1
    END IF

    'Get arguments
    serviceCName = WScript.Arguments.Item(0)
    subCAThumbprints = WScript.Arguments.Item(1)

    'Find SMS Provider
    WScript.StdOut.WriteLine "Searching for SMS Provider for local site..."
    SET objSMSNamespace = GetObject("winmgmts:{impersonationLevel=impersonate}!\\.\root\sms")
    SET results = objSMSNamespace.ExecQuery("SELECT * From SMS_ProviderLocation WHERE ProviderForLocalSite = true")

    'Process the results
    FOR EACH var in results
    siteCode = var.SiteCode
    NEXT

    IF siteCode = "" THEN
    WScript.StdOut.WriteLine "Failed to locate SMS provider."
    WScript.Quit 1
    END IF

    WScript.StdOut.WriteLine "SiteCode = " & siteCode 

    ' Connect to the SMS namespace
    SET objWMIService = GetObject("winmgmts:{impersonationLevel=impersonate}!\\.\root\sms\site_" & siteCode)

    'Get instance of SMS_AzureService
    DIM query
    query = "SELECT * From SMS_AzureService WHERE ServiceType = 'CloudProxyService' AND ServiceCName = '" & serviceCName & "'"
    WScript.StdOut.WriteLine "Run WQL query: " &  query
    SET objInstances = objWMIService.ExecQuery(query)

    IF IsNull(objInstances) OR (objInstances.Count = 0) THEN
    WScript.StdOut.WriteLine "Failed to get Azure_Service instance."
    WScript.Quit 1
    END IF

    FOR EACH var IN objInstances
    SET azService = var
    NEXT

    WScript.StdOut.WriteLine "Update [SubCACertThumbprint] to " & subCAThumbprints

    'Update SubCA cert thumbprints
    azService.Properties_.item("SubCACertThumbprint") = subCAThumbprints

    'Save data back to provider
    azService.Put_

    WScript.StdOut.WriteLine "[SubCACertThumbprint] is updated successfully."
```


## <a name="step-4-set-up-cloud-management-gateway"></a>Etapa 4: Configurar o gateway de gerenciamento de nuvem

>[!NOTE]
>Na versão 1610, o gateway de gerenciamento de nuvem é um recurso de pré-lançamento. Para habilitá-lo, confira [Use pre-release features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease) (Usar recursos de pré-lançamento de atualizações).

1. No console do Configuration Manager, acesse **Administração** > **Serviços de Nuvem** > **Gateway de Gerenciamento de Nuvem**.
2. Escolha **Criar Gateway de Gerenciamento de Nuvem**.

3. No Assistente para Criar Gateway de Gerenciamento de Nuvem, insira a ID de sua assinatura do Azure (copiada do portal de gerenciamento do Azure), e procure o arquivo de certificado que você usou para carregar como um certificado de gerenciamento do Azure. Escolha **Avançar** e aguarde alguns minutos para o console se conectar ao Azure.

4. Preencha os detalhes adicionais no assistente:

    - Especifique o nome do serviço que será executado no Azure. O nome do serviço deve conter apenas caracteres alfanuméricos e ter de três a 24 caracteres.

    - Escolha a região do Azure na qual você deseja que o serviço seja executado.

    - Especifique o número de máquinas virtuais que você deseja usar para o serviço. O padrão é 1, mas você pode executar até 16 máquinas virtuais para o serviço.

    >[!NOTE]
    >Se você usar um proxy da Internet para o ponto de conexão do gateway de gerenciamento de nuvem, será necessário aumentar o número de portas no proxy de acordo com o número de máquinas virtuais usadas, começando na porta 10124.

    - Especifique a chave privada (arquivo .pfx) que você exportou do certificado SSL personalizado.

    - Especifique o certificado raiz exportado do certificado do cliente.

    -   Especifique o mesmo FQDN de nome de serviço que você usou ao criar o novo modelo de certificado. Especifique um dos seguintes sufixos para o nome de serviço FQDN com base na nuvem do Azure que você está usando:

    Nuvem do Azure | Prefixo FQDN
    --------------|-------------
    Nuvem pública (comercial) | .cloudapp.net    
    Nuvem do Governamental | .usgovcloudapp.net

  - Desmarque a caixa ao lado de **Verificar Revogação de Certificado do Cliente** (a menos que você esteja publicando publicamente suas informações de CRL).

  - Escolha **Avançar** quando terminar.

5. Se você quiser monitorar o tráfego do gateway de gerenciamento de nuvem com um limite de 14 dias, escolha a caixa de seleção para ativar o alerta de limite. Em seguida, especifique o limite e a porcentagem de elevação dos níveis de alerta diferentes. Escolha **Avançar** quando terminar.

6. Examine as configurações e escolha **Avançar**. O Configuration Manager começa a configurar o serviço. Após fechar o assistente, demorará de cinco a 15 minutos para provisionar completamente o serviço no Azure. Verifique a coluna **Status** para gateway de gerenciamento de nuvem recém-configurado a fim de determinar quando o serviço estiver pronto.

## <a name="step-5-configure-primary-site-for-client-certification-authentication"></a>Etapa 5: Configurar um site primário para a autenticação de certificação do cliente

1. No console do Configuration Manager, acesse **Administração** > **Configuração do Site** > **Sites**.

2. Selecione o site primário para os clientes que você deseja gerenciar por meio do gateway de gerenciamento de nuvem e escolha **Propriedades**.

3. Na guia Comunicações de Computador Cliente da folha de propriedades do site primário, marque **Usar o certificado do cliente PKI (autenticação de cliente) quando disponível**.

4. Desmarque **Os clientes verificam a CRL (lista de certificados revogados) para sistemas de sites**. Essa opção seria necessária apenas se você estivesse publicando publicamente sua CRL.


## <a name="step-6-add-the-cloud-management-gateway-connector-point"></a>Etapa 6: Adicionar o ponto de conector do gateway de gerenciamento de nuvem

O ponto de conector de gateway de gerenciamento de nuvem é uma nova função de sistema de site para se comunicar com o gateway de gerenciamento de nuvem. Para adicionar o ponto do conector do gateway de gerenciamento de nuvem, siga as instruções em [Adicionar funções do sistema de sites para o System Center Configuration Manager](/sccm/core/servers/deploy/configure/add-site-system-roles).

## <a name="step-7-configure-roles-for-cloud-management-gateway-traffic"></a>Etapa 7: Configurar funções para o tráfego do gateway de gerenciamento de nuvem

A etapa final na configuração do gateway de gerenciamento de nuvem é configurar as funções do sistema de sites para aceitar o tráfego do gateway de gerenciamento de nuvem. Para a Visualização Técnica 1606, apenas as funções de ponto de gerenciamento, ponto de distribuição e ponto de atualização de software têm suporte para o gateway de gerenciamento de nuvem. Você deve configurar cada função separadamente.

1. No console do Configuration Manager, acesse **Administração** > **Configuração do Site** > **Funções de Servidores e Sistema de Site**.

2. Escolha o servidor de sistema de sites para a função que você deseja configurar para o tráfego do gateway de gerenciamento de nuvem.

3. Escolha a função e escolha **Propriedades**.

4. Na folha Propriedades de função, em Conexões de Cliente, escolha **HTTPS**, marque a caixa ao lado de **Permitir o tráfego do gateway de gerenciamento de nuvem do Configuration Manager** e escolha **OK**. Repita essas etapas para as funções restantes.

## <a name="step-8-configure-clients-for-cloud-management-gateway"></a>Etapa 8: Configurar clientes para o gateway de gerenciamento de nuvem

Após a configuração e execução completa do gateway de gerenciamento de nuvem e das funções do sistema, os clientes obterão automaticamente o local do serviço de gateway de gerenciamento da nuvem na próxima solicitação de local. Os clientes devem estar na rede corporativa para receber o local do serviço de gateway de gerenciamento de nuvem. O ciclo de sondagem para solicitações de localização é a cada 24 horas. Se você não quiser aguardar a solicitação de local normalmente agendada, force a solicitação reiniciando o serviço de Host de Agente do SMS (ccmexec.exe) no computador.

Com o local do serviço de gateway de gerenciamento de nuvem configurado no cliente, ele poderá determinar automaticamente se está na intranet ou na Internet. Se o cliente puder contatar o controlador de domínio ou o ponto de gerenciamento local, ele o usará para se comunicar com o Configuration Manager, caso contrário, ele considerará que está na Internet e usará o local do serviço de gateway de gerenciamento de nuvem para se comunicar.

>[!NOTE]
> Você pode forçar o cliente a usar sempre o gateway de gerenciamento de nuvem, independentemente se ele está na intranet ou na Internet. Para fazer isso, defina a seguinte chave do Registro no computador cliente:\
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`

Para verificar se os clientes podem contatar o Configuration Manager, execute o seguinte comando do PowerShell no computador cliente:

`gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate`

Esse comando exibe os pontos de gerenciamento que o cliente pode contatar, incluindo o serviço de gateway de gerenciamento de nuvem.

## <a name="next-steps"></a>Próximas etapas

[Monitorar clientes para o gateway de gerenciamento de nuvem](monitor-clients-cloud-management-gateway.md)



<!--HONumber=Dec16_HO3-->


