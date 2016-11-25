---

title: "Introdução às atualizações de software | Configuration Manager"
description: "Tenha noções básicas sobre atualizações de software no System Center Configuration Manager."
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
ms.assetid: e9778b13-c8a3-40eb-8655-34ac8ce9cdaa
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e41f91b9f796cb6a1a8eb2a500c7f615e07d60ac



---
# <a name="introduction-to-software-updates-in-system-center-configuration-manager"></a>Introdução às atualizações de software no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As atualizações de software no System Center Configuration Manager fornecem um conjunto de ferramentas e recursos que podem ajudar a gerenciar a tarefa complexa de acompanhar e aplicar atualizações de software aos computadores cliente da empresa. Um processo eficiente de gerenciamento de atualização de software é necessário para manter a eficiência operacional, solucionar problemas de segurança e manter a estabilidade da infraestrutura de rede. No entanto, devido à natureza variável da tecnologia e ao aparecimento contínuo de novas ameaças à segurança, a eficiência do gerenciamento de atualização de software exige atenção consistente e contínua.  

Para obter um exemplo que mostra como você pode implantar atualizações de software em seu ambiente, consulte [Cenário de exemplo para implantar atualizações de software de segurança](../deploy-use/example-scenario-deploy-monitor-monthly-security-updates.md).  

##  <a name="a-namebkmksynchronizationa-software-updates-synchronization"></a><a name="BKMK_Synchronization"></a> Sincronização das atualizações de software  
 A sincronização de atualizações de software no Configuration Manager usa o Microsoft Update para recuperar metadados de atualizações de software. O site de nível superior (site de administração central ou site primário autônomo) sincroniza com o Microsoft Update em um horário agendado ou quando você inicia a sincronização manualmente no console do Configuration Manager. Quando o Configuration Manager terminar a sincronização das atualizações de software no site de nível superior, a sincronização das atualizações de software se iniciará nos sites filho, se existirem. Quando sincronização termina em cada site primário ou secundário, uma política de site é criada para fornecer aos computadores cliente o local dos pontos de atualização de software.  

> [!NOTE]  
>  As atualizações de software são habilitadas por padrão nas configurações do cliente. No entanto, se você não definir a configuração do cliente **Habilitar as atualizações de software em clientes** para **Não** para desabilitar as atualizações de software em um coleção ou nas configurações padrão, o local dos pontos de atualização de software não será enviado aos clientes associados. Para obter detalhes, veja [Configurações do cliente para atualizações de software](../../core/clients/deploy/about-client-settings.md#BKMK_SoftwareUpdatesDeviceSetting).  

 Depois que o cliente recebe a política, ele inicia uma verificação da conformidade das atualizações de software e grava as informações no WMI (Windows Management Instrumentation). Em seguida, as informações de conformidade são enviadas ao ponto de gerenciamento que, por sua vez, envia as informações ao servidor do site. Para obter mais informações sobre avaliação de conformidade, consulte a seção [Software updates compliance assessment](#BKMK_SUMCompliance) neste tópico.  

 É possível instalar vários pontos de atualização de software em um site primário. O primeiro ponto de atualização de software que você instala é configurado como a origem da sincronização. A sincronização acontece no Microsoft Update ou em um servidor WSUS, não na hierarquia do Configuration Manager. Os outros pontos de atualização de software do site usam o primeiro ponto de atualização de software como a origem da sincronização.  

> [!NOTE]  
>  Quando o processo de sincronização de atualizações de software termina no site de nível superior, os metadados das atualizações de software são replicados nos sites filho por meio da replicação de banco de dados. Ao conectar um console do Configuration Manager ao site filho, o Configuration Manager exibe os metadados das atualizações de software. No entanto, até você instalar e configurar um ponto de atualização de software no site, os clientes não verificarão a conformidade das atualizações de software, não relatarão informações de conformidade para o Configuration Manager, e você não poderá implantar atualizações de software com êxito.  

### <a name="synchronization-on-the-top-level-site"></a>Sincronização no site de nível superior  
 O processo de sincronização de atualizações de software no site de nível superior recupera do Microsoft Update os metadados das atualizações de software que atendem aos critérios especificados em Propriedades do Componente de Ponto de Atualização de Software. Você define os critérios apenas no site de nível superior.  

> [!NOTE]  
>  É possível especificar um servidor WSUS existente que não está na hierarquia do Configuration Manager, em vez de Microsoft Updates como a origem da sincronização.  

 A lista a seguir descreve as etapas básicas do processo de sincronização no site de nível superior:  

1.  A sincronização de atualizações de software inicia.  

2.  O Gerenciador de Sincronização do WSUS envia uma solicitação ao WSUS em execução no ponto de atualização de software para iniciar a sincronização com o Microsoft Update.  

3.  Os metadados das atualizações de software são sincronizados no Microsoft Update e as alterações são inseridas ou atualizadas no banco de dados do WSUS.  

4.  Quando o WSUS termina a sincronização, o Gerenciador de Sincronização do WSUS sincroniza os metadados das atualizações de software do banco de dados do WSUS com o banco de dados do Configuration Manager, e as alterações após a última sincronização são inseridas ou atualizadas no banco de dados do site. Os metadados das atualizações de software são armazenados no banco de dados do site como item de configuração.  

5.  Os itens de configuração das atualizações de software são enviados aos sites filho por meio da replicação de banco de dados.  

6.  Quando a sincronização termina com êxito, o Gerenciador de Sincronização do WSUS cria a mensagem de status 6702.  

7.  O Gerenciador de Sincronização do WSUS envia uma solicitação de sincronização para todos os sites filho.  

8.  O Gerenciador de Sincronização do WSUS envia uma solicitação por vez ao WSUS em execução em outros pontos de atualização de software do site. Os servidores WSUS dos outros pontos de atualização de software são configurados para serem réplicas do WSUS em execução no ponto de atualização de software padrão do site.  

### <a name="synchronization-on-child-primary-and-secondary-sites"></a>Sincronização em sites primários e secundários filho  
 Durante o processo de sincronização de atualizações de software no site de nível superior, os itens de configuração das atualizações de software são replicados nos sites filho por meio da replicação de banco de dados. No fim do processo, o site de nível superior envia uma solicitação de sincronização ao site filho, que inicia a sincronização do WSUS. A lista a seguir fornece as etapas básicas do processo de sincronização em um site primário ou secundário filho:  

1.  O Gerenciador de Sincronização do WSUS recebe uma solicitação de sincronização do site de nível superior.  

2.  A sincronização de atualizações de software inicia.  

3.  O Gerenciador de Sincronização do WSUS faz uma solicitação para o WSUS em execução no ponto de atualização de software para iniciar a sincronização.  

4.  O WSUS em execução no ponto de atualização de software no site filho sincroniza os metadados de atualizações de software do WSUS em execução no ponto de atualização de software no site pai.  

5.  Quando a sincronização termina com êxito, o Gerenciador de Sincronização do WSUS cria a mensagem de status 6702.  

6.  Em um site primário, o Gerenciador de Sincronização do WSUS envia uma solicitação de sincronização para qualquer site secundário filho. O site secundário inicia a sincronização das atualizações de software com o site primário pai. O site secundário é configurado como uma réplica do WSUS em execução no site pai.  

7.  O Gerenciador de Sincronização do WSUS envia uma solicitação por vez ao WSUS em execução em outros pontos de atualização de software do site. Os servidores WSUS dos outros pontos de atualização de software são configurados para serem réplicas do WSUS em execução no ponto de atualização de software padrão do site.  

##  <a name="a-namebkmksumcompliancea-software-updates-compliance-assessment"></a><a name="BKMK_SUMCompliance"></a> Avaliação de conformidade das atualizações de software  
 Antes de você implantar atualizações de software em computadores cliente no Configuration Manager, inicie a verificação da conformidade das atualizações de software nos computadores cliente. Para cada atualização de software, uma mensagem de estado é criada contendo o estado de conformidade da atualização. As mensagens de estado são enviadas em massa para o ponto de gerenciamento e depois para o servidor do site, onde o estado de conformidade é inserido no banco de dados do site. O estado de conformidade das atualizações de software é exibido no console do Configuration Manager. Você pode implantar e instalar atualizações de software nos computadores que precisam dessas atualizações. As seções a seguir fornecem informações sobre os estados de conformidade e descreve o processo da verificação da conformidade das atualizações de software.  

### <a name="software-updates-compliance-states"></a>Estados de conformidade das atualizações de software  
 A seguir veja uma lista e descrição de cada estado de conformidade que é exibido no console do Configuration Manager para as atualizações de software.  

-   **Necessária**  

     Especifica que a atualização de software é aplicável e necessária no computador cliente. Qualquer uma das condições a seguir pode ser válida quando o estado da atualização de software é **Necessária**:  

    -   A atualização de software não foi implantada no computador cliente.  

    -   A atualização de software foi instalada no computador cliente. No entanto, a mensagem de estado mais recente ainda não foi inserida no banco de dados do servidor do site. O computador cliente repete a verificação da atualização após o término da instalação. Pode haver um atraso de até dois minutos para o cliente enviar o estado atualizado ao ponto de gerenciamento que, por sua vez, encaminha o estado atualizado ao servidor do site.  

    -   A atualização de software foi instalada no computador cliente. No entanto, a instalação da atualização de software requer a reinicialização do computador para ser concluída.  

    -   A atualização de software foi implantada no computador cliente, mas ainda não foi instalada.  

-   **Não necessário**  

     Especifica que a atualização de software não é aplicável no computador cliente. Portanto, a atualização de software não é necessária.  

-   **Instalado**  

     Especifica que a atualização de software é aplicável ao computador cliente e que o computador cliente já tem a atualização de software instalada.  

-   **Desconhecida**  

     Especifica que o servidor do site não recebeu uma mensagem de estado do computador cliente, normalmente porque:  

    -   O computador cliente não verificou com êxito a conformidade das atualizações de software.  

    -   A verificação foi concluída com êxito no computador cliente. No entanto, a mensagem de estado ainda não foi processada no servidor do site, talvez devido a um acúmulo de mensagens de estado.  

    -   A verificação foi concluída com êxito no computador cliente, mas a mensagem de estado não foi enviada pelo site filho.  

    -   A verificação foi concluída com êxito no computador cliente, mas o arquivo da mensagem de estado foi corrompido de alguma maneira e não pôde ser processado.  

### <a name="scan-for-software-updates-compliance-process"></a>Examinar o processo de conformidade das atualizações de software  
 Quando o ponto de atualização de software é instalado e sincronizado, uma política de computador de todo o site é criada, informando aos computadores cliente de que as atualizações de software do Configuration Manager foram habilitadas para o site. Quando um cliente recebe a política de computador, uma verificação de avaliação de conformidade é agendada para iniciar aleatoriamente nas próximas duas horas. Quando a verificação é iniciada, um processo do Agente Cliente de Atualizações de Software apaga o histórico de verificações, envia uma solicitação para localizar o servidor WSUS que deve ser usado na verificação e atualiza a Política de Grupo local com o local do servidor WSUS.  

> [!NOTE]  
>  Clientes baseados na Internet devem se conectar ao servidor do WSUS usando SSL.  

 Uma solicitação de verificação é passada para o WUA (Windows Update Agent). O WUA, em seguida, conecta-se ao local do servidor do WSU que está listado na política local, recupera os metadados de atualizações de software sincronizados no servidor do WSUS e verifica as atualizações no computador do cliente. Um processo do Agente Cliente de Atualizações de Software detecta que a verificação de conformidade foi concluída e cria mensagens de estado para cada atualização que foi alterada em conformidade com o estado, após a última verificação. As mensagens de estado são enviadas para o ponto de gerenciamento em massa a cada 15 minutos. O ponto de gerenciamento, em seguida, encaminha as mensagens de estado para o servidor do site, onde são inseridas no banco de dados do servidor do site.  

 Após a verificação inicial de conformidade das atualizações de software, a verificação é iniciada na agenda de verificação configurada. No entanto, se o cliente tiver verificado a conformidade das atualizações de software no período de tempo indicado pelo valor TTL (Vida Útil), usará o software de metadados de atualizações que é armazenado localmente. Quando a última verificação estiver fora do TTL, o cliente deverá se conectar ao WSUS em execução no ponto de atualização de software e atualizar os metadados de atualizações de software armazenados no cliente.  

 Incluindo o agendamento da verificação, a verificação de conformidade das atualizações de software pode ter início das seguintes maneiras:  

-   **Agendamento de verificação das atualizações de software**: a verificação de conformidade das atualizações de software começa no agendamento de verificação definido nas configurações do Agente Cliente de Atualizações de Software. Para obter mais informações sobre como definir as configurações do cliente de Atualizações de Software, veja [Configurações do cliente de Atualizações de Software](../../core/clients/deploy/about-client-settings.md#BKMK_SoftwareUpdatesDeviceSetting).  

-   **Ação Propriedades do Configuration Manager**: o usuário pode iniciar a ação **Ciclo de Verificação de Atualizações de Software** ou **Ciclo de Avaliação de Implantação de Atualizações de Software** na guia **Ação** na caixa de diálogo **Propriedades do Configuration Manager** no computador cliente.  

-   **Agendamento de reavaliação da implantação**: a avaliação da implantação e a verificação de conformidade das atualizações de software começam no agendamento de reavaliação da implantação definido nas configurações do Agente Cliente de Atualizações de Software. Para obter mais informações sobre as configurações do cliente de Atualizações de Software, veja [Configurações do cliente de Atualizações de Software](../../core/clients/deploy/about-client-settings.md#BKMK_SoftwareUpdatesDeviceSetting).  

-   **Antes de baixar arquivos de atualização**: quando um computador cliente recebe uma política de atribuição de uma nova implantação necessária, o Agente Cliente de Atualizações de Software baixa os arquivos de atualização no cache local do cliente. Para baixar os arquivos de atualização de software, o agente cliente inicia uma varredura para verificar se a atualização de software ainda é necessária.  

-   **Antes da instalação da atualização de software**: logo antes da instalação da atualização de software, o Agente Cliente de Atualizações de Software inicia uma verificação para confirmar se as atualizações de software ainda são necessárias.  

-   **Após a instalação da atualização de software**: logo após uma instalação de atualização de software ser concluída, o Agente Cliente de Atualizações de Software inicia uma verificação para confirmar se as atualizações não são mais necessárias e cria uma nova mensagem de estado que indica que a atualização de software foi instalada. Quando a instalação é concluída, mas uma reinicialização é necessária, a mensagem de estado indica que uma reinicialização está pendente no computador cliente.  

-   **Após a reinicialização do sistema**: quando uma reinicialização do sistema está pendente no computador cliente para que a instalação da atualização de software seja concluída, o Agente Cliente de Atualizações de Software inicia uma verificação após a reinicialização para confirmar se a atualização de software não é mais necessária e cria uma mensagem de estado que indica que a atualização de software está instalada.  

#### <a name="time-to-live-value"></a>Valor de vida útil  
 Os metadados de atualizações de software necessários na verificação de conformidade das atualizações são armazenados no computador cliente local e, por padrão, são relevantes por até 24 horas. Esse valor é conhecido como TTL (Vida Útil).  

#### <a name="scan-for-software-updates-compliance-types"></a>Examinar os tipos de conformidade das atualizações de software  
 O cliente verifica a conformidade das atualizações de software usando uma verificação online ou offline e uma verificação forçada ou não forçada, dependendo da forma pela qual a conformidade das atualizações de software é iniciada. A seguir há uma descrição dos métodos online ou offline para iniciar a verificação e se ela é forçada ou não forçada.  

-   **Agendamento da verificação das atualizações de software** (verificação online não forçada)  

     No agendamento de verificação configurado, o cliente só se conecta ao WSUS em execução no ponto de atualização de software para recuperar os metadados das atualizações de software quando a última verificação está fora do TTL.  

-   **Ciclo de Verificação de Atualizações de Software** ou **Ciclo de Avaliação de Implantação de Atualizações de Software** (verificação online forçada)  

     O computador cliente sempre se conecta ao WSUS em execução no ponto de atualização de software para recuperar os metadados das atualizações de software antes de o computador cliente verificar a conformidade das atualizações de software. Após a conclusão da verificação, o contador de TTL é redefinido. Por exemplo, se o TTL for 24 horas, depois que um usuário inicia uma verificação de conformidade das atualizações de software o TTL é redefinido para 24 horas.  

-   **Agendamento de reavaliação da implantação** (verificação online não forçada)  

     No agendamento de reavaliação da implantação configurado, o cliente só se conecta ao WSUS em execução no ponto de atualização de software para recuperar os metadados das atualizações de software quando a última verificação está fora do TTL.  

-   **Antes de baixar arquivos de atualização** (verificação online não forçada)  

     Para que o cliente possa baixar os arquivos de atualização em implantações necessárias, ele só se conecta ao WSUS em execução no ponto de atualização de software para recuperar os metadados das atualizações de software quando a última verificação está fora do TTL.  

-   **Antes da instalação da atualização de software** (verificação online não forçada)  

     Para que o cliente instale as atualização de software em implantações necessárias, ele só se conecta ao WSUS em execução no ponto de atualização de software para recuperar os metadados das atualizações de software quando a última verificação está fora do TTL.  

-   **Antes da instalação da atualização de software** (verificação offline forçada)  

     Depois que uma atualização de software é instalada, o Agente Cliente de Atualizações de Software inicia uma verificação usando os metadados locais. O cliente nunca se conecta ao WSUS em execução no ponto de atualização de software para recuperar metadados de atualizações de software.  

-   **Após a reinicialização do sistema** (verificação offline forçada)  

     Depois que uma atualização de software é instalada e o computador é reiniciado, o Agente Cliente de Atualizações de Software inicia uma verificação usando os metadados locais. O cliente nunca se conecta ao WSUS em execução no ponto de atualização de software para recuperar metadados de atualizações de software.  

##  <a name="a-namebkmkdeploymentpackagesa-software-update-deployment-packages"></a><a name="BKMK_DeploymentPackages"></a> Pacotes de implantação de atualização de software  
 Um pacote de implantação de atualização de software é o veículo usado para baixar atualizações de software para uma pasta de rede compartilhada, e copiar os arquivos de origem de atualização na biblioteca de conteúdo em servidores de site e nos pontos de distribuição definidos na implantação. Ao usar o Assistente de Atualizações de Downloads, você pode baixar atualizações de software e adicioná-las aos pacotes de implantação antes de implantá-la. Este assistente permite que você provisione atualizações de software nos pontos de distribuição e verifique se esta parte do processo de implantação foi bem-sucedida antes de implantar as atualizações de software nos clientes.  

 Quando você implanta atualizações de software baixadas usando o Assistente para Implantar Atualizações de Software, a implantação usa automaticamente o pacote de implantação que contém as atualizações de software. Quando atualizações de software que não foram baixadas são implantadas, você deve especificar um pacote de implantação novo ou existente no Assistente para Implantar Atualizações de Software e as atualizações de software são baixadas quando o assistente é concluído.  

> [!IMPORTANT]  
>  Você deve criar a pasta de rede compartilhada manualmente para os arquivos de origem do pacote de implantação antes de especificá-los no assistente. Cada pacote de implantação deve usar uma pasta de compartilhamento de rede diferente.  

> [!IMPORTANT]  
>  A conta de computador do Provedor de SMS e o usuário administrativo que baixa as atualizações de software, ambos requerem permissões de **Gravação** na origem do pacote. Restrinja o acesso à origem do pacote para reduzir o risco de ataques aos arquivos de origem de atualizações de software na origem do pacote.  

 Quando um novo pacote de implantação é criado, a versão do conteúdo é definida como 1 antes que qualquer atualização de software seja baixada. Quando os arquivos de atualização de software forem baixados com o uso do pacote, a versão do conteúdo é incrementada para 2. Portanto, todos os novos pacotes de implantação começam com uma versão de conteúdo de 2. Sempre que o conteúdo é alterado em um pacote de implantação, a versão do conteúdo é incrementada em 1. Para mais informações, consulte [Conceitos fundamentais para o gerenciamento de conteúdo](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

 Os clientes instalam atualizações de software em uma implantação usando qualquer ponto de distribuição que tem as atualizações de software disponíveis, independentemente do pacote de implantação. Mesmo que um pacote de implantação seja excluído para uma implantação ativa, os clientes ainda podem instalar as atualizações de software na implantação, desde que cada atualização seja baixada para pelo menos outro pacote de implantação e esteja disponível em um ponto de distribuição que possa ser acessado pelo cliente. Quando o último pacote de implantação que contém uma atualização de software é excluído, os computadores cliente não podem recuperar a atualização de software até que a atualização seja baixada novamente em um pacote de implantação. As atualizações de software aparecem com uma seta vermelha no console do Configuration Manager quando os arquivos de atualização não estão nos pacotes de implantação. As implantações serão exibidas com uma seta vermelha dupla se contiverem as atualizações nessa condição.  

##  <a name="a-namebkmkdeploymentworkflowsa-software-update-deployment-workflows"></a><a name="BKMK_DeploymentWorkflows"></a> Fluxos de trabalho de implantação de atualização de software  
 Há dois cenários principais para implantar atualizações de software em seu ambiente, a implantação manual e a implantação automática. Em geral, você implanta atualizações de software manualmente para criar uma linha de base para seus computadores cliente; em seguida, você gerencia as atualizações de software nos clientes usando a implantação automática. As seções a seguir fornecem um resumo do fluxo de trabalho de implantação manual e automática das atualizações de software.  

###  <a name="a-namebkmkmanualdeploymenta-manual-deployment-of-software-updates"></a><a name="BKMK_ManualDeployment"></a> Implantação manual de atualizações de software  
 Uma implantação manual de atualizações de software é o processo de selecionar atualizações de software no console do Configuration Manager e iniciar manualmente o processo de implantação. Esse método de implantação é usado geralmente para ter os computadores cliente em dia com as atualizações de software necessárias antes de serem criadas regras de implantação automáticas que gerenciam as implantações de atualização de software mensalmente e continuamente e para implantar requisitos de atualização de software fora da banda. A lista seguinte fornece o fluxo de trabalho geral para implantação manual das atualizações de software:  

1.  Filtro para atualizações de software que usam requisitos específicos. Por exemplo, você pode fornecer critérios que recuperam toda a segurança ou atualizações críticas de software que são necessárias em mais de 50 computadores cliente.  

2.  Crie um grupo de atualização de software que contém as atualizações de software.  

3.  Baixe o conteúdo das atualizações de software no grupo de atualização de software.  

4.  Implante manualmente o grupo de atualização de software.  

###  <a name="a-namebkmkautomaticdeploymenta-automatic-deployment-of-software-updates"></a><a name="BKMK_AutomaticDeployment"></a> Implantação automática de atualizações de software  
 A implantação automática de atualizações de software é configurada usando uma ADR (regra de implantação automática). Esse método de implantação geralmente é usado para suas atualizações de software mensais (geralmente conhecidas como "Patch Tuesday") e para o gerenciamento de atualizações de definição. Quando a regra é executada, as atualizações são removidas do grupo de atualização de software (se estiver usar um arquivo de grupo) de software, as atualizações de software que atendem aos critérios especificados (por exemplo, todas as atualizações de software de segurança lançados na última semana) são adicionadas a um grupo de atualização de software, os arquivos de conteúdo das atualizações de software são baixados e copiados nos pontos de distribuição e as atualizações de software são implantadas em computadores clientes na coleção de destino. A lista seguinte fornece o fluxo de trabalho geral para implantação automática das atualizações de software:  

1.  Crie uma ADR que especifica as configurações de implantação, como as seguintes:  

    -   Coleção de destino  

    -   Decida se deseja habilitar a implantação ou relatório em conformidade de atualizações de software para os computadores cliente na coleção de destino  

    -   Critérios de atualizações de software  

    -   Agendamento de avaliação e implantação  

    -   Experiência do usuário  

    -   Propriedades do download  

2.  As atualizações de software são adicionadas a um grupo de atualização de software.  

3.  O grupo de atualização de software é implantado nos computadores cliente na coleção de destino, se especificada.  

 Você deve determinar qual estratégia de implantação usar no seu ambiente. Por exemplo, é possível criar a ADR e ter com alvo uma coleção de clientes de teste. Depois de verificar se as atualizações de software estão instaladas no grupo de teste, é possível adicionar uma nova implantação à regra ou alterar a coleção na implantação existente para uma coleção de destino que inclua um conjunto maior de clientes. Os objetos de atualização de software que são criados pelas ADRs são interativos.  

-   As atualizações de software implantadas usando uma ADR são automaticamente implantadas nos novos clientes adicionados à coleção de destino.  

-   Novas atualizações de software adicionadas a um grupo de atualização de software são automaticamente implantadas em clientes na coleção de destino.  

-   É possível habilitar ou desabilitar as implantações a qualquer momento para a ADR.  

 Depois de criar uma ADR, é possível adicionar outras implantações à regra. Isso pode ajudá-lo a gerenciar a complexidade de implantar diferentes atualizações em diferentes coleções. Cada nova implantação tem a gama completa da funcionalidade e da experiência de monitoramento da implantação, e cada nova implantação que você adicionar:  

-   Usa o mesmo grupo e pacote de atualização que é criado quando o ADR é executado pela primeira vez  

-   Pode especificar uma coleção diferente  

-   Dá suporte a propriedades de implantação exclusivas, incluindo:  

    -   Tempo de ativação  

    -   Prazo  

    -   Mostrar ou ocultar a experiência do usuário final  

    -   Alertas separados para esta implantação  

##  <a name="a-namebkmkdeploymentprocessa-software-update-deployment-process"></a><a name="BKMK_DeploymentProcess"></a> Processo de implantação de atualização de software  
 Depois de implantar as atualizações de software ou quando uma regra de implementação automática executa e implanta atualizações de software, uma política de atribuição de implantação é adicionada à política do computador para o site. As atualizações de software são baixadas por meio do local de download, a Internet, ou de uma pasta de rede compartilhada, na origem do pacote. As atualizações de software são copiadas da origem do pacote para a biblioteca de conteúdo no servidor do site, e depois copiadas na biblioteca de conteúdo no ponto de distribuição.  

 Quando um computador cliente na coleção de destino da implantação recebe a política do computador, o Agente Cliente de Atualizações de Software começa uma verificação de avaliação. O agente cliente baixa o conteúdo das atualizações de software necessárias de um ponto de distribuição para o cache do cliente local logo depois de receber a implantação, mas aguarda a configuração do **Tempo disponível do software** da implantação para que as atualizações de software estejam disponíveis para serem instaladas. As atualizações de software em implantações opcionais (implantações que não têm um prazo de instalação) não são baixadas até que um usuário inicie manualmente a instalação.  

 Quando o prazo configurado passa, o Agente Cliente de Atualizações de Software realiza uma varredura para verificar se as atualizações de software ainda são necessárias. Em seguida, ele verifica o cache local no computador cliente para ver se os arquivos de origem da atualização ainda estão disponíveis. Por fim, o cliente instala as atualizações de software. Se o conteúdo tiver sido excluído do cache do cliente para liberar espaço para outra implantação, o cliente baixará as atualizações de software do ponto de distribuição no cache. As atualizações de software são sempre baixadas no cache do cliente independentemente do tamanho máximo do cache do cliente configurado. Quando a instalação é concluída, o agente cliente verifica se as atualizações de software não são mais necessárias e, em seguida, envia uma mensagem de estado para o ponto de gerenciamento para indicar que as atualizações estão instaladas no cliente.  

### <a name="required-system-restart"></a>Reinicialização necessária do sistema  
 Por padrão, quando as atualizações de software de uma implantação necessária são instaladas em um computador cliente e é necessário reiniciar o sistema para a instalação concluir, o sistema é reiniciado. Para atualizações de software instalados antes do prazo, a reinicialização automática do sistema é adiada até prazo, a menos que o computador seja reiniciado antes disso, por algum outro motivo. A reinicialização do sistema pode ser suprimida para servidores e estações de trabalho. Estas definições são configuradas na página **Experiência do Usuário** do assistente para Implantar Atualizações de Software ou Criar Assistente de Regra de Implantação Automática.  

### <a name="deployment-reevaluation-cycle"></a>Ciclo de reavaliação de implantação  
 Por padrão, os computadores cliente iniciam um ciclo de reavaliação de implantação a cada 7 dias. Durante esse ciclo de avaliação, o computador cliente verifica atualizações de software que foram implantadas e instaladas anteriormente. Se faltarem atualizações de software, elas serão reinstaladas por meio do cache local. Se uma atualização de software não estiver mais disponível no cache local, será baixada de um ponto de distribuição e depois instalada. Você pode configurar o agendamento da reavaliação na página **Atualizações de Software** nas configurações do cliente para o site.  

##  <a name="a-namebkmkembeddeddevicesa-support-for-windows-embedded-devices-that-use-write-filters"></a><a name="BKMK_EmbeddedDevices"></a> Suporte para dispositivos Windows Embedded que usam filtros de gravação  
 Quando você implanta atualizações de software em dispositivos Windows Embedded habilitados com filtro de gravação, pode especificar se quer desabilitar o filtro de gravação no dispositivo durante a implantação e reiniciá-lo após a implantação. Se o filtro de gravação não for desabilitado, o software será implantado em uma sobreposição temporária e não será mais instalado quando o dispositivo for reiniciado, a menos que outras alterações de forças de implantação sejam persistidas.  

> [!NOTE]  
>  Ao implantar uma atualização de software em um dispositivo Windows Embedded, verifique se o dispositivo é membro de uma coleção com uma janela de manutenção configurada. Isso permite que você gerencie se o filtro de gravação é desabilitado e habilitado na reinicialização do dispositivo.  

 A configuração de experiência do usuário que controla o comportamento do filtro de gravação é uma caixa de seleção denominada **Confirmar as alterações no prazo ou durante uma janela de manutenção (requer reinicializações)**.  

 Para obter mais informações sobre como o Configuration Manager gerencia dispositivos inseridos que usam filtros de gravação, veja [Planejamento para implantação do cliente em dispositivos Windows Embedded](../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

##  <a name="a-namebkmkextendsoftwareupdatesa-extend-software-updates-in-configuration-manager"></a><a name="BKMK_ExtendSoftwareUpdates"></a> Estender as atualizações de software no Configuration Manager  
 Use System Center Updates Publisher para gerenciar atualizações de software que não estão disponíveis no Microsoft Update. Depois de publicar as atualizações de software no servidor de atualização e sincronizá-las no Configuration Manager, você pode implantar as atualizações de software nos clientes do Configuration Manager. Para obter mais informações sobre o Updates Publisher, consulte [Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=252947).  

## <a name="next-steps"></a>Próximas etapas
[Planejar atualizações de software](../plan-design/plan-for-software-updates.md)



<!--HONumber=Nov16_HO1-->


