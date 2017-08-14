---
title: "Ferramenta de redefinição de atualização | Microsoft Docs"
description: "Usar a ferramenta de redefinição de atualização para atualizações no console para o System Center Configuration Manager."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 25fa89d6-7e47-45a6-8f4e-70b77560fba6
caps.latest.revision: 0
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: 1960f86e98a957559f379b9eeb6d293f7e4182e5
ms.contentlocale: pt-br
ms.lasthandoff: 07/29/2017

---
# <a name="update-reset-tool"></a>Ferramenta de redefinição de atualização

*Aplica-se a: System Center Configuration Manager (Branch Atual)*  


A partir da versão 1706, os sites primários do Configuration Manager e os sites de administração central incluem a Ferramenta de Redefinição de Atualização do Configuration Manager, **CMUpdateReset.exe**. Use a ferramenta para corrigir problemas quando as atualizações no console tiverem problemas de download ou replicação. A ferramenta é encontrada na pasta ***\cd.latest\SMSSETUP\TOOLS*** do servidor do site.

Você pode usar essa ferramenta com qualquer versão do branch atual que permanece com suporte.

Use essa ferramenta quando uma [atualização no console](/sccm/core/servers/manage/install-in-console-updates) ainda não estiver instalada e estiver em um estado de falha. Um estado de falha significa que o download da atualização está em andamento, mas ficou preso ou está demorando muito tempo. Muito tempo significa um período maior do que sua expectativa normal para pacotes de atualização de tamanho similar. Também pode ter havido uma falha ao replicar a atualização para os sites primários filhos.  

Quando você executa a ferramenta, ela é executada em relação à atualização que você especificar. Por padrão, a ferramenta não exclui com sucesso atualizações baixadas ou instaladas.  

### <a name="prerequisites"></a>Pré-requisitos
A conta usada para executar a ferramenta requer as seguintes permissões:
-   Permissões de **leitura** e **gravação** para o banco de dados do site de administração central e cada site primário em sua hierarquia. Para definir essas permissões, você poderá adicionar a conta de usuário como membro das [funções de banco de dados fixas](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) **db_datawriter** e **db_datareader** no banco de dados do Configuration Manager de cada site. A ferramenta não consegue interagir com os sites secundários.
-   **Administrador local** no site de nível superior da sua hierarquia.
-   **Administrador local** no computador que hospeda o ponto de conexão de serviço.

Você precisa da interface gráfica do usuário do pacote de atualização que você deseja redefinir. Para obter a interface gráfica do usuário:
  1.   No console, acesse **Administração** > **Atualizações e Manutenção**.
  2.   No painel de exibição, clique com o botão direito no título de uma das colunas (como **Estado**), em seguida, selecione **Guia do Pacote** para adicionar essa coluna à exibição.
  3.   Agora, a coluna mostra o GUID do pacote de atualização.

> [!TIP]  
> Para copiar a interface gráfica do usuário, selecione a linha para o pacote de atualização que deseja redefinir e, em seguida, use CTRL+C para copiar essa linha. Se você colar a seleção copiada em um editor de texto, poderá copiar somente a interface gráfica do usuário para usar como um parâmetro de linha de comando quando você executar a ferramenta.

### <a name="run-the-tool"></a>Executar a ferramenta    
A ferramenta deve ser executada no site de nível superior da hierarquia.

Ao executar a ferramenta, use os parâmetros de linha de comando para especificar:
  -   O SQL Server no site de nível superior da hierarquia.
  -   O nome do banco de dados do site no site de nível superior.
  -   O GUID do pacote de atualização que você deseja redefinir.

Com base no status da atualização, a ferramenta identifica os servidores adicionais os quais precisa acessar.   

Se o pacote de atualização estiver em um estado de *pós-download*, a ferramenta não limpará o pacote. Como opção, você pode forçar a remoção de uma atualização que baixou com êxito usando o parâmetro force delete (confira os parâmetros de linha de comando posteriormente neste tópico).

Depois que a ferramenta é executada:
-   Se um pacote tiver sido excluído, reinicie o serviço SMS_Executive no site de nível superior. Em seguida, verifique se há atualizações para que você possa baixar o pacote novamente.
-   Se um pacote não tiver sido excluído, não será necessário realizar qualquer ação. A atualização reinicializa e, depois, reinicia a replicação ou a instalação.

**Parâmetros da linha de comando:**  

| Parâmetro        |Descrição                 |  
|------------------|----------------------------|  
|**-S &lt;Nome de domínio totalmente qualificado do SQL Server do seu site de nível superior>** | *Necessária* <br> Especifique o nome de domínio totalmente qualificado do SQL Server que hospeda o banco de dados do site para o site de nível superior da sua hierarquia.    |  
| **-D &lt;Nome do banco de dados>**                        | *Necessária* <br> Especifique o nome do banco de dados no site de nível superior.  |  
| **-P &lt;Interface gráfica do usuário do pacote>**                         | *Necessária* <br> Especifique a GUID do pacote de atualização que você deseja redefinir.   |  
| **-I &lt;Nome da instância do SQL Server>**             | *Opcional* <br> Identifique a instância do SQL Server que hospeda o banco de dados do site. |
| **-FDELETE**                              | *Opcional* <br> Force a exclusão de um pacote de atualização baixado com êxito. |  
 **Exemplos:**  
 Em um cenário típico, você deve redefinir uma atualização que apresenta problemas de download. O FQDN do seu SQL Server é *server1.fabrikam.com*, o banco de dados do site é *CM_XYZ* e a GUID do pacote é *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Execute: ***CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

 Em um cenário mais complexo, você deve forçar a exclusão do pacote de atualização problemático. O FQDN do seu SQL Server é *server1.fabrikam.com*, o banco de dados do site é *CM_XYZ* e a GUID do pacote é *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Execute: ***CMUpdateReset.exe  -FDELETE -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

