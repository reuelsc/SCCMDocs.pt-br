---
title: "Notas de versão – Configuration Manager | Microsoft Docs"
description: "Consulte essas notas para problemas urgentes que ainda não foram corrigidos no produto ou abordados em um artigo da Base de Dados de Conhecimento Microsoft."
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: 41
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 7a6c89254d01f4074e5c170b20338686178ebdd3
ms.openlocfilehash: 59946d1328be1606ba7c4dab647e814c1b4e638a
ms.contentlocale: pt-br
ms.lasthandoff: 04/28/2017


---
# <a name="release-notes-for-system-center-configuration-manager"></a>Release notes for System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Com o System Center Configuration Manager, as notas de versão do produto são limitadas apenas a problemas urgentes que ainda não foram corrigidos no produto (disponíveis por meio de uma atualização no console) ou são detalhadas em um artigo da Base de Dados de Conhecimento Microsoft.  

 Para problemas conhecidos que afetam os cenários principais, essas informações são transmitidas na documentação do produto online na biblioteca de documentação do System Center Configuration Manager.  

> [!TIP]  
>  Este tópico contém notas de versão para o branch atual do System Center Configuration Manager. Para o Technical Preview do System Center Configuration Manager, consulte [Technical Preview do System Center Configuration Manager](../../../../core/get-started/technical-preview.md)  

## <a name="setup-and-upgrade"></a>Instalar e atualizar  

### <a name="after-you-update-a-configuration-manager-console-using-consolesetupexe-from-the-site-server-folder-recent-language-pack-changes-are-not-available"></a>Depois de atualizar um console do Configuration Manager usando ConsoleSetup.exe da pasta do servidor de site, as alterações recentes do pacote de idioma não estarão disponíveis
<!--  SMS 486420  Applicability should be 1610 and 1702.  -->
Depois de executar uma atualização in-loco para um console usando ConsoleSetup.exe de uma pasta de instalação de servidores de site, os pacotes de idioma instalados recentemente poderão não estar disponíveis. Isso ocorre quando:
- O site executa a versão 1610 ou 1702.
- O console é atualizado no local usando ConsoleSetup.exe da pasta de instalação do servidor do site.

Quando esse problema ocorre, o console reinstalado não usa o conjunto de pacotes de idiomas mais recente que foi configurado. Nenhum erro é retornado, mas os pacotes de idiomas disponíveis para o console não serão alterados.  

**Solução alternativa:** desinstale o console atual e, em seguida, reinstale o console como uma nova instalação. Você pode usar ConsoleSetup.exe da pasta de instalação de servidores do site. Durante a instalação, selecione os arquivos de pacote de idiomas que você deseja usar.


### <a name="with-version-1702-the-default-site-boundary-group-is-configured-for-use-for-site-assignment"></a>Com a versão 1702, o grupo de limites do site padrão está configurado para uso para a atribuição de site
<!--  SMS 486380   Applicability should only be to 1702. -->
Com a versão 1702, a guia Referência dos grupos de limites de site padrão tem uma marcação para **Usar esse grupo de limites para atribuição de site**, lista o site como o **Site atribuído** e fica desabilitada para que a configuração não possa ser editada ou removida.

**Solução alternativa:** nenhuma. Você pode ignorar essa configuração. Embora o grupo esteja habilitado para atribuição de site, o grupo de limites de site padrão não é usado para atribuição de site. Com a 1702, essa configuração garante que o grupo de limites de site padrão esteja associado ao site correto.



### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>Ao instalar um site de Branch de Manutenção em Longo Prazo usando a versão 1606, um site do Branch Atual é instalado
<!-- Consider move to core content  -->
Quando você usar a mídia de linha de base da versão 1606 da versão de outubro de 2016 para instalar o site LTSB (Branch de Manutenção de Longo Prazo), a Instalação instala um site do Branch Atual em vez disso. Isso ocorre porque a opção de instalar um ponto de conexão de serviço com a instalação do site não está selecionada.

 - Embora um ponto de conexão de serviço não seja necessário, ele deve ser selecionado para instalar durante a Instalação para instalar um site LTSB.

Após a conclusão da instalação, você pode desinstalar o ponto de conexão de serviço.  No entanto, você deve ter um ponto de conexão de serviço no modo offline ou online para enviar dados de telemetria e obter atualizações de segurança para os sites do Branch Atual e LTSB.

Se seu site foi instalado como um site do Branch Atual, mas você queria instalar o LTSB, você pode desinstalar o site e reinstalá-lo. Como alternativa, você pode entrar em contato com a [Ajuda e Suporte da Microsoft](http://go.microsoft.com/fwlink/?LinkId=243064) para obter assistência.  

Para confirmar qual branch foi instalado, no console em **Administração** > **Configuração do Site** > **Sites**, abra **Configurações de Hierarquia**. A opção de converter o site em um site do Branch Atual está disponível apenas quando o site executa o LTSB.  

**Solução alternativa:**  não há.   



### <a name="the--sql-server-backup-model-in-use-by-configuration-manager-can-change-from-full-to-simple"></a>O modelo de backup do SQL Server em uso pelo Configuration Manager pode ser alterado de completo para simples  
<!-- Confirm applicability for upgrade to later baselines. 1511 is out of support. 1606 is minmum supported baseline  -->

 Quando você atualiza para System Center Configuration Manager versão 1511, o modelo de backup do SQL Server em uso pelo Configuration Manager pode mudar de completo para simples.  

-   Se você usar uma tarefa de backup personalizada do SQL Server com o modelo de backup completo (em vez da tarefa interna de backup para o Configuration Manager), a atualização poderá alterar o modelo de backup de completo para simples.  

**Solução alternativa**: após atualizar para a versão 1511, examine a configuração do SQL Server e restaure-o como completo, se necessário.  



### <a name="an-update-is-stuck-with-a-state-of-downloading-in-the-updates-and-servicing-node-of-the-configuration-manager-console"></a>Uma atualização está paralisada no estado Baixando no nó Atualizações e Manutenção do console do Configuration Manager  
<!-- Source bug pending. Consider move to core content.  -->
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
<!-- Source bug pending  -->

Ao executar a instalação de uma pasta CD.Latest criada para a versão 1606 e usar os arquivos redist incluídos com essa pasta CD.Latest, a Instalação falha com os seguintes erros no log de instalação do Configuration Manager:

  - ERRO: falha de verificação de hash do arquivo para defaultcategories.dll
  - ERRO: falha na verificação de manifesto. Versão errada do manifesto?

**Solução alternativa:**  use um dos seguintes:
 - Durante a instalação, opte por baixar os arquivos redist mais recentes da Microsoft para usar em vez dos incluídos na pasta CD.Latest.
 - Exclua manualmente a pasta *cd.latest\redist\languagepack\zhh* e execute a instalação novamente.

### <a name="service-connection-tool-throws-an-exception-when-sql-server-is-remote-or-when-shared-memory-is-disabled"></a>A ferramenta de conexão do serviço gera uma exceção quando o SQL Server é remoto ou quando a Memória Compartilhada está desabilitada
Começando da versão 1606, a ferramenta de conexão de serviço gera uma exceção quando uma das seguintes opções é verdadeira:  
 -    O banco de dados do site é remoto do computador que hospeda o ponto de conexão de serviço e usa uma porta não padrão (uma porta diferente de 1433)
 -     O banco de dados do site está no mesmo servidor que o ponto de conexão de serviço, mas o protocolo SQL **Memória Compartilhada** está desabilitado

A exceção é semelhante à seguinte:
 - *Exceção sem tratamento: System.Data.SqlClient.SqlException: Erro de rede ou específico à instância ao estabelecer conexão com o SQL Server. O servidor não foi encontrado ou não estava acessível. Verifique se o nome da instância está correto e se o SQL Server está configurado para permitir conexões remotas. (provedor: Provedor de Pipes Nomeados, erro: 40 – Não foi possível abrir uma conexão com o SQL Server) –*

**Solução alternativa**: durante o uso da ferramenta, você deve modificar o Registro do servidor que hospeda o ponto de conexão de serviço para incluir informações sobre a porta do SQL Server:

   1.    Antes de usar a ferramenta, edite a seguinte chave do Registro e adicione o número da porta que está sendo usado como o nome do SQL Server:
    - Chave: HKLM\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\
      - Valor: &lt;Nome do SQL Server>
    - Adicionar: **,&lt;PORTA>**

    Por exemplo, para adicionar a porta *15001* a um servidor denominado *testserver.test.net*, a chave resultante seria: ***HKLM\Software\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\testserver.test.net,15001***

   2.    Depois de adicionar a porta ao Registro, a ferramenta deve funcionar normalmente.  

   3.    Depois que o uso da ferramenta for concluído, para as etapas **-connect** e **-import**, altere a chave do Registro de volta para o valor original.  




<!-- No current Backup and Recovery relenotes
## Backup and recovery
-->


<!-- No current  Client deployment and upgrade relenotes
## Client deployment and upgrade  
-->



## <a name="operating-system-deployment"></a>Implantação de sistema operacional  

### <a name="issue-with-the-windows-adk-for-windows-10-version-1511"></a>Problema com o Windows ADK para Windows 10, versão 1511  
Ao executar uma sequência de tarefas no Centro de Software que usa uma imagem de inicialização do Windows PE v.10.0.10586 do Windows ADK 10, versão 1511, quando o computador é reiniciado no Windows PE, ele falhará ao “Inicializar dispositivos de hardware” com o erro: **Falha na inicialização do Windows PE com código de erro 0x80220014**  

**Solução alternativa**: usar o Windows 10 ADK original. Para mais informações, consulte o seguinte Blog da equipe do System Center Configuration Manager: [problema com o Windows ADK para Windows 10](http://blogs.technet.com/b/configmgrteam/archive/2015/11/20/issue-with-the-windows-adk-for-windows-10-version-1511.aspx)  

### <a name="dynamic-application-installation-fails-during-task-sequence-which-successfully-completes"></a>A instalação dinâmica de aplicativos falha durante a sequência de tarefas que é concluída com êxito  
Ao implantar uma sequência de tarefas que usa a opção **Instalar aplicativos de acordo com a lista de variáveis dinâmicas**e um dos aplicativos não é instalado por algum motivo, a sequência de tarefas será relatada com êxito. Isso ocorre independentemente de como você configura as seguintes opções:  

-   **Continuar se houver erro** (na guia Opções da etapa Instalar Aplicativo)  

-   **Se instalação de um aplicativo falhar, continue instalando outros aplicativos da lista** (na guia Propriedades da etapa Instalar Aplicativo)  

É possível exibir o smsts.log, para determinar se um aplicativo falhou ao ser instalado.  

**Solução alternativa**: use a variável **_TSAppInstallStatus** como uma condição nas etapas posteriores em uma sequência de tarefas com uma condição de falha da sequência de tarefas se ocorreu um erro com um dos aplicativos dinâmicos.  

### <a name="smb-might-not-work-properly-after-you-use-a-task-sequence-to-install-windows-10"></a>O SMB pode não funcionar corretamente depois que você usar uma sequência de tarefas para instalar o Windows 10  
Quando você usa uma sequência de tarefas para instalar uma imagem do Windows 10, o SMB pode não funcionar corretamente após a instalação do cliente do Configuration Manager. Por exemplo, as seguintes etapas da sequência de tarefas podem falhar:  

-   Restaurar Estado do Usuário quando usada com um ponto de migração de estado  

-   Conectar à Pasta de Rede  

Em um prompt de comando do administrador F8, você ainda pode executar PING no computador, por exemplo, mas qualquer tráfego de rede SMB (como NET USE no prompt de comando) pode falhar com o erro 1231 – o local de rede não pode ser alcançado.  

**Solução alternativa**:  
adicione uma etapa da sequência de tarefas Executar Linha de Comando após a etapa da sequência de tarefas Configurar Windows e ConfigMgr para interromper e, em seguida, inicie o serviço Estação de Trabalho da seguinte forma:    
**net stop workstation /y & net start workstation**  

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>Planos de manutenção criam muitos grupos e implantações de atualização de software duplicados por padrão  
Por padrão, o assistente para Criar Planos de Manutenção atualmente é executado depois de cada sincronização de atualizações de software. Toda vez que o assistente é executado, ele cria um novo grupo e implantação de atualização de software. Se você tiver um agendamento de sincronização de atualizações de software que é executado várias vezes ao dia, por exemplo, o assistente para Criar Planos de Manutenção criará vários, e provavelmente idênticos, grupos e implantações de atualização de software todos os dias.  

**Solução alternativa**:    
depois de criar um plano de manutenção, abra as propriedades do plano de manutenção, vá para a guia **Agendamento de Avaliação**, escolha **Executar a regra em um agendamento**, clique em **Personalizar** e crie um agendamento personalizado. Por exemplo, o plano de manutenção pode ser agendado para ser executado a cada 60 dias.  

### <a name="when-a-high-risk-deployment-dialog-is-visible-to-a-user-subsequent-high-risk-dialogs-with-a-sooner-deadline-are-not-displayed"></a>Quando uma caixa de diálogo de implantação de alto risco está visível para um usuário, as caixas de diálogo de alto risco subsequentes com uma data limite anterior não são exibidas
Depois de criar e implantar uma implantação de tarefas de alto risco para usuários, uma caixa de diálogo de alto risco é exibida ao usuário. Se o usuário não fechar a caixa de diálogo, você criará e implantará outra implantação de alto risco com uma data limite antes que a primeira, o usuário não receberá uma caixa de diálogo atualizada até que ele feche a caixa de diálogo original. As implantações ainda serão executadas nas datas limite configuradas.

**Solução alternativa**:  
O usuário deve fechar a caixa de diálogo para a primeira implantação de alto risco para ver a caixa de diálogo para a próxima implantação de alto risco.

## <a name="mobile-device-management"></a>Gerenciamento de dispositivos móveis  

### <a name="cannot-create-an-enrollment-profile-on-a-primary-site"></a>Não é possível criar um perfil de registro em um site primário  
Um administrador não pode criar um perfil de registro no console de administração do System Center Configuration Manager que se conecta a um site primário. Ao tentar se registrar, o administrador verá o erro: “O token de DEP não foi atualizado. Carregue um token de DEP” no assistente de perfil de registro. Esse erro ocorre apesar de um token de DEP válido ter sido carregado no site de administração central.  

**Solução alternativa**: criar um perfil de registro no console do System Center Configuration Manager que se conecta ao site de administração central.  

### <a name="dep-cannot-use-non-alpha-numeric-characters-in-enrollment-profiles"></a>O DEP não pode usar caracteres não alfanuméricos em perfis de registro  
Perfis de registro associados ao DEP (Perfil de Registro do Dispositivo Móvel) da Apple não podem usar caracteres não alfanuméricos nos campos **Nome**, **Descrição**, **Departamento** e **Telefone** para o perfil de registro quando o DEP está habilitado. Usar caracteres não alfanuméricos nesses campos criará um perfil de registro, mas o perfil não poderá ser carregado para a Apple. Nenhuma mensagem de erro ou aviso é fornecido pelo servidor da Apple e os perfis não serão implantados em dispositivos gerenciados pelo DEP.  

**Solução alternativa**: nenhuma.

### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram"></a>O apagamento completo desabilita dispositivos Windows 10 com menos de 4 GB de RAM

Executar um apagamento completo em dispositivos Windows 10 RTM (versões anteriores à versão 1511) com menos de 4 GB de RAM pode tornar o dispositivo inutilizável. Após tentar apagar o dispositivo, não é possível iniciá-lo e ele não responde.

**Solução alternativa**: certifique-se de que PCs com Windows 10 RTM tenham pelo menos 4 GB de RAM disponível antes de executar um apagamento completo do dispositivo. Para exibir o número de versão de dispositivos Windows 10, digite "winver" em um prompt de comando. Se o dispositivo já tiver sido apagado e não estiver mais respondendo, use uma unidade Windows 10 USB inicializável para iniciar e recuperar o acesso ao dispositivo.

### <a name="when-a-user-belongs-to-two-or-more-user-collections-that-a-terms-and-conditions-policy-is-deployed-to-the-user-sees-multiple-sets-of-the-same-terms"></a>Quando um usuário pertencer a duas ou mais coleções de usuários às quais uma política de termos e condições é implantada, o usuário vê vários conjuntos dos mesmos termos  

Quando um administrador implantar um conjunto de termos em várias coleções de usuários, e um usuário for membro de mais de uma dessas coleções, esse usuário terá várias cópias apresentadas de termos idênticos ao abrir o Portal da Empresa.  Por exemplo, se um usuário chamado “SampleUser” for membro de duas coleções de usuários diferentes, uma chamada “CompanyEmployeesFTE” e “CompanyEmployeesNA”, e os termos e condições chamados “CompanyTerms” forem implantados em CompanyEmployeesFTE e CompanyEmployeesNA, SampleUser verá dois conjuntos idênticos de CompanyTerms na página de aceitação dos termos. Visto que os usuários só podem aceitar ou recusar todos os termos, não há nenhum risco de haver um estado de aceitação ambíguo (no qual o usuário tenha aceitado e rejeitado os termos ao mesmo tempo). O relatório de aceitação dos Termos e Condições incluirá apenas uma linha para cada conjunto de termos para cada usuário. Portanto, não há nenhum erro no relatório. O único efeito é que o usuário verá dois conjuntos de termos na página de aceitação.  

**Solução alternativa**: certifique-se de que cada usuário está incluído somente em uma coleção à qual os termos foram implantados.  

### <a name="android-for-work-email-profiles-that-use-certificate-authentication-are-not-applied-to-devices"></a>Perfis de email do Android for Work que usam a autenticação de certificado não são aplicados aos dispositivos
<!--  487657 -->
Quando um perfil de email do Android for Work for criado, haverá duas opções para autenticação. Um é o nome de usuário e senha, o outro são certificados. Neste momento, a opção de certificados não está funcionando. Se o perfil for criado com o método de autenticação definido como **certificados**, o perfil não será aplicado ao dispositivo, e o usuário receberá uma solicitação para inserir manualmente os detalhes da conta de email.

**SOLUÇÃO ALTERNATIVA**: nenhuma. Os administradores devem usar a opção de **nome de usuário e senha**, ou aguarde até que este problema tenha sido resolvido.

## <a name="reports-and-monitoring"></a>Relatórios e monitoramento  

### <a name="the-health-attestation-report-is-empty-even-though-health-attestation-data-was-previously-collected"></a>O Relatório de Atestado de Integridade está vazio, embora os dados de atestado de integridade tenham sido previamente coletados  
Quando um usuário administrativo com uma função de segurança que inclui a permissão **Leitura** para o grupo de permissão **Atestado de Integridade** exibir o relatório de Atestado de Integridade, o relatório estará vazio e não exibirá os dados. Isso ocorre porque as permissões para exibir dados no relatório de Atestado de Integridade são vinculados ao grupo de permissão **Afinidade de Dispositivo de Usuário**, em vez do grupo de permissão Atestado de Integridade.  

Esse problema afeta o System Center Configuration Manager com a atualização 1602 e deve ser resolvido em uma atualização futura.  

**Solução alternativa**: atribua ao usuário administrativo um grupo de segurança que inclua a permissão **Leitura** para o grupo de permissão **Afinidades de Dispositivo de Usuário**.  

### <a name="conditional-access"></a>Acesso condicional  

#### <a name="the-same-user-collection-is-not-blocked-from-being-added-to-both-exempted-and-targeted-collections"></a>A mesma coleção de usuários não é impedida de ser adicionada às Coleções Isenta e de Destino.  
Isso acontece apenas quando você adiciona a mesma **Coleção de Usuário** à página **Coleção Isenta** **antes** de adicioná-la à página **Coleção de Destino**.  Se você adicionar primeiro uma **Coleção de Usuário** à página **Coleções de Destino** e, em seguida, tentar adicionar a mesma **Coleção de Usuário** à página **Coleção Isenta**, você deverá ver a mensagem normal de bloqueio.  

Esse problema afeta o acesso condicional do System Center Configuration Manager para o **Exchange no Local** com a atualização 1602 e deve ser resolvido em uma atualização futura.  

**Solução alternativa:** adicione a **Coleção de Usuário** à página **Coleções de Destino** antes de escolher **Coleção de Usuário** na página **Coleção Isenta** ou verifique se você não está adicionando a mesma **Coleção de Usuário** às Coleções Isenta e de Destino.

## <a name="endpoint-protection"></a>Endpoint Protection
<!--  Product Studio bug 485370 added by Nathbarn 04 19 2017 -->
### <a name="antimalware-policy-fails-to-apply-on-windows-server-2016-core"></a>A política de antimalware não se aplica no Windows Server 2016 Core
A política de antimalware não se aplica no Windows Server 2016 Core.  O código de erro é 0x80070002.  Há uma dependência ausente para ConfigSecurityPolicy.exe.

**Solução alternativa:**  não há.  Como administrador, você pode usar a política de grupos para gerenciar as configurações do Windows Server 2016 Core.

