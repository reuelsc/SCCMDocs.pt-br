---
title: "Certificados PKI de implantação"
titleSuffix: Configuration Manager
description: Siga um exemplo passo a passo para conhecer como criar e implantar certificados PKI que o System Center Configuration Manager usa.
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3417ff88-7177-4a0d-8967-ab21fe7eba17
caps.latest.revision: "11"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 092e3e752a27ab652f2b38c0ba43e6e2e26c99c8
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="step-by-step-example-deployment-of-the-pki-certificates-for-system-center-configuration-manager-windows-server-2008-certification-authority"></a>Exemplo de implantação passo a passo dos certificados PKI para o System Center Configuration Manager: autoridade de certificação do Windows Server 2008

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este exemplo de implantação passo a passo, que usa uma AC (autoridade de certificação) do Windows Server 2008, contém procedimentos que mostram como criar e implantar os certificados PKI (infraestrutura de chave pública) usados pelo System Center Configuration Manager. Esses procedimentos usam uma Autoridade de Certificação (CA) corporativa e modelos de certificado. As etapas são apropriadas para uma rede de teste somente, como uma verificação de conceito.  

 Como não existe um método único de implantação dos certificados necessários, consulte a documentação de implantação de PKI sobre os procedimentos necessários e as práticas recomendadas para implantar os certificados necessários em um ambiente de produção. Para obter mais informações sobre os requisitos de certificado, consulte [Requisitos de certificado PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

> [!TIP]  
>  Você pode adaptar as instruções neste tópico para sistemas operacionais que não estão documentados na seção Requisitos de rede de teste. No entanto, se você estiver executando a AC emissora no Windows Server 2012, a versão do modelo de certificado não será solicitada. Em vez disso, especifique isso na guia **Compatibilidade** das propriedades do modelo:  
>   
>  -   **Autoridade de Certificação**: **Windows Server 2003**  
> -   **Destinatário do certificado**: **Windows XP / Server 2003**  

## <a name="in-this-section"></a>Nesta seção  
 As seções a seguir incluem instruções em um exemplo passo a passo de criação e implantação dos seguintes certificados que podem ser usados ​​com o System Center Configuration Manager:  

 [Requisitos de rede de teste](#BKMK_testnetworkenvironment)  

 [Visão geral dos certificados](#BKMK_overview2008)  

 [Implantar o certificado do servidor Web para sistemas de sites que executam o IIS](#BKMK_webserver2008_cm2012)  

 [Implantar o certificado de serviço para pontos de distribuição baseados em nuvem](#BKMK_clouddp2008_cm2012)  

 [Implantar o certificado do cliente para computadores Windows](#BKMK_client2008_cm2012)  

 [Implantar o certificado do cliente para pontos de distribuição](#BKMK_clientdistributionpoint2008_cm2012)  

 [Implantar o certificado de registro para dispositivos móveis](#BKMK_mobiledevices2008_cm2012)  

 [Implantar os certificados para AMT](#BKMK_AMT2008_cm2012)  

 [Implantar o certificado do cliente para computadores Mac](#BKMK_MacClient_SP1)  

##  <a name="BKMK_testnetworkenvironment"></a> Requisitos de rede de teste  
 As instruções passo a passo têm os seguintes requisitos:  

-   A rede de teste está executando Serviços de Domínio do Active Directory no Windows Server 2008, e está instalada como um único domínio, uma única floresta.  

-   Existe um servidor membro executando o Windows Server 2008 Enterprise Edition, que tem a função de Serviços de Certificados do Active Directory instalado nele e é configurado como uma AC (Autoridade de Certificação) raiz corporativa.  

-   Você tem um computador com o Windows Server 2008 (Standard Edition ou Enterprise Edition, R2 ou posterior) instalado, esse computador é designado como um servidor membro e o IIS (Serviços de Informações da Internet) está instalados nele. Esse computador será o servidor do sistema de sites do System Center Configuration Manager que você configurará com um FQDN (nome de domínio totalmente qualificado) de intranet para dar suporte a conexões do cliente na intranet e um FQDN de Internet, se precisar dar suporte a dispositivos móveis registrados pelo System Center Configuration Manager e clientes na Internet.  

-   Você tem um cliente do Windows Vista com o service pack mais recente instalado e este computador está configurado com um nome do computador que compreende caracteres ASCII e está associado ao domínio. O computador será um computador de cliente do System Center Configuration Manager.  

-   Você pode entrar com uma conta de administrador de domínio raiz ou uma conta de administrador de domínio corporativo e use essa conta para todos os procedimentos desta implantação de exemplo.  

##  <a name="BKMK_overview2008"></a> Visão geral dos certificados  
 A tabela a seguir lista os tipos de certificados PKI que podem ser necessários para o System Center Configuration Manager e descreve como eles são usados.  

|Requisitos do certificado|Descrição do certificado|  
|-----------------------------|-----------------------------|  
|Certificado do servidor Web para sistemas de sites que executam IIS|Use este certificado para criptografar dados e autenticar o servidor para os clientes. Ele deve ser instalado externamente do System Center Configuration Manager em servidores de sistemas de sites que executam o IIS (Serviços de Informações da Internet) e que estão configurados no System Center Configuration Manager para usar HTTPS.<br /><br /> Para obter as etapas para configurar e instalar este certificado, veja [Implantar o certificado do servidor Web para sistemas de sites que executam o IIS](#BKMK_webserver2008_cm2012) neste tópico.|  
|Certificado de serviço para os clientes se conectarem a pontos de distribuição baseados em nuvem|Para obter as etapas para configurar e instalar este certificado, consulte [Implantar o certificado de serviço para pontos de distribuição baseados em nuvem](#BKMK_clouddp2008_cm2012) neste tópico.<br /><br /> **Importante:** esse certificado é usado em conjunto com o certificado de gerenciamento do Microsoft Azure. Para obter mais informações sobre o certificado de gerenciamento, consulte [How to Create a Management Certificate](http://go.microsoft.com/fwlink/p/?LinkId=220281) (Como criar um certificado de gerenciamento) e [How to Add a Management Certificate to a Windows Azure Subscription](http://go.microsoft.com/fwlink/?LinkId=241722) (Como adicionar um certificado de gerenciamento a uma assinatura do Microsoft Azure) na seção Plataforma Microsoft Azure da Biblioteca MSDN.|  
|Certificado do cliente para computadores com Windows|Este certificado é usado para autenticar computadores cliente do System Center Configuration Manager em sistemas de sites que estão configurados para usar HTTPS. Ele também pode ser usado para pontos de gerenciamento e pontos de migração para monitoramento do status operacional quando estiverem configurados para usar HTTPS. Ele deve ser instalado externamente ao System Center Configuration Manager nos computadores.<br /><br /> Para obter as etapas para configurar e instalar este certificado, veja [Implantar o certificado do cliente para computadores Windows](#BKMK_client2008_cm2012) neste tópico.|  
|Certificado do cliente para pontos de distribuição|Este certificado tem duas finalidades:<br /><br /> Use este certificado para autenticar o ponto de distribuição para um ponto de gerenciamento habilitado para HTTPS antes que o ponto de distribuição envie mensagens de status.<br /><br /> Quando a opção do ponto de distribuição **Habilitar suporte a PXE para clientes** é selecionada, o certificado é enviado para computadores que o PXE inicializa para que eles possam se conectar a um ponto de gerenciamento habilitado para HTTPS durante a implantação do sistema operacional.<br /><br /> Para obter as etapas para configurar e instalar este certificado, veja [Implantar o certificado do cliente para pontos de distribuição](#BKMK_clientdistributionpoint2008_cm2012) neste tópico.|  
|Certificado de registro para dispositivos móveis|Este certificado é usado para autenticar clientes de dispositivos móveis do System Center Configuration Manager em sistemas de sites que estão configurados para usar HTTPS. Ele deve ser instalado como parte do registro do dispositivo móvel no System Center Configuration Manager e você escolhe o modelo do certificado definido como uma configuração do cliente do dispositivo móvel.<br /><br /> Para obter as etapas para configurar este certificado, veja [Implantar o certificado de registro para dispositivos móveis](#BKMK_mobiledevices2008_cm2012) neste tópico.|  
|Certificados para Intel AMT|Há três certificados relacionados ao gerenciamento fora de banda para computadores Intel AMT:<ul><li>Um certificado de provisionamento AMT (Active Management Technology)</li><li>Um certificado do servidor Web AMT</li><li>Opcionalmente, um certificado de autenticação de cliente para redes com ou sem fio 802.1X</li></ul>O certificado de provisionamento AMT deve ser instalado externamente ao System Center Configuration Manager no computador do ponto de serviço fora de banda e depois você escolhe o certificado instalado nas propriedades do ponto de serviço fora de banda. O certificado do servidor Web AMT e o certificado de autenticação de cliente são instalados durante provisionamento e gerenciamento de AMT e você escolhe os modelos de certificado configurados nas propriedades dos componentes de gerenciamento fora de banda.<br /><br /> Para obter as etapas para configurar esses certificados, confira [Implantar os certificados para AMT](#BKMK_AMT2008_cm2012) neste tópico.|  
|Certificado do cliente para computadores Mac|Você pode solicitar e instalar esse certificado em um computador Mac quando usar o registro do System Center Configuration Manager e escolher o modelo de certificado configurado como uma configuração do cliente do dispositivo móvel.<br /><br /> Para obter as etapas para configurar este certificado, veja [Implantar o certificado do cliente para computadores Mac](#BKMK_MacClient_SP1) neste tópico.|  

##  <a name="BKMK_webserver2008_cm2012"></a> Implantar o certificado do servidor Web para sistemas de sites que executam o IIS  
 Esta implantação de certificados abrange os seguintes procedimentos:  

-   Criar e emitir o modelo de certificado do servidor Web na autoridade de certificação  

-   Solicitar o certificado do servidor Web  

-   Configurar o IIS para usar o certificado do servidor Web  

###  <a name="BKMK_webserver22008"></a> Criar e emitir o modelo de certificado do servidor Web na autoridade de certificação  
 Esse procedimento cria um modelo de certificado para sistemas de sites do System Center Configuration Manager e o adiciona à Autoridade de Certificação.  

##### <a name="to-create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a>Criar e emitir o modelo de certificado do servidor Web na Autoridade de Certificação  

1.  Crie um grupo de segurança chamado **Servidores IIS ConfigMgr** que contenha os servidores membros para instalar os sistemas de sites do System Center Configuration Manager que executarão o IIS.  

2.  No servidor membro com os Serviços de Certificados instalados, no console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado** e escolha **Gerenciar** para carregar o console **Modelos de Certificado**.  

3.  No painel de resultados, clique com o botão direito do mouse na entrada que tem **Servidor Web** na coluna **Nome de Exibição do Modelo** e escolha **Duplicar Modelo**.  

4.  Na caixa de diálogo **Duplicar Modelo**, verifique se a opção **Windows 2003 Server, Enterprise Edition** está marcada e escolha **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

5.  Na caixa de diálogo **Propriedades do Novo Modelo**, na guia **Geral**, insira um nome de modelo, como **Certificado do Servidor Web do ConfigMgr** para gerar os certificados Web que serão usados nos sistemas de sites do Configuration Manager.  

6.  Escolha a guia **Nome da Entidade** e verifique se **Fornecer na solicitação** está selecionado.  

7.  Escolha a guia **Segurança** e remova a permissão **Registrar** dos grupos de segurança **Admins. do Domínio** e **Administradores de Empresa**.  

8.  Escolha **Adicionar**, insira **Servidores IIS do ConfigMgr** na caixa de texto e escolha **OK**.  

9. Escolha a permissão **Registrar** para este grupo e não desmarque a permissão **Ler**.  

10. Escolha **OK** e feche o **Console de Modelos de Certificado**.  

11. No console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado**, escolha **Novo** e **Modelo de Certificado a Ser Emitido**.  

12. Na caixa de diálogo **Habilitar Modelos de Certificado**, escolha o novo modelo que você acabou de criar, **Certificado do Servidor Web do ConfigMgr** e escolha **OK**.  

13. Se você não precisar criar ou emitir mais certificados, feche a **Autoridade de Certificação**.  

###  <a name="BKMK_webserver32008"></a> Solicitar o certificado do servidor Web  
 Este procedimento permite que você especifique valores FQDN de intranet e Internet que serão configurados nas propriedades do servidor de sistema de sites e instale o certificado do servidor Web no servidor membro que executa o IIS.  

##### <a name="to-request-the-web-server-certificate"></a>Para solicitar o certificado do servidor Web  

1.  Reinicie o servidor membro que executa o IIS para garantir que o computador possa acessar o modelo de certificado que você criou usando as permissões **Ler** e **Registrar** configuradas por você.  

2.  Escolha **Iniciar**, **Executar** e, em seguida, digite **mmc.exe.** No console vazio, escolha **Arquivo** e **Adicionar/Remover Snap-in**.  

3.  Na caixa de diálogo **Adicionar ou Remover Snap-ins**, escolha **Certificados** na lista de **Snap-ins disponíveis** e escolha **Adicionar**.  

4.  Na caixa de diálogo **Snap-in de certificado**, escolha **Conta de computador** e escolha **Avançar**.  

5.  Na caixa de diálogo **Selecionar Computador**, verifique se a opção **Computador local: (o computador no qual este console está sendo executado)** está marcada e escolha **Concluir**.  

6.  Na caixa de diálogo **Adicionar ou Remover Snap-ins**, escolha **OK**.  

7.  No console, expanda **Certificados (Computador Local)** e escolha **Pessoal**.  

8.  Clique com o botão direito do mouse em **Certificados**, escolha **Todas as Tarefas** e **Solicitar Novo Certificado**.  

9. Na página **Antes de Começar** escolha **Avançar**.  

10. Se você vir a página **Selecionar Política de Registro de Certificado**, escolha **Avançar**.  

11. Na página **Solicitar Certificados**, identifique o **Certificado do Servidor Web do ConfigMgr** na lista de certificados disponíveis e escolha **Mais informações são necessárias para se registrar neste certificado. Clique aqui para definir as configurações**.  

12. Na caixa de diálogo **Propriedades do Certificado**, na guia **Entidade**, não faça nenhuma alteração no **Nome da entidade**. Isso significa que a caixa **Valor** para o **Nome da entidade** permanece em branco. Em vez disso, na seção **Nome alternativo**, escolha a lista suspensa **Tipo** e escolha **DNS**.  

13. Na caixa **Valor**, especifique os valores de FQDN que serão especificados nas propriedades do sistema de sites do System Center Configuration Manager e escolha **OK** para fechar a caixa de diálogo **Propriedades do Certificado**.  

     Exemplos:  

    -   Se o sistema de sites aceitar apenas conexões de clientes da intranet e o FQDN de intranet do servidor do sistema de sites for **server1.internal.contoso.com**, digite **server1.internal.contoso.com** e escolha **Adicionar**.  

    -   Se o sistema de sites aceitar conexões de clientes da intranet e da Internet, o FQDN de intranet do servidor do sistema de sites for **server1.internal.contoso.com** e o FQDN de Internet do servidor do sistema de sites for **server.contoso.com**:  

        1.  Digite **server1.internal.contoso.com** e escolha **Adicionar**.  

        2.  Digite **server.contoso.com** e escolha **Adicionar**.  

        > [!NOTE]  
        >  Você pode especificar os FQDNs para o System Center Configuration Manager em qualquer ordem. No entanto, verifique se todos os dispositivos que usarão o certificado, tais como dispositivos móveis e servidores Web proxy, podem usar um SAN (nome alternativo da entidade) de certificado e vários valores no SAN. Se os dispositivos tiverem suporte limitado para valores de SAN em certificados, altere a ordem dos FQDNs ou use o valor Entidade.  

14. Na página **Solicitar Certificados**, escolha **Certificado do Servidor Web do ConfigMgr** na lista de certificados disponíveis e escolha **Registrar**.  

15. Na página **Resultados da Instalação de Certificados** espere até que o certificado seja instalado e escolha **Concluir**.  

16. Feche os **Certificados (computador local)**.  

###  <a name="BKMK_webserver42008"></a> Configurar o IIS para usar o certificado do servidor Web  
 Este procedimento associa o certificado instalado ao **Site Padrão**do IIS.  

##### <a name="to-set-up-iis-to-use-the-web-server-certificate"></a>Configurar o IIS para usar o certificado do servidor Web  

1.  No servidor membro que tem o IIS instalado, escolha **Iniciar**, **Programas**, **Ferramentas Administrativas** e **Gerenciador do IIS (Serviços de Informações da Internet)**.  

2.  Expanda **Sites**, clique com o botão direito do mouse em **Site Padrão** e escolha **Editar Ligações**.  

3.  Escolha a entrada **https** e escolha **Editar**.  

4.  Na caixa de diálogo **Editar Associação do Site**, selecione o certificado que você solicitou usando o modelo de Certificados do Servidor Web ConfigMgr e escolha **OK**.  

    > [!NOTE]  
    >  Se não tiver certeza de qual é o certificado correto, escolha um e escolha **Exibir**. Isso permite comparar os detalhes do certificado selecionado com os certificados no snap-in de certificados. Por exemplo, o snap-in de certificados mostra o modelo de certificado que foi usado para solicitar o certificado. Em seguida, você pode comparar a impressão digital do certificado solicitado usando o modelo de Certificados do Servidor Web ConfigMgr à impressão digital do certificado selecionado atualmente na caixa de diálogo **Editar Associação do Site**.  

5.  Escolha **OK** na caixa de diálogo **Editar Associação do Site** e escolha **Fechar**.  

6.  Feche o **Gerenciador do IIS (Serviços de Informações da Internet)**.  

 Agora o servidor membro está configurado com um certificado do servidor Web do System Center Configuration Manager.  

> [!IMPORTANT]  
>  Ao instalar o servidor do sistema de sites do System Center Configuration Manager neste computador, verifique se você especificou os mesmos FQDNs nas propriedades do sistema de sites que especificou ao solicitar o certificado.  

##  <a name="BKMK_clouddp2008_cm2012"></a> Implantar o certificado de serviço para pontos de distribuição baseados em nuvem  

Esta implantação de certificados abrange os seguintes procedimentos:  

-   [Criar e emitir o modelo de certificado personalizado do servidor Web na autoridade de certificação](#BKMK_clouddpcreating2008)  

-   [Solicitar o certificado personalizado do servidor Web](#BKMK_clouddprequesting2008)  

-   [Exportar o certificado personalizado do servidor Web para pontos de distribuição baseados em nuvem](#BKMK_clouddpexporting2008)  

###  <a name="BKMK_clouddpcreating2008"></a> Criar e emitir o modelo de certificado personalizado do servidor Web na autoridade de certificação  
 Este procedimento cria um modelo de certificado personalizado com base no modelo de certificado do servidor Web. O certificado é para os pontos de distribuição baseados em nuvem do System Center Configuration Manager e a chave privada deve ser exportável. Depois que o modelo de certificado é criado, ele é adicionado à autoridade de certificação.  

> [!NOTE]  
>  Este procedimento usa um modelo de certificado diferente do modelo de certificado do servidor Web que você criou para sistemas de sites que executam o IIS. Embora ambos os certificados requeiram a funcionalidade de autenticação de servidor, o certificado para pontos de distribuição baseado em nuvem requer que você insira um valor personalizado para o Nome da Entidade e a chave privada deve ser exportada. Como prática recomendada de segurança, não configure modelos de certificado para permitir que a chave privada seja exportada a menos que essa configuração seja necessária. O ponto de distribuição baseado em nuvem requer essa configuração, pois você deve importar o certificado como um arquivo, em vez de escolhe-lo no repositório de certificados.  
>   
>  Ao criar um novo modelo de certificado para esse certificado, você pode restringir os computadores que podem solicitar um certificado cuja chave privada pode ser exportada. Em uma rede de produção, você também pode adicionar as seguintes alterações a esse certificado:  
>   
>  -   Requerer aprovação para instalar o certificado, para obter segurança adicional.  
> -   Aumentar o período de validade do certificado. Como você precisa exportar e importar o certificado todas as vezes antes de ele expirar, um aumento no período de validade reduz a frequência de repetição desse procedimento. No entanto, um aumento no período de validade também diminui a segurança do certificado, pois ele fornece mais tempo para que um invasor descriptografe a chave privada e roube o certificado.  
> -   Usar um valor personalizado no SAN (Nome Alternativo da Entidade) do certificado para ajudar a identificá-lo dos certificados do servidor Web padrão que você usa com o IIS.  

##### <a name="to-create-and-issue-the-custom-web-server-certificate-template-on-the-certification-authority"></a>Para criar e emitir o modelo de certificado personalizado do servidor Web na autoridade de certificação  

1.  Crie um grupo de segurança chamado **Servidores de Site do ConfigMgr** que contenha os servidores membros para instalar os servidores do site primário do System Center Configuration Manager que gerenciará os pontos de distribuição baseados em nuvem.  

2.  No servidor membro que executa o console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado** e escolha **Gerenciar** para carregar o console de gerenciamento Modelos de Certificado.  

3.  No painel de resultados, clique com o botão direito do mouse na entrada que tem **Servidor Web** na coluna **Nome de Exibição do Modelo** e escolha **Duplicar Modelo**.  

4.  Na caixa de diálogo **Duplicar Modelo**, verifique se a opção **Windows 2003 Server, Enterprise Edition** está marcada e escolha **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

5.  Na caixa de diálogo **Propriedades do Novo Modelo**, na guia **Geral**, insira um nome de modelo, como **Certificado do Ponto de Distribuição Baseado em Nuvem do ConfigMgr**, para gerar os certificados do servidor Web para pontos de distribuição baseados em nuvem.  

6.  Escolha a guia **Tratamento de Solicitação** e escolha **Permitir que a chave privada seja exportada**.  

7.  Escolha a guia **Segurança** e remova a permissão **Registrar** do grupo de segurança **Administradores de Empresa**.  

8.  Escolha **Adicionar**, insira **Servidores do Site do ConfigMgr** na caixa de texto e escolha **OK**.  

9. Selecione a permissão **Registrar** para este grupo e não desmarque a permissão **Ler** .  

10. Escolha **OK** e feche o **Console de Modelos de Certificado**.  

11. No console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado**, escolha **Novo** e **Modelo de Certificado a Ser Emitido**.  

12. Na caixa de diálogo **Habilitar Modelos de Certificado**, escolha o novo modelo que você acabou de criar, **Certificado do Ponto de Distribuição Baseado em Nuvem do ConfigMgr** e escolha **OK**.  

13. Se você não precisar criar ou emitir mais certificados, feche a **Autoridade de Certificação**.  

###  <a name="BKMK_clouddprequesting2008"></a> Solicitar o certificado personalizado do servidor Web  
 Este procedimento solicita e instala o certificado personalizado do servidor Web no servidor membro que executará o servidor do site.  

##### <a name="to-request-the-custom-web-server-certificate"></a>Para solicitar o certificado personalizado do servidor Web  

1.  Reinicie o servidor membro depois de criar e configurar o grupo de segurança **Servidores do Site do ConfigMgr** para assegurar que o computador possa acessar o modelo de certificado criado usando as permissões **Ler** e **Registrar** que você configurou.  

2.  Escolha **Iniciar**, **Executar** e, em seguida, digite **mmc.exe.** No console vazio, escolha **Arquivo** e **Adicionar/Remover Snap-in**.  

3.  Na caixa de diálogo **Adicionar ou Remover Snap-ins**, escolha **Certificados** na lista de **Snap-ins disponíveis** e escolha **Adicionar**.  

4.  Na caixa de diálogo **Snap-in de certificado**, escolha **Conta de computador** e escolha **Avançar**.  

5.  Na caixa de diálogo **Selecionar Computador**, verifique se a opção **Computador local: (o computador no qual este console está sendo executado)** está marcada e escolha **Concluir**.  

6.  Na caixa de diálogo **Adicionar ou Remover Snap-ins**, escolha **OK**.  

7.  No console, expanda **Certificados (Computador Local)** e escolha **Pessoal**.  

8.  Clique com o botão direito do mouse em **Certificados**, escolha **Todas as Tarefas** e **Solicitar Novo Certificado**.  

9. Na página **Antes de Começar** escolha **Avançar**.  

10. Se você vir a página **Selecionar Política de Registro de Certificado**, escolha **Avançar**.  

11. Na página **Solicitar Certificados**, identifique o **Certificado do Ponto de Distribuição Baseado em Nuvem do ConfigMgr** na lista de certificados disponíveis e escolha **Mais informações são necessárias para se registrar neste certificado. Escolha aqui para definir as configurações**.  

12. Na caixa de diálogo **Propriedades do Certificado**, na guia **Entidade** do **Nome da entidade**, escolha **Nome comum** como **Tipo**.  

13. Na caixa **Valor** , especifique a escolha do nome do serviço e do nome de domínio usando um formato FQDN. Por exemplo: **clouddp1.contoso.com**.  

    > [!NOTE]  
    >  Torne o nome de serviço único em seu namespace. Você usará o DNS para criar um alias (registro CNAME) para mapear este nome do serviço para um GUID (identificador) gerado automaticamente e um endereço IP do Windows Azure.  

14. Escolha **Adicionar** e escolha **OK** para fechar a caixa de diálogo **Propriedades do Certificado**.  

15. Na página **Solicitar Certificados**, escolha **Certificado do Ponto de Distribuição Baseado em Nuvem do ConfigMgr** na lista de certificados disponíveis e escolha **Registrar**.  

16. Na página **Resultados da Instalação de Certificados** espere até que o certificado seja instalado e escolha **Concluir**.  

17. Feche os **Certificados (computador local)**.  

###  <a name="BKMK_clouddpexporting2008"></a> Exportar o certificado personalizado do servidor Web para pontos de distribuição baseados em nuvem  
 Este procedimento exporta o certificado personalizado do servidor Web para um arquivo, assim ele pode ser importando quando você criar o ponto de distribuição baseado em nuvem.  

##### <a name="to-export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a>Para exportar o certificado personalizado do servidor Web para pontos de distribuição baseados em nuvem  

1.  No console **Certificados (Computador Local)**, clique com o botão direito do mouse no certificado que você acabou de instalar, escolha **Todas as Tarefas** e escolha **Exportar**.  

2.  No Assistente para Exportação de Certificados, escolha **Avançar**.  

3.  Na página **Exportar Chave Privada**, escolha **Sim, exportar a chave privada** e escolha **Avançar**.  

    > [!NOTE]  
    >  Se essa opção não estiver disponível, o certificado foi criado sem a opção de exportar a chave privada. Nesse cenário, você não pode exportar o certificado no formato exigido. Você deve configurar o modelo de certificado para que a chave privada possa ser exportada e, em seguida, solicitar o certificado novamente.  

4.  Na página **Formato do Arquivo de Exportação**, verifique se a opção **Troca de Informações Pessoais – PKCS nº 12 (.PFX)** está selecionada.  

5.  Na página **Senha**, especifique uma senha forte para proteger o certificado exportado com sua chave privada e escolha **Avançar**.  

6.  Na página **Arquivo a Ser Exportado**, especifique o nome do arquivo que você deseja exportar e escolha **Avançar**.  

7.  Para fechar o assistente, escolha **Concluir** na página **Assistente para Exportação de Certificados** e escolha **OK** na caixa de diálogo de confirmação.  

8.  Feche os **Certificados (computador local)**.  

9. Armazene o arquivo com segurança e verifique se você pode acessá-lo do console do System Center Configuration Manager.  

 O certificado agora está pronto para ser importado quando você criar um ponto de distribuição baseado em nuvem.  

##  <a name="BKMK_client2008_cm2012"></a> Implantar o certificado do cliente para computadores Windows  
 Esta implantação de certificados abrange os seguintes procedimentos:  

-   Criar e emitir o modelo de certificado de autenticação de estação de trabalho na autoridade de certificação  

-   Configurar o registro automático do modelo de autenticação de estação de trabalho usando a política de grupo  

-   Registrar automaticamente o certificado de autenticação de estação de trabalho e verificar sua instalação nos computadores  

###  <a name="BKMK_client02008"></a> Criar e emitir o modelo de certificado de autenticação de estação de trabalho na autoridade de certificação  
 Esse procedimento cria um modelo de certificado para computadores cliente do System Center Configuration Manager e o adiciona à Autoridade de Certificação.  

##### <a name="to-create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a>Para criar e emitir o modelo de certificado de autenticação de estação de trabalho na autoridade de certificação  

1.  No servidor membro que executa o console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado** e escolha **Gerenciar** para carregar o console de gerenciamento Modelos de Certificado.  

2.  No painel de resultados, clique com o botão direito do mouse na entrada que tem **Autenticação de Estação de Trabalho** na coluna **Nome de Exibição do Modelo** e escolha **Duplicar Modelo**.  

3.  Na caixa de diálogo **Duplicar Modelo**, verifique se a opção **Windows 2003 Server, Enterprise Edition** está marcada e escolha **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

4.  Na caixa de diálogo **Propriedades do Novo Modelo**, na guia **Geral**, insira um nome de modelo, como **Certificado do Cliente do ConfigMgr**, para gerar os certificados do cliente que serão usados nos computadores cliente do Configuration Manager.  

5.  Escolha a guia **Segurança**, selecione o grupo **Computadores do Domínio** e selecione as permissões adicionais **Ler** e **Registrar Automaticamente**. Não desmarque **Registrar**.  

6.  Escolha **OK** e feche o **Console de Modelos de Certificado**.  

7.  No console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado**, escolha **Novo** e **Modelo de Certificado a Ser Emitido**.  

8.  Na caixa de diálogo **Habilitar Modelos de Certificado**, escolha o novo modelo que você acabou de criar, **Certificado do Cliente do ConfigMgr** e escolha **OK**.  

9. Se você não precisar criar ou emitir mais certificados, feche a **Autoridade de Certificação**.  

###  <a name="BKMK_client12008"></a> Configurar o registro automático do modelo de autenticação de estação de trabalho usando a política de grupo  
 Este procedimento configura a política de grupo para registrar automaticamente o certificado do cliente em computadores.  

##### <a name="to-set-up-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a>Para configurar o registro automático do modelo de autenticação da estação de trabalho usando a política de grupo  

1.  No controlador de domínio, escolha **Iniciar**, **Ferramentas Administrativas** e **Gerenciamento de Política de Grupo**.  

2.  Navegue até seu domínio, clique nele com o botão direito do mouse e escolha **Criar um GPO neste domínio e fornecer um link para ele aqui**.  

    > [!NOTE]  
    >  Esta etapa usa a prática recomendada de criação de uma nova Política de Grupo para configurações personalizadas em vez de editar a Política de Domínio Padrão que está instalada com os Serviços de Domínio Active Directory. Ao atribuir essa Política de Grupo no nível de domínio, você a aplicará a todos os computadores no domínio. Em um ambiente de produção, você pode restringir o registro automático para que ele registra somente em computadores selecionados. Você pode atribuir a política de grupo no nível da unidade organizacional ou filtrar a política de grupo de domínio com um grupo de segurança para que ela se aplique apenas aos computadores no grupo. Se você restringir o registro automático, lembre-se de incluir o servidor que está configurado como ponto de gerenciamento.  

3.  Na caixa de diálogo **Novo GPO**, insira um nome, como **Certificados de Registro Automático**, para a nova política de grupo e escolha **OK**.  

4.  No painel de resultados, na guia **Objetos de Política de Grupo Vinculados**, clique com o botão direito do mouse na nova política de grupo e escolha **Editar**.  

5.  Na caixa de diálogo **Editor de Gerenciamento de Política de Grupo**, expanda **Políticas** em **Configuração do Computador** e vá até **Configurações do Windows** / **Configurações de Segurança** / **Políticas de Chave Pública**.  

6.  Clique com o botão direito do mouse no tipo de objeto chamado **Cliente Serviços Certificado – Registro Automático** e escolha **Propriedades**.  

7.  Na lista suspensa **Modelo de Configuração**, escolha **Habilitado**, **Renovar certificados expirados, atualizar certificados pendentes e remover certificados revogados**, escolha **Atualizar certificados que usam modelos de certificados** e escolha **OK**.  

8.  Feche o **Gerenciamento de Política de Grupo**.  

###  <a name="BKMK_client22008"></a> Registrar automaticamente o certificado de autenticação de estação de trabalho e verificar sua instalação nos computadores  
 Este procedimento instala o certificado do cliente em computadores e verifica a instalação.  

##### <a name="to-automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-the-client-computer"></a>Para registrar automaticamente o certificado de autenticação de estação de trabalho e verificar sua instalação no computador cliente  

1.  Reinicie o computador da estação de trabalho e aguarde alguns minutos antes de entrar.  

    > [!NOTE]  
    >  A reinicialização de um computador é o método mais confiável de garantir o êxito no registro automático do certificado.  

2.  Entre com uma conta que tenha privilégios administrativos.  

3.  Na caixa de pesquisa, digite **mmc.exe.** e pressione **Enter**.  

4.  No console de gerenciamento vazio, escolha **Arquivo** e **Adicionar/Remover Snap-in**.  

5.  Na caixa de diálogo **Adicionar ou Remover Snap-ins**, escolha **Certificados** na lista de **Snap-ins disponíveis** e escolha **Adicionar**.  

6.  Na caixa de diálogo **Snap-in de certificado**, escolha **Conta de computador** e escolha **Avançar**.  

7.  Na caixa de diálogo **Selecionar Computador**, verifique se a opção **Computador local: (o computador no qual este console está sendo executado)** está marcada e escolha **Concluir**.  

8.  Na caixa de diálogo **Adicionar ou Remover Snap-ins**, escolha **OK**.  

9. No console, expanda **Certificados (Computador Local)**, **Pessoal** e escolha **Certificados**.  

10. No painel de resultados, confirme se um certificado tem a **Autenticação de Cliente** na coluna **Finalidade** e que o **Certificado do Cliente do ConfigMgr** está na coluna **Modelo de Certificado**.  

11. Feche os **Certificados (computador local)**.  

12. Repita as etapas de 1 a 11 para o servidor membro para verificar se o servidor que será configurado como ponto de gerenciamento também tem um certificado do cliente.  

 Agora, o computador está configurado com um certificado do cliente do System Center Configuration Manager.  

##  <a name="BKMK_clientdistributionpoint2008_cm2012"></a> Implantar o certificado do cliente para pontos de distribuição  

> [!NOTE]  
>  Este certificado também pode ser usado para imagens de mídia que não usam inicialização PXE, pois os requisitos do certificado são os mesmos.  

 Esta implantação de certificados abrange os seguintes procedimentos:  

-   Criar e emitir um modelo personalizado de certificado de autenticação de estação de trabalho na autoridade de certificação  

-   Solicitar o certificado personalizado de autenticação de estação de trabalho  

-   Exportar o certificado do cliente para pontos de distribuição  

###  <a name="BKMK_clientdistributionpoint02008"></a> Criar e emitir um modelo personalizado de certificado de autenticação de estação de trabalho na autoridade de certificação  
 Este procedimento cria um modelo de certificado personalizado para pontos de distribuição do System Center Configuration Manager para que a chave privada possa ser exportada e adiciona o modelo do certificado à autoridade de certificação.  

> [!NOTE]  
>  Este procedimento usa um modelo de certificado diferente do modelo de certificado que você criou para computadores cliente. Embora ambos os certificados requeiram a funcionalidade de autenticação de cliente, o certificado para pontos de distribuição requer que a chave privada seja exportada. Como prática recomendada de segurança, não configure modelos de certificado para permitir que a chave privada seja exportada a menos que essa configuração seja necessária. O ponto de distribuição requer essa configuração, pois você deve importar o certificado como um arquivo, em vez de escolhe-lo no repositório de certificados.  
>   
>  Ao criar um novo modelo de certificado para esse certificado, você pode restringir os computadores que podem solicitar um certificado cuja chave privada pode ser exportada. No exemplo de implantação, esse será o grupo de segurança que você criou anteriormente para servidores do sistema de sites do System Center Configuration Manager que executam o IIS. Em uma rede de produção que distribui as funções do sistema de site do IIS, considere a criação de um novo grupo de segurança para os servidores que executam pontos de distribuição, assim você pode restringir o certificado apenas para esses servidores do sistema de site. Você também pode adicionar as seguintes modificações para o certificado:  
>   
>  -   Requerer aprovação para instalar o certificado, para obter segurança adicional.  
> -   Aumentar o período de validade do certificado. Como você precisa exportar e importar o certificado todas as vezes antes de ele expirar, um aumento no período de validade reduz a frequência de repetição desse procedimento. No entanto, um aumento no período de validade também diminui a segurança do certificado, pois ele fornece mais tempo para que um invasor descriptografe a chave privada e roube o certificado.  
> -   Usar um valor personalizado no campo Entidade do certificado ou SAN (Nome Alternativo da Entidade) para ajudar a identificar esse certificado dos certificados do cliente padrão. Isso pode ser particularmente útil se você usar o mesmo certificado para vários pontos de distribuição.  

##### <a name="to-create-and-issue-the-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a>Para criar e emitir o modelo personalizado de certificado de autenticação de estação de trabalho na autoridade de certificação  

1.  No servidor membro que executa o console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado** e escolha **Gerenciar** para carregar o console de gerenciamento Modelos de Certificado.  

2.  No painel de resultados, clique com o botão direito do mouse na entrada que tem **Autenticação de Estação de Trabalho** na coluna **Nome de Exibição do Modelo** e escolha **Duplicar Modelo**.  

3.  Na caixa de diálogo **Duplicar Modelo**, verifique se a opção **Windows 2003 Server, Enterprise Edition** está marcada e escolha **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

4.  Na caixa de diálogo **Propriedades do Novo Modelo**, na guia **Geral**, insira um nome de modelo, como **Certificado do Ponto de Distribuição do Cliente do ConfigMgr**, para gerar o certificado de autenticação de cliente para pontos de distribuição.  

5.  Escolha a guia **Tratamento de Solicitação** e escolha **Permitir que a chave privada seja exportada**.  

6.  Escolha a guia **Segurança** e remova a permissão **Registrar** do grupo de segurança **Administradores de Empresa**.  

7.  Escolha **Adicionar**, insira **Servidores IIS do ConfigMgr** na caixa de texto e escolha **OK**.  

8.  Selecione a permissão **Registrar** para este grupo e não desmarque a permissão **Ler** .  

9. Escolha **OK** e feche o **Console de Modelos de Certificado**.  

10. No console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado**, escolha **Novo** e **Modelo de Certificado a Ser Emitido**.  

11. Na caixa de diálogo **Habilitar Modelos de Certificado**, escolha o novo modelo que você acabou de criar, **Certificado do Ponto de Distribuição de Cliente do ConfigMgr** e escolha **OK**.  

12. Se você não precisar criar ou emitir mais certificados, feche a **Autoridade de Certificação**.  

###  <a name="BKMK_clientdistributionpoint12008"></a> Solicitar o certificado personalizado de autenticação de estação de trabalho  
 Este procedimento solicita e instala o certificado do cliente personalizado no servidor membro que executa o IIS e que será configurado como ponto de distribuição.  

##### <a name="to-request-the-custom-workstation-authentication-certificate"></a>Para solicitar o certificado personalizado de autenticação de estação de trabalho  

1.  Escolha **Iniciar**, **Executar** e, em seguida, digite **mmc.exe.** No console vazio, escolha **Arquivo** e **Adicionar/Remover Snap-in**.  

2.  Na caixa de diálogo **Adicionar ou Remover Snap-ins**, escolha **Certificados** na lista de **Snap-ins disponíveis** e escolha **Adicionar**.  

3.  Na caixa de diálogo **Snap-in de certificado**, escolha **Conta de computador** e escolha **Avançar**.  

4.  Na caixa de diálogo **Selecionar Computador**, verifique se a opção **Computador local: (o computador no qual este console está sendo executado)** está marcada e escolha **Concluir**.  

5.  Na caixa de diálogo **Adicionar ou Remover Snap-ins**, escolha **OK**.  

6.  No console, expanda **Certificados (Computador Local)** e escolha **Pessoal**.  

7.  Clique com o botão direito do mouse em **Certificados**, escolha **Todas as Tarefas** e **Solicitar Novo Certificado**.  

8.  Na página **Antes de Começar** escolha **Avançar**.  

9. Se você vir a página **Selecionar Política de Registro de Certificado**, escolha **Avançar**.  

10. Na página **Solicitar Certificados**, escolha **Certificado do Ponto de Distribuição Cliente do ConfigMgr** na lista de certificados disponíveis e escolha **Registrar**.  

11. Na página **Resultados da Instalação de Certificados** espere até que o certificado seja instalado e escolha **Concluir**.  

12. No painel de resultados, confirme se um certificado tem a **Autenticação de Cliente** na coluna **Finalidade** e que o **Certificado do Ponto de Distribuição do Cliente do ConfigMgr** está na coluna **Modelo de Certificado**.  

13. Não feche os **Certificados (computador local)**.  

###  <a name="BKMK_exportclientdistributionpoint22008"></a> Exportar o certificado do cliente para pontos de distribuição  
 Este procedimento exporta o certificado personalizado de autenticação de estação de trabalho para um arquivo para que ele possa ser importado nas propriedades do ponto de distribuição.  

##### <a name="to-export-the-client-certificate-for-distribution-points"></a>Para exportar o certificado do cliente para pontos de distribuição  

1.  No console **Certificados (Computador Local)**, clique com o botão direito do mouse no certificado que você acabou de instalar, escolha **Todas as Tarefas** e escolha **Exportar**.  

2.  No Assistente para Exportação de Certificados, escolha **Avançar**.  

3.  Na página **Exportar Chave Privada**, escolha **Sim, exportar a chave privada** e escolha **Avançar**.  

    > [!NOTE]  
    >  Se essa opção não estiver disponível, o certificado foi criado sem a opção de exportar a chave privada. Nesse cenário, você não pode exportar o certificado no formato exigido. Você deve configurar o modelo de certificado para que a chave privada possa ser exportada e, em seguida, solicitar o certificado novamente.  

4.  Na página **Formato do Arquivo de Exportação**, verifique se a opção **Troca de Informações Pessoais – PKCS nº 12 (.PFX)** está selecionada.  

5.  Na página **Senha**, especifique uma senha forte para proteger o certificado exportado com sua chave privada e escolha **Avançar**.  

6.  Na página **Arquivo a Ser Exportado**, especifique o nome do arquivo que você deseja exportar e escolha **Avançar**.  

7.  Para fechar o assistente, escolha **Concluir** na página **Assistente para Exportação de Certificados** e escolha **OK** na caixa de diálogo de confirmação.  

8.  Feche os **Certificados (computador local)**.  

9. Armazene o arquivo com segurança e verifique se você pode acessá-lo do console do System Center Configuration Manager.  

 Agora o certificado está pronto para ser importado quando você configurar o ponto de distribuição.  

> [!TIP]  
>  Você pode usar o mesmo arquivo de certificado ao configurar imagens de mídia para uma implantação do sistema operacional que não usa inicialização PXE e a sequência de tarefas para instalar a imagem deve contatar um ponto de gerenciamento que requer conexões de cliente HTTPS.  

##  <a name="BKMK_mobiledevices2008_cm2012"></a> Implantar o certificado de registro para dispositivos móveis  
 Esta implantação do certificado tem um procedimento único para criar e emitir o modelo de certificado de registro na autoridade de certificação.  

### <a name="create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Criar e emitir o modelo de certificado de registro na autoridade de certificação  
 Esse procedimento cria um modelo de certificado de registro para dispositivos móveis do System Center Configuration Manager e o adiciona à Autoridade de Certificação.  

##### <a name="to-create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Para criar e emitir o modelo de certificado de registro na autoridade de certificação  

1.  Cria um grupo de segurança que contém usuários que registrarão dispositivos móveis no System Center Configuration Manager.  

2.  No servidor membro que tem os Serviços de Certificados instalados, no console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado** e escolha **Gerenciar** para carregar o console de gerenciamento de Modelos de Certificado.  

3.  No painel de resultados, clique com o botão direito do mouse na entrada que tem **Sessão Autenticada** na coluna **Nome de Exibição do Modelo** e escolha **Duplicar Modelo**.  

4.  Na caixa de diálogo **Duplicar Modelo**, verifique se a opção **Windows 2003 Server, Enterprise Edition** está marcada e escolha **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

5.  Na caixa de diálogo **Propriedades do Novo Modelo**, na guia **Geral**, insira um nome do modelo, como **Certificado de Registro do Dispositivo Móvel do ConfigMgr** para gerar os certificados de registro para os dispositivos móveis a serem gerenciados pelo System Center Configuration Manager.  

6.  Escolha a guia **Nome da Entidade**, verifique se a opção **Criar com base nas informações do Active Directory** está marcada, selecione **Nome comum** para o **Formato de nome da entidade:** e desmarque **Nome UPN** de **Incluir estas informações no nome da entidade alternativo**.  

7.  Escolha a guia **Segurança**, escolha o grupo de segurança que contém usuários que têm dispositivos móveis a serem registrados e escolha a permissão adicional **Registrar**. Não desmarque **Ler**.  

8.  Escolha **OK** e feche o **Console de Modelos de Certificado**.  

9. No console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado**, escolha **Novo** e **Modelo de Certificado a Ser Emitido**.  

10. Na caixa de diálogo **Habilitar Modelos de Certificado**, escolha o novo modelo que você acabou de criar, **Certificado de Registro do Dispositivo Móvel do ConfigMgr** e escolha **OK**.  

11. Se você não precisar criar ou emitir mais certificados, feche o console da Autoridade de Certificação.  

 Agora o modelo de certificado de registro de dispositivo móvel está pronto para ser selecionado quando você configurar um perfil de registro de dispositivo móvel nas configurações do cliente.  

##  <a name="BKMK_AMT2008_cm2012"></a> Implantar os certificados para AMT  
 Esta implantação de certificados abrange os seguintes procedimentos:  

-   Criar, emitir e instalar o certificado de provisionamento AMT  

-   Criar e emitir o certificado do servidor Web para computadores AMT  

-   Criar e emitir os certificados de autenticação de cliente para computadores AMT 802.1X  

###  <a name="BKMK_AMTprovisioning2008"></a> Criar, emitir e instalar o certificado de provisionamento AMT  
 Crie o certificado de provisionamento com sua AC interna quando computadores AMT são configurados com a impressão digital do certificado da AC raiz interna. Quando não for esse o caso e você precisar usar uma autoridade de certificação externa, use as instruções da empresa que emitiu o certificado de provisionamento AMT, o que, muitas vezes, envolverá solicitar o certificado do site público da empresa. Você também poderá encontrar instruções detalhadas para a AC externa escolhida no [site do Intel vPro Expert Center: Microsoft vPro Manageability](http://go.microsoft.com/fwlink/?LinkId=132001).  

> [!IMPORTANT]  
>  CAs externas podem não oferecer suporte ao identificador de objeto de provisionamento do Intel AMT. Quando esse for o caso, forneça o atributo OU do **Certificado de Instalação de Cliente do Intel(R)**.  

 Quando você solicitar um certificado de provisionamento AMT de uma AC externa, instale o certificado no repositório de certificados do computador pessoal no servidor membro que hospedará o ponto de serviço fora de banda.  

##### <a name="to-request-and-issue-the-amt-provisioning-certificate"></a>Para solicitar e emitir o certificado de provisionamento AMT  

1.  Crie um grupo de segurança que contenha as contas de computador de servidores do sistema de sites que executarão o ponto de serviço fora de banda.  

2.  No servidor membro com os Serviços de Certificados instalados, no console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado** e escolha **Gerenciar** para carregar o console **Modelos de Certificado**.  

3.  No painel de resultados, clique com o botão direito do mouse na entrada que tem **Servidor Web** na coluna **Nome de Exibição do Modelo** e escolha **Duplicar Modelo**.  

4.  Na caixa de diálogo **Duplicar Modelo**, verifique se a opção **Windows 2003 Server, Enterprise Edition** está marcada e escolha **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

5.  Na caixa de diálogo **Propriedades do Novo Modelo**, na guia **Geral**, insira um nome de modelo, como **Provisionamento AMT do ConfigMgr**, para o certificado de provisionamento AMT.  

6.  Escolha a guia **Nome da Entidade**, escolha **Criar com base nas informações do Active Directory** e **Nome comum**.  

7.  Escolha a guia **Extensões**, verifique se **Políticas de Aplicativo** está selecionada e escolha **Editar**.  

8.  Na caixa de diálogo **Editar Extensão de Políticas de Aplicativo**, escolha **Adicionar**.  

9. Na caixa de diálogo **Adicionar Política de Aplicativo**, escolha **Novo**.  

10. Na caixa de diálogo **Nova Política de Aplicativo**, digite **Provisionamento AMT** no campo **Nome** e digite o seguinte número para o **Identificador de Objeto**: **2.16.840.1.113741.1.2.3**.  

11. Escolha **OK** e **OK** na caixa de diálogo **Adicionar Política de Aplicativo**.  

12. Escolha **OK** na caixa de diálogo **Editar Extensão de Políticas de Aplicativo**.  

13. Na caixa de diálogo **Propriedades do Novo Modelo**, o seguinte está listado como descrição das **Políticas de Aplicativo**: **Autenticação de Servidor** e **Provisionamento AMT**.  

14. Escolha a guia **Segurança** e remova a permissão **Registrar** dos grupos de segurança **Admins. do Domínio** e **Administradores de Empresa**.  

15. Escolha **Adicionar**, insira o nome de um grupo de segurança que contenha a conta de computador para a função do sistema de sites do ponto de serviço fora de banda e escolha **OK**.  

16. Escolha a permissão **Registrar** para este grupo e não desmarque a permissão **Ler**.  

17. Escolha **OK** e feche o console de **Modelos de Certificado**.  

18. Em **Autoridade de Certificação**, clique com o botão direito do mouse em **Modelos de Certificado**, escolha **Novo** e escolha **Modelo de Certificado a ser Emitido**.  

19. Na caixa de diálogo **Habilitar Modelos de Certificado**, escolha o novo modelo que você acabou de criar, **Provisionamento AMT do ConfigMgr** e escolha **OK**.  

    > [!NOTE]  
    >  Se você não conseguir concluir as etapas 18 ou 19, verifique se está usando o Enterprise Edition do Windows Server 2008. Embora você possa configurar modelos com o Windows Server Standard Edition e os Serviços de Certificados, não é possível implantar certificados usando modelos de certificado modificados, a menos que você esteja usando o Enterprise Edition do Windows Server 2008.  

20. Não feche **Autoridade de Certificação**.  

 O certificado de provisionamento AMT de sua AC interna agora está pronto para ser instalado no computador do ponto de serviço fora de banda.  

##### <a name="to-install-the-amt-provisioning-certificate"></a>Para instalar o certificado de provisionamento AMT  

1.  Reinicie o servidor membro que executa o IIS para confirmar que ele pode acessar o modelo de certificado com a permissão configurada.  

2.  Escolha **Iniciar**, **Executar** e, em seguida, digite **mmc.exe.** No console vazio, escolha **Arquivo** e **Adicionar/Remover Snap-in**.  

3.  Na caixa de diálogo **Adicionar ou Remover Snap-ins**, escolha **Certificados** na lista de **Snap-ins disponíveis** e escolha **Adicionar**.  

4.  Na caixa de diálogo **Snap-in de certificado**, escolha **Conta de computador** e escolha **Avançar**.  

5.  Na caixa de diálogo **Selecionar Computador**, verifique se a opção **Computador local: (o computador no qual este console está sendo executado)** está marcada e escolha **Concluir**.  

6.  Na caixa de diálogo **Adicionar ou Remover Snap-ins**, escolha **OK**.  

7.  No console, expanda **Certificados (Computador Local)** e escolha **Pessoal**.  

8.  Clique com o botão direito do mouse em **Certificados**, escolha **Todas as Tarefas** e **Solicitar Novo Certificado**.  

9. Na página **Antes de Começar** escolha **Avançar**.  

10. Se você vir a página **Selecionar Política de Registro de Certificado**, escolha **Avançar**.  

11. Na página **Solicitar Certificados**, selecione **Provisionamento AMT** na lista de certificados disponíveis e escolha **Registrar**.  

12. Na página **Resultados da Instalação de Certificados** espere até que o certificado seja instalado e escolha **Concluir**.  

13. Feche os **Certificados (computador local)**.  

 O certificado de provisionamento AMT de sua AC interna agora está instalado e pronto para ser selecionado nas propriedades do ponto de serviço fora de banda.  

### <a name="create-and-issue-the-web-server-certificate-for-amt-based-computers"></a>Criar e emitir o certificado do servidor Web para computadores AMT  
 Use o procedimento a seguir para preparar os certificados do servidor Web para computadores AMT.  

##### <a name="to-create-and-issue-the-web-server-certificate-template"></a>Para criar e emitir o modelo de certificado do servidor Web  

1.  Crie um grupo de segurança vazio que contenha as contas de computador do AMT que o System Center Configuration Manager cria durante o provisionamento AMT.  

2.  No servidor membro com os Serviços de Certificados instalados, no console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado** e escolha **Gerenciar** para carregar o console **Modelos de Certificado**.  

3.  No painel de resultados, clique com o botão direito do mouse na entrada que tem **Servidor Web** na coluna **Nome de Exibição do Modelo** e escolha **Duplicar Modelo**.  

4.  Na caixa de diálogo **Duplicar Modelo**, verifique se a opção **Windows 2003 Server, Enterprise Edition** está marcada e escolha **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**  

5.  Na caixa de diálogo **Propriedades do Novo Modelo**, na guia **Geral**, insira um nome de modelo, como **Certificado do Servidor Web AMT do ConfigMgr**, para gerar os certificados Web que serão usados para gerenciamento fora de banda em computadores AMT.  

6.  Escolha a guia **Nome da Entidade**, escolha **Criar com base nas informações do Active Directory**, escolha **Nome comum** para o **Formato de nome de entidade** e desmarque **Nome UPN** para o nome da entidade alternativo.  

7.  Escolha a guia **Segurança** e remova a permissão **Registrar** dos grupos de segurança **Admins. do Domínio** e **Administradores de Empresa**.  

8.  Escolha **Adicionar** e insira o nome do grupo de segurança que você criou para provisionamento AMT e escolha **OK**.  

9. Escolha as seguintes permissões **Permitir** para esse grupo de segurança: **Ler** e **Registrar**.  

10. Escolha **OK** e feche o console de **Modelos de Certificado**.  

11. No console da **Autoridade de Certificação**, clique com o botão direito do mouse em **Modelos de Certificado**, escolha **Novo** e **Modelo de Certificado a Ser Emitido**.  

12. Na caixa de diálogo **Habilitar Modelos de Certificado**, escolha o novo modelo que você acabou de criar, **Certificado do Servidor Web AMT do ConfigMgr** e escolha **OK**.  

13. Se você não precisar criar ou emitir mais certificados, feche a **Autoridade de Certificação**.  

 Agora o modelo de servidor Web AMT está pronto para configurar computadores AMT com certificados do servidor Web. Escolha esse modelo de certificado nas propriedades do componente de gerenciamento fora de banda.  

### <a name="create-and-issue-the-client-authentication-certificates-for-8021x-amt-based-computers"></a>Criar e emitir os certificados de autenticação de cliente para computadores AMT 802.1X  
 Use o procedimento a seguir se computadores AMT forem usar certificados do cliente para redes com ou sem fio 802.1X autenticadas.  

##### <a name="to-create-and-issue-the-client-authentication-certificate-template-on-the-ca"></a>Para criar e emitir o modelo de certificado de autenticação do cliente na autoridade de certificação  

1.  No servidor membro com os Serviços de Certificados instalados, no console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado** e escolha **Gerenciar** para carregar o console **Modelos de Certificado**.  

2.  No painel de resultados, clique com o botão direito do mouse na entrada que tem **Autenticação de Estação de Trabalho** na coluna **Nome de Exibição do Modelo** e escolha **Duplicar Modelo**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**  

3.  Na caixa de diálogo **Propriedades do Novo Modelo**, na guia **Geral**, insira um nome de modelo, como **Certificado de Autenticação de Cliente do AMT 802.1X do ConfigMgr**, para gerar os certificados do cliente que serão usados para gerenciamento fora de banda em computadores AMT.  

4.  Escolha a guia **Nome da Entidade**, escolha **Criar com base nas informações do Active Directory** e **Nome comum** para o **Formato de nome de entidade**. Desmarque **Nome DNS** para o nome alternativo da entidade e escolha **Nome UPN**.  

5.  Escolha a guia **Segurança** e remova a permissão **Registrar** dos grupos de segurança **Admins. do Domínio** e **Administradores de Empresa**.  

6.  Escolha **Adicionar**, insira o nome do grupo de segurança que você especificará nas propriedades do componente de gerenciamento fora de banda para conter as contas de computador dos computadores AMT e escolha **OK**.  

7.  Selecione as seguintes permissões **Permitir** para esse grupo de segurança: **Ler** e **Registrar**.  

8.  Escolha **OK** e feche o console de gerenciamento de **Modelos de Certificado**, **certtmpl – [Modelos de Certificado]**.  

9. No console de gerenciamento da **Autoridade de Certificação**, clique com o botão direito do mouse em **Modelos de Certificado**, escolha **Novo** e **Modelo de Certificado a Ser Emitido**.  

10. Na caixa de diálogo **Habilitar Modelos de Certificado**, escolha o novo modelo que você acabou de criar, **Certificado de Autenticação de Cliente AMT 802.1X do ConfigMgr** e escolha **OK**.  

11. Se você não precisar criar ou emitir mais certificados, feche a **Autoridade de Certificação**.  

 Agora o modelo de certificado de autenticação do cliente está pronto para emitir certificados para computadores AMT que podem ser usados para autenticação do cliente do 802.1X. Escolha esse modelo de certificado nas propriedades do componente de gerenciamento fora de banda.  

##  <a name="BKMK_MacClient_SP1"></a> Implantar o certificado do cliente para computadores Mac  

Esta implantação do certificado tem um procedimento único para criar e emitir o modelo de certificado de registro na autoridade de certificação.  

###  <a name="BKMK_MacClient_CreatingIssuing"></a> Criar e emitir um modelo de certificado do cliente Mac na autoridade de certificação  
 Este procedimento cria um modelo de certificado personalizado para computadores Mac do System Center Configuration Manager e o adiciona à autoridade de certificação.  

> [!NOTE]  
>  Este procedimento usa um modelo de certificado diferente do modelo que você pode ter criado para computadores cliente Windows ou para pontos de distribuição.  
>   
>  Ao criar um novo modelo de certificado para esse certificado, você pode restringir a solicitação do certificado a usuários autorizados.  

##### <a name="to-create-and-issue-the-mac-client-certificate-template-on-the-certification-authority"></a>Para criar e emitir o modelo de certificado do cliente Mac na autoridade de certificação  

1.  Crie um grupo de segurança que contenha as contas de usuário para usuários administrativos que registrarão o certificado no computador Mac usando o System Center Configuration Manager.  

2.  No servidor membro que executa o console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado** e escolha **Gerenciar** para carregar o console de gerenciamento Modelos de Certificado.  

3.  No painel de resultados, clique com o botão direito do mouse na entrada que mostra **Sessão Autenticada** na coluna **Nome de Exibição do Modelo** e escolha **Duplicar Modelo**.  

4.  Na caixa de diálogo **Duplicar Modelo**, verifique se a opção **Windows 2003 Server, Enterprise Edition** está marcada e escolha **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

5.  Na caixa de diálogo **Propriedades do Novo Modelo**, na guia **Geral**, insira um nome de modelo, como **Certificado do Cliente Mac do ConfigMgr**, para gerar o certificado do cliente Mac.  

6.  Escolha a guia **Nome da Entidade**, verifique se a opção **Criar com base nas informações do Active Directory** está marcada, escolha **Nome comum** para o **Formato de nome da entidade:** e desmarque **Nome UPN** de **Incluir estas informações no nome da entidade alternativo**.  

7.  Escolha a guia **Segurança** e remova a permissão **Registrar** dos grupos de segurança **Admins. do Domínio** e **Administradores de Empresa**.  

8.  Escolha **Adicionar**, especifique o grupo de segurança que você criou na etapa um e escolha **OK**.  

9. Escolha a permissão **Registrar** para este grupo e não desmarque a permissão **Ler**.  

10. Escolha **OK** e feche o **Console de Modelos de Certificado**.  

11. No console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado**, escolha **Novo** e **Modelo de Certificado a Ser Emitido**.  

12. Na caixa de diálogo **Habilitar Modelos de Certificado**, escolha o novo modelo que você acabou de criar, **Certificado do Cliente Mac do ConfigMgr** e escolha **OK**.  

13. Se você não precisar criar ou emitir mais certificados, feche a **Autoridade de Certificação**.  

 Agora o modelo de certificado do cliente Mac está pronto para ser selecionado quando você definir as configurações do cliente para registro.
