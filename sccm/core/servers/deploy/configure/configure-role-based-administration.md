---
title: Configurar administração baseada em funções
titleSuffix: Configuration Manager
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 57413dd3-b2f8-4a5f-b27f-8464d357caff
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 73583d4dea93cefcbe9dd9615671606112cc8860
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65498941"
---
# <a name="configure-role-based-administration-for-configuration-manager"></a>Configurar administração baseada em funções para o Configuration Manager   

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

No Configuration Manager, a administração baseada em funções combina funções de segurança, escopos de segurança e coleções atribuídas para definir o escopo administrativo de cada usuário administrativo. Um escopo administrativo inclui os objetos que um usuário administrativo pode exibir no console do Configuration Manager e as tarefas relacionadas a esses objetos que o usuário administrativo tem permissão para realizar. As configurações de administração baseada em funções são aplicadas em cada site de uma hierarquia.  

 Se ainda não estiver familiarizado com os conceitos da administração baseada em funções, consulte [Fundamentos da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration).  

 As informações contidas nos procedimentos a seguir podem ajudá-lo a criar e configurar a administração baseada em funções e as configurações de segurança relacionadas:  

-   [Criar funções de segurança personalizadas](#BKMK_CreateSecRole)  

-   [Configurar funções de segurança](#BKMK_ConfigSecRole)  

-   [Configurar escopos de segurança para um objeto](#BKMK_ConfigSecScope)  

-   [Configurar coleções para gerenciar a segurança](#BKMK_ConfigColl)  

-   [Criar um novo usuário administrativo](#BKMK_Create_AdminUser)  

-   [Modificar o escopo administrativo de um usuário administrativo](#BKMK_ModAdminUser)  

##  <a name="BKMK_CreateSecRole"></a> Criar funções de segurança personalizadas  
 O Configuration Manager oferece várias funções de segurança internas. Se necessitar de funções de segurança adicionais, você poderá criar uma função de segurança personalizada criando a cópia de uma função de segurança existente e modificando essa cópia. Você pode criar uma função de segurança personalizada para conceder aos usuários administrativos as permissões de segurança adicionais de que eles necessitam e que não estão incluídas atualmente em uma função de segurança atribuída. Usando uma função de segurança personalizada, você pode conceder a eles somente as permissões de que eles precisam e impedir a atribuição de uma função de segurança que conceda mais permissões do que eles precisam.  

 Use o procedimento a seguir para criar uma nova atribuição de segurança usando uma função de segurança existente como modelo.  

#### <a name="to-create-custom-security-roles"></a>Para criar funções de segurança personalizadas  

1.  No console do Configuration Manager, acesse **Administração**.  

2.  No workspace **Administração**, expanda **Segurança**e selecione **Funções de Segurança**.  

     Use um dos seguintes processos para criar a nova função de segurança:  

    -   Para criar uma nova função de segurança personalizada, execute as seguintes ações:  

        1.  Selecione uma função de segurança existente para usar como origem para a nova função de segurança.  

        2.  Na guia **Início**, no grupo **Função de Segurança**, escolha **Copiar**. Essa ação criará uma cópia da função de segurança original.  

        3.  No assistente Copiar Função de Segurança, especifique um **Nome** para a nova função de segurança personalizada.  

        4.  Em **Atribuições de operações de segurança**, expanda cada nó **Operações de Segurança** para exibir as ações disponíveis.  

        5.  Para alterar a configuração de uma operação de segurança, escolha a seta para baixo na coluna **Valor** e escolha **Sim** ou **Não**.  

            > [!CAUTION]  
            >  Ao configurar uma atribuição de segurança personalizada, não conceda permissões que não sejam exigidas pelos usuários administrativos associados à nova função de segurança. Por exemplo, o valor **Modificar** da operação de segurança **Funções de Segurança** concede aos usuários administrativos permissão para editar qualquer função de segurança acessível, mesmo que eles não estejam associados a essa função de segurança.  

        6.  Após configurar as permissões, escolha **OK** para salvar a nova função de segurança.  

    -   Para importar uma função de segurança exportada de outra hierarquia do Configuration Manager, execute as seguintes ações:  

        1.  Na guia **Início**, no grupo **Criar**, escolha **Importar Função de Segurança**.  

        2.  Especifique o arquivo .xml que contém a configuração da função de segurança que você deseja importar. Escolha **Abrir** para concluir o procedimento e salvar a função de segurança.  

            > [!NOTE]  
            >  Após importar uma função de segurança, você poderá editar as propriedades dessa função para alterar as permissões de objeto associadas a ela.  

##  <a name="BKMK_ConfigSecRole"></a> Configurar funções de segurança  
 Os grupos de permissões de segurança definidos para uma função de segurança são chamados de atribuições de operação de segurança. As atribuições de operação de segurança representam uma combinação de tipos de objetos e ações que estão disponíveis para cada tipo de objeto. Você pode modificar as operações de segurança disponíveis para qualquer função de segurança personalizada, mas não é possível modificar as funções de segurança internas que o Configuration Manager fornece.  

 Use o procedimento a seguir para modificar as operações de segurança para uma função de segurança.  

#### <a name="to-modify-security-roles"></a>Para modificar as funções de segurança  

1.  No console do Configuration Manager, escolha **Administração**.  

2.  No workspace **Administração**, expanda **Segurança**e selecione **Funções de Segurança**.  

3.  Selecione a função de segurança personalizada que deseja modificar.  

4.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

5.  Escolha a guia **Permissões**.  

6.  Em **Atribuições de operações de segurança**, expanda cada nó **Operações de Segurança** para exibir as ações disponíveis.  

7.  Para alterar a configuração de uma operação de segurança, escolha a seta para baixo na coluna **Valor** e escolha **Sim** ou **Não**.  

    > [!CAUTION]  
    >  Ao configurar uma atribuição de segurança personalizada, não conceda permissões que não sejam exigidas pelos usuários administrativos associados à nova função de segurança. Por exemplo, o valor **Modificar** da operação de segurança **Funções de Segurança** concede aos usuários administrativos permissão para editar qualquer função de segurança acessível, mesmo que eles não estejam associados a essa função de segurança.  

8.  Após concluir a configuração das atribuições de operação de segurança, escolha **OK** para salvar a nova atribuição de segurança.  

##  <a name="BKMK_ConfigSecScope"></a> Configurar escopos de segurança para um objeto  
 Você gerencia a associação de um escopo de segurança para um objeto por meio do objeto, não por meio do escopo de segurança. As únicas configurações diretas para as quais os escopos de segurança oferecem suporte são as alterações de nome e descrição. Para alterar o nome e a descrição de um escopo de segurança ao exibir as propriedades dele, é necessário ter a permissão **Modificar** para o objeto protegível dos **Escopos de Segurança** .  

 Ao criar um novo objeto no Configuration Manager, ele é associado a cada escopo de segurança que está vinculado às funções de segurança da conta usada para criar o objeto. Esse comportamento ocorre quando essas funções de segurança fornecem as permissões **Criar** ou **Definir Escopo de Segurança**. Você pode alterar os escopos de segurança do objeto após sua criação.  

 Por exemplo, foi atribuída a você uma função de segurança que lhe concede permissão para criar um novo grupo de limites. Quando você cria um novo grupo de limites, você não tem opção à qual você possa atribuir escopos de segurança específicos. Em vez disso, os escopos de segurança disponíveis nas funções de segurança às quais você está associado são automaticamente atribuídos ao novo grupo de limites. Após salvar o novo grupo de limites, você poderá editar os escopos de segurança associados a ele.  

 Use o procedimento a seguir para configurar os escopos de segurança atribuídos a um objeto.  

#### <a name="to-configure-security-scopes-for-an-object"></a>Para configurar escopos de segurança para um objeto  

1.  No console do Configuration Manager, selecione um objeto que dê suporte à atribuição a um escopo de segurança.  

2.  Na guia **Início**, no grupo **Classificar**, escolha **Definir Escopos de Segurança**.  

3.  Na caixa de diálogo **Definir Escopos de Segurança** , selecione ou apague os escopos de segurança aos quais esse objeto está associado. Cada objeto que oferece suporte a escopos de segurança deve ser atribuído a pelo menos um escopo de segurança.  

4.  Escolha **OK** para salvar os escopos de segurança atribuídos.  

    > [!NOTE]  
    >  Quando você cria um novo objeto, você pode atribuí-lo a vários escopos de segurança. Para modificar o número de escopos de segurança associados ao objeto, é necessário alterar essa atribuição após a criação do objeto.  

##  <a name="BKMK_ConfigColl"></a> Configurar coleções para gerenciar a segurança  
 Não existem procedimentos para configurar coleções para a administração baseada em funções. As coleções não têm uma configuração de administração baseada em função. Em vez disso, você atribui coleções a um usuário administrativo ao configurar o usuário administrativo. As operações de segurança da coleção permitidas nas funções de segurança atribuídas aos usuários determinam as permissões que um usuário administrativo tem para coleções e recursos da coleção (membros da coleção).  

 Quando um usuário administrativo possui permissões para uma coleção, ele também tem permissões para coleções que estão limitadas a essa coleção. Por exemplo, sua organização usa uma coleção chamada Todos os Desktops. Também há uma coleção chamada Todos os Desktops da América do Norte, que está limitada à coleção Todos os Desktops. Se um usuário administrativo tiver permissões para Todos os Desktops, ele também terá as mesmas permissões para a coleção Todos os Desktops da América do Norte.

 Além disso, um usuário administrativo não pode usar as permissões **Excluir** ou **Modificar** em uma coleção que está diretamente atribuída a ele. Porém, podem usar essas permissões nas coleções que estão limitadas a essa coleção. No exemplo anterior, o usuário administrativo pode excluir ou modificar a coleção Todos os Desktops da América do Norte, mas não pode excluir ou modificar a coleção Todos os Desktops.  

##  <a name="BKMK_Create_AdminUser"></a> Criar um novo usuário administrativo  
 Para conceder acesso para gerenciar o Configuration Manager a indivíduos ou membros de um grupo de segurança, crie um usuário administrativo no Configuration Manager e especifique a conta do Windows do Usuário ou Grupo de Usuários. Cada usuário administrativo no Configuration Manager deve receber a atribuição de pelo menos uma função de segurança e um escopo de segurança. Você também pode atribuir coleções para limitar o escopo administrativo do usuário administrativo.  

 Use os procedimentos a seguir para criar novos usuários administrativos.  

#### <a name="to-create-a-new-administrative-user"></a>Para criar um novo usuário administrativo  

1.  No console do Configuration Manager, escolha **Administração**.  

2.  No workspace **Administração**, expanda **Segurança**e escolha **Usuários Administrativos**.  

3.  Na guia **Início**, no grupo **Criar**, escolha **Adicionar Usuário ou Grupo**.  

4.  Escolha **Procurar** e selecione a conta de usuário ou grupo a ser usada para esse novo usuário administrativo.  

    > [!NOTE]  
    >  Para a administração baseada em console, somente os usuários de domínio ou grupos de segurança podem ser especificados como um usuário administrativo.  

5.  Para **Funções de segurança associadas**, escolha **Adicionar** para abrir uma lista das funções de segurança disponíveis, marque a caixa de uma ou mais funções de segurança e escolha **OK**.  

6.  Escolha uma das duas opções a seguir para definir o comportamento de objeto protegível para o novo usuário:  

    -   **Todas as instâncias dos objetos relacionados às funções de segurança atribuídas**: essa opção associa o usuário administrativo ao escopo de segurança **Todos** e às coleções **Todos os Sistemas** e **Todos os Usuários e Grupos de Usuários**. As funções de segurança que são atribuídas ao usuário definem o acesso a objetos. Os novos objetos que esse usuário administrativo cria são atribuídos ao escopo de segurança **Padrão** .  

    -   **Somente as instâncias de objetos que estiverem atribuídas a coleções ou escopos de segurança especificados**: por padrão, essa opção associa o usuário administrativo ao escopo de segurança **Padrão** e a coleções de **Todos os sistemas** e **Todos os usuários e Grupos de usuários**. No entanto, os escopos de segurança e as coleções atuais são limitados aos que estão associados à conta que você usou para criar o novo usuário administrativo. Essa opção oferece suporte à adição ou remoção de escopos de segurança e coleções para personalizar o escopo administrativo do usuário administrativo.  

    > [!IMPORTANT]  
    >  As opções anteriores associam cada escopo de segurança e coleção associados a cada função de segurança atribuída ao usuário administrativo. Você pode usar uma terceira opção, **Associar funções de segurança atribuídas a escopos e coleções de segurança específicos**, para associar funções de segurança individuais a escopos e coleções de segurança específicos. Essa terceira opção fica disponível com a criação do novo usuário administrativo, quando você modifica o usuário administrativo.  

7.  Dependendo da sua seleção na etapa 6, execute a seguinte ação:  

    -   Se tiver selecionado **Todas as instâncias dos objetos relacionados às funções de segurança atribuídas**, escolha **OK** para concluir esse procedimento.  

    -   Se tiver selecionado **Somente instâncias de objetos atribuídas aos escopos e às coleções de segurança especificados**, é possível escolher **Adicionar** para selecionar coleções e escopos de segurança adicionais. Ou selecione um ou mais objetos na lista e escolha **Remover** para removê-los. Escolha **OK** para concluir esse procedimento.  

##  <a name="BKMK_ModAdminUser"></a> Modificar o escopo administrativo de um usuário administrativo  
 É possível modificar o escopo administrativo de um usuário administrativo ao adicionar ou remover funções de segurança, escopos de segurança e coleções que estão associados ao usuário. Cada usuário administrativo deve ser associado a pelo menos uma função de segurança e um escopo de segurança. Talvez você precise atribuir uma ou mais coleções para o escopo administrativo do usuário. A maioria das funções de segurança interage com as coleções e não funciona corretamente sem uma coleção atribuída.  

 Ao modificar um usuário administrativo, você pode alterar o comportamento de como os objetos protegíveis são associados às funções de segurança atribuídas. Os três comportamentos que podem ser selecionados são:  

-   **Todas as instâncias dos objetos relacionados às funções de segurança atribuídas**: essa opção associa o usuário administrativo ao escopo **Todos** e às coleções **Todos os Sistemas** e **Todos os Usuários e Grupos de Usuários**. As funções de segurança que são atribuídas ao usuário definem o acesso a objetos.  

-   **Somente as instâncias de objetos que estiverem atribuídas a coleções ou escopos de segurança especificados**: essa opção associa o usuário administrativo aos mesmos escopos de segurança e coleções que estão associados à conta que você usa para configurar o usuário administrativo. Essa opção oferece suporte à adição ou remoção de funções de segurança e coleções para personalizar o escopo administrativo do usuário administrativo.  

-   **Associar funções de segurança atribuídas a coleções e escopos de segurança específicos**: essa opção permite que você crie as associações específicas entre as funções de segurança individuais, os escopos de segurança e as coleções específicas do usuário.  

    > [!NOTE]  
    >  Essa opção está disponível somente quando você modifica as propriedades de um usuário administrativo.  

A configuração atual para o comportamento de objeto protegível altera o processo que você usa para atribuir as funções de segurança adicionais. Use os procedimentos a seguir que são baseados em opções diferentes para objetos protegíveis a fim de ajudá-lo a gerenciar um usuário administrativo.  

Use o procedimento a seguir para exibir e gerenciar a configuração de objetos protegíveis para um usuário administrativo.  

#### <a name="to-view-and-manage-the-securable-object-behavior-for-an-administrative-user"></a>Para exibir e gerenciar o comportamento do objeto protegível para um usuário administrativo  

1.  No console do Configuration Manager, escolha **Administração**.  

2.  No workspace **Administração**, expanda **Segurança**e escolha **Usuários Administrativos**.  

3.  Selecione o usuário administrativo que deseja modificar.  

4.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

5.  Escolha a guia **Escopos de Segurança** para exibir a configuração atual de objetos protegíveis para esse usuário administrativo.  

6.  Para modificar o comportamento do objeto protegível, selecione uma nova opção para o comportamento do objeto protegível. Após alterar essa configuração, confira o procedimento apropriado para obter diretrizes sobre como configurar os escopos de segurança, as coleções e as funções de segurança para esse usuário administrativo.  

7.  Escolha **OK** para concluir o procedimento.  

Use o procedimento a seguir para modificar um usuário administrativo que tem o comportamento de objeto passível de proteção definido como **Todas as instâncias de objetos relacionadas às funções de segurança atribuídas**.  

#### <a name="for-option-all-instances-of-the-objects-that-are-related-to-the-assigned-security-roles"></a>Para a opção: Todas as instâncias dos objetos relacionados às funções de segurança atribuídas  

1.  No console do Configuration Manager, escolha **Administração**.  

2.  No workspace **Administração**, expanda **Segurança**e escolha **Usuários Administrativos**.  

3.  Selecione o usuário administrativo que deseja modificar.  

4.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

5.  Escolha a guia **Escopos de Segurança** para confirmar se o usuário administrativo está configurado para **Todas as instâncias de objetos relacionadas às funções de segurança atribuídas**.  

6.  Para modificar as funções de segurança atribuídas, escolha a guia **Funções de Segurança**.  

    -   Para atribuir funções de segurança adicionais a esse usuário administrativo, escolha **Adicionar**, marque a caixa de cada função de segurança adicional que você deseja atribuir e escolha **OK**.  

    -   Para remover as funções de segurança, selecione uma ou mais funções de segurança da lista e escolha **Remover**.  

7.  Para modificar o comportamento de objeto protegível, escolha a guia **Escopos de Segurança** e escolha a nova opção para o comportamento de objeto protegível. Após alterar essa configuração, confira o procedimento apropriado para obter diretrizes sobre como configurar os escopos de segurança, as coleções e as funções de segurança para esse usuário administrativo.  

    > [!NOTE]  
    >  Quando o comportamento de objeto passível de proteção está definido como **Todas as instâncias de objetos relacionadas às funções de segurança atribuídas**, você não pode adicionar ou remover coleções e escopos de segurança específicos.  

8.  Escolha **OK** para concluir esse procedimento.  

Use o procedimento a seguir para modificar um usuário administrativo que tem o comportamento de objeto passível de proteção definido como **Somente instâncias de objetos atribuídas aos escopos e às coleções de segurança especificadas**.  

#### <a name="for-option-only-the-instances-of-objects-that-are-assigned-to-the-specified-security-scopes-and-collections"></a>Para a opção: Somente as instâncias de objetos que estiverem atribuídas a coleções ou escopos de segurança especificados  

1.  No console do Configuration Manager, escolha **Administração**.  

2.  No workspace **Administração**, expanda **Segurança**e escolha **Usuários Administrativos**.  

3.  Selecione o usuário administrativo que deseja modificar.  

4.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

5.  Escolha a guia **Escopos de Segurança** para confirmar se o usuário está configurado para **Somente instâncias de objetos atribuídas aos escopos e às coleções de segurança especificadas**.  

6.  Para modificar as funções de segurança atribuídas, escolha a guia **Funções de Segurança**.  

    -   Para atribuir funções de segurança adicionais a esse usuário, escolha **Adicionar**, marque a caixa de cada função de segurança adicional que você deseja atribuir e escolha **OK**.  

    -   Para remover as funções de segurança, selecione uma ou mais funções de segurança da lista e escolha **Remover**.  

7.  Para modificar os escopos de segurança e as coleções associadas a funções de segurança, escolha a guia **Escopos de Segurança**.  

    -   Para associar novos escopos de segurança ou coleções com todas as funções de segurança que estão atribuídos a esse usuário administrativo, escolha **Adicionar** e selecione uma das quatro opções. Se você selecionar **Escopo de Segurança** ou **Coleção**, marque a caixa para um ou mais objetos para concluir essa seleção e escolha **OK**.  

    -   Para remover uma coleção ou um escopo de segurança, escolha o objeto e escolha **Remover**.  

8.  Escolha **OK** para concluir esse procedimento.  

Use o procedimento a seguir para modificar um usuário administrativo que tem o comportamento de objeto passível de proteção definido como **Associar funções de segurança atribuídas a escopos e coleções de segurança específicos**.  

#### <a name="for-option-associate-assigned-security-roles-with-specific-security-scopes-and-collections"></a>Para a opção: Associar funções de segurança atribuídas a coleções e escopos de segurança específicos  

1.  No console do Configuration Manager, escolha **Administração**.  

2.  No workspace **Administração**, expanda **Segurança**e escolha **Usuários Administrativos**.  

3.  Selecione o usuário administrativo que deseja modificar.  

4.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

5.  Escolha a guia **Escopos de Segurança** para confirmar se o usuário administrativo está configurado para **Associar funções de segurança atribuídas a escopos e coleções de segurança específicos**.  

6.  Para modificar as funções de segurança atribuídas, escolha a guia **Funções de Segurança**.  

    -   Para atribuir funções de segurança adicionais para esse usuário administrativo, escolha **Adicionar**. Na caixa de diálogo **Adicionar Função de Segurança**, selecione uma ou mais funções de segurança disponíveis, escolha **Adicionar** e selecione um tipo de objeto para associar a funções de segurança selecionadas. Se você selecionar **Escopo de Segurança** ou **Coleção**, marque a caixa para um ou mais objetos para concluir essa seleção e escolha **OK**.  

        > [!NOTE]  
        >  Você deve configurar pelo menos um escopo de segurança antes das funções de segurança selecionadas poder ser atribuídas ao usuário administrativo. Quando você seleciona várias funções de segurança, cada escopo de segurança e coleção que você configura está associado a cada uma das funções de segurança selecionadas.  

    -   Para remover as funções de segurança, selecione uma ou mais funções de segurança da lista e escolha **Remover**.  

7.  Para modificar os escopos de segurança e as coleções associados a uma função de segurança específica, escolha a guia **Escopos de Segurança**, selecione a função de segurança e escolha **Editar**.  

    -   Para associar novos objetos a essa função de segurança, escolha **Adicionar** e selecione um tipo de objeto para associar a funções de segurança selecionadas. Se você selecionar **Escopo de Segurança** ou **Coleção**, marque a caixa para um ou mais objetos para concluir essa seleção e escolha **OK**.  

        > [!NOTE]  
        >  Você deve configurar pelo menos um escopo de segurança.  

    -   Para remover uma coleção ou escopo de segurança que está associado a essa função de segurança, selecione o objeto e escolha **Remover**.  

    -   Modificados os objetos associados, escolha **OK**.  

8.  Escolha **OK** para concluir esse procedimento.  

    > [!CAUTION]  
    >  Quando uma função de segurança concede a usuários administrativos a permissão de implantação de coleção, os usuários administrativos podem distribuir objetos a partir de qualquer escopo de segurança para os quais eles têm permissões de **leitura** de objetos, mesmo se o escopo de segurança esteja associado a uma função de segurança diferente.  
