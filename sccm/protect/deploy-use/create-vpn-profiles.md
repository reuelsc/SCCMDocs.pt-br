---
title: Como criar perfis de VPN no System Center Configuration Manager | Microsoft Docs
description: Saiba como criar perfis de VPN no System Center Configuration Manager.
ms.custom: 
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
caps.latest.revision: 15
author: nbigman
caps.handback.revision: 0
ms.author: nbigman
ms.manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 828e2ac9a3f9bcea1571d24145a1021fdf1091f3
ms.openlocfilehash: f674aa5502e4b3b45d0eda119419863892d72cff


---
# <a name="how-to-create-vpn-profiles-in-system-center-configuration-manager"></a>Como criar perfis de VPN no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


> [!NOTE]  
>
> - Para obter informações sobre quais tipos de conexão estão disponíveis para as plataformas de dispositivo diferentes, consulte [Perfis VPN no System Center Configuration Manager](../../protect/deploy-use/vpn-profiles.md).  
> - Para conexões VPN de terceiros, distribua o aplicativo VPN antes de implantar o perfil VPN. Se você não implantar o aplicativo, os usuários deverão fazer isso quando eles tentarem se conectar à VPN. Para saber como implantar aplicativos, consulte [Implantar aplicativos com o System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).

### <a name="start-the-create-vpn-profile-wizard"></a>iniciar o Assistente para Criar Perfil VPN  

1.  No console do System Center Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** do console do System Center Configuration Manager, expanda **Configurações de Conformidade**, expanda **Acesso aos Recursos da Empresa** e clique em **Perfis VPN**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Perfil VPN**.  

### <a name="provide-general-information-about-the-vpn-profile"></a>fornecer informações gerais sobre o perfil VPN  

1.  Na página **Geral** do **Assistente para Criar Perfil VPN**, especifique as seguintes informações:  

    -   **Nome** – Insira um nome exclusivo para o perfil de VPN (até 256 caracteres).  

        > [!IMPORTANT]  
        >  Não use os caracteres \\/:*?<>&#124; ou o caractere de espaço no nome do perfil VPN porque não há suporte para esses caracteres no perfil VPN do Windows Server.  

    -   **Descrição** – insira uma descrição para ajudá-lo a encontrar o perfil no console do System Center Configuration Manager (até 256 caracteres).  

    -   **Importar um item de perfil VPN existente de um arquivo** – selecione esta opção para exibir a página **Importar Perfil VPN**. Nessa página, você pode importar as informações do perfil VPN previamente exportadas para um arquivo XML (somente nos sistemas operacionais Windows 8.1 e Windows RT).  

### <a name="provide-connection-information-for-the-vpn-profile"></a>fornecer informações de conexão para o perfil VPN  

1.  Na página **Conexão** do assistente, especifique as seguintes informações:  

    -   **Tipo de conexão:** Na lista suspensa, selecione o tipo de conexão para a conexão VPN. É possível escolher entre os tipos de conexão na tabela a seguir que mostra as plataformas com suporte.  

        > [!IMPORTANT]  
        >  Antes de usar os perfis VPN implantados em um dispositivo, instale os aplicativos de VPN de terceiros de que precisa. Você pode usar as informações no tópico [Como criar aplicativos com o System Center Configuration Manager](../../apps/deploy-use/create-applications.md) para ajudá-lo a implantar o aplicativo usando o System Center Configuration Manager.  

    -   **Lista de servidores:** Clique em **Adicionar** para adicionar um novo servidor a ser usado para a conexão VPN. Dependendo do tipo de conexão, você poderá adicionar um ou mais servidores VPN e também especificar qual servidor deverá ser o padrão.  

        > [!NOTE]  
        >  Dispositivos que executam iOS não oferecem suporte ao uso de vários servidores VPN. Se você configurar vários servidores VPN e implantar o perfil VPN em um dispositivo iOS, apenas o servidor padrão será usado.  

     As demais opções da tabela a seguir poderão ser exibidas, dependendo do tipo de conexão selecionado. Consulte a documentação do servidor VPN para obter mais informações.  

    |Opção|Mais informações|Tipo de conexão|  
    |------------|----------------------|---------------------|  
    |**Território**|Especifique o nome do território de autenticação que você deseja usar. Um realm de autenticação é um agrupamento de recursos de autenticação usado pelo tipo de conexão Pulse Secure.|Pulse Secure|  
    |**Função**|Especifique o nome da função do usuário que tem acesso a essa conexão.|Pulse Secure|  
    |**Grupo de logon ou domínio**|Especifique o nome do grupo de logon ou domínio ao qual você deseja se conectar.|Dell SonicWALL Mobile Connect|  
    |**Impressão digital**|Especifique uma cadeia de caracteres, por exemplo "Código de impressões digitais da Contoso" que será usado para verificar se o servidor VPN é confiável.<br /><br /> Uma impressão digital pode ser:<br /><br /> - Enviada ao cliente para que ele saiba que pode confiar em qualquer servidor que apresentar essa impressão digital durante a conexão.<br /><br /> – Se o dispositivo não tiver a impressão digital, ele solicitará ao usuário para confiar no servidor VPN durante a conexão enquanto mostra a impressão digital (o usuário verifica a impressão digital e manualmente clica em confiar para se conectar).|Check Point Mobile VPN|  
    |**Enviar todo o tráfego de rede através da conexão VPN**|Se esta opção não estiver marcada, você poderá especificar rotas adicionais para a conexão (para os tipos de conexão **Microsoft SSL (SSTP)**, **Microsoft Automatic**, **IKEv2**, **PPTP** e **L2TP** ), que é conhecida como túnel dividido ou VPN.<br /><br /> Apenas as conexões com a rede da empresa são enviadas por um túnel VPN. O túnel VPN não é usado quando você se conecta aos recursos na Internet.|Todos|  
    |**Sufixo DNS específico da conexão**|Opcionalmente, especifique o sufixo DNS (Sistema de Nomes de Domínio) específico da conexão.|- <br />                            Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - <br />                            IKEv2<br /><br /> - <br />                            PPTP<br /><br /> - <br />                            L2TP|  
    |**Ignorar VPN quando conectado à rede Wi-Fi da empresa**|Especifica que a conexão VPN não será usada quando o dispositivo estiver conectado à rede Wi-Fi da empresa.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN<br /><br /> - Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - L2TP|  
    |**Ignorar VPN quando conectado à rede Wi-Fi local**|Especifica que a conexão VPN não será usada quando o dispositivo estiver conectado a uma rede Wi-Fi doméstica.|Todos|  
    |**Por aplicativo VPN (iOS 7 e posterior, Mac OS X 10.9 e posterior)**|Selecione esta opção se você deseja associar essa conexão VPN a um aplicativo iOS para que a conexão seja aberta quando o aplicativo é executado. É possível associar o perfil de VPN a um aplicativo ao implantá-lo.|- <br />                        Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
    |**XML personalizado (opcional)**|Permite que você especifique comandos XML personalizados para configurar a conexão VPN.<br /><br /> Exemplos:<br /><br /> Para o **Pulse Secure**:<br /><br /> **<pulse-schema><isSingleSignOnCredential\>true</isSingleSignOnCredential\></pulse-schema>**<br /><br /> Para o **CheckPoint Mobile VPN**:<br /><br /> **&lt;CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" /\>**<br /><br /> Para o **Dell SonicWALL Mobile Connect**:<br /><br /> **<MobileConnect\><Compression\>false</Compression\><debugLogging\>True</debugLogging\><packetCapture\>False</packetCapture\></MobileConnect\>**<br /><br /> Para o **F5 Edge Client**:<br /><br /> **&lt;f5-vpn-conf&gt;&lt;single-sign-on-credential /&gt;&lt;/f5-vpn-conf&gt;**<br /><br /> Consulte a documentação do VPN de cada fabricante para obter mais informações sobre como escrever comandos XML personalizados.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  

####   <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Recursos de VPN do Windows 10, disponíveis ao usar o Configuration Manager com o Intune  


> [!NOTE]  
> O nome de um perfil VPN que usa recursos de VPN do Windows 10 não pode estar em Unicode nem incluir caracteres especiais.


|Opção|Mais informações|Tipo de conexão|  
|------------|----------------------|---------------------|  
|**Ignorar VPN quando conectado à rede Wi-Fi da empresa**|Especifica que a conexão VPN não será usada quando o dispositivo estiver conectado à rede Wi-Fi da empresa. Insira o nome de rede confiável, que será usado para determinar se o dispositivo está conectado à rede da empresa.|Todos|  
|**Regras de tráfego de rede**|Defina quais protocolos, portas local e remota e os intervalos de endereços serão habilitados para a conexão VPN.<br /><br /> **Observação:** se você não criar uma regra de tráfego de rede, todos os protocolos, portas e intervalos de endereços serão habilitados. Depois de criar uma regra, somente os protocolos, portas e intervalos de endereços que você especificar na regra ou em regras adicionais serão usados pela conexão VPN.|Todos|  
|**Rotas**|Quais rotas usarão a conexão VPN. Observe que a criação de mais de 60 rotas pode causar falha na política. |Todos|  
|**Servidores DNS**|Quais servidores DNS são usados pela conexão VPN depois de a conexão ser estabelecida.|Todos|  
|**Aplicativos que se conectam automaticamente à VPN**|Você pode adicionar aplicativos ou importar listas de aplicativos, que usarão automaticamente a conexão VPN. O tipo de aplicativo determinará o identificador do aplicativo. Para um aplicativo da área de trabalho, forneça o caminho do arquivo do aplicativo. Para um aplicativo universal, forneça o PFN (Nome da Família de Pacotes). Para saber como encontrar o PFN de um aplicativo, consulte [Encontrar um nome da família de pacotes para VPN por aplicativo](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md). |Todos|

> [!IMPORTANT]
> É recomendável que você proteja todas as listas de aplicativos associados que você compila para uso na configuração de VPN por aplicativo. Se um usuário não autorizado modificar sua lista e você a importar para a lista de aplicativos VPN por aplicativo, você potencialmente autorizará o acesso VPN para aplicativos que não deveriam ter acesso. Uma forma de proteger a lista de aplicativos é usar uma ACL (lista de controle de acesso).


### <a name="configure-the-authentication-method-for-the-vpn-profile"></a>configurar o método de autenticação para o perfil VPN  

1.  Na página **Método de Autenticação** do assistente, especifique as seguintes informações:  

    -   **Método de autenticação:** Na lista suspensa, selecione o método de autenticação que será usado pela conexão VPN. Os itens da lista suspensa poderão ser diferentes, dependendo do tipo de conexão selecionado anteriormente. Os métodos de autenticação disponíveis e os tipos de conexão com suporte estão listados na tabela a seguir.  

        |Método de Autenticação|Tipos de conexão com suporte|  
        |---------------------------|--------------------------------|  
        |**Certificados**<br /><br /> **Observação:** se o certificado de cliente for utilizado para autenticação em um servidor RADIUS, como um Servidor de Políticas de Rede, o Nome Alternativo da Entidade no certificado deverá ser definido como o nome UPN.|- <br />                            Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
        |**Nome de usuário e senha**|- <br />                            Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
        |**Microsoft EAP-TTLS**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - PPTP<br /><br /> - IKEv2<br /><br /> - L2TP|  
        |**EAP protegido (PEAP) da Microsoft**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Senha de segurança da Microsoft (EAP-MSCHAP v2)**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Cartão inteligente ou outro certificado**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**MSCHAP v2**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**RSA SecurID** (Somente iOS)|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Usar certificados do computador**|IKEv2|  

         Dependendo das opções que você selecionar, você pode ser solicitado a especificar mais informações, como:  

        -   **Lembrar credenciais do usuário a cada logon**: Selecione esta opção para garantir que as credenciais do usuário sejam lembradas para que o usuário não precise digitar as credenciais sempre que uma conexão for estabelecida.  

        -   **Selecionar um certificado de cliente para a autenticação do cliente** –Selecione o certificado SCEP do cliente que você criou anteriormente que será usado para autenticar a conexão VPN. Para obter mais informações sobre como usar perfis de certificado no System Center Configuration Manager, consulte [Perfis de certificado do System Center Configuration Manager](introduction-to-certificate-profiles.md).  

            > [!NOTE]  
            >  Para dispositivos do iOS, o perfil SCEP selecionado será inserido no perfil de VPN. Para outras plataformas, uma regra de aplicabilidade é adicionada para garantir que o perfil de VPN não seja instalado se o certificado não estiver presente ou não for compatível.  
            >   
            >  Se o certificado do SCEP especificado não for compatível ou não tiver sido implantado, o perfil de VPN não será instalado no dispositivo.
            >  
            >  Dispositivos que executam o iOS dão suporte somente a RSA SecurID e MSCHAP v2 para o método de autenticação quando o tipo de conexão é PPTP. Para evitar erros de relatórios, implante um perfil VPN PPTP separado para dispositivos que executam o iOS.  

        - **Acesso condicional**
            - Escolha **Habilitar o acesso condicional para esta conexão de VPN** para garantir que os dispositivos que se conectam à VPN sejam testados quanto à conformidade de acesso condicional antes de se conectar. As políticas de conformidade estão descritas em [Políticas de conformidade de dispositivo no System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/device-compliance-policies.md)
            - Escolha **Habilitar logon único (SSO) com certificado alternativo** para escolher um certificado diferente do certificado Autenticação de VPN para a conformidade do dispositivo. Se você escolher essa opção, forneça o **EKU** (lista separada por vírgulas) e o **Hash do Emissor** para o certificado correto que o Cliente VPN deve localizar.

         - **Proteção de Informações do Windows** – forneça a identidade corporativa gerenciada pela empresa, que normalmente é o domínio primário da organização, por exemplo, *contoso.com*. Você pode especificar vários domínios pertencentes a sua organização, separando-os com o caractere "|". Por exemplo, *contoso.com|newcontoso.com*.   
            Para obter mais informações sobre a Proteção de Informações do Windows, confira [Criar uma WIP (Política de Informações do Windows) usando o Microsoft Intune](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/create-wip-policy-using-intune).   

         ![Configurar acesso condicional para VPN](../media/vpn-conditional-access.png)


        > [!NOTE]  
        >
        >Para alguns métodos de autenticação, é possível clicar em **Configurar** para abrir a caixa de diálogo de propriedades do Windows (caso haja suporte a esse método de autenticação na versão do Windows em que o console do System Center Configuration Manager está sendo executado), na qual é possível configurar as propriedades do método de autenticação.  

### <a name="configure-proxy-settings-for-the-vpn-profile"></a>definir as configurações de proxy para o perfil VPN  

1.  Na página **Configurações de Proxy** do **Assistente para Criar Perfil VPN**, marque a caixa de seleção **Definir configurações de proxy para este perfil VPN** caso a sua conexão VPN use um servidor proxy.  

2.  Especifique os detalhes sobre seu servidor proxy e suas configurações. Para obter mais informações, consulte a documentação do Windows Server.  

> [!NOTE]  
>  Em computadores com Windows 8.1, o perfil VPN não exibirá as informações de proxy até você se conectar à VPN com esse computador.  


### <a name="configure-further-dns-settings-if-required"></a>Definir outras configurações de DNS (se necessário)  
 Na página **Configurar Conexão VPN Automática** do assistente, é possível definir as seguintes configurações:  

-   **Habilitar VPN sob demanda** Selecione esta opção se desejar definir configurações de DNS adicionais nesta página do assistente para dispositivos Windows Phone 8.1.

> [!Note]  
> Essa configuração aplica-se somente a dispositivos Windows Phone 8.1 e só deve ser habilitada nos perfis VPN que serão implantados em dispositivos Windows Phone 8.1.


-   Lista de sufixos DNS (somente para dispositivos Windows Phone 8.1) – Configura os domínios que estabelecerão uma conexão VPN. Para cada domínio especificado, adicione o sufixo DNS, o endereço do servidor DNS e uma das seguintes ações sob demanda:  

    -   **Nunca estabelecer** – Nunca abrir uma conexão VPN  

    -   **Estabelecer, se necessário** – Abrir apenas uma conexão VPN se o dispositivo precisar se conectar aos recursos  

    -   **Estabelecer sempre** – Sempre abrir a conexão VPN  

-   **Mesclar** – Copia qualquer sufixos DNS configurado na **Lista de redes confiáveis**.  

-   **Lista de redes confiáveis** (somente para dispositivos Windows Phone 8.1) – Especifique um sufixo DNS em cada linha. Se o dispositivo estiver em uma rede confiável, a conexão VPN não será aberta.  

-   **Lista de pesquisa de sufixo** (somente para dispositivos Windows Phone 8.1) – Especifique um sufixo DNS em cada linha. Cada sufixo DNS que você especificar será pesquisado durante a conexão com um site usando um nome curto.  

     Por exemplo, você especifica os sufixos de DNS **domain1.contoso.com** e **domain2.contoso.com** e visita a URL **http://mywebsite**. Os seguintes endereços serão pesquisados:  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

> [!NOTE]  
>  Somente para dispositivos Windows Phone 8.1  
>   
>  Se a opção **Enviar todo o tráfego de rede pela conexão VPN** estiver marcada e a conexão VPN estiver usando o túnel completo, para o primeiro perfil provisionado no dispositivo, a conexão VPN será aberta automaticamente. Se você desejar que um perfil diferente abra automaticamente uma conexão, você deverá torná-lo o perfil padrão no dispositivo.  
>   
>  Se a opção **Enviar todo o tráfego de rede pela conexão VPN** não estiver marcada e a conexão VPN estiver usando um túnel dividido, uma conexão VPN poderá ser aberta automaticamente se você configurar rotas ou um sufixo DNS específico da conexão.  


### <a name="configure-supported-platforms-for-the-vpn-profile"></a>configurar plataformas com suporte para o perfil VPN  
 As plataformas com suporte são os sistemas operacionais em que o perfil VPN será instalado.  

Na página **Plataformas com Suporte** do **Assistente para Criar Perfil VPN**, selecione os sistemas operacionais nos quais o perfil VPN será instalado ou clique em **Selecionar todos** para instalar o perfil VPN em todos os sistemas operacionais disponíveis.  

### <a name="complete-the-wizard"></a>concluir o assistente  
 Na página **Resumo** do assistente, examine as ações a serem tomadas e escolha **Concluir**. O novo perfil VPN é exibido no nó **Perfis VPN** no espaço de trabalho **Ativos e Conformidade** .  

### <a name="next-steps"></a>Próximas etapas

- Para conexões VPN de terceiros, distribua o aplicativo VPN antes de implantar o perfil VPN. Se você não implantar o aplicativo, os usuários deverão fazer isso quando eles tentarem se conectar à VPN. Para saber como implantar aplicativos, consulte [Implantar aplicativos com o System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).

- Implante o perfil VPN conforme descrito em [Como implantar perfis VPN no System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  



<!--HONumber=Dec16_HO3-->


