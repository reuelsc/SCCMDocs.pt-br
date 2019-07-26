---
title: Technical Preview 1712 | Microsoft Docs
titleSuffix: Configuration Manager
description: Saiba mais sobre os recursos disponíveis no Technical Preview versão 1712 do System Center Configuration Manager.
ms.date: 12/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3ce372d6-bd93-4d4d-b612-5303f89c36f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: ce992a7d47d77d6542c4f6ede3fb37195714659a
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68339968"
---
# <a name="capabilities-in-technical-preview-1712-for-system-center-configuration-manager"></a>Funcionalidades do Technical Preview 1712 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1712. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview. 

Examine [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview) antes de instalar esta versão do technical preview. Este artigo familiariza você com os requisitos gerais e as limitações do uso de um technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos em um technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**Problemas conhecidos nesse Technical Preview:**
- **A atualização para uma versão prévia falha quando há um servidor do site no modo passivo**. Se você tiver um [servidor do site primário no modo passivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), deverá desinstalar o servidor do site no modo passivo antes de atualizar para esta nova versão de visualização. Você pode reinstalar o servidor de site no modo passivo após a conclusão da instalação pelo site.

  Para desinstalar o servidor do site no modo passivo:
  1. No console do Configuration Manager, acesse **Administração** > **Visão Geral** > **Configuração do Site** > **Servidores e Funções do Sistema de Sites** e, em seguida, selecione o servidor do site no modo passivo.
  2. No painel **Funções do Sistema de Sites**, clique com o botão direito do mouse na função **Servidor do Site** e, em seguida, escolha **Remover Função**.
  3. Clique com o botão direito no servidor do site de modo passivo e, em seguida, escolha **Excluir**.
  4. Após a desinstalação do servidor do site, no servidor do site primário ativo, reinicie o serviço **CONFIGURATION_MANAGER_UPDATE**.
  <!--sms489412-->


**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="do-not-automatically-upgrade-superseded-applications"></a>Não fazer upgrade automaticamente de aplicativos substituídos
<!-- 1351266 -->
Com base em seus [comentários no UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/11532669-fix-supercedence-behavior), nesta versão, você tem a opção de configurar uma implantação de aplicativo para não fazer upgrade automaticamente de versões substituídas. Agora, ao criar a implantação, na página **Configurações de Implantação** do **Assistente de Implantação de Software**, para uma finalidade de instalação **Disponível** ou **Obrigatória**, habilite ou desabilite a opção **Fazer upgrade automaticamente das versões substituídas deste aplicativo**.


## <a name="install-multiple-applications-in-software-center"></a>Instalar vários aplicativos no Centro de Software
<!-- 1357126 -->
Se um usuário final ou um técnico da área de trabalho precisar instalar vários aplicativos em um dispositivo, o Centro de Software agora dará suporte à instalação de vários aplicativos selecionados. Isso permite que o usuário seja mais eficiente, não aguardando a conclusão de uma instalação antes do início da próxima.

Ao usar o modo de seleção múltipla na guia **Aplicativos**, os seguintes critérios determinam quais aplicativos são habilitados para seleção múltipla pelo Centro de Software:
- O aplicativo está visível para o usuário
- O aplicativo ainda não está instalado
- A aprovação do administrador não é necessária ou já foi concedida
- O status do aplicativo está disponível (por exemplo, ainda não está baixando conteúdo)

### <a name="try-it-out"></a>Experimente!
**No console do Configuration Manager:** implante vários aplicativos em um usuário ou dispositivo para instalação, como disponíveis ou obrigatórios (com uma data limite futura). Não exigir aprovação do administrador. Para obter informações, confira [Deploy applications](/sccm/apps/deploy-use/deploy-applications) (Implantar aplicativos).

**No Centro de Software:**
 1. A guia **Aplicativos** deve estar aberta por padrão. 
 2. Para entrar no modo de seleção múltipla na exibição de lista, clique no novo ícone ![Ícone de seleção múltipla do Centro de Software](media/software-center-multi-select-apps.png) no canto superior direito.
 3. Selecione dois ou mais aplicativos a serem instalados clicando na caixa de seleção à esquerda dos aplicativos na lista.
 4. Clique no botão **Instalar Selecionados**.

Os aplicativos são instalados como de costume, agora somente em sucessão.


## <a name="client-based-pxe-responder-service"></a>Serviço de respondente PXE baseado no cliente
<!-- 1357148 -->
Um desafio comum para clientes é fornecer serviços PXE em escritórios remotos/filiais com pouca ou nenhuma infraestrutura de servidor. A função de ponto de distribuição dá suporte a sistemas operacionais cliente, mas não pode ser habilitada para PXE devido à dependência dos Serviços de Implantação do Windows.

Novas configurações de cliente agora estão disponíveis para permitir um serviço de respondente PXE em clientes do Configuration Manager. Uma imagem de inicialização habilitada para PXE deve residir no cache do cliente do respondente PXE.

### <a name="try-it-out"></a>Experimente!
Verifique se não há nenhum ponto de distribuição habilitado para PXE existente ou outros servidores PXE no ambiente de teste que podem entrar em conflito com esse respondente PXE do cliente.

No console do Configuration Manager:
1. No workspace **Biblioteca de Software** em **Sistemas Operacionais**, **Sequências de Tarefas**: crie uma sequência de tarefas usando o modelo personalizado.
   1. Clique em **Adicionar**, selecione **Geral** e, em seguida, a etapa **Definir Variável de Sequência de Tarefas**. Insira **SMSTSPersistContent** como a variável de sequência de tarefas e insira o valor **TRUE**.
   1. Clique em **Adicionar**, selecione **Software** e, em seguida, a etapa **Baixar Conteúdo do Pacote**. Clique no asterisco dourado e, em seguida, selecione uma imagem de inicialização habilitada para PXE. Inclua imagens de inicialização x86 e x64. Configure a etapa para colocá-la no **cache de cliente do Configuration Manager**.
   1. Clique em **Adicionar**, selecione **Geral** e, em seguida, a etapa **Definir Variável de Sequência de Tarefas**. Insira **SMSTSPreserveContent** como a variável de sequência de tarefas e insira o valor **TRUE**.
2. No workspace **Administração** em **Configurações do Cliente**: crie uma política personalizada de configurações de dispositivo do cliente.
   1. Selecione o grupo **Configurações de Cache do Cliente**.
   1. Defina a configuração **Habilitar cliente do Configuration Manager em um sistema operacional completo para compartilhar conteúdo** como **Sim**.
   1. Defina a configuração **Habilitar serviço de respondente PXE** como **Sim**.
   1. Para a configuração **Criar um certificado autoassinado ou importar um certificado do cliente PKI**, clique em **Fornecer um certificado**. Selecione **Importar certificado** se o ambiente de teste tiver um PKI; caso contrário, clique em **OK** para criar um certificado autoassinado. 
   1. Defina as configurações restantes, conforme necessário, para o ambiente de teste. (As configurações padrão deverão funcionar, a menos que haja requisitos de segurança ou de rede específicos.)
3. Implante a sequência de tarefas e as configurações personalizadas do cliente em uma coleção de clientes de destino a serem respondentes PXE. Aguarde até que as políticas sejam aplicadas e a sequência de tarefas seja executada.
4. Inicie outro cliente na mesma sub-rede para executar a inicialização da rede/PXE como de costume.

### <a name="known-issues"></a>Problemas conhecidos
- O editor de sequência de tarefas exibe um ícone vermelho de erro para a etapa **Baixar Conteúdo do Pacote** quando uma imagem de inicialização é adicionada, mas a sequência de tarefas é salva com êxito. A abertura dessa sequência de tarefas novamente no editor também mostra um aviso inofensivo informando que os objetos referenciados não podem ser encontrados. <!-- sms427542 -->
- A imagem de inicialização da etapa Baixar Conteúdo do Pacote não é mostrada na lista da sequência de tarefas personalizada de referências. Além disso, a ação **Distribuir Conteúdo** não está disponível. <!-- sms504017 -->


## <a name="change-in-the-configuration-manager-client-install"></a>Alteração na instalação do cliente do Configuration Manager  
Como resultado de seus comentários no UserVoice, o [Silverlight não é mais instalado automaticamente nos clientes.](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/10886427-please-do-not-install-silverlight-by-default-in-v) <!--1356195-->
  

## <a name="change-to-the-surface-device-dashboard"></a>Alteração no painel de dispositivos Surface
O painel do Surface agora exibe versões de firmware para dispositivos Surface, em vez da versão do sistema operacional. No console, vá até **Monitoramento** > **Surface Devices**. É possível exibir os seguintes itens:
- Percentual de Surfaces
- Percentual de modelos do Surface
- Cinco principais versões de firmware
 <!--1355788-->


## <a name="improvements-to-office-365-client-management-dashboard"></a>Melhorias no painel de Gerenciamento de Clientes do Office 365 
O painel de Gerenciamento de Clientes do Office 365 agora exibe uma lista de dispositivos relevantes quando seções de gráfico são selecionadas. No console, acesse **Biblioteca de Software** >**Visão Geral** >**Gerenciamento de Clientes do Office 365**. O painel é exibido à direita. A seleção de critérios do gráfico mostra uma lista de dispositivos.  
<!--1357281-->


## <a name="improvements-to-the-configuration-manager-console"></a>Melhorias no console do Configuration Manager 
Fizemos as melhorias a seguir no console do Configuration Manager, que foram resultado de seus comentários no UserVoice.

- [A lista de dispositivos exibe o usuário primário](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8782225-enable-a-column-for-primary-user): As listas de dispositivos em Ativos e Conformidade, Dispositivos agora exibem o usuário primário por padrão. O último usuário conectado também pode ser adicionado como uma coluna opcional. <!-- 1357280 -->
- [As coleções renomeadas são exibidas nas regras de associação de coleção existentes](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20125567-fix-the-renaming-of-collections): Se uma coleção for membro de outra coleção e for renomeada, o novo nome será atualizado de acordo com as regras de associação.<!--1357282--> 


## <a name="improvements-to-operating-system-deployment"></a>Melhorias na implantação do sistema operacional
Fizemos as melhorias a seguir na implantação de sistema operacional, algumas das quais foram resultado de seus comentários no UserVoice.
- [Visualizador de log padrão na imagem de inicialização](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/19269823-stop-cmtrace-from-asking-us-if-we-want-to-use-it-a): No Windows PE, ao iniciar cmtrace.exe, você não precisa mais escolher se deseja tornar este programa o visualizador padrão para arquivos de log. <!-- SMS 500897 -->
- Etapa Baixar o conteúdo do pacote: agora você pode adicionar imagens de inicialização nessa etapa da sequência de tarefas.


## <a name="windows-10-feedback-hub-app-integration"></a>Integração de aplicativos do hub de comentários do Windows 10

Adoramos tanto comentários que agora estamos permitindo-os por meio do [aplicativo hub de comentários](https://support.microsoft.com/en-us/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) interno do Windows 10. Ao **Adicionar novos comentários**, selecione a categoria **Enterprise Management** e, em seguida, escolha uma das seguintes subcategorias:
- Cliente do Configuration Manager
- Console do Configuration Manager
- Implantação de sistema operacional do Configuration Manager
- Configuration Manager Server

Continue usando nossa [página do UserVoice](http://configurationmanager.uservoice.com/) para votar em ideias de novos recursos no Configuration Manager.


<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Próximas etapas
Para obter informações de como instalar ou atualizar o branch da technical preview, consulte [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
