---
title: "Ferramenta de Registro de Atualização | Microsoft Docs"
description: "Descubra quando e como usar a ferramenta de registro de atualização para importar manualmente uma atualização para o console do Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cc13635-85d6-4b07-a3ec-c42188bc5c74
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: c729212d38168acfff3f11ea41f3d52b234c70c8


---
# <a name="use-the-update-registration-tool-to-import-hotfixes-to-system-center-configuration-manager"></a>Usar a Ferramenta de Registro de Atualização para importar hotfixes para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Algumas atualizações do Configuration Manager não estão disponíveis no serviço de nuvem da Microsoft e só são obtidas fora de banda. Um exemplo é um hotfix de versão limitada para resolver um problema específico.   
Quando for preciso instalar uma versão fora de banda e o nome do arquivo da atualização ou do hotfix terminar com a extensão **update.exe**, use a **ferramenta de registro de atualização** para importar manualmente a atualização para o console do Configuration Manager. A ferramenta permite extrair e transferir o pacote de atualização para o servidor do site, bem como registrar a atualização no console do Configuration Manager.  

 Se o arquivo de hotfix tiver a extensão de arquivo **.exe** (e não **update.exe**), consulte [Usar o Instalador dr Hotfix para instalar atualizações do System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  

> [!NOTE]  
>  Este tópico fornece diretrizes gerais sobre como instalar os hotfixes que atualizam o System Center Configuration Manager. Para obter detalhes sobre uma atualização ou um hotfix específico, consulte o artigo da KB (Base de Dados de Conhecimento) correspondente no site de Suporte da Microsoft.  

 **Pré-requisitos para usar a ferramenta de registro de atualização:**  

-   Somente atualizações fora de banda que terminem com a extensão **.update.exe** podem ser instaladas com essa ferramenta  

-   A ferramenta é autossuficiente com as atualizações individuais que você obtém diretamente da Microsoft  

-   A ferramenta não tem uma dependência no modo do ponto de conexão de serviço  

-   A ferramenta deve ser executada no computador que hospeda o ponto de conexão de serviço  

-   O computador onde a ferramenta é executada (o computador do ponto de conexão de serviço) deve ter o .NET Framework 4.52 instalado  

-   A conta usada para executar a ferramenta deve ter permissões de **administrador local** no computador que hospeda o ponto de conexão de serviço (no qual a ferramenta é executada)  

-   A conta usada para executar a ferramenta deve ter permissões de **gravação** para a seguinte pasta no computador que hospeda o ponto de conexão de serviço: **&lt;diretório de instalação do ConfigMgr\>\EasySetupPayload\offline**  

### <a name="to-use-the-update-registration-tool"></a>Para usar a ferramenta de registro de atualização  

1.  No computador que hospeda o ponto de conexão de serviço:  

    -   Abra um prompt de comando com privilégios administrativos e altere os diretórios para o local que contém **&lt;Produto\>-&lt;versão do produto\>-&lt;ID do artigo da KB\>-ConfigMgr.Update.exe**  

2.  Execute o seguinte comando para iniciar a ferramenta de registro de atualização:  

    -   **&lt;Produto\>-&lt;versão do produto\>-&lt;ID do artigo da KB\>-ConfigMgr.Update.exe**  

    Depois que o hotfix for registrado, ele aparecerá como uma nova atualização no console em até 24 horas.  Você pode acelerar o processo usando uma das seguintes opções:  

    -   Com a versão 1511: no console do Configuration Manager, navegue até **Administração > Serviços de Nuvem > Atualizações e Manutenção** e escolha **Iniciar processo de descoberta de atualização imediatamente**.  Isso inicia a importação do hotfix imediatamente após a conclusão do processo de registro, tornando-o disponível no console.  

    -   Com a versão 1602 e posteriores: no console do Configuration Manager, navegue para **Administração > Serviços de Nuvem > Atualizações e Manutenção** e clique em **Verificar Atualizações**  

    A ferramenta de registro de atualização registra suas ações em um arquivo .log no computador local. O arquivo de log tem o mesmo nome do arquivo .exe do hotfix e é gravado na pasta **%SystemRoot%/Temp**.  

     Depois que a atualização for registrada, você poderá fechar a ferramenta de registro de atualização.  

3.  Abra o console do Configuration Manager e navegue até **Administração** > **Serviços de Nuvem** > **Atualizações e Manutenção**. Os hotfixes que foram importados agora estão disponíveis para instalação. Para obter informações sobre a instalação de atualizações, consulte [Instalar atualizações no console para o System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md)  



<!--HONumber=Dec16_HO3-->


