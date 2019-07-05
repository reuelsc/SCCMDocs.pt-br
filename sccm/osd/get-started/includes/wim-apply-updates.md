---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 05/28/2019
ms.openlocfilehash: 1f809ca6499b502520a7662d9947f0799369bef2
ms.sourcegitcommit: 4981a796e7886befb7bdeeb346dba32be82aefd6
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67534559"
---
## <a name="BKMK_OSImagesApplyUpdates"></a> Aplicar atualizações de software a uma imagem

> [!Note]  
> Esta seção se aplica a **imagens do sistema operacional** e a **pacotes de atualização do sistema operacional**. Ela usa o termo geral "imagem" para referir-se ao arquivo WIM (imagem do Windows). Ambos esses objetos têm uma WIM, que contém os arquivos de instalação do Windows. Atualizações de software são aplicáveis a esses arquivos em ambos os objetos. O comportamento desse processo é o mesmo entre os dois objetos.  

A cada mês, há novas atualizações de software aplicáveis à imagem. Antes de aplicar as atualizações de software, você precisará dos seguintes pré-requisitos:

- Uma infraestrutura de atualizações de software  
- Atualizações de software sincronizadas com êxito  
- Baixadas as atualizações de software para a biblioteca de conteúdo no servidor do site  

Para mais informações, consulte [Implantar atualizações de software](/sccm/sum/deploy-use/deploy-software-updates).  

Aplique as atualizações de software relevantes a uma imagem em um agendamento especificado. Esse processo às vezes é chamado de *manutenção offline*. Nessa agenda, o Configuration Manager aplica a atualizações de software selecionadas à imagem. Ele então também pode redistribuir a imagem atualizada para pontos de distribuição.

> [!Important]  
> Embora você possa selecionar qualquer atualização de software aplicável para a imagem com base na versão, o DISM pode aplicar somente determinados tipos de atualizações à imagem. O arquivo **OfflineServicingMgr.log** mostra a seguinte entrada: `Not applying this update binary, it is not supported`.<!-- SCCMDocs issue 1324 -->

O banco de dados armazena informações sobre a imagem, incluindo as atualizações de software que foram aplicadas no momento da importação. As atualizações de software aplicadas à imagem desde que ela foi inicialmente adicionada também são armazenadas no banco de dados do site. Quando você inicia o Assistente para aplicar atualizações de software, ele recupera a lista de atualizações de software aplicáveis que o site ainda não tenha aplicado à imagem. O Configuration Manager copia as atualizações de software que você seleciona na biblioteca de conteúdo no servidor do site. Em seguida, ele aplica as atualizações de software à imagem.  

### <a name="servicing-process"></a>Processo de manutenção

1. No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione **Imagens do Sistema Operacional** ou **Pacotes de Atualização do Sistema Operacional**.  

2. Selecione o objeto ao qual deseja aplicar as atualizações de software.  

3. Na faixa de opções, selecione **Agendar Atualizações** para iniciar o assistente.  

4. Na página **Escolher Atualizações**, selecione as atualizações de software a serem aplicadas à imagem. Pode levar algum tempo para que a lista de atualizações apareça no assistente. Use o **filtro** para pesquisar cadeias de caracteres nos metadados. Use a lista suspensa **Arquitetura do sistema** para filtrar **X86**, **X64** ou **Todos**. Você pode selecionar uma, várias ou todas as atualizações nessa lista. Quando você terminar de selecionar atualizações, selecione **Próxima**.  

5. Na página **Definir Agendamento** , especifique as seguintes configurações e clique em **Próximo**.  

    1. **Agenda**: especifique o agendamento para quando o site se aplica as atualizações de software à imagem.  

    2. **Continuar se houver erro**: selecione essa opção para continuar a aplicar as atualizações de software à imagem em caso de erro.  

    3. **Atualizar pontos de distribuição com a imagem**: selecione essa opção para atualizar a imagem nos pontos de distribuição depois que o site aplicar as atualizações de software.  

6. Conclua o Assistente de Agendar Atualizações.  

> [!NOTE]  
> Para minimizar o tamanho do conteúdo, a manutenção dos pacotes de atualização do sistema operacional e das imagens do sistema operacional remove a versão mais antiga.  

### <a name="servicing-operations"></a>Operações de manutenção

No console do Configuration Manager, no nó **Imagens do Sistema Operacional** ou **Pacotes de Atualização do Sistema Operacional**, adicione as seguintes colunas à exibição:

- **Data de Atualizações Agendada**: essa propriedade mostra o próximo agendamento que você definiu.  
- **Atualizações de Status Agendadas**: essa propriedade mostra o status. Por exemplo, **Bem-sucedido** ou **Em processo**.  

Selecione um objeto de imagem específica e, em seguida, alterne para a guia **Status de Atualização** no painel de detalhes. Essa guia mostra a lista de atualizações na imagem.

Selecione um objeto de imagem específica e, em seguida, selecione **Propriedades** na faixa de opções. A guia **Atualizações Instaladas** mostra a lista de atualizações na imagem. A guia **Manutenção** é uma exibição somente leitura da agenda de manutenção atual e das atualizações que você programou para aplicar.

Quando o status é **Em processo**, você pode selecionar **Cancelar Atualizações Agendadas** na faixa de opções. Essa ação cancelará o processo de manutenção ativo.

Para solucionar problemas desse processo, exiba os arquivos **OfflineServicingMgr.log** e **dism.log** no servidor do site. Para obter mais informações, consulte [Arquivos de log](/sccm/core/plan-design/hierarchy/log-files).

### <a name="bkmk_servicing-drive"></a> Especificar a unidade para manutenção offline de imagem do sistema operacional

<!--1358924-->

Da versão 1810 em diante, especifique a unidade que o Configuration Manager usa durante a manutenção offline de imagens do sistema operacional. Esse processo pode consumir uma grande quantidade de espaço em disco com arquivos temporários. Essa opção oferece flexibilidade para selecionar a unidade a ser usada.

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**. Na faixa de opções, clique em **Configurar Componentes do Site** e selecione **Implantação de Sistema Operacional**.  

2. Na guia **Manutenção Offline**, especifique a opção para **Uma unidade local a ser usada pela manutenção offline de imagens**.  

Por padrão, essa configuração é **Automática**. Com esse valor, o Configuration Manager escolhe a unidade na qual ele é instalado.

Se você selecionar uma unidade que não existe no servidor do site, o Configuration Manager se comportará da mesma que se você selecionasse **Automático**.

Durante a manutenção offline, o Configuration Manager armazena arquivos temporariamente em uma pasta, `<drive>:\ConfigMgr_OfflineImageServicing`. Ele também cria imagem do sistema operacional nessa pasta.

### <a name="bkmk_resetbase"></a> Serviço de imagens otimizadas

<!--3555951-->

Começando na versão 1902, quando você aplica as atualizações de software a uma imagem do sistema operacional, há uma nova opção para otimizar a saída removendo as atualizações substituídas. A otimização do serviço offline só se aplica a imagens com um único índice.

Quando você agenda o site para aplicar atualizações de software a uma imagem do sistema operacional, ele usa a ferramenta de linha de comando DISM (Gerenciamento e Manutenção de Imagens de Implantação) do Windows. Durante o processo de serviço, essa alteração acrescenta as duas etapas adicionais a seguir:  

- Ele executa o DISM em relação à imagem offline montada com os parâmetros `/Cleanup-Image /StartComponentCleanup /ResetBase`. Se esse comando falhar, o processo de serviço atual falhará. Ele não confirma as alterações na imagem.  

- Depois que o Configuration Manager confirma as alterações na imagem e o desmonta-o do sistema de arquivos, ele exporta a imagem para outro arquivo. Esta etapa usa o parâmetro do DISM `/Export-Image`. Ele remove arquivos desnecessários da imagem, o que reduz o tamanho.  

A Microsoft recomenda que você aplique as atualizações regularmente às imagens offline. Você não precisa usar essa opção sempre que aplicar um serviço a uma imagem. Quando você faz esse processo mensalmente, o uso dessa nova opção fornece o máximo de benefício ao longo do tempo. Para obter mais informações, consulte [Recomendações para a etapa de instalar atualizações de software](/sccm/osd/understand/install-software-updates#recommendations).

Embora essa opção ajude a reduzir o tamanho geral da imagem atendida, ela aumenta o tempo para concluir o processo. Use o assistente para agendar o serviço durante horários convenientes. Ele também exige armazenamento adicional no servidor do site. Você pode personalizar o site para usar um local alternativo. Para obter mais informações, confira [Especificar a unidade para serviço de imagens do sistema operacional offline](#bkmk_servicing-drive).

#### <a name="process-to-optimize-image-servicing"></a>Processo para otimizar o serviço de imagens

1. Iniciar o [processo de serviço](#servicing-process).  

2. Na página **Definir Agendamento**, selecione a opção de **Remove atualizações substituídas depois que a imagem for atualizada**. Essa opção não é habilitada automaticamente. Se a imagem tiver mais de um índice, você não poderá usar essa opção.  

3. Para agendar o serviço de imagens, conclua o assistente.  

Valide e monitore o processo usando o **OfflineServicing.log**.
