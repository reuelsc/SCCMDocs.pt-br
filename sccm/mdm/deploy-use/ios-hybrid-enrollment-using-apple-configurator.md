---
title: "Registrar dispositivos iOS do Apple Configurator – Configuration Manager | Microsoft Docs"
descriptions: Pre-enroll iOS devices by using Apple Configurator with Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61a19d95-83ff-4ad8-9a67-f304d2ba54f2
caps.latest.revision: 5
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 991eff171dce95590a7f050e0d3b07f98c0224b3
ms.openlocfilehash: 6c6e9edbc7b2fca3d1be4feabb238efab80465fa
ms.contentlocale: pt-br
ms.lasthandoff: 01/24/2017


---
# <a name="ios-hybrid-enrollment-using-apple-configurator-with-configuration-manager"></a>Registro híbrido do iOS que usa o Apple Configurator com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As empresas que compram dispositivos iOS para serem usados pelos funcionários podem gerenciá-los usando o Microsoft Intune. Para preparar os dispositivos iOS corporativos para o registro, você deve configurar um perfil de registro no console do Configuration Manager e, em seguida, exportar a URL do perfil para uso pelo Apple Configurator. Você deve preparar o dispositivo iOS para registro ao conectá-lo a um computador Mac com um cabo USB e usar o Apple Configurator para configurá-lo. O alocador do Apple Configurator redefine o dispositivo e adiciona o perfil de registro para que o dispositivo possa ser registrado na primeira vez que o usuário ligar e percorrer o processo do Assistente de Instalação.

O procedimento a seguir é recomendado para dispositivos iOS dedicados que terão um único usuário que usa o dispositivo para acessar o email e os recursos corporativos, como aplicativos e data.  

## <a name="prerequisites"></a>Pré-requisitos  

-   Acesso físico aos dispositivos iOS  

-   Números de série do dispositivo – [Como obter um número de série do iOS](https://support.apple.com/en-us/HT204308)  

-   Computador Mac com o [Apple Configurator 2.0](http://go.microsoft.com/fwlink/?LinkId=518017)  

-   Cabos USB para conectar dispositivos ao seu computador Mac  

## <a name="step-1-add-a-corporate-owned-device-enrollment-profile"></a>Etapa 1: adicionar um perfil de registro de dispositivo corporativo

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Visão Geral** > **Todos os Dispositivos Corporativos** > **iOS** > **Perfis de Registro**. Clique em **Criar Perfil** para abrir o assistente de Criação de Perfil. Defina as configurações nas páginas a seguir:  

2.  Na página **Geral** , especifique as seguintes informações:  

    -   **Nome** (Não é visível para os usuários)  

    -   **Descrição** (Não é visível para os usuários)  

    -   **Afinidade do usuário** – especifica como os dispositivos são registrados. Para a maioria dos cenários do Assistente de Configuração, use **Solicitar afinidade de usuário**.  

        -   **Solicitar a afinidade de usuário**: o dispositivo deve ser afiliado a um usuário durante a configuração inicial e depois poderá receber permissão para acessar os dados e o email da empresa como esse usuário.  

        -   **Nenhuma afinidade de usuário**: O dispositivo não está afiliado a um usuário. Use esta afiliação para dispositivos que executam tarefas sem acessar aos dados de usuário local. Os aplicativos que exigem a afiliação com usuário não funcionarão.

    Clique em **Próximo** para continuar.  

3.  Na página **Programa de Registro do Dispositivo**, deixe a caixa de seleção **Definir configurações do Programa de Registro do Dispositivo para esse perfil** desmarcada e clique em **Avançar**.  

4.  Examine o resumo e, em seguida, clique em **Avançar** para criar o perfil de registro. Clique em **Fechar** para concluir o assistente. Agora você está pronto para adicionar números IMEI ou números de série aos dispositivos que deseja registrar.  

## <a name="step-2-predeclare-devices-to-enroll-with-setup-assistant"></a>Etapa 2: pré-anúncio de dispositivos para registro com o Assistente de Configuração

Nesta etapa, você pré-declara dispositivos corporativos, fornecendo uma lista de identificadores de hardware (IMEI ou números de série).

Para obter mais informações, confira [Pré-declarar dispositivos com número de série do iOS e IMEI](predeclare-devices-with-hardware-id.md). Ao concluir essa tarefa, retorne a esta página para continuar com a próxima etapa.

## <a name="step-3-export-the-profile-to-deploy-to-ios-devices"></a>Etapa 3: exportar o perfil para implantar em dispositivos iOS

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Visão Geral** > **Todos os Dispositivos Corporativos** > **iOS** > **Perfis de Registro**.

2.  Selecione o perfil de registro para implantar em dispositivos móveis e clique em **Exportar…**.

3.  Copie e salve a **URL de Perfil** em um arquivo que você pode editar.   

4.  Para oferecer suporte ao Apple Configurator 2, a URL do perfil 2.0 deve ser editada. Substitua a seguinte parte da URL:  

    ```  
    https://manage.microsoft.com/EnrollmentServer/Discovery.svc/iOS/ESProxy?id=  

    ```  

     por  

    ```  
    https://appleconfigurator2.manage.microsoft.com/MDMServiceConfig?id=  

    ```

5.  Salve a URL de perfil editada. Você a usará para adicionar a URL de perfil de registro no Apple Configurator na [próxima seção](#step-4-prepare-the-device-with-apple-configurator).  

> [!NOTE]
> A URL do perfil de registro é válida por duas semanas a partir de sua exportação. Depois de duas semanas, você deverá exportar uma nova URL para registro de dispositivos iOS.

## <a name="step-4-prepare-the-device-with-apple-configurator"></a>Etapa 4: preparar o dispositivo com o Apple Configurator

Para preparar os dispositivos iOS para registro, é necessário conectar cada dispositivo a um computador Mac e carregar o perfil de registro a eles.  

> [!WARNING]  
>  O Apple Configurator apaga e redefine os dispositivos com as configurações de fábrica.  

1.  Em um computador Mac, abra o **Apple Configurator 2**.  

2.  Na barra de menus, clique em **Apple Configurator 2** > **Preferências**.  

2.  No painel de preferências, selecione **Servidores** e clique no símbolo "+" abaixo do painel esquerdo para iniciar o assistente do Servidor MDM. Clique em **Avançar**.  

3.  Insira o **Nome** e a **URL de Registro** salvos [anteriormente](#step-3-export-the-profile-to-deploy-to-ios-devices). Clique em **Avançar**.  

   > [!NOTE]
   > Se você receber um aviso sobre os requisitos de perfil de confiança da Apple TV, cancele com segurança a opção **Perfil de Confiança** clicando no "X" cinza. Você pode ignorar com segurança qualquer Aviso de certificado de âncora.

   Para continuar, clique em **Avançar** até que o assistente seja concluído.  

4.  No painel **Servidores**, clique em "Editar" ao lado do perfil do novo servidor. Verifique se a URL de Registro corresponde exatamente à URL inserida anteriormente. Insira novamente a URL se ela for diferente e, em seguida, clique em **Salvar**.  

5.  Com um cabo USB, conecte um dispositivo iOS ao computador Mac.  

  > [!WARNING]  
  >  Esse processo redefine os dispositivos com as configurações de fábrica. Antes de conectar o dispositivo, redefina-o e ligue-o. Como uma prática recomendada, o dispositivo deve estar na tela de saudação antes de continuar.  

6.  Clique em **Preparar**. No painel **Preparar o Dispositivo iOS**, selecione **Manual** e clique em **Avançar**.  

7.  No painel **Registrar no Servidor MDM**, selecione o nome do servidor que você criou e, em seguida, clique em **Avançar**.  

9. No painel **Criar uma Organização**, escolha a **Organização** ou crie uma nova organização e clique em **Avançar**.  

10. No painel **Configurar o Assistente de Configuração do iOS**, escolha as etapas apresentadas ao usuário e clique em **Preparar**. Se receber uma solicitação, autentique para atualizar as configurações de confiança.  

11. Quando terminar, você pode desconectar o cabo USB.  

Repita essas etapas para todos os dispositivos que você deseja preparar para o registro.

## <a name="step-5-distribute-devices"></a>Etapa 5: distribuir dispositivos

Os dispositivos agora estão prontos para o registro corporativo. Desligue os dispositivos e distribua-os aos usuários. Quando o dispositivo for ativado, o Assistente de Configuração iniciará e solicitará ao usuário sua conta corporativa ou de estudante para iniciar o registro.

