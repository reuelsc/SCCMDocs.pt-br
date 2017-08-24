---
title: "Gerenciar configurações de atualizações de software | Microsoft Docs"
description: "Saiba mais sobre as configurações do cliente que são apropriadas para as atualizações de software em seu site depois de instalar o ponto de atualização de software."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 03/26/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 0d484c1a-e903-4bff-9e9b-e452c62e38a8
ms.openlocfilehash: fe4a8f56e0b554e206bcc4503a0268dc761ded81
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
#  <a name="BKMK_ManageSUSettings"></a> Gerenciar configurações de atualizações de software  

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Depois de sincronizar as atualizações de software no Configuration Manager, defina e verifique as configurações nas seções a seguir.

##  <a name="BKMK_ClientSettings"></a> Configurações do cliente para atualizações de software  
Após a instalação do ponto de atualização de software, as atualizações de software serão habilitadas em clientes por padrão e as configurações na página **Atualizações de Software** nas configurações do cliente terão valores padrão. As configurações de cliente são usadas em todo o site e afetam a frequência com que as atualizações de software são verificadas quanto à conformidade, bem como o modo e a frequência com que as atualizações de software são instaladas em computadores cliente. Antes de você implantar atualizações de software, verifique se as configurações do cliente são apropriadas para as atualizações de software em seu site.  

> [!IMPORTANT]  
>  A configuração **Habilitar as atualizações de software em clientes** é habilitada por padrão. Se você desmarcar essa configuração, o Configuration Manager removerá as políticas de implantação existentes do cliente.  

Para obter informações sobre como definir as configurações do cliente, consulte [Como definir as configurações do cliente](../../core/clients/deploy/configure-client-settings.md).  

Para mais informações sobre essas configurações do cliente, consulte [Sobre as configurações do cliente](../../core/clients/deploy/about-client-settings.md).  

##  <a name="BKMK_GroupPolicy"></a> Configurações de política de grupo para atualizações de software  
Há configurações específicas de política de grupo que são usadas pelo WUA (Windows Update Agent) em computadores cliente para se conectar ao WSUS que é executado no ponto de atualização de software. Essas configurações de política de grupo também são usadas para verificar com êxito a conformidade da atualização de software e atualizar automaticamente as atualizações de software e o WUA.

### <a name="specify-intranet-microsoft-update-service-location-local-policy"></a>Política local Especificar o local do serviço do Microsoft Update na intranet  
Quando o ponto de atualização de software é criado para um site, os clientes recebem uma política de computador que fornece o nome do servidor do ponto de atualização de software e configurar a política local **Especificar o local do serviço de atualização na intranet da Microsoft** no computador. O WUA recupera o nome do servidor que está especificado na política **Configurar o serviço de atualização da intranet para detectar atualizações** e se conecta a esse servidor quando verifica a conformidade das atualizações de software. Quando uma política de domínio é criada para a configuração **Especificar o local do serviço do Microsoft Update na intranet** , ela substitui a política local e o WUA provavelmente se conecta a outro servidor que não seja o ponto de atualização de software. Se isso acontecer, é provável que o cliente verifique a conformidade da atualização de software baseado em diferentes produtos, classificações e idiomas. Portanto, você não deve configurar a política do Active Directory para computadores cliente.  

### <a name="allow-signed-content-from-intranet-microsoft-update-service-location-group-policy"></a>Política de grupo Permitir conteúdo assinado do local do serviço do Microsoft Update da intranet  
Você deve habilitar a configuração da Política de Grupo **Permitir conteúdo assinado do local do serviço de atualização da intranet da Microsoft** antes do WUA verificar as atualizações de software que foram criadas e publicadas com o System Center Updates Publisher. Habilitada a configuração de política, o WUA aceitará as atualizações de software que foram recebidas através de um local de intranet se as atualizações de software são assinadas no repositório de certificados de **Editores Confiáveis** no computador local. Para obter mais informações sobre as configurações de Política de Grupo necessárias para o Updates Publisher, consulte [Biblioteca de documentação do Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=232476).  

### <a name="automatic-updates-configuration"></a>Configuração de atualizações automáticas  
As Atualizações Automáticas permitem que as atualizações de segurança e outros downloads importantes sejam recebidos em computadores cliente. As Atualizações Automáticas são definidas na configuração da Política de Grupo **Configurar Atualizações Automáticas** ou no Painel de Controle no computador local. Quando as Atualizações Automáticas são habilitadas, os computadores cliente recebem notificações de atualização e, dependendo das configurações definidas, eles baixam e instalam as atualizações necessárias. Quando as Atualizações Automáticas coexistem com as atualizações de software, é possível que cada computador cliente exiba ícones de notificação e notificações de exibição pop-up para a mesma atualização. Além disso, quando é necessário reiniciar, cada computador cliente pode exibir uma caixa de diálogo de reinicialização para a mesma atualização.  

### <a name="self-update"></a>Autoatualização  
Quando as Atualizações Automáticas são habilitadas em computadores cliente, o WUA executa automaticamente uma autoatualização quando uma versão mais recente está disponível ou quando há problemas com um componente do WUA. Quando as Atualizações Automáticas não são configuradas ou são desabilitadas e os computadores cliente têm uma versão mais recente do WUA, os computadores cliente devem executar o arquivo de instalação do WUA.  

## <a name="software-updates-properties"></a>Propriedades de atualizações de software
As propriedades de atualização de software fornecem informações sobre atualizações de software e conteúdo associado. Você também pode usar essas propriedades para definir configurações para atualizações de software. Ao abrir as propriedades das diversas atualizações de software, somente as guias **Tempo Máximo de Execução** e **Severidade Personalizada** serão exibidas.   

Use o procedimento a seguir para abrir as propriedades de atualização de software.  

#### <a name="to-open-software-update-properties"></a>Para abrir as propriedades de atualização de software  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  
2.  No espaço de trabalho Biblioteca de Software, expanda **Atualizações de Software**e clique em **Todas as Atualizações de Software**.  
3.  Selecione uma ou mais atualizações de software e clique na guia **Início** e clique em **Propriedades** no grupo **Propriedades** .  

   > [!NOTE]  
   >  No nó **Todas as Atualizações de Software**, o Configuration Manager exibirá somente atualizações de software com classificação **Crítica** e **Segurança** e que foram lançadas nos últimos 30 dias.  

###  <a name="BKMK_SoftwareUpdatesInformation"></a> Examinar informações de atualizações de software  
Nas propriedades de atualização de software, você pode analisar informações detalhadas sobre uma atualização de software. As informações detalhadas não serão exibidas quando você selecionar mais de uma atualização de software. As seções a seguir descrevem as informações disponíveis para uma atualização de software selecionada.  

####  <a name="BKMK_SoftwareUpdateDetails"></a> Detalhes da atualização de software  
Na guia **Detalhes da Atualização** , é possível exibir as seguintes informações de resumo sobre a atualização de software selecionada:  

- **ID do Boletim**: especifica a ID do boletim associada às atualizações do software de segurança. Você pode encontrar detalhes do boletim de segurança pesquisando a ID do boletim na página da Web [Pesquisa de boletim de segurança da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=58313) .  

- **ID do Artigo**: especifica a ID do artigo para a atualização do software. O artigo referenciado fornece informações mais detalhadas sobre a atualização do software e o problema que essa atualização corrige ou melhora.  

- **Data de revisão**: especifica a data em que a atualização de software foi modificada pela última vez.  

- **Classificação de severidade máxima**: especifica a classificação de severidade definida pelo fornecedor para a atualização de software.  

- **Descrição**: fornece uma visão geral sobre qual condição a atualização de software corrige ou melhora.  

- **Idiomas aplicáveis**: lista os idiomas para os quais a atualização de software é aplicável.  

- **Produtos afetados**: lista os produtos para os quais a atualização de software é aplicável.  

####  <a name="BKMK_ContentInformation"></a> Informações de conteúdo  
Na guia **Informações de Conteúdo** , revise as seguintes informações sobre o conteúdo associado à atualização de software selecionada:  

-   **ID do Conteúdo**: especifica a ID do conteúdo de atualização do software.  

-   **Baixado**: indica se o Configuration Manager baixou os arquivos de atualização do software.  

-   **Idioma**: especifica os idiomas para a atualização do software.  

-   **Caminho de Origem**: especifica o caminho para os arquivos de origem de atualização do software.  

-   **Tamanho (MB)**: especifica o tamanho dos arquivos de origem de atualização do software.  

####  <a name="BKMK_CustomBundleInformation"></a> Informações do grupo personalizado  
Na guia **Informações do Grupo Personalizado** , revise as informações do grupo personalizado para a atualização de software. Quando a atualização de software selecionada contém atualizações de software agrupadas que estão contidas no arquivo de atualização de software, elas são exibidas na seção **Informações do grupo** . Essa guia não exibe atualizações de software agrupadas que são exibidas na guia **Informações de Conteúdo** , como arquivos de atualização para idiomas diferentes.  

####  <a name="BKMK_SupersedenceInformation"></a> Informações da substituição  
Na guia **Informações da Substituição** , você pode exibir as seguintes informações sobre a substituição da atualização de software:  

- **Esta atualização foi substituída pelas seguintes atualizações**: especifica as atualizações de software que substituem essa atualização, o que significa que as atualizações listadas são mais recentes. Na maioria dos casos, você implantará uma das atualizações de software que substitui a atualização de software. As atualizações de software exibidas na lista contêm hiperlinks para páginas da Web que fornecem mais informações sobre as atualizações de software. Quando essa atualização não é substituída, **Nenhum** é exibido.  

- **Esta atualização substitui as seguintes atualizações**: especifica as atualizações de software que são substituídas por essa atualização de software, o que significa que essa atualização é mais recente. Na maioria dos casos, você implantará essa atualização de software para substituir as atualizações de software obsoletas. As atualizações de software exibidas na lista contêm hiperlinks para páginas da Web que fornecem mais informações sobre as atualizações de software. Quando essa atualização não substitui nenhuma outra atualização, **Nenhum** é exibido.  

###  <a name="BKMK_SoftwareUpdatesSettings"></a> Definir as configurações de atualizações de software  
Em propriedades, você pode definir as configurações de atualização de software para uma ou mais atualizações de software. Você pode definir a maioria das configurações de atualização de software somente no site de administração central ou no site primário autônomo. As seções a seguir ajudarão você a definir as configurações para atualizações de software.  

####  <a name="BKMK_SetMaxRunTime"></a> Definir tempo de execução máximo  
Na guia **Tempo Máximo de Execução** , defina a quantidade máxima de tempo que uma atualização de software tem alocada para ser concluída em computadores cliente. Se a atualização demorar mais do que o valor máximo do tempo de execução, o Configuration Manager criará uma mensagem de status e interromperá o monitoramento da implantação da instalação das atualizações de software. Você pode definir essa configuração somente no site de administração central ou em um site primário autônomo.  

O Configuration Manager também usa essa configuração para determinar se deve iniciar a instalação da atualização de software dentro de uma janela de manutenção configurada. Se o valor máximo do tempo de execução for maior do que o tempo restante disponível na janela de manutenção, a instalação das atualizações de software serão adiadas até o início da próxima janela de manutenção. Quando existirem várias atualizações de software para serem instaladas em um computador cliente com uma janela de manutenção configurada (período), a atualização de software com o tempo máximo de execução mais baixo será instalada primeiro; em seguida, a atualização de software com o próximo tempo máximo de execução mais baixo será instalada e assim por diante. Antes da instalação de cada atualização de software, o cliente verifica se a janela de manutenção disponível fornecerá tempo suficiente para a instalar a atualização de software. Após o início da instalação da atualização de software, ela continuará sendo instalada mesmo se a instalação ultrapassar o final da janela de manutenção. Para obter mais informações sobre janelas de manutenção, consulte [Como usar janelas de manutenção no System Center Configuration Manager](../../core/clients/manage/collections/use-maintenance-windows.md).  

Na guia **Tempo Máximo de Execução** , você pode exibir e definir as seguintes configurações:  

- **Tempo de execução máximo**: especifica o número máximo de minutos alocado para que uma instalação de atualização de software seja concluída antes que ela deixe de ser monitorada pelo Configuration Manager. Essa configuração também é usada para determinar se há tempo disponível suficiente restante para instalar a atualização antes do final de uma janela de manutenção. A configuração padrão é 60 minutos para service packs. Para outros tipos de atualização de software, o padrão será 10 minutos, se você tiver feito uma instalação nova do Configuration Manager versão 1511 ou posterior e 5 minutos quando você tiver atualizado de uma versão anterior. Os valores podem variar de 5 a 9999 minutos.  

> [!IMPORTANT]  
>  Verifique se você definiu o valor do tempo máximo de execução como inferior ao tempo da janela de manutenção configurada. Caso contrário, a instalação da atualização de software nunca será iniciada.  

####  <a name="BKMK_SetCustomSeverity"></a> Definir severidade personalizada  
Nas propriedades de uma atualização de software, você pode usar a guia **Severidade Personalizada** para configurar valores de severidade personalizada para as atualizações de software. Isso pode ser necessário se os valores de severidade predefinidos não atenderem às suas necessidades. Os valores personalizados estão listados na coluna **Severidade Personalizada** no console do Configuration Manager. Você pode classificar as atualizações de software pelos valores de severidade personalizada definidos e também pode criar consultas e relatórios que podem filtrar esses valores. Você pode definir essa configuração somente no site de administração central ou no site primário autônomo.  

Você pode definir as configurações a seguir na guia **Severidade Personalizada** .  

- **Severidade personalizada**: define um valor de severidade personalizada para as atualizações de software. Selecione **Crítico**, **Importante**, **Moderado**ou **Baixo** na lista. Por padrão, o valor da severidade personalizada está vazio.

## <a name="crl-checking-for-software-updates"></a>Verificação de CRL para atualizações de software
Por padrão, a CRL (lista de certificados revogados) não é verificada ao checar a assinatura nas atualizações de software do System Center Configuration Manager. Verificar a CRL sempre que um certificado é usado oferece mais segurança contra o uso de certificado revogado, mas gera atraso de conexão e incorre em processamentos adicionais no computador em que a verificação é executada.  

Se usada, a verificação da CRL deverá ser habilitada nos consoles do Configuration Manager que processam atualizações de software.  

#### <a name="to-enable-crl-checking"></a>Para habilitar a verificação da CRL  
No computador que executa a verificação de CRL, no DVD do produto, execute o seguinte prompt de comando: **\SMSSETUP\BIN\X64\\**<*idioma*>**\UpdDwnldCfg.exe /checkrevocation**.  

Por exemplo, para inglês (EUA), execute **\SMSSETUP\BIN\X64\00000409\UpdDwnldCfg.exe /checkrevocation**  
