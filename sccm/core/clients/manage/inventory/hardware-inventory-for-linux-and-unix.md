---
title: Inventário de hardware para Linux e UNIX
titleSuffix: Configuration Manager
description: Saiba como usar o inventário de hardware para Linux e UNIX no System Center Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1026d616-2a20-4fb2-8604-d331763937f8
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 68e60611356cbaea3dc14a42776e89ecdc951008
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32339410"
---
# <a name="hardware-inventory-for-linux-and-unix-in-system-center-configuration-manager"></a>Inventário de hardware para Linux e UNIX no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O cliente do System Center Configuration Manager para Linux e UNIX dá suporte ao inventário de hardware. Depois de coletar inventários de hardware, você pode executar o inventário de exibição no Gerenciador de recursos ou nos relatórios do Configuration Manager e usar essas informações para criar consultas e coleções que habilitam as seguintes operações:  

-   Implantação de software  

-   Impor janelas de manutenção  

-   Implantar configurações personalizadas do cliente  

 O inventário de hardware para servidores Linux e UNIX usa um servidor CMI (Common Information Model) baseado em padrões. O servidor CIM é executado como um serviço de software (ou daemon) e fornece uma infraestrutura de gerenciamento baseada em padrões da DMTF (Força-tarefa de gerenciamento distribuída). O servidor CIM fornece funcionalidade semelhante aos recursos de CIM do WMI (Windows Management Infrastructure ) que estão disponíveis em computadores baseados no Windows.  

 A partir da atualização cumulativa 1, o cliente para Linux e UNIX usa o software livre **omiserver** versão 1.0.6 no **Open Group**. (Antes da atualização cumulativa 1, o cliente usou **nanowbem** como seu servidor CIM).  

 O servidor CIM é instalado como parte do cliente para Linux e UNIX. O cliente para Linux e UNIX se comunica diretamente com o servidor CIM e não usa a interface do WS-MAN do servidor CIM. A porta WS-MAN no servidor de CIM é desabilitada quando o cliente é instalado. A Microsoft desenvolveu o servidor CIM que agora está disponível como software livre por meio do projeto OMI (Infraestrutura de Gerenciamento Aberto). Para obter mais informações sobre o projeto de Infraestrutura de Gerenciamento Aberto, veja o site do [The Open Group](http://go.microsoft.com/fwlink/p/?LinkId=262317) .  

 O inventário de hardware em servidores Linux e UNIX funciona pelo mapeamento de classes e propriedades Win32 WMI existentes para as classes e propriedades equivalentes em servidores Linux e UNIX. Esse mapeamento de classes e propriedades de um para um permite que o inventário de hardware do Linux e UNIX seja integrado com o Configuration Manager. Os dados de inventário de servidores Linux e UNIX são exibidos com o inventário de computadores baseados em Windows no console e relatórios do Configuration Manager. Isso fornece uma experiência consistente de gerenciamento heterogêneo.  

> [!TIP]  
>  Você pode usar o valor da **Legenda** para a classe do **Sistema Operacional** para identificar os diferentes sistemas operacionais com Linux e UNIX em consultas e coleções.  

##  <a name="BKMK_ConfigHardwareforLnU"></a> Configurando o inventário de hardware para servidores Linux e UNIX  
 Você pode usar as configurações padrão de cliente ou criar configurações personalizadas do dispositivo para configurar o inventário de hardware. Ao usar configurações personalizadas do dispositivo, você pode configurar as classes e propriedades que você deseja coletar apenas dos servidores Linux e UNIX. Você também pode especificar agendas personalizadas ao coletar inventários completos e delta de seus servidores Linux e UNIX.  

 O cliente para Linux e UNIX dá suporte para as seguintes classes de inventário de hardware que estão disponíveis em servidores Linux e UNIX:  

-   Win32_BIOS  

-   Win32_ComputerSystem  

-   Win32_DiskDrive  

-   Win32_DiskPartition  

-   Win32_NetworkAdapter  

-   Win32_NetworkAdapterConfiguration  

-   Win32_OperatingSystem  

-   Win32_Process  

-   Win32_Service  

-   Win32Reg_AddRemovePrograms  

-   SMS_LogicalDisk  

-   SMS_Processor  

 Nem todas as propriedades para essas classes de inventário são habilitadas para computadores Linux e UNIX no Configuration Manager.  

##  <a name="BKMK_OperationsforHardwareforLnU"></a> Operações de inventário de hardware  
 Depois de coletar inventários de hardware dos servidores Linux e UNIX, você pode exibir e usar essas informações da mesma maneira que você exibir o inventário coletado dos outros computadores:  

-   Use o Gerenciador de Recursos para exibir informações detalhadas sobre o inventário de hardware de servidores Linux e UNIX  

-   Crie consultas com base nas configurações específicas de hardware  

-   Crie coleções baseadas em consulta que se baseiam em configurações de hardware específicas  

-   Execute os relatórios que exibem detalhes específicos sobre as configurações de hardware  

 O inventário de hardware em um servidor Linux ou UNIX é executado de acordo com o agendamento configurado nas configurações do cliente. Por padrão, esse é a cada sete dias. O cliente para Linux e UNIX dá suporte aos ciclos de inventário completos e ciclos de inventário delta.  

 Você também pode forçar o cliente em um servidor Linux ou UNIX a executar o inventário de hardware imediatamente. Para executar o inventário de hardware em um cliente, use as credenciais **raiz** para executar o comando a seguir para iniciar um ciclo de inventário de hardware: **opt/microsoft/configmgr/bin/ccmexec -rs hinv**  

 As ações de inventário de hardware são inseridas no arquivo de log do cliente, **scxcm.log**.  

##  <a name="BKMK_CustomHINVforLinux"></a> Como usar a infraestrutura de gerenciamento aberto para criar um inventário de hardware personalizado  
 O cliente para Linux e UNIX dá suporte para o inventário de hardware personalizado que você pode criar usando a OMI (Infraestrutura de Gerenciamento Aberto). Para fazer isso, use as seguintes etapas:  

1.  Criar um provedor de inventário personalizado por meio da OMI de origem  

2.  Configure computadores para usar o novo provedor de relatórios de estoque  

3.  Habilitar o Configuration Manager para dar suporte ao novo provedor  

###  <a name="BKMK_LinuxProvider"></a> Crie um provedor de inventário de hardware personalizado para computadores Linux e UNIX:  
 Para criar um provedor de inventário de hardware personalizado para o cliente do Configuration Manager para Linux e UNIX, use **OMI Source – v.1.0.6** e siga as instruções da Guia de Introdução à OMI. Esse processo inclui a criação de um arquivo MOF (Managed Object Format) que define o esquema do novo provedor. Posteriormente, você importa o arquivo MOF no Configuration Manager para habilitar o suporte da nova classe personalizada de inventário.  

 Tanto o OMI Source - v.1.0.6 quanto o Guia de Introdução à OMI estão disponíveis para download no site do [The Open Group](http://go.microsoft.com/fwlink/p/?LinkId=262317) . Você pode localizar esses downloads na guia **Documentos** na seguinte página da Web no site OpenGroup.org: [OMI (Infraestrutura de Gerenciamento Aberta)](http://go.microsoft.com/fwlink/p/?LinkId=286805).  

###  <a name="BKMK_AddProvidertoLinux"></a> Configure cada computador que executa o Linux ou UNIX com o provedor de inventário de hardware personalizado:  
 Depois de criar um provedor de inventário personalizado, você deve copiar e registrar o arquivo de biblioteca do provedor em cada computador que tenha inventário que você deseja coletar.  

1.  Copie a biblioteca do provedor para cada computador Linux e UNIX, do qual você deseja coletar o inventário. O nome da biblioteca do provedor é semelhante à seguinte: **XYZ_MyProvider.so**  

2.  Em seguida, em cada computador Linux e UNIX, registre a biblioteca do provedor no servidor da OMI. O servidor da OMI é instalado no computador quando você instala o cliente do Configuration Manager para Linux e UNIX, mas você deverá registrar os provedores personalizados manualmente. Use a seguinte linha de comando para registrar o provedor: **/opt/microsoft/omi/bin/omireg XYZ_MyProvider.so**  

3.  Depois de registrar o novo provedor, teste-o usando a ferramenta **omicli** . A ferramenta **omicli** é instalada em cada computador Linux e UNIX, quando você instala o cliente do Configuration Manager para Linux e UNIX. Por exemplo, no local em que **XYZ_MyProvider** é o nome do provedor que você criou, execute o seguinte comando no computador: **/opt/microsoft/omi/bin/omicli ei root/cimv2 XYZ_MyProvider**  

     Para obter informações sobre o **omicli** e provedores personalizados de teste, veja o Guia de Introdução à OMI.  

> [!TIP]  
>  Use a distribuição de software para provedores personalizados de implantar e registrar provedores personalizados em cada computador cliente Linux e UNIX.  

###  <a name="BKMK_AddLinuxProvidertoCM"></a> Habilite a nova classe de inventário do Configuration Manager:  
 Antes que o Configuration Manager possa gerar relatórios sobre o inventário relatado pelo novo provedor em computadores Linux e UNIX, você deve importar o arquivo MOF (Managed Object Format) que define o esquema do provedor personalizado.  

 Para importar um arquivo MOF personalizado para o Configuration Manager, consulte [Como configurar o inventário de hardware no System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  
