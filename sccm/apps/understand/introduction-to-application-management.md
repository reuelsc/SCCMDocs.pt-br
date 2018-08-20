---
title: Introdução ao gerenciamento de aplicativos
titleSuffix: Configuration Manager
description: Descubra as informações básicas que você precisará para gerenciar e implantar aplicativos do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 70ab4136f39b4bf559c3d460ca1528bb4de0f6e1
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384283"
---
# <a name="introduction-to-application-management-in-configuration-manager"></a>Introdução ao gerenciamento de aplicativos no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Neste artigo, você aprenderá os conceitos básicos para começar a trabalhar com aplicativos do Configuration Manager.  

> [!TIP]  
>  Se você já sabe como gerenciar aplicativos no Configuration Manager, ignore este artigo. Passe para a criação de um aplicativo de exemplo: [Criar e implantar um aplicativo](/sccm/apps/get-started/create-and-deploy-an-application).  



## <a name="what-is-an-application"></a>O que é um aplicativo?  

Embora *aplicativo* seja um termo amplamente usado em computação, no Configuration Manager ele tem um significado específico. Pense em um aplicativo como uma caixa. Essa caixa contém um ou mais conjuntos de arquivos de instalação para um pacote de software (conhecido como um *tipo de implantação*), além de instruções sobre como implantar o software.  

Quando você implanta o aplicativo em dispositivos, os **requisitos** decidem que tipo de implantação o Configuration Manager instalará no dispositivo.  

Você pode fazer muito mais com um aplicativo. Você saberá mais à medida que lê este guia. As seções a seguir apresentam alguns conceitos que você precisará saber antes de começar a obter detalhes:  

#### <a name="deployment-type"></a>Tipo de implantação
Se o *aplicativo* é a caixa, o *tipo de implantação* é o conjunto de conteúdo na caixa. Um aplicativo precisa de pelo menos um tipo de implantação, pois ela determina como instalar o aplicativo. Use mais de um tipo de implantação para configurar um conteúdo e um programa de instalação diferentes para o mesmo aplicativo. 

Por exemplo, sua empresa tem um aplicativo de linha de negócios chamado Astoria. Os desenvolvedores do aplicativo fornecem uma das seguintes maneiras de instalar o aplicativo:
- Pacote do Windows Installer para funcionalidade completa em dispositivos Windows 10
- Um pacote do App-V para ser usado no farm de servidores de terminal
- Um pacote do aplicativo do Android para usuários móveis  

Você cria um único aplicativo para o Astoria no Configuration Manager. O aplicativo define os metadados de alto nível sobre o aplicativo que são comuns a todos os métodos de instalação e plataformas. Em seguida, você cria três tipos de implantação para os métodos de instalação disponíveis e implanta o aplicativo para todos os usuários. Com base nos requisitos e em outras configurações dos tipos de implantação, o Configuration Manager determina o método certo em cada caso de uso. 

Para obter mais informações, consulte [Criar tipos de implantação para o aplicativo](/sccm/apps/deploy-use/create-applications#bkmk_create-dt).

#### <a name="requirements"></a>requisitos
Nas versões anteriores do Configuration Manager, criava-se uma coleção de dispositivos na qual o aplicativo era implantado. Embora você ainda possa criar uma coleção, use os *requisitos* para especificar critérios mais detalhados para uma implantação de aplicativo.

Por exemplo, especificar que um aplicativo só pode ser instalado em dispositivos que executam o Windows 10. Quando você implantar o aplicativo em todos os seus dispositivos, ele somente será instalado nos dispositivos que executam o Windows 10.

O Configuration Manager avalia os requisitos para determinar se ele deve instalar um aplicativo e seus tipos de implantação. Em seguida, ele determina o tipo de implantação correto pelo qual instalar um aplicativo. A cada sete dias, por padrão, o cliente do Configuration Manager reavalia as regras de requisitos para determinar a conformidade de acordo com a configuração do cliente **Agendar reavaliação de implantações**.

Para obter mais informações, confira [Criar e implantar um aplicativo](/sccm/apps/get-started/create-and-deploy-an-application) e [Requisitos de tipo de implantação](/sccm/apps/deploy-use/create-applications#bkmk_dt-require).

#### <a name="global-conditions"></a>Condições globais
Embora os requisitos sejam usados com um tipo de implantação específico em um único aplicativo, também é possível criar *condições globais*. Essas condições são uma biblioteca de requisitos predefinidos que você pode usar com qualquer aplicativo e o tipo de implantação. O Configuration Manager inclui um conjunto de condições globais internas ou você também pode criar suas próprias condições. 

Para obter mais informações, confira [Criar condições globais](/sccm/apps/deploy-use/create-global-conditions).

#### <a name="simulated-deployment"></a>Implantação simulada
Uma *implantação simulada* avalia os requisitos, o método de detecção e as dependências de um aplicativo. Um cliente relata os resultados sem realmente instalar o aplicativo. 

Para saber mais, confira [Simular implantações de aplicativos](/sccm/apps/deploy-use/simulate-application-deployments).  

#### <a name="deployment-action"></a>Ação de implantação
Uma *ação de implantação* especifica se você deseja instalar ou desinstalar o aplicativo que está implantando. Nem todos os tipos de implantação dão suporte para a ação de desinstalação. 

Para obter informações, confira [Deploy applications](/sccm/apps/deploy-use/deploy-applications) (Implantar aplicativos).  

#### <a name="deployment-purpose"></a>Finalidade da implantação
A *finalidade da implantação* especifica se o aplicativo de implantação é **Obrigatório** ou está **Disponível**:  

- O cliente instala automaticamente uma implantação *Obrigatória* de acordo com o agendamento que você define. Quando o aplicativo não está oculto, os usuários podem acompanhar o status da implantação. Eles também podem usar o Centro de Software para instalar o aplicativo antes da data limite.  

- Se você implantar o aplicativo para um usuário como *Disponível*, o usuário o verá no Centro de Software e poderá solicitá-lo sob demanda.  

Para obter informações, confira [Deploy applications](/sccm/apps/deploy-use/deploy-applications) (Implantar aplicativos).  

#### <a name="revisions"></a>Revisões
Quando você faz *revisões* em um aplicativo ou tipo de implantação, o Configuration Manager cria uma nova versão do aplicativo. Execute as seguintes ações no console do Configuration Manager: 
- Exibir o histórico de cada revisão do aplicativo
- Exibir suas propriedades
- Restaurar uma versão anterior de um aplicativo
- Excluir uma versão antiga

Para obter mais informações, confira [Atualizar e desativar aplicativos](/sccm/apps/deploy-use/update-and-retire-applications).  

#### <a name="detection-method"></a>Método de detecção
Use *métodos de detecção* para descobrir se um dispositivo já instalou um aplicativo. Se o método de detecção indica que o aplicativo já está instalado, o Configuration Manager não tenta instalá-lo novamente.

Para obter mais informações, confira [Opções de método de detecção de tipo de implantação](/sccm/apps/deploy-use/create-applications##bkmk_dt-detect).

#### <a name="dependencies"></a>Dependências
As *dependências* definem um ou mais tipos de implantação de outro aplicativo que o cliente precisa instalar antes de instalar esse tipo de implantação. 

Para obter mais informações, confira [Dependências de tipo de implantação](/sccm/apps/deploy-use/create-applications#bkmk_dt-depend).  

#### <a name="supersedence"></a>Substituição
O Configuration Manager permite atualizar ou substituir os aplicativos existentes usando uma relação de *substituição*. Ao substituir um aplicativo, você especifica um novo tipo de implantação para substituir o tipo de implantação do aplicativo substituído. Você também pode decidir se atualiza ou desinstala o aplicativo substituído antes que o cliente instale o aplicativo substituto.

Para mais informações, consulte [Substituição de aplicativos](/sccm/apps/deploy-use/revise-and-supersede-applications#application-supersedence).  

#### <a name="user-centric-management"></a>Gerenciamento centrado no usuário
Os aplicativos do Configuration Manager dão suporte ao *gerenciamento centrado em usuário*, o que permite associar usuários específicos a dispositivos específicos. Em vez de precisar se lembrar do nome de um dispositivo do usuário, implante aplicativos para o usuário e para o dispositivo. Essa funcionalidade ajuda a garantir que os aplicativos mais importantes estejam sempre disponíveis em cada um dos dispositivos do usuário. Se um usuário adquire um novo computador, o Configuration Manager instala automaticamente seus aplicativos no dispositivo antes que ele entre. 

Para obter mais informações, confira [Vincular usuários e dispositivos com afinidade de dispositivo de usuário](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).  



## <a name="what-application-types-can-you-deploy"></a>Quais tipos de aplicativos posso implantar?  

O Configuration Manager permite que você implante os seguintes tipos de aplicativos:  

- Windows Installer (MSI)  

- Pacote do aplicativo do Windows (appx ou. appxbundle)  

    > [!Note]  
    > Começando na versão 1806, esse tipo inclui os novos formatos de pacote do aplicativo (msix) e lote de aplicativo (msixbundle) do Windows 10.<!--1357427-->  

- Pacote do aplicativo do Windows na Microsoft Store  

- Microsoft App-V v4 e v5  

- macOS  


Além disso, quando você gerencia dispositivos por meio do gerenciamento de dispositivo local do Microsoft Intune ou do Configuration Manager, é possível gerenciar mais estes tipos de aplicativo:  

- Pacote do aplicativo do Windows Phone (xap)  

- Pacote do aplicativo do Windows Phone na Microsoft Store  

- Pacote do aplicativo para iOS (ipa)  

- Pacote do aplicativo para iOS da Loja de Aplicativos  

- Pacote do aplicativo para Android (APK)  

- Pacote de aplicativo para Android no Google Play  

- Windows Installer por meio do MDM (MSI)  

- Aplicativo Web



## <a name="state-based-applications"></a>Aplicativos baseados em estado  

Os aplicativos do Configuration Manager usam monitoramento baseado em estado. Você pode acompanhar o último estado de implantação de aplicativo de usuários e dispositivos. Essas mensagens de estado exibem informações sobre dispositivos individuais. Por exemplo, ao implantar um aplicativo em uma coleção de usuários, você pode exibir o estado de conformidade da implantação e a finalidade da implantação no console do Configuration Manager. Monitore a implantação de software do espaço de trabalho **monitoramento** no console do Configuration Manager. Para obter mais informações, consulte [Monitor applications (Monitorar aplicativos)](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

Regularmente, o cliente do Configuration Manager reavalia as implantações de aplicativos. Por exemplo:  

- Um usuário desinstala um aplicativo implantado. No próximo ciclo de avaliação, o Configuration Manager detecta que o aplicativo não está presente. O cliente reinstala o aplicativo automaticamente.  

- O Configuration Manager não instalou um aplicativo em um dispositivo porque ele não atendeu aos requisitos. Mais adiante, uma alteração é feita ao dispositivo e agora ele atende aos requisitos. O Configuration Manager detecta essa alteração e o cliente instala o aplicativo.  

Você pode definir o intervalo de reavaliação de implantações de aplicativo. Use a configuração do cliente **Agendar reavaliação de implantações** no grupo **Implantação de software**. Para obter mais informações, consulte [Sobre as configurações do cliente](/sccm/core/clients/deploy/about-client-settings#software-deployment).  



## <a name="get-started-creating-an-application"></a>Introdução à criação de um aplicativo  

Se você quiser começar imediatamente a criar um aplicativo, acesse um passo a passo no artigo [Criar e implantar um aplicativo](/sccm/apps/get-started/create-and-deploy-an-application).  

Se você já está familiarizado com os conceitos básicos e deseja obter mais informações de referência sobre todas as opções disponíveis, comece a [Criar aplicativos](/sccm/apps/deploy-use/create-applications).  



## <a name="software-center"></a>Centro de software  

O Centro de Software é um aplicativo do Windows instalado com o cliente do Configuration Manager. Use-o para as seguintes ações:  
- Procurar e solicitar aplicativos implantados no dispositivo ou no usuário
- Instalar e agendar instalações de software
- Exibir o status de instalação de aplicativos, as atualizações de software e os sistemas operacionais
- Definir as configurações de controle remoto
- Configurar o gerenciamento de energia

Para obter mais informações, consulte os seguintes artigos:  
- [Planejar e configurar o gerenciamento de aplicativos](/sccm/apps/plan-design/plan-for-and-configure-application-management)
- [Guia do usuário do Centro de Software](/sccm/core/understand/software-center)

> [!Note]  
> A função de ponto de serviços Web do catálogo de aplicativos não é mais necessária no 1806, mas ainda é uma função com suporte. 
> 
> Não há suporte para a função de site do Catálogo de Aplicativos na versão 1806. Para saber mais, consulte [Recursos removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  



## <a name="packages-and-programs"></a>Pacotes e programas  

O Configuration Manager continua dando suporte a pacotes e programas usados nas versões anteriores do produto. 

Para obter mais informações, consulte [Pacotes e programas](/sccm/apps/deploy-use/packages-and-programs).  



## <a name="next-steps"></a>Próximas etapas

Agora que você entende os conceitos básicos do gerenciamento de aplicativos no Configuration Manager, continue nos os seguintes artigos:
- [Criar e implantar um aplicativo de exemplo](/sccm/apps/get-started/create-and-deploy-an-application)
- [Planejar e configurar o gerenciamento de aplicativos](/sccm/apps/plan-design/plan-for-and-configure-application-management)
- [Criar aplicativos](/sccm/apps/deploy-use/create-applications)
