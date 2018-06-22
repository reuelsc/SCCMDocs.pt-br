---
title: Criar uma implantação em fases para uma sequência de tarefas
titleSuffix: Configuration Manager
description: Criar implantações em fases para sequências de tarefas
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2bda41cfd01e5ef90771350e650f68a27c3af6ed
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32348626"
---
# <a name="create-phased-deployments-for-a-task-sequence-with-system-center-configuration-manager"></a>Criar implantações em fases para uma sequência de tarefas com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As implantações em fases automatizam uma distribuição coordenada e sequenciada de uma sequência de tarefas em várias coleções. Crie implantações em fases com o padrão de duas fases ou configure várias fases manualmente. A implantação em fases de sequências de tarefas não dá suporte ao PXE e à mídia de instalação. 

>[!NOTE]
> As implantações em fases são um recurso de pré-lançamento introduzido no Configuration Manager 1802. <!--1356837-->

## <a name="security-scope-and-log-file-information"></a>Informações sobre o escopo de segurança e arquivos de log

**Escopo de segurança**:</br>
As implantações criadas por Implantações em Fases não são visíveis para qualquer pessoa que não tem o escopo de segurança **Todos**.

**Arquivos de log**: </br>
SMS_PhasedDeployment.log

## <a name="create-a-default-two-phased-deployment-for-a-task-sequence"></a>Criar uma implantação em fases padrão para uma sequência de tarefas

Use as instruções a seguir para criar uma implantação em fases. 

1. No espaço de trabalho **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione **Sequências de Tarefas**.

2. Clique com o botão direito do mouse em uma sequência de tarefas existente e selecione **Criar Implantação em Fases**. 

3. Na guia **Geral**, nomeie a implantação em fases e lhe dê uma descrição (opcional), em seguida, selecione **Criar automaticamente uma implantação de duas fases padrão**. 

4. Preencha os campos **Primeira coleção** e **Segunda coleção**. Selecione **Avançar**.

5. Na guia **Configurações**, escolha uma opção para cada uma das configurações de agendamento e selecione **Próximo** quando concluir. 
    - **Critérios para o sucesso da primeira fase.** 
        - **Percentual de sucesso da implantação** – especifique o percentual de dispositivos que concluíram com êxito a implantação de acordo com os critérios de sucesso da fase. 
    - **Condições para o início da segunda fase de implantação após o sucesso da primeira fase** (escolha uma opção):
        - **Iniciar automaticamente esta fase após um período de adiamento (em dias)** – escolha o número de dias de espera antes do início da segunda fase após o sucesso da primeira. 
        - **Iniciar manualmente a segunda fase da implantação** – não inicie a segunda fase automaticamente após o sucesso da primeira. Exija que ela seja iniciada manualmente. 
    - **Depois que um dispositivo for direcionado, instalar o software** (escolha uma opção):
        - **Assim que possível** – define a data limite da instalação no dispositivo assim que o dispositivo é direcionado.
        - **Hora limite (em relação à hora em que o dispositivo é direcionado)** – define a data limite da instalação com determinado número de dias depois que o dispositivo é direcionado. 

6. Na guia **Fases**, clique na primeira fase e, em seguida, em **Editar**.  Especifique **Experiência do Usuário** como **Notificações do Usuário** e **Tratamento de filtro de gravação para dispositivos Windows Embedded**. Clique em **Aplicar**.

7. Especifique as configurações de **Pontos de Distribuição** da fase na guia **Pontos de Distribuição**. Clique em **Aplicar** e em **OK**.        

8. Na guia **Fases**, edite **Experiência do Usuário** e **Pontos de Distribuição** para a segunda fase. Clique em **Aplicar** e em **OK**.

9. Confirme as seleções na guia **Resumo** e, em seguida, clique em **Avançar** e continue com o assistente.

>[!WARNING]
>As implantações em fases não notificarão você se uma implantação de sequência de tarefas for de [alto risco](/sccm/protect/understand/settings-to-manage-high-risk-deployments.md). 


## <a name="suspend-and-resume-phases-or-move-to-the-next-phase"></a>Suspender e retomar fases ou ir para a próxima fase
Ocasionalmente, talvez você precise suspender manualmente uma implantação em fases, retomar uma implantação em fases suspensa ou ir para a próxima fase. 

### <a name="move-to-the-next-phase"></a>Ir para a próxima fase
Ao selecionar a configuração **Iniciar manualmente a segunda fase da implantação**, será necessário iniciar a segunda fase. Use as seguintes instruções para ir para a segunda fase: 

1. No console do Configuration Manager, selecione **Biblioteca de Software**, expanda **Sistemas Operacionais** e clique em **Sequências de Tarefas**.
2. Realce a sequência de tarefas.
3. Clique na guia **Implantação em Fases** na parte inferior do console. 
4. Clique com o botão direito do mouse na implantação em fases e selecione **Ir para a próxima fase**.
![Suspender, retomar ou ir para a próxima fase](media/Suspend-phased-deployment.PNG)

### <a name="suspend-or-resume-a-phased-deployment"></a>Suspender ou retomar uma implantação em fases
1. No console do Configuration Manager, selecione **Biblioteca de Software**, expanda **Sistemas Operacionais** e clique em **Sequências de Tarefas**.
2. Selecione a sequência de tarefas e clique na guia **Implantação em Fases** na parte inferior do console. 
3. Selecione a implantação em fases e clique em **Suspender** ou **Retomar** na faixa de opções.

## <a name="next-steps"></a>Próximas etapas
[Criar uma sequência de tarefas personalizada](create-a-custom-task-sequence.md) </br>
[Criar uma sequência de tarefas para implantações que não são de sistema operacional](create-a-task-sequence-for-non-operating-system-deployments.md). 








