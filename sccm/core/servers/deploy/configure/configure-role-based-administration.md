---
title: "Configurar administração baseada em função | Microsoft Docs"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 57413dd3-b2f8-4a5f-b27f-8464d357caff
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: fb5a3cb9fc5aebf512f09a2e584c1eee58b2d15a


---
# <a name="configure-role-based-administration-for-system-center-configuration-manager"></a>Configurar administração baseada em função para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

No System Center Configuration Manager, a administração baseada em funções combina funções de segurança, escopos de segurança e coleções atribuídas para definir o escopo administrativo para cada usuário administrativo. Um escopo administrativo inclui os objetos que um usuário administrativo pode exibir no console do Configuration Manager e as tarefas relacionadas a esses objetos que o usuário administrativo tem permissão para realizar. As configurações de administração baseada em funções são aplicadas em cada site de uma hierarquia.  

 Se ainda não estiver familiarizado com os conceitos da administração baseada em funções, consulte [Fundamentos da administração baseada em funções para o System Center Configuration Manager](../../../../core/understand/fundamentals-of-role-based-administration.md)  

 As informações contidas nos procedimentos a seguir podem ajudá-lo a criar e configurar a administração baseada em funções e as configurações de segurança relacionadas.  

-   [Criar funções de segurança personalizadas](#BKMK_CreateSecRole)  

-   [Configurar funções de segurança](#BKMK_ConfigSecRole)  

-   [Configurar escopos de segurança para um objeto](#BKMK_ConfigSecScope)  

-   [Configurar coleções para gerenciar a segurança](#BKMK_ConfigColl)  

-   [Criar um novo usuário administrativo](#BKMK_Create_AdminUser)  

-   [Modificar o escopo administrativo de um usuário administrativo](#BKMK_ModAdminUser)  

##  <a name="a-namebkmkcreatesecrolea-create-custom-security-roles"></a><a name="BKMK_CreateSecRole"></a> Criar funções de segurança personalizadas  
 O Configuration Manager oferece várias funções de segurança internas. Se necessitar de funções de segurança adicionais, você poderá criar uma função de segurança personalizada criando a cópia de uma função de segurança existente e modificando essa cópia. Você pode criar uma função de segurança personalizada para conceder aos usuários administrativos as permissões de segurança adicionais de que eles necessitam e que não estão incluídas atualmente em uma função de segurança atribuída. Usando uma função de segurança personalizada, você pode conceder a eles somente as permissões de que eles precisam e impedir a atribuição de uma função de segurança que conceda mais permissões do que eles precisam.  

 Use o procedimento a seguir para criar uma nova atribuição de segurança usando uma função de segurança existente como modelo.  

#### <a name="to-create-custom-security-roles"></a>Para criar funções de segurança personalizadas  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Segurança**e clique em **Funções de Segurança**.  

     Use um dos seguintes processos para criar a nova função de segurança:  

    -   Para criar uma nova função de segurança personalizada, execute as seguintes ações:  

        1.  Selecione uma função de segurança existente para usar como origem para a nova função de segurança.  

        2.  Na guia **Início** , no grupo **Função de Segurança** , clique em **Copiar**. Isso criará uma cópia da função de segurança de origem.  

        3.  No assistente Copiar Função de Segurança, especifique um **Nome** para a nova função de segurança personalizada.  

        4.  Em **Atribuições de operações de segurança**, expanda cada nó **Operações de Segurança** para exibir as ações disponíveis.  

        5.  Para alterar a configuração de uma operação de segurança, clique na seta para baixo na coluna **Valor** e selecione **Sim** ou **Não**.  

            > [!CAUTION]  
            >  Ao configurar uma atribuição de segurança personalizada, não conceda permissões que não sejam exigidas pelos usuários administrativos associados à nova função de segurança. Por exemplo, o valor **Modificar** para a operação de segurança **Funções de Segurança** concede aos usuários administrativos permissão para editar toda função de segurança acessível, mesmo que eles não estejam associados a essa função de segurança.  

        6.  Após configurar as permissões, clique em **OK** para salvar a nova função de segurança.  

    -   Para importar uma função de segurança exportada de outra hierarquia do Configuration Manager, execute as seguintes ações:  

        1.  Na guia **Início** , no grupo **Criar** , clique em **Importar Função de Segurança**.  

        2.  Especifique o arquivo .xml que contém a configuração da função de segurança que você deseja importar e clique em **Abrir** para concluir o procedimento e salvar a função de segurança.  

            > [!NOTE]  
            >  Após importar uma função de segurança, você poderá editar as propriedades dessa função para alterar as permissões de objeto associadas a ela.  

##  <a name="a-namebkmkconfigsecrolea-configure-security-roles"></a><a name="BKMK_ConfigSecRole"></a> Configurar funções de segurança  
 Os grupos de permissões de segurança definidos para uma função de segurança são chamados de atribuições de operação de segurança. As atribuições de operação de segurança representam uma combinação de tipos de objetos e ações que estão disponíveis para cada tipo de objeto. Você pode modificar as operações de segurança disponíveis para qualquer função de segurança personalizada, mas não é possível modificar as funções de segurança internas que o Configuration Manager fornece.  

 Use o procedimento a seguir para modificar as operações de segurança para uma função de segurança.  

#### <a name="to-modify-security-roles"></a>Para modificar as funções de segurança  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Segurança**e clique em **Funções de Segurança**.  

3.  Selecione a função de segurança personalizada que deseja modificar.  

4.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  Clique na guia **Permissões** .  

6.  Em **Atribuições de operações de segurança**, expanda cada nó **Operações de Segurança** para exibir as ações disponíveis.  

7.  Para alterar a configuração de uma operação de segurança, clique na seta para baixo na coluna **Valor** e selecione **Sim** ou **Não**.  

    > [!CAUTION]  
    >  Ao configurar uma atribuição de segurança personalizada, não conceda permissões que não sejam exigidas pelos usuários administrativos associados à nova função de segurança. Por exemplo, o valor **Modificar** para a operação de segurança **Funções de Segurança** concede aos usuários administrativos permissão para editar toda função de segurança acessível, mesmo que eles não estejam associados a essa função de segurança.  

8.  Após concluir a configuração das atribuições de operação de segurança, clique em **OK** para salvar a nova atribuição de segurança.  

##  <a name="a-namebkmkconfigsecscopea-configure-security-scopes-for-an-object"></a><a name="BKMK_ConfigSecScope"></a> Configurar escopos de segurança para um objeto  
 Você gerencia a associação de um escopo de segurança para um objeto a partir do objeto e não a partir do escopo de segurança. As únicas configurações diretas para as quais os escopos de segurança oferecem suporte são as alterações de nome e descrição. Para alterar o nome e a descrição de um escopo de segurança ao exibir as propriedades dele, é necessário ter a permissão **Modificar** para o objeto protegível dos **Escopos de Segurança** .  

 Quando você cria um objeto no Configuration Manager, esse novo objeto é associado a cada escopo de segurança que está associado às funções de segurança da conta usada para criar o objeto quando essas funções de segurança fornecem a permissão **Criar** ou **Definir Escopo de Segurança**. Somente após o objeto ser criado você poderá alterar os escopos de segurança aos quais ele está associado.  

 Por exemplo, foi atribuída a você uma função de segurança que lhe concede permissão para criar um novo grupo de limites. Quando você cria um novo grupo de limites, você não tem opção à qual você possa atribuir escopos de segurança específicos. Em vez disso, os escopos de segurança disponíveis nas funções de segurança às quais você está associado são automaticamente atribuídos ao novo grupo de limites. Após salvar o novo grupo de limites, você poderá editar os escopos de segurança associados a ele.  

 Use o procedimento a seguir para configurar os escopos de segurança atribuídos a um objeto.  

#### <a name="to-configure-security-scopes-for-an-object"></a>Para configurar escopos de segurança para um objeto  

1.  No console do Configuration Manager, selecione um objeto que dê suporte à atribuição a um escopo de segurança.  

2.  Na guia **Início** , no grupo **Classificar** , clique em **Definir Escopos de Segurança**.  

3.  Na caixa de diálogo **Definir Escopos de Segurança** , selecione ou apague os escopos de segurança aos quais esse objeto está associado. Cada objeto que oferece suporte a escopos de segurança deve ser atribuído a pelo menos um escopo de segurança.  

4.  Clique em **OK** para salvar os escopos de segurança atribuídos.  

    > [!NOTE]  
    >  Quando você cria um novo objeto, você pode atribuí-lo a vários escopos de segurança. Para modificar o número de escopos de segurança associados ao objeto, é necessário alterar essa atribuição após a criação do objeto.  

##  <a name="a-namebkmkconfigcolla-configure-collections-to-manage-security"></a><a name="BKMK_ConfigColl"></a> Configurar coleções para gerenciar a segurança  
 Não existem procedimentos para configurar coleções para a administração baseada em funções. As coleções não possuem uma configuração de administração baseada em funções; em vez disso, você atribui coleções a um usuário administrativo quando você configura o usuário. As operações de segurança da coleção permitidas nas funções de segurança atribuídas aos usuários determinam as permissões que um usuário administrativo tem para coleções e recursos da coleção (membros da coleção).  

 Quando um usuário administrativo possui permissões para uma coleção, ele também tem permissões para coleções que estão limitadas a essa coleção. Por exemplo, a sua organização usa uma coleção chamada Todos os Desktops, e lá há uma coleção chamada Todos os Desktops da América do Norte que está limitada à coleção Todos os Desktops. Se um usuário administrativo tiver permissões para Todos os Desktops, ele também terá as mesmas permissões para a coleção Todos os Desktops da América do Norte. Além disso, um usuário administrativo não pode usar a permissão **Excluir** ou **Modificar** na coleção que está diretamente atribuída a ele, mas pode usar essas permissões nas coleções que estão limitadas a essa coleção. Usando o exemplo anterior, o usuário administrativo pode excluir ou modificar a coleção Todos os Desktops da América do Norte, mas não pode excluir ou modificar a coleção Todos os Desktops.  

##  <a name="a-namebkmkcreateadminusera-create-a-new-administrative-user"></a><a name="BKMK_Create_AdminUser"></a> Criar um novo usuário administrativo  
 Para conceder acesso para gerenciar o Configuration Manager a indivíduos ou membros de um grupo de segurança, crie um usuário administrativo no Configuration Manager e especifique a conta do Windows do Usuário ou Grupo de Usuários. Cada usuário administrativo no Configuration Manager deve receber a atribuição de pelo menos uma função de segurança e um escopo de segurança. Você também pode atribuir coleções para limitar o escopo administrativo do usuário administrativo.  

 Use os procedimentos a seguir para criar novos usuários administrativos.  

#### <a name="to-create-a-new-administrative-user"></a>Para criar um novo usuário administrativo  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Segurança**e clique em **Usuários Administrativos**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Adicionar Usuário ou Grupo**.  

4.  Clique em **Procurar** e selecione a conta de usuário ou grupo a ser usada para esse novo usuário administrativo.  

    > [!NOTE]  
    >  Para a administração baseada em console, somente os usuários de domínio ou grupos de segurança podem ser especificados como um usuário administrativo.  

5.  Para **Funções de segurança associadas**, clique em **Adicionar** para abrir a lista de funções de segurança disponíveis, marque a caixa de seleção para uma ou mais funções de segurança e clique em **OK**.  

6.  Selecione uma das duas opções a seguir para definir o comportamento de objeto protegível para o novo usuário:  

    -   **Todos os objetos protegíveis que são relevantes para suas funções de segurança associadas**: essa opção associa o usuário administrativo ao escopo de segurança **Todos** e a coleções de nível raiz integradas a **Todos os sistemas**e **Todos os usuários** e Grupos de usuários. As funções de segurança atribuídas ao usuário definem o acesso a objetos. Os novos objetos que esse usuário administrativo cria são atribuídos ao escopo de segurança **Padrão** .  

    -   **Somente objetos protegíveis em escopos de segurança especificados ou coleções**: por padrão, essa opção associa o usuário administrativo ao escopo de segurança **Padrão** e a coleções de **Todos os sistemas** e **Todos os usuários e Grupos de usuários** . No entanto, os escopos de segurança e as coleções atuais são limitados aos que estão associados à conta que você usou para criar o novo usuário administrativo. Essa opção oferece suporte à adição ou remoção de escopos de segurança e coleções para personalizar o escopo administrativo do usuário administrativo.  

    > [!IMPORTANT]  
    >  As opções anteriores associam cada escopo de segurança e coleção associados a cada função de segurança atribuída ao usuário administrativo. Uma terceira opção, **Somente objetos protegíveis como determinado pelas funções de segurança do usuário administrativo**, pode ser usada para associar funções de segurança individuais a escopos de segurança e coleções específicos. Essa terceira opção fica disponível com a criação do novo usuário administrativo, quando você modifica o usuário administrativo.  

7.  Dependendo da sua seleção na etapa 6, execute a seguinte ação:  

    -   Se você selecionou **Todos os objetos protegíveis que são relevantes para suas funções de segurança associadas**, clique em **OK** para concluir esse procedimento.  

    -   Se você selecionou **Somente objetos protegíveis em escopos de segurança ou coleções especificadas**, clique em **Adicionar** para selecionar coleções e escopos de segurança adicionais ou selecione um ou mais objetos na lista e clique em **Remover** para removê-los. Clique em **OK** para concluir esse procedimento.  

##  <a name="a-namebkmkmodadminusera-modify-the-administrative-scope-of-an-administrative-user"></a><a name="BKMK_ModAdminUser"></a> Modificar o escopo administrativo de um usuário administrativo  
 É possível modificar o escopo administrativo de um usuário administrativo ao adicionar ou remover funções de segurança, escopos de segurança e coleções que estão associados ao usuário. Cada usuário administrativo deve ser associado a pelo menos uma função de segurança e um escopo de segurança. Talvez você precise atribuir uma ou mais coleções para o escopo administrativo do usuário. A maioria das funções de segurança interagem com as coleções e não funcionam corretamente sem uma coleção atribuída.  

 Ao modificar um usuário administrativo, você pode alterar o comportamento de como os objetos protegíveis são associados às funções de segurança atribuídas. Os três comportamentos que podem ser selecionados são:  

-   **Todos os objetos protegíveis que são relevantes para suas funções de segurança associadas**: essa opção associa o usuário administrativo ao escopo **Todos** e a coleções de nível raiz integradas a **Todos os sistemas**e **Todos os usuários**e Grupos de usuários. As funções de segurança que são atribuídas ao usuário definem o acesso a objetos.  

-   **Somente objetos protegíveis em escopos de segurança especificados ou coleções**: essa opção associa o usuário administrativo aos mesmos escopos de segurança e coleções associados à conta usada para configurar o usuário administrativo. Essa opção oferece suporte à adição ou remoção de funções de segurança e coleções para personalizar o escopo administrativo do usuário administrativo.  

-   **Somente objetos protegíveis conforme determinados pelas funções de segurança do usuário administrativo**: essa opção permite criar as associações específicas entre as funções de segurança individuais e escopos de segurança específicos e coleções para o usuário.  

    > [!NOTE]  
    >  Essa opção está disponível somente quando você modifica as propriedades de um usuário administrativo.  

A configuração atual para o comportamento de objeto protegível altera o processo que você usa para atribuir as funções de segurança adicionais. Use os procedimentos a seguir que são baseados em opções diferentes para objetos protegíveis a fim de ajudá-lo a gerenciar um usuário administrativo.  

 Use o procedimento a seguir para exibir e gerenciar a configuração de objetos protegíveis para um usuário administrativo:  

#### <a name="to-view-and-manage-the-securable-object-behavior-for-an-administrative-user"></a>Para exibir e gerenciar o comportamento do objeto protegível para um usuário administrativo  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Segurança**e clique em **Usuários Administrativos**.  

3.  Selecione o usuário administrativo que deseja modificar.  

4.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  Clique na guia **Escopos de Segurança** para exibir a configuração atual de objetos protegíveis para esse usuário administrativo.  

6.  Para modificar o comportamento do objeto protegível, selecione uma nova opção para o comportamento do objeto protegível. Feita a mudança dessa configuração, faça a referência do procedimento apropriado para consulta futura para configurar os escopos de segurança, as coleções e as funções de segurança para esse usuário administrativo.  

7.  Clique em **OK** para concluir o procedimento.  

 Use o procedimento a seguir para modificar um usuário administrativo que têm o comportamento de objeto protegível definido como **Todos os objetos protegíveis que são relevantes para suas funções de segurança associadas**:  

#### <a name="option-all-securable-objects-that-are-relevant-to-their-associated-security-roles"></a>Opção: todos os objetos protegíveis que são relevantes para suas funções de segurança associadas  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Segurança**e clique em **Usuários Administrativos**.  

3.  Selecione o usuário administrativo que deseja modificar.  

4.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  Clique na guia **Escopos de Segurança** para confirmar se o usuário administrativo está configurado para **Todos os objetos protegíveis que são relevantes para suas funções de segurança associadas**.  

6.  Para modificar as funções de segurança atribuídas, clique na guia **Funções de Segurança** .  

    -   Para atribuir funções de segurança adicionais para esse usuário administrativo, clique em **Adicionar**, marque a caixa de seleção para cada função de segurança adicional que deseja atribuir e clique em **OK**.  

    -   Para remover as funções de segurança, selecione uma ou mais funções de segurança da lista e clique em **Remover**.  

7.  Para modificar o comportamento de objeto protegível, clique na guia **Escopos de Segurança** e selecione a nova opção para o comportamento de objeto protegível. Feita a mudança dessa configuração, faça a referência do procedimento apropriado para consulta futura para configurar os escopos de segurança, as coleções e as funções de segurança para esse usuário administrativo.  

    > [!NOTE]  
    >  Quando o comportamento de objeto protegível está definido como **Todos os objetos protegíveis que são relevantes para suas funções de segurança associadas**, você não pode adicionar ou remover escopos de segurança e coleções específicas.  

8.  Clique em **OK** para concluir esse procedimento.  

 Use o procedimento a seguir para modificar um usuário administrativo que tem o comportamento de objeto protegível definido como **Somente objetos protegíveis em escopos de segurança ou coleções especificadas**.  

#### <a name="option-only-securable-objects-in-specified-security-scopes-or-collections"></a>Opção: somente objetos protegíveis em escopos de segurança ou coleções especificadas  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Segurança**e clique em **Usuários Administrativos**.  

3.  Selecione o usuário administrativo que deseja modificar.  

4.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  Clique na guia **Escopos de Segurança** para confirmar se o usuário está configurado para **Somente objetos protegíveis em escopos de segurança ou coleções especificadas**.  

6.  Para modificar as funções de segurança atribuídas, clique na guia **Funções de Segurança** .  

    -   Para atribuir funções de segurança adicionais para esse usuário, clique em **Adicionar**, marque a caixa de seleção para cada função de segurança adicional que deseja atribuir e clique em **OK**.  

    -   Para remover as funções de segurança, selecione uma ou mais funções de segurança da lista e clique em **Remover**.  

7.  Para modificar os escopos de segurança e as coleções associados a funções de segurança, clique na guia **Escopos de Segurança** .  

    -   Para associar novos escopos de segurança ou coleções com todas as funções de segurança que estão atribuídos a esse usuário administrativo, clique em **Adicionar** e selecione uma das quatro opções. Se você selecionar **Escopo de Segurança** ou **Coleção**, marque a caixa de seleção para um ou mais objetos para concluir essa seleção e clique em **OK**.  

    -   Para remover um escopo de segurança ou uma coleção, selecione o objeto e clique em **Remover**.  

8.  Clique em **OK** para concluir esse procedimento.  

 Use o procedimento a seguir para modificar um usuário administrativo que tem o comportamento de objeto protegível definido como **Somente objetos protegíveis como determinado pelas funções de segurança do usuário administrativo**.  

#### <a name="option-only-securable-objects-as-determined-by-the-security-roles-of-the-administrative-user"></a>Opção: somente objetos protegíveis como determinado pelas funções de segurança do usuário administrativo  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Segurança**e clique em **Usuários Administrativos**.  

3.  Selecione o usuário administrativo que deseja modificar.  

4.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  Clique na guia **Escopos de Segurança** para confirmar se o usuário administrativo está configurado para **Somente objetos protegíveis em escopos de segurança ou coleções especificadas**.  

6.  Para modificar as funções de segurança atribuídas, clique na guia **Funções de Segurança** .  

    -   Para atribuir funções de segurança adicionais para esse usuário administrativo, clique em **Adicionar**. Na caixa de diálogo **Adicionar Função de Segurança** , selecione uma ou mais funções de segurança disponíveis, clique em **Adicionar**e selecione um tipo de objeto para associar a funções de segurança selecionadas. Se você selecionar **Escopo de Segurança** ou **Coleção**, marque a caixa de seleção para um ou mais objetos para concluir essa seleção e clique em **OK**.  

        > [!NOTE]  
        >  Você deve configurar pelo menos um escopo de segurança antes das funções de segurança selecionadas poder ser atribuídas ao usuário administrativo. Quando você seleciona várias funções de segurança, cada escopo de segurança e coleção que você configura está associado a cada uma das funções de segurança selecionadas.  

    -   Para remover as funções de segurança, selecione uma ou mais funções de segurança da lista e clique em **Remover**.  

7.  Para modificar os escopos de segurança e as coleções associados a uma função de segurança específica, clique na guia **Escopos de Segurança** , selecione a função de segurança e clique em **Editar**.  

    -   Para associar novos objetos a essa função de segurança, clique em **Adicionar**e selecione um tipo de objeto para associar a funções de segurança selecionadas. Se você selecionar **Escopo de Segurança** ou **Coleção**, marque a caixa de seleção para um ou mais objetos para concluir essa seleção e clique em **OK**.  

        > [!NOTE]  
        >  Você deve configurar pelo menos um escopo de segurança.  

    -   Para remover uma coleção ou escopo de segurança que está associado a essa função de segurança, selecione o objeto e clique em **Remover**.  

    -   Modificados os objetos associados, clique em **OK**.  

8.  Clique em **OK** para concluir esse procedimento.  

    > [!CAUTION]  
    >  Quando uma função de segurança concede a usuários administrativos a permissão de implantação de coleção, os usuários administrativos podem distribuir objetos a partir de qualquer escopo de segurança para os quais eles têm permissões de **leitura** de objetos, mesmo se o escopo de segurança esteja associado a uma função de segurança diferente.  



<!--HONumber=Dec16_HO3-->

