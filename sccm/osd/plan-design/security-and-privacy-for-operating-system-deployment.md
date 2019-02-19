---
title: Segurança e privacidade para implantação do sistema operacional
titleSuffix: Configuration Manager
description: Saiba sobre as práticas recomendadas de segurança e privacidade para a implantação de sistema operacional no Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 5ee5928f-3d72-4b00-8156-1e0d1030a96c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8ad92f3857c1303bf3f4a7c171b0de98f75e56ee
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56135163"
---
# <a name="security-and-privacy-for-os-deployment-in-configuration-manager"></a>Segurança e privacidade para implantação de sistema operacional no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo contém informações de segurança e privacidade para o recurso de implantação de sistema operacional no Configuration Manager.  



##  <a name="bkmk_security"></a> Práticas recomendadas de segurança para implantação de sistema operacional  

 Use as práticas recomendadas de segurança a seguir para quando você implantar sistemas operacionais com o Configuration Manager:  


### <a name="implement-access-controls-to-protect-bootable-media"></a>Implementar controles de acesso para proteger a mídia inicializável

 Ao criar uma mídia inicializável, sempre atribua uma senha para ajudar a proteger a mídia. Mesmo com uma senha, ele somente criptografa os arquivos que contêm informações confidenciais e todos os arquivos pode ser substituídos.  

 Controle o acesso físico à mídia para impedir que um invasor use ataques de criptografia para obter o certificado de autenticação de cliente.  

 Para ajudar a impedir que um cliente instale algum conteúdo ou alguma política do cliente que foi violada, o conteúdo contém um hash e deve ser usado com a política original. Se o hash de conteúdo falhar ou a verificação do conteúdo corresponder à política, o cliente não usará a mídia inicializável. Somente o conteúdo é transformado em hash. A política não é transformada em hash, mas ela é criptografada e protegida quando você especifica uma senha. Esse comportamento torna mais difícil para um invasor modificar com êxito a política.  


### <a name="use-a-secure-location-when-you-create-media-for-os-images"></a>Usar uma localização segura ao criar mídia para imagens do sistema operacional

 Se usuários não autorizados tiverem acesso à localização, eles poderão violar os arquivos criados por você. Eles também poderão usar todo o espaço em disco disponível, resultando em falha na criação de mídia.  


### <a name="protect-certificate-files"></a>Proteger os arquivos de certificado 

 Proteger arquivos de certificado (.pfx) com uma senha forte. Se você armazena-os na rede, proteja o canal de rede ao importá-los para o Configuration Manager

 Quando você requer uma senha para importar o certificado de autenticação de cliente que você usa para a mídia inicializável, essa configuração ajuda a proteger o certificado de um invasor.  

 Use a assinatura SMB ou o IPsec entre o local de rede e o servidor de site para impedir que um invasor viole o arquivo de certificado.  


### <a name="block-or-revoke-any-compromised-certificates"></a>Bloquear ou revogar todos os certificados comprometidos 

 Se o certificado do cliente estiver comprometido, bloqueie o certificado do Configuration Manager. Se for um certificado PKI, revogue-o.  

 Para implantar um sistema operacional usando a mídia inicializável e a inicialização PXE, você deve ter um certificado de autenticação de cliente com uma chave privada. Se esse certificado estiver comprometido, bloqueie-o no nó **Certificados** no workspace **Administração**, no nó **Segurança**.  


### <a name="secure-the-communication-channel-between-the-site-server-and-the-sms-provider"></a>Proteja o canal de comunicação entre o servidor de site e o Provedor de SMS

 Quando o Provedor de SMS está é remoto do servidor do site, proteja o canal de comunicação para proteger imagens de inicialização.

 Quando você modifica imagens de inicialização e o Provedor de SMS é executado em um servidor que não é o servidor do site, as imagens de inicialização estão vulneráveis a ataque. Proteja o canal de rede entre esses computadores usando a assinatura SMB ou IPsec.  


### <a name="enable-distribution-points-for-pxe-client-communication-only-on-secure-network-segments"></a>Habilitar pontos de distribuição para comunicação do cliente PXE apenas em segmentos de rede segura

Quando um cliente enviar uma solicitação de inicialização PXE, você não tem como verificar se a solicitação é atendida por um ponto de distribuição válido habilitado para PXE. Esse cenário tem os seguintes riscos de segurança:  

 - Um ponto de distribuição não autorizado que responde às solicitações de PXE pode fornecer uma imagem violada aos clientes.  

 - Um invasor pode iniciar um ataque de intermediário contra o protocolo TFTP que é usado pelo PXE. Esse ataque pode enviar um código mal-intencionado com os arquivos de sistema operacional. O invasor também pode criar um cliente invasor para fazer solicitações do TFTP diretamente ao ponto de distribuição.  

 - Um invasor pode usar um cliente mal-intencionado para iniciar um ataque de negação de serviço contra o ponto de distribuição.  

Use proteção abrangente para proteger os segmentos de rede em que os clientes acessam pontos de distribuição habilitados para PXE.  

> [!WARNING]  
>  Por conta desses riscos de segurança, não habilite um ponto de distribuição para comunicação PXE quando ele estiver em uma rede não confiável, como uma rede de perímetro.  


### <a name="configure-pxe-enabled-distribution-points-to-respond-to-pxe-requests-only-on-specified-network-interfaces"></a>Configurar pontos de distribuição habilitados para PXE para responder às solicitações de PXE somente em interfaces de rede especificadas  

 Se você permitir que o ponto de distribuição responda às solicitações de PXE em todas as interfaces de rede, essa configuração pode expor o serviço PXE a redes não confiáveis.  


### <a name="require-a-password-to-pxe-boot"></a>Exigir uma senha para a inicialização PXE

 Quando você exige uma senha para a inicialização PXE, essa configuração adiciona um nível extra de segurança ao processo de inicialização PXE. Essa configuração ajuda a proteger contra ingresso de clientes invasores na hierarquia do Configuration Manager.  


### <a name="restrict-content-in-os-images-used-for-pxe-boot-or-multicast"></a>Restringir o conteúdo em imagens do sistema operacional usadas para inicialização PXE ou multicast

 Não incluir aplicativos de linha de negócios ou software que contenha dados confidenciais em uma imagem que você usa para inicialização PXE ou multicast.  

 Por conta dos riscos de segurança inerentes envolvidos com a inicialização PXE e multicast, reduza os riscos se um computador invasor baixar a imagem do sistema operacional.  


### <a name="restrict-content-installed-by-task-sequence-variables"></a>Restringir o conteúdo instalado por variáveis de sequência de tarefas

 Não inclua aplicativos de linha de negócios ou software que contenha dados confidenciais em pacotes de aplicativos instalados por você usando variáveis de sequências de tarefas.  

 Quando você implanta software usando variáveis de sequências de tarefas, ele pode ser instalado em computadores e usuários que não estão autorizados a receber esse software.  


### <a name="secure-the-network-channel-when-migrating-user-state"></a>Proteger o canal de rede durante a migração de estado do usuário

 Quando você migrar o estado do usuário, proteja o canal de rede entre o cliente e o ponto de migração do estado usando assinatura SMB ou IPsec.  

 Após a conexão inicial sobre HTTP, os dados de migração de estado do usuário serão transferidos usando SMB. Se você não proteger o canal de rede, um invasor poderá ler e modificar esses dados.  


### <a name="use-the-latest-version-of-usmt"></a>Use a versão mais recente do USMT

 Use a versão mais recente da USMT (Ferramenta de Migração do Usuário) à qual o Configuration Manager dá suporte.  

 A versão mais recente da USMT fornece aprimoramentos de segurança e mais controle para quando você migrar dados de estado do usuário.  


### <a name="manually-delete-folders-on-state-migration-points-when-you-decommission-them"></a>Excluir manualmente as pastas no ponto de migração de estado ao encerrá-las  

 Quando você remove uma pasta do ponto de migração de estado no console do Configuration Manager nas propriedades do ponto de migração de estado, o site não exclui a pasta física. Para proteger os dados de migração de estado contra divulgação de informações, remova manualmente o compartilhamento de rede e exclua a pasta.  


### <a name="dont-configure-the-deletion-policy-to-immediately-delete-user-state"></a>Não configurar a política de exclusão para excluir imediatamente o estado do usuário  

 Se você configurar a política de exclusão no ponto de migração de estado para remover dados marcados para exclusão imediatamente e se um invasor recuperar os dados de estado do usuário antes que o computador válido, o site excluirá imediatamente os dados de estado do usuário. Defina o intervalo **Excluir depois** para que seja longo o suficiente para verificar a restauração com êxito dos dados de estado do usuário.  


### <a name="manually-delete-computer-associations"></a>Excluir manualmente as associações de computador 

 Exclua manualmente as associações de computador quando a restauração de dados de migração de estado do usuário for concluída e verificada.

 O Configuration Manager não remove automaticamente as associações de computador. Ajude a proteger a identidade dos dados de estado do usuário excluindo manualmente associações de computador que não são mais necessárias.  


### <a name="manually-back-up-the-user-state-migration-data-on-the-state-migration-point"></a>Fazer backup dos dados de migração de estado do usuário manualmente no ponto de migração de estado  

 O Backup do Configuration Manager não inclui os dados de migração de estado do usuário no backup do site.  


### <a name="implement-access-controls-to-protect-the-prestaged-media"></a>Implementar controles de acesso para proteger a mídia em pré-teste  

 Controle o acesso físico à mídia para impedir que um invasor use ataques de criptografia para obter o certificado de autenticação de cliente e dados confidenciais.  


### <a name="implement-access-controls-to-protect-the-reference-computer-imaging-process"></a>Implementar controles de acesso para proteger o processo de geração de imagens do computador de referência  

 Verifique se o computador de referência que você usa para capturar imagens do sistema operacional está em um ambiente seguro. Use controles de acesso apropriados para que software inesperado ou mal-intencionado não possa ser instalado e incluído inadvertidamente na imagem capturada. Ao capturar a imagem, verifique se a localização de rede de destino é segura. Esse processo ajuda a assegurar que a imagem não possa ser violada depois que você capturá-la.  


### <a name="always-install-the-most-recent-security-updates-on-the-reference-computer"></a>Sempre instalar as atualizações de segurança mais recentes no computador de referência  

 Quando o computador de referência tem atualizações de segurança, ele ajuda a reduzir a janela de vulnerabilidade para novos computadores quando são inicializados pela primeira vez.  


### <a name="implement-access-controls-when-deploying-an-os-to-an-unknown-computer"></a>Implementar controles de acesso ao implantar um sistema operacional em um computador desconhecido

 Se você tiver de implantar um sistema operacional em um computador desconhecido, implemente controles de acesso para impedir que computadores não autorizados se conectem à rede.  

 O provisionamento de computadores desconhecidos fornece um método conveniente para implantar novos computadores sob demanda. Mas ele também pode permitir que um invasor se torne um cliente confiável na sua rede. Restrinja o acesso físico à rede e monitore os clientes para detectar computadores não autorizados. 

 Computadores respondendo a uma implantação de sistema operacional iniciadas pelo PXE podem ter todos os dados destruídos durante o processo. Esse comportamento pode resultar em perda de disponibilidade de sistemas reformatados inadvertidamente.  


### <a name="enable-encryption-for-multicast-packages"></a>Habilitar a criptografia de pacotes multicast  

 Para cada pacote de implantação de sistema operacional, você pode habilitar a criptografia quando o Configuration Manager transfere o pacote usando multicast. Essa configuração ajuda a impedir que computadores invasores ingressem na sessão multicast. Ele também ajuda a impedir que invasores violem a transmissão.  


### <a name="monitor-for-unauthorized-multicast-enabled-distribution-points"></a>Monitorar pontos de distribuição não autorizados habilitados para multicast  

 Se os invasores puderem ter acesso à rede, eles poderão configurar servidores multicast invasores para falsificar a implantação de sistema operacional.  


### <a name="when-you-export-task-sequences-to-a-network-location-secure-the-location-and-secure-the-network-channel"></a>Quando você exporta sequências de tarefas para um local de rede, proteja o local e o canal de rede

 Restrinja quem pode acessar a pasta de rede.  

 Use a assinatura SMB ou o IPsec entre o local de rede e o servidor do site para impedir que um invasor viole a sequência de tarefas exportada.  


### <a name="if-you-use-the-task-sequence-run-as-account-take-additional-security-precautions"></a>Se você usar a Execução de Sequência de Tarefas como Conta, tome precauções de segurança adicionais

 Se você usar a [execução de sequência de tarefas como conta](/sccm/core/plan-design/hierarchy/accounts#task-sequence-run-as-account), siga as etapas de precaução a seguir:  

 - Use uma conta com o mínimo possível de permissões.  

 - Não use a conta de acesso à rede para essa conta.  

 - Nunca faça da conta um administrador de domínio.  

 - Nunca configure perfis móveis para esta conta. Quando a sequência de tarefas for executada, ela baixará o perfil móvel da conta, o que deixará o perfil vulnerável a acesso no computador local.  

 - Limite o escopo da conta. Por exemplo, crie outra sequência de tarefas executada como contas para cada sequência de tarefas. Se uma conta for comprometida, somente os computadores cliente aos quais a conta tem acesso serão comprometidos. Se a linha de comando exigir acesso administrativo no computador, considere a criação de uma conta do administrador local exclusivamente para execução de sequência de tarefas como conta. Crie essa conta local em todos os computadores que executam a sequência de tarefas e exclua a conta assim que ela não for mais necessária.  


### <a name="restrict-and-monitor-the-administrative-users-who-are-granted-the-os-deployment-manager-security-role"></a>Restrinja e monitore os usuários administrativos que recebem a função de segurança do gerenciador de implantação de sistema operacional

 Os usuários administrativos a quem a **função de segurança do Gerenciador de Implantação de Sistema Operacional** é concedida podem criar certificados autoassinados. Esses certificados podem então ser usados para representar um cliente e obter a política do cliente do Configuration Manager.  


### <a name="use-enhanced-http-to-reduce-the-need-for-a-network-access-account"></a>Usar HTTP aprimorado para reduzir a necessidade de uma conta de acesso de rede

Começando na versão 1806, quando você habilita o [HTTP aprimorado](/sccm/core/plan-design/hierarchy/enhanced-http), vários cenários de implantação de sistema operacional não exigem uma conta de acesso de rede para baixar conteúdo de um ponto de distribuição. Para obter mais informações, confira [Sequências de tarefas e a conta de acesso à rede](/sccm/osd/plan-design/planning-considerations-for-automating-tasks#BKMK_TSNetworkAccessAccount).<!--1358278--> 



## <a name="security-issues-for-os-deployment"></a>Problemas de segurança para implantação do sistema operacional  

 Embora a implantação de sistema operacional possa ser uma forma conveniente de implantar os sistemas operacionais e as configurações mais seguras para computadores em sua rede, ela tem os seguintes riscos de segurança:  


### <a name="information-disclosure-and-denial-of-service"></a>Divulgação de informações e negação de serviço  

 Se um invasor tiver controle da sua infraestrutura do Configuration Manager, ele poderá executar qualquer sequência de tarefas. Esse processo pode incluir a formatação dos discos rígidos de todos os computadores cliente. As sequências de tarefas podem ser configuradas para conter informações confidenciais, como contas que têm permissões para ingressar no domínio e nas chaves de licenciamento por volume.  


### <a name="impersonation-and-elevation-of-privileges"></a>Representação e elevação de privilégios  

 As sequências de tarefas podem ingressar em um computador para o domínio, o que pode fornecer a um computador não autorizado acesso autenticado à rede. 

 Proteja o certificado de autenticação de cliente que é usado para mídia de sequência de tarefas inicializável e para implantação de inicialização PXE. Quando você captura um certificado de autenticação de cliente, esse processo permite que um invasor tenha a oportunidade de obter a chave privada no certificado. Esse certificado permite representar um cliente válido na rede. Nesse cenário, o computador não autorizado pode baixar a política, que pode conter dados confidenciais.  

 Se os clientes usam a conta de acesso de rede para acessar os dados armazenados no ponto de migração de estado, esses clientes compartilham efetivamente a mesma identidade. Eles poderiam acessar os dados de migração de estado de outro cliente que usa a conta de acesso de rede. Os dados são criptografados para que somente o cliente original possa lê-los, mas os dados podem ser violados ou excluídos.  


### <a name="client-authentication-to-the-state-migration-point-is-achieved-by-using-a-configuration-manager-token-that-is-issued-by-the-management-point"></a>A autenticação do cliente no ponto de migração de estado é obtida usando um token do Configuration Manager emitido pelo ponto de gerenciamento.  

 O Configuration Manager não limita nem gerencia a quantidade de dados que são armazenados no ponto de migração de estado. Um invasor pode preencher o espaço em disco disponível e causar uma negação de serviço.  


### <a name="if-you-use-collection-variables-local-administrators-can-read-potentially-sensitive-information"></a>Se você usar variáveis da coleção, os administradores locais poderão ler as informações potencialmente confidenciais  

 Embora as variáveis da coleção ofereçam um método flexível para implantar sistemas operacionais, esse recurso pode resultar em divulgação de informações confidenciais.  



##  <a name="bkmk_privacy"></a> Informações de privacidade para implantação de sistema operacional  

 Além de implantar um sistema operacional em computadores que não tenham nenhum, o Configuration Manager pode ser usado para migrar arquivos e configurações de usuários de um computador para outro. O administrador configura quais informações transferir, incluindo arquivos de dados pessoais, configurações e cookies do navegador.  

 O Configuration Manager armazena as informações em um ponto de migração de estado e as criptografa durante a transmissão e o armazenamento. Somente o novo computador associado às informações de estado pode recuperar as informações armazenadas. Se o novo computador perder a chave para recuperar as informações, um administrador do Configuration Manager com o direito para **Exibir Informações de Recuperação** em objetos de instância da associação do computador poderá acessar as informações e associá-las a um novo computador. Depois que o novo computador restaura as informações de estado, por padrão ele exclui os dados depois de um dia. A configuração pode ser feita quando o ponto de migração de estado remove os dados marcados para exclusão. O Configuration Manager não armazena as informações de migração de estado do banco de dados do site e não as envia à Microsoft.  

 Se você usar a mídia de inicialização para implantar as imagens do sistema operacional, sempre use a opção padrão para proteger por senha a mídia de inicialização. A senha criptografa quaisquer variáveis armazenadas na sequência de tarefas, mas as informações não armazenadas em uma variável podem estar vulneráveis à divulgação.  

 A implantação de sistema operacional pode usar as sequências de tarefas para executar muitas tarefas diferentes durante o processo de implantação, inclusive a instalação de aplicativos e atualizações de software. Ao configurar as sequências de tarefas, você deve estar ciente das implicações de privacidade da instalação de software.  

 O Configuration Manager não implementa a implantação de sistema operacional por padrão. Diversas etapas de configuração são exigidas antes de você coletar informações do estado do usuário ou criar sequências de tarefas ou imagens de inicialização.  

 Antes de configurar a implantação do sistema operacional, considere seus requisitos de privacidade.  



## <a name="see-also"></a>Consulte também

[Dados de diagnóstico e de uso](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)

[Segurança e privacidade do Configuration Manager](/sccm/core/plan-design/security/security-and-privacy)
