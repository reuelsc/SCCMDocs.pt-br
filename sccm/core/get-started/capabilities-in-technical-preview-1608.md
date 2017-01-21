---
title: Funcionalidades do Technical Preview 1608 do System Center Configuration Manager | Microsoft Docs
description: "Saiba mais sobre os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1608."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 63e1df5e-637c-4b07-b7ec-95340f43a805
caps.latest.revision: 15
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3bf44f850722afdb8dfe5922c8ceff11c9b56d08
ms.openlocfilehash: c41409e957f43aee3be994ab3e702232c7dfe6ea

---
# <a name="capabilities-in-technical-preview-1608-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1608 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1608. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview.      Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de um technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos em um technical preview.    


**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  




##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a>Melhorias na etapa de sequência de tarefas Preparar o Cliente do ConfigMgr para Captura  
A etapa Preparar o Cliente do ConfigMgr agora removerá completamente o cliente do Configuration Manager, em vez de apenas remover informações importantes. Quando a sequência de tarefas implantar a imagem capturada do sistema operacional, ela instalará um novo cliente do Configuration Manager sempre.  


## <a name="improvements-to-software-center"></a>Melhorias ao Centro de Software
* As guias **Aplicativos**, **Atualizações** e **Sistemas operacionais** do Centro de Software mostram qual software foi adicionado recentemente. Os números no painel de navegação mostram quantas novas ferramentas de software estão em cada guia.
* Agora os usuários podem agora solicitar aprovação para aplicativos e exibir o histórico de solicitações na exibição **Detalhes do aplicativo** no Centro de Software. O botão **Solicitar** em **Detalhes do Aplicativo** não redireciona mais para o Catálogo de Aplicativos baseado na Web.

## <a name="improvements-to-asset-intelligence"></a>Melhorias do Asset Intelligence
Adicionamos um campo às propriedades de software inventariado que permite definir uma relação de pai e filho com outro software. Na lista Software Inventariado, é possível exibir o pai de qualquer software e também ocultar todos os softwares filho.

### <a name="configure-a-parent-to-child-relationship"></a>Configurar uma relação de pai para filho
  1. Para configurar o software pai, no nó Software Inventariado, clique com o botão direito do mouse em um item de software na lista **Software Inventariado** e escolha **Propriedades**.
  2. Na caixa de diálogo aberta, selecione o software que você deseja definir como o software pai para a sua seleção inicial.

### <a name="filter-the-software-display"></a>Filtrar a exibição de software
Depois de definir relações de pai para filho, é possível filtrar a exibição para mostrar apenas o software pai ou que não tem nenhuma relação definida. Isso oculta todos os softwares definidos como um filho de outro software inventariado. Para fazer isso:
   1.   Na barra de pesquisa, escolha **Adicionar critérios**
   2. Selecione **Software Pai** e, em seguida, altere o valor dos critérios para **está vazio** e, em seguida, clique em **Pesquisar**.

A exibição agora mostra apenas os itens de software pai ou o software com nenhuma relação definida. O software que é apenas um filho de outro título não é exibido.

## <a name="remote-control-keyboard-translation"></a>Tradução do teclado de controle remoto
No passado, o Configuration Manager transmitia a posição da chave do local do visualizador para o local do participante do compartilhamento. Isso era problemático para as configurações de teclado diferentes do visualizador para participante do compartilhamento. Por exemplo, um visualizador com um teclado em inglês digitaria um "A", mas o teclado francês do participante do compartilhamento forneceria um "Q". Estamos alterando o comportamento padrão para que o próprio caractere seja transmitido do teclado do visualizador para o participante do compartilhamento e para o que o visualizador pretenda digitar chegue ao participante do compartilhamento.

Esse comportamento poderá ser desativado pelo visualizador se eles preferirem digitar de acordo com o esquema de teclado do participante do compartilhamento. Para alterar o comportamento, em **Controle Remoto do Configuration Manager**, escolha **Ação** e escolha **Habilitar Tradução do Teclado** para transmitir a posição da chave.

> [!NOTE]
>
> Chaves especiais, como ~!#@$%, não serão convertidas corretamente.



<!--HONumber=Dec16_HO3-->


