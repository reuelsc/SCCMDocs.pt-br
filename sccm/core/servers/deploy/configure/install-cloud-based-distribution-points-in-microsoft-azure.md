---
title: Instalar pontos de distribuição baseados em nuvem
titleSuffix: Configuration Manager
description: Saiba o que você precisa fazer para começar a usar os pontos de distribuição baseados em nuvem no Microsoft Azure.
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2c9c79c5e635a50fecf02c46e2a134df87c2d784
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32338407"
---
# <a name="install-cloud-based-distribution-points-in-microsoft-azure-for-system-center-configuration-manager"></a>Instalar pontos de distribuição baseados em nuvem no Microsoft Azure para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

É possível instalar pontos de distribuição baseados em nuvem do System Center Configuration Manager no Microsoft Azure. Se você não estiver familiarizado com pontos de distribuição baseados em nuvem, consulte [Usar um ponto de distribuição baseado em nuvem](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) antes de continuar.

 Antes de iniciar a instalação, certifique-se de ter os arquivos de certificado necessários:  

-   Um certificado de gerenciamento do Microsoft Azure exportado para um arquivo .cer e um arquivo .pfx.  

-   Um certificado de serviço de ponto de distribuição baseado em nuvem do Configuration Manager exportado para um arquivo .pfx.  

    > [!TIP]
    >   Para obter mais informações sobre esses certificados, consulte a seção de pontos de distribuição baseados em nuvem no tópico [Requisitos de certificado PKI para o System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md). Para ver um exemplo de implantação do certificado de serviço do ponto de distribuição baseado em nuvem, consulte a seção “Implantando o certificado de serviço em pontos de distribuição baseados em nuvem” em [Exemplo de implantação passo a passo dos certificados PKI para o System Center Configuration Manager: Autoridade de Certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  


 Depois de instalar o ponto de distribuição baseado em nuvem, o Azure gera automaticamente um GUID para o serviço e acrescenta isso ao sufixo DNS do **cloudapp.net**. Usando esse GUID, você deve configurar o DNS com um alias DNS (registro CNAME). Isso permite mapear o nome do serviço que você define no certificado de serviço de ponto de distribuição baseado em nuvem do Configuration Manager para o GUID gerado automaticamente.  

 Se você usa um servidor proxy da Web, talvez seja necessário definir as configurações de proxy para habilitar a comunicação com o serviço de nuvem que hospeda o ponto de distribuição.  

##  <a name="BKMK_ConfigWindowsAzureandInstallDP"></a> Configurar o Azure e instalar pontos de distribuição baseados em nuvem  
 Use os procedimentos a seguir para configurar o Azure para dar suporte a pontos de distribuição e depois instale o ponto de distribuição baseado em nuvem no Configuration Manager.  

### <a name="to-set-up-a-cloud-service-in-azure-for-a-distribution-point"></a>Para configurar um serviço de nuvem no Azure para um ponto de distribuição  

1.  Abra um navegador da Web no Portal do Azure, em https://manage.windowsazure.com e acesse sua conta.  

2.  Clique em **Serviços Hospedados, Contas de Armazenamento e CDN** e selecione **Certificados de Gerenciamento**.  

3.  Clique com o botão direito em sua assinatura e selecione **Adicionar Certificado**.  

4.  Para o **Arquivo de certificado**, especifique o arquivo .cer que contém o certificado de gerenciamento do Azure exportado para usar nesse serviço de nuvem e clique em **OK**.  

O certificado de gerenciamento é carregado no Azure e agora você pode instalar um ponto de distribuição baseado em nuvem.  

### <a name="to-install-a-cloud-based-distribution-point-for-configuration-manager"></a>Para instalar um ponto de distribuição baseado em nuvem para o Configuration Manager  

1.  Conclua as etapas no procedimento anterior para configurar um serviço de nuvem no Azure com um certificado de gerenciamento.  

2.  No espaço de trabalho **Administração** do console do Configuration Manager, expanda **Serviços de Nuvem** e selecione **Pontos de Distribuição de Nuvem**. Na guia **Início**, clique em **Criar Ponto de Distribuição de Nuvem**.  

3.  Na página **Geral** do Assistente para Criar Ponto de Distribuição na Nuvem, configure o seguinte:  

    -   Especifique a **ID da Assinatura** de sua conta do Azure.  

        > [!TIP]  
        >  Você pode localizar sua ID de assinatura do Azure no Portal do Azure.  

    -   Especifique o **Certificado de gerenciamento**. Clique em **Procurar** para especificar o arquivo .pfx que contém o certificado de gerenciamento do Azure exportado e digite a senha do certificado. Opcionalmente, você pode especificar um arquivo .publishsettings de versão 1 do Azure SDK 1.7.  

4.  Clique em **Avançar**. O Configuration Manager se conecta ao Azure para validar o certificado de gerenciamento.  

5.  Na página **Configurações**, especifique o seguinte e clique em **Próximo**:  

    -   Para a **Região**, selecione a região do Azure em que deseja criar o serviço de nuvem que hospeda esse ponto de distribuição.  

    -   Para o **Arquivo de certificado**, especifique o arquivo .pfx que contém o certificado exportado do serviço de ponto de distribuição baseado em nuvem do Configuration Manager. Digite a senha.  

        > [!NOTE]  
        >  A caixa **FQDN do Serviço** é automaticamente preenchida do nome da entidade do certificado. Na maioria dos casos, você não precisa editá-lo. A exceção é se você estiver usando um certificado curinga em um ambiente de teste. Por exemplo, neste caso você pode não especificar o nome do host, para que vários computadores que têm o mesmo sufixo DNS possam usar o certificado. Nesse cenário, a entidade do certificado contém um valor similar ao **CN=\*.contoso.com** e o Configuration Manager exibe uma mensagem que você deve especificar o FQDN correto. Clique em **OK** para fechar a mensagem e digite um nome específico antes do sufixo DNS para fornecer o FQDN completo. Por exemplo, você pode adicionar **clouddp1** para especificar o FQDN do serviço completo do **clouddp1.contoso.com**. O FQDN do Serviço deve ser exclusivo no domínio e não coincidir com qualquer dispositivo ingressado no domínio.  
        >   
        >  Os certificados com caracteres curinga têm suporte somente para ambientes de teste.  

6.  Na página **Alertas**, configure as cotas de armazenamento, cotas de transferência e com qual percentual dessas cotas que você deseja que o Configuration Manager gere alertas. Clique em **Avançar**.  

7.  Conclua o assistente.  

O assistente cria um novo serviço hospedado para o ponto de distribuição baseado em nuvem. Após fechar o assistente, você pode monitorar o progresso da instalação do ponto de distribuição baseado em nuvem no console do Configuration Manager. Você também pode monitorar o arquivo **CloudMgr.log** no servidor do site primário. Você pode monitorar o provisionamento do serviço de nuvem no Portal do Azure.  

> [!NOTE]  
>  Pode levar até 30 minutos para provisionar um novo ponto de distribuição no Azure. A seguinte mensagem é repetida no arquivo **CloudMgr.log** até que a conta de armazenamento esteja provisionada: **Aguardando a verificação da existência do contêiner. Verificará novamente em 10 segundos**. Em seguida, o serviço é criado e configurado.  

 Você pode identificar se a instalação do ponto de distribuição baseado em nuvem foi concluída, usando os seguintes métodos:  

-   No Portal do Azure, a **Implantação** do ponto de distribuição baseado em nuvem exibe um status de **Pronta**.  

-   No console do Configuration Manager, no espaço de trabalho **Administração**, **Configuração da Hierarquia**, no nó **Nuvem**, o ponto de distribuição baseado em nuvem exibe o status de **Pronto**.  

-   O Configuration Manager exibe uma mensagem de status com a ID **9409** para o componente SMS_CLOUD_SERVICES_MANAGER.  

##  <a name="BKMK_ConfigDNSforCloudDPs"></a> Configurar a resolução de nomes para pontos de distribuição baseados em nuvem  
 Antes de os clientes acessarem o ponto de distribuição baseado em nuvem, eles devem ser capazes de resolver o nome desse ponto de distribuição baseado em nuvem para um endereço IP gerenciado pelo Azure. Os clientes fazem isso em duas etapas:  

1.  Eles mapeiam o nome do serviço fornecido com o certificado de serviço do ponto de distribuição baseado em nuvem do Configuration Manager para o FQDN de serviço do Azure. Esse FQDN contém um GUID e o sufixo DNS de **cloudapp.net**. O GUID é gerado automaticamente após a instalação do ponto de distribuição baseado em nuvem. Você pode ver o FQDN completo no Portal do Azure consultando a **URL DO SITE** no painel do serviço de nuvem. Uma URL de site de exemplo é **http://d1594d4527614a09b934d470.cloudapp.net**.  

2.  Eles resolvem o FQDN de serviço do Azure para o endereço IP que o Azure aloca. Esse endereço IP também pode ser identificado no painel do serviço de nuvem no Portal do Azure, com o nome de **VIP (ENDEREÇO IP VIRTUAL PÚBLICO)**.  

Para mapear o nome do serviço fornecido com o certificado de serviço do ponto de distribuição baseado em nuvem do Configuration Manager (por exemplo, **clouddp1.contoso.com**) para seu FQDN de serviço do Azure (por exemplo, **d1594d4527614a09b934d470.cloudapp.net**), os servidores DNS na Internet devem ter um alias DNS (registro CNAME). Em seguida, os clientes podem resolver o FQDN de serviço do Azure para o endereço IP usando servidores DNS na Internet.  

##  <a name="BKMK_ConfigProxyforCloud"></a> Definir configurações de proxy para sites primários que gerenciam serviços de nuvem  
 Ao usar serviços de nuvem com o Configuration Manager, o site primário que gerencia o ponto de distribuição baseado em nuvem deve ter a capacidade de se conectar ao Portal do Azure. O site se conecta usando a conta **Sistema** do computador do site primário. Essa conexão é feita usando o navegador da Web padrão no computador do servidor do site primário.  

 No servidor do site primário que gerencia o ponto de distribuição baseado em nuvem, talvez seja necessário definir as configurações de proxy para habilitar o site primário a acessar a Internet e o Azure.  

 Use o procedimento a seguir para definir as configurações de proxy para o servidor do site primário no console do Configuration Manager.  

> [!TIP]  
>  Você também pode configurar o servidor proxy quando instalar novas funções do sistema de sites no servidor do site primário usando o **Assistente para Adicionar Funções do Sistema de Site**.  

#### <a name="to-set-up-proxy-settings-for-the-primary-site-server"></a>Para definir as configurações de proxy para o servidor do site primário  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Configuração de Site**e clique em **Funções de Servidores e Sistema de Site**. Selecione o servidor do site primário que gerencia o ponto de distribuição baseado em nuvem.  

3.  No painel de detalhes, clique com o botão direito em **Sistema de Site**e clique em **Propriedades**.  

4.  Em **Propriedades do Sistema de Sites**, selecione a guia **Proxy** e defina as configurações de proxy para esse servidor do site primário.  

5.  Clique em **OK** para salvar as configurações.  
