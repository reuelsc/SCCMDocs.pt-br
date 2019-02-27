---
title: Sites para sistemas de sites
titleSuffix: Configuration Manager
description: Saiba mais sobre os sites padrão e personalizado para servidores do sistema de sites no System Center Configuration Manager.
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 681f0893-e83b-476e-9ec0-a5dc7c9deeb6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fd2e358a93ff91c79f0f4716a596a9f7026c5daa
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123443"
---
# <a name="websites-for-site-system-servers-in-system-center-configuration-manager"></a>Sites para servidores de sistema de sites no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Várias funções de sistema de sites do Configuration Manager requerem o uso do IIS (Serviços de Informações da Internet) da Microsoft e usam o site padrão do IIS para hospedar serviços de sistema de sites. Quando você precisar executar outros aplicativos Web no mesmo servidor e as configurações não forem compatíveis com o Configuration Manager, considere o uso de um site personalizado para Configuration Manager.  

> [!TIP]  
>  É uma prática recomendada de segurança dedicar um servidor aos sistemas de sites do Configuration Manager que requerem o IIS. Ao executar outros aplicativos em um sistema de sites do Configuration Manager, você pode aumentar a superfície de ataques do computador.  




##  <a name="BKMK_What2Know"></a> O que saber antes de escolher usar sites personalizados  
 Por padrão, as funções do sistema de sites usam o **Site Padrão** no IIS. Isso é configurado automaticamente quando a função de sistema de sites é instalada. No entanto, em sites primários, você pode optar por usar sites personalizados em vez disso. Quando você usa sites personalizados:  

-   Sites personalizados estão habilitados para todo o site, não para servidores ou funções individuais do sistema de sites.  

-   Em sites primários, cada computador que hospedará uma função aplicável do sistema de sites deverá ser configurado com um site personalizado nomeado **SMSWEB**. Até que esse site seja criado e as funções de sistema de sites no computador sejam configuradas para usar o site personalizado, os clientes não poderão se comunicar com funções do sistema de sites no computador.  

-   Uma vez que os sites secundários são automaticamente configurados para usarem um site personalizado quando o site primário pai é configurado para fazer isso, você também deve criar sites personalizados no IIS em cada servidor do sistema de sites secundário que requer IIS.  


  **Pré-requisitos para usar sites personalizados:**  

 Antes de habilitar a opção de usar sites personalizados em um site, você deve:  

-   Criar um site personalizado chamado **SMSWEB** no IIS em cada servidor de sistema de sites que exigir IIS. Faça isso no site primário e em quaisquer sites filho secundários.  

-   Configure o site personalizado para responder à mesma porta configurada para a comunicação de cliente do Configuration Manager (porta de solicitação do cliente).  

-   Para cada site personalizado ou site padrão que usar uma pasta personalizada, coloque uma cópia do tipo de documento padrão que você usa na pasta raiz que hospeda o site. Por exemplo, em um computador Windows Server 2008 R2 com configurações padrão, o **iisstart.htm** é um de vários tipos de documentos padrão disponíveis. Você pode encontrar esse arquivo na raiz do site da Web padrão e colocar uma cópia desse arquivo (ou uma cópia do tipo de documento padrão usado) na pasta raiz que hospeda o site da Web SMSWEB personalizado. Para saber mais sobre os tipos de documento padrão, veja [Documento padrão &lt;defaultDocument\> do IIS](http://www.iis.net/configreference/system.webserver/defaultdocument).  

**Sobre os requisitos de IIS ‑**
**As seguintes funções de sistema de sites requerem IIS e um site para hospedar os serviços de sistema de sites:**  

-   Ponto de serviços Web do Catálogo de Aplicativos  

-   Ponto de sites da Web do Catálogo de Aplicativos  

-   Ponto de distribuição  

-   Ponto de registro  

-   Ponto proxy do registro  

-   Ponto de status de fallback  

-   Ponto de gerenciamento  

-   Ponto de atualização de software  

-   Ponto de migração de estado  

Considerações adicionais:  

-   Quando um site primário tem sites personalizados habilitados, os clientes atribuídos ao site são direcionados a comunicarem-se com os sites personalizado, em vez de sites padrão, em servidores de sistema de sites aplicáveis  

-   Se você usar sites personalizados para um site primário, considere usá-los para todos os sites primários em sua hierarquia para assegurar que os clientes possam usar roaming com sucesso dentro da hierarquia. (Roaming é quando um computador cliente é movido para um novo segmento de rede gerenciado por outro site. O roaming pode afetar os recursos que o cliente pode acessar localmente, em vez de acessar em um link WAN).  

-   As funções do sistema de sites que usam o IIS, mas não aceitam conexões de cliente, como o ponto do Reporting Services, também usam o site SMSWEB em vez de usar o padrão.  

-   Os sites personalizados exigem atribuir números de porta que difiram daqueles usados pelo site de computadores padrão. Um site padrão e um site personalizado não podem ser executados ao mesmo tempo se ambos tentarem usar as mesmas portas TCP/IP.  

-   As portas TCP/IP que você configurar no IIS para o site personalizado devem corresponder às portas de solicitação do cliente para o site.  

## <a name="switch-between-default-and-custom-websites"></a>Alternar entre sites padrão e personalizados  
Embora você possa marcar ou desmarcar a caixa de seleção para usar sites personalizados em um site primário a qualquer momento (essa é uma caixa de seleção na guia Geral de Propriedades do site), planeje cuidadosamente antes de fazer essa alteração. Quando essa configuração for alterada, todas as funções de sistema de sites aplicáveis ao site primário e a sites secundários filho devem ser desinstaladas e reinstaladas:  

As seguintes funções são **reinstaladas automaticamente**:  

-   Ponto de gerenciamento  

-   Ponto de distribuição  

-   Ponto de atualização de software  

-   Ponto de status de fallback  

-   Ponto de migração de estado  

As funções a seguir devem ser **reinstaladas manualmente**:  

-   Ponto de serviços Web do Catálogo de Aplicativos  

-   Ponto de sites da Web do Catálogo de Aplicativos  

-   Ponto de registro  

-   Ponto proxy do registro  

Além disso:  

-   Quando você alterna do site da Web padrão para usar um site da Web personalizado, o Configuration Manager não remove diretórios virtuais antigos. Se desejar remover os arquivos que o Configuration Manager usou, exclua manualmente os diretórios virtuais que foram criados sob o site da Web padrão.  

-   Se você alterar o site para usar sites personalizados, os clientes que já estão atribuídos ao site devem ser reconfigurados para usar as novas portas de solicitação de cliente para os sites personalizados. Veja [Como configurar as portas de comunicação do cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md).  

## <a name="set-up-custom-websites"></a>Configurar sites personalizados  
Uma vez que as etapas para criar um site personalizado variam para versões diferentes do sistema operacional, consulte a documentação para sua versão do sistema operacional para obter as etapas exatas, mas use as seguintes informações quando aplicável:  

-   O nome do site deve ser: **SMSWEB**.  

-   Ao configurar HTTPS, você deve especificar um certificado SSL para poder salvar a configuração.  

-   Depois de criar o site personalizado, remova as portas de site personalizado que você usar de outros sites no IIS:  

    1.  Edite as **Associações** de outros sites para remover portas que correspondam àquelas atribuídas ao site **SMSWEB**.  

    2.  Inicie o site **SMSWEB**.  

    3.  Reinicie o serviço **SMS_SITE_COMPONENT_MANAGER** no servidor do site.  
