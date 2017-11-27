---
title: "Alterar a autoridade de MDM para usuários específicos (autoridade de MDM mista)"
titleSuffix: Configuration Manager
description: "Saiba como alterar a autoridade de MDM do MDM híbrido para Intune autônomo somente para alguns usuários."
keywords: 
author: dougeby
manager: dougeby
ms.date: 09/14/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: 6f0201d7-5714-4ba0-b2bf-d1acd0203e9a
ms.openlocfilehash: 31d1d84c225d041f644669f0d3279e6bcd3f75ba
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="change-the-mdm-authority-for-specific-users-mixed-mdm-authority"></a>Alterar a autoridade de MDM para usuários específicos (autoridade de MDM mista) 

*Aplica-se a: System Center Configuration Manager (Branch Atual)*    

É possível configurar uma autoridade de MDM mista no mesmo locatário selecionando alguns usuários a serem gerenciados no Intune e outros para serem gerenciados com o MDM híbrido (Intune integrado ao Configuration Manager). Este tópico fornece informações de como começar a mover usuários para o Intune autônomo e considera que você tenha concluído as etapas a seguir:
- Usado a ferramenta de importação de dados para [Importar objetos do Configuration Manager para o Intune](migrate-import-data.md) (opcional).
- [Preparou o Intune para migração do usuário](migrate-prepare-intune.md) a fim de garantir que os usuários e respectivos dispositivos continuem sendo gerenciados depois que forem migrados.

> [!Note]    
> Se você decidir que deseja fazer uma reinicialização completa do seu locatário, o que removerá todas as políticas, aplicativos e registros de dispositivos, contate o suporte para obter assistência.

Os usuários migrados e seus dispositivos serão gerenciados no Intune e os outros dispositivos continuarão a ser gerenciados no Configuration Manager. Inicie com um pequeno grupo de usuários de teste para verificar se tudo está funcionando conforme o esperado. Em seguida, você migrará os grupos de usuários adicionais gradualmente até estar pronto para mudar a autoridade de MDM no nível do locatário do Configuration Manager para o Intune autônomo. 

## <a name="things-to-know-before-you-migrate-users"></a>O que você deve saber antes de migrar usuários
- Durante a migração em fases, todas as políticas de MDM ou os aplicativos existentes no Configuration Manager continuam a ser aplicados aos dispositivos de MDM híbrido.
- Os usuários são adicionados a um grupo do AAD que você designa como seu grupo de migração. Todos os dispositivos associados aos usuários no grupo de migração são gerenciados no Intune.
- Os dispositivos que forem adicionados ao grupo do AAD serão ignorados a menos que sejam dispositivos sem um usuário associado.
- Os usuários que não estiverem em um grupo do AAD marcado para migração herdarão automaticamente a autoridade de MDM no nível do locatário (Configuration Manager).
- Quando você migrar um usuário Intune, o usuário e os dispositivos aparecerão no Intune no portal do Azure após cerca de 15 minutos.  
- Depois de migrar usuários para o Intune autônomo, continue a gerenciar as seguintes configurações do Configuration Manager tanto para dispositivos do MDM híbrido quando do Intune autônomo:
    - [Certificado APNs (Apple Push Notification Service)](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac)
    - [Programa de registro de dispositivos](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)
    - Perfis de registro
    - [Licenças VPP (Volume Purchase Program)](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)
    - Identificadores corporativos 
    - [Certificados de assinatura de código](/sccm/mdm/deploy-use/enroll-hybrid-windows)
    - [Categorias de dispositivo](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections)
    - [Gerenciadores de registro](/sccm/mdm/plan-design/device-enrollment-methods)
    - Terms and conditions
    - SLKs do Windows
    - Identidade visual do Portal da Empresa    
      
> [!Important]    
  > Continue a editar as políticas no nível do locatário usando o console do Configuration Manager. Depois de [alterar sua autoridade de MDM no nível do locatário](change-mdm-authority.md) para o Intune, você passará a gerenciar essas políticas no Intune no Azure. 
- É recomendável não migrar as contas de usuário que foram adicionadas como gerenciadores de registro de dispositivo no Configuration Manager. Mais tarde, quando você alterar sua autoridade de MDM no nível do locatário para o Intune, essas contas de usuário serão migradas corretamente. Se você migrar a conta de usuário de gerenciador de registros de dispositivo antes da alteração da autoridade de MDM no nível do locatário, você deverá adicionar o usuário manualmente como um gerenciador de registros de dispositivo no Intune no Azure. No entanto, os dispositivos registrados usando um gerenciador de registros de dispositivo não são migrados com êxito. Você deve chamar o suporte para migrar esses dispositivos. Para obter detalhes, consulte [Adicionar um gerenciador de registros de dispositivo](https://docs.microsoft.com/en-us/intune/device-enrollment-manager-enroll#add-a-device-enrollment-manager).
- Os dispositivos registrados usando um gerenciador de registros de dispositivo e os dispositivos sem usuários associados não são migrados para a nova autoridade de MDM. Para esses dispositivos, é necessário chamar o suporte para ajudá-lo. Não solicite que o suporte execute uma redefinição de autoridade de MDM, pois isso apagaria os dados no Intune. Você deve [alterar sua autoridade de MDM](migrate-change-mdm-authority.md) do console do Configuration Manager.

## <a name="migrate-users-to-intune"></a>Migrar usuários para o Intune
Para testar se suas configurações do Intune estão funcionando conforme o esperado, primeiro migre um pequeno conjunto de usuários e seus dispositivos. Depois de confirmar tudo está funcionando conforme o esperado, você poderá começar a migração de mais grupos do AAD com mais usuários e seus dispositivos.

## <a name="migrate-a-test-group-of-users-to-intune-standalone"></a>Migrar um grupo de teste de usuários para o Intune autônomo
Os dispositivos para os usuários na coleção associada à assinatura do Intune podem ser registrados no MDM híbrido. Quando você remover um usuário da coleção, seus dispositivos registrados serão migrados para o Intune autônomo se o usuário tiver uma licença do Intune atribuída. Se você ainda não tiver atribuído licenças aos usuários que planeja migrar, consulte [Atribuir licenças do Intune a suas contas de usuário](https://docs.microsoft.com/intune/licenses-assign). Na coleção da assinatura do Intune, você pode excluir coleções de usuários da sua coleção principal para migrar os usuários da coleção excluída. 

No exemplo a seguir, a coleção de usuários Híbrido contém todos os membros da coleção de Todos os Usuários. Isso permite que qualquer usuário registre um dispositivo no MDM híbrido. Para migrar os usuários para o Intune autônomo, selecione Excluir Coleções e adicione uma coleção com os usuários a serem migrados. Quando estiver pronto para migrar mais usuários, você poderá adicionar coleções excluídas adicionais que incluam esses usuários. 

![Excluir coleções](../media/migrate-excludecollections.png)

> [!Note] 
> Quando a coleção **Todos os usuários** estiver selecionada para a assinatura do Intune, você não terá permissão para adicionar uma regra para excluir coleções. Crie uma nova coleção com base na coleção **Todos os usuários**, verifique se a coleção contém os usuários esperados e, em seguida, edite a assinatura do Intune para usar a nova coleção. Você pode excluir coleções de usuário da nova coleção para migrar usuários. 

Para migrar um grupo de usuários de teste para o Intune, crie uma coleção de usuários que contenha os usuários a serem migrados e, em seguida, exclua a coleção de usuários da coleção usada para a assinatura do Intune.   

O diagrama a seguir fornece uma visão geral de como funciona a migração de usuários.

 ![Visão geral da autoridade mista](../media/migrate-mixedauthority.svg)

1. Verifique se o usuário tem uma licença do EMS/Intune. 
2. Crie uma coleção a ser excluída da coleção da assinatura do Intune. Neste exemplo, a coleção **Todos os usuários híbridos** contém uma regra para excluir os usuários da coleção **Piloto de migração**. O **User1** é membro da coleção **Piloto de migração** e é excluído da coleção **Todos os usuários híbridos**. 
3. Agora, os dispositivos do **User1** são gerenciados pelo Intune no Portal do Azure. 
4. Todos os outros dispositivos continuam a ser gerenciados no console do Configuration Manager. 

## <a name="verify-intune-standalone-functionality"></a>Verificar a funcionalidade do Intune autônomo
Depois de migrar um pequeno conjunto de usuários, verifique se os dispositivos dos usuários estão listados no Intune. Acesse a folha **Dispositivos** e selecione **Todos os dispositivos**. 

Em seguida, verifique se as políticas, os perfis, os aplicativos, etc. estão funcionando conforme o esperado nos dispositivos do usuário.

## <a name="migrate-additional-users"></a>Migrar usuários adicionais
Depois de verificar que o Intune autônomo está funcionando conforme o esperado, você poderá iniciar a migração de usuários adicionais. Assim como você criou uma coleção com um conjunto de usuários de teste, crie coleções contendo os usuários a serem migrados e exclua essas coleções da coleção associada à assinatura do Intune. Para obter detalhes, consulte [Collection associated with your Intune subscription](#collection-associated-with-your-intune-subscription) (Coleção associada à sua assinatura do Intune).

## <a name="next-steps"></a>Próximas etapas
Depois de migrar usuários e testar a funcionalidades do Intune, considere se você está pronto para [alterar a autoridade de MDM](migrate-change-mdm-authority.md) do locatário do Intune do Configuration Manager para o Intune. 