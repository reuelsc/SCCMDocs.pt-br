---
title: Gerenciador de Filas de Trabalhos do DP
titleSuffix: Configuration Manager
description: Use o Gerenciador de Filas de Trabalhos do DP para solucionar problemas e gerenciar trabalhos de distribuição de conteúdo para pontos de distribuição do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4b72922a-d11e-4aef-b309-19f5f0716f32
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1365c3951a829d92cbdb2f6a4a87c8496f9ada3c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56136340"
---
# <a name="dp-job-queue-manager"></a>Gerenciador de Filas de Trabalhos do DP

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Gerenciador de Filas de Trabalhos do DP (Ponto de Distribuição) é uma das [ferramentas do Configuration Manager](/sccm/core/support/tools). Use-o para solucionar problemas e gerenciar trabalhos em andamento de distribuição de conteúdo para pontos de distribuição do Configuration Manager. 

A ferramenta exibe a lista de trabalhos que o componente do gerenciador de transferência de pacote tem em sua fila. Também mostra o status dos trabalhos: prontos para execução, em execução ou tentando novamente. Permite manipular os trabalhos na fila, mover os trabalhos mais para cima na lista, cancelar um trabalho ou iniciar a execução de um trabalho manualmente.

Também obtém informações do servidor do site no qual o ponto de distribuição está executado um trabalho. A ferramenta se conecta por meio do provedor ao servidor do site. Ela não se conecta a todos os pontos de distribuição remotos para coletar essas informações. Uma vez ela dispara ações e obtém informações por meio do provedor, há um atraso ao refletir as alterações dos pontos de distribuição remotos.



## <a name="usage"></a>Uso

Execute **DPJobMgr.exe**. O menu principal da ferramenta contém as seguintes guias: 

- [Conectar](#bkmk_connect): estabelecer a conexão inicial com o servidor do site primário  

- [Visão Geral](#bkmk_overview): resume em uma única exibição todos os trabalhos que estão em execução em todos os pontos de distribuição  

- [Informações de Ponto de Distribuição](#bkmk_dp-info): faça a seleção múltipla de pontos de distribuição para acompanhá-los e gerenciar um único trabalho de interesse  

- [Gerenciar Trabalhos](#bkmk_manage-jobs): Mostra em uma exibição simples uma lista de todos os trabalhos e seus status. Manipular trabalhos, movê-los para cima, cancelar ou iniciar manualmente.  


### <a name="bkmk_connect"></a> Guia Conectar

Use essa guia para estabelecer a conexão inicial ao servidor do site primário. Ele usa as credenciais do usuário conectado no momento. Você não pode se conectar ao site de administração central ou sites secundários. A conexão requer a função de segurança de **Administrador Completo**.

Depois que a ferramenta estabelecer uma conexão com sucesso, uma notificação na parte inferior da ferramenta confirmará que ela está conectada ao servidor do site. 


### <a name="bkmk_overview"></a> Guia Visão Geral

Mostra um resumo de todos os trabalhos em todos os pontos de distribuição. Veja as seguintes colunas:  

- **Ponto de Distribuição**: lista os nomes dos pontos de distribuição  

- **Trabalhos em Execução**: mostra o número de trabalhos simultâneos que estão em execução no ponto de distribuição específico.  

    > [!Tip]  
    > O número de distribuições de software concorrente é uma configuração de site. Modificada essa configuração nas Propriedades do Componente de Distribuição de Software.  

- **Total de Trabalhos**: mostra o número de todos os trabalhos direcionados a um ponto de distribuição específico. Esse número inclui os trabalhos em execução, que estão sendo repetidos ou que estão aguardando execução.  

- **Total de Novas Tentativas**: mostra o número de vezes que os trabalhos foram repetidos em um ponto de distribuição específico. Um número mais alto pode representar um problema geral com esse ponto de distribuição específico.  


> [!Tip]  
> - Para classificar cada coluna nessa guia, clique no nome da coluna  
> 
> - Atualize manualmente as informações nesta guia clicando em **Atualizar**  
> 
> - Atualizar automaticamente as informações nessa guia clicando em **Iniciar atualização automática** e configurando o intervalo de atualização automática. O intervalo de atualização padrão é de dois minutos.  


### <a name="bkmk_dp-info"></a> Guia de informações do Ponto de Distribuição

Mostra a lista de todos os pontos de distribuição no site conectado. O painel à esquerda lista todos os pontos de distribuição. Clique em **Selecionar Tudo** ou **Desmarcar Tudo**, conforme necessário, ou realize a seleção múltipla de ponto de distribuição específicos nessa lista. O painel à direita mostra os trabalhos para os pontos de distribuição selecionados.

Há oito colunas:  

- **Ícone de Status**: há três ícones de status possíveis:  

    - **Pronto**: indica que um determinado trabalho concluiu todas as etapas de verificação. Está pronto para ser adicionado a trabalhos simultâneos em execução. Trabalhos nesse estado geralmente estão em um estágio de espera. Eles esperam os processos em execução atuais serem concluídos para abrir um espaço para eles.  

    - **Em Execução**: indica que um trabalho específico está sendo executado em um ponto de distribuição. Para trabalhos de longa execução (pacotes grandes), geralmente há tempo para obter o progresso (%) até a conclusão. Ele mostra esse percentual na coluna **Progresso** nessa exibição. Para pacotes pequenos, a coluna **Progresso** pode ficar vazia. O trabalho já pode ter sido concluído no momento em que ele receber o status do ponto de distribuição remoto.  

    - **Tentar novamente**: indica que um determinado trabalho falhou e está agora em um estado de nova tentativa. Esse trabalho é repetido após o intervalo de repetição. Esse intervalo é configurável e será definido como 30 minutos por padrão.  

- **Software**: nome do pacote que é o destino de um ponto de distribuição específico  

- **ID do Pacote**: a ID do pacote referente ao pacote que está direcionado a um ponto de distribuição específico  

- **Tamanho**: tamanho do pacote em KB  

- **Progresso**: percentual de conclusão do trabalho. Para obter mais informações, veja a descrição do ícone de status **Em Execução**.  

- **Hora de Início/Reinício**: para um trabalho em execução, esse valor é a hora de início (verde). Para um trabalho de nova tentativa, esse valor é o momento em que ele tentará novamente o trabalho.  

- **Novas tentativas**: o número de vezes que ele repetiu esse pacote.  

- **Nome do Ponto de Distribuição**: o FQDN (nome de domínio totalmente qualificado) do ponto de distribuição  

> [!Tip]  
> - Para classificar cada coluna nessa guia, clique no nome da coluna  
> 
> - Atualize manualmente as informações nesta guia clicando em **Atualizar**  
> 
> - Atualizar automaticamente as informações nessa guia clicando em **Iniciar atualização automática** e configurando o intervalo de atualização automática. O intervalo de atualização padrão é de dois minutos.  
> 
> - Se você precisar modificar um trabalho específico, clique com o botão direito do mouse no trabalho nessa exibição e selecione **Gerenciar Trabalho**. Essa ação abre a [guia Gerenciar Trabalhos](#bkmk_manage-jobs).  


### <a name="bkmk_manage-jobs"></a> Guia Gerenciar Trabalhos

Mostra em uma exibição simples uma lista de todos os trabalhos e seus status. Contém as mesmas oito colunas que a [guia Informações do Ponto de Distribuição](#bkmk_dp-info). Nessa exibição, clique com o botão direito do mouse nos trabalhos para as seguintes ações:  

- **Executar**: inicia um trabalho em um estado que não em execução  

- **Mover para o Início**: move um ou mais trabalhos para o início da fila. Essa ação pode resultar em os trabalhos serem executados imediatamente. Um trabalho de menor prioridade pode ser colocado em pausa devido a essa ação.  

- **Mover para Cima**: move um trabalho em particular uma linha para cima. Um trabalho de menor prioridade pode colocar a execução em pausa devido a essa ação.  

- **Mover para Baixo**: move um trabalho em particular uma linha para baixo.  

- **Mover para o Fim**: move um ou mais trabalhos para o final da fila.  

    > [!Tip]  
    > Arraste e solte trabalhos na lista para movê-los.  

- **Cancelar**: tenta cancelar um ou mais trabalhos.  

    > [!Note]  
    > Você não pode cancelar trabalhos perto da hora de conclusão final. Se o servidor do site também for um ponto de distribuição, você não poderá cancelar trabalhos no servidor do site.  



## <a name="see-also"></a>Consulte também

- [Conceitos fundamentais para o gerenciamento de conteúdo](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [Gerenciador de transferência de pacote](/sccm/core/plan-design/hierarchy/package-transfer-manager)
