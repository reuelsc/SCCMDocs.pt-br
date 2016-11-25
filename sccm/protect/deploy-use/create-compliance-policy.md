---
title: "Criar e implantar uma política de conformidade do dispositivo | System Center Configuration Manager"
description: "Saiba como criar e implantar políticas de conformidade do dispositivo no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0cba232e-319f-4ae6-9ffa-4cd76c8bcb29
caps.latest.revision: 
author: karthikaraman
ms.author: karaman
manager: angrobe
robots: noindex
translationtype: Human Translation
ms.sourcegitcommit: 5c6cf3c1697b49708aa5192b67b08b700da7dc72
ms.openlocfilehash: bb91f4a711699790bb01f48d32183cf1215b1952

---

# <a name="create-and-deploy-a-device-compliance-policy"></a>Criar e implantar uma política de conformidade de dispositivo

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


## <a name="create-a-compliance-policy"></a>Criar uma política de conformidade

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.

2.  No espaço de trabalho **Ativos e Conformidade** , expanda **Configurações de Conformidade**e clique em **Políticas de Conformidade**.

3. Na guia **Início** , no grupo **Criar** , clique em **Criar Política de Conformidade**.

4. Na página **Geral** do **Assistente para Criar a Política de Conformidade**, especifique as seguintes informações:

  * **Nome**: insira um nome exclusivo para a política de conformidade. Você pode usar no máximo 256 caracteres.
  * **Descrição**: insira uma descrição que dê uma visão geral do perfil VPN e ajudem a identificá-lo no console do Configuration Manager. Você pode usar no máximo 256 caracteres.
  * **Tipo de política de conformidade**: selecione o tipo de política que você quer criar dependendo de o dispositivo ser gerenciado ou não pelo Configuration Manager. **Isso se aplica à versão em questão ou posterior**.<br /><br /> Para dispositivos gerenciados pelo Intune, escolha a opção **Regras de conformidade para dispositivos gerenciados sem o cliente do Configuration Manager** .  Ao escolher essa opção, você também poderá selecionar o tipo de plataforma ao qual deseja que essa política se aplique.
  * **Severidade de não conformidade dos relatórios**: especifique o nível de severidade que será relatado se esta política de conformidade for avaliada como não compatível. Os níveis de severidade disponíveis são os seguintes:<br /><br />
    * **Nenhum** – dispositivos que não cumprem essa regra de conformidade não relatam uma severidade de falha em relatórios do Configuration Manager.
    *  **Informações** – dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha de **Informações** em relatórios do Configuration Manager.   
    * **Aviso** – dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha de **Aviso** em relatórios do Configuration Manager.
    * **Crítico** – dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico** em relatórios do Configuration Manager.
    * **Crítico com evento** – dispositivos que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico com evento** em relatórios do Configuration Manager. Este nível de severidade também é registrado como um evento do Windows no log de eventos do aplicativo.|      

5.  Na página **Plataformas com Suporte** , escolha as plataformas de dispositivo nas quais esta política de conformidade será avaliada ou clique em **Selecionar todas** para escolher todas as plataformas de dispositivo.

6.  Na página **Regras** , defina uma ou mais regras que definem a configuração que os dispositivos devem ter para que eles sejam avaliados como compatíveis. Quando você cria uma política de conformidade, algumas regras são habilitadas por padrão, mas você pode editar ou excluí-las. Para obter uma lista completa de todas as regras, consulte a seção **Regras de política de conformidade** mais adiante neste tópico.

> [!NOTE]  
>  Em PCs com Windows, o sistema operacional Windows versão 8.1 será relatado como 6.3 em vez de 8.1.    Se a regra de versão do sistema operacional é definida como Windows 8.1 para Windows, em seguida, o dispositivo será relatado como não compatível mesmo que o dispositivo tenha Windows OS 8.1. Verifique se você está definindo a versão **relatada** correta do Windows para as regras de sistema operacional mínima e máxima. O número de versão deve corresponder à versão retornada pelo comando winver. Windows Phones não têm esse problema, a versão será relatada como 8.1 conforme o esperado.  
>   
>  Em PCs com o sistema operacional Windows 10, a versão deve ser definida como “10.0” + o número de build do sistema operacional retornado pelo comando winver. Por exemplo, poderia ser algo como 10.0.10586.  
> O Windows 10 Mobile não apresenta esse problema.  
>   
>  ![CA&#95;Win10OSversion](../media/CA_Win10OSversion.png)  

7.  Na página **Resumo** do assistente, examine as configurações feitas e conclua o assistente.

 A nova política é exibida no nó **Políticas de Conformidade** do espaço de trabalho **Ativos e Conformidade** .

## <a name="deploy-a-compliance-policy"></a>Implantar uma política de conformidade

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.

2.  No espaço de trabalho **Ativos e Conformidade** , expanda **Configurações de Conformidade**e clique em **Políticas de Conformidade**.

3.  Na guia **Início** , no grupo **Implantação** , clique em **Implantar**.

4.  Na caixa de diálogo **Implantar Política de Conformidade** , clique em **Procurar** para selecionar a coleção de usuários nos quais você deseja implantar a política.

     Além disso, é possível selecionar opções para gerar alertas quando a política não for compatível e também para configurar o agendamento por meio do qual essa política será avaliada quanto à conformidade.

5.  Quando terminar, clique em **OK**.

## <a name="monitor-the-compliance-policy"></a>Monitorar a política de conformidade

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Para exibir resultados de conformidade no console do Configuration Manager

1.  No console do Configuration Manager, clique em **Monitoramento**.

2.  No espaço de trabalho **Monitoramento** , clique em **Implantações**.

3.  Na lista **Implantações** , selecione a implantação da política de conformidade para a qual você deseja examinar as informações de conformidade.

4.  É possível examinar as informações de resumo sobre a conformidade da implantação da política na página principal. Para exibir informações mais detalhadas, selecione a implantação e, na guia **Início** , no grupo **Implantação** , clique em **Exibir Status** para abrir a página **Status da Implantação** .

     A página **Status da Implantação** contém as seguintes guias:

    -   **Compatível**: exibe a conformidade da política com base no número de ativos afetados. É possível clicar em uma regra para criar um nó temporário no nó **Usuários** ou **Dispositivos** que estão localizados no espaço de trabalho **Ativos e Conformidade** , que contém todos os usuários ou dispositivos que são compatíveis com esta regra. O painel **Detalhes do Ativo** exibe os usuários e os dispositivos compatíveis com a política. Clique duas vezes em um usuário dispositivo na lista para exibir informações adicionais.

    -   **Erro**: exibe uma lista de todos os erros da implantação da política selecionada com base no número de ativos afetados. É possível clicar em uma regra para criar um nó temporário no nó **Usuários** ou **Dispositivos** do espaço de trabalho **Ativos e Conformidade** , que contém todos os usuários ou dispositivos que geraram erros com esta regra. Ao selecionar um usuário ou dispositivo, o painel **Detalhes do Ativo** exibe os usuários ou os dispositivos afetados pelo problema selecionado. Clique duas vezes em um usuário ou dispositivo na lista para exibir informações adicionais sobre o problema.

    -   **Não Compatível**: exibe uma lista de todas as regras não compatíveis na política com base no número de ativos afetados. É possível clicar em uma regra para criar um nó temporário no nó **Usuários** ou **Dispositivos** do espaço de trabalho **Ativos e Conformidade** , que contém todos os usuários ou dispositivos que não são compatíveis com esta regra. Ao selecionar um usuário ou dispositivo, o painel **Detalhes do Ativo** exibe os usuários ou os dispositivos afetados pelo problema selecionado. Clique duas vezes em um usuário ou dispositivo na lista para exibir informações adicionais sobre o problema.

    -   **Desconhecido**: exibe uma lista de todos os usuários e dispositivos que não relataram a conformidade para a implantação da política selecionada junto com o status atual do cliente dos dispositivos.

### <a name="to-view-a-health-attestation-report"></a>Para exibir um Relatório de Atestado de Integridade

1.  **A partir da versão 1602 do Configuration Manager**, no console do Configuration Manager, clique em **Monitoramento**.

2.  Para exibir um relatório de resumo do status atual dos dispositivos, pelo respectivo status de conformidade, clique em **Segurança**. e clique em **Atestado de Integridade**.

3.  Para exibir um relatório que lista todos os dispositivos e todos os atributos de atestado de integridade, clique em **Segurança**. e clique em **Atestado de Integridade**.

## <a name="compliance-policy-rules"></a>Regras de política de conformidade
* **Exigir configurações de senha em dispositivos móveis:** requer que os usuários insiram uma senha antes que possam acessar seu dispositivo.

  **Com suporte em:**
    * Windows Phone 8+
    * iOS 6+
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
* **Exigir uma senha para desbloquear um dispositivo ocioso (atualização 1602):** exige que os usuários insiram uma senha para acessar o dispositivo que está bloqueado.

  **Com suporte em:**
  * Windows Phone 8+
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Minutos de inatividade antes que a senha seja exigida (atualização 1602):** especifica o tempo ocioso antes que o usuário precise inserir novamente sua senha. Defina o valor como uma das opções disponíveis: **1 minuto**, **5 minutos**, **15 minutos**, **30 minutos**, **1 hora**.

  Essa regra deve ser usada com **Exigir uma senha para desbloquear um dispositivo ocioso**. O valor definido aqui determina quando o dispositivo é considerado ocioso e é bloqueado, e  **Exigir uma senha para desbloquear um dispositivo ocioso** definida como **Verdadeira**exigirá que o usuário insira uma senha para acessar o dispositivo bloqueado.

  **Com suporte em:**
  * Windows Phone 8+
  * Windows RT/8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Requer atualizações automáticas (atualização 1602):** você pode exigir que os dispositivos com Windows 8.1 ou posterior instalem atualizações automaticamente e especificar a classe das atualizações.

  O valor deve ser definido como **Nenhum** para impedir a instalação automática, como **Recomendado** para instalar automaticamente todas as atualizações recomendadas ou como **Importante** para instalar somente as atualizações classificadas como importantes.

  **Com suporte em:**
  * Windows Phone 8+

* **Permitir senha simples:** permite que os usuários criem senhas simples, como "1234" ou "1111". Essa configuração fica **desabilitada por padrão**.

  **Com suporte em:**
  * Windows Phone 8+
  * iOS 6+

* **Comprimento mínimo da senha:** especifica o número mínimo de dígitos ou caracteres que a senha do usuário deve conter (**6** por padrão).

  **Com suporte em:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  >[!NOTE]
  >Para dispositivos que executam o Windows e são protegidos com uma Conta da Microsoft, a política de conformidade não será avaliada corretamente se o **Comprimento mínimo da senha** tiver mais de 8 caracteres ou se o **Número mínimo de conjuntos de caracteres** for maior do que 2.

* **Criptografia de arquivo no dispositivo móvel:** requer que o dispositivo seja criptografado para se conectar aos recursos. Dispositivos que executam o **Windows Phone 8** são **criptografados automaticamente**. Dispositivos que executam o **iOS** são criptografados ao definir a configuração **Exigir configurações de senha em dispositivos móveis** (habilitado por padrão).

  **Com suporte em:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
* **O dispositivo não pode estar com jailbreak ou com raiz:** se habilitado, dispositivos com jailbreak (iOS) ou com raiz (Android) não serão compatíveis (serão desabilitados por padrão).

  **Com suporte em:**
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
* **O perfil de email deve ser gerenciado pelo Intune:** quando essa opção for definida como Sim, o dispositivo deverá usar o perfil de email implantado para o dispositivo. O dispositivo será considerado incompatível se perfil de email não estiver implantado no mesmo grupo de usuários que o grupo visado pela política de conformidade.

  Ele também será incompatível se o usuário já tiver configurado uma conta de email no dispositivo que corresponda ao perfil de email do Intune implantado para o dispositivo. Nesse caso, o Intune não pode substituir o perfil de usuário provisionado e, portanto, não é capaz de gerenciá-lo. O usuário pode colocar o dispositivo em conformidade removendo as configurações de email existentes, o que permite que o Intune instale o perfil de email gerenciado.

  Para obter detalhes sobre os perfis de email, veja [Habilitar o acesso ao email corporativo usando perfis de email com o Microsoft Intune](https://technet.microsoft.com/library/dn800672.aspx). Essa configuração fica desabilitada por padrão.

  **Com suporte em:**
  * iOS 6+

* **Perfil de email:** se a opção **A conta de email deve ser gerenciada pelo Intune** estiver marcada, clique em **Selecionar** para escolher o perfil de email pelo qual os dispositivos deverão ser gerenciados. O perfil de email deve estar presente no dispositivo.

  **Com suporte em:**
  * iOS 6+

* **SO mínimo requerido:** quando um dispositivo não atender ao requisito mínimo de versão do sistema operacional, ele será relatado como não compatível. Será exibido um link com informações sobre como atualizar. O usuário final pode optar por atualizar seus dispositivos após o qual eles serão capazes de acessar os recursos da empresa.

  **Com suporte em:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
* **Versão máxima do SO permitida:** quando um dispositivo estiver usando uma versão de sistema operacional posterior àquela especificada na regra, o acesso aos recursos da empresa será bloqueado e o usuário será solicitado a entrar em contato com o administrador de TI. Até que haja uma alteração na regra para permitir a versão do SO, este dispositivo não pode ser usado para acessar recursos da empresa.

  **Com suporte em:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
* **Exigir que os dispositivos sejam reportados como íntegros (atualização 1602):** você pode definir uma regra para exigir que dispositivos com Windows 10 sejam obrigatoriamente relatados como íntegros em Políticas de Conformidade novas ou existentes. Se essa configuração for habilitada, os dispositivos com Windows 10 serão avaliados por meio do HAS (Serviço de Atestado de Integridade) para os seguintes pontos de dados:
 - **O BitLocker está habilitado:** quando o Bitlocker está ativado, o dispositivo é capaz de proteger os dados armazenados na unidade contra acesso não autorizado, quando o sistema é desligado ou entra no modo de hibernação.

   A Criptografia de Unidade de Disco BitLocker do Windows criptografa todos os dados armazenados no volume do sistema operacional Windows. O BitLocker usa o TPM para ajudar a proteger o sistema operacional Windows e os dados de usuário, além de ajudar a garantir que um computador não foi violado, mesmo se ele tiver sido deixado sem supervisão, perdido ou roubado.<br />Se o computador estiver equipado com um TPM compatível, o BitLocker usará o TPM para bloquear as chaves de criptografia que protegem os dados. Consequentemente, as chaves não poderão ser acessadas até que o TPM verifique o estado do computador.
  - **Integridade de código habilitada:** a integridade de código é um recurso que valida a integridade de um arquivo do driver ou do sistema toda vez que ele é carregado na memória. A integridade do código detecta se um arquivo do sistema ou do driver não assinado está sendo carregado no kernel, ou se um arquivo do sistema foi modificado por software mal-intencionado que está sendo executado por uma conta de usuário com privilégios de administrador
  - **Inicialização segura habilitada:** quando a Inicialização Segura está habilitada, o sistema é forçado a inicializar em um estado confiável de fábrica. Além disso, quando a Inicialização Segura está habilitada, os principais componentes usados para inicializar o computador devem ter assinaturas criptográficas corretas que sejam de confiança da organização fabricante do dispositivo. O firmware UEFI verifica isso antes de permitir que o computador seja iniciado. Se algum arquivo tiver sido violado, rompendo sua assinatura, o sistema não será inicializado.
  - **Antimalware de Início Antecipado habilitado (aplica-se somente a PCs):** o ELAM (Antimalware de Início Antecipado) fornece proteção para os computadores em sua rede quando estes são iniciados e antes que drivers de terceiros sejam inicializados.<br />Essa regra está desativada por padrão.

  Para saber mais sobre o funcionamento do serviço HAS, confira [CSP do Atestado de Integridade](https://msdn.microsoft.com/library/dn934876.aspx).
  **Com suporte em:**
  * Windows 10 e Windows 10 Mobile

  



<!--HONumber=Nov16_HO1-->


