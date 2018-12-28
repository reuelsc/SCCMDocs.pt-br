---
title: Criar e implantar uma política de conformidade de dispositivo
titleSuffix: Configuration Manager
description: Saiba como criar e implantar políticas de conformidade no Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 0fd76043-d7ee-423d-8c5f-aa7e9ed58ce0
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex
ms.openlocfilehash: 67cc82bdd114c9d525e5a9dacc1e5775d52150dd
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53414915"
---
# <a name="create-and-deploy-a-device-compliance-policy"></a>Criar e implantar uma política de conformidade de dispositivo

*Aplica-se a: System Center Configuration Manager (Branch atual)*


## <a name="create-a-compliance-policy"></a>Criar uma política de conformidade

1. No console do Configuration Manager, escolha **Ativos e Conformidade**.  

2. No workspace **Ativos e Conformidade**, expanda **Configurações de Conformidade**e escolha **Políticas de Conformidade**.  

3. Na guia **Início**, no grupo **Criar**, escolha **Criar Política de Conformidade**.  

4. Na página **Geral** do Assistente para Criar a Política de Conformidade, especifique as seguintes informações:  

    - **Nome**: Insira um nome exclusivo para a política de conformidade. Você pode usar até 256 caracteres.  

    - **Descrição**: Insira uma descrição que dê uma visão geral do perfil VPN e ajudem a identificá-lo no console do Configuration Manager. Você pode usar até 256 caracteres.  

    - **Tipo de política de conformidade**: Selecione o tipo de política que você quer criar dependendo de o dispositivo ser gerenciado ou não pelo Configuration Manager.  
    
    Para dispositivos gerenciados pelo Intune, escolha a opção **Regras de conformidade para dispositivos gerenciados sem o cliente do Configuration Manager** . Ao escolher essa opção, você também poderá selecionar o tipo de plataforma ao qual deseja que essa política se aplique.  

    - **Severidade de não conformidade dos relatórios** – especifique o nível de severidade relatado se essa política de conformidade for avaliada como fora de conformidade. Os níveis de severidade disponíveis são:  

        - **Nenhum**: Dispositivos que não cumprem essa regra de conformidade não relatam uma severidade de falha para relatórios do Configuration Manager.  

        - **Informações**: Os dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha **Informações** nos relatórios do Configuration Manager.  

        - **Aviso**: Os dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha **Aviso** nos relatórios do Configuration Manager.  

        - **Crítico**: Os dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha **Crítico** nos relatórios do Configuration Manager.  

        - **Crítico com evento**: Os dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha **Crítico** nos relatórios do Configuration Manager. O nível de severidade **crítico com evento** também é registrado como um evento do Windows no log de eventos do aplicativo.  

5. Na página **Plataformas Compatíveis**, escolha as plataformas de dispositivo nas quais essa política de conformidade será avaliada. Você também pode **Selecionar tudo** para escolher todas as plataformas de dispositivo. As plataformas com suporte são: O Windows 7, Windows 8.1 e Windows 10; Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 e Windows Server 2016.  

6. Na página **Regras** , defina uma ou mais regras que definem a configuração que os dispositivos devem ter para que eles sejam avaliados como compatíveis. Quando você cria uma política de conformidade, algumas regras são habilitadas por padrão, mas você pode editar ou excluir essas regras. Para obter uma lista completa de todas as regras, consulte a seção “Regras da política de conformidade” mais adiante neste artigo.  

    > [!NOTE]  
    > Em PCs com Windows, Windows versão 8.1 será relatado como 6.3. Se a regra de versão do sistema operacional é definida como Windows 8.1 para Windows, em seguida, o dispositivo será relatado como não compatível mesmo que o dispositivo tenha Windows 8.1. Verifique se você está definindo a versão *relatada* correta do Windows para as regras de sistema operacional mínima e máxima. O número de versão deve corresponder à versão que o comando **winver** retorna. Windows Mobile não apresentam esse problema; a versão será relatada como 8.1 conforme o esperado.  
    > 
    > Para computadores Windows com o Windows 10, a versão deve ser definida como **10.0** mais o número de build do sistema operacional a **winver** comando retorna.  

7. Na página **Resumo** do assistente, examine as configurações feitas e conclua o assistente.  

    A nova política é mostrada no nó **Políticas de Conformidade** do workspace **Ativos e Conformidade**.  


## <a name="deploy-a-compliance-policy"></a>Implantar uma política de conformidade

1. No console do Configuration Manager, escolha **Ativos e Conformidade**.  

2. No workspace **Ativos e Conformidade**, expanda **Configurações de Conformidade**e escolha **Políticas de Conformidade**.  

3. Na guia **Início**, no grupo **Implantação**, escolha **Implantar**.  

4. Na caixa de diálogo **Implantar Política de Conformidade**, escolha **Procurar** para selecionar a coleção de usuários nos quais você deseja implantar a política.  

    Além disso, selecione opções para gerar alertas quando a política não está em conformidade e para definir o agendamento por meio do qual essa política será avaliada quanto à conformidade.  

5. Quando terminar, escolha **OK**.  



## <a name="monitor-the-compliance-policy"></a>Monitorar a política de conformidade

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Para exibir resultados de conformidade no console do Configuration Manager

1. No console do Configuration Manager, escolha **Monitoramento**.  

2. No workspace **Monitoramento**, escolha **Implantações**.  

3. Na lista **Implantações** , selecione a implantação da política de conformidade para a qual você deseja examinar as informações de conformidade.  

4. É possível examinar as informações de resumo sobre a conformidade da implantação da política na página principal. Para exibir informações mais detalhadas, selecione a implantação e, na guia **Início**, no grupo **Implantação**, escolha **Exibir Status** para abrir a página **Status da Implantação**.  

    A página **Status da Implantação** tem as seguintes guias:  

    - **Compatível com**: Mostra a conformidade da política com base no número de ativos afetados. É possível escolher uma regra para criar um nó temporário no nó **Usuários** ou **Dispositivos** do workspace **Ativos e Conformidade**, que contém todos os usuários ou dispositivos que são compatíveis com esta regra. O painel **Detalhes do Ativo** mostra os usuários e os dispositivos compatíveis com a política. Para mostrar mais informações, clique duas vezes em um usuário ou dispositivo da lista.  

    - **Erro**: Mostra uma lista de todos os erros da implantação da política selecionada com base no número de ativos afetados. É possível escolher uma regra para criar um nó temporário no nó **Usuários** ou **Dispositivos** do workspace **Ativos e Conformidade**, que contém todos os usuários ou dispositivos que geraram erros com esta regra. Ao selecionar um usuário ou dispositivo, o painel **Detalhes do Ativo** mostra os usuários ou os dispositivos afetados pelo problema. Para mostrar mais informações sobre o problema, clique duas vezes em um usuário ou dispositivo da lista.  

    - **Fora de conformidade**: Mostra uma lista de todas as regras não compatíveis na política com base no número de ativos afetados. É possível escolher uma regra para criar um nó temporário no nó **Usuários** ou **Dispositivos** do workspace **Ativos e Conformidade**, que contém todos os usuários ou dispositivos que não são compatíveis com esta regra. Ao selecionar um usuário ou dispositivo, o painel **Detalhes do Ativo** mostra os usuários ou os dispositivos afetados pelo problema. Para mostrar mais informações sobre o problema, clique duas vezes em um usuário ou dispositivo da lista.  

    - **Desconhecido**: Mostra uma lista de todos os usuários e dispositivos que não relataram a conformidade para a implantação da política selecionada junto com o status atual do cliente dos dispositivos.  

#### <a name="to-monitor-the-compliance-status-of-an-individual-device"></a>Para monitorar o status de conformidade de um dispositivo individual

1. No console do Configuration Manager, escolha o workspace **Ativos e conformidade**.  

2. Escolha **Dispositivos**.  

3. Para habilitar mais colunas, clique com o botão direito do mouse em uma das colunas. Você pode adicionar as seguintes colunas:  

    > [!Note]  
    > Essas colunas não são mostradas por padrão.  

    - **ID de dispositivo do Active Directory do Azure**: O identificador exclusivo para o dispositivo no Azure Active Directory.  

    - **Detalhes do erro de conformidade**: Detalhes de mensagem de erro quando o processo dá errado. Se esta coluna estiver em branco, isso significará que nenhum erro foi encontrado e o status de conformidade foi registrado com êxito.  

    - **Local do erro de conformidade**: Mais detalhes sobre onde ocorreu a falha de compatibilidade. Se esta coluna estiver em branco, isso significará que nenhum erro foi encontrado e o status de conformidade foi registrado com êxito. Exemplos de onde o processo de conformidade poderia falhar:  

        - Cliente do ConfigMgr  
        - Ponto de gerenciamento  
        - Intune  
        - Azure Active Directory  

    - **Tempo de avaliação de conformidade**: Última vez em que foi verificada a conformidade.  

    - **Hora definida da conformidade**: Última vez que a conformidade foi atualizada para o Azure Active Directory.  

    - **Conformidade de acesso condicional**: Se a máquina está em conformidade com políticas de acesso condicional ou não.  

#### <a name="to-view-intune-compliance-policies-charts"></a>Para exibir gráficos de políticas de conformidade do Intune
1. No console do Configuration Manager, escolha **Monitoramento**. 

2. No workspace **Monitoramento**, acesse **Visão Geral** > **Configurações de Conformidade** > **Políticas de Conformidade**. Os gráficos a seguir são exibidos:  

    - **Conformidade geral do dispositivo**: Mostra a conformidade geral dos dispositivos para todas as políticas de conformidade.  

    - **Principais motivos de não conformidade**: Mostra as principais políticas para quais dispositivos não estão em conformidade.  

3. Escolha uma seção de um dos gráficos para fazer uma busca detalhada até uma lista de dispositivos nessa categoria.  

#### <a name="to-view-a-health-attestation-report"></a>Para exibir um relatório de atestado de integridade

1. No console do Configuration Manager, escolha **Monitoramento**.  

2. Para exibir um relatório de resumo do status atual dos dispositivos, pelo respectivo status de conformidade, escolha **Segurança** e, em seguida, **Atestado de Integridade**.  

3. Para exibir um relatório que lista todos os dispositivos e todos os atributos de atestado de integridade, escolha **Segurança** e, em seguida, **Atestado de Integridade**.  



## <a name="compliance-policy-rules"></a>Regras de política de conformidade

- **Exigir configurações de senha em dispositivos móveis**: Você pode exigir que os usuários insiram uma senha antes que possam acessar seu dispositivo.  

    **Tem suporte em**:  
    - Windows Phone 8+  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Exigir uma senha para desbloquear um dispositivo ocioso**: Você pode exigir que os usuários insiram uma senha para acessar o dispositivo que está bloqueado.  

    **Tem suporte em**:  
    - Windows Phone 8+  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Minutos de inatividade antes que a senha seja exigida**: Você pode especificar o tempo ocioso antes que o usuário precise inserir novamente sua senha. Defina o valor como uma das opções disponíveis: **1 minuto**, **5 minutos**, **15 minutos**, **30 minutos**, **1 hora**.  

    Essa regra deve ser usada com **Exigir uma senha para desbloquear um dispositivo ocioso**. O valor definido aqui determina quando o dispositivo é considerado ocioso e está bloqueado. Quando **Exigir uma senha para desbloquear um dispositivo ocioso** é definido como **True**, o usuário deverá digitar uma senha para acessar o dispositivo bloqueado.  

    **Tem suporte em**:  
    - Windows Phone 8+  
    - Windows RT/8.1  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Exigir atualizações automáticas**: Você pode exigir que os dispositivos com Windows 8.1 ou posterior instalem atualizações automaticamente e pode especificar a classe das atualizações.  

    O valor deve ser definido como **Nenhum** para impedir a instalação automática. Defina como **Recomendado** para instalar automaticamente todas as atualizações recomendadas. Para instalar somente as atualizações classificadas como importantes, defina como **Importante**.  

    **Tem suporte em**:  
    - Windows Phone 8+  

- **Permitir senhas simples**: Você pode permitir que os usuários criem senhas simples, como "1234" ou "1111". Essa configuração fica desabilitada por padrão.  

    **Tem suporte em**:  
    - Windows Phone 8+  
    - iOS 6+  

- **Comprimento mínimo da senha**: Você pode especificar o número mínimo de dígitos ou caracteres que a senha do usuário deve ter (6 por padrão).  

    **Tem suporte em**:  
    - Windows Phone 8+  
    - Windows 8.1  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

    > [!NOTE]  
    > Para dispositivos que executam o Windows e são protegidos com uma conta da Microsoft, a política de conformidade não será avaliada corretamente se o **Comprimento mínimo da senha** tiver mais de 8 caracteres ou se o **Número mínimo de conjuntos de caracteres** for maior do que 2.  

- **Criptografia de arquivo no dispositivo móvel**: Você pode exigir que o dispositivo seja criptografado para conectar-se aos recursos. Os dispositivos que executam o Windows Phone 8 são criptografados automaticamente. Dispositivos que executam o iOS são criptografados ao definir a configuração **Exigir configurações de senha em dispositivos móveis**. Essa configuração é habilitada por padrão.  

    **Tem suporte em**:  
    - Windows Phone 8+  
    - Windows 8.1  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Dispositivo não deve ser desbloqueado ou enraizado**: Se você habilitar essa configuração, (iOS) dispositivos desbloqueados ou com raiz (Android) não são compatíveis. Essa configuração fica desabilitada por padrão.  

    **Tem suporte em**:  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Perfil de email deve ser gerenciado pelo Intune**: Quando você define essa opção como **Sim**, o dispositivo deverá usar o perfil de email implantado para o dispositivo. O dispositivo será considerado incompatível se perfil de email não estiver implantado no mesmo grupo de usuários que o grupo visado pela política de conformidade.  

    Também é não compatível se o usuário já tiver configurado uma conta de email no dispositivo que corresponda ao perfil de email do Intune é implantado no dispositivo. Nesse caso, o Intune não pode substituir o perfil de usuário provisionado e, portanto, não pode gerenciá-lo. O usuário pode colocar o dispositivo em conformidade removendo a configuração de email existente, que permite que o Intune instale o perfil de email gerenciado.  

    Para obter mais informações sobre perfis de email, consulte [habilitar o acesso ao email corporativo usando perfis de email com o Microsoft Intune](https://docs.microsoft.com/intune/email-settings-configure). Essa configuração fica desabilitada por padrão.  

    **Tem suporte em**:  
    - iOS 6+  

- **Perfil de email**: Se a opção A conta de email deve ser gerenciada pelo Intune estiver marcada, escolha **Selecionar** para escolher o perfil de email pelo qual os dispositivos devem ser gerenciados. O perfil de email deve estar presente no dispositivo.  

    **Tem suporte em**:  
    - iOS 6+  

- **Sistema operacional mínimo exigido**: Quando um dispositivo não atender ao requisito mínimo de versão do sistema operacional que você especificar, ele será relatado como não compatível. Será exibido um link com informações sobre como atualizar. O usuário pode optar por atualizar seus dispositivos após o qual eles serão capazes de acessar os recursos da empresa.  

    **Tem suporte em**:  
    - Windows Phone 8+  
    - Windows 8.1  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Versão do sistema operacional máxima permitida**: Quando um dispositivo usar uma versão de sistema operacional posterior àquela que você especificou na regra, o acesso aos recursos da empresa será bloqueado e o usuário será solicitado a entrar em contato com o administrador de TI. Até que você altere a regra para permitir a versão do SO, este dispositivo não pode ser usado para acessar recursos da empresa.  

    **Tem suporte em**:  
    - Windows Phone 8+  
    - Windows 8.1  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Exigir que dispositivos sejam relatados como íntegros**: Você pode definir uma regra para exigir que os dispositivos com Windows 10 sejam obrigatoriamente relatados como íntegros em políticas de conformidade novas ou existentes. Se você habilitar essa configuração, os dispositivos Windows 10 serão avaliados por meio do serviço de atestado de integridade para os seguintes pontos de dados:  

    - **O BitLocker está habilitado**: Quando o BitLocker está ativado, o dispositivo pode proteger os dados armazenados na unidade contra acesso não autorizado, quando o sistema está desligado ou entra no modo de hibernação.  

        A Criptografia de Unidade de Disco BitLocker do Windows criptografa todos os dados armazenados no volume do sistema operacional Windows. O BitLocker usa o TPM para ajudar a proteger o sistema operacional Windows e os dados do usuário. Ele ajuda a garantir que um computador não será adulterado, mesmo se ficar sem supervisão, for perdido ou roubado.  

        Se o computador estiver equipado com um TPM compatível, o BitLocker usará o TPM para bloquear as chaves de criptografia que protegem os dados. Como resultado, as chaves não poderão ser acessadas até que o TPM confirme o estado do computador.  

    - **Integridade de código habilitada**: Integridade de código é um recurso que valida a integridade de um arquivo de sistema ou driver cada vez que ele é carregado na memória. A integridade do código detecta se um arquivo de sistema ou driver não assinado está sendo carregado no kernel. Ele também detecta se um arquivo do sistema foi alterado por software mal-intencionado que está sendo executado por uma conta de usuário com privilégios de administrador.  

    - **Inicialização segura está habilitada**: Quando a Inicialização Segura está habilitada, o sistema é forçado a iniciar em um estado confiável de fábrica. Além disso, quando a Inicialização Segura está habilitada, os principais componentes usados para iniciar o computador devem ter assinaturas criptográficas corretas que sejam de confiança da organização fabricante do dispositivo. O firmware UEFI verifica isso antes de permitir que o computador seja iniciado. Se todos os arquivos foram violados, interrompendo sua assinatura, o sistema não será iniciado.  

    - **Antimalware de início antecipado está habilitado**: Essa configuração aplica-se apenas a PCs. O ELAM (Antimalware de Início Antecipado) fornece proteção para os computadores em sua rede quando estes são iniciados e antes que drivers de terceiros sejam inicializados.  

        Essa regra está desativada por padrão.  

    Para obter mais informações, consulte [CSP do atestado de integridade](https://msdn.microsoft.com/library/dn934876.aspx).  

    **Tem suporte em**:  
    - Windows 10 e Windows 10 Mobile  

    > [!NOTE]  
    > A partir do Configuration Manager 1802, o Centro de Software mostra o item de atestado de integridade do dispositivo não for compatível com. <!--1235616-->   
    > ![Conformidade de dispositivo de atestado de integridade do dispositivo no Centro de Software](./media/Software-Center-noncompliant.PNG)  

- **Aplicativos que não podem ser instalados no dispositivo**: Se os usuários instalarem um aplicativo da lista de aplicativos fora de conformidade do administrador, eles serão bloqueados ao tentarem acessar o email corporativo e outros recursos corporativos que deem suporte ao acesso condicional. Essa regra exige o nome do aplicativo e a ID do aplicativo ao adicionar um aplicativo à lista fora de conformidade definida pelo administrador. O editor do aplicativo também pode ser adicionado, mas não é obrigatório.  

    **Tem suporte em**:  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Tipo de senha necessária**: Especifica se o usuário deve criar uma senha alfanumérica ou numérica. Para senhas alfanuméricas, especifique também o número mínimo de conjuntos de caracteres que a senha deverá conter. Os quatro conjuntos de caracteres são: letras minúsculas, maiúsculas, símbolos e números.  

    **Tem suporte em**:  
    - Windows Phone 8+  
    - Windows 8.1+  
    - iOS 6+  

- **Bloquear depuração de USB no dispositivo**: Você não precisa definir essa configuração, pois a depuração de USB já está desabilitada no Android para dispositivos de trabalho.  

    **Tem suporte em**:  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Bloquear aplicativos de fontes desconhecidas**: Exija que dispositivos impeçam a instalação de aplicativos de fontes desconhecidas. Você não precisa definir essa configuração, pois dispositivos Android for Work sempre restringem a instalação de fontes desconhecidas.  

    **Tem suporte em**:  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Exigir verificação de ameaças em aplicativos**: Essa configuração especifica que o recurso Verificar aplicativos está habilitado no dispositivo.  

    **Tem suporte em**:  
    - Android 4.2 a 4.4  
    - Samsung KNOX Standard 4.0+  


### <a name="find-an-app-id"></a>Localizar uma ID do aplicativo

A ID do aplicativo é um identificador que identifica exclusivamente o aplicativo dentro dos serviços de aplicativos da Apple e do Google. Um exemplo é `com.contoso.myapp`. Para localizar uma:

- **Android**: Encontre o aplicativo na URL que foi usado para criar o aplicativo da loja ID no Google Play. Uma ID do aplicativo de exemplo é: `...?id=com.companyname.appname&hl=en`  

- **iOS**  
    1. Localize o número de ID na URL da loja do iTunes. Por exemplo: `/id875948587?mt=8`  

    2. Em um navegador da web, vá para a URL a seguir, substituindo o número pelo número de identificação que você acabou de encontrar. Por exemplo, `https://itunes.apple.com/lookup?id=875948587`  

    3. Baixe e abra o arquivo de texto.  

    4. Procure o texto **bundleId**. Por exemplo: `"bundleId":"com.companyname.appname"`  

