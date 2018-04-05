---
title: Certificados do CMG
description: Saiba mais sobre os diferentes certificados digitais para uso com o gateway de gerenciamento de nuvem.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.openlocfilehash: 1c7adec8f8919736c61859791802a96766af31bb
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/23/2018
---
# <a name="certificates-for-the-cloud-management-gateway"></a>Certificados para o gateway de gerenciamento de nuvem

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Dependendo do cenário usado para gerenciar clientes na Internet com o CMG (gateway de gerenciamento de nuvem), você precisa de um ou mais certificados digitais. Para obter mais informações sobre os diferentes cenários, consulte [Planejar o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## <a name="cmg-server-authentication-certificate"></a>Certificado de autenticação de servidor do CMG

*Este certificado é obrigatório em todos os cenários.*

Você fornece esse certificado ao criar o CMG no console do Configuration Manager.

O CMG cria um serviço HTTPS ao qual os clientes baseados na Internet se conectam. O servidor exige um certificado de autenticação de servidor para criar o canal de segurança. Compre um certificado para essa finalidade de um provedor público ou emita-o por meio da PKI (infraestrutura de chave pública). Para obter mais informações, consulte [Certificado raiz confiável do CMG para clientes](#cmg-trusted-root-certificate-to-clients).

 > [!TIP]
 > Esse certificado exige um nome exclusivo para identificar o serviço no Azure. Antes de solicitar um certificado, confirme se o nome de domínio do Azure desejado é exclusivo. Por exemplo, *GraniteFalls.CloudApp.Net*. Faça logon no [portal do Microsoft Azure](https://portal.azure.com). Clique em **Criar um recurso**, selecione a categoria **Computação** e, em seguida, clique em **Serviço de Nuvem**. No campo **Nome DNS**, digite o prefixo desejado, por exemplo, *GraniteFalls*. A interface reflete se o nome de domínio está disponível ou se já está em uso por outro serviço. Não crie o serviço no portal; apenas use esse processo para verificar a disponibilidade do nome. 
  
 > [!NOTE]
 > A partir da versão 1802, o certificado de autenticação de servidor do CMG é compatível com caracteres curinga. Algumas autoridades de certificação emitem certificados usando um caractere curinga para o nome do host. Por exemplo, **\*.contoso.com**. Algumas organizações usam certificados curinga para simplificar sua PKI e reduzir os custos de manutenção.
 <!--491233-->


### <a name="cmg-trusted-root-certificate-to-clients"></a>Certificado raiz confiável do CMG para clientes

Os clientes devem confiar no certificado de autenticação de servidor do CMG. Há dois métodos para estabelecer essa relação de confiança:
- Use um certificado de um provedor de certificados público e globalmente confiável. Por exemplo, entre outros, VeriSign ou Thawte. Os clientes do Windows incluem ACs (autoridades de certificação) raiz confiáveis desses provedores. Usando um certificado de autenticação de servidor emitido por um desses provedores, os clientes automaticamente confiam nele. 
- Use um certificado emitido por uma AC corporativa da PKI (infraestrutura de chave pública). A maioria das implementações de PKI corporativo adiciona autoridades de certificação raiz confiáveis aos clientes do Windows. Por exemplo, usando os Serviços de Certificados do Active Directory com a política de grupo. Se você emitir o certificado de autenticação de servidor do CMG de uma AC na qual os clientes não confiam automaticamente, precisará adicionar o certificado raiz confiável da AC aos clientes baseados na Internet.
    - Também use perfis de certificado do Configuration Manager para provisionar certificados em clientes. Para obter mais informações, consulte [Introdução aos perfis de certificado](/sccm/protect/deploy-use/introduction-to-certificate-profiles).

### <a name="server-authentication-certificate-issued-by-public-provider"></a>Certificado de autenticação de servidor emitido por um provedor público

Ao usar esse método, os clientes confiam automaticamente no certificado e você não precisa criar um certificado personalizado por conta própria. O Configuration Manager cria o serviço no Azure com o domínio cloudapp.net. Um provedor de certificado público não pode emitir para você um certificado com esse nome. Use o seguinte processo para criar um alias DNS:

1. Crie um registro de nome canônico (CNAME) no DNS público de sua organização. Esse registro cria um alias para o CMG com um nome amigável que você usa no certificado público.
Por exemplo, a Contoso nomeia seu CMG **GraniteFalls**, que se torna **GraniteFalls.CloudApp.Net** no Azure. No namespace contoso.com do DNS público da Contoso, o administrador de DNS cria um novo registro CNAME para **GraniteFalls.Contoso.com** para o nome do host real **GraniteFalls.CloudApp.net**.
2. Solicite um certificado de autenticação de servidor de um provedor público usando o CN (Nome Comum) do alias CNAME.
Por exemplo, a Contoso usa **GraniteFalls.Contoso.com** para o CN do certificado.
3. Crie o CMG no console do Configuration Manager usando esse certificado. Na página **Configurações** do Assistente para Criação de Gateway de Gerenciamento de Nuvem: 
    - Quando você adiciona o certificado do servidor a esse serviço de nuvem (por meio do **Arquivo de certificado**), o assistente extrai o nome do host do CN do certificado como o nome do serviço. 
    - Em seguida, ele acrescenta esse nome do host a **cloudapp.net** ou **usgovcloudapp.net** para a nuvem do Azure US Government, como o FQDN do Serviço para criar o serviço no Azure.
    - Por exemplo, quando a Contoso cria o CMG, o Configuration Manager extrai o nome do host **GraniteFalls** do CN do certificado. O Azure cria o serviço real como **GraniteFalls.CloudApp.net**.

### <a name="server-authentication-certificate-issued-from-enterprise-pki"></a>Certificado de autenticação de servidor emitido pelo PKI corporativo

Crie um certificado SSL personalizado para o CMG da mesma maneira que para um ponto de distribuição na nuvem. Siga as instruções em [Implantando o certificado de serviço em pontos de distribuição baseados em nuvem](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012), mas realize o seguinte de forma diferente:

- Ao solicitar o certificado do servidor Web personalizado, forneça um FQDN para o nome comum do certificado. Para usar o CMG na nuvem pública do Azure, use um nome que termina com **cloudapp.net** ou **usgovcloudapp.net** para a nuvem do Azure US Government.



## <a name="azure-management-certificate"></a>Certificado de gerenciamento do Azure

*Esse certificado é obrigatório para implantações de serviço clássico. Ele não é obrigatório para implantações do Azure Resource Manager.*

Você fornece esse certificado no portal do Azure e ao criar o CMG no console do Configuration Manager.

Para criar o CMG no Azure, o ponto de conexão de serviço do Configuration Manager precisa primeiro se autenticar em sua assinatura do Azure. Ao usar uma implantação de serviço clássico, ele usa o certificado de gerenciamento do Azure para essa autenticação. Um administrador do Azure carrega o certificado em sua assinatura. Quando você cria o CMG no console do Configuration Manager, forneça esse certificado.

Para obter mais informações e instruções sobre como carregar um certificado de gerenciamento, consulte os artigos a seguir na documentação do Azure:

- [Serviços de nuvem e certificados de gerenciamento](/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)

- [Carregar um certificado de gerenciamento de serviço do Azure](/azure/azure-api-management-certs)

> [!IMPORTANT]
> Certifique-se de copiar a ID da assinatura associada ao certificado de gerenciamento. Use-o para criar o CMG no console do Configuration Manager.



## <a name="client-authentication-certificate"></a>Certificado de autenticação de cliente

*Esse certificado é obrigatório para os clientes baseados na Internet que executam dispositivos Windows 7, Windows 8.1 e Windows 10 não ingressados no Azure AD (Azure Active Directory). Ele também é obrigatório no ponto de conexão do CMG. Ele não é obrigatório para os clientes do Windows 10 ingressados no Azure AD.*

Os clientes usam esse certificado para se autenticarem no CMG. Os dispositivos Windows 10 híbridos ou ingressado no domínio de nuvem não exigem esse certificado, porque usam o Azure AD para autenticação.

Provisione esse certificado fora do contexto do Configuration Manager. Por exemplo, use os Serviços de Certificados do Active Directory e a política de grupo para emitir certificados de autenticação de cliente. Para obter mais informações, consulte [Implantando o certificado do cliente em computadores Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).


### <a name="client-trusted-root-certificate-to-cmg"></a>Certificado raiz confiável do cliente para o CMG

*Esse certificado é obrigatório ao usar certificados de autenticação de cliente. Quando todos os clientes usam o Azure AD para autenticação, esse certificado não é obrigatório.* 

Você fornece esse certificado ao criar o CMG no console do Configuration Manager.

O CMG deve confiar nos certificados de autenticação de cliente. Para estabelecer essa relação de confiança, forneça a cadeia de certificados raiz confiáveis. Especifique duas ACs raiz confiáveis e quatro ACs (subordinadas) intermediárias. 


#### <a name="export-the-client-certificates-trusted-root"></a>Exportar a raiz confiável do certificado do cliente

Depois de emitir um certificado de autenticação de cliente para um computador, use esse processo nesse computador para exportar a raiz confiável.

1.  Abra o menu Iniciar. Digite "executar" para abrir a janela Executar. Abra **mmc**. 

2.  No menu Arquivo, escolha **Adicionar/Remover Snap-in...**.

3.  Na caixa de diálogo Adicionar ou Remover Snap-ins, selecione **Certificados** e, em seguida, clique em **Adicionar**. 
    a. Na caixa de diálogo Snap-in dos certificados, selecione **Conta de computador** e, em seguida, clique em **Avançar**. 
    b. Na caixa de diálogo Selecionar Computador, selecione **Computador local** e, em seguida, clique em **Concluir**. 
    c. Na caixa de diálogo Adicionar ou Remover Snap-ins, clique em **OK**.

4.  Expanda **Certificados**, expanda **Pessoais** e selecione **Certificados**.

5.  Selecione um certificado cuja Finalidade Pretendida é a **Autenticação de Cliente**. 
    a. No menu Ação, selecione **Abrir**. 
    b. Alterne para a guia **Caminho de Certificação**. c. Selecione o próximo certificado na cadeia e, em seguida, clique em **Exibir Certificado**.

6.  Nessa nova caixa de diálogo Certificado, alterne para a guia **Detalhes**. Clique em **Copiar para Arquivo…**.

7.  Conclua o Assistente para Exportação de Certificados usando o formato de certificado padrão, **X.509 binário codificado em DER (.CER)**. Anote o nome e o local do certificado exportado.

8. Exporte todos os certificados no caminho de certificação do certificado de autenticação de cliente original. Anote quais certificados exportados são ACs intermediárias e quais são ACs raiz confiáveis.



## <a name="enable-management-point-for-https"></a>Habilitar o ponto de gerenciamento para HTTPS

*Requisitos de certificado*
- Nas versões 1706 ou 1710, ao gerenciar clientes tradicionais com a identidade local usando um certificado de autenticação de cliente, esse certificado é recomendado, mas não é obrigatório.
- Na versão 1710, ao gerenciar clientes do Windows 10 ingressados no Azure AD, esse certificado é obrigatório para os pontos de gerenciamento. 
- A partir da versão 1802, esse certificado é obrigatório em todos os cenários. 

Provisione esse certificado fora do contexto do Configuration Manager. Por exemplo, use os Serviços de Certificados do Active Directory e a política de grupo para emitir um certificado do servidor Web. Para obter mais informações, consulte [Requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements) e [Implantar o certificado do servidor Web em sistemas de sites que executam o IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).



## <a name="next-steps"></a>Próximas etapas

- [Configurar o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Perguntas frequentes sobre o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Segurança e privacidade para o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
