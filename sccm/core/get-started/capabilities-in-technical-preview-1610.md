---
title: Funcionalidades no Technical Preview 1610 do Configuration Manager
description: "Saiba mais sobre os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1610."
ms.custom: na
ms.date: 01/23/2017
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.topic: article
ms.assetid: 8b31fd3e-875a-4a31-9498-5b050aadce32
caps.latest.revision: 2
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 5d08d1f9ccd995d544c3c21c4af52ede73343077
ms.openlocfilehash: 59633ce68e2bb2d722900215751f345d6d098721
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017

---
# <a name="capabilities-in-technical-preview-1610-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1610 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*



Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1610. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview.      Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de um technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos em um technical preview.    


**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  
## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrar por tamanho do conteúdo em regras de implantação automática
Agora, você pode filtrar o tamanho do conteúdo para atualizações de software em regras de implantação automática. Por exemplo, você pode definir o filtro **Tamanho do Conteúdo (KB)** como **< 2048** para baixar apenas atualizações de software menores que 2 MB. Usar esse filtro impede que atualizações de software grandes sejam baixadas automaticamente, para dar melhor suporte à manutenção simplificada de nível inferior do Windows quando a largura de banda de rede é limitada. Para obter detalhes, consulte [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/) (Configuration Manager e Serviço do Windows simplificado em sistemas operacionais de nível inferior).

#### <a name="to-configure-the-content-size-field"></a>Para configurar o campo Tamanho do Conteúdo
Para configurar o campo **Tamanho do Conteúdo (KB)**, vá até a página **Atualizações de Software** no Assistente Criar Regra de Implantação Automática quando você cria uma ADR ou vá até a guia **Atualizações de Software** nas propriedades de uma ADR existente.

![Campo Tamanho do Conteúdo](media/contentsizefield.png)

## <a name="improved-functionality-for-required-software-dialogs"></a>Funcionalidade aprimorada para caixas de diálogo do software necessárias
Quando um usuário receber software obrigatório, na configuração **Suspender e lembrar dentro de:** ele pode selecionar na seguinte lista suspensa de valores:
- Mais tarde: especifica que as notificações são agendadas com base nas configurações de notificação definidas nas configurações do Agente Cliente.
- Tempo fixo: especifica que a notificação será agendada para ser exibida novamente após o tempo selecionado. Por exemplo, se o usuário selecionar 30 minutos, a notificação será exibida novamente em 30 minutos.

![Página do Agente de Computador nas configurações do Agente Cliente](media/computeragentsettings.png)

O tempo máximo de adiamento sempre se baseia nos valores de notificação definidos nas configurações do Agente Cliente em cada ponto na linha do tempo de implantação. Por exemplo, se a configuração **Prazo de implantação superior a 24 horas, lembrar o usuário a cada (horas)** na página do Agente de Computador estiver definida como 10 horas e demorar mais de 24 horas até o prazo em que a caixa de diálogo será iniciada, o usuário verá um conjunto de opções de adiamento de até 10 horas, mas nunca superior a esse valor. Conforme o prazo se aproximar, a caixa de diálogo mostrará menos opções, consistentes com as configurações do Agente Cliente relevantes para cada componente da linha do tempo de implantação.

Além disso, para uma implantação de alto risco, como uma sequência de tarefas que implanta um sistema operacional, a experiência de notificação do usuário final agora será mais invasiva. Em vez de uma notificação transitória na barra de tarefas, cada vez que o usuário for notificado de que uma manutenção de software crítica é necessária, uma caixa de diálogo como a seguinte será exibida no computador:

![Caixa de diálogo Software Exigido](media/requiredsoftwaredialog.png)


Para obter mais informações:
- [Configurações para gerenciar implantações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [Como definir as configurações do cliente](../clients/deploy/configure-client-settings.md)

## <a name="deny-previously-approved-application-requests"></a>Negar solicitações de aplicativos aprovadas anteriormente

Como administrador, agora você pode negar uma solicitação de aplicativo aprovada anteriormente. Uma vez que a solicitação for negada, para instalar o aplicativo posteriormente os usuários precisarão reenviar a solicitação. A negação não desinstala o aplicativo, ela apenas força a reaprovação de qualquer nova solicitação do aplicativo em questão para o usuário. Anteriormente, a negação de solicitação do aplicativo só estava disponível para solicitações de aplicativos que não tinham sido aprovadas.

#### <a name="try-it-out"></a>Experimente
Para negar uma solicitação de aplicativo aprovada:

1.    No console do Configuration Manager, [crie e implante um aplicativo](https://docs.microsoft.com/en-us/sccm/apps/deploy-use/create-applications) que requer aprovação.
2.    Em um computador cliente, abra o Centro de Software e envie uma solicitação para o aplicativo.
3.    No console do Configuration Manager, aprove a solicitação do aplicativo.
4.    Negue a solicitação do aplicativo aprovado: no console do Configuration Manager, navegue até **Biblioteca de Software** > **Visão Geral** > **Gerenciamento de Aplicativo** > **solicitações de aprovação** e selecione a solicitação de aplicativo que deseja negar.  Na faixa de opções, clique em **Negar**.

## <a name="exclude-clients-from-automatic-upgrade"></a>Excluir clientes da atualização automática
O Technical Preview 1610 apresenta uma nova configuração que você pode usar para excluir uma coleção de clientes e impedir que instalem automaticamente versões atualizadas dos clientes.  Ela se aplica à atualização automática, bem como a outros métodos, como a atualização baseada na atualização de software, scripts de logon e políticas de grupo. Pode ser usada para uma coleção de computadores que precisam de maior atenção ao atualizar o cliente. Um cliente que estiver em uma coleção excluída ignorará todas as solicitações para instalar o software cliente atualizado.

### <a name="configure-exclusion-from-automatic-upgrade"></a>Configurar a exclusão da atualização automática
Para configurar exclusões de atualizações automáticas:
1.    No console do Configuration Manager, abra **Configurações da Hierarquia** em **Administração > Configuração do Site > Sites** e selecione a guia **Atualizar Cliente**.
2.    Marque a caixa de seleção **Excluir clientes especificados da atualização** e, para **Coleção de exclusão**, selecione a coleção que deseja excluir. É possível selecionar apenas uma coleção para exclusão.
3.    Clique em **OK** para fechar e salvar a configuração. Em seguida, após os clientes atualizarem a política, os clientes na coleção excluída não instalarão automaticamente as atualizações no software cliente.

  ![Configurações para exclusão de atualizações automáticas](media/automatic_upgrade_exclusion.png)

> [!NOTE]
> Embora a interface do usuário afirme que os clientes não serão atualizados por meio de nenhum método, dois métodos podem ser usados para substituir essas configurações. A instalação do cliente por push e uma instalação manual do cliente podem ser usadas para substituir essa configuração. Para obter mais detalhes, veja a seção seguir.

### <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>Como atualizar um cliente que está em uma coleção excluída
Desde que uma coleção esteja configurada para ser excluída, os membros dessa coleção só poderão atualizar o software cliente usando um dos dois métodos, que substituem a exclusão:
 - **Instalação do cliente por push** – você pode usar a instalação do cliente por push para atualizar um cliente que está em uma coleção excluída. Isso é permitido pois é considerado que seja a intenção do administrador, e permite que você atualize os clientes sem remover toda a coleção da exclusão.       
 - **Instalação manual do cliente** – você pode atualizar manualmente os clientes que estão em uma coleção excluída quando usa a seguinte opção de linha de comando com ccmsetup:  ***/ignoreskipupgrade***

  Se você tentar atualizar manualmente um cliente que é um membro da coleção excluída e não usar essa opção, o cliente não instalará o novo software cliente. Para obter mais informações, consulte [Como instalar manualmente os clientes do Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-configuration-manager-clients-manually).

Para obter mais informações sobre os métodos de instalação de clientes, consulte [Como implantar clientes em computadores Windows no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).

## <a name="windows-defender-configuration-settings"></a>Definições de configuração do Windows Defender

Agora você pode definir as configurações de cliente do Windows Defender em computadores Windows 10 registrados no Intune usando itens de configuração no console do Configuration Manager.

Especificamente, você pode definir as seguintes configurações do Windows Defender:
- Permitir monitoramento em tempo real
- Permitir o monitoramento de comportamento
- Ativar o sistema de inspeção de rede
- Verificar todos os downloads
- Permitir a verificação de script
- Monitorar a atividade de arquivos e programas
  - Arquivos monitorados
- Dias para rastrear malwares resolvidos
- Permitir acesso à interface do usuário do cliente
- Agendar uma verificação do sistema
  - Dia do agendamento
  - Hora do agendamento
- Agendar uma verificação rápida diária
  - Hora do agendamento
- Limitar o percentual de uso da CPU durante uma verificação de arquivos mortos
- Verificar mensagens de email
- Verificar unidades removíveis
- Verificar unidades mapeadas
- Verificar arquivos abertos em compartilhamentos de rede
- Intervalo de atualização de assinatura
- Permitir proteção da nuvem
- Solicitar amostras aos usuários
- Detecção de aplicativos potencialmente indesejados
- Arquivos/pastas excluídos
- Extensões de arquivo excluídos
- Processos excluídos

> [!NOTE]
> Essas configurações podem ser definidas apenas em computadores cliente que executam o Windows 10 com a Atualização de novembro (1511) e superior.

### <a name="try-it-out"></a>Experimente!

1.    No console do Configuration Manager, clique em **Ativos e Conformidade** > **Visão Geral** > **Configurações de Conformidade** > **Itens de Configuração** e crie um novo **Item de Configuração**.
2.    Insira um nome, selecione **Windows 8.1 e Windows 10** em **Configurações para dispositivos gerenciados sem o cliente do Configuration Manager** e clique em **Avançar**.
3.    Verifique se **Todos os Windows 10 (64 bits)** e **Todos os Windows 10 (32 bits)** estão selecionados na página **Plataformas com Suporte** e, em seguida, clique em **Avançar**.
4.    Selecione o grupo de configurações **Windows Defender** e clique em **Avançar**.
5.    Defina as configurações desejadas nesta página e clique em **Avançar**.
6.    Conclua o assistente.
7.    Adicione este item de configuração a uma linha de base de configuração e implante essa linha de base em computadores que executam o Windows 10 com Atualização de novembro (1511) ou superior.

> [!NOTE]
> Lembre-se de marcar a caixa de seleção **Corrigir as configurações não compatíveis** ao implantar a linha de base de configuração.

## <a name="request-policy-sync-from-administrator-console"></a>Solicitar sincronização de política no console do administrador

Agora você pode solicitar uma sincronização de política em um dispositivo móvel no console do Configuration Manager, em vez de precisar solicitar uma sincronização no próprio dispositivo. As informações de estado da solicitação de sincronização ficam disponíveis como uma nova coluna as exibições do dispositivo, chamada **Estado de Sincronização Remota**. O estado também aparece na seção **Dados de descoberta** na caixa de diálogo **Propriedades** para cada dispositivo móvel.

### <a name="try-it-out"></a>Experimente!

1.    No console do Configuration Manager, acesse **Ativos e Conformidade** > **Visão Geral** > Dispositivos.
2.    No menu **Ações de Dispositivo Remoto**, selecione **Enviar Solicitação de Sincronização**.

A sincronização pode levar de cinco a dez minutos. Todas as alterações em políticas são sincronizadas com o dispositivo. Você pode acompanhar o estado da solicitação de sincronização na coluna **Estado de Sincronização Remota** na exibição **Dispositivos** ou na caixa de diálogo **Propriedades** do dispositivo.

## <a name="additional-security-role-support"></a>Suporte a funções de segurança adicionais

Além de Administrador Completo, as seguintes funções de segurança internas agora têm acesso completo aos itens no nó **Todos os dispositivos corporativos**, incluindo **Dispositivos Pré-Declarados**, **Perfis de Registro do iOS** e **Perfis de Registro do Windows**: •   **Gerenciador de Ativos** •   **Gerenciador de Acesso ao Recurso da Empresa**

O acesso somente leitura para essas áreas do console do Configuration Manager ainda é concedido à função de **Analista somente leitura**.

## <a name="conditional-access-for-windows-10-vpn-profiles"></a>Acesso condicional para perfis de VPN do Windows 10

Agora é possível exigir que dispositivos Windows 10, registrados no Azure Active Directory, sejam compatíveis para terem acesso VPN por meio de perfis de VPN do Windows 10 criados no console do Configuration Manager. Isso é possibilitado pela nova caixa de seleção **Habilitar o acesso condicional para esta conexão VPN** na página **Método de Autenticação** no assistente de perfil VPN e nas propriedades de perfil VPN para perfis VPN do Windows 10. Também será possível especificar um certificado diferente para autenticação de logon único se você habilitar o acesso condicional para o perfil.

## <a name="see-also"></a>Consulte também
[Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md)

