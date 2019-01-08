---
title: Testar atualização do banco de dados
titleSuffix: Configuration Manager
description: Teste a atualização do banco de dados do site ao instalar as atualizações para o Configuration Manager.
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: abb696f3-a816-4f12-a9f1-0503a81e1976
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4168b36553dacff69fab0972011a7d4c2843d787
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421936"
---
# <a name="test-the-database-upgrade-when-installing-an-update"></a>Testar a atualização do banco de dados ao instalar uma atualização

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As informações neste tópico podem ajudá-lo a executar uma atualização de banco de dados de teste antes de instalar uma atualização no console para a ramificação atual do Configuration Manager. No entanto, a atualização de teste não é mais uma etapa necessária ou recomendável, a menos que seu banco de dados seja suspeito ou esteja modificado por personalizações que não tenham suporte explícito do Configuration Manager.

## <a name="do-i-need-to-run-a-test-upgrade"></a>É necessário executar uma atualização de teste?
A substituição desse teste de atualização é possibilitada devido a alterações que foram introduzidas com o System Center Configuration Manager. Essas alterações simplificam o processo e a velocidade pela qual um ambiente de produção pode ser atualizado para versões mais recentes. Essa reestruturação foi feita para ajudar os clientes a se manterem atualizados com menos risco e menos sobrecarga operacional durante a instalação de cada nova atualização.

Há alterações para o modo como as atualizações são instaladas, incluindo a lógica que reverterá automaticamente uma atualização com falha sem a necessidade de executar uma recuperação de site. Essas alterações permitem o uso do console para gerenciar instalações de atualização e incluem uma opção para [repetir a instalação de uma atualização com falha](/sccm/core/servers/manage/install-in-console-updates#bkmk_retry).

> [!TIP]
> Quando você atualizar para o System Center Configuration Manager de um produto mais antigo, como o System Center 2012 Configuration Manager, [as atualizações de banco de dados de teste continuarão sendo uma etapa recomendada](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager#a-namebkmktesta-test-the-site-database-upgrade).

Se quiser planejar para testar a atualização de um banco de dados do site quando você instala uma atualização no console, as informações a seguir complementam a [orientação sobre como instalar uma atualização no console](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).

## <a name="prepare-to-run-a-test-database-upgrade"></a>Preparar para executar uma atualização de banco de dados de teste  
Antes de instalar uma nova atualização em sua hierarquia, como a atualização para a versão 1702, você pode testar a atualização de seu banco de dados do site.

Para executar o teste de atualização, use a instalação do Configuration Manager dos arquivos de origem da [pasta CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder) de um site que executa a versão do Configuration Manager para a qual você está atualizando. Esse requisito significa que, para testar a atualização do banco de dados para atualização 1702:
-   Você deve ter pelo menos um site que executa a versão 1702 do qual você pode obter essa pasta CD.Latest.
-   Se você não tiver um site que executa a versão necessária, instale um site em um ambiente de laboratório e, em seguida, atualize o site para a nova versão. Isso cria a pasta CD.Latest com a versão correta dos arquivos de origem.

O teste de atualização é executado em um backup do seu banco de dados do site que você restaurou para uma instância separada do SQL Server.  Execute a Instalação a partir da pasta **CD.Latest** com a opção da linha de comando **testdbupgrade** para testar a atualização que restaurou a cópia do banco de dados. Após a atualização de teste ser concluída, o banco de dados atualizado será descartado. Ele não pode ser usado por um site do Configuration Manager.

Se a instalação da atualização falhar, você não precisará recuperar o site. Em vez disso, você pode repetir a instalação da atualização de dentro do console.

##  <a name="run-the-test-upgrade"></a>Executar a atualização de teste    
1. Use a Instalação do Configuration Manager e os arquivos de origem da pasta **CD.Latest** de um site que executa a versão para a qual você planeja atualizar.  

2. Copie a pasta **CD.Latest** para um local na instância do SQL Server que você usará para executar a atualização do banco de dados de teste.

3. Crie um backup do banco de dados do site que você deseja testar a atualização. Em seguida, restaure uma cópia do banco de dados para uma instância do SQL Server que não hospede um site do Configuration Manager. A instância do SQL Server deve usar a mesma edição do SQL Server que seu banco de dados do site.  

4. Depois de restaurar a cópia do banco de dados, execute a **Instalação** da pasta CD.Latest que contém os arquivos de origem da versão para a qual você está atualizando. Ao executar a Instalação, use a opção de linha de comando **/TESTDBUPGRADE** . Se a instância do SQL Server que hospeda a cópia do banco de dados não for a instância padrão, forneça também os argumentos da linha de comando para identificar a instância que hospeda a cópia do banco de dados do site.   

   Por exemplo, você tem um banco de dados do site com o nome de banco de dados *SMS_ABC*. Você restaura uma cópia desse banco de dados do site para uma instância com suporte do SQL Server com o nome de instância *DBTest*. Para testar uma atualização dessa cópia do banco de dados do site, use a linha de comando a seguir: **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**.  

   Você pode encontrar o Setup.exe na seguinte localização na mídia de origem do System Center Configuration Manager: **SMSSETUP\BIN\X64**.  

5. Na instância do SQL Server em que você executa o teste de atualização, monitore o arquivo *ConfigMgrSetup.log* na raiz da unidade do sistema para verificar o andamento e o êxito.  

    Se o teste de atualização falhar, corrija os problemas relacionados à falha de atualização do banco de dados do site. Em seguida, crie um novo backup do banco de dados do site e teste a atualização da nova cópia do banco de dados.  



## <a name="next-steps"></a>Próximas etapas
Após a atualização do banco de dados de teste ser concluída com êxito, descarte o banco de dados atualizado. Ele não pode ser usado por um site do Configuration Manager. Você pode retornar a seu site ativo e [começar a instalação da atualização](/sccm/core/servers/manage/install-in-console-updates).
