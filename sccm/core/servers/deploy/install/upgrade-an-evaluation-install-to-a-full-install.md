---
title: "Atualizar instalações de avaliação | Microsoft Docs"
description: "Saiba como atualizar uma instalação de avaliação para uma instalação completa do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 66dc01b7d1eeed5ad8262c60164460b669301aaf

---
# <a name="upgrade-an-evaluation-install-of-system-center-configuration-manager-to-a-full-install"></a>Atualizar uma instalação de avaliação do System Center Configuration Manager para uma instalação Completa

*Aplica-se a: System Center Configuration Manager (Branch Atual)*



 Se você tiver instalado o System Center Configuration Manager como uma versão de avaliação, após 180 dias, o console do Configuration Manager se tornará somente leitura até você ativar o produto na página **Manutenção do Site** na Configuração. A qualquer momento antes ou depois do período de 180 dias, você tem a opção de atualizar para uma instalação de avaliação para uma instalação completa.  

> [!NOTE]  
>  Quando você conecta um console do Configuration Manager a uma instalação de avaliação do Configuration Manager, a barra de título do console mostra o número de dias que restam antes de expirar a instalação de avaliação. O número de dias não é atualizado automaticamente; é atualizado somente quando você faz uma nova conexão a um site.  

 **Você pode atualizar os seguintes sites que executam uma instalação de avaliação:**  

-   Site de administração central  

-   Site primário  

Como os sites secundários não são tratados como instalações de avaliação, você não precisa modificar um site secundário depois que seu site pai primário é atualizado para uma instalação completa.  

**Pré-requisitos para atualizar uma edição de avaliação para uma edição completa:**  

-   Você deve ter um produto válido a ser usado durante a atualização  

-   Sua conta deve ter permissões de **administrador** para o computador no qual o site está instalado  

### <a name="to-upgrade-an-evaluation-edition-of-configuration-manager-to-a-licensed-edition"></a>Para atualizar uma edição de avaliação do Configuration Manager para uma edição licenciada  

1.  No servidor do site, localize e execute **SETUP.exe** (instalação do Configuration Manager) na pasta de instalação do Configuration Manager (**%path%\BIN\X64**).  Você deve executar a cópia da instalação que está localizada no servidor do site na pasta do Configuration Manager, uma vez que não há opções de manutenção do site disponíveis quando você executa a instalação da mídia de instalação.  

2.  Na página **Antes de Começar** , clique em **Avançar**.  

3.  Na página **Guia de Introdução** , selecione **Realizar a manutenção do site ou redefinir o site**e clique em **Próximo**.  

4.  Na página **Manutenção do Site** , selecione **Atualizar a edição de avaliação para uma edição licenciada**, insira uma chave do produto (Product Key) válida e clique em **Avançar**.  

5.  Na página **Termos de Licença para Software Microsoft** , leia e aceite os termos de licença e clique em **Próximo**.  

6.  Na página **Configuração** , clique em **Fechar** para concluir o assistente.  

    > [!NOTE]  
    >  Uma barra de título dos consoles do Configuration Manager que permanecem conectados ao site que você atualiza pode indicar que o site ainda é uma versão de avaliação até que você reconecte o console ao site.  



<!--HONumber=Dec16_HO3-->


