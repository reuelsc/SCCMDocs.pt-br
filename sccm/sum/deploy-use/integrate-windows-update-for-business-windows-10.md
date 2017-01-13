---

title: "Integração ao Windows Update for Business no Windows 10 | Microsoft Docs"
description: "Use o Windows Update para Empresas para manter dispositivos baseados no Windows 10 na sua organização atualizados para dispositivos conectados ao serviço do Windows Update."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
translationtype: Human Translation
ms.sourcegitcommit: e6cf8c799b5be2f7dbb6fadadddf702ec974ae45
ms.openlocfilehash: 8bdbacd54632475ac69a0d0a9a34b2567c3daa13


---
# <a name="integration-with-windows-update-for-business-in-windows-10"></a>Integração com o Windows Update for Business no Windows 10

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A atualização do WUfB (Windows Update for Business) permite que você mantenha dispositivos baseados no Windows 10 em sua organização sempre atualizados com as defesas de segurança mais recentes e os recursos do Windows quando esses dispositivos se conectam diretamente ao serviço WU (Windows Update). O Configuration Manager consegue diferenciar entre os computadores Windows 10 que usam WUfB e WSUS para obter atualizações de software.  

 Alguns recursos do Configuration Manager não estão mais disponíveis quando os clientes do Configuration Manager são configurados para receber atualizações do WU, que inclui WUfB ou Windows Insiders:  

-   Relatórios de conformidade do Windows Update:  

    -   O Configuration Manager não será informado das atualizações que são publicadas no WU. Os clientes do Configuration Manager configurados para receber atualizações do WU exibirão o status **desconhecido** para essas atualizações no console do Configuration Manager.  

    -   Solucionar o problema do status de conformidade geral é difícil porque o status **desconhecido** é usado apenas para os clientes que não haviam informado o status de verificação do WSUS.  Agora ele também inclui os clientes do Configuration Manager que recebem atualizações do WU.  

    -   O acesso condicional (para recursos corporativos) com base no status de conformidade de atualização não funcionará conforme o esperado para os clientes que recebem atualizações do WU porque eles nunca atenderiam à conformidade do Configuration Manager.  

    -   A conformidade das Atualizações de Definição faz parte dos relatórios de conformidade de atualização geral e não funcionará conforme o esperado.  A conformidade das Atualizações de Definição também faz parte da avaliação de acesso condicional  

-   O relatório geral do Endpoint Protection para Defender com base no status de conformidade da atualização não retornará resultados precisos por causa dos dados de verificação ausentes.  

-   O Configuration Manager não poderá implantar atualizações da Microsoft, como Office, Internet Explorer e Visual Studio, para os clientes que estão conectados no WUfB para receber atualizações.  

-   O Configuration Manager não poderá implantar as atualizações de terceiros que são publicadas no WSUS e gerenciadas por meio do Configuration Manager para clientes que estão conectados no WUfB para receber atualizações.  

-   A implantação completa do cliente do Configuration Manager que usa a infraestrutura de atualizações de software não funcionará para clientes que estão conectados ao WUfB para receber atualizações.  

## <a name="identify-clients-that-use--wufb-for-windows-10-updates"></a>Identificar clientes que usam as atualizações do WUfB para o Windows 10  
 Use o procedimento a seguir para identificar clientes que usam o WUfB para obter atualizações do Windows 10, configure esses clientes para pararem de usar o WSUS para obter atualizações e implante um agente cliente de configuração para desabilitar o fluxo de trabalho de atualizações de software para esses clientes.  

 **Pré-requisitos**  

-   Clientes que executam o Windows 10 Desktop Pro ou Windows 10 Enterprise Edition versão 1511 ou posterior  

-   O[Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx) é implantado e os clientes usam o WUfB para obter atualizações do Windows 10.  

#### <a name="to-identify-clients-that-use-wufb"></a>Para identificar os clientes que usam o WUfB  

1.  Desabilite o Windows Update Agent para que ele não examine o WSUS, se tiver sido habilitado anteriormente.   
    A chave do Registro **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer** pode ser definida para indicar se o computador está verificando em relação ao WSUS ou ao Windows Update.  Quando o valor for 2, ele não verificará com relação ao WSUS.  

2.  Há um novo atributo, o **UseWUServer**, no nó **Windows Update** do Gerenciador de Recursos do Configuration Manager.  

3.  Crie uma coleção com base no atributo **UseWUServer** para todos os computadores que estão conectados por meio do WUfB para atualizações.  

4.  Crie uma configuração de agente cliente para desabilitar o fluxo de trabalho de atualização de software e implante a configuração na coleção de computadores que estão conectados diretamente ao WUfB.  

5.  Os computadores gerenciados via WUfB exibirão **Desconhecido** no status de conformidade e não serão contados como parte do percentual de conformidade geral.  



<!--HONumber=Dec16_HO3-->


