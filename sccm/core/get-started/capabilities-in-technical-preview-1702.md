---
title: Funcionalidades no Technical Preview 1702 do Configuration Manager
description: "Saiba mais sobre os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1702."
ms.custom: na
ms.date: 02/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aedd608d-6db3-4ea5-851d-70f2dcda6bb5
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 3bdbcd1a3c64a1d50f2f6219b2a5e17d60979864
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1702-for-system-center-configuration-manager"></a>Funcionalidades do Technical Preview 1702 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1702. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview. Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de um technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos em um technical preview.    


**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  

##  <a name="send-feedback-from-the-configuration-manager-console"></a>Enviar comentários do console do Configuration Manager

Essa visualização apresenta novas opções de comentários no console do Configuration Manager. As opções de comentários permitem que você envie comentários diretamente para a equipe de desenvolvimento por meio do site de comentários do UserVoice do Configuration Manager.  

>Você pode encontrar a opção **Comentários**:
-  Na faixa de opções, na extremidade esquerda da guia Página Inicial de cada nó.  
   ![Faixa de opções](./media/feedback-home.png)

-  Ao clicar com o botão direito do mouse em qualquer objeto no console.   
    ![Opção ao clicar com o botão direito do mouse](./media/feedback-option.png)   

Escolher **Comentários** abre seu navegador para o site de comentários do UserVoice do Configuration Manager, em https://configurationmanager.uservoice.com/forums/300492-ideas.
##  <a name="changes-for-updates-and-servicing"></a>Alterações em Atualizações e Manutenção
Os itens a seguir são apresentados com essa visualização.

**Opções de atualização mais simples**  
Na próxima vez que sua infraestrutura se qualificar para duas ou mais atualizações, somente a atualização mais recente será baixada. Por exemplo, se sua versão atual do site for duas ou mais antigas do que a versão mais recente disponível, somente a versão de atualização mais recente será baixada automaticamente.  

Você tem a opção de baixar e instalar as outras atualizações disponíveis, mesmo quando elas não são a versão mais atual. No entanto, você receberá um aviso de que a atualização foi substituída por uma mais recente. Para baixar uma atualização *Disponível para Download*, selecione a atualização no console e, em seguida, clique em **Baixar**.

**Limpeza aprimorada de atualizações mais antigas**   
Adicionamos uma função de limpeza automática que exclui os downloads desnecessários da pasta 'EasySetupPayload' no servidor do site.  


## <a name="peer-cache-improvements"></a>Aprimoramentos de cache de pares
A partir desta versão, um computador de origem de cache de pares rejeitará uma solicitação de conteúdo quando o computador de origem do cache de pares atender a qualquer uma das seguintes condições:  
 -  Está no modo de bateria fraca.
 -  A carga de CPU excede 80% no momento em que o conteúdo é solicitado.
 -  A E/S de disco tem um *AvgDiskQueueLength* que excede 10.
 -  Não há mais conexões disponíveis para o computador.   

Você pode definir essas configurações usando a classe de configuração de agente cliente para o recurso de origem par (*SMS_WinPEPeerCacheConfig*) quando usar o SDK do System Center Configuration Manager.

Quando o computador rejeita uma solicitação de conteúdo, o computador solicitante continuará a procurar conteúdo de fontes alternativas em seu pool de locais de fonte de conteúdo disponíveis.   

## <a name="azurediscovery"></a> Usar o Azure Active Directory Domain Services para gerenciar dispositivos, usuários e grupos

Com essa versão de technical preview você pode gerenciar os dispositivos ingressados no domínio gerenciado do Azure AD (Active Directory) Domain Services. Você também pode descobrir dispositivos, usuários e grupos no domínio com vários métodos de Descoberta do Configuration Manager.

A infraestrutura de site de technical preview, clientes e o domínio do Azure AD Domain Services devem ser executados no Azure.


### <a name="set-up-configuration-manager-to-use-azure-ad"></a>Configurar o Configuration Manager para usar o Azure AD
Para usar o Azure AD com o Configuration Manager, você precisará do seguinte:
-   Assinatura do Azure.
-   Azure AD com DS (Domain Services).
-   Um site do Configuration Manager executado em uma VM do Azure que está ingressada no Azure AD.
-   Clientes do Configuration Manager executados no mesmo ambiente do Azure AD.

Para configurar Azure AD Domain Service, consulte [Introdução aos Azure AD Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-getting-started).

### <a name="discover-resources"></a>Descobrir recursos
Depois de configurar o Configuration Manager para ser executado no Azure AD, você pode usar os seguintes métodos de descoberta do Active Directory para pesquisar recursos no Azure AD:  
- Descoberta de sistemas do Active Directory
- Descoberta de Usuário do Active Directory
- Descoberta de grupos do Active Directory  

Para cada método que você usar, edite a consulta LDAP para pesquisar as estruturas de UO do Azure AD, em vez dos contêineres que são comuns ao Active Directory local. Isso exige que você direcione a consulta para pesquisar o Active Directory em sua assinatura do Azure.  

Os exemplos seguintes usam um Azure AD do *contoso.onmicrosoft.com*:
 - **Descoberta do Sistema**   
O Azure AD armazena os dispositivos na UO **Computadores do AADDC**.  Configure o seguinte:  
  - *LDAP://OU=Computadores do AADDC,DC=contoso,DC=onmicrosoft,DC=com*  


- O AAD de **Descoberta de Usuário** armazena os usuários na UO **Usuários do AADDC**.  Configure o seguinte:
  - *LDAP://OU=Usuários do AADDC,DC= contoso,DC=onmicrosoft,DC=com*


- **Descoberta do Grupo**  
O Azure AD não tem uma UO que armazena grupos. Em vez disso, use a mesma estrutura geral das consultas de sistema ou usuário e configure a consulta LDAP para apontar para a UO que contém os grupos que você deseja descobrir.

Para obter mais informações sobre o Azure AD, consulte o seguinte:  
 - [Azure Active Directory Domain Services](https://azure.microsoft.com/en-us/services/active-directory-ds) em azure.microsoft.com.
 - [Documentação do Active Directory Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services) em docs.microsoft.com.

## <a name="conditional-access-device-compliance-policy-improvements"></a>Aprimoramentos na política de conformidade de dispositivo de acesso condicional

Uma nova regra de política de conformidade do dispositivo está disponível para ajudar a bloquear o acesso a recursos corporativos que dão suporte ao acesso condicional, quando os usuários estão usando aplicativos que fazem parte de uma lista de aplicativos fora de conformidade. A lista de aplicativos fora de conformidade pode ser definida pelo administrador ao adicionar a nova regra de conformidade **Aplicativos que não podem ser instalados**. Essa regra exige que o administrador insira o **Nome do Aplicativo**, a **ID do Aplicativo** e o **Editor do Aplicativo** (opcional) ao adicionar um aplicativo à lista fora de conformidade. Essa configuração se aplica apenas a dispositivos iOS e Android.

Além disso, isso ajuda as organizações a reduzir o vazamento de dados por aplicativos não seguros e evita o consumo de dados excessivo por determinados aplicativos.

- Saiba mais [como as políticas de conformidade de dispositivo funcionam](https://docs.microsoft.com/sccm/protect/deploy-use/device-compliance-policies).
- Saiba mais [como criar políticas de conformidade de dispositivo](https://docs.microsoft.com/sccm/protect/deploy-use/create-compliance-policy).

### <a name="try-it-out"></a>Experimente

**Cenário:** identifique aplicativos que podem estar causando o vazamento de dados enviando dados corporativos para fora da empresa ou que está causando consumo de dados excessivo, em seguida, [crie uma política de conformidade de dispositivo de acesso condicional](https://docs.microsoft.com/sccm/protect/deploy-use/create-compliance-policy) que adiciona esses aplicativos à lista de aplicativos fora de conformidade. Isso bloqueará o acesso aos recursos corporativos que dão suporte a acesso condicional até que o usuário possa remover o aplicativo bloqueado.

## <a name="antimalware-client-version-alert"></a>Alerta de versão do cliente de antimalware
Começando com essa versão de visualização, o Configuration Manager Endpoint Protection fornece um alerta se mais de 20% (padrão) dos clientes gerenciados estão usando uma versão expirada do cliente antimalware (ou seja, cliente do Windows Defender ou do Endpoint Protection).

### <a name="try-it-out"></a>Experimente
Certifique-se de que o Endpoint Protection esteja habilitado em todos os clientes de área de trabalho e servidor usando a política de configurações do cliente. Agora você pode exibir a **Versão do Cliente Antimalware** e o **Status de Implantação do Endpoint Protection** acessando **Ativos e Conformidade** > **Visão Geral** > **Dispositivos** > **Todos os Clientes de Desktops e Servidores**. Para verificar se há um alerta, exiba **Alertas** no espaço de trabalho **Monitoramento**. Se mais de 20% dos clientes gerenciados estiver executando uma versão expirada do software antimalware, o alerta de que o cliente antimalware está desatualizado será exibido. Esse alerta não aparece na guia **Monitoramento** > **Visão Geral**. Para atualizar clientes antimalware expirados, habilite as atualizações de software para clientes antimalware.

Para configurar o percentual em que o alerta é gerado, expanda **Monitoramento** > **Alertas** > **Todos os Alertas**, clique duas vezes em **Clientes antimalware desatualizados** e modifique a opção **Acionar alerta se o percentual de clientes gerenciados com uma versão desatualizada do cliente antimalware for de mais de**.

## <a name="compliance-assessment-for-windows-update-for-business-updates"></a>Avaliação de conformidade para atualizações do Windows Update for Business
Agora você pode configurar uma regra de atualização de política de conformidade para incluir um resultado de avaliação do Windows Update for Business como parte da avaliação de acesso condicional.
> [!IMPORTANT]
> Você deve ter o Windows 10 Insider Versão Prévia 15019 ou posterior para usar a avaliação de conformidade para atualizações do Windows Update for Business.

### <a name="allow-windows-update-for-business-to-manage-windows-10-updates"></a>Permitir que o Windows Update for Business gerencie atualizações do Windows 10
Para coletar informações de avaliação de conformidade para atualizações do Windows Update for Business, use o procedimento a seguir para definir a configuração do agente cliente para permitir explicitamente que o Windows Update for Business gerencie as atualizações do Windows 10.
1. No console do Configuration Manager, vá até **Administração** > **Configurações do Cliente**.
2. Nas propriedades de configurações do cliente, vá para **Atualizações de Software** e selecione **Sim** para a configuração **Gerenciar atualizações do Windows 10 com o Windows Update for Business**.

### <a name="create-a-compliance-policy-for-windows-update-for-business-assessment"></a>Criar uma política de conformidade para avaliação do Windows Update for Business
1. No console do Configuration Manager, acesse **Ativos e Conformidade** > **Configurações de Conformidade** > **Políticas de conformidade**.
2. Clique em **Criar Política de Conformidade** ou selecione uma política de conformidade existente para modificar.
3. Na página Geral, forneça um nome e uma descrição, selecione **Regras de conformidade para dispositivos gerenciados com o cliente do Configuration Manager**, defina a gravidade de não conformidade para o relatório e clique em **Avançar**.
4. Na página Plataformas com Suporte, selecione **Windows 10** e clique em **Avançar**.
5. Na página Regras, clique em **Novo...** e, para **Condição**, escolha **Exigir conformidade do Windows Update for Business**. A configuração **Valor** é automaticamente definida como **Verdadeiro**.

A nova política é exibida no nó **Políticas de Conformidade** do espaço de trabalho **Ativos e Conformidade** .

### <a name="deploy-a-compliance-policy"></a>Implantar uma política de conformidade
1. No console do Configuration Manager, acesse **Ativos e Conformidade** > **Configurações de Conformidade** e clique em **Políticas de Conformidade**.
2. Na guia **Início** , no grupo **Implantação** , clique em **Implantar**.
3. Na caixa de diálogo **Implantar Política de Conformidade** , clique em **Procurar** para selecionar a coleção de usuários nos quais você deseja implantar a política.
   Além disso, é possível selecionar opções para gerar alertas quando a política não for compatível e também para configurar o agendamento por meio do qual essa política será avaliada quanto à conformidade.
4. Quando terminar, clique em **OK**.

### <a name="monitor-the-compliance-policy"></a>Monitorar a política de conformidade
Depois de criar a política de conformidade, você pode monitorar os resultados de conformidade no console do Configuration Manager. Para obter detalhes, consulte [Monitorar a política de conformidade](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy).


## <a name="improvements-to-software-center-settings-and-notification-messages-for-high-impact-task-sequences"></a>Aprimoramentos nas configurações e mensagens de notificação do Centro de Software para sequências de tarefas de alto impacto
Esta versão inclui os seguintes aprimoramentos para configurações e mensagens de notificação do Centro de Software para sequências de tarefas de implantação de alto impacto:

- Nas propriedades da sequência de tarefas, agora você pode configurar qualquer sequência de tarefas, incluindo sequências de tarefas que não do sistema operacional, como uma implantação de alto risco. Qualquer sequência de tarefas que atender a determinadas condições será automaticamente definida como de alto impacto. Para obter detalhes, consulte [Gerenciar implantações de alto risco](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments).
- Nas propriedades da sequência de tarefas, você pode optar por usar a mensagem de notificação padrão ou criar sua própria mensagem de notificação personalizada para implantações de alto impacto.
- Nas propriedades da sequência de tarefas, você pode configurar as propriedades do Centro de Software, que incluem tornar uma reinicialização necessária, o tamanho do download da sequência de tarefas e o tempo de execução estimado.
- A mensagem de implantação de alto impacto padrão para atualizações in-loco agora indicam que seus aplicativos, dados e configurações são migrados automaticamente. Anteriormente, a mensagem padrão para qualquer instalação do sistema operacional indicava que todos os aplicativos, dados e configurações seriam perdidos, o que não era verdade para uma atualização in-loco.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Definir uma sequência de tarefas como uma sequência de tarefas de alto impacto
Use o procedimento a seguir para definir uma sequência de tarefas como de alto impacto.
> [!NOTE]
> Qualquer sequência de tarefas que atender a determinadas condições será automaticamente definida como de alto impacto. Para obter detalhes, consulte [Gerenciar implantações de alto risco](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments).

1. No console do Configuration Manager, acesse **Biblioteca de Software** > **Sistemas Operacionais** > **Sequências de Tarefas**.
2. Selecione a sequência de tarefas a ser editada e clique em **Propriedades**.
3. Na guia **Notificação do Usuário**, selecione **Essa é uma sequência de tarefas de alto impacto**.

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Criar uma notificação personalizada para implantações de alto risco
1. No console do Configuration Manager, acesse **Biblioteca de Software** > **Sistemas Operacionais** > **Sequências de Tarefas**.
2. Selecione a sequência de tarefas a ser editada e clique em **Propriedades**.
3. Na guia **Notificação do Usuário**, selecione **Usar texto personalizado**.
>  [!NOTE]
>  É possível definir o texto de notificação do usuário apenas quando **Essa é uma sequência de tarefas de alto impacto** está selecionado.

4. Defina as seguintes configurações (máximo de 255 caracteres para cada caixa de texto):

   **Texto do título da notificação do usuário**: especifica o texto azul exibido na notificação do usuário do Centro de Software. Por exemplo, na notificação do usuário padrão, esta seção contém algo como "Confirmar que você deseja atualizar o sistema operacional neste computador".

   **Texto da mensagem da notificação do usuário**: há três caixas de texto que fornecem o corpo da notificação personalizada.
   - 1º de caixa de texto: especifica o corpo do texto principal, geralmente contendo instruções para o usuário. Por exemplo, na notificação de usuário padrão, esta seção contém algo como "Atualizar o sistema operacional levará tempo e o computador poderá ser reiniciado várias vezes".
   - 2ª caixa de texto: especifica o texto em negrito abaixo do corpo do texto principal. Por exemplo, na notificação de usuário padrão, esta seção contém algo como “Essa atualização in-loco instala o novo sistema operacional e migra automaticamente seus aplicativos, dados e configurações”.
   - 3ª caixa de texto: especifica a última linha de texto sob o texto em negrito. Por exemplo, na notificação do usuário padrão, essa seção contém algo como “Clique em Instalar para começar. Caso contrário, clique em Cancelar”.   

   Digamos que você defina a seguinte notificação personalizada nas propriedades.

   ![Notificação personalizado para uma sequência de tarefas](.\media\user-notification.png)

   A mensagem de notificação a seguir será exibida quando o usuário final abrir a instalação do Centro de Software.

   ![Notificação personalizado para uma sequência de tarefas](.\media\user-notification-enduser.png)

### <a name="configure-software-center-properties"></a>Configurar as propriedades do Centro de Software
Use o procedimento a seguir para configurar os detalhes da sequência de tarefas exibida no Centro de Software. Esses detalhes são apenas para fins informativos.  
1. No console do Configuration Manager, acesse **Biblioteca de Software** > **Sistemas Operacionais** > **Sequências de Tarefas**.
2. Selecione a sequência de tarefas a ser editada e clique em **Propriedades**.
3. Na guia **Geral**, as seguintes configurações do Centro de Software estão disponíveis:
  - **Reinicialização Necessária**: permite que o usuário saiba se uma reinicialização é necessária durante a instalação.
  - **Tamanho do download (MB)**: especifica quantos megabytes são exibidos no Centro de Software para a sequência de tarefas.  
  - **Tempo de execução estimado (minutos)**: especifica o tempo de execução estimado em minutos exibido no Centro de Software para a sequência de tarefas.


## <a name="check-for-running-executable-files-before-installing-an-application"></a>Verificar se há arquivos executáveis antes de instalar um aplicativo

Na caixa de diálogo **Propriedades** de *<deployment type name>* de um tipo de implantação, na guia Comportamento de Instalação, agora você pode especificar um ou mais arquivos executáveis que, se estiverem em execução, bloquearão a instalação do tipo de implantação. O usuário deve fechar o arquivo executável em execução (ou ele pode ser fechado automaticamente para implantações com a finalidade obrigatória) antes de o tipo de implantação poder ser instalado.

### <a name="try-it-out"></a>Experimente.

1.  Nas propriedades de um tipo de implantação do Configuration Manager, escolha a guia **Comportamento de Instalação**.
2.  Escolha **Adicionar** para adicionar um ou mais nomes de arquivo executável que você deseja verificar. Você também pode adicionar um nome de exibição para tornar mais fácil para os usuários identificarem os aplicativos na lista.
3.  Se a implantação tiver a finalidade obrigatória, no assistente de implantação de software, você poderá opcionalmente escolher **Fechar automaticamente todos os executáveis em execução especificados na guia de comportamento de instalação da caixa de diálogo de propriedades do tipo de implantação**.

Se o aplicativo tiver sido implantado como **Disponível** e um usuário final tentar instalar um aplicativo, será solicitado que ele feche todos os executáveis em execução especificados antes de prosseguir com a instalação.

Se o aplicativo tiver sido implantado como **Necessário** e a opção **Fechar automaticamente todos os executáveis em execução especificados na guia de comportamento de instalação da caixa de diálogo de propriedades do tipo de implantação** estiver selecionada, ele verá uma caixa de diálogo informando que os executáveis especificados serão fechados automaticamente quando o prazo da instalação for atingido. Você pode agendar essas caixas de diálogo em **Configurações do Cliente** > **Agente de Computador**. Se você não quiser que o usuário final veja essas mensagens, selecione **Ocultar no Centro de Software e todas as notificações** na guia **Experiência do Usuário** das propriedades da implantação.

Se o aplicativo tiver sido implantado como **Necessário** e a opção **Fechar automaticamente todos os executáveis em execução especificados na guia de comportamento de instalação da caixa de diálogo de propriedades do tipo de implantação** não estiver selecionada, a instalação do aplicativo falhará se um ou mais dos aplicativos especificados estiverem em execução.

## <a name="create-pfx-certificates-with-s-mime-support"></a>Criar certificados PFX com suporte a S MIME

Agora você pode criar um perfil de certificado PFX que dá suporte a S/MIME e implantá-lo para os usuários.  Esse certificado pode então ser usado para criptografia e descriptografia S/MIME em todos os dispositivos que o usuário tiver registrado.

Além disso, agora você pode especificar várias ACs (autoridades de certificação) em várias funções de sistema de sites do Ponto de Registro de Certificado e, em seguida, atribuir quais ACs processam as solicitações como parte do perfil de certificado.

Para dispositivos iOS, você pode associar um perfil de certificado PFX a um perfil de email e habilitar a criptografia S/MIME.  Isso habilita o S/MIME no cliente de email nativo no iOS e associa o certificado de criptografia S/MIME correto a ele.

Para obter mais informações sobre certificados no Configuration Manager, consulte [Introdução aos perfis de certificado no System Center Configuration Manager]( https://docs.microsoft.com/sccm/protect/deploy-use/introduction-to-certificate-profiles).


## <a name="new-compliance-settings-for-ios-devices"></a>Novas configurações de conformidade para dispositivos iOS

Adicionamos novas configurações que podem ser usadas nos itens de configuração dos dispositivos iOS. Essas são configurações que anteriormente estavam no Microsoft Intune em uma configuração autônoma e agora estão disponíveis quando você usa o Intune com o Configuration Manager. Se você precisar de ajuda com qualquer uma dessas configurações, consulte [Configurações de política do iOS no Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/ios-policy-settings-in-microsoft-intune).

- **Sincronizar dados de aplicativos gerenciados para iCloud**
- **Entrega para continuar atividades em outro dispositivo**
- **Compartilhamento de Fotos do iCloud**
- **Biblioteca de Fotos do iCloud**
- **Confiar em novos autores de aplicativos empresariais**
- **Permitir que o usuário baixe o conteúdo da iBook Store sinalizado como 'Erotismo'** (apenas modo supervisionado)
- **Forçar Apple Watches emparelhados a usar a detecção de pulso**
- **Senha para solicitações de saída do AirPlay**
- **Modificar configurações da conta** (somente no modo supervisionado)
- **Alterações nas configurações de uso de dados para celular do aplicativo** (somente no modo supervisionado)
- **Apagar todo o conteúdo e as configurações** (somente no modo supervisionado)
- **Configurar restrições no dispositivo** (somente no modo supervisionado)
- **Usar o emparelhamento de host para controlar os dispositivos com os quais um dispositivo iOS pode ser emparelhado** (somente no modo supervisionado)
- **Instalar perfis de configuração e certificados** (somente no modo supervisionado)
- **Modificação do nome do dispositivo** (somente no modo supervisionado)
- **Modificação de senha** (somente no modo supervisionado)
- **Emparelhamento do Apple Watch** (somente no modo supervisionado)
- **Modificação das configurações de notificação** (somente no modo supervisionado)
- **Modificação de papel de parede** (somente no modo supervisionado)
- **Modificação das configurações de envio de diagnósticos** (somente no modo supervisionado)
- **Modificação de Bluetooth** (somente no modo supervisionado)
- **AirDrop** (somente no modo supervisionado)
- **Usar Siri para consultar o conteúdo da Internet gerado pelo usuário** (somente no modo supervisionado)
- **Filtro de profanidade da Siri** (somente no modo supervisionado)
- **Retornar resultados da Internet em pesquisa de Destaque** (somente no modo supervisionado)
- **Pesquisa de definição de palavra** (somente no modo supervisionado)
- **Teclados preditivos** (somente no modo supervisionado)
- **Correção automática** (somente no modo supervisionado)
- **Verificação ortográfica do teclado** (somente no modo supervisionado)
- **Atalhos de teclado** (somente no modo supervisionado)
<!--- - **Enterprise app trust settings modification** --->
- **Instalação de aplicativos usando somente o Apple Configurator e o iTunes** (somente no modo supervisionado)
- **Downloads automáticos de aplicativos** (somente no modo supervisionado)
- **Fazer alterações nas configurações do aplicativo Encontrar Meus Amigos** (somente no modo supervisionado)
- **Acesso à iBooks Store** (somente no modo supervisionado)
- **Aplicativo de mensagens** (somente no modo supervisionado)
- **Podcasts** (somente no modo supervisionado)
- **Apple Music** (somente no modo supervisionado)
- **iTunes Radio** (somente no modo supervisionado)
- **Apple News** (somente no modo supervisionado)
- **Game Center** (somente no modo supervisionado)
- **Tratar o AirDrop como um destino não gerenciado**

## <a name="android-for-work-support"></a>Suporte do Android for Work

Começando com a versão do Technical Preview 1702, você pode associar uma conta do Google ao seu locatário MDM híbrido. Isso permite que você faça o seguinte:

- Registre [dispositivos Android com suporte](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) como Android for Work, criando perfis de trabalho nesses dispositivos registrados
- Aprove aplicativos na loja Play for Work, sincronize-os com o console do Configuration Manager e, em seguida, os implemente nos perfis de trabalho dos dispositivos
- Crie e implante itens de configuração para definir as configurações de perfil de trabalho e senha para esses dispositivos
- Crie e implante itens de política de conformidade e perfis de acesso de recursos para dispositivos Android for Work como você já faz para dispositivos Android
- Executar limpeza seletiva em dispositivos Android for Work

Quando você registra um dispositivo como Android for Work, ele cria um perfil de trabalho no dispositivo que o Intune pode gerenciar. Este perfil de trabalho existe lado a lado com o perfil pessoal no dispositivo Android. Os usuários podem mudar facilmente entre os aplicativos do perfil de trabalho e do perfil pessoal. Você não pode gerenciar itens no perfil pessoal. Os dados e aplicativos pessoais permanecem não gerenciados. O Configuration Manager tem controle total sobre o perfil de trabalho e seu conteúdo e pode removê-lo do dispositivo.

O Android for Work é uma plataforma separada do Android e você precisará decidir qual forma de gerenciamento usar para dispositivos Android que têm suporte aos perfis de trabalho.

### <a name="try-it-out"></a>Experimente!
As seções a seguir descrevem o gerenciamento do Android for Work.

#### <a name="enable-android-for-work-management"></a>Habilitar o gerenciamento do Android for Work
1. Crie uma conta do Google em https://accounts.google.com/SignUp para usar como a conta de administrador do Android for Work que será associada a todas as tarefas de gerenciamento do Android for Work para esse locatário do Intune. Essa pode ser uma conta do Google compartilhada entre os administradores que gerenciam dispositivos Android. Essa é a conta do Google que sua organização usa para gerenciar e publicar aplicativos no console do Play for Work. Você usará essa conta para aprovar os aplicativos na loja do Play for Work, portanto, mantenha o controle do nome da conta e senha.
2. Habilite o registro do Android associando a conta do Google ao locatário do Intune gerenciado no Configuration Manager:
  1. Acesse **Administração** > **Visão Geral** > **Serviços de Nuvem** > **Assinaturas do Microsoft Intune** e selecione sua assinatura do Intune.
  2. Na faixa de opções, clique em **Configurar Plataformas** > **Android** e certifique-se de que **Habilitar registro do Android** esteja selecionado.
  3. Na faixa de opções, clique em **Configurar Plataformas** > **Android for Work**.
  4. Na caixa de diálogo, clique em **Configurar Android for Work no console do Intune**. O console do Intune é aberto no navegador da Web.
  5. Use suas credenciais de administrador do Intune para fazer logon no portal do Intune.
  6. Clique em **Configurar** para abrir o site do Android for Work da Google Play.
  7. Na página de entrada do Google, insira as credenciais da conta do Google da etapa 1 e forneça as informações da sua empresa.
3. Quando você retornar ao portal do Intune, o Android for Work estará habilitado e haverá três opções de registro para dispositivos do Android for Work:
  - **Gerenciar todos os dispositivos como Android** – (desabilitada) todos os dispositivos Android, incluindo dispositivos que dão suporte ao Android for Work, serão registrados como dispositivos Android convencionais
  - **Gerenciar dispositivos com suporte como Android for Work** – (habilitada) todos os dispositivos que dão suporte ao Android for Work são registrados como dispositivos Android for Work. Qualquer dispositivo Android que não tem suporte para Android for Work é registrado como um dispositivo Android convencional.
  - **Gerenciar dispositivos com suporte como Android for Work somente para os usuários nestes grupos** – (teste) permite direcionar o gerenciamento do Android for Work a um conjunto de usuários limitado. Somente os membros dos grupos selecionados que registram um dispositivo que dá suporte ao Android for Work são registrados como dispositivos Android for Work. Todos os outros são registrados como dispositivos Android.
  
> [!NOTE]
> Um problema conhecido impede que a opção **Gerenciar dispositivos com suporte para os usuários somente desses grupos como Android para o trabalho** funcione conforme o esperado. Os dispositivos dos usuários nos grupos Azure AD especificados se registrarão como Android, em vez de Android para o trabalho. Para testar o Android para o trabalho, você deve usar a opção **Gerenciar todos os dispositivos com suporte como Android para o trabalho**.


  Para habilitar o registro do Android for Work, você deve escolher uma das opções inferiores. A opção **Gerenciar dispositivos com suporte como Android for Work somente para os usuários nestes grupos** requer que você configure grupos de segurança do Azure Active Directory primeiro.

Você verá o nome da conta e o nome de organização no portal do Intune quando a associação for concluída. Nesse ponto, você pode fechar ambos os navegadores.

#### <a name="approve-and-deploy-android-for-work-apps"></a>Aprovar e implantar aplicativos do Android for Work
Siga essas etapas para aprovar aplicativos na loja Play for Work, sincronizá-los com o console do Configuration Manager e implantá-los em dispositivos Android for Work gerenciados. Para implantar aplicativos nos perfis de trabalho dos usuários, você precisará aprovar os aplicativos na Play for Work e, então, sincronizar os aplicativos com o console do Configuration Manager.

1. Abra um navegador e acesse: https://play.google.com/work.
2. Entre usando a conta de administrador do Google associada ao seu locatário do Intune.
3. Procure aplicativos que você deseja implantar em seu ambiente e clique em **Aprovar** para cada um deles.
4. No console do Configuration Manager, vá para **Administrador** > **Visão Geral** > **Serviços de Nuvem** > **Android for Work** e clique em **Sincronizar**.
5. Aguarde 10 minutos para os aplicativos serem sincronizados e vá para **Biblioteca de Software** > **Visão Geral** > **Gerenciamento de Aplicativos** > **Informações sobre Licença para Aplicativos da Store**.
6. Clique em um aplicativo sincronizado da Play for Work e clique em **Criar Aplicativo**.
7. Conclua o assistente e clique em **Fechar**.
8. Vá para **Biblioteca de Software** > **Visão Geral** > **Gerenciamento de Aplicativos** > **Aplicativos**, selecione um aplicativo do Android for Work e implante como de costume.

Para sincronizar aplicativos da Play for Work com o Configuration Manager, você deve aprovar pelo menos um aplicativo no site do Play for Work.

#### <a name="enroll-an-android-for-work-device"></a>Registrar um dispositivo Android for Work
A maneira como você registra dispositivos do Android for Work é semelhante ao registro do Android. Baixe e execute o aplicativo de Portal da Empresa para Android em seu dispositivo móvel. Será solicitado que você crie um perfil de trabalho como parte do processo de registro.  Depois de criar o perfil de trabalho, você deve mudar para a versão gerenciada do Portal da Empresa. O Portal da Empresa gerenciado é marcado com uma pequena pasta laranja no canto inferior direito.

#### <a name="create-and-deploy-a-configuration-item"></a>Criar e implantar um item de configuração
O Android for Work tem dois grupos de configuração para itens de configuração:
- Senha
- Perfil de trabalho

Você pode configurar o compartilhamento de conteúdo entre perfis de trabalho, bem como os seguintes itens de configuração em dispositivos executando o Android 6 ou superior:
- O comportamento para aplicativos solicitando permissões específicas
- Se as notificações para aplicativos no perfil de trabalho forem visíveis na tela de bloqueio

Para testar isso, crie um item de configuração por meio do fluxo de trabalho padrão, escolha **Android for Work** na página **Geral** e defina as configurações para cada um dos grupos de configuração, adicionando o item de configuração em uma linha de base e implantando como de costume. Essas configurações serão aplicadas somente a dispositivos registrados como Android for Work e não aos registados como Android.

#### <a name="perform-selective-wipe"></a>Executar limpeza seletiva
Os dispositivos registrados como Android for Work podem apenas ser apagados seletivamente porque você gerencia apenas o perfil de trabalho. Isso protege o perfil pessoal de ser apagado. Executar um apagamento seletivo em um dispositivo Android for Work remove o perfil de trabalho, incluindo todos os aplicativos e dados e cancela o registro do dispositivo.

Para apagar seletivamente um dispositivo Android for Work, use o [processo de apagamento seletivo](https://docs.microsoft.com/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe) normal no console do Configuration Manager.

#### <a name="known-issues-for-android-for-work"></a>Problemas conhecidos do Android para o trabalho
**Configurar a sincronização nos perfis de email do Android para o trabalho os faz falhar na implantação** Uma das opções da interface do usuário do ConfigMgr nos perfis de email do Android para o trabalho é "Programação". Em outras plataformas, isso permite que o administrador configure uma programação de sincronização de email e outros dados de conta de email nos dispositivos móveis em que estão implantados. No entanto, ele não funciona para perfis de email do Android para o trabalho e escolher qualquer opção diferente de "Não configurado" fará com que o perfil não seja implantado em todos os dispositivos.
