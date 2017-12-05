---
title: Recursos no Technical Preview 1606
titleSuffix: Configuration Manager
description: "Saiba mais sobre os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1606."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 134a2f60-811e-4dc9-a8f5-1ce0018c5c12
caps.latest.revision: "31"
author: erikje
ms.author: erikje
manager: angrobe
ms.openlocfilehash: 59a57e20a21aac7c650c25e13df0f3180c2110ea
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="capabilities-in-technical-preview-1606-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1606 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1606. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview.      Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de um technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos em um technical preview.    

**Problemas conhecidos nesse Technical Preview:**  
*  Quando você atualizar do Technical Preview 1604 para o 1605 e, em seguida, para a versão 1606, a atualização poderá falhar e um erro semelhante ao seguinte será registrado no **cmupdate.log**:

       ERROR: Failed to execute SQL Server command:  ~ ~-- Create site boundary group ~IF  dbo.fnIsCasOrStandalonePrimary() = 1 ~BEGIN ~   PRINT N'Create site boundary group during upgrade' ~   EXEC dbo.spBuildDefaultBoundaryGroups @UserName = N'SYSTEM' ~END          

    Se isso ocorrer, no nó **Atualizações e Manutenção**, clique em **Verificar se há atualizações** e, em seguida, **Tente novamente** realizar a instalação da atualização.
    ***

**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  

## <a name="dmp_category"></a> Categorizar automaticamente dispositivos em coleções
Você pode criar categorias de dispositivos, que podem ser usadas para colocar automaticamente os dispositivos em coleções de dispositivos ao usar o Configuration Manager com o Microsoft Intune. Os usuários devem, então, escolher uma categoria de dispositivo ao registrar um dispositivo no Intune. Além disso, você pode alterar a categoria de um dispositivo do console do Configuration Manager.

**Importante:** essa funcionalidade funciona com a versão de **junho de 2016** do Microsoft Intune. Verifique se você atualizou para essa versão antes de experimentar esses procedimentos.

### <a name="try-it-out"></a>Experimente!

### <a name="create-a-set-of-device-categories"></a>Criar um conjunto de categorias de dispositivo
1.  No espaço de trabalho **Ativos e Conformidade** do console do Configuration Manager, expanda **Visão Geral** e clique em **Coleções de Dispositivos**.
2.  Na guia **Início**, no grupo **Categorias**, clique em **Gerenciar Categorias de Dispositivo**.
3.  Na caixa de diálogo **Gerenciar Categorias de Dispositivo**, você pode criar, editar ou remover categorias. Tente criar uma nova categoria.

### <a name="associate-a-collection-with-a-device-category"></a>Associar uma coleção a uma categoria de dispositivos
Quando você associa uma coleção a uma categoria de dispositivos, todos os dispositivos na categoria especificada serão adicionados à coleção.
1.  Na caixa de diálogo **Propriedades** de uma coleção de dispositivos, clique em **Adicionar Regra** > **Regra de Categoria de Dispositivo**.
2.  Na caixa de diálogo **Create Device Category Membership Rule (Criar Regra de Associação de Categoria de Dispositivos)**, selecione a categoria que será aplicada a todos os dispositivos na coleção.
3.  Feche a caixa de diálogo **Create Device Category Membership Rule (Criar Regra de Associação de Categoria de Dispositivos)** e a caixa de diálogo de propriedades da coleção.

### <a name="change-the-category-of-a-device"></a>Alterar a categoria de um dispositivo
1.  No espaço de trabalho **Ativos e Conformidade** do console do Configuration Manager, expanda **Visão Geral** e clique em **Dispositivos**.
2.  Selecione um dispositivo na lista **Dispositivos** e, na guia **Início**, no grupo **Dispositivo**, clique em **Alterar Categoria**.
3.  Na caixa de diálogo **Editar Categoria de Dispositivo**, selecione a categoria a ser aplicada a esse dispositivo e clique em **OK**.

## <a name="dmp_grace"></a> Período de cortesia para imposição de implantações de atualizações de software e aplicativos obrigatórios

Em alguns casos, talvez você queira conceder aos usuários mais tempo instalar as atualizações de software ou as implantações de aplicativo obrigatórias além dos prazos configurados. Isso normalmente pode ser necessário quando um computador ficou desligado por um período estendido e precisa reinstalar uma grande quantidade de implantações de atualização ou aplicativo.
Por exemplo, se um usuário final acabou de voltar de férias, eles terá que aguardar um longo período enquanto as implantações de aplicativo atrasadas são instaladas.
Para ajudar a resolver esse problema, agora você pode definir um período de carência para a imposição implantando configurações de cliente do Configuration Manager para uma coleção.

### <a name="try-it-out"></a>Experimente!

Para configurar o período de carência, execute as seguintes ações:

1.  Na página **Agente de Computador** das configurações do cliente, configure a nova propriedade **Período de carência para a imposição após a data limite da implantação (horas):** com um valor entre **1** e **120** horas.
2.  Em uma nova implantação de aplicativo obrigatória ou nas propriedades de uma implantação existente, na página **Agendamento**, marque a caixa de seleção **Delay enforcement of this deployment according to user preferences (Atrasar a imposição dessa implantação de acordo com as preferências do usuário)** até o período de carência definido nas configurações do cliente.
Todas as implantações que têm essa caixa de seleção marcada e que são destinadas a dispositivos nos quais você também implantou as configurações do cliente usarão o período de carência de imposição.

Se você configurar um período de carência para a imposição e marcar a caixa de seleção, quando o prazo da instalação do aplicativo for atingido, ele será instalado na primeira janela fora do horário comercial que o usuário configurou até esse período de carência. No entanto, o usuário ainda poderá abrir o Centro de Software e instalar o aplicativo a qualquer momento que desejar. Depois que o período de carência expirar, a imposição retorna ao comportamento normal para implantações atrasadas.
Opções semelhantes foram adicionadas ao assistente de implantação de atualizações de software, ao assistente de regras de implantação automática e páginas de propriedades.

##  <a name="dmp_devg"></a> Uso do Configuration Manager como um instalador gerenciado com o Device Guard

O Device Guard é um recurso do Windows 10 que usa recursos de hardware e software para controlar rigorosamente o que pode ser executado no dispositivo.

Você pode ler uma visão geral detalhada do que o Device Guard faz e como ele funciona [nesse artigo do Technet](https://technet.microsoft.com/itpro/windows/whats-new/device-guard-overview).

Nessa versão, o Configuration Manager pode interoperar com o Device Guard e o [Windows AppLocker](https://technet.microsoft.com/library/dd723678(v=ws.10).aspx) para que os arquivos DLL e executáveis implantados com o Configuration Manager sejam automaticamente confiáveis uma vez que eles vêm de um Instalador Gerenciado, o que significa que eles poderão ser executados no dispositivo de destino e outro software não poderá ser executado a menos que tenha autorização explícita para ser executado por outras regras do AppLocker.  

No momento, essa funcionalidade não é configurável do console do Configuration Manager. Para configurar a política é necessário que você configure uma chave do Registro em cada cliente e configure serviços do Windows no cliente.
Após fazer isso, configure o arquivo de política do AppLocker. Depois de configurar o arquivo de política, você pode implantá-lo em qualquer dispositivo de cliente compatível.


Como todas as políticas do AppLocker, as políticas com regras do Instalador Gerenciado podem ser executadas em dois modos:

- Modo de auditoria – os aplicativos não têm a execução impedida, mas quaisquer aplicativos que seriam bloqueados são relatados em um arquivo de log (isso terá suporte em uma versão posterior do Configuration Manager).
- Imposição habilitada – os aplicativos têm a execução bloqueada.

É possível encontrar mais informações sobre como usar o Device Guard com o Configuration Manager no [Enterprise Mobility and Security blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/06/20/configmgr-as-a-managed-installer-with-win10) (Blog de Enterprise Mobility and Security).

Leitura adicional:

- [Introdução ao Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/introduction-to-device-guard-virtualization-based-security-and-code-integrity-policies)
- [Conformidade e certificação do Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-certification-and-compliance)
- [Guia de implantação do Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)

 ##  <a name="dmp_onprem"></a> Múltiplos pontos de gerenciamento para Gerenciamento de Dispositivo Móvel Local  
 Com o Technical Preview 1606, o MDM (Gerenciamento de Dispositivo Móvel) local dá suporte a um nova funcionalidade na Atualização de Aniversário do Windows 10 que configura automaticamente um dispositivo registrado para ter mais de um ponto de gerenciamento de dispositivos disponível para uso. Essa funcionalidade permite que o dispositivo realize o fallback para outro ponto de gerenciamento de dispositivos quando o que ele usa normalmente não estiver disponível. Essa funcionalidade funciona apenas para computadores com a Atualização de Aniversário do Windows 10 instalada.  

### <a name="try-it-out"></a>Experimente!  

1.  Instale mais de um ponto de gerenciamento de dispositivos na sua hierarquia.  

2.  Registre um dispositivo com a Atualização de Aniversário do Windows 10 para o gerenciamento de dispositivo móvel local.  

Para obter informações sobre como preparar seu site e registrar dispositivos para o gerenciamento de dispositivo móvel local, confira [Gerenciar dispositivos móveis com a infraestrutura local no System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

## <a name="cloud_proxy"></a>Serviço de Proxy de Nuvem para o gerenciamento de clientes na Internet

O Serviço de Proxy de Nuvem fornece uma maneira simples de gerenciar clientes do Configuration Manager na Internet. O serviço, que é implantado no Microsoft Azure e requer uma assinatura do Azure, conecta-se à sua infraestrutura do Configuration Manager local usando uma nova função chamada de ponto do conector de proxy de nuvem. Após ser completamente implantado e configurado, os clientes poderão acessar funções do sistema de sites do Configuration Manager locais independentemente de se eles estão conectados à rede privada interna ou na Internet.

Use o console do Configuration Manager para implantar o serviço no Azure, adicione a função de ponto do conector de proxy de nuvem e configure as funções do sistema de sites para permitir o tráfego de proxy de nuvem. No momento, o Serviço de Proxy de Nuvem dá suporte apenas às funções de ponto de gerenciamento, ponto de distribuição e ponto de atualização de software.

Os certificados de cliente e os certificados SSL são necessários para autenticar computadores e criptografar comunicações entre diferentes camadas do serviço. Normalmente, os computadores cliente recebem um certificado do cliente por meio da aplicação de política de grupo. Para criptografar o tráfego entre clientes e o servidor do sistema de sites hospedando as funções, você precisa criar um certificado SSL personalizado por meio da AC. Além desses dois tipos de certificados, você também precisa configurar um certificado de gerenciamento no Azure que permita que o Configuration Manager implante o Serviço de Proxy de Rede.  

### <a name="requirements-for-cloud-proxy-service-in-tp-1606"></a>Requisitos para o Serviço de Proxy de Nuvem na TP 1606
- Computadores cliente e o servidor do sistema de sites que está executando o ponto do conector de proxy de nuvem.
- Certificados SSL personalizados da AC interna – usado para criptografar a comunicação de computadores cliente e autenticar a identidade do Serviço de Proxy de Cliente.
- Assinatura do Azure para serviços de nuvem.
- Certificado de gerenciamento do Azure – usado para autenticar o Configuration Manager com o Azure.

### <a name="limitations-of-cloud-proxy-service-in-tp-1606"></a>Limitações do Serviço de Proxy de Nuvem na TP 1606

- Dá suporte apenas às funções de ponto de gerenciamento, ponto de distribuição e ponto de atualização de software.
- Não há suporte para políticas de usuário.
- Não pode ser usado com o [gerenciamento de dispositivo móvel local](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) no Configuration Manager.
- Tem suporte apenas na plataforma de nuvem pública do Azure.


### <a name="try-it-out"></a>Experimente!

O processo de implantação do Serviço de Proxy de Nuvem inclui as seguintes etapas:

1. Criar e emitir um certificado SSL personalizado para o Serviço de Proxy de Nuvem.
1. Exportar a raiz do certificado do cliente.
2. Carregar o certificado de gerenciamento no Azure.
3. Configure o Serviço de Proxy de Nuvem no console do Configuration Manager.
4. Configurar o site primário para usar a autenticação de certificado do cliente.
5. Adicionar o ponto do conector de proxy de nuvem ao seu site.
6. Configurar as funções do sistema de sites para aceitar o tráfego de proxy de nuvem.

As seções a seguir fornecem mais informações para concluir essas etapas.

#### <a name="create-a-custom-ssl-certificate"></a>Criar um certificado SSL personalizado

Você pode criar um certificado SSL personalizado para o Serviço de Proxy de Nuvem da mesma maneira que faria para um ponto de distribuição baseado em nuvem. Siga as instruções para [Implantando o certificado de serviço em pontos de distribuição baseados em nuvem](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012), mas faça estas ações de forma diferente:

* Ao configurar o novo modelo de certificado, conceda permissões de **Leitura** e **Registro** para o grupo de segurança que você configurou para os servidores do Configuration Manager.

#### <a name="export-the-client-certificates-root"></a>Exportar a raiz do certificado do cliente

A maneira mais fácil de exportar a raiz dos certificados de cliente usados na rede é abrir um certificado do cliente em um dos computadores ingressados no domínio que tenha um e copiá-lo.

>[!NOTE]
>Os certificados de cliente são necessários em qualquer computador que você desejar gerenciar com o Serviço de Proxy de Nuvem e no servidor do sistema de sites que hospeda o ponto do conector de proxy de nuvem. Se você precisar adicionar um certificado do cliente a qualquer uma desses computadores, confira [Implantando o certificado do cliente para computadores Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012).

1. Na janela Executar, digite **mmc** e pressione Executar.
2. No menu Arquivo no console de gerenciamento, clique em **Adicionar/Remover Snap-ins...**.
3. Na caixa de diálogo Adicionar ou Remover Snap-ins, clique em **Certificados**, clique em **Adicionar >**, **Conta de computador**, **Avançar**, **Computador local** e em **Concluir**. Clique em **OK** para fechar a caixa de diálogo.
4. Vá para **Certificados > Pessoal > Certificados**.
5. Clique duas vezes no certificado para autenticação do cliente no computador, clique na guia Caminho de Certificação e clique duas vezes na autoridade raiz (na parte superior do caminho).
6.  Clique na guia Detalhes e clique em **Copiar para Arquivo...**.
7. Conclua o Assistente de Exportação de Certificado usando o formato de certificado padrão. Verifique a nota do nome e local do certificado raiz que você criar. Você precisará dele para configurar o Serviço de Proxy de Nuvem em uma etapa posterior.

#### <a name="upload-the-management-certificate-to-azure"></a>Carregar o certificado de gerenciamento no Azure

Um certificado de gerenciamento do Azure é necessário para o Configuration Manager acessar a API do Azure e configurar o Serviço de Proxy de Nuvem. Para obter mais informações e instruções sobre como carregar um certificado de gerenciamento, consulte os artigos a seguir na documentação do Azure:
- [Visão geral sobre certificados para os Serviços de Nuvem do Azure](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)
- [Carregar um Certificado de Gerenciamento de API do Gerenciamento do Azure](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/).

Certifique-se de copiar a ID da assinatura associada ao certificado de gerenciamento. Você precisará dela para configurar o Serviço de Proxy de Nuvem no console do Configuration Manager.

#### <a name="set-up-cloud-proxy-service"></a>Configurar o Serviço de Proxy de Nuvem

1. No console do Configuration Manager, vá para **Administração > Serviços de Nuvem > Serviço de Proxy de Nuvem**.
2. Clique em **Criar Serviço de Proxy de Nuvem**.
3. No Assistente para Criar Serviço de Proxy de Nuvem, insira a ID da sua assinatura do Azure (copiado do portal de gerenciamento do Azure), clique em Procurar e selecione o arquivo de certificado que você usou para carregar como um certificado de gerenciamento do Azure. Clique em **Avançar**. Aguarde alguns minutos para o console para se conectar ao Azure.
4. Preencha os detalhes adicionais no assistente:
    - Especifique a chave privada (arquivo .pfx) que você exportou do certificado SSL personalizado.
    - Especifique o certificado raiz exportado do certificado do cliente.
    - Especifique o mesmo FQDN de nome de serviço que você usou ao criar o novo modelo de certificado.
    - Desmarque a caixa ao lado de **Verificar Revogação de Certificado do Cliente** (a menos que você esteja publicando publicamente suas informações de CRL).
    - Clique em **Avançar** quando terminar.
5. Examine as configurações e clique em **Avançar**. O Configuration Manager começa a configurar o serviço. Quando o assistente é concluído, você pode clicar em **Fechar**, no entanto, levará de 5 a 15 minutos para provisionar o serviço completamente no Azure. Verifique a coluna **Status** para o Serviço de Proxy de Nuvem recém-configurado para determinar quando o serviço está pronto.

#### <a name="configure-primary-site-for-client-certification-authentication"></a>Configurar um site primário para a autenticação de certificação de cliente

1. No console do Configuration Manager, vá para **Administração > Configuração de Site > Sites**.
2. Selecione o site primário para os clientes que você deseja gerenciar através do Serviço de Proxy de Nuvem e clique em **Propriedades**.
3. Na guia Client Computer Communications (Comunicações de Computador Cliente) da folha de propriedades do site primário, selecione a caixa ao lado de **Use PKI client certificate (client authentication) when available (Usar o certificado do cliente PKI (autenticação de cliente) quando disponível)**.
4. Certifique-se de desmarcar a caixa ao lado de **Os clientes verificam a CRL (lista de certificados revogados) para sistemas de sites**. Essa opção seria necessária apenas se você estivesse publicando publicamente sua CRL.
5. Clique em **OK**.

#### <a name="add-the-cloud-proxy-connector-point"></a>Adicionar o ponto do conector de proxy de nuvem

O ponto do conector de proxy de nuvem é uma nova função de sistema de sites para se comunicar com o Serviço de Proxy de Nuvem. Para adicionar o ponto do conector de proxy de nuvem, siga as instruções em [Add site system roles for System Center Configuration Manager](../../core/servers/deploy/configure/add-site-system-roles.md) (Adicionar funções do sistema de sites para o System Center Configuration Manager).

#### <a name="configure-roles-for-cloud-proxy-traffic"></a>Configurar funções para tráfego de proxy na nuvem

A etapa final na configuração do Serviço de Proxy de Nuvem é configurar as funções do sistema de sites para aceitar o tráfego de proxy de nuvem. Para o Tech Preview 1606, apenas as funções de ponto de gerenciamento, ponto de distribuição e ponto de atualização de software têm suporte para o Serviço de Proxy de Nuvem. Você deve configurar cada função separadamente.

1. No console do Configuration Manager, vá para **Administração > Configuração de Site > Funções de Servidores e Sistema de Site**.
2. Clique no servidor de sistema de sites para a função que você deseja configurar para o tráfego de proxy de nuvem.
3. Clique na função e clique em **Propriedades**.
4. Na folha Propriedades de função, em Conexões de Cliente, escolha **HTTPS**, marque a caixa ao lado de **Permitir tráfego do Proxy de Nuvem do Configuration Manager** e clique em **OK**. Repita essas etapas para as funções restantes.

#### <a name="check-status-on-a-client-on-the-internet"></a>Verificar o status em um cliente na Internet

Depois que o serviço e as funções forem completamente configurados, os clientes internos obterão o local do Serviço de Proxy de Nuvem na próxima solicitação de local. Os clientes com informações de local atualizadas podem se comunicar com o Configuration Manager na Internet. O ciclo de sondagem para solicitações de localização é a cada 24 horas. Se você não quiser aguardar a solicitação de local normalmente agendada, force a solicitação reiniciando o serviço de Host de Agente do SMS (ccmexec.exe) no computador.

Depois que os clientes tiverem as novas informações de local do Serviço de Proxy de Nuvem, tente verificar o status dos clientes que não estão mais na rede privada interna, mas têm acesso à Internet. Você também pode monitorar o tráfego no Serviço de Proxy de Nuvem acessando **Administração > Serviços de Nuvem > Serviço de Proxy de Nuvem**, selecionando serviço no painel de lista e exibindo as informações de tráfego no painel de detalhes.   

## <a name="manage_o365"></a>Gerenciamento do agente cliente do Office 365 no Configuration Manager  

A partir do Technical Preview 1606, você pode usar uma configuração de agente cliente do Configuration Manager em vez da política de grupo para habilitar os clientes do Office 365 para receber atualizações do Configuration Manager. Depois de definir essa configuração e implantar as atualizações do Office 365, o agente cliente do Configuration Manager se comunica com o agente cliente do Office 365 para baixar atualizações do Office 365 de um ponto de distribuição e instalá-las. O Configuration Manager também faz o inventário da configuração do agente cliente.

Para mais informações, confira [Manage Office 365 ProPlus updates](https://technet.microsoft.com/library/mt741983.aspx) (Gerenciar atualizações do Office 365 ProPlus).

### <a name="set-the-configuration-manager-client-setting-to-manage-the-office-365-client-agent"></a>Defina uma configuração de cliente do Configuration Manager para gerenciar o agente cliente do Office 365
1.  No console do Configuration Manager, escolha **Administração** > **Visão Geral** > **Configurações do Cliente**.
2. Abra as configurações do dispositivo apropriado para habilitar o agente cliente. Para obter mais informações sobre configurações do cliente padrão e personalizadas, consulte [Como definir as configurações do cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).
3. Clique em **Atualizações de Software** e selecione **Sim** para a configuração **Habilitar o gerenciamento do Agente Cliente do Office 365**.  


## <a name="osdpreservedriveletter"></a>A variável de sequência de tarefas OSDPreserveDriveLetter foi preterida
A variável OSDPreserveDriveLetter determina se a sequência de tarefas usa ou não a letra da unidade capturada no arquivo WIM da imagem do sistema operacional ao aplicar essa imagem a um computador de destino.
- Essa variável de sequência de tarefas foi preterida no Technical Preview 1606.

Durante uma implantação de sistema operacional, por padrão, a Instalação do Windows agora determina a melhor letra da unidade a ser usada (geralmente, C:). Se desejar especificar o uso de uma unidade diferente, mude o local na etapa da sequência de tarefas Aplicar Sistema Operacional. Vá para a configuração **Selecione o local onde deseja aplicar este sistema operacional**, selecione **Letra da unidade lógica específica** e escolha a unidade que deseja usar. Deve haver uma unidade atribuída com a letra escolhida no computador de destino. 

## <a name="updatesandservicing"></a>Alterações no nó Atualizações e Manutenção
Com o Technical Preview 1606, foram introduzidas várias ações que se aplicam às Atualizações e Manutenção no console do Configuration Manager:
- **Alteração de nome de nó:**

    No espaço de trabalho **Monitoramento**, o nó **Status de Manutenção do Site** foi renomeado para **Status de Serviço e Atualizações**.
- **Mais status da instalação:**

    Quando você exibe o status da instalação da atualização para um site, agora o console mostra detalhes separados para as seguintes ações:
    - **Baixar** (isso se aplica somente ao site de nível superior em que a função do sistema de sites do ponto de conexão de serviço está instalado)
    - **Replicação**
    - **Verificação de pré-requisitos**
    - **Instalação**

  Além disso, agora há informações mais detalhadas para cada etapa, incluindo qual arquivo de log você pode exibir para obter mais informações.  
-   **Nova opção para repetir as falhas de pré-requisito:**

    Nos espaços de trabalho **Administração** e **Monitoramento**, o nó **Atualizações e Manutenção** inclui um novo botão na Faixa de opções chamado **	Ignorar avisos de pré-requisito**.

    Ao instalar atualizações sem usar a opção de Ignorar avisos de pré-requisito (de dentro do Assistente de Atualizações), e a instalação da atualização for interrompida com um estado de **Prereq warning (Aviso de pré-requisito)**, você poderá selecionar **Ignorar avisos de pré-requisito** na faixa de opções para disparar uma continuação automática da instalação da atualização que ignora os avisos de pré-requisito.  



- **Exibição mais clara das atualizações:**

    Ao ver o nó **Atualizações e Manutenção**, agora você pode visualizar apenas as atualizações instaladas mais recentemente e quaisquer atualizações que estejam disponíveis para instalação. Para exibir atualizações instaladas anteriormente, clique no novo botão **Histórico**, que aparece na faixa de opções.  

-   **Opção renomeada para pré-produção:**

    No nó Atualizações e Manutenção, o botão chamado **Client options (Opções do cliente)** agora foi renomeado para **Promover o Cliente de Pré-produção**.
