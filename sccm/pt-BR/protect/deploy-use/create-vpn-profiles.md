---
title: 'Como criar perfis de VPN '
titleSuffix: Configuration Manager
description: Saiba como criar perfis de VPN no System Center Configuration Manager.
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d2969a0df23f7e8b74708a4aee03c3ea7f689a99
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-create-vpn-profiles-in-system-center-configuration-manager"></a>Como criar perfis de VPN no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os tipos de conexão disponíveis para as diferentes plataformas de dispositivo estão descritos em [Perfis VPN no System Center Configuration Manager](../../protect/deploy-use/vpn-profiles.md).  

Para conexões VPN de terceiros, distribua o aplicativo VPN antes de implantar o perfil VPN. Se você não implantar o aplicativo, os usuários deverão fazer isso quando eles tentarem se conectar à VPN. Para saber como implantar aplicativos, consulte [Implantar aplicativos com o System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).

### <a name="create-a-vpn-profile"></a>Criar um perfil VPN   

1.  No console do Configuration Manager, escolha **Ativos e Conformidade** > **Configurações de Conformidade** > **Acesso a Recursos da Empresa** > **Perfis VPN**.  

2.  Na guia **Início**, no grupo **Criar**, escolha **Criar Perfil VPN**.  


3.  Conclua a página **Geral**. Observe o seguinte:  

    - Selecione a **Plataforma** apropriada.

       - Se você selecionar a plataforma Windows 8.1, haverá a opção de selecionar **Importar um item de perfil de VPN existente de um arquivo** para importar as informações do perfil de VPN que foram exportadas para um arquivo XML.

    - Não use os caracteres \\/:*?&lt;>&#124; ou o caractere de espaço no nome do perfil VPN. Esses são caracteres sem suporte pelo perfil VPN do Windows Server.  


4.  Na página **Conexão**, especifique:  

    -   **Tipo de conexão**: escolha o tipo de conexão VPN. É possível escolher entre os tipos de conexão na tabela a seguir.  

    -   **Lista de servidores**: adicionar um novo servidor a ser usado para a conexão VPN. Dependendo do tipo de conexão, você pode adicionar um ou mais servidores VPN e especificar o servidor padrão.  

        > [!NOTE]  
        >  Dispositivos que executam iOS não oferecem suporte ao uso de vários servidores VPN. Se você configurar vários servidores VPN e implantar o perfil VPN em um dispositivo iOS, apenas o servidor padrão será usado.  

     Esta tabela fornece opções de tipos de conexão. Consulte a documentação do servidor VPN para obter mais informações.

| &nbsp;&nbsp;Opção&nbsp;&nbsp; | Mais informações | &nbsp;&nbsp;Conexão&nbsp;tipo&nbsp;&nbsp; |  
|----------------|----------------------|---------------------|  
|**Território**     |O realm de autenticação que você deseja usar. Um realm de autenticação é um agrupamento de recursos de autenticação usado pelo tipo de conexão Pulse Secure.|Pulse Secure|    
|**Função**        |A função de usuário que tem acesso a essa conexão. |Pulse Secure|  
|**Grupo de logon ou domínio** |O nome do grupo de logon ou domínio ao qual você deseja se conectar.|Dell SonicWALL Mobile Connect|  
|**Impressão digital**  |Uma cadeia de caracteres, por exemplo "Código de impressões digitais da Contoso" que será usado para verificar que o servidor VPN é confiável.<br /><br /> Uma impressão digital pode ser:<br /><br /> - Enviada ao cliente para que ele saiba que pode confiar em qualquer servidor que apresentar essa impressão digital durante a conexão.<br /><br /> - Se o dispositivo ainda não tiver a impressão digital, ele solicitará ao usuário para confiar no servidor VPN ao qual está se conectando enquanto mostra a impressão digital (o usuário verifica a impressão digital e manualmente escolhe **confiar** para se conectar).|Check Point Mobile VPN|  
|**Enviar todo o tráfego de rede através da conexão VPN** |Se esta opção não estiver marcada, você poderá especificar rotas adicionais para a conexão (para os tipos de conexão **Microsoft SSL (SSTP)**, **Microsoft Automatic**, **IKEv2**, **PPTP** e **L2TP** ), que é conhecida como túnel dividido ou VPN.<br /><br /> Apenas as conexões com a rede da empresa são enviadas por um túnel VPN. O túnel VPN não é usado quando você se conecta aos recursos na Internet. |Todos|  
|**Sufixo DNS específico da conexão** |O sufixo DNS (Sistema de Nomes de Domínio) específico da conexão.|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
|**Ignorar VPN quando conectado à rede Wi-Fi da empresa**  |A conexão VPN não será usada quando o dispositivo estiver conectado à rede Wi-Fi da empresa.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN<br /><br /> - Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - L2TP|  
|**Ignorar VPN quando conectado à rede Wi-Fi local**  |A conexão VPN não será usada quando o dispositivo estiver conectado a uma rede Wi-Fi doméstica.|Todos|  
|**Por aplicativo VPN (iOS 7 e posterior, Mac OS X 10.9 e posterior)** |Associar essa conexão VPN a um aplicativo iOS para que a conexão seja aberta quando o aplicativo é executado. É possível associar o perfil de VPN a um aplicativo ao implantá-lo.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
|**XML personalizado (opcional)** |Especificar comandos XML personalizados que configuram a conexão VPN.<br /><br /> Exemplos:<br /><br /> Para o **Pulse Secure**:<br /><br /> **&lt;pulse-schema><br /> &nbsp; &lt;isSingleSignOnCredential>true&lt;/isSingleSignOnCredential\><br />&lt;/pulse-schema>**<br /><br /> Para o **CheckPoint Mobile VPN**:<br /><br /> **&lt;CheckPointVPN <br /> &nbsp; port="443" name="CheckPointSelfhost" <br /> &nbsp; sso="true" <br /> &nbsp; debug="3"<br />/>**<br /><br /> Para o **Dell SonicWALL Mobile Connect**:<br /><br /> **&lt;MobileConnect\><br />&nbsp; &nbsp; &lt;Compression\>false&lt;/Compression\><br />&nbsp; &nbsp; &lt;debugLogging\>True&lt;/debugLogging\><br />&nbsp; &nbsp; &lt;packetCapture\>False&lt;/packetCapture\><br />&lt;/MobileConnect\>**<br /><br /> Para o **F5 Edge Client**:<br /><br /> **&lt;f5-vpn-conf>&lt;single-sign-on-credential>&lt;/f5-vpn-conf>**<br /><br /> Consulte a documentação do VPN de cada fabricante para obter mais informações sobre como escrever comandos XML personalizados.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  

> [!NOTE]  
>  Para saber mais sobre a criação de perfis de VPN para dispositivos móveis, confira [Criar perfis de VPN](../../mdm/deploy-use/create-vpn-profiles.md)  

Conclua o assistente. O novo perfil VPN é exibido no nó **Perfis VPN** no espaço de trabalho **Ativos e Conformidade** .

### <a name="next-steps"></a>Próximas etapas

- Para conexões VPN de terceiros, distribua o aplicativo VPN antes de implantar o perfil VPN. Se você não implantar o aplicativo, os usuários deverão fazer isso quando eles tentarem se conectar à VPN. Para saber como implantar aplicativos, consulte [Implantar aplicativos com o System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).

- Implante o perfil VPN conforme descrito em [Como implantar perfis VPN no System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  
