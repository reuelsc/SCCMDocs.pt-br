---
title: Início rápido do Centro de Suporte
titleSuffix: Configuration Manager
description: Capture rapidamente o estado de um cliente do Configuration Manager para solução de problemas.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5cb41e2b-4c79-4da9-a432-ff869c0870f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f63193f9d4c9c754a56186f7a36cb9fabaf95725
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500724"
---
# <a name="support-center-quickstart-guide"></a>Guia de início rápido do Centro de Suporte

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Centro de Suporte tem funcionalidades poderosas, incluindo a solução de problemas e a exibição de log em tempo real. Também pode ser usado em apenas alguns minutos para capturar o estado de um computador cliente do Configuration Manager. Essa capacidade inclui acesso a clientes remotos.

Criar um arquivo completo do *pacote de solução de problemas* que captura o estado do cliente. O pacote não contém apenas arquivos de log. Ele pode incluir outros tipos de dados, como configurações do Registro e configurações de cliente. Forneça o pacote para um técnico de suporte que usa o Visualizador do Centro de Suporte.



## <a name="prerequisites"></a>Pré-requisitos

- Direitos administrativos locais para um cliente do Configuration Manager  

- O instalador do Centro de Suporte. Esse arquivo está no servidor do site em `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`. Para obter mais informações, confira [Centro de Suporte – Instalar](/sccm/core/support/support-center#install).  



## <a name="step-1-create-a-data-bundle-on-a-local-client"></a>Etapa 1: criar um conjunto de dados em um cliente local

1.  Instale o Centro de Suporte no cliente do Configuration Manager.  

2.  Vá para o menu **Iniciar** no grupo do **Microsoft System Center** e selecione **Centro de Suporte**.  

3.  Na guia Início da faixa de opções, selecione **Coletar Dados Selecionados**. Por padrão, o Centro de Suporte coleta apenas o conjunto de dados mínimo: arquivos de log, configuração do cliente e sistema operacional.  

4.  Salve o arquivo do pacote de solução de problemas (.zip) em uma pasta no computador. Por padrão, o nome do arquivo é semelhante ao exemplo a seguir: `Support_c885cdfed3c7482bba4f9e662978ec07.zip`.  



## <a name="step-2-view-the-data-bundle-using-support-center-viewer"></a>Etapa 2: Exibir um pacote de dados usando o Visualizador do Centro de Suporte

1.  Abra o **Visualizador do Centro de Suporte**. Essa ação pode acontecer em qualquer computador no qual você instala o Centro de suporte.  

2.  Selecione **Abrir pacote**, navegue até o arquivo de pacote e selecione **Abrir**.  

3.  Depois que o Visualizador do Centro de Suporte processa o arquivo, alterne para cada guia disponível. Exiba os tipos de dados que o Centro de Suporte coleta por padrão:  

    - **Configuração**  

        - Configuração de cliente do Configuration Manager  

        - Sistema operacional  

        - Computador  

        - Serviços  

        - Adaptadores de rede  

    - **Logs**: escolha uma ou mais entradas na lista e selecione **Abrir**. Essa ação abre os arquivos de log selecionados no Visualizador de Log. Use este recurso para pesquisar códigos de erro e usar filtros avançados para ajudá-lo a analisar mais rapidamente arquivos de log.  



## <a name="collect-more-data"></a>Coletar mais dados

Além dessas capacidades básicas, o Centro de Suporte também pode coletar uma grande variedade de outras informações de estado do cliente. Abra **Centro de Suporte** e selecione **Coletar Todos os Dados**. Esse processo normalmente tem duração de alguns minutos, mesmo em computadores mais recentes. O Centro de Suporte coleta os dados adicionais a seguir:

  - **Política**: configurações de política do Configuration Manager, incluindo a configuração da política solicitada e a configuração da política real  

  - **Certificados**: informações de chave pública para certificados do cliente. O Centro de Suporte não coleta as chaves privadas do certificado.  

  - **Registro de cliente**: coleta informações de configuração de cliente do Registro. O Centro de Suporte coleta apenas as informações de Registro do Configuration Manager.  

  - **WMI cliente**: informações de configuração de cliente da WMI. O Centro de Suporte não coleta política do cliente.  

  - **Solução de problemas**: solução de problemas em tempo real para ajudar a diagnosticar problemas comuns de cliente do Active Directory, pontos de gerenciamento, rede, atribuições de política e registro.  

  - **Despejos de depuração**: execute um despejo de depuração do cliente e dos processos relacionados. Despejos de depuração podem ser grandes. Somente habilite essa opção ao realizar a solução de problemas de desempenho do cliente.  

