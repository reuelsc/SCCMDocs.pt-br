---
title: Definir as configurações do Microsoft Edge
titleSuffix: Configuration Manager
description: Definir as configurações do navegador da Web Microsoft Edge em clientes do Windows 10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: 57393c00faa0cc26d785d91ad1c6ecb9407ba5da
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/23/2018
---
# <a name="configure-microsoft-edge-settings-in-system-center-configuration-manager"></a>Definir as configurações do Microsoft Edge no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

<!-- 1357310 -->
A partir da versão 1802, para os clientes que utilizam o navegador da Web [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) em clientes do Windows 10, crie uma política de configurações de conformidade do Configuration Manager para definir várias configurações do Microsoft Edge. 



## <a name="policy-settings"></a>Configurações de política
Esta política atualmente inclui as seguintes configurações:
- **Definir o navegador Microsoft Edge como padrão** : configura a configuração do aplicativo padrão do Windows 10 para o navegador da Web para o Microsoft Edge
- **Permitir lista suspensa da barra de endereços**: exige o Windows 10, versão 1703 ou posterior. Para saber mais, confira a [política de navegador AllowAddressBarDropdown ](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).
- **Permitir sincronizar favoritos entre navegadores da Microsoft** : requer o Windows 10, versão 1703 ou posterior. Para saber mais, confira a [política de navegador SyncFavoritesBetweenIEAndMicrosoftEdge](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).
- **Permitir limpar dados de navegação na saída**: requer o Windows 10, versão 1703 ou posterior. Para saber mais, confira a [política do navegador ClearBrowsingDataOnExit](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).
- **Permitir não rastrear cabeçalhos**: para obter mais informações, confira a [política do navegador AllowDoNotTrack](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).
- **Permitir preenchimento automático**: para obter mais informações, confira a [ política do navegador AllowAutofill](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).
- **Permitir cookies**: para obter mais informações, confira a [política do navegador AllowCookies](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).
- **Permitir o bloqueador de pop-up**: para obter mais informações, confira a [política do navegador AllowPopups](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).
- **Permitir sugestões de pesquisa na barra de endereços**: Para saber mais, confira a [política do navegador AllowSearchSuggestionsinAddressBar](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).
- **Permitir enviar o tráfego de Intranet para o Internet Explorer** : para obter mais informações, confira a [política do navegador SendIntranetTraffictoInternetExplorer](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).
- **Permitir o gerenciador de senhas**: para obter mais informações, confira a [política do navegador AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).
- **Permitir Ferramentas para desenvolvedores**: Para saber mais, confira a [política do navegador AllowDeveloperTools](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).
- **Permitir extensões**: para obter mais informações, confira a [política de navegador AllowExtensions](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).



## <a name="create-the-microsoft-edge-browser-profile"></a>Criar o perfil do navegador Microsoft Edge

1. No console do Configuration Manager, vá até o espaço de trabalho **Ativos e conformidade**. Expanda as **Configurações de conformidade** e selecione o novo nó **Perfis de navegador do Microsoft Edge**. Clique na opção da faixa de opções para **Criar a política do navegador do Microsoft Edge**.
2. Especifique um **Nome** para a política, digite opcionalmente a **Descrição** e clique em **Avançar**.
3. Na página **Configurações**, altere o valor para **Configurado** para que as configurações sejam incluídas nesta política e clique em **Avançar**.
4. Na página **Plataformas com suporte**, selecione as versões e arquiteturas do sistema operacional às quais esta política se aplica e clique em **Avançar**. 
5. Conclua o assistente.



## <a name="deploy-the-policy"></a>Implantar a política

1. Selecione sua política e clique na opção da faixa de opções para **Implantar**.
2. Clique em **Procurar** para selecionar a coleção de usuário ou dispositivo para a qual implantar a política. 
3. Selecione as opções adicionais conforme necessário. 
    a. Gerar alertas quando a política não for compatível. 
    b. Defina o agendamento pelo qual o cliente avalia a conformidade do dispositivo com esta política.
4. Clique em **OK** para criar a implantação.



## <a name="next-steps"></a>Próximas etapas

Como qualquer política de configurações de conformidade, o cliente soluciona as configurações no agendamento especificado. [Monitore e relate a conformidade do dispositivo](/sccm/compliance/deploy-use/monitor-compliance-settings) no console do Configuration Manager.
