---
title: Gerenciador de Biblioteca de Conteúdo
titleSuffix: Configuration Manager
description: Use o Gerenciador de Biblioteca de Conteúdo para exibir e solucionar problemas de biblioteca de conteúdo no ponto de distribuição do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 691896d9-ec0f-461f-a3f2-40378ebd3121
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1fbd046115dcd4d13cec7a2bf880740a9dd616cc
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65495776"
---
# <a name="content-library-explorer"></a>Gerenciador de Biblioteca de Conteúdo

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Gerenciador de Biblioteca de Conteúdo é uma das [ferramentas do Configuration Manager](/sccm/core/support/tools). Use a ferramenta para as seguintes atividades:  

- Explorar a biblioteca de conteúdo em um ponto de distribuição específico  

- Solucionar problemas com a biblioteca de conteúdo  

- Copiar pacotes, conteúdo, pastas e arquivos da biblioteca de conteúdo  

- Redistribuir pacotes para o ponto de distribuição  

- Validar pacotes nos pontos de distribuição remotos  



## <a name="requirements"></a>requisitos

- Execute a ferramenta usando uma conta que tenha acesso administrativo a:  

    - O ponto de distribuição de destino  

    - O provedor WMI no servidor do site  

    - O provedor do Configuration Manager  

- Somente as funções de **Administrador Completo** e **Analista Somente Leitura** têm direitos suficientes para exibir todas as informações dessa ferramenta.  

    - Outras funções, como **Administrador de Aplicativos**, podem exibir informações parciais. Para obter mais informações, veja [Pacotes desabilitados](#bkmk_disabled-packages).  

    - O **Analista Somente Leitura** não pode redistribuir os pacotes usando essa ferramenta.  

- Execute a ferramenta em qualquer computador, desde que ele possa se conectar a:  

    - O ponto de distribuição de destino  

    - Um servidor do site primário  

    - O provedor do Configuration Manager  

- Se o ponto de distribuição estiver colocado no servidor do site, ainda será necessário ter acesso administrativo ao servidor do site.  



## <a name="usage"></a>Uso 

Quando você iniciar **ContentLibraryExplorer.exe**, insira o FQDN (nome de domínio totalmente qualificado) do ponto de distribuição de destino. Ele então se conecta ao ponto de distribuição. Se o ponto de distribuição fizer parte de um site secundário, ele solicitará que você informe o FQDN do servidor do site primário e do código do site primário.

No painel esquerdo, exiba os pacotes distribuídos para esse ponto de distribuição. Expanda os pacotes e explore sua estrutura de pastas. Essa estrutura corresponde à estrutura de pastas da qual você criou o pacote.

Quando você seleciona uma pasta, ela exibe no painel direito todos os arquivos dentro dela. Essa exibição inclui as seguintes informações: 
- Nome do arquivo
- Tamanho do arquivo
- Em qual unidade ele está
- Outros pacotes que usam o mesmo arquivo na unidade
- Quando o arquivo foi alterado pela última vez no ponto de distribuição

A ferramenta também se conecta ao provedor do Configuration Manager. Essa conexão determina quais pacotes são distribuídos para o ponto de distribuição, e se eles estão, na verdade, na biblioteca de conteúdo do ponto de distribuição. Por exemplo, um pacote que está aguardando a distribuição pode ainda não existir na biblioteca de conteúdo. Esse pacote apareceria como "PENDENTE" na ferramenta, e nenhuma ação seria habilitada para ele.


### <a name="bkmk_disabled-packages"></a> Pacotes desabilitados

Alguns pacotes estão presentes no ponto de distribuição, mas não visíveis no console do Configuration Manager. Esses pacotes são marcados com um asterisco (\*). Nenhuma ação pode ser executada nesses pacotes. Outros pacotes também podem ser marcados com um asterisco e ter ações desabilitadas. 

Há três razões principais para pacotes desabilitados:  

- O pacote é a atualização de cliente do Configuration Manager. O pacote inclui "ccmsetup.exe".  

- Sua conta de usuário não pode acessar o pacote, provavelmente devido à administração baseada em funções. Por exemplo, a função **Autor do Aplicativo** não consegue ver os pacotes do driver no console, assim, qualquer pacote do driver no ponto de distribuição é marcado como desabilitado.  

- O pacote fica órfão no ponto de distribuição.  


### <a name="validate-packages"></a>Validar pacotes

Valide pacotes usando **Pacote** > **Validar** na barra de ferramentas. Primeiro, selecione um nó de pacote no painel esquerdo. Não selecione um conteúdo nem uma pasta. A ferramenta se conecta ao provedor de WMI no ponto de distribuição para essa ação. Quando a ferramenta é iniciada, pacotes que estão sem um ou mais conteúdo são marcados como inválidos. Validar o pacote revela o conteúdo que está ausente. Se todo o conteúdo estiver presente, mas os dados estiverem corrompidos, a validação detectará o dano.


### <a name="redistribute-packages"></a>Redistribuir pacotes

Redistribua pacotes usando **Pacote** > **Redistribuir** na barra de ferramentas. Primeiro, selecione um nó de pacote no painel esquerdo. Essa ação requer permissões para redistribuir os pacotes.


### <a name="other-actions"></a>Outras ações

Use **Editar** > **Copiar** para copiar pacotes, conteúdo, pastas e arquivos da biblioteca de conteúdo para uma pasta especificada. Você não pode copiar a biblioteca de conteúdo em si. Selecione mais de um arquivo, mas você não pode selecionar várias pastas.

Pesquisar pacotes usando **Editar** > **Encontrar Pacote**. Essa ação pesquisa sua consulta no nome do pacote e na ID do pacote.



## <a name="limitations"></a>Limitações

- A ferramenta não pode manipular a biblioteca de conteúdo diretamente de nenhuma maneira. As alterações à biblioteca de conteúdo podem resultar em mau funcionamento.  

- A ferramenta pode redistribuir pacotes, mas apenas para o ponto de distribuição de destino.  

- Quando você coloca o ponto de distribuição no servidor do site, não pode validar os dados do pacote. Em vez disso, use o console do Configuration Manager. A ferramenta ainda inspeciona o pacote para garantir que todo o conteúdo esteja presente, embora não necessariamente intacto.  

- Não é possível excluir o conteúdo com essa ferramenta.



## <a name="see-also"></a>Consulte também

- [Conceitos fundamentais para o gerenciamento de conteúdo](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [Biblioteca de conteúdo](/sccm/core/plan-design/hierarchy/the-content-library)
