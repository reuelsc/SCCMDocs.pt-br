---
title: "Registro híbrido do iOS que usa o Apple Configurator com o Configuration Manager"
descriptions: Pre-enroll iOS devices by using Apple Configurator with Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61a19d95-83ff-4ad8-9a67-f304d2ba54f2
caps.latest.revision: 5
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 19f4880d6e7ba3da2e4bcfe725c1c806ee3b3334


---
# <a name="ios-hybrid-enrollment-using-apple-configurator-with-configuration-manager"></a>Registro híbrido do iOS que usa o Apple Configurator com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As empresas que compram dispositivos iOS para serem usados pelos funcionários podem gerenciá-los usando o Microsoft Intune. É possível pré-registrar dispositivos iOS conectando-os por USB a um computador Mac com o Apple Configurator. Antes de registrar, é necessário preparar um perfil de dispositivo de registro corporativo do Intune no console de administração do Intune e exportá-lo para o computador Mac. O processo de registro realizará a redefinição de fábrica do dispositivo e examinará o processo do Assistente de Configuração para configurar o dispositivo. O procedimento a seguir é recomendado para dispositivos iOS dedicados que terão um único usuário que usa o dispositivo para acessar o email e os recursos corporativos, como aplicativos e data.  

##  <a name="a-namebkmksaea-apple-configurator-enrollment-via-setup-assistant"></a><a name="BKMK_SAE"></a> Registro do Apple Configurator por meio do Assistente de Configuração  
 Usando o configurador Apple, é possível redefinir de fábrica dispositivos iOS e prepara-los para a configuração pelo novo usuário do dispositivo.  Esse método requer que você conecte o dispositivo iOS por USB a um computador Mac para configurar o registro corporativo e supõe que você esteja usando o Apple Configurator 2.0.  

 **Pré-requisitos**  

-   Acesso físico aos dispositivos iOS  

-   Números de série do dispositivo – [Como obter um número de série do iOS](https://support.apple.com/en-us/HT204308)  

-   Cabos de conexão USB  

-   Computador Mac com o [Apple Configurator 2.0](http://go.microsoft.com/fwlink/?LinkId=518017)  

#### <a name="enable-setup-assistant-enrollment-with-configuration-manager-and-intune"></a>Habilitar o registro do Assistente de Configuração com o Configuration Manager e o Intune  

1.  **Adicionar um perfil de Registro de Dispositivo Corporativo**   
    No console do Configuration Manager, no espaço de trabalho **Ativos e Conformidade**, expanda a **Visão Geral**, expanda **Todos os Dispositivos Pertencentes à Empresa**, expanda **iOS** e clique em **Perfis de Registro**. Clique em **Criar Perfil** na guia **Início** para abrir o assistente de Criação de Perfil. Defina as configurações nas páginas a seguir:  

    1.  On the **Geral** , especifique as informações a seguir e clique em **Avançar**.  

        -   **Nome** – nome do perfil de registro do dispositivo. (Não é visível para os usuários)  

        -   **Descrição** - Descrição do perfil de registro do dispositivo. (Não é visível para os usuários)  

        -   **Afinidade do usuário** – especifica como os dispositivos são registrados. Para a maioria dos cenários do Assistente de Configuração, use **Solicitar afinidade de usuário**.  

            -   **Solicitar a afinidade de usuário**: o dispositivo deve ser afiliado a um usuário durante a configuração inicial e depois poderá receber permissão para acessar os dados e o email da empresa como esse usuário.  

            -   **Nenhuma afinidade de usuário**: O dispositivo não está afiliado a um usuário. Use esta afiliação para dispositivos que executam tarefas sem acessar aos dados de usuário local. Os aplicativos que exigem a afiliação com usuário não funcionarão.  

    2.  Na página **Programa de Registro do Dispositivo**, deixe a caixa de seleção **Definir configurações do Programa de Registro do Dispositivo para esse perfil** desmarcada e clique em **Avançar**.  

    3.  Revise o Resumo e clique em Rede.  

2.  **Adicionar dispositivos iOS para registro com o Assistente de Configuração**   
    No console do Configuration Manager, no espaço de trabalho **Ativos e Conformidade**, expanda a **Visão Geral**, expanda **Todos os Dispositivos Pertencentes à Empresa**, expanda **iOS** e clique em **Informações do dispositivo**. e clique em **Adicionar dispositivos**. Você pode adicionar dispositivos de duas maneiras:  

    - É possível **Carregar um arquivo CSV contendo números de série** – crie uma lista de valores separados por vírgula (.csv) de duas colunas, sem cabeçalho, com limite de 5000 dispositivos ou 5 MB por arquivo csv. Para cada linha, a primeira célula é o número de série do dispositivo, a segunda célula são detalhes do dispositivo (opcionais).

  Quando visualizado em um editor de texto, esse arquivo .csv aparece como:  

    ```  
    0000000,PO 1234  
    111111111,PO 1234  
    ```  

    - Também é possível **Adicionar manualmente números de série e detalhes** – digite o número de série e os detalhes de até cinco dispositivos  

    Em seguida, clique em **Avançar**.  

3.  **Selecione os dispositivos a serem registrados**   
    Confirme os dispositivos a serem registrados. Não é possível importar os números de série já registrados ou registrados por outros meios. Clique em **Próximo** para continuar.  

4.  **Atribuir perfil**   
    Especifique o perfil a ser atribuído a dispositivos adicionados na lista de perfis disponíveis, examine os **Detalhes do perfil de registro** e clique em **Concluir**. Dispositivos adicionados manualmente podem ser atribuídos a qualquer perfil de Registro, mas dispositivos sincronizados com o DEP precisam ser atribuídos a um perfil habilitado para o DEP.  

5.  **Selecionar um perfil para implantar em dispositivos iOS**   
    No console do Configuration Manager, no espaço de trabalho **Ativos e Conformidade**, expanda **Visão geral**, expanda **Todos os Dispositivos Pertencentes à Empresa**, expanda **iOS**, clique em **Perfis de Registro** e selecione o perfil a ser implantado em dispositivos móveis. Clique em **Exportar...** na barra de tarefas. Copie e salve a **URL do perfil**. Você fará o upload no Apple Configurator posteriormente para definir o perfil do Intune utilizado pelos dispositivos iOS.  A URL do perfil de registro é válida por duas semanas a partir de sua exportação. Depois de duas semanas, você deve exportar um novo arquivo de URL para registro de dispositivos iOS.  

     Para oferecer suporte ao Apple Configurator 2, a URL do perfil 2.0 deve ser editada. Substitua:  

    ```  
    https://manage.microsoft.com/EnrollmentServer/Discovery.svc/iOS/ESProxy?id=  

    ```  

     por  

    ```  
    https://appleconfigurator2.manage.microsoft.com/MDMServiceConfig?id=  

    ```  

6.  **Preparar o dispositivo com o Apple Configurator**   
    Dispositivos iOS são conectados ao computador Mac e registrados para o gerenciamento de dispositivo móvel.  

    > [!WARNING]  
    >  Os dispositivos serão redefinidos para as configurações de fábrica durante o processo de registro.  

    1.  Em um computador Mac, abra o **Apple Configurator 2**.  Na barra de menus, clique em **Apple Configurator 2** e clique em **Preferências**.  

    2.  No painel de preferências, selecione **Servidores** e clique no símbolo "+" abaixo do painel esquerdo para iniciar o assistente do Servidor MDM. Clique em **Avançar**.  

    3.  Insira o **Nome** e a **URL de Registro** do Servidor MDM da etapa 5 acima. Clique em **Avançar**.  

         Se você receber um aviso sobre os requisitos de perfil de confiança da Apple TV, cancele com segurança a opção **Perfil de Confiança** clicando no "X" cinza. Você pode ignorar com segurança qualquer Aviso de certificado de âncora. Para continuar, clique em **Avançar** até que o assistente seja concluído.  

    4.  No painel **Servidores**, clique em "Editar" ao lado do perfil do novo servidor. Verifique se a URL de Registro corresponde exatamente à URL exportada do Intune. Digite novamente a URL original, se ela for diferente, e **Salve** o perfil de registro exportado do Intune.  

    5.  Conecte os dispositivos móveis iOS ao computador Apple com um adaptador USB.  

        > [!WARNING]  
        >  Os dispositivos serão redefinidos para as configurações de fábrica durante o processo de registro. Como prática recomendada, redefina o dispositivo e ligue-o. Como prática recomendada, os dispositivos devem estar na tela Hello quando você inicia o Assistente de Configuração.  

    6.  Clique em **Preparar**. No painel **Preparar o Dispositivo iOS**, selecione **Manual** e clique em **Avançar**.  

    7.  No painel **Registrar no Servidor MDM**, selecione o nome do servidor que você criou e, em seguida, clique em **Avançar**.  

    8.  No painel **Registrar no Servidor MDM**, selecione o nome do servidor que você criou e, em seguida, clique em **Avançar**.  

    9. No painel **Criar uma Organização**, escolha a **Organização** ou crie uma nova organização e clique em **Avançar**.  

    10. No painel **Configurar o Assistente de Configuração do iOS**, escolha as etapas apresentadas ao usuário e clique em **Preparar**. Se receber uma solicitação, autentique para atualizar as configurações de confiança.  

    11. Quando o dispositivo iOS terminar a preparação, desconecte o cabo USB.  

7.  **Distribuir dispositivos**   
    Os dispositivos agora estão prontos para o registro corporativo. Desligue os dispositivos e distribua-os aos usuários. Quando o dispositivo for ativado, o assistente de configuração iniciará e solicitará ao usuário sua conta corporativa ou de estudante.



<!--HONumber=Nov16_HO1-->


