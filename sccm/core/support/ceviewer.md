---
title: Collection Evaluation Viewer
titleSuffix: Configuration Manager
description: Use o Visualizador de Avaliação de Coleção para exibir e solucionar problemas do processo de avaliação de coleção no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: caad2d93-087c-4dc0-a2a7-6a2fd808b4c8
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 48b5abb686171b475233a2c61b80c0819ee26994
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500895"
---
# <a name="collection-evaluation-viewer"></a>Collection Evaluation Viewer

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Collection Evaluation Viewer é uma das [ferramentas do Configuration Manager](/sccm/core/support/tools). Use-a para exibir e solucionar problemas do processo de avaliação de coleção no servidor do site primário.

A ferramenta exibe as seguintes informações:  

- Informações históricas e em tempo real para avaliações de coleção completas e incrementais  

- O status da fila de avaliação  

- O tempo para as avaliações de coleção serem concluídas  

- Que coleções estão sendo avaliadas no momento  

- O tempo estimado para uma avaliação da coleção iniciar e ser concluída  



## <a name="about-collection-evaluation"></a>Sobre a avaliação da coleção

O processo de avaliação de coleção é executado avaliando as regras de associação de uma coleção para atualizar seus membros. O site coloca uma coleção que está sendo avaliada em uma das quatro filas diferentes:  

- **Fila Manual**: para coleções que um administrador selecionou manualmente para avaliação do console  

- **Nova Fila**: para coleções recém-criadas  

- **Fila Completa**: para coleções com devem passar por avaliação completa  

- **Fila Incremental**: para coleções com a avaliação incremental  

Há quatro threads que são executados para avaliar as coleções nas filas acima. Cada fila inclui uma série de matrizes, e cada matriz inclui as coleções a serem avaliadas. O thread que está em execução para a fila seleciona uma coleção de matriz e executa a avaliação. O comprimento da fila indica o número de matrizes na fila.



## <a name="requirements"></a>requisitos

- Execute a ferramenta no servidor do site  

- Execute a ferramenta por um usuário administrativo com pelo menos a função de **Analista Somente Leitura**  

- O usuário também requer permissão de **Leitura** para o banco de dados do site no SQL



## <a name="usage"></a>Uso

Execute **CEViewer.exe**. O menu principal da ferramenta contém as seguintes guias: 

- [Conectar](#bkmk_connect): estabeleça a conexão inicial com o servidor do site primário e o SQL Server  

- [Avaliação Completa](#bkmk_full-eval): lista as informações detalhadas sobre todas as avaliações completas anteriores   

- [Avaliação incremental](#bkmk_incremental-eval): lista informações detalhadas sobre todas as avaliações incrementais anteriores  

- [Todas as Filas](#bkmk_all-q): resume as avaliações da coleção atual para todas as quatro filas  

- [Fila Manual](#bkmk_manual-q): lista informações detalhadas sobre a avaliação da coleção atual na fila manual  

- [Nova Fila](#bkmk_new-q): lista informações detalhadas sobre a avaliação da coleção atual na nova fila  

- [Fila Completa](#bkmk_full-q): lista informações detalhadas sobre a avaliação da coleção atual na fila completa  

- [Fila Incremental](#bkmk_incremental-q): lista informações detalhadas sobre a avaliação da coleção atual na fila incremental  


### <a name="bkmk_connect"></a> Guia Conectar

Essa guia permite que você estabeleça a conexão inicial ao servidor do site primário. A ferramenta também estabelece uma conexão com o SQL Server que hospeda o banco de dados do site.

As conexões ao servidor do site primário e aos servidores SQL usam a credencial do usuário conectado no momento. Não há suporte para conexões com o site de administração central nem com um site secundário. Nenhum processo de avaliação de coleta é executado nesses sites.

Depois que a ferramenta estabelecer uma conexão com êxito, você verá uma notificação na parte inferior do Visualizador de Avaliação de Coleção confirmando a conexão da ferramenta com o SQL Server. 


### <a name="bkmk_full-eval"></a> Guia de Avaliação Completa

Mostra informações detalhadas sobre as últimas avaliações completas da coleção. Há oito colunas:  

- **Nome da Coleção**: o nome da coleção  

- **ID do Site**: a ID do site da coleção   

- **Tempo de Execução**: por quanto tempo a última avaliação da coleção foi executada, em segundos  

- **Hora de Conclusão da Última Avaliação**: quando a última avaliação da coleção foi concluída  

- **Hora da Próxima Avaliação**: quando a próxima avaliação completa será iniciada  

- **Alterações de Membro**: as alterações de membro na última avaliação de coleção. Essas alterações são positivas (membros adicionados) ou negativas (membros removidos).  

- **Hora da Última Alteração do Membro**: a hora mais recente em que houve uma alteração de associação na avaliação da coleção  

- **Porcentagem**: percentual do tempo de avaliação para essa coleção durante o tempo de avaliação total (todas as coleções)  


### <a name="bkmk_incremental-eval"></a> Guia de avaliação incremental

Mostra informações detalhadas sobre as últimas avaliações incrementais da coleção. Há sete colunas:  

- **Nome da Coleção**: o nome da coleção  

- **ID do Site**: a ID do site da coleção   

- **Tempo de Execução**: por quanto tempo a última avaliação da coleção foi executada, em segundos  

- **Hora de Conclusão da Última Avaliação**: quando a última avaliação da coleção foi concluída  

- **Alterações de Membro**: as alterações de membro na última avaliação de coleção. Essas alterações são positivas (membros adicionados) ou negativas (membros removidos).  

- **Hora da Última Alteração do Membro**: a hora mais recente em que houve uma alteração de associação na avaliação da coleção  

- **Porcentagem**: percentual do tempo de avaliação para essa coleção durante o tempo de avaliação total (todas as coleções)  


### <a name="bkmk_all-q"></a> Guia Todas as Filas

Resume as avaliações da coleção ao vivo para todas as quatro filas. Há seis seções:  

- **Resumo**: lista o número total da coleção e o comprimento da fila para todas as coleções em todas as quatro filas  

- **Avaliação em Execução**: lista que coleção está sendo avaliada no momento em cada fila e há quanto tempo está em execução  

- **Atualização Manual**: mostra um breve resumo das coleções que estão sendo avaliadas, o tempo estimado para a conclusão e a ordem da avaliação na fila manual  

- **Nova Coleção**: mostra um breve resumo das coleções que estão sendo avaliadas, o tempo estimado para a conclusão e a ordem da avaliação na fila de novas coleções  

- **Avaliação Completa**: mostra um breve resumo das coleções que estão sendo avaliadas, o tempo estimado para a conclusão e a ordem da avaliação na fila de avaliações completas  

- **Avaliação Incremental**: mostra um breve resumo das coleções que estão sendo avaliadas, o tempo estimado para a conclusão e a ordem da avaliação na fila de avaliações incrementais  


### <a name="bkmk_manual-q"></a> Guia Fila Manual

Mostra informações sobre a avaliação manual da coleção que está sendo examinada no momento. A ordem na lista é a ordem na qual a coleção será avaliada. Há quatro colunas:  

- **Nome da Coleção**: o nome da coleção  

- **ID do Site**: a ID do site da coleção   

- **Tempo de Conclusão Estimado**: a estimativa de quando a avaliação deverá ser concluída  

- **Tempo de Execução Estimado**: a estimativa de em quanto tempo a avaliação será executada, no formato dias:horas:minutos:segundos  


### <a name="bkmk_new-q"></a> Guia Nova Fila

Mostra as informações em tempo real sobre a nova avaliação de coleção que está sendo examinada. A ordem na lista é a ordem na qual a coleção será avaliada. Há quatro colunas:  

- **Nome da Coleção**: o nome da coleção  

- **ID do Site**: a ID do site da coleção   

- **Tempo de Conclusão Estimado**: a estimativa de quando a avaliação deverá ser concluída  

- **Tempo de Execução Estimado**: a estimativa de em quanto tempo a avaliação será executada, no formato dias:horas:minutos:segundos  


### <a name="bkmk_full-q"></a> Guia Fila Completa

Mostra informações sobre a avaliação completa da coleção que está sendo examinada no momento. A ordem na lista é a ordem na qual a coleção será avaliada. Há quatro colunas:  

- **Nome da Coleção**: o nome da coleção  

- **ID do Site**: a ID do site da coleção   

- **Tempo de Conclusão Estimado**: a estimativa de quando a avaliação deverá ser concluída  

- **Tempo de Execução Estimado**: a estimativa de em quanto tempo a avaliação será executada, no formato dias:horas:minutos:segundos  


### <a name="bkmk_incremental-q"></a> Guia Fila Incremental

Mostra informações sobre a avaliação da coleção incremental que está sendo examinada no momento. A ordem na lista é a ordem na qual a coleção será avaliada. Há quatro colunas:  

- **Nome da Coleção**: o nome da coleção  

- **ID do Site**: a ID do site da coleção   

- **Tempo de Conclusão Estimado**: a estimativa de quando a avaliação deverá ser concluída  

- **Tempo de Execução Estimado**: a estimativa de em quanto tempo a avaliação será executada, no formato dias:horas:minutos:segundos  



