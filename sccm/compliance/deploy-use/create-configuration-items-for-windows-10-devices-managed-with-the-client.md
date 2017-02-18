---
title: "Criar itens de configuração para o Windows 10 gerenciado pelo cliente – Configuration Manager | Microsoft Docs"
description: "Use o item de configuração do System Center Configuration Manager no Windows 10 para gerenciar configurações para computadores Windows 10 que são gerenciados pelo cliente do Configuration Manager."
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 14226fbe-dd07-4432-910b-130790624a4e
caps.latest.revision: 17
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 35e48666f4d1a2363304650f960531fd0630a291
ms.openlocfilehash: 030cc33d98c81f3a6d5dff2d4c011e03fff12dc2


---
# <a name="create-configuration-items-for-windows-10-devices-managed-with-the-system-center-configuration-manager-client"></a>Criar itens de configuração para dispositivos Windows 10 gerenciados com o Cliente do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use o item de configuração do System Center Configuration Manager no **Windows 10** para gerenciar configurações para computadores Windows 10 que são gerenciados pelo cliente do Configuration Manager.  

> [!IMPORTANT]  
>  Nesta versão, se você criou uma configuração **Senha** como parte de um item de configuração do tipo **Windows 10** (para um dispositivo gerenciado com o cliente do Configuration Manager), se a configuração ainda não existir ou se não tiver sido configurada no dispositivo Windows 10, ela será avaliada incorretamente como compatível.  
>   
>  Como alternativa, quando você criar uma configuração para esses dispositivos, verifique se a opção **Corrigir configurações não compatíveis** está marcada nas páginas de configurações do assistente para Criar Item de Configuração. Além disso, ao implantar uma linha de base de configuração que contém um item de configuração do Windows 10 que, por sua vez, contém configurações de senha, selecione **Corrigir regras não compatíveis quando suportadas** na caixa de diálogo Implantar Linhas de Base de Configuração. Usando essa solução alternativa, a configuração será monitorada e corrigida se for considerada não compatível. Após a correção, a configuração será relatada corretamente como **Compatível** (a menos que um problema seja encontrado; nesse caso, ele relatará **Erro**).  

## <a name="create-a-windows-10-configuration-item"></a>Criar um item de configuração do Windows 10  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Configurações de Conformidade** > **Itens de Configuração**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Item de Configuração**.  

4.  Na página **Geral** do **Assistente para Criar Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.  

5.  Em **Especificar o tipo de item de configuração que deseja criar**, selecione **Windows 10**.  

6.  Se você criar e atribuir categorias, clique em **Categorias** para ajudá-lo a pesquisar e filtrar itens de configuração no console do Configuration Manager.  

7.  Na página **Plataformas com Suporte**, selecione as plataformas específicas do Windows 10 que avaliarão o item de configuração.  

8.  Na página **Configurações do Dispositivo**, selecione o grupo de configurações que você deseja configurar. Consulte [Referência das definições de item de configuração do Windows 10](/sccm/compliance/deploy-use/create-configuration-items-for-windows-10-devices-managed-with-the-client#windows-10-configuration-item-settings-reference) neste tópico para obter detalhes e clique **Avançar**.  

    > [!TIP]  
    >  Se a configuração desejada não estiver na lista, marque a **caixa de seleção Definir configurações adicionais que não estão nos grupos de configuração padrão**.  

9. Em cada página de configurações, defina as configurações necessárias e se deseja corrigi-las quando não forem compatíveis nos dispositivos (quando houver suporte para essa opção).  

10. Para cada grupo de configurações, você também pode configurar a severidade que será relatada (nos relatórios do Configuration Manager) quando um item de configuração for considerado não compatível de:  

    -   **Nenhum** – Os dispositivos que não obedecem esta regra de conformidade não relatam uma severidade de falha.  

    -   **Informações** – Os dispositivos que não obedecem esta regra de conformidade relatam uma severidade de falha de **Informações**.  

    -   **Aviso** – Os dispositivos que não obedecem esta regra de conformidade relatam uma severidade de falha de **Aviso**.  

    -   **Crítico** – Os dispositivos que não obedecem esta regra de conformidade relatam uma severidade de falha de **Crítico**.  

    -   **Crítico com evento** – Os dispositivos que não obedecem esta regra de conformidade relatam uma severidade de falha de **Crítico**. Este nível de severidade também é registrado como um evento do Windows no log de eventos do aplicativo.  

11. Na página **Aplicabilidade da Plataforma**, examine as configurações que não são compatíveis com as plataformas com suporte selecionadas anteriormente. Você pode voltar e remover essas configurações ou pode continuar.  

    > [!TIP]  
    >  As configurações sem suporte não são avaliadas quanto à conformidade.  

12. Conclua o assistente.  

 Você pode exibir o novo item de configuração no nó **Itens de Configuração** do espaço de trabalho **Ativos e Conformidade** .  

##  <a name="windows-10-configuration-item-settings-reference"></a>Referência de configurações do item de configuração do Windows 10  

### <a name="password"></a>Senha  

|Configuração|Detalhes|  
|-------------|-------------|  
|**Configurações de senha necessárias em dispositivos**|Requer uma senha nos dispositivos com suporte.|  
|**Comprimento mínimo da senha (caracteres)**|O comprimento mínimo de caracteres para a senha.|  
|**Validade da senha em dias**|O número de dias antes que a senha precise ser alterada.|  
|**Número de senhas lembradas**|Impede a reutilização das senhas anteriores.|  
|**Número de tentativas de logon com falha antes do apagamento do dispositivo**|Apaga o dispositivo se o logon falhar esse número de vezes.|  
|**Tempo ocioso antes de o dispositivo móvel ser bloqueado**|Especifica quantos minutos o dispositivo deve ficar inativo antes que seja bloqueado automaticamente.|  
|**Complexidade da senha**|Escolha se é possível especificar um PIN como “1234” ou se é necessário fornecer uma senha forte.|  

###  <a name="device"></a>Dispositivo  

|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Bluetooth**|Permite o uso do recurso Bluetooth do dispositivo.|  

### <a name="cloud"></a>Nuvem  

|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Sincronização de configurações**|Permite a sincronização de configurações entre dispositivos.|  
|**Sincronização de credenciais**|Permite a sincronização de credenciais entre dispositivos.|  
|**Sincronização de configurações em conexões medidas**|Permita que as configurações sejam sincronizadas durante a medição da conexão com a Internet.|  

### <a name="roaming"></a>Roaming  

|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Roaming de dados**|Permita o roaming entre redes durante o acesso de dados.|  

### <a name="encryption"></a>Criptografia  

|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Criptografia de arquivo no dispositivo**|Exige que os arquivos no dispositivo sejam criptografados.|  

### <a name="system-security"></a>Segurança do sistema  

|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Controle de conta de usuário**|Define como o Controle de Conta de Usuário do Windows funciona no dispositivo.<br />Por exemplo, você pode desabilitá-lo ou definir o nível no qual ele o notificará.|  
|**Firewall da rede**|Habilita ou desabilita o Firewall do Windows.|  
|**SmartScreen**|Habilite ou desabilite o Windows SmartScreen.|  
|**Proteção contra vírus**|Exige que o software antivírus seja instalado e configurado.|  
|**As assinaturas de proteção contra vírus estão atualizadas**|Exige que os arquivos de assinatura do software antivírus no dispositivo sejam atualizados.|  

### <a name="windows-information-protection"></a>Proteção de Informações do Windows

Com o aumento do uso de dispositivos de funcionário dentro da empresa, aumenta também o risco de vazamentos acidentais de dados por meio de aplicativos e serviços, como email, mídia social e nuvem pública, que estão fora do controle da empresa. Por exemplo, quando um funcionário envia as imagens mais recentes de engenharia da sua conta de email pessoal, copia e cola informações do produto em um tweet ou salva um relatório de vendas em andamento no armazenamento de nuvem pública.

A WIP (Proteção de Informações do Windows) ajuda a proteger contra possíveis vazamentos de dados sem interferir de outras formas na experiência do funcionário. A WIP também ajuda a proteger dados e aplicativos corporativos contra vazamento acidental de dados em dispositivos corporativos e dispositivos pessoais que os funcionários levam para o trabalho, sem a necessidade de que sejam feitas alterações em seu ambiente ou em outros aplicativos.

 Os itens de configuração da WIP do Configuration Manager gerenciam a lista de aplicativos protegidos pela WIP, os locais de rede corporativa, o nível de proteção e as configurações de criptografia.

Para obter informações sobre como configurar a Proteção de Informações do Windows com o Configuration Manager, consulte [Proteger os dados da empresa usando a WIP (Proteção de Informações do Windows)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip).



<!--HONumber=Jan17_HO4-->


