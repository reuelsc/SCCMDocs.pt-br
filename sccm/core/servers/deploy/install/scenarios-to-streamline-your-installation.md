---
title: "Cenários de instalação | Microsoft Docs"
description: "Conheça técnicas para instalar uma nova hierarquia do Configuration Manager quando você estiver atualizando."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 8333f9280f609c761ba5368b801d273f9a11ebb5


---
# <a name="scenarios-to-streamline-your-installation-of-system-center-configuration-manager"></a>Cenários para simplificar a instalação do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Com o lançamento das versões de atualização para o branch atual do System Center Configuration Manager, há novos cenários para simplificar a instalação de uma nova hierarquia para uma versão de atualização (como a atualização 1602) e para atualizar do Microsoft System Center 2012 Configuration Manager.  

Entre os cenários com suporte estão:  

**Instalar uma nova hierarquia do branch atual do System Center Configuration Manager** que executa uma versão de atualização:  

-   Você instala apenas o site de nível superior seguido imediatamente pela instalação de uma atualização para levar esse site até a versão de atualização que você usará. Em seguida, você pode instalar os sites adicionais diretamente nessa versão de atualização.  

-   Esse cenário ignora a instalação de sites adicionais em um nível de linha de base para, depois, atualizá-los para a versão de atualização que você deseja usar.  

-   Esse cenário ignora a instalação de clientes com uma versão de linha de base para, depois, precisar reinstalá-los quando você atualizar para uma versão posterior.  

**Atualizar a infraestrutura do Microsoft System Center 2012 Configuration Manager** para uma versão de atualização do System Center Configuration Manager:  

-   Atualize manualmente o site de administração central e cada site primário para uma versão de linha de base (como a 1511) antes de instalar uma versão de atualização (como a 1602).  

-   Não atualize os sites secundários por meio do Microsoft System Center 2012 Configuration Manager até que seus sites primários executem a versão de atualização que você usará.  

-   Não atualize os clientes do Microsoft System Center 2012 Configuration Manager até que seus sites primários executem a versão de atualização que você usará.  

## <a name="scenario---install-a-new-hierarchy-to-an-update-version"></a>Cenário - Instalação de uma nova hierarquia para uma versão de atualização  
Nesse cenário de exemplo, instale o primeiro site de uma hierarquia usando uma versão de linha de base da versão 1511 do System Center Configuration Manager. Em seguida, instale a atualização 1602 antes de implantar sites ou clientes adicionais.  

-   Como você planeja usar uma versão de atualização (como a 1602) e não permanecer com uma versão de linha de base (como a 1511), não é necessário instalar sites adicionais e depois atualizá-los, nem instalar e atualizar clientes.  

-   Não instale sites secundários com a versão 1511 e depois atualize-os para a 1602. Em vez disso, instale-os após a execução da 1602 por seus sites primários.  

**Use a sequência abaixo:**  

1.  **Instale um site de nível superior para sua nova hierarquia** usando a mídia de linha de base.  

    -   Você só pode usar a mídia de linha de base para instalar o primeiro site de uma nova hierarquia.  

    -   Por exemplo, instale um site de nível superior usando a versão de linha de base da 1511. Consulte [Usar o Assistente de instalação para instalar sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)  

    Após essa etapa, o site de nível superior executará a versão 1511.  

2.  **Use atualizações no console para atualizar o site de nível superior para uma versão posterior.**  

    -   Antes de instalar quaisquer sites filho ou clientes, atualize seu site de nível superior para a versão de atualização que você planeja usar.  

    -   Por exemplo, você pode atualizar seu site de nível superior que executa a versão 1511 para a versão 1602. Consulte [Atualizações para o System Center Configuration Manager](../../../../core/servers/manage/updates.md).  

    Após essa etapa, o site de nível superior executará a versão 1602.  

3.  **Instale novos sites primários filho abaixo de um site de administração central.**  

    -   Use a mídia de instalação da pasta CD.Latest no servidor do site de administração central para instalar os sites primários filho.  (Consulte [A pasta CD.Latest do System Center Configuration Manager](../../../../core/servers/manage/the-cd.latest-folder.md))  

        -   A mídia de origem é necessária para garantir que os novos sites primários filho correspondam à versão do site de administração central.  

    Após essa etapa, seus novos sites primários filho executarão a versão 1602.  

4.  **Em cada site primário, use a opção no console para instalar novos sites secundários.**  

    -   Como você não instalou sites secundários enquanto os sites primários estavam com a versão 1511, não será necessário atualizar para sites secundários.  

    -   Em vez disso, instale novos sites secundários que executam a versão 1602. Consulte *Instalar um site secundário* em [Usar o Assistente de Instalação para instalar sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).  

    Após essa etapa, novos sites secundários serão instalados e executarão a versão 1602.  

5.  **Instale novos clientes no site primário.**  

    -   Como você não instalou clientes enquanto os sites primários estavam com a versão 1511, não será necessário atualizar os clientes da versão 1511 para a versão 1602.  

    -   Em vez disso, instale novos clientes que executam a versão 1602. Consulte [Implantar clientes no System Center Configuration Manager](../../../clients/deploy/deploy-clients-to-windows-computers.md).  

    Após essa etapa, os novos clientes que executam a versão 1602 serão instalados.  

## <a name="scenario---upgrade-system-center-2012-configuration-manager-to-an-update-version-of-system-center-configuration-manager-current-branch"></a>Cenário - Atualização do System Center 2012 Configuration Manager para uma versão de atualização da ramificação atual do System Center Configuration Manager  
Nesse cenário de exemplo, atualize sua infraestrutura do Microsoft System Center 2012 Configuration Manager para uma versão de atualização do System Center Configuration Manager, como a versão 1602.  

-   O site de administração central e cada site primário devem ser atualizados para a versão de linha de base 1511 antes de instalar a atualização para a versão 1602.  

-   Os clientes e os sites secundários não são atualizados ou instalam a versão 1511. Em vez disso, eles são movidos diretamente do Microsoft System Center 2012 Configuration Manager para o System Center Configuration Manager versão 1602.  

**Use a sequência abaixo:**  

1.  **Atualize seu site do Microsoft System Center 2012 Configuration Manager de nível superior** para uma versão de linha de base do branch atual usando a mídia de origem para o System Center Configuration Manager (como a versão 1511). Consulte [Atualização para o System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

    -   Assim como acontece com cenários de atualização tradicionais, sempre atualize primeiro o site de nível superior de uma hierarquia e, depois, atualize os sites filho.  

    Após essa etapa, seu site de nível superior executará a versão 1511.  

2.  **Atualize cada site primário filho em sua hierarquia** para a mesma versão de linha de base.  

    -   Quando você atualiza do Microsoft System Center 2012 Configuration Manager, é necessário atualizar manualmente cada site primário para uma versão de linha de base do branch atual.  

    -   Você não atualizará os sites secundários neste momento.  

    Após essa etapa, cada site primário executará a versão 1511.  

3.  **Defina as janelas de manutenção em sites primários filho.** Depois de atualizar todos os seus sites primários para a versão de linha de base, planeje a configuração das janelas de manutenção a fim de controlar quando esses sites instalarão as atualizações de infraestrutura. Consulte [Como usar as janelas de manutenção no System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md).  (As janelas de manutenção são chamadas de janelas de serviço na versão 1511.)  

    -   Um site primário filho instala automaticamente as mesmas atualizações que você instala em um site de administração central.  

    -   Os sites secundários não instalam automaticamente novas versões e devem ser atualizados manualmente de dentro do console.  

    > [!NOTE]  
    >  Se você usar a versão 1511 e quiser usar as janelas de serviço, será necessário instalar primeiro o hotfix do [artigo 3142341 da Base de Dados de Conhecimento da Microsoft](http://support.microsoft.com/kb/3142341). Esse problema é resolvido quando você instala a atualização 1602.  

    Após essa etapa, quando você instala atualizações no site de administração central, os sites primários filho instalarão essa atualização apenas quando for permitido pela janela de manutenção.  

4.  **Instale a versão de atualização em seu site de nível superior.** Isso atualiza o site de nível superior. Após um site de administração central instalar a versão da atualização, cada site primário filho instalará automaticamente a atualização, a menos que seja bloqueado por uma janela de manutenção.  

    -   Por exemplo, você pode atualizar seu site de nível superior da versão 1511 para a versão 1602. Consulte [Atualizações para o System Center Configuration Manager](../../../../core/servers/manage/updates.md)  

    Após essa etapa, o site de administração central e cada site primário executarão a versão 1602.  

5.  **Atualização de sites secundários.** Depois que um site primário instala a atualização e executa a versão 1602, você usa a opção no console para atualizar os sites secundários.  

    -   Isso atualiza os sites secundários diretamente do Microsoft System Center 2012 Configuration Manager para a versão de atualização instalada no site primário.  

    -   Para obter informações sobre como atualizar um site secundário, consulte [Atualizar sites](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade) em [Atualizar para o System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

6.  **Atualizar clientes.** Use as informações disponíveis em [Como atualizar clientes para computadores Windows no System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

    -   Isso atualiza os clientes diretamente do Microsoft System Center 2012 Configuration Manager para a versão de atualização instalada no site primário.  

    Após essa etapa, os clientes serão atualizados para a versão 1602 sem atualizar primeiro para a versão 1511.



<!--HONumber=Dec16_HO3-->


