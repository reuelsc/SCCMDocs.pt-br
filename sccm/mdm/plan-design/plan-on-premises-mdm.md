---
title: Planejar MDM local
titleSuffix: Configuration Manager
description: Planeje o Gerenciamento de Dispositivo Móvel local para gerenciar dispositivos móveis no System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 577672a6f816eaffc88c78d4baf3feab5b8989a1
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132176"
---
# <a name="plan-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Planejar o gerenciamento de dispositivo móvel local no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Considere os seguintes requisitos antes de preparar a infraestrutura do Configuration Manager para manipular o Gerenciamento de dispositivo móvel local.

##  <a name="bkmk_devices"></a> Dispositivos com suporte  
 O Gerenciamento de Dispositivo Móvel local permite gerenciar dispositivos móveis usando os recursos de gerenciamento inseridos nos sistemas operacionais dos dispositivos.  A funcionalidade de gerenciamento baseia-se no padrão OMA DM (Gerenciamento de Dispositivo da Open Mobile Alliance), e várias plataformas de dispositivo usam esse padrão para permitir que os dispositivos sejam gerenciados.  Nós os chamamos de **dispositivos modernos** (na documentação e na interface do usuário do console do Configuration Manager) para diferenciá-los de outros dispositivos que exigem o cliente do Configuration Manager para gerenciá-los.  

 > [!NOTE]  
>  O branch atual do Configuration Manager dá suporte ao registro no Gerenciamento de Dispositivo Móvel Local para dispositivos que executam os seguintes sistemas operacionais:  
>   
> -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team \(a partir do Configuration Manager versão 1602\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise
> -   Windows 10 IoT Enterprise   

##  <a name="bkmk_intune"></a> Uso da assinatura do Microsoft Intune  
 Para começar a usar o Gerenciamento de dispositivo móvel local, você precisará de uma assinatura do Microsoft Intune. A assinatura apenas é necessária para acompanhar o licenciamento dos dispositivos e não é usada para gerenciar ou armazenar informações de gerenciamento dos dispositivos. Todo o gerenciamento é manipulado na empresa de sua organização usando a infraestrutura do Configuration Manager local.  

 > [!NOTE]  
 > Com início na versão 1610, o Configuration Manager dá suporte ao gerenciamento de dispositivos móveis usando o Microsoft Intune e a infraestrutura local do Configuration Manager ao mesmo tempo.   

 Se o site tiver dispositivos com conectividade com a Internet, o serviço do Intune poderá ser usado para notificar os dispositivos para verificar se há atualizações de política no ponto de gerenciamento de dispositivos. Esse uso do Intune é destinado estritamente à notificação somente de dispositivos conectados à Internet. Dispositivos sem conexão à Internet (e que não podem ser contatados pelo Intune) dependem do intervalo de sondagem configurado para fazer check-in nas funções do sistema de sites para executar funções de gerenciamento.  

> [!TIP]  
>  Recomendamos que você configure o Intune antes de configurar as funções do sistema de sites necessárias para minimizar o tempo exigido para as funções do sistema de sites se tornarem funcionais.  

 Para obter informações sobre como configurar a assinatura do Intune, consulte [Configure uma assinatura do Microsoft Intune para o gerenciamento de dispositivo móvel local no System Center Configuration Manager](../../mdm/get-started/set-up-intune-subscription-on-premises-mdm.md).  

##  <a name="bkmk_roles"></a> Funções do sistema de sites necessárias  
 O Gerenciamento de Dispositivo Móvel local requer, pelo menos, uma de cada uma das seguintes funções do sistema de sites:  

- **Ponto proxy do registro** para dar suporte a solicitações de registro.  

- **Ponto de registro** para dar suporte ao registro de dispositivo.  

- **Ponto de gerenciamento de dispositivos** para a entrega da política. Essa função do sistema de sites é uma variação da função do ponto de gerenciamento que foi configurada para permitir o gerenciamento de dispositivo móvel.  

- **Ponto de distribuição** para entrega do conteúdo.  

- **Ponto de conexão de serviço** para se conectar ao Intune para notificar dispositivos fora do firewall.  

  Essas funções do sistema de sites podem ser instaladas no único servidor de sistema de sites ou podem ser executadas separadamente em servidores diferentes de acordo com as necessidades de sua organização. Cada servidor do sistema de sites usado para o Gerenciamento de Dispositivo Móvel local deve ser configurado como um ponto de extremidade HTTPS para a comunicação com dispositivos confiáveis. Para obter mais informações, consulte [Comunicação confiável necessária](#bkmk_trustedComs).  

  Para obter mais informações sobre como planejar funções do sistema de sites, veja [Planejamento para servidores de sistema de sites e funções de sistema de sites no System Center Configuration Manager](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).  

  Para obter mais informações sobre como adicionar as funções do sistema de sites necessárias, veja [Instalar funções do sistema de sites para o gerenciamento de dispositivo móvel local no System Center Configuration Manager](../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md).  

##  <a name="bkmk_trustedComs"></a> Comunicação confiável necessária  
 O Gerenciamento de Dispositivo Móvel local exige que as funções do sistema de sites sejam habilitadas para a comunicação HTTPS. Dependendo de suas necessidades, é possível usar a AC (autoridade de certificação) de sua empresa para estabelecer as conexões confiáveis entre servidores e dispositivos ou usar uma AC disponível publicamente para ser a autoridade confiável.  De qualquer forma, você precisará que um certificado de servidor Web seja configurado com o IIS nos servidores do sistema de sites que hospedam as funções do sistema de sites necessárias; além disso, você precisará do certificado raiz da AC instalado nos dispositivos que precisam se conectar aos servidores.  

 Se você usar a AC de sua empresa para estabelecer uma comunicação confiável, será necessário realizar as seguintes tarefas:  

- Crie e emita o modelo de certificado do servidor Web na AC.  

- Solicite um certificado do servidor Web para cada servidor do sistema de sites que hospeda uma função do sistema de sites necessária.  

- Configure o IIS no servidor do sistema de sites para usar o certificado de servidor Web solicitado.  

  Para dispositivos ingressados no domínio do Active Directory corporativo, o certificado raiz da AC corporativa já está disponível no dispositivo para conexões confiáveis. Isso significa que os dispositivos ingressados no domínio (como computadores desktop) serão automaticamente confiáveis para conexões HTTPS com os servidores do sistema de sites. No entanto, dispositivos não ingressados no domínio (normalmente móveis) não terão o certificado raiz necessário instalado. Esses dispositivos exigirão a instalação manual do certificado raiz para que eles se comuniquem com êxito com os servidores do sistema de sites que dão suporte ao Gerenciamento de Dispositivo Móvel local.  

  É necessário exportar o certificado raiz da AC emissora para uso pelos dispositivos individuais. Para obter o arquivo do certificado raiz, é possível exportá-lo usando a AC; outro método mais simples é usar o certificado do servidor Web emitido pela AC para extrair a raiz e criar um arquivo do certificado raiz.   Em seguida, o certificado raiz deve ser entregue ao dispositivo.  Alguns métodos de entrega de exemplo incluem  

- Sistema de arquivos  

- Anexo de email  

- Cartão de memória  

- Dispositivo vinculado  

- Armazenamento em nuvem (como OneDrive)  

- Conexão NFC (comunicação a curta distância)  

- Scanner de código de barras  

- Pacote de provisionamento OOBE (tela de apresentação)  

  Para obter mais informações, consulte [Configure certificados para comunicações confiáveis do Gerenciamento de Dispositivo Móvel Local no System Center Configuration Manager.](../../mdm/get-started/set-up-certificates-on-premises-mdm.md)  

##  <a name="bkmk_enrollment"></a> Considerações sobre registro  
 Para habilitar o registro de dispositivo para o Gerenciamento de Dispositivo Móvel local, os usuários devem ter permissão de registro e seus dispositivos devem poder ter uma comunicação confiável com os servidores do sistema de sites que hospedam as funções do sistema de sites necessárias.  

 A concessão da permissão de registro de usuário pode ser obtida por meio da configuração de um perfil de registro nas configurações do cliente do Configuration Manager. É possível usar as configurações padrão do cliente para enviar por push o perfil de registro para todos os usuários descobertos ou configurar o perfil de registro nas configurações personalizadas do cliente e enviar por push as configurações para uma ou mais coleções de usuários.  

 Com a permissão de registro de usuário concedida, os usuários podem registrar seus próprios dispositivos. Para ser registrado, o dispositivo do usuário deve ter o certificado raiz da AC (autoridade de certificação) que emitiu o certificado do servidor Web usado nos servidores do sistema de sites que hospedam as funções do sistema de sites necessárias.  

 Como uma alternativa ao registro iniciado pelo usuário, é possível configurar um pacote de registro em massa que permite que o dispositivo seja registrado sem a intervenção do usuário. Esse pacote pode ser entregue ao dispositivo antes que ele seja inicialmente provisionado para uso ou depois que o dispositivo passar pelo processo OOBE.  

 Para obter mais informações sobre como configurar e registrar dispositivos, veja  

-   [Configurar o registro de dispositivo para o gerenciamento de dispositivo móvel local no System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)  

-   [Registrar dispositivos para o gerenciamento de dispositivo móvel local no System Center Configuration Manager](../../mdm/deploy-use/enroll-devices-on-premises-mdm.md)  
