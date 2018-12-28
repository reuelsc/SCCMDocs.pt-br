---
title: Criar itens de configuração para dispositivos com iOS e Mac OS X gerenciados com o Intune
titleSuffix: Configuration Manager
description: Use o item de configuração do iOS e Mac OS X do System Center Configuration Manager para gerenciar as configurações de dispositivos iOS e Mac OS X.
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 613a48ac-c55d-4c4a-94ea-d3747a1b10cb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf5f580d10c48bb44b3c202832ffff3a06c5c37f
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416173"
---
# <a name="how-to-create-configuration-items-for-ios-and-mac-os-x-devices-managed-with-intune"></a>Como criar itens de configuração para dispositivos com iOS e Mac OS X gerenciados com o Intune
Use o item de configuração **iOS e Mac OS X** do System Center Configuration Manager para gerenciar as configurações para dispositivos iOS e Mac OS X que estão registrados no Microsoft Intune ou são gerenciados localmente pelo Configuration Manager.  
  
### <a name="to-create-an-ios-and-mac-os-x-configuration-item"></a>Para criar um item de configuração do iOS e Mac OS X  
  
1. No console do Configuration Manager, clique em **Ativos e conformidade**.  
  
2. No workspace **Ativos e Conformidade**, expanda **Configurações de Conformidade** e clique em **Itens de Configuração**.  
  
3. Na guia **Início** , no grupo **Criar** , clique em **Criar Item de Configuração**.  
  
4. Na página **Geral** do **Assistente para Criar Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.  
  
5. Em **Especificar o tipo de item de configuração que deseja criar**, selecione **iOS e Mac OS X**.  
  
6. Se você criar e atribuir categorias, clique em **Categorias** para ajudá-lo a pesquisar e filtrar itens de configuração no console do Configuration Manager.  
  
7. Na página **Plataformas com Suporte** do assistente, selecione as plataformas específicas do iOS ou Mac OS X que avaliarão o item de configuração.  
  
8. Na página **Configurações do Dispositivo** do assistente, selecione o grupo de configurações que deseja configurar. Veja [Referência de configurações do item de configuração para iOS e Mac OS X](#BKMK_Setref) neste tópico para obter detalhes e clique **Avançar**.  
  
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
  
    Você pode exibir o novo item de configuração no nó **Itens de Configuração** do workspace **Ativos e Conformidade**.  
  
##  <a name="ios-and-mac-os-x-configuration-item-settings-reference"></a>Referência de configurações do item de configuração para iOS e Mac OS X  
  
###  <a name="password"></a>Senha  
  
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Exigir configurações de senha em dispositivos móveis**|Requer uma senha nos dispositivos com suporte.|  
|**Comprimento mínimo da senha (caracteres)**|O comprimento mínimo da senha.|  
|**Validade da senha em dias**|O número de dias antes que uma senha precise ser alterada.|  
|**Número de senhas lembradas**|Impede a reutilização de senhas usadas anteriormente.|  
|**Número de tentativas de logon com falha antes de o dispositivo ser apagado**|Apaga o dispositivo se houver falha neste número de tentativas de logon.<br /><br /> (somente iOS)|  
|**Complexidade da senha**|Escolha se é possível especificar um PIN como “1234” ou se é necessário fornecer uma senha forte.| 
|**Permitir senha simples**|Permita senha simples, como **0000** e **1234**.|
|**Impressão digital de desbloqueio**|Permite o uso de uma impressão digital para desbloquear o dispositivo.|
|**Modificação de senha** (somente supervisionado)|Permita que a senha do dispositivo seja adicionada, alterada ou removida.|
  
###  <a name="device"></a>Dispositivo  
 Essas configurações se aplicam a dispositivos iOS e Mac OS X.  
  
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Adicionar amigos do Game Center**|Permite adicionar amigos no aplicativo Game Center.|
|**Discagem de voz**|Permite o uso do recurso de discagem de voz no dispositivo.|  
|**Assistente de voz**|Permite o uso de um aplicativo de assistência de voz como o Siri.|  
|**Assistente de voz quando bloqueado**|Permite o uso de um aplicativo de assistência de voz como o Siri quando o dispositivo estiver bloqueado.|  
|**Captura de tela**|Permite tirar uma captura de tela da tela do dispositivo.|  
|**Cliente de chat com vídeo**|Permite o uso de aplicativos de chat com vídeo, como o Facetime.|  
|**Jogo para vários participantes**|Permite jogar com outros jogadores na Internet.|  
|**Software de carteira pessoal quando bloqueado**|Permite o uso de software de carteira pessoal como o Passbook.|  
|**Envio de dados de diagnóstico**|Permita o envio de arquivos de log do aplicativo.|  
|**Notificações da central de ações**|Permita que o usuário acesse a exibição de notificações sem desbloquear o dispositivo.|
|**Apple Music** (somente supervisionado)|Permita o uso do aplicativo Apple Music.|
|**Podcasts** (somente supervisionado)|Permita o uso do aplicativo Podcasts.|
|**Aplicativo de mensagens** (somente supervisionado)|Permita o uso do aplicativo de mensagens para enviar mensagens de texto.|
|**Modificação de papel de parede** (somente supervisionado)|Permita que o usuário altere o papel de parede do dispositivo.|
|**Pesquisa de definição de palavra** (somente supervisionado)|Permita o recurso do iOS que deixa você realçar uma palavra e pesquisar sua definição.|
|**Detecção de pulso para Apple Watches emparelhados**|Quando habilitada, o Apple Watch não exibirá notificações quando não estiver sendo usado.|
|**Filtro de profanidade da Siri** (somente supervisionado)|Impede que a Siri dite ou fale palavrões.|
|**Modificação do nome do dispositivo** (somente supervisionado)|Permita que o usuário altere o nome do dispositivo.|
|**Modificação das configurações de envio de diagnósticos** (somente supervisionado)|Permita ou bloqueie a habilidade do dispositivo enviar dados de diagnóstico para a Apple.|
|**Game Center** (somente supervisionado)|Permita o uso do aplicativo Game Center.|
|**iTunes Radio** (somente supervisionado)|Permita o uso do aplicativo iTunes Radio.|
|**Apple News** (somente supervisionado)|Permita o uso do aplicativo Apple News.|
|**Emparelhamento do Apple Watch** (somente supervisionado)|Permita que o dispositivo emparelhe com um Apple Watch.|
|**Correção automática** (somente supervisionado)|Permite que o dispositivo corrija automaticamente palavras incorretas.|
|**Modificação de Bluetooth** (somente supervisionado)|Permita que o usuário altere as configurações de Bluetooth no dispositivo.|
|**Alterações nas configurações de uso de dados para celular do aplicativo** (somente supervisionado)|Permita ao usuário controlar quais aplicativos podem usar dados de celular.|
|**Atalhos de teclado** (somente supervisionado)|Permita o uso de atalhos de teclado.|
|**Teclados preditivos** (somente supervisionado)|Permita o uso de teclados preditivos que sugerem palavras que o usuário pode querer.|
|**Verificação ortográfica do teclado** (somente supervisionado)|Permite o verificador de ortografia do dispositivo.|
|**Modificação das configurações de notificação** (somente supervisionado)|Permita que o usuário altere as configurações de notificação do dispositivo.|
|**Retornar resultados da Internet em pesquisa de Destaque** (somente supervisionado)|Permita que a pesquisa de Destaque conecte-se à Internet para fornecer mais resultados.|
|**Usar Siri para consultar o conteúdo da Internet gerado pelo usuário** (somente supervisionado)|Permita que a Siri acesse sites da Web para responder perguntas.|

  
###  <a name="store"></a>Repositório  
 Estas configurações se aplicam apenas a dispositivos iOS.  
  
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Armazenamento de aplicativos**|Permite o acesso a loja de aplicativos no dispositivo.|  
|**Digite uma senha para acessar o armazenamento de aplicativos**|Os usuários devem digitar uma senha para acessar a loja de aplicativos.|  
|**Compras no aplicativo**|Permite que os usuários façam compras no aplicativo.|
|**Instalação de aplicativos usando somente o Apple Configurator e o iTunes** (somente supervisionado)|Habilita ou desabilita a Loja de Aplicativos da tela inicial do dispositivo. Os usuários ainda podem usar o iTunes ou a ferramenta Apple Configurator para instalar e atualizar aplicativos.|
|**Acesso à iBooks Store** (somente supervisionado)|Permita que o usuário procure e compre livros da iBooks Store.|
|**Downloads automáticos de aplicativo** (somente supervisionados)|Permita que aplicativos adquiridos em outros dispositivos sejam baixados automaticamente para esse dispositivo. Essa configuração não afeta as atualizações do aplicativo.|

  
###  <a name="browser"></a>Navegador  
 Estas configurações se aplicam apenas a dispositivos iOS.  
  
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Navegador padrão**|O usuário pode alterar o navegador de Internet padrão.|  
|**Preenchimento automático**|O usuário pode alterar as configurações de preenchimento automático no navegador.|  
|**Script ativo**|O navegador pode executar scripts, como scripts do ActiveX.|  
|**Bloqueador de pop-up**|Habilita ou desabilita o bloqueador de pop-ups do navegador.|  
|**Cookies**|Permita que os cookies sejam salvos no dispositivo.|  
|**Aviso de fraude**|Habilite ou desabilite avisos de sites fraudulentos potenciais.|  
  
###  <a name="content-rating"></a>Classificação de conteúdo  
 Estas configurações se aplicam apenas a dispositivos iOS.  
  
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Conteúdo explícito na loja de mídia**|Especifique se deseja permitir que conteúdo somente para adultos seja acessado da loja de aplicativos.|  
|**Região de classificações**|Especifica o país para o qual você deseja aplicar restrições de classificações.|  
|**Classificação de filme**|Especifique a classificação máxima de conteúdo de filme que deseja permitir.|  
|**Classificação de programa de TV**|Especifique a classificação máxima de programa de TV que deseja permitir.|  
|**Classificação de aplicativo**|Especifique a classificação máxima de conteúdo de aplicativo que deseja permitir.| 
|**Conteúdo da iBook Store sinalizado como 'Erotismo'** (apenas supervisionado)|Permita que o usuário baixe livros com a categoria "Erotismo".| 
  
> [!NOTE]  
>  As classificações que podem ser selecionadas podem variar de acordo com a **Região de classificações** selecionada.  
  
###  <a name="cloud"></a>Nuvem  
 Estas configurações se aplicam apenas a dispositivos iOS.  
  
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Backup na nuvem**|Permita o backup em um serviço de nuvem como o iCloud.|  
|**Backup criptografado**|Permita que o backup em um serviço de nuvem seja criptografado.|  
|**Sincronização de documentos**|Permita a sincronização de documentos em um serviço de nuvem.|  
|**Sincronização de fotos**|Permita a sincronização de fotos em um serviço de nuvem.| 
|**Biblioteca de Fotos do iCloud**|Se for definido como **Não**, desabilitará o uso da biblioteca de fotos do iCloud, o que permite aos usuários armazenar fotos e vídeos na nuvem. As fotos que não forem totalmente baixadas na biblioteca de fotos do iCloud para o dispositivo serão removidas do dispositivo se essa opção for definida como **Não**.|
|**Compartilhamento de Fotos do iCloud**|Defina como **Não** para desabilitar o Compartilhamento de Fotos do iCloud no dispositivo.|
|**Entrega para continuar atividades em outro dispositivo**|Permita que o usuário continue, em outro dispositivo iOS ou Mac OS X, o trabalho iniciado em um dispositivo iOS.|
|**Sincronizar dados de aplicativos gerenciados para iCloud**|Permita que os aplicativos que você gerencia com o Intune sincronizem dados com a conta do iCloud do usuário.|

  
###  <a name="security"></a>Segurança  
 Estas configurações se aplicam apenas a dispositivos iOS.  
  
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Câmera**|Permita o uso da câmera do dispositivo.| 
|**Confiar em novos autores de aplicativos empresariais**|Permita que o usuário opte por confiar em aplicativos que não foram baixados da loja de aplicativos.| 
  
###  <a name="roaming"></a>Roaming  
 Estas configurações se aplicam apenas a dispositivos iOS.  
  
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Roaming de voz**|Permite chamadas de voz durante o roaming.|  
|**Sincronização automática durante o roaming**|Permite a sincronização automática do dispositivo durante o roaming.|  
|**Roaming de dados**|Permita o roaming entre redes durante o acesso de dados.|  
  
###  <a name="system-security"></a>Segurança do sistema  
 Estas configurações se aplicam apenas a dispositivos iOS.  
  
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Usuário deve aceitar certificados TLS não confiáveis**|Se **Permitido**, permite que o usuário aceite estes certificados. Se **Proibido**, rejeita automaticamente os certificados não confiáveis.|
|**Permitir Bloqueio de Ativação (somente modo supervisionado)**|Use esta configuração para habilitar o Bloqueio de Ativação do iOS nos dispositivos iOS **supervisionados** que você gerencia. Para obter mais informações sobre o Bloqueio de Ativação, consulte [Manage iOS Activation Lock with System Center Configuration Manager](../../mdm/deploy-use/manage-ios-activation-lock.md) (Gerenciar o Bloqueio de Ativação do iOS com o System Center Configuration Manager).
|**Centro de controle na tela de bloqueio**|Controla se o aplicativo do centro de controle pode ser acessado quando o dispositivo estiver bloqueado.|  
|**Exibição de notificação na tela de bloqueio**|Controla se as notificações podem ser exibidas quando o dispositivo estiver bloqueado.|  
|**Exibição atual da tela de bloqueio**|Controla se a exibição Atual pode ser vista quando o dispositivo estiver bloqueado.|  
|**Modificar configurações da conta** (somente supervisionado)|Permita que o usuário altere as configurações de conta, como configurações de email.|
|**Fazer alterações nas configurações do aplicativo Encontrar Meus Amigos** (somente supervisionado)|Permita que o usuário altere as configurações para o aplicativo Encontrar Meus Amigos.|
|**Usar o emparelhamento de host para controlar os dispositivos com os quais um dispositivo iOS pode ser emparelhado** (somente supervisionado)|Permita que o emparelhamento do host deixe o administrador controlar com quais dispositivos um dispositivo iOS pode emparelhar.|
|**Apagar todo o conteúdo e as configurações** (somente supervisionado)|Permita o uso da opção de apagar todo o conteúdo e as configurações no dispositivo.|
|**Configurar restrições no dispositivo** (somente supervisionado)|Permita que o usuário configure as restrições de dispositivo (controles dos pais) no dispositivo.|
|**Instalar perfis de configuração e certificados** (somente supervisionado)|Permita que o usuário instale perfis de configuração e certificados.|
|**Senha para solicitações de saída do AirPlay**|Exigir uma senha de emparelhamento quando o usuário usar AirPlay para transmitir o conteúdo para outros dispositivos da Apple.|
  
###  <a name="data-protection"></a>Proteção de dados  
 Estas configurações se aplicam apenas a dispositivos iOS.  
  
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Abrir documentos em aplicativos gerenciados em outros aplicativos não gerenciados**|Para uso com aplicativos gerenciados pelas políticas de gerenciamento de aplicativos do Configuration Manager.|  
|**Abrir documentos em aplicativos não gerenciados em outros aplicativos gerenciados**|Para uso com aplicativos gerenciados pelas políticas de gerenciamento de aplicativos do Configuration Manager.| 
|**Tratar o AirDrop como um destino não gerenciado** (somente supervisionado)|Impede que os aplicativos gerenciados sejam capazes de enviar dados. Airdrop.|
|**AirDrop** (somente supervisionado)|Permita o uso do recurso AirDrop para trocar conteúdo com dispositivos próximos.|
  
###  <a name="compliant-and-noncompliant-apps-ios"></a>Aplicativos compatíveis e não compatíveis (iOS)  
 Permite especificar uma lista de aplicativos do iOS que estão em conformidade ou sem conformidade em sua empresa. Em seguida, você pode usar os relatórios para exibir os dispositivos que contêm aplicativos não compatíveis instalados e o usuário associado.  
  
 Não é possível especificar aplicativos compatíveis e não compatíveis no mesmo item de configuração.  
  
#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>Para especificar a lista de aplicativos compatíveis ou não compatíveis  
  
1. Na página **Aplicativos Compatíveis e Não Compatíveis (iOS)** , especifique as seguintes informações:  
  
   -   **Lista de aplicativos não compatíveis**: escolha essa opção se desejar especificar uma lista de aplicativos que serão relatados como não compatíveis se forem instalados pelos usuários.  
  
   -   **Lista de aplicativos compatíveis**: escolha essa opção se desejar especificar uma lista de aplicativos que os usuários têm permissão para instalar. Todos os outros aplicativos instalados serão relatados como não compatíveis.  
  
   -   **Adicionar** – adiciona um aplicativo à lista selecionada. Especifique um nome da sua preferência, opcionalmente o editor do aplicativo, e a URL para o aplicativo na loja de aplicativos.  
  
        Para especificar a URL, na iTunes App Store, procure o aplicativo que deseja usar.  
  
        Abra a página do aplicativo e copie a URL para a área de transferência. Agora você pode usar essa URL na lista de aplicativos compatíveis ou incompatíveis.  
  
        **Exemplo:** Pesquise o **Microsoft Word para iPad** aplicativo. A URL usada será **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**.  
  
   -   **Editar** – permite editar o nome, o fornecedor e a URL do aplicativo selecionado.  
  
   -   **Remover** – exclui o aplicativo selecionado da lista.  
  
   -   **Importar** – importa uma lista dos aplicativos que você especificou em um arquivo de valores separados por vírgulas. Use o formato, nome do aplicativo, editor e a URL do aplicativo no arquivo.  
  
2. Quando tiver terminado, clique em **Avançar**.  
  
   Você pode usar um dos seguintes relatórios para monitorar aplicativos compatíveis e não compatíveis:  
  
- **Lista e dispositivos de aplicativos não compatíveis para um usuário especificado** – Exibe informações sobre usuários e dispositivos que têm aplicativos instalados que não são compatíveis com uma política especificada.  
  
- **Resumo de usuários que têm aplicativos não compatíveis** – Exibe informações sobre usuários que têm aplicativos instalados que não são compatíveis com uma política especificada.  
  
  Para obter informações sobre como usar relatórios, consulte [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  
  
###  <a name="compliant-and-noncompliant-apps-mac-os-x"></a>Aplicativos compatíveis e não compatíveis (Mac OS X)  
 Permite especificar uma lista de aplicativos do Mac OS X que são compatíveis ou não compatíveis em sua empresa. Em seguida, você pode usar os relatórios para exibir os dispositivos que contêm aplicativos não compatíveis instalados e o usuário associado.  
  
 Não é possível especificar aplicativos compatíveis e não compatíveis no mesmo item de configuração.  
  
#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>Para especificar a lista de aplicativos compatíveis ou não compatíveis  
  
1. Na página **Aplicativos Compatíveis e Não Compatíveis (Mac OS X)** , especifique as seguintes informações:  
  
   - **Lista de aplicativos não compatíveis**: escolha essa opção se desejar especificar uma lista de aplicativos que serão relatados como não compatíveis se forem instalados pelos usuários.  
  
   - **Lista de aplicativos compatíveis**: escolha essa opção se desejar especificar uma lista de aplicativos que os usuários têm permissão para instalar. Todos os outros aplicativos instalados serão relatados como não compatíveis.  
  
   - **Adicionar** – adiciona um aplicativo à lista selecionada. Especifique um nome de sua preferência, opcionalmente, o fornecedor do aplicativo e a ID do pacote do aplicativo.  
  
     > [!TIP]
     >  Para localizar a ID do pacote de um aplicativo, use as seguintes etapas em um computador Mac que tem o aplicativo instalado:  
     > 
     > 1. Abra a pasta na qual o aplicativo está instalado (por exemplo, **/Aplicativos**)  
     >    2.  Selecione o pacote *<nome do aplicativo\>***.app** e escolha **Mostrar Conteúdo do Pacote**  
     >    3.  Abra o arquivo **Info.plist**  
     >    4.  Verifique o valor associado à chave **CFBundleIdentifier**  
     > 
     >    O formato para a ID do Pacote é **com.contoso.nomeaplicativo**  
  
   - **Editar** – permite editar o nome, o fornecedor e a ID do pacote do aplicativo selecionado.  
  
   - **Remover** – exclui o aplicativo selecionado da lista.  
  
   - **Importar** – importa uma lista dos aplicativos que você especificou em um arquivo de valores separados por vírgulas. Use o formato, nome do aplicativo, fornecedor e ID de lote de aplicativo encontrados no arquivo.  
  
2. Quando tiver terminado, clique em **Avançar**.  
  
   Você pode usar um dos seguintes relatórios para monitorar aplicativos compatíveis e não compatíveis:  
  
- **Lista e dispositivos de aplicativos não compatíveis para um usuário especificado** – Exibe informações sobre usuários e dispositivos que têm aplicativos instalados que não são compatíveis com uma política especificada.  
  
- **Resumo de usuários que têm aplicativos não compatíveis** – Exibe informações sobre usuários que têm aplicativos instalados que não são compatíveis com uma política especificada.  
  
  Para obter informações sobre como usar relatórios, consulte [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  
  
### <a name="ios-and-mac-os-x-custom-profile-settings"></a>Configurações de perfil personalizado para iOS e Mac OS X  
 Use **Perfis Personalizados do iOS e Mac OS X** para implantar as configurações criadas com a [ferramenta Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) em dispositivos iOS e Mac OS X. Essa ferramenta permite que você crie várias configurações que controlam a operação desses dispositivos e as exporte para um perfil de configuração. Em seguida, você poderá importar este perfil de configuração para um perfil personalizado do iOS e Mac OS X e implantar as configurações em usuários e dispositivos em sua organização.  
  
> [!NOTE]  
>  Verifique se as configurações exportadas da ferramenta Apple Configurator são compatíveis com a versão do iOS ou Mac OS X nos dispositivos nos quais você implantar o perfil. Para obter informações sobre como as incompatibilidades de configuração são resolvidas, procure a Referência de Perfil de Configuração e a Referência de Protocolo de Gerenciamento de Dispositivos Móveis no site do [Desenvolvedor Apple](https://developer.apple.com/) .  
  
#### <a name="to-create-an-ios-and-mac-os-x-custom-profile"></a>Para criar um perfil personalizado do iOS e Mac OS X  
  
1.  Na página **Definir configurações de perfil personalizado do iOS e Mac OS X** do **Assistente para Criar Item de Configuração**, especifique as seguintes informações:  
  
    -   **Nome do perfil de configuração personalizado (exibido a usuários)** – Forneça um nome para a política que será exibida no dispositivo e nos relatórios do Configuration Manager.  
  
    -   **Importar** – escolha um arquivo que você exportou da ferramenta Apple Configurator.  
  
    -   **Detalhes do perfil de configuração** – exibe o arquivo que você importou.  
  
    -   **Corrigir configurações não compatíveis** -  
  
         Selecione se deseja corrigir configurações não compatíveis (quando houver suporte).  
  
    -   **Severidade de não conformidade dos relatórios** – especifique o nível de severidade que será relatado se esta política de conformidade for avaliada como não compatível. Os níveis de severidade disponíveis são os seguintes:  
  
        > [!NOTE]  
        >  Quando um dispositivo Mac OS X está no modo de Suspensão, as políticas e os perfis não podem ser entregues nem inventariados. Como resultado, o console do Configuration Manager pode exibir temporariamente o status de configurações de Política, até a próxima vez que o dispositivo sair do modo de Suspensão.  
  
        -   **Nenhum** dispositivos que não cumprem essa regra de conformidade não relatam uma severidade de falha em relatórios do Configuration Manager.  
  
        -   **Informações** dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha de **Informações** em relatórios do Configuration Manager.  
  
        -   **Aviso** dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha de **Aviso** em relatórios do Configuration Manager.  
  
        -   **Crítico** dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico** em relatórios do Configuration Manager.  
  
        -   **Crítico com evento** dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico com evento** em relatórios do Configuration Manager. Este nível de severidade também é registrado como um evento do Windows no log de eventos do aplicativo.  
  
#### <a name="how-to-create-a-configuration-profile-file"></a>Como criar um arquivo de perfil de configuração  
 Você pode criar o arquivo de perfil de configuração usado pela política personalizada de duas maneiras:  
  
-   Exporte o arquivo (com a extensão **.mobileconfig**) da ferramenta Apple Configurator.  
  
-   Crie o arquivo você mesmo usando o esquema apropriado da [Referência de Chave de Perfil de Configuração da Apple](https://developer.apple.com/library/ios/featuredarticles/iPhoneConfigurationProfileRef/Introduction/Introduction.html).  
  
###  <a name="kiosk-mode-ios"></a>Modo de quiosque (iOS)  
 O modo de quiosque permite bloquear um dispositivo para permitir que somente alguns recursos funcionem. Por exemplo, você pode permitir que um dispositivo execute apenas um aplicativo gerenciado que você especificar ou pode desabilitar os botões de volume em um dispositivo. Essas configurações podem ser usadas para um modelo de demonstração de um dispositivo ou um dispositivo que é dedicado a apenas uma função, como um dispositivo de ponto de venda.  
  
#### <a name="to-configure-kiosk-mode-for-ios-devices"></a>Para configurar o modo de quiosque para dispositivos iOS  
  
1. Na página **Definir configurações do modo de quiosque para dispositivos iOS** do **Assistente para Criar Item de Configuração**, especifique as seguintes informações:  
  
   - **Selecionar Aplicativo** – escolha o aplicativo que terá permissão para ser executado quando o dispositivo estiver no modo de quiosque. Nenhum outro aplicativo poderá ser executado no dispositivo. Escolha:  
  
     - **Aplicativo Gerenciado** – Clique em Procurar e selecione um aplicativo gerenciado.  
  
     - **Aplicativo da Loja** – Especifique a URL para um aplicativo na loja de aplicativos e clique em **Obter a ID do aplicativo** para preencher o campo **ID de aplicativo** .  
  
       Para encontrar a URL do aplicativo:  
  
     - Usando um mecanismo de pesquisa, encontre o aplicativo que você deseja usar na iTunes App Store e abra a página do aplicativo.  
  
     - Copie a URL da página e use-a como a URL para especificar o aplicativo que você deseja executar no modo de quiosque.  
  
     - **Exemplo:** Pesquise **Microsoft Word para iPad**. A URL usada será **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**.  
  
   - **Toque** – habilita ou desabilita a tela touch no dispositivo.  
  
   - **Rotação da tela** – habilita ou desabilita a alteração da orientação da tela quando você gira o dispositivo.  
  
   - **Botões de volume** – habilita ou desabilita o uso dos botões de volume no dispositivo.  
  
   - **Botão de toque** – habilita ou desabilita o botão toque (mudo) no dispositivo.  
  
   - **Botão de suspensão e ativação da tela** – habilita ou desabilita o botão de ativação e suspensão da tela no dispositivo.  
  
   - **Bloqueio automático** – habilita ou desabilita o bloqueio automático do dispositivo.  
  
   - **Áudio mono** – habilita ou desabilita a configuração de acessibilidade **Áudio mono**.  
  
   - **Comando de voz** – habilita ou desabilita a configuração de acessibilidade **VoiceOver** que lê em voz alta o texto na tela do dispositivo.  
  
   - **Ajustes do comando de voz** – habilita ou desabilita os ajustes do comando de voz que permitem ajustar a função VoiceOver (por exemplo, a velocidade em que o texto na tela é lido em voz alta).  
  
   - **Zoom** – habilita ou desabilita a opção de acessibilidade **Zoom**, que permite usar o toque para ampliar a tela do dispositivo de acessibilidade.  
  
   - **Ajustes de zoom** – habilita ou desabilita os ajustes de zoom que permitem ajustar a função de zoom.  
  
   - **Inverter cores** – habilita ou desabilita a opção de acessibilidade **Inverter Cores** que ajusta a exibição para ajudar os usuários com deficiências visuais.  
  
   - **Ajustes de cores invertidas** – habilita ou desabilita ajustes de cores invertidas, que permitem ajustar a função de cores invertidas.  
  
   - **Toque assistencial** – habilita ou desabilita a opção de acessibilidade **Toque Assistencial**, que ajuda os usuários a executar gestos na tela que podem ser difíceis de executar.  
  
   - **Ajuste do toque assistencial** – habilita ou desabilita os ajustes de toque assistencial, que permitem ajustar a função de toque assistencial.  
  
   - **Seleção de fala** – habilita ou desabilita as configurações de acessibilidade **Seleção de Fala**, que podem ler em voz alta o texto que você selecionar.  
  
   - **Corrigir configurações não compatíveis** – escolha se deseja corrigir configurações não compatíveis (quando houver suporte).  
  
   - **Severidade de não conformidade dos relatórios** – especifique o nível de severidade que será relatado se esta política de conformidade for avaliada como não compatível. Os níveis de severidade disponíveis são:  
  
     -   **Nenhum** dispositivos que não cumprem essa regra de conformidade não relatam uma severidade de falha em relatórios do Configuration Manager.  
  
     -   **Informações** dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha de **Informações** em relatórios do Configuration Manager.  
  
     -   **Aviso** dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha de **Aviso** em relatórios do Configuration Manager.  
  
     -   **Crítico** dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico** em relatórios do Configuration Manager.  
  
     -   **Crítico com evento** dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico com evento** em relatórios do Configuration Manager. Este nível de severidade também é registrado como um evento do Windows no log de eventos do aplicativo.  
  
## <a name="see-also"></a>Consulte também  
 [Itens de configuração de dispositivos gerenciados sem o cliente do System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)
