---
title: Criar perfis Wi-Fi | System Center Configuration Manager
description: "Saiba como usar perfis de Wi-Fi no System Center Configuration Manager para implantar as configurações de rede sem fio para usuários em sua organização."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
caps.latest.revision: 13
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 295ccc2ce7c1dae55c45113cc8ff826e30f7079a


---
# <a name="how-to-create-wi-fi-profiles-in-system-center-configuration-manager"></a>Como criar perfis de Wi-Fi no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Use perfis de Wi-Fi no System Center Configuration Manager para implantar as configurações de rede sem fio para usuários na sua organização. Ao implantar essas configurações, você facilita que os usuários se conectem ao Wi-Fi.  

 Por exemplo, você instalou uma nova rede Wi-Fi chamada **Contoso Wi-Fi**. Agora você deseja provisionar todos os dispositivos que executam o sistema operacional iOS com as configurações necessárias para conectar-se a essa rede. Você pode criar um perfil de Wi-Fi contendo as configurações necessárias para conectar-se à rede sem fio **Contoso Wi-Fi** . Em seguida, você pode implantar esse perfil a todos os usuários que possuem dispositivos que executam o iOS na sua hierarquia. Os usuários de dispositivos iOS veem a rede da empresa na lista de redes sem fio e prontamente podem se conectar a essa rede.  

 Você pode configurar os seguintes tipos de dispositivo com perfis Wi-Fi:  

-   Dispositivos que executam o Windows 8.1 32 bits  

-   Dispositivos que executam o Windows 8.1 64-bit  

-   Dispositivos que executam o Windows RT 8.1  

-   Dispositivos que executam o Windows Phone 8.1  

-   Dispositivos que executam o Windows 10 Desktop ou Mobile  

-   Dispositivos IPhone que executam o iOS 5, iOS 6, iOS 7 e iOS 8  

-   Dispositivos IPad que executam o iOS 5, iOS 6, iOS 7 e iOS 8  

-   Dispositivos Android que executam a versão 4  

> [!IMPORTANT]  
>  Para implantar perfis em dispositivos Android, iOS, Windows Phone e em dispositivos Windows 8.1 ou posteriores registrados, esses dispositivos devem ser registrados no Microsoft Intune]. Para obter informações sobre como registrar seus dispositivos, consulte [Registrar dispositivos para gerenciamento no Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).  

 Ao criar um perfil Wi-Fi, você pode incluir uma várias configurações de segurança. Essas configurações incluem os certificados para validação de servidor e autenticação de cliente que foram provisionados com os perfis de certificado do Configuration Manager. Para obter mais informações sobre perfis de certificado, consulte [Perfis de certificado do System Center Configuration Manager](introduction-to-certificate-profiles.md).  

## <a name="steps-to-create-a-wi-fi-profile"></a>Etapas para criar um perfil Wi-Fi  
 Use as seguintes etapas necessárias para criar um perfil Wi-Fi usando o **Assistente para Criar Perfil Wi-Fi**.  

-   [Etapa 1: Iniciar o Assistente para Criar Perfil Wi-Fi](#BKMK_Step1)  

-   [Etapa 2: Fornecer informações gerais sobre o perfil Wi-Fi](#BKMK_Step2)  

-   [Etapa 3: Fornecer informações sobre a rede sem fio](#BKMK_Step3)  

-   [Etapa 4: Configurar a segurança para o perfil Wi-Fi](#BKMK_Step4)  

-   [Etapa 5: Definir configurações avançadas para o perfil Wi-Fi](#BKMK_Step5)  

-   [Etapa 6: Definir configurações de proxy para o perfil Wi-Fi](#BKMK_Step6)  

-   [Etapa 7: Configurar plataformas com suporte para o perfil Wi-Fi](#BKMK_Step7)  

-   [Etapa 8: concluir o assistente](#BKMK_Step8)  

##  <a name="a-namebkmkstep1a-step-1-start-the-create-wi-fi-profile-wizard"></a><a name="BKMK_Step1"></a> Etapa 1: Iniciar o Assistente para Criar Perfil Wi-Fi  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , expanda **Configurações de Conformidade**, expanda **Acesso aos Recursos da Empresa**e clique em **Perfis Wi-Fi**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Perfil Wi-Fi**.  

##  <a name="a-namebkmkstep2a-step-2-provide-general-information-about-the-wi-fi-profile"></a><a name="BKMK_Step2"></a> Etapa 2: Fornecer informações gerais sobre o perfil Wi-Fi  

1.  Na página **Geral** do assistente Criar perfil de Wi-Fi, insira um nome exclusivo e uma descrição para o perfil de Wi-Fi. Você pode usar no máximo 256 caracteres.  

2.  Se quiser usar as configurações de outro perfil de Wi-Fi, selecione **Importar um item de perfil Wi-Fi existente de um arquivo**.  

    > [!IMPORTANT]  
    >  Verifique se o perfil de Wi-Fi importado contém um XML válido para um perfil de Wi-Fi. O Configuration Manager não valida o perfil quando você importa o arquivo.  

3.  No  
                            **Severidade de não conformidade dos relatórios**: especifique o nível de severidade relatado se o perfil Wi-Fi for considerado como não compatível nos dispositivos cliente (por exemplo, se a instalação do perfil falhar). Os níveis de severidade disponíveis são os seguintes:  

    -   **Nenhum**: computadores que não cumprem essa regra de conformidade não relatam uma severidade de falha em relatórios do Configuration Manager.  

    -   **Informações**: computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Informações** em relatórios do Configuration Manager.  

    -   **Aviso**: computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Aviso** em relatórios do Configuration Manager.  

    -   **Crítico**: computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico** em relatórios do Configuration Manager.  

    -   **Crítico com evento**: computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico** em relatórios do Configuration Manager. Esse nível de severidade também é registrado como um evento do Windows no log de eventos de aplicativos.  

##  <a name="a-namebkmkstep3a-step-3-provide-information-about-the-wireless-network"></a><a name="BKMK_Step3"></a> Etapa 3: Fornecer informações sobre a rede sem fio  

1.  Na página **perfil de Wi-Fi** do assistente Criar perfil de Wi-Fi, especifique o nome descritivo para a conexão de Internet sem fio usando um máximo de 32 caracteres. Esse é o nome que esses dispositivos exibirão como o nome da rede.  

    > [!IMPORTANT]  
    >  O Configuration Manager não dá suporte ao uso de apóstrofos (**â€˜**) ou vírgulas (**,**) no nome da rede.  

2.  No **SSID**, especifique o nome (SSID) da rede sem fio à qual você deseja que os dispositivos sejam capazes de se conectar. Você pode usar no máximo 32 caracteres. O nome SSID diferencia maiúsculas de minúsculas, portanto, você deve inseri-la exatamente como ela está configurada.  

3.  Se você deseja permitir que os dispositivos sejam reconectados automaticamente à rede sem fio quando ela estiver no intervalo, selecione **Conectar automaticamente quando esta rede estiver no intervalo**.  

4.  Se você deseja permitir que os dispositivos continuem a verificar se há outras redes sem fio quando estiverem conectados à rede, selecione  
                            **Procurar outras redes sem fio enquanto estiver conectado a essa rede**.  

5.  Se você deseja permitir que os dispositivos se conectem à rede quando ela não estiver visível na lista de redes (porque está oculta e não está transmitindo seu nome), selecione **Conectar quando a rede não esteja transmitindo seu nome (SSID)**,  

##  <a name="a-namebkmkstep4a-step-4-configure-security-for-the-wi-fi-profile"></a><a name="BKMK_Step4"></a> Etapa 4: Configurar a segurança para o perfil Wi-Fi  

> [!IMPORTANT]  
>  Se você estiver criando um perfil de Wi-Fi para o Gerenciamento de Dispositivo Móvel Local, o branch atual do Configuration Manager dará suporte somente às seguintes configurações de segurança de Wi-Fi:  
>   
>  Tipos de segurança: **WPA2 Enterprise** ou **WPA2 Personal**  
> Tipos de criptografia: **AES** ou **TKIP**  
> Tipos de EAP: **Cartão inteligente ou outro certificado** ou **PEAP**  

1.  Na página **Configuração de segurança** do assistente Criar perfil de Wi-Fi, selecione o protocolo de segurança usado pela rede sem fio ou selecione **Sem autenticação (Aberta)** se a rede não for segura.  

     Somente para dispositivos Android: os tipos de segurança **WPA â€“ Pessoal**, **WPA2 â€“ Pessoal** e **WEP** não têm suporte.  

2.  selecione o método de criptografia usado pela rede sem fio.  

3.  selecione o tipo de EAP usado para autenticação na rede sem fio.  

     Somente para dispositivos Windows Phone: os tipos de EAP **LEAP** e **EAP-FAST** não têm suporte.  

4.  Clique em **Configurar** para especificar as propriedades para o tipo de EAP selecionada. Essa opção pode não estar disponível para alguns tipos de EAP selecionados.  

    > [!IMPORTANT]  
    >  Ao clicar em **Configurar**, a caixa de diálogo que abre é uma do Windows. Por isso, você deve verificar se o sistema operacional do computador que executa o console do Configuration Manager dá suporte à configuração do tipo de EAP selecionado.  
    >   
    >  Para dispositivos do iOS, se você escolher um método não EAP para autenticação, independentemente do método escolhido, o MS-CHAP v2 será usado para a conexão.  

5.  Se você quiser armazenar as credenciais de usuários para que eles não precisem inseri-las a cada logon, selecione **Lembrar as credenciais do usuário a cada logon**.  

### <a name="for-ios-devices-only"></a>Apenas para dispositivos iOS:  
 configure informações de todos os certificados necessários para a conexão Wi-Fi. Você deve configurar o certificado de cliente e o nome do certificado de servidor confiável ou o certificado raiz, da seguinte maneira:  

-   **Nomes de certificado de servidor confiável**: se o servidor ao qual o dispositivo se conecta usar um certificado de autenticação de servidor para identificar o servidor e ajudar a proteger o canal de comunicação, insira os nomes que aparecem no nome da entidade ou no nome alternativo da entidade desse certificado. O nome ou os nomes são normalmente o nome de domínio totalmente qualificado do servidor. Por exemplo, se o certificado do servidor tiver um nome comum de srv1.contoso.com na entidade do certificado, digite **srv1.contoso.com**. Se houver vários nomes especificados para o certificado do servidor no nome alternativo da entidade, insira cada nome, separado por ponto-e-vírgula.  

    > [!TIP]  
    >  Se o certificado de cliente selecionado para autenticação de cliente ou EAP para um dispositivo iOS for usado para autenticação em um servidor RADIUS, como um servidor que executa o Servidor de Políticas de Rede, o Nome Alternativo da Entidade deverá ser definido como o UPN.  

-   **Selecionar certificados raiz para validação do servidor**: se o servidor ao qual o dispositivo se conecta usar um certificado de autenticação de servidor não confiável para o dispositivo, selecione o perfil de certificado que contém o certificado raiz do certificado do servidor, a fim de criar uma cadeia de certificados de confiança no dispositivo.  

-   **Selecionar um certificado do cliente para autenticação do cliente**: se o servidor ou o dispositivo de rede exigir um certificado de cliente para autenticar o dispositivo que está sendo conectado, selecione o perfil de certificado que contém o certificado de autenticação de cliente.  

> [!NOTE]  
>  Antes de selecionar o certificado raiz e o certificado de cliente, você deve configurá-los e implantá-los como um perfil de certificado. Para obter mais informações sobre perfis de certificado, consulte [Perfis de certificado do System Center Configuration Manager](introduction-to-certificate-profiles.md).  

##  <a name="a-namebkmkstep5a-step-5-configure-advanced-settings-for-the-wi-fi-profile"></a><a name="BKMK_Step5"></a> Etapa 5: Definir configurações avançadas para o perfil Wi-Fi  
 Na página **Configurações Avançadas** do Assistente para Criar Perfil Wi-Fi, especifique configurações avançadas para o perfil Wi-Fi, como o modo de autenticação, as opções de logon único e a conformidade com FIPS (Federal Information Processing Standards). Para obter mais informações sobre essas opções, consulte a documentação do Windows.  

> [!NOTE]  
>  É possível que não haja configurações avançadas disponíveis ou elas poderão variar, dependendo das opções selecionadas na página **Configuração de Segurança** do assistente.  

##  <a name="a-namebkmkstep6a-step-6-configure-proxy-settings-for-the-wi-fi-profile"></a><a name="BKMK_Step6"></a> Etapa 6: Definir configurações de proxy para o perfil Wi-Fi  

1.  Na página **Configurações de Proxy** do Assistente para Criar Perfil Wi-Fi, marque a caixa de seleção **Definir configurações de proxy para este perfil Wi-Fi** caso a sua rede sem fio use um servidor proxy.  

2.  Especifique os detalhes sobre seu servidor proxy e suas configurações. Para obter mais informações, consulte a documentação do Windows Server.  

##  <a name="a-namebkmkstep7a-step-7-configure-supported-platforms-for-the-wi-fi-profile"></a><a name="BKMK_Step7"></a> Etapa 7: Configurar plataformas com suporte para o perfil Wi-Fi  
 Na página **Plataformas com Suporte** do Assistente para Criar Perfil Wi-Fi, selecione os sistemas operacionais onde você deseja instalar o perfil Wi-Fi. Opcionalmente, clique em **Selecionar tudo** para instalar o perfil Wi-Fi em todos os sistemas operacionais disponíveis.  

##  <a name="a-namebkmkstep8a-step-8-complete-the-wizard"></a><a name="BKMK_Step8"></a> Etapa 8: Concluir o assistente  
 Na página **Resumo** do assistente, examine as ações que ele executará e conclua o assistente. O novo perfil Wi-Fi é exibido no nó **Perfis Wi-Fi** , no espaço de trabalho **Ativos e Conformidade** .  

 Para obter informações sobre como implantar o perfil Wi-Fi, consulte [Como implantar perfis de Wi-Fi no System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  



<!--HONumber=Nov16_HO1-->


