---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 11/27/2018
ms.openlocfilehash: f6e46f8b0bf985eae87cd5157f8a82af5fa0b849
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142571"
---
##  <a name="BKMK_OSImagesApplyUpdates"></a> Aplicar atualizações de software a uma imagem  

> [!Note]  
> Esta seção se aplica a **imagens do sistema operacional** e a **pacotes de atualização do sistema operacional**. Ela usa o termo geral "imagem" para referir-se ao arquivo WIM (imagem do Windows). Ambos esses objetos têm uma WIM, que contém os arquivos de instalação do Windows. Atualizações de software são aplicáveis a esses arquivos em ambos os objetos. O comportamento desse processo é o mesmo entre os dois objetos.  

A cada mês, há novas atualizações de software aplicáveis à imagem. Antes de aplicar as atualizações de software, você precisará dos seguintes pré-requisitos: 

- Uma infraestrutura de atualizações de software  
- Atualizações de software sincronizadas com êxito  
- Baixadas as atualizações de software para a biblioteca de conteúdo no servidor do site  

Para mais informações, consulte [Implantar atualizações de software](/sccm/sum/deploy-use/deploy-software-updates).  

Aplique as atualizações de software relevantes a uma imagem em um agendamento especificado. Esse processo às vezes é chamado de *manutenção offline*. Nessa agenda, o Configuration Manager aplica a atualizações de software selecionadas à imagem. Ele então também pode redistribuir a imagem atualizada para pontos de distribuição. 

O banco de dados armazena informações sobre a imagem, incluindo as atualizações de software que foram aplicadas no momento da importação. As atualizações de software aplicadas à imagem desde que ela foi inicialmente adicionada também são armazenadas no banco de dados do site. Quando você inicia o Assistente para aplicar atualizações de software, ele recupera a lista de atualizações de software aplicáveis que o site ainda não tenha aplicado à imagem. O Configuration Manager copia as atualizações de software que você seleciona na biblioteca de conteúdo no servidor do site. Em seguida, ele aplica as atualizações de software à imagem.  


### <a name="servicing-process"></a>Processo de manutenção  

1.  No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione **Imagens do Sistema Operacional** ou **Pacotes de Atualização do Sistema Operacional**.  

2.  Selecione o objeto ao qual deseja aplicar as atualizações de software.  

3.  Na faixa de opções, selecione **Agendar Atualizações** para iniciar o assistente.  

4.  Na página **Escolher Atualizações**, selecione as atualizações de software a serem aplicadas à imagem. Pode levar algum tempo para que a lista de atualizações apareça no assistente. Use o **filtro** para pesquisar cadeias de caracteres nos metadados. Use a lista suspensa **Arquitetura do sistema** para filtrar **X86**, **X64** ou **Todos**. Você pode selecionar uma, várias ou todas as atualizações nessa lista. Quando você terminar de selecionar atualizações, selecione **Próxima**.  

5.  Na página **Definir Agendamento** , especifique as seguintes configurações e clique em **Próximo**.  

    a.  **Agendamento**: especifique o agendamento para quando o site aplica as atualizações de software à imagem.  

    b.  **Continuar se houver erro**:  selecione essa opção para continuar aplicando as atualizações de software à imagem em caso de erro.  

    c.  **Atualizar pontos de distribuição com a imagem**: selecione essa opção para atualizar a imagem nos pontos de distribuição após o site aplicar as atualizações de software.  

6.  Conclua o Assistente de Agendar Atualizações.  

> [!NOTE]  
>  Para minimizar o tamanho do conteúdo, a manutenção dos pacotes de atualização do sistema operacional e das imagens do sistema operacional remove a versão mais antiga.  


### <a name="servicing-operations"></a>Operações de manutenção

No console do Configuration Manager, no nó **Imagens do Sistema Operacional** ou **Pacotes de Atualização do Sistema Operacional**, adicione as seguintes colunas à exibição:
- **Data de Atualizações Agendadas**: essa propriedade mostra o próximo agendamento que você definiu.  
- **Status de Atualizações Agendadas**: essa propriedade mostra o status. Por exemplo, **Bem-sucedido** ou **Em processo**.  

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


