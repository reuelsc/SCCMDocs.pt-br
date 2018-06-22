---
title: Criar e implantar uma política do Windows Defender Application Guard
titleSuffix: Configuraton Manager
description: Crie e implante uma política do Windows Defender Application Guard.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e7f0a1ccb71abb2fec27e0430bd4195dc85aceae
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32348065"
---
# <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Criar e implantar políticas do Windows Defender Application Guard 
*Aplica-se a: System Center Configuration Manager (Branch Atual)*
<!-- 1351960 -->
Você pode criar e implantar políticas do [Windows Defender Application Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview) usando a proteção de ponto de extremidade do Configuration Manager. Essas políticas ajudam a proteger os usuários por meio da abertura de sites não confiáveis em um contêiner isolado seguro que não pode ser acessado pelas outras partes do sistema operacional.

## <a name="prerequisites"></a>Pré-requisitos

Para criar e implantar uma política do Windows Defender Application Guard, é necessário usar o Windows 10 Fall Creators Update (1709). Além disso, os dispositivos Windows 10 nos quais você implantará a política deverão ser configurados com uma política de isolamento de rede. Para obter mais informações, consulte a [Visão geral do Windows Defender Application Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview). 


## <a name="create-a-policy-and-to-browse-the-available-settings"></a>Crie uma política e para procurar as configurações disponíveis:

1. No console do Configuration Manager, escolha **Ativos e Conformidade**.
2. No espaço de trabalho **Ativos e Conformidade**, escolha **Visão Geral** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. Na guia **Início**, no grupo **Criar**, clique em **Criar Política do Windows Defender Application Guard**.
4. Usando o [artigo](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard) como referência, você pode procurar e definir as configurações disponíveis. O Configuration Manager permite que você defina algumas configurações de política. Consulte [Configurações de interação de host](#BKMK_HIS) e [Comportamento do aplicativo](#BKMK_AppB).
5. Na página **Definição de Rede**, especifique a identidade corporativa e defina o limite da rede corporativa.

    > [!NOTE]
    > Os computadores Windows 10 armazenam apenas uma lista de isolamento de rede no cliente. Você pode criar dois tipos diferentes de listas de isolamento de rede e implantá-los no cliente:
    >
    >  - uma da Proteção de Informações do Windows
    >  - e uma do Windows Defender Application Guard
    >
    > Se você implantar as duas políticas, essas listas de isolamento de rede deverão ser correspondentes. Se você implantar listas que não correspondem ao mesmo cliente, a implantação falhará. Para obter mais informações, consulte a [Documentação da Proteção de Informações do Windows](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).
    > 
    > 

6. Quando terminar, conclua o assistente e implante a política em um ou mais dispositivos Windows 10 1709.

### <a name="bkmk_HIS"></a> Configurações de interação de host
Configura as interações entre os dispositivos de host e o contêiner do Application Guard. Antes do Configuration Manager versão 1802, o comportamento do aplicativo e a interação de host estavam localizados na guia **Configurações**.

- **Área de Transferência** – Em configurações anteriores ao Configuration Manager 1802
    - Tipo de conteúdo permitido
        - Texto
        - Imagens
- **Impressão:**
    - Habilitar impressão em XPS
    - Habilitar impressão em PDF
    - Habilitar impressão nas impressoras locais
    - Habilitar impressão nas impressoras de rede
- **Elementos gráficos:** (a partir do Configuration Manager versão 1802)
    - Acesso ao processador gráfico virtual
- **Arquivos:** (a partir do Configuration Manager versão 1802)
    - Salvar os arquivos baixados no host

### <a name="bkmk_ABS"></a> Configurações de comportamento do aplicativo
Configura o comportamento do aplicativo na sessão do Application Guard. Antes do Configuration Manager versão 1802, o comportamento do aplicativo e a interação de host estavam localizados na guia **Configurações**.

- **Conteúdo:**
   - Os sites empresariais podem carregar o conteúdo não corporativo, como plug-ins de terceiros.
- **Outros:**
    - Manter os dados do navegador gerados pelo usuário
    - Auditar eventos de segurança na sessão isolada do Application Guard



## <a name="next-steps"></a>Próximas etapas
Para ler mais sobre o Windows Defender Application Guard: [Visão geral do Windows Defender Application Guard](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview).
[Perguntas frequentes sobre o Windows Defender Application Guard](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/faq-wd-app-guard).
