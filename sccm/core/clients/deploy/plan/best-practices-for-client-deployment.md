---
title: "Práticas recomendadas de implantação de cliente | Microsoft Docs"
description: "Conheça as práticas recomendadas para a implantação de cliente no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
caps.latest.revision: 11
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: 49b2520a82614bedc7bcc077604e0b89885119c2


---
# <a name="best-practices-for-client-deployment-in-system-center-configuration-manager"></a>Práticas recomendadas para a implantação de cliente no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as seguintes informações de práticas recomendadas para ajudar a implantar clientes em computadores no System Center Configuration Manager.  

## <a name="use-software-update-based-client-installation-for-active-directory-computers"></a>Use a instalação do cliente com base na atualização de software para computadores do Active Directory  
 Esse método de implantação do cliente tem a vantagem de usar tecnologias existentes do Windows: integra-se com a infraestrutura do Active Directory, exige o mínimo de configuração no Configuration Manager, é o mais fácil de configurar para firewalls e o mais seguro. Usando grupos de segurança e filtro WMI para a configuração de Política de Grupo, você também tem uma grande flexibilidade para controlar em quais computadores instalar o cliente do Configuration Manager.  

 Para obter mais informações, consulte [Como instalar clientes do Configuration Manager usando a instalação baseada em atualização de software](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

## <a name="extend-the-active-directory-schema-and-publish-the-site-so-that-you-can-run-ccmsetup-without-command-line-options"></a>Estender o esquema do Active Directory e publicar o site para que você possa executar o CCMSetup sem opções de linha de comando  
 Quando você estende o esquema do Active Directory para o Configuration Manager e o site é publicado no Active Directory Domain Services, muitas propriedades de instalação do cliente são publicadas neles. Se um computador puder localizar essas propriedades de instalação do cliente, ele poderá usá-las durante a implantação do cliente do Configuration Manager. Como essa informação é gerada automaticamente, o risco de erro humano associado à inserção manual de propriedades de instalação é eliminado.  

 Para obter mais informações, consulte [Sobre as propriedades de instalação de cliente publicadas nos Serviços de Domínio do Active Directory no System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

## <a name="when-you-have-many-clients-to-deploy-plan-a-phased-rollout-outside-business-hours"></a>Planejar uma distribuição em fases fora do horário comercial quando houver muitos clientes para implantar  
 Minimize o efeito dos requisitos de processamento da CPU no servidor do site, planejando uma distribuição em fases de clientes durante um período. Implante clientes fora do horário comercial para que os serviços críticos de negócios tenham mais largura de banda disponível durante o dia e os usuários não sejam interrompidos se o computador ficar mais lento ou exigir uma reinicialização para concluir a instalação.  

## <a name="enable-automatic-upgrade-after-your-main-client-deployment-has-finished"></a>Habilitar atualização automática após a implantação do cliente principal  
 As atualizações automáticas do cliente são úteis quando você quer atualizar um pequeno número de computadores cliente que podem ter sido perdidos pelo principal método de instalação do cliente. Por exemplo, você completou uma atualização inicial do cliente, mas alguns estavam offline durante a implantação da atualização. Você usa esse método para atualizar o cliente nesses computadores da próxima vez em que estiverem ativos.  

> [!NOTE]  
>  Melhorias de desempenho no Configuration Manager podem permitir que você use atualizações automáticas como o método principal de atualização de cliente. No entanto, o desempenho dependerá da infraestrutura da hierarquia como, por exemplo, o número de clientes.  

 Para obter mais informações sobre o método de atualização automática de cliente, consulte [Como atualizar clientes para computadores Windows no System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="use-smsmp-and-fsp-if-you-install-the-client-with-clientmsi-properties"></a>Use SMSMP e FSP se você instalar o cliente com propriedades client.msi  
 A propriedade SMSMP especifica o ponto inicial de gerenciamento para o cliente se comunicar e eliminar a dependência de soluções de local de serviços, como Serviços de Domínio Active Directory, DNS e WINS.  

 Use a propriedade FSP e instale um ponto de status de fallback, para que você possa monitorar a instalação e atribuição do cliente, e identificar quaisquer problemas de comunicação  

 Para obter mais informações sobre essas opções, consulte [Sobre as propriedades de instalação do cliente no System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md).  

## <a name="if-you-want-to-use-client-languages-other-than-english-install-the-client-language-packs-before-you-install-the-clients"></a>Se você quiser usar idiomas de cliente diferentes do inglês, instale os pacotes de idioma do cliente antes dos clientes.  
 Se você instalar os pacotes de idioma do cliente em um site depois dos clientes, estes deverão ser reinstalados antes de usarem os idiomas adicionais. Para clientes de dispositivos móveis, isso significa que você deve limpar o dispositivo móvel e registrá-lo novamente.  

 Para obter mais informações sobre como adicionar suporte para outros idiomas de clientes, consulte [Pacotes de idiomas no System Center Configuration Manager](../../../../core/servers/deploy/install/language-packs.md).  

## <a name="plan-and-prepare-any-required-pki-certificates-in-advance"></a>Planejar e preparar todos os certificados KPI antecipadamente  
 Para gerenciar dispositivos na internet, dispositivos móveis registrados e computadores Mac, você deve ter certificados PKI nos sistemas de site (pontos de gerenciamento e de distribuição) e os dispositivos clientes. Para muitos clientes, isso exige preparação e planejamento avançado, especialmente se você tiver uma equipe separada que gerencia sua PKI. Em redes de produção, você pode exigir aprovação do gerenciamento de alterações para usar novos certificados, reiniciar servidores de sistema do site ou os usuários podem ter que fazer logoff e logon para nova associação ao grupo. Além disso, você pode ter que dar tempo suficiente para a replicação de permissões de segurança e quaisquer novos modelos de certificado.  

 Para obter mais informações sobre os certificados PKI necessários, consulte [Requisitos de certificado PKI para o System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

## <a name="before-you-install-clients-configure-any-required-client-settings-and-maintenance-windows"></a>Para instalar clientes, defina quaisquer configurações de cliente necessárias e as janelas de manutenção.  
 Embora você possa definir configurações do cliente e janelas de manutenção antes ou depois que os clientes são instalados, defina as configurações necessárias antes de instalá-los para que essas opções sejam usadas assim que ele esteja instalado. Para obter mais informações, consulte [Como definir as configurações do cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md)  

 Configure as janelas de manutenção para os servidores e dispositivos Windows Embedded, a fim de garantir a continuidade de negócios para esses computadores essenciais aos negócios. Por exemplo, janelas de manutenção irão garantir que as atualizações de software necessárias e software antimalware não reiniciem o computador durante o horário comercial.  

> [!IMPORTANT]  
>  Em computadores com Windows 10 que você planeja proteger com o UWF (Filtro de Gravação Unificado), será preciso configurar o dispositivo para UWF antes de instalar o cliente. Isso permite que o Configuration Manager instale o cliente com um provedor de credenciais personalizado que impeça os usuários com direitos limitados de fazer logon no dispositivo durante o modo de manutenção.  

## <a name="for-mac-computers-and-mobile-devices-that-are-enrolled-by-configuration-manager-plan-your-user-enrollment-experience"></a>Planejar sua experiência de registro de usuário para computadores Mac e dispositivos móveis registrados pelo Configuration Manager  
 Se os usuários forem registrar seus próprios computadores Mac e dispositivos móveis usando o Configuration Manager, planeje e prepare a experiência do usuário. Por exemplo, você pode fazer o script do processo de instalação e registro através de uma página da Web para que os usuários insiram o valor mínimo de informações necessárias e você envie instruções para eles com um link por email.  

## <a name="when-you-manage-windows-embedded-devices-use-file-based-write-filters-fbwf-rather-than-enhanced-write-filters-ewf-for-higher-scalability"></a>Quando gerenciar dispositivos Windows Embedded, use FBWF (Filtros de Gravação com Base em Arquivos) em vez de EFW (Filtros de Gravação Avançados) para maior escalabilidade.  
 Dispositivos inseridos que usam EWF têm a probabilidade de experimentar ressincronizações de mensagem de estado. Se você tiver apenas alguns dispositivos inseridos que utilizam EWFs, poderá não perceber isso. No entanto, quando você tem vários dispositivos inseridos que ressincronizam suas informações, como o envio de inventário completo em vez de inventário delta, isso pode gerar um aumento notável em pacotes de rede e maior processamento da CPU no servidor do site.  

 Quando você tem uma opção de que tipo de filtro de gravação habilitar, escolha FBWF e configure exceções para manter o estado do cliente e os dados de inventário entre reinicialização do dispositivo para a eficiência da rede e da CPU no cliente do Configuration Manager. Para obter mais informações sobre filtros de gravação, veja   [Planejando a implantação de cliente em dispositivos do Windows Embedded no System Center Configuration Manager](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

 Para obter mais informações sobre o número máximo de clientes do Windows Embedded para os quais um site primário pode dar suporte, veja [Sistemas operacionais com suporte para clientes e dispositivos](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).  



<!--HONumber=Dec16_HO3-->


