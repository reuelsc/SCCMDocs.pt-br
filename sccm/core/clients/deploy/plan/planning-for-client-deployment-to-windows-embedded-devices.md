---
title: Planejar a implantação de cliente em dispositivos Windows Embedded
titleSuffix: Configuration Manager
description: Planeje a implantação de cliente em dispositivos do Windows Embedded no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 038e61f9-f49d-41d1-9a9f-87bec9e00d5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6ca987411775ec3a6fbe626d4b34f83313673f5b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32334820"
---
# <a name="planning-for-client-deployment-to-windows-embedded-devices-in-system-center-configuration-manager"></a>Planejando a implantação de cliente em dispositivos do Windows Embedded no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

<a name="BKMK_DeployClientEmbedded"></a> Se o dispositivo Windows Embedded não incluir o cliente do System Center Configuration Manager, você poderá usar algum dos métodos de instalação do cliente se o dispositivo atender às dependências necessárias. Se o dispositivo inserido der suporte a filtros de gravação, você deverá desabilitar esses filtros para poder instalar o cliente e reabilitá-los depois que o cliente for instalado e atribuído a um site.  

 É importante lembrar que quando os filtros são desabilitados, os drivers de filtro não devem ser desabilitados. Normalmente, estes drivers são iniciados automaticamente quando o computador é iniciado. Desabilitar os drivers impedirá a instalação do cliente ou interferirá na orquestração de filtro de gravação que fará com que as operações de cliente falhem. Estes são os serviços associados a cada tipo de filtro de gravação que devem permanecer em execução:  

|Tipo de filtro de gravação|Driver|Digite|Descrição|  
|-----------------------|------------|----------|-----------------|  
|EWF|EWF|Kernel|Implementa o redirecionamento de E/S de nível de setor nos volumes protegidos.|  
|FBWF|FBWF|Sistema de arquivos|Implementa o redirecionamento de E/S de nível de arquivo nos volumes protegidos.|  
|UWF|uwfreg|Kernel|Redirecionador de Registro UWF|  
|UWF|uwfs|Sistema de arquivos|Redirecionador de arquivo UWF|  
|UWF|uwfvol|Kernel|Gerenciador de volumes UWF|  

 Os filtros de gravação controlam como o sistema operacional mo dispositivo inserido é atualizado quando você faz alterações, como ao instalar um software. Quando filtros de gravação estão habilitados, em vez de fazer alterações diretamente no sistema operacional, essas alterações são redirecionadas para uma sobreposição temporária. Se as alterações forem gravadas somente na sobreposição, elas serão perdidas quando o dispositivo inserido for desligado. No entanto, se os filtros de gravação forem desabilitados temporariamente, as alterações poderão ser permanentes para que você não tenha de fazê-las novamente (ou reinstalar o software) sempre que o dispositivo inserido é reiniciado. Porém, a ação de desabilitar e reabilitar temporariamente os filtros de gravação requer uma ou mais reinicializações, de modo que você geralmente queira controlar quando isso acontece configurando janelas de manutenção para que as reinicializações ocorram fora do horário comercial.  

 É possível configurar opções para desabilitar e reabilitar automaticamente os filtros de gravação ao implantar software como aplicativos, sequências de tarefas, atualizações de software e o cliente do Endpoint Protection. A exceção é para as linhas de base de configuração com itens de configuração que usam a correção automática. Nesse cenário, a correção sempre ocorre na sobreposição para que ela esteja disponível somente até que o dispositivo seja reiniciado. A correção é aplicada novamente no próximo ciclo de avaliação, mas somente na sobreposição, que é apagada na reinicialização. Para forçar o Configuration Manager a confirmar as alterações de correção, é possível implantar a linha de base de configuração e outra implantação de software que dá suporte à confirmação da alteração assim que possível.  

 Se os filtros de gravação estiverem desabilitados, você poderá instalar o software em dispositivos Windows Embedded usando o Centro de Software. No entanto, se os filtros de gravação estiverem habilitados, ocorrerá falha na instalação e o Configuration Manager exibirá uma mensagem de erro informando que você não tem permissões suficientes para instalar o aplicativo.  

> [!WARNING]  
>  Mesmo que você não selecione as opções do Configuration Manager para confirmar as alterações, elas poderão ser confirmadas se outra instalação de software ou alteração que confirme as alterações for feita. Nesse cenário, as alterações originais serão confirmadas além das novas alterações.  

 Quando o Configuration Manager desabilita os filtros de gravação para tornar as alterações permanentes, somente os usuários com direitos administrativos locais podem fazer logon e usar o dispositivo inserido. Durante esse período, os usuários com direitos limitados são bloqueados e veem uma mensagem informando que o computador está indisponível pois está em manutenção. Isso ajuda a proteger o dispositivo enquanto ele está em um estado em que as alterações podem ser aplicadas permanentemente, e esse comportamento de bloqueio do modo de manutenção é outro motivo para configurar uma janela de manutenção por um período quando os usuários não fazem logon nesses dispositivos.  

 O Configuration Manager dá suporte ao gerenciamento dos seguintes tipos de filtros de gravação:  

-   FBWF (Filtro de Gravação Baseado em Arquivo) – Para mais informações, consulte [Filtro de Gravação Baseado em Arquivos](http://go.microsoft.com/fwlink/?LinkID=204717).  

-   RAM de EWF (Filtro de Gravação Avançado) – Para mais informações, consulte [Filtro de Gravação Avançado](http://go.microsoft.com/fwlink/?LinkId=204718).  

-   UWF (Filtro de Gravação Unificado) – Para mais informações, consulte [Filtro de Gravação Unificado](http://go.microsoft.com/fwlink/?LinkId=309236).  

 O Configuration Manager não dá suporte a operações do filtro de gravação quando o dispositivo Windows Embedded está no modo EWF RAM Reg.  

> [!IMPORTANT]  
>  Se tiver opção, use FBWF (filtros de gravação com base em arquivos) com o Configuration Manager para maior eficiência e escalabilidade mais alta.
>
> **Somente para dispositivos que usam FBWF** ‑ defina as seguintes exceções para manter o estado do cliente e os dados do inventário entre as reinicializações do dispositivo:  
>   
>  -   CCMINSTALLDIR\\\*.sdf  
> -   CCMINSTALLDIR\ServiceData  
> -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
>   
>  Os dispositivos que executam o Windows Embedded 8.0 e posterior não dão suporte a exclusões que contêm caracteres curinga. Nesses dispositivos, você deve configurar individualmente as seguintes exclusões:  
>   
>  -   Todos os arquivos em CCMINSTALLDIR com a extensão .sdf normalmente:  
>   
>     -   UserAffinityStore.sdf  
>     -   InventoryStore.sdf  
>     -   CcmStore.sdf  
>     -   StateMessageStore.sdf  
>     -   CertEnrollmentStore.sdf  
> -   CCMINSTALLDIR\ServiceData  
> -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
>   
> **Somente para dispositivos que usam FBWF e UWF**: quando os clientes em um grupo de trabalho usam certificados de autenticação para pontos de gerenciamento, você também deve excluir a chave privada para garantir que o cliente continue a se comunicar com o ponto de gerenciamento. Nesses dispositivos, configure as seguintes exceções:  
>   
>  -   c:\Windows\System32\Microsoft\Protect  
> -   c:\ProgramData\Microsoft\Crypto  
> -   HKEY_LOCAL_MACHINE\Software\Microsoft\SystemCertificates\SMS\Certificates  

 Para ver um exemplo da implantação e gerenciamento de dispositivos Windows Embedded habilitados para filtro de gravação no Configuration Manager, consulte [Cenário de exemplo para implantar e gerenciar os clientes do System Center Configuration Manager em dispositivos Windows Embedded](../../../../core/clients/deploy/example-scenario-for-deploying-and-managing-clients-on-windows-embedded-devices.md).  

 Para obter mais informações sobre como compilar imagens para dispositivos Windows Embedded e configurar filtros de gravação, consulte a documentação do Windows Embedded ou entre em contato com o OEM.  

> [!NOTE]  
>  Quando você seleciona as plataformas aplicáveis para implantações de software e itens de configuração, elas exibem as famílias do Windows Embedded em vez de versões específicas. Use a lista a seguir para mapear a versão específica do Windows Embedded para as opções na caixa de listagem:  
>   
>  -   **sistemas operacionais inseridos baseados no Windows XP (32 bits)** inclui o seguinte:  
>   
>      -   Windows XP Embedded  
>     -   Windows Embedded for Point of Service  
>     -   Windows Embedded Standard 2009  
>     -   Windows Embedded POSReady 2009  
> -   **Sistemas operacionais inseridos baseados no Windows 7 (32 bits)** inclui o seguinte:  
>   
>      -   Windows Embedded Standard 7 (32 bits)  
>     -   Windows Embedded POSReady 7 (32 bits)  
>     -   Windows ThinPC  
> -   **Os sistemas operacionais inseridos baseados no Windows 7 (64 bits)** incluem o seguinte:  
>   
>      -   Windows Embedded Standard 7 (64 bits)  
>     -   Windows Embedded POSReady 7 (64 bits)
