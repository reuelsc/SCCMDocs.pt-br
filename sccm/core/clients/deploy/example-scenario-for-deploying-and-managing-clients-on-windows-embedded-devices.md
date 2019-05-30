---
title: Cenário de exemplo – implantar clientes Windows Embedded
titleSuffix: Configuration Manager
description: Veja um cenário de exemplo para implantar e gerenciar clientes do System Center Configuration Manager em dispositivos Windows Embedded.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 10049c89-b37c-472b-b317-ce4f56cd4be7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7f0cc9800931c802d29edd5cacc1f1ed5e95c24e
ms.sourcegitcommit: f531d0a622f220739710b2fe6644ea58d024064a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65933273"
---
# <a name="example-scenario-for-deploying-and-managing-system-center-configuration-manager-clients-on-windows-embedded-devices"></a>Cenário de exemplo para implantação e gerenciamento de clientes do System Center Configuration Manager em dispositivos Windows Embedded

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este cenário demonstra como é possível gerenciar dispositivos Windows Embedded com filtro de gravação habilitado com o Configuration Manager. Se os dispositivos incorporados não derem suporte a filtros de gravação, eles se comportarão como clientes do Configuration Manager padrão e esses procedimentos não serão aplicáveis.  

A Coho Vineyard & Winery está abrindo um centro de visitantes e precisa de quiosques que executam o Windows Embedded para fazer apresentações interativas. A construção do novo centro do visitante não fica tão perto do departamento de TI, então os quiosques devem ser gerenciados remotamente. Além do software que executa as apresentações, esses dispositivos devem executar o software atualizado de proteção antimalware para cumprir as políticas de segurança da empresa. Os quiosques devem ser executados 7 dias por semana, sem tempo de inatividade enquanto o centro do visitante estiver aberto.  

 A Coho já executa o Configuration Manager para gerenciar dispositivos em sua rede. O Configuration Manager está configurado para executar o Endpoint Protection e instalar atualizações de software e aplicativos. No entanto, como a equipe de TI não havia gerenciado dispositivos Windows Embedded antes, o administrador do Configuration Manager executa um piloto para gerenciar dois quiosques no lobby de recepção.   

 Para gerenciar esses dispositivos Windows Embedded habilitados para filtro de gravação, o administrador do Configuration Manager executa as etapas a seguir para instalar o cliente do Configuration Manager, proteger o cliente usando o Endpoint Protection e instalar o software de apresentação interativa.  

1. O administrador do Configuration Manager (o Administrador) lê como os dispositivos Windows Embedded usam filtros de gravação e como o Configuration Manager pode facilitar essa tarefa, desabilitando e, em seguida, habilitando novamente os filtros de gravação de forma automática, a fim de persistir a instalação de um software.  

    Para mais informações, consulte [Planejando a implantação de cliente em dispositivos do Windows Embedded no System Center Configuration Manager](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

2. Antes de instalar o cliente do Configuration Manager, o administrador cria uma coleção de dispositivos baseada em consulta para os dispositivos Windows Embedded. Como a empresa usa os formatos de nomenclatura padrão para identificar seus computadores, o administrador pode identificar exclusivamente os dispositivos Windows Embedded pelas seis primeiras letras do nome do computador: **WEMDVC**. O administrador usa a seguinte consulta WQL para criar essa coleção: **select SMS_R_System.NetbiosName from SMS_R_System where SMS_R_System.NetbiosName like "WEMDVC%"**  

    Essa coleção permite que o administrador gerencie os dispositivos Windows Embedded com opções de configuração diferentes dos outros dispositivos. O administrador usará essa coleção para controlar reinicializações, implantar o Endpoint Protection com as configurações do cliente e implantar o aplicativo de apresentação interativa.  

    Consulte [Como criar coleções no System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

3. O administrador configura a coleção para uma janela de manutenção, a fim de garantir que as reinicializações que possam ser necessárias para instalar o aplicativo de apresentação e as atualizações não ocorram durante o horário de funcionamento do centro do visitante. O horário de funcionamento será das 9:00 às 18:00, de segunda a domingo. O administrador configura a janela de manutenção para todos os dias, das 18h30 às 6h00.  

4. Para obter mais informações, consulte [Como usar as janelas de manutenção no System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

5. Em seguida, o administrador define uma configuração personalizada do cliente do dispositivo para instalar o cliente do Endpoint Protection selecionando **Sim** nas seguintes configurações e, depois, implanta essa configuração de cliente personalizada na coleção de dispositivos Windows Embedded:  

   - **Instalar o cliente do Endpoint Protection em computadores cliente**  

   - **Para dispositivos Windows Embedded com filtros de gravação, confirme a instalação de cliente do Endpoint Protection (requer reinicialização)**  

   - **Permitir a instalação do cliente do Endpoint Protection e reiniciar para que seja executada fora das janelas de manutenção**  

     Quando o cliente do Configuration Manager for instalado, essas configurações instalarão o cliente do Endpoint Protection e verificar se ele se mantém no sistema operacional como parte da instalação, em vez de somente gravados na sobreposição. As políticas de segurança da empresa exigem que o software antimalware seja sempre instalado e o administrador não quer correr o risco de deixar os quiosques desprotegidos nem por um curto período se eles forem reinicializados.  

   > [!NOTE]  
   >  As reinicializações necessárias para instalar o cliente do Endpoint Protection são uma ocorrência única, que acontece durante o período de configuração dos dispositivos e antes do funcionamento do centro do visitante. Ao contrário da implantação periódica de aplicativos ou atualizações de definição de software, a próxima vez que o cliente do Endpoint Protection for instalado no mesmo dispositivo provavelmente será quando a empresa atualizar para a próxima versão do Configuration Manager.  

    Para obter mais informações, consulte [Configuring Endpoint Protection in System Center Configuration Manager (Configurando o Endpoint Protection no System Center Configuration Manager)](../../../protect/deploy-use/configure-endpoint-protection.md).  

6. Com as definições de configuração para o cliente já em vigor, o administrador prepara-se para instalar os clientes do Configuration Manager. Antes de instalar os clientes, o administrador precisa desabilitar manualmente o filtro de gravação nos dispositivos Windows Embedded. O administrador lê a documentação do OEM que acompanha os quiosques e segue as instruções para desabilitar os filtros de gravação.  

    O administrador renomeia o dispositivo de modo a usar o formato de nomenclatura padrão da empresa e, em seguida, instala o cliente manualmente executando o CCMSetup com o seguinte comando de uma unidade mapeada que contém os arquivos de origem do cliente: **CCMSetup.exe /MP:mpserver.cohovineyardandwinery.com SMSSITECODE=CO1**  

    Esse comando instala o cliente, atribui o cliente ao ponto de gerenciamento que tem o FQDN da intranet do **mpserver.cohovineyardandwinery.com**e atribui o cliente ao site principal chamado **CO1**.  

    O administrador sabe que sempre leva um tempo para que os clientes instalem e enviem o status novamente ao site. Portanto, o administrador aguarda antes de confirmar que os clientes foram instalados com êxito, atribuídos ao site e são exibidos como clientes na coleção criada para os dispositivos Windows Embedded.  

    Como confirmação adicional, o administrador verifica as propriedades do Configuration Manager no Painel de Controle nos dispositivos e compara-as com os computadores Windows padrão gerenciados pelo site. Por exemplo, na guia **Componentes** , o **Agente de inventário de hardware** exibe **Habilitado**, e na guia **Ações** , há 11 ações disponíveis, que incluem **Ciclo de avaliação de implantação de aplicativo** e **Ciclo de coleta de dados de descoberta**.  

    Confiante de que os clientes foram instalados com êxito, atribuídos e receberam a política do cliente do ponto de gerenciamento, em seguida, o administrador habilita manualmente os filtros de gravação seguindo as instruções do OEM.  

    Para obter mais informações, consulte:  

   -   [Como implantar clientes em computadores Windows no System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

   -   [Como atribuir clientes a um site no System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md)  

7. Agora que o cliente do Configuration Manager foi instalado nos dispositivos Windows Embedded, o administrador confirma se pode gerenciá-los da mesma forma que gerencia os clientes do Windows padrão. Por exemplo, no console do Configuration Manager, o administrador pode gerenciá-los remotamente usando o controle remoto, iniciar a política do cliente para eles e exibir as propriedades do cliente e o inventário de hardware.  

    Como esses dispositivos estão ingressados em um domínio do Active Directory, o administrador não precisa aprová-los manualmente como clientes confiáveis e confirma por meio do console do Configuration Manager que eles foram aprovados.  

    Para obter mais informações, consulte [Como gerenciar clientes no System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

8. Para instalar o software de apresentação interativa, o administrador executa o **Assistente de Implantação de Software** e configura um aplicativo necessário. Na página **Experiência do Usuário** do assistente, na seção **Manipulação do filtro de gravação para dispositivos Windows Embedded**, eles aceitam a opção padrão que seleciona **Confirmar as alterações na data limite ou durante uma janela de manutenção (exige reinicializações)** .  

    O administrador mantém essa opção padrão para os filtros de gravação a fim de garantir que o aplicativo seja persistido após uma reinicialização, de modo que ele fique sempre disponível aos visitantes que usam os quiosques. A janela de manutenção diária fornece um período de segurança durante o qual as reinicializações para instalação e quaisquer atualizações podem ocorrer.  

    O administrador implanta o aplicativo na coleção de dispositivos Windows Embedded.  

    Para obter mais informações, consulte [Como implantar aplicativos com o System Center Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

9. Para configurar atualizações de definição para o Endpoint Protection, o administrador usa atualizações de software e executa o Assistente para Criar Regra de Implantação Automática. Ela seleciona o modelo **Atualizações de Definição** para pré-popular o assistente com as configurações adequadas para o Endpoint Protection.  

     Essas configurações incluem o seguinte na página **Experiência do usuário** do assistente:  

   - **Comportamento da data limite**: A caixa de seleção **Instalação do Software** não está selecionada.  

   - **Manipulação de filtro de gravação para dispositivos Windows Embedded**: A caixa de seleção **Confirmar as alterações no prazo ou durante uma janela de manutenção (requer reinicializações)** não está selecionada.  

     O administrador mantém essas configurações padrão. Juntas, essas duas opções com essa configuração permitem quaisquer definições de software para que o Endpoint Protection seja instalado na sobreposição durante o dia e não aguarde para ser instalado e confirmado durante a janela de manutenção. Essa configuração é a que melhor atende à política de segurança da empresa para que computadores executem a proteção antimalware atualizada.  

     > [!NOTE]  
     >  Ao contrário das instalações de software para aplicativos, as definições de atualização de software para o Endpoint Protection podem ocorrer com muita frequência, até mesmo várias vezes no dia. Elas geralmente são arquivos pequenos. Para esses tipos de implantações relacionadas à segurança, geralmente pode ser útil sempre instalar na sobreposição em vez de aguardar até a janela de manutenção. O cliente do Configuration Manager reinstalará rapidamente as atualizações de definição de software se o dispositivo for reiniciado, pois essa ação inicia uma verificação de avaliação e não espera até a próxima avaliação agendada.  

     O administrador seleciona a coleção de dispositivos Windows Embedded para a regra de implantação automática.  

     Para obter mais informações, consulte  
               Etapa 3: Configurar atualizações de software do Configuration Manager para fornecer atualizações de definição a computadores cliente em [Configurando o Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/configure-endpoint-protection.md)  

10. O administrador decide configurar uma tarefa de manutenção que confirma periodicamente todas as alterações na sobreposição. Essa tarefa é para dar suporte à implantação de definições de atualização de software a fim de reduzir o número de atualizações que ficam acumuladas e devem ser instaladas novamente sempre que o dispositivo é reinicializado. Na experiência do administrador, isso ajuda os programas antimalware a serem executados com mais eficiência.  

    > [!NOTE]  
    >  Essas definições de atualização de software seriam vinculadas automaticamente à imagem se os dispositivos inseridos tiverem executado outra tarefa de gerenciamento que deu suporte à confirmação das alterações. Por exemplo, a instalação de uma nova versão do software de apresentação interativa também confirmaria as alterações das definições de atualização de software. Ou, a instalação de atualizações de software padrão todo mês em que a instalação durante a janela de manutenção também poderia confirma as alterações das definições de atualização de software. No entanto, neste cenário, em que as atualizações de software padrão não são executadas e é pouco provável que o software de apresentação interativa seja atualizado com frequência, isso pode ocorrer meses antes de as atualizações de definição de software serem vinculadas automaticamente à imagem.  

     O administrador primeiro cria uma sequência de tarefas personalizada que não tem configurações, a não ser o nome. Ele executa o Assistente para Criar Sequência de Tarefas:  

    1. Na página **Criar uma Sequência de Tarefas**, o administrador seleciona **Criar uma sequência de tarefas personalizada** e, em seguida, clica em **Avançar**.  

    2. Na página **Informações da Sequência de Tarefas**, o administrador insere **Tarefa de manutenção para confirmar alterações em dispositivos inseridos** como o nome da sequência de tarefas e, em seguida, clica em **Avançar**.  

    3. Na página **Resumo**, o administrador seleciona **Avançar** e conclui o assistente.  

       Em seguida, o administrador implanta essa sequência de tarefas personalizada na coleção de dispositivos Windows Embedded e configura o agendamento para ser executado todos os meses. Como parte das configurações de implantação, ele marca a caixa de seleção **Confirmar as alterações na data limite ou durante uma janela de manutenção (exige reinicializações)** para persistir as alterações após uma reinicialização. Para configurar essa implantação, o administrador seleciona a sequência de tarefas personalizada recém-criada e, em seguida, na guia **Página Inicial**, no grupo **Implantação**, ele clica em **Implantar** para iniciar o Assistente de Implantação de Software:  

    4. Na página **Geral**, o administrador seleciona a coleção de dispositivos Windows Embedded e, em seguida, clica em **Avançar**.  

    5. Na página **Configurações de Implantação**, o administrador seleciona a **Finalidade** de **Obrigatório** e, em seguida, clica em **Avançar**.  

    6. Na página **Agendamento**, o administrador clica em **Novo** para especificar um agendamento semanal durante a janela de manutenção e, em seguida, clica em **Avançar**.  

    7. O administrador conclui o assistente sem outras alterações.  

       Para obter mais informações, consulte  
                 [Gerenciar sequências de tarefas para automatizar tarefas no System Center Configuration Manager](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md).  

11. Para que os quiosques sejam executados automaticamente, o administrador escreve um script para definir os dispositivos com as seguintes configurações:  

    - Efetuar logon automaticamente, usando uma conta de convidado que não tenha senha.  

    - Executar automaticamente na inicialização a apresentação interativa do software.  

      O administrador usa pacotes e programas para implantar esse script na coleção de dispositivos Windows Embedded. Quando o administrador executa o Assistente de Implantação de Software, ele marca novamente a caixa de seleção **Confirmar as alterações na data limite ou durante uma janela de manutenção (exige reinicializações)** para persistir as alterações após uma reinicialização.  

      Para obter mais informações, consulte [Pacotes e programas no System Center Configuration Manager](../../../apps/deploy-use/packages-and-programs.md).  

12. Na manhã seguinte, o administrador verifica os dispositivos Windows Embedded. Ele confirma o seguinte:  

    - O quiosque está conectado automaticamente usando a conta de convidado.  

    - O software de apresentação interativa está sendo executado.  

    - O cliente do Endpoint Protection está instalado e possui as definições de atualização de software mais recentes.  

    - Esse dispositivo foi reiniciado durante a janela de manutenção.  

      Para obter mais informações, consulte:  

    - [Como monitorar o Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/monitor-endpoint-protection.md)  

    - [Monitorar aplicativos com o System Center Configuration Manager](/sccm/apps/deploy-use/monitor-applications-from-the-console)  

13. O administrador monitora os quiosques e relata o gerenciamento bem-sucedido deles a seu gerente. Como resultado, 20 quiosques são requisitados para o centro de visitantes.  

     Para evitar a instalação manual do cliente do Configuration Manager, que exige a desabilitação e a posterior habilitação manual dos filtros de gravação, o administrador garante que a ordem inclui uma imagem personalizada que já inclui a instalação e a atribuição de site do cliente do Configuration Manager. Além disso, os dispositivos são nomeados de acordo com o formato de nome da empresa.  

     Os quiosques são entregues ao centro de visitantes uma semana antes de sua abertura. Durante esse tempo, os quiosques são conectados à rede, todo o gerenciamento de dispositivos deles é automático e não é necessário administrador local. O administrador confirma se os quiosques estão funcionando conforme exigido:  

    -   Os clientes nos quiosques concluem o gerenciamento do site e baixam a chave de raiz confiável dos Serviços de Domínio Active Directory.  

    -   Os clientes nos quiosques são adicionados automaticamente à coleção de dispositivos do Windows Embedded e configurados com a janela de manutenção.  

    -   O cliente do Endpoint Protection está instalado e possui as definições de atualização de software mais recentes para proteção antimalware.  

    -   O software de apresentação interativa está instalado e sendo executado automaticamente, pronto para os visitantes.  

14. Após a configuração inicial, toda reinicialização exigida pelas atualizações ocorre somente quando o centro de visitantes está fechado.  
