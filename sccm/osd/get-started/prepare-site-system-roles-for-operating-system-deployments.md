---
title: "Preparar as funções do sistema de sites para implantações de sistema operacional | Microsoft Docs"
description: "Configure as funções do sistema de sites antes de implantar os sistemas operacionais no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 11c0f169afebdb071fefb5ce300fd1ae3481a94f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-site-system-roles-for-operating-system-deployments-with-system-center-configuration-manager"></a>Preparar as funções do sistema de sites para implantações de sistema operacional com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para implantar sistemas operacionais no System Center Configuration Manager, primeiro é necessário preparar as seguintes funções do sistema de sites que exigem configurações e considerações específicas.

##  <a name="BKMK_DistributionPoints"></a> Pontos de distribuição  
 Uma função do sistema de sites do ponto de distribuição que contém arquivos de origem para serem baixados por clientes, como conteúdo de aplicativos, pacotes de software, atualizações de software, imagens dos sistemas operacionais e imagens de inicialização. Você pode controlar a distribuição do conteúdo usando opções de largura de banda, limitação e agendamento.  

 É importante ter pontos de distribuição suficientes para dar suporte à implantação de sistemas operacionais nos computadores. Também é importante planejar o posicionamento desses pontos de distribuição na hierarquia. Você encontrará a maioria dessas informações em [Gerenciar conteúdo e infraestrutura de conteúdo](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md). No entanto, existem algumas considerações adicionais de planejamento para pontos de distribuição que são específicas para a implantação de sistema operacional.  

###  <a name="BKMK_AdditionalPlanning"></a> Considerações de planejamento adicionais para pontos de distribuição  
 Veja a seguir outros itens adicionais de planejamento a serem considerados para pontos de distribuição:  

-   **Como impedir implantações de sistema operacional indesejadas?**  

     O Configuration Manager não distingue os servidores do site de outros computadores de destino em uma coleção. Se você implantar uma sequência de tarefas necessária em uma coleção que contém um servidor do site, este último executará a sequência de tarefas da mesma maneira que qualquer outro computador na coleção que executa a sequência de tarefas. Verifique se a implantação de sistema operacional usa uma coleção que contém os clientes nos quais você pretende executar a implantação.  

     Você pode gerenciar o comportamento de implantações de sequência de tarefas de alto risco. Uma implantação de alto risco é instalada automaticamente em um cliente e tem o potencial de causar resultados indesejados. Por exemplo, uma sequência de tarefas com a finalidade obrigatória que implanta um sistema operacional. Para reduzir o risco de uma implantação de alto risco indesejada, você pode configurar as configurações de verificação de implantação. Para obter mais informações, consulte [Configurações para gerenciar implantações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

-   **Quantos computadores podem receber uma imagem do sistema operacional ao mesmo tempo de um único ponto de distribuição?**  

     Para estimar quantos pontos de distribuição você precisa, considere a velocidade de processamento e a E/S em disco do ponto de distribuição, a largura de banda disponível na rede e o impacto que o tamanho do pacote de imagem terá sobre esses recursos. Por exemplo, em uma rede Ethernet de 100 megabytes (MB), o número máximo para processar um pacote de imagem de 4 gigabytes (GB) em uma hora é de 11 computadores, se nenhum outro fator de recurso do servidor for levado em conta.  

     `100 Megabits/sec = 12.5 Megabytes/sec = 750 Megabytes/min = 45 Gigabytes/hour = 11 images @ 4GB per image.`  

     Se for necessário implantar um sistema operacional em um número específico de computadores em determinado período, distribua o pacote de imagem a um número apropriado de pontos de distribuição.  

-   **Posso implantar um sistema operacional em um ponto de distribuição?**  

     Você pode implantar um sistema operacional em um ponto de distribuição, mas a imagem do sistema operacional deve ser recebida de um ponto de distribuição diferente.  

###  <a name="BKMK_PXEDistributionPoint"></a> Configurando pontos de distribuição para aceitar solicitações PXE  
 Para implantar sistemas operacionais em clientes do Configuration Manager que fazem solicitações de inicialização PXE, você deve configurar um ou mais pontos de distribuição para aceitar solicitações PXE. Após configurar o ponto de distribuição, ele responderá à solicitação de inicialização PXE e determinará a ação apropriada de implantação a ser tomada.

> [!IMPORTANT]  
>  O[Windows Deployment Services](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDS) deve ser instalado em todos os pontos de distribuição habilitados para PXE.  

 Use o procedimento a seguir para modificar um ponto de distribuição existente para que ele possa aceitar solicitações PXE. Para obter mais informações sobre como configurar um novo ponto de distribuição, veja [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).  

#### <a name="to-modify-an-existing-distribution-point-to-accept-pxe-requests"></a>Para modificar um ponto de distribuição existente para aceitar solicitações PXE  

1.  No console do Configuration Manager, clique em **Administração**, expanda **Visão Geral** e clique em **Pontos de Distribuição**.  

2.  Selecione o ponto de distribuição a configurar, clique na guia **Início** no grupo **Propriedades** e clique em **Propriedades**.  

3.  Na página de propriedades do ponto de distribuição, clique na guia **PXE** . e selecione **Habilitar suporte a PXE para clientes** para habilitar o PXE nesse ponto de distribuição.  

4.  Clique em **Sim** na caixa de diálogo **Examinar Portas Necessárias para PXE** para confirmar que você deseja habilitar PXE. O O Configuration Manager configura automaticamente as portas padrão em um Firewall do Windows. Você deverá configurar manualmente as portas se usar um firewall diferente.  

    > [!NOTE]  
    >  Se o WDS e o DHCP estiverem instalados no mesmo servidor, você deverá configurar o WDS para escutar em uma porta diferente (uma vez que o DHCP escuta na mesma porta). Para obter mais informações, consulte [Considerações sobre quando você tem o WDS e DHCP no mesmo servidor](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDSandDHCP).  

5.  Selecione **Permitir que este ponto de distribuição responda às solicitações PXE de entrada** para habilitar o WDS de modo que ele responda às solicitações de serviço PXE de entrada. Use essa configuração para habilitar ou desabilitar o serviço sem remover a funcionalidade PXE do ponto de distribuição.  

6.  Selecione **Habilitar suporte a computadores desconhecidos** para implantar sistemas operacionais em computadores que não são gerenciados pelo Configuration Manager.  

7.  Selecione **Exigir uma senha quando os computadores usarem PXE**e especifique uma senha para fornecer segurança adicional para implantações PXE.  

8.  In the **Afinidade de Dispositivo de Usuário** , escolha como você deseja que o ponto de distribuição associe usuários ao computador de destino para as implantações PXE.  

    -   Selecione **Não usar afinidade de dispositivo de usuário** para não associar usuários com o computador de destino.  

    -   Selecione **Permitir afinidade de dispositivo de usuário com aprovação manual** para aguardar a aprovação de um usuário administrativo antes dos usuários serem associados ao computador de destino.  

    -   Selecione **Permitir afinidade de dispositivo de usuário com aprovação automática** para associar automaticamente os usuários ao computador de destino sem aguardar a aprovação.  

     Para mais informações, consulte [Associar usuários a um computador de destino](../get-started/associate-users-with-a-destination-computer.md).  

9. especifique se o ponto de distribuição deve responder às solicitações PXE de todas as interfaces de rede ou de interfaces de rede específicas. Se optar por fazer com que o ponto de distribuição responda a interfaces de rede específicas, você deverá fornecer o endereço MAC para cada interface de rede.  

10. Especifique, em segundos, qual é tempo de atraso para o ponto de distribuição antes de responder às solicitações do computador quando vários pontos de distribuição habilitados para PXE são usados.  

11. Clique em **OK** para atualizar as propriedades do ponto de distribuição.  

###  <a name="BKMK_RamDiskTFTP"></a> Personalizar o tamanho do bloco e da janela do RamDisk TFTP nos pontos de distribuição habilitados para PXE  
É possível personalizar o tamanho do bloco e da janela do RamDisk TFTP, e partir do Configuration Manager versão 1606, o tamanho da janela para pontos de distribuição habilitados pelo PXE. Se você tiver personalizado sua rede, isso poderá fazer com que o download da imagem de inicialização falhe com um erro de tempo limite devido ao tamanho muito grande do bloco ou da janela. A personalização do tamanho do bloco e da janela do RamDisk TFTP permite otimizar o tráfego TFTP ao usar o PXE para atender aos seus requisitos de rede específicos.   
Você precisará testar as configurações personalizadas no ambiente para determinar o que é mais eficiente.  

-   **Tamanho do bloco do TFTP**: o tamanho do bloco é o tamanho dos pacotes de dados que são enviados pelo servidor ao cliente que está baixando o arquivo (como discutido em RFC 2347). Um tamanho de bloco maior permite que o servidor envie menos pacotes, para que haja menos atrasos de viagem de ida e volta entre o servidor e o cliente. No entanto, um bloco de tamanho grande leva a pacotes fragmentados, com os quais a maioria das implementações do cliente PXE não é compatível.  

-   **Tamanho da janela do TFTP**: o TFTP exige um pacote ACK (de confirmação) para cada bloco de dados que é enviado. O servidor não enviará o próximo bloco na sequência enquanto não receber o pacote ACK do bloco anterior. As janelas do TFTP são um recurso nos Serviços de Implantação do Windows que permite definir quantos blocos de dados são necessários para preencher uma janela. O servidor envia os blocos de dados um após o outro até que a janela esteja preenchida; em seguida, o cliente envia um pacote ACK. Aumentar o tamanho da janela reduz o número de atrasos da viagem de ida e volta entre o cliente e o servidor, além de diminuir o tempo total que é necessário para baixar uma imagem de inicialização.  


#### <a name="to-modify-the-ramdisk-tftp-window-size"></a>Para modificar o tamanho da janela do RamDisk TFTP  

-   Adicione a seguinte chave do registro nos pontos de distribuição habilitados para PXE para personalizar o tamanho da janela do RamDisk TFTP:  

     **Local**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    Nome: RamDiskTFTPWindowSize  

     **Tipo**: REG_DWORD  

     **Valor**: &lt;tamanho de janela personalizado>  

 O valor padrão é 1 (um bloco de dados preenche a janela)  

#### <a name="to-modify-the-ramdisk-tftp-block-size"></a>Para modificar o tamanho do bloco do RamDisk TFTP  

-   Adicione a seguinte chave do registro nos pontos de distribuição habilitados para PXE para personalizar o tamanho da janela do RamDisk TFTP:  

     **Local**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    Nome: RamDiskTFTPBlockSize  

     **Tipo**: REG_DWORD  

     **Valor**: &lt;tamanho de bloco personalizado>  

 O valor padrão é 4096 (4 k).  


###  <a name="BKMK_DPMulticast"></a> Configurar pontos de distribuição para dar suporte a multicast  
 Multicast é um método de otimização da rede que pode ser usado nos pontos de distribuição quando vários clientes podem baixar a mesma imagem do sistema operacional ao mesmo tempo. Ao usar multicast, vários computadores podem baixar simultaneamente a imagem do sistema operacional, pois ela é difundida via multicast pelo ponto de distribuição, em vez de ter um ponto de distribuição que envia uma cópia dos dados para cada cliente por meio de uma conexão separada. Você deve configurar pelo menos um ponto de distribuição para dar suporte a multicast. Para mais informações, consulte [Usar o multicast para implantar o Windows pela rede](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

 Antes de implantar o sistema operacional, é necessário configurar um ponto de distribuição para oferecer suporte a multicast. Use o procedimento a seguir para modificar um ponto de distribuição existente para oferecer suporte a multicast. Para obter mais informações sobre como configurar um novo ponto de distribuição, consulte [Instalar e configurar pontos de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).

#### <a name="to-enable-multicast-for-a-distribution-point"></a>Para habilitar o multicast para um ponto de distribuição  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Visão Geral**e selecione o nó **Pontos de Distribuição** .  

3.  Selecione o ponto de distribuição que deseja usar para o multicast da imagem do sistema operacional.  

4.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  Selecione a guia **Multicast** e configure as seguintes opções:  

    -   **Habilitar Multicast**: você deve selecionar essa opção para o ponto de distribuição dar suporte a multicast.  

    -   **Conta de conexão multicast**: especifique uma conta para se conectar ao banco de dados do site.  

    -   **Configurações de endereço multicast**: especifique os endereços IP para enviar dados aos computadores de destino. Por padrão, o endereço IP é obtido de um servidor DHCP habilitado para distribuir endereços multicast. Dependendo do ambiente de rede, é possível especificar um intervalo de endereços IP entre 239.0.0.0 e 239.255.255.255.  

        > [!IMPORTANT]  
        >  Esses endereços IP devem ser acessíveis por computadores de destino que solicitam a imagem do sistema operacional. Isso significa que os roteadores e firewalls entre o computador de destino e o servidor do site devem ser configurados para permitir o tráfego multicast.  

    -   **Intervalo de Portas UDP**: especifique o intervalo de portas UDP para enviar os dados aos computadores de destino.  

        > [!IMPORTANT]  
        >  Essas portas devem ser acessíveis por computadores de destino que solicitam a imagem do sistema operacional. Isso significa que os roteadores e firewalls entre o computador de destino e o servidor do site devem ser configurados para permitir o tráfego multicast.  

    -   **Multicast agendado habilitado**: especifique como o Configuration Manager controla quando iniciar a implantação de sistemas operacionais em computadores de destino. Clique em **Habilitar multicast agendado**e selecione as opções a seguir.  

         Na caixa **Atraso de início de sessão**, especifique quantos minutos que o Configuration Manager aguardará antes de responder à primeira solicitação de implantação.  

         Na caixa **Tamanho mínimo da sessão**, especifique quantas solicitações devem ser recebidas antes que o Configuration Manager comece a implantar o sistema operacional.  

    -   **Taxa de transferência**: selecione a taxa de transferência para baixar os dados nos computadores de destino.  

    -   **Máximo de clientes**: especifique o número máximo de computadores de destino que podem baixar o sistema operacional desse ponto de distribuição.  

6.  Clique em **OK**.  

##  <a name="BKMK_StateMigrationPoints"></a> Ponto de migração de estado  
 O ponto de migração de estado armazena dados de estado do usuário, que são capturados em um computador e restaurados em outro. No entanto, ao capturar configurações do usuário para uma implantação de sistema operacional no mesmo computador, como em uma implantação em que você atualiza o sistema operacional no computador de destino, é possível optar por armazenar os dados no mesmo computador usando links físicos ou usar um ponto de migração de estado. Em certas implantações de computador, quando você cria o armazenamento de estado, o Configuration Manager automaticamente cria uma associação entre o armazenamento de estado e o computador de destino. Ao planejar um ponto de migração de estado, considere os fatores a seguir.  

### <a name="user-state-size"></a>Tamanho do estado do usuário  
 O tamanho do estado do usuário afeta diretamente o armazenamento em disco no ponto de migração de estado e o desempenho da rede durante a migração. Considere o tamanho do estado do usuário e o número de computadores a migrar. Considere, ainda, as configurações a serem migradas do computador. Por exemplo, se **Meus Documentos** já tiver sido armazenado em backup em um servidor, talvez não seja preciso migrá-lo como parte da implantação da imagem. Se for possível evitar migrações desnecessárias, o tamanho geral do estado do usuário será menor e diminuirá o impacto que, de outra maneira, haveria sobre o desempenho da rede e sobre o armazenamento em disco no ponto de migração de estado.  

### <a name="user-state-migration-tool"></a>Ferramenta de Migração de Estado do Usuário  
 Para capturar e restaurar o estado do usuário durante a implantação dos sistemas operacionais, use um pacote da	Ferramenta de Migração de Estado do Usuário (USMT) que aponte para os arquivos de origem da USMT. O Configuration Manager cria automaticamente esse pacote no console do Configuration Manager em **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Pacotes**. O Configuration Manager usa a USMT 10.0, que é distribuída no Windows ADK (Kit de Avaliação e Implantação do Windows) para capturar o estado do usuário de um sistema operacional e restaurá-lo em outro sistema operacional.  

 Para obter uma descrição dos diferentes cenários de migração para a USMT 10.0, veja [Cenários comuns de migração](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx).  

### <a name="retention-policy"></a>Política de retenção  
 Ao configurar o ponto de migração de estado, você pode especificar o tempo pelo qual serão mantidos os dados de estado do usuário nele armazenados. O tempo pelo qual serão mantidos os dados no ponto de migração de estado depende de duas considerações:  

-   O efeito que os dados armazenados têm sobre o armazenamento em disco.  

-   A possível necessidade de se manter os dados por certo período, caso uma nova migração seja necessária.  

 A migração de estado ocorre em duas fases: captura e restauração dos dados. Ao capturar dados, os dados de estado do usuário são coletados e salvos no ponto de migração de estado. Na restauração, os dados de estado do usuário são recuperados a partir do ponto de migração de estado, gravados no computador de destino e, então, a etapa de sequência de tarefas **Liberar Armazenamento de Estado** libera os dados armazenados. Quando os dados são liberados, o timer de retenção se inicia. Se você selecionar a opção de excluir os dados migrados imediatamente, os dados de estado do usuário serão excluídos assim que forem liberados. Se você selecionar a opção de manter os dados por determinado tempo, após a liberação, os dados serão excluídos quando decorrer esse período. Provavelmente, quanto mais longo for o período de retenção definido, mais espaço em disco será necessário.  

### <a name="select-drive-to-store-user-state-migration-data"></a>Selecionar a unidade para armazenar os dados de migração de estado do usuário  
 Ao configurar o ponto de migração de estado, você deve especificar a unidade, no servidor, na qual devem ser armazenados os dados da migração de estado do usuário. Selecione uma unidade na lista fixa de unidades. Algumas unidades, porém, podem não ser graváveis, como a unidade de CD ou uma unidade de compartilhamento não relacionada à rede. Além disso, algumas letras de unidade podem não estar mapeadas para as unidades no computador. Especifique uma unidade gravável e compartilhada ao configurar o ponto de migração de estado.  

### <a name="configure-a-state-migration-point"></a>Configurar um ponto de migração de estado  
 É possível usar os seguintes métodos para configurar um ponto de migração de estado para armazenar os dados de estado do usuário:  

-   Use o **Assistente para Criar Servidor do Sistema de Site** para criar um novo servidor do sistema de site para o ponto de migração de estado.  

-   Use o **Assistente para Adicionar Funções do Sistema de Site** para adicionar um ponto de migração de estado a um servidor existente.  

 Ao usar esses assistentes, você é solicitado a fornecer as seguintes informações do ponto de migração de estado:  

-   As pastas para armazenar os dados de estado do usuário.  

-   O número máximo de clientes que podem armazenar dados no ponto de migração de estado.  

-   O espaço livre mínimo para o ponto de migração de estado armazenar dados de estado do usuário.  

-   A política de exclusão para a função. Você pode especificar se os dados de estado do usuário serão excluídos imediatamente depois de serem restaurados em um computador ou após um número específico de dias depois que os dados do usuário são restaurados em um computador.  

-   Se você deseja que o ponto de migração de estado responda apenas às solicitações para restaurar dados de estado do usuário. Ao habilitar essa opção, você não pode usar o ponto de migração de estado para armazenar dados de estado do usuário.  

 Para obter as etapas para instalar uma função do sistema de sites, consulte [Adicionar funções do sistema de sites](../../core/servers/deploy/configure/add-site-system-roles.md).  
