---
title: "Notas de versão "
titleSuffix: Configuration Manager
description: "Consulte essas notas para problemas urgentes que ainda não foram corrigidos no produto ou abordados em um artigo da Base de Dados de Conhecimento Microsoft."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: 
caps.handback.revision: 
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 53685ef2647cfd87c2fcb603097186360f1c96a5
ms.sourcegitcommit: fbd4a9d2fa8ed4ddd3a0fecc4a2ec4fc0ccc3d0c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/19/2018
---
# <a name="release-notes-for-system-center-configuration-manager"></a>Release notes for System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Com o Configuration Manager, as notas da versão do produto estão limitadas a problemas urgentes. Esses problemas ainda não foram corrigidos no produto ou detalhados em um artigo da Base de dados de conhecimento da Microsoft.  

A documentação específica do recurso inclui informações sobre problemas conhecidos que afetam os cenários principais.  

> [!TIP]  
>  Este tópico contém notas de versão para o branch atual do Configuration Manager. Para saber mais sobre o branch da visualização técnica, consulte [Technical Preview do System Center Configuration Manager](../../../../core/get-started/technical-preview.md)  

Para saber mais sobre os novos recursos introduzidos com diferentes versões, confira os seguintes artigos:
- [Novidades na versão 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)
- [Novidades na versão 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)  
- [Novidades na versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702)



## <a name="setup-and-upgrade"></a>Instalar e atualizar  


### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>Ao instalar um site de Branch de Manutenção em Longo Prazo usando a versão 1606, um site do Branch Atual é instalado
<!-- Consider move to core content  -->
Quando você usar a mídia de linha de base da versão 1606 da versão de outubro de 2016 para instalar o site LTSB (Branch de Manutenção de Longo Prazo), a Instalação instala um site do Branch Atual em vez disso. Esse comportamento ocorre porque a opção de instalar um ponto de conexão de serviço com a instalação do site não está selecionada.

 - Embora um ponto de conexão de serviço não seja necessário, ele deve ser selecionado para instalar durante a Instalação para instalar um site LTSB.

Após a conclusão da instalação, você pode desinstalar o ponto de conexão de serviço. No entanto, você deve ter um ponto de conexão de serviço no modo offline ou online para enviar dados de telemetria e obter atualizações de segurança para os sites do Branch Atual e LTSB.

Se seu site foi instalado como um site do Branch Atual, mas você queria instalar o LTSB, você pode desinstalar o site e reinstalá-lo. Como alternativa, você pode entrar em contato com a [Ajuda e Suporte da Microsoft](http://go.microsoft.com/fwlink/?LinkId=243064) para obter assistência.  

Para confirmar qual branch foi instalado, no console em **Administração** > **Configuração do Site** > **Sites**, abra **Configurações de Hierarquia**. A opção de converter o site em um site do Branch Atual está disponível apenas quando o site executa o LTSB.  

**Solução alternativa:** nenhuma.   


### <a name="an-update-persists-in-downloading-state-in-the-updates-and-servicing-node-of-the-console"></a>Uma atualização continua no estado de download no nó de Atualizações e Manutenção do console  
<!-- Source bug pending. Consider move to core content.  8/15 Seeking validation of issue from Dev.  -->
Durante o download automático de atualizações por um ponto de conexão de serviço online, uma atualização pode ficar paralisada em um estado Baixando. Quando o download de uma atualização é paralisado, entradas semelhantes as que se seguem aparecem nos arquivos de log indicados:  

Log do DMPdownloader:  
`ERROR: Failed to download redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 with command  /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI  "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"`  

ConfigMgrSetup.log:  
`Error: failed to verify 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi' authenticode signature.`  
`Error: file signature check failed for 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi`  

**Solução alternativa**: no servidor do site, modifique a seguinte chave de registro para corresponder ao seguinte valor:  

-   **Chave a ser editada**: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **Valor do Estado**: definido como o decimal **146944** ou o hexadecimal **0x00023e00**  

Em seguida, reinicie o serviço SMS_Executive ou aguarde até 24 horas para o próximo ciclo de download automático.

### <a name="when-using-redistributable-files-from-the-cdlatest-folder-setup-fails-with-a-manifest-verification-error"></a>Ao usar arquivos redistribuíveis da pasta CD.Latest, a instalação falha com um erro de verificação de manifesto
<!-- Source bug pending    8/15 Seeking validation of issue from Dev.   -->

Ao executar a instalação da pasta CD.Latest criada para a versão 1606 e usar os arquivos redistribuíveis incluídos com essa pasta CD.Latest, a instalação falha com os seguintes erros no log de instalação do Configuration Manager:

  `ERROR: File hash check failed for defaultcategories.dll`  
  `ERROR: Manifest verification failed. Wrong version of manifest?`

**Solução alternativa:** use uma das seguintes opções:
 - Durante a instalação, opte por baixar os arquivos redistribuíveis mais recentes da Microsoft. Use os arquivos redistribuíveis mais recentes em vez dos arquivos incluídos na pasta CD.Latest.
 - Exclua manualmente a pasta *cd.latest\redist\languagepack\zhh* e execute a instalação novamente.



<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>Implantação e atualização do cliente  

### <a name="client-installation-fails-with-error-code-0x8007064c"></a>A instalação do cliente falha com o código de erro 0x8007064c
<!--- SMS 486973  applies 1606 to 1706. Not yet fixed. -->
*O seguinte problema se aplica a todas as versões ativas do Configuration Manager.*  

Quando você implanta o cliente em computadores com Windows, a instalação falha. O arquivo ccmsetup.log contém as seguintes entradas: 

`File 'C:\WINDOWS\ccmsetup\Silverlight.exe' returned failure exit code 1612. Fail the installation`  
`InstallFromManifest failed 0x8007064c`

**Solução alternativa** Uma versão do Silverlight corrompida e instalada anteriormente gera o problema. Para corrigir esse problema, execute a ferramenta a seguir no computador afetado: [Corrigir problemas que bloqueiam os programas de serem instalados ou removidos](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed).

## <a name="operating-system-deployment"></a>Implantação de sistema operacional  

### <a name="servicing-plans-create-many-duplicate-software-update-groups-and-deployments-by-default"></a>Planos de manutenção criam muitos grupos e implantações de atualização de software duplicados por padrão  
Por padrão, o assistente para Criar Planos de Manutenção atualmente é executado depois de cada sincronização de atualizações de software. Toda vez que o assistente é executado, ele cria um novo grupo e implantação de atualização de software. Se você tiver um agendamento de sincronização de atualizações de software que é executado várias vezes ao dia, o assistente para Criar Planos de Manutenção cria vários grupos e implantações de atualização de software todos os dias.  

**Solução alternativa**: depois de criar um plano de manutenção, abra as propriedades do plano de manutenção, vá para a guia **Agendamento de Avaliação**, escolha **Executar a regra em um agendamento**, clique em **Personalizar** e crie um agendamento personalizado. Por exemplo, o plano de manutenção pode ser agendado para ser executado a cada 60 dias.  



## <a name="software-updates"></a>Atualizações de software

### <a name="importing-an-office-365-client-settings-from-a-configuration-file-fails-when-it-contains-unsupported-languages"></a>Ocorrerá falha ao importar as configurações de cliente do Office 365 de um arquivo de configuração se elas contiverem idiomas sem suporte
<!-- 489258  Fixed in 1706  -->
*O seguinte problema se aplica à versão 1702 e versões anteriores.*   

Quando você importar as configurações de cliente do Office 365 de um arquivo de configurações XML existente e o arquivo contiver idiomas que não têm suporte pelo cliente do Office 365 ProPlus, ocorre um erro. Para saber mais, confira [Implantar aplicativos do Office 365 em clientes desde o Painel de Gerenciamento de Clientes do Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard).

**Solução alternativa**: use apenas os [idiomas com suporte pelo cliente do Office 365 ProPlus](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx) no arquivo de configuração XML.  



## <a name="mobile-device-management"></a>Gerenciamento de dispositivos móveis  

### <a name="beginning-with-version-1710-you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10------503274--should-be-fixed-by-1802-if-not-sooner---"></a>A partir da versão 1710, não é mais possível implantar perfis de VPN do Windows Phone 8.1 no Windows 10 <!-- 503274  Should be fixed by 1802, if not sooner -->
Na 1710, não é mais possível criar um perfil de VPN usando o fluxo de trabalho do Windows Phone 8.1 que também é aplicável a dispositivos Windows 10. Para esses perfis, a página de Plataformas com Suporte não é mostrada no assistente de criação. O Windows Phone 8.1 é selecionado automaticamente no back-end. A página Plataformas com Suporte está disponível nas propriedades do perfil, mas não exibe as opções do Windows 10.

**Solução alternativa**: use o fluxo de trabalho do perfil de VPN do Windows 10 para dispositivos Windows 10. Se essa opção não for viável para seu ambiente, contate o suporte. O suporte pode ajudá-lo a adicionar o direcionamento do Windows 10.


### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-of-memory"></a>O apagamento completo desabilita dispositivos Windows 10 com menos de 4 GB de memória
Executar limpeza completa em dispositivos que executam o Windows 10, versão 1507, com menos de 4 GB de RAM pode deixar o dispositivo inutilizável. Após tentar apagar o dispositivo, não é possível iniciá-lo e ele não responde.

**Solução alternativa**: certifique-se de que os dispositivos do Windows 10 tenham pelo menos 4 GB de memória disponível antes de executar uma limpeza completa. Para exibir o número de versão de dispositivos Windows 10, digite "winver" em um prompt de comando. Se você já limpou o dispositivo e ele não está mais responsivo, use uma unidade USB inicializável do Windows 10 para recuperar o dispositivo.


### <a name="when-a-user-belongs-to-two-or-more-user-collections-to-which-you-deploy-a-terms-and-conditions-policy-the-user-sees-multiple-sets-of-the-same-terms"></a>Quando um usuário pertencer a duas ou mais coleções de usuários às quais você implanta uma política de termos e condições, o usuário vê vários conjuntos dos mesmos termos  
<!-- 454394    -->
Se você implantar um conjunto de termos em várias coleções de usuários, e um usuário for membro de mais de uma dessas coleções, esse usuário vê várias cópias de termos idênticos no Portal da Empresa. Por exemplo:
- Um usuário chamado "SampleUser" é um membro de duas coleções de usuários diferentes, "CompanyEmployeesFTE" e "CompanyEmployeesNA"
- Você implanta os termos e condições "CompanyTerms" para CompanyEmployeesFTE e CompanyEmployeesNA
- O SampleUser vê dois conjuntos idênticos de CompanyTerms na página de aceitação de termos no Portal da Empresa. 

Os usuários só podem aceitar todos ou recusar todos os termos. Portanto, não há perigo de um estado de aceitação ambíguo. (Esse estado ambíguo acontece quando o usuário aceita e rejeita os mesmos termos). O relatório de aceitação dos Termos e Condições inclui apenas uma linha para cada conjunto de termos para cada usuário. Portanto, não há nenhum erro no relatório. O único efeito é que o usuário vê dois conjuntos de termos na página de aceitação.  

**Solução alternativa**: certifique-se de que cada usuário está incluído somente em uma coleção à qual os termos foram implantados.  


<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
