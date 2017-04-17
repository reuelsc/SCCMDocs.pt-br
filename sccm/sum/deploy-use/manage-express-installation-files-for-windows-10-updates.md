---
title: "Gerenciar os arquivos de instalação expressa para atualizações do Windows 10 | Microsoft Docs"
description: "O Configuration Manager dá suporte a arquivo de instalação expressa para o Windows 10, proporciona downloads menores e instalações mais rápidas nos clientes."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 03/24/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 459ad5a428102b5e040bec2eaf2a70fc89789dff
ms.lasthandoff: 03/27/2017

---

## <a name="manage-express-installation-files-for-windows-10-updates"></a>Gerenciar os arquivos de instalação expressa para atualizações do Windows 10
A partir da versão 1702, o Configuration Manager oferece suporte a arquivos de instalação expressa para atualizações do Windows 10. Ao usar uma versão do Windows 10 com suporte, você poderá usar as definições do Configuration Manager para baixar somente as alterações entre a Atualização Cumulativa do Windows 10 do mês atual e a atualização do mês anterior. Sem os arquivos de instalação expressa, o Configuration Manager baixa a Atualização Cumulativa do Windows 10 (incluindo todas as atualizações dos meses anteriores) a cada mês. Usar arquivos de instalação expressa proporciona downloads menores e instalações mais rápidas nos clientes.

> [!IMPORTANT]
> Embora as configurações para dar suporte ao uso de arquivos de instalação expressa estejam disponíveis no Configuration Manager versão 1702, o suporte ao cliente do sistema operacional está disponível no Windows 10 versão 1607 com uma atualização do Windows Update Agent. Essa atualização está incluída com as atualizações lançadas em 11 de abril de 2017 (Patch Tuesday). <!--For more information about these updates, see [support article 4015217](http://support.microsoft.com/kb/4015217).--> As atualizações futuras aproveitarão a expressa para downloads menores. O Windows 10 versão 1607 sem a atualização de versão e versões anteriores não dão suporte a arquivos de instalação expressa.

### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates-on-the-server"></a>Para habilitar o download de arquivos de instalação expressa para atualizações do Windows 10 no servidor
Para começar a sincronizar os metadados para arquivos de instalação expressa do Windows 10, você deve habilitá-la nas Propriedades do Ponto de Atualização de Software.
1.    No console do Configuration Manager, navegue até **Administração** > **Configuração de Site** > **Sites**.
2.    Selecione o site de administração central ou um site primário autônomo.
3.    Na guia **Início** , no grupo **Configurações** , clique em **Configurar Componentes do Site**e **Ponto de Atualização de Software**. Na guia **Arquivos de Atualização**, selecione **Baixar arquivos completos para todas as atualizações aprovadas e arquivos de instalação expressa para o Windows 10**.

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>Para habilitar o suporte para clientes baixarem e instalarem os arquivos de instalação expressa
Para habilitar o suporte a arquivos de instalação expressa nos clientes, você deve habilitar os arquivos de instalação expressa em clientes na seção Atualizações de Software das configurações do cliente. Isso cria um novo ouvinte HTTP que escuta solicitações para baixar arquivos de instalação expressa na porta que você especificar. Depois de implantar as configurações de cliente para habilitar essa funcionalidade no cliente, ele tentará baixar a diferença entre a Atualização Cumulativa do Windows 10 do mês atual e a atualização do mês anterior (os clientes devem executar uma versão do Windows 10 com suporte a arquivos de instalação expressa).
1.    Habilite o suporte a arquivos de instalação expressa nas propriedades do Componente de Ponto de Atualização de Software (procedimento anterior).
2.    No console do Configuration Manager, navegue para **Administração** > **Configurações do Cliente**.
3.    Selecione as configurações de cliente apropriadas e, em seguida, na guia **Início**, clique em **Propriedades**.
4.    Selecione a página **Atualizações de Software**, defina **Sim** para a configuração **Habilitar instalação de Atualizações Expressas em clientes** e configure a porta usada pelo ouvinte HTTP no cliente para a configuração **Porta usada para baixar o conteúdo para as Atualizações Expressas**.
