---
title: Regras de aplicabilidade
titleSuffix: Configuration Manager
description: Gerenciar regras de aplicabilidade para o System Center Updates Publisher
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 3cf0c2cd-397a-4622-b11c-961f334fb7d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b4b289daa6f0f76c1d8e71879050bdfb6f5de679
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65496487"
---
# <a name="manage-applicability-rules-in-updates-publisher"></a>Gerenciar regras de aplicabilidade para o Updates Publisher

*Aplica-se ao: System Center Updates Publisher*

Com o Updates Publisher, as regras de aplicabilidade definem os requisitos que devem ser atendidos antes que um dispositivo possa instalar uma atualização. As regras também são usadas para determinar se o computador possui uma atualização instalada. Uma regra de aplicabilidade complexa com várias partes é conhecida como um conjunto de regras.

Pacotes de atualização não usam regras de aplicabilidade.

## <a name="overview-of-applicability-rules"></a>Visão geral das regras de aplicabilidade
Gerencie as regras de aplicabilidade no **Workspace de Regras**. Quando você cria uma regra, está especificando uma ou mais condições. Ao especificar várias condições, você pode configurar relações entre as condições para que elas sejam avaliadas sequencialmente ou combinadas em instruções **And** ou **Or** lógicas.

Por exemplo, veja a seguir um conjunto de regras que contém três regras. A primeira regra verifica se o arquivo *MyFile* existe, e a segunda e a terceira verificam se o idioma do sistema operacional Windows é inglês ou japonês.

    And  
      File ‘\[PROGRAM\_FILES\] \\Microsoft\\MyFile’ exists  
      Or  
        Windows Language is English   
        Windows Language is Japanese

Todas as atualizações exigem pelo menos uma regra de aplicabilidade. As atualizações que você importa já têm regras de aplicabilidade aplicadas e, quando você cria suas próprias atualizações, precisa adicionar uma ou mais regras a elas. Você pode modificar e expandir as regras de qualquer atualização no Updates Publisher.

Para exibir regras que você criou, no **Workspace de Regras**, selecione uma regra na lista **Minhas regras salvas**. As condições individuais e as operações lógicas dessa são exibidas no painel **Regras de Aplicabilidade** do console. As regras para as atualizações que você importa só podem ser exibidas e modificadas durante a edição dessa atualização.

Você pode criar regras em dois locais no Updates Publisher:

-   No **Workspace de Regras** você cria e **salva** conjuntos de regras para usá-los mais tarde. Ao editar ou criar uma atualização, você pode selecionar **Regra salva** como o **Tipo de regra** e, em seguida, selecionar em uma lista de seus conjuntos de regra criados previamente.

-   Você também pode criar novas regras no momento da criação ou edição de uma atualização. As regras criadas dessa forma não são salvas para uso futuro.

## <a name="create-applicability-rule"></a>Criar uma regra de aplicabilidade
As informações a seguir são semelhantes à criação de regras no [Assistente para Criar Atualizar](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-update-wizard). Mas, ao contrário do assistente, você tem a opção de salvar seus conjuntos de regras para uso futuro.

1. No **Workspace de Regras**, escolha **Criar** para abrir o assistente para **Criar Regra**.

2. Especifique um nome para a regra e clique em ![Nova Regra](media/newrule.png). Isso abre a página **Regra de Aplicabilidade**, na qual é possível configurar regras.

3. Para **Tipo de regra**, selecione uma das seguintes opções. As opções que você deve configurar variam para cada tipo:

   - **Arquivo** – use essa regra para exigir que um dispositivo tenha um arquivo com propriedades que atendam a um ou mais critérios especificados por você antes que essa atualização possa ser aplicada.

   - **Registro –** use este tipo para especificar detalhes do registro que devem estar presentes para que um dispositivo se qualifique para instalar essa atualização.

   - **Sistema –** essa regra usa os detalhes do sistema para determinar a aplicabilidade. Você pode escolher entre a definição de uma versão do Windows, um idioma do Windows, a arquitetura do processador ou especificar uma consulta no WMI para identificar o sistema operacional dos dispositivos.

   - **Windows Installer –** use esse tipo de regra para determinar a aplicabilidade com base em um .MSI instalado ou em um patch do Windows Installer (.MSP). Você também pode determinar se há recursos ou componentes específicos instalados como parte do requisito.

     > [!IMPORTANT]   
     > Em dispositivos gerenciados, o Windows Update Agent não pode detectar pacotes de instalação do Windows instalados por usuário. Ao usar esse tipo de regra, configure outras regras de aplicabilidade, como versões de arquivo ou valores de chave do Registro, para que o pacote do Windows Installer possa ser detectado corretamente, independentemente de ter base no usuário ou no sistema.

   - **Salvar regra –** essa opção permite que você localize e use as regras definidas e salvas anteriormente.

4. Continue a adicionar e configurar outras regras conforme o desejado.

5. Use os botões de operação lógica para ordenar e agrupar regras diferentes a fim de criar verificações de pré-requisitos mais complexas.

6. Quando o conjunto de regras estiver concluído, clique em **OK** para salvá-lo. Agora, o conjunto de regras aparece na lista **Minhas regras salvas**.

## <a name="edit-applicability-rule-sets"></a>Editar conjuntos de regras de aplicabilidade
Para editar uma regra de aplicabilidade, no **Workspace de Regras** selecione qualquer regra salva na lista **Minhas regras salvas** e escolha **Editar** na faixa de opções. Isso abre o assistente para **Editar Regra**.

O assistente para **Editar Regra** exibe as regras atuais para o conjunto de regras. Edite as regras da mesma maneira que você usa o assistente para **Criar Regra** para criar novas regras. Use esse assistente para renomear o conjunto de regras, excluir regras, reordenar as regras e relações ou adicionar novas regras.

Depois de fazer as alterações, escolha **OK** para salvar as alterações e fechar o assistente.

Para obter mais detalhes sobre como usar o assistente de regras, veja a **Etapa 7**, a página de aplicabilidade, do [assistente para Criar Atualização](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-update-wizard).

## <a name="delete-applicability-rules"></a>Excluir as regras de aplicabilidade
Para excluir uma regra de aplicabilidade salva, no **Workspace de Regras** selecione qualquer regra ou conjunto de regras na lista **Minhas regras salvas** e escolha **Excluir** na faixa de opções. Isso remove a regra salva ou o conjunto de regras do Updates Publisher.

Para excluir uma regra de uma atualização específica, [edite a atualização](/sccm/sum/tools/manage-updates-with-updates-publisher#edit-updates-and-bundles).
