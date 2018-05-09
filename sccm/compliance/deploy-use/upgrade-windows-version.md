---
title: Atualizar dispositivos do Windows para uma versão diferente
titleSuffix: Configuration Manager
description: Atualize automaticamente os dispositivos que executam o Windows 10 Desktop ou Windows 10 Mobile para outra edição com o Configuration Manager.
ms.date: 01/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0c15e919978ae8458f426511dd9a0e6d7c311b4b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="upgrade-windows-devices-with-the-edition-upgrade-policy-in-system-center-configuration-manager"></a>Atualizar dispositivos Windows com a política de atualização de edição no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


A **Política de Atualização de Edição** lhe permite atualizar automaticamente os dispositivos que executem uma das seguintes versões do Windows 10 para uma edição diferente:

- Windows 10 Desktop
- Windows 10 Mobile

Há suporte para os seguintes caminhos de atualização:

- Do Windows 10 Pro para Windows 10 Enterprise
- Do Windows 10 Home para Windows 10 Education
- Do Windows 10 Mobile para Windows 10 Mobile Enterprise

Os dispositivos devem ser registrados no Microsoft Intune ou executar o software cliente do Configuration Manager. Essa política não é compatível no momento com PCs gerenciados por MDM local.

## <a name="before-you-start"></a>Antes de começar  
 Antes de começar a atualizar os dispositivos para a versão mais recente, examine os seguintes pré-requisitos:  

-   Para edições de área de trabalho do Windows 10: uma chave de produto válida para a nova versão do Windows em todos os dispositivos aos quais você destinará a política. Essa chave de produto pode ser uma MAK (chave de ativação múltipla) ou uma GVLK (chave genérica de licenciamento por volume). Uma GVLK também é conhecida como uma chave de instalação de cliente do KMS (Serviço de Gerenciamento de Chaves). Para obter mais informações, consulte [Planejar a ativação de volume](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Para obter uma lista de chaves de instalação de cliente do KMS, veja o [Apêndice A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) do guia de ativação do Windows Server. <!--496871-->  

-   Para Windows 10 Mobile: um arquivo de licença em XML do VLSC (Centro de Serviços de Licenciamento por Volume da Microsoft). Este arquivo contém as informações de licenciamento para a nova versão do Windows em todos os dispositivos que você destinar a política.

- Para gerenciar este tipo de política, você deve estar na função de segurança **Administrador Completo** do Configuration Manager.

## <a name="configure-the-edition-upgrade-policy"></a>Configurar a política de atualização de edição  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Configurações de Conformidade** > **Atualização da Edição do Windows 10**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Política de Atualização de Edição**.  

4.  Clique em **Criar Política**.  

5.  Na página **Geral** do **Assistente de Criação de Política de Atualização de Edição**, especifique as seguintes informações:  

    -   **Nome** – Insira um nome para a política de atualização de edição  

    -   **Descrição** (opcional) – Opcionalmente, digite uma descrição para a política, ajudando a identificá-la no console do Intune  

    -   **SKU para o qual atualizar o dispositivo** – na lista suspensa, selecione a edição de destino do Windows 10 Desktop ou Windows 10 Mobile  

    -   **Informações de licença** - Selecione um destes:  

        -   **Chave do produto** – Insira uma chave de produto válida para a edição de destino do Windows 10 Desktop  

            > [!NOTE]  
            >  Depois de criar uma política que contém uma chave do produto (Product Key), não é possível editar a chave do produto (Product Key) mais tarde. O Configuration Manager obscurece a chave por motivos de segurança. Para alterar a chave do produto (Product Key), você deve reinserir a chave inteira.  

        -   **Arquivo de licença** – Clique em **Procurar** para selecionar um arquivo de licença válido no formato XML. O Configuration Manager usa esse arquivo de licença para atualizar dispositivos Windows 10 Mobile.  

6.  Conclua o assistente.  


## <a name="deploy-the-edition-upgrade-policy"></a>Implantar a política de atualização de edição  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Configurações de Conformidade** > **Atualização da Edição do Windows 10**.  

3.  Selecione a política de atualização de edição do Windows 10 que deseja implantar e, na guia **Início** , no grupo **Implantação** , clique em **Implantar**.  

4.  Primeiro, na caixa de diálogo **Implantar Atualização da Edição do Windows 10**, escolha a coleção à qual você deseja implantar a política. Selecione o agendamento pelo qual o cliente avaliará a política e, em seguida, clique em **OK**. Para PCs gerenciados com o cliente do Configuration Manager, você deve implantar a política para uma coleção de dispositivos. Para computadores que são registrados com o Intune, você pode implantar a política a um usuário ou uma coleção de dispositivos. 



## <a name="next-steps"></a>Próximas etapas

Monitore essa implantação através do nó **Implantações** do espaço de trabalho **Monitoramento**. Se você encontrar erros indicando uma implantação malsucedida, por exemplo:
- **Não aplicável para este dispositivo**
- **Falha na conversão do tipo de dados**

Esses erros não significam que a implantação falhou. Verifique se a atualização foi executada com êxito no PC de destino.

Após avaliar a política de destino, o cliente será reiniciado dentro de duas horas a fim de aplicar a atualização. Certifique-se de informar os usuários nos quais você implanta a política ou agende a política para ser executada fora do horário de trabalho dos usuários.

Se o seguinte erro aparecer no **DcmWmiProvider.log** no cliente, verifique se você está usando a chave correta para seu cenário de ativação. Para obter mais informações, consulte a seção [Antes de começar](#before-you-start). Se você estiver usando um serviço de gerenciamento de chaves para a ativação, use uma [chave de instalação de cliente do KMS](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys).  <!-- 496871 -->   

`Failed to execute CheckApplicabilityMethod with error = 0x80041001 OsEditionUpgradeProvider`
