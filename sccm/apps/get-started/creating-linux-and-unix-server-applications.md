---
title: Criar aplicativos de servidores Linux e UNIX | Microsoft Docs
description: "Veja quais considerações você deverá levar em conta ao criar e implantar aplicativos para dispositivos Linux e Unix."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 79cd131a-1a24-4751-87c8-7f275e45d847
caps.latest.revision: 7
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: b599a58f25a868c638b7ee00cefff80b2f71244e
ms.openlocfilehash: f4373c888434aa6cd22e5f9b871e172cc50a7d30


---
# <a name="create-linux-and-unix-server-applications-with-system-center-configuration-manager"></a>Criar aplicativos de servidor Linux e UNIX com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Leve em conta as seguintes considerações ao criar e implantar aplicativos para computadores que executam Linux e UNIX.  

## <a name="general-considerations"></a>Considerações gerais  
 O cliente do Configuration Manager para Linux e UNIX dá suporte a **implantações de software que usam pacotes e programas**. Não é possível implantar os aplicativos do Configuration Manager em computadores que executam Linux e UNIX.  

 Os recursos de implantação de software Linux e UNIX incluem:  

-   Instalação de software para servidores Linux e UNIX, incluindo o seguinte:  

    -   Nova implantação de software  

    -   Atualizações de software para os programas que já estão em um computador  

    -   Patches do sistema operacional  

-   Comandos do Linux e UNIX nativos e scripts localizados nos servidores Linux e UNIX  

-   Implantações que são limitadas aos sistemas operacionais que você especificar ao selecionar a opção do programa **Somente nas plataformas cliente especificadas**

-   Janelas de manutenção para controlar quando o software é instalado

-   Mensagens de status da implantação para monitorar as implantações  

-   A opção para o cliente para restringir o uso da rede durante o download de software de um ponto de distribuição  

### <a name="differences-between-deploying-to-linux-and-unix-computers-and-deploying-to-windows-devices"></a>Diferenças entre implantar em computadores Linux e UNIX e implantar em dispositivos Windows
As principais diferenças entre implantar pacotes e programas em computadores Linux e UNIX e implantar pacotes e programas em dispositivos Windows são as seguintes:  

|Configuração|Detalhes|  
|-------------------|-------------|  
|Usar somente configurações relacionadas a computadores, não as relacionadas a usuários.|O cliente do Configuration Manager para Linux e UNIX não dá suporte a configurações destinadas a usuários.|  
|Configurar os programas para baixar software do ponto de distribuição e executar os programas do cache local do cliente.|O cliente do Configuration Manager para Linux e UNIX não dá suporte à execução do software no ponto de distribuição. Em vez disso, é necessário configurar para baixar o software no cliente e depois instalar.<br /><br /> Por padrão, após o cliente para Linux e UNIX instalar o software, esse software é excluído do cache do cliente. No entanto, os pacotes configurados com **Manter o conteúdo no cache do cliente** não são excluídos do cliente e permanecem no cache do cliente após a instalação do software.<br /><br /> O cliente para Linux e UNIX não dá suporte a configurações do cache do cliente, e o tamanho máximo deste cache é limitado somente pelo espaço livre em disco no computador cliente.|  
|Configurar a Conta de Acesso à Rede para acesso ao ponto de distribuição|Os computadores Linux e UNIX são projetados para serem computadores de grupo de trabalho. Para acessar os pacotes do ponto de distribuição no domínio do servidor do site do Configuration Manager, é necessário configurar a Conta de Acesso à Rede para o site. É necessário especificar essa conta como uma propriedade do componente de distribuição do software, além de configurá-la antes de implantar o software.<br /><br /> Você pode configurar várias Contas de Acesso à Rede em cada site. Os clientes do Linux e UNIX podem usar cada uma das contas configuradas como uma Conta de Acesso à Rede.<br /><br /> Para obter mais informações, consulte [Site components for System Center Configuration Manager](../../core/servers/deploy/configure/site-components.md).|  

 Você pode implantar os pacotes e programas em coleções que contêm somente clientes Linux ou UNIX, ou implantá-los em coleções que contêm tipos de clientes mistos, como a **Coleção Todos os Sistemas**. No entanto, clientes não Linux ou não UNIX não instalarão o software ou relatarão a falha.  

 Quando o cliente do Configuration Manager para Linux e UNIX recebe e executa uma implantação, ele gera mensagens de status. É possível exibir essas mensagens de status no console do Configuration Manager ou usando os relatórios para monitorar os status da implantação.  

 Para obter informações sobre como usar pacotes e programas, consulte [Packages and programs (Pacotes e programas)](../../apps/deploy-use/packages-and-programs.md).  

##  <a name="configure-packages-programs-and-deployments-for-linux-and-unix-servers"></a>Configurar pacotes, programas e implantações em servidores Linux e UNIX  
 É possível criar e implantar pacotes e programas usando as opções padrão disponíveis no console do Configuration Manager. O cliente não necessita de configurações exclusivas.  

 Use as informações nas seções a seguir para configurar pacotes e programas, bem como implantações.  

### <a name="packages-and-programs"></a>Pacotes e programas  
 Para criar um pacote ou programa para um servidor Linux ou UNIX, use o **Assistente para Criar Pacote e Programa**, no console do Configuration Manager. O cliente para Linux e UNIX oferece suporte à maioria das configurações de pacote e programa. No entanto, não há suporte para várias configurações. Quando você cria ou configura pacotes e programas, considere o seguinte:  

-   Inclua os tipos de arquivo com suporte nos computadores de destino.  

-   Defina as linhas de comando apropriadas para uso no computador de destino.  

-   Lembre-se que não há suporte para configurações que interagem com usuários.  

A tabela a seguir lista as propriedades de pacotes e programas sem suporte:  

|Propriedade de pacotes e de programas|Comportamento|Mais informações|  
|----------------------------------|--------------|----------------------|  
|Configurações de compartilhamento de pacote:<br /><br /> – Todas as opções|Um erro é gerado e ocorre falha na instalação do software|O cliente não oferece suporte a essa configuração. Em vez disso, o cliente deve baixar o software usando o HTTP ou HTTPS e executar a linha de comando de seu cache local.|  
|Configurações de atualização do pacote:<br /><br /> – Desconectar usuários dos pontos de distribuição|As configurações são ignoradas|O cliente não oferece suporte a essa configuração.|  
|Configurações de implantação do sistema operacional:<br /><br /> – Todas as opções|As configurações são ignoradas|O cliente não oferece suporte a essa configuração.|  
|Relatórios:<br /><br /> – Usar propriedades do pacote para correspondência de status MIF<br /><br /> – Usar esses campos para correspondência de status MIF|As configurações são ignoradas|O cliente não oferece suporte ao uso de status de arquivos MIF.|  
|**Executar**:<br /><br /> – Todas as opções|As configurações são ignoradas|O cliente sempre executa pacotes sem interface do usuário.<br /><br /> O cliente ignora todas as opções de configuração para Executar.|  
|Após a execução:<br /><br />– O Configuration Manager reinicia o computador<br /><br /> – O programa controla a reinicialização<br /><br /> – O Configuration Manager faz logoff do usuário|Um erro é gerado e ocorre falha na instalação do software|Não há suporte para a configuração de reinicialização do sistema e para as configurações específicas do usuário.<br /><br /> Quando qualquer configuração que não seja **Nenhuma ação é necessária** estiver em uso, o cliente gerará um erro e continuará a instalação do software, sem ações efetuadas.|  
|O programa pode ser executado:<br /><br /> – Somente quando um usuário está conectado|Um erro é gerado e ocorre falha na instalação do software|Não há suporte para as configurações específicas do usuário.<br /><br /> Quando essa opção estiver configurada, o cliente gerará um erro e ocorrerá falha na instalação do software.<br /><br /> As outras opções são ignoradas e a instalação do software continua.|  
|Modo de execução:<br /><br /> – Executar com direitos de usuário|As configurações são ignoradas|Não há suporte para as configurações específicas do usuário.<br /><br /> No entanto, o cliente oferece suporte a configuração em execução com direitos administrativos.<br /><br /> Ao especificar **Executar com direitos administrativos**, o cliente do Configuration Manager usa suas credenciais raiz.<br /><br /> Essa configuração não gera erro ou entrada de log. Em vez disso, a instalação de software falha quando o cliente gera um erro para a configuração de pré-requisitos de **O programa pode ser executado** = **Somente quando um usuário estiver conectado**.|  
|Permitir que os usuários exibam e interajam com o programa de instalação|As configurações são ignoradas|Não há suporte para as configurações específicas do usuário.<br /><br /> Essa configuração é ignorada e a instalação do software continua.|  
|Modo de unidade:<br /><br /> – Todas as opções|As configurações são ignoradas|Não há suporte para essa configuração porque o conteúdo é sempre baixado no cliente e executado localmente.|  
|Executar outro programa primeiro|Um erro é gerado e ocorre falha na instalação do software|Não há suporte para a instalação do programa recursivo.<br /><br /> Quando um programa está configurado para executar outro programa primeiro, a instalação do software falha e a instalação do outro programa não é iniciada.|  
|Quando este programa estiver atribuído a um computador:<br /><br /> – Executar uma vez a cada usuário que fizer logon|As configurações são ignoradas|Não há suporte para as configurações específicas do usuário.<br /><br /> No entanto, o cliente oferece suporte à configuração executar uma vez para o computador.<br /><br /> Essa configuração não gera erro ou entrada de log porque o erro e a entrada de log já são criados para a configuração de pré-requisitos do **O programa pode ser executado** = **Somente quando um usuário tiver efetuado logon**.|  
|Suprimir notificações do programa|As configurações são ignoradas|O cliente não implementa uma interface do usuário.<br /><br /> Quando essa configuração é selecionada, ela será ignorada e a instalação do software continua.|  
|Desabilitar este programa em computadores nos quais ele estiver implantado|As configurações são ignoradas|Não há suporte para essa configuração e ela não afeta a instalação do software.|  
|Permitir que este programa seja instalado da sequência de tarefas de Pacote de Instalação sem ser implantado||O cliente não oferece suporte a sequências de tarefas.<br /><br /> Não há suporte para essa configuração e ela não afeta a instalação do software.|  
|Windows Installer:<br /><br /> – Todas as opções|As configurações são ignoradas|O cliente não oferece suporte para arquivos ou configurações do Windows Installer.|  
|Modo de Manutenção do OpsMgr:<br /><br /> – Todas as opções|As configurações são ignoradas|O cliente não oferece suporte a essa configuração.|  

### <a name="deploy-software-to-a-linux-or-unix-server"></a>Implantar o software em um servidor Linux ou UNIX
 Para implantar softwares em um servidor Linux ou UNIX usando um pacote ou programa, é possível usar o **Assistente de Implantação de Software**, no console do Configuration Manager. Há suporte para a maioria das definições de implantação pelo cliente para Linux e UNIX. No entanto, não há suporte para várias configurações. Ao implantar softwares, considere o seguinte:  

-   É necessário provisionar o pacote para ao menos um ponto de distribuição que esteja associado a um grupo de limites configurado para local de conteúdo.  

-   O cliente para Linux e UNIX que recebe essa implantação deve ser capaz de acessar esse ponto de distribuição de seu local de rede.  

-   O cliente para Linux e UNIX baixa o pacote do ponto de distribuição e executa o programa no computador local.  

-   O cliente para Linux e UNIX não pode baixar pacotes de pastas compartilhadas. Ele baixa pacotes de pontos de distribuição habilitados para IIS que oferecem suporte para HTTP ou HTTPS.  

 A tabela a seguir lista as propriedades para implantações que não têm suporte:  

|Propriedade de implantação|Comportamento|Mais informações|  
|-------------------------|--------------|----------------------|  
|Configurações de implantação – finalidade:<br /><br /> – Disponível<br /><br /> – Necessária|As configurações são ignoradas|Não há suporte para as configurações específicas do usuário.<br /><br /> No entanto, o cliente oferece suporte à configuração **Necessária**, o que impõe o horário de instalação agendado, mas não oferece suporte à instalação manual antes do horário agendado.|  
|Enviar pacotes de ativação|As configurações são ignoradas|O cliente não oferece suporte a essa configuração.|  
|Agendamento de atribuição:<br /><br /> – logon<br /><br /> – logoff|Um erro é gerado e ocorre falha na instalação do software|Não há suporte para as configurações específicas do usuário.<br /><br /> No entanto, o cliente oferece suporte à configuração **O mais breve possível**.|  
|Configurações de notificação:<br /><br /> – Permitir que os usuários executem o programa de forma independente das atribuições|As configurações são ignoradas|O cliente não implementa uma interface do usuário.|  
|Quando o tempo de atribuição agendada for atingido, permita que esta atividade seja realizada fora da janela de manutenção:<br /><br /> – Reinicialização do sistema (se necessário para conclusão da instalação)|Um erro é gerado|O cliente não oferece suporte à reinicialização do sistema.|  
|Opção de implantação para redes locais rápidas:<br /><br /> – Executar programa do ponto de distribuição|Um erro é gerado e ocorre falha na instalação do software|O cliente não pode executar o software do ponto de distribuição; em vez disso, deve baixar o programa para poder executá-lo.|  
|Opção de implantação para limite de rede lento e não confiável ou um local de origem de fallback para o conteúdo:<br /><br /> – Permitir que os clientes compartilhem conteúdo com outros clientes na mesma sub-rede|As configurações são ignoradas|O cliente não dá suporte ao compartilhamento de conteúdo entre pares.|  

 Para obter mais informações sobre o local do conteúdo, consulte [Manage content and content infrastructure for System Center Configuration Manager (Gerenciar conteúdo e infraestrutura de conteúdo do System Center Configuration Manager)](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 Para obter mais informações sobre como criar uma implantação, consulte [Deploy applications (Implantar aplicativos)](../../apps/deploy-use/deploy-applications.md).  

##  <a name="manage-network-bandwidth-for-software-downloads-from-distribution-points"></a>Gerenciar largura de banda de rede para downloads de software dos pontos de distribuição  
 O cliente Linux e UNIX dá suporte para os controles de largura de banda de rede ao baixar software de um ponto de distribuição.  

 O cliente usa as configurações BITS (Serviço de Transferência Inteligente em Segundo Plano) como definições do cliente no Configuration Manager, mas não implementa o BITS. Em vez disso, para limitar o uso da largura de banda de rede, o cliente controla o tamanho da parte da solicitação HTTP e o atraso entre partes do download de software.  

 Para configurar um cliente que usa os controles de largura de banda de rede, configure as definições do cliente em **Transferência Inteligente em Segundo Plano** e aplique as definições ao computador cliente. Para usar os controles de largura de banda, o cliente deve receber as definições de cliente em **Transferência Inteligente em Segundo Plano** com as seguintes definições configuradas como **Sim**:  

-   **Limitar a largura de banda de rede máxima para transferências em segundo plano do BITS**  

 O cliente oferece suporte às seguintes configurações de Transferência Inteligente em Segundo Plano:  

    -   **Hora de início do período de limitação**  

    -   **Hora de término do período de limitação**  

    -   **Taxa de transferência máxima durante o período de limitação (Kbps)**  

    -   **Taxa de transferência máxima durante o período de limitação (Kbps)**  

As seguintes configurações de Transferência Inteligente em Segundo Plano não possuem suporte e são ignoradas pelo cliente do Linux e UNIX:  

-   **Permitir downloads de BITS fora do período de limitação**  

 Se o download de software para o cliente de um ponto de distribuição for interrompido, o cliente do Linux e UNIX não retomará o download. Em vez disso, ele reiniciará o download do pacote de software inteiro.  

##  <a name="configure-operations-for-software-deployments"></a>Configurar as operações para implantações de software  
 De maneira semelhante ao cliente Windows, o cliente do Configuration Manager para Linux e UNIX descobre novas implantações de software ao fazer a busca e a verificação de novas políticas. A frequência com que o cliente verifica novas políticas depende das configurações do cliente. É possível configurar as janelas de manutenção para controlar quando ocorrem implantações de software.  

 É possível configurar as implantações de software em servidores Linux e UNIX usando as propriedades de pacote, do programa e da implantação.  

 Quando o cliente recebe a política de uma implantação, ele envia uma mensagem de status. Ele também envia mensagens de status quando ele inicia a instalação do software ou quando a instalação termina ou falha.  

 Os programas para implantações de software são executados com as credenciais raiz com as quais o cliente do Configuration Manager para Linux e UNIX é executado. O código de saída do comando dos programas é usado para determinar o êxito ou a falha. O código de saída 0 (zero) é tratado como êxito. Além disso, o **stdout** (fluxo de saídas padrão) e o **stderr** (fluxo de erros padrão) são copiados no arquivo de log quando o nível de log está definido como INFO ou TRACE.  

> [!TIP]  
>  Se o software que você deseja implantar estiver localizado em um compartilhamento de NFS (Network File System) que o servidor Linux ou UNIX poderá acessar, não é necessário usar um ponto de distribuição para baixar o pacote. Em vez disso, ao criar o pacote, não marque a caixa de seleção **Este pacote contém arquivos de origem**. Ao configurar o programa, especifique a linha de comando apropriada para acessar diretamente o pacote no ponto de montagem do NFS.  



<!--HONumber=Dec16_HO3-->


