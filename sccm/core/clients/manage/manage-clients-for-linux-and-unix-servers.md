---
title: Gerenciar clientes Linux e UNIX
titleSuffix: Configuration Manager
description: Gerenciar clientes em servidores Linux e UNIX no Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 32e7a643c98fc8a6bd4baccda703146816930367
ms.sourcegitcommit: d8d142044586a53709b4478ad945f714737c8d6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58524040"
---
# <a name="how-to-manage-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Como gerenciar clientes em servidores Linux e UNIX no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

> [!Important]  
> A partir da versão 1902, o Configuration Manager não dá suporte a clientes Linux ou UNIX. 
> 
> Considere o Gerenciamento do Microsoft Azure para gerenciar servidores Linux. As soluções do Azure têm amplo suporte para Linux que, na maioria dos casos, supera a funcionalidade do Configuration Manager, incluindo o gerenciamento de patches de ponta a ponta para o Linux.

Ao gerenciar servidores Linux e UNIX com o Configuration Manager, você pode configurar coleções, janelas de manutenção e configurações do cliente para ajudar a gerenciar os servidores. Além disso, embora o cliente do Configuration Manager para Linux e UNIX não tenha uma interface de usuário, você pode forçar o cliente a pesquisar manualmente a política de cliente.

##  <a name="BKMK_CollectionsforLnU"></a> Coleções de servidores Linux e UNIX  
 Use coleções para gerenciar grupos de servidores Linux e UNIX da mesma maneira que usa coleções para gerenciar outros tipos de clientes. Coleções podem ser coleções de associação direta ou coleções com base em consulta. Coleções baseadas em consulta identificam os sistemas operacionais cliente, as configurações de hardware ou outros detalhes sobre o cliente que são armazenados no banco de dados do site. Por exemplo, você pode usar coleções que incluem servidores Linux e UNIX para gerenciar as seguintes configurações:  

- Configurações do cliente  

- Implantações de software  

- Impor janelas de manutenção  

  Para poder identificar um cliente Linux ou UNIX pelo seu sistema operacional ou sua distribuição, é necessário coletar o [inventário de hardware](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md) do cliente.  

  As configurações padrão do cliente para inventário de hardware incluem informações sobre o sistema operacional de um computador cliente. Você pode usar a propriedade **Legenda** da classe **Sistema Operacional** para identificar o sistema operacional de um servidor Linux ou UNIX.  

  Você pode exibir detalhes sobre os computadores que executam o cliente do Configuration Manager para Linux e UNIX no nó **Dispositivos** do workspace **Ativos e Conformidade** no console do Configuration Manager. No workspace **Ativos e Conformidade** do console do Configuration Manager, é possível exibir o nome do sistema operacional de cada computador na coluna **Sistema Operacional**.  

  Por padrão, os servidores Linux e UNIX são membros da coleção **Todos os Sistemas** . Recomendamos que você compile coleções personalizadas que incluam somente servidores Linux e UNIX ou um subconjunto deles. As coleções personalizadas permitem que você gerencie operações como implantação de software ou atribuição de configurações do cliente a grupos de computadores semelhantes, para que você possa medir com precisão o sucesso de uma implantação.   

  Ao compilar uma coleção personalizada para servidores Linux e UNIX, inclua consultas de regra de associação que incluem o atributo Caption para o atributo Operating System. Para obter informações sobre a criação de coleções, consulte [Como criar coleções no System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

##  <a name="BKMK_MaintenanceWindowsforLnU"></a> Janelas de manutenção para servidores Linux e UNIX  
 O cliente do Configuration Manager para servidores Linux e UNIX dá suporte ao uso de [janelas de manutenção](../../../core/clients/manage/collections/use-maintenance-windows.md). Esse suporte não foi alterado em clientes baseados em Windows.  

##  <a name="BKMK_ClientSettingsforLnU"></a> Configurações do cliente para servidores Linux e UNIX  
 Você pode [definir configurações do cliente](../../../core/clients/deploy/configure-client-settings.md) que se aplicam a servidores Linux e UNIX da mesma forma que você define configurações para outros clientes.  

 Por padrão, as **Configurações Padrão do Agente Cliente** se aplicam a servidores Linux e UNIX. Você também pode criar configurações de cliente personalizadas e implantá-las em coleções de clientes específicos.  

 Não há outras configurações do cliente que se aplicam somente aos clientes Linux e UNIX. No entanto, há configurações padrão do cliente que não se aplicam a clientes Linux e UNIX. O cliente para Linux e UNIX só aplica configurações para funcionalidade que ele dá suporte.  

 Por exemplo, uma configuração de dispositivo de cliente personalizada que habilita e configura definições de controle remoto seria ignorada por servidores Linux e UNIX porque o cliente para Linux e UNIX não oferece suporte a controle remoto.  

##  <a name="BKMK_PolicyforLnU"></a> Política de computador para servidores Linux e UNIX  
 O cliente para servidores Linux e UNIX sonda periodicamente seu site em relação à política de computador para saber mais sobre as configurações solicitadas e para verificar se há implantações.  

 Você também pode forçar o cliente em um servidor Linux ou UNIX a sondar imediatamente a política do computador. Para fazer isso, use as credenciais de **raiz** no servidor para executar o seguinte comando: **/opt/microsoft/configmgr/bin/ccmexec -rs policy**  

 Os detalhes sobre a pesquisa de política de computador são inseridos no arquivo de log do cliente compartilhado, **scxcm.log**.  

> [!NOTE]  
>  O cliente do Configuration Manager para Linux e UNIX nunca solicita nem processa a política de usuário.  

##  <a name="BKMK_ManageLinuxCerts"><a name="BKMK_ManageLinuxCerts"></a> Como gerenciar certificados no cliente para Linux e UNIX  
 Depois de instalar o cliente para Linux e UNIX, você pode usar a ferramenta **certutil** para atualizar o cliente com um novo certificado PKI e importar uma nova CRL (lista de Certificados Revogados). Quando você instala o cliente para Linux e UNIX, essa ferramenta é colocada em `/opt/microsoft/configmgr/bin/certutil`. 

 Para gerenciar certificados, em cada cliente execute certutil com uma das seguintes opções:  

|Opção|Mais informações|  
|------------|----------------------|  
|`importPFX`|Use esta opção para especificar um certificado para substituir o certificado que está sendo usado atualmente por um cliente.<br /><br /> Quando você usa o `-importPFX`, também é necessário usar o parâmetro de linha de comando `-password` para fornecer a senha associada ao arquivo PKCS#12.<br /><br /> Use `-rootcerts` para especificar requisitos de certificado raiz adicionais.<br /><br /> Exemplo: `certutil -importPFX <path to the PKCS#12 certificate> -password <certificate password> [-rootcerts <comma-separated list of certificates>]`|  
|`importsitecert`|Use esta opção para atualizar o certificado de assinatura de servidor do site localizado no servidor de gerenciamento.<br /><br /> Exemplo: `certutil -importsitecert <path to the DER certificate>`|  
|`importcrl`|Use esta opção para atualizar a CRL no cliente com um ou mais caminhos de arquivo da CRL.<br /><br /> Exemplo: `certutil -importcrl <comma separated CRL file paths>`|  
