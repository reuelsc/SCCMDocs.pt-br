---
title: Configurar certificados | MDM Local | System Center Configuration Manager
description: "Configure certificados para comunicações confiáveis do Gerenciamento de Dispositivo Móvel Local no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2a7d7170-1933-40e9-96d6-74a6eb7278e2
caps.latest.revision: 27
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 22a01ffa8385413c9671fd282c7337cbb6e2ffa0


---
# <a name="set-up-certificates-for-trusted-communications-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Set up certificates for trusted communications for On-premises Mobile Device Management in System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Gerenciamento de Dispositivo Móvel Local do System Center Configuration Manager exige as funções de sistema de sites ponto de registro, ponto proxy do registro, ponto de distribuição e ponto de gerenciamento de dispositivos para ser configurado para comunicações confiáveis com os dispositivos gerenciados. Qualquer servidor de sistema de sites que hospede uma ou mais dessas funções deve ter um certificado PKI exclusivo associado ao servidor Web nesse sistema. Um certificado com a mesma raiz que o certificado nos servidores também deve ser armazenado nos dispositivos gerenciados para estabelecer comunicação confiável com eles.  

 Para dispositivos ingressados no domínio, os Serviços de Certificados do Active Directory instala o certificado necessário com a raiz confiável em todos os dispositivos automaticamente. Para dispositivos não ingressados no domínio, você deve obter um certificado válido com uma raiz confiável por outros meios. Se você usar a autoridade de certificação do site como sua raiz confiável (que é a mesma que o Active Directory usa para dispositivos ingressados no domínio), os servidores do sistema de sites para o registro de ponto e o ponto proxy do registro deverão ter um certificado emitido pela autoridade de certificação associada a eles.  

 Cada dispositivo a ser gerenciado também precisará ter um certificado com a mesma raiz instalada nele para oferecer suporte a comunicações confiáveis com as funções de sistema de sites. Para dispositivos registrados em massa, você pode incluir o certificado no pacote de inscrição que é adicionado ao dispositivo para registrá-lo quando o dispositivo for iniciado pela primeira vez por um usuário. Para dispositivos registrados pelo usuário, você precisa adicionar o certificado por email, download da web ou algum outro método.  

 Como alternativa para dispositivos não ingressados no domínio, você pode usar a raiz de uma autoridade de certificação pública conhecida (como Verisign ou GoDaddy) para emitir o certificado de servidor, o que evita ter que instalar manualmente um certificado no dispositivo, pois a maioria dos dispositivos confia nativamente em conexões com servidores que usam a mesma raiz da autoridade de certificação pública. Essa é uma alternativa útil para dispositivos registrados pelo usuário nos quais não é possível instalar os certificados confiáveis por meio da autoridade de certificação do site em cada dispositivo.  

> [!IMPORTANT]  
>  Há várias maneiras de configurar os certificados para comunicações confiáveis entre dispositivos e servidores do sistema de sites para o Gerenciamento de Dispositivo Móvel Local. As informações fornecidas neste artigo são uma das maneiras de como fazer isso. Esse método requer que você esteja executando um servidor no seu site com a função Serviços de Certificados do Active Directory e os serviços de função Autoridade de Certificação e Registro via Web na Autoridade de Certificação instalados. Confira [Serviços de Certificados do Active Directory](http://go.microsoft.com/fwlink/p/?LinkId=115018) para obter mais informações e diretrizes sobre essa função do Windows Server.  

 Para configurar o site do Configuration Manager para as comunicações SSL necessárias para o Gerenciamento de Dispositivo Móvel Local, siga estas etapas de alto nível:  

-   [Configurar a AC (autoridade de certificação) para publicação de CRL](#bkmk_configCa)  

-   [Criar o modelo de certificado do servidor Web na AC](#bkmk_certTempl)  

-   [Solicitar o certificado do servidor Web para cada função de sistema de sites](#bkmk_requestCert)  

-   [Associar o certificado ao servidor Web](#bkmk_bindCert)  

-   [Exportar o certificado com a mesma raiz do certificado do servidor Web](#bkmk_exportCert)  

##  <a name="a-namebkmkconfigcaa-configure-the-certification-authority-ca-for-crl-publishing"></a><a name="bkmk_configCa"></a> Configurar a AC para publicação de lista de CRL  
 Por padrão, a autoridade de certificação usa CRLs (listas de certificados revogados) baseadas em LDAP que permite conexões para dispositivos ingressados no domínio. Você deve adicionar listas de certificados revogados baseadas em HTTP à autoridade de certificação para possibilitar que dispositivos não ingressados no domínio sejam confiáveis com certificados emitidos da autoridade de certificação. Esses certificados são necessários para comunicações SSL entre os servidores que hospedam as funções de sistema de sites do Configuration Manager e os dispositivos registrados no Gerenciamento de Dispositivo Móvel Local.  

 Siga as etapas abaixo a fim de configurar a autoridade de certificação para publicar automaticamente as informações da lista de certificados revogados para emissão de certificados que permitam conexões confiáveis de dispositivos ingressados e não ingressados no domínio:  

1.  No servidor que está executando a autoridade de certificação para seu site, clique em **Iniciar** > **Ferramentas Administrativas** > **Autoridade de Certificação**.  

2.  No console da Autoridade de Certificação, clique com o botão direito do mouse em **CertificateAuthority** e clique em **Propriedades**.  

3.  Nas propriedades de CertificateAuthority, clique na guia **Extensões** e verifique se a opção **Selecionar extensão** está definida como **Pontos de Distribuição da Lista de Certificados Revogados**  

4.  Selecione **http://<ServerDNSName\>/CertEnroll/<CAName\><CRLNameSuffix\><DeltaCRLAllowed\>.crl**. E as três opções abaixo:  

    -   **Inclua em CRLs. Os clientes utilizam isso para encontrar locais CRL Delta.**  

    -   **Inclua na extensão CDP de certificados emitidos.**  

    -   **Incluir na extensão IDP de CRLs emitidas**  

5.  Clique na guia **Módulo de Saída**, clique em **Propriedades…** e escolha **Permitir que certificados sejam publicados no sistema de arquivos**.  

6.  Clique em **OK** quando for notificado de que os Serviços de Certificados do Active Directory devem ser reiniciados.  

7.  Clique com o botão direito do mouse em **Certificados Revogados**, clique em **Todas as Tarefas** e em **Publicar**.  

8.  Na caixa de diálogo Publicar CRL, escolha **Somente CRL Delta** e clique em **OK**.  

##  <a name="a-namebkmkcerttempla-create-the-web-server-certificate-template-on-the-ca"></a><a name="bkmk_certTempl"></a> Criar o modelo de certificado do servidor Web na AC  
 Depois de publicar a nova lista de certificados revogados na autoridade de certificação, a próxima etapa é criar um modelo de certificado de servidor Web. Esse modo é exigido para emitir certificados para os servidores que hospedam as funções de sistema de sites ponto de registro, ponto proxy do registro, ponto de distribuição e ponto de gerenciamento de dispositivo. Esses servidores serão pontos de extremidade SSL para comunicações confiáveis entre as funções de sistema de sites e dispositivos registrados.    Siga as etapas abaixo para criar o modelo de certificado:  

1.  Crie um grupo de segurança chamado **Servidores MDM do ConfigMgr** que contenha os servidores que executam os sistemas de sites que exigem comunicações confiáveis com dispositivos registrados.  

2.  No console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado** e clique em **Gerenciar** para carregar o console dos Modelos de Certificado.  

3.  No painel de resultados, clique com o botão direito do mouse na entrada que exibe **Servidor Web** na coluna **Nome de Exibição do Modelo**e clique em **Duplicar Modelo**.  

4.  Na caixa de diálogo **Duplicar Modelo** , verifique se a opção **Windows 2003 Server, Enterprise Edition** está marcada e clique em **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**. O Configuration Manager não é compatível com os modelos de certificado do Windows Server 2008 para comunicações confiáveis usando HTTPS.  

    > [!NOTE]  
    >  Se a autoridade de certificação que você está usando estiver no Windows Server 2012, a versão do modelo do certificado não será solicitada quando você clicar em **Modelo Duplicado**. Em vez disso, especifique isso na guia **Compatibilidade** das propriedades do modelo, da seguinte forma:  
    >   
    >  **Autoridade de Certificação**: **Windows Server 2003**  
    >   
    >  **Destinatário do certificado**: **Windows XP / Server 2003**  

5.  Na caixa de diálogo **Propriedades do Novo Modelo**, na guia **Geral**, insira um nome de modelo para gerar os certificados da Web que serão usados nos sistemas de sites do Configuration Manager, como **Servidor Web do MDM ConfigMgr**.  

6.  Clique na guia **Nome da Entidade**, escolha **Criar das informações do Active Directory** e, para o formato de nome da entidade, especifique o **Nome DNS**. Desmarque a caixa de seleção do nome da entidade alternativa se **Nome UPN** estiver marcado.  

7.  Clique na guia **Segurança** e remova a permissão **Registrar** dos grupos de segurança **Admins. do domínio** e **Admins. da empresa**.  

8.  Clique em **Adicionar**, insira **Servidores MDM do ConfigMgr** na caixa de texto e clique em **OK**.  

9. Selecione a permissão **Registrar** para este grupo e não desmarque a permissão **Ler** .  

10. Clique em **OK**e feche o console de Modelos de Certificado.  

11. No console da Autoridade de Certificação, clique com o botão direito do mouse em **Modelos de Certificado**, clique em **Novo**e em **Modelo de certificado a ser emitido**.  

12. Na caixa de diálogo **Habilitar Modelos de Certificado**, escolha o novo modelo que você acabou de criar, **Servidor Web do MDM ConfigMgr** e clique em **OK**.  

##  <a name="a-namebkmkrequestcerta-request-the-web-server-certificate-for-each-site-system-role"></a><a name="bkmk_requestCert"></a> Solicitar o certificado do servidor Web para cada função de sistema de sites  
 Os dispositivos registrados no Gerenciamento de Dispositivo Móvel Local devem confiar nos pontos de extremidade SSL que hospedam o ponto de registro, ponto proxy do registro, ponto de distribuição e ponto de gerenciamento de dispositivos.  As etapas abaixo descrevem como solicitar o certificado do servidor Web para IIS. Você deve fazer isso para cada servidor (ponto de extremidade SSL) que hospeda uma das funções de sistema de sites exigidas para o Gerenciamento de Dispositivo Móvel Local.  

1.  No servidor do site primário, abra o prompt de comando com permissão de administrador, digite **MMC** e pressione **Enter**.  

2.  No MMC, clique em **Arquivo** > **Adicionar/Remover Snap-in**.  

3.  No snap-in de Certificados, escolha **Certificados**, clique em **Adicionar**, escolha **Conta de computador**, clique em **Avançar**, clique em **Concluir** e em **OK** para sair da janela Adicionar ou Remover Snap-in.  

4.  Clique com o botão direito do mouse em **Pessoal** e clique em **Todas as Tarefas** > **Solicitar Novo Certificado**.  

5.  No assistente de Registro de Certificado, clique em **Avançar**, escolha **Política de Registro do Active Directory** e clique em **Avançar**.  

6.  Marque a caixa de seleção próxima ao certificado do servidor Web (**Servidor Web MDM ConfigMgr**) e clique em **Registrar**.  

7.  Depois que o certificado for registrado, clique em **Concluir**.  

 Como cada servidor precisará de um certificado do servidor Web exclusivo, você precisará repetir esse processo para cada servidor que hospeda uma das funções de sistema de sites exigidas para o Gerenciamento de Dispositivo Móvel Local.  Se um servidor hospedar todas as funções de sistema de sites, você precisará solicitar apenas um certificado de servidor Web.  

##  <a name="a-namebkmkbindcerta-bind-the-certificate-to-the-web-server"></a><a name="bkmk_bindCert"></a> Associar o certificado ao servidor Web  
 Agora o novo certificado precisa ser associado ao servidor Web de cada servidor do sistema de sites que hospeda as funções de sistema de sites exigidas para o Gerenciamento de Dispositivo Móvel Local. Siga as etapas abaixo para cada servidor que hospeda as funções de sistema de sites ponto de registro e ponto proxy do registro. Se um servidor hospedar todas as funções de sistema de sites, basta seguir essas etapas de uma vez. Você não precisa realizar essa tarefa para as funções de sistema de sites ponto de distribuição e ponto de gerenciamento de dispositivos, uma vez que elas recebem automaticamente o certificado necessário durante o registro.  

1.  No servidor que hospeda o ponto de registro, o ponto proxy do registro, o ponto de distribuição ou o ponto de gerenciamento de dispositivos, clique em **Iniciar** > **Ferramentas Administrativas** > **Gerenciador do IIS**.  

2.  Em Conexões, navegue até **Site Padrão**, clique nele com o botão direito do mouse e, em seguida, clique em **Editar Ligações...**  

3.  Na caixa de diálogo Ligações do Site, clique em **https** e em **Editar…**  

4.  Na caixa de diálogo Editar Associação do Site, escolha o certificado que acabou de registrar para o **Certificado SSL**, clique em **OK** e em **Fechar**.  

5.  No console do Gerenciador do IIS, em Conexões, escolha o servidor Web e, no painel Ações à direita, clique em **Reiniciar**.  

##  <a name="a-namebkmkexportcerta-export-the-certificate-with-the-same-root-as-the-web-server-certificate"></a><a name="bkmk_exportCert"></a> Exportar o certificado com a mesma raiz do certificado do servidor Web  
 Os Serviços de Certificados do Active Directory geralmente instalam o certificado necessário da autoridade de certificação em todos os dispositivos ingressados no domínio. Mas dispositivos não ingressados no domínio não poderão se comunicar com as funções de sistema de sites sem certificado da autoridade de certificação raiz. Para obter o certificado necessário para que os dispositivos se comuniquem com as funções de sistema de sites, você pode exportá-lo do certificado associado ao servidor Web.  

 Siga estas etapas para exportar o certificado raiz do certificado do servidor Web.  

1.  No Gerenciador do IIS, clique em **Site da Web Padrão** e, no painel Ação à direita, clique em **Associações...**  

2.  Na caixa de diálogo Associações do Site, clique em **https** e em **Editar…**  

3.  Verifique se o certificado do servidor Web está selecionado e clique em **Exibir...**  

4.  Nas propriedades do certificado do servidor Web, clique em **Caminho de Certificação**, clique na raiz, na parte superior do caminho de certificação, e clique em **Exibir Certificado**.  

5.  Nas propriedades do certificado raiz, clique em **Detalhes** e em **Copiar para Arquivo...**  

6.  No Assistente para Exportação de Certificados, clique em **Avançar**.  

7.  Verifique se **X.509 binário codificado por DER (.CER)** está selecionado como formato e clique em **Avançar**.  

8.  Para o nome do arquivo, clique em **Procurar…**, escolha um local para salvar o arquivo de certificado, dê um nome ao arquivo e clique em **Salvar**.  

     Os dispositivos a serem registrados precisarão de acesso a esse arquivo para importar o certificado raiz, portanto escolha um local comum que a maioria dos computadores e dispositivos possa acessar, ou você pode salvá-lo em um local conveniente (como a unidade C) e movê-lo para um local comum posteriormente.  

     Clique em **Avançar**.  

9. Examine as configurações e clique em **Concluir**.  



<!--HONumber=Nov16_HO1-->


