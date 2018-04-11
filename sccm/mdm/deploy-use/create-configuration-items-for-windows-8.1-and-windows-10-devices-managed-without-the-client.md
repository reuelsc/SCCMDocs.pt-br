---
title: Criar itens de configuração para dispositivos Windows 8.1 e Windows 10 gerenciados com o Intune
titleSuffix: Configuration Manager
description: Use o item de configuração do Windows 10 do System Center Configuration Manager para gerenciar as configurações de computadores Windows 10.
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 23e1e4dc-623a-4521-ad04-ae9482927097
caps.latest.revision: 20
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 7f5a50ae6ea05af7e864cf94df3063d70bd737b4
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="how-to-create-configuration-items-for-windows-81-and-windows-10-devices-managed-without-the-system-center-configuration-manager-client"></a>Como criar itens de configuração para dispositivos Windows 8.1 e Windows 10 gerenciados sem o cliente do System Center Configuration Manager

  
 Use o item de configuração do **Windows 8.1 e Windows 10** do System Center Configuration Manager para gerenciar as configurações para dispositivos Windows 8.1 e Windows 10 que estão registrados no Microsoft Intune ou são gerenciados localmente pelo Configuration Manager.  
  
### <a name="to-create-a-windows-81-and-windows-10-configuration-item"></a>Para criar um item de configuração do Windows 8.1 e Windows 10  
  
1.  No console do Configuration Manager, clique em **Ativos e conformidade**.  
  
2.  No espaço de trabalho **Ativos e Conformidade** , expanda **Configurações de Conformidade**e clique em **Itens de Configuração**.  
  
3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Item de Configuração**.  
  
4.  Na página **Geral** do **Assistente para Criar Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.  
  
5.  Em **Especificar o tipo de item de configuração que deseja criar**, selecione **Windows 8.1 e Windows 10**.  
  
6.  Se você criar e atribuir categorias, clique em **Categorias** para ajudá-lo a pesquisar e filtrar itens de configuração no console do Configuration Manager.  
  
7.  Na página **Plataformas com Suporte** do assistente, selecione as plataformas específicas do Windows que avaliará o item de configuração.  
  
8.  Na página **Configurações do Dispositivo** do assistente, selecione o grupo de configurações que deseja configurar. Veja [Referência de configurações do item de configuração do Windows 8.1 e Windows 10](#BKMK_Setref) neste tópico para obter detalhes e clique **Avançar**.  
  
    > [!TIP]  
    >  Se a configuração desejada não estiver na lista, marque a **caixa de seleção Definir configurações adicionais que não estão nos grupos de configuração padrão**.  
  
9. Em cada página de configurações, defina as configurações necessárias e se deseja corrigi-las quando não forem compatíveis nos dispositivos (quando houver suporte para essa opção).  
  
10. Para cada grupo de configurações, você também pode configurar a gravidade relatada quando um item de configuração for considerado não compatível de:  
  
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
  
##  <a name="windows-81-and-windows-10-configuration-item-settings-reference"></a>Referência de configurações do item de configuração do Windows 8.1 e Windows 10  
  
### <a name="password"></a>Senha  
 Essas configurações são destinadas somente a dispositivos que executam o Windows 10 e posteriores.  
  
|Configuração|Detalhes|  
|-------------|-------------|  
|**Exigir configurações de senha em dispositivos**|Requer uma senha nos dispositivos com suporte.|  
|**Comprimento mínimo da senha (caracteres)**|O comprimento mínimo da senha.|  
|**Validade da senha em dias**|O número de dias antes que uma senha precise ser alterada.|  
|**Número de senhas lembradas**|Impede a reutilização de senhas usadas anteriormente.|  
|**Número de tentativas de logon com falha antes de o dispositivo ser apagado**|Apaga o dispositivo se houver falha neste número de tentativas de logon.|  
|**Tempo ocioso antes que o dispositivo móvel seja bloqueado**|Especifique o período de tempo que um dispositivo pode ficar ocioso (sem entrada do usuário) antes de ser bloqueado.|  
|**Complexidade da senha**|Escolha se é possível especificar um PIN como “1234” ou se é necessário fornecer uma senha forte.|  
|**Qualidade da senha**|Selecione o nível necessário de complexidade de senha e também se dispositivos biométricos podem ser usados.|  
|**Enviar PIN de recuperação de senha ao Exchange Server**|-|
|**Criptografia de dispositivo**|Habilite a criptografia em dispositivos de destino.|  
  
###  <a name="device"></a>Dispositivo  
  
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Captura de tela**|Permite tirar uma captura de tela da tela do dispositivo.<br /><br /> (somente Windows 10)|  
|**Envio de dados de diagnóstico**|Permita o envio de arquivos de log do aplicativo.<br /><br /> (somente Windows 8.1)|  
|**Envio de dados de diagnóstico (Windows 10)**|Permita o envio de arquivos de log do aplicativo.<br /><br /> (somente Windows 10)|  
|**Localização geográfica**|Permita que o dispositivo use informações de serviços de localização.<br /><br /> (somente Windows 10)|  
|**Copiar e colar**|Use copiar e colar para transferir dados entre aplicativos.<br /><br /> (somente Windows 10)|
|**Redefinição de fábrica**|Permite que o usuário final redefina o dispositivo para suas configurações iniciais.<br /><br /> (somente Windows 10)|  
|**Bluetooth**|Permita o uso da funcionalidade Bluetooth dos dispositivos.|  
|**Modo detectável do Bluetooth**|Permitir que o dispositivo seja descoberto por outros dispositivos Bluetooth.<br /><br /> (somente Windows 10)|  
|**Anúncios do Bluetooth**|Permita o uso de anúncio de Bluetooth.<br /><br /> (somente Windows 10)|  
|**Gravação de voz**|Permitir o uso dos recursos de gravação de voz do dispositivo.<br /><br /> (somente Windows 10)|
|**Cortana**|Permite o uso do assistente de voz Cortana.<br /><br /> (somente Windows 10)|
|**Notificações da central de ações**|Habilitar ou desabilitar o painel de notificações no Windows 10. <br /><br /> (somente Windows 10)|
|**Modificação das configurações de região (somente desktop)**|Impede que o usuário final altere as configurações de região no dispositivo.|
|**Modificação das configurações de energia e suspensão (somente desktop)**|Impede que o usuário final altere as configurações de energia e suspensão no dispositivo.|
|**Modificação das configurações de idioma (somente desktop)**|Impede que o usuário altere as configurações de idioma no dispositivo.|
|**Modificação do horário do sistema**|Impede que o usuário final altere a data e hora do dispositivo.|
|**Modificação do nome do dispositivo**|Impede que o usuário final altere o nome do dispositivo.|
  
### <a name="email-management"></a>Gerenciamento de email  
 Essas configurações são destinadas a dispositivos que executam o Windows 8.1 e o Windows 10.  
  
|Configuração|Detalhes|  
|-------------|-------------|  
|**Email POP e IMAP**|Permite a conexão a contas de email que usam os padrões POP e IMAP.|  
|**Tempo máximo para manter o email**|A duração de tempo que o email será mantido antes de ser excluído do servidor.|  
|**Formatos de mensagens permitidos**|Especifique se os emails do usuário podem ser em HTML ou somente em texto sem formatação.|  
|**Tamanho máximo de email de texto sem formatação (baixado automaticamente)**|Controla o tamanho máximo de emails com texto sem formatação quando baixados automaticamente.|  
|**Tamanho máximo para email HTML (baixado automaticamente)**|Controla o tamanho máximo de emails em HTML quando baixados automaticamente.|  
|**Tamanho máximo de um anexo (baixado automaticamente)**|Configura o tamanho máximo do email baixado automaticamente.|  
|**Sincronização de calendário**|Permita a sincronização de calendários com o dispositivo.|  
|**Conta de email personalizada**|Permita o uso de uma conta que não seja da Microsoft no dispositivo.|  
|**Tornar a Conta da Microsoft opcional no aplicativo de email do Windows**|Configure essa definição para remover o requisito de uma conta da Microsoft no Windows Mail.|  
  
### <a name="store"></a>Repositório  
 Essas configurações são destinadas somente a dispositivos que executam o Windows 10 e posteriores.  
  
|Configuração|Detalhes|  
|-------------|-------------|  
|**Armazenamento de aplicativos**|Permite o acesso a loja de aplicativos no dispositivo.|  
|**Digite uma senha para acessar o armazenamento de aplicativos**|Os usuários devem digitar uma senha para acessar a loja de aplicativos.|  
|**Compras no aplicativo**|Permite que os usuários façam compras no aplicativo.|
|**Atualização automática de aplicativos da store**|Permite que aplicativos instalados da Windows Store sejam atualizados automaticamente.|
|**Usar somente armazenamento particular**|Habilite esta opção para permitir que somente os usuários finais façam download de aplicativos de seu repositório particular.|
|**Inicialização de aplicativo proveniente do armazenamento**|Usado para desabilitar todos os aplicativos que foram previamente instalados no dispositivo ou baixados da Windows Store.|
  
### <a name="browser"></a>Navegador  
 Essas configurações são destinadas a dispositivos que executam o Windows 8.1 e o Windows 10.  
  
|Configuração|Detalhes|  
|-------------|-------------|  
|**Permitir navegador da Web**|Permita o uso do navegador da Web no dispositivo.|  
|**Preenchimento automático**|O usuário pode alterar as configurações de preenchimento automático no navegador.|  
|**Script ativo**|O navegador pode executar scripts, como scripts do ActiveX.|  
|**Plug-ins**|O usuário pode adicionar plug-ins ao Internet Explorer.|  
|**Bloqueador de pop-up**|Habilita ou desabilita o bloqueador de pop-ups do navegador.|  
|**Cookies**|Permita que os cookies sejam salvos no dispositivo.|  
|**Aviso de fraude**|Habilite ou desabilite avisos de sites fraudulentos potenciais.|  
  
###  <a name="internet-explorer"></a>Internet Explorer  
 Essas configurações são destinadas a dispositivos que executam o Windows 8.1 e o Windows 10.  
  
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Sempre enviar cabeçalho Não Acompanhar**|Impede que as informações de navegação sejam enviadas para sites de terceiros.|  
|**Zona de segurança da Intranet**|Atribua um nível de segurança à zona de segurança da Intranet.|  
|**Nível de segurança para a zona da Internet**|Configure o nível de segurança para a zona da Internet.|  
|**Nível de segurança para zona da intranet**|Configure o nível de segurança para a zona da intranet.|  
|**Nível de segurança para a zona de sites confiáveis**|Configure o nível de segurança para a zona de sites confiáveis.|  
|**Nível de segurança para a zona de sites restritos**|Configure o nível de segurança para a zona de sites restritos.|  
|**Namespaces para a zona da intranet**|Configure sites que são adicionados ou removidos da zona da intranet.|  
|**Ir para um site da intranet por uma entrada de palavra única**|Habilita ou desabilita a configuração que permite que o Internet Explorer acesse automaticamente um site de Intranet se um nome de site válido for inserido sem um HTTP precedente:|  
|**Opção de menu do Modo Empresarial**|Permita que os usuários ativem e desativem o modo Empresarial no menu **Ferramentas** do Internet Explorer.|  
|**Local do relatório de registro em log (URL)**|Especifique uma URL na qual os sites visitados serão registrados quando o Modo Empresarial estiver ativo.|  
|**Local da lista do site do modo Empresarial (URL)**|Especifique o local da lista de sites que usam o Modo Empresarial quando ele estiver ativo.|  
  
###  <a name="cloud"></a>Nuvem  
 Essas configurações são destinadas a dispositivos que executam o Windows 8.1 e o Windows 10.  
  
|Nome da configuração|Detalhes|Windows 8.1|Windows 10|  
|------------------|-------------|-----------------|----------------|  
|**Sincronização de configurações**|Permite a sincronização de configurações entre dispositivos.|Sim|Sim|  
|**Sincronização de credenciais**|Permite a sincronização de credenciais entre dispositivos.|Sim|Sim|  
|**Conta da Microsoft**|Permita o uso de uma conta da Microsoft no dispositivo.|Sim|Sim|  
|**Sincronização de configurações em conexões medidas**|Permita que as configurações sejam sincronizadas durante a medição da conexão com a Internet.|Sim|Sim|  
  
###  <a name="security"></a>Segurança  
  
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Instalação de arquivo não assinado**|Permite o carregamento de arquivos não assinados.<br /><br /> (somente Windows 10)|  
|**Aplicativos não assinados**|Permite o carregamento de aplicativos não assinados.<br /><br /> (somente Windows 10)|  
|**Mensagens SMS e MMS**|Permita mensagens SMS e MMS do dispositivo.<br /><br /> (somente Windows 10)|  
|**Armazenamento removível**|Permita o uso de armazenamento removível, como um cartão SD, no dispositivo.<br /><br /> (somente Windows 10)|  
|**Câmera**|Permita o uso da câmera do dispositivo.<br /><br /> (somente Windows 10)|  
|**Comunicação a curta distância (NFC)**|Permita a comunicação usando a NFC no dispositivo.<br /><br /> (somente Windows 10)|  
|**Modo AntiTheft**|Controla se o modo AntiTheft do Windows 10 é habilitado.<br /><br /> (somente Windows 10)|  
|**Permitir conexão USB**|Permite que os dispositivos se conectem a esse dispositivo usando uma conexão USB.<br /><br /> (somente Windows 10)|
|**Arquivo de perfil**|Provisiona um perfil de VPN para dispositivos com Windows RT.<br /><br /> somente Windows 8.1)|  
|**Nome do perfil**|Provisiona um perfil de VPN para dispositivos com Windows RT.<br /><br /> somente Windows 8.1)|  
|**Perfil de todos os usuários**|Provisiona um perfil de VPN para dispositivos com Windows RT.<br /><br /> somente Windows 8.1)|  
  
###  <a name="peak-synchronization"></a>Sincronização em horário de pico  
 Essas configurações são destinadas somente a dispositivos que executam o Windows 10 e posteriores.  
  
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Especificar o horário de pico**|Configure o horário de pico para sincronização de dispositivo móvel.|  
|**Frequência de sincronização no horário de pico**|Configure com que frequência a sincronização ocorrerá durante os horários de pico que você configurou.|  
|**Frequência de sincronização fora do horário de pico**|Configure com que frequência a sincronização ocorrerá fora dos horários de pico que você configurou.|  
  
###  <a name="roaming"></a>Roaming  
  
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Gerenciamento de dispositivos durante roaming**|Permite que o dispositivo seja gerenciado pelo Configuration Manager durante o roaming.<br /><br /> (somente Windows 10)|  
|**Download de software durante roaming**|Permite o download de aplicativos e software durante o roaming.<br /><br /> (somente Windows 10)|  
|**Download de emails durante roaming**|Permite downloads de email durante o roaming.<br /><br /> (somente Windows 10)|  
|**Roaming de dados**|Permita o roaming entre redes durante o acesso de dados.| 
|**VPN por celular**|Permite que o dispositivo acesse as conexões VPN enquanto estão conectados a uma rede de celular.<br /><br /> (somente Windows 10)|
|**Roaming de VPN no celular**|Permite que o dispositivo acesse as conexões VPN enquanto estão em roaming em uma rede de celular.<br /><br /> (somente Windows 10)| 
  
###  <a name="encryption"></a>Criptografia  
  
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Criptografia de cartão de memória**|Requer que todos os cartões de armazenamento usados com o dispositivo sejam criptografados.<br /><br /> (somente Windows 10)|  
|**Criptografia de arquivo no dispositivo**|Exige que os arquivos no dispositivo sejam criptografados.|  
|**Exigir assinatura de email**|Exige que os emails sejam assinados antes de ser enviados.|  
|**Algoritmo de assinatura**|Selecione o algoritmo de assinatura para os emails assinados.|  
|**Exigir criptografia de email**|Exige que os emails sejam criptografados antes de ser enviados.|  
|**Algoritmo de criptografia**|Selecione o algoritmo para criptografar emails.|  
  
###  <a name="wireless-communications"></a>Comunicações sem fio  
 Essas configurações são destinadas somente a dispositivos que executam o Windows 10 e posteriores.  
  
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Conexão de rede sem fio**|Habilite ou desabilite a funcionalidade de Wi-Fi dos dispositivos.|  
|**Compartilhamento da Internet por Wi-Fi**|Permite que os usuários usem seus dispositivos como um ponto de acesso móvel.|  
|**Descarregar dados para Wi-Fi quando possível**|Configure essa opção para usar a conexão Wi-Fi no dispositivo quando possível.|  
|**Relatórios de ponto de acesso Wi-Fi**|-|  
|**Configuração manual de Wi-Fi**|-|  
  
#### <a name="to-configure-a-wireless-network-connection"></a>Para configurar uma conexão de rede sem fio  
  
1.  Na página **Definir configurações de comunicação sem fio de dispositivos móveis** clique em **Adicionar**.  
  
2.  Na caixa de diálogo **Conexão de Rede Sem Fio**, especifique as seguintes informações sobre a conexão sem fio provisionada nos dispositivos móveis:  
  
|Configuração|Mais informações|  
|-------------|----------------------|  
|**Nome da rede (SSID)**|Insira o nome da rede Wi-Fi.|  
|**Conexão de rede**|Escolha **Internet** ou **Trabalho**.|  
|**Autenticação**|Escolha o método de autenticação para a conexão sem fio do:<br /><br /> - **Aberto**<br /><br /> - **Compartilhado**<br /><br /> - **WPA**<br /><br /> - **WPA-PSK**<br /><br /> - **WPA2**<br /><br /> - **WPA2-PSK**|  
|**Criptografia de dados**|Escolha o método de criptografia usado por esta conexão. Os valores que podem ser selecionados são diferentes dependendo do método de **Autenticação** selecionado:<br /><br /> - **Desabilitado**<br /><br /> - **WEP**<br /><br /> - **TKIP**<br /><br /> - **AES**|  
|**Índice de chave**|Selecione um índice de chave de **1** a **4** que será usado com uma configuração de **Criptografia de dados** de **WEP**.|  
|**Esta rede se conecta à Internet**|Selecione esta opção se desejar fornecer configurações de proxy que permitem que dispositivos móveis em uma conexão sem fio se conectem à Internet.|  
|**Configurações do servidor proxy**|Especifique, conforme necessário, as configurações de **Servidor** e **Porta** para **HTTP**, **WAP** e **Soquetes**.|  
|**Habilitar acesso à rede 802.1X**|Selecione esta opção se desejar proteger a conexão com a especificação de um tipo de EAP.|  
|**Tipo de EAP**|Escolha o tipo de EAP a ser usado do:<br /><br /> - **PEAP**<br> - **Cartão inteligente ou certificado**|  
  
  
  
### <a name="certificates"></a>Certificados  
 Permite importar certificados a serem instalados em dispositivos móveis.  
  
 Clique em **Importação**e especifique os seguintes valores:  
  
-   **Arquivo de certificado** – Clique em Procurar e selecione o arquivo de certificado com a extensão **.cer** que deseja importar.  
  
-   **Repositório de destino** – Escolha um ou mais repositórios de destino nos quais o certificado importado será adicionado ao dispositivo móvel de:  
  
    -   **Root**  
  
    -   **AC**  
  
    -   **Normal**  
  
    -   **Com privilégios**  
  
    -   **SPC**  
  
    -   **Par**  
  
-   **Função** – Se **SPC** (Certificado do Fornecedor de Software) estiver selecionado como o repositório de destino, escolha a função que será associada ao certificado por meio de:  
  
    -   **Operador Móvel**  
  
    -   **Gerenciador**  
  
    -   **Usuário autenticado**  
  
    -   **Administrador de TI**  
  
    -   **Usuário não autenticado**  
  
    -   **Servidor de provisionamento confiável**  
  
### <a name="system-security"></a>Segurança do sistema  
  
|Configuração|Detalhes|  
|-------------|-------------|  
|**Controle de conta de usuário**|Habilita ou desabilita o Controle de Conta de Usuário do Windows no dispositivo.|  
|**Firewall da rede**|Habilita ou desabilita o Firewall do Windows.<br /><br /> (somente Windows 8.1)|  
|**Atualizações (Windows 8.1 e anterior)**|Escolha como as atualizações de software do Windows são baixadas nos computadores. Por exemplo, é possível baixar automaticamente as atualizações, mas permitir que o usuário escolha quando instalá-las.|  
|**Classificação mínima de atualizações**|Escolha a classificação mínima das atualizações baixadas nos computadores com Windows: **Nenhuma**, **Importante**ou **Recomendada**.|  
|**Atualizações (Windows 10)**|Escolha como as atualizações de software do Windows são baixadas nos computadores. Por exemplo, é possível baixar automaticamente as atualizações, mas permitir que o usuário escolha quando instalá-las.<br /><br /> (somente Windows 10)|  
|**Dia de instalação**|Escolha o dia de instalação das atualizações.<br /><br /> (somente Windows 10)|  
|**Hora de instalação**|Escolha a hora de instalação das atualizações.<br /><br /> (somente Windows 10)|  
|**SmartScreen**|Habilite ou desabilite a Tela Inteligente do Windows.|  
|**Proteção contra vírus**|Selecione esta opção para garantir que o software antivírus está instalado no dispositivo.|  
|**As assinaturas de proteção contra vírus estão atualizadas**|Selecione esta opção para garantir que os arquivos de assinatura de antivírus estão atualizados.|  
|**Recursos de pré-lançamento**|Permite que a Microsoft implante configurações e recursos de pré-lançamento no dispositivo.<br /><br /> (somente Windows 10)|  
|**Instalação manual de certificado raiz**|(somente Windows 10)| 
|**Permitir cancelamento de registro manual**|Permite que o usuário cancelar seu próprio registro de gerenciamento por uma solução MDM.| 
  
###  <a name="windows-server-work-folders"></a>Pastas de Trabalho do Windows Server  
 Essas configurações são destinadas a dispositivos que executam o Windows 8.1 e o Windows 10.  
  
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**URL de pastas de trabalho**|Configura o local de uma pasta de trabalho do Windows Server com as qual os usuários podem se conectar por meio de seus dispositivos.|  
  
### <a name="allowed-and-blocked-apps-windows-phone-only"></a>Aplicativos permitidos e bloqueados (somente no Windows Phone)  
 Permite especificar uma lista de aplicativos gerenciados pelo Intune que são compatíveis ou não compatíveis em sua empresa. O Windows Phone pode permitir ou bloquear a instalação desses aplicativos.  
  
 Não é possível especificar aplicativos compatíveis e não compatíveis no mesmo item de configuração.  
  
#### <a name="to-specify-apps-that-are-allowed-or-blocked"></a>Para especificar os aplicativos que serão permitidos ou bloqueados  
  
Na página **Lista de Aplicativos Permitidos e Bloqueados**, especifique as seguintes informações:  
  
|Configuração|Mais informações|  
    |-------------|----------------------|  
    |**Lista de aplicativos bloqueados**|Escolha essa opção se quiser especificar uma lista de aplicativos que os usuários não têm permissão para instalar.|  
    |**Lista de aplicativos permitidos**|Selecione esta opção se desejar especificar uma lista de aplicativos que os usuários têm permissão para instalar. Qualquer outro aplicativo será impedido de ser instalado.|  
    |**Adicionar**|Adiciona um aplicativo à lista selecionada. Especifique um nome da sua preferência, opcionalmente o editor do aplicativo, e a URL para o aplicativo na loja de aplicativos.<br /><br /> Para especificar a URL, na Windows Store, procure o aplicativo que você quer usar.<br /><br /> Abra a página do aplicativo e copie a URL para a área de transferência. Agora você pode usar isso como a URL em uma lista de aplicativos permitidos ou bloqueados.<br /><br /> **Exemplo:** pesquise o aplicativo **Skype** na loja. A URL usada é **http://www.windowsphone.com/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51**.|  
    |**Editarar**|Permite editar o nome, editor e a URL do aplicativo selecionado.|  
    |**Removerr**|Exclui o aplicativo selecionado da lista.|  
    |**Importarar**|Importa uma lista dos aplicativos que você especificou em um arquivo de valores separados por vírgulas. Use o formato, nome do aplicativo, editor e a URL do aplicativo no arquivo.|  
  
### <a name="windows-10-team"></a>Windows 10 Team  
 Essas configurações são destinadas somente a dispositivos que executam o Windows 10 Team.  
  
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Permitir que a tela seja ativada automaticamente quando sensores detectarem alguém na sala**|Permite que o dispositivo seja ativado automaticamente quando o sensor detectar a alguém na sala.|  
|**PIN exigido para projeção sem fio**|Especifica se você deve inserir um PIN antes de poder usar os recursos de projeção sem fio do dispositivo.|  
|**Janela de Manutenção**|Configura a o intervalo em que atualizações podem ocorrer no dispositivo. Você pode configurar a hora de início do intervalo e sua duração (de 1 a 5 horas).|
|**Azure Operational Insights**|O Azure Operational Insights, parte do pacote Microsoft Operations Manager coleta, armazena e analisa os dados de arquivo de log de dispositivos do Windows 10 Team.<br>Para conectar-se ao Azure Operational Insights, especifique uma ID de Espaço de Trabalho e uma Chave de Espaço de Trabalho.| 
|**Projeção sem fio Miracast**|Habilite esta opção se você quiser permitir que o dispositivo Windows 10 Team use dispositivos habilitados para Miracast para o projeto.<br>Se você habilitar essa opção, em **Escolher canal Miracast**, selecione o canal do Miracast usado para o conteúdo do projeto.|
|**Informações sobre a reunião exibidas na tela de boas-vindas**|Se você habilitar essa opção, escolha as informações que serão exibidas no bloco **Reuniões** da tela de **Boas-Vindas**. Você pode:<br><br>- **Mostrar somente organizador e hora**<br>- **Mostrar organizador, hora e entidade (a entidade é oculta para reuniões particulares)**|
|**URL da imagem de tela de fundo da tela de bloqueio**|Use essa configuração para exibir um plano de fundo personalizado na tela **Boas-Vindas** dos dispositivos com Windows 10 Team a partir da URL especificada.<br>A imagem deve estar no formato PNG, e a URL deve começar com **https://**.| 
  
### <a name="windows-information-protection"></a>Windows Information Protection  

Com o aumento do uso de dispositivos de funcionário dentro da empresa, aumenta também o risco de vazamentos acidentais de dados por meio de aplicativos e serviços, como email, mídia social e nuvem pública, que estão fora do controle da empresa. Por exemplo, quando um funcionário envia as imagens mais recentes de engenharia da sua conta de email pessoal, copia e cola informações do produto em um tweet ou salva um relatório de vendas em andamento no armazenamento de nuvem pública.

A WIP (Proteção de Informações do Windows) ajuda a proteger contra possíveis vazamentos de dados sem interferir de outras formas na experiência do funcionário. A WIP também ajuda a proteger dados e aplicativos corporativos contra vazamento acidental de dados em dispositivos corporativos e dispositivos pessoais que os funcionários levam para o trabalho, sem a necessidade de que sejam feitas alterações em seu ambiente ou em outros aplicativos.

 Os itens de configuração da WIP do Configuration Manager gerenciam a lista de aplicativos protegidos pela WIP, os locais de rede corporativa, o nível de proteção e as configurações de criptografia.

Para obter informações sobre como configurar a proteção de dados empresariais com o Configuration Manager, consulte [Proteger os dados da empresa usando a WIP (Proteção de Informações do Windows)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip).


### <a name="microsoft-edge"></a>Microsoft Edge  
Essas configurações são destinadas a dispositivos que executam o Windows 10 e posteriores.  
  
|Nome da configuração|Detalhes|  
|------------------|-------------| 
|Microsoft Edge|Permita o uso do navegador da Web Edge no dispositivo.| 
|**Permitir sugestões de pesquisa na barra de endereços**|Permite que o mecanismo de pesquisa sugira sites à medida que você digita as frases da pesquisa.|  
|**Permitir envio de tráfego de intranet no Internet Explorer**||  
|**Permitir Não Rastrear**|Não rastreia informações de sites quando você não quer que rastreiem sua visita a um site.|  
|**Habilitar SmartScreen**|Use o SmartScreen para verificar se os arquivos que os usuários baixam não contêm código mal-intencionado.|  
|**Permitir pop-ups**|Permita ou desabilite os pop-ups do navegador.|  
|**Permitir cookies**|Permita ou desabilite cookies.|  
|**Permitir Preenchimento Automático**|Permita o uso do recurso Autopreenchimento do navegador Microsoft Edge.|  
|**Permitir Gerenciador de Senhas**|Permita o uso do recurso gerenciador de senha do navegador Microsoft Edge.|  
|**Local da lista de sites do Modo Empresarial**|Especifica onde encontrar a lista de sites que abre no modo Empresarial. Os usuários não podem editar essa lista.|
|**Bloquear o acesso à página about:flags**|Impeça o usuário final de acessar a página about:flags no Microsoft Edge que contém configurações experimentais e de desenvolvedor.|
|**Substituição de prompt SmartScreen**|Permitir que o usuário final ignore os avisos de filtro SmartScreen sobre sites mal-intencionados.|
|**Substituição de prompt SmartScreen para arquivos**|Permitir que o usuário final ignore os avisos de filtro SmartScreen sobre o download de arquivos mal-intencionados.|
|**Endereço IP do localhost WebRTC**|Bloqueie a exibição do endereço IP do localhost dos usuários ao fazer chamadas telefônicas usando a protocolo RTC da Web.|
|**Mecanismo de pesquisa padrão**|Especifique o mecanismo de pesquisa padrão a ser usado. Os usuários finais podem alterar esse valor a qualquer momento.|
|**URL de XML OpenSearch**|Você pode usar um arquivo XML de OpenSearch para criar um serviço de pesquisa para o Microsoft Edge.<br>Para obter mais detalhes, confira [OpenSearch](https://msdn.microsoft.com/library/windows/desktop/dd940337).|
|**Home pages (somente desktop)**|Adicione uma lista de sites que você deseja usar como home pages no navegador Microsoft Edge (somente no desktop).|  


### <a name="windows-defender"></a>Windows Defender
Essas configurações são destinadas a dispositivos que executam o Windows 10 e posteriores.
 
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Permitir monitoramento em tempo real**|Habilita a verificação em tempo real de malware, spyware e outros softwares indesejados.|
|**Permitir o monitoramento de comportamento**|Permite que o Defender verifique se há certos padrões conhecidos de atividade suspeita nos dispositivos.|
|**Habilitar o Sistema de Inspeção de Rede**|O NIS (Sistema de Inspeção de Rede) ajuda a proteger dispositivos contra explorações baseadas em rede usando as assinaturas de vulnerabilidades conhecidas do Microsoft Endpoint Protection Center para ajudar a detectar e bloquear tráfego mal-intencionado.|
|**Verificar todos os downloads**|Controla se o Defender examina todos os arquivos baixados da Internet.|
|**Permitir a verificação de script**|Permite que o Defender verifique os scripts que são usados no Internet Explorer.|
|**Monitorar a atividade de arquivo e programa**|Permite que o Defender monitore a atividade de arquivos e programas em dispositivos.
|**Dias para acompanhar malwares resolvidos**|Permite que o Defender continue acompanhando malwares resolvidos durante o número de dias especificado, para que você possa verificar manualmente os dispositivos afetados previamente. Se você definir o número de dias como 0, o malware permanecerá na pasta Quarentena e não será removido automaticamente.|
|**Permitir acesso à interface de usuário do cliente**|Controla se a interface de usuário do Windows Defender fica oculta dos usuários.<br>Quando essa configuração for alterada, ele entrará em vigor na próxima vez que o computador do usuário for reiniciado.|
|**Agendar uma verificação do sistema**|Permite o agendamento de uma verificação completa ou rápida do sistema, que ocorre regularmente no dia e hora selecionados.|
|**Agendar uma verificação rápida diária**|Permite o agendamento de uma verificação rápida que ocorre diariamente no momento selecionado
|**Limitar o uso da CPU durante uma verificação**|Permite a limitação da quantidade de CPU que as verificações têm permissão para usar (de 1 a 100).|
|**Verificar arquivos mortos**|Permite que o Defender examine arquivos mortos armazenados, como arquivos .zip ou .cab.|
|**Verificar mensagens de email**|Permite que o Defender verifique mensagens de email assim que elas chegam no dispositivo.|
|**Verificar unidades removíveis**|Permite que o Defender verifique unidades removíveis, como cartões USB.|
|**Verificar unidades mapeadas**|Permite que o Defender verifique arquivos nas unidades de rede mapeadas.<br>Se os arquivos na unidade forem somente leitura, o Defender não poderá remover qualquer malware encontrado neles.|
|**Verificar arquivos abertos em pastas de rede compartilhadas**|Permite que o Defender verifique arquivos em unidades de rede compartilhadas (por exemplo, aquelas acessadas de um caminho UNC)<br>Se os arquivos na unidade forem somente leitura, o Defender não poderá remover qualquer malware encontrado neles.|
|**Intervalo de atualização de assinatura**|Especifica o intervalo de verificação usado pelo Defender para procurar novos arquivos de assinatura.
|**Permitir proteção da nuvem**|Permite ou bloqueia o Microsoft Active Protection Service de receber informações sobre a atividade de malware de dispositivos gerenciados. Essas informações são usadas para aprimorar o serviço no futuro.|
|**Solicitar aos usuários o envio de amostras**|Controla se os arquivos que podem exigir mais análise para determinar se são mal-intencionados são enviados automaticamente à Microsoft.|
|**Detecção de aplicativos potencialmente indesejados**|Proteger os dispositivos de área de trabalho do Windows registrados contra a execução de software classificado pelo Windows Defender como potencialmente indesejados. Você pode se proteger contra a execução desses aplicativos, ou usar o modo de auditoria para informar quando um aplicativo potencialmente indesejado for instalado.|
|**Exclusões de arquivos e pastas**|Adicione um ou mais arquivos e pastas como C:\Path ou %ProgramFiles%\Path\filename.exe à lista de exclusões. Esses arquivos e pastas não serão incluídos em verificações em tempo real ou programadas.|
|**Exclusões de extensão de arquivo**|Adicione uma ou mais extensões de arquivo, como jpg ou txt, à lista de exclusões. Qualquer arquivo com essas extensões não serão incluídos em verificações em tempo real ou programadas.|
|**Exclusões de processo**|Adiciona um ou mais processos do tipo .exe, .com ou .scr à lista de exclusões. Esses processos não estão incluídos em verificações em tempo real ou programadas.|

  
## <a name="see-also"></a>Consulte também  
 [Itens de configuração de dispositivos gerenciados sem o cliente do System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)