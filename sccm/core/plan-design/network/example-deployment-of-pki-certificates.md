---
title: "Implantação de certificados PKI | System Center Configuration Manager"
description: "Siga um exemplo passo a passo para conhecer o processo de criação e implantação de certificados PKI que usam o System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3417ff88-7177-4a0d-8967-ab21fe7eba17
caps.latest.revision: 11
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 49dfa303453b26a64c1495a1259674e0d8a6bde2


---
# <a name="step-by-step-example-deployment-of-the-pki-certificates-for-system-center-configuration-manager-windows-server-2008-certification-authority"></a>Exemplo de implantação passo a passo dos certificados PKI para o System Center Configuration Manager: Autoridade de Certificação do Windows Server 2008

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este exemplo de implantação passo a passo, que usa uma AC (autoridade de certificação) do Windows Server 2008, contém procedimentos para orientá-lo no processo de criação e implantação de certificados PKI (infraestrutura de chave pública) usados pelo System Center Configuration Manager. Esses procedimentos usam uma Autoridade de Certificação (CA) corporativa e modelos de certificado. As etapas são apropriadas para uma rede de teste somente, como uma verificação de conceito.  

 Como não existe um método único de implantação dos certificados necessários, consulte a documentação de implantação de PKI sobre os procedimentos necessários e as práticas recomendadas para implantar os certificados necessários em um ambiente de produção. Para obter mais informações sobre os requisitos de certificado, consulte [Requisitos de certificado PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

> [!TIP]  
>  As instruções neste tópico podem facilmente ser adaptadas para sistemas operacionais que não estão documentados na seção Requisitos de rede de teste. No entanto, se você estiver executando a AC emissora no Windows Server 2012, a versão do modelo de certificado não será solicitada. Em vez disso, especifique isso na guia **Compatibilidade** das propriedades do modelo, da seguinte forma:  
>   
>  -   **Autoridade de Certificação**: **Windows Server 2003**  
> -   **Destinatário do certificado**: **Windows XP / Server 2003**  

## <a name="in-this-section"></a>Nesta seção  
 As seções a seguir incluem instruções em um exemplo passo a passo de criação e implantação dos seguintes certificados que podem ser usados ​​com o System Center Configuration Manager:  

 [Requisitos de rede de teste](#BKMK_testnetworkenvironment)  

 [Visão geral dos certificados](#BKMK_overview2008)  

 [Implantando o certificado do servidor Web para sistemas de sites que executam IIS](#BKMK_webserver2008_cm2012)  

 [Implantando o certificado de serviço para pontos de distribuição baseados em nuvem](#BKMK_clouddp2008_cm2012)  

 [Implantando o certificado do cliente para computadores com Windows](#BKMK_client2008_cm2012)  

 [Implantando o certificado do cliente para pontos de distribuição](#BKMK_clientdistributionpoint2008_cm2012)  

 [Implantando o certificado de registro para dispositivos móveis](#BKMK_mobiledevices2008_cm2012)  

 [Implantando os certificados para AMT](#BKMK_AMT2008_cm2012)  

 [Implantando o certificado do cliente para computadores Mac](#BKMK_MacClient_SP1)  

##  <a name="a-namebkmktestnetworkenvironmenta-test-network-requirements"></a><a name="BKMK_testnetworkenvironment"></a> Requisitos de rede de teste  
 As instruções passo a passo têm os seguintes requisitos:  

-   A rede de teste está executando Serviços de Domínio do Active Directory no Windows Server 2008, e está instalada como um único domínio, uma única floresta.  

-   Existe um servidor membro executando o Windows Server 2008 Enterprise Edition, que instalou nele a função de Serviços de Certificados do Active Directory, e é configurado como uma Autoridade de Certificação (CA) raiz corporativa.  

-   Você tem um computador com o Windows Server 2008 (Standard Edition ou Enterprise Edition, R2 ou posterior) instalado, designado como um servidor membro, com os IIS (Serviços de Informações da Internet) instalados nele. Esse computador será o servidor do sistema de sites do System Center Configuration Manager que você configurará com um FQDN de intranet (para dar suporte a conexões do cliente na intranet) e um FQDN de Internet, se precisar dar suporte a dispositivos móveis registrados pelo System Center Configuration Manager e clientes na Internet.  

-   Você tem um cliente do Windows Vista com o service pack mais recente instalado e este computador está configurado com um nome de computador que compreende caracteres ASCII e está associado ao domínio. O computador será um computador de cliente do System Center Configuration Manager.  

-   Faça login com uma conta de administrador de domínio raiz ou uma conta de administrador de domínio corporativo e use essa conta para todos os procedimentos desta implantação de exemplo.  

##  <a name="a-namebkmkoverview2008a-overview-of-the-certificates"></a><a name="BKMK_overview2008"></a> Visão geral dos certificados  
 A tabela a seguir lista os tipos de certificados PKI que podem ser necessários para o System Center Configuration Manager e descreve como eles são usados.  

|Requisitos do certificado|Descrição do certificado|  
|-----------------------------|-----------------------------|  
|Certificado do servidor Web para sistemas de sites que executam IIS|Use este certificado para criptografar dados e autenticar o servidor para os clientes. Ele deve ser instalado externamente do System Center Configuration Manager em servidores de sistemas de sites que executam o IIS e que estão configurados no System Center Configuration Manager para usar HTTPS.<br /><br /> Sobre as etapas de configuração e instalação desse certificado, consulte [Implantando o certificado do servidor Web para sistemas de sites que executam IIS](#BKMK_webserver2008_cm2012) , neste tópico.|  
|Certificado de serviço para os clientes se conectarem a pontos de distribuição baseados em nuvem|Para obter as etapas para configurar e instalar este certificado, consulte [Implantando o certificado de serviço para pontos de distribuição baseados em nuvem](#BKMK_clouddp2008_cm2012) neste tópico.<br /><br /> **Importante:** esse certificado é usado em conjunto com o certificado de gerenciamento do Microsoft Azure. Para obter mais informações sobre o certificado de gerenciamento, consulte [Como criar um certificado de gerenciamento para o Windows Azure](http://go.microsoft.com/fwlink/p/?LinkId=220281) e [Como adicionar um certificado de gerenciamento a uma assinatura do Windows Azure](http://go.microsoft.com/fwlink/?LinkId=241722) na seção Plataforma Windows Azure da Biblioteca MSDN.|  
|Certificado do cliente para computadores com Windows|Use este certificado para autenticar computadores cliente do System Center Configuration Manager em sistemas de sites que estão configurados para usar HTTPS. Ele também pode ser usado para pontos de gerenciamento e pontos de migração para monitoramento do status operacional quando estiverem configurados para usar HTTPS. Ele deve ser instalado externamente ao System Center Configuration Manager nos computadores.<br /><br /> Para obter as etapas para configurar e instalar este certificado, veja [Implantando o certificado do cliente para computadores com Windows](#BKMK_client2008_cm2012) neste tópico.|  
|Certificado do cliente para pontos de distribuição|Este certificado tem duas finalidades:<br /><br /> Use este certificado para autenticar o ponto de distribuição para um ponto de gerenciamento habilitado para HTTPS antes que o ponto de distribuição envie mensagens de status.<br /><br /> Quando a opção do ponto de distribuição **Habilitar suporte a PXE para clientes** é selecionada, o certificado é enviado para computadores que o PXE inicializa para que eles possam se conectar a um ponto de gerenciamento habilitado para HTTPS durante a implantação do sistema operacional.<br /><br /> Sobre as etapas de configuração e instalação desse certificado, consulte [Implantando o certificado do cliente para pontos de distribuição](#BKMK_clientdistributionpoint2008_cm2012) , neste tópico.|  
|Certificado de registro para dispositivos móveis|Use este certificado para autenticar clientes de dispositivos móveis do System Center Configuration Manager em sistemas de sites que estão configurados para usar HTTPS. Ele deve ser instalado como parte do registro do dispositivo móvel no System Center Configuration Manager e você seleciona o modelo do certificado definido como uma configuração do cliente do dispositivo móvel.<br /><br /> Para obter as etapas para configurar este certificado, veja [Deploying the Enrollment Certificate for Mobile Devices](#BKMK_mobiledevices2008_cm2012) neste tópico.|  
|Certificados para Intel AMT|Há três certificados relacionados a gerenciamento fora da banda para computadores Intel AMT: Um certificado de provisionamento AMT, um certificado do servidor Web AMT e, opcionalmente, um certificado de autenticação de cliente para redes 802.1X com ou sem fio.<br /><br /> Instale o certificado de provisionamento do AMT externamente ao System Center Configuration Manager no computador do ponto de serviço fora da banda, e depois selecione o certificado instalado nas propriedades do ponto de serviço fora da banda. O certificado do servidor Web AMT e o certificado de autenticação de cliente são instalados durante provisionamento e gerenciamento de AMT, e você seleciona os modelos de certificado configurados nas propriedades dos componentes de gerenciamento fora da banda.<br /><br /> Sobre as etapas de configuração e instalação desse certificado, consulte [Implantando os certificados para AMT](#BKMK_AMT2008_cm2012) , neste tópico.|  
|Certificado do cliente para computadores Mac|Em um computador Mac, solicite e instale esse certificado quando usar o registro do System Center Configuration Manager e selecione o modelo de certificado definido como uma configuração do cliente do dispositivo móvel.<br /><br /> Para obter as etapas para configurar este certificado, veja [Deploying the Client Certificate for Mac Computers](#BKMK_MacClient_SP1) neste tópico.|  

##  <a name="a-namebkmkwebserver2008cm2012a-deploying-the-web-server-certificate-for-site-systems-that-run-iis"></a><a name="BKMK_webserver2008_cm2012"></a> Implantando o certificado do servidor Web para sistemas de sites que executam IIS  
 Esta implantação de certificados abrange os seguintes procedimentos:  

-   Criar e emitir o modelo de certificado do servidor Web na Autoridade de Certificação  

-   Solicitando o certificado do servidor Web  

-   Configurar o IIS para usar o certificado do servidor Web  

###  <a name="a-namebkmkwebserver22008a-creating-and-issuing-the-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_webserver22008"></a> Criar e emitir o modelo de certificado do servidor Web na Autoridade de Certificação  
 Esse procedimento cria um modelo de certificado para sistemas de sites do System Center Configuration Manager e o adiciona à Autoridade de Certificação.  

##### <a name="to-create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a>Criar e emitir o modelo de certificado do servidor Web na Autoridade de Certificação  

1.  Crie um grupo de segurança chamado **Servidores IIS ConfigMgr** que contenha os servidores membros para instalar os sistemas de sites do System Center Configuration Manager que executarão o IIS.  

2.  No servidor membro que tem os Serviços de Certificados instalados, no console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado** e clique em **Gerenciar** para carregar o console **Modelos de Certificado** .  

3.  No painel de resultados, clique com o botão direito do mouse na entrada que exibe **Servidor Web** na coluna **Nome de Exibição do Modelo**e clique em **Duplicar Modelo**.  

4.  Na caixa de diálogo **Duplicar Modelo** , verifique se a opção **Windows 2003 Server, Enterprise Edition** está marcada e clique em **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

5.  Na caixa de diálogo **Propriedades do novo modelo** , na guia **Geral** , insira um nome de modelo para gerar os certificados Web que serão usados nos sistemas de sites do Configuration Manager, como **Certificado do servidor Web do ConfigMgr**.  

6.  Clique na guia **Nome da entidade** e verifique se **Fornecer na solicitação** está selecionado.  

7.  Clique na guia **Segurança** e remova a permissão **Registrar** dos grupos de segurança **Admins. do domínio** e **Admins. da empresa**.  

8.  Clique em **Adicionar**, insira **Servidores IIS do ConfigMgr** na caixa de texto e clique em **OK**.  

9. Selecione a permissão **Registrar** para este grupo e não desmarque a permissão **Ler** .  

10. Clique em **OK**e feche o **Console de modelos de certificado**.  

11. No console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado**, clique em **Novo**e em **Modelo de certificado a ser emitido**.  

12. Na caixa de diálogo **Ativar modelos de certificado** , selecione o novo modelo que você acabou de criar, **Certificado do servidor Web do ConfigMgr**, e clique em **OK**.  

13. Se você não precisar criar ou emitir mais certificados, feche a **Autoridade de Certificação**.  

###  <a name="a-namebkmkwebserver32008a-requesting-the-web-server-certificate"></a><a name="BKMK_webserver32008"></a> Solicitando o certificado do servidor Web  
 Este procedimento permite que você especifique valores FQDN de intranet e Internet que serão configurados nas propriedades do servidor de sistema de sites e instale o certificado do servidor Web no servidor membro que executa o IIS.  

##### <a name="to-request-the-web-server-certificate"></a>Para solicitar o certificado do servidor Web  

1.  Reinicie o servidor membro que executa o IIS, para garantir que o computador possa acessar o modelo de certificado que você criou, usando as permissões **Ler** e **Registrar** configuradas por você.  

2.  Clique em **Iniciar**, clique em **Executar**e digite **mmc.exe.** No console vazio, clique em **Arquivo**e clique em **Adicionar/Remover Snap-in**.  

3.  Na caixa de diálogo **Adicionar ou Remover Snap-ins** , selecione **Certificados** na lista de **Snap-ins disponíveis**e clique em **Adicionar**.  

4.  Na caixa de diálogo **Snap-in de certificado** , selecione **Conta de computador**e clique em **Próximo**.  

5.  Na caixa de diálogo **Selecionar Computador** , verifique se a opção **Computador Local: (o computador no qual este console está sendo executado)** está marcada e clique em **Concluir**.  

6.  Na caixa de diálogo **Adicionar ou Remover Snap-ins** , clique em **OK**.  

7.  No console, expanda **Certificados (computador local)**e clique em **Pessoal**.  

8.  Clique com o botão direito do mouse em **Certificados**, clique em **Todas as Tarefas**e em **Solicitar Novo Certificado**.  

9. Na página **Antes de Começar** , clique em **Avançar**.  

10. Se você vir a página **Selecionar política de registro de certificado** , clique em **Próximo**.  

11. Na página **Solicitar Certificados**, identifique o **Certificado do Servidor Web do ConfigMgr** na lista de certificados exibidos e clique em **Mais informações são necessárias para se registrar neste certificado. Clique aqui para definir as configurações**.  

12. Na caixa de diálogo **Propriedades do Certificado** , na guia **Entidade** , não faça nenhuma alteração no **Nome da entidade**. Isso significa que a caixa **Valor** para o **Nome da entidade** permanece em branco. Em vez disso, na seção **Nome alternativo** , clique na lista suspensa **Tipo** e selecione **DNS**.  

13. Na caixa **Valor**, especifique os valores de FQDN que serão especificados nas propriedades do sistema de sites do System Center Configuration Manager e clique em **OK** para fechar a caixa de diálogo **Propriedades do Certificado**.  

     Exemplos:  

    -   Se o sistema de sites só aceitar conexões de clientes da intranet, e o FQDN de intranet do servidor do sistema de sites for **server1.internal.contoso.com**: Digite **server1.internal.contoso.com**e clique em **Adicionar**.  

    -   Se o sistema de sites aceitar conexões de clientes da intranet e da Internet, o FQDN de intranet do servidor do sistema de sites for **server1.internal.contoso.com** e o FQDN de Internet do servidor do sistema de sites for **server.contoso.com**:  

        1.  Digite **server1.internal.contoso.com**e clique em **Adicionar**.  

        2.  Digite **server.contoso.com**e clique em **Adicionar**.  

        > [!NOTE]  
        >  Não importa em que ordem você especifica os FQDNs para o System Center Configuration Manager. No entanto, verifique se todos os dispositivos que usam o certificado, tais como dispositivos móveis e servidores Web proxy, podem usar um certificado SAN e vários valores no SAN. Se os dispositivos tiverem suporte limitado para valores de SAN em certificados, altere a ordem dos FQDNs ou use o valor Entidade.  

14. Na página **Solicitar certificados** , selecione **Certificado do servidor Web do ConfigMgr** , na lista de certificados exibida, e clique em **Registrar**.  

15. Na página **Resultados da instalação de certificados** , espere até que o certificado seja instalado e clique em **Concluir**.  

16. Feche os **Certificados (computador local)**.  

###  <a name="a-namebkmkwebserver42008a-configuring-iis-to-use-the-web-server-certificate"></a><a name="BKMK_webserver42008"></a> Configurar o IIS para usar o certificado do servidor Web  
 Este procedimento associa o certificado instalado ao **Site Padrão**do IIS.  

##### <a name="to-configure-iis-to-use-the-web-server-certificate"></a>Para configurar o IIS para usar o certificado do servidor Web  

1.  No servidor membro instalado pelo IIS, clique em **Iniciar**, clique em **Programas**, clique em **Ferramentas Administrativas**e em **Gerenciador do IIS (Serviços de Informações da Internet)**.  

2.  Expanda **Sites**, clique com o botão direito em **Site Padrão**e selecione **Editar Ligações**.  

3.  Clique na entrada **https** e em **Editar**.  

4.  Na caixa de diálogo **Editar Ligação do Site** , selecione o certificado que você solicitou usando o modelo de Certificados do Servidor Web ConfigMgr e clique em **OK**.  

    > [!NOTE]  
    >  Se não tiver certeza de qual é o certificado correto, selecione um e clique em **Exibir**. Isso permite comparar os detalhes do certificado selecionado com os certificados que são exibidos com o snap-in de Certificados. Por exemplo, o snap-in de Certificados exibe o modelo de certificado que foi usado para solicitar o certificado. Em seguida, você pode comparar a impressão digital do certificado do certificado solicitado com o modelo de Certificados do Servidor Web ConfigMgr com a impressão digital do certificado do certificado selecionado atualmente na caixa de diálogo **Editar Ligação do Site** .  

5.  Clique em **OK** na caixa de diálogo **Editar Ligação do Site** e clique em **Fechar**.  

6.  Feche o **Gerenciador do IIS (Serviços de Informações da Internet)**.  

 Agora, o servidor membro está provisionado com um certificado do servidor Web do System Center Configuration Manager.  

> [!IMPORTANT]  
>  Ao instalar o servidor do sistema de sites do System Center Configuration Manager neste computador, verifique se você especificou os mesmos FQDNs nas propriedades do sistema de sites que especificou ao solicitar o certificado.  

##  <a name="a-namebkmkclouddp2008cm2012a-deploying-the-service-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddp2008_cm2012"></a> Implantando o certificado de serviço para pontos de distribuição baseados em nuvem  

> [!NOTE]  
>  O certificado de serviço para pontos de distribuição baseados em nuvem se aplica ao System Center Configuration Manager SP1 e posterior.  

 Esta implantação de certificados abrange os seguintes procedimentos:  

-   [Criar e emitir o modelo personalizado de certificado do servidor Web na Autoridade de Certificação](#BKMK_clouddpcreating2008)  

-   [Solicitar o certificado personalizado do servidor Web](#BKMK_clouddprequesting2008)  

-   [Exportar o certificado personalizado do servidor Web para pontos de distribuição baseados em nuvem](#BKMK_clouddpexporting2008)  

###  <a name="a-namebkmkclouddpcreating2008a-creating-and-issuing-a-custom-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_clouddpcreating2008"></a> Criar e emitir o modelo personalizado de certificado do servidor Web na Autoridade de Certificação  
 Este procedimento cria um modelo de certificado personalizado com base no modelo de certificado do servidor Web. O certificado é para os pontos de distribuição baseados em nuvem do System Center Configuration Manager e a chave privada deve ser exportável. Depois que o modelo de certificado é criado, ele é adicionado à autoridade de certificação.  

> [!NOTE]  
>  Este procedimento usa um modelo de certificado diferente do modelo de certificado do servidor Web que você criou para sistemas de site que executam IIS, pois embora ambos os certificados requeiram recurso de autenticação do servidor, o certificado para pontos de distribuição baseados em nuvem requer a inserção de um valor com definição personalizada para o Nome da entidade, e a chave privada deve ser exportada. Como prática recomendada de segurança, não configure modelos de certificado para permitir que a chave privada seja exportada a menos que essa configuração seja solicitada. O ponto de distribuição baseado em nuvem requer essa configuração, pois você deve importar o certificado como um arquivo, em vez de selecioná-lo do repositório de certificados.  
>   
>  Ao criar um novo modelo de certificado para esse certificado, você pode restringir quais computadores requerem um certificado que permite a exportação da chave privada. Em uma rede de produção, você também pode adicionar as seguintes modificações para esse certificado:  
>   
>  -   Requerer aprovação para instalar o certificado, para obter segurança adicional.  
> -   Aumentar o período de validade do certificado. Como você precisa exportar e importar o certificado todas as vezes antes de ele expirar, aumentar o período de validade reduz a frequência de repetição desse procedimento. No entanto, quando você aumenta o período de validade, ele diminui a segurança do certificado, pois ele oferece mais tempo para que um invasor descriptografe a chave privada e roube o certificado.  
> -   Usar um valor personalizado no SAN (Nome Alternativo da Entidade) do certificado para ajudar a identificá-lo dos certificados do servidor Web padrão que você usa com o IIS.  

##### <a name="to-create-and-issue-the-custom-web-server-certificate-template-on-the-certification-authority"></a>Para criar e emitir o modelo de certificado personalizado do servidor Web na autoridade de certificação  

1.  Crie um grupo de segurança chamado **Servidores de Site do ConfigMgr** que contenha os servidores membros para instalar os servidores do site primário do System Center Configuration Manager que gerenciará os pontos de distribuição baseados em nuvem.  

2.  No servidor membro que executa o console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado**e clique em **Gerenciar** para carregar o console de gerenciamento Modelos de Certificado.  

3.  No painel de resultados, clique com o botão direito do mouse na entrada que exibe **Servidor Web** na coluna **Nome de Exibição do Modelo**e clique em **Duplicar Modelo**.  

4.  Na caixa de diálogo **Duplicar Modelo** , verifique se a opção **Windows 2003 Server, Enterprise Edition** está marcada e clique em **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

5.  Na caixa de diálogo **Propriedades do novo modelo** , na guia **Geral** , insira um nome de modelo para gerar os certificados do servidor Web para pontos de distribuição baseados em nuvem, como **Certificado do ponto de distribuição baseado em nuvem do ConfigMgr**.  

6.  Clique na guia **Tratamento de Solicitação** e selecione **Permitir que a chave privada seja exportada**.  

7.  Clique na guia **Segurança** e remova a permissão **Registrar** do grupo de segurança **Administradores de Empresa** .  

8.  Clique em **Adicionar**, insira **Servidores do Site do ConfigMgr** na caixa de texto e clique em **OK**.  

9. Selecione a permissão **Registrar** para este grupo e não desmarque a permissão **Ler** .  

10. Clique em **OK** e feche o **Console de Modelos de Certificado**.  

11. No console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado**, clique em **Novo**e em **Modelo de certificado a ser emitido**.  

12. Na caixa de diálogo **Ativar Modelos de Certificado** , selecione o novo modelo que você acabou de criar, **Certificado do ponto de distribuição baseado em nuvem do ConfigMgr**e clique em **OK**.  

13. Se você não precisar criar ou emitir mais certificados, feche a **Autoridade de Certificação**.  

###  <a name="a-namebkmkclouddprequesting2008a-requesting-the-custom-web-server-certificate"></a><a name="BKMK_clouddprequesting2008"></a> Solicitar o certificado personalizado do servidor Web  
 Este procedimento solicita e instala o certificado personalizado do servidor Web no servidor membro que executará o servidor do site.  

##### <a name="to-request-the-custom-web-server-certificate"></a>Para solicitar o certificado personalizado do servidor Web  

1.  Reinicie o servidor membro depois de criar e configurar o grupo de segurança **Servidores do Site do ConfigMgr** para assegurar que o computador pode acessar o modelo de certificado criado usando as permissões **Ler** e **Registrar** que você configurou.  

2.  Clique em **Iniciar**, clique em **Executar**e digite **mmc.exe.** No console vazio, clique em **Arquivo**e clique em **Adicionar/Remover Snap-in**.  

3.  Na caixa de diálogo **Adicionar ou Remover Snap-ins** , selecione **Certificados** na lista de **Snap-ins disponíveis**e clique em **Adicionar**.  

4.  Na caixa de diálogo **Snap-in de certificado** , selecione **Conta de computador**e clique em **Próximo**.  

5.  Na caixa de diálogo **Selecionar Computador** , verifique se a opção **Computador Local: (o computador no qual este console está sendo executado)** está marcada e clique em **Concluir**.  

6.  Na caixa de diálogo **Adicionar ou Remover Snap-ins** , clique em **OK**.  

7.  No console, expanda **Certificados (computador local)**e clique em **Pessoal**.  

8.  Clique com o botão direito do mouse em **Certificados**, clique em **Todas as Tarefas**e em **Solicitar Novo Certificado**.  

9. Na página **Antes de Começar** , clique em **Avançar**.  

10. Se você vir a página **Selecionar política de registro de certificado** , clique em **Próximo**.  

11. Na página **Solicitar Certificados**, identifique o **Certificado do Ponto de Distribuição Baseado em Nuvem do ConfigMgr** na lista de certificados exibidos e clique em **Mais informações são necessárias para se registrar neste certificado. Clique aqui para definir as configurações**.  

12. Na caixa de diálogo **Propriedades do Certificado** , na guia **Entidade** do **Nome da entidade**, selecione **Nome comum** como **Tipo**.  

13. Na caixa **Valor** , especifique a escolha do nome do serviço e do nome de domínio usando um formato FQDN. Por exemplo: **clouddp1.contoso.com**.  

    > [!NOTE]  
    >  Não importa o nome do serviço que você especifica, desde que ele seja único no seu namespace. Você usará o DNS para criar um alias (registro CNAME) para mapear este nome do serviço para um GUID (identificador) gerado automaticamente e um endereço IP do Windows Azure.  

14. Clique em **Adicionar**e clique em **OK** para fechar a caixa de diálogo **Propriedades do Certificado** .  

15. Na página **Solicitar certificados** , selecione **Certificado do ponto de distribuição baseado em nuvem do ConfigMgr** na lista de certificados exibida e clique em **Registrar**.  

16. Na página **Resultados da instalação de certificados** , espere até que o certificado seja instalado e clique em **Concluir**.  

17. Feche os **Certificados (computador local)**.  

###  <a name="a-namebkmkclouddpexporting2008a-exporting-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddpexporting2008"></a> Exportar o certificado personalizado do servidor Web para pontos de distribuição baseados em nuvem  
 Este procedimento exporta o certificado personalizado do servidor Web para um arquivo, assim ele pode ser importando quando você criar o ponto de distribuição baseado em nuvem.  

##### <a name="to-export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a>Para exportar o certificado personalizado do servidor Web para pontos de distribuição baseados em nuvem  

1.  No console **Certificados (Computador Local)** , clique com o botão direito do mouse no certificado que você acabou de instalar, selecione **Todas as Tarefas**e clique em **Exportar**.  

2.  No Assistente para Exportação de Certificados, clique em **Próximo**.  

3.  Na página **Exportar chave privada** , selecione **Sim, exportar a chave privada**e clique em **Próximo**.  

    > [!NOTE]  
    >  Se essa opção não estiver disponível, o certificado foi criado sem a opção de exportar a chave privada. Nesse cenário, você não pode exportar o certificado no formato exigido. Você deve configurar o modelo de certificado para permitir que a chave privada seja exportada e, em seguida, solicitar o certificado novamente.  

4.  Na página **Formato do arquivo de exportação** , verifique se a opção **Troca de informações pessoais - PKCS nº 12 (.PFX)** esta selecionada.  

5.  Na página **Senha** , especifique uma senha forte para proteger o certificado exportado com sua chave privada e clique em **Próximo**.  

6.  Na página **Arquivo a ser exportado** , especifique o nome do arquivo que você deseja exportar e clique em **Próximo**.  

7.  Para fechar o assistente, clique em **Concluir** na página **Assistente para Exportação de Certificados** e clique em **OK** na caixa de diálogo de confirmação.  

8.  Feche os **Certificados (computador local)**.  

9. Armazene o arquivo com segurança e verifique se você pode acessá-lo do console do System Center Configuration Manager.  

 O certificado agora está pronto para ser importado quando você criar um ponto de distribuição baseado em nuvem.  

##  <a name="a-namebkmkclient2008cm2012a-deploying-the-client-certificate-for-windows-computers"></a><a name="BKMK_client2008_cm2012"></a> Implantando o certificado do cliente para computadores com Windows  
 Esta implantação de certificados abrange os seguintes procedimentos:  

-   Criar e emitir o modelo de certificado de autenticação de estação de trabalho na autoridade de certificação  

-   Configurar o registro automático do modelo de autenticação da estação de trabalho usando a política de grupo  

-   Registrar automaticamente o certificado de autenticação de estação de trabalho e verificar sua instalação nos computadores  

###  <a name="a-namebkmkclient02008a-creating-and-issuing-the-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_client02008"></a> Criar e emitir o modelo de certificado de autenticação de estação de trabalho na autoridade de certificação  
 Esse procedimento cria um modelo de certificado para computadores cliente do System Center Configuration Manager e o adiciona à Autoridade de Certificação.  

##### <a name="to-create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a>Para criar e emitir o modelo de certificado de autenticação de estação de trabalho na autoridade de certificação  

1.  No servidor membro que executa o console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado**e clique em **Gerenciar** para carregar o console de gerenciamento Modelos de Certificado.  

2.  No painel de resultados, clique com o botão direito do mouse na entrada que exibe **Autenticação de estação de trabalho** na coluna **Nome de Exibição do Modelo**e clique em **Duplicar Modelo**.  

3.  Na caixa de diálogo **Duplicar Modelo** , verifique se a opção **Windows 2003 Server, Enterprise Edition** está marcada e clique em **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

4.  Na caixa de diálogo **Propriedades do novo modelo** , na guia **Geral** , insira um nome de modelo para gerar os certificados do cliente que serão usados nos computadores cliente do Configuration Manager, como **Certificado cliente do ConfigMgr**.  

5.  Clique na guia **Segurança** , selecione o grupo **Computadores do domínio** e selecione as permissões adicionais **Ler** e **Registrar automaticamente**. Não desmarque **Registrar**.  

6.  Clique em **OK** e feche o **Console de Modelos de Certificado**.  

7.  No console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado**, clique em **Novo**e em **Modelo de certificado a ser emitido**.  

8.  Na caixa de diálogo **Ativar Modelos de Certificado** , selecione o novo modelo que você acabou de criar, **Certificado do cliente do ConfigMgr**e clique em **OK**.  

9. Se você não precisar criar ou emitir mais certificados, feche a **Autoridade de Certificação**.  

###  <a name="a-namebkmkclient12008a-configuring-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a><a name="BKMK_client12008"></a> Configurar o registro automático do modelo de autenticação da estação de trabalho usando a política de grupo  
 Este procedimento configura a política de grupo para registrar automaticamente o certificado do cliente em computadores.  

##### <a name="to-configure-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a>Para configurar o registro automático do modelo de autenticação de estação de trabalho usando a política de grupo  

1.  No controlador de domínio, clique em **Iniciar**, clique em **Ferramentas Administrativas**e em **Gerenciamento de Política de Grupo**.  

2.  Navegue até seu domínio, clique nele com o botão direito e selecione **Criar um GPO neste domínio e fornecer um link para ele aqui**.  

    > [!NOTE]  
    >  Esta etapa usa a prática recomendada de criação de uma nova Política de Grupo para configurações personalizadas em vez de editar a Política de Domínio Padrão que está instalada com os Serviços de Domínio Active Directory. Com a atribuição dessa Política de Grupo no nível de domínio, você a aplicará a todos os computadores no domínio. No entanto, em um ambiente de produção, você pode restringir o registro automático para que ela se registre somente em computadores selecionados atribuindo a Política da Grupo em um nível da unidade organizacional ou você pode filtrar a Política de Grupo do domínio com um grupo de segurança para que ela se aplique somente aos computadores no grupo. Se você restringir o registro automático, lembre-se de incluir o servidor que esteja configurado como ponto de gerenciamento.  

3.  Na caixa de diálogo **Novo GPO** , insira um nome para a nova Política de Grupo, como **Certificados de registro automático**e clique em **OK**.  

4.  No painel de resultados, na guia **Objetos de Política de Grupo Vinculados** , clique com o botão direito na nova Política de Grupo e clique em **Editar**.  

5.  Na caixa de diálogo **Editor de Gerenciamento de Política de Grupo**, expanda **Políticas** em **Configuração do Computador**e navegue até **Configurações do Windows** / **Configurações de Segurança** / **Public Key Políticas**.  

6.  Clique com o botão direito do mouse no tipo de objeto chamado **Cliente Serviços Certificado – Registro Autom.** e clique em **Propriedades**.  

7.  Na lista suspensa **Modelo de Configuração** , selecione **Habilitado**, **Renovar certificados expirados, atualizar certificados pendentes e remover certificados revogados**, **Atualizar certificados que usam modelos de certificados**e clique em **OK**.  

8.  Feche o **Gerenciamento de Política de Grupo**.  

###  <a name="a-namebkmkclient22008a-automatically-enrolling-the-workstation-authentication-certificate-and-verifying-its-installation-on-computers"></a><a name="BKMK_client22008"></a> Registrar automaticamente o certificado de autenticação de estação de trabalho e verificar sua instalação nos computadores  
 Este procedimento instala o certificado do cliente em computadores e verifica a instalação.  

##### <a name="to-automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-the-client-computer"></a>Para registrar automaticamente o certificado de autenticação de estação de trabalho e verificar sua instalação no computador cliente  

1.  Reinicie o computador da estação de trabalho e aguarde alguns minutos antes de fazer logon.  

    > [!NOTE]  
    >  A reinicialização de um computador é o método mais confiável de garantir o êxito no registro automático do certificado.  

2.  Faça logon com uma conta que tenha privilégios administrativos.  

3.  Na caixa de pesquisa, digite **mmc.exe.**e pressione **Enter**.  

4.  No console de gerenciamento vazio, clique em **Arquivo**e, depois, em **Adicionar/Remover Snap-in**.  

5.  Na caixa de diálogo **Adicionar ou Remover Snap-ins** , selecione **Certificados** na lista de **Snap-ins disponíveis**e clique em **Adicionar**.  

6.  Na caixa de diálogo **Snap-in de certificado** , selecione **Conta de computador**e clique em **Próximo**.  

7.  Na caixa de diálogo **Selecionar Computador** , verifique se a opção **Computador local: (o computador no qual este console está sendo executado)** está marcada e clique em **Concluir**.  

8.  Na caixa de diálogo **Adicionar ou Remover Snap-ins** , clique em **OK**.  

9. No console, expanda **Certificados (computador local)**e, em seguida, **Pessoal**e clique em **Certificados**.  

10. No painel de resultados, confirme que um certificado exibido tem a **Autenticação de Cliente** exibida na coluna **Finalidade** e que o **Certificado do Cliente do ConfigMgr** é exibido na coluna **Modelo de certificado** .  

11. Feche os **Certificados (computador local)**.  

12. Repita as etapas de 1 a 11 para o servidor membro para verificar se o servidor que será configurado como ponto de gerenciamento também tem um certificado do cliente.  

 Agora, o computador está provisionado com um certificado de cliente do System Center Configuration Manager.  

##  <a name="a-namebkmkclientdistributionpoint2008cm2012a-deploying-the-client-certificate-for-distribution-points"></a><a name="BKMK_clientdistributionpoint2008_cm2012"></a> Implantando o certificado do cliente para pontos de distribuição  

> [!NOTE]  
>  Este certificado também pode ser usado para imagens de mídia que não usam inicialização PXE, pois os requisitos do certificado são os mesmos.  

 Esta implantação de certificados abrange os seguintes procedimentos:  

-   Criar e emitir um modelo personalizado de certificado de autenticação de estação de trabalho na autoridade de certificação  

-   Solicitar o certificado personalizado de autenticação de estação de trabalho  

-   Exportar o certificado do cliente para pontos de distribuição  

###  <a name="a-namebkmkclientdistributionpoint02008a-creating-and-issuing-a-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_clientdistributionpoint02008"></a> Criar e emitir um modelo personalizado de certificado de autenticação de estação de trabalho na autoridade de certificação  
 Este procedimento cria um modelo de certificado personalizado para pontos de distribuição do System Center Configuration Manager que permitem a exportação da chave privada e adiciona o modelo de certificado à autoridade de certificação.  

> [!NOTE]  
>  Este procedimento usa um modelo de certificado diferente daquele que você criou para computadores cliente, pois embora ambos os certificados requeiram recurso de autenticação de cliente, o certificado para pontos de distribuição requer a exportação da chave privada. Como prática recomendada de segurança, não configure modelos de certificado para permitir que a chave privada seja exportada a menos que essa configuração seja solicitada. O ponto de distribuição requer essa configuração, pois você deve importar o certificado como um arquivo, em vez de selecioná-lo do repositório de certificados.  
>   
>  Ao criar um novo modelo de certificado para esse certificado, você pode restringir quais computadores requerem um certificado que permite a exportação da chave privada. No exemplo de implantação, esse será o grupo de segurança que você criou anteriormente para servidores do sistema de sites do System Center Configuration Manager que executam o IIS. Em uma rede de produção que distribui as funções do sistema de site do IIS, considere a criação de um novo grupo de segurança para os servidores que executam pontos de distribuição, assim você pode restringir o certificado apenas para esses servidores do sistema de site. Você também pode adicionar as seguintes modificações para o certificado:  
>   
>  -   Requerer aprovação para instalar o certificado, para obter segurança adicional.  
> -   Aumentar o período de validade do certificado. Como você precisa exportar e importar o certificado todas as vezes antes de ele expirar, aumentar o período de validade reduz a frequência de repetição desse procedimento. No entanto, quando você aumenta o período de validade, ele diminui a segurança do certificado, pois ele oferece mais tempo para que um invasor descriptografe a chave privada e roube o certificado.  
> -   Usar um valor personalizado no campo Entidade do certificado ou SAN (Nome Alternativo da Entidade) para ajudar a identificar esse certificado dos certificados do cliente padrão. Isso pode ser particularmente útil se você usar o mesmo certificado para vários pontos de distribuição.  

##### <a name="to-create-and-issue-the-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a>Para criar e emitir o modelo personalizado de certificado de autenticação de estação de trabalho na autoridade de certificação  

1.  No servidor membro que executa o console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado**e clique em **Gerenciar** para carregar o console de gerenciamento Modelos de Certificado.  

2.  No painel de resultados, clique com o botão direito do mouse na entrada que exibe **Autenticação de estação de trabalho** na coluna **Nome de Exibição do Modelo**e clique em **Duplicar Modelo**.  

3.  Na caixa de diálogo **Duplicar Modelo** , verifique se a opção **Windows 2003 Server, Enterprise Edition** está marcada e clique em **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

4.  Na caixa de diálogo **Propriedades do novo modelo** , na guia **Geral** , insira um nome de modelo para gerar o certificado de autenticação de cliente para pontos de distribuição, como **Certificado do ponto de distribuição do cliente do ConfigMgr**.  

5.  Clique na guia **Tratamento de Solicitação** e selecione **Permitir que a chave privada seja exportada**.  

6.  Clique na guia **Segurança** e remova a permissão **Registrar** do grupo de segurança **Administradores de Empresa** .  

7.  Clique em **Adicionar**, insira **Servidores IIS do ConfigMgr** na caixa de texto e clique em **OK**.  

8.  Selecione a permissão **Registrar** para este grupo e não desmarque a permissão **Ler** .  

9. Clique em **OK** e feche o **Console de Modelos de Certificado**.  

10. No console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado**, clique em **Novo**e em **Modelo de certificado a ser emitido**.  

11. Na caixa de diálogo **Ativar Modelos de Certificado** , selecione o novo modelo que você acabou de criar, **Certificado do ponto de distribuição do cliente do ConfigMgr**e clique em **OK**.  

12. Se você não precisar criar ou emitir mais certificados, feche a **Autoridade de Certificação**.  

###  <a name="a-namebkmkclientdistributionpoint12008a-requesting-the-custom-workstation-authentication-certificate"></a><a name="BKMK_clientdistributionpoint12008"></a> Solicitar o certificado personalizado de autenticação de estação de trabalho  
 Este procedimento solicita e instala o certificado do cliente personalizado no servidor membro que executa o IIS e que será configurado como ponto de distribuição.  

##### <a name="to-request-the-custom-workstation-authentication-certificate"></a>Para solicitar o certificado personalizado de autenticação de estação de trabalho  

1.  Clique em **Iniciar**, clique em **Executar**e digite **mmc.exe.** No console vazio, clique em **Arquivo**e clique em **Adicionar/Remover Snap-in**.  

2.  Na caixa de diálogo **Adicionar ou Remover Snap-ins** , selecione **Certificados** na lista de **Snap-ins disponíveis**e clique em **Adicionar**.  

3.  Na caixa de diálogo **Snap-in de certificado** , selecione **Conta de computador**e clique em **Próximo**.  

4.  Na caixa de diálogo **Selecionar Computador** , verifique se a opção **Computador Local: (o computador no qual este console está sendo executado)** está marcada e clique em **Concluir**.  

5.  Na caixa de diálogo **Adicionar ou Remover Snap-ins** , clique em **OK**.  

6.  No console, expanda **Certificados (computador local)**e clique em **Pessoal**.  

7.  Clique com o botão direito do mouse em **Certificados**, clique em **Todas as Tarefas**e em **Solicitar Novo Certificado**.  

8.  Na página **Antes de Começar** , clique em **Avançar**.  

9. Se você vir a página **Selecionar política de registro de certificado** , clique em **Próximo**.  

10. Na página **Solicitar certificados** , selecione o **Certificado do ponto de distribuição do cliente do ConfigMgr** na lista de certificados exibida e clique em **Registrar**.  

11. Na página **Resultados da instalação de certificados** , espere até que o certificado seja instalado e clique em **Concluir**.  

12. No painel de resultados, confirme que um certificado exibido tem a **Autenticação de Cliente** exibida na coluna **Finalidade** e que o **Certificado do ponto de distribuição do cliente do ConfigMgr** é exibido na coluna **Modelo de certificado** .  

13. Não feche os **Certificados (computador local)**.  

###  <a name="a-namebkmkexportclientdistributionpoint22008a-exporting-the-client-certificate-for-distribution-points"></a><a name="BKMK_exportclientdistributionpoint22008"></a> Exportar o certificado do cliente para pontos de distribuição  
 Este procedimento exporta o certificado personalizado de autenticação de estação de trabalho para um arquivo, assim ele pode ser importado nas propriedades do ponto de distribuição.  

##### <a name="to-export-the-client-certificate-for-distribution-points"></a>Para exportar o certificado do cliente para pontos de distribuição  

1.  No console **Certificados (Computador Local)** , clique com o botão direito do mouse no certificado que você acabou de instalar, selecione **Todas as Tarefas**e clique em **Exportar**.  

2.  No Assistente para Exportação de Certificados, clique em **Próximo**.  

3.  Na página **Exportar chave privada** , selecione **Sim, exportar a chave privada**e clique em **Próximo**.  

    > [!NOTE]  
    >  Se essa opção não estiver disponível, o certificado foi criado sem a opção de exportar a chave privada. Nesse cenário, você não pode exportar o certificado no formato exigido. Você deve configurar o modelo de certificado para permitir que a chave privada seja exportada e, em seguida, solicitar o certificado novamente.  

4.  Na página **Formato do arquivo de exportação** , verifique se a opção **Troca de informações pessoais - PKCS nº 12 (.PFX)** esta selecionada.  

5.  Na página **Senha** , especifique uma senha forte para proteger o certificado exportado com sua chave privada e clique em **Próximo**.  

6.  Na página **Arquivo a ser exportado** , especifique o nome do arquivo que você deseja exportar e clique em **Próximo**.  

7.  Para fechar o assistente, clique em **Concluir** na página **Assistente para Exportação de Certificados** e clique em **OK** na caixa de diálogo de confirmação.  

8.  Feche os **Certificados (computador local)**.  

9. Armazene o arquivo com segurança e verifique se você pode acessá-lo do console do System Center Configuration Manager.  

 Agora o certificado está pronto para ser importado quando você configurar o ponto de distribuição.  

> [!TIP]  
>  Você pode usar o mesmo arquivo de certificado ao configurar imagens de mídia para uma implantação do sistema operacional que não usa inicialização PXE, e a sequência de tarefas para instalar a imagem deve contatar um ponto de gerenciamento que requer conexões de cliente HTTPS.  

##  <a name="a-namebkmkmobiledevices2008cm2012a-deploying-the-enrollment-certificate-for-mobile-devices"></a><a name="BKMK_mobiledevices2008_cm2012"></a> Implantando o certificado de registro para dispositivos móveis  
 Esta implantação do certificado tem um procedimento único para criar e emitir o modelo de certificado de registro na autoridade de certificação.  

### <a name="creating-and-issuing-the-enrollment-certificate-template-on-the-certification-authority"></a>Criando e emitindo o modelo de certificado de registro na autoridade de certificação  
 Esse procedimento cria um modelo de certificado de registro para dispositivos móveis do System Center Configuration Manager e o adiciona à Autoridade de Certificação.  

##### <a name="to-create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Para criar e emitir o modelo de certificado de registro na autoridade de certificação  

1.  Cria um grupo de segurança que contém usuários que registrarão dispositivos móveis no System Center Configuration Manager.  

2.  No servidor membro que tem os Serviços de Certificados instalados, no console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de certificado**e clique em **Gerenciar** para carregar o console de gerenciamento Modelos de certificado.  

3.  No painel de resultados, clique com o botão direito do mouse na entrada que exibe **Sessão Autenticada** na coluna **Nome de Exibição do Modelo**e clique em **Duplicar Modelo**.  

4.  Na caixa de diálogo **Duplicar Modelo** , verifique se a opção **Windows 2003 Server, Enterprise Edition** está marcada e clique em **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

5.  Na caixa de diálogo **Propriedades do novo modelo**, na guia **Geral**, insira um nome do modelo para gerar os certificados de registro para os dispositivos móveis a serem gerenciados pelo System Center Configuration Manager, como o **Certificado de registro do dispositivo móvel do ConfigMgr**.  

6.  Clique na guia **Nome da Entidade** , verifique se a opção **Criar com base nas informações do Active Directory** está marcada, selecione **Nome comum** para o **Formato de nome da entidade:** e desmarque **Nome UPN** de **Incluir estas informações no nome da entidade alternativo**.  

7.  Clique na guia **Segurança** , selecione o grupo de segurança que contém usuários que têm dispositivos móveis a serem registrados e selecione a permissão adicional **Registrar**. Não desmarque **Ler**.  

8.  Clique em **OK** e feche o **Console de Modelos de Certificado**.  

9. No console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado**, clique em **Novo**e em **Modelo de certificado a ser emitido**.  

10. Na caixa de diálogo **Ativar Modelos de Certificado** , selecione o novo modelo que você acabou de criar, **Certificado de registro do dispositivo móvel do ConfigMgr**e clique em **OK**.  

11. Se você não precisar criar ou emitir mais certificados, feche o console da Autoridade de Certificação.  

 Agora o modelo de certificado de registro de dispositivo móvel está pronto para ser selecionado quando você configurar um perfil de registro de dispositivo móvel nas configurações do cliente.  

##  <a name="a-namebkmkamt2008cm2012a-deploying-the-certificates-for-amt"></a><a name="BKMK_AMT2008_cm2012"></a> Implantando os certificados para AMT  
 Esta implantação de certificados abrange os seguintes procedimentos:  

-   Criar, emitir e instalar o certificado de provisionamento AMT  

-   Criar e emitir o certificado do servidor Web para computadores AMT  

-   Criar e emitir os certificados de autenticação de cliente para computadores AMT 802.1X  

###  <a name="a-namebkmkamtprovisioning2008a-creating-issuing-and-installing-the-amt-provisioning-certificate"></a><a name="BKMK_AMTprovisioning2008"></a> Creating, Issuing, and Installing the AMT Provisioning Certificate  
 Crie o certificado de provisionamento com sua CA interna quando computadores AMT são configurados com a impressão digital do certificado da autoridade de certificação raiz interna. Quando não for esse o caso e você precisar usar uma autoridade de certificação externa, use as instruções da empresa que emitiu o certificado de provisionamento AMT, o que, muitas vezes, envolverá solicitar o certificado do site público da empresa. Você também poderá encontrar instruções detalhadas para a autoridade de certificação externa escolhida sobre o Centro de Especialistas Intel vPro: site do Microsoft vPro Manageability ([http://go.microsoft.com/fwlink/?LinkId=132001](http://go.microsoft.com/fwlink/?LinkId=132001)).  

> [!IMPORTANT]  
>  CAs externas podem não oferecer suporte ao identificador de objeto de provisionamento do Intel AMT. Quando esse for o caso, use o método alternativo de fornecimento do atributo OU do **Certificado de instalação de cliente do Intel(R)**.  

 Quando você solicitar um certificado de provisionamento AMT de uma CA externa, instale o certificado no repositório de certificados do computador pessoal no servidor membro que hospedará o ponto de serviço fora de banda.  

##### <a name="to-request-and-issue-the-amt-provisioning-certificate"></a>Para solicitar e emitir o certificado de provisionamento AMT  

1.  Crie um grupo de segurança que contenha as contas de computador de servidores do sistema de site que executarão o ponto de serviço fora de banda.  

2.  No servidor membro com os Serviços de Certificados instalados, no console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado**e clique em **Gerenciar** para carregar o console **Modelos de Certificado** .  

3.  No painel de resultados, clique com o botão direito do mouse na entrada que exibe **Servidor Web** , na coluna **Nome de Exibição do Modelo** , e clique em **Duplicar Modelo**.  

4.  Na caixa de diálogo **Duplicar Modelo** , verifique se a opção **Windows 2003 Server, Enterprise Edition** está marcada e clique em **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

5.  Na caixa de diálogo **Propriedades do Novo Modelo** , na guia **Geral** , insira um nome de modelo para o certificado de provisionamento AMT, como **Provisionamento AMT do ConfigMgr**.  

6.  Na guia **Nome da Entidade** , selecione **Criar com base nas informações do Active Directory**e selecione **Nome comum**.  

7.  Clique na guia **Extensões** , verifique se **Políticas de Aplicativo** está selecionada e clique em **Editar**.  

8.  Na caixa de diálogo **Editar Extensão de Políticas de Aplicativo** , clique em **Adicionar**.  

9. Na caixa de diálogo **Adicionar Política de Aplicativo** , clique em **Novo**.  

10. Na caixa de diálogo **Nova Política de Aplicativo** , digite **Provisionamento AMT** no campo **Nome** e digite o seguinte número para o **Identificador de Objeto**: **2.16.840.1.113741.1.2.3**.  

11. Clique em **OK**e em **OK** na caixa de diálogo **Adicionar Política de Aplicativo** .  

12. Clique em **OK** na caixa de diálogo **Editar Extensão de Políticas de Aplicativo** .  

13. Na caixa de diálogo **Propriedades do Novo Modelo** , agora você deve ver o seguinte listado como descrição das **Políticas de Aplicativo** : **Autenticação de Servidor** e **Provisionamento AMT**.  

14. Clique na guia **Segurança** e remova a permissão **Registrar** dos grupos de segurança **Admins. do domínio** e **Admins. da empresa**.  

15. Clique em **Adicionar**, insira o nome de um grupo de segurança que contenha a conta de computador para a função do sistema de site do ponto de serviço fora de banda e clique em **OK**.  

16. Selecione a permissão **Registrar** para este grupo e não desmarque a permissão **Ler** .  

17. Clique em **OK**e feche o console de **Modelos de Certificado** .  

18. Em **Autoridade de Certificação**, clique com o botão direito do mouse em **Modelos de Certificado**, clique em **Novo**e em **Modelo de certificado a ser emitido**.  

19. Na caixa de diálogo **Ativar Modelos de Certificado** , selecione o novo modelo que você acabou de criar, **Provisionamento AMT do ConfigMgr**e clique em **OK**.  

    > [!NOTE]  
    >  Se você não conseguir concluir as etapas 18 ou 19, verifique se está usando o Enterprise Edition do Windows Server 2008. Embora você possa configurar modelos com o Windows Server Standard Edition e os Serviços de Certificados, não é possível implantar certificados usando modelos de certificado modificados, a menos que você esteja usando o Enterprise Edition do Windows Server 2008.  

20. Não feche **Autoridade de Certificação**.  

 O certificado de provisionamento AMT de sua CA interna agora está pronto para ser instalado no computador do ponto de serviço de banda.  

##### <a name="to-install-the-amt-provisioning-certificate"></a>Para instalar o certificado de provisionamento AMT  

1.  Reinicie o servidor membro que executa o IIS para confirmar que ele pode acessar o modelo de certificado com a permissão configurada.  

2.  Clique em **Iniciar**, clique em **Executar**e digite **mmc.exe.** No console vazio, clique em **Arquivo**e clique em **Adicionar/Remover Snap-in**.  

3.  Na caixa de diálogo **Adicionar ou Remover Snap-ins** , selecione **Certificados** na lista de **Snap-ins disponíveis**e clique em **Adicionar**.  

4.  Na caixa de diálogo **Snap-in de certificado** , selecione **Conta de computador**e clique em **Próximo**.  

5.  Na caixa de diálogo **Selecionar Computador** , verifique se a opção **Computador Local: (o computador no qual este console está sendo executado)** está marcada e clique em **Concluir**.  

6.  Na caixa de diálogo **Adicionar ou Remover Snap-ins** , clique em **OK**.  

7.  No console, expanda **Certificados (computador local)**e clique em **Pessoal**.  

8.  Clique com o botão direito do mouse em **Certificados**, clique em **Todas as Tarefas**e em **Solicitar Novo Certificado**.  

9. Na página **Antes de Começar** , clique em **Avançar**.  

10. Se você vir a página **Selecionar política de registro de certificado** , clique em **Próximo**.  

11. Na página **Solicitar certificados** , selecione **Provisionamento AMT do ConfigMgr** na lista de certificados exibida e clique em **Registrar**.  

12. Na página **Resultados da instalação de certificados** , espere até que o certificado seja instalado e clique em **Concluir**.  

13. Feche os **Certificados (computador local)**.  

 O certificado de provisionamento AMT de sua CA interna agora está instalado e pronto para ser selecionado nas propriedades do ponto de serviço fora de banda.  

### <a name="creating-and-issuing-the-web-server-certificate-for-amt-based-computers"></a>Criar e emitir o certificado do servidor Web para computadores AMT  
 Use o procedimento a seguir para preparar os certificados do servidor Web para computadores AMT.  

##### <a name="to-create-and-issue-the-web-server-certificate-template"></a>Para criar e emitir modelo de certificado do servidor Web  

1.  Crie um grupo de segurança vazio para conter as contas de computador do AMT que o System Center Configuration Manager cria durante o provisionamento de AMT.  

2.  No servidor membro com os Serviços de Certificados instalados, no console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado**e clique em **Gerenciar** para carregar o console **Modelos de Certificado** .  

3.  No painel de resultados, clique com o botão direito do mouse na entrada que exibe **Servidor Web** na coluna **Nome de Exibição do Modelo**e clique em **Duplicar Modelo**.  

4.  Na caixa de diálogo **Duplicar Modelo** , verifique se a opção **Windows 2003 Server, Enterprise Edition** está marcada e clique em **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**  

5.  Na caixa de diálogo **Propriedades do Novo Modelo** , na guia **Geral** , insira um nome de modelo para gerar os certificados Web que serão usados para gerenciamento fora de banda em computadores AMT, como **Certificado do servidor Web AMT do ConfigMgr**.  

6.  Clique na guia **Nome da Entidade** , clique em **Criar com base nas informações do Active Directory**, selecione **Nome comum** para o **Formato de nome de entidade**e desmarque **Nome UPN** para o nome alternativo da entidade.  

7.  Clique na guia **Segurança** e remova a permissão **Registrar** dos grupos de segurança **Admins. do domínio** e **Admins. da empresa**.  

8.  Clique em **Adicionar** e insira o nome do grupo de segurança que você criou para provisionamento AMT. Clique em **OK**.  

9. Selecione as seguintes permissões **Permitir** para esse grupo de segurança: **Ler** e **Registrar**.  

10. Clique em **OK**e feche o console de **Modelos de Certificado** .  

11. No console de **Autoridade de Certificação** , clique com o botão direito do mouse em **Modelos de Certificado**, clique em **Novo**e em **Modelo de certificado a ser emitido**.  

12. Na caixa de diálogo **Ativar Modelos de Certificado** , selecione o novo modelo que você acabou de criar, **Certificado do servidor Web AMT do ConfigMgr**, e clique em **OK**.  

13. Se você não precisar criar ou emitir mais certificados, feche a **Autoridade de Certificação**.  

 Agora o modelo de servidor Web MT está pronto para provisionar computadores AMT com certificados do servidor Web. Selecione esse modelo de certificado nas propriedades do componente de gerenciamento fora de banda.  

### <a name="creating-and-issuing-the-client-authentication-certificates-for-8021x-amt-based-computers"></a>Criar e emitir os certificados de autenticação de cliente para computadores AMT 802.1X  
 Use o procedimento a seguir se computadores AMT forem usar certificados do cliente para redes com ou sem fio 802.1X autenticadas.  

##### <a name="to-create-and-issue-the-client-authentication-certificate-template-on-the-ca"></a>Para criar e emitir o modelo de certificado de autenticação do cliente na autoridade de certificação  

1.  No servidor membro com os Serviços de Certificados instalados, no console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado**e clique em **Gerenciar** para carregar o console **Modelos de Certificado** .  

2.  No painel de resultados, clique com o botão direito do mouse na entrada que exibe **Autenticação de estação de trabalho** na coluna **Nome de Exibição do Modelo**e clique em **Duplicar Modelo**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**  

3.  Na caixa de diálogo **Propriedades do Novo Modelo** , na guia **Geral** , insira um nome de modelo para gerar os certificados do cliente que serão usados para gerenciamento fora de banda em computadores AMT, como **Certificado de autenticação do cliente do AMT 802.1X do ConfigMgr**.  

4.  Clique na guia **Nome da Entidade** , clique em **Criar com base nas informações do Active Directory** e selecione **Nome comum** para o **Formato de nome de entidade**. Desmarque **Nome DNS** para o nome alternativo da entidade e selecione **Nome UPN**.  

5.  Clique na guia **Segurança** e remova a permissão **Registrar** dos grupos de segurança **Admins. do domínio** e **Admins. da empresa**.  

6.  Clique em **Adicionar** e insira o nome do grupo de segurança que você especificará nas propriedades do componente de gerenciamento fora de banda, para conter as contas de computador dos computadores AMT. Clique em **OK**.  

7.  Selecione as seguintes permissões **Permitir** para esse grupo de segurança: **Ler** e **Registrar**.  

8.  Clique em **OK**e feche o console de gerenciamento de **Modelos de Certificado**, **certtmpl – [Modelos de Certificado]**.  

9. No console de gerenciamento de **Autoridade de Certificação** , clique com o botão direito do mouse em **Modelos de Certificado**, clique em **Novo**e em **Modelo de Certificado a Ser Emitido**.  

10. Na caixa de diálogo **Ativar Modelos de Certificado** , selecione o novo modelo que você acabou de criar, **Certificado de Autenticação do Cliente AMT 802.1X do ConfigMgr**, e clique em **OK**.  

11. Se você não precisar criar ou emitir mais certificados, feche a **Autoridade de Certificação**.  

 Agora o modelo de certificado de autenticação do cliente está pronto para emitir certificados para computadores AMT que podem ser usados para autenticação do cliente do 802.1X. Selecione esse modelo de certificado nas propriedades do componente de gerenciamento fora de banda.  

##  <a name="a-namebkmkmacclientsp1a-deploying-the-client-certificate-for-mac-computers"></a><a name="BKMK_MacClient_SP1"></a> Implantando o certificado do cliente para computadores Mac  

> [!NOTE]  
>  O certificado do cliente para computadores Mac se aplica apenas ao System Center Configuration Manager SP1 e posterior.  

 Esta implantação do certificado tem um procedimento único para criar e emitir o modelo de certificado de registro na autoridade de certificação.  

###  <a name="a-namebkmkmacclientcreatingissuinga-creating-and-issuing-a-mac-client-certificate-template-on-the-certification-authority"></a><a name="BKMK_MacClient_CreatingIssuing"></a> Criando e emitindo de um modelo de certificado do cliente Mac na autoridade de certificação  
 Este procedimento cria um modelo de certificado personalizado para computadores Mac do System Center Configuration Manager e o adiciona à autoridade de certificação.  

> [!NOTE]  
>  Este procedimento usa um modelo de certificado diferente do modelo que você pode ter criado para computadores cliente Windows ou para pontos de distribuição.  
>   
>  Com a criação de um novo modelo de certificado para esse certificado, você pode restringir a solicitação do certificado a usuários autorizados.  

##### <a name="to-create-and-issue-the-mac-client-certificate-template-on-the-certification-authority"></a>Para criar e emitir o modelo de certificado do cliente Mac na autoridade de certificação  

1.  Crie um grupo de segurança que contenha as contas de usuário para usuários administrativos que registrarão o certificado no computador Mac usando o System Center Configuration Manager.  

2.  No servidor membro que executa o console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado**e clique em **Gerenciar** para carregar o console de gerenciamento Modelos de Certificado.  

3.  No painel de resultados, clique com o botão direito do mouse na entrada que exibe **Sessão Autenticada** na coluna **Nome de Exibição do Modelo**e clique em **Duplicar Modelo**.  

4.  Na caixa de diálogo **Duplicar Modelo** , verifique se a opção **Windows 2003 Server, Enterprise Edition** está marcada e clique em **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

5.  Na caixa de diálogo **Propriedades do Novo Modelo** , na guia **Geral** , insira um nome de modelo para gerar o certificado do cliente Mac, como **Certificado do cliente Mac do ConfigMgr**.  

6.  Clique na guia **Nome da Entidade** , verifique se a opção **Criar com base nas informações do Active Directory** está marcada, selecione **Nome comum** para o **Formato de nome da entidade:** e desmarque **Nome UPN** de **Incluir estas informações no nome da entidade alternativo**.  

7.  Clique na guia **Segurança** e remova a permissão **Registrar** dos grupos de segurança **Admins. do domínio** e **Admins. da empresa** .  

8.  Clique em **Adicionar**, especifique o grupo de segurança que você criou na etapa um e clique em **OK**.  

9. Selecione a permissão **Registrar** para este grupo e não desmarque a permissão **Ler** .  

10. Clique em **OK** e feche o **Console de Modelos de Certificado**.  

11. No console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado**, clique em **Novo**e em **Modelo de certificado a ser emitido**.  

12. Na caixa de diálogo **Ativar Modelos de Certificado** , selecione o novo modelo que você acabou de criar, **Certificado do cliente Mac do ConfigMgr**e clique em **OK**.  

13. Se você não precisar criar ou emitir mais certificados, feche a **Autoridade de Certificação**.  

 Agora o modelo de certificado do cliente Mac está pronto para ser selecionado quando você definir as configurações do cliente para registro.



<!--HONumber=Nov16_HO1-->


