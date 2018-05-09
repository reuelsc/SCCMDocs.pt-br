---
title: Guia do usuário do Centro de Software
titleSuffix: Configuration Manager
description: Saiba mais sobre os recursos e as funcionalidades do Centro de Software
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.openlocfilehash: 4c45da7b5a4b7f8945b23d03d0fd551276205ee2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="software-center-user-guide"></a>Guia do usuário do Centro de Software

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O administrador de TI de sua organização usa o Centro de Software para instalar aplicativos, atualizações de software e atualizar o Windows. Este guia do usuário explica as funcionalidades do Centro de Software para os usuários do computador.

### <a name="general-notes-about-software-center-functionality"></a>Notas gerais sobre as funcionalidades do Centro de Software
- Este artigo descreve os últimos recursos do Centro de Software. Caso sua organização esteja usando uma versão mais antiga do Centro de Software, mas ainda compatível, nem todos os recursos estarão disponíveis. Para obter mais informações, contate o administrador de TI.
- O administrador de TI pode desabilitar alguns aspectos do Centro de Software. Sua experiência específica pode variar.
<!-- - Your IT admin may change the color of Software Center, and add your organization's logo. The images in this article show the default experience. -->



## <a name="how-to-open-software-center"></a>Como abrir o Centro de Software

Para o método mais simples para iniciar o Centro de Software em um computador Windows 10, pressione **Iniciar** e digite `Software Center`. 

Se você navegar no menu Iniciar, procure no grupo **Microsoft System Center** pelo ícone **Centro de Software**.



## <a name="applications"></a>Aplicativos

Clique na guia **Aplicativos** para encontrar e instalar aplicativos implantados para você ou nesse computador pelo administrador de TI.
- **Todos**: mostra todos os aplicativos que podem ser instalados
- **Obrigatório**: o administrador de TI impõe esses aplicativos. Se você desinstalar um desses aplicativos, o Centro de Software o reinstalará.
- **Filtros**: o administrador de TI pode criar categorias de aplicativos. Se estiver disponível, clique na lista suspensa para filtrar a exibição somente com os aplicativos de uma categoria específica. Selecione **Todos** para mostrar todos os aplicativos.
- **Classificar por**: reorganize a lista de aplicativos. Por padrão, essa lista é classificada pelo **Mais recente**.
- **Pesquisar**: ainda não está encontrando o que procura? Insira palavras-chave na caixa de pesquisa para encontrá-lo!
-  Alternar a exibição: clique nos ícones para alternar entre a exibição de lista e a de bloco. Por padrão, a lista de aplicativos é mostrada como blocos gráficos. 
    - Exibição de bloco: o administrador de TI pode personalizar os ícones. Abaixo de cada bloco, são exibidos o nome do aplicativo, o distribuidor e a versão. 
    - Exibição de lista: essa exibição mostra o ícone do aplicativo, o nome, o distribuidor, a versão e o status. 


### <a name="install-multiple-applications"></a>Instalar vários aplicativos 
<!-- 1357126 -->
Instale mais de um aplicativo por vez, em vez de aguardar a conclusão de um antes de iniciar o próximo. Nem todos os aplicativos são qualificados:
- O aplicativo está visível para você
- O aplicativo ainda não está instalado ou sendo baixado
- O administrador de TI não exige aprovação para instalar o aplicativo

Para instalar mais de um aplicativo por vez:
 1. Para entrar no modo de seleção múltipla na exibição de lista, clique no ícone de seleção múltipla ![Ícone de seleção múltipla do Centro de Software](media/software-center-multi-select-apps.png) no canto superior direito.
 2. Selecione dois ou mais aplicativos a serem instalados clicando na caixa de seleção à esquerda dos aplicativos na lista.
 3. Clique no botão **Instalar Selecionados**.

Os aplicativos são instalados como de costume, agora somente em sucessão.




## <a name="updates"></a>Atualizações

Clique na guia **Atualizações** para exibir e instalar atualizações de software implantadas nesse computador pelo administrador de TI.  
- **Todos**: mostra todas as atualizações que podem ser instaladas
- **Obrigatório**: o administrador de TI impõe essas atualizações.
- **Classificar por**: reorganize a lista de atualizações. Por padrão, essa lista é classificada por **Nome do aplicativo: A a Z**.

Para instalar as atualizações, clique em **Instalar Tudo**.

Para instalar somente atualizações específicas, clique no ícone para entrar no modo de seleção múltipla. Verifique as atualizações a serem instaladas e, em seguida, clique em **Instalar Selecionados**.



## <a name="operating-systems"></a>Sistemas operacionais

Clique na guia **Sistemas Operacionais** para exibir e instalar as versões do Windows implantadas nesse computador pelo administrador de TI.  
- **Todos**: mostra todas as versões do Windows que podem ser instaladas
- **Obrigatório**: o administrador de TI impõe essas atualizações.
- **Classificar por**: reorganize a lista de atualizações. Por padrão, essa lista é classificada por **Nome do aplicativo: A a Z**.



## <a name="installation-status"></a>Status da instalação

Clique na guia **Status da instalação** para exibir o status dos aplicativos. Você poderá ver os seguintes estados:
- **Instalado**: o Centro de Software já instalou esse aplicativo nesse computador.
- **Baixando**: o Centro de Software está baixando o software a ser instalado nesse computador.
- **Com Falha**: o Centro de Software encontrou um erro ao tentar instalar o software.



## <a name="device-compliance"></a>Conformidade do dispositivo

Clique na guia **Conformidade do dispositivo** para exibir o status de conformidade desse computador.

Clique em **Verificar conformidade** para avaliar as configurações do dispositivo em relação às políticas de segurança definidas pelo administrador de TI.



## <a name="options"></a>Opções

Clique na guia **Opções** para exibir as configurações adicionais desse computador.

### <a name="work-information"></a>Informações de trabalho

Indique as horas durante as quais você normalmente trabalha. O administrador de TI pode agendar as instalações de software fora do horário comercial. Permita, pelo menos, quatro horas por dia para tarefas de manutenção do sistema. O administrador de TI ainda poderá instalar atualizações de software e aplicativos críticos durante o horário comercial.

- Clique nas listas suspensas para selecionar os horários mais cedo e mais tarde em que você usa esse computador. Por padrão, esses valores variam das **5h** até às **22h**

- Marque a caixa de seleção ao lado dos dias da semana que você normalmente usa esse computador. O Centro de Software seleciona somente os dias da semana por padrão.  


### <a name="power-management"></a>Gerenciamento de Energia

O administrador de TI poderá definir políticas de gerenciamento de energia. Essas políticas ajudam sua organização a conservar eletricidade quando esse computador não está em uso. 

Para tornar esse computador isentos dessas políticas, marque a caixa de seleção **Não aplicar as configurações de energia de meu departamento de TI a este computador**. Essa configuração está desabilitada por padrão; o computador aplica as configurações de energia. 


### <a name="computer-maintenance"></a>Manutenção do computador

Especificar como o Centro de Software aplica as alterações no software antes da data limite
- **Instalar ou desinstalar automaticamente o software obrigatório e reiniciar o computador somente fora do horário comercial especificado**: essa configuração está desabilitada por padrão.
- **Suspender as atividades do Centro de Software quando meu computador estiver no modo de apresentação**: essa configuração está habilitada por padrão.
- **Política de Sincronização**: clique nesse botão quando instruído pelo administrador de TI. Esse computador verifica com os servidores se há algo novo, como aplicativos, atualizações de software ou sistemas operacionais.

