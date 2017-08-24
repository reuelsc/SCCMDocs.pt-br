---
title: "Como criar itens de configuração para dispositivos com Windows Phone gerenciados com o Intune | Microsoft Docs"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df10dc4d-c9ff-4574-bb33-8d30eb14cfe3
caps.latest.revision: "13"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: bcb2d14ef097afc2915932fe09f6d83c968aecf9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-configuration-items-for-windows-phone-devices-managed-without-the-system-center-configuration-manager-client"></a>Como criar itens de configuração para dispositivos Windows Phone gerenciados sem o cliente do System Center Configuration Manager
Use o item de configuração do **Windows Phone** do System Center Configuration Manager para gerenciar as configurações para dispositivos Windows Phone que estão registrados no Microsoft Intune ou são gerenciados localmente pelo Configuration Manager.  
  
### <a name="to-create-a-windows-phone-configuration-item"></a>Para criar um item de configuração do Windows Phone  
  
1.  No console do Configuration Manager, clique em **Ativos e conformidade**.  
  
2.  No espaço de trabalho **Ativos e Conformidade** , expanda **Configurações de Conformidade**e clique em **Itens de Configuração**.  
  
3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Item de Configuração**.  
  
4.  Na página **Geral** do **Assistente para Criar Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.  
  
5.  Em **Especificar o tipo de item de configuração que deseja criar**, selecione **Windows Phone**.  
  
6.  Se você criar e atribuir categorias, clique em **Categorias** para ajudá-lo a pesquisar e filtrar itens de configuração no console do Configuration Manager.  
  
7.  Na página **Plataformas com Suporte** do assistente, selecione as plataformas específicas do Windows Phone que avaliarão o item de configuração.  
  
8.  Na página **Configurações do Dispositivo** do assistente, selecione o grupo de configurações que deseja configurar. Veja [Referência de configurações do item de configuração do Windows Phone](#BKMK_Setref) neste tópico para obter detalhes e clique **Avançar**.  
  
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
  
##  <a name="windows-phone-configuration-item-settings-reference"></a>Referência de configurações do item de configuração do Windows Phone  
  
### <a name="password"></a>Senha  
 Essas configurações se aplicam ao Windows Phone 8 e Windows Phone 8.1.  
  
|Configuração|Detalhes|  
|-------------|-------------|  
|**Exigir configurações de senha em dispositivos**|Requer uma senha nos dispositivos com suporte.|  
|**Comprimento mínimo da senha (caracteres)**|O comprimento mínimo da senha.|  
|**Validade da senha em dias**|O número de dias antes que uma senha precise ser alterada.|  
|**Número de senhas lembradas**|Impede a reutilização de senhas usadas anteriormente.|  
|**Número de tentativas de logon com falha antes de o dispositivo ser apagado**|Apaga o dispositivo se houver falha neste número de tentativas de logon.|  
|**Complexidade da senha**|Escolha se é possível especificar um PIN como “1234” ou se é necessário fornecer uma senha forte.|  
|**Enviar PIN de recuperação de senha ao Exchange Server**||  
  
### <a name="device"></a>Dispositivo  
  
|Configuração|Detalhes|  
|-------------|-------------|  
|**Captura de tela**|Permite ao usuário tirar uma captura de tela da tela do dispositivo.<br /><br /> (Somente Windows Phone 8.1)|  
|**Envio de dados de diagnóstico**|Permita o envio de arquivos de log do aplicativo.|  
|**Localização geográfica**|Permita que o dispositivo use informações de serviços de localização.<br /><br /> (Somente Windows Phone 8.1)|  
|**Copiar e colar**|Use copiar e colar para transferir dados entre aplicativos.<br /><br /> (Somente Windows Phone 8.1)|  
|**Bluetooth**|Permite o uso da capacidade Bluetooth do dispositivo.|  
  
### <a name="email-management"></a>Gerenciamento de email  
 Essas configurações se aplicam ao Windows Phone 8 e Windows Phone 8.1.  
  
|Configuração|Detalhes|  
|-------------|-------------|  
|**Email POP e IMAP**|Permite a conexão a contas de email que usam os padrões POP e IMAP.|  
|**Tempo máximo para manter o email**|A duração de tempo que o email será mantido antes de ser excluído do servidor.|  
|**Formatos de mensagens permitidos**|Especifique se os emails do usuário podem ser em HTML ou somente em texto sem formatação.|  
|**Tamanho máximo de email de texto sem formatação (baixado automaticamente)**|Controla o tamanho máximo de emails com texto sem formatação quando baixados automaticamente.|  
|**Tamanho máximo para email HTML (baixado automaticamente)**|Controla o tamanho máximo de emails em HTML quando baixados automaticamente.|  
|**Tamanho máximo de um anexo (baixado automaticamente)**|Configura o email de tamanho máximo será baixado automaticamente.|  
|**Sincronização de calendário**||  
|**Conta de email personalizada**|Permita o uso de uma conta que não seja da Microsoft no dispositivo.|  
|**Tornar a Conta da Microsoft opcional no aplicativo de email do Windows**|Não exige o uso de uma conta da Microsoft para entrar no Windows Mail.|  
  
### <a name="store"></a>Repositório  
 Estas configurações se aplicam apenas a dispositivos Windows Phone 8.1.  
  
|Configuração|Detalhes|  
|-------------|-------------|  
|**Armazenamento de aplicativos**|Permite o acesso a loja de aplicativos no dispositivo.|  
  
### <a name="browser"></a>Navegador  
 Essas configurações se aplicam ao Windows Phone 8 e Windows Phone 8.1.  
  
|Configuração|Detalhes|  
|-------------|-------------|  
|**Permitir navegador da Web**|Habilitar ou desabilitar o navegador de Internet padrão.|  
|**Preenchimento automático**|O usuário pode alterar as configurações de preenchimento automático no navegador.|  
|**Script ativo**|O navegador pode executar scripts, como scripts do ActiveX.|  
|**Plug-ins**|O usuário pode adicionar plug-ins ao Internet Explorer.|  
|**Bloqueador de pop-up**|Habilita ou desabilita o bloqueador de pop-ups do navegador.|  
|**Aviso de fraude**|Habilite ou desabilite avisos de sites fraudulentos potenciais.|  
  
### <a name="internet-explorer"></a>Internet Explorer  
 Essas configurações se aplicam ao Windows Phone 8 e Windows Phone 8.1.  
  
|Configuração|Detalhes|  
|-------------|-------------|  
|**Sempre enviar cabeçalho Não Acompanhar**|Impede que as informações de navegação sejam enviadas para sites de terceiros.|  
|**Zona de segurança da Intranet**||  
|**Nível de segurança para a zona da Internet**|Configure o nível de segurança para a zona da Internet.|  
|**Nível de segurança para zona da intranet**|Configure o nível de segurança para a zona da intranet.|  
|**Nível de segurança para a zona de sites confiáveis**|Configure o nível de segurança para a zona de sites confiáveis.|  
|**Nível de segurança para a zona de sites restritos**|Configure o nível de segurança para a zona de sites restritos.|  
|**Namespaces para a zona da intranet**||  
|**Ir para um site da intranet por uma entrada de palavra única**|Habilita ou desabilita a configuração que permite que o Internet Explorer acesse automaticamente um site de Intranet se um nome de site válido for inserido sem um HTTP precedente:|  
|**Opção de menu do modo Empresarial**|Permita que os usuários ativem e desativem o modo Empresarial no menu **Ferramentas** do Internet Explorer.|  
|**Local do relatório de registro em log (URL)**|Especifique uma URL em que os sites visitados serão registrados quando o modo Empresarial estiver ativo.|  
|**Local da lista do site do modo Empresarial (URL)**|Especifique o local da lista de sites que usarão o modo Empresarial quando ele estiver ativo.|  
  
### <a name="cloud"></a>Nuvem  
  
|Configuração|Detalhes|  
|-------------|-------------|  
|**Sincronização de configurações**|Permite a sincronização de configurações entre dispositivos.|  
|**Sincronização de credenciais**|Permite a sincronização de credenciais entre dispositivos.|  
|**Conta da Microsoft**|Permita o uso de uma conta da Microsoft no dispositivo.<br /><br /> (Somente Windows Phone 8.1)|  
|**Sincronização de configurações em conexões medidas**|Permita que as configurações sejam sincronizadas durante a medição da conexão com a Internet.|  
  
### <a name="security"></a>Segurança  
  
|Configuração|Detalhes|  
|-------------|-------------|  
|**Instalação de arquivo não assinado**|Permite o carregamento de arquivos não assinados.|  
|**Aplicativos não assinados**|Permite o carregamento de aplicativos não assinados.|  
|**Mensagens SMS e MMS**|Permita mensagens SMS e MMS do dispositivo.|  
|**Armazenamento removível**|Permita o uso de armazenamento removível, como um cartão SD, no dispositivo.|  
|**Câmera**|Permita o uso da câmera do dispositivo.|  
|**Comunicação a curta distância (NFC)**|Permita a comunicação usando a NFC no dispositivo.<br /><br /> (Somente Windows Phone 8.1)|  
|**Permitir conexão USB**|Permita que os periféricos se conectem a esse dispositivo por USB.|
  
### <a name="peak-synchronization"></a>Sincronização em horário de pico  
 Essas configurações se aplicam ao Windows Phone 8 e Windows Phone 8.1.  
  
|Configuração|Detalhes|  
|-------------|-------------|  
|**Especificar o horário de pico**|Especifique um intervalo de tempo que será usado pelas duas configurações a seguir.|  
|**Frequência de sincronização no horário de pico**|Escolha com que frequência o dispositivo será sincronizado durante o horário de pico especificado.|  
|**Frequência de sincronização fora do horário de pico**|Escolha com que frequência o dispositivo será sincronizado fora do horário de pico especificado.|  
  
### <a name="roaming"></a>Roaming  
 Essas configurações se aplicam ao Windows Phone 8 e Windows Phone 8.1.  
  
|Configuração|Detalhes|  
|-------------|-------------|  
|**Gerenciamento de dispositivos durante roaming**|Permite que o dispositivo seja gerenciado pelo Configuration Manager durante o roaming.|  
|**Download de software durante roaming**|Permite o download de aplicativos e software durante o roaming.|  
|**Download de emails durante roaming**|Permite downloads de email durante o roaming.|  
|**Roaming de dados**|Permita o roaming entre redes durante o acesso de dados.|  
  
### <a name="encryption"></a>Criptografia  
 Essas configurações se aplicam ao Windows Phone 8 e Windows Phone 8.1.  
  
|Configuração|Detalhes|  
|-------------|-------------|  
|**Criptografia de cartão de memória**|Requer que todos os cartões de armazenamento usados com o dispositivo sejam criptografados.|  
|**Criptografia de arquivo no dispositivo**|Requer que os arquivos no dispositivo móvel sejam criptografados.|  
|**Exigir assinatura de email**|Exija que os emails sejam assinados antes de ser enviados.|  
|**Algoritmo de assinatura**|Selecione o algoritmo usado para assinar emails.|  
|**Exigir criptografia de email**|Exija que os emails sejam criptografados antes de ser enviados.|  
|**Algoritmo de criptografia**|Selecione o algoritmo usado para criptografar emails.|  
  
###  <a name="wireless-communications"></a>Comunicações sem fio  
 Essas configurações se aplicam ao Windows Phone 8 e Windows Phone 8.1.  
  
|Nome da configuração|Detalhes|  
|------------------|-------------|  
|**Conexão de rede sem fio**|Habilite ou desabilite a funcionalidade de Wi-Fi dos dispositivos.|  
|**Compartilhamento da Internet por Wi-Fi**|Permite que os usuários usem seus dispositivos como um ponto de acesso móvel.|  
|**Descarregar dados para Wi-Fi quando possível**||  
|**Relatórios de ponto de acesso Wi-Fi**||  
  
##### <a name="to-configure-a-wireless-network-connection"></a>Para configurar uma conexão de rede sem fio  
  
1.  Na página **Definir configurações de comunicação sem fio de dispositivos móveis** clique em **Adicionar**.  
  
2.  Na caixa de diálogo **Conexão de Rede Sem Fio** , especifique as seguintes informações sobre a conexão sem fio que será provisionada nos dispositivos móveis:  
  
|Configuração|Mais informações|  
|-------------|----------------------|  
|**Nome da rede (SSID)**||  
|**Conexão de rede**|Escolha **Internet** ou **Trabalho**.|  
|**Autenticação**|Escolha o método de autenticação para a conexão sem fio do:<br><br> - **Aberto**<br> - **Compartilhado**<br> - **WPA**<br> - **WPA-PSK**<br> - **WPA2**<br> - **WPA2-PSK**|  
|**Criptografia de dados**|Escolha o método de criptografia usado por esta conexão. Os valores que podem ser selecionados serão diferentes dependendo do método de **Autenticação** selecionado:<br><br> - **Desabilitado**<br> - **WEP**<br> - **TKIP**<br> - **AES**|  
|**Índice de chave**|Selecione um índice de chave de **1** a **4** que será usado com uma configuração de **Criptografia de dados** de **WEP**.|  
|**Esta rede se conecta à Internet**|Selecione esta opção se desejar fornecer configurações de proxy que permitem que dispositivos móveis em uma conexão sem fio se conectem à Internet.|  
|**Configurações do servidor proxy**|Especifique, conforme necessário, as configurações de **Servidor** e **Porta** para **HTTP**, **WAP** e **Soquetes**.|  
|**Habilitar acesso à rede 802.1X**|Selecione esta opção se desejar proteger a conexão com a especificação de um tipo de EAP.|  
|**Tipo de EAP**|Escolha o tipo de EAP a ser usado do:<br><br> - **PEAP**<br> - **Cartão inteligente ou certificado**|  
    
  
###  <a name="certificates"></a>Certificados  
 Permite importar certificados a serem instalados em dispositivos móveis.  
  
 Clique em **Importação**e especifique os seguintes valores:  
  
-   **Arquivo de certificado** – Clique em **Procurar** e selecione o arquivo de certificado com a extensão **.cer** que deseja importar.  
  
-   **Repositório de destino** – Escolha um ou mais repositórios de destino em que o certificado importado será adicionado no dispositivo móvel de:  
  
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
 Essas configurações se aplicam ao Windows Phone 8 e Windows Phone 8.1.  
  
|Configuração|Detalhes|  
|-------------|-------------|  
|**Controle de conta de usuário**|Habilita ou desabilita o Controle de Conta de Usuário do Windows no dispositivo.|  
|**Firewall da rede**|Habilita ou desabilita o Firewall do Windows.|  
|**Atualizações**|Escolha como as atualizações de software do Windows serão baixadas no computador. Por exemplo, é possível baixar automaticamente as atualizações, mas permitir que o usuário escolha quando instalá-las.|  
|**Classificação mínima de atualizações**|Escolha a classificação mínima das atualizações que serão baixadas nos computadores com Windows: **Nenhuma**, **Importante**ou **Recomendada**.|  
|**SmartScreen**|Habilite ou desabilite a Tela Inteligente do Windows.|  
|**Proteção contra vírus**|Certifique-se de que o dispositivo está protegido pelo software antivírus|  
|**As assinaturas de proteção contra vírus estão atualizadas**|Certifique-se de que as assinaturas de software antivírus estão atualizadas.|
|**Permitir cancelamento de registro manual**|Permita que o usuário remova seu dispositivo do MDM.|  
  
### <a name="windows-server-work-folders"></a>Pastas de Trabalho do Windows Server  
 Essas configurações se aplicam ao Windows Phone 8 e Windows Phone 8.1.  
  
|Configuração|Detalhes|  
|-------------|-------------|  
|**URL de pastas de trabalho**|Configura o local de uma pasta de trabalho do Windows Server com as qual os usuários podem se conectar por meio de seus dispositivos.|  
  
### <a name="allowed-and-blocked-apps-list-windows-phone-81-only"></a>Lista de aplicativos permitidos e bloqueados (apenas Windows Phone 8.1)  
 Permite especificar uma lista de aplicativos do Windows Phone que são compatíveis ou não compatíveis em sua empresa. Os aplicativos que você especificar como bloqueados não podem ser instalados pelos usuários. Se você especificar uma lista de aplicativos permitidos, os usuários poderão instalar somente os aplicativos na lista.  
  
 Não é possível especificar aplicativos permitidos e bloqueados no mesmo item de configuração.  
  
> [!IMPORTANT]  
>  Se você especificar uma lista de aplicativos permitidos, você deverá garantir que o aplicativo do portal da empresa e que todos os aplicativos implantados em dispositivos Windows Phone 8.1 estão na lista de aplicativos **Permitidos** .  
  
##### <a name="to-specify-an-allowed-or-blocked-apps-list"></a>Para especificar uma lista de aplicativos permitidos ou bloqueados  
  
1.  Na página **Lista de Aplicativos Permitidos e Bloqueados (Windows Phone 8.1)** , especifique as seguintes informações:  
  
|||  
|-|-|  
|Configuração|Mais informações|  
|**Lista de aplicativos bloqueados**|Selecione esta opção se desejar especificar uma lista de aplicativos que os usuários não terão permissão de instalar.|  
|**Lista de aplicativos permitidos**|Selecione esta opção se desejar especificar uma lista de aplicativos que os usuários têm permissão para instalar.|  
|**Adicionar**|Adiciona um aplicativo à lista selecionada. Especifique um nome de sua preferência, ou o editor do aplicativo, e a URL para o aplicativo na loja de aplicativos.<br /><br /> Para especificar a URL, na página da Loja do Windows Phone, procure o aplicativo que deseja usar.<br /><br /> **Exemplo:** procure o aplicativo **Skype** na loja. A URL usada será http://www.windowsphone.com/en-us/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51.<br /><br /> Para o aplicativo do portal da empresa ou para os aplicativos de linha de negócios, não é necessário especificar uma URL completa, somente o GUID do aplicativo.|  
|**Editarar**|Permite editar o nome, editor e a URL do aplicativo selecionado.|  
|**Removerr**|Exclui o aplicativo selecionado da lista.|  
|**Importarar**|Importa uma lista dos aplicativos que você especificou em um arquivo de valores separados por vírgulas. Use o formato, nome do aplicativo, editor e a URL do aplicativo no arquivo.|  
  
## <a name="see-also"></a>Consulte também  
 [Itens de configuração de dispositivos gerenciados sem o cliente do System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)