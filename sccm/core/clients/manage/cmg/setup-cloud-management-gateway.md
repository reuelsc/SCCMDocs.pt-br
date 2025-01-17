---
title: Configurar o gateway de gerenciamento de nuvem
titleSuffix: Configuration Manager
description: Use este processo passo a passo para configurar um CMG (gateway de gerenciamento de nuvem).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/17/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.collection: M365-identity-device-management
ms.openlocfilehash: 69ad130dddaecf2a9247126802f9c14fb7176db9
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67286594"
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Configurar o gateway de gerenciamento de nuvem para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este processo inclui as etapas necessárias para configurar um CMG (gateway de gerenciamento de nuvem).

> [!Note]  
> O Configuration Manager não habilita esse recurso opcional por padrão. É necessário habilitar esse recurso antes de usá-lo. Para obter mais informações, consulte [Enable optional features from updates (Habilitar recursos opcionais de atualizações)](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).


## <a name="before-you-begin"></a>Antes de começar

Comece lendo o artigo [Planejar o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway). Use esse artigo para determinar o design do CMG.

Use a seguinte lista de verificação para verificar se você tem as informações necessárias e os pré-requisitos para criar um CMG:  

- O ambiente do Azure a ser usado. Por exemplo, a Nuvem Pública do Azure ou a Nuvem do Azure US Government.  

- Um ou mais certificados são necessários para o CMG, dependendo do design. Para obter mais informações, consulte [Certificados do gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).  

- Da versão 1802 e *recomendada* em diante, selecione a **implantação do Azure Resource Manager**. Para obter mais informações, consulte [Azure Resource Manager](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager). Você precisa dos seguintes requisitos para uma implantação do Azure Resource Manager do CMG:  

    - Integração com o [Azure AD](/sccm/core/servers/deploy/configure/azure-services-wizard) para o **Gerenciamento de Nuvem**. A descoberta de usuário do Azure AD não é necessária.  

    - Os provedores de recursos **Microsoft.ClassicCompute** & **Microsoft.Storage** devem estar registrados na assinatura do Azure. Para obter mais informações, consulte [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-supported-services).

    - Um administrador da assinatura precisa entrar.  

- Um nome global exclusivo para o serviço. Esse nome é obtido do [certificado de autenticação de servidor do CMG](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_serverauth).  

- Se habilitar o CMG como um ponto de distribuição de nuvem, o mesmo nome de serviço globalmente exclusivo do CMG escolhido também precisará estar disponível como um nome de conta de armazenamento globalmente exclusivo. Esse nome é obtido do [certificado de autenticação de servidor do CMG](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_serverauth).

- A região do Azure para essa implantação do CMG.  

- A quantidade de instâncias de VM necessárias para escala e redundância.  

- Se você ainda precisar usar a implantação de serviço clássica do Azure no Configuration Manager versão 1810 ou anterior, precisará dos seguintes requisitos:  

    > [!Important]  
    > Da versão 1810 em diante, implantações de serviço clássico no Azure são preteridas no Configuration Manager. Use as implantações do Azure Resource Manager para o gateway de gerenciamento de nuvem. Para obter mais informações, confira [Planejar para CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).  
    >
    > A partir do Configuration Manager versão 1902, o Azure Resource Manager é o único mecanismo de implantação para novas instâncias do gateway de gerenciamento de nuvem.<!-- 3605704 -->

    - ID de assinatura do Azure  

    - Certificado de gerenciamento do Azure  


## <a name="set-up-a-cmg"></a>Configurar um CMG

Execute esse procedimento no site de nível superior. Esse site é um site primário autônomo ou o site de administração central.

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e selecione **Gateway de Gerenciamento de Nuvem**.  

2. Selecione **Criar Gateway de Gerenciamento de Nuvem** na faixa de opções.  

3. Iniciando na versão 1802, na página geral do assistente, selecione **Implantação do Azure Resource Manager** como o método de implantação do CMG.  

    Selecione **Entrar** para autenticar-se com uma conta de administrador de assinatura do Azure. O assistente popula automaticamente os campos restantes com as informações armazenadas durante o pré-requisito de integração do Azure AD. Se você tem várias assinaturas, selecione a **ID da Assinatura** da assinatura que deseja usar.

    > [!Note]  
    > Da versão 1810 em diante, implantações de serviço clássico no Azure são preteridas no Configuration Manager.
    >
    > Se você precisar usar uma implantação de serviço clássica, selecione essa opção nesta página. Primeiro insira sua **ID de assinatura** do Azure. Em seguida, selecione **Procurar** e escolha o arquivo .PFX do certificado de gerenciamento do Azure.

4. Especifique o **ambiente do Azure** para esse CMG. As opções da lista suspensa podem variar conforme o método de implantação.  

5. Selecione **Avançar**. Aguarde enquanto o site testa a conexão com o Azure.  

6. Na página Configurações do assistente, selecione primeiro **Procurar** e escolha o arquivo .PFX do certificado de autenticação de servidor do CMG. O nome desse certificado popula os campos obrigatórios **FQDN do serviço** e **Nome do serviço**.  

   > [!NOTE]  
   > A partir da versão 1802, o certificado de autenticação de servidor do CMG dá suporte a caracteres curinga. Se você usar um certificado curinga, substitua o asterisco (`*`) no campo **FQDN do serviço** pelo nome do host desejado para o CMG.<!--491233-->  

7. Selecione a lista suspensa **Região** para escolher a região do Azure para esse CMG.  

8. Na versão 1802, se estiver usando uma implantação do Azure Resource Manager, selecione uma opção **Grupo de Recursos**.
   1. Se você escolher **Usar existente**, selecione um grupo de recursos existente na lista suspensa. O grupo de recursos selecionado já deve existir na região selecionada na etapa 7. Se você selecionar um grupo de recursos existente e ele estiver em uma região diferente da selecionada anteriormente, haverá falhará no provisionamento do CMG.
   2. Se você escolher **Criar novo**, insira o nome do novo grupo de recursos.

9. No campo **Instância de VM**, insira o número de VMs desse serviço. O padrão é um, mas você pode aumentar para 16 VMs por CMG.  

10. Selecione **Certificados** para adicionar certificados raiz confiáveis do cliente. Adicione até duas ACs raiz confiáveis e quatro ACs intermediárias (subordinadas). Adicione todos os certificados na cadeia de confiança.  

    > [!Note]  
    > Da versão 1806 em diante, ao criar um CMG, não é mais necessário fornecer um certificado raiz confiável na página Configurações. Esse certificado não é necessário ao usar o Azure AD (Azure Active Directory) para autenticação do cliente, mas costumava ser necessário no assistente. Se você estiver usando certificados de autenticação de cliente de PKI, ainda será necessário adicionar um certificado raiz confiável para o CMG.<!--SCCMDocs-pr issue #2872-->  

11. Por padrão, o assistente habilita a opção **Confirmar a Revogação de Certificado do Cliente**. Uma CRL (lista de certificados revogados) deve ser publicada publicamente para que essa verificação funcione. Caso você não publique uma CRL, desmarque essa opção.  

12. Começando na versão 1806, por padrão, o assistente habilita a opção a seguir: **Permitir que o CMG funcione como um ponto de distribuição na nuvem e ofereça conteúdo do Armazenamento do Azure**. Agora um CMG também pode fornecer conteúdo aos clientes. Essa funcionalidade reduz os certificados necessários e o custo das VMs do Azure.  

13. Selecione **Avançar**.  

14. Para monitorar o tráfego do CMG com um limite de 14 dias, escolha a caixa de seleção para ativar o alerta de limite. Em seguida, especifique o limite e a porcentagem de elevação dos níveis de alerta diferentes. Escolha **Avançar** quando terminar.  

15. Examine as configurações e escolha **Avançar**. O Configuration Manager começa a configurar o serviço. Depois de fechar o assistente, levará de cinco a 15 minutos para provisionar completamente o serviço no Azure. Verifique a coluna **Status** do novo CMG para determinar quando o serviço está pronto.  

    > [!Note]  
    > Para solução de problemas de implantação do CMG, use **CloudMgr.log** e **CMGSetup.log**. Para obter mais informações, consulte [Arquivos de log](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).


## <a name="configure-primary-site-for-client-certificate-authentication"></a>Configurar um site primário para a autenticação de certificado de cliente

Se estiver usando [certificados de autenticação de cliente](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_clientauth) para que os clientes se autentiquem no CMG, siga este procedimento para configurar cada site primário.  

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione **Sites**.  

2. Selecione o site primário ao qual os clientes baseados na Internet são atribuídos e escolha **Propriedades**.  

3. Alterne para a guia **Comunicações de Computador Cliente** da folha de propriedades do site primário e marque **Usar o certificado do cliente PKI (autenticação de cliente) quando disponível**.  

4. Se você não publicar uma CRL, desmarque a opção **Os clientes verificam a CRL (lista de certificados revogados) para sistemas de sites**.  


## <a name="add-the-cmg-connection-point"></a>Adicionar o ponto de conexão do CMG

O ponto de conexão do CMG é a função de sistema de sites para comunicação com o CMG. Para adicionar o ponto de conexão do CMG, siga as instruções gerais para [instalar funções do sistema de sites](/sccm/core/servers/deploy/configure/install-site-system-roles). Na página Seleção de Função do Sistema do Assistente Adicionar Funções do Sistema de Sites, selecione **Ponto de conexão do gateway de gerenciamento de nuvem**. Selecione o **Nome do gateway de gerenciamento de nuvem** ao qual esse servidor se conecta. O assistente mostrará a região do CMG selecionado.

> [!Important]
> O ponto de conexão do CMG deve ter um [certificado de autenticação de cliente](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_clientauth) em alguns cenários.

Para solução de problemas de integridade de serviço do CMG, use **CMGService.log** e **SMS_Cloud_ProxyConnector.log**. Para obter mais informações, consulte [Arquivos de log](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).


## <a name="configure-client-facing-roles-for-cmg-traffic"></a>Configurar funções voltadas para o cliente para o tráfego do CMG

Configure os sistemas de sites do ponto de gerenciamento e do ponto de atualização de software para que eles aceitem o tráfego do CMG. Execute este procedimento no site primário, para todos os pontos de gerenciamento e os pontos de atualização de software que atendem a clientes baseados na Internet.  

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Funções do Sistema de Sites e Servidores**. Na guia Página Inicial da faixa de opções, no grupo de modo de exibição, selecione **Servidores com Função**. Em seguida, selecione **Ponto de gerenciamento** na lista.  

2. Selecione o servidor do sistema de sites que deseja configurar para o tráfego do CMG. Selecione a função **Ponto de gerenciamento** no painel de detalhes e, em seguida, selecione **Propriedades** na faixa de opções.  

3. Na folha de propriedades Ponto de gerenciamento, em Conexões de Cliente, marque a caixa ao lado de **Permitir o tráfego do gateway de gerenciamento de nuvem do Configuration Manager**.

    Dependendo do design do CMG e da versão do Configuration Manager, talvez seja necessário habilitar a opção **HTTPS**. Para obter mais informações, consulte [Habilitar ponto de gerenciamento para HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps).  

4. Selecione **OK** para fechar a janela Propriedades de ponto de gerenciamento.  

Repita essas etapas para pontos de gerenciamento adicionais, conforme necessário, e para os pontos de atualização de software.


## <a name="configure-boundary-groups"></a>Configurar grupos de limites

<!--3640932-->
A partir da versão 1902, é possível associar um CMG a um grupo de limites. Essa configuração permite que os clientes façam fallback ou voltem ao CMG padrão para comunicações de cliente de acordo com os relacionamentos de grupos de limite.

Para saber mais em grupos de limites, confira [Configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups).

Quando você [criar ou configurar um grupo de limites](/sccm/core/servers/deploy/configure/boundary-group-procedures), na guia **Referências**, adicione um gateway de gerenciamento de nuvem. Essa ação associará o CMG a esse grupo de limites.


## <a name="configure-clients-for-cmg"></a>Configurar clientes para o CMG

Quando o CMG e as funções do sistema de sites estão em execução, os clientes obtêm o local do serviço do CMG automaticamente na próxima solicitação de local. Os clientes devem estar na intranet para receber o local do serviço do CMG, a menos que você [instale e atribua clientes do Windows 10 usando o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure). O ciclo de sondagem para solicitações de localização é a cada 24 horas. Se você não quiser aguardar a solicitação de local normalmente agendada, force a solicitação reiniciando o serviço de Host de Agente do SMS (ccmexec.exe) no computador.  

> [!Note]
> Por padrão, todos os clientes recebem a política do CMG. Controle esse comportamento com a configuração do cliente [Permitir que os clientes usem um gateway de gerenciamento de nuvem](/sccm/core/clients/deploy/about-client-settings#enable-clients-to-use-a-cloud-management-gateway).

O cliente do Configuration Manager determina automaticamente se ele está na intranet ou na Internet. Se o cliente pode contatar um controlador de domínio ou um ponto de gerenciamento local, ele define seu tipo de conexão como **Atualmente intranet**. Caso contrário, ele alterna para **Atualmente Internet** e usa o local do serviço do CMG para se comunicar com o site.

>[!NOTE]
> Force o cliente a usar sempre o CMG, independentemente se ele está na intranet ou na Internet. Essa configuração é útil para fins de teste ou para clientes em escritórios remotos que você deseja forçar a usar o CMG. Defina a seguinte chave do Registro no cliente:
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`
>
> Especifique também essa configuração durante a instalação do cliente usando a propriedade [CCMALWAYSINF](/sccm/core/clients/deploy/about-client-installation-properties#ccmalwaysinf).

Para verificar se os clientes têm a política que especifica o CMG, abra um prompt de comando do Windows PowerShell como administrador no computador cliente e execute o seguinte comando: `Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}`

Esse comando exibe os pontos de gerenciamento baseado na Internet reconhecidos pelo cliente. Embora o CMG não seja tecnicamente um ponto de gerenciamento baseado na Internet, os clientes os veem como um.

> [!Note]  
> Para solução de problemas de tráfego de clientes do CMG, use **CMGHttpHandler.log**, **CMGService.log** e **SMS_Cloud_ProxyConnector.log**. Para obter mais informações, consulte [Arquivos de log](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).


## <a name="modify-a-cmg"></a>Modificar um CMG

Depois de criar um CMG, modifique algumas de suas configurações. Selecione o CMG no console do Configuration Manager e selecione **Propriedades**. Defina as configurações nas guias a seguir:  

#### <a name="general"></a>Geral

- **Certificado de gerenciamento do Azure**: altere o certificado de gerenciamento do Azure para o CMG. Essa opção é útil ao atualizar o certificado antes da expiração.  

#### <a name="settings"></a>Configurações

- **Arquivo de certificado**: altere o certificado de autenticação de servidor para o CMG. Essa opção é útil ao atualizar o certificado antes da expiração.  

- **Instância de VM**: altere o número de máquinas virtuais utilizadas pelo serviço no Azure. Essa configuração permite dimensionar o serviço vertical ou horizontalmente de forma dinâmica, de acordo com considerações sobre utilização ou custo.  

- **Certificados**: adicione ou remova certificados de Autoridade de Certificação raiz confiável ou intermediária. Essa opção é útil ao adicionar novas ACs ou desativar certificados expirados.  

- **Confirmar a Revogação de Certificado de Cliente**: se você não habilitou essa configuração originalmente ao criar o CMG, habilite-a posteriormente depois de publicar a CRL.  

- **Permitir que o CMG funcione como um ponto de distribuição na nuvem e ofereça conteúdo do Armazenamento do Azure**: começando na versão 1806, essa nova opção é habilitada por padrão. Agora um CMG também pode fornecer conteúdo aos clientes. Essa funcionalidade reduz os certificados necessários e o custo das VMs do Azure.<!--1358651-->  

#### <a name="alerts"></a>Alertas

Reconfigure os alertas a qualquer momento após a criação do CMG.


### <a name="redeploy-the-service"></a>Reimplantar o serviço

Alterações mais significativas, como as seguintes configurações, exigem a reimplantação do serviço:

- Método de implantação clássico no Azure Resource Manager
- Assinaturas
- Nome do serviço
- Privado para a PKI pública
- Região

Sempre mantenha, pelo menos, um CMG ativo para que os clientes baseados na Internet recebam a política atualizada. Os clientes baseados na Internet não podem se comunicar com um CMG removido. Os clientes não reconhecem um novo até que usam um perfil móvel novamente na intranet. Ao criar uma segunda instância do CMG para excluir a primeira, crie também outro ponto de conexão do CMG.

Por padrão, os clientes atualizam a política a cada 24 horas. Portanto, aguarde, pelo menos, um dia depois de criar um novo CMG antes de excluir o antigo. Se os clientes forem desativados ou estiverem sem uma conexão com a Internet, talvez você precise aguardar mais.

Começando com a versão 1802, caso você tenha um CMG no método de implantação clássico, precisará implantar um novo CMG para usar o método de implantação do Azure Resource Manager.<!--509753--> Há duas opções:  

- Caso deseje reutilizar o mesmo nome de serviço:  

    1. Primeiro exclua o CMG clássico, levando em conta as diretrizes de sempre ter, pelo menos, um CMG ativo para os clientes baseados na Internet.  

    2. Crie um novo CMG usando uma implantação do Resource Manager. Reutilize o mesmo certificado de autenticação de servidor.  

    3. Reconfigure o ponto de conexão do CMG para que ele use a nova instância do CMG.  

- Caso deseje usar um novo nome de serviço:  

    1. Crie um novo CMG usando uma implantação do Resource Manager. Use um novo certificado de autenticação de servidor.  

    2. Crie um novo ponto de conexão do CMG e um link com o novo CMG.  

    3. Aguarde, pelo menos, um dia para que os clientes baseados na Internet recebam a política sobre o novo CMG.  

    4. Exclua o CMG clássico.  

> [!Tip]  
> Para determinar o modelo de implantação atual de um CMG:<!--SCCMDocs issue #611-->  
>
> 1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e selecione o nó **Gateway de Gerenciamento de Nuvem**.  
> 2. Selecione a instância do CMG.  
> 3. No painel Detalhes na parte inferior da janela, procure o atributo **Modelo de Implantação**. Para uma implantação do Resource Manager, esse atributo é **Azure Resource Manager**. O modelo de implantação herdado com o certificado de gerenciamento do Azure é exibido como **Azure Service Manager**.
>
> Você também pode adicionar o atributo **Modelo de Implantação** como uma coluna à exibição de lista.  

### <a name="modifications-in-the-azure-portal"></a>Modificações no portal do Azure

Apenas modifique o CMG no console do Configuration Manager. Não há suporte para modificações no serviço ou nas VMs subjacentes diretamente no Azure. As alterações podem ser perdidas sem aviso prévio. Assim como ocorre com qualquer PaaS, o serviço pode recompilar as VMs a qualquer momento. Essas recompilações podem ocorrer para manutenção de hardware de back-end ou para aplicar atualizações no sistema operacional da VM.

### <a name="delete-the-service"></a>Excluir o serviço

Caso precise excluir o CMG, faça isso também no console do Configuration Manager. A remoção manual de componentes no Azure faz com que o sistema fique divergente. Esse estado deixa informações órfãs e comportamentos inesperados podem ocorrer.


## <a name="next-steps"></a>Próximas etapas

- [Monitorar clientes para o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway)
- [Perguntas frequentes sobre o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
