---
title: Introdução aos perfis de certificado
titleSuffix: Configuration Manager
description: Saiba como os perfis de certificado no System Center Configuration Manager funcionam com Serviços de Certificados do Active Directory.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c4230b935b7fabc44743d57fcb2315348edb4274
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32349680"
---
# <a name="introduction-to-certificate-profiles-in-system-center-configuration-manager"></a>Introdução aos perfis de certificado no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Os perfis de certificado funcionam com os Serviços de Certificados do Active Directory e a função NDES (Serviço de Registro de Dispositivo de Rede). Crie e implante certificados de autenticação para dispositivos gerenciados para que os usuários possam acessar facilmente os recursos da empresa. Por exemplo, você pode criar e implantar perfis de certificado para fornecer os certificados necessários para que os usuários se conectem a conexões de VPN e sem fio.

Os perfis de certificado podem configurar dispositivos de usuário automaticamente. Os usuários acessam os recursos da empresa, como redes Wi-Fi e servidores de VPN, sem instalar certificados manualmente nem usar um processo fora de banda. Os perfis de certificado ajudam a manter os recursos da empresa protegidos, porque permitem usar configurações mais seguras compatíveis com a PKI (infraestrutura de chave pública) da empresa. Por exemplo, exigir autenticação de servidor para todas as conexões de VPN e Wi-Fi porque você implantou os certificados necessários nos dispositivos gerenciados.   

Os perfis de certificado oferecem os seguintes recursos de gerenciamento:  

-   Registro de certificado e renovação de uma AC (autoridade de certificação) corporativa para dispositivos que executam iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop e Mobile e Android. Esses certificados podem ser usados para conexões Wi-Fi e VPN.  

-   Implantação de certificados AC raiz confiáveis e de certificados AC intermediários. Esses certificados configuram uma cadeia de confiança em dispositivos para conexões de VPN e Wi-Fi quando a autenticação de servidor é necessária.  

-   Monitorar e emitir relatórios sobre os certificados instalados.  

**Exemplo:** Todos os funcionários devem conseguir se conectar aos pontos de acesso Wi-Fi em vários locais corporativos. Para habilitar a conexão fácil do usuário, primeiro implante os certificados necessários para a conexão com o Wi-Fi. Em seguida, implante perfis de Wi-Fi que referenciem o certificado.  

**Exemplo:** você tem uma PKI em vigor. Você deseja passar para um método mais flexível e seguro de implantação de certificados. Os usuários devem ser capazes de acessar recursos da empresa em seus dispositivos pessoais sem comprometer a segurança. Configurar perfis de certificado com configurações e protocolos com suporte pela plataforma específica do dispositivo. Os dispositivos podem solicitar automaticamente esses certificados de um servidor de registro da Internet. Em seguida, configurar perfis VPN para usar esses certificados para que o dispositivo possa acessar os recursos da empresa.  



## <a name="types-of-certificate-profiles"></a>Tipos de perfis de certificado  
 Há três tipos de perfis de certificado:  

-   **Certificado de Autoridade de Certificação confiável** – implantar um certificado AC raiz confiável ou um certificado AC intermediário. Esses certificados formam uma cadeia de confiança quando o dispositivo precisa autenticar um servidor.  

-   **SCEP (protocolo SCEP)** – solicitar um certificado para um dispositivo ou usuário usando o protocolo SCEP. Esse tipo requer a função NDES (Serviço de Registro de Dispositivo de Rede) em um servidor que execute o Windows Server 2012 R2 ou posterior.

    Para criar um perfil de certificado **SCEP (protocolo SCEP)**, primeiro crie um perfil **Certificado de Autoridade de Certificação confiável**.

-   **Troca de informações pessoais (.pfx)** – solicitar um certificado .pfx (também conhecido como PKCS #12) para um dispositivo ou usuário.<!--1321368-->  

    Você pode criar perfis de certificado PFX [importando credenciais](/sccm/mdm/deploy-use/import-pfx-certificate-profiles) de certificados existentes ou [definindo uma autoridade de certificação](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) para processar solicitações.

    > [!Note]  
    > O Configuration Manager não habilita esse recurso opcional por padrão. É necessário habilitar esse recurso antes de usá-lo. Para obter mais informações, confira [Habilitar recursos opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

    Começando com a versão 1706, você pode usar a Microsoft ou a Entrust como autoridades de certificação para certificados de **Troca de informações pessoais (.pfx)**.


## <a name="requirements-and-supported-platforms"></a>Requisitos e plataformas com suporte  
Para implantar perfis de certificado que usam o SCEP, instale o ponto de registro de certificado em um servidor do sistema de sites. Também instale um módulo de política para NDES, o módulo de política do Configuration Manager, em um servidor que execute o Windows Server 2012 R2 ou posterior. Este servidor requer a função Serviços de Certificados do Active Directory e um NDES operacional que esteja acessível para os dispositivos que exigem os certificados. Para os dispositivos registrados pelo Microsoft Intune, o NDES precisar estar acessível pela Internet. Por exemplo, em uma sub-rede filtrada, também conhecida como DMZ.  

Os certificados PFX também exigem um ponto de registro de certificado. Também especifique a AC (autoridade de certificação) do certificado e as credenciais de acesso relevantes. A partir da versão 1706, você pode especificar a Microsoft ou Entrust como autoridades de certificação.  

Para obter mais informações sobre como o Serviço de Registro de Dispositivo de Rede dá suporte a um módulo de política para que o Configuration Manager possa implantar certificados, consulte [Usando um Módulo de Política com o Serviço de Registro de Dispositivo de Rede](http://go.microsoft.com/fwlink/p/?LinkId=328657).  

Dependendo dos requisitos, o Configuration Manager permite implantar certificados em diferentes repositórios de certificados em vários tipos de dispositivos e sistemas operacionais. Os seguintes dispositivos e sistemas operacionais têm suporte:  

-   Windows RT 8.1  

-   Windows 8.1  

-   Windows Phone 8.1  

-   Windows 10 Desktop e Mobile  

-   iOS  

-   Android  

> [!IMPORTANT]  
>  Para implantar perfis em dispositivos Android, iOS, Windows Phone e em dispositivos registrados Windows 8.1 ou posteriores, esses dispositivos devem ser [registrados no Microsoft Intune](/intune/device-enrollment).   

Um cenário típico do Configuration Manager é instalar certificados AC raiz confiáveis para autenticar servidores de Wi-Fi e de VPN quando a conexão usa os protocolos de autenticação EAP-TLS, EAP-TTLS e PEAP, além dos protocolos de túnel de VPN IKEv2, L2TP/IPsec e Cisco IPsec.  

É necessário instalar um certificado AC raiz corporativo no dispositivo para que o dispositivo possa solicitar certificados usando um perfil de certificado SCEP.  

Você pode especificar configurações em um perfil de certificado do SCEP para solicitar certificados personalizados para diferentes ambientes ou requisitos de conectividade. O **Assistente para Criar Perfil de Certificado** tem duas páginas de parâmetros de registro. A primeira, **Registro do SCEP**, inclui configurações para a solicitação de registro e onde instalar o certificado. A segunda, **Propriedades do Certificado**, descreve o certificado solicitado.  

## <a name="deploying-certificate-profiles"></a>Implantando de perfis de certificado  
 Quando você implanta um perfil de certificado, os arquivos de certificado dentro do perfil são instalados em dispositivos clientes. Todos os parâmetros do SCEP também são implantados, e as solicitações do SCEP são processadas no dispositivo cliente. Você pode implantar perfis de certificado em coleções de usuários ou de dispositivos e especificar o armazenamento de destino para cada certificado. Regras de aplicabilidade determinam se os certificados podem ser instalados no dispositivo. Quando os perfis de certificado são implantados em coleções de usuários, a afinidade de dispositivo de usuário determina quais dos dispositivos de usuários devem instalar os certificados. Quando os perfis de certificado que incluem certificados de usuário são implantados em coleções de dispositivos, por padrão, os certificados são instalados em cada um dos dispositivos primários dos usuários. Você pode modificar esse comportamento para instalar o certificado em qualquer um dos dispositivos dos usuários na página **Registro do protocolo SCEP** do **Assistente para Criar Perfil de Certificado**. Se os dispositivos forem computadores do grupo de trabalho, os certificados de usuário não serão implantados.  

## <a name="monitoring-certificate-profiles"></a>Monitorando perfis de certificado  

Você pode monitorar implantações de perfil de certificado exibindo resultados de conformidade ou relatórios. Essas abordagens estão descritas em [Como monitorar perfis de certificado](/sccm/protect/deploy-use/monitor-certificate-profiles).


## <a name="automatic-revocation-of-certificates"></a>Revogação automática de certificados  
 O System Center Configuration Manager revoga automaticamente os certificados de usuário e do computador implantados usando perfis de certificado nas seguintes circunstâncias:  

-   O dispositivo é desativado do gerenciamento do System Center Configuration Manager.  

-   O dispositivo é apagado seletivamente.  

-   O dispositivo é bloqueado da hierarquia do System Center Configuration Manager.  

 Para revogar os certificados, o servidor do site envia um comando de revogação para a autoridade de certificação emissora. O motivo da revogação é **Cessação da Operação**.  
