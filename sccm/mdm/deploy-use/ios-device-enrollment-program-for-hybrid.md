---
title: 'Registrar dispositivos iOS com o Programa de registro de dispositivos (DEP) '
titleSuffix: Configuration Manager
description: Habilite o registro no DEP (Programa de Registro de Dispositivos) do iOS para implantações híbridas no Configuration Manager com o Intune.
ms.date: 09/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 78d44adc-9b1c-4bc6-b72d-e93873916ea6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4628dd18ed865088c68cf38810e984a18f0ba0ad
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53422208"
---
# <a name="ios-device-enrollment-program-dep-enrollment-for-hybrid-deployments-with-configuration-manager"></a>Registro no DEP (Programa de Registro de Dispositivos) do iOS para implantações híbridas com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch atual)*

As empresas podem adquirir dispositivos iOS por meio do programa de registro de dispositivo da Apple e, em seguida, gerenciá-los usando o Microsoft Intune. Para gerenciar dispositivos iOS de propriedade corporativa com o DEP (Programa de Registro de Dispositivo) da Apple, as empresas devem concluir as etapas com a Apple para participar do programa e adquirir dispositivos por meio desse programa. Detalhes do processo estão disponíveis em: [https://deploy.apple.com](https://deploy.apple.com). As vantagens do programa incluem instalação não assistida de dispositivos sem conectar cada dispositivo por USB a um computador.  

 Antes de registrar dispositivos iOS corporativos pelo DEP, você precisa de um token do DEP da Apple. Esse token permite que Intune sincronize informações sobre dispositivos participantes no DEP pertencentes a sua empresa. Ele também permite que o Intune carregue perfis de registro na Apple e atribua dispositivos a esses perfis.  

## <a name="apple-dep-enrollment-for-ios-devices"></a>Registro pelo DEP da Apple para dispositivos iOS  
 Os procedimentos a seguir descrevem como especificar dispositivos iOS adquiridos por meio do DEP da Apple, como dispositivos da empresa gerenciados pelo Intune. Quando o usuário liga o dispositivo pela primeira vez, ele recebe o perfil de gerenciamento do DEP e executa o Assistente de Instalação e levá-o para o gerenciamento.  

##  <a name="enable-dep-enrollment-in-configuration-manager-with-intune"></a>Habilitar o registro de DEP no Configuration Manager com o Intune  

1. **Comece a gerenciar dispositivos iOS com o Configuration Manager**   
   Para poder registrar dispositivos iOS do DEP (Programa de Registro de Dispositivo), você deve concluir as etapas para [Configurar o gerenciamento de dispositivo móvel híbridos](../../mdm/deploy-use/setup-hybrid-mdm.md) incluindo [etapas para dar suporte ao registro no iOS](../deploy-use/enroll-hybrid-ios-mac.md).
2. **Criar uma solicitação de token do DEP**   
   No console do Configuration Manager, no workspace **Administração**, expanda **Configuração da Hierarquia**, expanda **Serviços de Nuvem** e clique em **Assinaturas do Microsoft Intune**. Clique em **Criar Solicitação de Token de DEP** na guia **Início** , clique em **Procurar** para especificar o local de download para a solicitação de token de DEP e clique em **Baixar**. Salve o arquivo de solicitação de token DEP (.pem) localmente. O arquivo .pem é usado para solicitar um token confiável (.p7m) do portal do Programa de Registro de Dispositivo da Apple.  
3. **Obter um token do Programa de Registro de Dispositivo**   
   Vá até o [Portal do Programa de Registro de Dispositivos](https://deploy.apple.com) (https://deploy.apple.com) e entre com sua ID da Apple corporativa. Essa ID da Apple deve ser usada no futuro para renovar seu token do DEP.  
   1. No console do [Portal do Programa de Registro de Dispositivo](https://deploy.apple.com), vá para **Programa de Registro de Dispositivo** > **Gerenciar Servidores**e clique em **Adicionar Servidor MDM**.  
      ![Captura de tela da adição do servidor MDM no portal do Programa de registro de dispositivos](../media/enrollment-program-token-add-server.png)
   2. Insira o **Nome do Servidor MDM**e clique em **Avançar**. O nome do servidor é para sua referência para identificar o servidor MDM. Não é o nome ou URL do servidor do Intune ou do Configuration Manager.  
   3. A caixa de diálogo **Adicionar <ServerName>\>** é aberta. Clique em **Escolher Arquivo...** para carregar o arquivo .pem que você criou na etapa anterior e clique em **Avançar**.  
   4. A caixa de diálogo **Adicionar <ServerName>\>** exibe um link **Seu Token do Servidor**. Baixe o arquivo de token (.p7m) do servidor em seu computador e clique em **Concluído**.  

      Esse arquivo de certificado (.p7m) é usado para estabelecer uma relação de confiança entre servidores do Programa de Registro de Dispositivo da Apple.  
4. **Adicione o token do DEP ao Configuration Manager**   
   No console do Configuration Manager, no workspace **Administração**, expanda a **Configuração da Hierarquia** e clique em **Assinaturas do Microsoft Intune**. Clique em **Configurar Plataformas** na guia **Início** e clique em **iOS**. Selecione **Habilitar Programa de Registro de Dispositivo**, navegue até o arquivo de certificado (.p7m), clique em **Abrir**, em **Carregar**e em **OK**.  

## <a name="add-a-corporate-device-enrollment-policy"></a>Adicionar uma Política de Registro de Dispositivo Corporativo  

1. No console do Configuration Manager, no workspace **Ativos e Conformidade**, expanda a **Visão Geral**, expanda **Todos os Dispositivos Pertencentes à Empresa**, expanda **iOS** e clique em **Perfis de Registro**. Clique em **Criar Perfil** na guia **Início** para abrir o assistente de Criação de Perfil. Defina as configurações nas páginas a seguir:  
2. On the **Geral** , especifique as informações a seguir e clique em **Avançar**.  
   - **Nome** – nome do perfil de registro do dispositivo. (Não é visível para os usuários)  
   - **Descrição** - Descrição do perfil de registro do dispositivo. (Não é visível para os usuários)  
   - **Afinidade do usuário** – especifica como os dispositivos são registrados. Consulte [Afinidade de usuário para dispositivos híbridos gerenciados no Configuration Manager](../../mdm/deploy-use/user-affinity-for-hybrid-managed-devices.md).  

     - **Solicitar afinidade do usuário**: O dispositivo deve ser afiliado a um usuário durante a instalação inicial e, em seguida, poderá receber permissão para acessar dados da empresa e o email como esse usuário.  A afinidade do usuário deve ser configurada para dispositivos gerenciados por DEP que pertencem aos usuários e que precisam usar o portal da empresa (por exemplo, para instalar aplicativos).  
       > [!NOTE]
       > O DEP com afinidade do usuário requer que o ponto de extremidade misto/nome do usuário do ADFS WS-Trust 1.3 esteja habilitado para solicitar o token do usuário.

     - **Sem afinidade de usuário**: O dispositivo não está afiliado a um usuário. Use esta afiliação para dispositivos que executam tarefas sem acessar aos dados de usuário local. Os aplicativos que exigem a afiliação com usuário não funcionarão.  
       ![Captura de tela do nome de perfil DEP, descrição e prompt de Afinidade do Usuário](../media/dep-general.png)

3. Na página **Configurações do Programa de Registro do Dispositivo**, especifique as informações a seguir e clique em **Avançar**.  
    -   **Departamento**: Essas informações são exibidas quando os usuários tocam em "Sobre a configuração" durante a ativação.  
    -   **Número de telefone de suporte**: Exibido quando o usuário clica o **precisa de Ajuda** botão durante a ativação.
       ![Captura de tela da atribuição de perfil DEP para dispositivos iOS](../media/dep-settings.png)

    - **Modo de preparação**: Esse estado é definido durante a ativação e não pode ser alterado sem redefinir o dispositivo de fábrica:  
        -   **Sem supervisão** – Recursos de gerenciamento limitados  
        -   **Supervisionado** – Habilita mais opções de gerenciamento e desabilita o Bloqueio de Ativação por padrão  
    - **Bloquear perfil de registro do dispositivo**: Esse estado é definido durante a ativação e não pode ser alterado sem uma redefinição de fábrica.  
      -   **Desabilitar** – Permite que o perfil de gerenciamento seja removido do menu **Configurações**  
      -   **Habilitar** – (requer o **Modo de Preparação** = **Supervisionado**) Desabilita as configurações do iOS que poderiam permitir a remoção do perfil de gerenciamento  

4. Na página **Assistente de Configuração** , defina as configurações que personalizam o Assistente de Configuração do iOS que é iniciado quando o dispositivo é ligado pela primeira vez e clique em **Avançar**. Essas configurações incluem:  
   -   **Senha** – Solicitar senha durante a ativação. Sempre exija uma senha, a menos que o dispositivo esteja protegido ou tenha o acesso controlado de alguma outra maneira (ou seja, o modo de quiosque que restringe o dispositivo a um aplicativo).  
   -   **Serviços de Localização** – Se habilitado, o Assistente de Instalação solicitará o serviço durante a ativação  
   -   **Restaurar** – Se habilitado, o Assistente de Instalação solicitará o backup do iCloud durante a ativação  
   -   **ID da Apple** – Uma ID da Apple é exigida para baixar aplicativos na App Store do iOS, incluindo aqueles instalados pelo Intune. Se habilitado, o iOS solicitará aos usuários uma ID da Apple quando o Intune tentar instalar um aplicativo sem uma ID.  
   -   **Termos e Condições** – Se habilitado, o Assistente de Instalação solicitará que os usuários aceitem os termos e as condições da Apple durante a ativação  
   -   **ID de Toque** – Se habilitada, o Assistente de Configuração solicitará o serviço durante a ativação
   -   **Apple Pay** – Se habilitado, o Assistente de Configuração solicitará o serviço durante a ativação
   -   **Zoom** – Se habilitado, o Assistente de Configuração solicitará o serviço durante a ativação
   -   **Siri** – Se habilitado, o Assistente de Instalação solicitará o serviço durante a ativação  
   -   **Enviar dados de diagnóstico para a Apple** – Se habilitado, o Assistente de Instalação solicitará o serviço durante a ativação  
   ![Captura de tela da atribuição de perfil DEP para dispositivos iOS](../media/dep-setup-assistant.png)
5. Na página **Gerenciamento Adicional**, especifique se uma conexão USB pode ser usada para configurações de gerenciamento adicional. Ao selecionar **Exigir certificado**, você deve importar um certificado de gerenciamento do Apple Configurator a ser usado para este perfil.  Defina como **Não permitir** para impedir a sincronização de arquivos com iTunes ou gerenciamento por meio do Apple Configurator. A Microsoft recomenda definir **Não permitir**, exportar configurações adicionais do Apple Configurator e implantar como um perfil de configuração do iOS Personalizado, em vez de usar essa configuração para permitir a implantação manual com ou sem um certificado.  

   -   **Não permitir** – Impede que o dispositivo se comunique via USB (desabilita emparelhamento)  
   -   **Permitir** – Permite que o dispositivo se comunique por meio de conexão USB com qualquer PC ou Mac  
   -   **Exigir certificados** – Permite o emparelhamento com um Mac com um certificado importado para o perfil de registro  

## <a name="assign-dep-devices-for-management"></a>Atribuir dispositivos do DEP para gerenciamento

1. Vá até o [Portal do Programa de Registro de Dispositivos](https://deploy.apple.com) (https://deploy.apple.com) e entre com sua ID da Apple corporativa.
2. Vá para **Programa de Implantação** > **Programa de Registro de Dispositivo** > **Gerenciar Dispositivos**. Especifique como você vai **Escolher Dispositivos**, forneça informações do dispositivo e especifique os detalhes por **Número de Série**, **Número do Pedido**do dispositivo ou ao **Carregar o Arquivo CSV**. Em seguida, selecione **Atribuir ao Servidor**, selecione o <*ServerName*> que você especificou na etapa 3 e clique em **OK**.  
![Captura de tela da adição de dispositivos no portal do Programa de registro de dispositivos Apple](../media/enrollment-program-token-specify-serial.png)

3.  **Sincronizar dispositivos gerenciados pelo DEP**   
    No workspace **Ativos e Conformidade**, vá para **Todos os Dispositivos de Propriedade Corporativa** > **Dispositivos Pré-declarados**. Na guia **Início** , clique em **Sincronização de DEP**. Uma solicitação de sincronização é enviada à Apple. Depois de concluída a sincronização, os dispositivos gerenciados pelo DEP são exibidos.

    > [!NOTE]
    > Na configuração híbrida, a operação de sincronização DEP é disparada manualmente clicando em **Sincronização DEP** no console do Configuration Manager.

4.  **Atribuir perfil DEP**<br>No workspace **Ativos e Conformidade**, vá para **Todos os Dispositivos de Propriedade Corporativa** > **iOS** > **Perfis de Registro**. Selecione o perfil de registro DEP, em seguida, na guia **Início**, clique em **Atribuir a dispositivos**. Selecione os dispositivos que usarão esse perfil de registro, clique em **Adicionar** em seguida, clique em **OK**.

    > [!NOTE]
    > Depois que um perfil DEP for atribuído a um dispositivo, você poderá substituir o perfil apenas por outro perfil DEP. No entanto, você não pode remover a atribuição do perfil DEP. Para remover um perfil DEP de um dispositivo, você deve cancelar a inscrição do dispositivo.  
     ![Captura de tela da atribuição de perfil DEP para dispositivos iOS](../media/dep-assign-profile.png)

## <a name="distribute-devices-to-users"></a>Distribuir dispositivos para usuários
Agora você pode fornecer seus dispositivos de propriedade corporativa para usuários. A caixa de diálogo **Status de Registro** dos dispositivos gerenciados indica **Não contatado** até que o dispositivo seja ligado e execute o Assistente de Configuração para registrar o dispositivo. Quando um dispositivo iOS for ativado, ele será registrado para gerenciamento pelo Intune.
