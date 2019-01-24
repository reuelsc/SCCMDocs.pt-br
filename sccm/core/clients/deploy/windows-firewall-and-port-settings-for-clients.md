---
title: Configurações de porta firewall de cliente do Windows
titleSuffix: Configuration Manager
description: Selecione as configurações de porta e de Firewall do Windows para clientes no System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: dce4b640-c92f-401a-9873-ce9aa9262014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 94af249b91735a535ea4056f8a5f19d120632770
ms.sourcegitcommit: 818f98187d377a90263d1b1c89d4c1fdbf8c908b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2019
ms.locfileid: "54398482"
---
# <a name="windows-firewall-and-port-settings-for-clients-in-system-center-configuration-manager"></a>Configurações do Firewall do Windows e de porta para computadores cliente no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os computadores cliente no System Center Configuration Manager que executam o Firewall do Windows muitas vezes exigem a configuração de exceções para permitir a comunicação com seu site. As exceções que você deverá configurar dependem dos recursos de gerenciamento usados com o cliente do Configuration Manager.  

 Use as seções a seguir para identificar esses recursos de gerenciamento e para obter mais informações sobre como configurar o Firewall do Windows para essas exceções.  

##  <a name="BKMK_ModifyingWindowsFirewall"></a> Modificando as portas e os programas permitidos pelo Firewall do Windows  
 Use o procedimento a seguir para modificar as portas e os programas no Firewall do Windows para o cliente do Configuration Manager.  

#### <a name="to-modify-the-ports-and-programs-permitted-by-windows-firewall"></a>Para modificar as portas e os programas permitidos pelo Firewall do Windows  

1.  No computador que executa o Firewall do Windows, abra o Painel de Controle.  

2.  Clique com o botão direito do mouse em **Firewall do Windows**e clique em **Abrir**.  

3.  Configure as exceções necessárias e os programas e portas personalizados de que você precisa.  

## <a name="programs-and-ports-that-configuration-manager-requires"></a>Programas e portas que o Configuration Manager exige  
 Os seguintes recursos do Configuration Manager exigem exceções no Firewall do Windows:  

### <a name="queries"></a>Consultas  
 Se você executar o console do Configuration Manager em um computador com o Firewall do Windows, as consultas falharão na primeira execução e o sistema operacional exibirá uma caixa de diálogo perguntando se você deseja desbloquear o statview.exe. Se você desbloquear o statview.exe, as futuras consultas serão executadas sem erros. Também é possível adicionar o statview.exe manualmente à lista de programas e serviços na guia **Exceções** do Firewall do Windows antes de executar uma consulta.  

### <a name="client-push-installation"></a>Instalação do Cliente por Push  
 Para usar push para instalar o cliente do Configuration Manager, adicione o seguinte como exceções ao Firewall do Windows:  

-   Entrada e saída: **Compartilhamento de arquivos e impressoras**  

-   Entrada: **WMI (Instrumentação de Gerenciamento do Windows)**  

### <a name="client-installation-by-using-group-policy"></a>Instalação de cliente usando Política de Grupo  
 Para usar Política de Grupo para instalar o cliente do Configuration Manager, adicione **Compartilhamento de Arquivo e Impressora** como exceção ao Firewall do Windows.  

### <a name="client-requests"></a>Solicitações de cliente  
 Para computadores cliente se comunicarem com os sistemas de sites do Configuration Manager, adicione o seguinte como exceções ao Firewall do Windows:  

 Saída: Porta TCP **80** (para comunicação HTTP)  

 Saída: Porta TCP **443** (para comunicação HTTPS)  

> [!IMPORTANT]  
>  Esses são números de porta padrão que podem ser alterados no Configuration Manager. Para obter mais informações, consulte [Como configurar portas de comunicação do cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md). Se os valores padrão dessas portas forem alterados, será necessário configurar também exceções correspondentes no Firewall do Windows.  

### <a name="client-notification"></a>Notificação de Cliente  
 Para o ponto de gerenciamento notificar os computadores cliente sobre uma ação que deve ser executada quando um usuário administrativo selecionar uma ação de cliente no console do Configuration Manager, como baixar a política do computador ou iniciar uma verificação de malware, adicione o seguinte como exceção ao Firewall do Windows:  

 Saída: Porta TCP **10123**  

 Se essa comunicação não tiver êxito, o Configuration Manager voltará a usar automaticamente a porta de comunicação cliente-ponto de gerenciamento existente de HTTP ou HTTPS:  

 Saída: Porta TCP **80** (para comunicação HTTP)  

 Saída: Porta TCP **443** (para comunicação HTTPS)  

> [!IMPORTANT]  
>  Esses são números de porta padrão que podem ser alterados no Configuration Manager. Para obter mais informações, consulte [Como configurar portas de comunicação do cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md). Se os valores padrão dessas portas forem alterados, será necessário configurar também exceções correspondentes no Firewall do Windows.  

### <a name="remote-control"></a>Controle remoto  
 Para usar o controle remoto do Configuration Manager, autorize a seguinte porta:  

-   Entrada: Porta TCP **2701**  

### <a name="remote-assistance-and-remote-desktop"></a>Assistência Remota e Área de Trabalho Remota  
 Para iniciar a Assistência Remota no console do Configuration Manager, adicione o programa personalizado **Helpsvc.exe** e a porta de entrada personalizada TCP **135** à lista de programas e serviços permitidos no Firewall do Windows no computador cliente. Também é necessário permitir a **Assistência Remota** e a **Área de Trabalho Remota**. Se você iniciar a Assistência Remota no computador cliente, o Firewall do Windows irá configurar e permitir automaticamente a **Assistência Remota** e a **Área de Trabalho Remota**.  

### <a name="wake-up-proxy"></a>Proxy de ativação  
 Se a configuração de cliente do proxy de ativação for habilitada, um novo serviço chamado Proxy de Ativação do ConfigMgr usará um protocolo ponto a ponto para verificar se outros computadores estão ativos na sub-rede e ativá-los, se necessário. Essa comunicação usa as seguintes portas:  

 Saída: Porta UDP **25536**  

 Saída: Porta UDP **9**  

 Esses são os números da porta padrão que podem ser alterados no Configuration Manager usando as configurações de clientes de **Gerenciamento de Energia** para **Número de porta proxy de ativação (UDP)** e **Número de porta Wake On LAN (UDP)**. Se você especificar a configuração de cliente **Gerenciamento de energia**: **Exceção do Firewall do Windows para proxy de ativação**, essas portas serão automaticamente configuradas no Firewall do Windows para clientes. No entanto, se os clientes tiverem em execução um firewall diferente, configure manualmente as exceções para esses números de porta.  

 Além dessas portas, o proxy de ativação também usa mensagens de solicitação de eco ICMP (Internet Control Message Protocol) de um computador cliente para outro computador cliente. Essa comunicação é usada para confirmar se o outro computador cliente está ativo na rede. O ICMP é, por vezes, referido como comandos ping TCP/IP.  

 Para mais informações sobre o proxy de ativação, confira [Planejar a ativação de clientes no System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

### <a name="windows-event-viewer-windows-performance-monitor-and-windows-diagnostics"></a>Visualizador de Eventos do Windows, Monitor de Desempenho do Windows e Diagnóstico do Windows  
 Para acessar o Visualizador de Eventos do Windows, o Monitor de Desempenho do Windows e o Diagnóstico do Windows no console do Configuration Manager, habilite **Compartilhamento de Arquivo e Impressora** como exceção no Firewall do Windows.  

## <a name="ports-used-during-configuration-manager-client-deployment"></a>Portas usadas durante a implantação do cliente do Configuration Manager  
 As tabelas a seguir listam as portas que são usadas durante o processo de instalação do cliente.  

> [!IMPORTANT]  
>  Se houver um firewall entre os servidores de sistema de site e o computador cliente, confirme se o firewall permite o tráfego para as portas necessárias ao método de instalação de cliente selecionado. Por exemplo, firewalls geralmente impedem o êxito na instalação de cliente por push porque bloqueiam o protocolo SMB e as RPCs (chamadas de procedimento remoto). Neste cenário, use um método diferente de instalação de cliente, como instalação manual (executando o arquivo CCMSetup.exe) ou instalação de cliente baseada em Política de Grupo. Esses métodos alternativos de instalação de cliente não exigem SMB ou RPC.  

 Para obter mais informações sobre como configurar o Firewall do Windows no computador cliente, consulte [Modificando as portas e os programas permitidos pelo Firewall do Windows](#BKMK_ModifyingWindowsFirewall).  

### <a name="ports-that-are-used-for-all-installation-methods"></a>Portas que são usadas para todos os métodos de instalação  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP do computador cliente para um ponto de status de fallback, quando um ponto de status de fallback é atribuído ao cliente.|--|80 (Consulte a observação 1, **Porta alternativa disponível**)|  

### <a name="ports-that-are-used-with-client-push-installation"></a>Portas que são usadas com instalação de cliente por push  
 Além das portas listadas na tabela a seguir, a instalação de cliente por push também usa mensagens de solicitação de eco ICMP do servidor do site para o computador cliente para confirmar se o computador cliente está disponível na rede. O ICMP é, por vezes, referido como comandos ping TCP/IP. O ICMP não tem um número de protocolo UDP ou TCP, portanto, não está listado na tabela a seguir. Contudo, todo dispositivo de rede interventor, como firewalls, deve permitir o tráfego ICMP para que a instalação de cliente por push seja bem-sucedida.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB entre o servidor do site e o computador cliente.|--|445|  
|Mapeador de ponto de extremidade RPC entre o servidor do site e o computador cliente.|135|135|  
|Portas dinâmicas RPC entre o servidor do site e o computador cliente.|--|DINÂMICO|  
|Protocolo HTTP do computador cliente para um ponto de gerenciamento quando a conexão é por HTTP.|--|80 (Consulte a observação 1, **Porta alternativa disponível**)|  
|Protocolo HTTPS do computador cliente para um ponto de gerenciamento quando a conexão é por HTTPS.|--|443 (Veja a observação 1, **Porta alternativa disponível**)|  

### <a name="ports-that-are-used-with-software-update-point-based-installation"></a>Portas que são usadas com a instalação baseada em ponto de atualização de software  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP do computador cliente para o ponto de atualização de software.|--|80 ou 8530 (Consulte a observação 2, **Windows Server Update Services**)|  
|Protocolo HTTPS do computador cliente para o ponto de atualização de software.|--|443 ou 8531 (Consulte a observação 2, **Windows Server Update Services**)|  
|O Protocolo SMB entre o servidor de origem e o computador cliente ao especificar a propriedade de linha de comando CCMSetup **/source:&lt;Caminho\>**.|--|445|  

### <a name="ports-that-are-used-with-group-policy-based-installation"></a>Portas que são usadas com a instalação baseada em Política de Grupo  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP do computador cliente para um ponto de gerenciamento quando a conexão é por HTTP.|--|80 (Consulte a observação 1, **Porta alternativa disponível**)|  
|Protocolo HTTPS do computador cliente para um ponto de gerenciamento quando a conexão é por HTTPS.|--|443 (Veja a observação 1, **Porta alternativa disponível**)|  
|O Protocolo SMB entre o servidor de origem e o computador cliente ao especificar a propriedade de linha de comando CCMSetup **/source:&lt;Caminho\>**.|--|445|  

### <a name="ports-that-are-used-with-manual-installation-and-logon-script-based-installation"></a>Portas que são usadas com a instalação manual e a instalação baseada em script de logon  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB entre o computador cliente e um compartilhamento de rede a partir do qual o CCMSetup.exe é executado.<br /><br /> Ao instalar o Configuration Manager, os arquivos de origem da instalação do cliente são copiados e compartilhados automaticamente da pasta *&lt;CaminhoInstalação\>* \Client nos pontos de gerenciamento. No entanto, é possível copiar esses arquivos e criar um novo compartilhamento em qualquer computador na rede. Como alternativa, é possível eliminar esse tráfego de rede executando o CCMSetup.exe localmente, por exemplo, usando mídia removível.|--|445|  
|Protocolo HTTP do computador cliente para um ponto de gerenciamento quando a conexão é feita por HTTP e a propriedade de linha de comando **/origem:&lt;Caminho\>** do CCMSetup não é especificada.|--|80 (Consulte a observação 1, **Porta alternativa disponível**)|  
|Protocolo HTTPS do computador cliente para um ponto de gerenciamento quando a conexão é por HTTPS e a propriedade de linha de comando **/origem:&lt;Caminho\>** do CCMSetup não é especificada.|--|443 (Veja a observação 1, **Porta alternativa disponível**)|  
|O Protocolo SMB entre o servidor de origem e o computador cliente ao especificar a propriedade de linha de comando CCMSetup **/source:&lt;Caminho\>**.|--|445|  

### <a name="ports-that-are-used-with-software-distribution-based-installation"></a>Portas que são usadas com a instalação baseada em distribuição de software  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB entre o ponto de distribuição e o computador cliente.|--|445|  
|Protocolo HTTP do cliente para um ponto de distribuição quando a conexão é por HTTP.|--|80 (Consulte a observação 1, **Porta alternativa disponível**)|  
|Protocolo HTTPS do cliente para um ponto de distribuição quando a conexão é por HTTPS.|--|443 (Veja a observação 1, **Porta alternativa disponível**)|  

## <a name="notes"></a>Anotações  
 **1 Porta alternativa disponível** No Configuration Manager, você pode definir uma porta alternativa para esse valor. Se tiver sido definida uma porta personalizada, substitua essa porta personalizada ao definir as informações de filtro IP para políticas IPsec ou para configurar firewalls.  

 **2 Windows Server Update Services** É possível instalar o Windows Server Update Service (WSUS) no site padrão (porta 80) ou em um site personalizado (porta 8530).  

 Após a instalação, é possível alterar a porta. Não é necessário usar o mesmo número de porta em toda a hierarquia do site.  

 Se a porta HTTP for 80, a porta HTTPS deverá ser 443.  

 Se a porta HTTP tiver outro número, a porta HTTPS deverá ser um número acima. Por exemplo, 8530 e 8531.
