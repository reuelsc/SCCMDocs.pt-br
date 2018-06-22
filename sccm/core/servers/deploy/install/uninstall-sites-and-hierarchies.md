---
title: Desinstalar sites
titleSuffix: Configuration Manager
description: Use esses detalhes como um guia para desinstalar um site do System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d466edd2-97f0-44c1-a73e-d71abbdbf4a8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0f87975d660a94d04cdd7d0e10816b6e2815fe53
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342062"
---
# <a name="uninstall-sites-and-hierarchies-in-system-center-configuration-manager"></a>Desinstalar sites e hierarquias no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use os detalhes a seguir como um guia se você precisar desinstalar um site do System Center Configuration Manager.  

Para desativar uma hierarquia com vários sites, a sequência de remoção é importante. Inicie a desinstalação dos sites na parte inferior da hierarquia e depois passe para a parte superior:  

1.  Remova os sites secundários anexados aos sites primários.  
2.  Remova os sites primários.
3.  Depois que todos os sites primários são removidos, é possível desinstalar o site de administração central.  


##  <a name="BKMK_RemoveSecondarysite"></a> Remover um site secundário de uma hierarquia  
Você não pode mover um site secundário ou reatribuir um site secundário a um novo site primário pai. Para ser removido da hierarquia, um site secundário deve ser excluído de seu site pai direto. Use o Assistente para Excluir Site Secundário do console do Configuration Manager para remover um site secundário. Ao remover um site secundário, você deve escolher se deseja excluí-lo ou desinstalá-lo:  

-   **Desinstalar o site secundário**. Use esta opção para remover um site secundário funcional que está acessível pela rede. Essa opção desinstala o Configuration Manager do servidor do site secundário e, em seguida, exclui todas as informações sobre o site e seus recursos da hierarquia de sites do Configuration Manager. Se o Configuration Manager instalou o SQL Server Express como parte da instalação do site secundário, o Configuration Manager desinstalará o SQL Express quando desinstalar o site secundário. Se o SQL Server Express foi instalado antes do site secundário, o Configuration Manager não desinstalará o SQL Server Express.  

-   **Excluir o site secundário**. Use essa opção se uma das seguintes opções for verdadeira:  

    -   Falha na instalação de um site secundário  
    -   O site secundário continua a ser exibido no console do Configuration Manager após desinstalá-lo

    Essa opção exclui todas as informações sobre o site e seus recursos da hierarquia do Configuration Manager, mas deixa o Configuration Manager instalado no servidor do site secundário.  

    > [!NOTE]  
    >  Você também pode usar a Ferramenta de Manutenção de Hierarquia e a opção **/DELSITE** para excluir um site secundário. Para obter mais informações, consulte [Ferramenta de Manutenção de Hierarquia (Preinst.exe) para o System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

#### <a name="to-uninstall-or-delete-a-secondary-site"></a>Para desinstalar ou excluir um site secundário  

1.  Verifique se o usuário administrativo que executa a Instalação tem os seguintes direitos de segurança:  

    -   Direitos administrativos no computador do site secundário  
    -   Direitos do Administrador Local no servidor de banco de dados do site remoto para o site primário, se ele for remoto  
    -   Função de segurança de Administrador de Infraestrutura ou de Administrador Completo no site primário pai  
    -   Direitos Sysadmin no banco de dados de site do site secundário  

2.  No console do Configuration Manager, selecione **Administração**.  
3.  No espaço de trabalho **Administração**, expanda **Configuração do Site** e selecione **Sites**.  
4.  Selecione o servidor do site secundário que deseja remover.  
5.  Na guia **Início**, no grupo **Site**, selecione **Excluir**.  
6.  Na página **Geral** , selecione desinstalar ou excluir o site secundário e clique em **Avançar**.  
7.  Na página **Resumo**, verifique as configurações e selecione **Avançar**.  
8.  Na página **Conclusão**, selecione **Fechar** para sair do assistente.  

##  <a name="BKMK_UninstallPrimary"></a> Desinstalar um site primário  
Você pode executar a Instalação do Configuration Manager para desinstalar um site primário que não tem um site secundário associado. Para desinstalar um site primário, considere o seguinte:  

-   Quando clientes do Configuration Manager estão dentro dos limites configurados no site, e o site primário é parte de uma hierarquia do Configuration Manager, considere adicionar os limites a um site primário diferente na hierarquia antes de desinstalar o site primário.  
-   Quando o servidor do site primário não está mais disponível, você deve usar a Ferramenta de Manutenção de Hierarquia no site de administração central para excluir o site primário do banco de dados do site. Para obter mais informações, consulte [Ferramenta de Manutenção de Hierarquia (Preinst.exe) para o System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

Use o procedimento a seguir para desinstalar um site primário.  

#### <a name="to-uninstall-a-primary-site"></a>Para desinstalar um site primário  

1.  Verifique se o usuário administrativo que executa a Instalação tem os seguintes direitos de segurança:  

    -   Direitos de Administrador Local no servidor do site de administração central  
    -   Direitos do Administrador Local no servidor de banco de dados do site remoto para o site de administração central, se for remoto
    -   Direitos sysadmin no banco de dados do site do site de administração central  
    -   Direitos de Administrador Local no computador do site primário  
    -   Direitos do Administrador Local no servidor de banco de dados do site remoto para o site primário, se ele for remoto  
    -   Um nome de usuário associado à função de segurança do Administrador de Infraestrutura ou de Administrador Completo no site de administração central  

2.  Inicie a Instalação do Configuration Manager no servidor do site primário usando um dos seguintes métodos:  

    -   Em **Iniciar**, selecione **Instalação do Configuration Manager**.  
    -   Abra o Setup.exe de &lt;*ConfigMgrInstallationMedia*>\SMSSETUP\BIN\X64.  
    -   Abra o Setup.exe de &lt;*ConfigMgrInstallationPath*>\BIN\X64.  

3.  Na página **Antes de Começar** escolha **Avançar**.  
4.  Na página **Guia de Introdução**, selecione **Desinstalar um site do Configuration Manager** e selecione **Avançar**.  
5.  Em **Desinstalar o Site do Configuration Manager**, especifique se deseja remover o banco de dados do site do servidor do site primário e se deseja remover o console do Configuration Manager. Por padrão, a Instalação remove os dois itens.  

    > [!IMPORTANT]  
    >  Quando um site secundário é conectado a um site primário, você deve remover o site secundário para poder desinstalar o site primário.  

6.  Selecione **Sim** para confirmar a desinstalação do site primário do Configuration Manager.  

##  <a name="BKMK_UninstallPrimaryDistViews"></a> Desinstalar um site primário configurado com exibições distribuídas  
 Para desinstalar um site filho primário que tem exibições distribuídas configuradas ativadas para seu link de replicação para o site de administração central, você deve desligar as exibições distribuídas na hierarquia. Use as informações a seguir para desligar exibições distribuídas antes de desinstalar um site primário.  

#### <a name="to-uninstall-a-primary-site-that-is-configured-with-distributed-views"></a>Para desinstalar um site primário configurado com exibições distribuídas  

1.  Para desinstalar qualquer site primário, você deve desligar as exibições distribuídas em cada link na hierarquia entre o site de administração central e um site primário.  
2.  Depois de desligar as exibições distribuídas em cada link, confirme se os dados do site primário concluem a reinicialização no site de administração central. Para monitorar a inicialização de dados, no console do Configuration Manager, no espaço de trabalho **Monitoramento**, exiba o link no nó **Replicação de Banco de Dados**.  
3.  Após os dados reinicializarem com êxito com o site de administração central, você pode desinstalar o site primário. Para desinstalar um site primário, consulte [Desinstalar um site primário](#BKMK_UninstallPrimary).  
4.  Quando o site primário é completamente desinstalado, você pode reconfigurar exibições distribuídas em links para sites primários.  

    > [!IMPORTANT]  
    >  Se você desinstalar o site primário antes de desligar as exibições distribuídas em cada site ou antes que os dados do site primário reinicializem com êxito no site de administração central, a replicação de dados entre os sites primários e o site de administração central pode falhar. Nesse cenário, você deve desligar as exibições distribuídas de cada link em sua hierarquia de sites e então, após os dados reinicializarem com êxito no site de administração central, você pode reconfigurar as exibições distribuídas.  

##  <a name="BKMK_UninstallCAS"></a> Desinstalar o site de administração central  
 É possível executar o programa de Instalação do Configuration Manager para desinstalar um site de administração central que não tem sites primários filho. Use o procedimento a seguir para desinstalar um site de administração central.  

#### <a name="to-uninstall-a-central-administration-site"></a>Para desinstalar um site de administração central  

1.  Verifique se o usuário administrativo que executa a Instalação tem os seguintes direitos de segurança:  

    -   Direitos de Administrador Local no servidor do site de administração central  
    -   Direitos de administrador local no servidor de banco de dados do site para o site de administração central, se o servidor de banco de dados do site não estiver instalado no servidor de site 

2.  Inicie a Instalação do Configuration Manager no servidor do site central usando um dos seguintes métodos:  

    -   Em **Iniciar**, clique em **Instalação do Configuration Manager**.  
    -   Abra o Setup.exe de &lt;*ConfigMgrInstallationMedia*>\SMSSETUP\BIN\X64.  
    -   Abra o Setup.exe de &lt;*ConfigMgrInstallationPath*>\BIN\X64.  

3.  Na página **Antes de Começar** escolha **Avançar**.  
4.  Na página **Guia de Introdução**, selecione **Desinstalar um site do Configuration Manager** e selecione **Avançar**.  
5.  Em **Desinstalar o Site do Configuration Manager**, especifique se deseja remover o banco de dados do site do servidor de site de administração central e se deseja remover o console do Configuration Manager. Por padrão, a Instalação remove os dois itens.  

    > [!IMPORTANT]  
    >  Quando houver um site primário conectado ao site de administração central, você deve desinstalar o site primário para poder desinstalar o site de administração central.  

6.  Selecione **Sim** para confirmar a desinstalação do site de administração central do Configuration Manager.  
