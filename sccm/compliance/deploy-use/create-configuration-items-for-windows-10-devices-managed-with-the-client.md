---
title: 'Criar itens de configuração para Windows 10 gerenciados pelo cliente '
titleSuffix: Configuration Manager
description: Use o item de configuração do System Center Configuration Manager no Windows 10 para gerenciar configurações para computadores Windows 10 que são gerenciados pelo cliente do Configuration Manager.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 14226fbe-dd07-4432-910b-130790624a4e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9cfb8209343581f8d6b9dc7949032d6399669f95
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68339150"
---
# <a name="create-configuration-items-for-windows-10-devices"></a>Criar itens de configuração para dispositivos Windows 10
Use o item de configuração do System Center Configuration Manager no **Windows 10** para gerenciar configurações para computadores Windows 10 que são gerenciados pelo cliente do Configuration Manager.  
  
> [!IMPORTANT]  
>  Nesta versão, se você criou uma configuração de **senha** como parte de um item de configuração do tipo **Windows 10** (para um dispositivo gerenciado com o cliente do Configuration Manager), esteja ciente do problema a seguir. Se a configuração ainda não existir ou não tiver sido configurada no dispositivo Windows 10, ela será avaliada incorretamente como em conformidade.  
>   
>  Como alternativa, quando você criar uma configuração para esses dispositivos, verifique se a opção **Corrigir configurações não compatíveis** está marcada nas páginas de configurações do assistente para Criar Item de Configuração. Além disso, ao implantar uma linha de base de configuração que contém um item de configuração do Windows 10 que, por sua vez, contém configurações de senha, selecione **Corrigir regras não compatíveis quando houver suporte para elas**. Você faz essa seleção na caixa de diálogo implantar linhas de base de configuração. Usando essa solução alternativa, a configuração é monitorada e corrigida se for considerada não compatível. Após a correção, a configuração é relatada corretamente como **Compatível** (a menos que um problema seja encontrado; nesse caso, ele relatará **Erro**).  
  
### <a name="to-create-a-windows-10-configuration-item"></a>Para criar um item de configuração do Windows 10  
  
1. No console do Configuration Manager, selecione **Ativos e Conformidade**.  
  
2. No espaço de trabalho **Ativos e Conformidade**, expanda **Configurações de Conformidade** e selecione **Itens de Configuração**.  
  
3. Na guia **Início**, no grupo **Criar**, selecione **Criar Item de Configuração**.  
  
4. Na página **Geral** do assistente para **Criar Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.  
  
5. Em **Especificar o tipo de item de configuração que deseja criar**, selecione **Windows 10**.  
  
6. Se você quiser criar e atribuir categorias para ajudar a pesquisar e filtrar itens de configuração no console do Configuration Manager, selecione **Categorias**.  
  
7. Na página **Plataformas com Suporte** do assistente, selecione as plataformas específicas do Windows 10 que avaliarão o item de configuração.  
  
8. Na página **Configurações do Dispositivo** do assistente, selecione o grupo de configurações que deseja configurar. (Para obter detalhes, consulte [referência de configurações do item de configuração do Windows 10](#BKMK_Ref) neste artigo.) Em seguida, selecione **Avançar**.  
  
   > [!TIP]  
   >  Se a configuração desejada não estiver na lista, marque a caixa de seleção **Definir configurações adicionais que não estão nos grupos de configuração padrão**.  
  
9. Em cada página de configurações, defina as configurações necessárias e se deseja corrigi-las quando não estiverem em conformidade nos dispositivos (quando houver suporte).  
  
10. Para cada grupo de configurações, você também pode configurar a gravidade relatada quando um item de configuração for considerado não compatível:  
  
    -   **Nenhum**: dispositivos que não cumprem essa regra de conformidade não relatam uma gravidade de falha em relatórios do Configuration Manager.  
  
    -   **Informações**: dispositivos que não cumprem essa regra de conformidade relatam a gravidade de falha **Informações** em relatórios do Configuration Manager.  
  
    -   **Aviso**: dispositivos que não cumprem essa regra de conformidade relatam a gravidade de falha **Aviso** em relatórios do Configuration Manager.  
  
    -   **Crítico**: dispositivos que não cumprem essa regra de conformidade relatam a gravidade de falha **Crítico** em relatórios do Configuration Manager.  
  
    -   **Crítico com evento**: dispositivos que não cumprem essa regra de conformidade relatam a gravidade de falha **Crítico** em relatórios do Configuration Manager. Esse nível de severidade também é registrado como um evento do Windows no log de eventos de aplicativos.  
  
11. Na página **Aplicabilidade da Plataforma** do assistente, reveja as configurações que não são compatíveis com as plataformas com suporte selecionadas anteriormente. Você pode voltar e remover essas configurações ou pode continuar.  
  
    > [!TIP]  
    >  As configurações sem suporte não são avaliadas quanto à conformidade.  
  
12. Conclua o assistente.  
  
    Você pode exibir o novo item de configuração no nó **Itens de Configuração** do workspace **Ativos e Conformidade**.  
  
## <a name="BKMK_Ref"></a> Windows 10 configuration item settings reference  
  
### <a name="password"></a>Senha  
  
|Configuração|Detalhes|  
|-------------|-------------|  
|**Exigir configurações de senha em dispositivos**|Requer uma senha nos dispositivos com suporte.|  
|**Comprimento mínimo da senha (caracteres)**|O comprimento mínimo de caracteres para a senha.|  
|**Validade da senha em dias**|O número de dias antes que a senha precise ser alterada.|  
|**Número de senhas lembradas**|Impede a reutilização de senhas anteriores.|  
|**Número de tentativas de logon com falha antes do apagamento do dispositivo**|Limpa o dispositivo se o logon falhar por este número de vezes.|  
|**Tempo ocioso antes que o dispositivo móvel seja bloqueado**|Especifica por quantos minutos o dispositivo deve ficar inativo antes de ser bloqueado automaticamente.|  
|**Complexidade da senha**|Escolha se é possível especificar um PIN como “1234” ou se é necessário fornecer uma senha forte.|
|**Número de conjuntos de caracteres complexos exigidos na senha**|Se você tiver selecionado uma senha **forte**, use essa configuração para configurar o número de conjuntos de caracteres complexos necessários. Para uma senha forte, essa configuração deve ser definida com pelo menos **3**, o que significa que letras e números são obrigatórios. Selecione **4** se quiser aplicar uma senha que requer ainda caracteres especiais como **(% $** .<br>(somente Windows 10)  |
  
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
|**Roaming de dados**|Permita o roaming entre redes ao acessar dados.|  
  
### <a name="encryption"></a>Criptografia  
  
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Criptografia de arquivo no dispositivo**|Exige que os arquivos no dispositivo sejam criptografados.|  
  
### <a name="system-security"></a>Segurança do sistema  
  
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Controle de conta de usuário**|Define como o Controle de Conta de Usuário do Windows funciona no dispositivo.<br />Por exemplo, você pode desabilitá-lo ou definir o nível no qual ele o notificará.|  
|**Firewall da rede**|Habilita ou desabilita o Firewall do Windows.|  
|**SmartScreen**|Habilita ou desabilita o Windows SmartScreen.|  
|**Proteção contra vírus**|Exige que o software antivírus seja instalado e configurado.|  
|**As assinaturas de proteção contra vírus estão atualizadas**|Exige que os arquivos de assinatura do software antivírus no dispositivo sejam atualizados.|  
  
### <a name="windows-information-protection"></a>Windows Information Protection

Com o aumento do uso de dispositivos de funcionário dentro da empresa, aumenta também o risco de vazamentos acidentais de dados por meio de aplicativos e serviços, como email, mídia social e nuvem pública. Eles estão fora do controle da organização. Os exemplos incluem quando um funcionário:

- Envia as imagens de engenharia mais recentes de sua conta de email pessoal.
- Copia e cola informações do produto em um tweet.
- Salva um relatório de vendas em andamento em seu armazenamento em nuvem pública.

A WIP (Proteção de Informações do Windows, anteriormente conhecida como proteção de dados empresariais) ajuda a proteger contra esse possível vazamentos de dados sem interferir na experiência do funcionário. A WIP também ajuda a proteger dados e aplicativos corporativos contra vazamentos de dados acidentais em dispositivos corporativos e dispositivos pessoais que os funcionários levam para o trabalho. O WIP não requer alterações no seu ambiente ou em outros aplicativos.

Configuration Manager itens de configuração da proteção de informações do Windows, gerencie o seguinte:

- A lista de aplicativos protegidos por WIP
- Locais de rede corporativa
- Nível de proteção
- Configurações de criptografia
  

Para saber mais sobre como configurar a WIP com o Configuration Manager, confira [Proteger os dados da empresa usando a WIP (Proteção de Informações do Windows)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip).
  
## <a name="see-also"></a>Consulte também  
[Itens de configuração de dispositivos gerenciados com o cliente do System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items.md)
