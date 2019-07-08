---
title: Implantar clientes no Windows
titleSuffix: Configuration Manager
description: Saiba como implantar o cliente do Configuration Manager em computadores Windows.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0f560c5bf4ca9a3b58652bc3c53b83d8cf0479cf
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67551053"
---
# <a name="how-to-deploy-clients-to-windows-computers-in-configuration-manager"></a>Como implantar clientes em computadores Windows no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo apresenta detalhes de como implantar o cliente do Configuration Manager em computadores Windows. Para obter mais informações sobre como planejar e preparar a implantação do cliente, confira estes artigos:
- [Métodos de instalação de cliente](/sccm/core/clients/deploy/plan/client-installation-methods)  
- [Pré-requisitos para a implantação de clientes em computadores com Windows](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers)   
- [Segurança e privacidade para clientes do Configuration Manager](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  
- [Práticas recomendadas para a implantação de cliente](/sccm/core/clients/deploy/plan/best-practices-for-client-deployment)  



##  <a name="BKMK_ClientPush"></a> Instalação do cliente por push

Há três maneiras principais de usar o push de cliente:  

- Quando você configura a instalação do cliente por push para um site, a instalação do cliente é executada automaticamente em computadores que o site detecta. Esse método está no escopo limites configurados do site quando esses limites são configurados como um grupo de limites.  

- Inicie uma instalação do cliente por push executando o Assistente de Instalação do Cliente por Push para uma coleção específica ou um recurso específico em uma coleção.  

- Use o Assistente de Instalação do Cliente por Push para instalar o cliente do Configuration Manager, que pode ser usado para [consultar](/sccm/core/servers/manage/introduction-to-queries) o resultado. A instalação terá êxito apenas se um dos itens retornados pela consulta for o atributo **ResourceID** da classe **Recurso do Sistema**.

Se o servidor do site não puder acessar o computador cliente nem iniciar o processo de instalação, ele repetirá automaticamente a instalação a cada hora. O servidor continua tentando novamente por até sete dias.  

Para ajudar a acompanhar o processo de instalação do cliente, instale um ponto de status de fallback antes de instalar os clientes. Quando você instala um ponto de status de fallback, ele é atribuído automaticamente aos clientes quando eles são instalados pelo método de instalação do cliente por push. Para acompanhar o andamento da instalação do cliente, exiba os relatórios de atribuição e de implantação do cliente.

Os arquivos de log do cliente fornecem informações mais detalhadas para solução de problemas. Os arquivos de log não exigem um ponto de status de fallback. Por exemplo, o arquivo CCM.log no servidor do site registra todos os problemas que ocorrem quando o servidor do site conecta-se ao computador. O arquivo CCMSetup.log no cliente registra o processo de instalação.  

> [!IMPORTANT]  
>  O push do cliente terá êxito apenas se todos os pré-requisitos forem atendidos. Para obter mais informações, consulte [Dependências do método de instalação](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#installation-method-dependencies).


### <a name="configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>Configurar o site para usar automaticamente o push do cliente para os computadores descobertos

1.  No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**.  

2.  Selecione o site para o qual deseja configurar a instalação automática do cliente por push em todo o site.  

3.  Na guia **Página inicial** da faixa de opções, no grupo **Configurações**, selecione **Configurações de Instalação do Cliente** e então **Instalação do Cliente por Push**.  

4.  Na guia **Geral** da janela Propriedades da Instalação do Cliente por Push, selecione **Habilitar a instalação automática do cliente por push em todo o site**.

5. Da versão 1806 em diante, atualizar o site habilita uma verificação do Kerberos para o push do cliente. A opção para **Permitir conexão fallback para NTLM** é habilitada por padrão, o que é consistente com o comportamento anterior. Se o site não puder autenticar o cliente usando Kerberos, ele tentará realizar a conexão novamente usando NTLM. A configuração recomendada para maior segurança é desabilitar essa configuração, o que exige Kerberos sem fallback de NTLM.<!--1358204-->  

    > [!NOTE]  
    > Ao usar o push de cliente para instalar o cliente do Configuration Manager, o servidor do site cria uma conexão remota com o cliente. Da versão 1806 em diante, o site poderá exigir autenticação mútua do Kerberos não permitindo fallback para NTLM antes de estabelecer a conexão. Essa melhoria ajuda a proteger a comunicação entre o servidor e o cliente.  
    > 
    > Dependendo de suas políticas de segurança, seu ambiente pode já preferir ou exigir Kerberos em vez da autenticação NTLM mais antiga. Para saber mais sobre as considerações de segurança desses protocolos de autenticação, leia sobre a [Configuração da política de segurança do Windows para restringir NTLM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations).  
    > 
    > Para usar esse recurso, os clientes devem estar em uma floresta confiável do Active Directory. O Kerberos no Windows depende do Active Directory para autenticação mútua.  

6.  Selecione os tipos de sistema para os quais o Configuration Manager deve enviar por push o software cliente. Selecione se deseja instalar o cliente em controladores de domínio.  

7.  Na guia **Contas**, especifique uma ou mais contas para o Configuration Manager usar ao conectar-se ao computador de destino. Selecione o ícone **Criar**, insira o **Nome de usuário** e a **Senha** (com até 38 caracteres), confirme a senha e, em seguida, selecione **OK**. Especifique, pelo menos, uma conta de instalação do cliente por push. Essa conta deve ter direitos de administrador local no computador de destino para instalar o cliente. Se você não especificar uma conta de instalação do cliente por push, o Configuration Manager tentará usar a conta de computador do sistema de sites. O push do cliente entre domínios falha ao usar a conta de computador do sistema de sites.  

    > [!NOTE]  
    >  Para usar o push do cliente em um site secundário, especifique a conta no site secundário que inicia o push do cliente.  
    >   
    >  Para obter mais informações sobre a conta de instalação do cliente por push, consulte o procedimento a seguir, [Usar o Assistente de Instalação do Cliente por Push](#use-the-client-push-installation-wizard).  

8.  Especificar todas as propriedades de instalação necessárias na guia **Propriedades de Instalação**.

     Se você tiver estendido o esquema do Active Directory para o Configuration Manager, o site publicará as [Propriedades de instalação de cliente](/sccm/core/clients/deploy/about-client-installation-properties) especificadas no Active Directory Domain Services. Quando o CCMSetup é executado sem propriedades de instalação, ele lê essas propriedades do Active Directory.  

    > [!NOTE]  
    >  Se você habilitar a instalação do cliente por push em um site secundário, defina a propriedade **SMSSITECODE** com o código do site do Configuration Manager de seu site primário pai. Se você tiver estendido o esquema do Active Directory para o Configuration Manager, defina essa propriedade como **AUTO** para encontrar automaticamente a atribuição de site correta.


### <a name="use-the-client-push-installation-wizard"></a>Usar o Assistente de Instalação do Cliente por Push

1.  No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**.  

2.  Selecione o site para o qual deseja configurar a instalação automática do cliente por push em todo o site.  

3.  Na guia **Página inicial** da faixa de opções, no grupo **Configurações**, selecione **Configurações de Instalação do Cliente** e então **Instalação do Cliente por Push**.  

4.  Especificar todas as propriedades de instalação necessárias na guia **Propriedades de Instalação**.  

    Se você tiver estendido o esquema do Active Directory para o Configuration Manager, o site publicará as [Propriedades de instalação de cliente](/sccm/core/clients/deploy/about-client-installation-properties) especificadas no Active Directory Domain Services. Quando o CCMSetup é executado sem propriedades de instalação, ele lê essas propriedades do Active Directory.

5.  No console do Configuration Manager, vá até o workspace **Ativos e conformidade**.  

6.  No nó **Dispositivos**, selecione um ou mais computadores. Ou selecione uma coleção de computadores no nó **Coleções de Dispositivos**.  

7.  Na guia **Página Inicial** da faixa de opções, escolha uma destas opções:  

    -   Para efetuar push do cliente para um ou mais dispositivos, no grupo **Dispositivo**, selecione **Instalar Cliente**.  

    -   Para efetuar push do cliente para uma coleção de dispositivos, no grupo **Coleção**, selecione **Instalar Cliente**.  

8. Na página **Antes de Começar** do Assistente para Instalar o Cliente do Configuration Manager, examine as informações e, em seguida, selecione **Avançar**.  

9. Selecione as opções apropriadas na página **Opções de Instalação**.  

10. Examine as configurações de instalação e feche o assistente.  

> [!NOTE]  
> Use esse assistente para instalar clientes mesmo que o site não esteja configurado para o push do cliente.  

##  <a name="BKMK_ClientSUP"></a> Instalação baseada em atualização de software  

A instalação do cliente baseada em atualização de software publica o cliente em um ponto de atualização de software como uma atualização de software. Use esse método para uma primeira instalação ou uma atualização.  

Se o cliente do Configuration Manager estiver instalado em um computador, esse computador receberá a política do cliente do site. Essa política inclui o nome do servidor de ponto de atualização de software e a porta da qual obter atualizações de software.

> [!IMPORTANT]  
>  Para a instalação baseada em atualização de software, use o mesmo servidor WSUS (Windows Server Update Services) para instalação do cliente e atualizações de software. Esse servidor deve ser o ponto de atualização de software ativo em um site primário. Para mais informações, confira [Install a software update point](/sccm/sum/get-started/install-a-software-update-point) (Instalar um ponto de atualização de software).

Se o cliente do Configuration Manager não estiver instalado em um computador, configure e atribua um objeto de Política de Grupo. Essa Política de Grupo especifica o nome do servidor do ponto de atualização de software.  

Não é possível adicionar propriedades de linha de comando a uma instalação do cliente baseada em atualização de software. Se você estender o esquema do Active Directory para o Configuration Manager, a instalação do cliente consultará automaticamente o Active Directory Domain Services para as propriedades de instalação.  

Se você não estendeu o esquema do Active Directory, use a Política de Grupo para provisionar as configurações de instalação do cliente. Essas configurações são aplicadas automaticamente na instalação do cliente baseada em atualização de software. Para obter mais informações, veja a seção sobre [Como provisionar propriedades de instalação do cliente](#BKMK_Provision) e o artigo sobre [Como atribuir clientes a um site](/sccm/core/clients/deploy/assign-clients-to-a-site).  

Use os procedimentos a seguir para configurar computadores sem um cliente do Configuration Manager para usar o ponto de atualização de software. Também há um procedimento para publicar o software cliente para o ponto de atualização de software.  

> [!TIP]  
>  Se os computadores estiverem em um estado de reinicialização pendente após uma instalação anterior do software, uma instalação de cliente baseada em atualização de software poderá causar a reinicialização do computador.  


### <a name="configure-a-group-policy-object-to-specify-the-software-update-point"></a>Configurar um objeto de Política de Grupo para especificar o ponto de atualização de software  

1.  Use o **Console de Gerenciamento de Política de Grupo** para abrir um Objeto de Política de Grupo novo ou existente.  

2.  Expanda **Configuração do Computador**, **Modelos Administrativos** e **Componentes do Windows** e selecione **Windows Update**.  

3.  Abra as propriedades da configuração **Especificar o local do serviço do Microsoft Update na intranet** e selecione **Habilitado**.  

4.  **Definir o serviço de atualização da intranet para detectar atualizações**: especifique o nome e a porta do servidor de ponto de atualização de software.  

    -   Se você configurou o sistema de sites do Configuration Manager para usar um FQDN (nome de domínio totalmente qualificado), use esse formato.  

    -   Se o sistema de sites do Configuration Manager não estiver configurado para usar um FQDN, use um formato de nome curto.

    > [!TIP]  
    >  Para determinar o número da porta, consulte [Como determinar as configurações de porta usadas pelo WSUS](/sccm/sum/plan-design/plan-for-software-updates).  

     Exemplo no formato FQDN: `http://server1.contoso.com:8530`  

5.  **Definir o servidor de estatísticas da intranet**: Essa configuração normalmente é definida com o mesmo nome do servidor.

6.  Atribua o Objeto de Política de Grupo aos computadores nos quais você deseja instalar o cliente e receber atualizações de software.  


### <a name="publish-the-configuration-manager-client-to-the-software-update-point"></a>Publicar o cliente do Configuration Manager no ponto de atualização de software  

1.  No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**.  

2.  Selecione o site para o qual deseja configurar a instalação do cliente baseada em atualização de software.  

3.  Na guia **Página Inicial** da faixa de opções, no grupo **Configurações**, selecione **Configurações de Instalação de Cliente** e, em seguida, selecione **Instalação do Cliente Baseada em Atualização de Software**.  

4.  Selecione **Habilitar instalação do cliente baseada na atualização de software**.  

5.  Se a versão do cliente do site for mais recente que a versão no ponto de atualização de software, a caixa de diálogo **Versão Mais Recente do Pacote de Cliente Detectada** será aberta. Selecione **Sim** para publicar a versão mais recente.  

    > [!NOTE]  
    >  Se você ainda não tiver publicado o software cliente para o ponto de atualização de software, essa caixa de diálogo estará em branco.

A atualização de software para o cliente do Configuration Manager não é atualizada automaticamente quando há uma nova versão. Quando você atualizar o site, repita este procedimento para atualizar o cliente.  

##  <a name="BKMK_ClientGP"></a> Instalação da Política de Grupo

Use a Política de Grupo no Active Directory Domain Services para publicar ou atribuir o cliente do Configuration Manager. O cliente é instalado quando o computador é iniciado. Quando você usa a Política de Grupo, o cliente aparece em **Adicionar ou Remover Programas** no Painel de Controle. O usuário poderá instalá-lo de lá.  

Use o pacote do Windows Installer CCMSetup.msi para instalações baseadas em Política de Grupo. Esse arquivo é encontrado na pasta `<ConfigMgr installation directory>\bin\i386` no servidor do site. Não é possível adicionar propriedades a esse arquivo para alterar o comportamento de instalação.  

> [!IMPORTANT]  
>  Você deve ter permissões de administrador para acessar os arquivos de instalação do cliente.  

-   Se você tiver estendido o esquema do Active Directory para o Configuration Manager e selecionado **Publicar este site no Active Directory Domain Services** na guia **Avançado** da caixa de diálogo **Propriedades do Site**, os computadores cliente pesquisarão automaticamente as propriedades de instalação no Active Directory Domain Services. Para obter mais informações, consulte [Sobre as propriedades de instalação do cliente publicadas no Active Directory Domain Services](/sccm/core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services).  

-   Se você não estendeu o esquema do Active Directory, confira a seção sobre [provisionar propriedades de instalação do cliente](#BKMK_Provision) para obter informações sobre como armazenar as propriedades de instalação no Registro do Windows de computadores. O cliente usa essas propriedades de instalação quando é instalado.  

Para obter mais informações, confira [Como usar a Política de Grupo para instalar o software remotamente](https://support.microsoft.com/help/816102/how-to-use-group-policy-to-remotely-install-software-in-windows-server).  

##  <a name="BKMK_Manual"></a> Instalação manual

Instale o software cliente manualmente em computadores usando CCMSetup.exe. Localize esse programa e seus arquivos de suporte na pasta Cliente da pasta de instalação do Configuration Manager no servidor do site. O site compartilha esta pasta na rede como:  

 `\\<site server name>\SMS_<site code>\Client\`  

 `<site server name>` é o nome do servidor do site primário. `<site code>` é o código do site primário ao qual o cliente está atribuído. Para executar CCMSetup.exe da linha de comando no cliente, conecte-se a esse local de rede e, em seguida, execute o comando.  

> [!IMPORTANT]  
>  Você deve ter permissões de administrador para acessar os arquivos de instalação do cliente.  

O CCMSetup.exe copia todos os pré-requisitos necessários para o computador cliente e chama o pacote do Windows Installer (Client.msi) para instalar o cliente. Não é possível executar o Client.msi diretamente.  

Para modificar o comportamento da instalação do cliente, especifique opções de linha de comando para o CCMSetup.exe e o Client.msi. Verifique se você especificou os parâmetros de CCMSetup que começam com `/` antes de especificar as propriedades de Client.msi. Por exemplo:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`

Neste exemplo, o cliente é instalado com as seguintes opções:  

|Opção|Descrição|  
|--------------|-----------------|  
|`/mp:SMSMP01`|Esse parâmetro de CCMSetup especifica o ponto de gerenciamento SMSMP01 para baixar os arquivos de instalação necessários do cliente.|  
|`/logon`|Esse parâmetro de CCMSetup especifica se a instalação deve ser interrompida se for encontrado um cliente do Configuration Manager no computador.|  
|`SMSSITECODE=AUTO`|Esta propriedade de Client.msi especifica que o cliente tenta localizar o código do site do Configuration Manager a ser usado, por exemplo, usando o Active Directory Domain Services.|  
|`FSP=SMSFP01`|Essa propriedade de Client.msi especifica que o ponto de status de fallback chamado SMSFP01 é usado para receber mensagens de estado enviadas do computador cliente.|  

 Para obter mais informações, veja [Sobre os parâmetros e as propriedades de instalação de cliente](/sccm/core/clients/deploy/about-client-installation-properties).  

> [!TIP]  
> Para que o procedimento instale o cliente do Configuration Manager em um dispositivo Windows 10 moderno usando a identidade do Azure AD (Azure Active Directory), confira [Instalar e atribuir os clientes do Windows 10 do Configuration Manager usando o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Esse procedimento destina-se a clientes em uma intranet ou Internet.  


### <a name="manual-installation-examples"></a>Exemplos de instalação manual

Estes exemplos destinam-se a clientes que ingressaram no Active Directory em uma intranet. Eles usam os seguintes valores:  

- **MPSERVER**: servidor que hospeda o ponto de gerenciamento   
- **FSPSERVER**: servidor que hospeda o ponto de status de fallback  
- **ABC**: código do site  
- **contoso.com**: nome de domínio  

Suponha que você tenha configurado todos os servidores do sistema de site com um FQDN de intranet e publicado as informações do site no Active Directory.  

Comece com as seguintes etapas no computador cliente:  
1. Entre como um administrador local.  
2. Mapeie a unidade Z para `\\MPSERVER\SMS_ABC\Client`.  
3. Mude o prompt de comando para a unidade Z.  

Então execute um dos seguintes comandos:  


#### <a name="manual-example-1"></a>Exemplo manual 1  

`CCMSetup.exe`  

Este comando instala o cliente sem parâmetros nem propriedades adicionais. O cliente é configurado automaticamente com as propriedades de instalação do cliente publicadas no Active Directory Domain Services, incluindo estas configurações:  

- Código do site: essa configuração exige que a localização de rede do cliente seja incluído em um grupo de limites configurado para atribuição do cliente.  
- Ponto de gerenciamento.
- Ponto de status de fallback.
- Comunicar-se somente usando HTTPS.  

Para obter mais informações, consulte [Sobre as propriedades de instalação do cliente publicadas no Active Directory Domain Services](/sccm/core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services).  


#### <a name="manual-example-2"></a>Exemplo manual 2  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
Este comando substitui a configuração automática fornecida pelo Active Directory Domain Services. Ele não exige que o local de rede do cliente seja incluído em um grupo de limites configurado para atribuição do cliente. Em vez disso, a instalação especifica estas configurações:
- Código do site.
- Ponto de gerenciamento da intranet.
- Ponto de gerenciamento baseado na Internet.
- Ponto de status de fallback que aceita conexões da Internet.
- Usar um certificado de PKI (infraestrutura de chave pública) (se disponível) que tenha o período de validade mais longo.  

##  <a name="BKMK_ClientLogonScript"></a> Instalação de script de logon

O Configuration Manager é compatível com o uso de scripts de logon para instalar o software cliente do Configuration Manager. Use o arquivo de programa CCMSetup.exe em um script de logon para disparar a instalação do cliente.  

A instalação de script de logon usa os mesmos métodos da instalação manual do cliente. Especifique o parâmetro de instalação `/logon` para CCMSsetup.exe. Se qualquer versão do cliente já existir no computador, esse parâmetro impedirá que o cliente seja instalado. Esse comportamento impede a reinstalação do cliente toda vez que o script de logon é executado.  

Se você não especificar nenhuma fonte de instalação usando o parâmetro `/Source` e nenhum ponto de gerenciamento do qual obter a instalação for especificado pelo parâmetro `/MP`, CCMSetup.exe localizará o ponto de gerenciamento pesquisando no Active Directory Domain Services. Esse comportamento ocorrerá apenas se você tiver estendido o esquema para o Configuration Manager e publicado o site do Active Directory Domain Services. Como alternativa, o cliente pode usar DNS ou WINS para localizar um ponto de gerenciamento.  



##  <a name="BKMK_ClientApp"></a> Instalação de pacote e programa  

Use o Configuration Manager para criar e implantar um pacote e um programa que atualiza o software cliente para dispositivos selecionados. O Configuration Manager fornece um arquivo de definição de pacote que preenche as propriedades do pacote com valores geralmente usados. Personalize o comportamento da instalação do cliente especificando propriedades e parâmetros de linha de comando adicionais.  

> [!NOTE]  
>  Não é possível atualizar clientes do Configuration Manager 2007 usando esse método. Em vez disso, use a atualização automática de cliente, que cria e implanta automaticamente um pacote com a versão mais recente do cliente. Para obter mais informações, consulte [Atualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients).  
>   
>  Para obter mais informações sobre como migrar de versões mais antigas do cliente do Configuration Manager, consulte [Planejando uma estratégia de migração do cliente](/sccm/core/migration/planning-a-client-migration-strategy).  

 
### <a name="create-a-package-and-program-for-the-client-software"></a>Criar um pacote e um programa para o software cliente  

Use o procedimento a seguir para criar um pacote e um programa do Configuration Manager que você possa implantar nos computadores cliente do Configuration Manager para atualizar o software cliente.  

1.  No console do Configuration Manager, vá para o workspace **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** e selecione o nó **Pacotes**.  

2.  Na guia **Página Inicial** da faixa de opções, no grupo **Criar**, selecione **Criar Pacote com base na Definição**.  

3.  Na página **Definição do Pacote** do assistente, selecione **Microsoft** na lista **Editor** e selecione **Atualização de Cliente do Configuration Manager** na lista **Definição do pacote**.  

4.  Na página **Arquivos de Origem**, selecione **Sempre obter arquivos da pasta de origem**.  

5.  Na página **Pasta de Origem**, selecione **Caminho de rede (Nome UNC)** . Em seguida, insira o caminho de rede para o servidor e o compartilhamento que contém os arquivos de instalação do cliente.  

    > [!NOTE]  
    >  O computador no qual a implantação do Configuration Manager é executada deve ter acesso à pasta de rede especificada. Caso contrário, a instalação do cliente falhará.  

    Para alterar uma das propriedades de instalação do cliente, modifique a linha de comando do CCMSetup.exe na guia **Geral** da caixa de diálogo do programa **Propriedades de atualização silenciosa de agente do Configuration Manager**. As propriedades de instalação padrão são `/noservice SMSSITECODE=AUTO`.  

6. Distribua o pacote para todos os pontos de distribuição em que você deseja hospedar o pacote de atualização do cliente. Então implante o pacote nas coleções de dispositivos que contêm os clientes que você deseja atualizar.  



## <a name="bkmk_mdm"></a> Dispositivos do Windows gerenciados pelo Intune MDM

Implante o cliente do Configuration Manager em dispositivos registrados com o Microsoft Intune.

Esse procedimento é para um cliente tradicional conectado à intranet. Ele usa métodos tradicionais de autenticação de cliente. Para garantir que o dispositivo permaneça em um estado gerenciado após a instalação do software cliente, o dispositivo deverá estar na intranet e dentro do limite do site do Configuration Manager.  

Para que o procedimento instale o cliente do Configuration Manager em um dispositivo Windows 10 moderno usando a identidade do Azure AD, confira [Instalar e atribuir os clientes do Windows 10 do Configuration Manager usando o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

> [!NOTE]  
> Por padrão, em algumas versões do Configuration Manager, o dispositivo cancela o registro do Intune depois que o software cliente está instalado.
> 
> Da versão 1710 em diante, os clientes não cancelam o registro do Intune. Ambos podem usar o cliente do Configuration Manager e o registro de MDM ao mesmo tempo. Para obter mais informações, confira [Visão geral do cogerenciamento](/sccm/comanage/overview).  


###  <a name="install-clients-by-using-intune"></a>Instalar clientes usando o Intune  

1. No Intune, [adicione um aplicativo de linha de negócios do Windows](https://docs.microsoft.com/intune/lob-apps-windows) que contenha o arquivo de instalação do cliente do Configuration Manager CCMSetup.msi. Esse arquivo pode ser encontrado na pasta a seguir no servidor do site: `<ConfigMgr installation directory>\bin\i386`.  

2. No Intune Software Publisher, insira os parâmetros de linha de comando. Por exemplo, use este comando com um cliente tradicional em uma intranet:  

   `CCMSETUPCMD="/MP:<FQDN of management point> SMSMP=<FQDN of management point> SMSSITECODE=<your site code> DNSSUFFIX=<DNS suffix of management point>"`  

   > [!NOTE]  
   > Para obter um exemplo de linha de comando a ser usado com um cliente moderno do Windows 10 com a autenticação do Azure AD, confira [Como preparar dispositivos baseados na Internet para cogerenciamento](/sccm/comanage/how-to-prepare-win10#install-the-configuration-manager-client).  

3. [Atribua o aplicativo](https://docs.microsoft.com/intune/deploy-use/deploy-apps-in-microsoft-intune) a um grupo de computadores Windows registrados.  



##  <a name="BKMK_ClientImage"></a> Instalação de imagem do sistema operacional

Pré-instale o software cliente do Configuration Manager em um computador de referência usado para criar uma imagem do sistema operacional.

> [!IMPORTANT]  
> Ao usar a sequência de tarefas do Configuration Manager para implantar a imagem do SO, a etapa [Preparar Cliente do ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) remove completamente o cliente do Configuration Manager.  


### <a name="prepare-the-client-computer-for-imaging"></a>Preparar o computador cliente para a geração de imagens  

1.  Instale manualmente o software cliente do Configuration Manager no computador de referência. Para obter mais informações, veja [Como instalar manualmente os clientes do Configuration Manager](#BKMK_Manual).  

    > [!IMPORTANT]  
    >  Não especifique um código do site do Configuration Manager para o cliente nas propriedades de linha de comando do CCMSetup.exe.  

2.  Em um prompt de comando, digite `net stop ccmexec` para interromper o serviço de Host de Agente SMS (CcmExec.exe) no computador de referência.  

3.  Exclua o arquivo SMSCFG.INI da pasta Windows no computador de referência.  

4.  Remova os certificados armazenados no repositório de computador local no computador de referência. Por exemplo, se você usar certificados PKI, deverá remover os certificados no repositório **Pessoal** para o **Computador** e o **Usuário** antes de criar a imagem do computador.  

5.  Se os clientes forem instalados em uma hierarquia do Configuration Manager diferente daquela do computador de referência, remova a chave de raiz confiável do computador de referência.  

    > [!NOTE]  
    >  Se os clientes não conseguirem consultar o Active Directory Domain Services para localizar um ponto de gerenciamento, eles usarão a chave de raiz confiável para determinar pontos de gerenciamento confiáveis. Se você implantar todos os clientes com imagens na mesma hierarquia que a do computador mestre, deixe a chave de raiz confiável no lugar. 
    > 
    > Se você implantar os clientes em diferentes hierarquias, remova a chave de raiz confiável. Provisione também esses clientes com a nova chave de raiz confiável. Para obter mais informações, consulte [Planejando a chave de raiz confiável](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRTK).  

6.  Use o software de geração de imagens para capturar uma imagem do computador de referência.  

7.  Implante a imagem nos computadores de destino.  



##  <a name="BKMK_ClientWorkgroup"></a> Computadores do grupo de trabalho  

O Configuration Manager dá suporte à instalação do cliente para computadores do grupos de trabalho. Instale o cliente em computadores do grupo de trabalho usando o método especificado em [Como instalar manualmente os clientes do Configuration Manager](#BKMK_Manual).  


### <a name="prerequisites"></a>Pré-requisitos  

-   Instale manualmente o cliente em cada computador do grupo de trabalho. Durante a instalação, o usuário interativo deve ter direitos de administrador local.  

-   Para acessar recursos no domínio do servidor do site do Configuration Manager, configure a conta de acesso à rede para o site. Especifique essa conta no componente de site de distribuição de software. Para obter mais informações, confira [Componentes do site](/sccm/core/servers/deploy/configure/site-components).  


### <a name="limitations"></a>Limitações  

-   Os clientes do grupo de trabalho não podem localizar pontos de gerenciamento do Active Directory Domain Services. Em vez disso, use DNS, WINS ou outro ponto de gerenciamento.  

-   Não há suporte para roaming global. Os clientes do grupo de trabalho não podem consultar o Active Directory Domain Services para obter informações do site.  

-   Os métodos de descoberta do Active Directory não podem descobrir computadores nos grupos de trabalho.  

-   Você não pode implantar o software para os usuários de computadores do grupo de trabalho.  

-   Você não pode usar o método de instalação do cliente por push para instalar o cliente em computadores do grupo de trabalho.  

-   Clientes do grupo de trabalho não podem usar o Kerberos para autenticação e podem exigir aprovação manual.  

-   Você não pode configurar um cliente de grupo de trabalho como um ponto de distribuição. O Configuration Manager exige que os computadores do ponto de distribuição sejam membros de um domínio.  


### <a name="install-the-client-on-workgroup-computers"></a>Instalar o cliente em computadores do grupo de trabalho  

Verifique os pré-requisitos e siga as instruções na seção [Como instalar manualmente os clientes do Configuration Manager](#BKMK_Manual).  


#### <a name="workgroup-example-1"></a>Exemplo de grupo de trabalho 1

Este exemplo executa as seguintes ações:
- Instala o cliente para gerenciamento de clientes da intranet
- Especifica o código do site
- Especifica o sufixo DNS para localizar um ponto de gerenciamento  

 `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

     
#### <a name="workgroup-example-2"></a>Exemplo de grupo de trabalho 2

Este exemplo exige que o cliente esteja em um local de rede configurado em um grupo de limites. Se esse requisito não for atendido, a atribuição de site automática não funcionará. O comando inclui um ponto de status de fallback no servidor FSPSERVER. Essa propriedade ajuda a acompanhar a implantação do cliente e a identificar todos os problemas de comunicação do cliente.

   `CCMSetup.exe FSP=fspserver.constoso.com`  

      

##  <a name="BKMK_ClientInternet"></a> Gerenciamento de cliente baseado na Internet  
 
> [!NOTE]  
> Esta seção não se aplica a clientes que usam um [gateway de gerenciamento de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway). Para instalar clientes baseados na Internet usando um gateway de gerenciamento de nuvem, confira [Instalar e atribuir clientes do Windows 10 do Configuration Manager usando o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure).  

Quando o site do Configuration Manager é compatível com [gerenciamento de clientes baseado na Internet](/sccm/core/clients/manage/plan-internet-based-client-management) para clientes que em algumas estão na intranet e em outras vezes estão na Internet, você tem duas opções ao instalar clientes na intranet:  

-   Incluir a propriedade Client.msi de `CCMHOSTNAME=<internet FQDN of the internet-based management point>` ao instalar o cliente, por exemplo, usando instalação manual ou push do cliente. Quando você usa esse método, atribua diretamente o cliente ao site. Você não pode usar a atribuição automática de site. Veja a seção [Como instalar manualmente os clientes do Configuration Manager](#BKMK_Manual), que apresenta um exemplo desse método de configuração.  

-   Instale o cliente para o gerenciamento de clientes na intranet e, em seguida, atribua um ponto de gerenciamento de clientes baseado na Internet ao cliente. Alterar o ponto de gerenciamento usando as propriedades do cliente na página **Configuration Manager** no Painel de Controle ou usando um script. Ao usar esse método, você pode usar a atribuição automática de clientes. Para obter mais informações, veja a seção [Como configurar clientes para o gerenciamento de clientes baseado na Internet após a instalação do cliente](#BKMK_ConfigureIBCM_MP).  

Para instalar clientes que estejam na Internet, escolha um dos seguintes métodos compatíveis:  

-   Forneça um mecanismo para que esses clientes se conectem temporariamente à intranet com uma VPN. Em seguida, instale o cliente usando um método de instalação do cliente apropriado.  

-   Use um método de instalação que seja independente do Configuration Manager. Por exemplo, empacote os arquivos de origem de instalação do cliente na mídia removível e envie a mídia aos usuários. Os arquivos de origem de instalação do cliente estão localizados na pasta `<installation path>\Client` no servidor do site do Configuration Manager. Inclua na mídia um script para copiar manualmente a pasta do cliente. Nessa pasta, instale o cliente usando CCMSetup.exe e todas as propriedades de linha de comando CCMSetup adequadas.  

> [!NOTE]  
>  O Configuration Manager não dá suporte à instalação de um cliente diretamente do ponto de gerenciamento baseado na Internet ou do ponto de atualização de software baseado na Internet.

Os clientes gerenciados pela Internet devem se comunicar com sistemas de sites baseados na Internet. Garanta que esses clientes também têm certificados PKI (infraestrutura de chave pública) antes de instalar o cliente. Instale esses certificados independentemente do Configuration Manager. Para obter mais informações, veja [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  


### <a name="install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>Instalar clientes na Internet especificando as propriedades de linha de comando do CCMSetup  

1.  Siga as instruções na seção [Como instalar manualmente os clientes do Configuration Manager](#BKMK_Manual). Sempre inclua as seguintes opções:  

    -   Parâmetro de linha de comando de CCMSetup `/source:<local path of the copied Client folder>`  

    -   Parâmetro de linha de comando de CCMSetup `/UsePKICert`  

    -   Propriedade Client.msi `CCMHOSTNAME=<FQDN of internet-based management point>`  

    -   Propriedade Client.msi `SMSSIGNCERT=<local path of exported site server signing certificate>`  

    -   Propriedade Client.msi `SMSSITECODE=<site code of internet-based management point>`  

    > [!NOTE]  
    >  Se o site tiver mais de um ponto de gerenciamento baseado na Internet, não importará qual deles você especificar para a propriedade `CCMHOSTNAME`. Quando um cliente do Configuration Manager se conecta ao ponto de gerenciamento baseado na Internet especificado, esse ponto de gerenciamento envia ao cliente uma lista de pontos de gerenciamento baseados na Internet disponíveis no site. O cliente seleciona um ponto aleatoriamente na lista.

2.  Se você não quiser que o cliente verifique a CRL (lista de certificados revogados), especifique o parâmetro de linha de comando do CCMSetup `/NoCRLCheck`.  

3.  Se estiver usando um ponto de status de fallback baseado na Internet, especifique a propriedade `FSP=<internet FQDN of the internet-based fallback status point>` do Client.msi.  

4.  Se você estiver instalando o cliente para o gerenciamento de clientes apenas da Internet, especifique a propriedade `CCMALWAYSINF=1` do Client.msi.  

5.  Determine se você precisa especificar propriedades adicionais de parâmetros da linha de comando CCMSetup. Por exemplo, se o cliente tiver mais de um certificado PKI válido, talvez você precise especificar um critério de seleção de certificado. Para obter uma lista de propriedades disponíveis, confira [Sobre as propriedades e os parâmetros de instalação do cliente](/sccm/core/clients/deploy/about-client-installation-properties).  


#### <a name="internet-based-example"></a>Exemplo baseado na Internet

`CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`    

Este exemplo instala o cliente com os seguintes comportamentos:
  - Usar arquivos de origem de uma pasta na unidade D.
  - Usar um certificado PKI do cliente.
  - Selecionar o certificado com o período de validade mais longo.
  - Gerenciamento de clientes apenas na Internet.
  - Atribuir o cliente para usar o ponto de gerenciamento baseado na Internet chamado SERVER1.
  - Atribuir o ponto de status de fallback baseado na Internet no domínio contoso.com.
  - Atribuir o cliente ao site ABC.  


###  <a name="BKMK_ConfigureIBCM_MP"></a> Para configurar clientes para o gerenciamento de clientes baseado na Internet após a instalação do cliente  

Para atribuir o ponto de gerenciamento baseado na Internet após a instalação do cliente, use um destes procedimentos. O primeiro requer configuração manual e é apropriado para poucos clientes. O segundo é mais apropriado para a configuração de muitos clientes.  


#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-from-the-configuration-manager-control-panel"></a>Configurar clientes para gerenciamento de clientes baseado na Internet após a instalação do cliente usando o painel de controle do Configuration Manager  

1.  Abra o painel de controle do **Configuration Manager** no cliente.  

2.  Na guia **Internet**, insira o FQDN (nome de domínio totalmente qualificado) do ponto de gerenciamento baseado na Internet como o **FQDN de Internet**.  

    > [!NOTE]  
    >  A guia **Internet** ficará disponível apenas se o cliente tiver um certificado PKI do cliente.  

3.  Se o cliente acessar a Internet usando um servidor proxy, insira as configurações do servidor proxy.  


#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>Configurar clientes para o gerenciamento de clientes baseado na Internet após a instalação do cliente usando um script  

##### <a name="vbscript"></a>VBScript

1.  Abra um editor de texto, como o Bloco de Notas.  

2.  Copie e insira o seguinte código VBScript no arquivo. Substitua `mp.contoso.com` pelo FQDN de Internet de seu ponto de gerenciamento baseado na Internet.  

    ``` VBScript 
    on error resume next  

    ' Create variables.  
    Dim newInternetBasedManagementPointFQDN  
    Dim client  

    newInternetBasedManagementPointFQDN = "mp.contoso.com"  

    ' Create the client COM object.  
    Set client = CreateObject ("Microsoft.SMS.Client")  

    ' Set the internet-based management point FQDN by calling the SetCurrentManagementPoint method.  
    client.SetInternetManagementPointFQDN newInternetBasedManagementPointFQDN  

    ' Clear variables.  
    Set client = Nothing  
    Set internetBasedManagementPointFQDN = Nothing  

    ```  

    > [!NOTE]  
    >  Para excluir um ponto de gerenciamento especificado baseado na Internet, remova o valor FQDN do servidor entre aspas. A linha torna-se `newInternetBasedManagementPointFQDN = ""`.

4.  Salve o arquivo com uma extensão .vbs.  

5.  Use cscript.exe para executar o script em computadores cliente. Use um destes seguintes métodos:  

    -   Implante o arquivo nos clientes existentes do Configuration Manager usando um pacote e um programa.  

    -   Execute o arquivo localmente em clientes existentes do Configuration Manager clicando duas vezes no arquivo de script do Explorador de Arquivos.  

Talvez você precise reiniciar o cliente para que as alterações entrem em vigor.  

##### <a name="powershell"></a>PowerShell

1. Abra um editor embutido do PowerShell, como o Visual Studio Code ou o PowerShell ISE. Você também pode usar um editor de texto, como o Bloco de Notas.

2. Copie e insira as linhas de código a seguir no arquivo. Substitua `'mp.contoso.com'` pelo FQDN de Internet de seu ponto de gerenciamento baseado na Internet.

    ``` PowerShell
    
    $newInternetBasedManagementPointFQDN = 'mp.contoso.com'
    $client = New-Object -ComObject Microsoft.SMS.Client
    $client.SetInternetManagementPointFQDN($newInternetBasedManagementPointFQDN)
    Restart-Service CcmExec
    $client.GetInternetManagementPointFQDN()
    
    ```

    > [!NOTE]  
    >  A última linha existe somente para verificar o novo valor de ponto de gerenciamento da Internet.
    >
    >  Para excluir um ponto de gerenciamento especificado baseado na Internet, remova o valor FQDN do servidor entre aspas. A linha torna-se `$newInternetBasedManagementPointFQDN = ''`.

3. Execute este script com direitos elevados.


##  <a name="BKMK_Provision"></a> Provisionar propriedades de instalação do cliente para a Política de Grupo e instalações do cliente baseadas em atualização de software

Use a Política de Grupo do Windows para provisionar computadores com as propriedades de instalação do cliente do Configuration Manager. Essas propriedades são armazenadas no registro do computador. O cliente os lê quando ele é instalado. Esse procedimento normalmente não é necessário, mas pode ser necessário para alguns cenários de instalação do cliente, como:  

-   Você está usando as configurações de Política de Grupo ou métodos de instalação do cliente baseados em atualização de software. Você não estendeu o esquema do Active Directory para o Configuration Manager.  

-   Você deseja substituir as propriedades de instalação do cliente em computadores específicos.  

> [!NOTE]  
>  Se uma das propriedades de instalação for fornecida na linha de comando do CCMSetup.exe, as propriedades de instalação provisionadas nos computadores não serão usadas.

Um modelo administrativo de Política de Grupo chamado ConfigMgrInstallation.adm é fornecido na mídia de instalação do Configuration Manager. Use esse modelo para provisionar computadores cliente com propriedades de instalação.


### <a name="configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>Configurar e atribuir as propriedades de instalação do cliente usando um Objeto de Política de Grupo  

1.  Importe o modelo administrativo ConfigMgrInstallation.adm para um Objeto de Política de Grupo novo ou existente usando um editor como o Editor de Objeto de Política de Grupo do Windows. Localize este arquivo na pasta `TOOLS\ConfigMgrADMTemplates` na mídia de instalação do Configuration Manager.  

2.  Abra as propriedades da configuração importada **Definir configurações de implantação de cliente**.  

3.  Selecione **Habilitado**.  

4.  Na caixa **CCMSetup** , digite as propriedades de linha de comando CCMSetup necessárias. Para obter uma lista das propriedades de linha de comando do CCMSetup e exemplos de uso, veja [Sobre as parâmetros e propriedades de instalação do cliente](/sccm/core/clients/deploy/about-client-installation-properties).  

5.  Atribuir o Objeto de Política de Grupo a computadores que você deseja provisionar com as propriedades de instalação do cliente do Configuration Manager.  
