---
title: Publicar dados do site | Microsoft Docs
description: Saiba como publicar sites do Configuration Manager no Active Directory Domain Services.
ms.custom: na
ms.date: 2/7/2017
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
ms.sourcegitcommit: e7629fdf7fdf615fa27894158c3d101432c95a04
ms.openlocfilehash: bcfb002c503485f03ba27d7346acb61d0d3c6087


---
# <a name="publish-site-data-for-system-center-configuration-manager"></a>Publicar dados do site para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Após estender o esquema do Active Directory para o System Center Configuration Manager, pode publicar sites do Configuration Manager no Active Directory Domain Services (AD DS). Isso possibilita que os computadores do Active Directory recuperem com segurança as informações do site de uma fonte confiável. Apesar de não ser necessário publicar informações do site no AD DS para a funcionalidade básica do Configuration Manager, essa configuração pode reduzir a sobrecarga administrativa.  

-   **Quando um site está configurado para publicar no AD DS**, os clientes do Configuration Manager podem encontrar automaticamente pontos de gerenciamento por meio da publicação do Active Directory. Para tanto só é preciso usar uma consulta LDAP em um servidor de catálogo global.  

-   **Quando um site não publicar no AD DS**, os clientes devem ter um mecanismo alternativo para localizar seu ponto de gerenciamento padrão.  

Para saber mais sobre como clientes localizam um ponto gerenciamento, veja [Entenda como os clientes encontram serviços e recursos do site para o System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="configure-sites-to-publish-to-ad-ds"></a>Configurar sites para publicar no AD DS  
 Veja as etapas de alto nível abaixo:  

-   Você deve [estender o esquema do Active Directory para o System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md) em cada floresta em que publicar dados do site. Certifique-se também de que o contêiner do **System Management** esteja presente.  

-   Você deve conceder, à conta de computador de cada site primário que publicará dados, **controle total** sobre o contêiner do **System Management** e todos os seus objetos filho.  

### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-active-directory-forest"></a>Para habilitar um site do Configuration Manager para publicar informações do site na floresta do Active Directory

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Configuração de Site**e clique em **Sites**. Selecione o site em que deseja publicar seus dados do site. Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

3.  Na guia **Publicando** das propriedades do site, selecione as florestas nas quais esse site publicará dados.  

4.  Clique em **OK** para salvar a configuração.  

### <a name="to-set-up-active-directory-forests-for-publishing"></a>Para configurar florestas do Active Directory para publicação  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho de **Administração** , clique em **Florestas do Active Directory**. Se uma descoberta de florestas do Active Directory tiver sido executada anteriormente, você verá cada floresta descoberta no painel de resultados. A floresta local e quaisquer florestas confiáveis são detectadas quando a descoberta de florestas do Active Directory é executada. Somente as florestas não confiáveis devem ser adicionadas manualmente.  

    -   Para configurar uma floresta descoberta anteriormente, selecione-a no painel de resultados. Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades** para abrir as propriedades da floresta. Continue na etapa 3.  

    -   Para configurar uma nova floresta que não esteja listada: na guia **Início**, no grupo **Criar**, clique em **Adicionar Floresta** para abrir a caixa de diálogo **Adicionar Florestas**. Continue na etapa 3.  

3.  Na guia **Geral**, complete as configurações da floresta que você deseja descobrir e especifique a **Conta da Floresta do Active Directory**.  

    > [!NOTE]  
    >  A descoberta de florestas do Active Directory requer uma conta global para descobrir e publicar em florestas não confiáveis. Se você não usar a conta de computador do servidor do site, será possível selecionar somente uma conta global.  

4.  Se você pretende permitir que os sites publiquem dados nessa floresta, na guia **Publicação** conclua as configurações para que seja possível fazer publicações nessa floresta.  

    > [!NOTE]  
    >  Se você permitir que sites publiquem em uma floresta, deve estender o esquema do Active Directory dessa floresta para o Configuration Manager. A conta de floresta do Active Directory deve ter permissões de controle total ao contêiner do sistema nessa floresta.  

5.  Ao concluir a configuração da floresta a ser usada com a descoberta de florestas do Active Directory, clique em **OK** para salvá-la.  



<!--HONumber=Feb17_HO1-->


