---
title: Recursos no Technical Preview 1609
titleSuffix: Configuration Manager
description: "Saiba mais sobre os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1609."
ms.custom: na
ms.date: 01/23/2017
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: article
ms.assetid: e2a59116-b2e5-4dd2-90eb-0b8a5eb50b56
caps.latest.revision: "2"
author: erikje
ms.author: erikje
manager: angrobe
ms.openlocfilehash: e1cceae5f73d003be2fe64df9e6dbaa7badaf0c7
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="capabilities-in-technical-preview-1609-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1609 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*



Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1609. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview.      Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de um technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos em um technical preview.    

**Problemas conhecidos nesse Technical Preview:**  
*  Quando você atualiza para o Technical Preview 1609 do Configuration Manager, todas as políticas de atualização de edição implantadas serão excluídas. Para continuar a usar essas políticas, você deve recriá-las e implantá-las.


**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  

## <a name="improvements-to-endpoint-protection"></a>Melhorias no Endpoint Protection
Aperfeiçoamento nas configurações de política antimalware do Endpoint Protection – agora você pode especificar o nível em que o Serviço de Proteção de Nuvem do Endpoint Protection bloqueará arquivos suspeitos. Uma nova configuração permite aos administradores especificar computadores “arriscados” com base nas grandes quantidades de malware que eles encontram.

## <a name="increased-number-of-enrolled-devices"></a>Aumento do número de dispositivos registrados
Os administradores agora podem habilitar os usuários para registrar até 15 dispositivos no gerenciamento de dispositivo móvel híbridos no Intune. O limite era cinco dispositivos por usuário.

## <a name="additional-apple-dep-settings"></a>Configurações adicionais do Apple DEP

Os administradores agora podem definir as seguintes configurações do Apple DEP (Programa de Registro do Dispositivo) no perfil do DEP para dispositivos iOS e Mac:
- **ID de Toque**
- **Zoom**
- **Siri**

Se habilitado, o Assistente de Configuração da Apple solicitará esse dispositivo durante a ativação.

## <a name="integration-with-upgrade-analytics"></a>Integração com o Upgrade Analytics

O Upgrade Analytics permite que você avalie e analise a prontidão e a compatibilidade do dispositivo com o Windows 10 para permitir atualizações mais fáceis e estáveis. Com a integração do Upgrade Analytics ao Configuration Manager, você pode acessar os dados de compatibilidade da atualização no console de administração do Configuration Manager e, da lista de dispositivos, destinar dispositivos para atualização ou correção.

Você pode ler mais sobre o Upgrade Analytics em [Get started with Upgrade Analytics](https://technet.microsoft.com/itpro/windows/deploy/upgrade-analytics-get-started) (Introdução ao Upgrade Analytics).

## <a name="native-connection-types-for-windows-10-vpn-hybrid-profiles"></a>Tipos de conexão nativa para perfis híbridos de VPN do Windows 10

Ao usar o Configuration Manager com o Intune, agora você pode criar perfis de VPN do Windows 10 com os tipos de conexão Microsoft Automatic, IKEv2, PPTP e L2TP no console do Configuration Manager sem usar o OMA-URI.

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Aprimoramentos na integração da Windows Store para Empresas com o Configuration Manager

Nesta versão, atualizamos a [integração da Windows Store para Empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) com esses novos recursos:

**Atualização:** na versão de technical preview atual, o recurso de sincronização imediata não é funcional.

- Anteriormente, você podia implantar apenas aplicativos gratuitos da Windows Store para Empresas. Agora, o Configuration Manager também dá suporte à implantação de aplicativos licenciados online pagos (apenas para dispositivos registrados do Intune).
- Agora você pode iniciar uma sincronização imediata entre a Windows Store para Empresas e o Configuration Manager.
- Agora você pode modificar a chave secreta do cliente obtida do Azure Active Directory

### <a name="try-it-out"></a>Experimente!

#### <a name="purchase-and-sync-a-paid-online-licensed-app"></a>Compre e sincronize um aplicativo licenciado online pago

1. Compre aplicativo licenciado online pago da Windows Store para Empresas.
2. No espaço de trabalho **Administração** do console do Configuration Manager, clique em **Serviços de Nuvem** > **Atualizações e Manutenção** > **Windows Store para Empresas**.
3. Na guia **Início**, no grupo **Sincronizar**, clique em **Sincronizar Agora**.
4. Logo depois disso, o aplicativo que você adquiriu aparecerá no nó **Informações sobre Licença para Aplicativos da Loja** do espaço de trabalho **Gerenciamento de Aplicativos**.

#### <a name="create-and-deploy-a-configuration-manager-application-from-the-synchronized-app-data"></a>Criar e implantar um aplicativo do Configuration Manager por meio dos dados do aplicativo sincronizado

O procedimento para criar e implantar um aplicativo do Configuration Manager por meio de um aplicativo pago da loja é o mesmo da criação de um aplicativo por meio de um aplicativo gratuito. Consulte a seção **Criar e implantar um aplicativo do Configuration Manager por meio de um aplicativo da Windows Store para Empresas** em [Gerenciar aplicativos da Windows Store para Empresas com o System Center Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).


#### <a name="modify-the-client-secret-key-from-azure-active-directory"></a>Modificar a chave secreta do cliente do Azure Active Directory

1. No espaço de trabalho **Administração** do console do Configuration Manager, clique em **Serviços de Nuvem** > **Atualizações e Manutenção** > **Windows Store para Empresas**.
2. Selecione sua conta da Windows Store para Empresas e clique em **Propriedades**.
3. Na caixa de diálogo **Windows Store for Business Account Properties (Propriedades da conta da Windows Store para Empresas)**, insira uma nova chave no campo **Chave secreta do cliente** e clique em **Verificar**. Depois de verificar, clique em **Aplicar** e feche a caixa de diálogo.


## <a name="new-compliance-settings-for-configuration-items"></a>Novas configurações de conformidade para itens de configuração

Adicionamos várias novas configurações que você pode usar em seus itens de configuração para várias plataformas de dispositivo.
Essas são configurações que anteriormente estavam no Microsoft Intune em uma configuração autônoma e agora estão disponíveis quando você usa o Intune com o Configuration Manager.
Se você precisar de ajuda com qualquer uma dessas configurações, abra [Manage settings and features on your devices with Microsoft Intune policies (Gerenciar configurações e recursos em seus dispositivos com políticas do Microsoft Intune)](https://docs.microsoft.com/en-us/intune/deploy-use/manage-settings-and-features-on-your-devices-with-microsoft-intune-policies) e selecione o subtópico de configurações da plataforma desejada.


### <a name="new-settings-for-android-devices"></a>Novas configurações para dispositivos Android

#### <a name="password-settings"></a>Configurações de senha

- **Lembrar histórico de senha**
- **Permitir desbloqueio por impressão digital**

#### <a name="security-settings"></a>Configurações de segurança

- **Exigir criptografia em cartões de memória**
- **Permitir captura de tela**
- **Permitir envio de dados diagnósticos**

#### <a name="browser-settings"></a>Configurações do navegador

- **Permitir navegador da Web**
- **Permitir preenchimento automático**
- **Permitir bloqueador de pop-up**
- **Permitir cookies**
- **Permitir script ativo**

#### <a name="app-settings"></a>Configurações do aplicativo

- **Permitir Google Play Store**

#### <a name="device-capability-settings"></a>Configurações de funcionalidade do dispositivo

- **Permitir armazenamento removível**
- **Permitir compartilhamento de Internet por Wi-Fi**
- **Permitir geolocalização**
- **Permitir NFC**
- **Permitir Bluetooth**
- **Permitir roaming de voz**
- **Permitir roaming de dados**
- **Permitir mensagens SMS/MMS**
- **Permitir assistência de voz**
- **Permitir discagem por voz**
- **Permitir copiar e colar**


### <a name="new-settings-for-ios-devices"></a>Novas configurações para dispositivos iOS

#### <a name="password-settings"></a>Configurações de senha

- **Número de caracteres complexos necessários na senha**
- **Permitir senha simples**
- **Minutos de inatividade antes de a senha ser necessária**
- **Lembrar histórico de senha**

### <a name="new-settings-for-mac-os-x-devices"></a>Novas configurações para dispositivos Mac OS X

#### <a name="password-settings"></a>Configurações de senha

- **Número de caracteres complexos necessários na senha**
- **Permitir senha simples**
- **Lembrar histórico de senha**
- **Minutos de inatividade antes que o protetor de tela seja ativado**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Novas configurações para dispositivos Windows 10 Desktop e Mobile

#### <a name="password-settings"></a>Configurações de senha

- **Número mínimo de conjuntos de caracteres**
- **Lembrar histórico de senha**
- **Exigir uma senha quando o dispositivo volta do estado ocioso**

#### <a name="security-settings"></a>Configurações de segurança

- **Exigir criptografia no dispositivo móvel**
- **Permitir cancelamento de registro manual**

#### <a name="device-capability-settings"></a>Configurações de funcionalidade do dispositivo

- **Permitir VPN por celular**
- **Permitir roaming de VPN no celular**
- **Permitir a redefinição do telefone**
- **Permitir conexão USB**
- **Permitir Cortana**
- **Permitir notificações da central de ações**

### <a name="new-settings-for-windows-10-team-devices"></a>Novas configurações para os dispositivos do Windows 10 Team

#### <a name="device-settings"></a>Configurações do dispositivo

- **Habilitar Azure Operational Insights**
- **Habilitar projeção sem fio Miracast**
- **Escolher as informações da reunião exibidas na tela de boas-vindas**
- **URL da imagem de tela de fundo da tela de bloqueio**


### <a name="new-settings-for-windows-81-devices"></a>Novas configurações para dispositivos Windows 8.1

#### <a name="applicability-settings"></a>Configurações de aplicabilidade

- **Aplicar todas as configurações ao Windows 10**

#### <a name="password-settings"></a>Configurações de senha

- **Tipo de senha necessária**
- **Número mínimo de conjuntos de caracteres**
- **Tamanho mínimo da senha**
- **Número de falhas de entrada repetidas permitidas antes que o dispositivo seja apagado**
- **Minutos de inatividade antes que a tela seja desligada**
- **Expiração da senha (dias)**
- **Lembrar histórico de senha**
- **Evitar a reutilização de senhas anteriores**
- **Permitir PIN e senha com imagem**

#### <a name="browser-settings"></a>Configurações do navegador

- **Permitir detecção automática da rede intranet**


### <a name="new-settings-for-windows-phone-81-devices"></a>Novas configurações para dispositivos Windows Phone 8.1

#### <a name="applicability-settings"></a>Configurações de aplicabilidade

- **Aplicar todas as configurações ao Windows 10**

#### <a name="password-settings"></a>Configurações de senha

- **Número mínimo de conjuntos de caracteres**
- **Permitir senha simples**
- **Lembrar histórico de senha**

#### <a name="device-capability-settings"></a>Configurações de funcionalidade do dispositivo

- **Permitir conexão automática a pontos de acesso Wi-Fi gratuitos**


## <a name="improvements-for-boundary-groups"></a>Aprimoramentos para grupos de limites
Essa versão prévia introduz alterações importantes para os grupos de limites e como eles funcionam com pontos de distribuição. Essas alterações ajudarão a simplificar o design da infraestrutura de conteúdo, enquanto proporcionam a você mais controle sobre como e quando os clientes realizam o fallback para pesquisar pontos de distribuição adicionais como locais de fonte de conteúdo. Isso inclui pontos de distribuição baseados em nuvem e locais.

Esses aprimoramentos substituem comportamentos e conceitos com os quais você talvez esteja familiarizado hoje (como configurar pontos de distribuição para serem rápidos ou lentos) e os substituem por um novo modelo que deve ser mais fácil de configurar e manter. Essas alterações também são bases para alterações futuras que melhoram outras funções do sistema de sites associadas aos grupos de limites.  

Durante a atualização para a 1609, a atualização converte suas configurações de grupo de limites atuais de acordo com o novo modelo para que essas alterações não incomodem suas configurações de distribuição de conteúdo (consulte [Atualizar grupos de limites existentes para o novo modelo](/sccm/core/get-started/capabilities-in-technical-preview-1609#bkmk_update)).

As seções a seguir detalham as alterações introduzidas com essa versão prévia, como funciona o novo modelo e o que você pode esperar ao atualizar um site que já tenha grupos de limites configurados.



### <a name="changes-in-ui-and-behavior-for-boundary-groups-and-content-locations"></a>Alterações na interface do usuário e comportamento de grupos de limites e locais de conteúdo
A seguir estão as principais alterações de grupos de limites e como os clientes encontram conteúdo. Muitas dessas alterações e conceitos funcionam em conjunto.
-   **As configurações para rápido ou lento foram removidas:** você não configura mais pontos de distribuição individuais para serem rápidos ou lentos.  Em vez disso, cada sistema de sites associado a um grupo de limites é tratado da mesma forma. Por causa dessa alteração, as guias **Referências** das propriedades do grupo de limites não dão mais suporte à configuração de Rápido ou Lento.
-   **Novo grupo de limites padrão em cada site:** cada site primário tem um novo grupo de limites padrão chamado ***Default-Site-Boundary-Group\<sitecode>***.  Quando um cliente não está em um local de rede que é atribuído a um grupo de limites, o cliente usará os sistemas de sites associados ao grupo padrão do seu site atribuído. Planeje usar esse grupo de limites como uma substituição para o conceito de local de conteúdo de fallback.    
 -  **'Allow fallback source locations for content' (Permitir locais de origem de fallback para conteúdo)** foi removido: você não configura mais explicitamente um ponto de distribuição para ser usado para o fallback e as opções essa configuração foram removidos da interface do usuário.

    Além disso, o resultado da configuração **Permitir que os clientes usem um local de origem de fallback para o conteúdo** em um tipo de implantação para aplicativos foi alterado. Essa configuração em um tipo de implantação agora permite que um cliente use o grupo de limites de site padrão como um local de fonte de conteúdo.

 -  **Relações de grupos de limites:** cada grupo de limites pode ser vinculado a um ou mais grupos de limites adicionais. Esses links formam relações que são configuradas na nova guia de propriedades de grupo limites chamada **Relações**:
    -   Cada grupo de limites ao qual o cliente está associado diretamente é chamado de grupo de limites **atual**.  
    -   Qualquer grupo de limites que um cliente possa usar devido a uma associação entre o grupo de limites *atual* desse cliente e outro grupo é chamado de grupo de limites **vizinho**.
    -  A guia **Relações** é o local em que você adiciona grupos de limites que podem ser usados como um grupo de limites *vizinho*. Você também pode configurar um tempo em minutos que determina quando um cliente que não consegue localizar o conteúdo de um ponto de distribuição no grupo *atual* começará a pesquisar locais de conteúdo daqueles grupos de limites *vizinhos*.

        Quando você adicionar ou alterar uma configuração de grupo de limites, terá a opção de bloquear o fallback para aquele grupo de limites específico daquele grupo atual que está sendo configurado.

    Para usar a nova configuração, você define associações explícitas (links) de um grupo de limites para outro e configura todos os pontos de distribuição nesse grupo associado com o mesmo tempo em minutos. O tempo que você configurar determina quando um cliente que não consegue localizar uma fonte de conteúdo de seu grupo de limites *atual* pode começar a pesquisar fontes de conteúdo desse grupo de limites vizinho.

    Além dos grupos de limites configurados explicitamente, cada grupo de limite tem um link implícito para o grupo de limites de site padrão. Este link se torna ativo após 120 minutos, momento em que o grupo de limites de site padrão se torna um grupo de limites vizinho, o que permite que os clientes usem os pontos de distribuição associados a aquele grupo de limites como locais de fonte de conteúdo.

    Esse comportamento substitui o que anteriormente era chamado de fallback de conteúdo.  Você pode substituir esse comportamento padrão de 120 minutos associando explicitamente o grupo de limites de site padrão a um grupo *atual* e definindo um tempo específico em minutos ou bloqueando totalmente o fallback para impedir seu uso.


-   **Os clientes tentam obter o conteúdo de cada ponto de distribuição por até dois minutos:** quando um cliente pesquisa um local de fonte de conteúdo, ele tenta acessar cada ponto de distribuição por dois minutos antes de tentar outro ponto de distribuição. Essa é uma alteração de versões anteriores em que os clientes tentavam se conectar a um ponto de distribuição por até duas horas.

    - O primeiro ponto de distribuição que um cliente tenta usar é selecionado aleatoriamente do pool de pontos de distribuição disponíveis no grupo (ou grupos) de limites *atual* do cliente.

    - Após dois minutos, se o cliente não encontrou o conteúdo, ele muda para um novo ponto de distribuição e tenta obter o conteúdo daquele servidor. Esse processo se repete a cada dois minutos até que o cliente localize o conteúdo ou atinja o último servidor em seu pool.

    - Se um cliente não conseguir encontrar um local de fonte de conteúdo válido de seu pool *atual* antes do período de fallback para um grupo de limites *vizinho*, ele adicionará os pontos de distribuição daquele grupo *vizinho* ao final de sua lista atual e pesquisará o grupo de locais de fonte de conteúdo expandido que inclui os pontos de distribuição dos dois grupos de limites.

        > [!TIP]  
        > Quando você cria um link explícito do grupo de limites atual para o grupo de limites de site padrão e define um tempo de fallback menor do que o tempo de fallback de um link para um grupo de limites vizinho, os clientes começam a pesquisar os locais de origem do grupo de limites de site padrão antes de incluir o grupo vizinho.

    - Quando o cliente falha em obter o conteúdo do último servidor no pool, ele inicia o processo novamente.


### <a name="how-the-new-model-works"></a>Como o novo modelo funciona
Quando você configura grupos de limites, associa limites (locais de rede) e funções do sistema de sites, como pontos de distribuição, ao grupo de limites. Isso ajuda a vincular os clientes aos servidores do sistema de sites como pontos de distribuição que estão localizados próximos aos clientes na rede.   
-   Você pode atribuir o mesmo limite a vários grupos de limites
-   Servidores de sistema de sites, como pontos de distribuição, podem ser associados a vários grupos de limites, tornando-os disponíveis para uma gama mais ampla de locais de rede
-   Se um ponto de distribuição não estiver associado a um grupo de limites, os clientes não poderão usar esse ponto de distribuição como um local de fonte de conteúdo.

A partir desse technical preview, você define relações de grupo de limites para configurar o comportamento de fallback para locais de fonte de conteúdo. Esse novo comportamento é configurado na nova guia **Relações** das propriedades do grupo de limites e substitui a configuração dos sistemas de sites para serem rápidos ou lentos e a configuração de um grupo de limites para permitir o fallback do local de fonte para o conteúdo.

Na guia Relações você adiciona outros grupos de limites para configurar uma relação com esses grupos. Cada relação é um vínculo unidirecional do grupo de limites **atual** para o grupo de limites adicionado, que é chamado de **vizinho**. Para cada link que criar, você poderá configurar pontos de distribuição com um tempo de fallback em minutos. Este tempo é usado para determinar após quanto tempo os clientes no grupo de limites *atual* poderão começar a usar os pontos de distribuição no grupo de limites *vizinho* se eles não conseguirem encontrar um local de fonte de conteúdo válido de seu grupo de limites atual.

Quando um cliente não consegue encontrar conteúdo e começa a pesquisar os locais dos grupos de limites vizinho, ele aumenta o pool de pontos de distribuição disponíveis para aquele cliente de uma maneira controlada.  

-   Um grupo de limites pode ter mais de uma Relação. Isso permite que você configure o fallback para vizinhos diferentes para que ele ocorra após períodos de tempo diferentes.
-   Os clientes realizarão o fallback apenas para um grupo de limites que seja um vizinho de seu gripo de limites atual.
-   Quando um cliente é um membro de vários grupos de limites, o grupo de limite atual é definido como uma união de todos os grupos de limites do cliente.  Esse cliente pode, então, realizar o fallback para um vizinho de qualquer um desses grupos de limites original.

Além dos links que você define, há um link implícito que é criado automaticamente entre os grupos de limites que você cria e o grupo de limites padrão que é criado automaticamente para cada site. Esse link automático:
-   É usado por clientes que não estão em um limite associado a nenhum grupo de limites na sua hierarquia e usam automaticamente o grupo de limites padrão do seu site atribuído para identificar os locais de fonte de conteúdo válidos.   
-   É uma opção de fallback padrão do grupo de limites atual para o grupo de limites padrão de sites que é usada após 120 minutos.

**Exemplo de uso do novo modelo:**     
Você cria três grupos de limites que não compartilham limites ou servidores de sistemas de sites:
-   Grupo BG_A com os pontos de distribuição DP_A1 e DP_A2 associados ao grupo
-   Grupo BG_B com os pontos de distribuição DP_B1 e DP_B2 associados ao grupo
-   Grupo BG_C com os pontos de distribuição DP_C1 e DP_C2 associados ao grupo

Você adiciona os locais de rede dos seus clientes como limites apenas para o grupo BG_A e, em seguida, configura relações daquele grupo de limites para os outros dois grupos de limites:
-   Você configura os pontos de distribuição para o primeiro grupo *vizinho* (BG_B) a ser usado depois de 10 minutos. Esse grupo contém os pontos de distribuição DP_B1 e DP_B2. Ambos estão bem conectadas aos primeiros locais de limite dos grupos.
-   Você configura o segundo grupo *vizinho* (BG_C) a ser usado depois de 20 minutos. Esse grupo contém os pontos de distribuição DP_C1 e DP_C2. Ambos estão em uma WAN dos outros dois grupos de limites.
-   Você também adiciona um ponto de distribuição que está localizado no servidor de site ao grupo de limites de site padrão dos sites. Esse é o local de fonte de conteúdo de menor preferência, mas está localizado centralmente para todos os seus grupos de limites.

    Exemplo de grupos de limites e tempos de fallback:

     ![BG_Fallack](media/BG_Fallback.png)


Com essa configuração:
-   O cliente inicia a pesquisa de conteúdo dos pontos de distribuição em seu grupo de limites *atual* (BG_A), pesquisando cada ponto de distribuição por dois minutos antes de alternar para o próximo ponto de distribuição no grupo de limites. O pool de clientes dos locais de fonte de conteúdo válidos incluem o DP_A1 e o DP_A2.
-   Se o cliente não conseguir localizar o conteúdo de seu grupo de limites *atual* depois de pesquisar por 10 minutos, ele adicionará os pontos de distribuição do grupo de limites BG_B à sua pesquisa. Então, ele continua a pesquisar o conteúdo de um ponto de distribuição em seu pool combinado de pontos de distribuição que agora inclui os dos grupos de limites BG_A e BG_B. O cliente continua a entrar em contato com cada ponto de distribuição por dois minutos antes de mudar para o próximo ponto de distribuição de seu pool. O pool de clientes dos locais de fonte de conteúdo válidos incluem DP_A1, DP_A2, DP_B1 e DP_B2.
-   Depois de mais 10 minutos (total de 20 minutos), se o cliente ainda não encontra um ponto de distribuição com o conteúdo, ele expande seu pool de pontos de distribuição disponíveis para os pontos do segundo grupo *vizinho*, o grupo de limites BG_C. O cliente agora tem 6 pontos de distribuição para pesquisar (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 e DP_C2) e continua a mudar para um novo ponto de distribuição a cada dois minutos até que o conteúdo seja encontrado.
-   Se o cliente não tiver encontrado conteúdo depois de um total de 120 minutos, ele realizará o fallback para incluir o *grupo de limites de site padrão* como parte de sua pesquisa contínua. Agora o pool de pontos de distribuição inclui todos os pontos de distribuição dos três grupos de limites configurados e o ponto de distribuição final localizado no computador do servidor do site.  O cliente continua, então, a pesquisa do conteúdo, alterando os pontos de distribuição a cada dois minutos até que o conteúdo seja encontrado.

Ao configurar os diferentes grupos vizinhos para estarem disponíveis em momentos diferentes, você controla quando pontos de distribuição específicos são adicionados como um local de fonte de conteúdo e quando, ou se, o cliente usa o fallback para o grupo de limites de site padrão como uma rede de segurança para o conteúdo que não está disponível em nenhum outro local.


### <a name="bkmk_update"></a>Atualizar grupos de limites existentes para o novo modelo
Quando você instala a versão 1609 e atualiza seu site, as configurações a seguir são feitas automaticamente. Elas devem garantir que o comportamento de fallback atual permaneça disponível, até que você configure novos grupos de limites e relações.  
-   Os pontos de distribuição não protegidos em um site são adicionados ao grupo de limites *Default-Site-Boundary-Group\<sitecode>* desse site.
-   É feita uma cópia de cada grupo de limites existente que inclui um servidor do site configurado com uma conexão lenta. O nome do novo grupo é ***\<nome do grupo de limites original>-Slow-Tmp***:  
    -   Os sistemas de sites que têm uma conexão rápida são deixados no grupo de limites original.
    -   Uma cópia dos sistemas de sites que têm uma conexão lenta são adicionadas à cópia do grupo de limites. Os sistemas de sites originais configurados como lentos permanecem no grupo de limites original para compatibilidade com versões anteriores, mas não são usados nesse grupo de limites.
    -   Esta cópia do grupo de limites não tem limites associados a ela. No entanto, um link de fallback é criado entre o grupo original e a nova cópia de grupo de limites que tem o tempo de fallback definido como zero.

 A tabela a seguir identifica o novo comportamento de fallback que você pode esperar da combinação das configurações de ponto a distribuição e as configurações de implantação originais:

A configuração de implantação original para "Não executar programa" na rede lenta  |A configuração do ponto de distribuição original para “Allow client to use a fallback source location for content” (Permitir que o cliente use um local de fonte de fallback para o conteúdo)  |Novo comportamento de fallback  
---------|---------|---------
Selecionada     |  Selecionada    |  **Sem fallback** – usar apenas os pontos de distribuição no grupo de limites atual       
Selecionada     |  Não selecionada|  **Sem fallback** – usar apenas os pontos de distribuição no grupo de limites atual       
Não selecionada |  Não selecionada|  **Fallback para o vizinho** – usar os pontos de distribuição no grupo de limites atual e, em seguida, adicionar os pontos de distribuição do grupo de limite vizinho. A menos que um link explícito para o grupo de limites de site padrão esteja configurado, os clientes não realizarão o fallback para esse grupo.    
Não selecionada | Selecionada     |   **Fallback normal** – usar pontos de distribuição no grupo de limites atual, em seguida, os dos grupos de limites vizinho e padrão de site

 Todas as outras configurações de implantação resultam em **Fallback normal**.  



## <a name="office-365-client-management-dashboard"></a>Painel de gerenciamento de clientes do Office 365  
O Technical Preview 1609 do Configuration Manager introduz um novo painel. Para exibir o painel, no console do Configuration Manager, vá até **Biblioteca de Software** > **Visão Geral** > **Gerenciamento de Cliente do Office 365**.
>[!NOTE]
>No espaço de trabalho **Novidades** no console do Configuration Manager, o novo painel está nomeado incorretamente como **Office 365 Servicing dashboard (Painel de serviços do Office 365)**.

O painel exibe gráficos para o seguinte:

- Número de clientes do Office 365
- Versões do cliente do Office 365
- Idiomas do cliente do Office 365
- Canais do cliente do Office 365     
Para mais informações, confira [Visão geral dos canais de atualização do Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx).
- Regras de implantação automática que têm o cliente do Office 365 selecionado no conjunto de produtos disponíveis.

Você pode executar as seguintes ações no painel:
- Na parte superior do painel, use a configuração suspensa **Coleção** para filtrar os dados do painel por membros de uma coleção específica.
- No canto superior direito do painel, clique em **Office 365 Installer (Instalador do Office 365)** para iniciar o Assistente de Instalação de Cliente do Office 365 para implantar aplicativos do Office 365 em clientes. Para obter detalhes, confira Implantar aplicativos do Office 365 em clientes [Implantar aplicativos do Office 365 em clientes](#deploy-office-365-apps-to-clients).
- Na parte intermediária direita do painel, clique em **Create an ADR (Criar um ADR)** para abrir o Assistente de Regra de Implantação Automática para criar uma nova ADR (regra de implantação automática). Para criar uma ADR para aplicativos do Office 365, selecione **Office 365 Client (Cliente do Office 365)** quando você escolher o produto. Para mais informações, confira [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates) (Implantar atualizações de software automaticamente).
- No canto inferior direito do painel, clique em **Create Client Agent Settings (Criar Configurações do Agente Cliente)** para abrir as configurações do Agente Cliente. Para obter mais informações, consulte [Sobre as configurações do cliente](/sccm/core/clients/deploy/about-client-settings).



Para mais informações sobre as atualizações do Office 365 ProPlus, confira [Manage Office 365 ProPlus updates with Configuration Manager](/sccm/sum/deploy-use/manage-office-365-proplus-updates) (Gerenciar atualizações do Office 365 ProPlus com o Configuration Manager).

## <a name="deploy-office-365-apps-to-clients"></a>Implantar aplicativos do Office 365 em clientes
Nessa versão, no painel de gerenciamento de clientes do Office 365, é possível iniciar o Instalador do Office 365 que permite que você defina as configurações de instalação do Office 365, baixe arquivos de CDNs (Redes de Distribuição de Conteúdo) do Office e implante os arquivos como um aplicativo no Configuration Manager.

### <a name="limitations-of-office-365-deployment"></a>Limitações de implantação do Office 365
- Você pode ter problemas ao tentar importar configurações do cliente (XML) existentes no Assistente de Instalação do Aplicativo do Office 365. Você pode definir manualmente as configurações do cliente sem problemas.

#### <a name="to-deploy-office-365-apps-to-clients"></a>Para implantar aplicativos do Office 365 em clientes
1. No console do Configuration Manager, navegue até **Biblioteca de Software** > **Visão Geral** > **Gerenciamento de Cliente do Office 365**.
2. Clique em **Office 365 Installer (Instalador do Office 365)** no painel superior direito. O Assistente de Instalação de Cliente do Office 365 é aberto.
3. Na página **Configurações de Aplicativo**, forneça um nome e uma descrição para o aplicativo, insira o local de download para os arquivos e clique em **Avançar**. Observe que o local deve ser especificado no formato &#92;&#92;*servidor*&#92;*compartilhamento*.
4. Na página **Import Client Settings (Importar Configurações do Cliente)**, escolha se deseja importar as configurações do cliente do Office 365 de um arquivo de configuração XML existente ou especificar as configurações manualmente e clique em **Avançar**.
Quando você tiver um arquivo de configuração existente, insira o local do arquivo e vá para a etapa 7. Observe que o local deve ser especificado no formato &#92;&#92;*servidor*&#92;*compartilhamento*&#92;*nome do arquivo*.XML.

    > [!IMPORTANT]
    >Você pode ter problemas ao tentar importar configurações do cliente (XML) existentes nesse technical preview.

5. Na página **Client Products (Produtos do Cliente)**, selecione o pacote do Office 365 usado, selecione os aplicativos que deseja incluir, selecione quaisquer produtos Office adicionais que devem ser incluídos e clique em **Avançar**.
6. Na página **Configurações do Cliente**, escolha as configurações a serem incluídas e clique em **Avançar**.
7. Na página **Implantação**, escolha se deseja implantar o aplicativo e clique em **Avançar**.
Se você optar por não implantar o pacote no assistente, vá para a etapa 9.
8. Configure o restante das páginas do assistente como você faria para uma implantação de aplicativo típica. Para mais informações, confira [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application) (Criar e implantar um aplicativo).
9. Conclua o assistente.
10. Você pode implantar ou editar o aplicativo exatamente como faria com qualquer outro aplicativo no Configuration Manager de **Biblioteca de Software** > **Visão Geral** > **Gerenciamento de Aplicativos** > **Aplicativos**.

>[!NOTE]
>Depois de implantar aplicativos do Office 365, você pode criar regras de implantação automática para manter os aplicativos. Para criar uma ADR para aplicativos do Office 365, clique em **Create an ADR (Criar um ADR)** e selecione **Office 365 Client (Cliente do Office 365)** quando você escolher o produto. Para mais informações, confira [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates) (Implantar atualizações de software automaticamente).

## <a name="BKMK_UEFIConversion"></a>Melhorias na conversão de BIOS para UEFI
Agora você pode personalizar uma sequência de tarefas de implantação do sistema operacional com uma nova variável, TSUEFIDrive, para que a etapa Reiniciar o Computador prepare uma partição FAT32 no disco rígido para a transição para UEFI. O procedimento a seguir fornece um exemplo de como você pode criar etapas de sequência de tarefas para preparar o disco rígido para a conversão de BIOS para UEFI.

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Para preparar a partição FAT32 para a conversão para UEFI:
Em uma sequência de tarefas existente para instalar um sistema operacional, você adicionará um novo grupo com etapa para realizar a conversão de BIOS para UEFI.

1. Crie um novo grupo de sequências de tarefas após as etapas para capturar arquivos e configurações e antes das etapas para instalar o sistema operacional. Por exemplo, crie um grupo após o grupo de **Capturar Arquivos e Configurações** denominado **BIOS-to-UEFI (BIOS para UEFI)**.
2. Na guia **Opções** do novo grupo, adicione uma nova variável de sequência de tarefas como uma condição em que **_SMSTSBootUEFI** é **diferente** de **true**. Isso impede que as etapas no grupo sejam executadas quando um computador já estiver no modo UEFI.
![Grupo BIOS to UEFI (BIOS para UEFI)](media/BIOS-to-UEFI-group.png)
3. No novo grupo, adicione a etapa de sequência de tarefas **Reiniciar Computador**. Em **Especifique o que executar após reiniciar**, selecione **The boot image assigned to this task sequence is selected (A imagem de inicialização atribuída a essa sequência de tarefas está selecionada)** para iniciar o computador no Windows PE.  
4. Na guia **Opções**, adicione uma variável de sequência de tarefa como uma condição em que **_SMSTSInWinPE equals false (_SMSTSInWinPE é igual a falso)**. Isso impede que esta etapa seja executada se o computador já estiver no Windows PE.

    ![Etapa Reiniciar Computador](media/Restart-in-Windows-PE.png)
5. Adicione uma etapa para iniciar a ferramenta de OEM que converterá o firmware de BIOS para UEFI. Isso geralmente será uma etapa de sequência de tarefas **Executar Linha de Comando** com uma linha de comando para iniciar a ferramenta de OEM.
5.  Adicione a etapa de sequência de tarefas Formatar e Particionar Disco que particionará e formatará o disco rígido. Na etapa, faça o seguinte:
    1.  Crie a partição FAT32 que será convertida em UEFI antes de o sistema operacional ser instalado. Escolha **GGT** para **Tipo de disco**.
    ![Etapa Formatar e particionar disco](media/Format-and-partition-disk.png)
    2.  Vá para as propriedades da partição FAT32. Digite **TSUEFIDrive** no campo **Variável**. Quando a sequência de tarefas detectar essa variável, ela preparará para a transição de UEFI antes de reiniciar o computador.
    ![Propriedades da partição](media/Partition-properties.png)
    3. Crie uma partição NTFS que o mecanismo de sequência de tarefas usa para salvar seu estado e para armazenar arquivos de log.
6.  Adicione a etapa de sequência de tarefas **Reiniciar Computador**. Em **Especifique o que executar após reiniciar**, selecione **The boot image assigned to this task sequence is selected (A imagem de inicialização atribuída a essa sequência de tarefas está selecionada)** para iniciar o computador no Windows PE.  




## <a name="intune-compliance-charts"></a>Gráficos de conformidade do Intune
Nesta versão, você pode obter uma exibição rápida da conformidade geral para dispositivos e os principais motivos para não conformidade usando novos gráficos no **Espaço de Trabalho de Monitoramento** no console do Configuration Manager.

#### <a name="to-view-the-intune-compliance-charts"></a>Para exibir os gráficos de conformidade do Intune
1. No console do Configuration Manager, acesse **Monitoramento** > **Visão Geral** > **Configurações de Conformidade**.
2. O gráfico **Overall Device Compliance (Conformidade Geral do Dispositivo)** é exibido.
3. Clique no nó **Políticas de Conformidade** para exibir os gráficos **Overall Device Compliance (Conformidade Geral do Dispositivo)** e **Top Non-Compliance Reasons (Principais motivos de não conformidade)**.

### <a name="limitations-of-intune-compliance-charts-in-tp-1609"></a>Limitações dos gráficos de conformidade do Intune na TP 1609
- No momento, a busca detalhada para o gráfico **Overall Device Compliance (Conformidade Geral do Dispositivo)** gera um erro.
- O gráfico **Top Non-Compliance Reasons (Principais motivos de não conformidade)** lista o nome da política e não os motivos de não conformidade individuais. Você pode clicar na política para fazer a busca detalhada e ver os dispositivos que não são compatíveis com essa política.

### <a name="try-it-out"></a>Experimente
Conclua as seções a seguir na ordem:

#### <a name="check-overall-compliance-chart"></a>Verificar o gráfico de conformidade geral
1. Adicione em duas políticas de conformidade do iOS no Configuration Manager. Uma política deve ter um conjunto de configurações para dispositivos (por exemplo, definir o comprimento do PIN para 6). A outra política deve ter outro conjunto de configurações (por exemplo, a complexidade do PIN). As configurações de política não devem se sobrepor ou estar em conflito.
2. Implante as duas políticas em um conjunto de usuários.
3. Registre dois dispositivos iOS no Intune usando a mesma conta de usuário e uma conta que recebeu as políticas na etapa anterior. Os dispositivos não devem atender aos critérios da política de conformidade.
4. No Configuration Manager, verifique o gráfico **Overall Device Compliance (Conformidade Geral do Dispositivo)**. Os dois dispositivos devem ser indicados com não compatíveis.
<!-- 5. Click the **Non-compliant** section of the chart. Both devices should appear in the filtered view under **Assets and Compliance** > **Overview** > **Device**. -->

#### <a name="check-the-top-non-compliance-reasons-chart"></a>Verificar o gráfico Top Non-compliance Reasons (Principais motivos de não conformidade)
5. Verifique o gráfico **Top Non-compliance Reasons (Principais motivos de não conformidade)**. Este gráfico lista os cinco principais motivos de não conformidade, mas quando apenas duas configurações de conformidade foram definidas em políticas, apenas os dois principais motivos de não conformidade são exibidas.
6. Clique em uma das seções no gráfico. Os dois dispositivos devem aparecer na exibição filtrada em **Ativos e Conformidade** > **Visão Geral** > **Dispositivo**.

#### <a name="make-devices-compliant-and-check-the-charts"></a>Tornar os dispositivos compatíveis e verificar os gráficos
7. Tore um dos dispositivos compatível com uma das políticas. Verifique o gráfico **Overall Device Compliance (Conformidade Geral do Dispositivo)** novamente. O gráfico deve exibir um dispositivo compatível e um dispositivo não compatível.
8. Torne o outro dispositivo compatível com a mesma política. Isso tornará um dispositivo compatível com as duas políticas e um dispositivo compatível com apenas uma das políticas.
9. Verifique o gráfico **Top Non-compliance Reasons (Principais motivos de não conformidade)**. Deve haver apenas um motivo de não conformidade listado.
<!--7. Click the **Compliant** section of the chart. Only the compliant device should appear in the filtered view. -->





## <a name="see-also"></a>Consulte também
[Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md)
