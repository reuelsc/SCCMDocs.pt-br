---
title: Planejar MDM local
titleSuffix: Configuration Manager
description: Planejar o gerenciamento de dispositivo móvel local gerenciar dispositivos móveis no Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: bb9349a8c3f107f2da139148e4476537fe6aa7ed
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558075"
---
# <a name="plan-for-on-premises-mdm-in-configuration-manager"></a>Planejar MDM local no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Gerenciamento de dispositivo móvel (MDM) do local permite que você gerencie dispositivos móveis usando os recursos de gerenciamento integrados do sistema operacional do dispositivo. A funcionalidade de gerenciamento baseia-se no padrão OMA DM (Gerenciamento de Dispositivo da Open Mobile Alliance), e várias plataformas de dispositivo usam esse padrão para permitir que os dispositivos sejam gerenciados. Esses dispositivos são chamados *os dispositivos modernos* na documentação e o console do Configuration Manager. Esse termo o distingue de outros dispositivos que exigem o cliente do Configuration Manager para gerenciá-los.  

Considere os seguintes requisitos antes de preparar a infraestrutura do Configuration Manager para lidar com o MDM local.



## <a name="bkmk_devices"></a> Dispositivos com suporte  

O branch atual do Configuration Manager dá suporte ao registro no Gerenciamento de Dispositivo Móvel Local para dispositivos que executam os seguintes sistemas operacionais:  
  
- Windows 10 Enterprise  
- Windows 10 Pro  
- Windows 10 Team   
- Windows 10 Mobile  
- Windows 10 Mobile Enterprise
- Windows 10 IoT Enterprise   



##  <a name="bkmk_intune"></a> A assinatura do Microsoft Intune  

Para começar a usar o MDM local, você precisa de uma assinatura do Microsoft Intune. A assinatura só é necessário para acompanhar o licenciamento de dispositivos e não é usada para gerenciar ou armazenar informações de gerenciamento para os dispositivos. Todos os dados de gerenciamento é armazenado em sua organização usando a infraestrutura do Configuration Manager local.  

> [!Note]  
> Começando na versão 1810, uma conexão do Intune não é mais necessário para novas implantações de MDM local.<!--3607730, fka 1359124--> Sua organização ainda exige licenças do Intune para usar esse recurso. No momento, é possível remover a conexão do Intune de implantações de MDM local existentes. Para obter mais informações, confira a [postagem no blog de suporte do Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

Se o site tiver dispositivos com conectividade com a internet, o serviço do Intune pode ser usado para notificar os dispositivos para verificar o gerenciamento de dispositivo de ponto para atualizações de política. Esse comportamento usa o Intune estritamente à notificação de dispositivos para a internet. Dispositivos sem conexões de internet e que não pode ser contatado pelo Intune contam com o intervalo de sondagem configurado para fazer check-in de funções do sistema de site para funções de gerenciamento.  

> [!TIP]  
> Antes de configurar as funções do sistema de sites necessárias, configure a assinatura do Intune. Essa ação minimiza o tempo necessário para as funções para se tornarem funcionais.  

Para obter informações sobre como configurar a assinatura do Intune, consulte [configurar uma assinatura do Microsoft Intune para MDM local](/sccm/mdm/get-started/set-up-intune-subscription-on-premises-mdm).  



##  <a name="bkmk_roles"></a> Site system roles  

Local MDM requer pelo menos um de cada uma das seguintes funções do sistema de site:  

- **Ponto proxy do registro** para dar suporte a solicitações de registro.  

- **Ponto de registro** para dar suporte ao registro de dispositivo.  

- **Ponto de gerenciamento de dispositivos** para a entrega da política. Essa função do sistema de sites é uma variação da função do ponto de gerenciamento que foi configurada para permitir o gerenciamento de dispositivo móvel.  

- **Ponto de distribuição** para entrega do conteúdo.  

- **Ponto de conexão de serviço** para se conectar ao Intune para notificar dispositivos fora do firewall.  

Essas funções do sistema de site podem ser instaladas no servidor de sistema de site único ou podem ser executadas separadamente em servidores diferentes, dependendo das necessidades da sua organização. Cada servidor do sistema de site usado para o MDM local deve ser configurado como um ponto de extremidade HTTPS para comunicação com dispositivos confiáveis. Para obter mais informações, consulte [Comunicação confiável necessária](#bkmk_trustedComs).  

Para obter mais informações sobre como planejar funções do sistema de site, consulte [planejar para funções e servidores do sistema de site do Configuration Manager](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles).  

Para obter mais informações sobre como adicionar as funções do sistema de sites necessárias, consulte [instalar funções do sistema de site para o MDM local](/sccm/mdm/get-started/install-site-system-roles-for-on-premises-mdm).  



##  <a name="bkmk_trustedComs"></a> Comunicações confiáveis  

MDM local exige as funções de sistema de sites sejam habilitadas para comunicações HTTPS. Dependendo das suas necessidades, você pode usar a autoridade de certificação da sua empresa (CA) para estabelecer as conexões confiáveis entre servidores e dispositivos. Você também pode usar uma autoridade de certificação publicamente disponível para ser a autoridade confiável. De qualquer forma, você precisa de um certificado do servidor web para ser configurado no IIS nos servidores de sistema de sites hospedando as funções do sistema de sites necessárias. Também é necessário o certificado raiz da AC instalado nos dispositivos que precisam se conectar aos servidores.  

Se você usar a autoridade de certificação da sua empresa para estabelecer uma comunicação confiável, faça as seguintes tarefas:  

- Crie e emita o modelo de certificado do servidor Web na AC.  

- Solicite um certificado do servidor Web para cada servidor do sistema de sites que hospeda uma função do sistema de sites necessária.  

- Configure o IIS no servidor do sistema de sites para usar o certificado de servidor Web solicitado.  

Para dispositivos ingressados no domínio do Active Directory corporativo, o certificado raiz da AC corporativa já está disponível no dispositivo para conexões confiáveis. Esse comportamento significa que os dispositivos ingressados no domínio são automaticamente confiáveis para conexões HTTPS com servidores do sistema de site. No entanto, os dispositivos não ingressados em domínio não obtém automaticamente o certificado raiz necessário instalado. Para se comunicar com êxito com servidores do sistema de sites que dão suporte a MDM local, dispositivos não ingressados no domínio como dispositivos móveis exigem que você instalar manualmente o certificado raiz neles.  

Exporte o certificado raiz da autoridade de certificação emissora para uso pelos dispositivos individuais. Para obter o arquivo de certificado raiz, você pode exportá-lo usando a autoridade de certificação. Outro método é usar o certificado do servidor web emitido pela autoridade de certificação para extrair a raiz e criar um arquivo de certificado raiz. Em seguida, o certificado raiz deve ser entregue ao dispositivo. Alguns métodos de entrega de exemplo incluem:

- Sistema de arquivos  

- Anexo de email  

- Cartão de memória  

- Dispositivo vinculado  

- Armazenamento em nuvem (como OneDrive)  

- Conexão NFC (comunicação a curta distância)  

- Scanner de código de barras  

- Pacote de provisionamento OOBE (tela de apresentação)  

Para obter mais informações, consulte [configurar certificados para comunicações confiáveis no MDM local](/sccm/mdm/get-started/set-up-certificates-on-premises-mdm)  



##  <a name="bkmk_enrollment"></a> Registro de dispositivo

Para habilitar o registro de dispositivo para o MDM local
- Os usuários devem ter permissão para registrar 
- Dispositivos devem ser configurados para comunicações confiáveis com os servidores de sistema de sites que hospedam as funções necessárias  

Conceda aos usuários permissão para registrar dispositivos, configurando um perfil de registro nas configurações do cliente do Configuration Manager. Você pode usar as configurações do cliente para enviar por push o perfil de registro para todos os usuários descobertos. Você pode também configurar o perfil de registro nas configurações personalizadas do cliente e enviar por push as configurações para um ou mais coleções de usuários.  

Depois que os usuários recebem permissão, eles podem registrar seus próprios dispositivos. Para ser registrado, o dispositivo do usuário deve ter o certificado raiz da autoridade de certificação (CA) que emitiu o certificado do servidor web usado nos servidores de sistema de sites hospedando as funções necessárias.  

Como uma alternativa ao registro iniciado pelo usuário, você pode configurar um pacote de registro em massa. Este pacote permite que o dispositivo seja registrado sem a intervenção do usuário. Ele pode ser fornecido para o dispositivo antes que ela é provisionada para uso ou depois que o dispositivo passar pelo processo OOBE.  

Para obter mais informações sobre como configurar e registrar dispositivos, consulte os seguintes artigos: 

- [Configurar o registro de dispositivo para MDM local](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm)  

- [Registrar dispositivos para MDM local](/sccm/mdm/deploy-use/enroll-devices-on-premises-mdm)  

