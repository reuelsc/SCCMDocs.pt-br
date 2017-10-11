---
title: "Propriedades de instalação do cliente | Microsoft Docs"
description: "Aprenda sobre as propriedades de instalação do cliente no System Center Configuration Manager."
ms.custom: na
ms.date: 01/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
caps.latest.revision: "15"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: ef515da67a7293de60a7678dee69e9785d339352
ms.sourcegitcommit: 96b79fa091f44e8e6ac5652f6cbbb4b873a8bad9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2017
---
# <a name="about-client-installation-properties-in-system-center-configuration-manager"></a>Sobre as propriedades de instalação do cliente no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use o comando CCMSetup.exe do System Center Configuration Manager para instalar manualmente o cliente do Configuration Manager.  

##  <a name="aboutCCMSetup"></a> Sobre o CCMSetup.exe  
 O comando CCMSetup.exe baixa os arquivos necessários para instalar o cliente de um ponto de gerenciamento ou local de origem. Esses arquivos podem incluir:  

-   O Client.msi do pacote do Windows Installer que instala o software cliente.  

-   Arquivos de instalação do BITS (Serviço de Transferência Inteligente em Segundo Plano) da Microsoft.  

-   Arquivos de instalação do Windows Installer.  

-   Atualizações e correções para o cliente do Configuration Manager.  

> [!NOTE]  
>  No Configuration Manager, não é possível executar o arquivo Client.msi diretamente.  

 O CCMSetup.exe fornece [propriedades de linha de comando](#ccmsetup-exe-command-line-properties) para personalizar a instalação. Também é possível especificar propriedades para modificar o comportamento do Client.msi na linha de comando CCMSetup.exe.  

> [!IMPORTANT]  
>  Especifique as propriedades do CCMSetup antes de especificar as propriedades do Client.msi.  

 CCMSetup.exe e seus arquivos de suporte estão localizados no servidor do site do Configuration Manager na pasta **Cliente** da pasta de instalação do Configuration Manager. Essa pasta é compartilhada na rede como **&lt;Nome do Servidor do Site\>\SMS_&lt;Código do Site\>\Cliente**.  

 No prompt de comando, o comando CCMSetup.exe usa o seguinte formato:  

 `CCMSetup.exe [<Ccmsetup properties>] [<client.msi setup properties>]`  

 Exemplo:  

 “CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01”  

 Esse exemplo faz o seguinte:  

-   Especifica o ponto de gerenciamento chamado SMSMP01 para solicitar uma lista de pontos de distribuição para baixar os arquivos de instalação do cliente.  

-   Especifica se a instalação deverá ser interrompida se já houver uma versão do cliente no computador.  

-   Instrui o client.msi a atribuir o cliente ao código do site S01.  

-   Instrui o client.msi a usar o ponto de status de fallback chamado SMSFP01.  

> [!NOTE]  
>  Se uma propriedade contiver espaços, coloque-a entre aspas.  


> [!IMPORTANT]  
>  Se você tiver estendido o esquema do Active Directory para o Configuration Manager, muitas propriedades da instalação do cliente serão publicadas no Active Directory Domain Services e serão lidas automaticamente pelo cliente do Configuration Manager. Para obter uma lista das propriedade de instalação do cliente publicadas nos Serviços de Domínio do Active Directory, veja [Sobre as propriedades de instalação de cliente publicadas nos Serviços de Domínio do Active Directory no System Center Configuration Manager](about-client-installation-properties-published-to-active-directory-domain-services.md)  

##  <a name="ccmsetupexe-command-line-properties"></a>Propriedades de linha de comando do CCMSetup.exe  

### <a name=""></a>/?  

Abre a caixa de diálogo **CCMSetup** mostrando as propriedades de linha de comando para ccmsetup.exe.  

Exemplo: **ccmsetup.exe /?**  

### <a name="sourceltpath"></a>/source:&lt;Caminho\>  

 Especifica o local de download do arquivo. Use um caminho local ou UNC. Os arquivos são baixados usando o protocolo SMB.  Para usar **/source**, a conta de usuário do Windows da instalação do cliente deve ter permissões de Leitura do local.

> [!NOTE]  
>  É possível usar a propriedade **/source** várias vezes em uma linha de comando para especificar locais de download alternativos.  

 Exemplo: **ccmsetup.exe /source:"\\\computer\folder"**  

### <a name="mpltcomputer"></a>/mp:&lt;Computador\>

 Especifica um ponto de gerenciamento de origem para os computadores se conectarem, para que eles possam encontrar o ponto de distribuição mais próximo dos arquivos de instalação. Se não houver pontos de distribuição ou os computadores não conseguirem baixar os arquivos dos pontos de distribuição após 4 horas, os clientes baixarão do ponto de gerenciamento especificado.  

> [!IMPORTANT]  
>  Essa propriedade é usada para especificar um ponto de gerenciamento inicial para os computadores encontrarem uma fonte de download e pode ser qualquer ponto de gerenciamento em qualquer site. Ela não *atribui* o cliente a um ponto de gerenciamento.   

 Os computadores baixarão os arquivos por meio de uma conexão HTTP ou HTTPS, dependendo da configuração da função do sistema de site para as conexões do cliente. O download usa a limitação do BITS, se configurada. Se todos os pontos de distribuição e de gerenciamento estiverem configurados somente para conexões HTTPS do cliente, verifique se o computador cliente tem um certificado de cliente válido.  

Você pode usar a propriedade de linha de comando **/mp** para especificar vários pontos de gerenciamento para que se houver falha na conexão do computador ao primeiro, será feita uma nova tentativa de conexão ao segundo e assim por diante. Ao especificar vários pontos de gerenciamento, separe os valores por ponto-e-vírgula.

Se o cliente se conectar a um ponto de gerenciamento usando HTTPS, normalmente, será necessário especificar o FQDN, não o nome do computador. O valor deve corresponder ao Nome Alternativo da Entidade ou à Entidade do certificado PKI do ponto de gerenciamento. Embora o Configuration Manager dê suporte ao uso de um nome do computador no certificado para conexões na intranet, como uma prática recomendada de segurança, recomenda-se o uso de um FQDN.

Exemplo de uso do nome do computador: `ccmsetup.exe /mp:SMSMP01`  

Exemplo de uso do FQDN: `ccmsetup.exe /mp:smsmp01.contoso.com`  

### <a name="retryltminutes"></a>/retry:&lt;Minutos\>

O intervalo de repetição se o CCMSetup.exe falhar ao baixar os arquivos de instalação.  O CCMSetup continuará tentando até atingir o limite especificado na propriedade **downloadtimeout**.  

Exemplo: `ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

Impede que o CCMSetup seja executado como um serviço, que é o padrão. Quando o CCMSetup é executado como um serviço, ele é executado no contexto da conta Sistema Local do computador, que pode não ter direitos suficientes para acessar os recursos da rede necessários para a instalação. Com **/noservice**, o CCMSetup.exe é executado no contexto da conta de usuário usada para iniciar a instalação. Além disso, se você pretende usar um script para executar o CCMSetup.exe com a propriedade **/service**, o CCMSetup.exe é fechado após a inicialização do serviço e pode não relatar os detalhes da instalação corretamente.   

Exemplo: `ccmsetup.exe /noservice`  

### <a name="service"></a>/service

Especifica que o CCMSetup deverá ser executado como um serviço que usa a conta Sistema Local.  

Exemplo: `ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

Especifica se o software cliente deverá ser desinstalado. Para obter mais informações, consulte [How to manage clients in System Center Configuration Manager](../manage/manage-clients.md).  

Exemplo: `ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

Especifica se a instalação do cliente deverá ser interrompida caso uma versão do cliente já esteja instalada.  

Exemplo: `ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

 Especifica se o CCMSetup deverá forçar o computador cliente a ser reiniciado se isso for necessário para concluir a instalação. Se essa opção não for especificada, o CCMSetup será fechado quando uma reinicialização for necessária e continuará após a próxima reinicialização manual.  

 Exemplo: `CCMSetup.exe /forcereboot`  

### <a name="bitspriorityltpriority"></a>/BITSPriority:&lt;Prioridade\>

 Especifica a prioridade de download, quando os arquivos de instalação do cliente são baixados por meio de uma conexão HTTP. Os valores possíveis são:  

-   FOREGROUND  

-   HIGH  

-   NORMAL  

-   LOW  

 O valor padrão é NORMAL.  

 Exemplo: `ccmsetup.exe /BITSPriority:HIGH`  

### <a name="downloadtimeoutltminutes"></a>/downloadtimeout:&lt;Minutos\>

A duração em minutos que o CCMSetup tentará baixar os arquivos de instalação antes de interromper o processo. O valor padrão é **1440** minutos (1 dia).  

Exemplo: `ccmsetup.exe /downloadtimeout:100`  

### <a name="usepkicert"></a>/UsePKICert

 Quando especificado, o cliente usa um certificado PKI que inclui a autenticação de cliente, se disponível. Se um certificado válido não for encontrado, o cliente usará uma conexão HTTP e um certificado autoassinado, que também é o comportamento quando essa propriedade não é usada.

> [!NOTE]  
>  Em alguns cenários, você não precisa especificar essa propriedade ao instalar um cliente e ainda usar um certificado do cliente. Esses cenários incluem a instalação de um cliente usando a instalação do cliente por push e a instalação do cliente baseada em ponto de atualização de software. No entanto, será necessário especificar essa propriedade sempre que instalar um cliente e usar a propriedade **/mp** para especificar um ponto de gerenciamento que seja configurado para aceitar somente conexões de clientes via HTTPS. Você também deverá especificar essa propriedade ao instalar um cliente para comunicação apenas da Internet, usando a propriedade CCMALWAYSINF=1 (junto às propriedades do ponto de gerenciamento baseado na Internet e o código do site). Para obter mais informações sobre o gerenciamento de clientes baseado em Internet, consulte [Considerações sobre a comunicação do cliente da Internet ou de uma floresta não confiável](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) em [Comunicação entre pontos de extremidade no System Center Configuration Manager](../../plan-design/hierarchy/communications-between-endpoints.md).  

 Exemplo: `CCMSetup.exe /UsePKICert`  

### <a name="nocrlcheck"></a>/NoCRLCheck

 Especifica se um cliente não deverá verificar a CRL (lista de certificados revogados) ao se comunicar por uma conexão HTTPS com um certificado PKI.  

 Quando não especificado, o cliente verifica a CRL antes de estabelecer uma conexão HTTPS.  

 Para obter mais informações sobre a verificação de CRL do cliente, consulte [Planejando a revogação de certificados PKI](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs) em [Planejando a segurança no System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Exemplo: `CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="configltconfiguration-file"></a>/config:&lt;arquivo de configuração\>

Especifica o nome de um arquivo de texto que contém as propriedades de instalação do cliente.

- Se a propriedade **/noservice** do CCMSetup não for especificada, esse arquivo deverá estar localizado na pasta do CCMSetup, que é %Windir%\\Ccmsetup nos sistemas operacionais de 32 e 64 bits.
- Se você especificar a propriedade **/noservice** , esse arquivo será localizado na mesma pasta em que o CCMSetup.exe será executado.  

Exemplo: `CCMSetup.exe /config:&lt;Configuration File Name.txt\>`  

Use o arquivo mobileclienttemplate.tcf na pasta &lt;Configuration Manager directory\>\\bin\\&lt;platform\> do computador do servidor do site para fornecer o formato de arquivo correto. Esse arquivo também contém comentários sobre as seções e como elas são usadas. Especifique as propriedades de instalação do cliente na seção [Instalação do cliente], após o seguinte texto: **Install=INSTALL=ALL**.  

Entrada de seção de exemplo [Instalação do Cliente]: `Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="skipprereqltfilename"></a>/skipprereq:&lt;nome do arquivo\>

 Especifica que CCMSetup.exe não deve instalar o programa de pré-requisitos especificado quando o cliente do Configuration Manager for instalado. Essa propriedade oferece suporte à inserção de diversos valores. Use o caractere ponto-e-vírgula (;) para separar cada valor.  


 Exemplos: `CCMSetup.exe /skipprereq:silverlight.exe` ou `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;Silverlight.exe`  

### <a name="forceinstall"></a>/forceinstall

 Especifica se um cliente existente será desinstalado e um novo cliente será instalado.  

### <a name="excludefeaturesltfeature"></a>/ExcludeFeatures:&lt;recurso\>

Especifica se o CCMSetup.exe não instalará o recurso especificado quando o cliente for instalado.  

Exemplo: `CCMSetup.exe /ExcludeFeatures:ClientUI` não instalará o Centro de Software no cliente.  

> [!NOTE]  
>  Nessa versão, **ClientUI** é o único valor com suporte da propriedade **/ExcludeFeatures** .  

##  <a name="ccmsetupReturnCodes"></a> Códigos de retorno de CCMSetup.exe  
 O comando CCMSetup.exe fornece os códigos de retorno concluídos a seguir. Para solucionar problemas, examine o contexto e detalhes adicionais sobre códigos de retorno no arquivo ccmsetup.log do computador cliente.  

|Código de retorno|Significado|  
|-----------------|-------------|  
|0|Êxito|  
|6|Erro|  
|7|Reinicialização necessária|  
|8|Instalação já em execução|  
|9|Falha na avaliação de pré-requisito|  
|10|Falha na validação do hash do manifesto de Instalação|  

##  <a name="clientMsiProps"></a> Propriedades do Client.msi  
 As propriedades a seguir podem modificar o comportamento da instalação do client.msi. Se você usar o método de instalação por push do cliente, também será possível especificar as propriedades na guia **Cliente** da caixa de diálogo **Propriedades de Instalação por Push do Cliente** .  

### <a name="ccmadmins"></a>CCMADMINS  

Especifica uma ou mais contas de usuário Windows ou grupos para terem acesso às configurações e políticas do cliente. Isso é útil quando o administrador do Configuration Manager não tem credenciais administrativas locais no computador cliente. Especifique uma lista de contas separadas por ponto-e-vírgula.  

Exemplo: `CCMSetup.exe CCMADMINS="Domain\Account1;Domain\Group1"`  

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

Especifica se o computador poderá ser reiniciado após a instalação do cliente, se necessário.  

> [!IMPORTANT]  
>  O computador será reiniciado sem nenhum aviso, mesmo se um usuário estiver conectado.  

Exemplo: **CCMSetup.exe  CCMALLOWSILENTREBOOT**  

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

 Definida como 1 para especificar se o cliente será sempre baseado na Internet e nunca se conectará à intranet. O tipo de conexão do cliente exibe **Sempre Internet**.  

 Essa propriedade deve ser usada em conjunto com CCMHOSTNAME, que especifica o FQDN do ponto de gerenciamento baseado na Internet. Ela também deve ser usada em conjunto com a propriedade /UsePKICert do CCMSetup e com o código do site.  

 Para obter mais informações sobre o gerenciamento de clientes baseado em Internet, consulte [Considerações sobre a comunicação do cliente da Internet ou de uma floresta não confiável](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) em [Comunicação entre pontos de extremidade no System Center Configuration Manager](../../plan-design/hierarchy/communications-between-endpoints.md).  

 Exemplo: `CCMSetup.exe /UsePKICert  CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`  

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

 Especifica a lista de emissores de certificados, que é uma lista de certificados AC (Certificação de Raiz Confiável) em que o site do Configuration Manager confia.  

 Para obter mais emformações sobre a lista de emissores de certificado e como os clientes podem usá-los durante o processo de seleção de certificado, veja [Plannemg for PKI client certificate selection](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection) em [Plan for security em System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Esta é uma correspondência com diferenciação de maiúsculas e minúsculas dos atributos da entidade no certificado de CA raiz. Os atributos podem ser separados por uma vírgula (,) ou por um ponto-e-vírgula (;). Vários certificados de autoridade de certificação raiz podem ser especificados por meio de uma barra de separação. Exemplo:  

 `CCMCERTISSUERS=”CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US &#124; CN=Litware Corporate Root CA; O=Litware, Inc.”`  

> [!TIP]  
>  Faça referência ao arquivo mobileclient.tcf na pasta &lt;Diretório do Configuration Manager\>\bin\\&lt;plataforma\> no computador do servidor do site para copiar **CertificateIssuers=&lt;cadeia de caracteres\>** configurado para o site.  

### <a name="ccmcertsel"></a>CCMCERTSEL

 Especifica os critérios de seleção de certificado se o cliente tem mais de um certificado para a comunicação HTTPS (um certificado válido que inclui a capacidade de autenticação de cliente).  

 É possível pesquisar uma correspondência exata (use **Subject:**) ou uma correspondência parcial (use **SubjectStr:)** no Nome da Entidade ou no Nome Alternativo da Entidade. Exemplos:  

 `CCMCERTSEL="Subject:computer1.contoso.com"` pesquisa um certificado com uma correspondência exata para o nome do computador “computer1.contoso.com” no Nome da Entidade ou no Nome Alternativo da Entidade.  

 `CCMCERTSEL="SubjectStr:contoso.com"` pesquisa um certificado que contém “contoso.com” no Nome da Entidade ou no Nome Alternativo da Entidade.  

 Você também pode usar o OID (identificador de objeto) ou nomes de objetos diferenciados nos atributos do Nome da Entidade ou do Nome Alternativo da Entidade, por exemplo:  

 `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"` pesquisa o atributo da unidade organizacional expresso como um identificador de objeto e os Computadores nomeados.  

 `CCMCERTSEL="SubjectAttr:OU = Computers"` pesquisa o atributo da unidade organizacional expresso como um nome diferenciado e os Computadores nomeados.  

> [!IMPORTANT]  
>  Se você usar a caixa Nome da Entidade, **Subject:** diferenciará maiúsculas de minúsculas e **SubjectStr:** não diferenciará maiúsculas de minúsculas.  
>   
>  Se você usar a caixa Nome Alternativo da Entidade, **Subject:** e **SubjectStr:** não diferenciarão maiúsculas de minúsculas.  

 A lista completa de atributos que você pode usar para seleção de certificado está listada na [Valores de atributo com suporte para os critérios de seleção de certificado PKI](#BKMK_attributevalues).  

 Se mais de um certificado corresponder à pesquisa e a propriedade CCMFIRSTCERT for definida como 1, o certificado com o período de validade mais longo será selecionado.  

### <a name="ccmcertstore"></a>CCMCERTSTORE

 Especifica um nome alternativo de repositório de certificados se o certificado do cliente para HTTPS não está localizado no repositório de certificados padrão **Pessoal** no repositório do Computador.  

 Exemplo: `CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

  Habilita o log de depuração. Os valores podem ser definidos como 0 (desativado, padrão) ou 1 (ativado). Isso faz com que o cliente registre informações de baixo nível para solução de problemas. Como prática recomendada, evite usar essa propriedade em sites de produção, pois pode ocorrer registro em log excessivo, dificultando a localização de informações importantes nos arquivos de log. CCMENABLELOGGING também deve ser definido como TRUE para habilitar o log de depuração.  

  Exemplo: `CCMSetup.exe CCMDEBUGLOGGING=1`  

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

  Por padrão, defina como TRUE para habilitar o log. Os arquivos de log são armazenados na pasta **Logs** da pasta de instalação do cliente do Configuration Manager. Por padrão, essa pasta é %Windir%\CCM\Logs.  

  Exemplo: `CCMSetup.exe CCMENABLELOGGING=TRUE`  

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL  

 A frequência na qual a ferramenta de avaliação de integridade do cliente (ccmeval.exe) é executada. Pode ser de **1** a **1440** minutos. Por padrão, é executada uma vez por dia.  

### <a name="ccmevalhour"></a>CCMEVALHOUR

 A hora em que a ferramenta de avaliação de integridade do cliente (ccmeval.exe) é executada, entre **0** (meia-noite) e **23** (23h). É executada à meia-noite por padrão.  

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

 Se definida como 1, essa propriedade especifica que o cliente deve selecionar o certificado PKI com o período de validade mais longo. Essa configuração poderá ser necessária se você estiver usando Proteção de Acesso à Rede com imposição IPsec.  

 Exemplo: `CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`  

### <a name="ccmhostname"></a>CCMHOSTNAME

 Especifica o FQDN do ponto de gerenciamento baseados na Internet, se o cliente for gerenciado pela Internet.  

 Não especifique essa opção com a propriedade de instalação SMSSITECODE=AUTO. Clientes baseados na Internet devem ser atribuídos diretamente a seus sites baseados na Internet.  

 Exemplo: `CCMSetup.exe  /UsePKICert CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

### <a name="ccmhttpport"></a>CCMHTTPPORT

 Especifica a porta que o cliente deve usar ao se comunicar por HTTP com servidores do sistema de site. Definida como a Porta 80 por padrão.  

 Exemplo: `CCMSetup.exe CCMHTTPPORT=80`  

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

Especifica a porta que o cliente deve usar ao se comunicar por HTTPS com servidores do sistema de site. Definida como a Porta 443 por padrão.  

Exemplo: `CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`  

### <a name="ccminstalldir"></a>CCMINSTALLDIR

 Identifica a pasta na qual os arquivos do cliente do Configuration Manager são instalados, *%Windir%*\CCM por padrão. Independentemente do local em que esses arquivos são instalados, o arquivo Ccmcore.dll é sempre instalado na pasta *%Windir%\System32*. Além disso, em sistemas operacionais de 64 bits, uma cópia do arquivo Ccmcore.dll sempre é instalada na pasta *%Windir%*\SysWOW64 para dar suporte aos aplicativos de 32 bits que usam a versão de 32 bits das APIs do cliente do Configuration Manager por meio do SDK (Software Developer Kit) do Configuration Manager.  

 Exemplo: `CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`  

### <a name="ccmloglevel"></a>CCMLOGLEVEL

Especifica o nível de detalhe a ser gravado nos arquivos de log do Configuration Manager. Especifique um inteiro de 0 a 3, em que 0 corresponde ao log mais detalhado e 3 registra apenas os erros. O padrão é 1.  

Exemplo: `CCMSetup.exe CCMLOGLEVEL=3`  

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Quando um arquivo de log do Configuration Manager chega a 250000 bytes de tamanho (ou ao valor especificado pela propriedade CCMLOGMAXSIZE), ele é renomeado como um backup e um novo arquivo de log é criado.  

Essa propriedade especifica quantas versões anteriores do arquivo de log serão mantidas. O valor padrão é 1. Se o valor for definido como 0, nenhum arquivo de log antigo será mantido.  

Exemplo: `CCMSetup.exe CCMLOGMAXHISTORY=0`  

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

O tamanho máximo do arquivo de log em bytes. Quando um log chega ao tamanho especificado, ele é renomeado como um arquivo de histórico e um novo arquivo é criado. Essa propriedade deve ser definida como pelo menos 10000 bytes. O valor padrão é 250000 bytes.  

Exemplo: `CCMSetup.exe CCMLOGMAXSIZE=300000`  

### <a name="disablesiteopt"></a>DISABLESITEOPT

 Se definido como TRUE, desabilita a capacidade de os usuários finais com credenciais administrativas no computador cliente alterarem o site atribuído do Configuration Manager em **Configuration Manager** no Painel de Controle do cliente.  

 Exemplo: **CCMSetup.exe DISABLESITEOPT=TRUE**  

### <a name="disablecacheopt"></a>DISABLECACHEOPT

Se definido como TRUE, desabilitará a capacidade de os usuários finais com credenciais administrativas no computador cliente alterarem as configurações da pasta de cache do cliente para o cliente do Configuration Manager usando o Configuration Manager no Painel de Controle do computador cliente.  

Exemplo: `CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

 Especifica um domínio DNS de clientes para localizar os pontos de gerenciamento publicados no DNS. Quando um ponto de gerenciamento é localizado, ele informa o cliente sobre outros pontos de gerenciamento na hierarquia. Isso significa que o ponto de gerenciamento localizado usando a publicação de DNS não precisa ser do site do cliente, mas pode ser qualquer ponto de gerenciamento na hierarquia.  

> [!NOTE]  
>  Você não precisará especificar essa propriedade se o cliente estiver no mesmo domínio que o ponto de gerenciamento publicado. Nesse caso, o domínio do cliente é usado automaticamente para pesquisar pontos de gerenciamento no DNS.  

 Para obter mais informações sobre a publicação de DNS como um método de local de serviço para clientes do Configuration Manager, consulte [Local do serviço e como os clientes determinam seu ponto de gerenciamento atribuído](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location) em [Entender como os clientes encontram serviços e recursos do site para o System Center Configuration Manager](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

> [!NOTE]  
>  Por padrão, a publicação de DNS não está habilitada no Configuration Manager.  

 Exemplo: `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`  

### <a name="fsp"></a>FSP

Especifica o ponto de status de fallback que recebe e processa mensagens de estado enviadas por computadores cliente do Configuration Manager.  

Para obter mais informações sobre o ponto de status de fallback, consulte [Determinar se você precisa de um ponto de status de fallback](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients#determine-if-you-need-a-fallback-status-point).  

Exemplo: `CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

 Especifica se a presença da versão mínima necessária do App-V (Microsoft Application Virtualization) não é verificada antes da instalação do cliente.  

> [!IMPORTANT]  
>  Se instalar o cliente do Configuration Manager sem instalar o App-V, você não poderá implantar aplicativos virtuais.  

 Exemplo: `CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`  

### <a name="notifyonly"></a>NOTIFYONLY

Especifica se o status do cliente relatará, mas não corrigirá os problemas encontrados no cliente.  

Exemplo: `CCMSetup.exe NOTIFYONLY=TRUE`  

Para obter mais informações, consulte [How to configure client status in System Center Configuration Manager](configure-client-status.md).  

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

 Se um cliente do Configuration Manager tiver a chave de raiz confiável incorreta do Configuration Manager e não puder contatar um ponto de gerenciamento confiável para receber a nova chave de raiz confiável, será necessário remover a chave de raiz confiável antiga manualmente usando essa propriedade. Essa situação poderá ocorrer quando um cliente for movido de uma hierarquia de site para outra. Essa propriedade se aplica a clientes que usam a comunicação de cliente por HTTP e HTTPS.  

 Exemplo: `CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

Habilita a atribuição automática de site para as atualizações do cliente quando usado com [SMSSITECODE](#smssitecode)=AUTO.

Exemplo: `CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

Especifica o local da pasta cache do cliente no computador cliente, o qual armazena arquivos temporários. Por padrão, o local é *%Windir \ccmcache*.  

Exemplo: `CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

Essa propriedade pode se usada em conjunto com a propriedade SMSCACHEFLAGS para controlar o local da pasta de cache do cliente.  

Exemplo: `CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE` instala a pasta de cache do cliente na maior unidade de disco do cliente disponível.  

### <a name="smscacheflags"></a>SMSCACHEFLAGS

Especifica ainda mais detalhes sobre a instalação da pasta cache do cliente. Você pode usar propriedades SMSCACHEFLAGS individualmente ou em combinação, separadas por ponto-e-vírgula. Se essa propriedade não for especificada, a pasta cache do cliente será instalada de acordo com a propriedade SMSCACHEDIR, a pasta não será compactada e o valor SMSCACHESIZE será usado como o tamanho em MB da pasta.  

Essa configuração será ignorada quando um cliente existente for atualizado.  

Propriedades:  

-   PERCENTDISKSPACE: especifica o tamanho da pasta como um percentual do espaço total em disco. Se você especificar essa propriedade, será necessário especificar a propriedade SMSCACHESIZE como o valor da porcentagem a ser usado.  

-   PERCENTFREEDISKSPACE: especifica o tamanho da pasta como um percentual do espaço em disco livre. Se você especificar essa propriedade, será necessário especificar a propriedade SMSCACHESIZE como o valor da porcentagem a ser usado. Por exemplo, se o disco tiver 10 MB livres e a propriedade SMSCACHESIZE for especificada como 50, o tamanho da pasta será definido como 5 MB. Não é possível usar essa propriedade com a propriedade PERCENTDISKSPACE.  

-   MAXDRIVE: especifica que a pasta deve ser instalada no maior disco disponível. Esse valor será ignorado se for especificado um caminho com a propriedade SMSCACHEDIR.  

-   MAXDRIVESPACE: especifica que a pasta deve ser instalada na unidade de disco com mais espaço livre. Esse valor será ignorado se for especificado um caminho com a propriedade SMSCACHEDIR.  

-   NTFSONLY: especifica se a pasta pode ser instalada somente em unidades de disco NTFS. Esse valor será ignorado se for especificado um caminho com a propriedade SMSCACHEDIR.  

-   COMPRESS: especifica se a pasta deve ser armazenada em um formato compactado.  

-   FAILIFNOSPACE: especifica que o software cliente deve ser removido se não houver espaço suficiente para instalar a pasta.  

Exemplo: `CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`  


### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> A partir do Configuration Manager versão 1606, novas configurações de cliente estão disponíveis para especificar o tamanho da pasta de cache do cliente. O acréscimo dessas configurações de cliente substitui com eficiência o uso de SMSCACHESIZE como uma propriedade client.msi para especificar o tamanho do cache do cliente. Para obter mais informações, consulte as [configurações de cliente para tamanho de cache](about-client-settings.md#client-cache-settings).  

Para o 1602 e anteriores, SMSCACHESIZE especifica o tamanho da pasta cache do cliente em megabytes (MB) ou como uma percentual quando usada com a propriedade PERCENTDISKSPACE ou PERCENTFREEDISKSPACE. Se essa propriedade não for definida, a pasta usará por padrão o tamanho máximo de 5120 MB. O menor valor que pode ser especificado é 1 MB.  

> [!NOTE]  
>  Se um novo pacote que deve ser baixado fizer com que a pasta exceda o tamanho máximo e se a pasta não puder ser removida para criar espaço suficiente disponível, o download do pacote falhará e o programa ou o aplicativo não será executado.  

Essa configuração será ignorada quando você atualizar um cliente existente e quando o cliente baixar as atualizações de software.  

Exemplo: `CCMSetup.exe SMSCACHESIZE=100`  

> [!NOTE]  
>  Se você reinstalar um cliente, você não poderá usar as propriedade de instalação SMSCACHESIZE ou SMSCACHEFLAGS para definir o tamanho do cache para que seja menor do que era anteriormente. Se você tentar fazer isso, o valor será ignorado e o tamanho do cache será definido automaticamente com o tamanho anterior.  

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

Especifica o local e a ordem em que o instalador do Configuration Manager verificará as definições de configuração. A propriedade é uma cadeia de caracteres que contém um ou mais caracteres, cada um definindo uma fonte de configuração específica. Use os valores de caractere R, P, M e U, sozinhos ou em combinação:  

-   R: verificar as definições de configurações no Registro.  

   Para obter mais informações, consulte [informações sobre como armazenar propriedades de instalação do cliente no Registro](https://technet.microsoft.com/library/gg712298.aspx#BKMK_Provision).  

-   P: verificar as definições de configuração nas propriedades de instalação fornecidas no prompt de comando.  

-   M: verificar as configurações existentes ao atualizar um cliente mais antigo com o software cliente do Configuration Manager.  

-   U: atualizar o cliente instalado para uma versão mais recente (e usa o código do site atribuído).  

 Por padrão, a instalação do cliente usa `PU` para verificar primeiro as propriedades de instalação e depois as configurações existentes.  

 Exemplo: `CCMSetup.exe SMSCONFIGSOURCE=RP`  

### <a name="smsdirectorylookup"></a>SMSDIRECTORYLOOKUP

 Especifica se o cliente pode usar o WINS (serviço de cadastramento na Internet do Windows) para localizar um ponto de gerenciamento que aceite conexões HTTP. Os clientes usam esse método quando não conseguem encontrar um ponto de gerenciamento nos Serviços de Domínio Active Directory ou no DNS.  

 Essa propriedade não afeta o uso do WINS pelo cliente para a resolução de nomes.  

 Você pode configurar dois modos diferentes para essa propriedade:  

-   NOWINS: essa é a configuração mais segura para essa propriedade e impede que os clientes encontrem um ponto de gerenciamento no WINS.  Quando você usar essa configuração, os clientes deverão ter um método alternativo para localizar um ponto de gerenciamento na intranet, como os Serviços de Domínio Active Directory ou usando a publicação DNS.  

-   WINSSECURE (padrão): nesse modo, um cliente que usa a comunicação HTTP pode usar o WINS para localizar um ponto de gerenciamento. No entanto, o cliente deverá ter uma cópia da chave de raiz confiável antes de se conectar com êxito a ponto de gerenciamento. Para obter mais emformações, veja [Plannemg for the Trusted Root Key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) em [Plan for security em System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  


 Exemplo: `CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  

### <a name="smsmp"></a>SMSMP

Especifica um ponto de gerenciamento inicial para o cliente do Configuration Manager usar.  

> [!IMPORTANT]  
>  Se o ponto de gerenciamento aceitar somente conexões de cliente por HTTPS, será necessário prefixar o nome do ponto de gerenciamento com https://.  

Exemplo: `CCMSetup.exe SMSMP=smsmp01.contoso.com`

Exemplo: `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  

### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

 Especifica a chave de raiz confiável do Configuration Manager quando ela não pode ser recuperada do Active Directory Domain Services. Essa propriedade se aplica a clientes que usam a comunicação de cliente por HTTP e HTTPS. Para obter mais emformações, veja [Plannemg for the Trusted Root Key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) em [Plan for security em System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Exemplo: `CCMSetup.exe SMSPUBLICROOTKEY=&lt;key\>`  

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

 Usada para reinstalar a chave de raiz confiável do Configuration Manager. Especifica o caminho completo e o nome do arquivo para um arquivo que contém a chave de raiz confiável. Essa propriedade se aplica a clientes que usam a comunicação de cliente por HTTP e HTTPS. Para obter mais emformações, veja [Plannemg for the Trusted Root Key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) em [Plan for security em System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Exemplo: “CCMSetup.exe SMSROOTKEYPATH=&lt;Caminho completo e nome do arquivo\>`”  

### <a name="smssigncert"></a>SMSSIGNCERT

 Especifica o caminho completo e o nome do arquivo .cer do certificado autoassinado exportado do servidor do site.  

 Esse certificado é armazenado no repositório de certificados **SMS** e tem como nome da Entidade **Servidor do Site** e como nome amigável **Certificado de Autenticação do Servidor do Site**.  

 Exemplo: **CCMSetup.exe /UsePKICert SMSSIGNCERT=&lt;Caminho completo e nome do arquivo\>**  

### <a name="smssitecode"></a>SMSSITECODE

 Especifica o site do Configuration Manager ao qual atribuir o cliente do Configuration Manager. Isso pode ser um código do site de três caracteres ou a palavra AUTO. Se AUTO for especificado, ou se essa propriedade não for especificada, o cliente tentará determinar sua atribuição de site do Configuration Manager usando o Active Directory Domain Services ou um ponto de gerenciamento especificado. Para habilitar AUTO para atualizações de cliente, você também deve definir [SITEREASSIGN](#sitereassign) como TRUE.    

> [!NOTE]  
>  Não use AUTOMÁTICO se você também especificar o ponto de gerenciamento da Internet (CCMHOSTNAME). Nesse caso, você deve atribuir diretamente o cliente ao site.  

 Exemplo: `CCMSetup.exe SMSSITECODE=XZY`  

##  <a name="BKMK_attributevalues"></a> Valores de atributo com suporte para os critérios de seleção de certificado PKI  
 O Configuration Manager dá suporte aos seguintes valores de atributo dos critérios de seleção de certificado PKI:  

|Atributo OID|Atributo de nome diferenciado|Definição de atributo|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Componente do domínio|  
|1.2.840.113549.1.9.1|E ou email|Endereço de email|  
|2.5.4.3|CN|Nome comum|  
|2.5.4.4|SN|Nome da entidade|  
|2.5.4.5|SERIALNUMBER|Número de série|  
|2.5.4.6|C|Código do país|  
|2.5.4.7|L|Localidade|  
|2.5.4.8|S ou ST|Nome do estado ou província|  
|2.5.4.9|RUA|Endereço|  
|2.5.4.10|O|Nome da organização|  
|2.5.4.11|OU|Unidade organizacional|  
|2.5.4.12|T ou Título|Título|  
|2.5.4.42|G ou GN ou GivenName|Nome|  
|2.5.4.43|I ou Iniciais|Iniciais|  
|2.5.29.17|(nenhum valor)|Nome alternativo da entidade|  
