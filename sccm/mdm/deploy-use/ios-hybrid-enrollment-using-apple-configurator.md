---
title: 'Registrar dispositivos iOS com o Apple Configurador '
titleSuffix: Configuration Manager
descriptions: Pre-enroll iOS devices by using Apple Configurator with Configuration Manager.
ms.date: 08/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 61a19d95-83ff-4ad8-9a67-f304d2ba54f2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b07fc7bf1c4a226456506d0131c3d6bad14b1766
ms.sourcegitcommit: a6a6507e01d819217208cfcea483ce9a2744583d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2019
ms.locfileid: "66748225"
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

## <a name="add-a-corporate-owned-device-enrollment-profile"></a>Adicionar um perfil de registro de dispositivo corporativo

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Visão Geral** > **Todos os Dispositivos Corporativos** > **iOS** > **Perfis de Registro**. Clique em **Criar Perfil** para abrir o assistente de Criação de Perfil. Defina as configurações nas páginas a seguir:  

2.  Na página **Geral** , especifique as seguintes informações:  

    -   **Nome** (Não é visível para os usuários)  

    -   **Descrição** (Não é visível para os usuários)  

    -   **Afinidade do usuário** – especifica como os dispositivos são registrados. Para a maioria dos cenários do Assistente de Configuração, use **Solicitar afinidade de usuário**.  

        -   **Solicitar afinidade do usuário**: O dispositivo deve ser afiliado a um usuário durante a instalação inicial e, em seguida, poderá receber permissão para acessar dados da empresa e o email como esse usuário.  

        -   **Sem afinidade de usuário**: O dispositivo não está afiliado a um usuário. Use esta afiliação para dispositivos que executam tarefas sem acessar aos dados de usuário local. Os aplicativos que exigem a afiliação com usuário não funcionarão.

    Clique em **Próximo** para continuar.  

3.  Na página **Programa de Registro do Dispositivo**, deixe a caixa de seleção **Definir configurações do Programa de Registro do Dispositivo para esse perfil** desmarcada e clique em **Avançar**.  

4.  Examine o resumo e, em seguida, clique em **Avançar** para criar o perfil de registro. Clique em **Fechar** para concluir o assistente. Agora você está pronto para adicionar números IMEI ou números de série aos dispositivos que deseja registrar.  

## <a name="predeclare-devices-to-enroll-with-setup-assistant"></a>Pré-declarar dispositivos para registro com o Assistente de Configuração

Nesta etapa, você pré-declara dispositivos corporativos, fornecendo uma lista de identificadores de hardware (IMEI ou números de série).

Para obter mais informações, confira [Pré-declarar dispositivos com número de série do iOS e IMEI](predeclare-devices-with-hardware-id.md). Ao concluir essa tarefa, retorne a esta página para continuar com a próxima etapa.

## <a name="export-the-profile-to-deploy-to-ios-devices"></a>Exportar o perfil para implantar em dispositivos iOS

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Visão Geral** > **Todos os Dispositivos Corporativos** > **iOS** > **Perfis de Registro**.

2.  Selecione o perfil de registro para implantar em dispositivos móveis e clique em **Exportar…** .

3.  Copie e salve a **URL de Perfil** em um arquivo que você pode editar.   

4.  Para oferecer suporte ao Apple Configurator 2, a URL do perfil 2.0 deve ser editada. Substitua a seguinte parte da URL:  

    ```  
    https://manage.microsoft.com/EnrollmentServer/Discovery.svc/iOS/ESProxy?id=  

    ```  

     por  

    ```  
    https://appleconfigurator2.manage.microsoft.com/MDMServiceConfig?id=  

    ```

5.  Salve a URL de perfil editada. Você a usará para adicionar a URL de perfil de registro no Apple Configurator na [próxima seção](#prepare-the-device-with-apple-configurator).  

> [!NOTE]
> A URL do perfil de registro é válida por duas semanas a partir de sua exportação. Depois de duas semanas, você deverá exportar uma nova URL para registro de dispositivos iOS.

## <a name="prepare-the-device-with-apple-configurator"></a>Preparar o dispositivo com o Apple Configurator

Para preparar os dispositivos iOS para registro, é necessário conectar cada dispositivo a um computador Mac e carregar o perfil de registro a eles.  

> [!WARNING]  
>  O Apple Configurator apaga e redefine os dispositivos com as configurações de fábrica.  

1. Em um computador Mac, abra o **Apple Configurator 2**.  

2. Na barra de menus, clique em **Apple Configurator 2** > **Preferências**.  

3. No painel de preferências, selecione **Servidores** e clique no símbolo "+" abaixo do painel esquerdo para iniciar o assistente do Servidor MDM. Clique em **Avançar**.  

4. Insira o **Nome** e a **URL de Registro** salvos [anteriormente](#export-the-profile-to-deploy-to-ios-devices). Clique em **Avançar**.  

   > [!NOTE]
   > Se você receber um aviso sobre os requisitos de perfil de confiança da Apple TV, cancele com segurança a opção **Perfil de Confiança** clicando no "X" cinza. Você pode ignorar com segurança qualquer Aviso de certificado de âncora.

   Para continuar, clique em **Avançar** até que o assistente seja concluído.  

5. No painel **Servidores**, clique em "Editar" ao lado do perfil do novo servidor. Verifique se a URL de Registro corresponde exatamente à URL inserida anteriormente. Insira novamente a URL se ela for diferente e, em seguida, clique em **Salvar**.  

6. Com um cabo USB, conecte um dispositivo iOS ao computador Mac.  

   > [!WARNING]  
   >  Esse processo redefine os dispositivos com as configurações de fábrica. Antes de conectar o dispositivo, redefina-o e ligue-o. Como uma prática recomendada, o dispositivo deve estar na tela de saudação antes de continuar.  

7. Clique em **Preparar**. No painel **Preparar o Dispositivo iOS**, selecione **Manual** e clique em **Avançar**.  

8. No painel **Registrar no Servidor MDM**, selecione o nome do servidor que você criou e, em seguida, clique em **Avançar**.  

9. No painel **Criar uma Organização**, escolha a **Organização** ou crie uma nova organização e clique em **Avançar**.  

10. No painel **Configurar o Assistente de Configuração do iOS**, escolha as etapas apresentadas ao usuário e clique em **Preparar**. Se receber uma solicitação, autentique para atualizar as configurações de confiança.  

11. Quando terminar, você pode desconectar o cabo USB.  

Repita essas etapas para todos os dispositivos que você deseja preparar para o registro.

## <a name="distribute-devices"></a>Distribuir dispositivos

Os dispositivos agora estão prontos para o registro corporativo. Desligue os dispositivos e distribua-os aos usuários. Quando o dispositivo for ativado, o Assistente de Configuração iniciará e solicitará ao usuário sua conta corporativa ou de estudante para iniciar o registro.
