---
title: Integração com o Windows Update for Business no Windows 10
titleSuffix: Configuration Manager
description: Use o Windows Update para Empresas para manter dispositivos baseados no Windows 10 na sua organização atualizados para dispositivos conectados ao serviço do Windows Update.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
ms.collection: M365-identity-device-management
ms.openlocfilehash: 456e4537e7c397063c50422e8c408dc5d688af04
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56121566"
---
# <a name="integration-with-windows-update-for-business-in-windows-10"></a>Integração com o Windows Update for Business no Windows 10

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O WUfB (Windows Update para Empresas) permite que você mantenha dispositivos baseados no Windows 10 em sua organização sempre atualizados com as últimas defesas de segurança e os recursos do Windows quando esses dispositivos se conectam diretamente ao serviço WU (Windows Update). O Configuration Manager pode diferenciar entre os computadores Windows 10 que usam o WUfB e o WSUS para obter atualizações de software.  

 Alguns recursos do Configuration Manager não estão mais disponíveis quando os clientes do Configuration Manager são configurados para receber atualizações do WU, que inclui WUfB ou Windows Insiders:  

-   Relatórios de conformidade do Windows Update:  

    -   O Configuration Manager não será informado das atualizações que são publicadas no WU. Os clientes do Configuration Manager configurados para receber atualizações do WU exibirão o status **desconhecido** para essas atualizações no console do Configuration Manager.  

    -   Solucionar o problema do status de conformidade geral é difícil porque o status **desconhecido** é usado apenas para os clientes que não relataram o status de verificação novamente do WSUS. Agora ele também inclui os clientes do Configuration Manager que recebem atualizações do WU.  

    -   O acesso condicional (para recursos corporativos) com base no status de conformidade de atualização não funcionará conforme o esperado para os clientes que recebem atualizações do WU porque eles nunca atenderiam à conformidade do Configuration Manager.  

    -   A conformidade das Atualizações de Definição faz parte dos relatórios de conformidade de atualização geral e não funcionará conforme o esperado.  A conformidade das Atualizações de Definição também faz parte da avaliação de acesso condicional  

-   O relatório geral do Endpoint Protection para o Defender com base no status de conformidade das atualizações não retornará resultados precisos por causa dos dados de verificação ausentes.  

-   O Configuration Manager não poderá implantar atualizações da Microsoft, como Office, IE e Visual Studio, nos clientes que estão conectados ao WUfB para receber atualizações.  

-   O Configuration Manager não poderá implantar as atualizações de terceiros que são publicadas no WSUS e gerenciadas por meio do Configuration Manager para clientes que estão conectados no WUfB para receber atualizações.  

-   A implantação completa do cliente do Configuration Manager que usa a infraestrutura de atualizações de software não funcionará para clientes que estão conectados ao WUfB para receber atualizações.  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>Identificar clientes que usam as atualizações do WUfB para o Windows 10  
 Use o procedimento a seguir para identificar os clientes que usam o WUfB para obter atualizações do Windows 10. Em seguida, configure esses clientes para interromper o uso do WSUS para obter atualizações e implante uma configuração do agente cliente para desabilitar o fluxo de trabalho de atualizações de software para esses clientes.  

 **Pré-requisitos**  

-   Clientes que executam o Windows 10 Desktop Pro ou Windows 10 Enterprise Edition versão 1511 ou posterior  

-   O[Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx) é implantado e os clientes usam o WUfB para obter atualizações do Windows 10.  

#### <a name="to-identify-clients-that-use-wufb"></a>Para identificar os clientes que usam o WUfB  

1.  Desabilite o Windows Update Agent para que ele não verifique o WSUS, caso ele tenha sido habilitado anteriormente. A chave do Registro a seguir pode ser definida para indicar se o computador está fazendo uma verificação no WSUS ou no Windows Update.  Quando o valor for 2, ele não verificará o WSUS.  
    - **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer**

2.  Há um novo atributo, **UseWUServer**, no nó **Windows Update** do Gerenciador de Recursos do Configuration Manager.  

3.  Crie uma coleção com base no atributo **UseWUServer** para todos os computadores que estão conectados por meio do WUfB para atualizações.  

4.  Crie uma configuração do agente cliente para desabilitar o fluxo de trabalho de atualização de software. Implante a configuração na coleção de computadores que estão conectados diretamente ao WUfB.  

5.  Os computadores gerenciados via WUfB exibirão **Desconhecido** no status de conformidade e não serão contados como parte do percentual de conformidade geral.  

## <a name="configure-windows-update-for-business-deferral-policies"></a>Configurar as políticas de adiamento do Windows Update for Business
<!-- 1290890 --> A partir do Configuration Manager versão 1706, você pode configurar as políticas de adiamento para as Atualizações de Recurso do Windows 10 ou Atualizações de Qualidade para dispositivos com Windows 10 gerenciados diretamente pelo Windows Update for Business. Você pode gerenciar as políticas de adiamento no novo nó **Políticas do Windows Update for Business** em **Biblioteca de Software** > **Manutenção do Windows 10**.

>[!NOTE] 
>A partir do Configuration Manager versão 1802, você pode definir políticas de adiamento para o programa Windows Insider. <!--507201-->Para obter mais informações sobre o programa Windows Insider, consulte [Introdução ao programa Windows Insider para Empresas](https://docs.microsoft.com/windows/deployment/update/waas-windows-insider-for-business).

### <a name="prerequisites"></a>Pré-requisitos
-   Windows 10 versão 1703 ou posterior
-   Os dispositivos Windows 10 gerenciados pelo Windows Update para Empresas precisam ter conectividade com a Internet

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Para criar uma política de adiamento do Windows Update for Business
1. Em **Biblioteca de Software** > **Manutenção do Windows 10** > **Políticas do Windows Update for Business**
2. Na guia **Início**, no grupo **Criar**, selecione **Criar a Política do Windows Update for Business** para abrir o Assistente de criação de política do Windows Update for Business.
3. Na página **Geral**, forneça um nome e uma descrição para a política.
4. Na página **Políticas de Adiamento**, defina se deseja adiar ou pausar as Atualizações de Recurso. Normalmente, as Atualizações de Recurso são recursos novos do Windows. Depois de definir a configuração **Nível de preparação do branch**, defina se, e por quanto tempo, você quer adiar o recebimento de Atualizações de Recurso após a disponibilização da Microsoft.
    - **Nível de preparação do branch**: defina o branch para o qual o dispositivo receberá atualizações do Windows (Branch Atual ou Branch Atual para Negócios).
    - **Período de adiamento (dias)**:  especifique o número de dias durante os quais as Atualizações de Recurso serão adiadas. Você pode adiar o recebimento dessas Atualizações de Recurso por um período de 365 dias a partir do lançamento.
    - **Pausar atualizações de recursos a partir de**: selecione se você quer pausar o recebimento de Atualizações de Recursos nos dispositivos durante um período de até 60 dias a contar do momento que você pausar as atualizações. Após o número máximo de dias, a funcionalidade de pausa expirará automaticamente, e o dispositivo verificará no Windows Update se há atualizações aplicáveis. Após essa verificação, você poderá pausar as atualizações novamente. Retome as Atualizações de Recurso desmarcando a caixa de seleção.   
5. Escolha se deseja adiar ou pausar as Atualizações de Qualidade. Normalmente, as Atualizações de Qualidade são correções e aprimoramentos funcionalidades existentes do Windows, e geralmente são publicadas na primeira terça-feira de cada mês, embora possam ser liberadas a qualquer momento pela Microsoft. Você pode definir se, e por quanto tempo, deseja adiar o recebimento das Atualizações de Qualidade após sua disponibilização.
    - **Período de adiamento (dias)**: especifique em quantos dias as Atualizações de Qualidade serão adiadas. Você pode adiar o recebimento dessas Atualizações de qualidade por um período de 30 dias a partir do lançamento.
    - **Pausar atualizações de qualidade a partir de**: selecione se você quer pausar o recebimento de Atualizações de Qualidade nos dispositivos durante um período de até 35 dias a contar do momento que você pausar as atualizações. Após o número máximo de dias, a funcionalidade de pausa expirará automaticamente, e o dispositivo verificará no Windows Update se há atualizações aplicáveis. Após essa verificação, você poderá pausar as atualizações novamente. Retome as Atualizações de Qualidade desmarcando a caixa de seleção.
6. Selecione **Instalar as atualizações de outros produtos da Microsoft** para habilitar a configuração da política de grupo que torna as configurações de adiamento aplicáveis ao Microsoft Update, bem como para o Windows Update.
7. Selecione **Incluir drivers com o Windows Update** para atualizar automaticamente os drivers de Windows Updates. Se você desmarcar essa configuração, as atualizações de driver não serão baixadas do Windows Update.
8. Conclua o assistente para criar a nova política de adiamento.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Para implantar uma política de adiamento do Windows Update for Business
1. Em **Biblioteca de Software** > **Manutenção do Windows 10** > **Políticas do Windows Update for Business**
2. Na guia **Início**, no grupo **Implantação**, selecione **Implantar a Política do Windows Update for Business**.
3. Defina as seguintes configurações:
    - **Política de configuração para implantação**: selecione a política do Windows Update para Empresas que você deseja implantar.
    - **Coleta**: clique em **Procurar** para selecionar a coleção de usuários na qual você deseja implantar a política.
    - **Corrigir regras não compatíveis quando houver suporte**: selecione para corrigir automaticamente quaisquer regras não compatíveis com o WMI (Instrumentação de Gerenciamento do Windows), o Registro, os scripts e todas as configurações de dispositivos móveis registrados pelo Configuration Manager.
    - **Permitir correção fora da janela de manutenção**: se uma janela de manutenção tiver sido configurada para a coleção na qual você está implantando a política, habilite esta opção para permitir que as configurações de conformidade corrijam o valor fora da janela de manutenção. Para obter mais informações sobre janelas de manutenção, consulte [Como usar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).
    - **Gerar um alerta**: configurará um alerta gerado se a conformidade da linha de base de configuração for menor que um percentual especificado por uma data e hora determinadas. Você também pode especificar se deseja que um alerta seja enviado para o System Center Operations Manager.
    - **Atraso aleatório (horas)**: especifica uma janela de atraso para evitar o processamento excessivo no Serviço de Registro de Dispositivo de Rede. O valor padrão é de 64 horas.
    - **Agendamento**: especifique o agendamento de avaliação de conformidade com base no qual o perfil implantado será avaliado em computadores cliente. O agendamento poderá ser simples ou personalizado. O perfil será avaliado por computadores cliente quando o usuário fizer logon.
4.  Conclua o assistente para implantar o perfil.
