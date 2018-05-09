---
title: Cenário de exemplo para implantar e monitorar as atualizações de software de segurança
titleSuffix: Configuration Manager
description: Use este cenário de exemplo de como usar atualizações de software no Configuration Manager para implantar e monitorar as atualizações de software de segurança que a Microsoft lança mensalmente.
author: aczechowski
manager: dougeby
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: c32f757a-02da-43f2-b055-5cfd097d8c43
ms.author: aaroncz
ms.openlocfilehash: eadb7dc9f3f9fc4f4ccca1b27257d8f05cb19ebc
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="example-scenario-for-using-system-center-configuration-manager-to-deploy-and-monitor-the-security-software-updates-released-monthly-by-microsoft"></a>Exemplo de cenário de uso do System Center Configuration Manager para implantar e monitorar as atualizações de software de segurança liberadas mensalmente pela Microsoft

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico fornece um cenário de exemplo de como usar atualizações de software no System Center Configuration Manager para implantar e monitorar as atualizações de software de segurança que a Microsoft lança mensalmente.  

 Neste cenário, João é o administrador do Configuration Manager no Banco Woodgrove. João precisa criar uma estratégia de implantação de atualização de software com as condições e os requisitos a seguir:  

-   A implantação de atualização de software ativo ocorre uma vez por semana, após a Microsoft lançar as atualizações de software de segurança na segunda terça-feira de cada mês. Esse evento é normalmente conhecido como "Patch Tuesday".  

-   Atualizações de software são baixadas e testadas nos pontos de distribuição. Então, uma implantação é testada em uma sub-rede de clientes antes de João implementar integralmente as atualizações de software em seu ambiente de produção.  

-   João poderá monitorar a conformidade das atualizações de software mensalmente ou anualmente.  

 Este cenário pressupõe que a infraestrutura do ponto de atualização de software já foi implementada. Use as informações na tabela a seguir para planejar e configurar as atualizações de software no Configuration Manager.  

|Processar|Referência|  
|-------------|---------------|  
|Rever os conceitos principais para atualizações de software.|[Introdução às atualizações de software](../understand/software-updates-introduction.md)|  
|Planejar atualizações de software. Essas informações ajudam a planejar considerações quanto à capacidade e a determinar a infraestrutura do ponto de atualização de software, a instalação do ponto de atualização de software, as configurações de sincronização e as configurações de cliente para atualizações de software.|[Planejar atualizações de software](../plan-design/plan-for-software-updates.md)|  
|Configurar as atualizações de software. Essas informações ajudam a instalar e configurar os pontos de atualização de software em sua hierarquia e a configurar e sincronizar as atualizações de software.<br /><br /> Neste cenário, João configura o agendamento da sincronização de atualizações de software para ocorrer na segunda quarta-feira de cada mês, garantindo assim recuperar as atualizações mais recentes de software de segurança da Microsoft.|[Sincronizar atualizações de software](../get-started/synchronize-software-updates.md)|  

 As seções a seguir, neste tópico, fornecem como exemplo etapas para ajudá-lo a implantar e monitorar as atualizações de software de segurança do Configuration Manager em sua organização.

##  <a name="BKMK_Step1"></a> Etapa 1: Criar um grupo de atualização de software para fins de conformidade anual  
 João cria um grupo de atualização de software que pode ser usado para monitorar a conformidade de todas as atualizações de software de segurança lançadas em 2016. Ele executa as etapas da tabela a seguir.  

|Processar|Referência|  
|-------------|---------------|  
|No nó **Todas as Atualizações de Software** do console do Configuration Manager, João adiciona critérios para exibir somente as atualizações de software de segurança liberadas ou revisadas no ano de 2015 que atendem aos seguintes critérios:<br /><br /><ul><li>**Critérios**: Data de lançamento ou revisão</li><li>**Condição**: é maior ou igual à data específica<br />**Valor**: 1/1/2015</li><li>**Critérios**: classificação da atualização<br />**Valor**: Atualizações de Segurança</li><li>**Critérios**: Expirado <br />**Valor**: Não</li></ul>|Nenhuma informação adicional|
|João adiciona todas as atualizações de software filtradas a um novo grupo de atualização de software com os seguintes requisitos:<br /><br /><ul><li>**Nome**: Grupo de Conformidade - Atualizações de Segurança da Microsoft 2015</li><li>**Descrição**: Atualizações de software|[Adicionar atualizações de software a um grupo de atualização](add-software-updates-to-an-update-group.md)|  

##  <a name="BKMK_Step2"></a> Etapa 2: Criar uma regra de implantação automática para o mês atual  
 João cria uma regra de implantação automática para as atualizações de software de segurança lançadas pela Microsoft para o mês vigente. Ele executa as etapas da tabela a seguir.  

|Processar|Referência|  
|-------------|---------------|  
|João cria uma regra de implantação automática com os seguintes requisitos:<br /><br /><ol><li>Na guia **Geral** , João configura o seguinte:<br /> <ul><li>Especifica o nome **Atualizações de Segurança Mensais**.</li><li>Seleciona um conjunto de teste com clientes limitados.</li><li>Seleciona **Criar um novo grupo de atualização de software**.</li><li>Verifica se **Habilitar a implantação após esta regra ser executada** não está selecionado.</li></ul></li><li>Na guia **Configurações de implantação** , João seleciona as configurações padrão.</li><li>Na página **Atualizações de software**, João configura os seguintes filtros de propriedade e critérios de pesquisa:<br /><ul><li>Data de lançamento ou revisão **Último mês**.</li><li>Classificação da atualização **Atualizações de segurança**.</li></ul></li><li>Na página **Avaliação**, João habilita a regra para execução em um agendamento para a **segunda quinta-feira** de cada **mês**. João também verifica que seu agendamento da sincronização está definido para execução na **segunda quarta-feira** de cada **mês**.</li><li>João usa as configurações padrão nas páginas de Agendamento de implantação, Experiência do usuário, Alertas e Configurações de download.</li><li>Na página do **Pacote de Implantação**, João especifica um novo pacote de implantação.</li><li>João usa as configurações padrão nas páginas de Local de download e Seleção de idioma.</li></ol>|[Implantar atualizações de software automaticamente](automatically-deploy-software-updates.md)|  

##  <a name="BKMK_Step3"></a> Etapa 3: Verificar se as atualizações de software estão prontas para ser implantadas  
 Na segunda quinta-feira de cada mês, João verifica se as atualizações de software estão prontas para ser implantadas. Ele executa a etapa a seguir.  

|Processar|Referência|  
|-------------|---------------|  
|João verifica se a sincronização de atualizações de software foi concluída com êxito.|[Status da sincronização de atualizações de software](monitor-software-updates.md#BKMK_SUSyncStatus)|  

##  <a name="BKMK_Step4"></a> Etapa 4: Implantar o grupo de atualização de software  
 Depois que João verifica que as atualizações de software estão prontas para ser implantadas, ele implanta as atualizações. Ele executa as etapas da tabela a seguir.  

|Processar|Referência|  
|-------------|---------------|  
|João cria duas implantações de teste para o novo grupo de atualização de software. Ele considera os ambientes a seguir para cada implantação:<br /><br /> **Implantação de teste da estação de trabalho**: John considera o seguinte para a implantação de teste da estação de trabalho:<br /><br /><ul><li>Especifica uma coleção de implantação que contém um subconjunto de clientes da estação de trabalho para verificar a implantação.</li><li>Define as configurações de implantação apropriadas para os clientes da estação de trabalho em seu ambiente.</li></ul><br />**Implantação de teste do servidor**: John considera o seguinte para a implantação de teste do servidor:<br /><br /><ul><li>Especifica uma coleção de implantação que contém um subconjunto de clientes de servidor para verificar a implantação.</li><li>Define as configurações de implantação apropriadas para os clientes de servidor em seu ambiente.</li></ul>|[Implantar atualizações de software](deploy-software-updates.md)|  
|João verifica se as implantações de teste obtiveram êxito.|[Status de implantação de atualizações de software](monitor-software-updates.md#BKMK_SUDeployStatus)|  
|João atualiza as duas implantações com novas coleções que incluem seus servidores e estações de trabalho de produção.|Nenhuma informação adicional|  

##  <a name="BKMK_Step5"></a> Etapa 5: Monitorar a conformidade das atualizações de software implantadas  
 João monitora a conformidade de suas implantações de atualização de software. Ele executa a etapa da tabela a seguir.  

|Processar|Referência|  
|-------------|---------------|  
|João monitora o status da implantação de atualizações de software no console do Configuration Manager e verifica os relatórios de implantação de atualização de software disponíveis no console.|[Monitorar atualizações de software no System Center Configuration Manager](../../sum/deploy-use/monitor-software-updates.md)|  

##  <a name="BKMK_Step6"></a> Etapa 6: Adicionar atualizações de software mensais ao grupo de atualização anual  
 João adiciona as atualizações de software do grupo de atualização de software mensal ao grupo de atualização de software anual. Ele executa a etapa da tabela a seguir.  

|Processar|Referência|  
|-------------|---------------|  
|João seleciona as atualizações de software do grupo de atualização mensal e adiciona as atualizações de software ao grupo de atualização que ele criou para fins de conformidade anual. Para viabilizar o gerenciamento, ele controla a conformidade da atualização de software e cria vários relatórios.|[Adicionar atualizações de software a um grupo de atualização implantado](add-software-updates-to-an-update-group.md)|  

João concluiu com êxito sua implantação mensal de atualizações de software de segurança. Ele continuará monitorando e documentando a conformidade das atualizações de software para assegurar que os clientes em seu ambiente estejam dentro dos níveis de conformidade aceitáveis.  

##  <a name="BKMK_MonthlyProcess"></a> Processo mensal recorrente para implantar atualizações de software  
 Depois do primeiro mês em que implantou as atualizações de software, João executa as etapas de três a seis para implantar as atualizações de software de segurança lançadas mensalmente pela Microsoft.  
