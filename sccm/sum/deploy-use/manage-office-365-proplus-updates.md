---
title: Gerenciar atualizações do Office 365 ProPlus
titleSuffix: Configuration Manager
description: O Configuration Manager sincroniza a atualização de clientes do Office 365 do catálogo do WSUS para o servidor do site para disponibilizar as atualizações para implantar em clientes.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.openlocfilehash: f49757235aab1bb919b6bd6012fba2e9adfc1a24
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384796"
---
# <a name="manage-office-365-proplus-with-configuration-manager"></a>Gerenciar o Office 365 ProPlus com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Configuration Manager permite gerenciar aplicativos do Office 365 ProPlus das seguintes maneiras:

- [Painel de gerenciamento de clientes do Office 365](#office-365-client-management-dashboard): examine as informações de clientes do Office 365 no painel de gerenciamento de clientes do Office 365. A partir do Configuration Manager versão 1802, o painel de gerenciamento de clientes do Office 365 exibe uma lista de dispositivos relevantes quando seções de gráfico são selecionadas. <!--1357281 -->

- [Implantar aplicativos do Office 365](#deploy-office-365-apps): você pode iniciar o instalador do Office 365 no painel de gerenciamento de clientes do Office 365 para facilitar a experiência de instalação inicial do aplicativo do Office 365. O assistente permite que você defina as configurações de instalação do Office 365, baixe arquivos das redes de distribuição de conteúdo (CDNs) do Office, e crie e implante um aplicativo de script com o conteúdo.    

- [Implantar atualizações do Office 365](#deploy-office-365-updates): você pode gerenciar as atualizações de cliente do Office 365 usando o fluxo de trabalho do gerenciamento de atualização de software. Quando a Microsoft publica uma nova atualização de cliente do Office 365 na Rede de Distribuição de Conteúdo do Office (CDN), a Microsoft também publica um pacote de atualização para o Windows Server Update Services (WSUS). Após o Configuration Manager sincronizar a atualização de clientes do Office 365 do catálogo do WSUS para o servidor do site, a atualização ficará disponível para implantar em clientes.    

- [Adicionar idiomas para downloads de atualizações do Office 365](#add-languages-for-office-365-update-downloads): você pode adicionar suporte para o Configuration Manager para baixar atualizações em qualquer idioma compatível com o Office 365. Isso significa que o Configuration Manager não precisa dar suporte ao idioma, contanto que o Office 365 dê esse suporte. Antes do Configuration Manager versão 1610, você deve baixar e implantar as atualizações nos mesmos idiomas configurados nos clientes do Office 365. 

- [Alterar o canal de atualização](#change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager): use a política de grupo para distribuir uma alteração de valor da chave do registro para os clientes do Office 365 para alterar o canal de atualização.


## <a name="office-365-client-management-dashboard"></a>Painel de Gerenciamento de Clientes do Office 365  
O painel de Gerenciamento de Clientes do Office 365 fornece gráficos com as seguintes informações:

- Número de clientes do Office 365
- Versões do cliente do Office 365
- Idiomas do cliente do Office 365
- Canais do cliente do Office 365     
  Para mais informações, confira [Visão geral dos canais de atualização do Office 365 ProPlus](/DeployOffice/overview-of-update-channels-for-office-365-proplus).

Para exibir o painel de Gerenciamento de Clientes do Office 365, no console do Configuration Manager, vá até **Biblioteca de Software** > **Visão Geral** > **Gerenciamento de Clientes do Office 365**. Na parte superior do painel, use a configuração suspensa **Coleção** para filtrar os dados do painel por membros de uma coleção específica. A partir do Configuration Manager versão 1802, o painel de gerenciamento de clientes do Office 365 exibe uma lista de dispositivos relevantes quando seções de gráfico são selecionadas.

### <a name="display-data-in-the-office-365-client-management-dashboard"></a>Dados de exibição no painel de Gerenciamento de Clientes do Office 365
Os dados que são exibidos no painel de Gerenciamento de Clientes do Office 365 vêm de inventário de hardware. Habilite o inventário de hardware e selecione a classe de inventário de hardware **Configurações do Office 365 ProPlus** para que os dados sejam exibidos no painel. 
#### <a name="to-display-data-in-the-office-365-client-management-dashboard"></a>Como exibir dados no painel de Gerenciamento de Clientes do Office 365
1. Habilite inventário de hardware se ele ainda não estiver habilitado. Para mais detalhes, consulte [Configurar inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).
2. No console do Configuration Manager, acesse **Administração** > **Configurações do Cliente** > **Configurações do Cliente Padrão**.  
3. Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  
4. No **configurações do cliente padrão** caixa de diálogo, clique em **inventário de Hardware**.  
5. No **configurações do dispositivo** clique em **Definir Classes**.  
6. Na caixa de diálogo **Classes de Inventário de Hardware**, selecione **Configurações do Office 365 ProPlus**.  
7.  Clique em **OK** para salvar suas alterações e fechar o **Classes de inventário de Hardware** caixa de diálogo. <br/>O painel de Gerenciamento de Clientes do Office 365 começará a exibir dados à medida que o inventário de hardware for relatado.

## <a name="deploy-office-365-apps"></a>Implantar aplicativos do Office 365  
Inicie o instalador do Office 365 no painel de gerenciamento de clientes do Office 365 para a instalação inicial de aplicativos do Office 365. O assistente permite que você defina as configurações de instalação do Office 365, baixe arquivos das redes de distribuição de conteúdo (CDNs) do Office, e crie e implante um aplicativo de script para os arquivos. Até que o Office 365 seja instalado nos clientes e a [tarefa de atualizações automáticas do Office](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus) seja executada, as atualizações do Office 365 não se aplicam. Para fins de teste, você pode executar a tarefa de atualização manualmente.

Para versões anteriores do Configuration Manager, execute as seguintes etapas para instalar os aplicativos do Office 365 pela primeira vez em clientes:
- Baixar a Ferramenta de Implantação do Office 365 (ODT)
- Baixe os arquivos de origem de instalação do Office 365, incluindo todos os pacotes de idiomas de que você precisa.
- Gere o Configuration.xml que especifica a versão e o canal corretos do Office.
- Crie e implante um pacote herdado ou um aplicativo de script para os clientes para instalar os aplicativos do Office 365.

### <a name="requirements"></a>requisitos
- O computador que executa o Instalador do Office 365 deve ter acesso à Internet.  
- O usuário que executa o Instalador do Office 365 deve ter acesso de **leitura** e **gravação** ao compartilhamento de local de conteúdo que é fornecido no assistente.
- Se você receber um erro 404 download, copie os seguintes arquivos para a pasta %temp% do usuário:
  - [releasehistory.xml](http://officecdn.microsoft.com/pr/wsus/releasehistory.cab)
  - [o365client_32bit.xml](http://officecdn.microsoft.com/pr/wsus/ofl.cab)  

### <a name="deploy-office-365-apps-using-configuration-manager-version-1806-or-higher"></a>Implante aplicativos do Office 365 usando o Configuration Manager versão 1806 ou superior: 
Começando no Configuration Manager 1806, a Ferramenta de Personalização do Office é integrada ao instalador do Office 365 no console do Configuration Manager. Ao criar uma implantação do Office 365, agora você pode definir dinamicamente as configurações de capacidade de gerenciamento mais recentes do Office. <!--1358149-->

1. No console do Configuration Manager, navegue até **Biblioteca de Software** > **Visão Geral** > **Gerenciamento de Cliente do Office 365**.
2. Clique em **Office 365 Installer (Instalador do Office 365)** no painel superior direito. O Assistente de Instalação de Cliente do Office 365 é aberto.
3. Na página **Configurações de Aplicativo**, forneça um nome e uma descrição para o aplicativo, insira o local de download para os arquivos e clique em **Avançar**. O local deve ser especificado como &#92;&#92;*servidor*&#92;*compartilhar*.
4. Na página **Configurações do Office**, clique em **Acessar a Ferramenta de Personalização do Office**. Isso abrirá ao [Ferramenta de Personalização do Office para Clique para Executar](https://config.office.com).
5. Defina as configurações desejadas para a instalação do Office 365. Clique o **Enviar** no canto superior direito da página quando você concluir a configuração. 
6. Na página **Implantação**, determine se você deseja implantar agora ou mais tarde. Se optar por implantar mais tarde, você poderá encontrar o aplicativo na **Biblioteca de Software** < **Gerenciamento de Aplicativos** < **Aplicativos**.  
7. Confirme as configurações na página **Resumo**. 
8. Clique em **Avançar** e, em seguida, clique em **Fechar** após a conclusão do Assistente para Instalação de Cliente do Office 365. 

### <a name="deploy-office-365-apps-using-configuration-manager-version-1802-and-prior"></a>Implante aplicativos do Office 365 usando o Configuration Manager versão 1802 e versões anteriores:

1. No console do Configuration Manager, navegue até **Biblioteca de Software** > **Visão Geral** > **Gerenciamento de Cliente do Office 365**.
2. Clique em **Office 365 Installer (Instalador do Office 365)** no painel superior direito. O Assistente de Instalação de Cliente do Office 365 é aberto.
3. Na página **Configurações de Aplicativo**, forneça um nome e uma descrição para o aplicativo, insira o local de download para os arquivos e clique em **Avançar**. O local deve ser especificado como &#92;&#92;*servidor*&#92;*compartilhar*.
4. Na página **Importar Configurações de Cliente**, escolha se deseja importar as configurações de cliente do Office 365 de um arquivo de configuração XML existente ou especificar as configurações manualmente. Clique em **Avançar** quando terminar.  

    Quando você tiver um arquivo de configuração existente, insira o local do arquivo e vá para a etapa 7. Você deve especificar o local no formulário &#92;&#92;*server*&#92;*share*&#92;*filename*.XML.
    > [!IMPORTANT]    
    > O arquivo de configuração XML deve conter apenas [idiomas com suporte pelo cliente do Office 365 ProPlus](https://docs.microsoft.com/deployoffice/office2016/language-identifiers-and-optionstate-id-values-in-office-2016).

5. Na página **Produtos do Cliente**, selecione o pacote do Office 365 utilizado. Selecione os aplicativos que você deseja incluir. Selecione produtos do Office adicionais que devem ser incluídos e, em seguida, clique em **Avançar**.
6. Na página **Configurações do Cliente**, escolha as configurações a serem incluídas e clique em **Avançar**.
7. Na página **Implantação**, escolha se deseja implantar o aplicativo e clique em **Avançar**. <br/>Se você optar por não implantar o pacote no assistente, vá para a etapa 9.
8. Configure o restante das páginas do assistente como você faria para uma implantação de aplicativo típica. Para obter detalhes, consulte [Create and deploy an application (Criar e implantar um aplicativo)](/sccm/apps/get-started/create-and-deploy-an-application).
9. Conclua o assistente.
10. Você pode implantar ou editar o aplicativo em **Biblioteca de Softwares** > **Visão Geral** > **Gerenciamento de Aplicativos** > **Aplicativos**.    

Depois que você criar e implantar os aplicativos do Office 365 usando o Instalador do Office 365, o Configuration Manager não gerenciará as atualizações do Office por padrão. Para permitir que os clientes do Office 365 recebam atualizações do Configuration Manager, veja [Implantar atualizações do Office 365 com o Configuration Manager](#deploy-office-365-updates-with-configuration-manager).

Depois de implantar aplicativos do Office 365, você pode criar regras de implantação automática para manter os aplicativos. Para criar uma regra de implantação automática para aplicativos do Office 365, clique em **Criar uma ADR** no painel de Gerenciamento de Clientes do Office 365. Selecione **Cliente do Office 365** quando escolher o produto. Para mais informações, confira [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates) (Implantar atualizações de software automaticamente).


## <a name="deploy-office-365-updates"></a>Implantar atualizações do Office 365
Há uma [tarefa de Atualizações Automáticas no Office 365](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus) agendada que é executada várias vezes por semana. Se você instalou o Office 365 recentemente, talvez o canal de atualização ainda não esteja definido e uma verificação de atualização não localizará as atualizações aplicáveis a ele. Para fins de teste, você pode iniciar manualmente a tarefa de atualização. 

Use as etapas a seguir para implantar atualizações do Office 365 com o Configuration Manager:

1.  [Verifique os requisitos](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#requirements-for-using-configuration-manager-to-manage-office-365-client-updates) para usar o Configuration Manager para gerenciar atualizações de clientes do Office 365 na seção **Requisitos para usar o Configuration Manager para gerenciar atualizações de clientes do Office 365** do artigo.  

2.  [Configure os pontos de atualização de software](../get-started/configure-classifications-and-products.md) para sincronizar as atualizações de clientes do Office 365. Defina as **atualizações** para a classificação e selecione o **cliente do Office 365**. Sincronize as atualizações de software depois de configurar os pontos de atualização de software para usar a classificação **Atualizações**.
3.  Permita que os clientes do Office 365 recebam atualizações do Configuration Manager. Use as configurações do cliente do Configuration Manager ou a política de grupo para habilitar o cliente.   

    **Método 1**: a partir do Configuration Manager versão 1606, é possível usar a configuração do cliente do Configuration Manager para gerenciar o agente cliente do Office 365. Depois de definir essa configuração e implantar as atualizações do Office 365, o agente cliente do Configuration Manager se comunica com o agente cliente do Office 365 para baixar as atualizações de um ponto de distribuição e instalá-las. O Configuration Manager faz um inventário das configurações de cliente do Office 365 ProPlus.    

      1.  No console do Configuration Manager, escolha **Administração** > **Visão Geral** > **Configurações do Cliente**.  

      2.  Abra as configurações do dispositivo apropriado para habilitar o agente cliente. Para obter mais informações sobre configurações do cliente padrão e personalizadas, consulte [Como definir as configurações do cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

      3.  Clique em **Atualizações de Software** e selecione **Sim** para a configuração **Habilitar o gerenciamento do Agente Cliente do Office 365**.  

    **Método 2**: [Permitir que os clientes do Office 365 recebam atualizações](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#BKMK_EnableClient) do Configuration Manager usando a Ferramenta de Implantação do Office ou a Política de Grupo.  

4. [Implante as atualizações do Office 365](deploy-software-updates.md) nos clientes.   

> [!Important]
> - A partir do Configuration Manager versão 1706, as atualizações de cliente do Office 365 foram movidas para o nó **Gerenciamento de Clientes do Office 365** >**Atualizações do Office 365**. Essa movimentação não afetará a configuração de ADR. 
> - Antes do Configuration Manager versão 1610, você deve baixar e implantar as atualizações nos mesmos idiomas configurados nos clientes do Office 365. Por exemplo, digamos que você tenha um cliente do Office 365 configurado com os idiomas en-us e de-de. No servidor do site, você baixa e implanta apenas conteúdo de en-us para uma atualização correspondente do Office 365. Quando o usuário inicia a instalação desta atualização por meio do Centro de Software, a atualização trava durante o download do conteúdo para de-de.   


## <a name="restart-behavior-and-client-notifications-for-office-365-updates"></a>Comportamento de reinicialização e notificações do cliente para atualizações do Office 365
Quando você implanta uma atualização em um cliente do Office 365, o comportamento de reinicialização e as notificações de cliente são diferentes, dependendo da versão do Configuration Manager. A tabela a seguir fornece informações sobre a experiência do usuário final quando o cliente recebe uma atualização do Office 365:

|Versão do Configuration Manager |Experiência do usuário final|  
|----------------|---------------------|
|Antes do 1610|Um sinalizador de reinicialização é definido e a atualização é instalada após a reinicialização do computador.|
|1610|Aplicativos do Office 365 são desligados sem aviso antes da instalação da atualização|
|1610 com a atualização <br/>1702|Um sinalizador de reinicialização é definido e a atualização é instalada após a reinicialização do computador.|
|1706|O cliente recebe notificações pop-up e no aplicativo, bem como uma caixa de diálogo de contagem regressiva, antes da instalação da atualização.|
|1802| O cliente recebe notificações pop-up e no aplicativo, bem como uma caixa de diálogo de contagem regressiva, antes da instalação da atualização. </br>Se um aplicativo do Office 365 estiver sendo executado durante uma imposição de atualização de clientes do Office 365, os aplicativos do Office não serão forçados a fechar. Em vez disso, a instalação da atualização retornará exigindo uma reinicialização do sistema <!--510006-->|


> [!Important]
>
>No Configuration Manager versão 1706, observe os seguintes detalhes:
>
>- Um ícone de notificação é exibido na área de notificação na barra de tarefas para os aplicativos necessários para os quais o prazo é de 48 horas e o conteúdo da atualização já foi baixado. 
>- Uma caixa de diálogo de contagem regressiva é exibida para os aplicativos necessários para os quais o prazo é de 7,5 horas e a atualização já foi baixada. O usuário pode adiar a caixa de diálogo de contagem regressiva até três vezes antes do prazo. Quando for adiada, a contagem regressiva será exibida novamente depois de duas horas. Se não for adiada, haverá uma contagem regressiva de 30 minutos e a atualização será instalada quando a contagem regressiva expirar.
>- Uma notificação pop-up pode não ser exibida até que o usuário clique no ícone na área de notificação. Além disso, se a área de notificação tiver um espaço mínimo, o ícone de notificação poderá não ficar visível, a menos que o usuário abra ou expanda a área de notificação. 
>- A notificação e a caixa de diálogo de contagem regressiva podem ser iniciadas enquanto o usuário não está trabalhando ativamente no dispositivo. Por exemplo, quando o dispositivo está bloqueado durante a noite, é possível que os aplicativos do Office em execução no dispositivo sejam forçados a fechar para instalar a atualização. Antes de fechar o aplicativo, o Office salva os dados de aplicativo para evitar a perda de dados. 
>- Se o prazo já tiver passado ou estiver configurado para iniciar assim que possível, os aplicativos do Office executados poderão ser forçados a fechar sem notificações. 
>- Se o usuário instalar uma atualização do Office antes do prazo, o Configuration Manager verificará se a atualização está instalada quando o prazo for atingido. Se a atualização não for detectada no dispositivo, a atualização está instalada. 
>- A barra de notificação no aplicativo não será exibida em aplicativos do Office que estiverem em execução antes que a atualização seja baixada. A notificação no aplicativo será exibida apenas para aplicativos que forem abertos depois que a atualização for baixada.
>- Para atualizações do Office disparadas por um período de serviço ou agendados para o horário não comercial, é possível que os aplicativos do Office em execução sejam forçados a fechar sem notificações para que a atualização seja instalada. 
>- Para obter mais informações, confira [Notificações de atualização do usuário final para o Office 365](https://docs.microsoft.com/deployoffice/end-user-update-notifications-for-office-365-proplus)



## <a name="add-languages-for-office-365-update-downloads"></a>Adicionar idiomas a downloads de atualização do Office 365
Você pode adicionar suporte para que o Configuration Manager baixe atualizações em qualquer idioma com suporte do Office 365, independentemente de haver suporte no Configuration Manager.    

> [!IMPORTANT]  
> A configuração de idiomas de atualização adicionais do Office 365 é aplicada a todo o site. Depois de adicionar os idiomas usando o procedimento a seguir, todas as atualizações do Office 365 serão baixadas nesses idiomas, bem como os idiomas que você selecionar na página **Seleção de idioma** nos assistentes Baixar atualizações de software ou Implantar atualizações de software.

### <a name="to-add-support-to-download-updates-for-additional-languages"></a>Para adicionar suporte para baixar atualizações para outros idiomas
Use o procedimento a seguir no ponto de atualização de software do site de administração central ou no site primário autônomo.
1. Em um prompt de comando, digite *wbemtest* como administrador para abrir o Testador de Instrumentação de Gerenciamento do Windows.
2. Clique em **Conectar**e, em seguida, digite *root\sms\site_&lt;siteCode&gt;*.
3. Clique em **Consulta** e, em seguida, execute a seguinte consulta: *select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"*  
   ![Consulta WMI](..\media\1-wmiquery.png)
4. No painel de resultados, clique duas vezes no objeto com o código de site para o site de administração central ou o site primário autônomo.
5. Selecione a propriedade **Acessórios**, clique em **Editar propriedade** e, em seguida, clique em **Exibir incorporado**.
![Editor de propriedades](..\media\2-propeditor.png)
6. Começando no primeiro resultado de consulta, abra cada objeto até encontrar aquele com **AdditionalUpdateLanguagesForO365** na propriedade **PropertyName**.
7. Selecione **Value2** e clique em **Editar propriedade**.  
![Editar a propriedade Value2](..\media\3-queryresult.png)
8. Adicione mais idiomas à propriedade **Value2** e clique em **Salvar propriedade**. <br/> Por exemplo, pt-pt (para português - Portugal), af-za (para africâner - África do Sul), nn-no (para Norueguês (Nynorsk) - Noruega), etc. Você digitaria `pt-pt,af-za,nn-no` para os idiomas de exemplo. Não use espaços entre os idiomas.
 
   ![Adicionar idiomas no Editor de Propriedades](..\media\4-props.png)  
9. Clique em **Fechar**, em **Fechar**, em **Salvar Propriedade** e em **Salvar Objeto** (se você clicar em **Fechar** aqui, os valores serão descartados). Clique em **Fechar** e, em seguida, em **Sair** para sair do Testador de Instrumentação de Gerenciamento do Windows.
10. No console do Configuration Manager, vá para **Biblioteca de software** > **Visão geral** > **Gerenciamento de Clientes do Office 365** > **Atualizações do Office 365**.
11. Agora, ao baixar as atualizações do Office 365, elas serão baixadas no idioma selecionado no assistente e configurou neste procedimento. Para verificar se as atualizações foram baixadas no idioma correto, vá para a origem do pacote para a atualização e procure por arquivos com o código de idioma no nome do arquivo.  
![Nomes de arquivos com idiomas adicionais](..\media\5-verification.png)

## <a name="updating-office-365-during-task-sequences-when-office-365-is-installed-in-the-base-image"></a>Atualizando o Office 365 durante as sequências de tarefas quando o Office 365 é instalado na imagem de base
Quando você instala um sistema operacional em que o Office 365 já está instalado na imagem, é possível que o valor da chave do Registro do canal de atualização tenha o local de instalação original. Nesse caso, a verificação de atualização não mostrará as atualizações de cliente do Office 365 conforme a aplicação. Há uma tarefa de atualizações automáticas do Office agendada que é executada várias vezes por semana. Depois de executar essa tarefa, o canal de atualização apontará para a URL de CDN do Office configurada e a verificação mostrará essas atualizações conforme aplicável. <!--510452-->

Para garantir que o canal de atualização esteja definido para que as atualizações aplicáveis serão encontradas, execute as seguintes etapas:
1. Em um computador com a mesma versão do Office 365 que a imagem base do sistema operacional, abra o Agendador de Tarefas (taskschd.msc) e identifique a tarefa de atualizações automáticas do Office 365. Normalmente, ela está localizada em **Biblioteca do Agendador de Tarefas** >**Microsoft**>**Office**.
2. Clique com o botão direito do mouse na tarefa de atualizações automáticas e selecione **Propriedades**.
3. Vá para a guia **Ações** e clique em **Editar**. Copie o comando e todos os argumentos. 
4. No console do Configuration Manager, edite sua sequência de tarefas.
5. Adicione uma nova etapa **Executar Linha de Comando** antes da etapa **Instalar atualizações** na sequência de tarefas. 
6. Copie o comando e os argumentos que foram reunidos da tarefa agendada de atualizações automáticas do Office. 
7. Clique em **OK**. 

## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a>Alterar o canal de atualização após habilitar os clientes do Office 365 para receber atualizações do Configuration Manager
Para alterar o canal de atualização após habilitar os clientes do Office 365 para receber atualizações do Configuration Manager, use a política de grupo para distribuir uma alteração de valor da chave do registro para os clientes do Office 365. Altere a chave do registro **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** para usar um dos seguintes valores:

- Canal Mensal <br/>
<i>(anteriormente Canal Atual)</i>:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60

- Canal Semestral <br/>
<i>(anteriormente Canal Adiado)</i>:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114

- Canal Mensal (direcionado)<Br/>
 <i>(anteriormente Primeira Versão do Canal Atual)</i>:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be

- Canal Semestral (direcionado) <br/>
<i>(anteriormente Primeira Versão do Canal Adiado)</i>:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf
<!--the channel names changed in Sept 2017- https://docs.microsoft.com/en-us/DeployOffice/overview-of-update-channels-for-office-365-proplus?ui=en-US&rs=en-US&ad=US>


<!--- You can create an Office 365 app without using the Office 365 Installation Wizard. To do this, you use the Office 2016 Deployment Tool (ODT) to download Office installation source files to a network share, generate Configure.xml that specifies the correct Office version and channel, and so on. Then, create an app for the files using the normal app management process.
> [!Note]
> The Office 365 Installation Wizard was introduced in Configuration Manager version 1702 and provides an easy way to create Office 365 apps.

- [Download the Office 2016 Deployment Tool](http://aka.ms/ODT2016) from the Microsoft Download Center.  
- Review the [configuration options for the Office Deployment Tool](https://technet.microsoft.com/library/jj219426.aspx).

You can create an application just as you would with any other application in Configuration Manager from **Software Library** > **Overview** > **Application Management** > **Applications**. For details, see [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application).
--->

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->
