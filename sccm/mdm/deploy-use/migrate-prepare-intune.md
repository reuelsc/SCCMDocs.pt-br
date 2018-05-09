---
title: Preparar o Intune para migração de usuários
titleSuffix: Configuration Manager
description: Saiba como preparar o Intune no Azure para a migração do usuário do híbrida MDM.
author: aczechowski
manager: dougeby
ms.date: 12/05/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: db97ae9e-34f4-4e10-a282-cd211f612bb4
ms.openlocfilehash: a2636713f8c121eecd826eeba060f8e3f8e865f3
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="prepare-intune-for-user-migration"></a>Preparar o Intune para migração de usuários 

*Aplica-se a: System Center Configuration Manager (Branch Atual)*    

Antes de migrar os usuários do MDM híbrido (integrado ao Intune com o Configuration Manager) para o Intune autônomo, você deverá seguir algumas etapas para preparar o Intune. Essas etapas ajudam a garantir que os usuários e seus dispositivos migrados continuem gerenciados. Quando você concluir essas etapas e iniciar a migração para o Intune, o processo deverá ser transparente para os usuários.  

## <a name="fix-issues-found-during-data-collection-and-import"></a>Corrigir os problemas encontrados durante a importação e a coleta de dados
Se você seguiu o processo de [importar dados do Configuration Manager para o Microsoft Intune](migrate-import-data.md), a ferramenta Importador de Dados do Intune forneceu um resumo de todos os objetos que ela não pôde importar. Alguns dos problemas típicos que geralmente são encontrados e as etapas para corrigi-los no Intune, são listados na tabela a seguir: 

|Problema  |Correção  |
|---------|---------|
|As coleções baseadas em uma associação direta ou em uma complexa não são serão migradas automaticamente.|Você deve criar grupos do AAD (Azure Active Directory) no Azure para substituir a coleção que não foi importada. Em seguida, você deve atribuir o objeto ao grupo.|
|As políticas não eram importáveis |Você deve recriar a política no Intune.|
|Implantação de um objeto não importada|Você deve atribuir o objeto ao grupo. O grupo deve conter os mesmos usuários da coleção para a implantação.|

## <a name="create-intune-objects"></a>Criar objetos do Intune 
Se você seguiu o processo de [importar dados do Configuration Manager para o Microsoft Intune](migrate-import-data.md) e corrigiu os problemas durante o processo de importação, verifique se os objetos importados estão configurados corretamente. Além disso, crie os objetos adicionais (políticas, perfis, aplicativos, etc.) no Intune que você precisa em sua organização. 

## <a name="assign-intune-licenses-to-migrated-users"></a>Atribuir licenças do Intune aos usuários migrados
No Configuration Manager, você adiciona uma coleção na assinatura do Intune e os membros da coleção têm a capacidade de registrar seus dispositivos. Embora haja uma licença do Intune reservada para dispositivos registrados, essas licenças não são associadas especificamente ao usuário ou ao dispositivo. Por exemplo, não há uma licença do Intune no AAD para um usuário que tenha um dispositivo registrado. No entanto, no Intune autônomo você deve configurar uma licença do Intune para cada usuário. Você deve fazer isso antes de migrar um usuário para o Intune autônomo para garantir que o usuário e seus dispositivos sejam gerenciados pelo Intune após a alteração na autoridade de MDM. Para saber mais, veja [Atribuir licenças do Intune a suas contas de usuário](https://docs.microsoft.com/intune/licenses-assign). 

## <a name="verify-intune-user-groups"></a>Verificar os grupos de usuários do Intune
Os usuários e grupos provavelmente já estão no AAD, porque a sincronização de diretório está configurada. Para verificar se os usuários fazem parte do grupo de usuários correto, recomendamos que você examine seus grupos de usuários do Intune. Direcione políticas, perfis, aplicativos, etc. para esses grupos. Verifique se os usuários migrados para o Intune autônomo fazem parte dos grupos corretos. 

## <a name="configure-role-based-administration-control-rbac"></a>Configurar o RBAC (controle de administração baseada em funções)
Como parte da migração, configure todas as funções de RBAC necessárias no Intune e atribua usuários a essas funções. Observe que há diferenças entre o RBAC no Configuration Manager e no Intune, como a definição de escopo dos recursos. Para obter detalhes, consulte [RBAC (controle de administração baseada em funções) com o Intune](https://docs.microsoft.com/intune/role-based-access-control).

## <a name="assign-apps-and-policies-to-aad-groups"></a>Atribuir aplicativos e políticas aos grupos do AAD
Se você seguiu a fase [Importar dados do Configuration Manager para o Microsoft Intune](migrate-import-data.md) do processo de migração para migrar diferentes objetos do Configuration Manager para o Intune, muitos dos seus objetos já devem estar atribuídos aos grupos do AAD. No entanto, você deve verificar se todos os objetos (aplicativos, políticas, perfis, etc.) são atribuídos aos grupos do AAD corretos. Se você atribuir objetos corretamente, os dispositivos do usuário serão configurados automaticamente depois que o usuário for migrado e a migração deverá ser transparente para os usuários. Para obter detalhes de como atribuir os objetos a um grupo do AAD, consulte o seguinte: 
- [Atribuir políticas](https://docs.microsoft.com/intune/get-started-policies) 
- [Atribuir perfis](https://docs.microsoft.com/intune/device-profile-assign) 
- [Atribuir aplicativos](https://docs.microsoft.com/intune/get-started-apps) 

## <a name="terms-and-conditions-policy"></a>Política de termos e condições
Assim como outras políticas no nível do locatário, as políticas de termos e condições são migradas automaticamente para o Intune quando a autoridade mista está habilitada para o locatário.  No entanto, você deve atribuir os termos e condições a um grupo que contenha usuários migrados para relatar a aceitação dos usuários migrados com precisão e garantir que os termos e condições sejam direcionados corretamente para novas atualizações dos termos e condições ou para novos registros de dispositivos. Os usuários não precisam aceitar os termos e condições novamente, a menos que haja alterações feitas na política no console do Configuration Manager. Para obter detalhes, consulte [Atribuir termos e condições](https://docs.microsoft.com/intune/terms-and-conditions-create#assign-terms-and-conditions).

## <a name="configure-the-exchange-connector"></a>Configurar o Exchange Connector
Se você usa o Exchange e tem um Exchange Connector local no Configuration Manager, será necessário [configurar o Exchange Connector local no Intune](https://docs.microsoft.com/intune/exchange-connector-install). Considere também as informações nas seções a seguir para ajudar você a migrar para o Intune Exchange Connector e para assegurar que o acesso condicional funcione apropriadamente após a migração.

### <a name="powershell-scripts-to-help-you-migrate-to-the-intune-exchange-connector"></a>Scripts do PowerShell para ajudar você a migrar para o Intune Exchange Connector 
Os scripts do PowerShell estão disponíveis para ajudar você a se preparar para transicionar seus dispositivos do Exchange do Configuration Manager Exchange Connector para o Intune Exchange Connector. Embora a execução desses scripts seja opcional, recomendamos executá-los para remover dispositivos inativos do Exchange, o que impede o Intune de descobrir dispositivos desnecessários. A execução dos scripts assegura que os dispositivos descobertos por meio do Exchange possam ser mesclados com dispositivos registrados tranquilamente com o Intune. Execute esses scripts antes de configurar o Intune Exchange Connector. Os scripts do PowerShell fazem parte da instalação do Intune Data Importer que você usa para [importar os dados do Configuration Manager no Microsoft Intune](migrate-import-data.md) no próximo artigo. Para obter detalhes e baixar os scripts, acesse a página [Microsoft Intune Data Importer](https://github.com/ConfigMgrTools/Intune-Data-Importer) do GitHub.

### <a name="steps-to-ensure-conditional-access-works-properly-after-user-migration"></a>Etapas para assegurar que o acesso condicional funcione apropriadamente após a migração do usuário
Para que o acesso condicional funcione corretamente após a migração de usuários e para garantir que os usuários continuem a ter acesso ao servidor de email, verifique se o seguinte é verdadeiro:
- Se a configuração padrão de nível de acesso do Exchange ActiveSync (DefaultAccessLevel) for definida para bloquear ou colocar em quarentena, os dispositivos poderão perder o acesso ao email. 
- Se o Exchange Connector estiver instalado no Configuration Manager e a configuração **Nível de acesso quando um dispositivo móvel não é gerenciado por uma regra** tiver o valor **Permitir acesso**, você deverá instalar o [Exchange Connector local](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access) no Intune antes de migrar os usuários. Defina a configuração padrão de nível de acesso no Intune na folha **Exchange local** em **Configurações de acesso avançadas do Exchange ActiveSync**. Para obter detalhes, consulte [Configurar o acesso local ao Exchange](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access).
- Use a mesma configuração para ambos os conectores. O último conector que você configurar substituirá as configurações do ActiveSync da organização gravadas anteriormente por outro conector. Se você configurar os conectores de forma diferente, poderão ocorrer alterações de acesso condicional inesperadas.
- Remova os usuários do direcionamento de acesso condicional no Configuration Manager quando eles forem migrados para o Intune autônomo.

## <a name="configure-the-microsoft-intune-certificate-connector"></a>Configurar o Microsoft Intune Certificate Connector
Se você usar o NDES para emitir certificados usando o protocolo SCEP, será necessário configurar o Microsoft Intune Certificate Connector. O computador que hospeda o conector NDES do Intune não pode ser o mesmo computador que hospeda o conector NDES do Configuration Manager. Para obter detalhes, consulte [Configurar e gerenciar certificados SCEP com o Intune](https://docs.microsoft.com/en-us/intune/certificates-scep-configure). 

> [!Important]    
> Depois de configurar o conector, você deverá modificar os perfis do SCEP importados para referenciar a nova URL do servidor.

## <a name="next-step"></a>Próximas etapas
Depois de preparar o Intune para a migração, você estará pronto para migrar um conjunto de usuários de teste para o Intune autônomo. Para obter detalhes, consulte [Change the MDM authority for specific users (mixed authority)](migrate-mixed-authority.md) [Alterar a autoridade de MDM para usuários específicos (autoridade mista)].


