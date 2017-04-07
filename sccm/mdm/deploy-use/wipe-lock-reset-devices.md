---
title: "Proteja seus dados com apagamento, bloqueio ou redefinição de senha remotos usando o System Center Configuration Manager | Microsoft Docs"
description: "Proteja os dados do dispositivo com apagamento completo, apagamento seletivo, bloqueio remoto ou redefinição de senha usando o System Center Configuration Manager."
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 770da7bd-02dd-474a-9604-93ff1ea0c1e4
caps.latest.revision: 18
caps.handback.revision: 0
author: nathbarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: ef020a0409c1f1a68f76ecadc9885801e6c1ad4e
ms.lasthandoff: 03/27/2017

---
# <a name="protect-data-with-remote-wipe-lock-or-passcode-reset-using-system-center-configuration-manager"></a>Protege seus dados com apagamento, bloqueio ou redefinição de senha remotos usando o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Configuration Manager fornece recursos de apagamento seletivo, apagamento completo, bloqueio remoto e redefinição de senha. Os dispositivos móveis podem armazenar dados corporativos confidenciais e fornecer acesso a muitos recursos corporativos. Para proteger os dispositivos você pode emitir:  

-   Um apagamento completo para restaurar as configurações de fábrica do dispositivo.  

-   Um apagamento seletivo para remover somente os dados da empresa.  

-   Um bloqueio remoto para ajudar a proteger um dispositivo que pode estar perdido.  

-   Redefinir a senha do dispositivo.  

##  <a name="full-wipe"></a>apagamento completo  
 Você pode emitir um comando de apagamento para um dispositivo quando precisar proteger um dispositivo perdido ou quando desativar um dispositivo de seu uso ativo.  

 Emita um **apagamento completo** para um dispositivo para restaurá-lo às suas configurações de fábrica. Isso remove todos os dados da empresa e do usuário e configurações.  É possível fazer um apagamento completo em dispositivos Windows Phone, iOS, Android e Windows 10.  

> [!NOTE]
> Apagar dispositivos Windows 10 em versões anteriores à versão 1511 com menos de 4 GB de RAM pode deixar o dispositivo sem resposta. [Saiba mais.](https://technet.microsoft.com/library/mt592024.aspx#full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram)

### <a name="to-initiate-a-remote-wipe-from-the-configuration-manager-console"></a>Para iniciar um apagamento remoto no console do Configuration Manager  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** e selecione **Dispositivos**. Como alternativa, é possível clicar em **Coleções de Dispositivos** e selecionar uma coleção.  

2.  Selecione o dispositivo que deseja desativar/apagar.  

3.  Clique em **Ações de Dispositivo Remoto** no **Grupo de Dispositivos**e selecione **Desativar/Apagar**.  

## <a name="selective-wipe"></a>apagamento seletivo  
 Emita um **apagamento seletivo** para um dispositivo para remover apenas os dados da empresa. A tabela a seguir descreve por plataforma qual dado foi removido e o efeito nos dados que permaneceram no dispositivo após o apagamento seletivo.  

 **iOS**  

|Conteúdo removido ao desativar um dispositivo|iOS|  
|--------------------------------------------|---------|  
|Aplicativos da empresa e dados associados instalados usando o Configuration Manager e o Intune.|Aplicativos são desinstalados. Dados de aplicativo da empresa são removidos.|  
|Perfis VPN e Wi-Fi|Removidos.|  
|Certificados|Removidos e revogados.|  
|Configurações|Removidos, exceto para: **Permitir roaming de voz**, **Permitir roaming de dados** e **Permitir sincronização automática durante roaming**.|  
|Agente de gerenciamento|O perfil de gerenciamento é removido.|  
|Perfis de email|Para perfis de email provisionados pelo Intune, a conta de email e o email são removidos.|  

 **Android e Android Samsung KNOX Standard**  

|Conteúdo removido ao desativar um dispositivo|Android|Samsung KNOX Standard|  
|--------------------------------------------|-------------|------------------|  
|Aplicativos da empresa e dados associados instalados usando o Configuration Manager e o Intune.|Aplicativos e dados permanecem instalados.|Aplicativos são desinstalados.|  
|Perfis VPN e Wi-Fi|Removidos.|Removidos.|  
|Certificados|Revogado.|Revogado.|  
|Configurações|Requisitos removidos.|Requisitos removidos.|  
|Agente de gerenciamento|O privilégio de administrador do dispositivo é revogado.|O privilégio de administrador do dispositivo é revogado.|  
|Perfis de email|Não aplicável.|Para perfis de email provisionados pelo Intune, a conta de email e o email são removidos.|  

**Android for Work**

Executar a limpeza seletiva em um dispositivo Android para Trabalho remove o perfil de trabalho junto com todos os dados, os aplicativos e as configurações no perfil de trabalho nesse dispositivo. Isso retira o dispositivo do gerenciamento com o Configuration Manager e o Intune. O apagamento completo não tem suporte para Android for Work.

 **Windows 10, Windows 8.1, Windows RT 8.1 e Windows RT**  

|Conteúdo removido ao desativar um dispositivo|Windows 10, Windows 8.1 e Windows RT 8.1|  
|---------------------------------|-------------|
|Aplicativos da empresa e dados associados instalados usando o Configuration Manager e o Intune.|Os aplicativos são desinstalados e a chaves de sideload são removidas. Os aplicativos que usam a Limpeza Seletiva do Windows terão a chave de criptografia revogada, e os dados não estarão mais acessíveis.|  
|Perfis VPN e Wi-Fi|Removidos.|  
|Certificados|Removidos e revogados.|  
|Configurações|Requisitos removidos.|
|Agente de gerenciamento|Não aplicável. O agente de gerenciamento é integrado.|  
|Perfis de email|Remove o email habilitado para EFS que inclui o aplicativo Mail para emails e anexos de email do Windows.|  

 **Windows 10 Mobile, Windows Phone 8.0 e Windows Phone 8.1**

 |Conteúdo removido ao desativar um dispositivo|Windows 10 Mobile, Windows Phone 8 e Windows Phone 8.1|  
|-|-|
|Aplicativos da empresa e dados associados instalados usando o Configuration Manager e o Intune.|Aplicativos são desinstalados. Dados de aplicativo da empresa são removidos.|  
|Perfis VPN e Wi-Fi|Removido para Windows 10 Mobile e Windows Phone 8.1|  
|Certificados|Removido para o Windows Phone 8.1.|  
|Agente de gerenciamento|Não aplicável. O agente de gerenciamento é interno|  
|Perfis de email|Removido (exceto no Windows Phone 8.0)|  

 As configurações a seguir também são removidas dos dispositivos Windows 10 Mobile e Windows Phone 8.1:  

-   Exigir uma senha para desbloquear os dispositivos móveis  
-   Permitir senha simples  
-   Comprimento mínimo da senha  
-   Tipo de senha necessária  
-   Expiração da senha (dias)  
-   Lembrar de histórico de senha  
-   Número de falhas de logon repetidas permitido antes do dispositivo ser apagado  
-   Minutos de inatividade antes de a senha ser necessária  
-   Tipo de senha necessária – o número mínimo de conjuntos de caracteres  
-   Permitir câmera  
-   Exigir criptografia no dispositivo móvel  
-   Permitir armazenamento removível  
-   Permitir navegador da web  
-   Permitir loja de aplicativo  
-   Permitir captura de tela  
-   Permitir localização geográfica  
-   Permitir Conta da Microsoft  
-   Permitir copiar e colar  
-   Permitir compartilhamento de Internet por Wi-Fi  
-   Permitir conexão automática para liberar pontos de acesso Wi-Fi  
-   Permitir relatórios de pontos de acesso Wi-Fi  
-   Permitir redefinição de fábrica  
-   Permitir Bluetooth  
-   Permitir NFC  
-   Permitir Wi-Fi  

### <a name="to-initiate-a-remote-wipe-from-the-configuration-manager-console"></a>Para iniciar um apagamento remoto no console do Configuration Manager  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** e selecione **Dispositivos**. Como alternativa, é possível clicar em **Coleções de Dispositivos** e selecionar uma coleção.  

2.  Selecione o dispositivo que deseja desativar/apagar.  

3.  Clique em **Ações de Dispositivo Remoto** no **Grupo de Dispositivos**e selecione **Desativar/Apagar**.  

## <a name="wiping-encrypting-file-system-efs-enabled-content"></a>Apagando conteúdo habilitado para EFS (Sistema de Arquivos de Criptografia)  
 O apagamento seletivo de conteúdo criptografados com EFS é suportado pelo Windows 8.1 e Windows RT 8.1. O exemplo a seguir se aplica a um apagamento seletivo de conteúdo habilitado para EFS:  

-   Somente os aplicativos e dados protegidos por EFS que usam o mesmo domínio de Internet que a conta do Intune são apagados de forma seletiva. Para obter mais informações, consulte [Apagamento Seletivo do Windows para Gerenciamento de Dados do Dispositivo](http://technet.microsoft.com/library/dn486874.aspx).  

-   Se houver que qualquer alteração feita no domínio associado ao EFS, as alterações podem levar até 48 horas para que os aplicativos e dados usando o novo domínio possam ser apagados seletivamente.  

-   Cada domínio registrado com o Intune é o domínio que será apagado.  

 Os dados e os aplicativos que atualmente têm suporte apagamento seletivo do EFS são:  

-   Aplicativo de email para o Windows  

-   Pastas de trabalho  

-   Pastas e arquivos criptografados pelo EFS. Para obter mais informações, consulte as [Práticas recomendadas para criptografia de sistema de arquivos](http://support.microsoft.com/kb/223316).  

### <a name="best-practices-for-selective-wipe"></a>Práticas recomendadas para apagamento seletivo  

-   Para apagar email com êxito, provisione perfis de email para dispositivos iOS e Windows Phone 8.1.  

-   Para apagar email com êxito, verifique se os aplicativos são distribuídos por meio do gerenciamento de aplicativos de dispositivos móveis.  

-   Para iOS, defina a configuração "Permitir backup no iCloud" como "Não permitir" para que os usuários não possam restaurar o conteúdo usando o iCloud.  

-   Se uma conta for desativada, depois de um ano ela será desativada pelo Intune e um apagamento seletivo será executado.  

##  <a name="passcode-reset"></a>Redefinição de senha  
 Se um usuário esquecer sua senha, você poderá ajudá-lo removendo a senha de um dispositivo ou impondo uma nova senha temporária em um dispositivo. A tabela abaixo lista como a redefinição de senha funciona em diferentes plataformas remotas.  

|Plataforma|Redefinição de senha|  
|--------------|--------------------|  
|iOS|Suportado para limpar a senha de um dispositivo. Não cria uma nova senha temporária.|  
|Android|Suportado e uma senha temporária é criada.|
|Android for Work | Sem suporte|
|Windows 10|Não tem suporte no momento.|  
|Windows Phone 8 e Windows Phone 8.1|Com suporte|  
|Windows RT 8.1 |Sem suporte|  
|Windows 8.1|Sem suporte|  

### <a name="to-reset-the-passcode-on-a-mobile-device-remotely-in-configuration-manager"></a>Para reconfigurar a senha em um dispositivo móvel remotamente no Configuration Manager  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** e selecione **Dispositivos**. Como alternativa, é possível clicar em **Coleções de Dispositivos** e selecionar uma coleção.  

2.  Selecione o dispositivo ou os dispositivos nos quais a senha será reconfigurada.  

3.  Clique em **Ações de Dispositivo Remoto** no **Grupo de Dispositivos**e selecione **Reconfiguração de Senha**.  

### <a name="to-show-the-state-of-the-passcode-reset"></a>Para mostrar o estado de reconfiguração de senha  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** e selecione **Dispositivos**. Como alternativa, é possível clicar em **Coleções de Dispositivos** e selecionar uma coleção.  

2.  Selecione o dispositivo ou os dispositivos nos quais será mostrado o estado de reconfiguração de senha.  

3.  Clique em **Ações de Dispositivo Remoto** no **Grupo de Dispositivos**e selecione **Mostrar Estado da Senha**.  

##  <a name="remote-lock"></a>Bloqueio remoto  
 Se um usuário perder o dispositivo, você poderá bloquear o dispositivo remotamente. A tabela abaixo lista como o bloqueio remoto funciona em diferentes plataformas móveis.  

|Plataforma|Bloqueio remoto|  
|--------------|-----------------|  
|iOS|Com suporte|  
|Android|Com suporte|  
|Windows 10|Não tem suporte no momento.|  
|Windows Phone 8 e Windows Phone 8.1|Com suporte|  
|Windows RT 8.1 |Suportado se o usuário atual do dispositivo for o mesmo usuário que registrou o dispositivo.|  
|Windows 8.1|Suportado se o usuário atual do dispositivo for o mesmo usuário que registrou o dispositivo.|  

### <a name="to-lock-a-mobile-device-remotely-through-the-configuration-manager-console"></a>Para bloquear um dispositivo móvel remotamente por meio do console do Configuration Manager  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** e selecione **Dispositivos**. Como alternativa, é possível clicar em **Coleções de Dispositivos** e selecionar uma coleção.  

2.  Selecione o dispositivo ou os dispositivos que serão bloqueados.  

3.  Clique em **Ações de Dispositivo Remoto** no **Grupo de Dispositivos**e selecione **Bloqueio Remoto**.  

### <a name="to-show-the-state-of-the-remote-lock"></a>Para mostrar o estado do bloqueio remoto  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** e selecione **Dispositivos**. Como alternativa, é possível clicar em **Coleções de Dispositivos** e selecionar uma coleção.  

2.  Selecione o dispositivo no qual será mostrado o estado do bloqueio remoto.  

3.  Clique em **Ações de Dispositivo Remoto** no **Grupo de Dispositivos**e selecione **Mostrar Estado do Bloqueio Remoto**.  

### <a name="see-also"></a>Consulte também  
 [Apagamento Seletivo do Windows para Gerenciamento de Dados do Dispositivo](http://technet.microsoft.com/library/dn486874.aspx)   

