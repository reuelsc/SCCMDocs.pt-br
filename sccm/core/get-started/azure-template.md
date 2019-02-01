---
title: Criar um laboratório no Azure
titleSuffix: Configuration Manager
description: Automatize a criação de um laboratório do Configuration Manager Technical Preview usando modelos do Azure
ms.date: 01/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9875c443-19bf-43a0-9203-3a741f305096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a6f087b6905d307c707b95e3926a01b0c482f857
ms.sourcegitcommit: b8167a60fd6f2d8387b2db723976c0e2c4198d33
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54832821"
---
# <a name="create-a-configuration-manager-technical-preview-lab-in-azure"></a>Criar um laboratório do Configuration Manager Technical Preview no Azure

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

<!--3556017-->

Este guia descreve como criar um ambiente de laboratório do Configuration Manager no Microsoft Azure. Ele usa os modelos do Azure para simplificar e automatizar a criação de um laboratório usando recursos do Azure. Esse processo instala a versão mais recente do branch do Configuration Manager Technical Preview. 

Para obter mais informações sobre o branch atual do Configuration Manager, confira [Configuration Manager no Azure](/sccm/core/understand/configuration-manager-on-azure).



## <a name="prerequisites"></a>Pré-requisitos

Esse processo requer uma assinatura do Azure na qual você possa criar os seguintes objetos: 
- quatro máquinas virtuais Standard_D2s_v3
- uma conta de armazenamento Standard_LRS

> [!Tip]  
> Consulte a [Calculadora de preços do Azure](https://azure.microsoft.com/pricing/calculator/) para ajudar a determinar os possíveis custos.  



## <a name="process"></a>Processar

1. Acesse o [modelo do Configuration Manager](https://azure.microsoft.com/resources/templates/sccm-technicalpreview/).  

2. Selecione **Implantar no Azure**, que abre o portal do Azure.  

3. Preencha o modelo de início rápido do Azure com as seguintes informações:

    - Informações básicas  

        - **Assinatura**: o nome da assinatura na qual as VMs serão criadas  

        - **Grupo de recursos**: selecione um grupo de recursos a ser usado para essas VMs  

        - **Localização**: selecione um datacenter do Azure para hospedar esse ambiente de laboratório  

    - Configurações  

        - **Prefixo**: o nome de prefixo das máquinas. Para obter mais informações, confira [Informações sobre a VM do Azure](#azure-vm-info).  

        - **Nome do usuário administrador**: o nome de um usuário nas VMs com direitos administrativos. Você pode usar esse usuário para entrar nas VMs.  

        - **Senha de administrador**: A senha precisa atender aos requisitos de complexidade do Azure. Para obter mais informações, confira [adminPassword](https://docs.microsoft.com/rest/api/compute/virtualmachines/createorupdate#osprofile).  

    > [!Important]  
    > As configurações a seguir são exigidas pelo Azure. Use os valores padrão. Não altere esses valores.  
    > 
    > - **\_Local dos artefatos**: o local dos scripts deste modelo <!-- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sccm-technicalpreview/ -->  
    >
    > - **\_Token de SAS do local dos artefatos**: O sasToken é necessário para acessar o local dos artefatos  
    > 
    > - **Localização**: o local de todos os recursos

4. Leia os termos e condições. Se você concordar, marque **Concordo com os termos e condições descritos acima**. Em seguida, selecione **Comprar** para continuar. 

O Azure valida as configurações e, em seguida, começa a implantação. Verifique o status da implantação no portal do Azure. O processo pode levar de 2 a 4 horas. Mesmo quando o portal do Azure mostra uma implantação bem-sucedida, os scripts de configuração continuam a ser executados. Não reinicie as VMs durante o processo.

Para ver o status dos scripts de configuração, conecte-se ao servidor `<prefix>PS1` e exiba o seguinte arquivo: `%windir%\TEMP\ProvisionScript\PS1.json`. Se ele mostrar todas as etapas como concluídas, o processo estará concluído.

Para conectar-se às VMs, primeiro obtenha no portal do Azure os endereços IP públicos de cada VM. Quando você se conectar à VM, o nome de domínio será `contoso.com`. Use as credenciais que você especificou no modelo de implantação. Para obter mais informações, confira [Como se conectar e entrar em uma máquina virtual do Azure que executa o Windows](https://docs.microsoft.com/azure/virtual-machines/windows/connect-logon).



## <a name="azure-vm-info"></a>Informações sobre a VM do Azure

As quatro máquinas virtuais têm as seguintes especificações:
- Standard_D2s_v3, que tem dois núcleos de CPU e 8 GB de memória  
- Windows Server 2016 Datacenter Edition
- 150 GB de espaço em disco
- Um endereço IP público e um privado. Os IPs públicos estão em um grupo de segurança de rede que só permite conexões de área de trabalho remota na porta TCP 3389. 

O prefixo que você especificou no modelo de implantação é o prefixo do nome da VM. Por exemplo, se você definir "contoso" como o prefixo, o nome de computador do controlador de domínio será `contosoDC`.


### `<prefix>DC`

Controlador de domínio do Active Directory

#### <a name="windows-features-and-roles"></a>Recursos e funções do Windows
- ADDS (Active Directory Domain Services)
- .NET
- RDC (Compactação Diferencial Remota)


### `<prefix>PS1`

- SQL Server
- Windows 10 ADK com o Windows PE 
- Site primário do Configuration Manager

#### <a name="windows-features-and-roles"></a>Recursos e funções do Windows
- .NET
- RDC (Compactação Diferencial Remota) 
- IIS (Serviços de Informações da Internet)


### `<prefix>MPDP`

- Ponto de gerenciamento
- Ponto de distribuição

#### <a name="windows-features-and-roles"></a>Recursos e funções do Windows
- .NET
- RDC (Compactação Diferencial Remota) 
- IIS (Serviços de Informações da Internet)
- BITS (Serviço de Transferência Inteligente em Segundo Plano)


### `<prefix>Other`

Essa VM pode ser usada como um cliente ou para hospedar outras funções de site.

#### <a name="windows-features-and-roles"></a>Recursos e funções do Windows
- .NET
- RDC (Compactação Diferencial Remota) 


