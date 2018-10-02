---
title: Nova versão 1702
titleSuffix: Configuration Manager
description: Veja os detalhes das alterações e os novos recursos introduzidos na versão 1702 do System Center Configuration Manager.
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6abf61488a96ec3299b606b10901b0787b82edc9
ms.sourcegitcommit: fe279229a90fdc8cddbb13c7ffdbbb22af0e25ef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47229340"
---
# <a name="what39s-new-in-version-1702-of-system-center-configuration-manager"></a>Novidades da versão 1702 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A atualização 1702 da ramificação atual do System Center Configuration Manager está disponível como uma atualização no console para sites instalados anteriormente que executam as versões 1602, 1606 ou 1610. Também está disponível como uma versão de linha de base que você pode usar ao instalar uma nova implantação.

> [!TIP]  
> Para instalar um novo site, você deve usar uma versão de linha de base do Configuration Manager.  
>  Saiba mais sobre:    
>   - [Instalação de novos sites](https://technet.microsoft.com/library/mt590197.aspx)  
>   - [Instalação de atualizações em sites](https://technet.microsoft.com/library/mt607046.aspx)  
>   - [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

As seções a seguir fornecem detalhes sobre as alterações e novas funcionalidades introduzidas na versão 1702 do Configuration Manager.  

## <a name="deprecated-features-and-operating-systems"></a>Sistemas operacionais e recursos preteridos
Saiba mais sobre alterações de suporte antes que elas sejam implementadas em [itens removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

A versão 1702 descarta o suporte para os seguintes produtos:
- **SQL Server 2008 R2**, para servidores de banco de dados do site. A substituição de suporte foi [anunciada primeiro](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-support-for-sql-server-versions-as-a-site-database) em 10 de julho de 2015. Esta versão do SQL Server permanece com suporte quando você usa uma versão do Configuration Manager anterior à 1702.
- **Windows Server 2008 R2**, para funções de servidores de sistema e a maioria das funções do sistema de sites. A substituição de suporte foi [anunciada primeiro](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems) em 10 de julho de 2015. Esta versão do Windows permanece com suporte quando você usa uma versão do Configuration Manager anterior à 1702.  
- **Windows Server 2008**, para funções de servidores de sistema e a maioria das funções do sistema de sites. A substituição de suporte foi [anunciada primeiro](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems) em 10 de julho de 2015.
- **Windows XP Embedded**, como um sistema operacional cliente. A substituição foi [anunciada primeiro](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client#deprecated-client-operating-systems) em 10 de julho de 2015. Esta versão do Windows permanece com suporte quando você usa uma versão do Configuration Manager anterior à 1702.




## <a name="site-infrastructure"></a>Infraestrutura do site

### <a name="improvements-for-in-console-search"></a>Melhorias da pesquisa no console
Veja a seguir as melhorias no uso de pesquisa no console do Configuration Manager:
 - **Caminho do Objeto:**  
  Muitos objetos agora dão suporte a uma coluna chamada **Caminho do Objeto**.  Quando você pesquisar e incluir essa coluna nos resultados da exibição, poderá exibir o caminho para cada objeto. Por exemplo, se você executar uma pesquisa por aplicativos no nó Aplicativos e também pesquisar nos subnós, a coluna *Caminho do Objeto* no painel de resultados mostrará o caminho para cada objeto que é retornado.   

- **Preservação do texto de pesquisa:**  
  Quando você inserir texto na caixa de texto de pesquisa e alternar entre a pesquisa de um subdiretório e o nó atual, o texto digitado persistirá e permanecerá disponível para uma nova pesquisa, sem a necessidade de redigitá-lo.

- **Preservação da sua decisão de pesquisar subnós:**  
 A opção selecionada para a pesquisa no *nó atual* ou em *todos os subnós* agora é mantida após alterar o nó no qual você está trabalhando. Esse novo comportamento significa que você não precisa redefinir constantemente essa decisão ao percorrer o console. Ao abrir o console, a opção padrão é pesquisar somente o nó atual.


### <a name="send-feedback-from-the-configuration-manager-console"></a>Enviar comentários do console do Configuration Manager

 Você pode usar as opções de comentários no console para enviar comentários diretamente para a equipe de desenvolvimento.

 Você pode encontrar a opção **Comentários**:
 -  Na faixa de opções, na extremidade esquerda da guia Página Inicial de cada nó.  
    ![Faixa de opções](./media/feedback-home.png)

 -  Ao clicar com o botão direito do mouse em qualquer objeto no console.   
     ![Opção ao clicar com o botão direito do mouse](./media/feedback-option.png)   

 Escolher **Comentários** abre seu navegador para o site de comentários do [UserVoice do Configuration Manager](https://go.microsoft.com/fwlink/?linkid=617029).


###  <a name="changes-for-updates-and-servicing"></a>Alterações em Atualizações e Manutenção
Veja a seguir as alterações em Atualizações e Manutenção:

- **Local do nó**   
  Depois de instalar a versão 1702, o nó **Atualizações e manutenção** aparece como um nó de nível superior em **Administração**. Não é mais um nó filho abaixo de **Serviços de nuvem**.

- **Novos estados de atualização**  
  Quando você exibe as atualizações disponíveis no console, há dois novos estados:  
  - **Disponível para instalação** - esta é uma atualização que foi baixado e está pronta para instalar.
  - **Pronto para download** -essa atualização está disponível, mas não foi baixada. Você pode optar por baixar essa atualização, mas ela foi substituída por uma mais recente.


- **Opções de atualização mais simples**  
  Na próxima vez que sua infraestrutura se qualificar para duas ou mais atualizações, somente a atualização mais recente será baixada. Por exemplo, se sua versão atual do site for duas ou mais antigas do que a versão mais recente disponível, somente a versão de atualização mais recente será baixada automaticamente.  

  Você pode escolher baixar e instalar as outras atualizações disponíveis, mesmo quando elas não são a versão mais atual. Se você baixar uma versão mais antiga, receberá um aviso de que a atualização foi substituída por uma mais recente. Para baixar uma atualização *Disponível para Download*, selecione a atualização no console e, em seguida, clique em **Baixar**.

- **Limpeza aprimorada de atualizações mais antigas**   
  Adicionamos uma função de limpeza automática que exclui os downloads desnecessários da pasta 'EasySetupPayload' no servidor do site. Como isso é apresentado com a versão 1702, a limpeza começa a funcionar após a instalação de uma atualização subsequente como um pacote cumulativo de atualizações ou uma versão de atualização futura.  


### <a name="data-warehouse-service-point"></a>Ponto de serviço do Data Warehouse
 Use o ponto de serviço do Data Warehouse para armazenar e relatar dados históricos de longo prazo para sua implantação do Configuration Manager.

 O data warehouse dá suporte a até 2 TB de dados, com carimbos de data e hora para controle de alterações. O armazenamento dos dados é possibilitado por meio de sincronizações automatizadas do banco de dados de site do Configuration Manager para o banco de dados de data warehouse. Essas informações estarão acessíveis no seu ponto do Reporting Services.

 Para saber mais, veja o [Ponto de serviço do Data Warehouse](/sccm/core/servers/manage/data-warehouse).


### <a name="peer-cache-improvements"></a>Aprimoramentos de cache de pares
 A partir da versão 1702, um computador de origem de cache de pares rejeitará uma solicitação de conteúdo quando o computador de origem do cache de pares atender a qualquer uma das seguintes condições:  
  -  Está no modo de bateria fraca.
  -  A carga de CPU excede 80% no momento em que o conteúdo é solicitado.
  -  A E/S de disco tem um *AvgDiskQueueLength* que excede 10.
  -  Não há mais conexões disponíveis para o computador.   
Para saber mais, veja **Acesso limitado a uma origem de cache de pares** em [Cache de pares para clientes do Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).   

Além disso, três novos relatórios são adicionados ao seu ponto de relatório. Você pode usar esses relatórios para saber mais detalhes sobre solicitações de conteúdo rejeitadas, incluindo o limite de grupo, o computador e o conteúdo envolvidos. Consulte [Monitoramento](/sccm/core/plan-design/hierarchy/client-peer-cache#monitoring) no tópico de cache de pares.

### <a name="content-library-cleanup-tool"></a>Ferramenta de limpeza da biblioteca de conteúdo
 Use a [ferramenta de limpeza da biblioteca de conteúdo](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) para remover o conteúdo de pontos de distribuição quando esse conteúdo não está mais associado a um aplicativo.


### <a name="use-the-oms-connector-with-the-azure-government-cloud"></a>Usar o conector do OMS com a nuvem Azure Governamental
Você pode usar o conector do OMS para se conectar ao OMS Log Analytics na nuvem do Microsoft Azure Governamental. Isso exige a modificação de um arquivo de configuração antes de instalar o conector do OMS para que o conector possa trabalhar com a nuvem governamental. Para saber mais, veja [Usar o conector do OMS com a nuvem Azure Governamental](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#fairfaxconfig).

### <a name="software-update-points-are-added-to-boundary-groups"></a>Os pontos de atualização de software são adicionados aos grupos de limites
A partir da versão 1702, os clientes usam grupos de limites para localizar um novo ponto de atualização de software, fazer fallback e localizar um novo ponto de atualização de software se o atual não estiver mais acessível. Você pode adicionar pontos de atualização de software individuais a grupos de limites diferentes para controlar quais servidores um cliente pode encontrar. Para saber mais, veja [pontos de atualização de software](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) no tópico [Configurando grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups).


<!-- ## Migration  -->

<!-- ## Client management  -->

## <a name="compliance-settings"></a>Configurações de conformidade

### <a name="new-compliance-settings-for-ios"></a>Novas configurações de conformidade para iOS

Adicionamos várias novas configurações para dispositivos iOS para corresponderem aos disponíveis com o Microsoft Intune.
Para obter uma lista de todas as configurações disponíveis, veja [Criar itens de configuração para dispositivos com iOS e Mac OS X gerenciados com o Intune](/sccm/mdm/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client).


## <a name="application-management"></a>Gerenciamento de aplicativos

### <a name="improved-support-for-windows-store-for-business-apps"></a>Suporte aprimorado para aplicativos da Windows Store para Empresas

Agora você pode implantar aplicativos licenciados online da Windows Store para Empresas para computadores com Windows 10 que você gerencia usando o cliente do Configuration Manager.
Para saber mais, veja [Gerenciar aplicativos da Windows Store para Empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

### <a name="check-for-running-executable-files-before-installing-an-application"></a>Verificar se há arquivos executáveis antes de instalar um aplicativo

Na caixa de diálogo **Propriedades** de um tipo de implantação, na guia **Comportamento de Instalação**, agora você pode especificar um ou mais arquivos executáveis que, se estiverem em execução, bloquearão a instalação do tipo de implantação. O usuário deve fechar o arquivo executável em execução (ou ele pode ser fechado automaticamente para implantações com a finalidade obrigatória) antes de o tipo de implantação poder ser instalado.

Se o aplicativo tiver sido implantado como **Disponível** e um usuário final tentar instalar um aplicativo, será solicitado que ele feche todos os executáveis em execução especificados antes de prosseguir com a instalação.

Se o aplicativo tiver sido implantado como **Necessário** e a opção **Fechar automaticamente todos os executáveis em execução especificados na guia de comportamento de instalação da caixa de diálogo de propriedades do tipo de implantação** estiver selecionada, ele verá uma caixa de diálogo informando que os executáveis especificados serão fechados automaticamente quando o prazo da instalação for atingido.

### <a name="app-management-improvements-for-hybrid-mdm"></a>Melhorias de gerenciamento de aplicativo para MDM híbrido

- [Implantar aplicativos iOS adquiridos por volume em coleções de dispositivos](#deploy-volume-purchased-ios-apps-to-device-collections)
- [Suporte para o Volume Purchase Program do iOS para educação](#support-for-ios-volume-purchase-program-for-education)
- [Suporte para vários tokens do Volume Purchase Program](#support-for-multiple-volume-purchase-program-tokens)


## <a name="operating-system-deployment"></a>Implantação de sistema operacional

### <a name="expire-stand-alone-media"></a>Expirar mídia autônoma
Quando você cria mídia autônoma, há novas opções para definir datas de início e vencimento opcionais na mídia. Essas configurações estão desabilitadas por padrão. As datas são comparadas com a hora do sistema no computador antes de a mídia autônoma ser executada. Quando a hora do sistema for anterior à hora de início ou posterior à hora de expiração, a mídia autônoma não será iniciada. Essas opções também estão disponíveis usando o cmdlet New-CMStandaloneMedia PowerShell. Para obter detalhes, veja [Criar mídia autônoma](/sccm/osd/deploy-use/create-stand-alone-media).

### <a name="package-id-displayed-in-task-sequence-steps"></a>ID do pacote exibida nas etapas da sequência de tarefas
Qualquer etapa de sequência da tarefa que faz referência a um pacote, pacote de driver, imagem do sistema operacional, imagem de inicialização ou pacote de atualização do sistema operacional agora exibirá a ID do pacote do objeto referenciado. Quando uma etapa de sequência de tarefas fizer referência a um aplicativo, ela exibirá a ID do objeto.

### <a name="support-for-additional-content-in-stand-alone-media"></a>Suporte para conteúdo adicional na mídia autônoma
Agora há suporte para conteúdo adicional na mídia autônoma. Você pode selecionar pacotes adicionais, pacotes de driver e aplicativos para obter preparação na mídia junto com outros conteúdos referenciados na sequência de tarefas. Anteriormente, somente o conteúdo referenciado na sequência de tarefas era preparado na mídia autônoma. Para obter detalhes, veja [Criar mídia autônoma](/sccm/osd/deploy-use/create-stand-alone-media).

### <a name="hardware-inventory-collects-uefi-information"></a>O inventário de hardware coleta informações de UEFI
Uma nova classe de inventário de hardware (**SMS_Firmware**) e a propriedade (**UEFI**) estão disponíveis para ajudá-lo a determinar se um computador é iniciado no modo UEFI. Quando um computador é iniciado no modo UEFI, a propriedade **UEFI** é definida como **TRUE**. Isso é habilitado no inventário de hardware por padrão. Para obter mais informações sobre o inventário de hardware, consulte [Como configurar o inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

### <a name="improvements-to-software-center-warning-messages-for-high-impact-task-sequences"></a>Aprimoramentos nas mensagens de aviso do Centro de Software para sequências de tarefas de alto impacto
Esta versão inclui os seguintes aprimoramentos para mensagens de aviso do Centro de Software para sequências de tarefas de implantação de alto impacto:

- Nas propriedades da sequência de tarefas, agora você pode configurar qualquer sequência de tarefas, incluindo sequências de tarefas que não do sistema operacional, como uma implantação de alto risco. Qualquer sequência de tarefas que atender a determinadas condições será automaticamente definida como de alto impacto. Para obter detalhes, consulte [Gerenciar implantações de alto risco](/sccm/protect/understand/settings-to-manage-high-risk-deployments).
- Nas propriedades da sequência de tarefas, você pode optar por usar a mensagem de notificação padrão ou criar sua própria mensagem de notificação personalizada para implantações de alto impacto.
- Nas propriedades da sequência de tarefas, você pode configurar as propriedades do Centro de Software, que incluem tornar uma reinicialização necessária, o tamanho do download da sequência de tarefas e o tempo de execução estimado.
- A mensagem de implantação de alto impacto padrão para atualizações in-loco agora indicam que seus aplicativos, dados e configurações são migrados automaticamente. Anteriormente, a mensagem padrão para qualquer instalação do sistema operacional indicava que todos os aplicativos, dados e configurações seriam perdidos, o que não era verdade para uma atualização in-loco.

Para obter detalhes, veja [Definir configurações da sequência de tarefas de alto impacto](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#set-a-task-sequence-as-a-high-impact-task-sequence)

### <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Retornar à página anterior quando uma sequência de tarefas falhar
Agora, você pode retornar à página anterior ao executar uma sequência de tarefas e ocorrer uma falha. Antes dessa versão, era necessário reiniciar a sequência de tarefas ao ocorrer uma falha. Por exemplo, você pode usar o botão **Anterior** nos seguintes cenários:

- Quando um computador é iniciado no Windows PE, a caixa de diálogo de inicialização da sequência de tarefas pode ser exibida antes da sequência estar disponível. Ao clicar em Avançar nesse cenário, a página final da sequência de tarefas exibe uma mensagem informando que não há sequências de tarefas disponíveis. Agora, você pode clicar em **Anterior** para pesquisar novamente por sequências de tarefas disponíveis. Você pode repetir esse processo até que a sequência de tarefas esteja disponível.
- Quando você executa uma sequência de tarefas, porém pacotes dependentes de conteúdo ainda não estão disponíveis nos pontos de distribuição, a sequência de tarefas falhará. Agora, você poderá distribuir o conteúdo ausente (se ainda não tiver sido distribuído) ou aguardar o conteúdo estar disponível nos pontos de distribuição e, em seguida, clicar em **Anterior** para que a pesquisa de sequência de tarefas pesquise novamente o conteúdo.

### <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Conteúdo de armazenamento prévio em cache para sequências de tarefas e implantações disponíveis
A partir da versão 1702, para implantações disponíveis de sequências de tarefas, é possível optar por usar o conteúdo de armazenamento prévio em cache. O conteúdo de armazenamento prévio em cache oferece a opção de permitir que o cliente baixe apenas o conteúdo aplicável assim que receber a implantação. Portanto, quando o usuário clicar em **Instalar** no Centro de Software, o conteúdo estará pronto e a instalação iniciará rapidamente, pois o conteúdo está no disco rígido local. Para obter detalhes, veja [Configurar o conteúdo de armazenamento prévio em cache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).

### <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Converter de BIOS para UEFI durante uma atualização in-loco
A Atualização do Windows 10 para Criadores apresenta uma ferramenta de conversão simples que automatiza o processo para reparticionar o disco rígido para hardware habilitado para UEFI e integra a ferramenta de conversão ao processo de atualização in-loco do Windows 7 para o Windows 10. Quando você combina essa ferramenta com a sequência de tarefas de atualização do sistema operacional e a ferramenta de OEM que converte o firmware do BIOS para UEFI, pode converter os computadores de BIOS para UEFI durante uma atualização in-loco para a Atualização do Windows 10 para Criadores. Para obter detalhes, consulte [Etapas de sequência de tarefas para gerenciar o BIOS para a conversão para UEFI](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

### <a name="improvements-to-the-install-applications-task-sequence-step"></a>Melhorias na etapa da sequência de tarefas de Instalar Aplicações
Esta versão introduziu os seguintes aprimoramentos:
- Aumentou o número máximo de aplicativos que você pode instalar para 99 na etapa de sequência de tarefas **Instalar Aplicativos**. O número máximo anterior era de 9 aplicativos.
- Ao adicionar aplicativos à etapa da sequência de tarefas **Instalar Aplicativos** no editor de sequência de tarefas, agora você pode selecionar vários aplicativos no painel **Selecionar aplicativo para instalar**.

### <a name="improvements-to-the-auto-apply-driver-task-sequence"></a>Melhorias para a sequência de tarefas do Driver de aplicação automática
Novas variáveis de sequência de tarefas estão agora disponíveis para configurar o valor de tempo limite na etapa de sequência de tarefas do Driver de aplicação automática ao fazer solicitações do catálogo HTTP. As seguintes variáveis e valores padrão (em segundos) estão disponíveis:
   - SMSTSDriverRequestResolveTimeOut  
     Padrão: 60
   - SMSTSDriverRequestConnectTimeOut  
     Padrão: 60
   - SMSTSDriverRequestSendTimeOut  
     Padrão: 60
   - SMSTSDriverRequestReceiveTimeOut  
     Padrão: 480

### <a name="windows-10-adk-tracked-by-build-version"></a>Windows 10 ADK controlado pela versão de build
O Windows 10 ADK agora é controlado pela versão de build para garantir uma experiência com mais suporte ao personalizar imagens de inicialização do Windows 10. Por exemplo, se o site usa o Windows ADK para Windows 10, versão 1607, somente as imagens de inicialização com a versão 10.0.14393 poderão ser personalizadas no console. Para obter detalhes sobre como personalizar as versões WinPE, consulte [Personalizar imagens de inicialização](/sccm/osd/get-started/customize-boot-images).

### <a name="default-boot-image-source-path-can-no-longer-be-changed"></a>O caminho de origem de imagem de inicialização padrão não pode ser alterado
As imagens de inicialização padrão são gerenciadas pelo Configuration Manager e o caminho de origem da imagem de inicialização padrão não pode mais ser alterado no console do Configuration Manager ou ao usar o SDK do Configuration Manager. Você pode continuar a configurar um caminho de origem personalizado para imagens de inicialização personalizadas.

### <a name="default-boot-images-are-regenerated-after-upgrading-configuration-manager-to-a-new-version"></a>Imagens de inicialização padrão são geradas novamente após a atualização do Configuration Manager para uma nova versão
A partir desta versão, quando você atualiza a versão do Windows ADK e usa as atualizações e instalações para instalar a versão mais recente do Configuration Manager, o Configuration Manager regenera as imagens de inicialização padrão. Inclui a nova versão da Janela PE do Windows ADK atualizado e a nova versão de personalizações, drivers e cliente, entre outros, do Configuration Manager. Imagens de inicialização personalizadas não são modificadas. Para mais detalhes, consulte [Gerenciar imagens de inicialização](/sccm/osd/get-started/manage-boot-images#BKMK_BootImageDefault).

## <a name="software-updates"></a>Atualizações de software

### <a name="deploy-office-365-apps-to-clients"></a>Implantar aplicativos do Office 365 em clientes
A partir da versão 1702, no painel de gerenciamento de clientes do Office 365, é possível iniciar o Instalador do Office 365 que permite que você defina as configurações de instalação do Office 365, baixe arquivos de CDNs (Redes de Distribuição de Conteúdo) do Office e implante os arquivos como um aplicativo no Configuration Manager. Para saber mais, veja [Gerenciar atualizações do Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps).

> [!IMPORTANT]
> O aplicativo do Office 365 que você cria e implanta usando o Assistente para aplicativo do Office 365 no Configuration Manager não é gerenciado automaticamente pelo Configuration Manager até que você habilite a configuração de agente de cliente de atualização **Habilitar o gerenciamento do cliente do Office 365 novamente**. Para obter detalhes, veja [Sobre configurações do cliente](/sccm/core/clients/deploy/about-client-settings).

### <a name="manage-express-installation-files-for-windows-10-updates"></a>Gerenciar os arquivos de instalação expressa para atualizações do Windows 10
A partir da versão 1702, o Configuration Manager oferece suporte a arquivos de instalação expressa para atualizações do Windows 10. Ao usar uma versão do Windows 10 com suporte, você poderá usar as definições do Configuration Manager para baixar somente as alterações entre a Atualização Cumulativa do Windows 10 do mês atual e a atualização do mês anterior. Sem os arquivos de instalação expressa, o Configuration Manager baixa a Atualização Cumulativa do Windows 10 (incluindo todas as atualizações dos meses anteriores) a cada mês. Usar arquivos de instalação expressa proporciona downloads menores e instalações mais rápidas nos clientes. Para obter detalhes, veja [Gerenciar os arquivos de instalação expressa para atualizações do Windows 10](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).


<!-- ## Reporting  -->

<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Gerenciamento de dispositivos móveis

### <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>As versões do Android e iOS não precisam mais ser direcionadas nos assistentes de criação do MDM híbrido

A partir da versão 1702 para MDM (gerenciamento de dispositivo móvel) híbrido, você não precisa mais indicar versões específicas do Android e do iOS ao criar novas políticas e perfis de dispositivos gerenciados pelo Intune. Em vez disso, escolha um dos seguintes tipos de dispositivo:

- Android
- Samsung KNOX Standard 4.0 e superior
- iPhone
- iPad

Essa alteração afeta os assistentes de criação dos seguintes itens:

- Itens de configuração
- Políticas de conformidade
- Perfis de certificado
- Perfis de email
- Perfis de VPN
- Perfis de Wi-Fi

Com essa alteração, as implantações híbridas podem fornecer suporte com mais rapidez para novas versões do Android e do iOS sem precisar de uma nova versão ou extensão do Configuration Manager. Assim que uma nova versão passar a ter suporte no Intune autônomo, os usuários poderão atualizar seus dispositivos móveis para essa versão.

Para evitar problemas ao atualizar de versões anteriores do Configuration Manager, as versões dos sistemas operacionais móveis ainda estarão disponíveis nas páginas de propriedades desses itens. Se você ainda precisar direcionar a uma versão específica, crie o novo item e especifique a versão de destino na página de propriedades do item recém-criado. 

> [!NOTE]
> A última versão do sistema operacional móvel disponível nas páginas de propriedades aplicam-se a essa versão e todas as versões subsequentes. As páginas de propriedades fornecem as seguintes opções para os sistemas operacionais de destino posteriores ao Android 7 e ao iOS 10: 
> - **Android 7 ou posterior**
> - **Todos os dispositivos iPhone ou iPod touch com iOS 10 ou posterior**
> - **Todos os dispositivos iOS 10 e iPad superiores**

### <a name="android-for-work-support"></a>Suporte do Android for Work
A partir da versão 1702, o gerenciamento híbrido de dispositivos móveis com o Microsoft Intune agora oferece suporte ao registro e ao gerenciamento de dispositivos do Android for Work. Orientação para dispositivo Android for Work gerenciado:

- [Registrar dispositivos Android for Work](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-enrollment)
- [Aprovar e implantar aplicativos do Android for Work](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [Criar itens de configuração para o Android for Work](/sccm/mdm/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-for-work-configuration-items)
- [Limpeza seletiva em dispositivos Android for Work](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)
- [Perfis de email para Android for Work](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [Políticas de conformidade para Android for Work](/sccm/mdm/deploy-use/create-compliance-policy)


### <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Implantar aplicativos iOS adquiridos por volume em coleções de dispositivos

Agora você pode implantar aplicativos licenciados para dispositivos, bem como os usuários. Dependendo da capacidade dos aplicativos para dar suporte ao licenciamento de dispositivos, uma licença apropriada será solicitada quando você implantá-la, da seguinte maneira:

|||||
|-|-|-|-|
|Versão do Configuration Manager|O aplicativo dá suporte ao licenciamento de dispositivos?|Tipo de coleção de implantação|Licença solicitada|
|Anterior à versão 1702|Sim|usuário|Licença de usuário|
|Anterior à versão 1702|Não|usuário|Licença de usuário|
|Anterior à versão 1702|Sim|Dispositivo|Licença de usuário|
|Anterior à versão 1702|Não|Dispositivo|Licença de usuário|
|Versão 1702 e posterior|Sim|usuário|Licença de usuário|
|Versão 1702 e posterior|Não|usuário|Licença de usuário|
|Versão 1702 e posterior|Sim|Dispositivo|Licença de dispositivo|
|Versão 1702 e posterior|Não|Dispositivo|Licença de usuário|

Para saber mais sobre aplicativos do iOS adquiridos por volume, veja [Gerenciar aplicativos iOS adquiridos por volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

### <a name="support-for-ios-volume-purchase-program-for-education"></a>Suporte para o Volume Purchase Program do iOS para educação

Agora você também pode implantar e controlar aplicativos que você adquiriu do Volume Purchase Program for Education do iOS.
Para saber mais sobre aplicativos do iOS adquiridos por volume, veja [Gerenciar aplicativos iOS adquiridos por volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

### <a name="support-for-multiple-volume-purchase-program-tokens"></a>Suporte para vários tokens do Volume Purchase Program

Agora você pode associar vários tokens de programa de compra por volume da Apple ao seu Configuration Manager.
Para saber mais sobre aplicativos do iOS adquiridos por volume, veja [Gerenciar aplicativos iOS adquiridos por volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

### <a name="support-for-line-of-business-apps-in-windows-store-for-business"></a>Suporte para aplicativos de linha de negócios na Windows Store para Empresas

Agora você pode sincronizar aplicativos personalizados de linha de negócios da Windows Store para Empresas.

### <a name="conditional-access-device-compliance-policy-improvements"></a>Aprimoramentos na política de conformidade de dispositivo de acesso condicional

Uma nova regra de política de conformidade do dispositivo está disponível para ajudar a bloquear o acesso a recursos corporativos que dão suporte ao acesso condicional, quando os usuários estão usando aplicativos que fazem parte de uma lista de aplicativos fora de conformidade. A lista de aplicativos fora de conformidade pode ser definida pelo administrador ao adicionar a nova regra de conformidade **Aplicativos que não podem ser instalados**. Essa regra exige que o administrador insira o **Nome do Aplicativo**, a **ID do Aplicativo** e o **Editor do Aplicativo** (opcional) ao adicionar um aplicativo à lista fora de conformidade. Essa configuração se aplica apenas a dispositivos iOS e Android.

Além disso, isso ajuda as organizações a reduzir o vazamento de dados por aplicativos não seguros e evita o consumo de dados excessivo por determinados aplicativos.

- Saiba mais [como as políticas de conformidade de dispositivo funcionam](/sccm/mdm/deploy-use/device-compliance-policies).
- Saiba mais [como criar políticas de conformidade de dispositivo](/sccm/mdm/deploy-use/create-compliance-policy).

### <a name="new-mobile-threat-defense-monitoring-tools"></a>Novas ferramentas de monitoramento de defesa contra ameaças móveis

A partir da versão 1702, você tem novas maneiras de monitorar o status de conformidade com seu provedor de serviços de defesa contra ameaças móveis.

- Saiba mais em [Como monitorar a conformidade de Defesa contra Ameaças Móveis](https://docs.microsoft.com/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance).

## <a name="protect-devices"></a>Proteger dispositivos

### <a name="detect-outdated-antimalware-client-versions"></a>Detectar versões desatualizadas do cliente antimalware
A partir da versão 1702, você poderá configurar um alerta para garantir que os clientes do Endpoint Protection não estejam desatualizados. Para saber mais, veja [Alerta de cliente de malware desatualizado](/sccm/protect/deploy-use/endpoint-configure-alerts#detect-outdated-antimalware-client-versions).

### <a name="device-health-attestation-updates"></a>Atualizações do atestado de integridade do dispositivo
O serviço de atestado de integridade do dispositivo para clientes locais agora pode ser configurado e gerenciado do ponto de gerenciamento. Para saber mais, veja [Atestado de integridade](/sccm/core/servers/manage/health-attestation).

### <a name="certificate-profiles-for-windows-hello-for-business"></a>Perfis de certificado para o Windows Hello para Empresas

Se você pretende armazenar perfis de certificado no contêiner de chaves do Windows Hello para Empresas, e o perfil de certificado usa o EKU de Logon de Cartão Inteligente, deverá configurar permissões para registro de chave para garantir que o certificado seja validado corretamente.
Para saber mais, veja as [Configurações para Windows Hello para Empresas](/sccm/protect/deploy-use/windows-hello-for-business-settings).

### <a name="new-windows-hello-for-business-notification-for-end-users"></a>Nova notificação do Windows Hello para Empresas para usuários finais
Uma nova notificação do Windows 10 informa aos usuários finais que eles devem executar ações adicionais para concluir a instalação do Windows Hello para Empresas (por exemplo, definir um PIN).
