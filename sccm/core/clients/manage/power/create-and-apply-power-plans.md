---
title: Criar e aplicar planos de energia | System Center Configuration Manager
description: Criar e aplicar planos de energia no System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 738eddaa-52e2-467f-b453-821ef2884d47
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 18017c64aa6e6769a1ea0921274d05625e99610d


---
# <a name="how-to-create-and-apply-power-plans-in-system-center-configuration-manager"></a>Como criar e aplicar planos de energia no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O gerenciamento de energia no System Center Configuration Manager permite que você aplique planos de energia fornecidos com o Configuration Manager a coleções de computadores em sua hierarquia ou crie seus próprios planos de energia personalizados. Use o procedimento descrito neste tópico para aplicar um plano de energia interno ou personalizado aos computadores.  

> [!IMPORTANT]  
>  Só é possível aplicar os planos de energia do Configuration Manager a coleções de dispositivos.  

 Se um computador for membro de várias coleções, e a cada um for aplicável um plano de energia diferente, as seguintes ações serão executadas:  

-   Plano de energia: se vários valores para as configurações de energia forem aplicados a um computador, o valor menos restritivo será usado.  

-   Hora de ativação: se várias horas de ativação forem aplicadas a um computador desktop, a hora mais próxima à meia-noite será usada.  

 Use o relatório **Computadores com vários planos de energia** para exibir todos os computadores que têm vários planos de energia aplicados a eles. Isso pode ajudá-lo a descobrir os computadores que apresentam conflitos de energia. Para obter mais informações sobre relatórios de gerenciamento de energia, consulte [Como monitorar e planejar o gerenciamento de energia no System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

> [!IMPORTANT]  
>  As configurações de energia definidas usando a Política de Grupo do Windows substituirão as configurações definidas pelo gerenciamento de energia do Configuration Manager.  

 Use o procedimento a seguir para criar e aplicar um plano de energia do Configuration Manager.  

### <a name="to-create-and-apply-a-power-plan"></a>Para criar e aplicar um plano de energia  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Coleções de Dispositivos**.  

3.  Na lista **Coleções de Dispositivos** , clique na coleção à qual deseja aplicar as configurações de gerenciamento de energia e, na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Na guia **Gerenciamento de Energia** da caixa de diálogo *Propriedades\>***<Nome de Coleção**, selecione **Especificar configurações de gerenciamento de energia para esta coleção**.  

    > [!NOTE]  
    >  Você também pode clicar em **Procurar** e copiar as configurações do gerenciamento de energia de uma coleção selecionada para a coleção selecionada.  

5.  Nos campos **Início** e **Término** , especifique as horas de início e de término do horário de pico (ou comercial).  

6.  Habilite a **Hora de ativação (computadores desktops)** para especificar uma hora em que um computador desktop sairá do modo de suspensão ou hibernação para instalar atualizações agendadas ou instalações de software.  

    > [!IMPORTANT]  
    >  O gerenciamento de energia usa o recurso de tempo de ativação interno do Windows para que os computadores saiam do modo de suspensão ou hibernação. As configurações da hora de ativação não são aplicadas a computadores portáteis, para evitar cenários em que possam ser ativados quando não estiverem conectados. O tempo de ativação é aleatório e os computadores serão ativados durante o período de uma hora a partir do horário de ativação especificado.  

7.  Se quiser configurar um plano de energia personalizado para o horário de pico (ou comercial), selecione **Horário de Pico Personalizado (ConfigMgr)** na lista suspensa **Plano do Horário de Pico** e clique em **Editar**. Se quiser configurar um plano de energia para o horário fora de pico (ou fora do horário comercial), selecione **Horário Fora de Pico Personalizado (ConfigMgr)** na lista suspensa **Plano do Horário Fora de Pico** e clique em **Editar**.  

    > [!NOTE]  
    >  Você pode usar o relatório **Atividade do computador** para ajudá-lo a decidir os agendamentos a ser usados para o horário de pico e fora de pico quando aplicar os planos de energia às coleções de computadores. Para mais informações, consulte [Como monitorar e planejar o gerenciamento de energia no System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

     Também é possível selecionar **Equilibrado (ConfigMgr)**, **Alto Desempenho (ConfigMgr)** e **Economia de Energia (ConfigMgr)**nos planos de energia internos e depois clicar em **Exibição** para exibir as propriedades de cada plano de energia.  

    > [!NOTE]  
    >  Não é possível modificar os planos de energia internos.  

8.  Na caixa de diálogo *Propriedades\>***<nome do plano de energia**, defina as seguintes configurações:  

    -   **Nome:** especifique um nome para esse plano de energia ou use o valor padrão fornecido.  

    -   **Descrição:**  especifique uma descrição para esse plano de energia ou use o valor padrão fornecido.  

    -   **Especificar as propriedades para este plano de energia:** configure as propriedades do plano de energia. Para desabilitar uma propriedade, desmarque a caixa de seleção. Para obter mais informações sobre as configurações disponíveis, veja [Available power management plan settings](#BKMK_Plans) neste tópico.  

        > [!IMPORTANT]  
        >  As configurações habilitadas são aplicadas aos computadores quando o plano de energia é aplicado. Se você desmarcar uma caixa de seleção da configuração de energia, o valor no computador cliente não será alterado quando o plano de energia é aplicado. Desmarcar uma caixa de seleção não restaura a configuração de energia para seu valor anterior à aplicação de um plano de energia.  

9. Clique em **OK** para fechar a caixa de diálogo *Propriedades\>***<nome do plano de energia**.  

10. Clique em **OK** para fechar a caixa de diálogo *Configurações\>***<Nome da Coleção** e aplicar o plano de energia.  

##  <a name="a-namebkmkplansa-available-power-management-plan-settings"></a><a name="BKMK_Plans"></a> Configurações de plano de gerenciamento de energia disponíveis  
 A tabela a seguir lista as configurações de gerenciamento de energia disponíveis no Configuration Manager. Você pode definir configurações separadas para quando o computador estiver conectado ou funcionando com bateria. Dependendo da versão do Windows que você está usando, algumas configurações podem não ser configuráveis.  

> [!NOTE]  
>  As configurações de energia que não forem definidas manterão seu valor atual nos computadores cliente.  

|Nome|Descrição|  
|----------|-----------------|  
|**Desligar o monitor após (minutos)**|Especifica o período de tempo, em minutos, em que o computador deverá ficar inativo antes que a tela seja desligada. Especifique um valor de **0** se você não quiser que o gerenciamento de energia desligue a tela.|  
|**Suspensão após (minutos)**|Especifica o período de tempo, em minutos, em que o computador deverá ficar inativo antes de entrar no modo de suspensão. Especifique um valor de **0** se não quiser que o gerenciamento de energia entre no modo de suspensão no computador.|  
|**Exigir uma senha durante a ativação**|Um valor **Sim** ou **Não** especifica se uma senha é necessária para desbloquear o computador quando ele entra a ativação do modo de suspensão.|  
|**Ação do botão de energia**|Especifica a ação executada quando o botão de energia do computador é pressionado. Especifica a ação que ocorre quando o usuário fecha a tampa de um computador portátil. Os valores possíveis são **Não fazer nada**, **Suspender**, **Hibernar** e **Desligar**.|  
|**Botão de energia do menu Iniciar**|Especifica a ação que ocorre quando você pressiona o botão de energia do menu **Iniciar** do computador. Especifica a ação que ocorre quando o usuário fecha a tampa de um computador portátil. Os valores possíveis são **Suspender**, **Hibernar** e **Desligar**.|  
|**Ação do botão Suspender**|Especifica a ação que ocorre quando você pressiona o botão **Suspensão** do computador. Especifica a ação que ocorre quando o usuário fecha a tampa de um computador portátil. Os valores possíveis são **Não fazer nada**, **Suspender**, **Hibernar** e **Desligar**.|  
|**Ação de fechamento da tampa**|Especifica a ação que ocorre quando o usuário fecha a tampa de um computador portátil. Os valores possíveis são **Não fazer nada**, **Suspender**, **Hibernar** e **Desligar**.|  
|**Desligar o disco rígido após (minutos)**|Especifica o período de tempo, em minutos, em que o disco rígido do computador deverá ficar inativo antes que ele seja desligado. Especifique um valor de **0** se você não quiser que o gerenciamento de energia desligue o disco rígido do computador.|  
|**Hibernação após (minutos)**|Especifica o período de tempo, em minutos, em que o computador deverá ficar inativo antes de entrar no modo de hibernação. Especifique um valor de **0** se não quiser que o gerenciamento de energia entre no modo de hibernação no computador.|  
|**Ação de bateria fraca**|Especifica a ação que ocorre quando a bateria do computador atinge o nível de notificação de bateria fraca especificado. Especifica a ação que ocorre quando o usuário fecha a tampa de um computador portátil. Os valores possíveis são **Não fazer nada**, **Suspender**, **Hibernar** e **Desligar**.|  
|**Ação de bateria crítica**|Especifica a ação executada quando a bateria do computador atinge o nível de notificação de bateria crítica especificado. Especifica a ação que ocorre quando o usuário fecha a tampa de um computador portátil. Os valores possíveis incluem **Suspender**, **Hibernar** e **Desligar**.|  
|**Permitir suspensão híbrida**|Selecionar o valor **On** ou **Off** especifica se o Windows salva um arquivo de hibernação quando entrando em suspensão, o que pode ser usado para restaurar o estado do computador em caso de perda de energia enquanto ele entrou em suspensão.<br /><br /> A suspensão híbrida foi projetada para computadores desktop e, por padrão, não está habilitada em computadores portáteis. Em computadores que executam o Windows 7, a habilitação da suspensão híbrida desabilita a funcionalidade de hibernação.|  
|**Permitir estado de espera durante a ação de suspensão**|Selecionar o valor **On** ou **Off** permite que o computador esteja em espera, o que ainda consome alguns energia, mas permite que o computador seja ativado mais rapidamente. Se essa configuração for definida como **Desligado**, o computador poderá apenas hibernar ou ser desligado.|  
|**Ociosidade necessária para suspensão (%)**|Especifica o percentual de tempo ocioso no tempo do processador do computador necessário para que o computador entre no modo de suspensão. Para computadores que executam o Windows 7, esse valor é sempre definido como **0**.|  
|**Habilitar o temporizador de ativação do Windows para computadores desktop**|Selecionar o valor **Habilitar** ou **Desabilitar** pode habilitar o temporizador interno do Windows a ser usado pelo gerenciamento de energia para ativar um computador desktop. Quando um computador desktop é ativado usando o temporizador de ativação do Windows, ele permanecerá ativo por 10 minutos por padrão para permitir que computador tenha tempo para instalar quaisquer atualizações ou receber a política.<br /><br /> Não há suporte para temporizadores de ativação em computadores portáteis, para evitar cenários em que possam ser ativados quando não estiverem conectados.|  



<!--HONumber=Nov16_HO1-->


