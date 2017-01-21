---
title: "Instalar pontos de distribuição baseados em nuvem | Microsoft Docs"
description: "Saiba o que você precisa fazer para começar a usar os pontos de distribuição baseados em nuvem no Microsoft Azure."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
caps.latest.revision: 7
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: aba573b2822568236c006e7af19b421639faa8bc

---
# <a name="install-cloud-based-distribution-points-in-microsoft-azure-for-system-center-configuration-manager"></a>Instalar pontos de distribuição baseados em nuvem no Microsoft Azure para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

É possível instalar pontos de distribuição baseados em nuvem do System Center Configuration Manager no Microsoft Azure. Se você não está familiarizado com pontos de distribuição baseados em nuvem, consulte [Usar um ponto de distribuição baseado em nuvem](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) antes de continuar.

 Antes de começar a instalação, certifique-se de ter os arquivos de certificado necessários:  

-   Um certificado de gerenciamento do Microsoft Azure exportado para um arquivo .cer e um arquivo .pfx.  

-   Um certificado de serviço de ponto de distribuição baseado em nuvem do Configuration Manager exportado para um arquivo .pfx.  

    > [!TIP]
    >   Para obter mais informações sobre esses certificados, consulte a seção de pontos de distribuição baseados em nuvem no tópico [Requisitos de certificado PKI para o System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md). Para ver um exemplo de implantação do certificado de serviço do ponto de distribuição baseado em nuvem, consulte a seção *Implantando o certificado de serviço em pontos de distribuição baseados em nuvem* em [Exemplo de implantação passo a passo dos certificados PKI para o System Center Configuration Manager: Autoridade de Certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  


 Depois de instalar o ponto de distribuição baseado em nuvem, o Microsoft Azure gera automaticamente um GUID para o serviço e acrescenta isso ao sufixo DNS do **cloudapp.net**. Usando esse GUID, é necessário configurar o DNS com um alias do DNS (registro CNAME) para mapear o nome do serviço que você define no certificado de serviço de ponto de distribuição baseado em nuvem do Configuration Manager para o GUID gerado automaticamente.  

 Se você usa um servidor proxy da Web, talvez seja necessário definir as configurações de proxy para habilitar a comunicação com o serviço de nuvem que hospeda o ponto de distribuição.  

##  <a name="a-namebkmkconfigwindowsazureandinstalldpa-configure-microsoft-azure-and-install-cloud-based-distribution-points"></a><a name="BKMK_ConfigWindowsAzureandInstallDP"></a> Configurar o Microsoft Azure e instalar pontos de distribuição baseados em nuvem  
 Use os procedimentos a seguir para configurar o Microsoft Azure para dar suporte a pontos de distribuição e depois instale o ponto de distribuição baseado em nuvem no Configuration Manager.  

#### <a name="to-configure-a-cloud-service-in-microsoft-azure-for-a-distribution-point"></a>Para configurar um serviço de nuvem no Microsoft Azure para um ponto de distribuição  

1.  Abra um navegador da Web no Portal de Gerenciamento do Microsoft Azure em https://manage.windowsazure.com e acesse sua conta do Microsoft Azure.  

2.  Clique em **Serviços Hospedados, Contas de Armazenamento e CDN** e selecione **Certificados de Gerenciamento**.  

3.  Clique com o botão direito em sua assinatura e selecione **Adicionar Certificado**.  

4.  Para o **arquivo de Certificado**, especifique o arquivo .cer que contém o certificado de gerenciamento do Microsoft Azure exportado que será usado neste serviço de nuvem e clique em **OK**.  

 O certificado de gerenciamento é carregado no Microsoft Azure e agora é possível instalar um ponto de distribuição baseado em nuvem.  

#### <a name="to-install-a-cloud-based-distribution-point-for-configuration-manager"></a>Para instalar um ponto de distribuição baseado em nuvem para o Configuration Manager  

1.  Conclua as etapas no procedimento anterior para configurar o serviço de nuvem no Microsoft Azure com um certificado de gerenciamento.  

2.  No espaço de trabalho **Administração** do console do Configuration Manager, expanda **Serviços em Nuvem**, selecione **Pontos de Distribuição na Nuvem** e, na guia **Início**, clique em **Criar Ponto de Distribuição na Nuvem**.  

3.  Na página **Geral** do Assistente para Criar Ponto de Distribuição na Nuvem, configure:  

    -   Especifique a **ID de Assinatura** de sua conta do Microsoft Azure.  

        > [!TIP]  
        >  Você pode encontrar sua ID de assinatura do Microsoft Azure no Portal de Gerenciamento do Microsoft Azure.  

    -   Especifique o **Certificado de gerenciamento**. Clique em **Procurar** para especificar o arquivo .pfx que contém o certificado de gerenciamento do Microsoft Azure exportado e digite a senha do certificado. Opcionalmente, é possível especificar um arquivo .publishsettings de versão 1 do Microsoft Azure SDK 1.7  

4.  Clique em **Avançar**, e o Configuration Manager se conecta ao Microsoft Azure para validar o certificado de gerenciamento.  

5.  Na página **Configurações** , especifique as seguintes configurações e clique em **Próximo**:  

    -   Para a **Região**, selecione a região do Microsoft Azure onde deseja criar o serviço de nuvem que hospeda este ponto de distribuição.  

    -   Para o **Arquivo de Certificado**, especifique o arquivo .pfx que contém o certificado de serviço de ponto de distribuição baseado em nuvem do Configuration Manager exportado e digite a senha.  

        > [!NOTE]  
        >  A caixa **FQDN do Serviço** é automaticamente preenchida a partir do nome da Entidade do certificado e, na maioria dos casos, não é necessário editá-la. A exceção é se você está usando o certificado com caracteres curinga em um ambiente de teste, onde o nome do host não está especificado para que vários computadores que têm o mesmo sufixo DNS possam usar o certificado. Nesse cenário, a Entidade do certificado contém um valor similar ao **CN=\*.contoso.com** e o Configuration Manager exibe uma mensagem que você deve especificar o FQDN correto. Clique em **OK** para fechar a mensagem e digite um nome específico antes do sufixo DNS para fornecer o FQDN completo. Por exemplo, você pode adicionar **clouddp1** para especificar o FQDN do serviço completo do **clouddp1.contoso.com**. O FQDN do Serviço deve ser exclusivo no domínio e não coincidir com qualquer dispositivo de domínio associado.  
        >   
        >  Os certificados com caracteres curinga têm suporte somente para ambientes de teste.  

6.  Na página **Alertas**, configure as cotas de armazenamento, cotas de transferência e com qual percentual dessas cotas que você deseja que o Configuration Manager gere alertas e clique em **Avançar**.  

7.  Conclua o assistente.  

 O assistente cria um novo serviço hospedado para o ponto de distribuição baseado em nuvem. Ao fechar o assistente, é possível monitorar o progresso da instalação do ponto de distribuição baseado em nuvem no console do Configuration Manager ou o arquivo **CloudMgr.log** no servidor do site primário. Você também pode monitorar o provisionamento do serviço de nuvem no Portal de Gerenciamento do Microsoft Azure.  

> [!NOTE]  
>  Pode levar até 30 minutos para provisionar um novo ponto de distribuição no Microsoft Azure. A seguinte mensagem é repetida no arquivo **CloudMgr.log** até que a conta de armazenamento esteja provisionada: **Aguardando a verificação da existência do contêiner. Verificará novamente em 10 segundos**. Em seguida, o serviço é criado e configurado.  

 Você pode identificar se a instalação do ponto de distribuição baseado em nuvem foi concluída, usando os seguintes métodos:  

-   No Portal de Gerenciamento do Microsoft Azure, a **Implantação** do ponto de distribuição baseado em nuvem exibe um status de **Pronto**.  

-   No espaço de trabalho **Administração**, **Configuração da Hierarquia**, no nó **Nuvem** do console do Configuration Manager, o ponto de distribuição baseado em nuvem exibe o status de **Pronto**.  

-   O Configuration Manager exibe uma mensagem de status com a ID **9409** para o componente SMS_CLOUD_SERVICES_MANAGER.  

##  <a name="a-namebkmkconfigdnsforclouddpsa-configure-name-resolution-for-cloud-based-distribution-points"></a><a name="BKMK_ConfigDNSforCloudDPs"></a> Configurar a resolução de nomes para pontos de distribuição baseados em nuvem  
 Antes que os clientes possam acessar o ponto de distribuição baseado em nuvem, eles devem conseguir resolver o nome do ponto de distribuição baseado em nuvem para um endereço IP gerenciado pelo Microsoft Azure. Os clientes fazem isso em duas etapas:  

1.  Eles mapeiam o nome do serviço fornecido com o certificado de serviço do ponto de distribuição baseado em nuvem do Configuration Manager para o FQDN de serviço do Microsoft Azure. Esse FQDN contém um GUID e o sufixo DNS de **cloudapp.net**. O GUID é gerado automaticamente após a instalação do ponto de distribuição baseado em nuvem. É possível ver o FQDN completo no Portal de Gerenciamento do Microsoft Azure consultando a **URL do SITE** no painel do serviço de nuvem. Uma URL do site de exemplo é **http://d1594d4527614a09b934d470.cloudapp.net**.  

2.  Eles resolvem o FQDN de serviço do Microsoft Azure para o endereço IP alocado pelo Microsoft Azure. Este endereço IP também pode ser identificado no painel do serviço de nuvem no portal do Microsoft Azure, com o nome de **VIP (ENDEREÇO IP VIRTUAL PÚBLICO)**.  

Para mapear o nome do serviço fornecido com o certificado de serviço do ponto de distribuição baseado em nuvem do Configuration Manager (por exemplo, **clouddp1.contoso.com**) para seu FQDN de serviço do Microsoft Azure (por exemplo, **d1594d4527614a09b934d470.cloudapp.net**), os servidores DNS na Internet devem ter um alias DNS (registro CNAME). Em seguida, os clientes podem resolver o FQDN do serviço do Microsoft Azure para o endereço IP usando servidores DNS na Internet.  

##  <a name="a-namebkmkconfigproxyforclouda-configure-proxy-settings-for-primary-sites-that-manage-cloud-services"></a><a name="BKMK_ConfigProxyforCloud"></a> Definir configurações de proxy para sites primários que gerenciam serviços de nuvem  
 Ao usar serviços de nuvem com o Configuration Manager, o site primário que gerencia o ponto de distribuição baseado em nuvem deve ter a capacidade de se conectar ao Portal de Gerenciamento do Microsoft Azure usando a conta do **Sistema** do computador do site primário. Essa conexão é feita usando o navegador da Web padrão no computador do servidor do site primário.  

 No servidor do site primário que gerencia o ponto de distribuição baseado em nuvem, talvez seja necessário definir as configurações de proxy para habilitar o site primário a acessar a Internet e o Microsoft Azure.  

 Use o procedimento a seguir para definir as configurações de proxy para o servidor do site primário no console do Configuration Manager.  

> [!TIP]  
>  Você também pode configurar o servidor proxy quando instalar novas funções do sistema de site no servidor do site primário usando o **Assistente para Adicionar Funções do Sistema de Site**.  

#### <a name="to-configure-proxy-settings-for-the-primary-site-server"></a>Para definir as configurações de proxy para o servidor do site primário  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Configuração do Site**, clique em **Funções de Servidores e Sistema de Site**e selecione o servidor do site primário que gerencia o ponto de distribuição baseado em nuvem.  

3.  No painel de detalhes, clique com o botão direito em **Sistema de Site**e clique em **Propriedades**.  

4.  Em **Propriedades do Sistema de site**, selecione a guia **Proxy** e defina as configurações de proxy para esse servidor do site primário.  

5.  Clique em **OK** para salvar a nova configuração do servidor proxy.  



<!--HONumber=Dec16_HO3-->


