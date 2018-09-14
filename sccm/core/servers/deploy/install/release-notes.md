---
title: Notas de versão
titleSuffix: Configuration Manager
description: Saiba mais sobre os problemas urgentes que ainda não foram corrigidos no produto nem abordados em um artigo da Base de Dados de Conhecimento de Suporte da Microsoft.
ms.date: 08/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 939ab4b97a1a62eeae834873dd39e2f0d435527d
ms.sourcegitcommit: 7eebd112a9862bf98359c1914bb0c86affc5dbc0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/22/2018
ms.locfileid: "42590090"
---
# <a name="release-notes-for-configuration-manager"></a>Notas de versão do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Com o Configuration Manager, as notas da versão do produto estão limitadas a problemas urgentes. Esses problemas ainda não foram corrigidos no produto nem detalhados em um artigo da Base de Dados de Conhecimento de Suporte da Microsoft.  

A documentação específica do recurso inclui informações sobre problemas conhecidos que afetam os cenários principais.  

> [!TIP]  
>  Este tópico contém notas de versão para o branch atual do Configuration Manager. Para obter informações sobre o branch da visualização técnica, confira [Visualização Técnica](/sccm/core/get-started/technical-preview)  

Para saber mais sobre os novos recursos introduzidos com diferentes versões, confira os seguintes artigos:
- [Novidades na versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806)  
- [Novidades na versão 1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)
- [Novidades na versão 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)



## <a name="setup-and-upgrade"></a>Instalar e atualizar  


### <a name="when-using-redistributable-files-from-the-cdlatest-folder-setup-fails-with-a-manifest-verification-error"></a>Ao usar arquivos redistribuíveis da pasta CD.Latest, a instalação falha com um erro de verificação de manifesto
<!-- 510080, 490569  -->

Ao executar a instalação da pasta CD.Latest criada para a versão 1606 e usar os arquivos redistribuíveis incluídos nessa pasta CD.Latest, a instalação falha com os seguintes erros no log de Instalação do Configuration Manager:

  `ERROR: File hash check failed for defaultcategories.dll`  
  `ERROR: Manifest verification failed. Wrong version of manifest?`

#### <a name="workaround"></a>Solução alternativa
Use uma das seguintes opções:
 - Durante a instalação, opte por baixar os arquivos redistribuíveis mais recentes da Microsoft. Use os arquivos redistribuíveis mais recentes em vez dos arquivos incluídos na pasta CD.Latest.
 - Exclua manualmente a pasta *cd.latest\redist\languagepack\zhh* e execute a instalação novamente.


### <a name="setup-command-line-option-joinceip-must-be-specified"></a>O JoinCEIP da opção de linha de comando de instalação deve ser especificado
<!--510806-->
*Aplicável a: Configuration Manager versão 1802*

A partir do Configuration Manager versão 1802, o recurso Programa de Aperfeiçoamento da Experiência do Usuário é removido do produto. Durante a [automatização da instalação](/sccm/core/servers/deploy/install/command-line-options-for-setup) de um novo site por meio de um script de linha de comando ou autônomo, a instalação retorna um erro que indica que um parâmetro necessário está ausente. 

#### <a name="workaround"></a>Solução alternativa
Embora isso não afete o resultado do processo de instalação, inclua o parâmetro **JoinCEIP** na linha de comando de instalação.

 > [!Note]  
 > O parâmetro EnableSQM para a [instalação do console](/sccm/core/servers/deploy/install/install-consoles) não é necessário.


### <a name="cloud-service-manager-component-stopped-on-site-server-in-passive-mode"></a>Componente do gerenciador de serviços de nuvem parado no servidor do site no modo passivo
<!--VSO 2858826, SCCMDocs issue 772-->
*Aplicável a: Configuration Manager versão 1806*

Se o [ponto de conexão de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point) estiver colocalizado com um [servidor de site no modo passivo](/sccm/core/servers/deploy/configure/site-server-high-availability), a implantação e o monitoramento de um [gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) não serão iniciados. O componente do gerenciador de serviços de nuvem (SMS_CLOUD_SERVICES_MANAGER) está em um estado parado.

#### <a name="workaround"></a>Solução alternativa
Mova a função de ponto de conexão do serviço para outro servidor.



<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>Implantação e atualização do cliente

### <a name="azure-ad-enabled-clients-cant-communicate-with-management-point"></a>Os clientes habilitados para o Azure AD não podem se comunicar com o ponto de gerenciamento
<!--501089-->
*Aplicável a: Configuration Manager versão 1706*
<!--also fixed in 1710 HFRU--> No cenário de [instalação e atribuição dos clientes do Configuration Manager Windows 10 usando o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure), a comunicação do cliente falha quando o ponto de gerenciamento habilitado para HTTPS usa credenciais de banco de dados alternativas. 

#### <a name="workaround"></a>Solução alternativa
Atenue esse problema com uma das seguintes ações:
- Atualizar o site para a última versão e aplicar o último hotfix
- Altere as credenciais usadas pelo ponto de gerenciamento.


<!-- ## Operating system deployment  -->



## <a name="software-updates"></a>Atualizações de software

### <a name="changing-office-365-client-setting-doesnt-apply"></a>Não se aplica a alteração da configuração do cliente do Office 365 
<!--511551-->
*Aplicável a: Configuration Manager versão 1802*  

Implante uma [configuração de cliente](/sccm/core/clients/deploy/about-client-settings#enable-management-of-the-office-365-client-agent) com **Habilitar o gerenciamento do Agente Cliente do Office 365** configurado para `Yes`. Em seguida, altere a configuração para `No` ou `Not Configured`. Depois de atualizar a política de clientes direcionados, as atualizações do Office 365 ainda são gerenciadas pelo Configuration Manager. 

#### <a name="workaround"></a>Solução alternativa
Altere o seguinte valor de registro para `0` e reinicie o **Serviço Clique para Executar do Microsoft Office** (ClickToRunSvc):

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\office\16.0\Common\officeupdate]
"OfficeMgmtCOM"=dword:00000000
```



## <a name="mobile-device-management"></a>Gerenciamento de dispositivos móveis  

### <a name="you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10"></a>Não é mais possível implantar perfis de VPN do Windows Phone 8.1 no Windows 10
<!-- 503274  -->
*Aplicável a: Configuration Manager versão 1710*

Não é possível criar um perfil de VPN usando o fluxo de trabalho do Windows Phone 8.1, o que também é aplicável aos dispositivos Windows 10. Para esses perfis, o assistente de criação não mostra mais a página Plataformas compatíveis. O Windows Phone 8.1 é selecionado automaticamente no back-end. A página Plataformas compatíveis está disponível nas propriedades do perfil, mas ela não exibe as opções do Windows 10.

#### <a name="workaround"></a>Solução alternativa
 Use o fluxo de trabalho do perfil de VPN do Windows 10 para dispositivos Windows 10. Se essa opção não for viável para seu ambiente, contate o suporte. O suporte pode ajudá-lo a adicionar o direcionamento do Windows 10.



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
