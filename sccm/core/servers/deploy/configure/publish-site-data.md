---
title: Publicar dados do site | Microsoft Docs
description: Saiba como publicar sites do Configuration Manager no Active Directory Domain Services.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 17cf034f-eaff-43ce-bc8e-917213c1db74
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: eb44c1c8c908e9cac17dc6d3011a3111eeb949b1


---
# <a name="publish-site-data-for-system-center-configuration-manager"></a>Publicar dados do site para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Depois de estender o esquema do Active Directory para o System Center Configuration Manager, você pode publicar os sites do Configuration Manager para o AD DS (Active Directory Domain Services) para que os computadores do Active Directory possam recuperar as informações do site provenientes de uma fonte confiável. Apesar de não ser necessário publicar informações do site para os AD DS para a funcionalidade básica do Configuration Manager, essa configuração pode reduzir a sobrecarga administrativa.  

-   **Quando um site está configurado para publicar para o AD DS**, os clientes do Configuration Manager podem encontrar automaticamente pontos de gerenciamento por meio da publicação do Active Directory usando uma consulta LDAP para um servidor de catálogo global.  

-   **Quando um site não publicar no AD DS**, os clientes devem ter um mecanismo alternativo para localizar seu ponto de gerenciamento padrão.  

Para obter mais informações sobre como clientes localizam um ponto gerenciamento, consulte [Entenda como os clientes encontram serviços e recursos do site para o System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="configure-sites-to-publish-to-ad-ds"></a>Configurar sites para publicar no AD DS  
 Veja as etapas de alto nível abaixo:  

-   Você deve [Estender o esquema do Active Directory para o System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md) em cada floresta em que você publicar dados do site e verificar se o contêiner do **System Management** existe.  

-   Você deve conceder, à conta de computador de cada site primário que publicará dados,   **controle total** sobre o contêiner do **System Management** e todos os seus objetos filho.  

#### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-active-directory-forest"></a>Para habilitar um site do Configuration Manager para publicar informações do site na floresta do Active Directory:  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Configuração do Site** e clique em **Sites**. Selecione o site que você deseja configurar para publicar seus dados do site, e em seguida, na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

3.  Na guia **Publicação** das propriedades do site, selecione as florestas nas quais esse site publicará dados.  

4.  Clique em **OK** para salvar a configuração.  

 Use o procedimento a seguir para configurar uma floresta do Active Directory para publicação:  

#### <a name="to-configure-active-directory-forests-for-publishing"></a>Para configurar florestas do Active Directory para publicação:  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho de **Administração** , clique em **Florestas do Active Directory**. Se uma descoberta de florestas do Active Directory tiver sido executada anteriormente, você verá cada floresta descoberta no painel de resultados. A floresta local e quaisquer florestas confiáveis são detectadas quando a descoberta de florestas do Active Directory é executada. Somente as florestas não confiáveis devem ser adicionadas manualmente.  

    -   Para configurar uma floresta descoberta anteriormente, selecione-a no painel de resultados e na guia **Início** , no grupo **Propriedades** , clique em **Propriedades** para abrir as propriedades da floresta. Continue na etapa 3.  

    -   Para configurar uma nova floresta que não esteja listada: na guia **Início** , no grupo **Criar** , clique em **Adicionar Floresta** para abrir a caixa de diálogo **Adicionar Floresta** . Continue na etapa 3.  

3.  Na guia **Geral** , complete as configurações da floresta que você deseja descobrir e especifique a **Conta da Floresta do Active Directory**.  

    > [!NOTE]  
    >  A descoberta de florestas do Active Directory requer uma conta global para descobrir e publicar em florestas não confiáveis. Se você não usar a conta de computador do servidor do site, será possível selecionar somente uma conta global.  

4.  Se você pretende permitir que os sites publiquem dados nessa floresta, na guia **Publicação** conclua as configurações para que seja possível fazer publicações nessa floresta.  

    > [!NOTE]  
    >  Se você permitir que sites publiquem em uma floresta, será necessário estender o esquema do Active Directory dessa floresta para o Configuration Manager, e a conta da floresta do Active Directory deverá ter permissões de controle total no contêiner do sistema dessa floresta.  

5.  Ao concluir a configuração da floresta a ser usada com a descoberta de florestas do Active Directory, clique em **OK** para salvá-la.  



<!--HONumber=Dec16_HO3-->


