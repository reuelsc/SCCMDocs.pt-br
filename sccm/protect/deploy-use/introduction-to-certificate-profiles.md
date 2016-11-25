---
title: "Introdução aos perfis de certificado | System Center Configuration Manager"
description: "Saiba como os perfis de certificado no System Center Configuration Manager funcionam com Serviços de Certificados do Active Directory."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
caps.latest.revision: 7
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 41567ba411732baf9e920595203f699179dcb20a


---
# <a name="introduction-to-certificate-profiles-in-system-center-configuration-manager"></a>Introdução aos perfis de certificado no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Os perfis de certificado do System Center Configuration Manager integram-se aos Serviços de Certificados do Active Directory e à função do Serviço de Registro de Dispositivo de Rede para provisionar os certificados de autenticação para dispositivos gerenciados para que os usuários possam acessar os recursos da empresa sem problemas. Por exemplo, você pode criar e implantar perfis de certificado para fornecer os certificados necessários para que os usuários iniciem conexões VPN e sem fio.  

 Os perfis de certificado no System Center Configuration Manager oferecem os seguintes recursos de gerenciamento:  

-   Registro de certificado e renovação de uma AC (autoridade de certificação) corporativa para dispositivos que executam iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop e Mobile e Android. Esses certificados podem ser usados para conexões Wi-Fi e VPN.  

-   Implantação de certificados de autoridade de certificação raiz confiável e certificados de autoridade de certificação intermediários para configurar uma cadeia de confiança em dispositivos para conexões VPN e Wi-Fi, quando a autenticação de servidor for exigida.  

-   Monitorar e emitir relatórios sobre os certificados instalados.  

 Os perfis de certificado podem configurar automaticamente dispositivos de usuários para que os recursos da empresa, como redes Wi-Fi e servidores VPN, possam ser acessados sem a necessidade de instalar certificados manualmente ou usar um processo fora da banda. Perfis de certificado também podem ajudar a manter os recursos da empresa protegidos, porque você pode usar configurações mais seguras que têm suporte por sua infraestrutura de chave pública (PKI) corporativa. Por exemplo, você pode exigir autenticação de servidor para todas as conexões VPN e Wi-Fi porque provisionou os certificados necessários nos dispositivos gerenciados.  

 **Exemplo:** Todos os funcionários devem conseguir se conectar aos pontos de acesso Wi-Fi em vários locais corporativos. Para tal, é possível implantar os certificados necessários para estabelecer a conexão Wi-Fi e também implantar perfis de Wi-Fi no System Center Configuration Manager que referenciam o certificado correto a ser usado para que a conexão Wi-Fi seja estabelecida para os usuários sem problemas.  

 **Exemplo:** Você tem uma PKI implementada e desejar mover para um método mais flexível e seguro de provisionamento de certificados que permite aos usuários acessar os recursos da empresa em seus dispositivos pessoais sem comprometer a segurança. Para fazer isso, você pode configurar perfis de certificado com configurações e protocolos com suporte para a plataforma específica do dispositivo. Os dispositivos podem solicitar automaticamente esses certificados de um servidor de registro da Internet. Você pode configurar perfis VPN para usar esses certificados para que o dispositivo possa acessar os recursos da empresa.  

## <a name="types-of-certificate-profile"></a>Tipos de perfil de certificado  
 É possível criar três tipos de perfis de certificado no System Center Configuration Manager:  

-   **Certificado de AC confiável** - Permite implantar uma AC de raiz ou intermediária confiável para formar uma cadeia de certificados de confiança quando o dispositivo precisar autenticar-se em um servidor.  

-   **Protocolo SCEP** – permite solicitar um certificado para um dispositivo ou usuário usando o protocolo SCEP e o Serviço de Registro de Dispositivo de Rede em um servidor que executa o Windows Server 2012 R2.
-   -   **Troca de informações pessoais (.pfx)** – Permite solicitar um certificado para um dispositivo ou usuário usando o protocolo SCEP e o Serviço de Registro de Dispositivo de Rede em um servidor que executa o Windows Server 2012 R2.

    > [!NOTE]  
    >  Você deve criar um perfil de certificado do tipo **Certificado de AC confiável** para poder criar um perfil de certificado do tipo **Configurações do protocolo SCEP**.  

## <a name="requirements-and-supported-platforms"></a>Requisitos e plataformas com suporte  
 Para implantar perfis de certificado que usam o protocolo SCEP, você deve instalar o ponto de registro de certificado em um servidor do sistema de site no site de administração central ou em um site primário. Além disso, você deve instalar um módulo de política para o Serviço de Registro de Dispositivo de Rede, o Módulo de Política do Configuration Manager, em um servidor que executa o Windows Server 2012 R2 com a função de Serviços de Certificados do Active Directory e um Serviço de Registro de Dispositivo de Rede operacional que possa ser acessado pelos dispositivos que exigem os certificados. Para dispositivos registrados pelo Microsoft Intune, isso requer que o Serviço de Registro de Dispositivo de Rede esteja acessível da Internet, por exemplo, em uma sub-rede filtrada (também conhecida como DMZ).  

 Para obter mais informações sobre como o Serviço de Registro de Dispositivo de Rede dá suporte a um módulo de política para que o System Center Configuration Manager possa implantar certificados, consulte [Usando um módulo de política com o Serviço de Registro de Dispositivo de Rede](http://go.microsoft.com/fwlink/p/?LinkId=328657).  

 O System Center Configuration Manager dá suporte à implantação de certificados em repositórios de certificado diferentes, dependendo do requisito, e também do tipo de dispositivo e sistema operacional. Os seguintes dispositivos e sistemas operacionais têm suporte:  

-   Windows RT 8.1  

-   Windows 8.1  

-   Windows Phone 8.1  

-   Windows 10 Desktop e Mobile  

-   iOS  

-   Android  

> [!IMPORTANT]  
>  Para implantar perfis em dispositivos Android, iOS, Windows Phone e em dispositivos registrados Windows 8.1 ou posteriores, esses dispositivos devem ser registrados no Microsoft Intune. Para obter informações sobre como registrar seus dispositivos, veja [Gerenciar dispositivos móveis com o Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).  

 Um cenário típico do System Center Configuration Manager é instalar certificados de AC raiz confiável para autenticar servidores Wi-Fi e VPN quando a conexão usa protocolos de autenticação EAP-TLS, EAP-TTLS e PEAP, além de protocolos de túnel IKEv2, L2TP/IPsec e Cisco IPsec VPN.  

 Você deve verificar se um certificado de autoridade de certificação raiz corporativo está instalado no dispositivo para que ele possa solicitar certificados usando um perfil de certificado SCEP.  

 Você pode especificar uma variedade de configurações em um perfil de certificado do protocolo SCEP para solicitar certificados personalizados para diferentes ambientes ou requisitos de conectividade. O **Assistente para Criar Perfil de Certificado** contém duas páginas de parâmetros de registro. A primeira, **Registro de SCEP**, contém as configurações da solicitação de registro e o local onde o certificado deve ser instalado. A segunda, **Propriedades do Certificado**, descreve o certificado solicitado.  

## <a name="deploying-certificate-profiles"></a>Implantando de perfis de certificado  
 Quando você implanta um perfil de certificado, os arquivos de certificado dentro do perfil são instalados em dispositivos clientes. Todos os parâmetros SCEP também serão implantados, e as solicitações de SCEP serão processadas no dispositivo cliente. Você pode implantar perfis de certificado em coleções de usuários ou coleções de dispositivos e especificar o armazenamento de destino para cada certificado. Regras de aplicabilidade determinam se os certificados podem ser instalados no dispositivo. Quando os perfis de certificado são implantados em coleções de usuários, a afinidade de dispositivo de usuário determina quais dos dispositivos de usuários instalarão os certificados. Quando os perfis de certificado que contêm certificados de usuário são implantados em coleções de dispositivos, por padrão, os certificados serão instalados em cada um dos dispositivos primários dos usuários. É possível modificar esse comportamento para instalar o certificado em qualquer um dos dispositivos dos usuários na página **Registro do protocolo SCEP** do **Assistente Criar Perfil de Certificado**. Além disso, os certificados de usuário não serão implantados em dispositivos se eles forem computadores de grupo de trabalho.  

## <a name="monitoring-certificate-profiles"></a>Monitorando perfis de certificado  
 É possível monitorar implantações do perfil de certificado no nó **Implantações** do espaço de trabalho **Monitoramento** no console do System Center Configuration Manager.  

 Também é possível usar um dos seguintes relatórios do System Center Configuration Manager para monitorar perfis de certificado:  

-   **Histórico de certificados que são emitidos pelo ponto de registro de certificado**  

-   **Lista de ativos por estado de emissão de certificado para certificados registrados pelo ponto de registro de certificado**  

-   **Lista de ativos com certificados próximos da data de expiração**  

## <a name="automatic-revocation-of-certificates"></a>Revogação automática de certificados  
 O System Center Configuration Manager revoga automaticamente os certificados de usuário e do computador implantados usando perfis de certificado nas seguintes circunstâncias:  

-   O dispositivo é desativado do gerenciamento do System Center Configuration Manager.  

-   O dispositivo é apagado seletivamente.  

-   O dispositivo é bloqueado da hierarquia do System Center Configuration Manager.  

 Para revogar os certificados, o servidor do site envia um comando de revogação para a autoridade de certificação emissora. O motivo da revogação é **Cessação da Operação**.  



<!--HONumber=Nov16_HO1-->


