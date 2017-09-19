---
title: "Práticas recomendadas de implantação de cliente | Microsoft Docs"
description: "Conheça as práticas recomendadas para a implantação de cliente no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
caps.latest.revision: "11"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 22f0981022f50d316b2572a720ae3c818daf0d43
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2017
---
# <a name="best-practices-for-client-deployment-in-system-center-configuration-manager"></a>Práticas recomendadas para a implantação de cliente no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


## <a name="use-software-update-based-client-installation-for-active-directory-computers"></a>Use a instalação do cliente com base na atualização de software para computadores do Active Directory  
 Esse método de implantação do cliente usa as tecnologias existentes do Windows, é integrado à infraestrutura do Active Directory, exige o mínimo de configuração no Configuration Manager, é o mais fácil de configurar para firewalls e é o mais seguro. Usando grupos de segurança e filtro WMI para a configuração de Política de Grupo, você também tem uma grande flexibilidade para controlar em quais computadores instalar o cliente do Configuration Manager.  

 Para obter mais informações, consulte [Como instalar clientes do Configuration Manager usando a instalação baseada em atualização de software](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

## <a name="extend-the-active-directory-schema-and-publish-the-site-so-that-you-can-run-ccmsetup-without-command-line-options"></a>Estender o esquema do Active Directory e publicar o site para que você possa executar o CCMSetup sem opções de linha de comando  
 Quando você estende o esquema do Active Directory para o Configuration Manager e o site é publicado no Active Directory Domain Services, muitas propriedades de instalação do cliente são publicadas neles. Se um computador puder localizar essas propriedades de instalação do cliente, ele poderá usá-las durante a implantação do cliente do Configuration Manager. Como essa informação é gerada automaticamente, o risco de erro humano associado à inserção manual de propriedades de instalação é eliminado.  

 Para obter mais informações, consulte [Sobre as propriedades de instalação de cliente publicadas nos Serviços de Domínio do Active Directory no System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

## <a name="use-a-phased-rollout-to-manage-cpu-usage"></a>Usar uma distribuição em fases para gerenciar o uso da CPU  
 Minimize o efeito dos requisitos de processamento da CPU no servidor do site usando uma distribuição em fases de clientes. Implante clientes fora do horário comercial para que outros serviços tenham mais largura de banda disponível durante o dia e os usuários não sejam interrompidos se o computador ficar lento ou exigir uma reinicialização.  

## <a name="enable-automatic-upgrade-after-your-main-client-deployment-has-finished"></a>Habilitar atualização automática após a implantação do cliente principal  
 As [atualizações automáticas do cliente](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) são úteis quando você deseja atualizar um pequeno número de computadores cliente que podem ter sido perdidos pelo principal método de instalação do cliente, devido à possibilidade de estarem offline. 

> [!NOTE]  
>  Melhorias de desempenho no Configuration Manager podem permitir que você use atualizações automáticas como o método principal de atualização de cliente. No entanto, o desempenho dependerá da infraestrutura da hierarquia como, por exemplo, o número de clientes.  


## <a name="use-smsmp-and-fsp-if-you-install-the-client-with-clientmsi-properties"></a>Use SMSMP e FSP se você instalar o cliente com propriedades client.msi  
 A propriedade SMSMP especifica o ponto inicial de gerenciamento para o cliente se comunicar e eliminar a dependência de soluções de local de serviços, como Serviços de Domínio Active Directory, DNS e WINS.  

 Use a propriedade FSP e instale um ponto de status de fallback, para que você possa monitorar a instalação e atribuição do cliente, e identificar quaisquer problemas de comunicação  

 Para obter mais informações sobre essas opções, consulte [Sobre as propriedades de instalação do cliente no System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md).  

## <a name="install-client-language-packs-before-you-install-the-clients"></a>Instalar pacotes de idiomas do cliente antes de instalar os clientes  
Recomendamos a instalação de pacotes de idiomas do cliente antes da implantação do cliente. Se você instalar [pacotes de idiomas do cliente](../../../../core/servers/deploy/install/language-packs.md) (para habilitar idiomas adicionais) em um site após a instalação dos clientes, será necessário reinstalar os clientes antes que eles usem os idiomas. Para clientes de dispositivos móveis, é necessário apagar o dispositivo móvel e registrá-lo novamente.  

## <a name="prepare-required-pki-certificates-in-advance"></a>Preparar os certificados PKI necessários com antecedência  
 Para gerenciar dispositivos na internet, dispositivos móveis registrados e computadores Mac, você deve ter certificados PKI nos sistemas de site (pontos de gerenciamento e de distribuição) e os dispositivos clientes. Em redes de produção, você pode exigir aprovação do gerenciamento de alterações para usar novos certificados, reiniciar servidores de sistema do site ou os usuários podem ter que fazer logoff e logon para nova associação ao grupo. Além disso, você pode ter que dar tempo suficiente para a replicação de permissões de segurança e quaisquer novos modelos de certificado.  

 Para obter mais informações sobre os certificados PKI necessários, consulte [Requisitos de certificado PKI para o System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

## <a name="before-you-install-clients-configure-any-required-client-settings-and-maintenance-windows"></a>Para instalar clientes, defina quaisquer configurações de cliente necessárias e as janelas de manutenção.  
 Embora seja possível [definir configurações do cliente](../../../../core/clients/deploy/configure-client-settings.md) e janelas de manutenção antes ou após a instalação dos clientes, é melhor definir as configurações necessárias antes de instalá-los para que elas sejam usadas assim que o cliente é instalado. 

 Configure janelas de manutenção para servidores e dispositivos Windows Embedded, a fim de garantir a continuidade dos negócios para dispositivos críticos. As janelas de manutenção garantirão que as atualizações de software necessárias e o software antimalware não reiniciam o computador durante o horário comercial.  

> [!IMPORTANT]  
>  Em computadores com Windows 10 que você planeja proteger com o UWF (Filtro de Gravação Unificado), será preciso configurar o dispositivo para UWF antes de instalar o cliente. Isso permite que o Configuration Manager instale o cliente com um provedor de credenciais personalizado que impede usuários com direitos limitados de fazer logon no dispositivo durante o modo de manutenção.  

## <a name="plan-your-user-enrollment-experience-for-mac-computers-and-mobile-devices"></a>Planejar sua experiência de registro de usuário para computadores Mac e dispositivos móveis   
 Se os usuários forem registrar seus próprios computadores Mac e dispositivos móveis no Configuration Manager, planeje a experiência do usuário. Por exemplo, você pode gerar o script do processo de instalação e registro usando uma página da Web, para que os usuários insiram a quantidade mínima de informações necessárias e enviar instruções com um link por email.  

## <a name="use-file-based-write-filters-for-windows-embedded-devices"></a>Usar filtros de gravação baseados em arquivo para dispositivos Windows Embedded 
 Dispositivos inseridos que usam EWF têm a probabilidade de experimentar ressincronizações de mensagem de estado. Se você tiver apenas alguns dispositivos inseridos que utilizam EWFs, poderá não perceber isso. No entanto, quando você tem vários dispositivos inseridos que ressincronizam suas informações, como o envio de inventário completo em vez de inventário delta, isso pode gerar um aumento notável em pacotes de rede e maior processamento da CPU no servidor do site.  

 Quando você tem uma opção de que tipo de filtro de gravação habilitar, escolha FBWF e configure exceções para manter o estado do cliente e os dados de inventário entre reinicialização do dispositivo para a eficiência da rede e da CPU no cliente do Configuration Manager. Para obter mais informações sobre filtros de gravação, veja   [Planejando a implantação de cliente em dispositivos do Windows Embedded no System Center Configuration Manager](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

 Para obter mais informações sobre o número máximo de clientes do Windows Embedded para os quais um site primário pode dar suporte, veja [Sistemas operacionais com suporte para clientes e dispositivos](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).  
