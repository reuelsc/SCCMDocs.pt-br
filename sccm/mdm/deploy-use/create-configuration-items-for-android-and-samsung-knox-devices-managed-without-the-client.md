---
title: "Criar itens de configuração para dispositivos Android e Samsung KNOX Standard gerenciados com o Intune | Microsoft Docs"
description: "Use o item de configuração do Android e Samsung KNOX Standard no System Center Configuration Manager para gerenciar as configurações dos dispositivos."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b66f3c4-e3bb-4f6a-abd5-55be649ff90d
caps.latest.revision: 17
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 67ea4d2a7c9753aa406a84157930564213b6cc0a
ms.lasthandoff: 03/06/2017


---
# <a name="create-configuration-items-for-android-and-samsung-knox-standard-devices-managed-with-intune"></a>Criar itens de configuração para dispositivos Android e Samsung KNOX Standard gerenciados com o Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use o item de configuração **Android e Samsung KNOX** do System Center Configuration Manager para gerenciar configurações para dispositivos Android e Samsung KNOX Standard que estão registrados no Microsoft Intune ou são gerenciados localmente pelo Configuration Manager.  

## <a name="create-an-android-and-samsung-knox-standard-configuration-item"></a>Criar um item de configuração do Android e Samsung KNOX Standard  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Configurações de Conformidade** > **Itens de Configuração**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Item de Configuração**.  

4.  Na página **Geral** do **Assistente para Criar Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.  

5.  Em **Especificar o tipo de item de configuração que deseja criar**, selecione **Android e Samsung KNOX**.  

6.  Se você criar e atribuir categorias, clique em **Categorias** para ajudá-lo a pesquisar e filtrar itens de configuração no console do Configuration Manager.  

7.  Na página **Plataformas com Suporte**, selecione as plataformas específicas do Android ou Samsung KNOX Standard que avaliarão o item de configuração.  

8.  Na página **Configurações do Dispositivo**, selecione o grupo de configurações que você deseja configurar. Veja [Referência de configurações do item de configuração para o Android e Samsung KNOX Standard](#android-and-samsung-knox-standard-configuration-item-settings-reference) neste tópico para obter detalhes e clique **Avançar**.  

    > [!TIP]  
    >  Se a configuração desejada não estiver na lista, marque a **caixa de seleção Definir configurações adicionais que não estão nos grupos de configuração padrão**.  

9. Em cada página de configurações, defina as configurações necessárias e se deseja corrigi-las quando não forem compatíveis nos dispositivos (quando houver suporte para essa opção).  

10. Para cada grupo de configurações, você também pode configurar a severidade que será relatada (nos relatórios do Configuration Manager) quando um item de configuração for considerado não compatível de:  

    -   **Nenhum** – Os dispositivos que não obedecem esta regra de conformidade não relatam uma severidade de falha.  

    -   **Informações** – Os dispositivos que não obedecem esta regra de conformidade relatam uma severidade de falha de **Informações**.  

    -   **Aviso** – Os dispositivos que não obedecem esta regra de conformidade relatam uma severidade de falha de **Aviso**.  

    -   **Crítico** – Os dispositivos que não obedecem esta regra de conformidade relatam uma severidade de falha de **Crítico**.  

    -   **Crítico com evento** – Os dispositivos que não obedecem esta regra de conformidade relatam uma severidade de falha de **Crítico**.   

11. Na página **Aplicabilidade da Plataforma**, examine as configurações que não são compatíveis com as plataformas com suporte selecionadas anteriormente. Você pode voltar e remover essas configurações ou pode continuar.  

    > [!TIP]  
    >  As configurações sem suporte não são avaliadas quanto à conformidade.  

12. Conclua o assistente.  

 Você pode exibir o novo item de configuração no nó **Itens de Configuração** do espaço de trabalho **Ativos e Conformidade** .  

##  <a name="android-and-samsung-knox-standard-configuration-item-settings-reference"></a>Referência de configurações do item de configuração para o Android e Samsung KNOX Standard  

### <a name="password"></a>Senha  
 Essas configurações se aplicam aos dispositivos Android e Samsung KNOX Standard.  

|Configuração|Detalhes|  
|-------------|-------------|  
|**Exigir configurações de senha em dispositivos**|Requer uma senha nos dispositivos com suporte.|  
|**Comprimento mínimo da senha (caracteres)**|O comprimento mínimo da senha.|  
|**Validade da senha em dias**|O número de dias antes que uma senha precise ser alterada.|  
|**Número de senhas lembradas**|Impede a reutilização de senhas usadas anteriormente.|  
|**Número de tentativas de logon com falha antes de o dispositivo ser apagado**|Apaga o dispositivo se houver falha neste número de tentativas de logon.|  
|**Tempo ocioso antes que o dispositivo móvel seja bloqueado**|Selecione o período até que o dispositivo seja bloqueado se não estiver sendo usado.|
|**Qualidade da senha**|Selecione o nível necessário de complexidade de senha e também se dispositivos biométricos podem ser usados.|  
|**Permitir Smart Lock e outros agentes de confiança**|Permite controlar o recurso Smart Lock em dispositivos Android compatíveis. Essa capacidade do telefone, às vezes conhecida como agentes de confiança, permite desabilitar ou ignorar a senha da tela de bloqueio do dispositivo se o dispositivo estiver em um local confiável, como quando ele está conectado a um dispositivo Bluetooth específico, ou quando ele está perto de uma marca NFC. Você pode usar essa configuração para impedir que usuários finais configurem o Smart Lock.|
|Impressão digital de desbloqueio (KNOX 5.0+)|Permite que usuários usem uma impressão digital para desbloquear dispositivos compatíveis.|

###  <a name="device"></a>Dispositivo  
 Estas configurações se aplicam apenas a dispositivos Samsung KNOX Standard.  

|Nome da configuração|Detalhes|  
|------------------|-------------|
|**Discagem de voz**|Habilita ou desabilita o recurso de discagem de voz no dispositivo.|
|**Assistente de voz**|Permite o uso do software Assistente de voz no dispositivo.|
|**Captura de tela**|Permite ao usuário capturar o conteúdo da tela como uma imagem.|
|**Envio de dados de diagnóstico**|Permite que o dispositivo envie informações de diagnóstico ao Google.|
|**Localização geográfica**|Permite que o dispositivo utilize informações de localização.|
|**Copiar e colar**|Permite as funções de copiar e colar no dispositivo.|  
|**Redefinição de fábrica**|Permita que o usuário execute uma redefinição de fábrica no dispositivo.|  
|**Permitir compartilhamento de área de transferência entre aplicativos**|Use a área de transferência para copiar e colar entre aplicativos.|
|**Bluetooth**|Permite o uso do recurso Bluetooth do dispositivo.|

### <a name="store"></a>Repositório
|Configuração|Detalhes|  
|-------------|-------------|  
|**Armazenamento de aplicativos**|Permite o acesso ao aplicativo Google Play Store no dispositivo.|

### <a name="browser"></a>Navegador
|Configuração|Detalhes|  
|-------------|-------------|
|**Permitir navegador da Web**|Especifica se o navegador da Web padrão do dispositivo pode ser usado.|
|**Preenchimento automático**|Permite o uso da função de preenchimento automático do navegador da Web.|
|**Script ativo**|Permite que o navegador da Web do dispositivo use o script ativo.|
|**Bloqueador de pop-up**|Permite o uso de um bloqueador de pop-up no navegador da Web.|
|**Cookies**|Permite que o navegador da Web do dispositivo use cookies.|

### <a name="cloud"></a>Nuvem  
 Estas configurações se aplicam apenas a dispositivos Samsung KNOX Standard.  

|Configuração|Detalhes|  
|-------------|-------------|  
|**Backup do Google**|Permite o uso do backup do Google.|  
|**Sincronização automática da conta do Google**|Permite que as configurações de conta do Google sejam sincronizadas automaticamente.|  



### <a name="security"></a>Segurança  

|Configuração|Detalhes|  
|-------------|-------------|  
|**Mensagens SMS e MMS**|Permite o uso de mensagens SMS e MMS no dispositivo.|
|**Armazenamento removível**|Permita que o dispositivo use o armazenamento removível, como um cartão SD.|
|**Câmera**|Permite o uso da câmera do dispositivo.<br /><br /> Aplica-se a dispositivos Android e Samsung KNOX Standard.|  
|**Comunicação a curta distância (NFC)**|Permite operações que usam comunicação de curta distância, se o dispositivo oferecer suporte.|
|**YouTube**|Permite o uso do aplicativo YouTube no dispositivo.<br /><br /> Aplica-se somente a dispositivos Samsung KNOX Standard.|  
|**Desligar**|Permite que o dispositivo seja desligado.<br /><br /> Aplica-se somente a dispositivos Samsung KNOX Standard.|

### <a name="roaming"></a>Roaming
|Configuração|Detalhes|  
|-------------|-------------|
|**Roaming de voz**|Permite o roaming de voz quando o dispositivo estiver em uma rede de celular.|
|**Roaming de dados**|Permite o roaming de dados quando o dispositivo estiver em uma rede de celular.|

### <a name="encryption"></a>Criptografia  
 Essas configurações se aplicam aos dispositivos Android e Samsung KNOX Standard.  

|Configuração|Detalhes|  
|-------------|-------------|  
|**Criptografia de cartão de memória**|Especifica se o cartão de armazenamento do dispositivo deve ser criptografado.|
|**Criptografia de arquivo no dispositivo**|Requer que os arquivos no dispositivo móvel sejam criptografados.|  

### <a name="wireless-communications"></a>Comunicações sem fio
|Configuração|Detalhes|  
|-------------|-------------|
|**Conexão de rede sem fio**|Permite o uso dos recursos de Wi-Fi do dispositivo.|
|**Compartilhamento de Internet por Wi-Fi**|Permite o uso de compartilhamento de Internet por Wi-Fi no dispositivo.|


### <a name="kiosk-mode-samsung-knox-standard-only"></a>Modo de quiosque (apenas Samsung KNOX Standard)  
 O modo de quiosque permite bloquear um dispositivo para permitir que somente alguns recursos funcionem. Por exemplo, você pode permitir que um dispositivo execute apenas um aplicativo gerenciado que você especificar ou pode desabilitar os botões de volume em um dispositivo. Essas configurações podem ser usadas para um modelo de demonstração de um dispositivo ou um dispositivo que é dedicado a apenas uma função, como um dispositivo de ponto de venda.  

#### <a name="to-configure-kiosk-mode-for-a-samsung-knox-standard-device"></a>Para configurar o modo de quiosque para dispositivos Samsung KNOX Standard  

Na página **Definir Configurações de Modo de Quiosque para Dispositivos Samsung KNOX** do **Assistente de Criação de Item de Configuração**, especifique as seguintes informações:  

- **Selecionar aplicativo** ‑ Clique em **Procurar** para selecionar um aplicativo Android do Configuration Manager (com a extensão **.apk**) que poderá ser executado quando o dispositivo estiver no modo de quiosque. Nenhum outro aplicativo poderá ser executado no dispositivo.
- **Botões de volume** – habilita ou desabilita o uso dos botões de volume no dispositivo.
- **Botão de suspensão e ativação da tela** – Habilita ou desabilita o botão de ativação e suspensão da tela no dispositivo.|  

###  <a name="compliant-and-noncompliant-apps-android"></a>Aplicativos compatíveis e não compatíveis (Android)  
 Permite especificar uma lista de aplicativos Android que são compatíveis ou não compatíveis em sua empresa. Em seguida, você pode usar os relatórios para exibir os dispositivos que contêm aplicativos não compatíveis instalados e o usuário associado.  

 Não é possível especificar aplicativos compatíveis e não compatíveis no mesmo item de configuração.  

#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>Para especificar a lista de aplicativos compatíveis ou não compatíveis  

1.  Na página **Aplicativos Compatíveis e Não Compatíveis (Android)** , especifique as seguintes informações:  

    |Configuração|Mais informações|  
    |-------------|----------------------|  
    |**Lista de aplicativos não compatíveis**|Selecione esta opção se desejar especificar uma lista de aplicativos que serão relatados como não compatíveis se forem instalados pelos usuários.|  
    |**Lista de aplicativos compatíveis**|Selecione esta opção se desejar especificar uma lista de aplicativos que os usuários têm permissão para instalar. Todos os outros aplicativos instalados serão relatados como não compatíveis.|  
    |**Adicionar**|Adiciona um aplicativo à lista selecionada. Especifique um nome da sua preferência, opcionalmente o editor do aplicativo, e a URL para o aplicativo na loja de aplicativos.<br /><br /> Para especificar a URL, na [seção de aplicativos do Google Play](https://play.google.com/store/apps), procure o aplicativo que deseja usar.<br /><br /> Abra a página do aplicativo e copie a URL para a área de transferência. Agora você pode usar essa URL na lista de aplicativos compatíveis ou incompatíveis.<br /><br /> **Exemplo:** pesquise o **Microsoft Office Mobile**na Google Play. A URL usada será **https://play.google.com/store/apps/details?id=com.microsoft.office.officehub**.|  
    |**Editarar**|Permite editar o nome, o fornecedor e a URL do aplicativo selecionado.|  
    |**Removerr**|Exclui o aplicativo selecionado da lista.|  
    |**Importarar**|Importa uma lista dos aplicativos que você especificou em um arquivo de valores separados por vírgulas. Use o formato, nome do aplicativo, editor e a URL do aplicativo no arquivo.|  

2.  Quando tiver terminado, clique em **Avançar**. Os itens de configuração que contêm as configurações de aplicativo compatíveis e não compatíveis devem ser implantados em coleções de usuários.

 Você pode usar um dos seguintes relatórios para monitorar aplicativos compatíveis e não compatíveis:  

-   **Lista e dispositivos de aplicativos não compatíveis para um usuário especificado** – Exibe informações sobre usuários e dispositivos que têm aplicativos instalados que não são compatíveis com uma política especificada.  

-   **Resumo de usuários que têm aplicativos não compatíveis** – Exibe informações sobre usuários que têm aplicativos instalados que não são compatíveis com uma política especificada.  

 Para obter informações sobre como usar relatórios, consulte [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  
