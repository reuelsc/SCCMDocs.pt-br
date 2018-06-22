---
title: Como criar itens de configuração para dispositivos com Android for Work gerenciados com o Intune
titleSuffix: Configuration Manager
ms.date: 2017-07-31
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ab6784fd-8c57-4be9-858f-50fe39f2ff5f
author: aczechowski
ms.author: aaroncz
ms.openlocfilehash: ba70e4d3a87f2a305312449907730174c62c4775
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351268"
---
# <a name="how-to-create-configuration-items-for-android-for-work-devices-managed-with-intune"></a>Como criar itens de configuração para dispositivos com Android for Work gerenciados com o Intune

 Use o item de configuração **Android for Work** do System Center Configuration Manager para gerenciar configurações para dispositivos do Android for Work que estão registrados no Microsoft Intune ou são gerenciados localmente pelo Configuration Manager.  

### <a name="to-create-an-android-for-work-configuration-item"></a>Para criar um item de configuração para o Android for Work  

1.  No console do Configuration Manager, clique em **Ativos e conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , expanda **Configurações de Conformidade**e clique em **Itens de Configuração**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Item de Configuração**.  

4.  Na página **Geral** do **Assistente para Criar Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.  

5.  Em **Especificar o tipo de item de configuração que deseja criar**, selecione **Android for Work**.  

6.  Escolha **Categorias** se você criar e atribuir categorias para ajudá-lo a pesquisar e filtrar os itens de configuração no console do Configuration Manager.  

  Clique em **Avançar**.

7.  Na página **Configurações do Dispositivo** do assistente, selecione os grupos de configurações que você quer configurar. Confira [Configurações de item de configuração do Android for Work](#android-for-work-configuration-item-settings-reference) para obter detalhes, e clique em **Avançar**.  

  > [!TIP]  
  >  Se a configuração desejada não estiver na lista, marque a **caixa de seleção Definir configurações adicionais que não estão nos grupos de configuração padrão**.  

9. Em cada página de configurações, defina as configurações necessárias e se deseja corrigi-las quando não forem compatíveis nos dispositivos (quando houver suporte para essa opção).  

10. Para cada grupo de configurações, você também pode configurar a severidade que será relatada quando um item de configuração for considerado não compatível de:  

    -   **Nenhum** – dispositivos que não cumprem essa regra de conformidade não relatam uma severidade de falha em relatórios do Configuration Manager.  

    -   **Informações** – dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha de **Informações** em relatórios do Configuration Manager.  

    -   **Aviso** – dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha de **Aviso** em relatórios do Configuration Manager.  

    -   **Crítico** – dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico** em relatórios do Configuration Manager.  

    -   **Crítico com evento** – dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico com evento** em relatórios do Configuration Manager. Este nível de severidade também é registrado como um evento do Windows no log de eventos do aplicativo.  

11. Na página **Aplicabilidade da Plataforma** do assistente, examine as configurações que não são compatíveis com as plataformas com suporte selecionadas anteriormente. Você pode voltar e remover essas configurações ou pode continuar.  

    > [!TIP]  
    >  As configurações sem suporte não são avaliadas quanto à conformidade.  

12. Conclua o assistente.  

 Você pode exibir o novo item de configuração no nó **Itens de Configuração** do espaço de trabalho **Ativos e Conformidade** .  

##  <a name="android-for-work-configuration-item-settings-reference"></a>Referência de configurações do item de configuração do Android for Work  

### <a name="password"></a>Senha  

|Configuração|Detalhes|  
|-------------|-------------|  
|**Exigir configurações de senha em dispositivos**|Requer uma senha nos dispositivos com suporte.|  
|**Comprimento mínimo da senha (caracteres)**|O comprimento mínimo da senha.|  
|**Validade da senha em dias**|O número de dias antes que uma senha precise ser alterada.|  
|**Número de senhas lembradas**|Impede a reutilização de senhas usadas recentes.|  
|**Número de tentativas de logon com falha antes de o dispositivo ser apagado**|Apaga o dispositivo se houver falha neste número de tentativas de logon.|  
|**Tempo ocioso antes que o dispositivo móvel seja bloqueado**|Selecione a quantidade de tempo durante o qual o dispositivo fica inutilizado de ser bloqueado.|
|**Qualidade da senha**|Selecione o nível necessário de complexidade de senha e também se dispositivos biométricos podem ser usados.|  
|**Permitir Smart Lock e outros agentes de confiança**|Permite controlar o recurso Smart Lock em dispositivos Android compatíveis. Essa capacidade do telefone, às vezes conhecida como agentes de confiança, permite desabilitar ou ignorar a senha da tela de bloqueio do dispositivo se o dispositivo estiver em um local confiável, como quando ele está conectado a um dispositivo Bluetooth específico, ou quando ele está perto de uma marca NFC. Você pode usar essa configuração para impedir que usuários finais configurem o Smart Lock.|
|**Impressão digital de desbloqueio**|&nbsp;|

###  <a name="work-profile"></a>Perfil de trabalho  
 Estas configurações se aplicam apenas a dispositivos Samsung KNOX.  

|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Permitir o compartilhamento de dados entre perfis pessoais e de trabalho**|Escolha:<br>- **Não configurado**<br>- **Restrições de compartilhamento padrão**<br>- **Os aplicativos no perfil de trabalho podem lidar com solicitações de perfil pessoal**<br>- **Os aplicativos no perfil pessoal podem lidar com solicitações de perfil de trabalho**<br><br>(Confira também [Configurações de copiar e colar](#copy-paste-configuration-item-settings) usando o URI personalizado)|  
|**Ocultar notificações de perfil de trabalho quando o dispositivo estiver bloqueado (Android 6.0 e posteriores)**||
|**Definir política de permissão do aplicativo padrão (Android 6.0 e posteriores)**|Escolha:<br>- **Não configurado**<br>- **Sempre solicitar**<br>- **Concessão automática**<br>- **Negação automática**|

### <a name="copy-paste-configuration-item-settings"></a>Copiar e colar definições de item de configuração
Nenhuma das opções **Permitir compartilhamento de dados entre perfis pessoais e de trabalho** impede o comportamento de copiar e colar. Use uma configuração personalizada que pode ser configurada para impedir ações de copiar e colar. Isso pode ser definido por meio do URI personalizado.

- OMA-URI: ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
- Tipo de valor: Booliano

A definição de DisallowCrossProfileCopyPaste como true impede o comportamento de copiar e colar entre perfis de trabalho e pessoal do Android for Work.

## <a name="see-also"></a>Consulte também  
 [Itens de configuração de dispositivos gerenciados sem o cliente do System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)
