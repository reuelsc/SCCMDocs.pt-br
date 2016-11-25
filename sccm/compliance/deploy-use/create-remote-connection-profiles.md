---
title: "Criar perfis de conexão remota | System Center Configuration Manager"
description: "Use perfis de conexão remota do System Center Configuration Manager para permitir que seus usuários se conectem remotamente a computadores de trabalho."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8c6eabc4-5dda-4682-b03e-3a450e6ef65a
caps.latest.revision: 8
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: fd05211959d844c3658e3c5ead70b0c9a7f90116


---

# <a name="remote-connection-profiles-in-system-center-configuration-manager"></a>Perfis de conexão remota no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use os perfis de conexão remota do System Center Configuration Manager para permitir que seus usuários se conectem remotamente a computadores de trabalho quando não estiverem conectados ao domínio ou se seus computadores pessoais estiverem conectados via Internet.  

 Usuários podem se conectar ao seu computador de trabalho com os seguintes tipos de dispositivo:  

-   Computadores que executam o Microsoft Windows  

-   Dispositivos que executam o iOS  

-   Dispositivos que executam o Android  

Os perfis de conexão remota permitem que você implante configurações de Conexão de Área de Trabalho Remota para os usuários na hierarquia de seu Configuration Manager. Em seguida, os usuários podem usar o portal da empresa para acessar qualquer computador de trabalho primário através da Área de Trabalho Remota usando as configurações de Conexão de Área de Trabalho Remota fornecidas pelo portal da empresa.  

O Microsoft Intune será necessário se você desejar que os usuários se conectem aos seus computadores de trabalho usando o portal da empresa. Se você não estiver usando o Intune, os usuários ainda poderão usar as informações do perfil de conexão remota para se conectarem aos seus computadores de trabalho usando a Área de Trabalho Remota por meio de uma conexão VPN.  

> [!IMPORTANT]  
>  Quando você especifica configurações de perfil de conexão remota usando o console do Configuration Manager, elas são armazenadas na política local do computador cliente. Essas configurações podem substituir as configurações da Área de Trabalho Remota definidas por outro aplicativo. Além disso, se você usar a Política de Grupo do Windows para definir as configurações da Área de Trabalho Remota, as configurações especificadas na Política de Grupo substituirão as que estão definidas usando o Configuration Manager.  

 Quando você instalar o Configuration Manager, um novo grupo de segurança, **Conexão de PC Remota**, será criado. Esse grupo é preenchido quando você implanta um perfil de conexão remota contendo os usuários primários do computador no qual o perfil é implantado. Embora um administrador local possa adicionar nomes de usuário a esse grupo, esses usuários serão removidos do grupo quando os perfis de conexão remota implantados forem avaliados quanto à conformidade na próxima vez.  

 Se você adicionar manualmente um usuário a este grupo, o usuário poderá iniciar conexões remotas, mas as informações da conexão não serão publicadas no portal da empresa.  

 Se você remover manualmente do grupo um usuário adicionado pelo Configuration Manager, o Configuration Manager corrigirá automaticamente essa alteração adicionando o usuário novamente na próxima vez que o perfil de conexão remota for avaliado quanto à conformidade.  

> [!IMPORTANT]  
>  Se o relacionamento de afinidade de dispositivo de usuário entre um usuário e um dispositivo mudar (por exemplo, o computador ao qual um usuário se conecta deixar de ser um dispositivo primário do usuário), o Configuration Manager desabilitará o perfil de conexão remota e as configurações do Firewall do Windows para evitar conexões ao computador.  

## <a name="prerequisites"></a>Pré-requisitos  

### <a name="external-dependencies"></a>Dependências externas  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Servidor de Gateway de Área de Trabalho Remota.|Para permitir que os usuários se conectem à Internet fora do domínio da empresa, você deve instalar e configurar o servidor de Gateway de Área de Trabalho Remota.<br /><br /> Se as configurações de Área de Trabalho Remota ou de Serviços de Terminal forem gerenciadas por outras configurações de Política de Grupo ou aplicativo, os perfis de conexão remota poderão não funcionar corretamente. Quando você implanta perfis de conexão remota por meio do console do Configuration Manager, suas configurações correspondentes são armazenadas na política local do computador cliente. Essas configurações podem substituir as configurações da Área de Trabalho Remota definidas por outro aplicativo. Além disso, se você usar as configurações da Política de Grupo para definir as configurações da Área de Trabalho Remota, as configurações especificadas na Política de Grupo substituirão as definidas pelo Configuration Manager.<br /><br /> Para obter mais informações sobre como instalar e configurar o servidor de Gateway de Área de Trabalho Remota, consulte a documentação do Windows Server.|  
|Se os computadores cliente executarem um firewall baseado em host, ele deverá habilitar o programa mstsc.exe.|Ao configurar um perfil de conexão remota, você deve habilitar a configuração **Permitir exceção do Firewall do Windows para conexões nos domínios do Windows e em redes privadas** . Quando essa configuração é habilitada, o Configuration Manager configura automaticamente o Firewall do Windows para habilitar o programa mstsc.exe. No entanto, se os computadores cliente executarem um firewall baseado em host diferente, configure manualmente essa dependência do firewall.<br /><br /> As configurações de Política de Grupo para definir o Firewall do Windows podem substituir a configuração definida no Configuration Manager. Se você usar uma Política de Grupo para configurar o Firewall do Windows, verifique se as configurações dessa política não bloqueiam o programa Mstsc.exe.|  

### <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|O Configuration Manager deve estar conectado ao Microsoft Intune (conhecido como uma configuração híbrida).|Para obter mais informações sobre como conectar o Configuration Manager ao Microsoft Intune, consulte Gerenciar dispositivos móveis com o Configuration Manager e o Microsoft Intune.|  
|Para que um usuário possa se conectar a um computador de trabalho na rede da empresa, esse computador deve ser o dispositivo primário do usuário.|Para obter mais informações sobre afinidade de dispositivo de usuário, consulte [Vincular usuários e dispositivos com a afinidade de dispositivo de usuário](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).|  
|Permissões específicas de segurança devem ter sido concedidas para gerenciar os perfis de conexão remota.|A função de segurança de **Gerenciador de Configurações de Conformidade** inclui as permissões necessárias para gerenciar os perfis de conexão remota. Para obter mais informações, consulte <br />[Configurar administração baseada em funções](/sccm/core/servers/deploy/configure/configure-role-based-administration).|  

## <a name="security-and-privacy-considerations-for-remote-connection-profiles"></a>Considerações de segurança e privacidade para perfis de conexão remota  

### <a name="security-considerations"></a>Considerações sobre segurança  

|Prática recomendada de segurança|Mais informações|  
|----------------------------|----------------------|  
|Especificar manualmente a afinidade de dispositivo de usuário, em vez de permitir que os usuários identifiquem o dispositivo principal. Além disso, não habilitar a configuração baseada em uso.|Devido ao fato de que você deve habilitar **Permitir que todos os usuários primários do computador de trabalho conectem-se remotamente** para poder implantar um perfil de conexão remota, sempre especifique manualmente a afinidade de dispositivo de usuário. Não considere as informações coletadas dos usuários ou do dispositivo para autorização. Se você implantar perfis de conexão remota, e um usuário administrativo confiável não especificar a afinidade de dispositivo de usuário, é possível que usuários não autorizados recebam privilégios elevados e sejam capazes de se conectar remotamente aos computadores.<br /><br /> Se você habilitar a configuração baseada no uso, essas informações serão coletadas por meio de mensagens de estado para as quais o Configuration Manager não oferece segurança. Para ajudar a reduzir essa ameaça, use o protocolo IPsec ou a assinatura do protocolo SMB entre os computadores cliente e o ponto de gerenciamento.|  
|Restringir direitos do administrador local no computador do servidor do local.|Um usuário com direitos administrativos locais no servidor do site podem adicionar manualmente membros ao grupo de segurança Conexão de PC Remota que o Configuration Manager cria e mantém automaticamente. Isso poderá resultar na elevação de privilégios porque os membros adicionados a esse grupo recebem permissões de Área de Trabalho Remota.|  

### <a name="privacy-considerations"></a>Considerações sobre privacidade  

-   Se um usuário inicia uma conexão com um computador de trabalho do portal da empresa, um arquivo com extensão rdp ou .wsrdp é baixado e contém o nome do dispositivo e o nome do servidor de Gateway de Área de Trabalho Remota que é necessário para iniciar a sessão da Área de Trabalho Remota. A extensão do arquivo depende do sistema operacional do dispositivo. Por exemplo, os sistemas operacionais Windows 7 e Windows 8 usam um arquivo .rdp e o Windows 8.1 usa um arquivo .wsrdp.  

-   O usuário pode optar por abrir ou salvar o arquivo .rdp. Se o usuário optar por abrir o arquivo .rdp, esse arquivo poderá ser armazenado no cache do navegador da Web, dependendo das configurações de retenção definidas para o navegador. Se o usuário optar por salvar o arquivo, o arquivo não será armazenado no cache do navegador. Ele será salvo até que o usuário o exclua manualmente.  

-   O arquivo .wsrdp é baixado e salvo automaticamente localmente. Esse arquivo será substituído na próxima vez que o usuário executar uma sessão da Área de Trabalho Remota.  

-   Antes de configurar os perfis de conexão remota, considere seus requisitos de privacidade.  


## <a name="create-a-remote-connection-profile"></a>Criar um perfil de conexão remota

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Configurações de Conformidade** > **Perfis de Conexão Remota**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Perfil de Conexão Remota**.  

4.  Na página **Geral** do **Assistente para Criar Perfil de Conexão Remota**, especifique um nome e uma descrição opcional para o perfil usando, no máximo, 256 caracteres para cada um.  

5.  Na página de configurações **Perfil**, especifique as seguintes configurações para o perfil de conexão remota:  

    -   **Nome completo e porta do servidor de Gateway de Área de Trabalho Remota (opcional)** – Especifique o nome do Servidor de Gateway de Área de Trabalho Remota a ser usado para conexões.  

        > [!NOTE]  
        >  O Configuration Manager não dá suporte ao uso de nomes de domínio internacionalizados para especificar um servidor nesta caixa.  
        >   
        >  O nome do servidor deverá ter, no máximo, 256 caracteres e poderá conter caracteres maiúsculos, minúsculos, numéricos, além dos caracteres **–** e **_** , separados por pontos.  

    -   **Permitir conexões somente de computadores que executam a Área de Trabalho Remota com a Autenticação no Nível da Rede**  

6.  selecione **Habilitado** ou **Desabilitado** para cada uma das configurações de conexão a seguir:  

    -   **Permitir conexões remotas para computadores de trabalho**  

    -   **Permitir que todos os usuários primários do computador de trabalho se conectem remotamente**  

    -   **Permitir exceção de Firewall do Windows para conexões nos domínios do Windows e em redes privadas**  

    > [!IMPORTANT]  
    >  Todas as três configurações devem ser as mesmas para que você possa passar essa página do assistente.  

7.  Na página **Resumo**, examine as ações a serem executadas e conclua o assistente.  

 O novo perfil de conexão remota é exibido no nó **Perfis de Conexão Remota** no espaço de trabalho **Ativos e Conformidade** .  

Implantar um perfil de conexão remota  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Configurações de Conformidade** > **Perfis de Conexão Remota**.  

3.  Na lista **Perfis de Conexão Remota** , selecione o perfil de conexão remota que você deseja implantar e, na guia **Início** do grupo **Implantação** , clique em **Implantar**.  

4.  Na caixa de diálogo **Implantar Perfil de Conexão Remota** , especifique as seguintes informações:  

    -   **Coleção** - clique em **Procurar** para selecionar a coleção de dispositivos onde você deseja implantar o perfil de conexão remota.  

    -   **Corrigir regras não compatíveis quando suportadas** – habilite esta opção para corrigir automaticamente o perfil de conexão remota quando for considerado não compatível em um computador cliente, por exemplo, quando não estiver presente.  

    -   **Permitir correção fora da janela de manutenção** – se uma janela de manutenção tiver sido configurada para a coleção na qual você está implantando o perfil de conexão remota, habilite esta opção para permitir que o Configuration Manager corrija o perfil de conexão remota fora da janela de manutenção. Para obter mais informações sobre janelas de manutenção, consulte [Como usar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).  

    -   **Gerar um alerta** - habilite essa opção para configurar um alerta que será gerado se a conformidade do perfil de conexão remota for menor do que uma porcentagem especificada por uma data e hora determinadas. Você também pode especificar se deseja que um alerta seja enviado para o System Center Operations Manager.  

    -   **Especificar o agendamento da avaliação de conformidade para esta linha de base de configuração** - Especifique o agendamento pelo qual o perfil de conexão remota implantado é avaliado nos dispositivos. Você pode especificar um agendamento simples ou personalizado.  

    > [!TIP]  
    >  Se um dispositivo deixa a coleção à qual o perfil de conexão remota foi implantado, as configurações do perfil de conexão remota serão desabilitadas no dispositivo. No entanto, para que esse processo ocorra corretamente, você já deveria ter implantado pelo menos um item de configuração ou linha de base de configuração que contenha um item de configuração do seu site.  
    >   
    >  O perfil será avaliado pelos dispositivos quando o usuário fizer logon.  
    >   
    >  Se dois perfis de conexão remota forem implantados na mesma coleção de dispositivos, no qual em um perfil a opção **Corrigir regras não compatíveis quando suportadas** está marcada e no outro perfil a mesma opção não está marcada, e se os dois perfis de conexão remota contiverem configurações de conexão diferentes, então o perfil em que a opção não está marcada poderá substituir as configurações do outro perfil. O Configuration Manager não dá suporte a este tipo de implantação de perfil de conexão remota.  

5.  Clique em **OK** para fechar a caixa de diálogo **Implantar Perfil de Conexão Remota** e criar a implantação.  

## <a name="monitor-a-remote-connection-profile"></a>Monitorar um perfil de conexão remota  

### <a name="view-compliance-results-in-the-configuration-manager-console"></a>Exibir resultados de conformidade no console do Configuration Manager  

1.  No console do Configuration Manager, clique em **Monitoramento** > **Implantações**.  

3.  Na lista **Implantações** , selecione a implantação do perfil de conexão remota para a qual deseja examinar as informações de conformidade.  

4.  Você pode examinar as informações de resumo sobre a conformidade da implantação do perfil de conexão remota na página principal. Para exibir informações mais detalhadas, selecione a implantação do perfil de conexão remota e, na guia **Início** do grupo **Implantação** , clique em **Exibir Status** para abrir a página **Status da Implantação** .  

     A página **Status da Implantação** contém as seguintes guias:  

    -   **Compatível:** exibe a conformidade do perfil de conexão remota com base no número de ativos afetados. Você pode clicar duas vezes em uma regra para criar um nó temporário no nó **Usuários** do espaço de trabalho **Ativos e Conformidade** . Esse nó contém todos os dispositivos que são compatíveis com o perfil de conexão remota. O painel **Detalhes do Ativo** também exibe os dispositivos compatíveis com esse perfil. Clique duas vezes em um dispositivo na lista para exibir informações adicionais.  

        > [!IMPORTANT]  
        >  O perfil de conexão remota não será avaliado se não for aplicável a um dispositivo cliente. No entanto, ele é retornado como compatível.  

    -   **Erro:** exibe uma lista de todos os erros da implantação do perfil de conexão remota selecionado com base no número de ativos afetados. Você pode clicar duas vezes em uma regra para criar um nó temporário no nó **Usuários** do espaço de trabalho **Ativos e Conformidade** . Esse nó contém todos os dispositivos que geraram erros com esse perfil. Quando você seleciona um dispositivo, o painel **Detalhes do Ativo** exibe os dispositivos afetados pelo problema selecionado. Clique duas vezes em um dispositivo na lista para exibir informações adicionais sobre o problema.  

    -   **Não Compatível:** exibe uma lista de todas as regras não compatíveis no perfil de conexão remota com base no número de ativos afetados. Você pode clicar duas vezes em uma regra para criar um nó temporário no nó **Usuários** do espaço de trabalho **Ativos e Conformidade** . Esse nó contém todos os dispositivos não compatíveis com esse perfil. Quando você seleciona um dispositivo, o painel **Detalhes do Ativo** exibe os dispositivos afetados pelo problema selecionado. Clique duas vezes em um dispositivo na lista para exibir informações adicionais sobre o problema.  

    -   **Desconhecido:** exibe uma lista de todos os dispositivos que não relataram a conformidade para a implantação do perfil de conexão remota selecionado, junto com o status atual do cliente dos dispositivos.  

5.  Na página **Status da Implantação** , você pode examinar informações detalhadas sobre a conformidade do perfil de conexão remota implantado. Um nó temporário é criado no nó **Implantações** , que ajuda você a localizar essas informações novamente com rapidez.  

### <a name="view-compliance-results-with-reports"></a>Exibir resultados de conformidade com relatórios  
 O Configuration Manager inclui relatórios internos que podem ser usados para monitorar informações sobre perfis de conexão remota. Esses relatórios têm a categoria de relatório de **Gerenciamento de Conformidade e Configurações**.  

> [!IMPORTANT]  
>  Você deve usar um caractere curinga (%) ao utilizar os parâmetros **Filtro de dispositivo** e **Filtro de usuário** nos relatórios de configurações de conformidade.  

 Para obter mais informações sobre como configurar relatórios no Configuration Manager, consulte [Relatórios no System Center Configuration Manager](/sccm/core/servers/manage/reporting).  



<!--HONumber=Nov16_HO1-->


