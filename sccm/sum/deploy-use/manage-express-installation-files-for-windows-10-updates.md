---
title: Gerenciar atualizações expressas do Windows 10
titleSuffix: Configuration Manager
description: O Configuration Manager dá suporte a arquivo de instalação expressa para o Windows 10, proporciona downloads menores e instalações mais rápidas nos clientes.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/15/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.openlocfilehash: 5f29b7a5d82b58358bdecd5508391db219b2cedc
ms.sourcegitcommit: 4b8afbd08ecf8fd54950eeb630caf191d3aa4767
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36260917"
---
# <a name="manage-express-installation-files-for-windows-10-updates"></a>Gerenciar os arquivos de instalação expressa para atualizações do Windows 10

O Configuration Manager dá suporte a arquivos de instalação expressa para atualizações do Windows 10. Configure o cliente para baixar somente as alterações entre a atualização cumulativa do Windows 10 do mês atual e a atualização do mês anterior. Sem os arquivos da instalação expressa, os clientes do Configuration Manager baixam a atualização cumulativa do Windows 10 completa a cada mês (incluindo todas as atualizações dos meses anteriores). Usar arquivos de instalação expressa proporciona downloads menores e instalações mais rápidas nos clientes.

Para saber como usar o Configuration Manager para gerenciar o conteúdo de atualização e ficar atualizado com o Windows 10, confira [Otimizar a entrega de atualização do Windows 10](/sccm/sum/deploy-use/optimize-windows-10-update-delivery).  


> [!IMPORTANT]  
> O suporte ao cliente do sistema operacional está disponível no Windows 10, versão 1607, com uma atualização para o Windows Update Agent. Essa atualização foi incluída nas atualizações lançadas em 11 de abril de 2017. Para obter mais informações sobre essas atualizações, consulte o [artigo de suporte 4015217](http://support.microsoft.com/kb/4015217). As atualizações futuras aproveitam a expressa para downloads menores. As versões anteriores do Windows 10 e o Windows 10 versão 1607 sem essa atualização não dão suporte a arquivos de instalação expressa.  


### <a name="enable-the-site-to-download-express-installation-files-for-windows-10-updates"></a>Habilite o site para baixar arquivos de instalação expressa para atualizações do Windows 10
Para começar a sincronizar os metadados para arquivos de instalação expressa do Windows 10, habilite-a nas Propriedades do ponto de atualização de software.  

1. No console do Configuration Manager, acesse o espaço de trabalho **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**.  

2. Selecione o site de administração central ou um site primário autônomo.  

3. Na faixa de opções, clique em **Configurar Componentes do Site** e clique em **Ponto de Atualização de Software**. Mude para a guia **Arquivos de Atualização** e selecione **Baixar arquivos completos de todas as atualizações aprovadas e arquivos de instalação expressa para o Windows 10**.

> [!NOTE]    
> Você não pode configurar o componente de ponto de atualização de software para baixar *apenas* atualizações expressas.  O site baixa os arquivos de instalação expressa adicionais aos arquivos completos. Isso aumenta a quantidade de conteúdo armazenada na biblioteca de conteúdo e distribuída e armazenada nos pontos de distribuição.

> [!Tip]  
> Para determinar o espaço real que está sendo usado no disco pelo arquivo, verifique a propriedade **Tamanho em disco** do arquivo. A propriedade Tamanho em disco deve ser consideravelmente menor do que o valor de Tamanho. Para saber mais, confira [Perguntas frequentes para otimizar a distribuição de atualizações do Windows 10](/sccm/sum/deploy-use/optimize-windows-10-update-delivery#bkmk_faq).  


### <a name="enable-clients-to-download-and-install-express-installation-files"></a>Habilitar os clientes para baixarem e instalarem os arquivos de instalação expressa
Para habilitar o suporte a arquivos de instalação expressa nos clientes, habilite os arquivos de instalação expressa no grupo **Atualizações de Software** das configurações do cliente. Essa configuração cria um novo ouvinte HTTP que escuta solicitações para baixar arquivos de instalação expressa na porta que você especificar.

> [!NOTE]    
> Esta é a porta local que os clientes usam para ouvir solicitações da Otimização de Entrega ou Serviço de Transferência Inteligente em Segundo Plano (BITS) para baixar conteúdo expresso do ponto de distribuição. Você não precisa abrir essa porta nos firewalls porque todo o tráfego está no computador local.  

Depois de implantar configurações do cliente para habilitar essa funcionalidade no cliente, ele tenta baixar o delta entre a atualização cumulativa do Windows 10 do mês atual e a atualização do mês anterior. Os clientes devem executar uma versão do Windows 10 que dá suporte a arquivos de instalação expressa.  

1. Habilite o suporte a arquivos de instalação expressa nas propriedades do componente de ponto de atualização de software (procedimento anterior).  

2. No console do Configuration Manager, vá até o espaço de trabalho **Administração** e selecione **Configurações do Cliente**.  

3. Selecione as configurações de cliente apropriadas e clique em **Propriedades** na faixa de opções.  

4. Selecione o grupo **Atualizações de Software**. Configure como **Sim** a configuração para **Habilitar a instalação de Atualizações Expressas em clientes**. Configure a **porta usada para baixar o conteúdo para as atualizações expressas** com a porta usada pelo ouvinte HTTP no cliente.  
