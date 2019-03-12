---
title: Notas de versão
titleSuffix: Configuration Manager
description: Saiba mais sobre os problemas urgentes que ainda não foram corrigidos no produto nem abordados em um artigo da base de dados de conhecimento do Suporte da Microsoft.
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c7e4307d61cccf968729f013ebaa4bfab4b0027e
ms.sourcegitcommit: 56ec6933cf7bfc93842f55835ad336ee3a1c6ab5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57211526"
---
# <a name="release-notes-for-configuration-manager"></a>Notas de versão do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Com o Configuration Manager, as notas da versão do produto estão limitadas a problemas urgentes. Esses problemas ainda não foram corrigidos no produto nem detalhados em um artigo da Base de Dados de Conhecimento de Suporte da Microsoft.  

A documentação específica do recurso inclui informações sobre problemas conhecidos que afetam os cenários principais.  

Este tópico contém notas de versão para o branch atual do Configuration Manager. Para obter informações sobre o branch da visualização técnica, confira [Visualização Técnica](/sccm/core/get-started/technical-preview)  

Para saber mais sobre os novos recursos introduzidos com diferentes versões, confira os seguintes artigos:
- [Novidades na versão 1810](/sccm/core/plan-design/changes/whats-new-in-version-1810)
- [Novidades na versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806)  
- [Novidades na versão 1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)

> [!Tip]  
> Para ser notificado quando esta página for atualizada, copie e cole a seguinte URL em seu leitor de feeds de RSS: `https://docs.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us`



## <a name="set-up-and-upgrade"></a>Configurar e atualizar  


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
*Aplica-se a: Configuration Manager versão 1802*

A partir do Configuration Manager versão 1802, o recurso Programa de Aperfeiçoamento da Experiência do Usuário é removido do produto. Durante a [automatização da instalação](/sccm/core/servers/deploy/install/command-line-options-for-setup) de um novo site por meio de um script de linha de comando ou autônomo, a instalação retorna um erro que indica que um parâmetro necessário está ausente. 

#### <a name="workaround"></a>Solução alternativa
Embora isso não afete o resultado do processo de instalação, inclua o parâmetro **JoinCEIP** na linha de comando de instalação.

 > [!Note]  
 > O parâmetro EnableSQM para a [instalação do console](/sccm/core/servers/deploy/install/install-consoles) não é necessário.


### <a name="cloud-service-manager-component-stopped-on-site-server-in-passive-mode"></a>Componente do gerenciador de serviços de nuvem parado no servidor do site no modo passivo
<!--VSO 2858826, SCCMDocs issue 772-->
*Aplica-se a: Configuration Manager versão 1806*

Se o [ponto de conexão de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point) estiver colocalizado com um [servidor de site no modo passivo](/sccm/core/servers/deploy/configure/site-server-high-availability), a implantação e o monitoramento de um [gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) não serão iniciados. O componente do gerenciador de serviços de nuvem (SMS_CLOUD_SERVICES_MANAGER) está em um estado parado.

#### <a name="workaround"></a>Solução alternativa
Mova a função de ponto de conexão do serviço para outro servidor.



<!-- ## Backup and recovery  -->


<!--## Client deployment and upgrade-->



## <a name="os-deployment"></a>Implantação de sistema operacional

### <a name="after-passive-site-server-is-promoted-the-default-boot-image-packages-still-have-package-source-on-the-previous-active-server"></a>Depois que o servidor do site passivo for promovido, os pacotes de imagem de inicialização padrão ainda terão a origem do pacote no servidor ativo anterior
<!--3453224, SCCMDocs-pr issue 3097-->
*Aplica-se a: Configuration Manager versão 1810*

Se você tiver um servidor do site no modo passivo (servidor B), quando promovê-lo a ativo, o local do conteúdo para imagens de inicialização padrão continuará a fazer referência ao servidor anteriormente ativo (servidor A). Se o servidor A tem uma falha de hardware, você não pode atualizar ou alterar as imagens de inicialização padrão.

#### <a name="workaround"></a>Solução alternativa
Nenhum



## <a name="software-updates"></a>Atualizações de software

### <a name="security-roles-are-missing-for-phased-deployments"></a>As funções de segurança estão ausentes para implantações em fases
<!--3479337, SCCMDocs-pr issue 3095-->
*Aplica-se a: Configuration Manager versão 1810*

A função de segurança interna **Gerenciador de Implantação de SO** tem permissões para [implantações em fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence). Estas permissões estão ausentes das funções a seguir:  

- **Administrador de Aplicativos**  
- **Gerenciador de Implantação de Aplicativos**  
- **Gerenciador de Atualização de Software**  

A função **Autor do Aplicativo** pode parecer ter algumas permissões para implantações em fases, mas não deve ser capaz de criar implantações. 

Um usuário com uma dessas funções pode iniciar o assistente Criar implantação em fases, podendo também ver implantações em fases para uma atualização de software ou aplicativo. Esse usuário não pode concluir o assistente nem fazer alterações em uma implantação existente.

#### <a name="workaround"></a>Solução alternativa
Criar uma função de segurança personalizada. Copie uma função de segurança existente e adicione as seguintes permissões na classe de objeto **Implantação em Fases**:
- Criar  
- Excluir  
- Modificar  
- Ler  

Para obter mais informações, confira [Criar funções de segurança personalizadas](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_CreateSecRole)


### <a name="changing-office-365-client-setting-doesnt-apply"></a>Não se aplica a alteração da configuração do cliente do Office 365 
<!--511551-->
*Aplica-se a: Configuration Manager versão 1802*  

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
*Aplica-se a: Configuration Manager versão 1710*

Não é possível criar um perfil de VPN usando o fluxo de trabalho do Windows Phone 8.1, o que também é aplicável aos dispositivos Windows 10. Para esses perfis, o assistente de criação não mostra mais a página Plataformas compatíveis. O Windows Phone 8.1 é selecionado automaticamente no back-end. A página Plataformas compatíveis está disponível nas propriedades do perfil, mas ela não exibe as opções do Windows 10.

#### <a name="workaround"></a>Solução alternativa
 Use o fluxo de trabalho do perfil de VPN do Windows 10 para dispositivos Windows 10. Se essa opção não for viável para seu ambiente, contate o suporte. O suporte pode ajudá-lo a adicionar o direcionamento do Windows 10.



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
