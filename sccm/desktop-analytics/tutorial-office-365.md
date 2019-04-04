---
title: Tutorial – implantar o Office 365
titleSuffix: Configuration Manager
description: Um tutorial sobre como usar a área de trabalho de análise e o Configuration Manager para implantar o Office 365 em um grupo piloto.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: tutorial
ms.assetid: 0b2b633a-91d7-4497-8c2a-1fc7aa310bb1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 12f19fe6f52d1ceb4b47b080e45030df898a332a
ms.sourcegitcommit: da753df27d3909265ca45d3e79091f1e98758d16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2019
ms.locfileid: "58913550"
---
# <a name="tutorial-deploy-office-365-to-pilot"></a>Tutorial: Implantar o Office 365 para piloto 

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Este tutorial usa a análise de área de trabalho e o Configuration Manager para implantar o Office 365 ProPlus em um grupo piloto. Ele destaca a integração do serviço de nuvem para fornecer ideias para implantar o aplicativo com o produto no local. Use análise de área de trabalho para determinar os melhores dispositivos para colocar em um grupo piloto. Em seguida, use o Configuration Manager para obter atual com o Office.

Neste tutorial, você aprenderá como:  

> [!div class="checklist"]  
> * Configurar análise de área de trabalho no portal do Azure  
> * Conectar o Configuration Manager e definir configurações de dispositivo  
> * Criar um plano de implantação de área de trabalho de análise do Office 365 ProPlus  
> * Implantar o Office 365 ProPlus no Configuration Manager para o grupo piloto  

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar. Quando configurado corretamente, o uso da área de trabalho de análise não incorre em custos do Azure. 

A análise da área de trabalho usa um *espaço de trabalho do Log Analytics* na sua assinatura do Azure. Um espaço de trabalho é essencialmente um contêiner que inclui informações de conta e informações de configuração simples para a conta. Para obter mais informações, consulte [gerenciar espaços de trabalho](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json).



## <a name="prerequisites"></a>Pré-requisitos

Antes de iniciar este tutorial, certifique-se de que ter os seguintes pré-requisitos:  

- Uma assinatura do Azure Active Directory, com **administrador da empresa** permissões  

- O Configuration Manager, versão 1810 com 4488598 de Rollup de atualização ou posterior, com **administrador completo** função  

- Pelo menos um dispositivo Windows 10 com as seguintes configurações:  

    - Windows 10, versão 1709 ou posterior

    - A atualização de qualidade cumulativa mais recente do Windows 10  

    - Configuration Manager versão 1810 do cliente com o pacote cumulativo de atualizações 4486457 ou posterior  

    - Uma versão do Windows com base no instalador do Office, como o Office 2013  

- Aprovação de negócios para configurar o nível de dados de diagnóstico do Windows para **avançado (limitado)** nos dispositivos piloto  

    Para obter mais informações, consulte [privacidade de área de trabalho de análise](/sccm/desktop-analytics/privacy).

- Conectividade de rede do dispositivo para os seguintes pontos de extremidade de internet:

    - `https://v10c.events.data.microsoft.com`  
    - `https://settings-win.data.microsoft.com`  
    - `http://adl.windows.com`  
    - `https://watson.telemetry.microsoft.com`  
    - `https://umwatsonc.events.data.microsoft.com`  
    - `https://ceuswatcab01.blob.core.windows.net`  
    - `https://ceuswatcab02.blob.core.windows.net`  
    - `https://eaus2watcab01.blob.core.windows.net`  
    - `https://eaus2watcab02.blob.core.windows.net`  
    - `https://weus2watcab01.blob.core.windows.net`  
    - `https://weus2watcab02.blob.core.windows.net`  
    - `https://www.msftncsi.com`  
    - `https://www.msftconnecttest.com`  
    - `https://kmwatsonc.events.data.microsoft.com`  
    - `https://oca.telemetry.microsoft.com`  
    - `https://login.live.com`  
    - `https://nexusrules.officeapps.live.com`  
    - `https://nexus.officeapps.live.com`  
    - `https://office.pipe.aria.microsoft.com`  
    - `https://graph.windows.net` (na função de servidor do Configuration Manager somente)
    - `https://fef.msua06.manage.microsoft.com` (na função de servidor do Configuration Manager somente)

    Para obter mais informações, consulte [como habilitar o compartilhamento de área de trabalho de análise de dados](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

> [!Important]  
> Estes pré-requisitos são para os fins deste tutorial. Para obter mais informações sobre os pré-requisitos gerais para análise de área de trabalho com o Configuration Manager, consulte [pré-requisitos](/sccm/desktop-analytics/overview#prerequisites).  



## <a name="set-up-desktop-analytics"></a>Configurar Análise de Área de Trabalho

Use este procedimento para entrar no Analytics de área de trabalho e configurá-lo em sua assinatura. Esse procedimento é um processo único para configurar a análise de área de trabalho para sua organização.  

1. Abra o portal de análise de área de trabalho no gerenciamento de dispositivo do Microsoft 365 como um usuário com **administrador da empresa** permissões. Selecione **iniciar**.  

2. Sobre o **aceite o contrato de serviço** página, examine o contrato de serviço e selecione **Accept**.  

3. Sobre o **confirmar sua assinatura** página, a lista de licenças qualificadas necessárias são para recursos de integridade de dispositivo do Windows da área de trabalho de análise. Selecione **Avançar** para continuar.  

4. Sobre o **dar aos usuários acesso** página, análise de área de trabalho pré-configura dois grupos de segurança no Azure Active Directory:  

    - **Os proprietários do espaço de trabalho**: Criar e gerenciar espaços de trabalho. Essas contas precisam de acesso de proprietário à assinatura do Azure.  

    - **Colaboradores de espaço de trabalho**: Criar e gerenciar planos de implantação neste espaço de trabalho. Eles não precisam de qualquer acesso do Azure adicional.  
  
   Para adicionar um usuário a um grupo, digite seu nome ou endereço de email na **insira o nome ou endereço de email** seção grupo apropriado. Quando terminar, selecione **próxima**. 

5. Na página para **definir seu espaço de trabalho**:  

    - Para usar um espaço de trabalho para análise de área de trabalho, selecione-o e continue com a próxima etapa.  

    - Para criar um espaço de trabalho para análise de área de trabalho, selecione **adicionar espaço de trabalho**.  

        1. Insira um **nome do espaço de trabalho**.  

        2. Selecione a lista suspensa para **selecione o nome de assinatura do Azure para este espaço de trabalho**e escolha a assinatura do Azure para este espaço de trabalho.  

        3. Selecione o **região** na lista e, em seguida, selecione **Add**.  

6. Selecione um espaço de trabalho novo ou existente e, em seguida, selecione **definido como espaço de trabalho de análise de área de trabalho**.  Em seguida, selecione **Continue** na **confirmar e conceder acesso** caixa de diálogo.  

7. Na nova guia do navegador, escolha uma conta para usar para entrar. Selecione a opção para **consentir em nome de sua organização** e selecione **Accept**.  

8. Volta na página para **definir seu espaço de trabalho**, selecione **próxima**.  

9. Sobre o **última etapa** página, selecione **vá para a área de trabalho de análise**. O portal do Azure mostra a área de trabalho de analítica **Home** página.  


### <a name="create-an-app-in-azure-ad-for-configuration-manager"></a>Criar um aplicativo no Azure AD para o Configuration Manager  

1. No [portal do Azure](https://portal.azure.com), acesse **Azure Active Directory**e selecione **registros do aplicativo**. Em seguida, selecione **novo registro de aplicativo**.  

2. No **criar** painel, defina as seguintes configurações:  

    - **Nome**: um nome exclusivo que identifica o aplicativo, por exemplo: `Desktop-Analytics-Connection`  

    - **Tipo de aplicativo**: **Aplicativo Web / API**  

    - **URL de logon**: esse valor não é usado pelo Configuration Manager, mas exigido pelo Azure AD. Insira uma URL exclusiva e é válida, por exemplo: `https://configmgrapp`  
  
    Selecione **Criar**.  

3. Selecione o aplicativo e observe os **ID do aplicativo**. Esse valor é um GUID que é usado para configurar a conexão do Configuration Manager.  

4. Selecione **as configurações** sobre o aplicativo e, em seguida, selecione **chaves**. No **senhas** , digite um **descrição da chave**, especifique uma expiração **duração**e, em seguida, selecione **salvar**. Cópia de **valor** da chave, que é usado para configurar a conexão do Configuration Manager. 

    > [!Important]  
    > Isso é a única oportunidade para copiar o valor da chave. Se você não copiá-lo agora, você precisará criar outra chave.  
    > 
    > Salve o valor da chave em um local seguro.  

5. No aplicativo **as configurações** painel, selecione **permissões necessárias**.  

    1. Sobre o **permissões necessárias** painel, selecione **Add**.  

    2. No **adicionar acesso à API** painel **selecionar uma API**.  

    3. Pesquise o **Microsserviço do Configuration Manager** API. Selecione-o e, em seguida, escolha **selecionar**.  

    4. Sobre o **habilitar acesso** painel, selecione ambas as permissões de aplicativo: **Gravar dados de coleção de CM** e **ler dados de coleção de CM**. Em seguida, escolha **selecionar**.  

    5. Sobre o **adicionar acesso à API** painel, selecione **feito**.  

6. Sobre o **permissões necessárias** página, selecione **conceder permissões**. Selecione **Sim**.  

7. Copie a ID de locatário do AD do Azure. Esse valor é um GUID que é usado para configurar a conexão do Configuration Manager. Selecione **Azure Active Directory** no menu principal e, em seguida, selecione **propriedades**. Cópia de **ID de diretório** valor.  



## <a name="connect-configuration-manager"></a>Conectar o Configuration Manager

Use este procedimento para atualizar do Configuration Manager, conecte-se à área de trabalho de análise e definir as configurações do dispositivo. Esse procedimento é um processo único para anexar a sua hierarquia para o serviço de nuvem.  


### <a name="update-configuration-manager"></a>Atualizar do Configuration Manager

Instale o pacote de cumulativo de atualizações do Configuration Manager versão 1810 (4486457) para dar suporte à integração com a área de trabalho de análise. Para obter mais informações sobre esta atualização, consulte [atualização cumulativa para o branch atual do Configuration Manager, versão 1810](https://support.microsoft.com/help/4486457).

1. Atualize o site com o pacote cumulativo de atualizações da versão 1810. Para obter mais informações, confira [Instalar atualizações no console](/sccm/core/servers/manage/install-in-console-updates).  

2. Atualize clientes. Para simplificar este processo, considere o uso da atualização automática do cliente. Para obter mais informações, consulte [Atualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  


### <a name="connect-to-the-service"></a>Conectar-se ao serviço

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e selecione o nó **Serviços do Azure**. Selecione **configurar serviços do Azure** na faixa de opções.  

2. Sobre o **serviços do Azure** página do Assistente de serviços do Azure, defina as seguintes configurações:  

    - Especifique um **nome** para o objeto no Configuration Manager  

    - Especifique um opcional **descrição** para ajudá-lo a identificar o serviço  

    - Selecione **análise de área de trabalho** na lista de serviços disponíveis  
  
   Selecione **Avançar**.  

3. Sobre o **aplicativo** , selecione apropriado **ambiente do Azure**. Em seguida, selecione **importação** para o aplicativo web. Defina as seguintes configurações na **importar aplicativos** janela:  

    - **Nome do locatário do Azure AD**: Esse nome é como ele é chamado no Configuration Manager  

    - **ID de locatário do Azure AD**: O **ID de diretório** você copiou do Azure AD   

    - **ID do cliente**: O **ID do aplicativo** você copiou do aplicativo Azure AD   

    - **Chave secreta**: A tecla **valor** você copiou do aplicativo Azure AD   

    - **Vencimento da Chave Secreta**: A mesma data de expiração da chave   

    - **URI da ID do aplicativo**: Essa configuração deve preencher automaticamente com o seguinte valor: `https://cmmicrosvc.manage.microsoft.com/`  
  
   Selecione **Verify**e, em seguida, selecione **Okey** para fechar a janela Importar aplicativos. Selecione **próxima** na página do aplicativo do Assistente de serviços do Azure.  

4. Sobre o **dados de diagnóstico** página, defina as seguintes configurações:  

    - **ID comercial**: esse valor deve preencher automaticamente com a ID da sua organização  

    - **Nível de dados de diagnóstico do Windows 10**: Selecione pelo menos **avançado (limitado)**  

    - **Permitir que o nome do dispositivo nos dados de diagnóstico**: selecione **habilitar**  
  
   Selecione **Avançar**. O **funcionalidade disponível** página mostra a funcionalidade de análise de área de trabalho que está disponível com as configurações de dados de diagnóstico da página anterior. Selecione **Avançar**.  

5. Sobre o **coleções** página, defina as seguintes configurações:  

    - **Nome de exibição**: O portal de análise de área de trabalho exibe essa conexão do Configuration Manager usando esse nome. Usá-lo para diferenciar entre hierarquias diferentes. Por exemplo, *laboratório de teste* ou *produção*.  

    - **Coleção de destino**: Esta coleção inclui todos os dispositivos que o Configuration Manager configura com sua ID comercial e as configurações de dados de diagnóstico. É o conjunto completo de dispositivos do Configuration Manager se conecta ao serviço de análise de área de trabalho.  

    - **Dispositivos na coleção de destino usam um proxy de usuário autenticado para comunicação de saída**: Por padrão, esse valor é **não**. Se for necessário em seu ambiente, definido como **Sim**.   

    - **Selecione as coleções específicas para sincronizar com a área de trabalho de análise**: Selecione **adicionar** incluir coleções adicionais. Essas coleções estão disponíveis no portal de análise de área de trabalho para o agrupamento com planos de implantação. Certifique-se de incluir coleções de exclusão do projeto-piloto e piloto.  

        Essas coleções continuam a sincronização como suas alterações de associação. Por exemplo, o seu plano de implantação usa uma coleção com uma regra de associação do Windows 7. Como esses dispositivos de atualização para o Windows 10, e o Configuration Manager avalia a associação da coleção, esses dispositivos soltem fora a coleta e o plano de implantação.  

6. Conclua o assistente.  

O Configuration Manager cria uma política de configurações para configurar dispositivos na coleção de destino. Esta política inclui as configurações de dados de diagnóstico para habilitar dispositivos para enviar dados à Microsoft. Por padrão, clientes atualizam a política a cada hora. Depois de receber as novas configurações, pode ser mais várias horas, antes que os dados estão disponíveis na área de trabalho de análise.

Monitore a configuração de seus dispositivos para análise de área de trabalho. No console do Configuration Manager, vá para o **biblioteca de Software** espaço de trabalho, expanda o **manutenção do Microsoft 365** nó e selecione o **integridade de Conexão** painel.  

Configuration Manager sincroniza qualquer plano de implantação de área de trabalho de análise dentro de 15 minutos de criar a conexão. No console do Configuration Manager, vá para o **biblioteca de Software** espaço de trabalho, expanda o **manutenção do Microsoft 365** nó e selecione o **planos de implantação** nó. 



## <a name="create-a-desktop-analytics-deployment-plan"></a>Criar um plano de implantação de área de trabalho de análise

Use este procedimento para criar um plano de implantação na área de trabalho de análise.

1. Abra o [portal de análise de área de trabalho](https://aka.ms/m365aprod). Usar credenciais que tenham pelo menos **colaboradores do espaço de trabalho** permissões.  

2. Selecione **planos de implantação** no grupo gerenciar.  

3. No **planos de implantação** painel, selecione **criar**.  

4. No **criar plano de implantação** painel, defina as seguintes configurações:  

    - **Nome**: Planejar um nome exclusivo para a implantação, por exemplo `Office 365 pilot`  

    - **Produtos e versões**: Selecione o **Office** produto e a versão mais recente disponível recomendada. Por exemplo, **os clientes do Office 365, versão 1808 (recomendado)**.  

    - **Grupos de dispositivos**: Selecione um ou mais grupos e, em seguida, selecione **definido como grupos de destino**. Grupos com **sccm** como a fonte são coleções sincronizadas do Configuration Manager.  

    - **Regras de preparação**: Essas regras ajudam a determinar quais dispositivos está qualificado para atualização. Selecione **aplicativos do Office** e defina as seguintes configurações:  

        - Atualizar o Office 365 ProPlus de 32 bits para 64 bits. Essa configuração só se aplica a dispositivos que executam uma versão de 64 bits do Windows. A configuração padrão é **Sim**.  

        - Ao atualizar de uma versão anterior do Office, deixe mais antiga preterida aplicativos do Office. Esse comportamento se aplica mesmo se esses aplicativos não existem na versão mais recente do Office. A configuração padrão é **não**.  

        - Baixa instalar o limite de contagem para seus suplementos do Office. O limite padrão é `2%`. Suplementos abaixo desse limite são definidos automaticamente *baixa contagem de instalações*. Análise da área de trabalho não valida esses suplementos durante o piloto. 

            Se um suplemento é instalado em uma porcentagem maior de computadores que esse limite, o plano de implantação marcará o suplemento como *Noteworthy*. Em seguida, você pode decidir sua importância para testar durante a fase piloto.   

    - **Data de conclusão**: Escolha a data pelo qual Office deve ser totalmente implantado para todos os dispositivos de destino.  

5. Selecione **Criar**. O novo plano é exibida na lista de planos de implantação ao seu que está sendo processado. O processamento pode levar até 48 horas antes de prosseguir para a próxima etapa.  

6. Abra o plano de implantação, selecionando seu nome.  

7. No menu de plano de implantação, nos **preparação** grupo, selecione **identificar importância**.  

    1. Sobre o **suplementos do Office** , selecione para mostrar apenas **não revisado** ativos.  

    2. Selecione cada suplemento e, em seguida, selecione **editar**. Você pode selecionar mais de um aplicativo para editar ao mesmo tempo.   

    3. Escolha um nível de importância do **importância** lista. Se quiser que a área de trabalho de análise para validar o suplemento durante o piloto, selecione **crítica** ou **importante**. Ele não valida os suplementos marcados como **importante não**. Considere o risco de compatibilidade e outras informações de plano ao se atribuírem níveis de importância.  

        Ao se atribuírem níveis de importância, você também pode escolher o decisão de atualização.  

    4. Selecione **salvar** ao concluir.  

8. No menu de plano de implantação, nos **preparação** grupo, selecione **identificar piloto**.  

    1. Examine os dispositivos recomendados para o piloto.  

    2. Selecione cada dispositivo e selecione **adicionar ao projeto-piloto**. Se discordar com a recomendação, selecione **substituir**.  

        Para obter mais informações sobre como a área de trabalho de análise torna essas recomendações, selecione o ícone de informações no canto superior direito dos **Identify piloto** painel.



## <a name="deploy-office-365-in-configuration-manager"></a>Implantar o Office 365 no Configuration Manager

Use este procedimento para implantar o Office 365 ProPlus no Configuration Manager para o grupo piloto.

- Se você ainda não tiver um, primeiro [criar um aplicativo do Office 365 ProPlus](#bkmk_create-app)  

- [Implantar o aplicativo](#bkmk_deploy-app) usando o plano de implantação de área de trabalho de análise  

- [Instalar o aplicativo](#bkmk_install-app) no Centro de Software em um dispositivo de destino  

<!-- 
- [Monitor](#bkmk_monitor-app) status in Configuration Manager  
 -->

### <a name="bkmk_create-app"></a> Criar um aplicativo do Office 365 ProPlus

1. No console do Configuration Manager, vá para o **biblioteca de Software**e selecione o **gerenciamento de clientes do Office 365** nó. Selecione o **instalador do Office 365** lado a lado no painel.  

2. Sobre o **configurações do aplicativo** , forneça um **nome** para este aplicativo. Por exemplo, `Office 365 ProPlus`. Opcionalmente, especificar uma **descrição**. Especifique o **local do conteúdo** para os arquivos de instalação e em seguida, selecione **próxima**.  

3. Sobre o **configurações do Office** página, selecione **vá para a ferramenta de personalização do Office**. Configure as configurações de implantação necessários para sua instalação do Office 365:  

    1. No **produtos e versões** grupo, selecione **Office 365 ProPlus** na lista e selecione **adicionar**.  

    2. No **linguagem** de grupo, selecione o idioma principal.  

    3. No **Update e atualize** grupo, verifique se a configuração para **desinstale qualquer versão do MSI do Office, incluindo Visio e Project** está **em**.  

    4. Defina as configurações adicionais conforme necessário pela sua organização.  

    5. Ao concluir, selecione **revisão** no canto superior direito. Examine as configurações definidas e, em seguida, selecione **enviar**.  

5. Selecione **Avançar**. Sobre o **implantação** página, selecione **não** para implantá-lo agora. (O procedimento a seguir usa o plano de implantação de área de trabalho de análise para a implantação.) Selecione **próxima** e conclua o assistente.  


### <a name="bkmk_deploy-app"></a> Implantar o Office 365 usando o plano de implantação de área de trabalho de análise

1. No console do Configuration Manager, vá para o **biblioteca de Software**, expanda **área de trabalho de análise de manutenção**e selecione o **planos de implantação** nó.  

2. Selecione seu plano de implantação piloto do Office 365 e, em seguida, selecione **detalhes do plano de implantação** na faixa de opções.  

3. No **criar um piloto do status** lado a lado, escolha **Application** na lista suspensa e selecione **implantar**.  

4. No **geral** página do assistente par implantar Software, selecione **procurar** ao lado de **Software** campo. Selecione seu aplicativo do Office 365, por exemplo, **Office 365 ProPlus**. Com a integração de análise de área de trabalho, o Configuration Manager cria automaticamente uma coleção para o plano de implantação piloto. Selecione **Avançar**.  

5. Sobre o **conteúdo** página, selecione **Add**e, em seguida, selecione **ponto de distribuição**. Selecione um ponto de distribuição disponíveis para hospedar o conteúdo de instalação e, em seguida, selecione **Okey**. Em seguida, selecione **Avançar**.  

6. Sobre o **configurações de implantação** página, selecione **próxima** para aceitar as configurações padrão. (Uma instalação disponível).  

7. Sobre o **agendamento** página, selecione **próxima** para aceitar as configurações padrão. (Disponível assim que possível.)  

8. Sobre o **experiência de usuário** página, selecione **próxima** para aceitar as configurações padrão. (Exibir no Centro de Software e mostrar apenas as notificações para reinicializações do computador).  

9. Sobre o **alertas** página, selecione **próxima** para aceitar as configurações padrão.  

10. Conclua o assistente.  


### <a name="bkmk_install-app"></a> Instalar o Office 365 no Centro de Software

1. Entrar em um dispositivo que é um membro do plano de implantação piloto.  

2. Abra **Centro de Software** e instalar o aplicativo disponível para o Office 365.  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->




## <a name="next-steps"></a>Próximas etapas

Avance para o próximo artigo para saber mais sobre planos de implantação de área de trabalho de análise.
> [!div class="nextstepaction"]  
> [Planos de implantação](/sccm/desktop-analytics/about-deployment-plans)

