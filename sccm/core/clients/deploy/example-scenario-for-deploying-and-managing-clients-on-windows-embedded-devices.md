---
title: "Cenário de exemplo – implantar clientes Windows Embedded | Microsoft Docs"
description: "Veja um cenário de exemplo para implantar e gerenciar clientes do System Center Configuration Manager em dispositivos Windows Embedded."
ms.custom: na
ms.date: 01/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 10049c89-b37c-472b-b317-ce4f56cd4be7
caps.latest.revision: 8
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: a650ad8e7b1f9468dd04165a3e43a89387b5d696
ms.openlocfilehash: b07af49e2fecf6cc41258c87794ca7952206bb8a
ms.lasthandoff: 01/17/2017


---
# <a name="example-scenario-for-deploying-and-managing-system-center-configuration-manager-clients-on-windows-embedded-devices"></a>Cenário de exemplo para implantação e gerenciamento de clientes do System Center Configuration Manager em dispositivos Windows Embedded

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este cenário demonstra como é possível gerenciar dispositivos Windows Embedded com filtro de gravação habilitado com o Configuration Manager. Se os dispositivos incorporados não derem suporte a filtros de gravação, eles se comportarão como clientes do Configuration Manager padrão e esses procedimentos não serão aplicáveis.  

A Coho Vineyard & Winery está abrindo um centro de visitantes e precisa de quiosques que executam o Windows Embedded para fazer apresentações interativas. A construção do novo centro do visitante não fica tão perto do departamento de TI, então os quiosques devem ser gerenciados remotamente. Além do software que executa as apresentações, esses dispositivos devem executar o software atualizado de proteção antimalware para cumprir as políticas de segurança da empresa. Os quiosques devem ser executados 7 dias por semana, sem tempo de inatividade enquanto o centro do visitante estiver aberto.  

 A Coho já executa o Configuration Manager para gerenciar dispositivos em sua rede. O Configuration Manager está configurado para executar o Endpoint Protection e instalar atualizações de software e aplicativos. No entanto, como a equipe de TI não havia gerenciado dispositivos Windows Embedded antes, Jane, administradora do Configuration Manager, executa um piloto para gerenciar dois quiosques no lobby de recepção.   

 Para gerenciar esses dispositivos Windows Embedded com filtro de gravação habilitado, Jane executa as seguintes etapas para instalar o cliente do Configuration Manager, proteger o cliente usando o Endpoint Protection e instalar o software de apresentação interativa.  

1.  Jane lê de que forma os dispositivos Windows Embedded usam filtros de gravação e como o Configuration Manager pode facilitar essa tarefa, desabilitando e depois habilitando novamente os filtros de gravação automaticamente, para manter a instalação de um software.  

     Para mais informações, consulte [Planejando a implantação de cliente em dispositivos do Windows Embedded no System Center Configuration Manager](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

2.  Antes de instalar o cliente do Configuration Manager, Jane cria uma nova coleção de dispositivos baseada em consulta para os dispositivos Windows Embedded. Como a empresa usa os formatos de nomenclatura padrão para identificar seus computadores, Jane pode identificar exclusivamente os dispositivos Windows Embedded pelas seis primeiras letras do nome do computador: **WEMDVC**. Ela usa a seguinte consulta WQL para criar essa coleção: **select SMS_R_System.NetbiosName from SMS_R_System where SMS_R_System.NetbiosName like "WEMDVC%"**  

     Essa coleção permite a ela gerenciar os dispositivos Windows Embedded com opções de configuração diferentes dos outros dispositivos. Ela usará essa coleção para controlar reinicializações, implantar o Endpoint Protection com configurações do cliente e implantar o aplicativo de apresentação interativa.  

     Consulte [Como criar coleções no System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

3.  Jane configura a coleção para uma janela de manutenção para garantir que reinicializações que talvez sejam necessárias para instalar o aplicativo de apresentação e quaisquer atualizações não ocorram durante o horário de funcionamento do centro do visitante. O horário de funcionamento será das 9:00 às 18:00, de segunda a domingo. Ela configura a janela de manutenção para todos os dias, das 18:30 às 6:00.  

4.  Para obter mais informações, consulte [Como usar as janelas de manutenção no System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

5.  Jane, então, define uma configuração personalizada do cliente do dispositivo para instalar o cliente do Endpoint Protection, selecionando **Sim** nas etapas seguintes e, depois, implanta essa configuração personalizada na coleção de dispositivos Windows Embedded:  

    -   **Instalar o cliente do Endpoint Protection em computadores cliente**  

    -   **Para dispositivos Windows Embedded com filtros de gravação, confirme a instalação de cliente do Endpoint Protection (requer reinicialização)**  

    -   **Permitir a instalação do cliente do Endpoint Protection e reiniciar para que seja executada fora das janelas de manutenção**  

     Quando o cliente do Configuration Manager for instalado, essas configurações instalarão o cliente do Endpoint Protection e verificar se ele se mantém no sistema operacional como parte da instalação, em vez de somente gravados na sobreposição. As políticas de segurança da empresa requerem que o software antimalware sempre seja instalado, e Jane não deseja correr o risco de deixar os quiosques desprotegidos nem por um curto período se eles forem reinicializados.  

    > [!NOTE]  
    >  As reinicializações necessárias para instalar o cliente do Endpoint Protection são uma ocorrência única, que acontece durante o período de configuração dos dispositivos e antes do funcionamento do centro do visitante. Ao contrário da implantação periódica de aplicativos ou atualizações de definição de software, a próxima vez que o cliente do Endpoint Protection for instalado no mesmo dispositivo provavelmente será quando a empresa atualizar para a próxima versão do Configuration Manager.  

     Para obter mais informações, consulte [Configuring Endpoint Protection in System Center Configuration Manager (Configurando o Endpoint Protection no System Center Configuration Manager)](../../../protect/deploy-use/configure-endpoint-protection.md).  

6.  Com as configurações para o cliente já em vigor, Jane prepara-se para instalar os clientes do Configuration Manager. Antes de instalar os clientes, ela deve desativar manualmente o filtro de gravação nos dispositivos Windows Embedded. Ela lê a documentação do OEM que acompanha os quiosques e segue as instruções para desativar os filtros de gravação.  

     Jane renomeia o dispositivo para que ele use o formato de nomenclatura padrão da empresa e instala o cliente manualmente executando o CCMSetup com o seguinte comando de uma unidade mapeada que contém os arquivos de origem do cliente: **CCMSetup.exe /MP:mpserver.cohovineyardandwinery.com SMSSITECODE=CO1**  

     Esse comando instala o cliente, atribui o cliente ao ponto de gerenciamento que tem o FQDN da intranet do **mpserver.cohovineyardandwinery.com**e atribui o cliente ao site principal chamado **CO1**.  

     Jane sabe que sempre leva um tempo para que os clientes instalem e enviem o status de volta ao site. Então, ela aguarda antes de confirma que os clientes foram instalados com êxito, atribuídos ao site e mostrados como clientes na coleção que ela criou para dispositivos Windows Embedded.  

     Como confirmação adicional, ela verifica as propriedades do Configuration Manager no Painel de Controle nos dispositivos e compara-as com computadores Windows padrão gerenciados pelo site. Por exemplo, na guia **Componentes** , o **Agente de inventário de hardware** exibe **Habilitado**, e na guia **Ações** , há 11 ações disponíveis, que incluem **Ciclo de avaliação de implantação de aplicativo** e **Ciclo de coleta de dados de descoberta**.  

     Confiante de que os clientes foram instalados com êxito, atribuídos e que recebem a política do cliente do ponto de gerenciamento, Jane habilita manualmente os filtros de gravação seguindo as instruções do OEM.  

     Para obter mais informações, consulte:  

    -   [Como implantar clientes em computadores Windows no System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

    -   [Como atribuir clientes a um site no System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md)  

7.  Agora que o cliente do Configuration Manager foi instalado nos dispositivos Windows Embedded, Jane confirma que ela pode gerenciá-los da mesma forma que gerencia os clientes Windows padrão. Por exemplo, no console do Configuration Manager, ela pode gerenciá-los remotamente usando controle remoto, iniciar a política do cliente para eles e ver as propriedades do cliente e o inventário de hardware.  

     Como esses dispositivos estão ligados a um domínio do Active Directory, ela não precisa aprová-los manualmente como clientes confiáveis e confirma por meio do console do Configuration Manager que eles foram aprovados.  

     Para obter mais informações, consulte [How to manage clients in System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

8.  Para instalar o software de apresentação interativa, Jane executa o **Assistente de implantação de software** e configura o aplicativo necessário. Na página **Experiência do usuário** do assistente, na seção **Manuseio de filtro de gravação para dispositivos Windows Embedded** , ela aceita a opção padrão que seleciona **Confirmar as alterações no prazo ou durante uma janela de manutenção (requer reinicializações)**.  

     Jane mantém a opção padrão para os filtros de gravação a fim de garantir que o aplicativo permaneça depois de uma reinicialização, assim ele estará sempre disponível aos visitantes que usam os quiosques. A janela de manutenção diária fornece um período de segurança durante o qual as reinicializações para instalação e quaisquer atualizações podem ocorrer.  

     Jane implanta o aplicativo na coleção de dispositivos Windows Embedded.  

     Para obter mais informações, consulte [Como implantar aplicativos com o System Center Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

9. Para configurar atualizações de definição para o Endpoint Protection, Jane use atualizações de software e executa o Assistente para criar regra de implantação automática. Ela seleciona o modelo **Atualizações de definição** para pré-preencher o assistente com as configurações adequadas para o Endpoint Protection.  

     Essas configurações incluem o seguinte na página **Experiência do usuário** do assistente:  

    -   **Comportamento do prazo**: a caixa de seleção **Instalação de Software** não está selecionada.  

    -   **Tratamento de filtro de gravação para dispositivos Windows Embedded**: a caixa de seleção **Confirmar alterações no prazo ou durante uma janela de manutenção (requer reinicializações)** não está selecionada.  

     Jane mantém essas configurações padrão. Juntas, essas duas opções com essa configuração permitem quaisquer definições de software para que o Endpoint Protection seja instalado na sobreposição durante o dia e não aguarde para ser instalado e confirmado durante a janela de manutenção. Essa configuração é a que melhor atende à política de segurança da empresa para que computadores executem a proteção antimalware atualizada.  

    > [!NOTE]  
    >  Ao contrário das instalações de software para aplicativos, as definições de atualização de software para o Endpoint Protection podem ocorrer com muita frequência, até mesmo várias vezes no dia. Elas geralmente são arquivos pequenos. Para esses tipos de implantações relacionadas à segurança, geralmente pode ser útil sempre instalar na sobreposição em vez de aguardar até a janela de manutenção. O cliente do Configuration Manager reinstalará rapidamente as atualizações de definição de software se o dispositivo for reiniciado, pois essa ação inicia uma verificação de avaliação e não espera até a próxima avaliação agendada.  

     Jane seleciona a coleção de dispositivos Windows Embedded para a regra de implantação automática.  

     Para obter mais informações, consulte  
                  Etapa 3: configurar atualizações de software do Configuration Manager para fornecer atualizações de definição a computadores cliente em [Configurando o Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/configure-endpoint-protection.md)  

10. Jane decide configurar uma tarefa de manutenção que periodicamente confirma todas as alterações na sobreposição. Essa tarefa é para dar suporte à implantação de definições de atualização de software a fim de reduzir o número de atualizações que ficam acumuladas e devem ser instaladas novamente sempre que o dispositivo é reinicializado. Em sua experiência, isso ajuda os programas antimalware a serem executados com mais eficiência.  

    > [!NOTE]  
    >  Essas definições de atualização de software seriam vinculadas automaticamente à imagem se os dispositivos inseridos tiverem executado outra tarefa de gerenciamento que deu suporte à confirmação das alterações. Por exemplo, a instalação de uma nova versão do software de apresentação interativa também confirmaria as alterações das definições de atualização de software. Ou, a instalação de atualizações de software padrão todo mês em que a instalação durante a janela de manutenção também poderia confirma as alterações das definições de atualização de software. No entanto, neste cenário, em que as atualizações de software padrão não são executadas e é pouco provável que o software de apresentação interativa seja atualizado com frequência, isso pode ocorrer meses antes de as atualizações de definição de software serem vinculadas automaticamente à imagem.  

     Jane primeiro cria uma sequência de tarefas personalizada que não possui configurações a não ser o nome. Ela executa o Assistente para criação de sequência de tarefas:  

    1.  Na página **Criar uma nova sequência de tarefas** , ela seleciona **Criar uma nova sequência de tarefas personalizada**e clica em **Próximo**.  

    2.  Na página **Informações de Sequência de Tarefas** , ela digita **Maintenance task to commit changes on embedded devices** para o nome da sequência de tarefas e clica em **Avançar**.  

    3.  Na página **Resumo** , ela seleciona **Próximo**e conclui o assistente.  

     Em seguida, implanta essa sequência de tarefas personalizada na coleção de dispositivos Windows Embedded e configura a agenda para executar todos os meses. Como parte das configurações de implantação, ela marca a caixa de seleção **Confirmar as alterações no prazo ou durante uma janela de manutenção (requer reinicializações)** para manter as alterações depois de uma reinicialização. Para configurar essa implantação, ela seleciona a sequência de tarefas personalizada recém-criada e, na guia **Início** , no grupo **Implantação** , clica em **Implantar** para iniciar o Assistente de implantação de software:  

    1.  Na página **Geral** , ela seleciona a coleção de dispositivos Windows Embedded e clica em **Próximo**.  

    2.  Na página **Configurações de implantação** , ela seleciona a **Finalidade** de **Obrigatório**e clica em **Próximo**.  

    3.  Na página **Agendamento** , ela clica em **Novo** para especificar uma agenda semanal durante a janela de manutenção e clica em **Próximo**.  

    4.  Ele conclui o assistente sem outras alterações.  

     Para obter mais informações, consulte  
                  [Gerenciar sequências de tarefas para automatizar tarefas no System Center Configuration Manager](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md).  

11. Para que os quiosques funcionem automaticamente, Janaina grava um script para definir as seguintes configurações dos dispositivos:  

    -   Efetuar logon automaticamente, usando uma conta de convidado que não tenha senha.  

    -   Executar automaticamente na inicialização a apresentação interativa do software.  

     Janaina usa pacotes e programas para implantar esse script à coleção de dispositivos do Windows Embedded. Ao executar o Assistente de Implantação de Software, ela novamente seleciona a caixa de seleção **Confirmar as alterações no prazo ou durante uma janela de manutenção (requer reinicializações)** para manter as alterações depois de uma reinicialização.  

     Para obter mais informações, consulte [Pacotes e programas no System Center Configuration Manager](../../../apps/deploy-use/packages-and-programs.md).  

12. Na manhã seguinte, Janaina verifica os dispositivos do Windows Embedded. Ela confirma o seguinte:  

    -   O quiosque está conectado automaticamente usando a conta de convidado.  

    -   O software de apresentação interativa está sendo executado.  

    -   O cliente do Endpoint Protection está instalado e possui as definições de atualização de software mais recentes.  

    -   Esse dispositivo foi reiniciado durante a janela de manutenção.  

     Para obter mais informações, consulte:  

    -   [Como monitorar o Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/monitor-endpoint-protection.md)  

    -   [Monitorar aplicativos com o System Center Configuration Manager](/sccm/apps/deploy-use/monitor-applications-from-the-console)  

13. Janaina monitora os quiosques e relata o gerenciamento bem-sucedido deles a seu gerente. Como resultado, 20 quiosques são requisitados para o centro de visitantes.  

     Para evitar a instalação manual do cliente do Configuration Manager, que requer a desabilitação e habilitação manual dos filtros de gravação, Jane verifica se a ordem inclui uma imagem personalizada que já inclui a instalação e atribuição de site do cliente do Configuration Manager. Além disso, os dispositivos são nomeados de acordo com o formato de nome da empresa.  

     Os quiosques são entregues ao centro de visitantes uma semana antes de sua abertura. Durante esse tempo, os quiosques são conectados à rede, todo o gerenciamento de dispositivos deles é automático e não é necessário administrador local. Janaina confirma que os quiosques estão funcionando conforme exigido:  

    -   Os clientes nos quiosques concluem o gerenciamento do site e baixam a chave de raiz confiável dos Serviços de Domínio Active Directory.  

    -   Os clientes nos quiosques são adicionados automaticamente à coleção de dispositivos do Windows Embedded e configurados com a janela de manutenção.  

    -   O cliente do Endpoint Protection está instalado e possui as definições de atualização de software mais recentes para proteção antimalware.  

    -   O software de apresentação interativa está instalado e sendo executado automaticamente, pronto para os visitantes.  

14. Após a configuração inicial, toda reinicialização exigida pelas atualizações ocorre somente quando o centro de visitantes está fechado.  

