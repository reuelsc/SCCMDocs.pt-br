---
title: Windows Autopilot para dispositivos existentes
titleSuffix: Configuration Manager
description: Siga esta sequência de tarefas do Configuration Manager para refazer a imagem e provisionar um dispositivo Windows 7 para o modo orientado pelo usuário do Windows Autopilot
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 2e96f847-5b5a-4da9-8e8f-6aa488838508
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6878e36e5bf20774f6eef1ee855dda2f95dabfb4
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 03/07/2019
ms.locfileid: "57557990"
---
# <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot para dispositivos existentes
<!--3607717, fka 1358333-->

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O [Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) fornece uma maneira para as organizações enviarem dispositivos Windows 10 novos, sem uso, diretamente ao usuário final e definir o fluxo de provisionamento que o usuário deverá seguir para ter um dispositivo Windows 10 produtivo e seguro. O dispositivo está registrado com serviço Windows Autopilot para que você possa atribuir o perfil do Windows Autopilot necessário. Esse perfil define a experiência de configuração inicial do usuário (OOBE) naquele dispositivo. 

O [Windows Autopilot para dispositivos existentes](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) está disponível com o Windows 10, versão 1809 ou posterior. Esse recurso permite refazer a imagem e provisionar um dispositivo Windows 7 para o [modo orientado pelo usuário do Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) usando uma única sequência de tarefas nativa do Configuration Manager. 



## <a name="prerequisites"></a>Pré-requisitos

- Adquira a mídia de instalação para o Windows 10, versão 1809 ou posterior. Em seguida, crie uma imagem do sistema operacional do Configuration Manager. Para obter mais informações, confira [Gerenciar imagens do sistema operacional](/sccm/osd/get-started/manage-operating-system-images).

- No Microsoft Intune, crie perfis para o Windows Autopilot. Para saber mais, confira [Registrar dispositivos Windows no Intune usando Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot).

- Um dispositivo que ainda não está registrado no serviço Windows Autopilot. Se o dispositivo já estiver registrado, o perfil atribuído terá precedência. O piloto automático para o perfil de dispositivos existente se aplica somente se que o perfil online expira.



## <a name="create-the-configuration-file"></a>Criar o arquivo de configuração

1. Em um dispositivo Windows com acesso à internet, abra uma janela administrativa de comando do PowerShell e execute os seguintes comandos:  

    1. Instale os módulos necessários e aceite os prompts para continuar  
        ``` PowerShell  
        Install-Module AzureAD
        Install-Module WindowsAutopilotIntune 
        Import-Module WindowsAutopilotIntune 
        ```

    2. Entre no Intune com as credenciais de administrador  
        ``` PowerShell  
        Connect-AutopilotIntune 
        ```

    3. Recupere todos os perfis do Windows Autopilot associados ao seu locatário do Intune  
        ``` PowerShell  
        $AutopilotProfile = Get-AutopilotProfile
        ```

    4. Crie um arquivo de configuração para cada perfil. Os arquivos são nomeados com o nome de exibição do perfil e são salvos na área de trabalho do usuário atual.<!--PowerShell example courtesy of GitHub user treestryder from SCCMDocs issue #1196-->  
        ``` PowerShell  
        $AutopilotProfile | ForEach-Object { $_ | ConvertTo-AutoPilotConfigurationJSON | Set-Content -Encoding Ascii "~\Desktop\$($_.displayName).json" }
        ```  

        > [!Note]  
        > O arquivo de configuração pode conter somente um perfil. Cada perfil deve estar dentro de chaves `{}`.  

2. Salve um dos perfis em um arquivo codificado em ANSI denominado **AutopilotConfigurationFile.json**. Salve-o em um local adequado como uma fonte de pacote do Configuration Manager.  

    > [!Tip]  
    > Se você usar o cmdlet do PowerShell **Out-File** ​​para redirecionar a saída JSON para um arquivo, ele usará a codificação Unicode por padrão. Esse cmdlet também poderá truncar as linhas longas. Use o cmdlet **Set-Content** com o parâmetro `-Encoding ASCII` para definir a codificação de texto correta.   
    > 
    > O Bloco de Notas do Windows usa codificação ANSI por padrão.  

3. Crie um pacote do Configuration Manager que contenha esse arquivo. Ele não exige um programa. Saiba mais em [Criar um pacote](/sccm/apps/deploy-use/packages-and-programs#create-a-package-and-program).  

    > [!NOTE]  
    > O Windows requer que esse arquivo se chame **AutopilotConfigurationFile.json**. Para usar mais de um perfil do Autopilot, crie pacotes separados do Configuration Manager.  



## <a name="create-the-task-sequence"></a>Criar a sequência de tarefas

1. No console do Configuration Manager, acesse o espaço de trabalho **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione o nó **Sequências de Tarefas**. Selecione **Criar Sequência de Tarefas** na faixa de opções.  

2. Na página **Criar nova sequência de tarefas**, selecione a opção para **Implantar o Windows Autopilot em dispositivos existentes**.  

3. Na página **Informações da Sequência de Tarefas**, especifique um nome, adicione uma descrição (opcional) e selecione uma imagem de inicialização. Saiba mais sobre versões de imagens de inicialização compatíveis em [Suporte para Windows 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).  

4. Na página **Instalar Windows**, selecione o **Pacote de imagem** do Windows 10. Em seguida, defina as seguintes configurações:  

    - **Índice de imagens**: selecione Enterprise, Education ou Professional, conforme exigido pela sua organização  

    - Habilite a opção para **Particionar e formatar o computador de destino antes de instalar o sistema operacional**  

    - **Configure a sequência de tarefas para uso com o Bitlocker**: se você habilitar essa opção, a sequência de tarefas inclui as etapas necessárias para habilitar o Bitlocker  

    - **Chave do produto**: se você precisar especificar uma chave de produto para ativação do Windows, insira-a aqui  

    - Selecione uma das opções a seguir para configurar a conta de administrador local no Windows 10:  
        - **Gere a senha do administrador local aleatoriamente e desabilite a conta em todas as plataformas com suporte (recomendado)**
        - **Habilitar a conta e especificar a senha do administrador local**

5. Na página **Configurar Rede**, selecione a opção para **Ingressar em um grupo de trabalho**. Esta sequência de tarefas usa a ferramenta de preparação do sistema Windows (sysprep). Se o dispositivo tiver ingressado em um domínio, o sysprep falhará.  

6. Na página **Instalar o Configuration Manager**, inclua todas as propriedades de instalação necessárias para o seu ambiente.  

    > [!Tip]  
    > A sequência de tarefas precisará apenas dessas informações se os componentes do cliente do Configuration Manager forem necessários durante a sequência de tarefas antes da execução do sysprep. Por exemplo, para instalar as atualizações de software ou aplicativos. Se você não estiver fazendo essas ações, o cliente não será necessário. Ele será desinstalado antes de a sequência de tarefas executar o sysprep.  

7. A página **Incluir atualizações** seleciona a opção para **Não instalar nenhuma atualização de software** por padrão.  

    > [!Tip]  
    > Use a manutenção de imagens offline para manter a imagem atualizada com as atualizações de qualidade mais recentes do Windows 10. Saiba mais em [Aplicar atualizações de software a uma imagem do sistema operacional](/sccm/osd/get-started/manage-operating-system-images#BKMK_OSImagesApplyUpdates).  

8. Na página **Instalar aplicativos**, é possível selecionar os aplicativos que devem ser instalados durante a sequência de tarefas. No entanto, a Microsoft recomenda que você espelhe a abordagem de imagem de assinatura com esse cenário. Após as provisões de dispositivo com o Autopilot, aplique todos os aplicativos e configurações do cogerenciamento do Microsoft Intune ou do Configuration Manager. Esse processo fornece uma experiência consistente entre usuários que recebem novos dispositivos e aqueles que usam o Windows Autopilot para dispositivos existentes.  

8. Na página **Preparação do Sistema**, selecione o pacote que inclui o arquivo de configuração do Autopilot. Por padrão, a sequência de tarefas reinicia o computador depois que ele executa o Sysprep do Windows. Você também pode selecionar a opção para **Desligar o computador após a conclusão dessa sequência de tarefas**. Essa opção permite preparar um dispositivo e, em seguida, fornecê-lo a um usuário para uma experiência consistente com o Autopilot.  

9. Conclua o assistente.  

Se você editar a sequência de tarefas, será semelhante à sequência de tarefas padrão para aplicar uma imagem do sistema operacional existente. Essa sequência de tarefas inclui as seguintes etapas adicionais:  

- **Aplicar a configuração do Windows Autopilot**: esta etapa aplica o arquivo de configuração do Autopilot do pacote especificado. Não é um novo tipo de etapa, é uma etapa para **Executar a linha de comando** para copiar o arquivo.  

- **Preparar o Windows para captura**: esta etapa executa o Windows Sysprep e inclui a nova opção para **Desligar o computador depois de executar essa ação**. Para obter mais informações, consulte [Preparar o Windows para Captura](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareWindowsforCapture).  

A sequência de tarefas do Windows Autopilot para dispositivos existentes faz com que um dispositivo ingresse no Azure Active Directory (Azure AD). 

Use a [movimentação de pasta conhecida](https://docs.microsoft.com/onedrive/redirect-known-folders) do OneDrive for Business para garantir que seja feito o backup dos dados do usuário antes da atualização do Windows 10.



## <a name="next-steps"></a>Próximas etapas

Use o cogerenciamento para aprimorar os recursos de gerenciamento dos dispositivos Windows 10. O segundo caminho para o cogerenciamento é por meio do provisionamento moderno com o Windows Autopilot. Para obter mais informações, consulte os seguintes artigos:

- [O que é cogerenciamento?](/sccm/comanage/overview)
- [Caminhos para o cogerenciamento](/sccm/comanage/quickstart-paths)
- [Windows Autopilot com cogerenciamento](/sccm/comanage/quickstart-autopilot)

