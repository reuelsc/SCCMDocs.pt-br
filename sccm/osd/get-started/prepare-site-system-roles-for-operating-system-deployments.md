---
title: Preparar as funções do sistema de sites para implantação de sistema operacional
titleSuffix: Configuration Manager
description: Configurar as funções de sistema de sites antes de implantar sistemas operacionais no Configuration Manager
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cbfa49dddb19d588a3fe16f042b50af590cf39e8
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383721"
---
# <a name="prepare-site-system-roles-for-os-deployments-with-configuration-manager"></a>Preparar funções do sistema de site para implantações de sistema operacional com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para implantar sistemas operacionais no Configuration Manager, primeiro prepare as seguintes funções do sistema de sites que exigem considerações e configurações específicas.



##  <a name="BKMK_DistributionPoints"></a> Pontos de distribuição  

A função do sistema de sites do ponto de distribuição hospeda os arquivos de origem para download pelos clientes. Esse conteúdo destina-se a aplicativos, atualizações de software, imagens do sistema operacional, imagens de inicialização e pacotes de driver. Controle a distribuição de conteúdo usando opções de largura de banda, limitação e agendamento.  

É importante ter pontos de distribuição suficientes para dar suporte à implantação de sistemas operacionais nos computadores. Também é importante planejar o posicionamento desses pontos de distribuição na hierarquia. Para mais informações, confira [Manage content and content infrastructure](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure) (Gerenciar o conteúdo e a infraestrutura de conteúdo). Este artigo inclui algumas considerações sobre planejamento adicionais para pontos de distribuição específicas à implantação de sistema operacional.  


###  <a name="BKMK_AdditionalPlanning"></a> Considerações de planejamento adicionais para pontos de distribuição  

Os seguintes itens são itens de planejamento adicionais a serem considerados para os pontos de distribuição:  

#### <a name="how-can-i-prevent-unwanted-os-deployments"></a>Como impedir implantações de sistema operacional indesejadas?  
O Configuration Manager não distingue os servidores do site de outros computadores de destino em uma coleção. Se você implantar uma sequência de tarefas obrigatória em uma coleção que inclui um servidor do site, ele executará a sequência de tarefas da mesma maneira como qualquer outro computador na coleção. Garanta que a implantação de sistema operacional usa uma coleção que inclui os clientes pretendidos.  

Gerencie o comportamento de implantações de sequência de tarefas de alto risco. Uma implantação de alto risco é instalada automaticamente em um cliente e tem o potencial de causar resultados indesejados. Por exemplo, uma sequência de tarefas com a finalidade obrigatória que implanta um sistema operacional. Para reduzir o risco de uma implantação de alto risco indesejada, defina as configurações de verificação da implantação. Para obter mais informações, consulte [Configurações para gerenciar implantações de alto risco](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments).  

#### <a name="how-many-computers-can-receive-an-os-image-at-one-time-from-a-single-distribution-point"></a>Quantos computadores podem receber uma imagem de sistema operacional ao mesmo tempo de um único ponto de distribuição?  
Para estimar de quantos pontos de distribuição você precisa, considere as seguintes variáveis:  
- A velocidade de processamento do ponto de distribuição
- A velocidade de disco do ponto de distribuição
- A largura de banda disponível na rede
- O tamanho do pacote de imagem   
  
Por exemplo, se você não considerar outros fatores de recurso do servidor, o número máximo de computadores que poderão processar um pacote de imagem de 4 GB em uma hora em uma rede Ethernet de 100 megabits/s será de 11 computadores.  

`100 megabits/sec = 12.5 megabytes/sec = 750 megabytes/min = 45 gigabytes/hour = 11 images @ 4 GB per image`  

Se for necessário implantar um sistema operacional em um número específico de computadores em determinado período, distribua a imagem para um número apropriado de pontos de distribuição.  

#### <a name="can-i-deploy-an-os-to-a-distribution-point"></a>Posso implantar um sistema operacional em um ponto de distribuição?  
Você pode implantar um sistema operacional em um ponto de distribuição, mas a imagem do sistema operacional precisa ser recebida de um ponto de distribuição diferente.  


###  <a name="BKMK_PXEDistributionPoint"></a> Configurando pontos de distribuição para aceitar solicitações PXE  

Para implantar sistemas operacionais em clientes do Configuration Manager que fazem solicitações de inicialização PXE, configure um ou mais pontos de distribuição para aceitar solicitações PXE. Depois de configurar o ponto de distribuição, ele responde às solicitações de inicialização PXE e determina a ação de implantação apropriada a ser tomada. Para mais informações, consulte [Instalar ou modificar um ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  


###  <a name="BKMK_RamDiskTFTP"></a> Personalizar os tamanhos do bloco e da janela do RamDisk TFTP nos pontos de distribuição habilitados para PXE  

Personalize o tamanho do bloco e da janela do RamDisk TFTP nos pontos de distribuição habilitados para PXE. Se você personalizou a rede, um tamanho grande de bloco ou de janela pode fazer com que o download da imagem de inicialização falhe com um erro de tempo limite. As personalizações de tamanho do bloco e da janela do RamDisk TFTP permitem otimizar o tráfego TFTP ao usar o PXE para atender aos seus requisitos de rede específicos. Para determinar qual configuração é a mais eficiente, teste as configurações personalizadas no ambiente.  

-   **Tamanho do bloco do TFTP**: o tamanho do bloco é o tamanho dos pacotes de dados enviados pelo servidor ao cliente que está baixando o arquivo. Um tamanho de bloco maior permite que o servidor envie menos pacotes, para que haja menos atrasos de viagem de ida e volta entre o servidor e o cliente. No entanto, um tamanho grande de bloco leva a pacotes fragmentados, com os quais a maioria das implementações de cliente PXE não é compatível.  

-   **Tamanho da janela do TFTP**: o TFTP exige um pacote ACK (de confirmação) para cada bloco de dados que é enviado. O servidor não enviará o próximo bloco na sequência enquanto não receber o pacote ACK do bloco anterior. As janelas do TFTP permitem definir a quantidade de blocos de dados necessários para preencher uma janela. O servidor envia os blocos de dados um após o outro até que a janela esteja preenchida; em seguida, o cliente envia um pacote ACK. Se você aumentar o tamanho dessa janela, ela reduzirá o número de atrasos da viagem de ida e volta entre o cliente e o servidor, além de diminuir o tempo total necessário para baixar uma imagem de inicialização.  
  

#### <a name="modify-the-ramdisk-tftp-window-size"></a>Modificar o tamanho da janela do RamDisk TFTP  
Para personalizar o tamanho da janela do RamDisk TFTP, adicione a seguinte chave do Registro nos pontos de distribuição habilitados para PXE:  

- **Local**: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **Nome**: RamDiskTFTPWindowSize  
- **Tipo**: REG_DWORD  
- **Valor**: (tamanho da janela personalizado)  
    - O valor padrão é **1** (um bloco de dados preenche a janela).  

#### <a name="modify-the-ramdisk-tftp-block-size"></a>Modificar o tamanho do bloco do RamDisk TFTP  
Para personalizar o tamanho da janela do RamDisk TFTP, adicione a seguinte chave do Registro nos pontos de distribuição habilitados para PXE:  

- **Local**: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **Nome**: RamDiskTFTPBlockSize  
- **Tipo**: REG_DWORD  
- **Valor**: (tamanho do bloco personalizado)  
    - O valor padrão é **4096**.  

> [!Note]  
> Os Serviços de Implantação do Windows e o serviço de respondente PXE do Configuration Manager dão suporte a essas configurações TFTP.  


###  <a name="BKMK_DPMulticast"></a> Configurar pontos de distribuição para dar suporte a multicast  

Multicast é um método de otimização de rede. Use-o nos pontos de distribuição quando vários clientes possam baixar a mesma imagem do sistema operacional ao mesmo tempo. Quando você usa o multicast, vários computadores podem baixar simultaneamente a imagem do sistema operacional como se fosse multicast pelo ponto de distribuição. Sem o multicast, o ponto de distribuição envia uma cópia dos dados para cada cliente por uma conexão separada. Para mais informações, consulte [Usar o multicast para implantar o Windows pela rede](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network).  

Antes de implantar o sistema operacional, configure um ponto de distribuição para dar suporte a multicast. Para obter mais informações, consulte [Instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-multicast).



##  <a name="BKMK_StateMigrationPoints"></a> Ponto de migração de estado  

O ponto de migração de estado armazena os dados de estado do usuário capturados pela USMT em um computador e, em seguida, restaurados em outro computador. No entanto, ao capturar as configurações do usuário para uma implantação de sistema operacional no mesmo computador, como em uma implantação em que você atualiza o Windows no computador de destino, você pode escolher se deseja armazenar os dados no mesmo computador usando links físicos ou usar um ponto de migração de estado. Em certas implantações de computador, quando você cria o armazenamento de estado, o Configuration Manager automaticamente cria uma associação entre o armazenamento de estado e o computador de destino. Ao planejar um ponto de migração de estado, considere os seguintes fatores:    


### <a name="user-state-size"></a>Tamanho do estado do usuário  

O tamanho do estado do usuário afeta diretamente o armazenamento em disco no ponto de migração de estado e o desempenho da rede durante a migração. Considere o tamanho do estado do usuário e o número de computadores a migrar. Considere, ainda, as configurações a serem migradas do computador. Por exemplo, se a pasta **Meus Documentos** já tiver sido copiada em backup em um servidor, talvez não seja preciso migrá-la como parte da implantação da imagem. Evitar migrações desnecessárias mantém o tamanho geral do estado do usuário menor e diminui o impacto que ele, de outra maneira, terá sobre o desempenho da rede e o armazenamento em disco no ponto de migração de estado.  


### <a name="user-state-migration-tool"></a>Ferramenta de Migração de Estado do Usuário  

Para capturar e restaurar o estado do usuário durante a implantação dos sistemas operacionais, use um pacote da USMT (Ferramenta de Migração do Usuário) que aponta para os arquivos de origem da USMT. O Configuration Manager cria automaticamente esse pacote no console do Configuration Manager em **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Pacotes**. O Configuration Manager usa a USMT 10 para capturar o estado do usuário de um sistema operacional e, em seguida, restaurá-lo em outro. O Windows ADK (Kit de Avaliação e Implantação) para Windows 10 inclui a USMT 10.

Para obter uma descrição dos diferentes cenários de migração para a USMT 10, consulte [Cenários comuns de migração](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios) na documentação do Windows.  


### <a name="retention-policy"></a>Política de retenção  

Ao configurar o ponto de migração de estado, especifique o tempo durante o qual serão mantidos os dados de estado do usuário armazenados nele. O tempo pelo qual serão mantidos os dados no ponto de migração de estado depende de duas considerações:  

-   O efeito que os dados armazenados têm sobre o armazenamento em disco.  

-   A possível necessidade de se manter os dados por certo período, caso uma nova migração seja necessária.  
  
  
A migração de estado ocorre em duas fases: captura e restauração dos dados. Ao capturar dados, os dados de estado do usuário são coletados e salvos no ponto de migração de estado. Na restauração, os dados de estado do usuário são recuperados a partir do ponto de migração de estado, gravados no computador de destino e, então, a etapa de sequência de tarefas **Liberar Armazenamento de Estado** libera os dados armazenados. Quando os dados são liberados, o timer de retenção se inicia. Se você selecionar a opção para excluir os dados migrados imediatamente, os dados de estado do usuário serão excluídos assim que forem liberados. Se você selecionar a opção de manter os dados por determinado tempo, após a liberação, os dados serão excluídos quando decorrer esse período. Quanto mais longo for o período de retenção definido, provavelmente, mais espaço em disco será necessário.  


### <a name="select-drive-to-store-user-state-migration-data"></a>Selecionar a unidade para armazenar os dados de migração de estado do usuário  

Ao configurar o ponto de migração de estado, especifique a unidade, no servidor, na qual devem ser armazenados os dados da migração de estado do usuário. Selecione uma unidade na lista fixa de unidades. Algumas unidades, porém, podem não ser graváveis, como a unidade de CD ou uma unidade de compartilhamento não relacionada à rede. Além disso, algumas letras da unidade podem não ser mapeadas para nenhuma unidade no computador. Especifique uma unidade gravável e compartilhada ao configurar o ponto de migração de estado.  


### <a name="configure-a-state-migration-point"></a>Configurar um ponto de migração de estado  

Use os métodos a seguir para configurar um ponto de migração de estado para armazenar os dados de estado do usuário:  

-   Use o **Assistente para Criar Servidor do Sistema de Site** para criar um novo servidor do sistema de site para o ponto de migração de estado.  

-   Use o **Assistente para Adicionar Funções do Sistema de Site** para adicionar um ponto de migração de estado a um servidor existente.  

Ao usar esses assistentes, você deve fornecer as seguintes informações para o ponto de migração de estado:  

-   As pastas para armazenar os dados de estado do usuário.  

-   O número máximo de clientes que podem armazenar dados no ponto de migração de estado.  

-   O espaço livre mínimo para o ponto de migração de estado armazenar dados de estado do usuário.  

-   A política de exclusão para a função. Especifique se os dados de estado do usuário serão excluídos imediatamente depois de serem restaurados em um computador ou após um número específico de dias depois que os dados do usuário forem restaurados em um computador.  

-   Se você deseja que o ponto de migração de estado responda apenas às solicitações para restaurar dados de estado do usuário. Ao habilitar essa opção, você não pode usar o ponto de migração de estado para armazenar dados de estado do usuário.  

Para obter as etapas para instalar uma função do sistema de sites, consulte [Adicionar funções do sistema de sites](/sccm/core/servers/deploy/configure/add-site-system-roles).  
