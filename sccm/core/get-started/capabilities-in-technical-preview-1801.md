---
title: Technical Preview 1801 | Microsoft Docs
titleSuffix: Configuration Manager
description: Saiba mais sobre os recursos disponíveis no Technical Preview versão 1801 do System Center Configuration Manager.
ms.date: 01/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5a352ae0-355f-4fcf-b863-fb0654f51c52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: c0ce9a88e66e441749034dff3a6e0dc1dd6bc745
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133996"
---
# <a name="capabilities-in-technical-preview-1801-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1801 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1801. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview. 

Examine [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview) antes de instalar esta versão do technical preview. Este artigo familiariza você com os requisitos gerais e as limitações do uso de um technical preview, como atualizar entre versões e como fornecer comentários.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**Problemas conhecidos nesse Technical Preview:**
- **A atualização para uma versão prévia falha quando há um servidor do site no modo passivo**. Se você tiver um [servidor do site primário no modo passivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), deverá desinstalar o servidor do site no modo passivo antes de atualizar para esta nova versão de visualização. Você pode reinstalar o servidor de site no modo passivo após a conclusão da instalação pelo site.

  Para desinstalar o servidor do site no modo passivo:
  1. No console do Configuration Manager, acesse **Administração** > **Visão Geral** > **Configuração do Site** > **Servidores e Funções do Sistema de Sites** e, em seguida, selecione o servidor do site no modo passivo.
  2. No painel **Funções do Sistema de Sites**, clique com o botão direito do mouse na função **Servidor do Site** e, em seguida, escolha **Remover Função**.
  3. Clique com o botão direito no servidor do site de modo passivo e, em seguida, escolha **Excluir**.
  4. Após a desinstalação do servidor do site, no servidor do site primário ativo, reinicie o serviço **CONFIGURATION_MANAGER_UPDATE**.
  <!--sms 489412-->


**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.
 -  Task 1
 -  Task 2              
-->



## <a name="create-phased-deployments"></a>Criar implantações em fases
<!-- 1357405 --> as implantações em fases automatizam uma distribuição coordenada e sequenciada do software sem criar várias implantações. Nesta versão de Technical Preview, o assistente de implantação em fases pode ser concluído para sequências de tarefas no console do administrador. No entanto, as implantações não são criadas. 

### <a name="try-it-out"></a>Experimente!  
  Tente concluir as tarefas. Em seguida, envie **Comentários** da guia **Início** da faixa de opções, nos informando como isso funcionou.
 
**Criar uma implantação em fases para uma sequência de tarefas** </br>
1. No workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione **Sequências de Tarefas**.
2. Clique com o botão direito do mouse em uma sequência de tarefas existente e selecione **Criar Implantação em Fases**. 
3. Sobre o guia **Geral**, nomeie a implantação em fases, descrição (opcional) e selecione **Criar automaticamente as fases de piloto e de produção padrão**. 
4. Popule os campos **Coleção piloto** e **Coleção de produção**. Selecione **Avançar**.
5. Na guia **Configurações**, escolha uma opção para cada uma das configurações de agendamento e selecione **Próximo** quando concluir. 
6. Na guia **Fases**, edite qualquer uma das fases se necessário e clique em **Próximo**.
7. Confirme suas seleções na guia **Resumo** e clique em **Próximo** para continuar.

## <a name="co-management-reporting"></a>Relatórios de cogerenciamento
<!-- 1356648 --> Se estiver usando as funcionalidades de [cogerenciamento](/sccm/core/clients/manage/co-management-overview), agora você poderá exibir um painel com informações sobre cogerenciamento em seu ambiente. No console do Configuration Manager, navegue até o workspace **Monitoramento**, expanda **Upgrade Readiness** e selecione o painel **Cogerenciamento**. O painel inclui os seguintes blocos:
- **Dispositivos cogerenciados**: o percentual de dispositivos no ambiente habilitados por você para cogerenciamento
- **Distribuição do SO**: a divisão dos sistemas operacionais por versão. Este gráfico usa os seguintes agrupamentos:
  - Windows 7 e 8.x
  - Windows 10 inferior a 1709
  - Windows 10 1709 e posterior
    > [!NOTE] 
    > O Windows 10 versão 1709 e posterior é um pré-requisito para o cogerenciamento
- **Status de cogerenciamento**: a divisão de êxito ou falha do dispositivo nas seguintes categorias:
   - Sucesso, Ingressado no Azure AD híbrido
   - Sucesso, Ingressado no Azure AD
   - Falha: falha no registro automático
- **Transição de carga de trabalho**: um gráfico de barras mostra o número de dispositivos cuja transição foi para o Microsoft Intune foi realizada por você para as três cargas de trabalho disponíveis: 
   - Políticas de conformidade
   - Acesso de Recurso
   - Windows Update for Business

### <a name="prerequisites"></a>Pré-requisitos
- O computador que executa o console do Configuration Manager requer o Internet Explorer 9 ou posterior.



## <a name="improvements-to-automatic-deployment-rule-evaluation-schedule"></a>Melhorias ao agendamento de avaliação da regra de implantação automática
<!-- 1357133 --> Com base nos [comentários no UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8819518-software-update-patch-tuesday-scheduling), agora você pode agendar avaliação da ADR (regra de implantação automática) para o deslocamento de um dia base. Por exemplo, um deslocamento de dois dias após a segunda terça-feira do mês faz com que a regra seja avaliada na quinta-feira. 

### <a name="try-it-out"></a>Experimente!  
 Tente concluir as tarefas. Em seguida, envie **Comentários** da guia **Início** da faixa de opções, nos informando como isso funcionou. <br/>

**Criar uma agenda personalizada que realiza avaliações e o deslocamento da ADR em relação a um dia base** </br>
1.  No workspace **Biblioteca de Software**, expanda **Atualizações de Software** e selecione **Regras de Implantação Automática**.
2. Clique com o botão direito do mouse em **Regras de Implantação Automática** e escolha **Criar Regra de Implantação Automática**. 
3. Siga os prompts para concluir as guias **Geral**, **Configurações de Implantação** e **Atualizações de Software**. 
4. Na guia **Agendamento de Avaliação**, selecione **Executar a Regra em um agendamento** e **Personalizar**.
5. Para o agendamento personalizado, selecione **Mensal** e coloque-o em um dia base, tal como a segunda terça-feira. 
6. Clique em **Deslocamento (dias)** e no número de dias para o deslocamento, depois em **OK** quando terminar.  
7. Conclua o restante do **Assistente de Criação de Regra de Implantação Automática**. 



## <a name="reassign-distribution-point"></a>Reatribuir ponto de distribuição
<!-- 1306937 --> Muitos clientes têm amplas infraestruturas do Configuration Manager e estão reduzindo sites primários ou secundários para simplificar os ambientes deles. Eles ainda precisam manter os pontos de distribuição de localizações de filiais para fornecer conteúdo para clientes gerenciados. Esses pontos de distribuição geralmente contêm vários terabytes de conteúdo ou mais. Distribuir esse conteúdo para esses servidores remotos custa muito em termos de largura de banda de rede e de tempo. 

Este recurso permite reatribuir um ponto de distribuição para outro site primário sem redistribuir o conteúdo. Esta ação atualiza a atribuição de sistema, persistindo todo o conteúdo no servidor. Se você precisar reatribuir vários pontos de distribuição, primeiro execute essa ação em um único ponto de distribuição e, em seguida, prossiga com servidores adicionais, um por vez.

> [!IMPORTANT]
> O servidor do sistema de sites só pode hospedar a função de ponto de distribuição. Se o servidor do sistema de sites hospedar outra função de servidor do Configuration Manager, tal como o ponto de migração de estado, você não poderá reatribuir o ponto de distribuição. Você não pode reatribuir um ponto de distribuição de nuvem. 

Essa opção não está funcionando com esta versão devido ao limite de um único site primário para o Technical Preview. Considere o cenário e, em seguida, da guia **Início** da faixa de opções, envie **Comentários** sobre os recursos desta ação.
1. No console do Configuration Manager, vá até o workspace **Administração** e selecione o nó **Pontos de Distribuição**.
2. Clique com o botão direito do mouse no ponto de distribuição de destino e selecione **Reatribuir Ponto de Distribuição**. 
  ![Reatribuir Ponto de Distribuição](media/1306937-reassign-dp.png)
3. Selecione o servidor do site e o código do site ao qual você deseja reatribuir este ponto de distribuição. 
  ![Selecionar um Servidor do Site](media/1306937-select-site.png)



## <a name="improvements-to-hardware-inventory"></a>Melhorias ao inventário de hardware
<!-- 1357389 --> Para classes recém-adicionadas, tamanhos de cadeia de caracteres maiores que 255 caracteres podem ser especificados para as propriedades de inventário de hardware que não são chaves.

### <a name="try-it-out"></a>Experimente!  
Tente concluir as tarefas. Em seguida, envie **Comentários** da guia **Início** da faixa de opções, nos informando como isso funcionou.<br/>

1. No workspace **Administração**, clique em **Configurações do Cliente**, realce uma configuração de dispositivo cliente a ser editada, clique com o botão direito do mouse e selecione **Propriedades**. 
2. Selecione **Inventário de Hardware** e, em seguida, **Definir Classes** e **Adicionar**.
3. Clique no botão **Conectar**.
4. Preencha **Nome do Computador**, **Namespace do WMI**, selecione **recursivo** se necessário. Forneça credenciais, se necessário, para se conectar. Clique em **Conectar** para exibir as classes do namespace.
5. Selecione uma nova classe e clique em **Editar**.
6. Altere o **Comprimento** de pelo menos uma propriedade que é uma cadeia de caracteres, não uma chave, tornando-o maior que 255. Clique em **OK**. 
7. Certifique-se de que a propriedade editada está selecionada para **Adicionar Classe de Inventário de Hardware** e clique em **OK**. 
8. Colete o inventário de hardware com a classe recém-adicionada que contém uma propriedade com tamanho maior que 255 caracteres. 



## <a name="improvements-to-client-settings-for-software-center"></a>Melhorias às configurações do cliente para o Centro de Software
<!-- 1351224 & 1355146 --> Nesta versão do Technical Preview, foram feitas melhorias na personalização do Centro de Software nas configurações do cliente. 

1. As configurações do cliente para o Centro de Software agora têm um botão **Personalizar**.
2. Uma visualização foi adicionada para mostrar a aparência da faixa do Centro de Software.<!--1351224-->
    - Se um logotipo não estiver selecionado, a visualização mostrará a cor e o texto do nome da empresa.
    - Se um logotipo estiver selecionado, a visualização mostrará o logotipo e o texto do nome da empresa.  
3.  **Ocultar aplicativos não aprovados no Centro de Software** é uma nova configuração do Centro de Software. Quando essa opção é habilitada, os aplicativos disponíveis do usuário que requerem aprovação são ocultos no Centro de Software.<!--1355146-->

### <a name="try-it-out"></a>Experimente!  
 Tente concluir as tarefas. Em seguida, envie **Comentários** da guia **Início** da faixa de opções, nos informando como isso funcionou.

1. No workspace **Administração**, clique em **Configurações do Cliente**. Selecione uma configuração de dispositivo do cliente a ser editada. Clique com o botão direito do mouse nela e selecione **Propriedades**, depois **Centro de Software**.
2.  Clique no botão **Personalizar**. Teste as diferentes configurações de personalização, incluindo a visualização.
3. Habilite a configuração **Ocultar aplicativos não aprovados no Centro de Software**. Observe as alterações no Centro de Software. 



## <a name="new-settings-for-windows-defender-application-guard"></a>Novas configurações para o Windows Defender Application Guard
<!-- 1356256 --> Para dispositivos Windows 10 versão 1709 e posteriores, há duas novas configurações de interação de host para o [Windows Defender Application Guard](/sccm/protect/deploy-use/create-deploy-application-guard-policy). 
1. O acesso ao processador de gráficos virtuais do host pode ser concedido a sites. 
2. Arquivos baixados dentro do contêiner podem ser persistentes no host. </br>



## <a name="improvements-to-run-scripts"></a>Melhorias ao recurso Executar Scripts
<!-- 1236459 --> O [recurso **Executar Scripts**](/sccm/apps/deploy-use/create-deploy-scripts) agora permite importar e executar scripts assinados do PowerShell. 
- Para manter a integridade de script, scripts assinados devem ser importados em vez de copiados/colados. 
- Scripts assinados importados não podem ser editados após a importação.
    
>[!IMPORTANT]
>Neste Technical Preview, existem duas limitações temporárias.
>- Scripts só podem ser importados no recurso Executar Scripts e não podem ser editados diretamente do console.
>- Scripts importados com uma codificação não Unicode podem ser exibidos no console incorretamente. O script ainda será executado conforme escrito originalmente.





## <a name="next-steps"></a>Próximas etapas
Para obter informações de como instalar ou atualizar o branch da technical preview, consulte [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
