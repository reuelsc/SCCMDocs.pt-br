---
title: "Segurança e privacidade do cliente | Microsoft Docs"
description: "Saiba mais sobre a privacidade e a segurança de clientes no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
caps.latest.revision: "10"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 1d871b0e1a2897c236d17211a23c9c7d93e42313
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-clients-in-system-center-configuration-manager"></a>Segurança e privacidade de clientes no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo contém informações sobre segurança e privacidade para clientes no System Center Configuration Manager e para dispositivos móveis que são gerenciados pelo conector do Exchange Server:  

##  <a name="BKMK_Security_Cliients"></a> Práticas recomendadas de segurança para clientes  
 Quando o Configuration Manager aceita dados de dispositivos que executam o cliente do Configuration Manager, isso introduz o risco de os clientes atacarem o site. Por exemplo, eles podem enviar inventário com problemas ou tentar sobrecarregar os sistemas de site. Implante o cliente do Configuration Manager somente em dispositivos em que você confia. Além disso, use as práticas de segurança recomendadas a seguir para ajudar a proteger o site contra dispositivos não autorizados ou comprometidos:  

 **Use certificados PKI (Infraestrutura de Chave Pública) para comunicação do cliente com os sistemas de sites que executam o IIS.**  

-   Como uma propriedade do site, defina **Configurações do sistema de site** para **HTTPS apenas**.  

-   Instale clientes com a propriedade CCMSetup **/UsePKICert**  

-   Use uma CRL (Lista de Revogação de Certificado) e certifique-se de que os clientes e servidores que se comunicam sempre possam acessá-la.  

 Esses certificados são obrigatórios para clientes de dispositivos móveis e conexões de cliente de computador na Internet e, com a exceção dos pontos de distribuição, são recomendados para todas as conexões de clientes na intranet.  

 Para mais informações sobre os requisitos de certificado PKI e como eles são usados para ajudar a proteger o Configuration Manager, confira [Requisitos de certificado PKI para o System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 **Aprove automaticamente computadores cliente de domínios confiáveis e verifique e aprove manualmente outros computadores**  

 Você pode configurar a aprovação da hierarquia como manual, automática para computadores em domínios confiáveis, ou automática para todos os computadores. O método mais seguro de aprovação é aprovar automaticamente os clientes que são membros de domínios confiáveis, e depois verificar manualmente e aprovar todos os outros computadores. Não é recomendável aprovar todos os clientes automaticamente a menos que você tenha acesso outros controles para impedir que computadores não confiáveis ​​acessem sua rede.  

 A aprovação identifica um computador em que você confia para ser gerenciado pelo Configuration Manager quando não é possível usar a autenticação PKI.  

 Para obter mais informações sobre aprovar computadores manualmente, consulte [Gerenciando clientes no nó Dispositivos](../../../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode).  

 **Não confie em bloqueio para impedir que os clientes acessem a hierarquia do Configuration Manager**  

 Clientes bloqueados são rejeitados pela infraestrutura do Configuration Manager para que não possam se comunicar com os sistemas de sites para baixar política, carregar dados de inventário ou enviar mensagens de estado ou status. No entanto, não dependem de bloqueio para proteger a hierarquia do Configuration Manager de computadores não confiáveis ​​quando os sistemas de sites aceitam conexões de clientes HTTP. Neste cenário, um cliente bloqueado poderia ingressar novamente no site com uma ID de hardware e um novo certificado autoassinado. O bloqueio for criado para ser usado para bloquear uma mídia de inicialização perdida ou comprometida ao implantar um sistema operacional para os clientes e quando todos os sistemas de sites aceitam conexões de cliente HTTPS. Se você usar uma PKI e suportar uma CRL, sempre considere a revogação de certificado como a principal linha de defesa contra certificados potencialmente comprometidos. O bloqueio de clientes no Configuration Manager oferece uma segunda linha de defesa para proteger sua hierarquia.  

 Para mais informações, consulte [Determinar o bloqueio de clientes no System Center Configuration Manager](../../../../core/clients/deploy/plan/determine-whether-to-block-clients.md).  

 **Use os métodos de instalação de cliente mais seguros que sejam práticos para o seu ambiente:**  

-   Para computadores de domínio, a instalação do cliente de Política de Grupo e os métodos de instalação do cliente baseados em atualização de software são mais seguros do que a instalação por push de cliente.  

-   A geração de imagens e a instalação manual podem ser muito seguras se você aplicar controles de acesso e alteração.  

 De todos os métodos de instalação do cliente, a instalação por push é a menos segura por causa das muitas dependências que tem, o que inclui permissões administrativas locais, compartilhamento de Administrador e as diversas exceções de firewall. Essas dependências aumentam a superfície de ataque.  

 Para obter mais informações sobre diferentes métodos de instalação de cliente, consulte [Métodos de instalação do cliente no System Center Configuration Manager](../../../../core/clients/deploy/plan/client-installation-methods.md).  

 Além disso, sempre que possível, escolha um método de instalação de cliente que requeira permissões de segurança mínimas no Configuration Manager e restrinja os usuários administrativos aos quais são atribuídas funções de segurança que incluem permissões que possam ser usadas para outros fins que não a implantação do cliente. Por exemplo, a atualização automática do cliente requer a função de segurança **Administrador Completo** , que concede a um usuário administrativo todas as permissões de segurança.  

 Para obter mais informações sobre as dependências e as permissões de segurança necessárias para cada método de instalação do cliente, consulte "Dependências do método de instalação" em [Pré-requisitos para clientes de computadores](../../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#BKMK_prereqs_computers).  

 **Se você precisar usar a instalação do cliente por push, execute etapas adicionais para proteger a conta de instalação do cliente por push**  

 Embora esta conta deva ser um membro do grupo local de **Administradores** em cada computador que instalará o software cliente do Configuration Manager, nunca adicione a conta de instalação do cliente por push ao grupo **Admins. do Domínio**. Em vez disso, crie um grupo global e inclua esse grupo global ao grupo local de **Administradores** em seus computadores cliente. Você também pode criar um objeto de Política de Grupo para adicionar uma definição de Grupo Restrito à Conta de Instalação de Push de Cliente para o grupo local de **Administradores** .  

 Para segurança adicional, crie várias Contas de Instalação de Push de Cliente, cada uma com acesso administrativo a um número limitado de computadores, de modo que, se uma conta estiver comprometida, apenas os computadores cliente aos quais essa conta tem acesso sejam comprometidos.  

 **Remova os certificados antes de gerar imagens no computador cliente**  

 Se você planeja implantar clientes usando tecnologia de imagem, sempre remova os certificados, como certificados PKI que incluem a autenticação do cliente e certificados autoassinados, antes de capturar a imagem. Se você não remover esses certificados, os clientes poderão representar um ao outro e você não poderá verificar os dados de cada cliente.  

 Para obter mais informações sobre como usar o Sysprep para preparar um computador para geração de imagens, consulte a documentação de implantação do Windows.  

 **Certifique-se de que os clientes do computador do Configuration Manager obtenham uma cópia autorizada desses certificados:**  

-   A chave de raiz confiável do Configuration Manager  

     Caso você não tenha estendido o esquema do Active Directory para o Configuration Manager, e os clientes não usem certificados PKI ao se comunicar com os pontos de gerenciamento, os clientes contam com a chave de raiz confiável do Configuration Manager para autenticar os pontos de gerenciamento válidos. Neste cenário, os clientes não têm nenhuma maneira de verificar se o ponto de gerenciamento é confiável para a hierarquia, a menos que usem a chave de raiz confiável. Sem a chave de raiz confiável, um invasor capacitado pode direcionar clientes para um ponto de gerenciamento não autorizado.  

     Quando os clientes não puderem baixar a chave de raiz confiável do Configuration Manager do catálogo global ou usando certificados PKI, pré-provisione os clientes com a chave de raiz confiável para garantir que eles não possam ser direcionados para um ponto de gerenciamento não autorizado. Para obter mais informações, consulte [Planning for the Trusted Root Key](../../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

-   O certificado de autenticação de servidor do site  

     Os clientes usam o certificado de assinatura do servidor do site para verificar se o servidor do site assinou a política de cliente baixada de um ponto de gerenciamento. Esse certificado é assinado automaticamente pelo servidor do site e publicado nos Serviços de Domínio Active Directory.  

     Quando os clientes não podem baixar o certificado de assinatura do Catálogo Global do servidor do site, por padrão eles o baixam do ponto de gerenciamento. Quando o ponto de gerenciamento está exposto a uma rede não confiável (como a Internet), instale manualmente o certificado de assinatura de servidor do site nos clientes para garantir que eles não possam executar políticas de clientes que tenham sido adulteradas por meio de um ponto de gerenciamento comprometido.  

     Para instalar manualmente o certificado de assinatura de servidor do site, use a propriedade CCMSetup client.msi **SMSSIGNCERT**. Para obter mais informações, consulte [Sobre as propriedades de instalação do cliente no System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md).  

 **Não use atribuição automática de site se o cliente for baixar a chave de raiz confiável do primeiro ponto de gerenciamento contatado**  

 Essa prática recomendada de segurança está vinculada à entrada anterior. Para evitar o risco de um novo cliente baixar a chave de raiz confiável por meio de um ponto de gerenciamento não autorizado, use a atribuição automática de site apenas nos seguintes cenários:  

-   O cliente pode acessar informações do site do Configuration Manager publicadas no Active Directory Domain Services.  

-   Você provisiona previamente o cliente com a chave de raiz confiável.  

-   Você usa certificados PKI de uma autoridade de certificação corporativa para estabelecer relação de confiança entre o cliente e o ponto de gerenciamento.  

 Para obter mais informações sobre a chave raiz confiável, consulte [Planning for the Trusted Root Key](../../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

 **Instale os computadores cliente com a opção CCMSetup Client.msi SMSDIRECTORYLOOKUP=NoWINS**  

 O método local mais seguro de serviço para os clientes encontrarem sites e pontos de gerenciamento é usar Serviços de Domínio Active Directory. Se isso não for possível, por exemplo, porque não você não pode estender o esquema do Active Directory para o Configuration Manager, ou porque os clientes estão em uma floresta ou um grupo de trabalho não confiável, você poderá usar a publicação DNS como um método alternativo de local de serviço. Se ambos os métodos falharem, os clientes poderão recorrer ao uso de WINS quando o ponto de gerenciamento não estiver configurado para conexões de cliente HTTPS.  

 Como a publicação no WINS é menos segura do que outros métodos de publicação, configure os computadores cliente para não voltarem a usar o WINS especificando SMSDIRECTORYLOOKUP=NoWINS. Se você precisar usar o WINS como local de serviço, utilize SMSDIRECTORYLOOKUP=WINSSECURE (a configuração padrão), que usa a chave de raiz confiável do Configuration Manager para validar o certificado autoassinado do ponto de gerenciamento.  

> [!NOTE]  
>  Quando o cliente é configurado para SMSDIRECTORYLOOKUP=WINSSECURE e encontra um ponto de gerenciamento do WINS, o cliente verifica a sua cópia da chave de raiz confiável do Configuration Manager que está no WMI. Se a assinatura do certificado do ponto de gerenciamento corresponder à cópia do cliente da chave de raiz confiável, o certificado será validado e o cliente se comunicará com o ponto de gerenciamento que encontrou usando o WINS. Se a assinatura do certificado do ponto de gerenciamento não corresponder à cópia da chave de raiz confiável do cliente, o certificado não será validado e o cliente não se comunicará com o ponto de gerenciamento que encontrou usando WINS.  

 **Verifique se as janelas de manutenção são grandes o suficiente para implantar atualizações de software críticas**  

 Você pode configurar janelas de manutenção para coleções de dispositivos, para restringir os momentos em que o Configuration Manager pode instalar software nesses dispositivos. Se você configurar a janela de manutenção como muito pequena, o cliente não poderá instalar atualizações críticas de software, o que o deixa vulnerável ao ataque mitigado pela atualização de software.  

 **Tomar precauções extras de segurança quanto aos dispositivos do Windows Embedded com filtros de gravação, para reduzir a superfície de ataque caso o Configuration Manager desabilite os filtros de gravação para persistir com instalações e alterações de software**  

 Quando os filtros de gravação estão habilitados nos dispositivos do Windows Embedded, qualquer instalação ou alteração de software é feita apenas na sobreposição e não persiste após a reinicialização. Se você usar o Configuration Manager para desabilitar temporariamente os filtros de gravação para persistir instalações de software e alterações, durante este período, o dispositivo incorporado ficará vulnerável às alterações em todos os volumes, o que inclui pastas compartilhadas.  

 Embora o Configuration Manager bloqueie o computador durante esse período, para que somente os administradores locais possam fazer logon, sempre que possível, adote precauções adicionais de segurança para ajudar a proteger o computador. Por exemplo, habilite restrições adicionais no firewall e desconecte o dispositivo da rede.  

 Se você usar janelas de manutenção para manter as alterações, planeje essas janelas com cuidado para minimizar o tempo de desativação dos filtros de gravação, mas com duração suficiente para permitir a instalação do software e reiniciar para concluir.  

 **Se você usar o software de instalação do cliente de atualização baseado em atualizações e instalar uma versão mais recente do cliente no site, atualize a atualização de software publicado no ponto de atualização de software para que os clientes recebam a versão mais recente**  

 Se você instalar uma versão mais recente do cliente no site, por exemplo, atualizar o site, a atualização de software para implantação do cliente que é publicada no ponto de atualização de software não será atualizada automaticamente. Você deve publicar novamente o cliente do Configuration Manager no ponto de atualização de software e clicar em **Sim** para atualizar o número de versão.  

 Para mais informações, confira o procedimento "Para publicar o cliente do Configuration Manager no ponto de atualização de software" em [Como instalar clientes do Configuration Manager usando a instalação baseada em atualização de software](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

 **Defina a configuração do dispositivo do cliente Agente de Computador Suspender a entrada do PIN do BitLocker ao reiniciar como Sempre somente em computadores em que você confia e que tenham acesso físico restrito**  

 Quando você define essa configuração do cliente como **Sempre**, o Configuration Manager pode concluir a instalação do software para ajudar a garantir que atualizações críticas de software sejam instaladas e que os serviços sejam retomados. No entanto, se um invasor interceptar o processo de reinicialização, poderá assumir o controle do computador. Use essa definição apenas quando confiar no computador e quando o acesso físico ao computador for restrito. Por exemplo, essa configuração pode ser apropriada para servidores em um data center.  

 **Não defina a configuração de dispositivo do cliente Agente de Computador Política de Execução de PowerShell como Ignorar.**  

 Essa configuração permite que o cliente do Configuration Manager execute scripts do PowerShell não assinados, o que pode permitir que o malware seja executado em computadores cliente. Se for necessário selecionar essa opção, use uma configuração de cliente personalizada e atribua-a apenas aos computadores cliente que executam scripts do PowerShell não assinados.  

##  <a name="bkmk_mobile"></a> Práticas recomendadas de segurança para dispositivos móveis  
 **Para dispositivos móveis registrados com o Configuration Manager e que terão suporte na Internet: instale o ponto proxy do registro em uma rede de perímetro e o ponto de registro na intranet**  

 Essa separação de função ajuda a proteger o ponto de registro de um ataque. Se o ponto de registro estiver comprometido, um invasor poderá obter certificados de autenticação e roubar as credenciais de usuários que registram seus dispositivos móveis.  

 **Para dispositivos móveis: defina as configurações de senha para ajudar a proteger dispositivos móveis contra acesso não autorizado**  

 Para dispositivos móveis registrados pelo Configuration Manager: use um item de configuração do dispositivo móvel para configurar a complexidade de senha para ser o PIN e pelo menos o comprimento padrão como o comprimento mínimo de senha.  

 Para dispositivos móveis que não têm o cliente do Configuration Manager instalado, mas que são gerenciados pelo conector do Exchange Server: defina as **Configurações de Senha** para o conector do Exchange Server de tal forma que a complexidade da senha seja o PIN e especifique pelo menos o comprimento padrão como o comprimento mínimo de senha.  

 **Para dispositivos móveis: ajude a impedir a adulteração de informações de inventário e de estado, permitindo que os aplicativos sejam executados apenas quando são assinados por empresas em que você confia, e não permita que arquivos não assinados sejam instalados**  

 Para dispositivos móveis registrados pelo Configuration Manager: use um item de configuração de dispositivo móvel para definir a configuração de segurança **Aplicativos não assinados** como **Proibido** e configure **Instalações de arquivo não assinadas** como uma origem confiável.  

 Para dispositivos móveis que não têm o cliente do Configuration Manager instalado, mas que são gerenciados pelo conector do Exchange Server: defina as **Configurações do aplicativo** para o conector do Exchange Server de tal forma que a **Instalação de arquivo não assinado** e **Aplicativos não assinados** sejam configurados como **Proibido**.  

 **Para dispositivos móveis: ajude a evitar ataques de elevação de privilégio, bloqueando o dispositivo móvel quando não é usado**  

 Para dispositivos móveis registrados pelo Configuration Manager: use um item de configuração do dispositivo móvel para definir a configuração de senha **Tempo ocioso em minutos antes de o dispositivo móvel ser bloqueado**.  

 Para dispositivos móveis que não têm o cliente do Configuration Manager instalado, mas que são gerenciados pelo conector do Exchange Server: defina as **Configurações de Senha** para que o conector do Exchange Server configure **Tempo ocioso em minutos antes de o dispositivo móvel ser bloqueado**.  

 **Para dispositivos móveis: ajude a impedir a elevação de privilégios, restringindo os usuários que podem registrar seus dispositivos móveis.**  

 Use uma configuração de cliente personalizada, em vez de configurações padrão, para permitir que apenas usuários autorizados registrem seus dispositivos móveis.  

 **Para dispositivos móveis: não implante aplicativos para usuários que têm dispositivos móveis registrados pelo Configuration Manager ou Microsoft Intune nos seguintes cenários:**  

-   Quando o dispositivo móvel é usado por mais de uma pessoa.  

-   Quando o dispositivo é registrado por um administrador em nome de um usuário.  

-   Quando o dispositivo é transferido para outra pessoa sem ser desativado e, em seguida, registrado novamente.  

 Uma relação de afinidade com o dispositivo do usuário é criada durante o registro, que mapeia o usuário que realiza o registro no dispositivo móvel. Se outro usuário usar o dispositivo móvel, ele poderá executar os aplicativos que você implanta no usuário original, o que pode resultar em uma elevação de privilégios. Da mesma forma, se um administrador registrar o dispositivo móvel para um usuário, os aplicativos implantados para o usuário não serão instalados no dispositivo móvel. Em vez disso, os aplicativos implantados para o administrador poderão ser instalados.  

 Ao contrário da afinidade de dispositivo de usuário para computadores Windows, não é possível definir manualmente informações de afinidade de dispositivo do usuário para dispositivos móveis registrados pelo Microsoft Intune.  

 Se você transferir a propriedade de um dispositivo móvel registrado pelo Intune, desative o dispositivo móvel do Intune para remover a afinidade de dispositivo de usuário e depois peça ao usuário atual que registre o dispositivo novamente.  

 **Para dispositivos móveis: verifique se os usuários registraram seus próprios dispositivos móveis para o Microsoft Intune**  

 Como um relacionamento de afinidade de dispositivo do usuário é criado durante o registro, o qual mapeia o usuário que realiza o registro para o dispositivo móvel, se um administrador registrar o dispositivo móvel para um usuário, os aplicativos implantados para o usuário não serão instalados no dispositivo móvel; em vez disso, os aplicativos implantados para o administrador poderão ser instalados.  

 **Para o conector do Exchange Server: Verifique se a conexão entre o servidor do site do Configuration Manager e o computador do Exchange Server é segura**  

 Use o IPsec se o Exchange Server estiver no local; o Exchange hospedado protege automaticamente a conexão usando SSL.  

 **Para o conector do Exchange Server: use o princípio de privilégios limitados para o conector**  

 Para obter uma lista dos cmdlets mínimos que o conector do Exchange Server requer, consulte [Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

##  <a name="bkmk_macs"></a> Práticas recomendadas de segurança para Macs  
 **Para computadores Mac: armazene e acesse os arquivos de origem do cliente de um local seguro.**  

 O Configuration Manager não verifica se estes arquivos de origem do cliente foram violados antes da instalação ou registro do cliente em um computador Mac. Baixe esses arquivos de uma fonte confiável e armazene e acesse-os com segurança.  

 **Para computadores Mac: independentemente do Configuration Manager, monitore e rastreie o período de validade do certificado registrado para os usuários.**  

 Para garantir a continuidade dos negócios, monitore e acompanhe o período de validade dos certificados que você usa em computadores Mac. O Configuration Manager não dá suporte para a renovação automática desse certificado nem avisa que o certificado está prestes a expirar. Um período de validade típico é 1 ano.  

 Para obter informações sobre como renovar o certificado, consulte  [Renewing the Mac Client Certificate Manually](../../../../core/clients/deploy/deploy-clients-to-macs.md#renewing-the-mac-client-certificate).  

 **Para computadores Mac: considere configurar o certificado de AC raiz confiável, que é acreditado apenas para o protocolo SSL, para ajudá-lo a proteger-se contra elevação de privilégios.**  

 Ao registrar computadores Mac, um certificado de usuário para gerenciar o cliente do Configuration Manager é automaticamente instalado junto com o certificado raiz confiável ao qual o certificado de usuário se encadeia. Se desejar restringir a confiança deste certificado raiz apenas para o protocolo SSL, use o seguinte procedimento.  

 Após completar esse procedimento, o certificado raiz não será confiável para validar outros protocolos que não sejam SSL, por exemplo, S/MIME, EAP ou assinatura de código.  

> [!NOTE]  
>  Você também pode usar esse procedimento se instalou o certificado do cliente independentemente do Configuration Manager.  

 Para restringir o certificado AC raiz somente para o protocolo SSL:  

1.  No computador Mac, abra uma janela de terminal.  

2.  Digite o comando **sudo /Aplicativos/Utilitários/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

3.  Na caixa de diálogo **Acesso ao Conjunto de Chaves** , na seção **Conjuntos de Chaves** , clique em **Sistema**e, na seção **Categoria** , clique em **Certificados**.  

4.  Localize e, em seguida, clique duas vezes no certificado AC raiz para o certificado de cliente Mac.  

5.  Na caixa de diálogo do certificado de autoridade de certificação raiz, expanda a seção **Confiar** e faça as seguintes alterações:  

    1.  Para a configuração **Ao usar este certificado** , altere a definição padrão **Sempre Confiar** para **Usar Padrões do Sistema**.  

    2.  Na definição **Secure Sockets Layer (SSL)** , altere **nenhum valor especificado** para **Sempre Confiar**.  

6.  Feche a caixa de diálogo e, quando solicitado, insira a senha do administrador e clique em **Atualizar Configurações**.  

##  <a name="BKMK_SecurityIssues_Clients"></a> Problemas de segurança para clientes do Configuration Manager  
 Os seguintes problemas de segurança não têm nenhuma atenuação:  

-   Mensagens de status não são autenticadas  

     Nenhuma autenticação é realizada em mensagens de status. Quando um ponto de gerenciamento aceita conexões de cliente HTTP, qualquer dispositivo pode enviar mensagens de status para o ponto de gerenciamento. Se o ponto de gerenciamento aceitar conexões de clientes HTTPS apenas, um dispositivo deverá obter um certificado de autenticação de cliente válido de uma autoridade de certificação raiz confiável, mas também poderá depois enviar qualquer mensagem de status. Se um cliente enviar uma mensagem de status inválida, ela será descartada.  

     Há algumas possibilidades de ataques contra essa vulnerabilidade. Um invasor pode enviar uma mensagem de status falsa para ganhar associação em uma coleção baseada em consultas de mensagens de status. Qualquer cliente pode lançar uma negação de serviço contra o ponto de gerenciamento inundando-o com mensagens de status. Se as mensagens de status provocarem ações em regras de filtro de mensagens de status, um invasor poderá acionar a regra de filtro de mensagens de status. Um invasor também pode enviar mensagem de status que gera informações de relatórios imprecisas.  

-   As políticas podem ser redirecionadas para clientes que não sejam o alvo  

     Existem vários métodos que os invasores podem usar para fazer uma política específica a um cliente ser aplicada a um cliente totalmente diferente. Por exemplo, um invasor em um cliente confiável pode enviar um inventário falso ou informações de descoberta para que o computador seja adicionado a uma coleção à qual ele não deve pertencer e receber todas as implantações dessa coleção. Enquanto existem controles para ajudar a impedir que os invasores modifiquem a política diretamente, os invasores podem pegar uma política existente para reformatar e reimplantar um sistema operacional e enviá-lo para um computador diferente, criando uma negação de serviço. Esses tipos de ataques exigem tempo preciso e amplo conhecimento da infraestrutura do Configuration Manager.  

-   Logs de cliente permitem o acesso do usuário  

     Todos os arquivos de log do cliente permitem aos usuários acesso de leitura e aos usuários interativos, acesso de gravação. Se você permitir log detalhado, os invasores poderão ler os arquivos de log para procurar informações sobre conformidade ou vulnerabilidades do sistema. Processos como a instalação de software executados no contexto de um usuário devem poder gravar logs com uma conta de usuário de direitos limitados. Isso significa que um invasor também pode gravar logs com uma conta de direitos limitados.  

     O risco mais grave é que um invasor possa remover informações dos arquivos de log que um administrador venha a precisar para auditoria e detecção de intrusos.  

-   Um computador pode ser usado para obter um certificado designado para registro do dispositivo móvel  

     Quando o Configuration Manager processa uma solicitação de registro, não é possível verificar se a solicitação teve origem em um dispositivo móvel ou um computador. Se a solicitação for de um computador, ele poderá instalar um certificado PKI que o permita se registrar com o Configuration Manager. Para ajudar a evitar um ataque de elevação de privilégios neste cenário, permita que apenas usuários confiáveis ​​registrem seus dispositivos móveis e acompanhe atentamente as atividades de registro.  

-   A conexão de um cliente com o ponto de gerenciamento não será descartada se você bloquear um cliente e o cliente bloqueado continuar a enviar pacotes de notificação de cliente para o ponto de gerenciamento, como mensagens keep-alive  

     Quando você bloqueia um cliente em que já não confia, e estabeleceu uma comunicação de notificação do cliente, o Configuration Manager não desconecta a sessão. O cliente bloqueado pode continuar a enviar pacotes para o seu ponto de gerenciamento até desconectar-se da rede. Esses pacotes são apenas pequenos pacotes keep alive e esses clientes não podem ser gerenciados pelo Configuration Manager até serem desbloqueados.  

-   Quando você usa a atualização automática do cliente e o cliente é direcionado para um ponto de gerenciamento para baixar os arquivos de origem do cliente, o ponto de gerenciamento não é confirmado como uma fonte confiável  

-   Quando os usuários registram computadores Mac pela primeira vez, eles correm risco de falsificação de DNS  

     Quando o computador Mac se conecta ao ponto proxy do registro durante o registro, é improvável que o computador Mac já tenha o certificado de autoridade de certificação raiz. Nesse ponto, o servidor é não confiável pelo computador Mac e solicita ao usuário para continuar. Se o nome totalmente qualificado do ponto proxy do registro for resolvido por um servidor DNS não autorizado, o computador Mac poderá ser direcionado a um ponto proxy do registro não autorizado e instalar certificados de uma fonte não confiável. Para reduzir esse risco, siga as práticas recomendadas para evitar a falsificação de DNS em seu ambiente.  

-   O registro do Mac não limita as solicitações de certificado  

     Os usuários podem registrar novamente seus computadores Mac, cada vez solicitando um novo certificado de cliente. O Configuration Manager não verifica várias solicitações ou limita o número de certificados solicitados de um único computador. Um usuário não autorizado pode executar um script que repete a solicitação de linha de comando, causando uma negação de serviço na rede ou na autoridade de certificação emissora. Para reduzir esse risco, monitore cuidadosamente a autoridade de certificação emissora sobre esse tipo de comportamento suspeito. Um computador que apresente este tipo de comportamento deve ser bloqueado imediatamente da hierarquia do Configuration Manager.  

-   Uma confirmação de apagamento não verifica se o dispositivo foi apagado com êxito  

     Quando você inicia uma ação de apagamento para um dispositivo móvel e o Configuration Manager exibe o status do apagamento a ser confirmado, a verificação é que o Configuration Manager enviou a mensagem com êxito e que não foi o dispositivo que agiu sobre ele. Além disso, para dispositivos móveis gerenciados pelo conector do Exchange Server, uma confirmação de apagamento verifica se o comando foi recebido pelo Exchange, não pelo dispositivo.  

-   Se você usar as opções para aplicar alterações em dispositivos do Windows Embedded, as contas poderão ser bloqueadas antes do esperado.  

     Se o dispositivo Windows Embedded estiver executando um sistema operacional anterior ao Windows 7 e um usuário tentar fazer logon enquanto os filtros de gravação estiverem desabilitados para confirmar alterações feitas pelo Configuration Manager, o número de tentativas de logon incorretas permitido antes que a conta seja bloqueada será efetivamente reduzido à metade. Por exemplo, se **Limite de Bloqueio de Conta** estiver configurado como 6 e um usuário errar sua senha 3 vezes, a conta será bloqueada, criando uma situação de negação de serviço.  Se os usuários fizerem logon em dispositivos inseridos nesse cenário, advirta-os sobre a possibilidade de um limite de bloqueio reduzido.  

##  <a name="BKMK_Privacy_Cliients"></a> Informações de privacidade para clientes do Configuration Manager  
 Quando você implanta o cliente do Configuration Manager, habilita as configurações do cliente para que possa usar os recursos de gerenciamento do Configuration Manager. As definições que você usa para configurar os recursos podem ser aplicadas a todos os clientes na hierarquia do Configuration Manager, independentemente se estão diretamente conectados à rede corporativa, através de uma sessão remota, ou conectado à Internet, mas com suporte do Configuration Manager.  

 As informações do cliente são armazenadas no banco de dados do Configuration Manager e não são enviadas à Microsoft. As informações são mantidas no banco de dados até que sejam excluídas pelas tarefas de manutenção do site **Excluir Dados Antigos de Descoberta** a cada 90 dias. Você pode configurar o intervalo de exclusão.  

 Antes de configurar o cliente do Configuration Manager, considere seus requisitos de privacidade.  

### <a name="privacy-information-for-mobile-devices-that-are-enrolled-by-configuration-manager"></a>Informações de privacidade para dispositivos móveis registrados pelo Configuration Manager  
 Para obter informações de privacidade para quando você registrar um dispositivo móvel pelo Configuration Manager, confira [Política de privacidade do System Center Configuration Manager – Adendo do dispositivo móvel](../../../../core/misc/privacy/privacy-statement-mobile-device-addendum.md).  

### <a name="client-status"></a>Status do cliente  
 O Configuration Manager monitora as atividades de clientes, as avalia periodicamente e pode corrigir o cliente do Configuration Manager e suas dependências. O status do cliente é habilitado por padrão e utiliza métricas do lado do servidor para verificações de atividade do cliente, ações do lado do cliente para verificações automáticas, correção e envio de informações de status do cliente ao site do Configuration Manager. O cliente executa as verificações automáticas de acordo com um agendamento que você pode configurar. O cliente envia os resultados das verificações para o site do Configuration Manager. Essas informações são criptografadas durante a transferência.  

 As informações de status do cliente são armazenadas no banco de dados do Configuration Manager e não são enviadas à Microsoft. As informações não são armazenadas em formato criptografado no banco de dados do site. Essas informações são mantidas no banco de dados até serem excluídas de acordo com o valor definido na configuração do cliente **Manter o histórico de status do cliente durante o seguinte número de dias** . O valor padrão dessa configuração é a cada 31 dias.  

 Para poder instalar o cliente do Configuration Manager com verificação de status do cliente, considere seus requisitos de privacidade.  

##  <a name="BKMK_Privacy_ExchangeConnector"></a> Informações de privacidade para dispositivos móveis gerenciados com o conector do Exchange Server  
 O conector do Exchange Server localiza e gerencia dispositivos que se conectam ao Exchange Server (local ou hospedado) usando o protocolo ActiveSync. Os registros localizados pelo conector do Exchange Server são armazenados no banco de dados do Configuration Manager. As informações são coletadas do Exchange Server. Ele não contém qualquer informação adicional do que os dispositivos móveis enviam para o Exchange Server.  

 As informações do dispositivo móvel não são enviadas à Microsoft. As informações do dispositivo móvel são armazenadas no banco de dados do Configuration Manager. As informações são mantidas no banco de dados até que sejam excluídas pelas tarefas de manutenção do site **Excluir Dados Antigos de Descoberta** a cada 90 dias. Você pode configurar o intervalo de exclusão.  

 Para poder instalar e configurar o conector do Exchange Server, considere os requisitos de privacidade.  
