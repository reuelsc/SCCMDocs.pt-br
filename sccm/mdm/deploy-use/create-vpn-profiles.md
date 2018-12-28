---
title: Perfis de VPN
titleSuffix: Configuration Manager
description: Saiba mais sobre os perfis de VPN em dispositivos móveis no Configuration Manager.
ms.date: 06/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 45388103-2410-4c7e-b4cf-73a1bda485fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1c90525b20107cbc926e3775f10d75b7c7083cac
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424554"
---
# <a name="vpn-profiles-on-mobile-devices-in-system-center-configuration-manager"></a>Perfis de VPN em dispositivos móveis no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch atual)*

Use perfis de VPN no Configuration Manager para implantar as configurações de VPN para usuários de dispositivo móvel em sua organização. Ao implantar essas configurações, você minimiza o esforço do usuário final necessário para conectar-se aos recursos na rede corporativa.  

Por exemplo, você deseja configurar todos os dispositivos iOS para conectar a um compartilhamento de arquivos na rede corporativa. Crie um perfil de VPN com as configurações de conexão necessárias. Em seguida, implante esse perfil para todos os usuários com dispositivos iOS. Esses usuários verão a conexão de VPN na lista de redes disponíveis e poderão se conectar facilmente a essa rede.  

Ao criar um perfil VPN, você pode incluir uma várias configurações de segurança. Por exemplo, você pode especificar certificados para validação de servidor e autenticação de cliente que foram configurados com os perfis de certificado do Configuration Manager. Para obter mais informações, consulte [Certificate profiles (Perfis de Certificado)](../../protect/deploy-use/introduction-to-certificate-profiles.md).  



## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>Perfis de VPN usando o Configuration Manager junto com o Intune

Para implantar perfis em dispositivos iOS, Android, Windows Phone e Windows 8.1, esses dispositivos devem estar registrados no Microsoft Intune. Dispositivos em outras plataformas também podem ser registrados no Intune. Para obter informações sobre como registrar, veja [Registrar dispositivos no Microsoft Intune](/intune/device-enrollment). 

Esta tabela mostra o tipo de conexão com suporte em cada plataforma de dispositivo:  

 |Tipo de conexão|iOS e macOS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop e Mobile|  
 |---------------|---------------|-------|-----------|----------|--------------|-----------------|-----------------------------|  
 |Cisco AnyConnect|Sim<sup>1</sup>|Sim|Não|Não|Não|Não|Não|
 |Cisco (IPSec)|Somente iOS|Não|Não|Não|Não|Não|Não|  
 |Pulse Secure|Sim|Sim|Sim|Não|Sim|Sim|Sim|  
 |F5 Edge Client|Sim|Sim|Sim|Não|Sim|Sim|Sim|  
 |Dell SonicWALL Mobile Connect|Sim|Sim|Sim|Não|Sim|Sim|Sim|  
 |Check Point Mobile VPN|Sim|Sim|Sim|Não|Sim|Sim|Sim|  
 |Microsoft SSL (SSTP)|Não|Não|Sim|Sim|Sim|Não|Não|  
 |Microsoft Automatic|Não|Não|Sim|Sim|Sim|Não|Sim|  
 |IKEv2|Sim (política personalizada, iOS 9 e versões posteriores)|Não|Sim|Sim|Sim|Sim|Sim|  
 |PPTP|Sim|Não|Sim|Sim|Sim|Não|Sim|  
 |L2TP|Sim|Não|Sim|Sim|Sim|Não|Sim (OMA-URI)|  

<sup>1</sup> A partir da versão 1802, o uso do tipo de conexão do Cisco AnyConnect varia.<!--1357393-->  
   - Use a opção **Cisco Legacy AnyConnect** para perfis de VPN nas seguintes versões:
       - iOS com Cisco AnyConnect versão 4.0.5 ou anterior
       - macOS com qualquer versão do Cisco AnyConnect
   - Use a opção **Cisco AnyConnect** para perfis de VPN nas seguintes versões:
       - iOS com Cisco AnyConnect versão 4.0.7 ou posterior

     > [!Tip]  
     > O Cisco AnyConnect 4.0.07x e posterior para iOS foi introduzido na versão 1802, como um [recurso de pré-lançamento](/sccm/core/servers/manage/pre-release-features). Na [atualização 4163547](https://support.microsoft.com/help/4163547) da versão 1802, esse recurso deixou de ser um recurso de pré-lançamento.  
  
  
> [!Note]  
> O F5 Access para iOS versões 3.0 e posterior não conta com suporte para perfis de VPN no MDM híbrido. Este produto também é chamado de F5 Access 2018. Se você precisar criar perfis de VPN para esse cliente de VPN, use o Intune autônomo. Futuras versões do iOS, incluindo a versão 12, não oferecem suporte às versões 2.1 ou anteriores do F5 Access. Para saber mais, confira o [blog da equipe de suporte do Microsoft Intune](https://aka.ms/iOS12_and_VPN).


## <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Recursos de VPN do Windows 10, disponíveis ao usar o Configuration Manager com o Intune  

As seguintes opções estão disponíveis para todos os tipos de conexão no Windows 10:

- **Ignorar VPN quando conectada à rede Wi-Fi da empresa**: A conexão VPN não é usada quando o dispositivo estiver conectado à rede Wi-Fi da empresa. Insira o nome de rede confiável usado para determinar se o dispositivo está conectado à rede corporativa.  

- **Regras de tráfego de rede**: Defina os protocolos, porta local, porta remota e intervalos de endereços para habilitar para a conexão VPN.  

     > [!Note]  
     > Se você não criar uma regra de tráfego de rede, todos os protocolos, portas e intervalos de endereços serão habilitados. Depois de criar uma regra, somente os protocolos, portas e intervalos de endereços que você especificar na regra ou em regras adicionais serão usados pela conexão de VPN.  
  
- **Rotas**: Rotas que usam a conexão VPN. A criação de mais de 60 rotas pode causar falha na política.  

- **Servidores DNS**: Quais servidores DNS são usados pela conexão VPN depois de a conexão ser estabelecida.  

- **Aplicativos que se conectam automaticamente à VPN**: Você pode adicionar aplicativos ou importar listas de aplicativos que usam automaticamente a conexão VPN. O tipo de aplicativo determina o identificador do aplicativo. Para um aplicativo da área de trabalho, forneça o caminho do arquivo do aplicativo. Para um aplicativo universal, forneça o PFN (Nome da Família de Pacotes). Para saber como encontrar o PFN de um aplicativo, consulte [Encontrar um nome da família de pacotes para VPN por aplicativo](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md).  

     > [!IMPORTANT]  
     > Proteja todas as listas de aplicativos associados que você cria para uso na configuração de VPN por aplicativo. Se um usuário não autorizado modificar sua lista e você a importar para a lista de aplicativos de VPN por aplicativo, você potencialmente autorizará o acesso de VPN para aplicativos que não deveriam ter acesso. Uma forma de proteger a lista de aplicativos é usar uma ACL (lista de controle de acesso).  



## <a name="create-vpn-profiles"></a>Criar perfis de VPN


1. Em **Ativos e Conformidade** do console do Configuration Manager, expanda o workspace **Ativos e Conformidade**, expanda **Acesso aos Recursos da Empresa** e selecione **Perfis de VPN**. 

2. Clique em **Criar perfil de VPN** na faixa de opções.  

3. Na página **Geral**, especifique um **Nome**e, em seguida, selecione o **Tipo de perfil de VPN**.   
     > [!NOTE]  
     > O nome de um perfil VPN que usa recursos de VPN do Windows 10 não pode estar em Unicode nem incluir caracteres especiais.


4. Se a página **Plataformas com suporte** estiver disponível, selecione as versões do sistema operacional para o tipo de perfil de VPN especificado anteriormente. Escolha **Selecionar tudo** para instalar o perfil de VPN em todos os sistemas operacionais disponíveis.  

5. Configure a conexão de VPN na página **Conexão**. Para obter mais informações sobre essas opções, veja a etapa na página Conexão em [Criar um perfil de VPN](/sccm/protect/deploy-use/create-vpn-profiles#create-a-vpn-profile).  

6. Na página **Método de Autenticação**, especifique as seguintes configurações:  

   - **Método de autenticação**: Selecione o método de autenticação que usa a conexão VPN. Os métodos disponíveis dependem do tipo de conexão, conforme mostrado nesta tabela.  

     |Método de Autenticação|Tipos de&nbsp;conexão&nbsp;com suporte|  
     |---------------------------|--------------------------------|  
     |**Certificados**<br /><br /> **Observações:**<ul><li>Se o certificado do cliente autenticar em um servidor RADIUS, como um Servidor de Políticas de Rede, o Nome Alternativo da Entidade no certificado deverá ser definido como o Nome UPN.</li><li>Para implantações do Android, selecione o identificador EKU e o valor de hash de impressão digital do emissor do certificado. Caso contrário, os usuários devem selecionar o certificado apropriado manualmente.</li></ul>  |<ul><li>Cisco AnyConnect</li><li>Cisco Legacy AnyConnect</li><li>Pulse Secure</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> Check Point Mobile VPN</li></ul>|  
     |**Nome de usuário e senha**|<ul><li>Pulse Secure</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> Check Point Mobile VPN</li></ul>|  
     |**Microsoft EAP-TTLS**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>PPTP</li><li>IKEv2</li><li>L2TP</li></ul>|  
     |**EAP protegido (PEAP) da Microsoft**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**Senha de segurança da Microsoft (EAP-MSCHAP v2)**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**Cartão inteligente ou outro certificado**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**MSCHAP v2**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**RSA SecurID** (Somente iOS)|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**Usar certificados do computador**|<ul><li>IKEv2</li></ul>|  

      Dependendo das opções selecionadas, você poderá receber uma solicitação para especificar mais informações, como:  

     - **Lembre-se as credenciais do usuário a cada logon**: As credenciais do usuário sejam lembradas para que os usuários não precisem inseri-las a cada vez que se conectam.  

     - **Selecione um certificado de cliente para autenticação de cliente**: Selecione o cliente criado anteriormente [certificado SCEP](create-pfx-certificate-profiles.md) que é usado para autenticar a conexão VPN.   

       > [!NOTE]  
       >  Para dispositivos com iOS, o perfil SCEP selecionado é inserido no perfil de VPN. Para outras plataformas, uma regra de aplicabilidade é adicionada para garantir que o perfil de VPN não seja instalado se o certificado não estiver presente ou não for compatível.  
       >   
       >  Se o certificado SCEP especificado não for compatível ou não tiver sido implantado, o perfil de VPN não será instalado no dispositivo.
       >  
       >  Dispositivos que executam o iOS dão suporte somente a RSA SecurID e MSCHAP v2 para o método de autenticação quando o tipo de conexão é PPTP. Para evitar erros de relatórios, implante um perfil VPN PPTP separado para dispositivos que executam o iOS.   

     - **Acesso condicional**  
         - Escolha **Habilitar o acesso condicional para esta conexão de VPN** para garantir que os dispositivos que se conectam à VPN sejam testados quanto à conformidade de acesso condicional antes de se conectar. Para mais informações, veja [Políticas de conformidade do dispositivo](/sccm/protect/deploy-use/device-compliance-policies).  

         - Escolha **Habilitar logon único (SSO) com certificado alternativo** para escolher um certificado diferente do certificado Autenticação de VPN para a conformidade do dispositivo. Se você escolher essa opção, forneça o **EKU** (lista separada por vírgulas) e o **Hash do Emissor** para o certificado correto que o Cliente VPN deve localizar.  

       - Para **Proteção de Informações do Windows**, forneça a identidade corporativa gerenciada pela empresa, que normalmente é o domínio primário da organização, por exemplo, *contoso.com*. Você pode especificar vários domínios pertencentes a sua organização, separando-os com o caractere "|". Por exemplo, *contoso.com|newcontoso.com*. Para obter mais informações, veja [Criar e implantar a política de proteção de aplicativo Proteção de Informações do Windows com o Intune](/intune/windows-information-protection-policy-create).   

       ![Criar Assistente de Perfil de VPN, página Método de Autenticação](media/vpn-conditional-access.png)

       Quando a versão de cliente do Windows dá suporte, é disponibilizada a opção para **Configurar** o método de autenticação. Esta opção abre a caixa de diálogo de propriedades do Windows para configurar o método de autenticação. Se **Configurar** estiver desabilitada, use meios diferentes para configurar as propriedades do método de autenticação.  

7. Na página **Configurações de Proxy** do **Assistente para Criar Perfil VPN**, marque a caixa **Definir configurações de proxy para este perfil VPN** caso a sua conexão VPN use um servidor proxy. Em seguida, forneça as informações do servidor proxy. Para obter mais informações, consulte a documentação do Windows Server.  

   > [!NOTE]  
   >  Em computadores com Windows 8.1, o perfil VPN não exibirá as informações de proxy até você se conectar à VPN usando esse computador.  


8. Configurar outras configurações de DNS, se for necessário.  

9. Conclua o assistente. O nó **Perfis de VPN** no workspace **Ativos e Conformidade** mostra o novo perfil de VPN.  



## <a name="next-steps"></a>Próximas etapas  
Para saber mais sobre como implantar perfis de VPN, veja [Implantar Wi-Fi, VPN, email e perfis de certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

 Use os artigos a seguir para ajudá-lo a planejar, configurar, operar e manter perfis VPN:  

-   [Pré-requisitos para perfis de VPN](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Segurança e privacidade para perfis de VPN](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
