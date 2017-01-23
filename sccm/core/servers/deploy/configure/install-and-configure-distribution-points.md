---
title: "Gerenciar pontos de distribuição | Microsoft Docs"
description: "Hospede o conteúdo (arquivos e software) que você implantar para usuários e dispositivos usando pontos de distribuição. Veja como instalar e configurá-los."
ms.custom: na
ms.date: 1/9/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: cae118d2f28eea3bc47e344ca6f2ba8192f031c2
ms.openlocfilehash: 160c3c94c822bc78e2d61b7a51d130b47f4c204e

---
# <a name="install-and-configure-distribution-points-for-system-center-configuration-manager"></a>Instalar e configurar pontos de distribuição para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Instale pontos de distribuição do System Center Configuration Manager para hospedar o conteúdo (arquivos e software) que você implantar em dispositivos e usuários. Também é possível criar grupos de pontos de distribuição que simplificam como você gerencia pontos de distribuição e como distribui conteúdo para pontos de distribuição.  

 Quando **instala um novo ponto de distribuição** (usando o Assistente de Instalação) ou **gerencia as propriedades de um ponto de distribuição existente** (editando as propriedades dos pontos de distribuição), você pode definir a maioria das configurações dos ponto de distribuição. No entanto, há algumas configurações que só estão disponíveis ao instalar ou editar, mas não ambos:  

-   **Configurações que estão disponíveis somente ao instalar um ponto de distribuição:**  

    -   Permitir que o Gerenciador de Configurações instale o IIS no computador do ponto de distribuição  

    -   Definir configurações de espaço da unidade para o ponto de distribuição  

-   **Etapas de configuração que estão disponíveis somente ao editar as propriedades de um ponto de distribuição:**  

    -   Gerenciar relacionamentos de grupo de pontos de distribuição  

    -   Exibir o conteúdo implantado no ponto de distribuição  

    -   Configurar limites de taxa de transferência de dados para os pontos de distribuição  

    -   Configurar agendamentos para transferências de dados para os pontos de distribuição  

##  <a name="a-namebkmkinstalla-install-a-distribution-point"></a><a name="bkmk_install"></a> Instalar um ponto de distribuição  
 É necessário designar um servidor do sistema de site como ponto de distribuição para que o conteúdo possa ser disponibilizado para computadores cliente. Você pode adicionar a função de site do ponto de distribuição a um novo servidor do sistema de site ou adicionar a nova função de site a um servidor do sistema de site existente.  

 Quando instala um novo ponto de distribuição, você usa um assistente de instalação que o orienta quanto às configurações disponíveis. Antes de começar, considere o seguinte:  

-   É necessário ter as seguintes permissões de segurança para criar e configurar o ponto de distribuição:  

    -   **Ler** para o objeto **Ponto de Distribuição**  

    -   **Copiar para o Ponto de Distribuição** para o objeto **Ponto de Distribuição**  

    -   **Modificar** para o objeto **Site**  

    -   **Gerenciar Certificados para Implantação do Sistema Operacional** para o objeto **Site**  

-   O IIS deve estar instalado no servidor que hospedará o ponto de distribuição. Quando você instala a função de sistema de sites, o Configuration Manager pode instalar e configurar o IIS para você.  

Use os procedimentos básicos a seguir para instalar ou modificar um ponto de distribuição e consulte a seção [Configurações de ponto de distribuição](#bkmk_configs) neste tópico para obter detalhes sobre as opções de configuração disponíveis.  

#### <a name="to-install-a-distribution-point"></a>Para instalar um ponto de distribuição  

1.  No console do Configuration Manager, clique em **Administração** >  **Configuração do Site** > **Funções de Servidores e Sistema de Site**.  

2.  Adicione a função de sistema de sites do ponto de distribuição a um servidor de sistema de sites novo ou existente:  

    -   **Novo servidor do sistema de sites**: na guia **Início** , no grupo **Criar** , clique em **Criar Servidor do Sistema de Sites**. O Assistente para Criar Servidor do Sistema de Site se abre.  

    -   **Servidor do sistema de site existente**: Clique no servidor no qual você deseja instalar a função do sistema de site do ponto de distribuição. Ao clicar em um servidor, uma lista das funções do sistema de site que já estão instaladas no servidor será exibida no painel de resultados.  

         Na guia **Início** , no grupo **Servidor** , clique em **Adicionar Função do Sistema de Site**. O Assistente para Adicionar Funções do Sistema de Site se abre.  

3.  Na página **Geral** , especifique as configurações gerais para o servidor do sistema de site. Ao adicionar o ponto de distribuição em um servidor do sistema de site existente, verifique os valores que foram previamente configurados.  

4.  Na página **Seleção de Função do Sistema** , selecione **Ponto de distribuição** na lista de funções disponíveis e clique em **Próximo**.  

5.  Para as páginas subsequentes do assistente, consulte as informações na seção [Configurações de ponto de distribuição](#bkmk_configs) para concluir cada página do assistente quando solicitado.  

     Por exemplo, se quiser instalar o ponto de distribuição como um ponto de distribuição por pull, selecione **Habilitar este ponto de distribuição para efetuar pull de conteúdo de outros pontos de distribuição** e defina as configurações de que os pontos de distribuição por pull precisam.  

6.  Depois de concluir o assistente, a função de site de ponto de distribuição é adicionada ao servidor do sistema de site.  

#### <a name="to-modify-a-distribution-point"></a>Para modificar um ponto de distribuição  

1.  No console do Configuration Manager, clique em **Administração** >  **Pontos de Distribuição** e selecione o ponto de distribuição que deseja configurar.  

2.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

3.  Use as informações na seção [Configurações de ponto de distribuição](#bkmk_configs) ao editar as propriedades do ponto de distribuição.  

4.  Após fazer as alterações desejadas, salve as configurações e feche as propriedades do ponto de distribuição.  

##  <a name="a-namebkmkmanagea-manage-distribution-point-groups"></a><a name="bkmk_manage"></a> Gerenciar grupos de pontos de distribuição  
 Os grupos de pontos de distribuição fornecem um agrupamento lógico de pontos de distribuição para distribuição de conteúdo. Você pode usar esses grupos para gerenciar e monitorar conteúdo de um local central para pontos de distribuição que abrangem vários sites  

-   É possível adicionar um ou mais pontos de distribuição de qualquer site na hierarquia a um grupo de pontos de distribuição  

-   Você pode adicionar um ponto de distribuição a mais de um grupo de pontos de distribuição  

-   Quando você distribui o conteúdo a um grupo de pontos de distribuição, o Configuration Manager distribui o conteúdo a todos os pontos de distribuição que são membros do grupo de pontos de distribuição  

-   Se você adicionar um ponto de distribuição ao grupo de pontos de distribuição após uma distribuição de conteúdo inicial, o Configuration Manager distribuirá automaticamente o conteúdo ao novo membro do ponto de distribuição  

-   Você pode associar uma coleção a um grupo de pontos de distribuição. Então, ao distribuir conteúdo àquela coleção, o Configuration Manager determina os grupos de pontos de distribuição associados à coleção, e o conteúdo é distribuído a todos os pontos de distribuição que são membros de tais grupos de pontos de distribuição  

    > [!NOTE]  
    >  Após distribuir o conteúdo a uma coleção, se você depois a associar a um novo grupo de pontos de distribuição, redistribua o conteúdo na coleção antes que ele seja distribuído ao novo grupo de pontos de distribuição.  

#### <a name="to-create-and-configure-a-new-distribution-point-group"></a>Para criar e configurar um novo grupo de pontos de distribuição  

1.  No console do Configuration Manager, clique em **Administração** > **Grupos de Pontos de Distribuição**.  

2.  Na guia **Início** , no grupo **Criar** , clique em **Criar Grupo**.  

3.  Digite o nome e a descrição para o grupo de pontos de distribuição.  

4.  Na guia **Coleções** , clique em **Adicionar**, selecione as coleções que você deseja associar ao grupo de pontos de distribuição e então clique em **OK**.  

5.  Na guia **Membros** , clique em **Adicionar**, selecione os pontos de distribuição que você deseja adicionar como membros do grupo de pontos de distribuição, e então clique em **OK**.  

6.  Clique em **OK** para criar o grupo de pontos de distribuição.  

#### <a name="to-add-distribution-points-and-associate-collections-to-an-existing-distribution-point-group"></a>Para adicionar pontos de distribuição e associar coleções a um grupo de pontos de distribuição existente  

1.  No console do Configuration Manager, clique em **Administração** > **Grupos de Pontos de Distribuição**.  

2.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

3.  Na guia **Coleções** , clique em **Adicionar** para selecionar as coleções que deseja associar ao grupo de pontos de distribuição e clique em **OK**.  

4.  Na guia **Membros** , clique em **Adicionar** para selecionar os pontos de distribuição que deseja adicionar como membros do grupo de pontos de distribuição e então clique em **OK**.  

5.  Clique em **OK** para salvar as alterações no grupo de pontos de distribuição.  

#### <a name="to-add-selected-distribution-points-to-a-new-distribution-point-group"></a>Para adicionar os pontos de distribuição selecionados a um novo grupo de pontos de distribuição  

1.  No console do Configuration Manager, clique em **Administração** > **Pontos de Distribuição** e selecione os pontos de distribuição que deseja adicionar ao novo grupo de pontos de distribuição.  

2.  Na guia **Início** , no grupo **Ponto de Distribuição** , expanda **Adicionar Itens Selecionados**, e clique em **Adicionar Itens Selecionados ao Novo Grupo de Pontos de Distribuição**.  

3.  Digite o nome e a descrição para o grupo de pontos de distribuição.  

4.  Na guia **Coleções** , clique em **Adicionar** para selecionar as coleções que deseja associar ao grupo de pontos de distribuição e clique em **OK**.  

5.  Na guia **Membros**, confirme se você deseja que o Configuration Manager adicione os pontos de distribuição listados como membros do grupo de pontos de distribuição. Clique em **Adicionar** para modificar os pontos de distribuição que você deseja adicionar como membros do grupo de pontos de distribuição, e clique em **OK**.  

6.  Clique em **OK** para criar o grupo de pontos de distribuição.  

#### <a name="to-add-selected-distribution-points-to-existing-distribution-point-groups"></a>Para adicionar pontos de distribuição selecionados aos grupos de pontos de distribuição existentes  

1.  No console do Configuration Manager, clique em **Administração** > **Pontos de Distribuição** e selecione os pontos de distribuição que deseja adicionar ao novo grupo de pontos de distribuição.  

2.  Na guia **Início** , no grupo **Ponto de Distribuição** , expanda **Adicionar Itens Selecionados**, e clique em **Adicionar Itens Selecionados aos Grupos de Pontos de Distribuição Existentes**.  

3.  Nos **Grupos de Pontos de Distribuição Disponíveis**, selecione os grupos de pontos de distribuição aos quais os pontos de distribuição selecionados serão adicionados como membros, e clique em **OK**.  

##  <a name="a-namebkmkconfigsa-distribution-point-configurations"></a><a name="bkmk_configs"></a> Configurações de ponto de distribuição  
 Pontos de distribuição individuais dão suporte a diversas configurações diferentes. No entanto, nem todos os tipos de ponto de distribuição dão suporte a todas as configurações. Por exemplo, pontos de distribuição baseados em nuvem não dão suporte a implantações de conteúdo habilitadas para PXE ou multicast. Você pode encontrar informações sobre limitações específicas nos tópicos a seguir:  

-   [Use um ponto de distribuição baseado em nuvem com o System Center Configuration Manager](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

-   [Use um ponto de distribuição de recepção baseado em nuvem com o System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)  

As seções a seguir descrevem as configurações que podem ser selecionadas ao instalar um novo ponto de distribuição ou editar as propriedades de um ponto de distribuição existente:  

### <a name="general"></a>Geral  
 Defina as configurações gerais do ponto de distribuição:  

-   **Instalar e configurar o IIS se exigido pelo Configuration Manager:** selecione esta configuração para permitir que o Configuration Manager instale e configure o IIS (Serviços de Informações da Internet) no servidor se ele ainda não estiver instalado. O IIS deve ser instalado em todos os pontos de distribuição. Se o IIS não for instalado no servidor e você não selecionar essa configuração, você deverá instalar o IIS para que o ponto de distribuição possa ser instalado com êxito.  

    > [!NOTE]  
    >  Essa opção só está disponível ao instalar um novo ponto de distribuição  

- **Habilitar e configurar o BranchCache para esse ponto de distribuição:** selecione esta configuração permitir que o Configuration Manager configure o Windows BranchCache no servidor do ponto de distribuição.  Para obter mais informações sobre como usar o Windows BranchCache com o System Center Configuration Manager, consulte [BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#a-namebkmkbranchcachea-branchcache) em *Suporte para recursos do Windows e redes no System Center Configuration Manager*.

-   **Configurar como os dispositivos de cliente se comunicam com o ponto de distribuição:** há vantagens e desvantagens no uso de HTTP e HTTPS. Para obter mais informações, consulte *Melhores práticas de segurança para gerenciamento de conteúdo* em [Conceitos fundamentais para o gerenciamento de conteúdo no System Center Configuration Manager](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   **Permitir que clientes se conectem anonimamente**: esta configuração especifica se o ponto de distribuição permitirá conexões anônimas de clientes do Configuration Manager com a biblioteca de conteúdo.  

    > [!IMPORTANT]  
    >  O reparo de um aplicativo do Windows Installer pode falhar em um cliente quando você não usar essa configuração.  
    >   
    >  -   Quando você implanta um aplicativo do Windows Installer em um cliente do Configuration Manager, o Configuration Manager baixa o arquivo para o cache local do cliente e os arquivos são removidos após a conclusão da instalação.  
    > -   O cliente do Configuration Manager atualiza a lista de origem do Windows Installer para os aplicativos instalados do Windows Installer, com o caminho de conteúdo para a biblioteca de conteúdo nos pontos de distribuição associados.  
    > -   Posteriormente, se você iniciar a ação de reparo usando Adicionar ou Remover Programas em um cliente do Configuration Manager, o MSIExec tentará acessar o caminho de conteúdo utilizando um usuário anônimo.  
    >   
    >  No entanto, você pode instalar a atualização descrita no artigo [2619572](http://go.microsoft.com/fwlink/?LinkId=279699) da Base de Dados de Conhecimento da Microsoft e modificar uma chave do Registro para alterar esse comportamento.  
    >   
    >  -   Após a atualização ser instalada nos clientes, o MSIExec acessará o caminho do conteúdo usando a conta de usuário conectada quando a configuração **Permitir que clientes se conectem anonimamente** não estiver selecionada.  

-   **Criar um certificado autoassinado ou importar um certificado de cliente PKI (infraestrutura de chave pública) para o ponto de distribuição:** o certificado tem as seguintes finalidades:  

    -   autentica o ponto de distribuição em um ponto de gerenciamento antes que o ponto de distribuição envie mensagens de status.  

    -   Ao marcar a caixa de seleção **Habilitar suporte a PXE para clientes** na página **Configurações PXE** , o certificado é enviado para computadores que executam uma inicialização PXE para que eles possam se conectar a um ponto de gerenciamento durante a implantação do sistema operacional.  

    Quando todos os pontos de gerenciamento do site estiverem configurados para HTTP, crie um certificado autoassinado. Quando os pontos de gerenciamento estiverem configurados para HTTPS, importe um certificado de cliente PKI.  

    Para importar o certificado, navegue até um arquivo PKCS #12 (Public Key Cryptography Standard) que contenha um certificado PKI com os seguintes requisitos para o Configuration Manager:  

    -   O uso pretendido deve incluir a autenticação do cliente.  

    -   A chave privada deve ser habilitada para ser exportada.  

    > [!TIP]  
    >  Não há requisitos específicos para a entidade do certificado nem para o SAN (Nome Alternativo da Entidade), e você pode usar o mesmo certificado para vários pontos de distribuição.  

     Para obter mais informações sobre os requisitos de certificado, consulte [Requisitos de certificado PKI para o System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

     Para ver um exemplo de implantação deste certificado, consulte a seção *Implantando o certificado de cliente para pontos de distribuição* em [Exemplo de implantação passo a passo dos certificados PKI para o System Center Configuration Manager: Autoridade de Certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

-   **Habilitar este ponto de distribuição para conteúdo pré-configurado:** selecione esta configuração para habilitar o ponto de distribuição para conteúdo pré-configurado. Quando essa configuração é selecionada, você pode configurar o comportamento de distribuição ao distribuir conteúdo. É possível optar por sempre pré-configurar o conteúdo no ponto de distribuição, pré-configurar o conteúdo inicial para o pacote, mas usar o processo normal de distribuição de conteúdo quando houver atualizações no conteúdo, ou sempre usar o processo normal de distribuição de conteúdo para o conteúdo no pacote.  

### <a name="drive-settings"></a>Configurações da unidade  

> [!NOTE]  
>  Essas opções só estão disponíveis ao instalar um novo ponto de distribuição  

Especifique as configurações de unidade para o ponto de distribuição. É possível configurar até duas unidades de disco para a biblioteca de conteúdo e duas unidades de disco para o compartilhamento de pacotes, embora o Configuration Manager possa usar unidades adicionais quando as duas primeiras atingirem a reserva de espaço de unidade configurada. A página **Configurações de Unidade** configura a prioridade das unidades de disco e a quantidade de espaço livre em disco que permanece em cada unidade de disco.  

-   **Reserva de espaço de unidade (MB)**: o valor que você define para esta configuração determina a quantidade de espaço livre na unidade antes que o Configuration Manager escolha uma unidade diferente e continue o processo de cópia nessa unidade. Arquivos de conteúdo podem abranger várias unidades.  

-   **Locais de Conteúdo:** especifique os locais de conteúdo para a biblioteca de conteúdo e o compartilhamento de pacotes. O Configuration Manager copia conteúdo para o local de conteúdo primário até que a quantidade de espaço livre atinja o valor especificado para **Reserva de espaço de unidade (MB)**. Por padrão, os locais de conteúdo são definidos para **Automático**. O local de conteúdo primário é definido na unidade de disco que tem mais espaço em disco na instalação, e o local secundário é atribuído à unidade de disco que tem o segundo espaço em disco mais livre. Quando as unidades primárias e secundárias atingirem a reserva de espaço de unidade, o Configuration Manager selecionará outra unidade disponível com o maior espaço em disco e continuará o processo de cópia.  

> [!NOTE]  
>  Para impedir que o Configuration Manager instale em uma unidade específica, crie um arquivo vazio chamado **no_sms_on_drive.sms** e copie-o para a pasta raiz da unidade antes de instalar o ponto de distribuição.  

### <a name="pull-distribution-point"></a>Ponto de distribuição de recepção  
Quando seleciona **Habilitar este ponto de distribuição para efetuar pull de conteúdo de outros pontos de distribuição**, você altera o comportamento de como o computador obtém o conteúdo que você distribui para o ponto de distribuição. Ele se torna um ponto de distribuição de recepção.  

Para cada ponto de distribuição de recepção configurado, você deve especificar um ou mais pontos de distribuição de origem do qual o ponto de distribuição de recepção obtém o conteúdo.  

-   Clique em **Adicionar** e selecione um ou mais dos pontos de distribuição disponíveis para que sejam os pontos de distribuição de origem.  

-   Clique em **Remover** para remover o ponto de distribuição selecionado como ponto de distribuição de origem.  

-   Use os botões de seta para ajustar a ordem em que os pontos de distribuição de origem são contatados pelo ponto de distribuição de recepção quando ele tenta transferir conteúdo. Os pontos de distribuição com o menor valor são contatados primeiro.  

### <a name="pxe"></a>PXE  
Especifique se é para habilitar o PXE no ponto de distribuição. Quando você habilita o PXE, o Configuration Manager instala os Serviços de Implantação do Windows no servidor, se necessário. O Serviços de Implantação do Windows é o serviço que executa a inicialização PXE para instalar sistemas operacionais. Após você concluir o assistente para criar o ponto de distribuição, o Configuration Manager instalará um provedor nos Serviços de Implantação do Windows que usa funções de inicialização do PXE.  

Ao selecionar **Habilitar suporte a PXE para clientes**, configure os seguintes parâmetros:  

-   **Permitir que este ponto de distribuição responda às solicitações PXE de entrada**: especifica se é para habilitar os Serviços de Implantação do Windows para que respondam às solicitações de serviço PXE. Use essa caixa de seleção para habilitar ou desabilitar o serviço sem remover a funcionalidade PXE do ponto de distribuição.  

-   **Habilitar suporte a computadores desconhecidos**: especifique se deseja habilitar o suporte para computadores que não são gerenciados pelo Configuration Manager.  

-   **Exigir uma senha quando os computadores usarem PXE**: para fornecer segurança adicional para implantações PXE, especifique uma senha forte.  

-   **Afinidade de dispositivo de usuário**: especifique como deseja que o ponto de distribuição associe usuários ao computador de destino para implantações PXE. Selecione uma das seguintes opções:  

    -   **Permitir afinidade de dispositivo de usuário com aprovação automática**: selecione essa configuração para associar automaticamente os usuários ao computador de destino sem aguardar a aprovação.  

    -   **Permitir afinidade de dispositivo de usuário pendente de aprovação de administrador**: selecione essa configuração para aguardar a aprovação de um usuário administrativo antes que os usuários sejam associados ao computador de destino.  

    -   **Não permitir afinidade de dispositivo de usuário**: selecione essa configuração para especificar que os usuários não são associados ao computador de destino.  

     Para obter mais informações sobre afinidade de dispositivo de usuário, consulte [Vincular usuários e dispositivos com a afinidade de dispositivo de usuário no System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

-   **Interfaces de rede**: especifique se o ponto de distribuição deve responder às solicitações PXE de todas as interfaces de rede ou de interfaces de rede específicas. Se o ponto de distribuição responde a uma interface de rede específica, você deve fornecer o endereço MAC para cada interface de rede.  

-   **Especifique o atraso de resposta do servidor PXE (segundos)**: especifica, em segundos, qual é tempo de atraso para o ponto de distribuição antes de responder às solicitações do computador quando vários pontos de distribuição habilitados para PXE são usados. Por padrão, o ponto de serviço de PXE do Configuration Manager responde primeiro às solicitações de PXE da rede.  

> [!NOTE]  
>  É possível usar o protocolo PXE para iniciar implantações de sistema operacional em computadores cliente do Configuration Manager. O Configuration Manager usa a função de site do ponto de distribuição habilitado para PXE para iniciar o processo de implantação do sistema operacional. O ponto de distribuição habilitado para PXE deve ser configurado para responder às solicitações de inicialização de PXE feitas por clientes do Configuration Manager na rede e interagir com a infraestrutura do Configuration Manager para determinar as ações de implantação apropriadas que devem ser executadas.  

### <a name="multicast"></a>Multicast  
Especifique se é para habilitar o multicast no ponto de distribuição. Quando você habilita o multicast, o Configuration Manager instala os Serviços de Implantação do Windows no servidor, se necessário.  

Ao marcar a caixa de seleção **Habilitar multicast para enviar dados a vários clientes simultaneamente** , configure os seguintes parâmetros:  

-   **Conta de Conexão Multicast**: especifique a conta a ser usada ao configurar as conexões de banco de dados do Configuration Manager para multicast.  

-   **Configurações de endereço multicast**: especifique os endereços IP usados para enviar dados aos computadores de destino. Por padrão, o endereço IP é obtido de um servidor DHCP habilitado para distribuir endereços multicast. Dependendo do ambiente de rede, é possível especificar um intervalo de endereços IP entre 239.0.0.0 e 239.255.255.255.  

    > [!IMPORTANT]  
    >  Os endereços IP configurados devem estar acessíveis a computadores de destino que solicitam a imagem do sistema operacional. Verifique se os roteadores e firewalls permitem o tráfego multicast entre o computador de destino e o servidor do site.  

-   **Intervalo de portas UDP para multicast**: especifique o intervalo de portas UDP usado para enviar dados aos computadores de destino.  

    > [!IMPORTANT]  
    >  As portas UDP devem estar acessíveis a computadores de destino que solicitam a imagem do sistema operacional. Verifique se os roteadores e firewalls permitem o tráfego multicast entre o computador de destino e o servidor do site.  

-   **Taxa de transferência do cliente**: selecione a taxa de transferência usada para baixar os dados nos computadores de destino.  

-   **Máximo de clientes**: especifique o número máximo de computadores de destino que podem baixar o sistema operacional desse ponto de distribuição.  

-   **Habilitar multicast agendado**: especifique como o Configuration Manager controla quando iniciar a implantação de sistemas operacionais em computadores de destino. Quando selecionada, configure as seguintes opções:  

    -   **Atraso de início da sessão (minutos)**: especifique o número de minutos que o Configuration Manager espera antes de responder à primeira solicitação de implantação.  

    -   **Tamanho mínimo da sessão (clientes)**: especifique quantas solicitações devem ser recebidas antes que o Configuration Manager comece a implantar o sistema operacional.  

> [!NOTE]  
>  As implantações multicast conservam a largura de banda da rede enviando simultaneamente dados a vários clientes do Configuration Manager, em vez de enviar uma cópia dos dados a cada cliente por uma conexão separada. Para obter mais informações sobre como usar multicast para implantar sistemas operacionais, consulte [Usar o multicast para implantar o Windows pela rede com o System Center Configuration Manager](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

### <a name="group-relationships"></a>Relacionamentos de grupo  

> [!NOTE]  
>  Essas opções estão disponíveis somente ao editar as propriedades de um ponto de distribuição instalado anteriormente  

Gerencie os grupos de pontos de distribuição dos quais esse ponto de distribuição é membro.  

Para adicionar esse ponto de distribuição como membro a um grupo de pontos de distribuição existente, clique em **Adicionar**. Selecione um grupo de pontos de distribuição existente na lista da caixa de diálogo **Adicionar a Grupos de Pontos de Distribuição** e clique em **OK**.  

Para remover esse ponto de distribuição de um grupo de pontos de distribuição, selecione o grupo na lista e clique em **Remover**.  

### <a name="content"></a>Conteúdo  

> [!NOTE]  
>  Essas opções estão disponíveis somente ao editar as propriedades de um ponto de distribuição instalado anteriormente  

Gerencie o conteúdo distribuído para o ponto de distribuição. A seção Pacotes de implantação fornece uma lista dos pacotes distribuídos para esse ponto de distribuição. Você pode selecionar um pacote da lista e executar as seguintes ações:  

-   **Validar**: inicia o processo para validar a integridade dos arquivos de conteúdo no pacote. Para exibir os resultados do processo de validação de conteúdo, no espaço de trabalho **Monitoramento** , expanda **Status da Distribuição**e clique no nó **Status do Conteúdo** .  

-   **Redistribuir**: copia todos os arquivos de conteúdo do pacote nos pontos de distribuição e substitui os arquivos existentes. Você normalmente usa essa operação para reparar arquivos de conteúdo do pacote.  

-   **Remover**: remove os arquivos de conteúdo do ponto de distribuição para o pacote.  

### <a name="content-validation"></a>Validação de conteúdo  
Especifique se é para definir um agendamento para validar a integridade dos arquivos de conteúdo no ponto de distribuição. Quando você habilita a validação de conteúdo segundo um cronograma, o Configuration Manager inicia o processo no horário agendado e todo o conteúdo no ponto de distribuição é verificado. Também é possível configurar a prioridade da validação de conteúdo. Por padrão, a prioridade é definida como **Mais Baixa**.  

Para exibir os resultados do processo de validação de conteúdo, no espaço de trabalho **Monitoramento** , expanda **Status da Distribuição**e clique no nó **Status do Conteúdo** . O conteúdo de cada tipo de pacote (por exemplo, aplicativo, pacote de atualização de software e imagem de inicialização) é exibido.  

> [!WARNING]  
>  Embora você especifique o cronograma de validação de conteúdo usando o horário local do computador, ele é exibido no console do Configuration Manager usando UTC.  

### <a name="boundary-group"></a>Grupo de limites  
Gerencie os grupos de limites aos quais esse ponto de distribuição está atribuído. Você pode associar grupos de limites a um ponto de distribuição. Durante a implantação do conteúdo, os clientes devem estar em um grupo de limites associado ao ponto de distribuição para usá-lo como local de origem do conteúdo.
Além disso:
- Em versões anteriores à 1610, é possível marcar a caixa de seleção **Permitir que os clientes usem este sistema de sites como local de origem de fallback de conteúdo** para permitir que clientes fora desses grupos de limites façam fallback e usem o ponto de distribuição como local de origem de conteúdo quando não houver outro ponto de distribuição disponível. Para obter mais informações sobre os grupos de limite, consulte [Grupos de limite para as versões 1511, 1602 e 1606](/sccm/core/servers/deploy/configur/boundary-groups-for-1511-1602-and-1606), e para os pontos de distribuição preferenciais, consulte [Conceitos fundamentais para o gerenciamento de conteúdo no System Center Configuration Manager](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).
- Na versão 1610 ou posterior, você pode configurar as *Relações* do grupo de limites que definem quanto e a quais grupos de limites um cliente poderá realizar fallback para localizar o conteúdo. Para obter mais informações, consulte [Grupos de limites](/sccm/core/servers/deploy/configur/define-site-boundaries-and-boundary-groups#boundary-groups).


### <a name="schedule"></a>Agendamento  

> [!NOTE]  
>  Essas opções estão disponíveis somente ao editar as propriedades de um ponto de distribuição instalado anteriormente  

> [!TIP]  
>  Essa guia está disponível somente ao editar as propriedades de um ponto de distribuição remoto do computador do servidor de site.  

 Especifique se deseja configurar um cronograma que restringe quando o Configuration Manager pode transferir dados para o ponto de distribuição.  

> [!IMPORTANT]  
>  A agenda se baseia no fuso horário do site de envio, não do ponto de distribuição.  

Para restringir dados, selecione o período de tempo e uma das configurações a seguir para a **Disponibilidade**:  

-   **Aberto para todas as prioridades**: especifica se o Configuration Manager deve enviar dados para o ponto de distribuição sem restrições.  

-   **Permitir prioridade média e alta**: especifica se o Configuration Manager deve enviar somente dados de prioridade média e alta para o ponto de distribuição.  

-   **Permitir alta prioridade apenas**: especifica se o Configuration Manager deve enviar somente dados de prioridade alta para o ponto de distribuição.  

-   **Fechado**: especifica que o Configuration Manager não deve enviar dados para o ponto de distribuição.  

Você pode restringir os dados por prioridade ou encerrar a conexão por períodos de tempo selecionados.  

### <a name="rate-limits"></a>Limites de taxa  

> [!NOTE]  
>  Essas opções estão disponíveis somente ao editar as propriedades de um ponto de distribuição instalado anteriormente  

> [!TIP]  
>  Essa guia está disponível somente ao editar as propriedades de um ponto de distribuição remoto do computador do servidor de site.  

Especifique se você deve configurar os limites de taxa para controlar a largura de banda da rede que está em uso ao transferir o conteúdo para o ponto de distribuição. Você pode escolher entre as seguintes opções:  

-   **Ilimitado ao enviar para este destino**: especifica se o Configuration Manager deve enviar conteúdo ao ponto de distribuição sem restrições de limites de taxas.  

-   **Modo de pulso**: especifica o tamanho dos blocos de dados que são enviados para o ponto de distribuição. Você também pode especificar um retardo de tempo entre o envio de cada bloco de dados. Use essa opção quando você deve enviar dados através de uma conexão de rede com largura de banda bem baixa para o ponto de distribuição. Por exemplo, você pode ter restrições para enviar 1 KB de dados a cada cinco segundos, independentemente da velocidade do link ou seu uso em um determinado tempo.  

-   **Limitado a taxas máximas de transferência especificadas por hora**: especifique essa configuração para que um site envie dados para um ponto de distribuição usando somente a porcentagem de tempo que você define. Quando você usa essa opção, o Configuration Manager não identifica a largura de banda disponível das redes. Em vez disso, ele divide em períodos o tempo em que pode enviar dados. Os dados são enviados em um curto bloco de tempo, que é seguido por blocos de tempo quando os dados não são enviados. Por exemplo, se a taxa máxima estiver definida como **50%**, o Configuration Manager transmitirá dados por um período, seguido de igual período quando nenhum dado será enviado. A quantidade de tamanho real de dados ou o tamanho do bloco de dados não é gerenciado. Em vez disso, somente a quantidade de tempo durante a qual os dados são enviados é gerenciada.  



<!--HONumber=Jan17_HO2-->


