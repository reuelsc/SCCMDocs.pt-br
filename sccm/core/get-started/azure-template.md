---
title: Criar um laboratório no Azure
titleSuffix: Configuration Manager
description: Automatizar a criação de um laboratório da visualização técnica do Configuration Manager ou do laboratório de avaliação de branch atual usando modelos do Azure
ms.date: 07/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9875c443-19bf-43a0-9203-3a741f305096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0c4c565d3c1754ce60ec8f9b7d5dcd2d487f8db1
ms.sourcegitcommit: cdad3ca82018f1755e5186f8949a898cd201b565
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68411488"
---
# <a name="create-a-configuration-manager-lab-in-azure"></a>Criar um laboratório do Configuration Manager no Azure

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

<!--3556017-->

Este guia descreve como criar um ambiente de laboratório do Configuration Manager no Microsoft Azure. Ele usa os modelos do Azure para simplificar e automatizar a criação de um laboratório usando recursos do Azure. Dois modelos do Azure são fornecidos: 

- O modelo do Azure da visualização técnica do Configuration Manager instala a versão mais recente do branch da visualização técnica do Configuration Manager.
- O modelo do Azure do branch atual do Configuration Manager instala a avaliação da versão mais recente do branch atual do Configuration Manager. 

Para saber mais, consulte [Configuration Manager no Azure](/sccm/core/understand/configuration-manager-on-azure).



## <a name="prerequisites"></a>Pré-requisitos

Esse processo requer uma assinatura do Azure na qual você possa criar os seguintes objetos: 
- Duas máquinas virtuais Standard_B2s para o Controlador de Domínio e funções do pacote de gerenciamento e do ponto de distribuição.
- Uma máquina virtual Standard_B2ms para o Servidor Primário de Site e para o servidor de banco de dados do SQL.
- uma conta de armazenamento Standard_LRS

> [!Tip]  
> Consulte a [Calculadora de preços do Azure](https://azure.microsoft.com/pricing/calculator/) para ajudar a determinar os possíveis custos.  



## <a name="process"></a>Processar

1. Vá para o [modelo da visualização técnica do Configuration Manager](https://azure.microsoft.com/resources/templates/sccm-technicalpreview/) ou [modelo do branch atual do Configuration Manager](https://azure.microsoft.com/resources/templates/sccm-currentbranch/).  

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
    > - **\_Local dos artefatos**: A localização dos scripts para este modelo <!-- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sccm-technicalpreview/ -->  
    >
    > - **\_Token de SAS do local dos artefatos**: O sasToken é necessário para acessar o local dos artefatos  
    > 
    > - **Localização**: o local de todos os recursos

4. Leia os termos e condições. Se você concordar, marque **Concordo com os termos e condições descritos acima**. Em seguida, selecione **Comprar** para continuar. 

O Azure valida as configurações e, em seguida, começa a implantação. Verifique o status da implantação no portal do Azure. O processo pode levar de 2 a 4 horas. Mesmo quando o portal do Azure mostra uma implantação bem-sucedida, os scripts de configuração continuam a ser executados. Não reinicie as VMs durante o processo.

Para ver o status dos scripts de configuração, conecte-se ao servidor `<prefix>PS1` e exiba o seguinte arquivo: `%windir%\TEMP\ProvisionScript\PS1.json`. Se ele mostrar todas as etapas como concluídas, o processo estará concluído.

Para conectar-se às VMs, primeiro obtenha no portal do Azure os endereços IP públicos de cada VM. Quando você se conectar à VM, o nome de domínio será `contoso.com`. Use as credenciais que você especificou no modelo de implantação. Para obter mais informações, confira [Como se conectar e entrar em uma máquina virtual do Azure que executa o Windows](https://docs.microsoft.com/azure/virtual-machines/windows/connect-logon).



## <a name="azure-vm-info"></a>Informações sobre a VM do Azure

Todas as três VMs possuem as seguintes especificações:
- 150 GB de espaço em disco
- Um endereço IP público e um privado. Os IPs públicos estão em um grupo de segurança de rede que só permite conexões de área de trabalho remota na porta TCP 3389. 

O prefixo que você especificou no modelo de implantação é o prefixo do nome da VM. Por exemplo, se você definir "contoso" como o prefixo, o nome de computador do controlador de domínio será `contosoDC`.


### `<prefix>DC01`

- Controlador de domínio do Active Directory
- Standard_B2s, que tem dois núcleos de CPU e 4 GB de memória
- Windows Server 2019 Datacenter Edition

#### <a name="windows-features-and-roles"></a>Recursos e funções do Windows
- ADDS (Active Directory Domain Services)
- .NET
- RDC (Compactação Diferencial Remota)


### `<prefix>PS01`

- Standard_B2ms, que tem dois núcleos de CPU e 8 GB de memória
- Windows Server 2016 Datacenter Edition
- SQL Server
- Windows 10 ADK com o Windows PE 
- Site primário do Configuration Manager

#### <a name="windows-features-and-roles"></a>Recursos e funções do Windows
- .NET
- RDC (Compactação Diferencial Remota) 
- IIS (Serviços de Informações da Internet)


### `<prefix>DPMP01`

- Standard_B2s, que tem dois núcleos de CPU e 4 GB de memória
- Windows Server 2019 Datacenter Edition
- Ponto de distribuição
- Ponto de gerenciamento

#### <a name="windows-features-and-roles"></a>Recursos e funções do Windows
- .NET
- RDC (Compactação Diferencial Remota) 
- IIS (Serviços de Informações da Internet)
- BITS (Serviço de Transferência Inteligente em Segundo Plano)

### `<prefix>CL01`

- Somente para o modelo de avaliação do branch atual do Configuration Manager
- Windows 10
- Cliente do Configuration Manager
