---
title: "Notas de versão "
titleSuffix: Configuration Manager
description: "Consulte essas notas para problemas urgentes que ainda não foram corrigidos no produto ou abordados em um artigo da Base de Dados de Conhecimento Microsoft."
ms.custom: na
ms.date: 11/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: "41"
caps.handback.revision: "0"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 8030ce7f98ebb34d9581ad036513b9b1c879c0ad
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2017
---
# <a name="release-notes-for-system-center-configuration-manager"></a>Release notes for System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Com o System Center Configuration Manager, as notas de versão do produto são limitadas apenas a problemas urgentes que ainda não foram corrigidos no produto (disponíveis por meio de uma atualização no console) ou são detalhadas em um artigo da Base de Dados de Conhecimento Microsoft.  

As informações sobre problemas conhecidos que afetam os cenários principais são transmitidas na documentação do produto online na biblioteca de documentação do System Center Configuration Manager.  

> [!TIP]  
>  Este tópico contém notas de versão para o branch atual do System Center Configuration Manager. Para o Technical Preview do System Center Configuration Manager, consulte [Technical Preview do System Center Configuration Manager](../../../../core/get-started/technical-preview.md)  

Para obter informações sobre os novos recursos introduzidos com diferentes versões, confira:
- [Novidades na versão 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)  
- [Novidades na versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702)
- [Novidades na versão 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610)



## <a name="setup-and-upgrade"></a>Instalar e atualizar  


### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>Ao instalar um site de Branch de Manutenção em Longo Prazo usando a versão 1606, um site do Branch Atual é instalado
<!-- Consider move to core content  -->
Quando você usar a mídia de linha de base da versão 1606 da versão de outubro de 2016 para instalar o site LTSB (Branch de Manutenção de Longo Prazo), a Instalação instala um site do Branch Atual em vez disso. Isso ocorre porque a opção de instalar um ponto de conexão de serviço com a instalação do site não está selecionada.

 - Embora um ponto de conexão de serviço não seja necessário, ele deve ser selecionado para instalar durante a Instalação para instalar um site LTSB.

Após a conclusão da instalação, você pode desinstalar o ponto de conexão de serviço.  No entanto, você deve ter um ponto de conexão de serviço no modo offline ou online para enviar dados de telemetria e obter atualizações de segurança para os sites do Branch Atual e LTSB.

Se seu site foi instalado como um site do Branch Atual, mas você queria instalar o LTSB, você pode desinstalar o site e reinstalá-lo. Como alternativa, você pode entrar em contato com a [Ajuda e Suporte da Microsoft](http://go.microsoft.com/fwlink/?LinkId=243064) para obter assistência.  

Para confirmar qual branch foi instalado, no console em **Administração** > **Configuração do Site** > **Sites**, abra **Configurações de Hierarquia**. A opção de converter o site em um site do Branch Atual está disponível apenas quando o site executa o LTSB.  

**Solução alternativa:**  não há.   


### <a name="an-update-is-stuck-with-a-state-of-downloading-in-the-updates-and-servicing-node-of-the-configuration-manager-console"></a>Uma atualização está paralisada no estado Baixando no nó Atualizações e Manutenção do console do Configuration Manager  
<!-- Source bug pending. Consider move to core content.  8/15 Seeking validation of issue from Dev.  -->
Durante o download automático de atualizações por um ponto de conexão de serviço online, uma atualização pode ficar paralisada em um estado Baixando. Quando o download de uma atualização é paralisado, entradas semelhantes as que se seguem aparecem nos arquivos de log indicados:  

Log do DMPdownloader:  

-   ERRO: falha ao baixar redistribuição para 037cd17e-4d7b-40e1-802b-14bb682364c7 com o comando /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI  "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"  

ConfigMgrSetup.log:  

-   Erro: falha ao verificar assinatura authenticode 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi'.  

-   Erro: falha de verificação de assinatura de arquivo para 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi  

**Solução alternativa**: no servidor do site, modifique a chave do Registro a seguir para corresponder ao que segue e reinicie o serviço SMS_Executive ou aguarde até 24 horas para o próximo ciclo de download automático.  

-   **Chave a ser editada**: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **Valor do Estado**: definido como decimal **146944** ou hexadecimal **0x00023e00**  


###  <a name="setup-fails-when-using-redist-files-from-the-cdlatest-folder-with-a-manifest-verification-error"></a>A instalação falha ao usar arquivos redist do pasta CD.Latst com um erro de verificação de manifesto
<!-- Source bug pending    8/15 Seeking validation of issue from Dev.   -->

Ao executar a instalação de uma pasta CD.Latest criada para a versão 1606 e usar os arquivos redist incluídos com essa pasta CD.Latest, a Instalação falha com os seguintes erros no log de instalação do Configuration Manager:

  - ERRO: falha de verificação de hash do arquivo para defaultcategories.dll
  - ERRO: falha na verificação de manifesto. Versão errada do manifesto?

**Solução alternativa:**  use um dos seguintes:
 - Durante a instalação, opte por baixar os arquivos redist mais recentes da Microsoft para usar em vez dos incluídos na pasta CD.Latest.
 - Exclua manualmente a pasta *cd.latest\redist\languagepack\zhh* e execute a instalação novamente.



<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>Implantação e atualização do cliente  

### <a name="client-installation-fails-with-error-code-0x8007064c"></a>A instalação do cliente falha com o código de erro 0x8007064c
<!--- SMS 486973  applies 1606 to 1706. Not yet fixed. -->
*O seguinte se aplica a todas as versões ativas do Configuration Manager.*   
Com todas as versões ativas de Quando você implanta o cliente em computadores com Windows, a instalação falha. O arquivo ccmsetup.log contém uma entrada "Arquivo 'C:\WINDOWS\ccmsetup\Silverlight.exe' retornou o código de falha de saída 1612. Falha na instalação"seguido por "Falha de InstallFromManifest 0x8007064c".

**Solução alternativa** Isso é causado por uma versão do Silverlight instalada anteriormente que estava corrompida. Você pode tentar executar a ferramenta a seguir no computador afetado para corrigir esse problema: [https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed)

## <a name="operating-system-deployment"></a>Implantação de sistema operacional  

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>Planos de manutenção criam muitos grupos e implantações de atualização de software duplicados por padrão  
Por padrão, o assistente para Criar Planos de Manutenção atualmente é executado depois de cada sincronização de atualizações de software. Toda vez que o assistente é executado, ele cria um novo grupo e implantação de atualização de software. Se você tiver um agendamento de sincronização de atualizações de software que é executado várias vezes ao dia, por exemplo, o assistente para Criar Planos de Manutenção criará vários, e provavelmente idênticos, grupos e implantações de atualização de software todos os dias.  

**Solução alternativa**:    
depois de criar um plano de manutenção, abra as propriedades do plano de manutenção, vá para a guia **Agendamento de Avaliação**, escolha **Executar a regra em um agendamento**, clique em **Personalizar** e crie um agendamento personalizado. Por exemplo, o plano de manutenção pode ser agendado para ser executado a cada 60 dias.  



## <a name="software-updates"></a>Atualizações de software

### <a name="importing-an-office-365-client-settings-from-a-configuration-file-fails-when-it-contains-unsupported-languages"></a>Ocorrerá falha ao importar as configurações de cliente do Office 365 de um arquivo de configuração se elas contiverem idiomas sem suporte
<!-- 489258  Fixed in 1706  -->
*O seguinte se aplica à versão 1702 e versões anteriores.*   
Quando você importar as configurações de cliente do Office 365 de um arquivo de configurações XML existente e o arquivo contiver idiomas que não têm suporte pelo cliente do Office 365 ProPlus, ocorrerá um erro. Para obter detalhes, veja [Implantar aplicativos do Office 365 a clientes a partir do Painel de Gerenciamento de Clientes do Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard).

**Solução alternativa**:    
Use apenas os [idiomas com suporte pelo cliente do Office 365 ProPlus](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx) no arquivo de configuração XML.  



## <a name="mobile-device-management"></a>Gerenciamento de dispositivos móveis  

### <a name="beginning-with-version-1710-you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10------503274--should-be-fixed-by-1802-if-not-sooner---"></a>A partir da versão 1710, não é mais possível implantar perfis de VPN do Windows Phone 8.1 no Windows 10 <!-- 503274  Should be fixed by 1802, if not sooner -->
Na 1710, não é mais possível criar um perfil de VPN usando o fluxo de trabalho do Windows Phone 8.1 que também é aplicável a dispositivos Windows 10. Para esses perfis, a página Plataformas compatível não é mais exibida no assistente de criação, e o Windows Phone 8.1 é selecionado automaticamente no back-end; nas páginas de propriedades, a página Plataformas com suporte está disponível, mas não são exibidas as opções do Windows 10.

**Solução alternativa**: use o fluxo de trabalho do perfil de VPN do Windows 10 para dispositivos Windows 10. Se isso não for viável para seu ambiente, contate o suporte. O suporte pode ajudá-lo a adicionar o direcionamento do Windows 10, se necessário.


### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram"></a>O apagamento completo desabilita dispositivos Windows 10 com menos de 4 GB de RAM
Executar um apagamento completo em dispositivos Windows 10 RTM (versões anteriores à versão 1511) com menos de 4 GB de RAM pode tornar o dispositivo inutilizável. Após tentar apagar o dispositivo, não é possível iniciá-lo e ele não responde.

**Solução alternativa**: certifique-se de que PCs com Windows 10 RTM tenham pelo menos 4 GB de RAM disponível antes de executar um apagamento completo do dispositivo. Para exibir o número de versão de dispositivos Windows 10, digite "winver" em um prompt de comando. Se o dispositivo já tiver sido apagado e não estiver mais respondendo, use uma unidade Windows 10 USB inicializável para iniciar e recuperar o acesso ao dispositivo.


### <a name="when-a-user-belongs-to-two-or-more-user-collections-that-a-terms-and-conditions-policy-is-deployed-to-the-user-sees-multiple-sets-of-the-same-terms"></a>Quando um usuário pertencer a duas ou mais coleções de usuários às quais uma política de termos e condições é implantada, o usuário vê vários conjuntos dos mesmos termos  
<!-- 454394    -->
Quando um administrador implantar um conjunto de termos em várias coleções de usuários, e um usuário for membro de mais de uma dessas coleções, esse usuário terá várias cópias apresentadas de termos idênticos ao abrir o Portal da Empresa.  Por exemplo, se um usuário chamado “SampleUser” for membro de duas coleções de usuários diferentes, uma chamada “CompanyEmployeesFTE” e “CompanyEmployeesNA”, e os termos e condições chamados “CompanyTerms” forem implantados em CompanyEmployeesFTE e CompanyEmployeesNA, SampleUser verá dois conjuntos idênticos de CompanyTerms na página de aceitação dos termos. Visto que os usuários só podem aceitar ou recusar todos os termos, não há nenhum risco de haver um estado de aceitação ambíguo (no qual o usuário tenha aceitado e rejeitado os termos ao mesmo tempo). O relatório de aceitação dos Termos e Condições incluirá apenas uma linha para cada conjunto de termos para cada usuário. Portanto, não há nenhum erro no relatório. O único efeito é que o usuário verá dois conjuntos de termos na página de aceitação.  

**Solução alternativa**: certifique-se de que cada usuário está incluído somente em uma coleção à qual os termos foram implantados.  


### <a name="android-for-work-email-profiles-that-use-certificate-authentication-are-not-applied-to-devices"></a>Perfis de email do Android for Work que usam a autenticação de certificado não são aplicados aos dispositivos
<!--  487657      -->
Quando um perfil de email do Android for Work for criado, haverá duas opções para autenticação. Um é o nome de usuário e senha, o outro são certificados. Neste momento, a opção de certificados não está funcionando. Se o perfil for criado com o método de autenticação definido como **certificados**, o perfil não será aplicado ao dispositivo, e o usuário receberá uma solicitação para inserir manualmente os detalhes da conta de email.

**SOLUÇÃO ALTERNATIVA**: nenhuma. Os administradores devem usar a opção de **nome de usuário e senha**, ou aguarde até que este problema tenha sido resolvido.



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
