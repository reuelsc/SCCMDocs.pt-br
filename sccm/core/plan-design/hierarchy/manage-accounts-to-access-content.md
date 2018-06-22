---
title: Contas para acessar conteúdo
titleSuffix: Configuration Manager
description: Saiba mais sobre as contas em que os clientes acessam conteúdo do System Center Configuration Manager.
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a7df9d0f-fbde-47eb-97e7-3d29536424fa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c21601246cb0024837256b7cf8d4c1576c00149d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32338679"
---
# <a name="manage-accounts-to-access-content-in-system-center-configuration-manager"></a>Gerenciar contas para acessar conteúdo | System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Antes de implantar o conteúdo no System Center Configuration Manager, considere como os clientes acessarão esse conteúdo nos pontos de distribuição. Este artigo descreve as seguintes contas usadas para essa finalidade:

-   **Conta de acesso à rede**. Usada pelos clientes para conectar a um ponto de distribuição e acessar o conteúdo. Por padrão, os clientes tentarão primeiro a conta do computador.

     Essa conta também é usada pelos pontos de distribuição de recepção para obter o conteúdo de um ponto de distribuição de origem em uma floresta remota.  

-   **Conta de Acesso ao Pacote**. Por padrão, o Configuration Manager concede acesso ao conteúdo em um ponto de distribuição para as contas internas chamadas de **Usuários** e **Administradores**. Você pode configurar permissões adicionais para restringir o acesso.  

-   **Conta de Conexão Multicast**. Usada para implantações de sistema operacional.  

##  <a name="bkmk_NAA"></a> Conta de acesso à rede  
 Os computadores cliente usam a Conta de acesso à rede quando não podem usar a conta do computador local para acessar conteúdo em pontos de distribuição. Por exemplo, isso se aplica a clientes do grupo de trabalho e computadores de domínios não confiáveis. Essa conta também pode ser usada durante a implantação do sistema operacional quando o computador que está instalando o sistema operacional ainda não tem uma conta de computador no domínio.  

-   Os clientes usam somente a conta de acesso à rede para acessar recursos na rede.  

-   Você pode configurar várias contas para usar como Conta de acesso à rede em cada site primário.  

-   Os clientes primeiro tentam acessar o conteúdo em um ponto de distribuição usando a conta *nomecomputador*$. Se essa conta falhar, eles tentarão usar uma Conta de acesso à rede. Os clientes continuam tentando usar a Conta de acesso à rede mesmo que tenha falhado anteriormente.  

### <a name="permissions"></a>Permissões
Conceda a essa conta as permissões mínimas adequadas que o cliente necessita para acessar o software para o conteúdo que o cliente necessita.  

-   A conta deve ter o direito de **Acesso a este computador pela rede** no ponto de distribuição.  

-   Crie a conta em qualquer domínio que forneça o acesso necessário aos recursos. A conta de acesso à rede deve incluir sempre um nome de domínio. Não há suporte para segurança de passagem para essa conta. Se houver pontos de distribuição em vários domínios, crie a conta em um domínio confiável.  

> [!TIP]  
>  Para evitar bloqueios de conta, não altere a senha em uma conta de acesso à rede existente. Em vez disso, crie uma nova conta e configure-a no Configuration Manager. Quando tiver passado tempo suficiente para que todos os clientes recebam os detalhes da nova conta, remova a conta antiga das pastas de rede compartilhadas e exclua-a.  

> [!IMPORTANT]  
>  Não conceda a essa conta direitos interativos de logon.  
>   
>  Não conceda a essa conta o direito de ingressar computadores ao domínio. Se tiver de adicionar computadores ao domínio durante uma sequência de tarefas, use a Conta de Adição de Domínio do Editor de Sequência de Tarefas.  

### <a name="to-configure-the-network-access-account"></a>Para configurar a conta de acesso à rede  

1.  No console do Configuration Manager, clique em **Administração** >   **Configuração do Site** >  **Sites** e selecione o site.  

2.  No grupo **Configurações**, clique em **Configurar componentes do site** > **Distribuição de software**.  

3.  Clique na guia **Conta de acesso à rede**. Configure uma ou mais contas e clique em **OK**.  

##  <a name="bkmk_Paa"></a> Contas de Acesso ao Pacote  
 As Contas de Acesso ao Pacote possibilitam definir permissões do sistema de arquivos NTFS para especificar usuários e grupos de usuários que podem acessar o conteúdo do pacote em pontos de distribuição. Por padrão, o Configuration Manager concede acesso somente a contas de **Usuários** e **Administradores** genéricas. Entretanto, você pode controlar o acesso a computadores cliente usando contas ou grupos do Windows adicionais. Os dispositivos móveis sempre recuperam o conteúdo do pacote anonimamente e, portanto, não usam as Contas de Acesso ao Pacote.  

 Por padrão, quando o Configuration Manager copia os arquivos de conteúdo de um pacote para um ponto de distribuição, ele concede acesso de **Leitura** ao grupo local **Usuários** e **Controle Total** ao grupo local **Administradores**. As permissões reais necessárias dependerão do pacote. Se houver clientes em grupos de trabalho ou em florestas não confiáveis, os clientes usarão a Conta de Acesso à Rede para acessar o conteúdo do pacote. Verifique se a Conta de Acesso à Rede tem permissões para o pacote usando as Contas de Acesso ao Pacote definidas.  

 Use contas em um domínio que possa acessar os pontos de distribuição. Se você criar ou modificar a conta após a criação do pacote, deverá redistribuir o pacote. A atualização do pacote não altera as permissões do sistema de arquivos NTFS no pacote.  

 Não é necessário adicionar a Conta de Acesso à Rede como Conta de Acesso ao Pacote, pois a associação do grupo **Usuários** a adiciona automaticamente. Restringir a Conta de Acesso de Pacote somente à Conta de Acesso à Rede não impede que clientes acessem o pacote.  

### <a name="to-manage-access-accounts"></a>Para gerenciar as contas de acesso  

1.  No console do Configuration Manager, escolha **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de software**, determine o tipo de conteúdo para o qual você deseja gerenciar as contas de acesso e siga as etapas fornecidas:  

    -   **Aplicativos**: expanda **Gerenciamento de aplicativos**, clique em **Aplicativos** e selecione os aplicativos para os quais você quer gerenciar as contas de acesso.  

    -   **Pacotes**: expanda **Gerenciamento de aplicativos**, clique em **Pacotes** e selecione os pacotes para os quais você quer gerenciar as contas de acesso.  

    -   **Pacotes de implantação**: expanda **Atualizações de software**, clique em **Pacotes de implantação** e selecione os pacotes de implantação para os quais você quer gerenciar as contas de acesso.  

    -   **Pacotes de driver**: expanda **Sistemas operacionais**, clique em **Pacotes de driver** e selecione os pacotes de drivers para os quais você quer gerenciar as contas de acesso.  

    -   **Imagens do sistema operacional**: expanda **Sistemas operacionais**, clique em **Imagens do sistema operacional** e selecione as imagens do sistema operacional para as quais você quer gerenciar as contas de acesso.  

    -   **Instaladores de sistema operacional**: expanda **Sistemas operacionais**, clique em **Instaladores de sistema operacional** e selecione os instaladores de sistema operacional para os quais você quer gerenciar as contas de acesso.  

    -   **Imagens de inicialização**: expanda **Sistemas operacionais**, clique em **Imagens de inicialização** e selecione as imagens de inicialização para as quais você quer gerenciar as contas de acesso.  

3.  Clique com o botão direito no objeto selecionado e clique em **Gerenciar Contas de Acesso**.  

4.  Na caixa de diálogo **Adicionar Conta** , especifique o tipo de conta que receberá permissão de acesso ao conteúdo e os direitos de acesso associados à conta.  

    > [!NOTE]  
    >  Quando você adiciona um nome de usuário para a conta e o Configuration Manager encontra uma conta de usuário local e uma conta de usuário de domínio com esse nome, o Configuration Manager estabelece direitos de acesso para a conta de usuário de domínio.  

##  <a name="bkmk_multi"></a> Conta de Conexão Multicast  
 A Conta de Conexão Multicast é usada por pontos de distribuição configurados para multicast, para ler as informações do banco de dados do site.  

-   Especifique uma conta a ser usada ao configurar conexões de banco de dados do Configuration Manager para multicast.  

-   Por padrão, é usada a conta do computador do ponto de distribuição, mas você pode configurar uma conta de usuário, em vez disso.  

-   Você deve especificar uma conta de usuário sempre que o banco de dados do site estiver em uma floresta não confiável.  

-   A conta deve ter permissões de **Leitura** para o banco de dados do site.  

Por exemplo, se o seu centro de dados tiver uma rede de perímetro em uma floresta diferente do servidor e do banco de dados do site, você poderá usar essa conta para ler as informações multicast do banco de dados do site.

Se você criar essa conta, crie-a com direitos limitados, a conta local no computador que executa o Microsoft SQL Server.  

> [!IMPORTANT]  
>  Não conceda a essa conta direitos interativos de logon.  
