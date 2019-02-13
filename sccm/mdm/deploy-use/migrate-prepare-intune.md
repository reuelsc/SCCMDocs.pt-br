---
title: Preparar o Intune para migração de usuários
titleSuffix: Configuration Manager
description: Saiba como preparar o Intune no Azure para a migração do usuário do híbrida MDM.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/26/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: db97ae9e-34f4-4e10-a282-cd211f612bb4
ms.collection: M365-identity-device-management
ms.openlocfilehash: e217c7afc2910a23fe3f29fa215d58574f3d79d8
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137806"
---
# <a name="prepare-intune-for-user-migration"></a>Preparar o Intune para migração de usuários 

*Aplica-se a: System Center Configuration Manager (Branch atual)*    
Antes de migrar os usuários do MDM híbrido para Intune autônomo, execute as etapas para preparar o Intune. Essas etapas ajudam a garantir que seus usuários migrados e seus dispositivos continuem a ser gerenciado. Quando você concluir essas etapas e iniciar a migração para o Intune, não há nenhum impacto significativos para os usuários.  

## <a name="fix-issues-found-during-data-collection-and-import"></a>Corrigir os problemas encontrados durante a importação e a coleta de dados
Se você tiver usado a ferramenta Intune Data Importer [importar dados do Configuration Manager para o Microsoft Intune](migrate-import-data.md), ele resumidos os objetos que ele não foi possível importar. Alguns dos problemas típicos e etapas para corrigi-los no Intune, são listados na tabela a seguir: 

|Problema  |Fix  |
|---------|---------|
|Coleções com base na associação direta ou em uma complexa não são migradas automaticamente.|Crie grupos do Active Directory do Azure (AD Azure) no Azure para substituir a coleção que não foi importada. Em seguida, atribua o objeto ao grupo.|
|As políticas não eram importáveis |Recrie a política do Intune.|
|Implantação de um objeto não importada|Atribua o objeto ao grupo. O grupo deve incluir os mesmos usuários da coleção para a implantação.|

## <a name="create-intune-objects"></a>Criar objetos do Intune 
Se você [importou dados do Configuration Manager para o Microsoft Intune](migrate-import-data.md) e corrigir problemas durante o processo, verifique se os objetos importados estão configurados corretamente. Também crie quaisquer objetos adicionais (políticas, perfis e aplicativos) no Intune que você precisa em sua organização. 

## <a name="assign-intune-licenses-to-migrated-users"></a>Atribuir licenças do Intune aos usuários migrados
No Configuration Manager, você adiciona uma coleção para a assinatura do Intune e os membros da coleção podem registrar seus dispositivos. Enquanto uma licença do Intune é reservada para dispositivos registrados, essas licenças não estão associadas um usuário ou dispositivo. Por exemplo, você não encontrar uma licença do Intune no Azure AD para um usuário que tenha um dispositivo registrado. 

No Intune autônomo, configure uma licença do Intune para cada usuário. Configurar a licença *antes de* migrar um usuário para o Intune autônomo. Essa ação torna-se de que o usuário e seus dispositivos são gerenciados pelo Intune após a alteração na autoridade de MDM. Para saber mais, veja [Atribuir licenças do Intune a suas contas de usuário](https://docs.microsoft.com/intune/licenses-assign). 

## <a name="verify-intune-user-groups"></a>Verificar os grupos de usuários do Intune
Os usuários e grupos provavelmente já estão no Azure AD porque você tem a sincronização de diretório configurada. Para verificar se os usuários fazem parte do grupo de usuários correto, recomendamos que você examine seus grupos de usuários do Intune. Você direcionar políticas, perfis e aplicativos a esses grupos. Verifique se os usuários migrados para o Intune autônomo fazem parte dos grupos corretos. 

## <a name="configure-role-based-administration-control-rbac"></a>Configurar o RBAC (controle de administração baseada em funções)
Como parte da migração, configure todas as funções de RBAC necessárias no Intune e atribua usuários a essas funções. Há diferenças entre o RBAC no Configuration Manager e o Intune, como o escopo de recursos. Para obter mais informações, consulte [controle de administração baseada em função (RBAC) com o Intune](https://docs.microsoft.com/intune/role-based-access-control).

## <a name="assign-apps-and-policies-to-aad-groups"></a>Atribuir aplicativos e políticas aos grupos do AAD
Se você [importou dados do Configuration Manager para o Microsoft Intune](migrate-import-data.md), muitos dos seus objetos já devem estar atribuídos aos grupos do AD do Azure. Verifique se todos os objetos (aplicativos, políticas e perfis) são atribuídos para a correta grupos do Azure AD. Se você atribuir objetos corretamente, os dispositivos do usuário são configurados automaticamente depois que o usuário for migrado e a migração não deve ter qualquer impacto significativos para os usuários. Para obter mais informações sobre como atribuir os objetos a um grupo do AD do Azure, consulte os seguintes artigos: 
- [Atribuir políticas](https://docs.microsoft.com/intune/get-started-policies)  
- [Atribuir perfis](https://docs.microsoft.com/intune/device-profile-assign)  
    > [!NOTE]  
    > Quando o Intune implanta o novo perfil de email, os usuários recebem uma solicitação para inserir novamente sua senha. Esse comportamento resulta em emails que estão sendo baixados novamente em dispositivos dos usuários. Quaisquer modificações personalizadas feitas pelo usuário precisará ser feito novamente. 
- [Atribuir aplicativos](https://docs.microsoft.com/intune/get-started-apps) 

## <a name="terms-and-conditions-policy"></a>Política de termos e condições
Assim como outras políticas no nível do locatário, as políticas de termos e condições são migradas automaticamente para o Intune quando a autoridade mista está habilitada para o locatário.  No entanto, você deve atribuir os termos e condições para um grupo que contenha migrado usuários para relatar a aceitação para os usuários migrados com precisão e certifique-se de que os termos e condições sejam direcionadas corretamente futuras termos e condições ou dispositivo registros. Os usuários não precisarão aceitem novamente os termos e condições, a menos que haja alterações feitas na política no console do Configuration Manager. Para obter mais informações, consulte [atribuir termos e condições](https://docs.microsoft.com/intune/terms-and-conditions-create#assign-terms-and-conditions).

## <a name="configure-the-exchange-connector"></a>Configurar o Exchange Connector
Se você usa o Exchange e tem um Exchange Connector local no Configuration Manager, será necessário [configurar o Exchange Connector local no Intune](https://docs.microsoft.com/intune/exchange-connector-install). Considere também as informações nas seções a seguir para ajudá-lo a migrar para o Intune Exchange Connector e para garantir que o acesso condicional funciona corretamente após a migração.

### <a name="powershell-scripts-to-help-you-migrate-to-the-intune-exchange-connector"></a>Scripts do PowerShell para ajudar você a migrar para o Intune Exchange Connector 
Os scripts do PowerShell estão disponíveis para ajudar você a se preparar para transicionar seus dispositivos do Exchange do Configuration Manager Exchange Connector para o Intune Exchange Connector. Embora a execução desses scripts seja opcional, recomendamos executá-los para remover dispositivos inativos do Exchange, o que impede o Intune de descobrir dispositivos desnecessários. A execução dos scripts assegura que os dispositivos descobertos por meio do Exchange possam ser mesclados com dispositivos registrados tranquilamente com o Intune. Execute esses scripts antes de configurar o Intune Exchange Connector. Os scripts do PowerShell fazem parte da instalação do Intune Data Importer que você usa para [importar os dados do Configuration Manager no Microsoft Intune](migrate-import-data.md) no próximo artigo. Para obter detalhes e baixar os scripts, acesse a página [Microsoft Intune Data Importer](https://github.com/ConfigMgrTools/Intune-Data-Importer) do GitHub.

### <a name="steps-to-make-sure-conditional-access-works-properly-after-user-migration"></a>Etapas para que o acesso condicional se funciona corretamente após a migração do usuário
Para acesso condicional funcione corretamente após a migração de usuários e certifique-se de que os usuários continuem a ter acesso ao servidor de email, verifique se que as seguintes configurações estão definidas:
- Se a configuração padrão de nível de acesso do Exchange ActiveSync (DefaultAccessLevel) for definida para bloquear ou colocar em quarentena, os dispositivos poderão perder o acesso ao email. 
- Se o Exchange Connector está instalado no Configuration Manager e o **nível de acesso quando um dispositivo móvel não é gerenciado por uma regra** tem o valor de **permitir o acesso**, instale o [ Conector do Exchange no local](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access) no Intune antes de migrar os usuários. Defina a configuração de nível de acesso padrão no Intune na **Exchange no local** página no **configurações de acesso avançadas do Exchange ActiveSync**. Para obter mais informações, consulte [configurar o Exchange local acesso](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access).
- Use a mesma configuração para ambos os conectores. O último conector que você configurar substituirá as configurações do ActiveSync da organização gravadas anteriormente por outro conector. Se você configurar os conectores de forma diferente, poderão ocorrer alterações de acesso condicional inesperadas.
- Remova os usuários do direcionamento de acesso condicional no Configuration Manager quando eles forem migrados para o Intune autônomo.

## <a name="configure-the-microsoft-intune-certificate-connector"></a>Configurar o Microsoft Intune Certificate Connector
Se você usar o NDES para emitir certificados usando o protocolo SCEP, será necessário configurar o Microsoft Intune Certificate Connector. O computador que hospeda o conector NDES do Intune não pode ser o mesmo computador que hospeda o conector NDES no Configuration Manager. Para obter mais informações, consulte [configurar e gerenciar certificados SCEP com o Intune](https://docs.microsoft.com/intune/certificates-scep-configure). 

> [!Important]    
> Depois de configurar o conector, modificar perfis do SCEP importados para referenciar a nova URL do servidor.

## <a name="next-step"></a>Próximas etapas
Depois de preparar o Intune para migração, você estará pronto para migrar um conjunto de usuários de teste para o Intune autônomo. Para obter mais informações, consulte [alterar a autoridade MDM para usuários específicos (autoridade misturadas)](migrate-mixed-authority.md).


