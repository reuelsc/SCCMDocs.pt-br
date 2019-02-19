---
title: Alterar a autoridade de MDM
titleSuffix: Configuration Manager
description: Saiba como alterar a autoridade MDM do MDM híbrido para Intune autônomo para usuários específicos (autoridade de MDM mista).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 11/14/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 6f0201d7-5714-4ba0-b2bf-d1acd0203e9a
ms.collection: M365-identity-device-management
ms.openlocfilehash: b7f2875852b49ab8af9b1f34c4747f12a6620896
ms.sourcegitcommit: fd16fc2b681608fd6def5bad2cedffbcd1f2423a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/18/2019
ms.locfileid: "56405668"
---
# <a name="change-the-mdm-authority-for-specific-users-mixed-mdm-authority"></a>Alterar a autoridade de MDM para usuários específicos (autoridade de MDM mista) 

*Aplica-se a: System Center Configuration Manager (Branch Atual)*    

Você pode configurar uma autoridade de MDM mista no mesmo locatário. Gerenciar alguns usuários no Microsoft Intune e outros com o MDM híbrido. Este artigo fornece informações sobre como começar a mover usuários para o Intune autônomo. Ele pressupõe que você concluiu as etapas a seguir:  

- Usado a ferramenta de importação de dados para [Importar objetos do Configuration Manager para o Intune](migrate-import-data.md) (opcional).  

- [Preparar o Intune para migração do usuário](migrate-prepare-intune.md) a fim de garantir que os usuários e respectivos dispositivos continuem sendo gerenciados depois da migração.  

> [!Note]    
> Uma reinicialização completa do seu locatário remove todas as políticas, aplicativos e registros de dispositivo. Se você decidir que deseja fazer esse processo, contate o suporte para obter assistência.  

Gerencie usuários migrados e seus dispositivos no Intune. Continue a gerenciar outros dispositivos no Configuration Manager. Para verificar se tudo está funcionando conforme o esperado, inicie com um pequeno grupo de teste de usuários. Em seguida, migre grupos de usuários adicionais gradualmente. Quando você estiver pronto, mude a autoridade MDM de nível de locatário do Configuration Manager para o Intune autônomo. 

> [!Important]  
> A partir de 13 de agosto de 2018, o gerenciamento de dispositivos móveis híbrido é um [recurso preterido](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para saber mais, confira [O que é o MDM híbrido](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## <a name="things-to-know-before-you-migrate-users"></a>O que você deve saber antes de migrar usuários

- Durante a migração em fases, todas as políticas de MDM ou os aplicativos existentes no Configuration Manager continuam a ser aplicados aos dispositivos de MDM híbrido.  

- Os dispositivos para os usuários na coleção associada à assinatura do Intune podem ser registrados no MDM híbrido. Todos os dispositivos associados aos usuários que não estão na coleção são gerenciados no Intune, contanto que o usuário tenha uma licença do Intune/EMS.   

    > [!Note]  
    > Os usuários podem se inscrever no Intune autônomo, mesmo que você os tenha bloqueado por meio do console do Configuration Manager. Para bloquear completamente o registro de um usuário, não licencie os usuários indesejados para o Intune. Eles não podem se inscrever sem uma licença.<!--SCCMDocs issue 738-->  

- Quando você migrar um usuário Intune, o usuário e os dispositivos aparecerão no Intune no Portal do Azure após cerca de 15 minutos.   

- Depois de migrar usuários para o Intune autônomo, continue a gerenciar as seguintes configurações do Configuration Manager tanto para dispositivos do MDM híbrido quando do Intune autônomo:  

    - [Certificado APNs (Apple Push Notification Service)](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac)  

    - [Programa de registro de dispositivos](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)  

        > [!Note]  
        > Você não precisa recriar seu token de DEP ou removê-lo do Configuration Manager. Ele migra automaticamente para o Intune 24 horas após você alterar autoridade do MDM do locatário do Configuration Manager para o Intune. Essa alteração é a etapa final na migração. (Se o token de DEP não migrar dentro de 24 horas, contate o suporte da Microsoft para obter assistência.)  

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
  > Continue a editar as políticas no nível do locatário usando o console do Configuration Manager. Depois que você [alterar sua autoridade MDM do nível do locatário](/sccm/mdm/deploy-use/change-mdm-authority) ao Intune, as políticas de nível de locatário que eram gerenciados no Configuration Manager automaticamente migrar para o Intune no Azure. É um exemplo de tal uma política para certificados do Apple Push Notification service (APNs).<!--SCCMDocs issue #971-->  

-   Se você usar certificados com assinatura de código, recomendamos que você migre os usuários em uma abordagem em fases. Depois que um dispositivo móvel é migrado, ele faz uma solicitação de autoridade de certificação para um novo certificado. Ao usar uma abordagem em fases para migrar usuários (e seus dispositivos), ela limita o número de solicitações simultâneas de autoridade de certificação.  

- Não migre contas de usuário que foram adicionadas como gerenciadores de registro de dispositivo (DEM) no Configuration Manager. Mais tarde, quando você alterar sua autoridade de MDM no nível do locatário para o Intune, essas contas de usuário serão migradas corretamente. Se você migrar a conta de usuário do DEM antes da alteração de autoridade MDM de nível de locatário, você deve adicionar manualmente o usuário como um DEM no Intune no Azure. No entanto, dispositivos registrados usando um DEM não migrem com êxito. Entre em contato com o suporte para migrar esses dispositivos. Para saber mais, confira [Adicionar um gerenciador de registro de dispositivo](https://docs.microsoft.com/intune/device-enrollment-manager-enroll#add-a-device-enrollment-manager).  

    > [!Note]  
    > Enquanto estiver no modo de autoridade mista, não mova essas contas para o Intune removendo-as da coleção de nuvem do ConfigMgr. Se você fizer isso, o usuário se tornará um usuário padrão e não poderá inscrever mais de 15 dispositivos. Em vez disso, migre esses usuários e seus dispositivos assim que você alternar totalmente a autoridade do MDM para o locatário.<!--Intune bug 2174210-->  

- Dispositivos registrados usando um DEM e dispositivos sem [afinidade do usuário](/sccm/mdm/deploy-use/user-affinity-for-hybrid-managed-devices) não são migradas automaticamente para a nova autoridade MDM. Para alternar a autoridade de gerenciamento para esses dispositivos MDM, confira [Migrar dispositivos sem afinidade de usuário](#migrate-devices-without-user-affinity).  



## <a name="migrate-users-to-intune"></a>Migrar usuários para o Intune

Para testar se suas configurações do Intune estão funcionando conforme o esperado, primeiro migre um pequeno conjunto de usuários e seus dispositivos. Depois de confirmar tudo está funcionando conforme o esperado, você poderá começar a migração de mais grupos do AAD com mais usuários e seus dispositivos.



## <a name="migrate-a-test-group-of-users-to-intune-standalone"></a>Migrar um grupo de teste de usuários para o Intune autônomo

Os dispositivos para os usuários na coleção associada à assinatura do Intune podem ser registrados no MDM híbrido. Quando você remove um usuário da coleção, se o usuário tiver uma licença do Intune atribuída, seus dispositivos registrados são migrados para o Intune autônomo. Se você ainda não tiver atribuído licenças aos usuários que você planeja migrar, consulte [atribuir licenças do Intune às contas de usuário](https://docs.microsoft.com/intune/licenses-assign). Na coleção da assinatura do Intune, você pode excluir coleções de usuários da sua coleção principal para migrar os usuários da coleção excluída. 

No exemplo a seguir, a coleção de usuários Híbrido contém todos os membros da coleção de Todos os Usuários. Essa configuração permite que qualquer usuário registre um dispositivo no MDM híbrido. Para migrar os usuários para o Intune autônomo, selecione Excluir Coleções e adicione uma coleção com os usuários a serem migrados. Quando estiver pronto para migrar mais usuários, adicione coleções excluídas adicionais que contenham esses usuários. 

![Excluir coleções](../media/migrate-excludecollections.png)

> [!Note]  
> Quando você tiver o **todos os usuários** coleção selecionada para a assinatura do Intune, você não tiver permissão para adicionar uma regra para excluir coleções. Criar uma nova coleção com base nas **todos os usuários** coleção. Verifique se a coleção contém os usuários que você espera. Em seguida, edite a assinatura do Intune para usar a nova coleção. Você pode excluir coleções de usuário da nova coleção para migrar usuários.  

Para migrar um grupo de usuários de teste para o Intune, crie uma coleção de usuário que contém os usuários para migrar. Em seguida, exclua a coleção de usuários da coleção que é usada para a assinatura do Intune.   

O diagrama a seguir fornece uma visão geral de como funciona a migração de usuários.

 ![Visão geral da autoridade mista](../media/migrate-mixedauthority.svg)

1. Verifique se o usuário tem uma licença do EMS/Intune.   

2. Crie uma coleção a ser excluída da coleção da assinatura do Intune. Neste exemplo, a coleção **Todos os usuários híbridos** contém uma regra para excluir os usuários da coleção **Piloto de migração**. O **User1** é membro da coleção **Piloto de migração** e é excluído da coleção **Todos os usuários híbridos**.  

3. Agora, os dispositivos do **User1** são gerenciados pelo Intune no Portal do Azure.   

4. Todos os outros dispositivos continuam a ser gerenciados no console do Configuration Manager.  



## <a name="verify-intune-standalone-functionality"></a>Verificar a funcionalidade do Intune autônomo

Depois de migrar um pequeno conjunto de usuários, verifique se os dispositivos dos usuários estão listados no Intune. Acesse **Dispositivos** e selecione **Todos os dispositivos**. 

Em seguida, verifique se as políticas, os perfis e os aplicativos estão funcionando conforme o esperado nos dispositivos dos usuários.



## <a name="migrate-additional-users"></a>Migrar usuários adicionais

Depois de verificar que o Intune autônomo está funcionando conforme o esperado, inicie a migração de usuários adicionais. Assim como você criou uma coleção com um conjunto de usuários de teste, crie coleções que incluem usuários a serem migrados. Exclua essas coleções da coleção que está associada com a assinatura do Intune. Para obter detalhes, consulte [Collection associated with your Intune subscription](#collection-associated-with-your-intune-subscription) (Coleção associada à sua assinatura do Intune).



## <a name="migrate-devices-without-user-affinity"></a>Migrar dispositivos sem afinidade de usuário

Para migrar o formulário de dispositivos individuais do Configuration Manager para Intune que foram registrados sem afinidade do usuário, use o cmdlet Switch-MdmDeviceAuthority do PowerShell.  Depois de migrar dispositivos selecionados usando o cmdlet, validar no Intune no Azure que a migração ocorreu como esperado para os dispositivos selecionados. Em seguida, quando você estiver pronto, altere a autoridade de MDM para o Intune do locatário para concluir a migração de todos os dispositivos restantes com o Configuration Manager como sua autoridade de MDM.

### <a name="cmdlet-switch-mdmdeviceauthority"></a>Cmdlet *Switch-MdmDeviceAuthority*

#### <a name="synopsis"></a>SYNOPSIS
O cmdlet alterna a autoridade de gerenciamento de dispositivos MDM sem afinidade de usuário (por exemplo, dispositivos registrados em lite). O cmdlet alterna entre o Intune e Configuration Manager autoridades de gerenciamento. Ele muda para os dispositivos especificados com base nas autoridades de gerenciamento, quando você executar o cmdlet.

### <a name="syntax"></a>SINTAXE
`Switch-MdmDeviceAuthority -DeviceIds <Guid[]> [-Credential <PSCredential>] [-Force] [-LogFilePath <string>] [-LoggingLevel {Off | Critical | Error | Warning | Information | Verbose | ActivityTracing | All}] [-Confirm] [-WhatIf] [<CommonParameters>]`


### <a name="parameters"></a>PARÂMETROS
#### `-Credential <PSCredential>`
Um objeto de credencial do PowerShell para a conta de usuário do Azure AD que é usado ao alternar as autoridades de gerenciamento de dispositivo. Se o parâmetro não for especificado, o usuário é solicitado para credenciais. A função do diretório para esta conta de usuário deve ser um **Administrador global** ou um **Administrador limitado** com a função administrativa de **Administrador do Intune**.

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
Solicita sua confirmação antes de executar o comando.
 
#### `-WhatIf [<SwitchParameter>]`
Descreve o que aconteceria se você executasse o comando sem realmente executar o comando.
 
#### `<CommonParameters>`
Esse cmdlet oferece suporte a parâmetros comuns: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer, PipelineVariable e OutVariable. Para obter mais informações, veja [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

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

Depois de migrar usuários e testar a funcionalidade do Intune, considere se você está pronto para [alterar a autoridade de MDM](migrate-change-mdm-authority.md) do locatário do Intune do Configuration Manager para o Intune. 
