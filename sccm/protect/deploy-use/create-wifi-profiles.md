---
title: Crie perfis Wi-Fi | Microsoft Docs
description: "Saiba como usar perfis de Wi-Fi no System Center Configuration Manager para implantar as configurações de rede sem fio para usuários em sua organização."
ms.custom: na
ms.date: 12/11/2016
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
ms.sourcegitcommit: 22a74f3b12fe4f4559b682a8fcb287863a7686af
ms.openlocfilehash: 1262cb7d524fdce21f778e2179275bd177e9330f


---
# <a name="how-to-create-wi-fi-profiles-in-system-center-configuration-manager"></a>Como criar perfis de Wi-Fi no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Use perfis de Wi-Fi no System Center Configuration Manager para implantar as configurações de rede sem fio para usuários na sua organização. Ao implantar essas configurações, você facilita que os usuários se conectem ao Wi-Fi.  

 Por exemplo, você tem uma rede Wi-Fi que deseja habilitar para a conexão de todos os dispositivos iOS. Crie um perfil de Wi-Fi contendo as configurações necessárias para conectar-se à rede sem fio. Em seguida, implante o perfil para todos os usuários com dispositivos iOS na sua hierarquia. Os usuários de dispositivos iOS veem a rede da empresa na lista de redes sem fio e prontamente podem se conectar a essa rede.  

 Você pode configurar os seguintes tipos de dispositivo com perfis Wi-Fi:  

-   Dispositivos que executam o Windows 8.1 32 bits  

-   Dispositivos que executam o Windows 8.1 64-bit  

-   Dispositivos que executam o Windows RT 8.1  

-   Dispositivos que executam o Windows Phone 8.1  

-   Dispositivos que executam o Windows 10 Desktop ou Mobile  

-   Dispositivos IPhone que executam o iOS 5, iOS 6, iOS 7 e iOS 8  

-   Dispositivos IPad que executam o iOS 5, iOS 6, iOS 7 e iOS 8  

-   Dispositivos Android que executam a versão 4 ou posterior

> [!IMPORTANT]  
>  Para implantar perfis em dispositivos Android, iOS, Windows Phone e em dispositivos registrados Windows 8.1 ou posteriores, esses dispositivos devem ser registrados no Microsoft Intune. Para obter informações sobre como registrar seus dispositivos, consulte [Registrar dispositivos para gerenciamento no Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).  

 Ao criar um perfil Wi-Fi, você pode incluir uma várias configurações de segurança. Essas configurações incluem os certificados para validação de servidor e autenticação de cliente que foram enviados por push usando os perfis de certificado do Configuration Manager. Para obter mais informações sobre perfis de certificado, consulte [Perfis de certificado do System Center Configuration Manager](introduction-to-certificate-profiles.md).  

## <a name="create-a-wi-fi-profile"></a>Criar um perfil de Wi-Fi  

1.  No console do Configuration Manager, escolha **Ativos e Conformidade** > **Configurações de Conformidade** >  **Acesso a Recursos da Empresa** > **Perfis de Wi-Fi**.  

3.  Na guia **Início**, no grupo **Criar**, clique em **Criar Perfil Wi-Fi**.  

1.  Na página **Geral**, insira um nome exclusivo e uma descrição para o perfil de Wi-Fi.  Se quiser usar as configurações de outro perfil de Wi-Fi, selecione **Importar um item de perfil Wi-Fi existente de um arquivo**.  

    > [!IMPORTANT]  
    >  Verifique se o perfil de Wi-Fi importado contém um XML válido para um perfil de Wi-Fi. O Configuration Manager não valida o perfil quando você importa o arquivo.  

3.  Em **Gravidade de não conformidade dos relatórios**, especifique o nível de gravidade relatado se o perfil Wi-Fi for considerado como não compatível nos dispositivos cliente (por exemplo, se a instalação do perfil falhar). Os níveis de severidade disponíveis são os seguintes:  

    -   **Nenhum**: computadores que não cumprem essa regra de conformidade não relatam uma severidade de falha em relatórios do Configuration Manager.  

    -   **Informações**: computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Informações** em relatórios do Configuration Manager.  

    -   **Aviso**: computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Aviso** em relatórios do Configuration Manager.  

    -   **Crítico**: computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico** em relatórios do Configuration Manager.  

    -   **Crítico com evento**: computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico** em relatórios do Configuration Manager. Esse nível de severidade também é registrado como um evento do Windows no log de eventos de aplicativos.  

1.  Na página **Perfil de Wi-Fi** forneça o nome que os dispositivos exibirão como o nome da rede.  

    > [!IMPORTANT]  
    >  O Configuration Manager não dá suporte ao uso de apóstrofos (**â€˜**) ou vírgulas (**,**) no nome da rede.  

2.  Especifique a **SSID** que diferencia maiúsculas de minúsculas
3.  Escolha também as outras opções de conectividade apropriadas.   **Conectar-se quando a rede não estiver transmitindo seu nome (SSID)**, se houver uma possibilidade de que o SSID esteja oculto  

4.  Na página **Configuração de Segurança**, selecione o protocolo de segurança usado pela rede sem fio ou selecione **Sem autenticação (Aberta)** se a rede não for segura.
    > [!IMPORTANT]  
    >  Se você estiver criando um perfil de Wi-Fi para o Gerenciamento de Dispositivo Móvel Local, o branch atual do Configuration Manager dará suporte somente às seguintes configurações de segurança de Wi-Fi:  
    >   
    >  Tipos de segurança: **WPA2 Enterprise** ou **WPA2 Personal**  
    > Tipos de criptografia: **AES** ou **TKIP**  
    > Tipos de EAP: **Cartão inteligente ou outro certificado** ou **PEAP**  
  
    > Para dispositivos Android, os tipos de segurança **WPA Pessoal**, **WPA2 Pessoal** e **WEP** não têm suporte.  

2.  selecione o método de criptografia usado pela rede sem fio.  

3.  selecione o tipo de EAP usado para autenticação na rede sem fio.  

     Somente para dispositivos Windows Phone: os tipos de EAP **LEAP** e **EAP-FAST** não têm suporte.  

4.  Clique em **Configurar** para especificar as propriedades para o tipo de EAP selecionada. Essa opção pode não estar disponível para alguns tipos de EAP selecionados.  

    > [!IMPORTANT]  
    >  Ao clicar em **Configurar**, a caixa de diálogo que abre é uma do Windows. Por isso, você deve verificar se o sistema operacional do computador que executa o console do Configuration Manager dá suporte à configuração do tipo de EAP selecionado.  
    >   
    >  Para dispositivos do iOS, se você escolher um método não EAP para autenticação, independentemente do método escolhido, o MS-CHAP v2 será usado para a conexão.  

5.  Se você quiser armazenar as credenciais de usuários para que eles não precisem inseri-las a cada logon, selecione **Lembrar as credenciais do usuário a cada logon**.  

6. **Apenas para dispositivos iOS:**  
 configure informações de todos os certificados necessários para a conexão Wi-Fi. Você deve configurar o certificado de cliente e o nome do certificado de servidor confiável ou o certificado raiz, da seguinte maneira:  

    -   **Nomes de certificado de servidor confiável**: se o servidor ao qual o dispositivo se conecta usar um certificado de autenticação de servidor para identificar o servidor e ajudar a proteger o canal de comunicação, insira os nomes que aparecem no nome da entidade ou no nome alternativo da entidade desse certificado. O nome ou os nomes são normalmente o nome de domínio totalmente qualificado do servidor. Por exemplo, se o certificado do servidor tiver um nome comum de srv1.contoso.com na entidade do certificado, digite **srv1.contoso.com**. Se houver vários nomes especificados para o certificado do servidor no nome alternativo da entidade, insira cada nome, separado por ponto-e-vírgula.  

    > [!TIP]  
    >  Se o certificado de cliente selecionado para autenticação de cliente ou EAP para um dispositivo iOS for usado para autenticação em um servidor RADIUS, como um servidor que executa o Servidor de Políticas de Rede, o Nome Alternativo da Entidade deverá ser definido como o UPN.  

    -   **Selecionar certificados raiz para validação do servidor**: se o servidor ao qual o dispositivo se conecta usar um certificado de autenticação de servidor não confiável para o dispositivo, selecione o perfil de certificado que contém o certificado raiz do certificado do servidor, a fim de criar uma cadeia de certificados de confiança no dispositivo.  

    -   **Selecionar um certificado do cliente para autenticação do cliente**: se o servidor ou o dispositivo de rede exigir um certificado de cliente para autenticar o dispositivo que está sendo conectado, selecione o perfil de certificado que contém o certificado de autenticação de cliente.  

    > [!NOTE]  
    >  Antes de selecionar o certificado raiz e o certificado de cliente, você deve configurá-los e implantá-los como um perfil de certificado. Para obter mais informações sobre perfis de certificado, consulte [Perfis de certificado do System Center Configuration Manager](introduction-to-certificate-profiles.md).  

7.  Na página **Configurações Avançadas**, especifique configurações avançadas para o perfil Wi-Fi, como o modo de autenticação, as opções de logon único e a conformidade com FIPS (Federal Information Processing Standards). Para obter mais informações sobre essas opções, consulte a documentação do Windows. É possível que não haja configurações avançadas disponíveis ou elas poderão variar, dependendo das opções selecionadas na página **Configuração de Segurança** do assistente.  

1.  Na página **Configurações de Proxy**, selecione **Definir configurações de proxy para este perfil Wi-Fi** se sua rede sem fio usa um servidor proxy e, em seguida, forneça as informações de configuração.  

2. Na página **Plataformas com Suporte**, selecione os sistemas operacionais nos quais você deseja instalar o perfil Wi-Fi. Opcionalmente, clique em **Selecionar tudo** para instalar o perfil Wi-Fi em todos os sistemas operacionais disponíveis.  

### <a name="next-steps"></a>Próximas etapas
 Para obter informações sobre como implantar o perfil Wi-Fi, consulte [Como implantar perfis de Wi-Fi no System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  



<!--HONumber=Dec16_HO3-->


