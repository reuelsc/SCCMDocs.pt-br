---
title: Certificados do CMG
description: Saiba mais sobre os diferentes certificados digitais para uso com o gateway de gerenciamento de nuvem.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 11/27/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.collection: M365-identity-device-management
ms.openlocfilehash: 69c5f446c465655adb1e9fee1b891a3152af47e9
ms.sourcegitcommit: f38ef9afb0c608c0153230ff819e5f5e0fb1520c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2019
ms.locfileid: "58197088"
---
# <a name="certificates-for-the-cloud-management-gateway"></a>Certificados para o gateway de gerenciamento de nuvem

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Dependendo do cenário usado para gerenciar clientes na Internet com o CMG (gateway de gerenciamento de nuvem), você precisa de um ou mais dos seguintes certificados digitais:  

- [Certificado de autenticação de servidor do CMG](#bkmk_serverauth)  
    - [Certificado raiz confiável do CMG para clientes](#bkmk_cmgroot)  
    - [Certificado de autenticação de servidor emitido por um provedor público](#bkmk_serverauthpublic)  
    - [Certificado de autenticação de servidor emitido pelo PKI empresarial](#bkmk_serverauthpki)  

- [Certificado de gerenciamento do Azure](#bkmk_azuremgmt)  

- [Certificado de autenticação de cliente](#bkmk_clientauth)  
    - [Certificado raiz confiável do cliente para o CMG](#bkmk_clientroot)  

- [Habilitar o ponto de gerenciamento para HTTPS](#bkmk_mphttps)  


Para obter mais informações sobre os diferentes cenários, consulte [Planejar o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


### <a name="general-information"></a>Informações gerais
<!--SCCMDocs issue #779-->
Certificados para o Gateway de Gerenciamento de Nuvem têm suporte para as seguintes configurações:  

- Comprimento de chave de 2048 ou 4096 bits

- Da versão 1710 em diante, suporte para provedores de armazenamento de chaves para chaves privadas do certificado. Para obter mais informações, consulte [Visão geral dos certificados CNG](/sccm/core/plan-design/network/cng-certificates-overview).  

- Iniciando na versão 1802, quando você configura o Windows com a seguinte política: **Criptografia do sistema: use algoritmos em conformidade com FIPS para criptografia, hash e assinatura**  

- Da versão 1802 em diante, suporte para **TLS 1.2**. Para obter mais informações, veja [Referência técnica para controles de criptografia](/sccm/core/plan-design/security/cryptographic-controls-technical-reference#about-ssl-vulnerabilities).  



## <a name="bkmk_serverauth"></a> Certificado de autenticação de servidor do CMG

*Este certificado é obrigatório em todos os cenários.*

Você fornece esse certificado ao criar o CMG no console do Configuration Manager.

O CMG cria um serviço HTTPS ao qual os clientes baseados na Internet se conectam. O servidor exige um certificado de autenticação de servidor para criar o canal de segurança. Adquira um certificado para essa finalidade de um provedor público ou emita-o por meio da PKI (infraestrutura de chave pública). Para obter mais informações, consulte [Certificado raiz confiável do CMG para clientes](#cmg-trusted-root-certificate-to-clients).

 > [!TIP]
 > Esse certificado exige um nome exclusivo para identificar o serviço no Azure. Antes de solicitar um certificado, confirme se o nome de domínio do Azure desejado é exclusivo. Por exemplo, *GraniteFalls.CloudApp.Net*. Faça logon no [portal do Microsoft Azure](https://portal.azure.com). Selecione **Criar um recurso**, escolha a categoria **Computação** e, em seguida, selecione **Serviço de Nuvem**. No campo **Nome DNS**, digite o prefixo desejado, por exemplo, *GraniteFalls*. A interface reflete se o nome de domínio está disponível ou se já está em uso por outro serviço. Não crie o serviço no portal; apenas use esse processo para verificar a disponibilidade do nome. 
  
 > [!TIP]
 > Se o CMG também estiver habilitado como um ponto de Distribuição na Nuvem, confirme que o nome do serviço CMG escolhido também é um nome exclusivo da Conta de Armazenamento do Azure. Por exemplo, *GraniteFalls*. Faça logon no [portal do Microsoft Azure] (https://portal.azure.com). Selecione **Criar um recurso**, escolha a categoria **Armazenamento** e, em seguida, selecione **Conta de armazenamento – blob, arquivo, tabela, fila**. Clique em **Criar** e, em **Detalhes da instância**, insira o mesmo nome escolhido para o serviço CMG, por exemplo, *GraniteFalls*. A interface reflete se o nome da conta de armazenamento está disponível ou se já está em uso por outro serviço. Não crie a conta de armazenamento no portal; apenas use esse processo para verificar a disponibilidade do nome. Se o nome do serviço de nuvem do CMG for exclusivo, mas o nome da conta de armazenamento não for, o provisionamento falhará.
 
 > [!NOTE]
 > A partir da versão 1802, o certificado de autenticação de servidor do CMG dá suporte a caracteres curinga. Algumas autoridades de certificação emitem certificados usando um caractere curinga para o nome do host. Por exemplo, **\*.contoso.com**. Algumas organizações usam certificados curinga para simplificar sua PKI e reduzir os custos de manutenção.<!--491233-->  
 > 
 > Para saber mais sobre como usar um certificado curinga com um CMG, consulte [Configurar um CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#set-up-a-cmg).<!--SCCMDocs issue #565-->  


### <a name="bkmk_cmgroot"></a> Certificado raiz confiável do CMG para clientes

Os clientes devem confiar no certificado de autenticação de servidor do CMG. Há dois métodos para estabelecer essa relação de confiança: 

- Use um certificado de um provedor de certificados público e globalmente confiável. Por exemplo, DigiCert, Thawte ou VeriSign, entre outros. Os clientes do Windows incluem ACs (autoridades de certificação) raiz confiáveis desses provedores. Usando um certificado de autenticação de servidor emitido por um desses provedores, os clientes automaticamente confiam nele.  

- Use um certificado emitido por uma AC corporativa da PKI (infraestrutura de chave pública). A maioria das implementações de PKI corporativo adiciona autoridades de certificação raiz confiáveis aos clientes do Windows. Por exemplo, usando os Serviços de Certificados do Active Directory com a política de grupo. Se você emitir o certificado de autenticação de servidor do CMG de uma AC na qual os clientes não confiam automaticamente, adicione o certificado raiz confiável da AC aos clientes baseados na Internet.  

    - Também use perfis de certificado do Configuration Manager para provisionar certificados em clientes. Para obter mais informações, consulte [Introdução aos perfis de certificado](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

> [!Note]  
> Da versão 1806 em diante, ao criar um CMG, não é mais necessário fornecer um certificado raiz confiável na página Configurações. Esse certificado não é necessário ao usar o Azure AD (Azure Active Directory) para autenticação do cliente, mas costumava ser necessário no assistente. Se você estiver usando certificados de autenticação de cliente de PKI, ainda será necessário adicionar um certificado raiz confiável para o CMG.<!--SCCMDocs-pr issue #2872-->  


### <a name="bkmk_serverauthpublic"></a> Certificado de autenticação de servidor emitido por um provedor público

Um provedor de certificados de terceiros não pode criar um certificado para CloudApp.net, pois esse domínio pertence à Microsoft. Você só pode obter um certificado emitido para um domínio de sua propriedade. O principal motivo para adquirir um certificado de um provedor de terceiros é que os clientes já confiam no certificado raiz daquele provedor.

Use o seguinte processo para criar um alias DNS:

1. Crie um registro de nome canônico (CNAME) no DNS público de sua organização. Esse registro cria um alias para o CMG com um nome amigável que você usa no certificado público.

    Por exemplo, a Contoso nomeia seu CMG **GraniteFalls**, que se torna **GraniteFalls.CloudApp.Net** no Azure. No namespace contoso.com do DNS público da Contoso, o administrador de DNS cria um novo registro CNAME para **GraniteFalls.Contoso.com** para o nome do host real **GraniteFalls.CloudApp.net**.  

2. Solicite um certificado de autenticação de servidor de um provedor público usando o CN (Nome Comum) do alias CNAME.
Por exemplo, a Contoso usa **GraniteFalls.Contoso.com** para o CN do certificado.  

3. Crie o CMG no console do Configuration Manager usando esse certificado. Na página **Configurações** do Assistente para Criação de Gateway de Gerenciamento de Nuvem:   

    - Quando você adiciona o certificado do servidor a esse serviço de nuvem (por meio do **Arquivo de certificado**), o assistente extrai o nome do host do CN do certificado como o nome do serviço.  

    - Em seguida, ele acrescenta esse nome do host a **cloudapp.net** ou **usgovcloudapp.net** para a nuvem do Azure US Government, como o FQDN do Serviço para criar o serviço no Azure.  

    - Por exemplo, quando a Contoso cria o CMG, o Configuration Manager extrai o nome do host **GraniteFalls** do CN do certificado. O Azure cria o serviço real como **GraniteFalls.CloudApp.net**.  

Quando você cria a instância do CMG no Configuration Manager, embora o certificado tenha GraniteFalls.Contoso.com, o Configuration Manager só extrai o nome do host, por exemplo: GraniteFalls. Ele acrescenta esse nome de host ao CloudApp.net, que o Azure requer durante a criação de um serviço de nuvem. O alias CNAME no namespace DNS para seu domínio, Contoso.com, mapeia juntos esses dois FQDNs. O Configuration Manager fornece aos clientes uma política para acessar esse CMG, e o mapeamento de DNS as vincula para que eles possam acessar com segurança o serviço no Azure.<!--SCCMDocs issue #565-->  


### <a name="bkmk_serverauthpki"></a> Certificado de autenticação de servidor emitido pelo PKI empresarial

Crie um certificado SSL personalizado para o CMG da mesma maneira que para um ponto de distribuição na nuvem. Siga as instruções em [Implantando o certificado de serviço em pontos de distribuição baseados em nuvem](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012), mas realize o seguinte de forma diferente:

- Ao solicitar o certificado do servidor Web personalizado, forneça um FQDN para o nome comum do certificado. Esse nome pode ser um nome de domínio público que você tem ou é possível usar o domínio cloudapp.net. Se estiver usando seu próprio domínio público, consulte o processo acima para criar um alias de DNS no DNS público de sua organização.  

- Ao usar o domínio cloudapp.net público para o certificado do servidor Web do CMG:  

    - Na nuvem pública do Azure, use um nome que termine em **cloudapp.net**  

    - Use um nome que termine em **usgovcloudapp.net** para a nuvem do Governo dos EUA do Azure  



## <a name="bkmk_azuremgmt"></a> Certificado de gerenciamento do Azure

*Esse certificado é obrigatório para implantações de serviço clássico. Ele não é obrigatório para implantações do Azure Resource Manager.*

> [!Important]  
> Da versão 1810 em diante, implantações de serviço clássico no Azure são preteridas no Configuration Manager. Comece a usar as implantações do Azure Resource Manager para o gateway de gerenciamento de nuvem. Para obter mais informações, confira [Planejar para CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).

Você fornece esse certificado no portal do Azure e ao criar o CMG no console do Configuration Manager.

Para criar o CMG no Azure, o ponto de conexão de serviço do Configuration Manager precisa primeiro se autenticar em sua assinatura do Azure. Ao usar uma implantação de serviço clássico, ele usa o certificado de gerenciamento do Azure para essa autenticação. Um administrador do Azure carrega o certificado em sua assinatura. Quando você cria o CMG no console do Configuration Manager, forneça esse certificado.

Para obter mais informações e instruções sobre como carregar um certificado de gerenciamento, consulte os artigos a seguir na documentação do Azure:

- [Serviços de nuvem e certificados de gerenciamento](https://docs.microsoft.com/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)  

- [Carregar um certificado de gerenciamento de serviço do Azure](https://docs.microsoft.com/azure/azure-api-management-certs)  

> [!IMPORTANT]
> Certifique-se de copiar a ID da assinatura associada ao certificado de gerenciamento. Use-o para criar o CMG no console do Configuration Manager.



## <a name="bkmk_clientauth"></a> Certificado de autenticação de cliente

*Esse certificado é obrigatório para os clientes baseados na Internet que executam dispositivos Windows 7, Windows 8.1 e Windows 10 não ingressados no Azure AD (Azure Active Directory). Ele também é obrigatório no ponto de conexão do CMG. Ele não é obrigatório para os clientes do Windows 10 ingressados no Azure AD.*

Os clientes usam esse certificado para se autenticarem no CMG. Os dispositivos Windows 10 híbridos ou ingressado no domínio de nuvem não exigem esse certificado, porque usam o Azure AD para autenticação.

Provisione esse certificado fora do contexto do Configuration Manager. Por exemplo, use os Serviços de Certificados do Active Directory e a política de grupo para emitir certificados de autenticação de cliente. Para obter mais informações, consulte [Implantando o certificado do cliente em computadores Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).

O ponto de conexão do CMG requer que esse certificado encaminhe com segurança solicitações de cliente para um ponto de gerenciamento de HTTPS. Se você estiver usando o Azure AD ou HTTP aprimorado, esse certificado não será necessário. Para obter mais informações, consulte [Habilitar ponto de gerenciamento para HTTPS](#bkmk_mphttps).


### <a name="bkmk_clientroot"></a> Certificado raiz confiável do cliente para o CMG

*Esse certificado é obrigatório ao usar certificados de autenticação de cliente. Quando todos os clientes usam o Azure AD para autenticação, esse certificado não é obrigatório.* 

Você fornece esse certificado ao criar o CMG no console do Configuration Manager.

O CMG deve confiar nos certificados de autenticação de cliente. Para estabelecer essa relação de confiança, forneça a cadeia de certificados raiz confiáveis. Especifique duas ACs raiz confiáveis e quatro ACs (subordinadas) intermediárias. 


#### <a name="export-the-client-certificates-trusted-root"></a>Exportar a raiz confiável do certificado do cliente

Depois de emitir um certificado de autenticação de cliente para um computador, use esse processo nesse computador para exportar a raiz confiável.

1.  Abra o menu Iniciar. Digite "executar" para abrir a janela Executar. Abra `mmc`.  

2.  No menu Arquivo, escolha **Adicionar/Remover Snap-in...**.  

3.  Na caixa de diálogo Adicionar ou Remover Snap-ins, selecione **Certificados** e, em seguida, selecione **Adicionar**.  

    a. Na caixa de diálogo Snap-in dos certificados, selecione **Conta de computador** e, em seguida, selecione em **Avançar**.  

    b. Na caixa de diálogo Selecionar Computador, selecione **Computador local** e, em seguida, selecione em **Concluir**.  

    c. Na caixa de diálogo Adicionar ou Remover Snap-ins, selecione **OK**.  

4.  Expanda **Certificados**, expanda **Pessoais** e selecione **Certificados**.  

5.  Selecione um certificado cuja Finalidade Pretendida é a **Autenticação de Cliente**.  

    a. No menu Ação, selecione **Abrir**.  

    b. Vá para a guia **Caminho de Certificação**.  

    c. Selecione o próximo certificado na cadeia e, em seguida, selecione **Exibir Certificado**.  

6.  Nessa nova caixa de diálogo Certificado, mude para a guia **Detalhes**. Selecione **Copiar para Arquivo...**.  

7.  Conclua o Assistente para Exportação de Certificados usando o formato de certificado padrão, **X.509 binário codificado em DER (.CER)**. Anote o nome e o local do certificado exportado.  

8. Exporte todos os certificados no caminho de certificação do certificado de autenticação de cliente original. Anote quais certificados exportados são ACs intermediárias e quais são ACs raiz confiáveis.  



## <a name="bkmk_mphttps"></a> Habilitar o ponto de gerenciamento para HTTPS

Provisione esse certificado fora do contexto do Configuration Manager. Por exemplo, use os Serviços de Certificados do Active Directory e a política de grupo para emitir um certificado do servidor Web. Para obter mais informações, consulte [Requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements) e [Implantar o certificado do servidor Web em sistemas de sites que executam o IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).


- Na versão 1710, esse certificado é recomendado, mas não é obrigatório, para gerenciar clientes tradicionais com a identidade local usando um certificado de autenticação de cliente. Esse certificado é obrigatório para os pontos de gerenciamento ao gerenciar clientes do Windows 10 ingressados no Microsoft Azure Active Directory.

- Na versão 1802, esse certificado é obrigatório em todos os cenários. Somente os pontos de gerenciamento que você habilitar para CMG devem ser HTTPS. Essa alteração no comportamento fornece melhor suporte para autenticação baseada em token do Azure AD.  

- Começando na versão 1806, ao usar a opção do site para **Usar certificados gerados pelo Configuration Manager para o sistema de sites HTTP**, o ponto de gerenciamento pode ser HTTP. Para obter mais informações, confira [HTTP aprimorado](/sccm/core/plan-design/hierarchy/enhanced-http).

### <a name="management-point-client-connection-mode-summary"></a>Resumo do modo de conexão do cliente do ponto de gerenciamento
Essas tabelas resumem se o ponto de gerenciamento requer HTTP ou HTTPS, dependendo do tipo de cliente e da versão do site.

#### <a name="for-internet-based-clients-communicating-with-the-cloud-management-gateway"></a>Para clientes baseados na Internet se comunicando com o gateway de gerenciamento de nuvem
Configure um ponto de gerenciamento local para permitir conexões do CMG com o seguinte modo de conexão de cliente:

| Tipo de cliente   | 1710        | 1802        | 1806        | 1810        |
|------------------|-------------|-------------|-------------|-------------|
| Grupo de trabalho        | HTTP, HTTPS | HTTPS       | E-HTTP<sup>[Observação 1](#bkmk_note1)</sup>, HTTPS | E-HTTP<sup>[Observação 1](#bkmk_note1)</sup>, HTTPS |
| Ingressado no domínio do AD | HTTP, HTTPS | HTTPS       | E-HTTP<sup>[Observação 1](#bkmk_note1)</sup>, HTTPS | E-HTTP<sup>[Observação 1](#bkmk_note1)</sup>, HTTPS |
| Ingressado no Azure AD  | HTTPS       | HTTPS       | E-HTTP, HTTPS | E-HTTP, HTTPS |
| Ingressado no híbrido    | HTTP, HTTPS | HTTPS       | E-HTTP, HTTPS | E-HTTP, HTTPS |

<a name="bkmk_note1"></a> 

> [!Note]  
> **Observação 1**: essa configuração exige que o cliente tenha um [certificado de autenticação de cliente](#bkmk_clientauth) e só dá suporte a cenários centrados no dispositivo.  

#### <a name="for-on-premises-clients-communicating-with-the-on-premises-management-point"></a>Para clientes locais se comunicando com o ponto de gerenciamento local
Configure um ponto de gerenciamento local com o seguinte modo de conexão de cliente:

| Tipo de cliente   | 1710        | 1802        | 1806        | 1810        |
|------------------|-------------|-------------|-------------|-------------|
| Grupo de trabalho        | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS |
| Ingressado no domínio do AD | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS |
| Ingressado no Azure AD  | HTTPS       | HTTPS       | HTTPS       | HTTPS       |
| Ingressado no híbrido    | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS |

> [!Note]  
> Na versão 1806, os clientes ingressados no domínio do AD dão suporte a cenários centrados no dispositivo e no usuário que se comunicam com um ponto de gerenciamento de HTTP ou de HTTPS.  
> 
> Clientes ingressados no Azure AD e no híbrido podem se comunicar por meio de HTTP para cenários centrados em dispositivos, mas precisam de E-HTTP ou HTTPS para habilitar cenários centrados no usuário. Caso contrário, eles se comportariam da mesma maneira que os clientes de grupo de trabalho.  


#### <a name="legend-of-terms"></a>Legenda de termos
- *Grupo de trabalho*: o dispositivo não está associado a um domínio ou ao Azure AD, mas tem um [certificado de autenticação de cliente](#bkmk_clientauth)  
- *Ingressado no domínio do AD*: você ingressa o dispositivo em um domínio do Active Directory local  
- *Ingressado no Azure AD*: também conhecido como ingressado no domínio de nuvem, você ingressa o dispositivo em um locatário do Azure Active Directory  
- *Ingressado no híbrido*: você ingressa o dispositivo tanto em um domínio do Active Directory quanto em um locatário do Azure AD  
- *HTTP*: nas propriedades do ponto de gerenciamento, você define as conexões do cliente para **HTTP**  
- *HTTPS*: nas propriedades do ponto de gerenciamento, você define as conexões do cliente para **HTTPS**  
- *E-HTTP*: nas propriedades do site, guia Comunicação do Computador Cliente, você define as configurações do sistema de sites para **HTTPS ou HTTP** e, em seguida, habilita a nova opção para **Usar certificados gerados pelo Configuration Manager para sistemas de sites HTTP**. Configure o ponto de gerenciamento para HTTP, o ponto de gerenciamento de HTTP está pronto para comunicação HTTP e HTTPS (cenários de autenticação de token).   



## <a name="next-steps"></a>Próximas etapas

- [Configurar o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  

- [Perguntas frequentes sobre o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)  

- [Segurança e privacidade para o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)  
