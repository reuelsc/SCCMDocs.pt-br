---
title: "Criar e implantar uma política de conformidade de dispositivo | Microsoft Docs"
description: "Saiba como criar e implantar políticas de conformidade do dispositivo no System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0fd76043-d7ee-423d-8c5f-aa7e9ed58ce0
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
robots: noindex
ms.translationtype: Human Translation
ms.sourcegitcommit: 216d288aa7b7f2b98df86f59355d879366dcd44d
ms.openlocfilehash: 4baa6e0fe009f5f7dc33f5ab4adb1ec5e5c5271b
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017

---

# <a name="create-and-deploy-a-device-compliance-policy"></a>Criar e implantar uma política de conformidade de dispositivo

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


## <a name="create-a-compliance-policy"></a>Criar uma política de conformidade

1.  No console do System Center Configuration Manager, escolha **Ativos e Conformidade**.

2.  No espaço de trabalho **Ativos e Conformidade**, expanda **Configurações de Conformidade**e escolha **Políticas de Conformidade**.

3.  Na guia **Início**, no grupo **Criar**, escolha **Criar Política de Conformidade**.

4.  Na página **Geral** do Assistente para Criar a Política de Conformidade, especifique as seguintes informações:

  * **Nome**. Insira um nome exclusivo para a política de conformidade. Você pode usar até 256 caracteres.

  * **Descrição**. Insira uma descrição que dê uma visão geral do perfil VPN e ajudem a identificá-lo no console do Configuration Manager. Você pode usar até 256 caracteres.

  * **Tipo de política de conformidade**. Selecione o tipo de política que você quer criar dependendo de o dispositivo ser gerenciado ou não pelo Configuration Manager. Isso se aplica à versão em questão ou posterior.<br /><br /> Para dispositivos gerenciados pelo Intune, escolha a opção **Regras de conformidade para dispositivos gerenciados sem o cliente do Configuration Manager** . Ao escolher essa opção, você também poderá selecionar o tipo de plataforma ao qual deseja que essa política se aplique.

  * **Severidade de não conformidade para relatórios**. Especifique o nível de severidade que será relatado se esta política de conformidade for avaliada como não compatível. Os níveis de severidade disponíveis são:

     * **Nenhum**. Os dispositivos que não cumprem essa regra de conformidade não relatam uma severidade de falha nos relatórios do Configuration Manager.
     * **Informações**. Os dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha **Informações** nos relatórios do Configuration Manager.   
     * **Aviso**. Os dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha **Aviso** nos relatórios do Configuration Manager.
     * **Crítico**. Os dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha **Crítico** nos relatórios do Configuration Manager.
     * **Crítico com evento**. Os dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha **Crítico** nos relatórios do Configuration Manager. Esse nível de severidade também é registrado como um evento do Windows no log de eventos de aplicativos.      

5.  Na página **Plataformas com Suporte**, escolha as plataformas de dispositivo nas quais esta política de conformidade será avaliada ou escolha **Selecionar todas** para escolher todas as plataformas de dispositivo. As plataformas com suporte são: Windows 7, Windows 8.1 e Windows 10; Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 e Windows Server 2016.

6.  Na página **Regras** , defina uma ou mais regras que definem a configuração que os dispositivos devem ter para que eles sejam avaliados como compatíveis. Quando você cria uma política de conformidade, algumas regras são habilitadas por padrão, mas você pode editar ou excluí-las. Para obter uma lista completa de todas as regras, confira a seção “Regras de política de conformidade” mais adiante neste tópico.

  > [!NOTE]  
  >  Em computadores com Windows, o sistema operacional Windows versão 8.1 será relatado como 6.3 em vez de 8.1. Se a regra de versão do sistema operacional é definida como Windows 8.1 para Windows, em seguida, o dispositivo será relatado como não compatível mesmo que o dispositivo tenha Windows 8.1. Verifique se você está definindo a versão *relatada* correta do Windows para as regras de sistema operacional mínima e máxima. O número de versão deve corresponder à versão que o comando **winver** retorna. Windows Phones não têm esse problema, a versão será relatada como 8.1 conforme o esperado. Para PCs com o sistema operacional Windows 10, a versão deve ser definida como **10.0** mais o número de build do sistema operacional que o comando **winver** retorna.

7.  Na página **Resumo** do assistente, examine as configurações feitas e conclua o assistente.

 A nova política é mostrada no nó **Políticas de Conformidade** do espaço de trabalho **Ativos e Conformidade**.

## <a name="deploy-a-compliance-policy"></a>Implantar uma política de conformidade

1.  No console do Configuration Manager, escolha **Ativos e Conformidade**.

2.  No espaço de trabalho **Ativos e Conformidade**, expanda **Configurações de Conformidade**e escolha **Políticas de Conformidade**.

3.  Na guia **Início**, no grupo **Implantação**, escolha **Implantar**.

4.  Na caixa de diálogo **Implantar Política de Conformidade**, escolha **Procurar** para selecionar a coleção de usuários nos quais você deseja implantar a política.

     Além disso, é possível selecionar opções para gerar alertas quando a política não for compatível e definir o agendamento por meio do qual essa política será avaliada quanto à conformidade.

5.  Quando terminar, escolha **OK**.

## <a name="monitor-the-compliance-policy"></a>Monitorar a política de conformidade

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Para exibir resultados de conformidade no console do Configuration Manager

1.  No console do Configuration Manager, escolha **Monitoramento**.

2.  No espaço de trabalho **Monitoramento**, escolha **Implantações**.

3.  Na lista **Implantações** , selecione a implantação da política de conformidade para a qual você deseja examinar as informações de conformidade.

4.  É possível examinar as informações de resumo sobre a conformidade da implantação da política na página principal. Para exibir informações mais detalhadas, selecione a implantação e, na guia **Início**, no grupo **Implantação**, escolha **Exibir Status** para abrir a página **Status da Implantação**.

    A página **Status da Implantação** tem as seguintes guias:

    -   **Compatível**. Mostra a conformidade da política com base no número de ativos afetados. É possível escolher uma regra para criar um nó temporário no nó **Usuários** ou **Dispositivos** do espaço de trabalho **Ativos e Conformidade**, que contém todos os usuários ou dispositivos que são compatíveis com esta regra. O painel **Detalhes do Ativo** mostra os usuários e os dispositivos compatíveis com a política. Clique duas vezes em um usuário dispositivo na lista para mostrar informações adicionais.

    -   **Erro**. Mostra uma lista de todos os erros da implantação da política selecionada com base no número de ativos afetados. É possível escolher uma regra para criar um nó temporário no nó **Usuários** ou **Dispositivos** do espaço de trabalho **Ativos e Conformidade**, que contém todos os usuários ou dispositivos que geraram erros com esta regra. Ao selecionar um usuário ou dispositivo, o painel **Detalhes do Ativo** mostra os usuários ou os dispositivos afetados pelo problema. Clique duas vezes em um usuário ou dispositivo na lista para mostrar informações adicionais sobre o problema.

    -   **Não compatível**. Mostra uma lista de todas as regras não compatíveis na política com base no número de ativos afetados. É possível escolher uma regra para criar um nó temporário no nó **Usuários** ou **Dispositivos** do espaço de trabalho **Ativos e Conformidade**, que contém todos os usuários ou dispositivos que não são compatíveis com esta regra. Ao selecionar um usuário ou dispositivo, o painel **Detalhes do Ativo** mostra os usuários ou os dispositivos afetados pelo problema. Clique duas vezes em um usuário ou dispositivo na lista para mostrar informações adicionais sobre o problema.

    -   **Desconhecida**. Mostra uma lista de todos os usuários e dispositivos que não relataram a conformidade para a implantação da política selecionada junto com o status atual do cliente dos dispositivos.

#### <a name="to-monitor-the-compliance-status-of-an-individual-device"></a>Para monitorar o status de conformidade de um dispositivo individual

1.  No console do Configuration Manager, escolha o espaço de trabalho **Ativos e conformidade**.

2.  Escolha **Dispositivos**.

3.  Clique com botão direito em uma das colunas para habilitar mais colunas.

  Você pode adicionar as seguintes colunas:

  - **ID do dispositivo do Azure Active Directory**.  O identificador exclusivo para o dispositivo no Azure Active Directory.

  - **Detalhes do erro de conformidade**.  Os detalhes das mensagens de erro quando o processo de ponta a ponta dá errado. Se esta coluna estiver em branco, isso significará que nenhum erro foi encontrado e o status de conformidade foi registrado com êxito.

  - **Local do erro de conformidade**.  Mais detalhes sobre onde ocorreu a falha de compatibilidade. Se esta coluna estiver em branco, isso significará que nenhum erro foi encontrado e o status de conformidade foi registrado com êxito. Exemplos de onde o processo de conformidade poderia falhar: 
      - Cliente do ConfigMgr
      - Ponto de gerenciamento
      - Intune
      - Azure Active Directory
<br></br>
  - **Tempo de avaliação da conformidade**. Última vez em que foi verificada a conformidade.

  - **Hora da definição da conformidade**. Última vez que a conformidade foi atualizada para o Azure Active Directory.

  - **Conformidade de acesso condicional**.  Se a máquina está em conformidade com políticas de acesso condicional ou não.

  > [!IMPORTANT]
  > Essas colunas não são mostradas por padrão.

#### <a name="to-view-intune-compliance-policies-charts"></a>Para exibir gráficos de políticas de conformidade do Intune
1. A partir da versão 1610 do Configuration Manager, no console do Configuration Manager, escolha **Monitoramento**.

2. No espaço de trabalho **Monitoramento**, acesse **Visão Geral** > **Configurações de Conformidade** > **Políticas de Conformidade**.

   Os gráficos a seguir são exibidos:

    - **Conformidade geral do dispositivo**. Mostra a conformidade geral dos dispositivos para todas as políticas de conformidade.
    - **Principais motivos de não conformidade**. Mostra as principais políticas para quais dispositivos não estão em conformidade.

3. Escolha uma seção de um dos gráficos para fazer uma busca detalhada até uma lista de dispositivos nessa categoria.

#### <a name="to-view-a-health-attestation-report"></a>Para exibir um relatório de atestado de integridade

1.  A partir da versão 1602 do Configuration Manager, no console do Configuration Manager, escolha **Monitoramento**.

2.  Para exibir um relatório de resumo do status atual dos dispositivos, pelo respectivo status de conformidade, escolha **Segurança** e, em seguida, **Atestado de Integridade**.

3.  Para exibir um relatório que lista todos os dispositivos e todos os atributos de atestado de integridade, escolha **Segurança** e, em seguida, **Atestado de Integridade**.

## <a name="compliance-policy-rules"></a>Regras de política de conformidade
* **Exigir configurações de senha em dispositivos móveis**. Você pode exigir que os usuários insiram uma senha antes que possam acessar seu dispositivo.

  **Com suporte em:**
    * Windows Phone 8+
    * iOS 6+
    * Android 4.0+
    * Samsung KNOX Standard 4.0+

* **Exigir uma senha para desbloquear um dispositivo ocioso** (atualização 1602). Você pode exigir que os usuários insiram uma senha para acessar o dispositivo que está bloqueado.

  **Com suporte em:**
  * Windows Phone 8+
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Minutos de inatividade antes que a senha seja solicitada** (atualização 1602). Você pode especificar o tempo ocioso antes que o usuário precise inserir novamente sua senha. Defina o valor como uma das opções disponíveis: **1 minuto**, **5 minutos**, **15 minutos**, **30 minutos**, **1 hora**.

  Essa regra deve ser usada com **Exigir uma senha para desbloquear um dispositivo ocioso**. O valor definido aqui determina quando o dispositivo é considerado ocioso e está bloqueado. Quando **Exigir uma senha para desbloquear um dispositivo ocioso** é definido como **True**, o usuário deverá digitar uma senha para acessar o dispositivo bloqueado.

  **Com suporte em:**
  * Windows Phone 8+
  * Windows RT/8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Exigir atualizações automáticas** (atualização 1602). Você pode exigir que os dispositivos com Windows 8.1 ou posterior instalem atualizações automaticamente e pode especificar a classe das atualizações.

  O valor deve ser definido como **Nenhum** para impedir a instalação automática, como **Recomendado** para instalar automaticamente todas as atualizações recomendadas ou como **Importante** para instalar somente as atualizações classificadas como importantes.

  **Com suporte em:**
  * Windows Phone 8+

* **Permitir senha simples**. Você pode permitir que os usuários criem senhas simples, como "1234" ou "1111". Essa configuração fica desabilitada por padrão.

  **Com suporte em:**
  * Windows Phone 8+
  * iOS 6+

* **Tamanho mínimo da senha**. Você pode especificar o número mínimo de dígitos ou caracteres que a senha do usuário deve ter (6 por padrão).

  **Com suporte em:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

  >[!NOTE]
  >Para dispositivos que executam o Windows e são protegidos com uma conta da Microsoft, a política de conformidade não será avaliada corretamente se o **Comprimento mínimo da senha** tiver mais de 8 caracteres ou se o **Número mínimo de conjuntos de caracteres** for maior do que 2.

* **Criptografia de arquivo no dispositivo móvel**. Você pode exigir que o dispositivo seja criptografado para conectar-se aos recursos. Os dispositivos que executam o Windows Phone 8 são criptografados automaticamente. Dispositivos que executam o iOS são criptografados ao definir a configuração **Exigir configurações de senha em dispositivos móveis**. Essa configuração é habilitada por padrão.

  **Com suporte em:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **O dispositivo não deve ser desbloqueado nem modificado**. Se você habilitar essa configuração, os dispositivos desbloqueados (iOS) ou com raiz (Android) não serão compatíveis. Essa configuração fica desabilitada por padrão.

  **Com suporte em:**
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **O perfil de email deve ser gerenciado pelo Intune**. Quando você define essa opção como **Sim**, o dispositivo deverá usar o perfil de email implantado para o dispositivo. O dispositivo será considerado incompatível se perfil de email não estiver implantado no mesmo grupo de usuários que o grupo visado pela política de conformidade.

  Ele também será incompatível se o usuário já tiver configurado uma conta de email no dispositivo que corresponda ao perfil de email do Intune implantado para o dispositivo. Nesse caso, o Intune não pode substituir o perfil de usuário provisionado e, portanto, não é capaz de gerenciá-lo. O usuário pode colocar o dispositivo em conformidade removendo as configurações de email existentes, o que permite que o Intune instale o perfil de email gerenciado.

  Para obter detalhes sobre os perfis de email, veja [Habilitar o acesso ao email corporativo usando perfis de email com o Microsoft Intune](https://technet.microsoft.com/library/dn800672.aspx). Essa configuração fica desabilitada por padrão.

  **Com suporte em:**
  * iOS 6+

* **Perfil de email**. Se a opção **A conta de email deve ser gerenciada pelo Intune** estiver marcada, escolha **Selecionar** para escolher o perfil de email pelo qual os dispositivos devem ser gerenciados. O perfil de email deve estar presente no dispositivo.

  **Com suporte em:**
  * iOS 6+

* **SO mínimo requerido**. Quando um dispositivo não atende ao requisito mínimo de versão do sistema operacional que você especificou, ele será relatado como sem conformidade. Será exibido um link com informações sobre como atualizar. O usuário pode optar por atualizar seus dispositivos após o qual eles serão capazes de acessar os recursos da empresa.

  **Com suporte em:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Versão máxima do SO permitida**. Quando um dispositivo usar uma versão de sistema operacional posterior àquela que você especificou na regra, o acesso aos recursos da empresa será bloqueado e o usuário será solicitado a entrar em contato com o administrador de TI. Até que você altere a regra para permitir a versão do SO, este dispositivo não pode ser usado para acessar recursos da empresa.

  **Com suporte em:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Exigir que os dispositivos sejam relatados como íntegros**(atualização 1602). Você pode definir uma regra para exigir que os dispositivos com Windows 10 sejam obrigatoriamente relatados como íntegros em políticas de conformidade novas ou existentes. Se você habilitar essa configuração, os dispositivos com Windows 10 serão avaliados por meio do HAS (Serviço de Atestado de Integridade) para os seguintes pontos de dados:

  - **O BitLocker está habilitado**. Quando o BitLocker está ativado, o dispositivo pode proteger os dados armazenados na unidade contra acesso não autorizado, quando o sistema é desligado ou entra no modo de hibernação.

   A Criptografia de Unidade de Disco BitLocker do Windows criptografa todos os dados armazenados no volume do sistema operacional Windows. O BitLocker usa o TPM para ajudar a proteger o sistema operacional Windows e os dados do usuário. Ele ajuda a garantir que um computador não seja violado, mesmo se ficar aberto, se for perdido ou roubado.
   
   Se o computador estiver equipado com um TPM compatível, o BitLocker usará o TPM para bloquear as chaves de criptografia que protegem os dados. Consequentemente, as chaves não poderão ser acessadas até que o TPM verifique o estado do computador.

  - **A integridade do código está habilitada**. A integridade do código é um recurso que valida a integridade de um arquivo do driver ou do sistema toda vez que ele é carregado na memória. A integridade do código detecta se um arquivo de sistema ou driver não assinado está sendo carregado no kernel. Ele também detecta se um arquivo do sistema foi alterado por software mal-intencionado que está sendo executado por uma conta de usuário com privilégios de administrador.

  - **A inicialização segura está habilitada**. Quando a Inicialização Segura está habilitada, o sistema é forçado a iniciar em um estado confiável de fábrica. Além disso, quando a Inicialização Segura está habilitada, os principais componentes usados para iniciar o computador devem ter assinaturas criptográficas corretas que sejam de confiança da organização fabricante do dispositivo. O firmware UEFI verifica isso antes de permitir que o computador seja iniciado. Se algum arquivo tiver sido violado, rompendo sua assinatura, o sistema não será iniciado.

  - **O antimalware de inicialização antecipada está habilitado**. Essa configuração aplica-se apenas a PCs. O ELAM (Antimalware de Início Antecipado) fornece proteção para os computadores em sua rede quando estes são iniciados e antes que drivers de terceiros sejam inicializados.
  
   Essa regra está desativada por padrão.

  Para saber mais sobre o funcionamento do serviço HAS, confira [CSP do Atestado de Integridade](https://msdn.microsoft.com/library/dn934876.aspx).

  **Com suporte em:**
  * Windows 10 e Windows 10 Mobile

- **Aplicativos que não podem ser instalados no dispositivo**. Se os usuários instalarem um aplicativo da lista de aplicativos fora de conformidade do administrador, eles serão bloqueados ao tentarem acessar o email corporativo e outros recursos corporativos que deem suporte ao acesso condicional. Essa regra exige o nome do aplicativo e a ID do aplicativo ao adicionar um aplicativo à lista fora de conformidade definida pelo administrador. O editor do aplicativo também pode ser adicionado, mas não é obrigatório.

    **Com suporte em:**
      * iOS 6+
      * Android 4.0+
      * Samsung KNOX Standard 4.0+

### <a name="find-an-app-id"></a>Localizar uma ID do aplicativo

A ID do aplicativo é um identificador que identifica exclusivamente o aplicativo dentro dos serviços de aplicativos da Apple e do Google. Por exemplo, com.contoso.myapp. Para localizar uma:

- **Android**
    - Você pode localizar a ID do aplicativo na URL da Google Play Store usada para criar o aplicativo. Um exemplo de ID do aplicativo: *…?id=com.nomedaempresa.nomedoapp&hl=en*

- **iOS**
    1. Na URL da loja do iTunes, localize o número de identificação, como o mostrado neste exemplo: */id875948587?mt=8*

    2. Em um navegador da Web, vá para a URL a seguir, substituindo o número pelo número de identificação que você acabou de encontrar (nesse caso, o exemplo anterior): https://itunes.apple.com/lookup?id=875948587

    3. Baixe e abra o arquivo de texto.
  
    4. Procure o texto **bundleId**.

    Um exemplo de ID do aplicativo: "*bundleId*":"*com.companyname.appname*" 


