---
title: "Privacidade de segurança do controle remoto | Microsoft Docs"
description: "Obtenha as informações de segurança e privacidade de controle remoto no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 272ee86b-d3d9-4fd9-b5c4-73e490e1a1e4
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 342a58d2b7439f721381beb43188594b5278043d


---
# <a name="security-and-privacy-for-remote-control-in-system-center-configuration-manager"></a>Segurança e privacidade do controle remoto no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico contém as informações de segurança e privacidade de controle remoto no System Center 2012 Configuration Manager.  

##  <a name="a-namebkmksecurityhardwareinventorya-security-best-practices-for-remote-control"></a><a name="BKMK_Security_HardwareInventory"></a> Práticas recomendadas de segurança para o controle remoto  
 Use as práticas recomendadas de segurança a seguir ao gerenciar computadores cliente usando o controle remoto.  

|Prática recomendada de segurança|Mais informações|  
|----------------------------|----------------------|  
|Ao se conectar a um computador remoto, não continue se NTLM for usado em vez da autenticação Kerberos.|Quando o Configuration Manager detectar que a sessão de controle remoto é autenticada pelo NTLM em vez do Kerberos, você verá um prompt que avisa que a identidade do computador remoto não pode ser verificada. Não continue com a sessão de controle remoto. A autenticação NTLM é um protocolo de autenticação mais fraco do que o Kerberos e é vulnerável à reprodução e à representação.|  
|Não habilite o compartilhamento da Área de transferência no visualizador do controle remoto.|A Área de Transferência dá suporte a objetos como arquivos executáveis e texto e pode ser usada pelo usuário no computador host durante a sessão de controle remoto para executar um programa no computador de origem.|  
|Não digite senhas de contas com privilégios ao administrar remotamente um computador.|O software que observa a entrada do teclado pode capturar a senha. Ou então, se o programa que está sendo executado no computador cliente não for o programa do qual o usuário do controle remoto assume o controle, o programa poderá estar capturando a senha. Quando são necessárias contas e senhas, o usuário final deve inseri-las.|  
|Bloqueie o teclado e o mouse durante uma sessão de controle remoto.|Se o Configuration Manager detectar que a conexão de controle remoto foi encerrada, ele bloqueará automaticamente o teclado e o mouse para que um usuário não possa assumir o controle da sessão de controle remoto aberta. No entanto, essa detecção pode não ocorrer imediatamente e não ocorrerá se o serviço de controle remoto for encerrado.<br /><br /> Selecione a ação **Bloquear Teclado e Mouse Remotos** na janela **Controle Remoto do ConfigMgr** .|  
|Não permita que os usuários definam as configurações de controle remoto no Centro de Software.|Não habilite a configuração do cliente **Os usuários podem alterar as configurações de política ou de notificação no Centro de Software** para ajudar a impedir que os usuários sejam espionados.<br /><br /> Essa configuração destina-se ao computador e não ao usuário conectado.|  
|Habilite o perfil do Firewall do Windows do **Domínio** .|Habilite a configuração do cliente **Habilitar controle remoto em perfis de exceção de Firewall de clientes** e selecione o Firewall do Windows do **Domínio** para os computadores da intranet.|  
|Se você fizer logout durante uma sessão de controle remoto e fizer logon como um usuário diferente, certifique-se de fazer logout antes de se desconectar da sessão de controle remoto.|Se você não fizer logout nesse cenário, a sessão permanecerá aberta.|  
|Não forneça aos usuários direitos de administrador local.|Quando você concede aos usuários direitos de administrador local, eles poderão assumir sua sessão de controle remoto ou comprometer suas credenciais.|  
|Use a Política de Grupo ou o Configuration Manager para definir as configurações de Assistência Remota, mas não ambos.|Você pode usar o Configuration Manager e a Política de Grupo para fazer alterações de configuração nas configurações da Assistência Remota. Quando a Política de Grupo é atualizada no cliente, por padrão, ele otimiza o processo alterando apenas as políticas que foram alteradas no servidor. O Configuration Manager altera as configurações na política de segurança local, que não poderão ser substituídas a menos que a atualização da Política de Grupo seja forçada.<br /><br /> A configuração da política nos dois locais pode levar a resultados inconsistentes. Escolha um dos métodos a seguir para definir as configurações de Assistência Remota.|  
|Habilite a configuração do cliente **Solicitar ao usuário a permissão de Controle Remoto**.|Embora haja maneiras de contornar esta configuração de cliente que solicita ao usuário a confirmação de uma sessão de controle remoto, habilite essa configuração para reduzir a possibilidade de espionagem dos usuários enquanto estiverem trabalhando em tarefas confidenciais.<br /><br /> Além disso, instrua os usuários a verificar o nome da conta que é exibido durante a sessão de controle remoto e a se desconectarem da sessão se suspeitarem que a conta não é autorizada.|  
|Limite a lista de Visualizadores Permitidos.|Os direitos de administrador local não são necessários para que um usuário possa usar o controle remoto.|  

### <a name="security-issues-for-remote-control"></a>Problemas de segurança para o controle remoto  
 O gerenciamento de computadores cliente usando o controle remoto apresenta os seguintes problemas de segurança:  

-   Não considere confiáveis as mensagens de auditoria do controle remoto.  

     Se você iniciar uma sessão de controle remoto e depois fizer logon usando credenciais alternativas, a conta original enviará as mensagens de auditoria, e não a conta que usou as credenciais alternativas.  

     As mensagens de auditoria não serão enviadas se você copiar os arquivos binários para o controle remoto em vez de instalar o console do Configuration Manager e depois executar o controle remoto no prompt de comando.  

##  <a name="a-namebkmkprivacyhardwareinventorya-privacy-information-for-remote-control"></a><a name="BKMK_Privacy_HardwareInventory"></a> Informações sobre privacidade para o controle remoto  
 O controle remoto permite exibir sessões ativas nos computadores cliente do Configuration Manager e potencialmente exibir quaisquer informações armazenadas nesses computadores. Por padrão, o controle remoto não está habilitado.  

 Embora você possa configurar o controle remoto para fornecer um aviso destacado e obter o consentimento de um usuário antes do início de uma sessão de controle remoto, ele também pode monitorar os usuários sem a permissão ou o conhecimento deles. Você pode configurar o nível de acesso Somente Exibição para que nada possa ser alterado no controle remoto, ou Controle Total. A conta do administrador que está estabelecendo a conexão é exibida na sessão de controle remoto, para ajudar os usuários a identificar quem está se conectando ao computador deles.  

 Por padrão, o Configuration Manager concede permissões de Controle Remoto ao grupo local de Administradores.  

 Antes de configurar o controle remoto, considere seus requisitos de privacidade.  



<!--HONumber=Dec16_HO3-->


