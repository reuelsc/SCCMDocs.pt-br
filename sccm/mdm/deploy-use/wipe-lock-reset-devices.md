---
title: "Proteger dados com apagamento remoto, bloqueio ou redefinição de senha"
titleSuffix: Configuration Manager
description: "Proteja os dados do dispositivo com uma limpeza completa, limpeza seletiva, bloqueio remoto ou redefinição de senha usando o System Center Configuration Manager."
ms.custom: na
ms.date: 10/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 770da7bd-02dd-474a-9604-93ff1ea0c1e4
caps.latest.revision: "18"
caps.handback.revision: "0"
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 55d49c388b4ea60627f72ffe61796c70de6f9416
ms.sourcegitcommit: a5f8b5cfdabf0298e4302e24210e725a06a9de82
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2017
---
# <a name="protect-data-with-remote-wipe-lock-or-passcode-reset-by-using-system-center-configuration-manager"></a>Proteger os dados com a limpeza remota, bloqueio ou redefinição de senha usando o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager fornece os recursos de limpeza seletiva, limpeza completa, bloqueio remoto e redefinição de senha. Os dispositivos móveis podem armazenar dados corporativos confidenciais e fornecer acesso a muitos recursos corporativos. Para ajudar a proteger os dispositivos, você pode emitir:  

- Um apagamento completo para restaurar as configurações de fábrica do dispositivo.  

- Um apagamento seletivo para remover somente os dados da empresa.  

- Um bloqueio remoto para ajudar a proteger um dispositivo que pode estar perdido.  

- Uma redefinição de senha do dispositivo.  

## <a name="full-wipe"></a>Apagamento completo  
Você pode emitir um comando de apagamento para um dispositivo quando precisar proteger um dispositivo perdido ou quando desativar um dispositivo de seu uso ativo.  

Emita um **apagamento completo** para um dispositivo para restaurá-lo às suas configurações de fábrica. Isso remove todos os dados da empresa e do usuário e configurações. É possível fazer um apagamento completo em dispositivos Windows Phone, iOS, Android e Windows 10.  

> [!NOTE]
> Você só pode executar um apagamento completo em dispositivos corporativos.

> [!NOTE]
> Apagar dispositivos Windows 10 em versões anteriores à versão 1511 com menos de 4 GB de RAM pode deixar o dispositivo sem resposta. [Saiba mais](https://technet.microsoft.com/library/mt592024.aspx#full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram).

#### <a name="to-initiate-a-remote-wipe-from-the-configuration-manager-console"></a>Para iniciar um apagamento remoto no console do Configuration Manager  

1. No console do Configuration Manager, escolha **Ativos e Conformidade**, e escolha **Dispositivos**. Como alternativa, é possível escolher **Coleções de Dispositivos** e selecionar uma coleção.  

2. Selecione o dispositivo que deseja desativar/apagar.  

3. Clique em **Ações do Dispositivo Remoto** no **Grupo de Dispositivos**e escolha **Desativar/Limpar**.  

## <a name="selective-wipe"></a>Limpeza seletiva  
Emita um **apagamento seletivo** para um dispositivo para remover apenas os dados da empresa. A tabela a seguir descreve, por plataforma, qual dado foi removido e o efeito nos dados que permaneceram no dispositivo após a limpeza seletiva.  

**iOS**  

|Conteúdo removido quando você está desativando um dispositivo|iOS|  
|--------------------------------------------|---------|  
|Aplicativos da empresa e dados associados instalados usando o Configuration Manager e o Intune|Aplicativos são desinstalados. Dados de aplicativo da empresa são removidos.|  
|Perfis VPN e Wi-Fi|Removidos.|  
|Certificados|Removidos e revogados.|  
|Configurações|Removidos, exceto para: **Permitir roaming de voz**, **Permitir roaming de dados** e **Permitir sincronização automática durante roaming**.|  
|Agente de gerenciamento|O perfil de gerenciamento é removido.|  
|Perfis de email|Para os perfis de email configurados pelo Intune, a conta de email e o email são removidos.|  

**Android e Android Samsung KNOX Standard**  

|Conteúdo removido quando você está desativando um dispositivo|Android|Samsung KNOX Standard|  
|--------------------------------------------|-------------|------------------|  
|Aplicativos da empresa e dados associados instalados usando o Configuration Manager e o Intune|Aplicativos e dados permanecem instalados.|Aplicativos são desinstalados.|  
|Perfis VPN e Wi-Fi|Removidos.|Removidos.|  
|Certificados|Revogado.|Revogado.|  
|Configurações|Os requisitos são removidos.|Os requisitos são removidos.|  
|Agente de gerenciamento|O privilégio de administrador do dispositivo é revogado.|O privilégio de administrador do dispositivo é revogado.|  
|Perfis de email|Não aplicável.|Para os perfis de email configurados pelo Intune, a conta de email e o email são removidos.|  

**Android for Work**

Fazer uma limpeza seletiva em um dispositivo Android for Work remove o perfil de trabalho junto com todos os dados, aplicativos e configurações no perfil de trabalho nesse dispositivo. Isso retira o dispositivo do gerenciamento com o Configuration Manager e o Intune. O apagamento completo não tem suporte para Android for Work.

 **Windows 10, Windows 8.1, Windows RT 8.1 e Windows RT**  

|Conteúdo removido quando você está desativando um dispositivo|Windows 10, Windows 8.1 e Windows RT 8.1|  
|---------------------------------|-------------|
|Aplicativos da empresa e dados associados instalados usando o Configuration Manager e o Intune|Os aplicativos são desinstalados e a chaves de sideload são removidas. Os aplicativos que usam a Limpeza Seletiva do Windows terão a chave de criptografia revogada e os dados não estarão mais acessíveis.|  
|Perfis VPN e Wi-Fi|Removidos.|  
|Certificados|Removidos e revogados.|  
|Configurações|Os requisitos são removidos.|
|Agente de gerenciamento|Não aplicável. O agente de gerenciamento é interno.|  
|Perfis de email|O email habilitado para EFS é removido, que inclui o aplicativo de email para o Windows e anexos.|  

 **Windows 10 Mobile, Windows Phone 8.0 e Windows Phone 8.1**

|Conteúdo removido quando você está desativando um dispositivo|Windows 10 Mobile, Windows Phone 8 e Windows Phone 8.1|  
|-|-|
|Aplicativos da empresa e dados associados instalados usando o Configuration Manager e o Intune|Aplicativos são desinstalados. Dados de aplicativo da empresa são removidos.|  
|Perfis VPN e Wi-Fi|Removido para o Windows 10 Mobile e Windows Phone 8.1.|  
|Certificados|Removido para o Windows Phone 8.1.|  
|Agente de gerenciamento|Não aplicável. O agente de gerenciamento é interno.|  
|Perfis de email|Removido (exceto no Windows Phone 8.0).|  

As configurações a seguir também são removidas dos dispositivos Windows 10 Mobile e Windows Phone 8.1:  

- **Exigir uma senha para desbloquear os dispositivos móveis**  
- **Permitir senha simples**  
- **Tamanho mínimo da senha**  
- **Tipo de senha necessária**
- **Expiração da senha (dias)**  
- **Lembrar histórico de senha**  
- **Número de falhas de entrada repetidas permitidas antes que o dispositivo seja apagado**  
- **Minutos de inatividade antes de a senha ser necessária**  
- **Tipo de senha necessária – o número mínimo de conjuntos de caracteres**  
- **Permitir câmera**
- **Exigir criptografia no dispositivo móvel**  
- **Permitir armazenamento removível**  
- **Permitir navegador da Web**  
- **Permitir armazenamento de aplicativos**  
- **Permitir captura de tela**  
- **Permitir geolocalização**  
- **Permitir Conta da Microsoft**  
- **Permitir copiar e colar**  
- **Permitir compartilhamento de Internet por Wi-Fi**  
- **Permitir conexão automática a pontos de acesso Wi-Fi gratuitos**  
- **Permitir relatório de ponto de acesso Wi-Fi**  
- **Permitir redefinição de fábrica**
- **Permitir Bluetooth**  
- **Permitir NFC**
- **Permitir Wi-Fi**

#### <a name="to-initiate-a-remote-wipe-from-the-configuration-manager-console"></a>Para iniciar um apagamento remoto no console do Configuration Manager  

1. No console do Configuration Manager, escolha **Ativos e Conformidade**, e escolha **Dispositivos**. Como alternativa, é possível escolher **Coleções de Dispositivos** e selecionar uma coleção.  

2. Selecione o dispositivo que deseja desativar/apagar.  

3. Clique em **Ações do Dispositivo Remoto** no **Grupo de Dispositivos**e escolha **Desativar/Limpar**.  

## <a name="wiping-efs-enabled-content"></a>Apagar conteúdo habilitado para EFS  
O Windows 8.1 e o Windows RT 8.1 suportam a limpeza seletiva do conteúdo criptografado do Sistema de Arquivos com Criptografia (EFS). O exemplo a seguir se aplica a um apagamento seletivo de conteúdo habilitado para EFS:  

- Somente os aplicativos e os dados protegidos por EFS, com o mesmo domínio de Internet da conta do Intune, são apagados de forma seletiva. Para obter mais informações, consulte [Apagamento Seletivo do Windows para Gerenciamento de Dados do Dispositivo](http://technet.microsoft.com/library/dn486874.aspx).  

- Se houver qualquer alteração no domínio associado ao EFS, as alterações poderão levar até 48 horas para que os aplicativos e os dados usando o novo domínio possam ser apagados seletivamente.  

- Cada domínio registrado com o Intune é o domínio que será apagado.  

Os dados e os aplicativos que atualmente têm suporte da limpeza seletiva do EFS são:  

- Aplicativo de email para o Windows.  

- Pastas de trabalho.

- Pastas e arquivos criptografados pelo EFS. Para obter mais informações, consulte as [Práticas recomendadas para criptografia de sistema de arquivos](http://support.microsoft.com/kb/223316).  

### <a name="best-practices-for-selective-wipe"></a>Práticas recomendadas para a limpeza seletiva  

- Para limpar o email com êxito, configure perfis de email para os dispositivos iOS e Windows Phone 8.1.  

- Para limpar o email com êxito, verifique se os aplicativos são distribuídos por meio do gerenciamento de aplicativos dos dispositivos móveis.  

- Para o iOS, defina a configuração **Permitir backup no iCloud** para **Não permitir** para que os usuários não possam restaurar o conteúdo usando o iCloud.  

- Se uma conta for desativada, depois de um ano ela será desativada pelo Intune e uma limpeza seletiva será executada.  

##  <a name="passcode-reset"></a>Redefinição de senha  
Se um usuário esquecer sua senha, você poderá ajudá-lo removendo a senha de um dispositivo ou impondo uma nova senha temporária em um dispositivo. A tabela abaixo lista como a redefinição da senha funciona em diferentes plataformas móveis.  

|Plataforma|Redefinição de senha|  
|--------------|--------------------|  
|iOS|Suportado para limpar a senha de um dispositivo. Não cria uma nova senha temporária.|
|macOS| Não há suporte.|
|Android|Suportado e uma senha temporária é criada.|
|Android for Work | Não há suporte.|
|PCs com Windows 10|Não há suporte.|  
|Celular com Windows 10|Suportado, exceto os dispositivos ingressados do Azure AD.|
|Windows Phone 8.1|Com suporte.|  
|Windows RT 8.1 |Não há suporte.|  
|PCs com Windows 8.1 |Não há suporte.|  

> [!Note]    
> Você deve executar a ação de redefinição de senha no site de nível superior do seu ambiente. Por exemplo, se você usa um site de administração central, a ação somente pode ser executada nesse site. Se você estiver usando um site primário autônomo, a ação somente poderá ser executada nesse site.

#### <a name="to-reset-the-passcode-on-a-mobile-device-remotely-in-configuration-manager"></a>Para reconfigurar a senha em um dispositivo móvel remotamente no Configuration Manager  

1. No console do Configuration Manager, escolha **Ativos e Conformidade**, e escolha **Dispositivos**. Como alternativa, é possível escolher **Coleções de Dispositivos** e selecionar uma coleção.  

2. Selecione o dispositivo ou os dispositivos nos quais a senha será reconfigurada.  

3. Clique em **Ações do Dispositivo Remoto** no **Grupo de Dispositivos**e escolha **Redefinir Senha**.  

#### <a name="to-show-the-state-of-the-passcode-reset"></a>Para mostrar o estado de reconfiguração de senha  

1. No console do Configuration Manager, escolha **Ativos e Conformidade**, e escolha **Dispositivos**. Como alternativa, é possível escolher **Coleções de Dispositivos** e selecionar uma coleção.  

2. Selecione o dispositivo ou os dispositivos nos quais será mostrado o estado de reconfiguração de senha.  

3. Clique em **Ações do Dispositivo Remoto** no **Grupo de Dispositivos**e escolha **Mostrar Estado da Senha**.  

## <a name="remote-lock"></a>Bloqueio remoto  
Se um usuário perder o dispositivo, você poderá bloqueá-lo remotamente. A tabela abaixo lista como o bloqueio remoto funciona em diferentes plataformas móveis.  

|Plataforma|Bloqueio remoto|  
|--------------|-----------------|  
|iOS|Com suporte.|  
|Android|Com suporte.|  
|Windows 10|Não tem suporte no momento.|  
|Windows Phone 8 e Windows Phone 8.1|Com suporte.|  
|Windows RT 8.1 |Suportado se o usuário atual do dispositivo for o mesmo usuário que registrou o dispositivo.|  
|Windows 8.1|Suportado se o usuário atual do dispositivo for o mesmo usuário que registrou o dispositivo.|  

> [!Note]    
> Você deve executar a ação de bloqueio remoto no site de nível superior do seu ambiente. Por exemplo, se você usa um site de administração central, a ação somente pode ser executada nesse site. Se você estiver usando um site primário autônomo, a ação somente poderá ser executada nesse site.

#### <a name="to-lock-a-mobile-device-remotely-through-the-configuration-manager-console"></a>Para bloquear um dispositivo móvel remotamente por meio do console do Configuration Manager  

1. No console do Configuration Manager, escolha **Ativos e Conformidade**, e escolha **Dispositivos**. Como alternativa, é possível escolher **Coleções de Dispositivos** e selecionar uma coleção.  

2. Selecione o dispositivo ou os dispositivos que serão bloqueados.  

3. Escolha **Ações do Dispositivo Remoto** no **Grupo de Dispositivos**e escolha **Bloqueio Remoto**.  

#### <a name="to-show-the-state-of-the-remote-lock"></a>Para mostrar o estado do bloqueio remoto  

1. No console do Configuration Manager, escolha **Ativos e Conformidade**, e escolha **Dispositivos**. Como alternativa, é possível escolher **Coleções de Dispositivos** e selecionar uma coleção.  

2. Selecione o dispositivo no qual será mostrado o estado do bloqueio remoto.  

3. Escolha **Ações do Dispositivo Remoto** no **Grupo de Dispositivos**e escolha **Mostrar Estado do Bloqueio Remoto**.  

### <a name="see-also"></a>Consulte também  
[Apagamento Seletivo do Windows para Gerenciamento de Dados do Dispositivo](http://technet.microsoft.com/library/dn486874.aspx)   
