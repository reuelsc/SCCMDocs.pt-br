---
title: Conectar o Configuration Manager
titleSuffix: Configuration Manager
description: Um guia de instruções para conectar o Configuration Manager com a análise de área de trabalho.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fb16dd6e802c58f042b7eee8ae782e7118dabf1c
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159189"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>Como conectar o Configuration Manager com a análise de área de trabalho

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Análise da área de trabalho está totalmente integrado com o Configuration Manager. Primeiro, verifique se que o site é atualizado para dar suporte a recursos mais recentes. Em seguida, crie a conexão de área de trabalho de análise no Configuration Manager. Por fim, monitore a integridade de conexão.


## <a name="bkmk_hotfix"></a> Atualizar o site

Primeiro, certifique-se de que seu site do Configuration Manager está em execução pelo menos versão 1902. Para obter mais informações, confira [Instalar atualizações no console](/sccm/core/servers/manage/install-in-console-updates).

Você também precisará instalar o versão 1902 pacote cumulativo de atualizações (4500571) para dar suporte à integração com a área de trabalho de análise. Para obter mais informações sobre esta atualização, consulte [atualização cumulativa para o branch atual do Configuration Manager, versão 1902](https://support.microsoft.com/help/4500571).

1. Atualize o site com o pacote cumulativo de atualizações para a versão 1902. Para obter mais informações, confira [Instalar atualizações no console](/sccm/core/servers/manage/install-in-console-updates).  

2. Atualize clientes. Para simplificar este processo, considere o uso da atualização automática do cliente. Para obter mais informações, consulte [Atualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  



## <a name="bkmk_connect"></a> Conectar-se ao serviço

Use este procedimento para conectar o Configuration Manager para análise de área de trabalho e definir as configurações do dispositivo. Esse procedimento é um processo único para anexar a sua hierarquia para o serviço de nuvem.  

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e selecione o nó **Serviços do Azure**. Selecione **configurar serviços do Azure** na faixa de opções.  

    > [!Tip]  
    > No console do Configuration Manager, vá para o **biblioteca de Software** espaço de trabalho e selecione o **área de trabalho de análise de manutenção** nó. No *novo para a área de trabalho de análise?* , selecione o segundo link para *conectar o Configuration Manager para o serviço de análise de área de trabalho*.  

2. Sobre o **serviços do Azure** página do Assistente de serviços do Azure, defina as seguintes configurações:  

    - Especifique um **Nome** para o objeto no Configuration Manager.  

    - Especifique uma **Descrição** opcional para ajudá-lo a identificar o serviço.  

    - Selecione **análise de área de trabalho** na lista de serviços disponíveis.  
  
   Selecione **Avançar**.  

3. Sobre o **aplicativo** , selecione apropriado **ambiente do Azure**. Em seguida, selecione **procurar** para o aplicativo web.  

4. Se você tiver um aplicativo existente que você deseja reutilizar esse serviço, escolha-o na lista e selecione **Okey**.  

5. Na maioria dos casos, você pode criar um aplicativo para a conexão de área de trabalho de análise com esse assistente. Selecione **Criar**.<!-- 3572123 -->  

    > [!Tip]  
    > Se você não pode criar o aplicativo nesse assistente, você pode criar manualmente o aplicativo no Azure AD e, em seguida, importar no Configuration Manager. Para obter mais informações, consulte [importação e criar aplicativos para o Configuration Manager](/sccm/desktop-analytics/troubleshooting#create-and-import-app-for-configuration-manager).  

6. Defina as seguintes configurações na **criar aplicativo de servidor** janela:  

    - **Nome do aplicativo**: Um nome amigável para o aplicativo no Azure AD.

    - **URL da home page**: esse valor não é usado pelo Configuration Manager, mas é exigido pelo Azure AD. Por padrão, esse valor é `https://ConfigMgrService`.  

    - **URI da ID do aplicativo**: esse valor precisa ser exclusivo no locatário do Azure AD. Ele é no token de acesso usado pelo cliente do Configuration Manager para solicitar acesso ao serviço. Por padrão, esse valor é `https://ConfigMgrService`.  

    - **Período de validade da Chave Secreta**: escolha **1 ano** ou **2 anos** na lista suspensa. Um ano é o valor padrão.  

    Selecione **entrar** . Após a autenticação bem-sucedida no Azure, a página mostra o **Nome do Locatário do Azure AD** para referência.
        
    > [!Note]  
    > Conclua esta etapa como uma **administrador da empresa**. Essas credenciais não são salvas pelo Configuration Manager. Essa persona não exige permissões no Configuration Manager e não precisa ser a mesma conta que executa o Assistente de Serviços do Azure.  

    Selecione **OK** para criar o aplicativo Web no Azure AD e feche a caixa de diálogo Criar Aplicativo para Servidores. Na caixa de diálogo do aplicativo de servidor, selecione **Okey**. Em seguida, selecione **próxima** na página do aplicativo do Assistente de serviços do Azure.  

7. Sobre o **dados de diagnóstico** página, defina as seguintes configurações:  

    - **ID comercial**: esse valor deve preencher automaticamente com a ID. da sua organização Se ele não abrir, certifique-se de seu servidor proxy está configurado para permitir todos os itens necessários [pontos de extremidade](/sccm/desktop-analytics/enable-data-sharing#endpoints) antes de continuar. Como alternativa, recuperar sua ID comercial manualmente a partir de [portal de análise de área de trabalho](/sccm/desktop-analytics/monitor-connection-health#bkmk_ViewCommercialID).  

    - **Nível de dados de diagnóstico do Windows 10**: Selecione pelo menos **básico**. Consulte [níveis de dados de diagnóstico](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)
  
    - **Permitir que o nome do dispositivo nos dados de diagnóstico**: selecione **habilitar**  

        > [!Note]  
        > Começando com o Windows 10 versão 1803, o nome do dispositivo não será enviado à Microsoft por padrão. Se você não enviar o nome do dispositivo, ele aparece na área de trabalho de análise como "Desconhecido". Esse comportamento pode tornar difícil de identificar e avaliar os dispositivos.  

   Selecione **Avançar**. O **funcionalidade disponível** página mostra a funcionalidade de análise de área de trabalho que está disponível com as configurações de dados de diagnóstico da página anterior. Selecione **próxima** para continuar ou **Previous** para fazer alterações.  

    ![Exemplo de página de funcionalidade disponível no Assistente de serviços do Azure](media/available-functionality.png)

8. Sobre o **coleções** página, defina as seguintes configurações:  

    - **Nome de exibição**: O portal de análise de área de trabalho exibe essa conexão do Configuration Manager usando esse nome. Usá-lo para diferenciar entre hierarquias diferentes. Por exemplo, *laboratório de teste* ou *produção*.  

    - **Coleção de destino**: Esta coleção inclui todos os dispositivos que o Configuration Manager configura com sua ID comercial e as configurações de dados de diagnóstico. É o conjunto completo de dispositivos do Configuration Manager se conecta ao serviço de análise de área de trabalho.  

    - **Dispositivos na coleção de destino usam um proxy de usuário autenticado para comunicação de saída**: Por padrão, esse valor é **não**. Se for necessário em seu ambiente, definido como **Sim**.  

    - **Selecione as coleções específicas para sincronizar com a área de trabalho de análise**: Selecione **Add** incluir coleções adicionais de seus **coleção de destino** hierarquia. Essas coleções estão disponíveis no portal de análise de área de trabalho para o agrupamento com planos de implantação. Certifique-se de incluir coleções de exclusão do projeto-piloto e piloto.  <!-- 4097528 -->  

        > [!Important]  
        > Essas coleções continuam a sincronização como suas alterações de associação. Por exemplo, o seu plano de implantação usa uma coleção com uma regra de associação do Windows 7. Como esses dispositivos de atualização para o Windows 10, e o Configuration Manager avalia a associação da coleção, esses dispositivos soltem fora a coleta e o plano de implantação.  


9. Conclua o assistente.  

O Configuration Manager cria uma política de configurações para configurar dispositivos na coleção de destino. Esta política inclui as configurações de dados de diagnóstico para habilitar dispositivos para enviar dados à Microsoft. Por padrão, clientes atualizam a política a cada hora. Depois de receber as novas configurações, pode ser mais várias horas, antes que os dados estão disponíveis na área de trabalho de análise.



## <a name="bkmk_monitor"></a> Monitorar a integridade de conexão

Monitore a configuração de seus dispositivos para análise de área de trabalho. No console do Configuration Manager, vá para o **biblioteca de Software** espaço de trabalho, expanda o **área de trabalho de análise de manutenção** nó e selecione o **integridade de Conexão** Painel de controle.  

Para obter mais informações, consulte [monitorar a integridade de conexão](/sccm/desktop-analytics/troubleshooting#monitor-connection-health).

Configuration Manager sincroniza suas coleções dentro de 60 minutos de criar a conexão. No portal de análise de área de trabalho, vá para **piloto Global**e ver suas coleções de dispositivos do Configuration Manager.



## <a name="next-steps"></a>Próximas etapas

Avance para o próximo artigo para registrar dispositivos para análise de área de trabalho.
> [!div class="nextstepaction"]  
> [Registrar dispositivos](/sccm/desktop-analytics/enroll-devices)  
