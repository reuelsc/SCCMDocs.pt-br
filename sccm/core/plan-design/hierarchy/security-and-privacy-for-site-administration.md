---
title: "Segurança e privacidade da administração de site | Microsoft Docs"
description: "Otimize a segurança e a privacidade para administração de site no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1d58176e-abc0-4087-8583-ce70deb4dcf5
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: aca2169c8f5f855e84ca924ca56f6b64bba80fd6


---
# <a name="security-and-privacy-for-site-administration-in-system-center-configuration-manager"></a>Segurança e privacidade para administração de site no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico contém informações de segurança e privacidade para a hierarquia e sites do System Center Configuration Manager.

##  <a name="a-namebkmksecuritysitesa-security-best-practices-for-site-administration"></a><a name="BKMK_Security_Sites"></a> Práticas recomendadas de segurança para administração de site  
 Use as práticas recomendadas de segurança a seguir para ajudar a proteger a hierarquia e os sites do System Center Configuration Manager.  

 **Executar a instalação somente de uma fonte confiável e proteger o canal de comunicação entre a mídia de instalação e o servidor do site.**  

 Para ajudar a evitar a violação dos arquivos de origem, execute a instalação de uma fonte confiável. Se você armazenar arquivos na rede, proteja o local de rede.  

 Se você executar a instalação de um local de rede, para ajudar a evitar que um invasor viole os arquivos enquanto eles são transmitidos pela rede, use a assinatura IPsec ou SMB entre o local de origem dos arquivos de instalação e o servidor do site.  

 Além disso, se você usar o Downloader de Instalação para baixar os arquivos solicitados pela instalação, assegure também a proteção do local onde esses arquivos são armazenados e proteja o canal de comunicação desse local ao executar a instalação.  

 **Estenda o esquema do Active Directory para o System Center Configuration Manager e publique sites no Active Directory Domain Services.**  

 Não é exigido que as extensões do esquema executem o System Center Configuration Manager, mas elas criam um ambiente mais seguro, pois os clientes Configuration Manager e servidores do site podem recuperar informações de uma fonte confiável.  

 Se os clientes estiverem em um domínio não confiável, implante as seguintes funções do sistema de sites no domínio dos clientes:  

-   Ponto de gerenciamento  

-   Ponto de distribuição  

-   Ponto de sites da Web do Catálogo de Aplicativos  

> [!NOTE]  
>  Um domínio confiável para o Configuration Manager requer autenticação Kerberos, portanto, se os clientes estão em outra floresta que não tenha uma relação de confiança bidirecional com a floresta do servidor do site, considera-se que esses clientes estão em domínio não confiável. Uma relação de confiança externa não é suficiente para essa finalidade.  

 **Usar o IPsec para proteger as comunicações entre os servidores do sistema de site e sites.**  

 Embora o Configuration Manager proteja a comunicação entre o servidor do site e o computador que executa o SQL Server, o Configuration Manager não protege a comunicação entre funções do sistema de sites e o SQL Server. Somente alguns sistemas de site (o ponto de registro e o ponto de serviços Web do catálogo de aplicativos) podem ser configurados para HTTPS para comunicação intrassite.  

 Se você não usar controles adicionais para proteger esses canais de servidor para servidor, os invasores poderão usar vários ataques de falsificação e intermediários. Usar a assinatura SMB quando você não pode usar o IPsec.  

> [!NOTE]  
>  É particularmente importante proteger o canal de comunicação entre o servidor do site e o servidor de origem do pacote. Essa comunicação usa SMB. Se você não pode usar o IPsec para proteger essa comunicação, use a assinatura SMB para assegurar que os arquivos não sejam violados antes de os clientes baixarem e executarem os arquivos.  

 **Não altere os grupos de segurança que o Configuration Manager cria e gerencia para comunicação do sistema de sites.**  

 Grupos de segurança:  

-   **SMS_SiteSystemToSiteServerConnection_MP_&lt;SiteCode\>**  

-   **SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;SiteCode\>**  

-   **SMS_SiteSystemToSiteServerConnection_Stat_&lt;SiteCode\>**  

O Configuration Manager cria e gerencia automaticamente esses grupos de segurança. Isso inclui remover contas de computador quando uma função do sistema do site é removida.  

Para garantir a continuidade do serviço e o mínimo de privilégios, não edite manualmente esses grupos.  

**Se os clientes não puderem consultar o servidor de catálogo global para obter informações do Configuration Manager, gerencie o processo de provisionamento da chave de raiz confiável.**  

Se os clientes não puderem consultar o catálogo global para obter informações do Configuration Manager, eles deverão confiar na chave de raiz confiável para autenticar pontos de gerenciamento válidos. A chave de raiz confiável é armazenada no Registro do cliente e pode ser definida usando a política de grupo ou configuração manual.  

Se o cliente não tiver uma cópia da chave de raiz confiável antes de contatar um ponto de gerenciamento pela primeira vez, ele confiará no primeiro ponto de gerenciamento com o qual ele se comunica. Para reduzir o risco de um invasor direcionar clientes para um ponto de gerenciamento não autorizado, você pode pré-provisionar os clientes com a chave de raiz confiável. Para obter mais informações, consulte [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

**Usar números de porta não padrão.**  

Quando você usa números de porta não padrão, isso pode fornecer segurança adicional, pois dificulta a exploração do ambiente por invasores na preparação de um ataque. Se você decidir usar portas não padrão, planeje-as antes de instalar o Configuration Manager e use-as consistentemente em todos os sites na hierarquia. Portas de solicitação do cliente e o Wake on LAN são exemplos de onde você pode usar números de porta não padrão.  

**Usar a separação de funções nos sistemas de site.**  

Embora você possa instalar todas as funções do sistema de site em um único computador, essa prática raramente é usada em redes de produção, pois ela cria um único ponto de falha.  

**Reduzir o perfil de ataque.**  

Quando você instala cada função do sistema de site em um servidor diferente, isso reduz a chance de que um ataque a vulnerabilidades em um sistema de site seja usado contra um sistema de site diferente. Muitas funções do sistema de site requerem a instalação do IIS (Serviços de Informações da Internet) no sistema de site e isso aumenta a superfície de ataque. Se você precisar combinar funções do sistema de site para reduzir as despesas de hardware, combine funções do sistema de site do IIS somente a outras funções do sistema de site que requer o IIS.  

> [!IMPORTANT]  
>  A função do ponto de status de fallback é uma exceção: como essa função do sistema de sites aceita dados autenticados de clientes, a função do ponto de status de fallback nunca deve ser atribuída a outra função do sistema de sites do Configuration Manager.  


**Siga as práticas recomendadas de segurança para o Windows Server e execute o Assistente de Configuração de Segurança em todos os sistemas de site.**  

O SCW (Assistente de Configuração de Segurança) ajuda a criar uma política de segurança que você pode aplicar a qualquer servidor em sua rede. Depois de instalar o modelo do System Center Configuration Manager, o SCW reconhece aplicativos, portas, serviços e funções do sistema de sites do Configuration Manager. Em seguida, ele permite a comunicação necessária para o Configuration Manager e bloqueia a comunicação desnecessária.  

O Assistente de Configuração de Segurança está incluído no kit de ferramentas do System Center 2012 Configuration Manager, que pode ser baixado do Centro de Download da Microsoft: [System Center 2012 – Configuration Manager Component Add-ons and Extensions](http://go.microsoft.com/fwlink/p/?LinkId=251931) (System Center 2012 – Complementos e extensões do componente do Configuration Manager).  

**Configurar endereços IP estáticos para sistemas de site.**  

Os endereços IP estáticos são mais fáceis de proteger contra ataques de resolução de nomes.  

Os endereços IP estáticos também facilitam a configuração do IPsec, que é uma prática recomendada de segurança para proteger a comunicação entre sistemas de sites no Configuration Manager.  

**Não instale outros aplicativos em servidores do sistema de site.**  

Ao instalar outros aplicativos em servidores do sistema de sites, você aumenta a superfície de ataque para o Configuration Manager e corre o risco de problemas de incompatibilidade.  

**Exigir assinatura e habilitar a criptografia como uma opção do site.**  

Habilite as opções de assinatura e criptografia para o site. Verifique se todos os clientes podem oferecer suporte ao algoritmo de hash SHA-256 e habilite a opção **Exigir SHA-256**.  

**Restrinja e monitore usuários administrativos do Configuration Manager e use a administração baseada em funções para conceder a esses usuários as permissões mínimas que eles exigem.**  

Conceda acesso administrativo ao Configuration Manager somente a usuários em que você confia e conceda a eles permissões mínimas usando as funções de segurança internas ou personalizando as funções de segurança. Os usuários administrativos que podem criar, modificar e implantar aplicativos, sequência de tarefas, atualizações de software, itens de configuração e linhas de base de configuração, podem potencialmente controlar dispositivos na hierarquia do Configuration Manager.  

Periodicamente, audite atribuições do usuário administrativo e seu nível de autorização para verificar as alterações necessárias.  

Para obter mais informações sobre a configuração da administração baseada em funções, consulte [Configure role-based administration for System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md).  

**Proteja backups do Configuration Manager e o canal de comunicação ao fazer backup e restaurar.**  

Quando você faz backup do Configuration Manager, essas informações incluem certificados e outros dados confidenciais que podem ser usados por um invasor para representação.  

Use a assinatura SMB ou IPsec ao transferir esses dados pela rede e proteja o local do backup.  

**Sempre que você exportar ou importar objetos do console do Configuration Manager para um local da rede, proteja o local e o canal de rede.**  

Restrinja quem pode acessar a pasta de rede.  

Use a assinatura SMB ou o IPsec entre o local de rede e o servidor do site e entre o computador que executa o console do Configuration Manager e o servidor do site para evitar que um invasor viole os dados exportados. Use IPsec para criptografar os dados na rede e para evitar a divulgação de informações.  

**Se um sistema de sites falhar para desinstalar ou interromper o funcionamento e não puder ser restaurado, remova manualmente os certificados do Configuration Manager deste servidor e de outros servidores do Configuration Manager.**  

Para remover o PeerTrust que foi originalmente estabelecido com o sistema de sites e as funções do sistema de sites, remova manualmente os certificados do Configuration Manager do servidor com falha no repositório de certificados **Pessoas Confiáveis** em outros servidores do sistema de sites. Isso é particularmente importante se você redefinir o servidor sem reformatá-lo.  

Para obter mais informações sobre estes certificados, veja a seção Controles de criptografia para a comunicação do servidor na [Referência técnica para controles de criptografia usados no System Center Configuration Manager](../../../protect/deploy-use/cryptographic-controls-technical-reference.md).  

**Não configurar os sistemas de site baseados na Internet site para conectar a rede de perímetro e a intranet.**  

Não configure servidores do sistema de site para serem de hospedagem múltipla, assim eles se conectam à rede de perímetro e à intranet. Embora essa configuração permita que sistemas de site baseados na Internet aceitem conexões do cliente da Internet e da intranet, ela elimina um limite de segurança entre a rede de perímetro e a intranet.  

**Se o servidor do sistema de site estiver em uma rede não confiável (como uma rede de perímetro), configure o servidor do site para iniciar conexões para o sistema de site.**  

Por padrão, os sistemas de site iniciam conexões para o servidor do site para transferir dados, o que pode ser um risco à segurança quando a inicialização da conexão se origina de uma rede não confiável para uma rede confiável. Quando os sistemas de site aceitam conexões da Internet ou residem em uma floresta não confiável, configure a opção do sistema de site **Exigir que o servidor do site inicie conexões com este sistema de site** para que, depois da instalação do sistema de site e de quaisquer funções do sistema de site, todas as conexões sejam iniciadas da rede confiável.  

**Se você usar um servidor proxy da Web para gerenciamento de clientes baseado na Internet, use a ponte SSL para SSL, usando a terminação com autenticação.**  

 Quando você configura a terminação SSL no servidor proxy da Web, os pacotes da Internet estão sujeitos à inspeção antes de serem encaminhados à rede interna. O servidor proxy da Web autentica a conexão do cliente, termina a conexão e depois abre uma nova conexão autenticada com os sistemas de área baseados na Internet.  

 Quando os computadores cliente do Configuration Manager usam um servidor Web proxy para se conectar a sistemas de sites baseados na Internet, a identidade do cliente (GUID do cliente) fica protegida na carga do pacote para que o ponto de gerenciamento não considere o servidor Web proxy como o cliente. Se o servidor proxy da Web não oferecer suporte aos requisitos para a ponte SSL, o túnel SSL terá suporte. Essa é uma opção menos segura, pois os pacotes de SSL da Internet são encaminhados para os sistemas de site sem terminação SSL, para que não possam ser inspecionados quanto a conteúdo mal-intencionado.  

 Se o servidor proxy da Web não oferecer suporte os requisitos para a ponte SSL, você poderá usar o túnel SSL. No entanto, essa é uma opção menos segura, pois os pacotes de SSL da Internet são encaminhados para os sistemas de site sem terminação SSL, para que não possam ser inspecionados quanto a conteúdo mal-intencionado.  

> [!WARNING]  
>  Os dispositivos móveis que são registrados pelo Configuration Manager não podem usar a ponte SSL e devem usar somente o túnel SSL.  

**As configurações a serem usadas se você definir o site para ativar computadores para instalar o software.**  

-   Se você usar pacotes de inicialização tradicionais, use unicast em vez de transmissões direcionadas por sub-rede  

-   Se você tiver de usar transmissões direcionadas por sub-rede, configure roteadores para permitir transmissões direcionadas por IP somente do servidor do site e somente em um número de porta não padrão  

Para obter mais informações sobre as diferentes tecnologias Wake On LAN, consulte [Planning How to Wake Up Clients in System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md) (Planejando como ativar clientes no System Center Configuration Manager).

**Se você usa notificação por email, configure o acesso autenticado para o servidor de email SMTP.**  

Sempre que possível, use um servidor de email que ofereça suporte a acesso autenticado e use a conta de computador do servidor do site para autenticação. Se for necessário especificar uma conta de usuário para autenticação, use uma conta que tenha o mínimo de privilégios.  

##  <a name="a-namebkmksecuritysiteservera-security-best-practices-for-the-site-server"></a><a name="BKMK_Security_SiteServer"></a> Práticas recomendadas de segurança para o servidor do site  
 Use as práticas recomendadas de segurança a seguir para ajudar a proteger o servidor do site do Configuration Manager.  

 **Instale o Configuration Manager em um servidor membro em vez de em um controlador de domínio.**  

 Os sistemas de sites e o servidor do site do Configuration Manager não precisam da instalação em um controlador de domínio. Controladores de domínio não têm outro banco de dados SAM (Gerenciamento de Contas de Segurança) local além do banco de dados do domínio. Ao instalar o Configuration Manager em um servidor membro, você poderá manter as contas do Configuration Manager no banco de dados SAM local, em vez de manter no banco de dados do domínio.  

 Essa prática também reduz a superfície sujeita a ataques nos controladores de domínio.  

 **Instale sites secundários, evitando copiar os arquivos no servidor do site secundário pela rede.**  

 Ao executar a Instalação e criar um site secundário, não selecione a opção para copiar os arquivos do site pai no site secundário nem use um local de origem na rede. Quando você copia arquivos pela rede, algum invasor habilidoso pode invadir o pacote de instalação do site secundário e adulterar os arquivos antes de serem instalados, apesar de que seria difícil cronometrar esse ataque. Esse ataque pode ser reduzido com o uso de IPsec ou SMB quando você transferir os arquivos.  

 Em vez de copiar os arquivos pela rede, no servidor do site secundário, copie os arquivos de origem da mídia para uma pasta local. Depois, ao executar a Instalação para criar um site secundário, na página **Arquivos de Origem de Instalação** , selecione **Usar os arquivos de origem no seguinte local no computador do site secundário (mais seguro)**e especifique essa pasta.  

 Para obter mais informações, consulte [Install a secondary site](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary) (Instalar um site secundário) no tópico [Install System Center Configuration Manager sites](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md) (Instalar sites do System Center Configuration Manager).  

##  <a name="a-namebkmksecuritysqlservera-security-best-practices-for-sql-server"></a><a name="BKMK_Security_SQLServer"></a> Práticas recomendadas de segurança para o SQL Server  
 O Configuration Manager usa o SQL Server como banco de dados back-end. Se o banco de dados estiver comprometido, os invasores poderão ignorar o Configuration Manager e acessar diretamente o SQL Server para iniciar ataques por meio do Configuration Manager. Considere os ataques contra o SQL Server de risco muito elevado, os quais devem ser reduzidos adequadamente.  

 Use as práticas recomendadas de segurança a seguir para ajudar a proteger SQL Server para o Configuration Manager.  

 **Não use o servidor de banco de dados do site do Configuration Manager para executar outros aplicativos do SQL Server.**  

 Quando você aumenta o acesso ao servidor de banco de dados do site do Configuration Manager, isso aumenta o risco aos dados do Configuration Manager. Se o banco de dados do site do Configuration Manager estiver comprometido, outros aplicativos no mesmo computador SQL Server também estarão em risco.  

 **Configurar o SQL Server para usar autenticação do Windows.**  

 Embora o Configuration Manager acesse o banco de dados do site usando uma conta do Windows e autenticação do Windows, ainda é possível configurar o SQL Server para usar o modo misto do SQL Server. O modo misto do SQL Server permite logins adicionais do SQL para acessar o banco de dados, o que não é necessário e aumenta a superfície sujeita a ataques.  

 **Adote medidas adicionais para garantir que os sites secundários que usam o SQL Server Express tenham as últimas atualizações de software.**  

 Quando você instala um site primário, o Configuration Manager baixa o SQL Server Express do Centro de Download da Microsoft e copia os arquivos no servidor do site primário. Quando você instala um site secundário e seleciona a opção que instala o SQL Server Express, o Configuration Manager instala a versão baixada anteriormente e não verifica se há novas versões disponíveis. Para garantir que o site secundário tenha as versões mais recentes, execute um dos procedimentos a seguir:  

-   Depois de instalado o site secundário, execute o Windows Update no servidor do site secundário.  

-   Antes de instalar o site secundário, instale manualmente o SQL Server Express no computador que irá executar o servidor do site secundário e verifique se você instalou a versão mais recente, bem como as atualizações de software. Em seguida, instale o site secundário e selecione a opção de usar uma instância existente do SQL Server.  

Periodicamente, execute o Windows Update para esses sites e para todas as versões instaladas do SQL Server para garantir que eles tenham as últimas atualizações de software.  

**Siga as práticas recomendadas para o SQL Server.**  

Identifique e siga as práticas recomendadas para a sua versão do SQL Server. No entanto, leve em consideração os seguintes requisitos do Configuration Manager:  

-   A conta de computador do servidor do site deve ser um membro do grupo de Administradores no computador que executa o SQL Server. Se você seguir a recomendação do SQL Server de "provisionar entidades de segurança de administração explicitamente", a conta que usar para executar a Instalação no servidor do site deverá ser um membro do grupo de usuários do SQL.  

-   Se você instalar o SQL Server usando uma conta de usuário de domínio, verifique se a conta de computador do servidor do site está configurada para um SPN (Nome da Entidade de Serviço), que é publicado em Serviços de Domínio Active Directory . Sem o SPN, a autenticação Kerberos e a instalação do Configuration Manager falharão.  

##  <a name="a-namebkmksecurityiisa-security-best-practices-for-site-systems-that-run-iis"></a><a name="BKMK_Security_IIS"></a> Práticas recomendadas de segurança para os sistemas de site que executam IIS  
Várias funções do sistema de sites no Configuration Manager requerem o IIS. Proteger o IIS permite que o Configuration Manager funcione corretamente e reduz o risco de ataques à segurança. Quando for viável, minimize o número de servidores que requerem IIS. Por exemplo, execute apenas o número de pontos de gerenciamento que você precisa para dar suporte à sua base de clientes, levando em consideração a alta disponibilidade e o isolamento da rede para o gerenciamento de clientes baseado na Internet.  

 Use as práticas recomendadas de segurança a seguir para proteger os sistemas de site que executam IIS.  

 **Desabilite as funções do IIS de que você não precisa.**  

 Instale o mínimo de recursos do IIS para a função do sistema de site que você instalar. Para obter mais informações, consulte [Site and site system prerequisites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Pré-requisitos de site e sistema de sites)  

 **Configure as funções do sistema de site para exigir HTTPS.**  

 Quando os clientes se conectam a um sistema de site usando HTTP, em vez de HTTPS, eles usam a autenticação do Windows, que pode voltar a usar a autenticação NTLM em vez da autenticação Kerberos. Quando a autenticação NTLM é usada, os clientes podem se conectar a um servidor não autorizado.  

 A exceção a essa prática recomendada de segurança podem ser os pontos de distribuição, pois as contas de acesso ao pacote não funcionam quando o ponto de distribuição está configurado para HTTPS. As contas de acesso ao pacote fornecem autorização para acesso ao conteúdo, de modo que você pode restringir quais usuários podem acessar o conteúdo. Para obter mais informações, consulte [Security Best Practices for Content Management](../../../core/plan-design/hierarchy/security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement).  

**Configure uma CTL (Lista de Certificados Confiáveis) no IIS para as funções do sistema de sites.**  

Funções do sistema de sites:  

-   Um ponto de distribuição configurado para HTTPS.  

-   Um gerenciamento configurado para HTTPS e habilitado para oferecer suporte a dispositivos móveis.  

Uma CTL é uma lista definida de autoridades de certificação confiáveis. Quando você usa uma CTL com Política de Grupo e implantação de PKI, uma CTL permite complementar as autoridades de certificação confiáveis ​​existentes configuradas na rede, como aquelas instaladas automaticamente com o Microsoft Windows ou adicionadas por meio de autoridades de certificação raiz corporativas do Windows. No entanto, quando uma CTL é configurada no IIS, ela define um subconjunto dessas autoridades de certificação confiáveis.  

Esse subconjunto fornece mais controle sobre a segurança, pois a CTL restringe os certificados de cliente aceitos para somente aqueles emitidos a partir da lista de autoridades de certificação na CTL. Por exemplo, o Windows vem com um número de certificados de autoridades de certificação de terceiros bem conhecidas, como VeriSign e Thawte. Por padrão, computadores que executam o IIS confiam em certificados vinculados a essas autoridades de certificação bem conhecidas. Quando você não configurar o IIS com uma CTL para as funções do sistema de sites listadas, todo dispositivo que tenha um certificado do cliente emitido por essas autoridades de certificação será aceito como um cliente válido do Configuration Manager. Se você configurar o IIS com uma CTL que não inclua essas autoridades de certificação, as conexões do cliente serão recusadas ​​se o certificado for vinculado a essas autoridades de certificação. Entretanto, para que os clientes do Configuration Manager sejam aceitos para as funções do sistema de sites listadas, será necessário configurar o IIS com uma CTL que especifique as autoridades de certificação usadas pelos clientes do Configuration Manager.  

> [!NOTE]  
>  Somente as funções do sistema de sites listadas requerem que você configure uma CTL no IIS; a lista de emissores de certificado que o Configuration Manager usa para pontos de gerenciamento fornece a mesma funcionalidade aos computadores cliente quando eles se conectam a pontos de gerenciamento de HTTPS.  

Para obter mais informações sobre como configurar uma lista de autoridades de certificação confiáveis ​​no IIS, consulte a documentação do IIS.  

**Não coloque o servidor do site em um computador com IIS.**  

A separação de funções ajuda a reduzir o perfil de ataque e a aumentar a capacidade de recuperação. Além disso, a conta de computador do servidor do site geralmente tem privilégios administrativos em todas as funções do sistema de sites (e, possivelmente, em clientes do Configuration Manager, caso você use a instalação do cliente por push).  

**Use servidores IIS dedicados para o Configuration Manager.**  

Embora seja possível hospedar vários aplicativos baseados na Web nos servidores IIS usados pelo Configuration Manager, essa prática pode aumentar significativamente a superfície sujeita a ataques. Aplicativos mal configurados podem permitir que um invasor obtenha o controle de um sistema de sites do Configuration Manager, o que poderia permitir que ele também obtivesse o controle da hierarquia.  

Se você precisar executar outros aplicativos baseados na Web em sistemas de sites do Configuration Manager, crie um site personalizado para os sistemas de sites do Configuration Manager.  

**Use um site da Web personalizado.**  

Para sistemas de sites que executam o IIS, você pode configurar o Configuration Manager para usar um site personalizado em vez do site padrão do IIS. Se for necessário executar outros aplicativos Web no sistema de site, você deverá usar um site da Web personalizado. Essa configuração abrange todo o site, não apenas um sistema de site específico.  

Além de fornecer segurança adicional, você deverá usar um site da Web personalizado se executar outros aplicativos Web no sistema de sites.  

**Se você alternar do site da Web padrão para um site da Web personalizado depois que todas as funções do ponto de distribuição forem instaladas, remova os diretórios virtuais padrão.**  

Quando você alterna do site da Web padrão para um site da Web personalizado, o Configuration Manager não remove diretórios virtuais antigos. Remova os diretórios virtuais que o Configuration Manager criou originalmente no site padrão.  

Por exemplo, os diretórios virtuais a serem removidos de um ponto de distribuição são os seguintes:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  

**Siga as práticas recomendadas para o Servidor IIS.**  

Identifique e siga as práticas recomendadas para a sua versão do Servidor IIS. No entanto, leve em consideração todos os requisitos do Configuration Manager para funções específicas do sistema de sites. Para obter mais informações, consulte [Site and site system prerequisites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Pré-requisitos de site e sistema de sites).  

##  <a name="a-namebkmksecuritymanagementpointa-security-best-practices-for-the-management-point"></a><a name="BKMK_Security_ManagementPoint"></a> Práticas recomendadas de segurança para o ponto de gerenciamento  
 Os pontos de gerenciamento são a principal interface entre dispositivos e o Configuration Manager. Considere os ataques contra o ponto de gerenciamento e o servidor em que ele é executado de risco muito elevado e a serem reparados adequadamente. Aplique todas as práticas recomendadas de segurança apropriadas e monitore atividades incomuns.  

 Use as práticas recomendadas de segurança a seguir para ajudar a proteger um ponto de gerenciamento no Configuration Manager.  

**Ao instalar um cliente do Configuration Manager em um ponto de gerenciamento, atribua-o ao site desse ponto de gerenciamento.**  

 Evite o cenário em que um cliente do Configuration Manager que está em um sistema de sites do ponto de gerenciamento é atribuído a outro site além daquele do ponto de gerenciamento.  

 Se você migrar de uma versão anterior para o System Center Configuration Manager, migre o software cliente no ponto de gerenciamento para o System Center Configuration Manager assim que possível.  

##  <a name="a-namebkmksecurityfspa-security-best-practices-for-the-fallback-status-point"></a><a name="BKMK_Security_FSP"></a> Práticas recomendadas de segurança para o ponto de status de fallback  
 Use as práticas recomendadas de segurança a seguir ao instalar um ponto de status de fallback no Configuration Manager.  

 Para obter mais informações sobre considerações de segurança ao instalar um ponto de status de fallback, consulte [Determine Whether You Require a Fallback Status Point](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md#BKMK_Determine_FSP).  

**Não execute outras funções do sistema de site no sistema de site e não as instale em um controlador de domínio.**  

 Como o ponto de status de fallback é projetado para aceitar comunicação não autenticada de qualquer computador, a execução dessa função do sistema de site com outras funções do sistema de site ou em um controlador de domínio aumenta consideravelmente o risco a esse servidor.  

**Quando usar certificados PKI para comunicação do cliente no Configuration Manager, instale o ponto de status de fallback antes de instalar os clientes.**  

 Se os sistemas de sites do Configuration Manager não aceitarem a comunicação de cliente HTTP, você poderá não saber que os clientes não são gerenciados devido a problemas de certificado relacionados à PKI. No entanto, se os clientes forem atribuídos a um ponto de status de fallback, esses problemas de certificado serão relatados pelo ponto de status de fallback.  

 Por motivos de segurança, não é possível atribuir um ponto de status de fallback a clientes após a instalação deles; você pode atribuir essa função somente durante a instalação do cliente.  

**Evite usar o ponto de status de fallback na rede de perímetro.**  

 Por design, o ponto de status de fallback aceita dados de qualquer cliente. Embora um ponto de status de fallback na rede de perímetro possa ajudar a solucionar problemas de clientes baseados na Internet, balanceie os benefícios da solução de problemas com o risco de um sistema de site que aceita dados não autenticados em uma rede acessível publicamente.  

 Se você instalar o ponto de status de fallback na rede de perímetro ou em qualquer rede não confiável, configure o servidor do site para iniciar as transferências de dados, em vez da configuração padrão, a qual permite que o ponto de status de fallback inicie uma conexão com o servidor do site.  

##  <a name="a-namebkmksecurityissuesclientsa-security-issues-for-site-administration"></a><a name="BKMK_SecurityIssues_Clients"></a> Problemas de segurança para a administração do site  
 Reveja os problemas de segurança a seguir para o Configuration Manager:  

-   O Configuration Manager não tem defesa contra um usuário administrativo autorizado que usa o Configuration Manager para atacar a rede. Usuários administrativos não autorizados são um alto risco à segurança e podem iniciar vários ataques, que incluem:  

    -   Usar a implantação de software para instalar e executar automaticamente softwares mal-intencionados em cada computador cliente do Configuration Manager na empresa.  

    -   Usar o controle remoto para assumir o controle remoto de um cliente do Configuration Manager sem a permissão dele.  

    -   Configurar intervalos de sondagem rápidos e grandes quantidades de inventário para criar ataques de negação de serviço a clientes e servidores.  

    -   Usar um único site na hierarquia para gravar dados em dados do Active Directory de outro site.  

    A hierarquia do site é o limite de segurança; considere a possibilidade de sites serem apenas limites de gerenciamento.  

    Audite todas as atividades do usuário administrativo e examine rotineiramente os logs de auditoria. Exija que todos os usuários administrativos do Configuration Manager passem por uma verificação em segundo plano antes de serem contratados e exija novas verificações periódicas como uma condição para sua admissão.  

-   Se o ponto de registro estiver comprometido, um invasor poderá obter certificados de autenticação e roubar as credenciais de usuários que registram seus dispositivos móveis.  

    O ponto de registro se comunica com uma autoridade de certificação e pode criar, modificar e excluir objetos do Active Directory. Nunca instale o ponto de registro na rede de perímetro e monitore a atividade incomum.  

-   Se você permitir políticas de usuários para o gerenciamento de clientes baseado na Internet ou configurar o ponto de sites da Web do catálogo de aplicativos em usuários quando eles estiverem na Internet, você aumentará seu perfil de ataque.  

    Além de usar certificados PKI para conexões de cliente para servidor, essas configurações requerem a autenticação do Windows, que pode retornar ao uso da autenticação NTLM em vez da Kerberos. A autenticação NTLM é vulnerável a ataques de repetição e de representação. Para autenticar com êxito um usuário na Internet, permita uma conexão a partir do servidor do sistema de site baseado na Internet com um controlador de domínio.  

-   O compartilhamento Admin$ é necessário em servidores do sistema de site.  

    O servidor de sites do Configuration Manager utiliza o compartilhamento Admin$ para se conectar aos sistemas de sites e executar operações de serviço neles. Não desative ou remova o compartilhamento Admin$.  

-   O Configuration Manager usa serviços de resolução de nomes para se conectar a outros computadores e é difícil proteger esses arquivos contra ataques de segurança, como falsificação, adulteração, repúdio, divulgação de informações confidenciais, negação de serviço e elevação de privilégio.  

    Identifique e siga as práticas recomendadas de segurança para a versão do DNS e do WINS usada para a resolução de nomes.  

##  <a name="a-namebkmkprivacycliientsa-privacy-information-for-discovery"></a><a name="BKMK_Privacy_Cliients"></a> Informações de privacidade para descoberta  
 A descoberta cria registros para recursos de rede e os armazena no banco de dados do System Center Configuration Manager. Registros de dados de descobertas contêm informações do computador, como endereço IP, sistema operacional e o nome do computador. Os métodos de descoberta do Active Directory também podem ser configurados para descobrir quaisquer informações armazenadas nos Serviços de Domínio Active Directory.  

 O único método de descoberta habilitado por padrão é a descoberta de pulsação, mas esse método somente descobre computadores que já têm o software cliente do System Center Configuration Manager instalado.  

 As informações de descoberta não são enviadas à Microsoft. As informações de descoberta são armazenadas no banco de dados do Configuration Manager. As informações são retidas no banco de dados até que sejam excluídas pela tarefa de manutenção de site **Excluir Dados Antigos de Descoberta** a cada 90 dias. Você pode configurar o intervalo de exclusão.  

 Para configurar métodos de descoberta adicionais ou estender a descoberta do Active Directory, considere seus requisitos de privacidade.  



<!--HONumber=Dec16_HO3-->


