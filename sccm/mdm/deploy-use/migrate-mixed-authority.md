---
title: Alterar a autoridade de MDM para usuários específicos (autoridade de MDM mista)
titleSuffix: Configuration Manager
description: Saiba como alterar a autoridade de MDM do MDM híbrido para Intune autônomo somente para alguns usuários.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 6f0201d7-5714-4ba0-b2bf-d1acd0203e9a
ms.openlocfilehash: 46fb1333c58f3010acde4d064044a124050d211a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="change-the-mdm-authority-for-specific-users-mixed-mdm-authority"></a>Alterar a autoridade de MDM para usuários específicos (autoridade de MDM mista) 

*Aplica-se a: System Center Configuration Manager (Branch Atual)*    

É possível configurar uma autoridade de MDM mista no mesmo locatário selecionando alguns usuários a serem gerenciados no Intune e outros para serem gerenciados com o MDM híbrido (Intune integrado ao Configuration Manager). Este artigo fornece informações de como começar a mover usuários para o Intune autônomo e considera que você tenha concluído as etapas a seguir:
- Usado a ferramenta de importação de dados para [Importar objetos do Configuration Manager para o Intune](migrate-import-data.md) (opcional).
- [Preparou o Intune para migração do usuário](migrate-prepare-intune.md) a fim de garantir que os usuários e respectivos dispositivos continuem sendo gerenciados depois que forem migrados.

> [!Note]    
> Se você decidir que deseja fazer uma reinicialização completa do seu locatário, o que remove todas as políticas, aplicativos e registros de dispositivos, contate o suporte para obter assistência.

Os usuários migrados e seus dispositivos são gerenciados no Intune e os outros dispositivos continuam a ser gerenciados no Configuration Manager. Inicie com um pequeno grupo de usuários de teste para verificar se tudo está funcionando conforme o esperado. Em seguida, migre os grupos de usuários adicionais gradualmente até estar pronto para mudar a autoridade de MDM no nível do locatário do Configuration Manager para o Intune autônomo. 

## <a name="things-to-know-before-you-migrate-users"></a>O que você deve saber antes de migrar usuários
- Durante a migração em fases, todas as políticas de MDM ou os aplicativos existentes no Configuration Manager continuam a ser aplicados aos dispositivos de MDM híbrido.
- Os dispositivos para os usuários na coleção associada à assinatura do Intune podem ser registrados no MDM híbrido. Todos os dispositivos associados aos usuários que não estão na coleção são gerenciados no Intune, contanto que o usuário tenha uma licença do Intune/EMS. 
- Quando você migrar um usuário Intune, o usuário e os dispositivos aparecerão no Intune no Portal do Azure após cerca de 15 minutos.  
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
-   Se você usar certificados com assinatura de código, recomendamos que você migre os usuários em uma abordagem em fases. Depois que um dispositivo móvel é migrado, ele faz uma solicitação de autoridade de certificação para um novo certificado. Ao usar uma abordagem em fases para migrar usuários (e seus dispositivos), ela limita o número de solicitações simultâneas de autoridade de certificação.
- É recomendável não migrar as contas de usuário que foram adicionadas como gerenciadores de registro de dispositivo no Configuration Manager. Mais tarde, quando você alterar sua autoridade de MDM no nível do locatário para o Intune, essas contas de usuário serão migradas corretamente. Se você migrar a conta de usuário de gerenciador de registros de dispositivo antes da alteração da autoridade de MDM no nível do locatário, você deverá adicionar o usuário manualmente como um gerenciador de registros de dispositivo no Intune no Azure. No entanto, os dispositivos registrados usando um gerenciador de registros de dispositivo não são migrados com êxito. Você deve chamar o suporte para migrar esses dispositivos. Para obter detalhes, consulte [Adicionar um gerenciador de registros de dispositivo](https://docs.microsoft.com/en-us/intune/device-enrollment-manager-enroll#add-a-device-enrollment-manager).
- Os dispositivos registrados usando um gerenciador de registros de dispositivo, e os dispositivos sem [afinidade de usuário](/sccm/mdm/deploy-use/user-affinity-for-hybrid-managed-devices) não serão migrados automaticamente para a nova autoridade de MDM. Para alternar a autoridade de gerenciamento para esses dispositivos MDM, confira [Migrar dispositivos sem afinidade de usuário](#migrate-devices-without-user-affinity).

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

## <a name="migrate-devices-without-user-affinity"></a>Migrar dispositivos sem afinidade de usuário
Os dispositivos registrados usando um gerenciador de registros de dispositivo, e os dispositivos sem [afinidade de usuário](/sccm/mdm/deploy-use/user-affinity-for-hybrid-managed-devices) não serão migrados automaticamente para a nova autoridade de MDM. Use o cmdlet do PowerShell *Switch-MdmDeviceAuthority* para alternar entre as autoridades de gerenciamento do Intune e do Configuration Manager nos cenários a seguir: 

-   Cenário 1: Use o cmdlet *Switch-MdmDeviceAuthority* para migrar os dispositivos selecionados e validar a possibilidade de gerenciá-los usando o Intune no Azure. Depois, quando tudo estiver pronto, [altere a autoridade de MDM para o Intune do locatário](migrate-change-mdm-authority.md) para completar a migração dos dispositivos. 
-   Cenário 2: quando você estiver pronto para alterar a autoridade de MDM para o Intune do locatário, execute estas ações para migrar seus dispositivos sem afinidade do usuário:
    - Use o cmdlet para alterar a autoridade de MDM de seus dispositivos sem afinidade do usuário antes de [alterar a autoridade de para o Intune do locatário](migrate-change-mdm-authority.md).    
    - Entre em contato com o suporte para que os dispositivos sem afinidade de usuário sejam trocados após a alteração da autoridade de MDM para o Intune do locatário.

Para alternar a autoridade de gerenciamento desses dispositivos MDM, use o cmdlet *Switch-MdmDeviceAuthority* para alternar entre as autoridades de gerenciamento do Intune e do Configuration Manager. 

### <a name="cmdlet-switch-mdmdeviceauthority"></a>Cmdlet *Switch-MdmDeviceAuthority*

#### <a name="synopsis"></a>SINOPSE
O cmdlet alterna a autoridade de gerenciamento de dispositivos MDM sem afinidade de usuário (por exemplo, dispositivos registrados em lite). O cmdlet alterna entre as autoridades de gerenciamento do Intune e do Configuration Manager para os dispositivos especificados com base nas autoridades de gerenciamento ao executar o cmdlet.

### <a name="syntax"></a>SINTAXE
`Switch-MdmDeviceAuthority -DeviceIds <Guid[]> [-Credential <PSCredential>] [-Force] [-LogFilePath <string>] [-LoggingLevel {Off | Critical | Error | Warning | Information | Verbose | ActivityTracing | All}] [-Confirm] [-WhatIf] [<CommonParameters>]`


### <a name="parameters"></a>PARÂMETROS
#### `-Credential <PSCredential>`
Um objeto de credencial do PowerShell para a conta de usuário do Azure AD que é usado ao alternar as autoridades de gerenciamento de dispositivo. As credenciais serão solicitadas ao usuário se o parâmetro não for especificado. A função do diretório para esta conta de usuário deve ser um **Administrador global** ou um **Administrador limitado** com a função administrativa de **Administrador do Intune**.

#### `-DeviceIds <Guid[]>`
As IDs dos dispositivos de MDM que precisam ter sua autoridade de gerenciamento alternada. As IDs de dispositivo são identificadores exclusivos para os dispositivos exibidos pelo console do Configuration Manager.

#### `-Force [<SwitchParameter>]`
Especifique um parâmetro para desabilitar o prompt Deve Continuar.<br>
 
#### `-LogFilePath <string>`
Caminho para o local do arquivo de log.
 
#### `-LoggingLevel <SourceLevels>`
O nível de log é usado para determinar o tipo dos logs que precisam ser gravados no arquivo de log.
 
Esses são os valores possíveis para LoggingLevel:

  - ActivityTracing
  - Todos
  - Crítico
  - Erro
  - Informações
  - Desativar
  - Detalhado
  - Aviso
 
#### `-Confirm [<SwitchParameter>]`
Solicita a sua confirmação antes de executar o comando.
 
#### `-WhatIf [<SwitchParameter>]`
Descreve o que aconteceria se você executasse o comando, sem chegar a executá-lo de verdade.
 
#### `<CommonParameters>`
Este cmdlet dá suporte a parâmetros comuns: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer, PipelineVariable e OutVariable. Para obter mais informações, veja [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

### <a name="example-1"></a>Exemplo 1

``` powershell
C:\PS>Switch-MdmDeviceAuthority -Credential $creds -DeviceIds $deviceIds
 
  DeviceId       : 62e6ea43-18f8-4278-bcd4-a4baed2c6d24
  Success        : True
  FailureReason  :
  NewAuthority   : Intune
  CompletionTime : 11/15/2017 8:00:11 PM
 
Description
 
-----------
 
Successfully switched the management authority of the device from Configuration Manager to Intune.
```

### <a name="remarks"></a>COMENTÁRIOS
- Para ver os exemplos, digite: `get-help Switch-MdmDeviceAuthority -examples`  
- Para obter mais informações, digite: `get-help Switch-MdmDeviceAuthority -detailed`  
- Para obter informações técnicas, digite: `get-help Switch-MdmDeviceAuthority -full`  
- Para obter ajuda online, digite: `get-help Switch-MdmDeviceAuthority -online`   


## <a name="next-steps"></a>Próximas etapas
Depois de migrar usuários e testar a funcionalidades do Intune, considere se você está pronto para [alterar a autoridade de MDM](migrate-change-mdm-authority.md) do locatário do Intune do Configuration Manager para o Intune. 