---
title: Deployment Monitoring Tool
titleSuffix: Configuration Manager
description: Use a Ferramenta de Monitoramento da Implantação para solucionar problemas de implantações de software em um cliente do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9edc214f-f405-456d-80df-8adcc2a5428d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2188ce295f999b392166c99133822ad8fc1e441e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125231"
---
# <a name="deployment-monitoring-tool"></a>Deployment Monitoring Tool

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A Ferramenta de Monitoramento da Implantação é uma dos [ferramentas do Configuration Manager](/sccm/core/support/tools). É uma interface gráfica do usuário criada para ajudar na solução de problemas de aplicativo, na atualização de software e em implantações de linha de base de configuração em um cliente do Configuration Manager. A ferramenta é somente leitura, pois não altera nenhum estado no cliente. Você pode usá-la com segurança para diagnosticar os cenários comuns de implantação.


## <a name="features"></a>Recursos

- Execute-a como um administrador para solucionar problemas de implantações em um cliente local.  

- Solucione problemas de implantações em um cliente remoto. Inicialize a ferramenta e conecte-se a um computador remoto como administrador.  

- Exporte para XML todos os dados coletados na ferramenta. Compartilhe o arquivo XML com outras pessoas e use-o como uma plataforma comum para falar sobre solução de problemas de implantações.  

- Importe dados exportados anteriormente para um computador diferente e use-os para executar a ferramenta no modo offline.   


## <a name="usage"></a>Uso

A Ferramenta de Monitoramento de Implantação dá suporte apenas à interface gráfica do usuário. Para inicializar a ferramenta, execute **DeploymentMonitoringTool.exe** como administrador. Há três modos de exibição:  

- **Propriedades do Cliente**: uma lista de atributos úteis sobre o dispositivo e o cliente do Configuration Manager. Este modo de exibição é o padrão.   

- **Implantações**: exibir todas as implantações de destino no momento. Selecione uma implantação no painel de resultados para exibir mais informações no painel de detalhes.  

- **Todas as Atualizações**: exibir todas as atualizações de software e seus status.  

Para copiar dados em qualquer modo de exibição, selecione uma célula e pressione **CTRL** + **C**.


### <a name="actions-menu"></a>Menu de ações

As seguintes ações estão disponíveis no menu **Ações**:  

- **Conectar ao computador remoto**: selecione um computador ao qual se conectar. Quando você não especificar um nome de usuário e senha, ele usará as credenciais atuais. Clique em **Salvar** para se conectar ao computador remoto.  

- **Exportar Dados**: selecione o arquivo no qual gravar os dados e, em seguida, clique em **Salvar**. Use o arquivo XML exportado para a solução de problemas remota em um computador diferente.  

- **Importar Dados**: selecione um arquivo para importar para a ferramenta.  

- **Exibir Log**: abre um arquivo de log associado, dependendo do modo de exibição:  
    - Propriedades do Cliente: `\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Implantações: `\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Todas as atualizações: `C:\Windows\WindowsUpdate.log`



## <a name="see-also"></a>Consulte também

- [Implantar aplicativos](/sccm/apps/deploy-use/deploy-applications)
- [Implantar atualizações de software](/sccm/sum/deploy-use/deploy-software-updates)
- [Implantar linhas de base de configuração](/sccm/compliance/deploy-use/deploy-configuration-baselines)
