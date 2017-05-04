---
title: Perfis VPN no System Center Configuration Manager | Microsoft Docs
description: "Perfis de VPN em dispositivos móveis no System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45388103-2410-4c7e-b4cf-73a1bda485fc
caps.latest.revision: 18
caps.handback.revision: 0
author: lleonard-msft
ms.author: alleonar
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 699b79b68440b61904a9053e5004318a2a248bfd
ms.openlocfilehash: 8adc41a30bf12a91a272029db49e50ba003d3e9c
ms.lasthandoff: 04/25/2017

---
# <a name="vpn-profiles-on-mobile-devices-in-system-center-configuration-manager"></a>Perfis de VPN em dispositivos móveis no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use perfis de VPN no System Center Configuration Manager para implantar as configurações de VPN para usuários de dispositivo móvel em sua organização. Ao implantar essas configurações, você minimiza o esforço do usuário final necessário para conectar-se aos recursos na rede da empresa.  

 Por exemplo, você deseja provisionar todos os dispositivos que executam o sistema operacional iOS com as configurações necessárias para se conectar ao compartilhamento de arquivos na rede corporativa. Você pode criar um perfil VPN que contém as configurações necessárias para conectar-se à rede corporativa e implantar esse perfil a todos os usuários que possuem dispositivos que executam o iOS na sua hierarquia. Os usuários de dispositivos iOS veem a conexão VPN na lista de redes disponíveis e podem se conectar a essa rede com o mínimo de esforço.  

 Quando você cria um perfil VPN, pode incluir uma grande variedade de configurações de segurança, inclusive certificados para validação de servidor e autenticação cliente que foram provisionados usando os perfis de certificado do System Center Configuration Manager. Para obter mais informações sobre perfis de certificado, consulte [Perfis de certificado do System Center Configuration Manager](../../protect/deploy-use/introduction-to-certificate-profiles.md).  

 ## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>Perfis de VPN usando o Configuration Manager junto com o Intune

 Para implantar perfis em dispositivos iOS, Android, Windows Phone e Windows 8.1, esses dispositivos devem ser registrados no Microsoft Intune. Dispositivos em outras plataformas também podem ser registrados no Intune. Para obter informações sobre como registrar, veja [Gerenciar dispositivos móveis com o Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx). Esta tabela mostra qual tipo de conexão tem suporte para cada plataforma de dispositivo:  

 |Tipo de conexão|iOS e Mac OS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop e Mobile|  
 |---------------------|----------------------|-------------|-----------------|----------------|--------------------|-----------------------|-----------------------------------|  
 |Cisco AnyConnect|Sim|Sim|Não|Não|Não|Não|Sim (OMA-URI)|  
 |Pulse Secure|Sim|Sim|Sim|Não|Sim|Sim|Sim|  
 |F5 Edge Client|Sim|Sim|Sim|Não|Sim|Sim|Sim|  
 |Dell SonicWALL Mobile Connect|Sim|Sim|Sim|Não|Sim|Sim|Sim|  
 |Check Point Mobile VPN|Sim|Sim|Sim|Não|Sim|Sim|Sim|  
 |Microsoft SSL (SSTP)|Não|Não|Sim|Sim|Sim|Não|Não|  
 |Microsoft Automatic|Não|Não|Sim|Sim|Sim|Não|Sim (OMA-URI)|  
 |IKEv2|Sim (Política personalizada)|Não|Sim|Sim|Sim|Sim|Sim (OMA-URI)|  
 |PPTP|Sim|Não|Sim|Sim|Sim|Não|Sim (OMA-URI)|  
 |L2TP|Sim|Não|Sim|Sim|Sim|Não|Sim (OMA-URI)|  

## <a name="create-vpn-profiles"></a>Criar perfis de VPN
[Como criar perfis VPN no System Center Configuration Manager](../../protect/deploy-use/create-vpn-profiles.md) fornece informações gerais sobre como criar perfis de VPN.

###   <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Recursos de VPN do Windows 10, disponíveis ao usar o Configuration Manager com o Intune  


> [!NOTE]  
> O nome de um perfil VPN que usa recursos de VPN do Windows 10 não pode estar em Unicode nem incluir caracteres especiais.


|Opção|Mais informações|Tipo de conexão|  
    |------------|----------------------|---------------------|  
    |**Ignorar VPN quando conectado à rede Wi-Fi da empresa**|A conexão VPN não será usada quando o dispositivo estiver conectado à rede Wi-Fi da empresa. Insira o nome de rede confiável usado para determinar se o dispositivo está conectado à rede da empresa.|Todos|  
    |**Regras de tráfego de rede**|Defina quais protocolos, portas local e remota e os intervalos de endereços serão habilitados para a conexão VPN.<br /><br /> **Observação:** se você não criar uma regra de tráfego de rede, todos os protocolos, portas e intervalos de endereços serão habilitados. Depois de criar uma regra, somente os protocolos, portas e intervalos de endereços que você especificar na regra ou em regras adicionais serão usados pela conexão VPN.|Todos|  
    |**Rotas**|Quais rotas usarão a conexão VPN. Observe que a criação de mais de 60 rotas pode causar falha na política. |Todos|  
    |**Servidores DNS**|Quais servidores DNS são usados pela conexão VPN depois de a conexão ser estabelecida.|Todos|  
    |**Aplicativos que se conectam automaticamente à VPN**|Você pode adicionar aplicativos ou importar listas de aplicativos, que usarão automaticamente a conexão VPN. O tipo de aplicativo determinará o identificador do aplicativo. Para um aplicativo da área de trabalho, forneça o caminho do arquivo do aplicativo. Para um aplicativo universal, forneça o PFN (Nome da Família de Pacotes). Para saber como encontrar o PFN de um aplicativo, consulte [Encontrar um nome da família de pacotes para VPN por aplicativo](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md). |Todos|

> [!IMPORTANT]
> É recomendável que você proteja todas as listas de aplicativos associados que você compila para uso na configuração de VPN por aplicativo. Se um usuário não autorizado modificar sua lista e você a importar para a lista de aplicativos VPN por aplicativo, você potencialmente autorizará o acesso VPN para aplicativos que não deveriam ter acesso. Uma forma de proteger a lista de aplicativos é usar uma ACL (lista de controle de acesso).


1.  Na página **Método de Autenticação** do assistente, especifique:  

    -   **Método de Autenticação:** selecione o método de autenticação que a conexão VPN usará. Os métodos disponíveis dependem do tipo de conexão, conforme mostrado nesta tabela.  

        |Método de Autenticação|Tipos de&nbsp;conexão&nbsp;com suporte|  
        |---------------------------|--------------------------------|  
        |**Certificados**<br /><br /> **Observações:**<br />– Se o certificado de cliente autenticar em um servidor RADIUS, como um Servidor de Políticas de Rede, o Nome Alternativo da Entidade no certificado deverá ser definido como o UPN.<br/><br />– Para implantações do Android, selecione o identificador EKU e o valor de hash de impressão digital do emissor do certificado.  Caso contrário, os usuários devem selecionar o certificado apropriado manualmente.  |- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
        |**Nome de usuário e senha**|- Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
        |**Microsoft EAP-TTLS**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - PPTP<br /><br /> - IKEv2<br /><br /> - L2TP|  
        |**EAP protegido (PEAP) da Microsoft**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Senha de segurança da Microsoft (EAP-MSCHAP v2)**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Cartão inteligente ou outro certificado**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**MSCHAP v2**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**RSA SecurID** (Somente iOS)|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Usar certificados do computador**|IKEv2|  

         Dependendo das opções que você selecionar, você pode ser solicitado a especificar mais informações, como:  

        -   **Lembrar as credenciais do usuário a cada logon**: as credenciais dos usuários são lembradas para que eles não precisem inseri-las sempre que se conectarem.  

        -   **Selecionar um certificado de cliente para a autenticação do cliente** – Selecione o [certificado SCEP](create-pfx-certificate-profiles.md) do cliente que você criou anteriormente e que será usado para autenticar a conexão VPN.   

            > [!NOTE]  
            >  Para dispositivos do iOS, o perfil SCEP selecionado será inserido no perfil de VPN. Para outras plataformas, uma regra de aplicabilidade é adicionada para garantir que o perfil de VPN não seja instalado se o certificado não estiver presente ou não for compatível.  
            >   
            >  Se o certificado do SCEP especificado não estiver em conformidade ou não tiver sido implantado, o perfil de VPN não será instalado no dispositivo.
            >  
            >  Dispositivos que executam o iOS dão suporte somente a RSA SecurID e MSCHAP v2 para o método de autenticação quando o tipo de conexão é PPTP. Para evitar erros de relatórios, implante um perfil VPN PPTP separado para dispositivos que executam o iOS.  

        - **Acesso condicional**
            - Escolha **Habilitar o acesso condicional para esta conexão de VPN** para garantir que os dispositivos que se conectam à VPN sejam testados quanto à conformidade de acesso condicional antes de se conectar. As políticas de conformidade estão descritas em [Políticas de conformidade de dispositivo no System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/device-compliance-policies.md)
            - Escolha **Habilitar logon único (SSO) com certificado alternativo** para escolher um certificado diferente do certificado Autenticação de VPN para a conformidade do dispositivo. Se você escolher essa opção, forneça o **EKU** (lista separada por vírgulas) e o **Hash do Emissor** para o certificado correto que o Cliente VPN deve localizar.

         - **Proteção de Informações do Windows** – forneça a identidade corporativa gerenciada pela empresa, que normalmente é o domínio primário da organização, por exemplo, *contoso.com*. Você pode especificar vários domínios pertencentes a sua organização, separando-os com o caractere "|". Por exemplo, *contoso.com|newcontoso.com*.   
              Para obter mais informações sobre a Proteção de Informações do Windows, confira [Criar uma WIP (Política de Informações do Windows) usando o Microsoft Intune](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/create-wip-policy-using-intune).   

         ![Configurar acesso condicional para VPN](media/vpn-conditional-access.png)

         Quando suportado pela versão do Windows que está executando o Configuration Manager _e_ o método de autorização selecionado, você pode clicar em **Configurar** para abrir a caixa de diálogo de propriedades do Windows e configurar as propriedades do método de autenticação.  Se a opção **Configurar** estiver desabilitada, use meios alternativos para configurar as propriedades do método de autenticação.

2.  Na página **Configurações de Proxy** do **Assistente para Criar Perfil VPN**, marque a caixa de seleção **Definir configurações de proxy para este perfil VPN** caso a sua conexão VPN use um servidor proxy. Em seguida, forneça as informações do servidor proxy. Para obter mais informações, consulte a documentação do Windows Server.  

    > [!NOTE]  
    >  Em computadores com Windows 8.1, o perfil VPN não exibirá as informações de proxy até você se conectar à VPN com esse computador.  


3. Definir outras configurações de DNS (se necessário)  
 Na página **Configurar Conexão VPN Automática** é possível definir o seguinte:  

    -   **Habilitar VPN sob demanda** use se desejar definir configurações de DNS adicionais para dispositivos Windows Phone 8.1. Essa configuração aplica-se somente a dispositivos Windows Phone 8.1 e só deve ser habilitada nos perfis VPN que serão implantados em dispositivos Windows Phone 8.1.

    -   Lista de sufixos DNS (somente dispositivos Windows Phone 8.1) – Configura os domínios que estabelecerão uma conexão VPN. Para cada domínio especificado, adicione o sufixo DNS, o endereço do servidor DNS e uma das seguintes ações sob demanda:  

        -   **Nunca estabelecer** – Nunca abrir uma conexão VPN  

        -   **Estabelecer, se necessário** – Abrir apenas uma conexão VPN se o dispositivo precisar se conectar aos recursos  

        -   **Estabelecer sempre** – Sempre abrir a conexão VPN  

    -   **Mesclar** – Copia qualquer sufixos DNS configurado na **Lista de redes confiáveis**.  

    -   **Lista de redes confiáveis** (somente dispositivos Windows Phone 8.1) – Especificar um sufixo DNS em cada linha. Se o dispositivo estiver em uma rede confiável, a conexão VPN não será aberta.  

    -   **Lista de pesquisa de sufixo** (somente dispositivos Windows Phone 8.1) – Especificar um sufixo DNS em cada linha. Cada sufixo DNS será pesquisado durante a conexão com um site usando um nome curto.  

     Por exemplo, você especifica os sufixos de DNS **domain1.contoso.com** e **domain2.contoso.com** e visita a URL **http://mywebsite**. Os seguintes endereços serão pesquisados:  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

    > [!NOTE]  
    >  Somente para dispositivos Windows Phone 8.1  
    >   
    >  Se a opção **Enviar todo o tráfego de rede pela conexão VPN** estiver marcada e a conexão VPN estiver usando o túnel completo, para o primeiro perfil provisionado no dispositivo, a conexão VPN será aberta automaticamente. Se você desejar que um perfil diferente abra automaticamente uma conexão, você deverá torná-lo o perfil padrão no dispositivo.  
    >   
    >  Se a opção **Enviar todo o tráfego de rede pela conexão VPN** não estiver marcada e a conexão VPN estiver usando um túnel dividido, uma conexão VPN poderá ser aberta automaticamente se você configurar rotas ou um sufixo DNS específico da conexão.  


4. Na página **Plataformas com Suporte** do **Assistente para Criar Perfil VPN**, selecione os sistemas operacionais nos quais o perfil VPN será instalado ou clique em **Selecionar todos** para instalar o perfil VPN em todos os sistemas operacionais disponíveis.  

5. Conclua o assistente. O novo perfil VPN é exibido no nó **Perfis VPN** no espaço de trabalho **Ativos e Conformidade** .  


**Implantação:** Confira [Implantar Wi-Fi, VPN, email e perfis de certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) para obter informações sobre como implantar perfis de VPN.

### <a name="next-steps"></a>Próximas etapas  
 Use os tópicos a seguir para ajudar a planejar, configurar, operar e manter perfis de VPN no Configuration Manager.  

-   [Pré-requisitos para perfis de VPN no System Center Configuration Manager](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Segurança e privacidade para perfis de VPN no System Center Configuration Manager](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)

