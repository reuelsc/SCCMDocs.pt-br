---
title: Implantar clientes UNIX/Linux
titleSuffix: Configuration Manager
description: Saiba como implantar clientes em um servidor UNIX ou Linux no Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15a4e323-9f42-4fea-bb14-f2b905d1f77c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 855869db6d127999218964d06e50179c70efed0a
ms.sourcegitcommit: d8d142044586a53709b4478ad945f714737c8d6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58524091"
---
# <a name="how-to-deploy-clients-to-unix-and-linux-servers-in-configuration-manager"></a>Como implantar clientes em servidores UNIX e Linux no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

> [!Important]  
> A partir da versão 1902, o Configuration Manager não dá suporte a clientes Linux ou UNIX. 
> 
> Considere o Gerenciamento do Microsoft Azure para gerenciar servidores Linux. As soluções do Azure têm amplo suporte para Linux que, na maioria dos casos, supera a funcionalidade do Configuration Manager, incluindo o gerenciamento de patches de ponta a ponta para o Linux.


Antes de poder gerenciar um servidor Linux ou UNIX com o Configuration Manager, é necessário instalar o cliente do Configuration Manager para Linux e UNIX em cada servidor Linux ou UNIX. Você pode executar a instalação do cliente manualmente em cada computador ou usar um script de shell que instala o cliente remotamente. O Configuration Manager não dá suporte para o uso de instalação do cliente por push para servidores Linux ou UNIX. Como opção, você pode configurar um Runbook para o System Center Orchestrator automatizar a instalação do cliente no servidor Linux ou UNIX.  

 Independentemente do método de instalação que você usar, o processo de instalação requer o uso de um script chamado **install** para gerenciar o processo de instalação. Esse script será incluído quando você baixar o cliente para Linux e UNIX.  

 O script de instalação do cliente do Configuration Manager para Linux e UNIX dá suporte a propriedades de linha de comando. Algumas propriedades de linha de comando são necessárias, enquanto outras são opcionais. Por exemplo, quando você instala o cliente, você deve especificar um ponto de gerenciamento do site que é usado pelo servidor Linux ou UNIX para o contato inicial com o site. Para obter uma lista completa das propriedades de linha de comando, confira as [propriedades de linha de comando para instalar o cliente em servidores Linux e UNIX](#BKMK_CmdLineInstallLnUClient).  

 Depois de instalar o cliente, é possível especificar as Configurações do Cliente no console do Configuration Manager para configurar o agente cliente da mesma maneira que faria com clientes baseados em Windows. Para obter mais informações, consulte  [Configurações do cliente para servidores Linux e UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ClientSettingsforLnU).  

##  <a name="BKMK_AboutInstallPackages"></a> Informações sobre pacotes de instalação do cliente e o agente Universal  
 Para instalar o cliente para Linux e UNIX em uma plataforma específica, você deve usar o pacote de instalação do cliente aplicável para o computador no qual você instala o cliente. Pacotes de instalação do cliente aplicáveis são incluídos como parte do download de cada cliente no [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184). Além dos pacotes de instalação do cliente, o download do cliente inclui o script **install** que gerencia a instalação do cliente em cada computador.  

 Ao instalar um cliente, você pode usar as mesmas propriedades de processo e de linha de comando, independentemente do pacote de instalação de cliente que você usar.  

 Para obter informações sobre os sistemas operacionais, as plataformas e os pacotes de instalação do cliente aos quais cada versão do cliente do Configuration Manager para Linux e UNIX dá suporte, consulte [Servidores Linux e UNIX](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#linux-and-unix-servers).  

##  <a name="BKMK_InstallLnUClient"></a> Instalar o cliente em servidores Linux e UNIX  
 Para instalar o cliente para Linux e UNIX, você pode executar um script em cada computador Linux ou UNIX. O script é nomeado **instalar** e oferece suporte às propriedades de linha de comando que modificam o comportamento da instalação e referenciam o pacote de instalação do cliente. O pacote de instalação de cliente e script de instalação deve estar localizado no cliente. O pacote de instalação de cliente contém os arquivos do cliente do Configuration Manager para um sistema operacional e para uma plataforma Linux ou UNIX específica.
Cada pacote de instalação de cliente contém todos os arquivos necessários para concluir a instalação do cliente e, ao contrário dos computadores baseados em Windows, ele não baixa arquivos adicionais de um ponto de gerenciamento ou de outro local de origem.  

 Depois de instalar o cliente do Configuration Manager para Linux e UNIX, não é necessário reinicializar o computador. Assim que a instalação do software for concluída, o cliente está operacional. Se você reinicializar o computador, o cliente do Configuration Manager reiniciará automaticamente.  

 O cliente instalado é executado com credenciais raiz. São necessárias credenciais raiz para coletar o inventário de hardware e realizar as implantações de software.  

 Use o seguinte formato de comando:  

 `./install -mp <computer> -sitecode <sitecode> <property #1> <property #2> <client installation package>`  

-   `install` é o nome do arquivo de script que instala o cliente para Linux e UNIX. Esse arquivo é fornecido com o software cliente.  

-   `-mp <computer>` especifica o ponto de gerenciamento inicial que é usado pelo cliente. Exemplo: `smsmp.contoso.com`  

-   `-sitecode <site code>` especifica o código do site ao qual o cliente é atribuído. Exemplo: `S01`  

-   `<property #1> <property #2>` especifica as propriedades de linha de comando a serem usadas com o script de instalação.  

    > [!NOTE]  
    >  Confira mais informações nas [propriedades de linha de comando para instalação do cliente em servidores Linux e UNIX](#BKMK_CmdLineInstallLnUClient).  

-   **pacote de instalação do cliente** é o nome do pacote .tar de instalação do cliente para o sistema operacional do computador, versão e arquitetura da CPU. O arquivo de. tar de instalação do cliente deve ser especificado pela última. Exemplo: `ccm-Universal-x64.<build>.tar`  

###  <a name="BKMK_ToInstallLnUClinent"></a> Para instalar o cliente do Configuration Manager em servidores Linux e UNIX  

1.  Em um computador com Windows, [baixe o arquivo do cliente apropriado para o servidor Linux ou UNIX](https://go.microsoft.com/fwlink/?LinkID=525184) você deseja gerenciar.  

2.  Execute o arquivo autoextraível .exe no computador com Windows para extrair o script de instalação e o arquivo .tar de instalação do cliente.  

3.  Copie o script **install** e o arquivo .tar em uma pasta no servidor que deseja gerenciar.  

4.  No servidor UNIX ou Linux, execute o seguinte comando para habilitar o script a ser executado como um programa: `chmod +x install`  

    > [!IMPORTANT]  
    >  Você deve usar credenciais raiz para instalar o cliente.  

5.  Em seguida, execute o seguinte comando para instalar o cliente do Configuration Manager: `./install -mp <hostname> -sitecode <code> ccm-Universal-x64.<build>.tar`  

     Quando você digitar esse comando, use propriedades de linha de comando adicionais que você precisar. Confira uma lista das propriedades de linha de comando em [Propriedades de linha de comando para instalação do cliente em servidores Linux e UNIX](#BKMK_CmdLineInstallLnUClient)  

6.  Após o script ser executado, valide a instalação ao examinar o arquivo **/var/opt/microsoft/scxcm.log** . Além disso, é possível confirmar se o cliente está instalado e se comunicando com o site exibindo detalhes do cliente no nó **Dispositivos** do workspace **Ativos e Conformidade** do console do Configuration Manager.  

###  <a name="BKMK_CmdLineInstallLnUClient"></a> Propriedades de linha de comando para instalação do cliente em servidores Linux e UNIX  
 As seguintes propriedades estão disponíveis para modificar o comportamento do script de instalação:  

> [!NOTE]  
>  Use a propriedade `-h` para exibir essa lista de propriedades com suporte.  

-   `-mp <server FQDN>`  

     Necessário. Especifica por FQDN, o servidor de ponto de gerenciamento que o cliente usa como um ponto inicial de contato.  

    > [!IMPORTANT]  
    >  Essa propriedade não especifica o ponto de gerenciamento ao qual o cliente será atribuído após a instalação.  

    > [!NOTE]  
    >  Quando você usa a propriedade `-mp` para especificar um ponto de gerenciamento que está configurado para aceitar somente conexões de cliente HTTPS, você também deve usar a propriedade `-UsePKICert`.  

-   `-sitecode <sitecode>`  

     Necessário. Especifica o site primário do Configuration Manager ao qual atribuir o cliente do Configuration Manager. Exemplo: `-sitecode S01`  

-   `-fsp <server_FQDN>`  

     Opcional. Especifica o FQDN, o servidor de ponto de status de fallback que o cliente usa para enviar mensagens de estado. Para saber mais, confira as informações sobre como [determinar se você precisa de um ponto de status de fallback](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients#determine-if-you-need-a-fallback-status-point).  

-   `-dir <directory>`  

     Opcional. Especifica um local alternativo para instalar os arquivos do cliente do Configuration Manager. Por padrão, o cliente é instalado no seguinte local: `/opt/microsoft`  

-   `-nostart`  

     Opcional. Impede a inicialização automática do serviço de cliente do Configuration Manager, **ccmexec.bin**, após concluir a instalação do cliente.  

     Depois que o cliente é instalado, você deve iniciar o serviço de cliente manualmente.  

     Por padrão, o serviço de cliente é iniciado depois de concluir a instalação do cliente, e cada vez que o computador for reiniciado.  

-   `-clean`  

     Opcional. Especifica a remoção de todos os arquivos do cliente e dados de um cliente instalado anteriormente para Linux e UNIX, antes de inicia a instalação. Essa ação remove o banco de dados do cliente e o repositório de certificados.  

-   `-keepdb`  

     Opcional. Especifica que o banco de dados do cliente local é mantido e reutilizado ao reinstalar um cliente. Por padrão, quando você reinstalar um cliente esse banco de dados é excluído.  

-   `-UsePKICert <parameter>`  

     Opcional. Especifica o nome de arquivo e caminho completo para um certificado x. 509 PKI no formato de certificado padrão de chave pública (PKCS #12). Esse certificado é usado para autenticação do cliente. Se um certificado não for especificado durante a instalação e você precisará adicionar ou alterar um certificado, use o utilitário **certutil** . Confira mais informações em [Como gerenciar certificados no cliente para Linux e UNIX](/sccm/core/clients/manage/manage-clients-for-linux-and-unix-servers#BKMK_ManageLinuxCerts).  

     Ao usar o `-UsePKICert`, também é necessário que você forneça a senha associada ao arquivo PKCS#12 usando o parâmetro de linha de comando `-certpw`.  

     Se você não usar essa propriedade para especificar um certificado PKI, o cliente usará um certificado autoassinado e todas as comunicações com sistemas de site serão via HTTP.  

     Se você especificar um certificado inválido na linha de comando de instalação de cliente, nenhum erro será retornado. A validação do certificado ocorre depois que o cliente é instalado. Quando o cliente é iniciado, os certificados são validados com o ponto de gerenciamento. Se um certificado não passar na validação, a seguinte mensagem será exibida no **scxcm.log**: **Falha ao validar o certificado de ponto de gerenciamento**. O local do arquivo de log padrão é:  **/var/opt/microsoft/scxcm.log**.  

     > [!NOTE]  
     > É necessário que você especifique essa propriedade ao instalar um cliente e usar a propriedade `-mp` para especificar um ponto de gerenciamento que é configurado para aceitar somente conexões de clientes via HTTPS.  

     Exemplo: `-UsePKICert <full path and filename> -certpw <password>`  

-   `-certpw <parameter>`  

     Opcional. Especifica a senha associada com o arquivo PKCS#12 que você especificou usando a propriedade `-UsePKICert`.  

     Exemplo: `-UsePKICert <full path and filename> -certpw <password>`  

-   `-NoCRLCheck`  

     Opcional. Especifica que um cliente não deveria verificar a lista de certificados revogados (CRL) ao se comunicar via HTTPS usando um certificado PKI. Quando essa opção não for especificada, o cliente verificará a CRL antes de estabelecer uma conexão HTTPS usando certificados PKI. Para obter mais informações sobre a verificação de CRL do cliente, consulte Planejando a revogação de certificados PKI.  

     Exemplo: `-UsePKICert <full path and filename> -certpw <password> -NoCRLCheck`  

-   `-rootkeypath <file location>`  

     Opcional. Especifica o nome de arquivo e caminho completo para a chave raiz confiável do Configuration Manager. A chave de raiz confiável do Configuration Manager fornece um mecanismo que os clientes Linux e UNIX usam para verificar se estão conectados a um sistema de sites que pertence à hierarquia correta.  

     Se você não especificar a chave raiz confiável na linha de comando, o cliente confiará no primeiro ponto de gerenciamento com o qual ele se comunica e recuperará automaticamente a chave raiz confiável do ponto de gerenciamento.  

     Para obter mais informações, consulte  [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

     Exemplo: `-rootkeypath <full path and filename>`  

-   `-httpport <port>`  

     Opcional. Especifica a porta configurada nos pontos de gerenciamento que o cliente usa ao se comunicar com pontos de gerenciamento via HTTP. Se a porta não for especificada, será usado o valor padrão de 80.  

     Exemplo: `-httpport 80`  

-   `-httpsport <port>`  

     Opcional. Especifica a porta configurada nos pontos de gerenciamento que o cliente usa ao se comunicar com pontos de gerenciamento via HTTPS. Se a porta não for especificada, será usado o valor padrão de 443.  

     Exemplo: `-UsePKICert <full path and certificate name> -httpsport 443`  

-   `-ignoreSHA256validation`  

     Opcional. Especifica que a instalação do cliente ignora a validação do SHA-256. Use essa opção ao instalar o cliente em sistemas operacionais que não foram lançados com uma versão do OpenSSL que dá suporte a SHA-256. Para saber mais, confira as informações [sobre os sistemas operacionais Linux e UNIX que não dão suporte a SHA-256](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256).  

-   `-signcertpath <file location>`  

     Opcional. Especifica o caminho completo e **. cer** nome do arquivo do certificado autoassinado exportado no servidor do site. Se os certificados PKI não estiverem disponíveis, o servidor do site do Configuration Manager gerará automaticamente certificados autoassinados.  

     Esses certificados são usados para validar que as políticas do cliente baixadas do ponto de gerenciamento foram enviadas do local desejado. Se um certificado autoassinado não for especificado durante a instalação ou se você precisar alterar o certificado, use o utilitário **certutil** . Confira mais informações em [Como gerenciar certificados no cliente para Linux e UNIX](/sccm/core/clients/manage/manage-clients-for-linux-and-unix-servers#BKMK_ManageLinuxCerts).  

     Esse certificado é recuperado por meio do repositório de certificados **SMS** e tem como nome da Entidade **Servidor do Site** e como nome amigável **Certificado de Autenticação do Servidor do Site**.  

     Se essa opção não for especificada durante a instalação, os clientes Linux e UNIX confiarão no primeiro ponto de gerenciamento com o qual eles se comunicarem. Eles recuperam automaticamente o certificado de autenticação do ponto de gerenciamento.  

     Exemplo: `-signcertpath <full path and file name>`  

-   `-rootcerts`  

     Opcional. Especifica certificados PKI adicionais para importar aqueles que não fazem parte de uma hierarquia de autoridade de certificação de pontos de gerenciamento (CA). Se você especificar vários certificados na linha de comando, eles devem ser delimitados por vírgulas.  

     Use esta opção se você usar certificados de cliente PKI que não são encadeados a um certificado de autoridade de certificação raiz que é confiável para os pontos de gerenciamento dos seus sites. Os pontos de gerenciamento rejeitarão o cliente se o certificado do cliente não estiver encadeado a um certificado raiz confiável na lista de emissores de certificado do site.  

     Se você não usar essa opção, o cliente Linux e UNIX verificará a hierarquia de confiança usando somente o certificado na opção `-UsePKICert`.  

     Exemplo: `-rootcerts <full path and file name>,<full path and file name>`  

###  <a name="BKMK_UninstallLnUClient"></a> Desinstalando o cliente dos servidores Linux e UNIX  
 Para desinstalar o cliente do Configuration Manager para Linux e UNIX, use o utilitário de desinstalação, **desinstalar**. Por padrão, esse arquivo está localizado no **/opt/microsoft/SMS/bin/** pasta no computador cliente. Este comando de desinstalação não oferece suporte a nenhum parâmetro de linha de comando e removerá todos os arquivos relacionados ao software cliente do servidor.  

 Para desinstalar o cliente, use a seguinte linha de comando: **/opt/microsoft/configmgr/bin/uninstall**  

 Não é necessário reinicializar o computador depois de desinstalar o cliente do Configuration Manager no Linux e UNIX.  

##  <a name="BKMK_ConfigLnUClientCommuincations"></a> Configurar portas de solicitação do cliente para Linux e UNIX  
 Semelhante a clientes baseados em Windows, o cliente do Configuration Manager para Linux e UNIX usa HTTP e HTTPS para se comunicar com sistemas de sites do Configuration Manager. As portas que o cliente do Configuration Manager usa para se comunicar são conhecidas como portas da solicitação.  

 Quando você instala o cliente do Configuration Manager para Linux e UNIX, é possível alterar as portas de solicitação padrão dos clientes, especificando as propriedades de instalação **-httpport** e **-httpsport**. Quando você não especificar a propriedade de instalação e um valor personalizado, o cliente usará os valores padrão. Os valores padrão são **80** para tráfego HTTP e **443** para tráfego HTTPS.  

 Depois de instalar o cliente, você não poderá alterar sua configuração de porta de solicitação. Em vez disso, para alterar a configuração de porta, você deve reinstalar o cliente e especifique a nova configuração de porta. Quando você reinstalar o cliente para alterar os números de porta de solicitação, execute o comando **instalar**, semelhante à nova instalação do cliente, mas use a propriedade de linha de comando adicional do **-keepdb**. Essa opção instrui a instalação a manter o banco de dados e os arquivos do cliente, inclusive o armazenamento GUID e o repositório de certificados.  

 Para obter mais informações sobre números de porta de comunicação de cliente, consulte [Como configurar portas de comunicação do cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md).  

##  <a name="BKMK_ConfigClientMP"></a> Configurar o cliente para Linux e UNIX localizar pontos de gerenciamento  
 Ao instalar o cliente do Configuration Manager para Linux e UNIX, é necessário especificar um ponto de gerenciamento para ser usado como um ponto inicial de contato.  

 O cliente do Configuration Manager para Linux e UNIX entra em contato com esse ponto de gerenciamento no momento em que o cliente é instalado. Se o cliente falhar no contato com o ponto de gerenciamento, o software cliente continuará tentando até obter êxito.  

 Para obter mais informações sobre como os clientes localizam os pontos de gerenciamento, consulte [Localizando pontos de gerenciamento](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points).
