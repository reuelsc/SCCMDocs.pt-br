---
title: Criar itens de configuração para dispositivos Android e Samsung KNOX Standard gerenciados com o Intune
titleSuffix: Configuration Manager
description: Use o item de configuração do Android e Samsung KNOX Standard no System Center Configuration Manager para gerenciar as configurações dos dispositivos.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7b66f3c4-e3bb-4f6a-abd5-55be649ff90d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fbfcc2189e2ce06e6348936caad6c68de51f5bdb
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-system-center-configuration-manager-client"></a>Como criar itens de configuração para dispositivos Android e Samsung KNOX gerenciados sem o cliente do System Center Configuration Manager

Use o item de configuração **Android e Samsung KNOX** do System Center Configuration Manager para gerenciar as configurações para os dispositivos Android e Samsung KNOX que estão registrados no Microsoft Intune ou são gerenciados localmente pelo Configuration Manager.  

#### <a name="to-create-an-android-and-samsung-knox-configuration-item"></a>Para criar um item de configuração do Android e Samsung KNOX  

1. No console do Configuration Manager, escolha **Ativos e Conformidade**.  

2. No espaço de trabalho **Ativos e Conformidade** , expanda **Configurações de Conformidade**e escolha em **Itens de Configuração**.  

3. Na guia **Início**, no grupo **Criar**, clique em **Criar Item de Configuração**.  

4. Na página **Geral** do Assistente para Criar Item de Configuração, especifique um nome e uma descrição opcional para o item de configuração.  

5. Em **Especificar o tipo de item de configuração que deseja criar**, escolha **Android e Samsung KNOX**.  

6. Escolha **Categorias** se você criar e atribuir categorias para ajudá-lo a pesquisar e filtrar os itens de configuração no console do Configuration Manager.  

7. Na página **Plataformas com Suporte** do assistente, escolha as plataformas específicas do Android ou Samsung KNOX que avaliarão o item de configuração.  

8. Na página **Configurações do Dispositivo** do assistente, escolha o grupo de configurações que você deseja configurar. Veja a [Referência de configurações do item de configuração para Android e Samsung KNOX](#BKMK_setref) neste tópico para obter detalhes e escolha **Avançar**.  

    > [!TIP]  
    >  Se a configuração desejada não estiver na lista, marque a caixa **Definir configurações adicionais que não estão nos grupos de configuração padrão**.  

9. Em cada página de configurações, defina as configurações necessárias. E mais, escolha se deseja corrigi-las quando não estiverem em conformidade nos dispositivos (quando houver suporte).  

10. Para cada grupo de configurações, você também pode configurar a severidade que será relatada quando um item de configuração for considerado em não conformidade:  

    - **Nenhum**. Os dispositivos que não cumprem essa regra de conformidade não relatam uma severidade de falha nos relatórios do Configuration Manager.  

    - **Informações**. Os dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha **Informações** nos relatórios do Configuration Manager.  

    - **Aviso**. Os dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha **Aviso** nos relatórios do Configuration Manager.  

    - **Crítico**. Os dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha **Crítico** nos relatórios do Configuration Manager.  

    - **Crítico com evento**. Os dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha **Crítico** nos relatórios do Configuration Manager. Esse nível de severidade também é registrado como um evento do Windows no log de eventos de aplicativos.  

11. Na página **Aplicabilidade da Plataforma** do assistente, examine as configurações incompatíveis com as plataformas com suporte selecionadas anteriormente. Você pode voltar e remover essas configurações ou pode continuar.  

    > [!TIP]  
    >  As configurações sem suporte não são avaliadas quanto à conformidade.  

12. Conclua o assistente.  

 Você pode exibir o novo item de configuração no nó **Itens de Configuração** do espaço de trabalho **Ativos e Conformidade** .  

## <a name="android-and-samsung-knox-configuration-item-settings-reference"></a>Referência de configurações do item de configuração para o Android e Samsung KNOX  

### <a name="password"></a>Senha  
Essas configurações se aplicam aos dispositivos Android e Samsung KNOX.  

|Configuração|Detalhes|  
|-------------|-------------|  
|**Exigir configurações de senha em dispositivos**|Requer uma senha nos dispositivos com suporte.|  
|**Comprimento mínimo da senha (caracteres)**|Especifica o comprimento mínimo da senha.|  
|**Validade da senha em dias**|Especifica o número de dias antes de uma senha precisar ser alterada.|  
|**Número de senhas lembradas**|Impede a reutilização de senhas usadas anteriormente.|  
|**Número de tentativas de logon com falha antes de o dispositivo ser apagado**|Apaga o dispositivo se houver falha neste número de tentativas de logon.|  
|**Tempo ocioso antes que o dispositivo móvel seja bloqueado**|Especifica o período até que o dispositivo seja bloqueado se não estiver sendo usado.|
|**Qualidade da senha**|Especifica o nível necessário de complexidade da senha e também se os dispositivos biométricos podem ser usados.|  
|**Permitir Smart Lock e outros agentes de confiança**|Permite controlar o recurso Smart Lock em dispositivos Android compatíveis. Essa capacidade do telefone permite desabilitar ou ignorar a senha da tela de bloqueio do dispositivo, caso o dispositivo esteja em um local confiável, como quando ele está conectado a um dispositivo Bluetooth específico ou quando está perto de uma marcação NFC. É possível usar essa configuração para impedir que os usuários configurem o Smart Lock.|
|**Impressão digital de desbloqueio (KNOX 5.0+)**|Permite usar uma impressão digital para desbloquear os dispositivos compatíveis.|

### <a name="device"></a>Dispositivo   

|Configuração|Detalhes|  
|------------------|-------------|  
|**Discagem de voz**|Habilita ou desabilita o recurso de discagem de voz no dispositivo.|
|**Assistente de voz**|Permite o uso do software Assistente de voz no dispositivo.|
|**Captura de tela**|Permite ao usuário capturar o conteúdo da tela como uma imagem.|
|**Envio de dados de diagnóstico**|Permite que o dispositivo envie informações de diagnóstico ao Google.|
|**Localização geográfica**|Permite que o dispositivo use informações de localização.|
|**Copiar e colar**|Permite as funções de copiar e colar no dispositivo.|
|**Redefinição de fábrica**|Permite que o usuário execute uma redefinição de fábrica no dispositivo.|  |
|**Permitir compartilhamento de área de transferência entre aplicativos**|Permite que o usuário use a área de transferência para copiar e colar entre os aplicativos.|  |
|**Bluetooth**|Permite o uso de Bluetooth no dispositivo.|

### <a name="store"></a>Repositório

|Configuração|Detalhes|  
|------------------|-------------|  
|**Armazenamento de aplicativos**|Permite que o usuário acesse o armazenamento do Google Play no dispositivo.|

### <a name="browser"></a>Navegador

|Configuração|Detalhes|  
|------------------|-------------|  
|**Permitir navegador da Web**|Permite que o navegador da Web padrão do dispositivo seja usado.|
|**Preenchimento automático**|Permite o uso da função de preenchimento automático do navegador da Web.|
|**Script ativo**|Permite que o navegador da Web do dispositivo use o script ativo.|
|**Bloqueador de pop-up**|Permite o uso de um bloqueador de pop-up no navegador da Web.|
|**Cookies**|Permite que o navegador da Web do dispositivo use cookies.|

### <a name="cloud"></a>Nuvem  

|Configuração|Detalhes|  
|-------------|-------------|  
|**Backup do Google**|Permite o uso de backup do Google.|  
|**Sincronização automática da conta do Google**|Permite que as configurações de conta do Google sejam sincronizadas automaticamente.|  

### <a name="security"></a>Segurança  

|Configuração|Detalhes|  
|-------------|-------------|  
|**Mensagens SMS e MMS**|Permite o uso de mensagens SMS e MMS no dispositivo.|
|**Armazenamento removível**|Permite que o dispositivo use o armazenamento removível, como um cartão SD.|
|**Câmera**|Permite o uso da câmera do dispositivo.<br /><br /> Aplica-se a dispositivos Android e Samsung KNOX.|
|**Comunicação a curta distância (NFC)**|Permite operações que usam comunicação de curta distância, caso o dispositivo ofereça suporte.|
|**YouTube**|Permite o uso do aplicativo YouTube no dispositivo.<br /><br /> Aplica-se somente a dispositivos Samsung KNOX.|  
|**Desligar**|Permite que o dispositivo seja desligado.<br /><br /> Aplica-se somente a dispositivos Samsung KNOX.|  

### <a name="roaming"></a>Roaming

|Configuração|Detalhes|  
|-------------|-------------|  
|Roaming de voz|Permite o roaming de voz quando o dispositivo estiver em uma rede de celular.|
|Roaming de dados|Permite o roaming de dados quando o dispositivo estiver em uma rede de celular.|


### <a name="encryption"></a>Criptografia  
 Essas configurações se aplicam aos dispositivos Android e Samsung KNOX.  

|Configuração|Detalhes|  
|-------------|-------------|  
|**Criptografia de cartão de memória**|Exige que o cartão de armazenamento do dispositivo seja criptografado.|
|**Criptografia de arquivo no dispositivo**|Requer que os arquivos no dispositivo móvel sejam criptografados.|  

### <a name="wireless-communications"></a>Comunicações sem fio

|Configuração|Detalhes|  
|-------------|-------------|  
|**Conexão de rede sem fio**|Permite o uso dos recursos de Wi-Fi do dispositivo.|
|**Compartilhamento da Internet por Wi-Fi**|Permite o uso de compartilhamento de Internet por Wi-Fi no dispositivo.|


### <a name="compliant-and-noncompliant-apps-android"></a>Aplicativos compatíveis e não compatíveis (Android)  
É possível especificar uma lista de aplicativos Android que não estão em conformidade ou não em sua empresa. Então, você pode usar relatórios para exibir os dispositivos que contêm aplicativos em não conformidade instalados e o usuário associado.  

Não é possível especificar aplicativos compatíveis e não compatíveis no mesmo item de configuração.  

#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>Para especificar a lista de aplicativos compatíveis ou não compatíveis  

Na página **Aplicativos Compatíveis e Não Compatíveis (Android)** , especifique as seguintes informações:  

|Configuração|Mais informações|  
|-------------|----------------------|  
|**Lista de aplicativos não compatíveis**|Especifica uma lista de aplicativos que serão relatados como em não conformidade se forem instalados pelos usuários.|  
|**Lista de aplicativos compatíveis**|Especifica uma lista de aplicativos que os usuários têm permissão de instalar. Todos os outros aplicativos instalados serão relatados como não compatíveis.|  
|**Adicionar**|Adiciona um aplicativo à lista selecionada. Especifique um nome da sua preferência, opcionalmente o editor do aplicativo, e a URL para o aplicativo na loja de aplicativos.<br /><br /> Para especificar a URL, na [seção de aplicativos do Google Play](https://play.google.com/store/apps), procure o aplicativo que deseja usar.<br /><br /> Abra a página do aplicativo e copie a URL para a área de transferência. Agora você pode usar essa URL na lista de aplicativos compatíveis ou incompatíveis.<br /><br /> **Exemplo:** pesquise o **Microsoft Office Mobile**na Google Play. A URL usada será **https://play.google.com/store/apps/details?id=com.microsoft.office.officehub**.|  
|**Editarar**|Permite editar o nome, editor e URL do aplicativo selecionado.|  
|**Removerr**|Exclui o aplicativo selecionado da lista.|  
|**Importarar**|Importa uma lista dos aplicativos que você especificou em um arquivo de valores separados por vírgulas. Use o formato, nome do aplicativo, editor e URL do aplicativo no arquivo.|  

## <a name="android-for-work-configuration-items"></a>Itens de configuração do Android for Work
O Android for Work tem dois grupos de configuração para itens de configuração:

- **Senha**. Idêntica às configurações para o Android "clássico".

- **Perfil de Trabalho**. Habilita as seguintes configurações do Android for Work:
  - **Permitir o compartilhamento de dados entre perfis pessoais e de trabalho**
  - **Ocultar notificações de perfil de trabalho quando o dispositivo é bloqueado** (Android 6.0+)
  - **Configurar a política de permissão de aplicativo padrão** (Android 6.0+)

Para criar um item de configuração no perfil de trabalho do Android, escolha **Android for Work** na página **Geral** e defina as configurações de cada um dos grupos de configuração. Adicione o item de configuração a uma linha de base e implante como de costume. Essas configurações serão aplicadas somente nos dispositivos registrados como Android for Work, e não nos registrados como Android.

### <a name="kiosk-mode-samsung-knox-only"></a>Modo de quiosque (apenas Samsung KNOX)  
É possível usar o modo de quiosque para bloquear um dispositivo para permitir que somente alguns recursos funcionem. Por exemplo, você pode permitir que um dispositivo execute apenas um aplicativo gerenciado especificado ou desabilitar os botões de volume em um dispositivo. Essas configurações podem ser usadas para um modelo de demonstração de um dispositivo. Ou podem ser usadas para um dispositivo que é dedicado a apenas uma função, como um dispositivo de ponto de venda.  

#### <a name="to-configure-kiosk-mode-for-a-samsung-knox-device"></a>Para configurar o modo de quiosque para dispositivos Samsung KNOX  

1. Na página **Definir Configurações do Modo de Quiosque para Dispositivos Samsung KNOX** do Assistente para Criar o Item de Configuração, especifique as seguintes informações:  

   |Configuração|Mais informações|  
   |-------------|----------------------|  
   |**Selecionar aplicativo**|Escolha em **Procurar** para selecionar um aplicativo Android do Configuration Manager (com a extensão **.apk**) que poderá ser executado quando o dispositivo estiver no modo de quiosque. Nenhum outro aplicativo poderá ser executado no dispositivo.|  
   |**Botões de volume**|Habilita ou desabilita o uso dos botões de volume no dispositivo.|  
   |**Suspensão e botão de ativação da tela**|Habilita ou desabilita o botão de ativação e suspensão da tela no dispositivo.|  

2. Quando tiver terminado, escolha **Avançar**.  

## <a name="reports-for-monitoring"></a>Relatórios para monitoramento
Você pode usar um dos seguintes relatórios para monitorar aplicativos com e sem conformidade:  

- **Lista de Aplicativos e Dispositivos sem conformidade para um usuário específico**. Mostra informações sobre os usuários e dispositivos que têm aplicativos instalados e não estão em conformidade com uma política especificada.  

- **Resumo dos Usuários com Aplicativos em Não Conformidade**. Mostra informações sobre os usuários que têm aplicativos instalados que não estão em conformidade com uma política especificada.  

Para obter informações sobre como usar relatórios, consulte [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  

## <a name="see-also"></a>Consulte também  
[Itens de configuração de dispositivos gerenciados sem o cliente do System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)
