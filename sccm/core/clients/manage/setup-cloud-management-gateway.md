---
title: Configurar o Gateway de Gerenciamento de Nuvem
titleSuffix: Configuration Manager
description: 
author: arob98
ms.author: angrobe
manager: angrobe
ms.date: 09/26/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.openlocfilehash: 7463cd7199098b21843fd5b99ed284a12ff91e00
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Configurar o gateway de gerenciamento de nuvem para o Configuration Manager

*Aplica-se ao: System Center Configuration Manager (Branch Atual)* O processo de configuração do gateway de gerenciamento de nuvem no Configuration Manager inclui as seguintes etapas:

## <a name="step-1-configure-required-certificates"></a>Etapa 1: Configurar os certificados necessários

> [!TIP]  
> Antes de solicitar um certificado, confirme se o nome de domínio desejado do Azure (por exemplo, GraniteFalls.CloudApp.Net) é exclusivo. Para fazer isso, efetue logon no [Portal do Microsoft Azure](https://manage.windowsazure.com), clique em **Novo**, selecione **Serviço de Nuvem** e **Criação Personalizada**. No campo **URL**, digite o nome de domínio desejado (não clique na marca de seleção para criar o serviço). O portal refletirá se o nome de domínio está disponível, ou se já está em uso por outro serviço.

### <a name="option-1-preferred---use-the-server-authentication-certificate-from-a-public-and-globally-trusted-certificate-provider-like-verisign"></a>Opção 1 (preferencial) - Use o certificado de autenticação do servidor de um provedor de certificados público e globalmente confiável (como a VeriSign)

Ao usar esse método, os clientes confiarão automaticamente no certificado e você não precisará criar um certificado SSL personalizado por conta própria.

1. Crie um CNAME (registro de nome canônico) no DNS (serviço de nome de domínio) público de sua organização para criar um alias para o serviço de gateway de gerenciamento de nuvem com um nome amigável que será usado no certificado público.
Por exemplo, a Contoso nomeia seu serviço de gateway de gerenciamento de nuvem como **GraniteFalls**, que no Azure será **GraniteFalls.CloudApp.Net**. No namespace contoso.com do DNS público da Contoso, o administrador de DNS cria um novo registro CNAME para **GraniteFalls.Contoso.com** para o nome do host real **GraniteFalls.CloudApp.net**.
2. Em seguida, solicite um certificado de autenticação de servidor de um provedor público usando o CN (nome comum) do alias CNAME.
Por exemplo, a Contoso usa **GraniteFalls.Contoso.com** para o CN do certificado.
3. Crie o serviço de gateway de gerenciamento de nuvem no console do Configuration Manager usando esse certificado.
    - Na página **Configurações** do Assistente para Criar Gateway de Gerenciamento de Nuvem: quando você adicionar o certificado do servidor para esse serviço de nuvem (do **Arquivo de certificado**), o assistente extrairá o nome do host do CN do certificado como o nome do serviço e, em seguida, acrescentará isso a **cloudapp.net** (ou a **usgovcloudapp.net** da nuvem do Governo dos EUA do Azure) como o FQDN do Serviço para criar o serviço no Azure.
Por exemplo, ao criar o gateway de gerenciamento de nuvem na Contoso, o nome do host **GraniteFalls** é extraído do CN do certificado, para que o serviço real no Azure seja criado como **GraniteFalls.CloudApp.net**.

### <a name="option-2---create-a-custom-ssl-certificate-for-cloud-management-gateway-in-the-same-way-as-for-a-cloud-based-distribution-point"></a>Opção 2 - Crie um certificado SSL personalizado para o gateway de gerenciamento de nuvem da mesma maneira que faria para um ponto de distribuição baseado em nuvem

Você pode criar um certificado SSL personalizado para o gateway de gerenciamento de nuvem da mesma maneira que faria para um ponto de distribuição baseado em nuvem. Siga as instruções para [Implantando o certificado de serviço em pontos de distribuição baseados em nuvem](/sccm/core/plan-design/network/example-deployment-of-pki-certificates), mas faça estas ações de forma diferente:

- Ao solicitar o certificado de servidor Web personalizado, forneça um FQDN para o nome comum do certificado que termine em **cloudapp.net** para usar o gateway de gerenciamento de nuvem na nuvem pública do Azure, ou **usgovcloudapp.net** para a nuvem do Azure Governamental.


## <a name="step-2-export-the-client-certificates-root"></a>Etapa 2: Exportar a raiz do certificado do cliente

A maneira mais fácil de exportar a raiz dos certificados de cliente usados na rede é abrir um certificado do cliente em um dos computadores ingressados no domínio que tenha uma e copiá-la.

> [!NOTE]
>
> Os certificados de cliente são necessários em qualquer computador que você queira gerenciar com o gateway de gerenciamento de nuvem e no servidor do sistema de sites que hospeda o ponto do conector do gateway de gerenciamento de nuvem. Se você precisar adicionar um certificado do cliente a qualquer uma desses computadores, confira [Implantando o certificado do cliente para computadores Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).

1.  Na janela Executar, digite **mmc** e pressione Executar.

2.  No menu Arquivo, escolha **Adicionar/Remover Snap-in...**.

3.  Na caixa de diálogo Adicionar/Remover Snap-ins, escolha **Certificados** > **Adicionar &gt;**   >  **Conta de computador** > **Avançar** > **Computador Local** > **Concluir**.

4.  Acesse **Certificados** &gt; **Pessoal** &gt; **Certificados**.

5.  Clique duas vezes no certificado para autenticação do cliente no computador, escolha a guia Caminho de Certificação e clique duas vezes na autoridade raiz (na parte superior do caminho).

6.  Na guia Detalhes, escolha **Copiar para Arquivo...**.

7.  Conclua o Assistente de Exportação de Certificado usando o formato de certificado padrão. Verifique a nota do nome e local do certificado raiz que você criar. Você precisará disso ao configurar o gateway de gerenciamento de nuvem em uma [etapa posterior](#step-4-set-up-cloud-management-gateway).

>[!NOTE]
>Se o certificado do cliente tiver sido emitido por uma autoridade de certificação subordinada, será necessário repetir esta etapa para cada certificado na cadeia.

## <a name="step-3-upload-the-management-certificate-to-azure"></a>Etapa 3: Carregar o certificado de gerenciamento no Azure

Um certificado de gerenciamento do Azure é necessário para o Configuration Manager acessar a API do Azure e configurar o gateway de gerenciamento de nuvem. Para obter mais informações e instruções sobre como carregar um certificado de gerenciamento, consulte os artigos a seguir na documentação do Azure:

- [Visão geral sobre certificados para os Serviços de Nuvem do Azure](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)

- [Carregar um Certificado de Gerenciamento de API do Gerenciamento do Azure](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/)

>[!IMPORTANT]
>Certifique-se de copiar a ID da assinatura associada ao certificado de gerenciamento. Você precisará dela para configurar o gateway de gerenciamento de nuvem no console do Configuration Manager na [próxima etapa](#step-4-set-up-cloud-management-gateway).



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

    - Especifique o certificado raiz (e qualquer certificado subordinado) exportado do certificado do cliente. O assistente aceita até dois certificados raiz e quatro certificados subordinados.

    -   Especifique o mesmo FQDN de nome de serviço que você usou ao criar o novo modelo de certificado. Especifique um dos seguintes sufixos para o nome de serviço FQDN com base na nuvem do Azure que você está usando:

    Nuvem do Azure | Prefixo FQDN
    --------------|-------------
    Nuvem pública (comercial) | .cloudapp.net    
    Nuvem do Governamental | .usgovcloudapp.net

  - Desmarque a caixa ao lado de **Verificar Revogação de Certificado do Cliente** (a menos que você esteja publicando publicamente suas informações de CRL).

  - Escolha **Avançar** quando terminar.

5. Se você quiser monitorar o tráfego do gateway de gerenciamento de nuvem com um limite de 14 dias, escolha a caixa de seleção para ativar o alerta de limite. Em seguida, especifique o limite e a porcentagem de elevação dos níveis de alerta diferentes. Escolha **Avançar** quando terminar.

6. Examine as configurações e escolha **Avançar**. O Configuration Manager começa a configurar o serviço. Após fechar o assistente, demorará de cinco a 15 minutos para provisionar completamente o serviço no Azure. Verifique a coluna **Status** do novo gateway de gerenciamento de nuvem para determinar quando o serviço está pronto.

## <a name="step-5-configure-primary-site-for-client-certification-authentication"></a>Etapa 5: Configurar um site primário para a autenticação de certificação do cliente

1. No console do Configuration Manager, acesse **Administração** > **Configuração do Site** > **Sites**.

2. Selecione o site primário para os clientes que você deseja gerenciar por meio do gateway de gerenciamento de nuvem e escolha **Propriedades**.

3. Na guia Comunicações de Computador Cliente da folha de propriedades do site primário, marque **Usar o certificado do cliente PKI (autenticação de cliente) quando disponível**.

4. Desmarque **Os clientes verificam a CRL (lista de certificados revogados) para sistemas de sites**. Essa opção seria necessária apenas se você estivesse publicando publicamente sua CRL.


## <a name="step-6-add-the-cloud-management-gateway-connector-point"></a>Etapa 6: Adicionar o ponto de conector do gateway de gerenciamento de nuvem

O ponto de conector de gateway de gerenciamento de nuvem é uma nova função de sistema de site para se comunicar com o gateway de gerenciamento de nuvem. Para adicionar o ponto do conector do gateway de gerenciamento de nuvem, siga as instruções em [Adicionar funções do sistema de sites para o System Center Configuration Manager](/sccm/core/servers/deploy/configure/add-site-system-roles).

## <a name="step-7-configure-roles-for-cloud-management-gateway-traffic"></a>Etapa 7: Configurar funções para o tráfego do gateway de gerenciamento de nuvem

A etapa final na configuração do gateway de gerenciamento de nuvem é configurar as funções do sistema de sites para aceitar o tráfego do gateway de gerenciamento de nuvem. Somente as funções de ponto de gerenciamento e o ponto de atualização de software têm suporte para o gateway de gerenciamento de nuvem. Cada função é configurada separadamente.

1. No console do Configuration Manager, acesse **Administração** > **Configuração do Site** > **Funções de Servidores e Sistema de Site**.

2. Escolha o servidor de sistema de sites para a função que você deseja configurar para o tráfego do gateway de gerenciamento de nuvem.

3. Escolha a função e escolha **Propriedades**.

4. Na folha Propriedades de função, em Conexões de Cliente, marque a caixa de seleção ao lado de **Permitir o tráfego do gateway de gerenciamento de nuvem do Configuration Manager** e escolha **OK**. Repita essas etapas para as funções restantes. Habilitar a opção **HTTPS** também é recomendada como uma prática recomendada de segurança, mas não é obrigatória.

## <a name="step-8-configure-clients-for-cloud-management-gateway"></a>Etapa 8: Configurar clientes para o gateway de gerenciamento de nuvem

Após a configuração e execução completa do gateway de gerenciamento de nuvem e das funções do sistema, os clientes obterão automaticamente o local do serviço de gateway de gerenciamento da nuvem na próxima solicitação de local. Os clientes devem estar na rede corporativa para receber o local do serviço de gateway de gerenciamento de nuvem. O ciclo de sondagem para solicitações de localização é a cada 24 horas. Se você não quiser aguardar a solicitação de local normalmente agendada, force a solicitação reiniciando o serviço de Host de Agente do SMS (ccmexec.exe) no computador.

Com o local do serviço de gateway de gerenciamento de nuvem configurado no cliente, ele poderá determinar automaticamente se está na intranet ou na Internet. Se o cliente puder contatar o controlador de domínio ou o ponto de gerenciamento local, ele o usará para comunicar-se com o Configuration Manager. Caso contrário, ele considerará que ele está na Internet e usará o local do serviço de gateway de gerenciamento de nuvem para se comunicar.

>[!NOTE]
> Você pode forçar o cliente a usar sempre o gateway de gerenciamento de nuvem, independentemente se ele está na intranet ou na Internet. Para fazer isso, defina a seguinte chave do Registro no computador cliente:\
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`

Para verificar se os clientes podem contatar o Configuration Manager, execute o seguinte comando do PowerShell no computador cliente:

`gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate`

Esse comando exibe os pontos de gerenciamento que o cliente pode contatar, incluindo o serviço de gateway de gerenciamento de nuvem.

## <a name="next-steps"></a>Próximas etapas

[Monitorar clientes para o gateway de gerenciamento de nuvem](monitor-clients-cloud-management-gateway.md)
