---
title: Funcionalidades no Technical Preview 1607 do Configuration Manager
description: "Saiba mais sobre os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1607."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bb69547-3370-4860-96b0-7fb600c56482
caps.latest.revision: 11
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 1b9e49da1a5bbfca93fe683b82d2c0056a22cc1f
ms.openlocfilehash: 4717e0f8eef01501fb5b5790e855c476c1ca4590
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017

---
# <a name="capabilities-in-technical-preview-1607-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1607 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1607. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview.      Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de um technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos em um technical preview.    


**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  

## <a name="dmp_edition"></a>Melhorias na Política de atualização de edição do Windows 10

Nesta versão, as seguintes melhorias foram feitas nesta política:

* Agora é possível usar a política de atualização de edição com computadores Windows 10 que executam o cliente do Configuration Manager além de computadores Windows 10 registrados com o Microsoft Intune.
* É possível atualizar do Windows 10 Professional para qualquer uma das plataformas no assistente compatíveis com o hardware.

[Leia mais sobre a Política de Atualização de Edição do Windows 10](/sccm/compliance/deploy-use/upgrade-windows-version)

### <a name="try-it-out"></a>Experimente!

1. Use as informações no [tópico de política de atualização de edição existente](/sccm/compliance/deploy-use/upgrade-windows-version) para criar uma política de atualização de edição.
2. Implante esta política em um computador Windows 10 que executa o cliente do Configuration Manager.
Quando a política atinge um computador Windows definido como destino, o computador será reiniciado dentro de duas horas para aplicar a atualização. No momento, você não pode suprimir esta reinicialização. Certifique-se de informar os usuários nos quais você implanta a política ou agende a política para ser executada fora do horário de trabalho dos usuários.

### <a name="known-issue-with-this-release"></a>Problemas conhecidos com sta versão
Nas configurações de cliente do Configuration Manager, é possível ver as configurações da **Atualização de Edição**. Nesta versão, essas configurações não são funcionais. Use as instruções fornecidas acima para atualizar o Windows 10 para uma versão mais recente.

## <a name="customizable-branding-for-software-center-dialogs"></a>Identidade visual personalizável para caixas de diálogo do Centro de Software

A identidade visual personalizada do Centro de Software foi introduzida no Configuration Manager versão 1602. No Technical Preview versão 1607, agora essa identidade visual foi estendida para todas as caixas de diálogo e notificações da barra de tarefas associadas para fornecer uma experiência mais consistente aos usuários do Centro de Software.

### <a name="try-it-out"></a>Experimente!

A identidade visual personalizada do Centro de Software é aplicada de acordo com as regras a seguir:

1. Se a função de servidor do site ponto de sites da Web do catálogo de aplicativos não estiver instalada, o Centro de Software exibirá o nome da organização especificado na configuração do cliente **Nome da organização exibido no Centro de Software** do **Agente de Computador**. Para ver instruções, consulte [How to configure client settings (Como definir as configurações do cliente)](../../core/clients/deploy/configure-client-settings.md).

2. Se a função de servidor do site ponto de sites da Web do catálogo de aplicativos estiver instalada, o Centro de Software exibirá o nome da organização a e cor especificados nas propriedades da função de servidor do site ponto de sites da Web do catálogo de aplicativos. Para obter mais informações, consulte [Configuration options for Application Catalog website point (Opções de configuração do ponto de sites da Web do catálogo de aplicativos)](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website).

3. Se uma assinatura do Microsoft Intune estiver configurada e conectada ao ambiente do Configuration Manager, o Centro de Software exibirá o nome da organização, a cor e o logotipo da empresa especificados nas propriedades de assinatura do Intune. Para obter mais informações, consulte [Configure the Microsoft Intune subscription](/mdm/deploy-use/configure-intune-subscription) (Configurar a assinatura do Microsoft Intune).

## <a name="use-the-same-network-adapter-for-multiple-pxe-initiated-deployments"></a>Usar o mesmo adaptador de rede para várias implantações iniciadas por PXE
No Technical Preview versão 1607, quando você usa um adaptador ethernet para obter a imagem de vários dispositivos (como um adaptador ethernet USB que você usa em vários dispositivos), é possível habilitar uma nova configuração que permite a você inserir identificadores de hardware para os adaptadores ethernet. O Configuration Manager ignora os identificadores de hardware na lista ao executar uma instalação PXE e para registro de clientes.

Para obter mais informações sobre esse problema, consulte o [Blog da equipe de suporte OSD do Configuration Manager](https://blogs.technet.microsoft.com/system_center_configuration_manager_operating_system_deployment_support_blog/2015/08/27/reusing-the-same-nic-for-multiple-pxe-initiated-deployments-in-system-center-configuration-manger-osd/).  

### <a name="enable-the-feature-to-manage-duplicate-hardware-identifiers"></a>Habilitar o recurso para gerenciar os identificadores de hardware duplicados  
1. No console do Configuration Manager, vá para **Administração** > **Visão Geral** > **Serviços em Nuvem** > **Atualizações e Manutenção** > **Recursos**.
2. No painel Exibição, selecione **Gerenciar identificadores de hardware duplicados**.
3. Na guia **Início**, no grupo **Recursos**, clique em **Ativar**.

### <a name="add-hardware-identifiers-for-configuration-manager-to-ignore"></a>Adicionar identificadores de hardware para o Configuration Manager ignorar  
1. No console do Configuration Manager, vá para **Administração** > **Visão Geral** > **Configuração de Site** > **Sites**.
2. Na guia **Início** , no grupo **Sites** , clique em **Configurações da Hierarquia**.
3. Vá para a guia **Aprovação de Cliente e Registros de Conflitos**.
4. Clique em **Adicionar** na seção **Identificadores de hardware duplicados** para adicionar novos identificadores de hardware.

