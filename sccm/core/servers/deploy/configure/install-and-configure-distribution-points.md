---
title: Gerenciar pontos de distribuição
titleSuffix: Configuration Manager
description: Use pontos de distribuição para hospedar o conteúdo a ser implantado em usuários e dispositivos.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0ab848051d5eaa85d2b515145ff64471aee81a31
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53415034"
---
# <a name="install-and-configure-distribution-points-in-configuration-manager"></a>Instalar e configurar pontos de distribuição no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Instale pontos de distribuição do Configuration Manager para hospedar os arquivos de conteúdo implantados em dispositivos e usuários. Crie grupos de pontos de distribuição para simplificar o modo de gerenciamento dos pontos de distribuição e o modo de distribuição do conteúdo para os pontos de distribuição.  

*Instale um novo ponto de distribuição* usando o assistente de instalação. Para obter mais informações, confira [Instalar um ponto de distribuição](#bkmk_install). Para *gerenciar as propriedades de um ponto de distribuição existente*, edite as propriedades do ponto de distribuição. Para obter mais informações, consulte [Configurar um ponto de distribuição](#bkmk_configs). 

Defina a maioria das configurações do ponto de distribuição com um desses métodos. Algumas configurações estão disponíveis somente quando você estiver instalando ou editando, mas não ambos:  

-   Configurações disponíveis somente ao instalar um ponto de distribuição:  

    -   **Permitir que o Gerenciador de Configurações instale o IIS no computador do ponto de distribuição**

    -   **Definir configurações de espaço da unidade para o ponto de distribuição**  

-   Configurações disponíveis somente ao editar as propriedades de um ponto de distribuição:  

    -   **Gerenciar relacionamentos de grupo de pontos de distribuição**  

    -   **Exibir o conteúdo implantado no ponto de distribuição**  

    -   **Configurar limites de taxa de transferências de dados para os pontos de distribuição**  

    -   **Configurar agendamentos para transferências de dados para pontos de distribuição**  



##  <a name="bkmk_install"></a> Instalar um ponto de distribuição  

Escolha um servidor do sistema de sites como um ponto de distribuição para que o conteúdo possa ser disponibilizado aos computadores cliente. Atribua um ponto de distribuição a, pelo menos, um [grupo de limites](/sccm/core/servers/deploy/configure/boundary-groups#distribution-points) antes que os computadores cliente locais possam usar esse ponto de distribuição como um local de fonte de conteúdo. Adicione a função de ponto de distribuição a um novo servidor do sistema de sites ou a um existente.


### <a name="bkmk_install-prereq"></a> Pré-requisitos

Quando instala um novo ponto de distribuição, você usa um assistente de instalação que o orienta quanto às configurações disponíveis. Antes de começar, considere os seguintes pré-requisitos:  

-   É necessário ter as seguintes permissões de segurança para criar e configurar o ponto de distribuição:  

    -   **Ler** para o objeto **Ponto de Distribuição**  

    -   **Copiar para o Ponto de Distribuição** para o objeto **Ponto de Distribuição**  

    -   **Modificar** para o objeto **Site**  

    -   **Gerenciar Certificados para Implantação do Sistema Operacional** para o objeto **Site**  

-   Instale o IIS (Serviços de Informações da Internet) no servidor Windows que hospeda o ponto de distribuição. Ou, quando você instalar a função do sistema de sites, o Configuration Manager poderá instalar e configurar o IIS para você.  


### <a name="bkmk_install-procedure"></a> Procedimento para instalar um ponto de distribuição  

Use este procedimento para adicionar um novo ponto de distribuição. Para alterar a configuração de um ponto de distribuição existente, confira a seção [Configurar um ponto de distribuição](#bkmk_configs).  

Comece com o procedimento geral para [Instalar funções do sistema de sites](/sccm/core/servers/deploy/configure/install-site-system-roles). Selecione a função **ponto de distribuição** na página **Seleção de Função do Sistema** do assistente para Criar Servidor do Sistema de Sites. Essa ação adiciona as seguintes páginas ao assistente:  
- [Ponto de distribuição](#bkmk_config-general)
- [Configurações de Unidade](#bkmk_config-drive)
- [Ponto de Distribuição por Pull](#bkmk_config-pull)
- [Configurações PXE](#bkmk_config-pxe)
- [Multicast](#bkmk_config-multicast)
- [Validação de Conteúdo](#bkmk_config-valid)
- [Grupos de Limites](#bkmk_config-boundary)

> [!Important]  
> As configurações a seguir estão disponíveis somente para a instalação de um ponto de distribuição:  
> 
> - **Permitir que o Gerenciador de Configurações instale o IIS no computador do ponto de distribuição**  
> 
> - **Definir configurações de espaço da unidade para o ponto de distribuição**  

Para obter mais informações sobre as páginas do assistente específicas da função de ponto de distribuição, confira a seção [Configurar um ponto de distribuição](#bkmk_configs). Por exemplo, se você deseja instalar o ponto de distribuição como um [ponto de distribuição por pull](#bkmk_config-pull), escolha a opção para **Habilitar esse ponto de distribuição para efetuar pull de conteúdo de outros pontos de distribuição**. Em seguida, faça as configurações adicionais que os pontos de distribuição por pull precisam.  

Depois que você concluir o assistente para Criar Servidor do Sistema de Sites, o site adicionará a função de ponto de distribuição para o servidor do sistema de sites.  



##  <a name="bkmk_manage"></a> Gerenciar grupos de pontos de distribuição  

Os grupos de pontos de distribuição fornecem um agrupamento lógico de pontos de distribuição para distribuição de conteúdo. Use esses grupos para gerenciar e monitorar de um local central o conteúdo de pontos de distribuição que abrangem vários sites. Lembre-se do seguinte ponto:

-   Adicione um ou mais pontos de distribuição de qualquer site na hierarquia a um grupo de pontos de distribuição.  

-   Adicione um ponto de distribuição a mais de um grupo de pontos de distribuição.  

-   Quando você distribui conteúdo a um grupo de pontos de distribuição, o Configuration Manager distribui o conteúdo a todos os pontos de distribuição que são membros do grupo.  

-   Se você adicionar um ponto de distribuição ao grupo após uma distribuição de conteúdo inicial, o Configuration Manager distribuirá automaticamente o conteúdo ao novo membro do ponto de distribuição.  

-   Associe uma coleção a um grupo de pontos de distribuição. Quando você distribui conteúdo para essa coleção, o Configuration Manager determina quais grupos estão associados à coleção. Em seguida, ele distribui o conteúdo a todos os pontos de distribuição que são membros desses grupos.  

    > [!NOTE]  
    >  Após distribuir o conteúdo a uma coleção, se você depois a associar a coleção a um novo grupo de pontos de distribuição, redistribua o conteúdo na coleção antes que ele seja distribuído ao novo grupo de pontos de distribuição.  

As seções a seguir listam os procedimentos das seguintes ações para gerenciar grupos de pontos de distribuição:  
- [Criar e configurar um grupo de pontos de distribuição](#bkmk_dpgroup-create)
- [Modificar um grupo de pontos de distribuição existente](#bkmk_dpgroup-modify)
- [Adicionar pontos de distribuição selecionados aos grupos de pontos de distribuição existentes](#bkmk_dpgroup-addexist)


### <a name="bkmk_dpgroup-create"></a> Procedimento para criar e configurar um novo grupo de pontos de distribuição  

1.  No console do Configuration Manager, acesse o workspace **Administração** e selecione o nó **Grupos de Pontos de Distribuição**.  

2.  Na faixa de opções, clique em **Criar Grupo**.  

3.  Na janela Criar Grupo de Pontos de Distribuição, insira o **Nome** e, opcionalmente, uma **Descrição** para o grupo.  

4.  Na guia **Membros**, clique em **Adicionar**.  

5.  Na janela Adicionar Pontos de Distribuição, selecione um ou mais pontos de distribuição a serem adicionados como membros do grupo. Clique em **OK**.  

6.  Se necessário, mude para a guia **Coleções** da janela Criar Grupo de Pontos de Distribuição e clique em **Adicionar**.  

7.  Na janela Selecionar Coleções, selecione as coleções a serem associadas ao grupo de pontos de distribuição e, em seguida, clique em **OK**.  

8.  Na janela Criar Grupo de Pontos de Distribuição, clique em **OK** para criar o grupo.  


#### <a name="create-a-new-group-from-an-existing-distribution-point"></a>Criar um grupo usando um ponto de distribuição existente

1.  No console do Configuration Manager, vá até o workspace **Administração** e selecione o nó **Pontos de Distribuição**. Selecione um ou mais pontos de distribuição a serem adicionados a um novo grupo de pontos de distribuição.  

2.  Na faixa de opções, clique em **Adicionar Itens Selecionados** e, em seguida, clique em **Adicionar Itens Selecionados ao Novo Grupo de Pontos de Distribuição**.  

Esse processo popula automaticamente a guia **Membros** da janela Criar Grupo de Pontos de Distribuição com os servidores selecionados.


### <a name="bkmk_dpgroup-modify"></a> Procedimento para modificar um grupo de pontos de distribuição existente  

1.  No console do Configuration Manager, acesse o workspace **Administração** e selecione o nó **Grupos de Pontos de Distribuição**.  

2.  Selecione um grupo de pontos de distribuição existente a ser modificado. Na faixa de opções, clique em **Propriedades**.  

3.  Para associar novas coleções a esse grupo, mude para a guia **Coleções** e, em seguida, clique em **Adicionar**. Selecione as coleções e, em seguida, clique em **OK**.  

4.  Para adicionar novos pontos de distribuição a esse grupo, mude para a guia **Membros** e, em seguida, clique em **Adicionar**. Selecione os pontos de distribuição e, em seguida, clique em **OK**.  

5.  Escolha **OK** para salvar as alterações no grupo de pontos de distribuição.  


### <a name="bkmk_dpgroup-addexist"></a> Procedimento para adicionar os pontos de distribuição selecionados aos grupos de pontos de distribuição existentes  

1.  No console do Configuration Manager, vá até o workspace **Administração** e selecione o nó **Pontos de Distribuição**. Selecione um ou mais pontos de distribuição a serem adicionados a um grupo existente.  

2.  Na faixa de opções, clique em **Adicionar Itens Selecionados** e, em seguida, clique em **Adicionar Itens Selecionados a Grupos de Pontos de Distribuição Existentes**.  

3.  Nos **Grupos de pontos de distribuição disponíveis**, selecione os grupos nos quais os pontos de distribuição selecionados serão adicionados como membros. Clique em **OK**.  



## <a name="bkmk_reassign"></a> Reatribuir um ponto de distribuição
<!-- 1306937 --> Muitos clientes têm amplas infraestruturas do Configuration Manager e estão reduzindo sites primários ou secundários para simplificar os ambientes deles. Eles ainda precisam manter os pontos de distribuição de localizações de filiais para fornecer conteúdo para clientes gerenciados. Esses pontos de distribuição geralmente contêm vários terabytes de conteúdo ou mais. Distribuir esse conteúdo para esses servidores remotos custa muito em termos de largura de banda de rede e de tempo. 

A partir da versão 1802, esse recurso permite reatribuir um ponto de distribuição para outro site primário sem a redistribuição do conteúdo. Esta ação atualiza a atribuição de sistema, persistindo todo o conteúdo no servidor. Se você precisar reatribuir vários pontos de distribuição, primeiro execute essa ação em um único ponto de distribuição. Em seguida, continue com os demais servidores, um por vez.

> [!IMPORTANT]  
> O servidor de destino pode hospedar apenas a função de ponto de distribuição. Se o servidor do sistema de sites hospedar outra função de servidor do Configuration Manager, tal como o ponto de migração de estado, você não poderá reatribuir o ponto de distribuição. Você não pode reatribuir um ponto de distribuição de nuvem. 

Antes de reatribuir um ponto de distribuição, adicione a conta de computador do servidor do site de destino ao grupo local de Administradores no servidor do ponto de distribuição de destino. 

Siga estas etapas para reatribuir um ponto de distribuição:

1. No console do Configuration Manager, conecte-se ao site de administração central.  

2. Acesse o workspace **Administração** e selecione o nó **Pontos de Distribuição**.  

3. Clique com o botão direito do mouse no ponto de distribuição de destino e selecione **Reatribuir Ponto de Distribuição**.  

4. Selecione o servidor do site de destino e o código do site ao qual você deseja reatribuir esse ponto de distribuição.  

Monitore a reatribuição da mesma forma como quando você adiciona uma nova função. O método mais simples é atualizar a exibição do console após alguns minutos. Adicione a coluna de código do site à exibição. Esse valor é alterado quando o Configuration Manager reatribui o servidor. Se você tentar realizar outra ação no servidor de destino antes de atualizar a exibição do console, ocorrerá um erro de "objeto não encontrado". Garanta que o processo foi concluído e atualize a exibição do console antes de iniciar outras ações no servidor.

Depois de reatribuir um ponto de distribuição, atualize o certificado do servidor. O novo servidor do site precisa recriptografar esse certificado usando sua chave pública e armazená-lo no banco de dados do site. Para obter mais informações, consulte a configuração **Criar um certificado autoassinado ou importar um certificado de cliente PKI (infraestrutura de chave pública) para o ponto de distribuição** na guia [Geral](#general) das propriedades do ponto de distribuição. 

- Para certificados PKI, você não precisa criar um novo certificado. Importe o mesmo .PFX e insira a senha.  

- Para certificados autoassinados, ajuste a data ou hora de vencimento para atualizá-los.  

- Se você não atualizar o certificado, o ponto de distribuição ainda fornecerá o conteúdo, mas as seguintes funções falharão:  

    - Mensagens de validação do conteúdo (o distmgr.log mostra que ele não pode descriptografar o certificado)  

    - Suporte a PXE para clientes  


### <a name="tips"></a>Dicas 

- Execute essa ação no site de administração central. Essa prática ajuda com a replicação para os sites primários.  

- Não distribua o conteúdo para o servidor de destino e, em seguida, tente reatribuí-lo. As tarefas de distribuição do conteúdo que estão em andamento poderão falhar durante o processo de reatribuição, mas elas tentarão novamente como de costume.  

- Se o servidor também é um cliente do Configuration Manager, reatribua também o cliente ao novo site primário. Essa etapa é especialmente crítica para pontos de distribuição pull, que usam componentes cliente para baixar o conteúdo.  

- Esse processo remove o ponto de distribuição do grupo de limites padrão do site antigo. Você precisa adicioná-lo manualmente ao grupo de limites padrão do novo site, se necessário. Todas as outras atribuições de grupo de limites permanecem as mesmas.  



##  <a name="bkmk_configs"></a> Configurar um ponto de distribuição  

Pontos de distribuição individuais dão suporte a diversas configurações diferentes. No entanto, nem todos os tipos de ponto de distribuição dão suporte a todas as configurações. Por exemplo, os pontos de distribuição na nuvem não dão suporte a implantações habilitadas para PXE ou multicast. Para obter mais informações sobre limitações específicas, confira os seguintes artigos:  

-   [Usar um ponto de distribuição na nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)  

-   [Usar um ponto de distribuição por pull](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)  

As seções a seguir descrevem as configurações do ponto de distribuição para [instalar um novo](#bkmk_install-procedure) ou [editar um existente](#bkmk_change-procedure):  
- [Configurações gerais](#bkmk_config-general)
- [Configurações de Unidade](#bkmk_config-drive)
- [Ponto de Distribuição por Pull](#bkmk_config-pull)
- [Configurações PXE](#bkmk_config-pxe)
- [Multicast](#bkmk_config-multicast)
- [Validação de Conteúdo](#bkmk_config-valid)
- [Grupos de Limites](#bkmk_config-boundary)


#### <a name="bkmk_change-procedure"></a> Procedimento para alterar um ponto de distribuição  

1.  No console do Configuration Manager, vá até o workspace **Administração** e selecione o nó **Pontos de Distribuição**.  

2.  Selecione o ponto de distribuição a ser configurado. Na faixa de opções, clique em **Propriedades**.  

3.  Use as informações nas seções a seguir quando estiver editando as propriedades do ponto de distribuição.  

4.  Depois de fazer as alterações desejadas, clique em **OK** para salvar suas configurações e fechar as propriedades do ponto de distribuição.  


### <a name="bkmk_config-general"></a> Geral  

As seguintes configurações estão na página **Ponto de distribuição** do assistente para Criar Servidor do Sistema de Sites e na guia **Geral** da janela Propriedades do ponto de distribuição:  

-   **Instalar e configurar o IIS se exigido pelo Configuration Manager**: Se o IIS ainda não tiver sido instalado no servidor, o Configuration Manager o instalará e o configurará. O Configuration Manager requer o IIS em todos os pontos de distribuição. Se você não escolher essa configuração e o IIS não estiver instalado no servidor, primeiro instale o IIS para que o Configuration Manager possa instalar o ponto de distribuição com êxito.  

    > [!NOTE]  
    >  Essa opção é exibida apenas na página **Ponto de distribuição** do assistente para Criar Servidor do Sistema de Sites. Ela está disponível apenas para a [instalação de um novo ponto de distribuição](#bkmk_install-procedure).  

- **Habilitar e configurar o BranchCache para este ponto de distribuição**: escolha esta configuração permitir que o Configuration Manager configure o Windows BranchCache no servidor do ponto de distribuição. Para obter mais informações, confira [BranchCache](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#branchcache).  

- **Ajustar a velocidade de download para usar a largura de banda de rede não utilizada (Windows LEDBAT)**<!--1358112-->: Começando na versão 1806, habilite os pontos de distribuição para usar o controle de congestionamento de rede. Para obter mais informações, confira [LEDBAT do Windows](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#windows-ledbat). O ponto de distribuição precisa estar executando o Windows Server, versão 1709. Não há nenhum pré-requisito do cliente.  

- **Descrição**: uma descrição opcional para essa função de ponto de distribuição.  

-   **Configure como os dispositivos cliente se comunicam com o ponto de distribuição**: Há vantagens e desvantagens no uso do **HTTP** ou do **HTTPS**. Para obter mais informações, consulte [Melhores práticas de segurança para gerenciamento de conteúdo](/sccm/core/plan-design/hierarchy/security-and-privacy-for-content-management#BKMK_Security_ContentManagement).  

-   **Permitir que clientes se conectem anonimamente**: essa configuração especifica se o ponto de distribuição permite conexões anônimas de clientes do Configuration Manager com a biblioteca de conteúdo.  

    > [!Important]  
    > Se você não usa essa configuração, aplique as alterações descritas no artigo da Base de Dados de Conhecimento Microsoft [2619572](https://support.microsoft.com/help/2619572/) nos clientes Windows 7. Caso contrário, o reparo de aplicativos do Windows Installer poderá falhar.  
    >   
    >  Quando você implanta um aplicativo do Windows Installer, o cliente do Configuration Manager baixa o arquivo em seu cache local. O cliente, eventualmente, remove os arquivos após a conclusão da instalação. O cliente do Configuration Manager atualiza a lista de fontes do Windows Installer para o aplicativo. Ele define o caminho do conteúdo para a biblioteca de conteúdo nos pontos de distribuição associados. Mais tarde, se você tentar reparar o aplicativo no dispositivo, o MSIExec tentará acessar o caminho do conteúdo usando um usuário anônimo.  
    >   
    >  Depois que você instalar a atualização nos clientes e modificar a chave do Registro documentada, o MSIExec acessará o caminho do conteúdo usando a conta de usuário conectada.  

-   **Criar um certificado autoassinado ou importar um certificado de cliente PKI**: o Configuration Manager usa esse certificado para as seguintes finalidades:  

    -   autentica o ponto de distribuição em um ponto de gerenciamento antes que o ponto de distribuição envie mensagens de status.  

    -   Quando você **Habilitar suporte a PXE para clientes** na página **Configurações do PXE**, o ponto de distribuição enviará o certificado para os computadores que realizam a inicialização PXE. Esses computadores o usam para se conectar a um ponto de gerenciamento durante o processo de implantação do sistema operacional.  

    Ao configurar todos os pontos de gerenciamento no site para HTTP, selecione a opção para **Criar certificado autoassinado**. Ao configurar os pontos de gerenciamento para HTTPS, use a opção para **Importar certificado** da PKI.  

    Para importar o certificado, navegue até um arquivo PKCS #12 (Public Key Cryptography Standard) válido. Este arquivo PFX ou CER tem o certificado PKI com os seguintes requisitos do Configuration Manager:  

    -   O uso pretendido inclui a autenticação de cliente  

    -   Habilitar a chave privada para ser exportada  

    > [!TIP]  
    >  Não há nenhum requisito específico para a entidade do certificado ou o SAN (nome alternativo da entidade). Se necessário, use o mesmo certificado para vários pontos de distribuição.  

     Para obter mais informações sobre os requisitos de certificado, consulte [Requisitos do certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

     Para ver um exemplo de implantação desse certificado, confira a seção [Implantando o certificado do cliente para pontos de distribuição](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012).  

-   **Habilitar esse ponto de distribuição para conteúdo pré-teste**: essa configuração permite que você adicione conteúdo no servidor, antes de distribuir o software. Como os arquivos de conteúdo já estão na biblioteca de conteúdo, eles não são transferidas pela rede quando você distribui o software. Para obter mais informações, confira [Conteúdo pré-teste](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent).  


### <a name="bkmk_config-drive"></a> Configurações de unidade  

> [!NOTE]  
>  Essas opções só estão disponíveis ao instalar um novo ponto de distribuição.  

Especifique as configurações de unidade para o ponto de distribuição. Configure até duas unidades de disco para a biblioteca de conteúdo e duas unidades de disco para o compartilhamento de pacotes. O Configuration Manager pode usar outras unidades quando as duas primeiras atingirem a reserva de espaço de unidade configurada. A página **Configurações de Unidade** configura a prioridade das unidades de disco e a quantidade de espaço livre em disco que permanece em cada unidade de disco.  

-   **Reserva de espaço na unidade (MB)**: esse valor determina a quantidade de espaço livre que uma unidade precisa ter para que o Configuration Manager escolha uma outra unidade para continuar processo de cópia. Arquivos de conteúdo podem abranger várias unidades.  

-   **Localizações de conteúdo**: especifique os locais para o compartilhamento de biblioteca e pacote de conteúdo nesse ponto de distribuição. Por padrão, todos os locais de conteúdo são definidos como **Automático**. O Configuration Manager copia conteúdo para o local de conteúdo primário até que a quantidade de espaço livre atinja o valor especificado para **Reserva de espaço de unidade (MB)**. Quando você seleciona **Automático**, o Configuration Manager define os locais de conteúdo primários como a unidade de disco com mais espaço em disco na instalação. Ele define os locais secundários como a unidade de disco com o segundo maior espaço livre em disco. Quando os locais primários e secundários atingem a reserva de espaço na unidade, o Configuration Manager seleciona outra unidade disponível com o maior espaço livre em disco para continuar o processo de cópia.  

> [!Tip]  
>  Para impedir que o Configuration Manager instale em uma unidade específica, crie um arquivo vazio chamado **no_sms_on_drive.sms** e copie-o para a pasta raiz da unidade antes de instalar o ponto de distribuição.  

Para obter mais informações, confira [A biblioteca de conteúdo](/sccm/core/plan-design/hierarchy/the-content-library).


### <a name="bkmk_config-pull"></a> Ponto de distribuição por pull  

Quando você seleciona **Habilitar este ponto de distribuição para efetuar pull de conteúdo de outros pontos de distribuição**, ele se torna um ponto de distribuição por pull. É possível alterar o comportamento de como o ponto de distribuição obtém o conteúdo que você distribui a ele. Para obter mais informações, consulte [Usar um ponto de distribuição pull](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

Para cada ponto de distribuição por pull que você configurar, especifique um ou mais pontos de distribuição de fonte dos quais ele obterá o conteúdo:  

-   Clique em **Adicionar** e selecione um ou mais dos pontos de distribuição disponíveis para que se tornem fontes.  

-   Use os botões de seta para ajustar a prioridade. Quando o ponto de distribuição por pull tenta transferir o conteúdo, a prioridade é a ordem em que ele contata os pontos de distribuição de fonte. Primeiro, ele contata os pontos de distribuição com o menor valor.  


### <a name="bkmk_config-pxe"></a> PXE  

Especifique se é para habilitar o PXE no ponto de distribuição. Use o PXE para iniciar implantações de sistema operacional nos clientes. Para obter mais informações de como usar o PXE no Configuration Manager, confira [Usar o PXE para implantar o Windows na rede](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).

Quando você habilita o PXE, o Configuration Manager instala o WDS (Serviços de Implantação do Windows) no servidor, se necessário. O WDS é o serviço que executa a inicialização PXE para instalar sistemas operacionais. Depois de concluir o assistente para criar o ponto de distribuição, o Configuration Manager instala um provedor no WDS que usa as funções de inicialização PXE. 

Começando na versão 1806, você pode habilitar o PXE em um ponto de distribuição sem o WDS. 

Selecione a opção para **Habilitar suporte a PXE para clientes** e, em seguida, defina as seguintes configurações:  

 > [!Note]  
 > Clique em **Sim** na caixa de diálogo **Examinar Portas Necessárias para PXE** para confirmar que você deseja habilitar o PXE. O Configuration Manager configura automaticamente as portas padrão no firewall do Windows. Se você usar um firewall diferente, configure as portas manualmente.  
 >   
 > Se você instalar o WDS e DHCP no mesmo servidor, configure o WDS para escutar em uma porta diferente. Por padrão, o DHCP escuta na mesma porta. Para obter mais informações, consulte [Considerações sobre quando você tem o WDS e DHCP no mesmo servidor](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment#BKMK_WDSandDHCP).  

- **Permitir que este ponto de distribuição responda às solicitações PXE de entrada**: Especifique se deseja habilitar o WDS para responder a solicitações de serviço PXE. Use essa configuração para habilitar e desabilitar o serviço sem remover a funcionalidade PXE do ponto de distribuição.  

- **Habilitar suporte a computadores desconhecidos**: especifique se deseja habilitar o suporte para computadores não gerenciados pelo Configuration Manager. Para obter mais informações, consulte [Preparar implantações de computador desconhecido](/sccm/osd/get-started/prepare-for-unknown-computer-deployments).  

- **Habilitar um respondente PXE sem o Serviço de Implantação do Windows**: começando na versão 1806, essa opção habilita um respondente PXE no ponto de distribuição, que não requer WDS. Esse respondente PXE dá suporte a redes IPv6. Se você habilitar essa opção em um ponto de distribuição que já esteja habilitado para PXE, o Configuration Manager suspenderá o serviço WDS. Se você desabilitar essa opção, mas escolher a opção **Habilitar suporte a PXE para clientes**, o ponto de distribuição habilitará o WDS novamente.<!--1357580-->  

- **Exigir uma senha quando os computadores usarem PXE**: para fornecer segurança adicional para implantações PXE, especifique uma senha forte.  

- **Afinidade de dispositivo de usuário**: especifique como deseja que o ponto de distribuição associe usuários ao computador de destino para implantações PXE. Selecione uma das seguintes opções:  

  - **Permitir afinidade de dispositivo de usuário com aprovação automática**: selecione essa configuração para associar automaticamente os usuários ao computador de destino sem aguardar a aprovação.  

  - **Permitir afinidade de dispositivo de usuário pendente de aprovação de administrador**: escolha essa configuração para aguardar a aprovação de um usuário administrativo antes que os usuários sejam associados ao computador de destino.  

  - **Não permitir afinidade de dispositivo de usuário**: escolha essa configuração para especificar que os usuários não são associados ao computador de destino. Essa é a configuração padrão.  

    Para obter mais informações sobre afinidade de dispositivo de usuário, consulte [Vincular usuários e dispositivos com a afinidade de dispositivo de usuário](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).  

- **Adaptadores de rede**: especifique se o ponto de distribuição deve responder às solicitações PXE de todas as interfaces de rede ou de interfaces de rede específicas. Se o ponto de distribuição responde a adaptadores de rede específicos, forneça o endereço MAC de cada adaptador de rede.  

    > [!Note]  
    > Ao alterar o adaptador de rede, reinicie o serviço do WDS para garantir que ele salve a configuração corretamente. Começando na versão 1806, ao usar o serviço de respondente PXE, reinicie o **Serviço de Respondente PXE do ConfigMgr** (SccmPxe).<!--SCCMDocs issue 642-->  

- **Especificar o atraso de resposta do servidor PXE (segundos)**: ao usar vários servidores PXE, especifique quanto tempo esse ponto de distribuição habilitado para PXE deve esperar para responder às solicitações do computador. Por padrão, o ponto de distribuição habilitado para PXE do Configuration Manager responde imediatamente.  


### <a name="bkmk_config-multicast"></a> Multicast  

Especifique se é para habilitar o multicast no ponto de distribuição. As implantações multicast conservam a largura de banda da rede enviando dados simultaneamente a vários clientes do Configuration Manager. Sem o multicast, o servidor envia uma cópia dos dados para cada cliente em uma conexão separada. Para obter mais informações de como usar multicast para implantação de sistema operacional, confira [Usar o multicast para implantar o Windows na rede](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network).

Quando você habilita o multicast, o Configuration Manager instala o WDS (Serviços de Implantação do Windows) no servidor, se necessário.  

Selecione a opção para **Habilitar multicast para enviar dados a vários clientes simultaneamente** e, em seguida, defina as seguintes configurações:  

- **Conta de conexão multicast**: especifique uma conta a ser usada ao configurar conexões de banco de dados do Configuration Manager para multicast. Para obter mais informações, confira a [Conta de conexão multicast](/sccm/core/plan-design/hierarchy/accounts#multicast-connection-account).  

- **Configurações de endereço multicast**: especifique os endereços IP para enviar os dados aos computadores de destino. Por padrão, o endereço IP é obtido de um servidor DHCP que está habilitado para distribuir endereços multicast. Dependendo do ambiente de rede, é possível especificar um intervalo de endereços IP entre 239.0.0.0 e 239.255.255.255.  

    > [!IMPORTANT]  
    >  Os endereços IP que você configura precisam ser acessíveis pelos computadores de destino que solicitam a imagem do sistema operacional. Verifique se os roteadores e firewalls permitem tráfego multicast entre o computador de destino e o ponto de distribuição.  

- **Intervalo de portas UDP para multicast**: especifique o intervalo de portas UDP usadas para enviar os dados aos computadores de destino.  

    > [!IMPORTANT]  
    >  As portas UDP precisam estar acessíveis aos computadores de destino que solicitam a imagem do sistema operacional. Verifique se os roteadores e firewalls permitem o tráfego multicast entre o computador de destino e o servidor do site.  

- **Máximo de clientes**: especifique o número máximo de computadores de destino que pode baixar a imagem do sistema operacional desse ponto de distribuição.  

- **Habilitar multicast agendado**: especifique como o Configuration Manager é controlado ao iniciar a implantação de sistemas operacionais em computadores de destino. Configure as seguintes opções:  

    - **Atraso de início da sessão (minutos)**: especifique o número de minutos que o Configuration Manager espera antes de responder à primeira solicitação de implantação.  

    - **Tamanho mínimo da sessão (clientes)**: especifique quantas solicitações devem ser recebidas antes que o Configuration Manager comece a implantar o sistema operacional.  


> [!IMPORTANT]  
> Começando na versão 1806, para habilitar e configurar o multicast na guia **Multicast** das propriedades do ponto de distribuição, o ponto de distribuição precisa usar o Serviço de Implantação do Windows.  
> - Se você **Habilitar suporte a PXE para clientes** e **Habilitar multicast para enviar dados a vários clientes simultaneamente**, você não poderá **Habilitar um respondente PXE sem o Serviço de Implantação do Windows**.  
> - Se você **Habilitar suporte a PXE para clientes** e **Habilitar um respondente PXE sem o Serviço de Implantação do Windows**, você não poderá **Habilitar multicast para enviar dados a vários clientes simultaneamente**  


### <a name="bkmk_config-group"></a> Relacionamentos de grupo  

> [!NOTE]  
>  Essas opções estão disponíveis somente ao editar as propriedades de um ponto de distribuição instalado anteriormente.  

Gerencie os grupos de pontos de distribuição dos quais esse ponto de distribuição é membro.  

Para adicionar esse ponto de distribuição como membro a um grupo de pontos de distribuição existente, clique em **Adicionar**. Na janela Adicionar a Grupos de Pontos de Distribuição, selecione um grupo existente e clique em **OK**.  

Para remover esse ponto de distribuição de um grupo de pontos de distribuição, selecione o grupo na lista e, em seguida, clique em **Remover**.  


### <a name="bkmk_config-content"></a> Conteúdo  

> [!NOTE]  
>  Essas opções estão disponíveis somente ao editar as propriedades de um ponto de distribuição instalado anteriormente.  

Gerencie o conteúdo distribuído ao ponto de distribuição. Selecione na lista de pacotes de implantação e execute as seguintes ações:  

- **Validar**: inicie o processo para validar a integridade dos arquivos de conteúdo para o software. Para exibir os resultados do processo de validação de conteúdo, no workspace **Monitoramento**, expanda **Status da Distribuição**e escolha o nó **Status do Conteúdo**. Para obter mais informações, confira [Validar o conteúdo](/sccm/core/servers/deploy/configure/deploy-and-manage-content#validate-content).   

- **Redistribuir**: copia todos os arquivos de conteúdo do software selecionado para o ponto de distribuição e substitui os arquivos existentes. Essa ação pode ser usada para reparar arquivos de conteúdo. Para obter mais informações, confira [Redistribuir o conteúdo](/sccm/core/servers/deploy/configure/deploy-and-manage-content#redistribute-content).  

-   **Remover**: remove os arquivos de conteúdo do software do ponto de distribuição. Para obter mais informações, confira [Remover conteúdo](/sccm/core/servers/deploy/configure/deploy-and-manage-content#remove-content).    


### <a name="bkmk_config-valid"></a> Validação de conteúdo  

Defina um agendamento para validar a integridade dos arquivos de conteúdo no ponto de distribuição. Quando você habilita a validação de conteúdo segundo um agendamento, o Configuration Manager inicia o processo no horário agendado. Ele verifica todo o conteúdo no ponto de distribuição. Também é possível configurar a prioridade da validação de conteúdo. Por padrão, a prioridade é definida como **Mais Baixa**. O aumento da prioridade pode aumentar o uso do processador e do disco no servidor durante o processo de validação, mas o processo é concluído com mais rapidez. 

Para exibir os resultados do processo de validação de conteúdo, no workspace **Monitoramento**, expanda **Status da Distribuição**e escolha o nó **Status do Conteúdo**. Ele mostra o conteúdo para cada tipo de software, por exemplo, aplicativo, pacote de atualização de software e imagem de inicialização.  

> [!WARNING]  
>  Embora você especifique o cronograma de validação de conteúdo usando o horário local do computador, o console do Configuration Manager mostra o cronograma em UTC.  

Para obter mais informações, confira [Validar o conteúdo](/sccm/core/servers/deploy/configure/deploy-and-manage-content#validate-content).


### <a name="bkmk_config-boundary"></a> Boundary groups  

Gerencie os grupos de limites aos quais você deseja atribuir esse ponto de distribuição. Adicione o ponto de distribuição a pelo menos um grupo de limites. Durante a implantação do conteúdo, os clientes devem estar em um grupo de limites associado a um ponto de distribuição para usá-lo como local de origem do conteúdo.

Configure as *relações* do grupo de limites que definem quanto e em quais grupos de limites um cliente pode fazer fallback para encontrar o conteúdo. Para obter mais informações, consulte [Grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).

Clique em **Adicionar** e selecione um grupo de limites existente na lista.

Para criar um grupo de limites para esse ponto de distribuição, clique em **Criar**. Para obter mais informações de como criar e configurar um grupo de limites, confira [Procedimentos para grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups#procedures-for-boundary-groups).

Quando você estiver editando as propriedades de um ponto de distribuição já instalado, gerencie a opção para **Habilitar para distribuição sob demanda**. Essa opção permite que o Configuration Manager distribua o conteúdo automaticamente para esse servidor quando um cliente o solicita. Para obter mais informações, confira [Distribuição de conteúdo sob demanda](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#on-demand-content-distribution).


### <a name="bkmk_config-sched"></a> Agendamento  

> [!NOTE]  
>  Essas opções estão disponíveis somente ao editar as propriedades de um ponto de distribuição instalado anteriormente. 
> 
>  Essa guia está disponível somente quando você edita as propriedades de um ponto de distribuição remoto em relação ao servidor do site.  

Configure um agendamento que restringe quando o Configuration Manager pode transferir dados para o ponto de distribuição. Restrinja os dados por prioridade ou feche a conexão por períodos de tempo selecionados.   

Para restringir dados, selecione o período de tempo na grade e, em seguida, escolha uma das seguintes configurações de **Disponibilidade**:  

- **Aberto para todas as prioridades**: o Configuration Manager envia dados para o ponto de distribuição sem restrições. Essa é a configuração padrão para todos os períodos de tempo.  

- **Permitir prioridade média e alta**: o Configuration Manager envia somente dados de média e alta prioridade ao ponto de distribuição.  

- **Permitir alta prioridade apenas**: o Configuration Manager envia somente dados de alta prioridade ao ponto de distribuição.  

- **Fechado**: o Configuration Manager não envia dados ao ponto de distribuição.  

Configure a **Prioridade de distribuição** do software na guia **Configurações de Distribuição** das propriedades do software. 

> [!IMPORTANT]  
>  A agenda se baseia no fuso horário do site de envio, não do ponto de distribuição.  


### <a name="bkmk_config-rate"></a> Limites de taxa  

> [!NOTE]  
>  Essas opções estão disponíveis somente ao editar as propriedades de um ponto de distribuição instalado anteriormente.  
>   
>  Essa guia está disponível somente quando você edita as propriedades de um ponto de distribuição remoto em relação ao servidor do site.  

Configure limites de taxa para controlar a largura de banda de rede que o Configuration Manager usa para transferir o conteúdo ao ponto de distribuição. Escolha dentre as seguintes opções:  

- **Ilimitado ao enviar para este destino**: o Configuration Manager envia conteúdo ao ponto de distribuição sem restrições de limites de taxas. Essa é a configuração padrão.  

- **Modo de pulso**: essa opção especifica o tamanho dos blocos de dados que o servidor do site envia para o ponto de distribuição. Você também pode especificar um retardo de tempo entre o envio de cada bloco de dados. Use essa opção quando você deve enviar dados através de uma conexão de rede com largura de banda bem baixa para o ponto de distribuição. Por exemplo, é possível especificar a restrição de enviar 1 KB de dados a cada cinco segundos, independentemente da velocidade do link ou de seu uso em um determinado momento.  

- **Limitado a taxas máximas de transferência especificadas por hora**: especifique essa configuração para que um site envie dados para um ponto de distribuição usando somente a porcentagem de tempo que você define. Quando você usa essa opção, o Configuration Manager não identifica a largura de banda disponível da rede. Nesse caso, ele divide o tempo em que pode enviar dados. O servidor envia dados por um curto período de tempo, seguido por períodos de tempo em que os dados não são enviados. Por exemplo, se você definir **Limitar largura de banda disponível** a **50%**, o Configuration Manager transmitirá dados por um período de tempo seguido de igual período de tempo igual em que nenhum dado é enviado. O tamanho real da quantidade de dados ou o tamanho do bloco de dados não é gerenciado. Ele gerencia apenas o período de tempo durante o qual envia dados.  
