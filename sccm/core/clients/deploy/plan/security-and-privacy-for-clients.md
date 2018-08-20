---
title: Segurança e privacidade do cliente
titleSuffix: Configuration Manager
description: Saiba mais sobre segurança e privacidade para clientes do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3dfb749695ffb7a8ecdeab5e4fbed764023eb6e2
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385585"
---
# <a name="security-and-privacy-for-configuration-manager-clients"></a>Segurança e privacidade para clientes do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo descreve informações de segurança e privacidade para clientes do Configuration Manager. Também inclui informações de privacidade para dispositivos móveis gerenciados usando o [conector do Exchange Server](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  



##  <a name="BKMK_Security_Clients"></a> Práticas recomendadas de segurança para clientes  

O site do Configuration Manager aceita dados de dispositivos que executam o cliente do Configuration Manager. Esse comportamento introduz o risco de os clientes atacarem o site. Por exemplo, eles podem enviar inventário com problemas ou tentar sobrecarregar os sistemas de site. Implante o cliente do Configuration Manager somente em dispositivos em que você confia. Além disso, use as práticas de segurança recomendadas a seguir para ajudar a proteger o site contra dispositivos não autorizados ou comprometidos:  

#### <a name="use-public-key-infrastructure-pki-certificates-for-client-communications-with-site-systems-that-run-iis"></a>Use certificados PKI (infraestrutura de chave pública) para comunicação do cliente com os sistemas de sites que executam o IIS  

-   Como uma propriedade do site, defina **Configurações do sistema de site** para **HTTPS apenas**.  

-   Instale clientes com a propriedade CCMSetup `UsePKICert`.  

-   Use uma CRL (Lista de Revogação de Certificado) e certifique-se de que os clientes e servidores que se comunicam sempre possam acessá-la.  

Clientes de dispositivos móveis e alguns clientes baseados na Internet exigem esses certificados. A Microsoft recomenda esses certificados para todas as conexões de cliente na intranet.  

Para obter mais informações sobre os requisitos de certificado PKI e como eles são usados para ajudar a proteger o Configuration Manager, veja [Requisitos de certificado de PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  


#### <a name="automatically-approve-client-computers-from-trusted-domains-and-manually-check-and-approve-other-computers"></a>Aprove automaticamente computadores cliente de domínios confiáveis e verifique e aprove manualmente outros computadores  

Quando não é possível usar a autenticação de PKI, a aprovação identifica um computador em que você confia para ser gerenciado pelo Configuration Manager. A hierarquia tem as seguintes opções para configurar a aprovação do cliente:  
- Manual
- Automática para computadores em domínios confiáveis
- Automática para todos os computadores  

O método mais seguro de aprovação é aprovar automaticamente os clientes que são membros de domínios confiáveis. Em seguida, verifique manualmente e aprove todos os outros computadores. Não é recomendável aprovar todos os clientes automaticamente, a menos que você tenha acesso a outros controles para impedir que computadores não confiáveis ​​acessem sua rede.  

Para obter mais informações sobre como aprovar computadores manualmente, veja [Gerenciar clientes no nó de dispositivos](/sccm/core/clients/manage/manage-clients#BKMK_ManagingClients_DevicesNode).  


#### <a name="dont-rely-on-blocking-to-prevent-clients-from-accessing-the-configuration-manager-hierarchy"></a>Não confiar em bloqueio para impedir que os clientes acessem a hierarquia do Configuration Manager  

Clientes bloqueados são rejeitados pela infraestrutura do Configuration Manager. Se os clientes estiverem bloqueados, eles não poderão se comunicar com sistemas de sites para baixar a política, carregar dados de inventário nem enviar mensagens de estado ou status. 

O bloqueio é projetado para os seguintes cenários: 
- Para bloquear mídia de inicialização perdida ou comprometida quando você implanta um sistema operacional para os clientes
- Quando todos os sistemas de site aceitam conexões de cliente HTTPS 

Quando os sistemas de sites aceitam conexões de cliente HTTP, eles não dependem de bloqueio para proteger a hierarquia do Configuration Manager contra computadores não confiáveis. Neste cenário, um cliente bloqueado poderia reingressar no site com um novo certificado autoassinado e ID de hardware. 

A revogação de certificado é a principal linha de defesa contra certificados potencialmente comprometidos. Uma CRL (lista de certificados revogados) só está disponível sando uma PKI (infraestrutura de chave pública) com suporte. O bloqueio de clientes no Configuration Manager oferece uma segunda linha de defesa para proteger sua hierarquia.  

Para obter mais informações, veja [Determinar se é necessário bloquear clientes](/sccm/core/clients/deploy/plan/determine-whether-to-block-clients).  


#### <a name="use-the-most-secure-client-installation-methods-that-are-practical-for-your-environment"></a>Use os métodos de instalação de cliente mais seguros que sejam praticáveis para o seu ambiente  

-   Para computadores de domínio, a instalação do cliente de Política de Grupo e os métodos de instalação do cliente baseados em atualização de software são mais seguros do que a instalação por push de cliente.  

-   Se você aplicar controles de acesso e de alteração, use métodos de instalação manual e geração de imagens.  

-   Na versão 1806 ou posterior, use a autenticação mútua Kerberos com a instalação do cliente por push.  

De todos os métodos de instalação do cliente, a instalação do cliente por push é o menos seguro devido às suas muitas dependências. Essas dependências incluem permissões administrativas locais, o compartilhamento Admin$ e exceções do firewall. O número e o tipo dessas dependências aumentam a superfície de ataque.  

Da versão 1806 em diante, ao usar o push de cliente, o site pode exigir autenticação mútua do Kerberos não permitindo fallback para NTLM antes de estabelecer a conexão. Essa melhoria ajuda a proteger a comunicação entre o servidor e o cliente. Para obter mais informações, veja [Como instalar clientes com o push do cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).<!--1358204-->  

Para obter mais informações sobre os diferentes métodos de instalação de cliente, veja [Métodos de instalação do cliente](/sccm/core/clients/deploy/plan/client-installation-methods).  

Sempre que possível, selecione um método de instalação do cliente que exija permissões de segurança mínimas no Configuration Manager. Restrinja os usuários administrativos atribuídos a funções de segurança com permissões que possam ser usadas para finalidades que não implantação do cliente. Por exemplo, configurar uma atualização automática do cliente requer a função de segurança **Administrador Completo**, que concede a um usuário administrativo todas as permissões de segurança.  

Para obter mais informações sobre as dependências e as permissões de segurança necessárias para cada método de instalação do cliente, veja "Dependências do método de instalação" em [Pré-requisitos para clientes de computadores](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#BKMK_prereqs_computers).  


#### <a name="if-you-must-use-client-push-installation-take-additional-steps-to-secure-the-client-push-installation-account"></a>Se você usar a instalação por push de cliente, execute etapas adicionais para proteger a Conta de Instalação de Push de Cliente  

Essa conta deve ser um membro do grupo **Administradores** local em cada computador que instala o cliente do Configuration Manager. Nunca adicione a Conta de Instalação do Cliente por Push ao grupo **Administradores de Domínio**. Em vez disso, crie um grupo global e adicione esse grupo global ao grupo local de **Administradores** em seus clientes. Crie um objeto de política de grupo para adicionar uma configuração de Grupo Restrito para adicionar a Conta de Instalação do Cliente por Push ao grupo local de **Administradores**.  

Para obter segurança adicional, crie várias Contas de Instalação do Cliente por Push, cada uma com acesso administrativo a um número limitado de computadores. Se uma conta for comprometida, somente os computadores cliente aos quais a conta tem acesso serão comprometidos.  


#### <a name="remove-certificates-before-imaging-clients"></a>Remover certificados antes da geração de imagens dos clientes  

Quando você implanta clientes usando imagens do sistema operacional, sempre remova os certificados antes de capturar a imagem. Esses certificados incluem os certificados de PKI para autenticação de cliente e os certificados autoassinados. Se você não remover esses certificados, os clientes poderão representar uns aos outros. Você não pode verificar os dados para cada cliente.  

Para obter mais informações, veja [Criar uma sequência de tarefas para capturar um sistema operacional](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system).  


#### <a name="ensure-that-the-configuration-manager-computer-clients-get-an-authorized-copy-of-these-certificates"></a>Verifique se os clientes do computador do Configuration Manager obtêm uma cópia autorizada desses certificados  

-   O certificado de chave de raiz confiável do Configuration Manager  

    Quando as duas instruções a seguir forem verdadeiras, os clientes contarão com a chave de raiz confiável do Configuration Manager para autenticar os pontos de gerenciamento válido:  

      - Você não estendeu o esquema do Active Directory para o Configuration Manager
      - Os clientes não usam certificados de PKI quando se comunicam com pontos de gerenciamento  

    Neste cenário, os clientes não têm nenhuma maneira de verificar se o ponto de gerenciamento é confiável para a hierarquia, a menos que usem a chave de raiz confiável. Sem a chave de raiz confiável, um invasor capacitado pode direcionar clientes para um ponto de gerenciamento não autorizado.  

    Quando os clientes não conseguem baixar a chave de raiz confiável do Configuration Manager do Catálogo Global ou usando certificados PKI, provisione previamente os clientes com a chave de raiz confiável. Essa ação garanta que eles não possam ser direcionados a um ponto de gerenciamento invasor. Para obter mais informações, consulte [Planejando a chave de raiz confiável](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRTK).  

-   O certificado de autenticação de servidor do site  

     Os clientes usam esse certificado para verificar se o servidor do site assinou a política baixada de um ponto de gerenciamento. Esse certificado é assinado automaticamente pelo servidor do site e publicado nos Serviços de Domínio Active Directory.  

     Quando os clientes não podem baixar o certificado de autenticação do servidor do site do Catálogo Global, por padrão, eles o baixam do ponto de gerenciamento. Se o ponto de gerenciamento estiver exposto a uma rede não confiável, como a Internet, instale manualmente o certificado de autenticação do servidor do site em clientes. Essa ação garante que eles não possam baixar políticas de cliente adulteradas de um ponto de gerenciamento comprometido.  

     Para instalar manualmente o certificado de assinatura de servidor do site, use a propriedade CCMSetup client.msi **SMSSIGNCERT**. Para obter mais informações, veja [Sobre propriedades de instalação do cliente](/sccm/core/clients/deploy/about-client-installation-properties).  


#### <a name="dont-use-automatic-site-assignment-if-the-client-downloads-the-trusted-root-key-from-the-first-management-point-it-contacts"></a>Não use atribuição automática de site se o cliente baixar a chave de raiz confiável do primeiro ponto de gerenciamento contatado  

Para evitar o risco de um novo cliente baixar a chave de raiz confiável por meio de um ponto de gerenciamento não autorizado, apenas use a atribuição automática de site nos seguintes cenários:  

-   O cliente pode acessar informações do site do Configuration Manager publicadas no Active Directory Domain Services.  

-   Você provisiona previamente o cliente com a chave de raiz confiável.  

-   Você usa certificados PKI de uma autoridade de certificação corporativa para estabelecer relação de confiança entre o cliente e o ponto de gerenciamento.  

Para obter mais informações sobre a chave raiz confiável, veja [Planejamento da chave de raiz confiável](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRTK).  


#### <a name="install-client-computers-with-the-ccmsetup-clientmsi-option-smsdirectorylookupnowins"></a>Instale os computadores cliente com a opção CCMSetup Client.msi SMSDIRECTORYLOOKUP=NoWINS  

O método local mais seguro de serviço para os clientes encontrarem sites e pontos de gerenciamento é usar Serviços de Domínio Active Directory. Às vezes esse método não é possível para alguns ambientes. Por exemplo, porque não é possível estender o esquema do Active Directory para o Configuration Manager, ou porque os clientes estão em uma floresta ou grupo de trabalho não confiável. Se esse método não for possível, use a publicação DNS como um método de local de serviço alternativo. Se ambos os métodos falharem e quando o ponto de gerenciamento não estiver configurado para conexões de cliente HTTPS, os clientes poderão realizar o fallback para usarem WINS.  

A publicação no WINS é menos segura do que outros métodos de publicação. Configure computadores cliente para não fazerem fallback para o uso do WINS especificando **SMSDIRECTORYLOOKUP=NoWINS**. Se você precisar usar WINS como local de serviço, use **SMSDIRECTORYLOOKUP=WINSSECURE**. Essa é a configuração padrão. Ele usa a chave de raiz confiável do Configuration Manager para validar o certificado autoassinado do ponto de gerenciamento.  

> [!NOTE]  
>  Quando você configura o cliente para **SMSDIRECTORYLOOKUP=WINSSECURE** e encontra um ponto de gerenciamento do WINS, o cliente verifica a sua cópia da chave de raiz confiável do Configuration Manager que está na WMI.  
> 
> Se a assinatura no certificado do ponto de gerenciamento corresponder à cópia do cliente da chave de raiz confiável, o certificado será validado. Depois de validar o certificado, o cliente começa a se comunicar com o ponto de gerenciamento que ele encontrou usando WINS.  
> 
> Se a assinatura no certificado do ponto de gerenciamento não corresponder à cópia do cliente da chave de raiz confiável, o certificado não será válido. Nesse cenário, o cliente não se comunica com o ponto de gerenciamento que ele encontrou usando WINS.  


#### <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>Verifique se as janelas de manutenção são grandes o suficiente para implantar atualizações de software críticas  

Janelas de manutenção para coleções de dispositivos restringem os momentos em que o Configuration Manager pode instalar software nesses dispositivos. Se você configurar a janela de manutenção para ser muito pequena, o cliente não poderá instalar atualizações críticas de software. Esse comportamento deixa o cliente vulnerável a qualquer ataque que a atualização de software minimize.  


#### <a name="take-additional-security-precautions-to-reduce-the-attack-surface-on-windows-embedded-devices-with-write-filters"></a>Tome precauções de segurança adicionais para reduzir a superfície de ataque em dispositivos do Windows Embedded com filtros de gravação  

Quando você habilita filtros de gravação em dispositivos Windows Embedded, todas as instalações de software ou alterações são feitas somente na sobreposição. Essas alterações não persistem depois que o dispositivo é reiniciado. Se você usar o Configuration Manager para desabilitar os filtros de gravação, durante esse período, o dispositivo incorporado ficará vulnerável às alterações em todos os volumes. Esses volumes incluem pastas compartilhadas.  

O Configuration Manager bloqueia o computador durante esse período de modo que somente os administradores locais possam entrar. Sempre que possível, tome precauções de segurança adicionais para ajudar a proteger o computador. Por exemplo, habilite restrições adicionais no firewall.  

Se você usar janelas de manutenção para manter as alterações, planeje essas janelas com cuidado. Minimize o tempo pelo qual os filtros de gravação estão desabilitados, mas torne-os longos o suficiente para permitir que instalações de software e reinícios sejam concluídos.  


#### <a name="use-the-latest-client-version-with-software-update-based-client-installation"></a>Use a versão mais recente do cliente com a instalação do cliente baseada em atualização de software

Se você usar a instalação do cliente com base em atualização de software e instalar uma versão posterior do cliente no site, atualize a atualização de software publicada. Então os clientes recebem a versão mais recente do ponto de atualização de software.  

Quando você atualiza o site, a atualização de software para a implantação do cliente publicada no ponto de atualização de software não será atualizada automaticamente. Você deve publicar novamente o cliente do Configuration Manager no ponto de atualização de software e atualizar o número de versão.  

Para obter mais informações, veja [Como instalar clientes do Configuration Manager usando instalação baseada em atualização de software](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientSUP).  


#### <a name="only-suspend-bitlocker-pin-entry-on-trusted-and-restricted-access-devices"></a>Apenas suspender a entrada de PIN do BitLocker em dispositivos confiáveis e de acesso restrito  

Somente defina a configuração do cliente **Suspender entrada de PIN do BitLocker na reinicialização** como **Sempre** para computadores em que você confia e que tenham acesso físico restrito.

Quando você define essa configuração de cliente para **Sempre**, o Configuration Manager pode concluir a instalação do software. Esse comportamento ajuda a instalar atualizações de software críticas e retomar os serviços. No entanto, se um invasor interceptar o processo de reinicialização, ele poderá assumir o controle do computador. Use essa configuração apenas quando confiar no computador e quando o acesso físico ao computador for restrito. Por exemplo, essa configuração pode ser apropriada para servidores em um data center.  

Para obter mais informações sobre essa configuração do cliente, veja [Sobre configurações do cliente](/sccm/core/clients/deploy/about-client-settings#suspend-bitlocker-pin-entry-on-restart).  


#### <a name="dont-bypass-powershell-execution-policy"></a>Não ignorar a política de execução do PowerShell   

Se você definir a configuração de cliente do Configuration Manager para **Política de execução do PowerShell** como **Ignorar**, o Windows permitirá a execução de scripts do PowerShell não assinados. Esse comportamento pode permitir que malware seja executado em computadores cliente. Quando sua organização exige essa opção, use uma configuração personalizada do cliente. Atribua-o somente aos computadores cliente que devem executar scripts do PowerShell não assinados.  

Para obter mais informações sobre essa configuração do cliente, veja [Sobre configurações do cliente](/sccm/core/clients/deploy/about-client-settings#powershell-execution-policy).  



##  <a name="bkmk_mobile"></a> Práticas recomendadas de segurança para dispositivos móveis  


#### <a name="install-the-enrollment-proxy-point-in-a-perimeter-network-and-the-enrollment-point-in-the-intranet"></a>Instale o ponto proxy do registro em uma rede de perímetro e o ponto de registro na intranet  

Para dispositivos móveis baseados na Internet registrados com o Configuration Manager, instale o ponto proxy do registro em uma rede de perímetro e o ponto de registro na intranet. Essa separação de função ajuda a proteger o ponto de registro de um ataque. Se um invasor comprometer o ponto de registro, ele poderá obter certificados para autenticação. Além disso, eles poderão roubar as credenciais de usuários que registrem seus dispositivos móveis.  


#### <a name="configure-the-password-settings-to-help-protect-mobile-devices-from-unauthorized-access"></a>Defina as configurações de senha para ajudar a proteger dispositivos móveis contra acesso não autorizado  

*Para dispositivos móveis registrados pelo Configuration Manager*: use um item de configuração de dispositivo móvel para configurar a complexidade da senha como o PIN. Especifique pelo menos o comprimento de senha mínimo padrão.  

*Para dispositivos móveis que não tem o cliente do Configuration Manager instalado, mas que são gerenciados pelo conector do Exchange Server*: defina as **Configurações de Senha** para o conector do Exchange Server de modo que a complexidade da senha seja o PIN. Especifique pelo menos o comprimento de senha mínimo padrão.  


#### <a name="only-allow-applications-to-run-that-are-signed-by-companies-that-you-trust"></a>Somente permita a execução de aplicativos assinados por empresas em que você confia  

Ajude a impedir a adulteração de informações de inventário e de status, permitindo que aplicativos sejam executados apenas quando são assinados por empresas em que você confia. Não permita que os dispositivos instalem os arquivos não assinados.  

*Para dispositivos móveis registrados pelo Configuration Manager*: use um item de configuração de dispositivo móvel para definir a configuração de segurança **Aplicativos não assinados** como **Proibido**. Configure **Instalações de arquivo não assinadas** para que sejam uma fonte confiável.  

*Para dispositivos móveis que não têm o cliente do Configuration Manager instalado, mas que são gerenciados pelo conector do Exchange Server*: defina as **Configurações do Aplicativo** para o conector do Exchange Server de modo que as opções **Instalação de arquivo não assinado** e **Aplicativos não assinados** sejam **Proibidas**.  


#### <a name="lock-mobile-devices-when-not-in-use"></a>Bloquear dispositivos móveis quando eles não estiverem em uso  

Ajude a evitar ataques de elevação de privilégio bloqueando o dispositivo móvel quando ele não estiver em uso.

*Para dispositivos móveis registrados pelo Configuration Manager*: use um item de configuração do dispositivo móvel para definir a configuração de senha **Tempo ocioso em minutos antes de o dispositivo móvel ser bloqueado**.  

*Para dispositivos móveis que não têm o cliente do Configuration Manager instalado, mas que são gerenciados pelo conector do Exchange Server*: defina as **Configurações de Senha** para que o conector do Exchange Server configure **Tempo ocioso em minutos antes do bloqueio do dispositivo móvel**.  


#### <a name="restrict-the-users-who-can-enroll-their-mobile-devices"></a>Restringir os usuários que podem registrar seus dispositivos móveis  

Ajude a impedir a elevação de privilégios, restringindo os usuários que podem registrar seus dispositivos móveis. Use uma configuração de cliente personalizada, em vez de configurações padrão, para permitir que apenas usuários autorizados registrem seus dispositivos móveis.  


#### <a name="user-device-affinity-guidance-for-mobile-devices"></a>Diretrizes de afinidade de dispositivo de usuário para dispositivos móveis  

Não implante aplicativos para usuários que tenham dispositivos móveis registrados pelo Configuration Manager ou Microsoft Intune nos seguintes cenários:  

-   Quando o dispositivo móvel é usado por mais de uma pessoa.  

-   O dispositivo é registrado por um administrador em nome de um usuário.  

-   Quando o dispositivo é transferido para outra pessoa sem ser desativado e, em seguida, registrado novamente.  

O registro de dispositivo cria um relacionamento de afinidade de dispositivo de usuário. Essa relação mapeia o usuário que realiza o registro para o dispositivo móvel. Se outro usuário usar o dispositivo móvel, ele poderá executar os aplicativos implantados no usuário original, o que pode resultar em uma elevação de privilégios. De modo semelhante, se um administrador registrar o dispositivo móvel para um usuário, os aplicativos implantados para o usuário não serão instalados no dispositivo móvel. Em vez disso, os aplicativos implantados para o administrador podem ser instalados.  

Diferentemente da afinidade de dispositivo de usuário para computadores Windows, não é possível definir manualmente informações de afinidade de dispositivo de usuário para dispositivos móveis registrados pelo Microsoft Intune.  

Se você transferir a propriedade de um dispositivo móvel registrado pelo Intune, primeiro desative o dispositivo móvel do Intune. Essa ação remove a relação de afinidade de dispositivo de usuário. Então peça para o usuário atual registrar o dispositivo novamente.  


#### <a name="make-sure-that-users-enroll-their-own-mobile-devices-for-microsoft-intune"></a>Verifique se os usuários registraram seus próprios dispositivos móveis para o Microsoft Intune  

Um relacionamento de afinidade de dispositivo de usuário é criado durante o registro. Essa ação mapeia o usuário que realiza o registro para o dispositivo móvel. Se um administrador registrar o dispositivo móvel para um usuário, os aplicativos implantados para o usuário não serão instalados no dispositivo móvel. Em vez disso, os aplicativos implantados para o administrador podem ser instalados.  


#### <a name="protect-the-connection-between-the-configuration-manager-site-server-and-the-exchange-server"></a>Proteger a conexão entre o servidor do site do Configuration Manager e do Exchange Server   

Se o Exchange Server for local, use IPsec. O Exchange hospedado protege automaticamente a conexão usando SSL.  


#### <a name="use-the-principle-of-least-privileges-for-the-connector"></a>Use o princípio de privilégios limitados para o conector  

Para obter uma lista dos cmdlets mínimos que o conector do Exchange Server requer, veja [Gerenciar dispositivos móveis com o Configuration Manager e o Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  



##  <a name="bkmk_macs"></a> Práticas recomendadas de segurança para Macs  


#### <a name="store-and-access-the-client-source-files-from-a-secured-location"></a>Armazene e acesse os arquivos de origem do cliente de um local seguro  

Antes da instalação ou do registro do cliente em um computador Mac, o Configuration Manager não verifica se estes arquivos de origem do cliente foram violados. Baixe esses arquivos de uma fonte confiável. Armazene e acesse-os com segurança.  


#### <a name="monitor-and-track-the-validity-period-of-the-certificate"></a>Monitorar e acompanhar o período de validade do certificado  

Para garantir a continuidade dos negócios, monitore e acompanhe o período de validade dos certificados que você usa em computadores Mac. O Configuration Manager não dá suporte para a renovação automática desse certificado, nem avisa que o certificado está prestes a expirar. Um período de validade típico é um ano.  

Para obter informações sobre como renovar o certificado, veja [Renovação manual do certificado do cliente Mac](/sccm/core/clients/deploy/deploy-clients-to-macs#renewing-the-mac-client-certificate).  


#### <a name="configure-the-trusted-root-certificate-for-ssl-only"></a>Configurar o certificado raiz confiável para SSL apenas  

Para ajudar a proteger-se contra a elevação de privilégios, configure o certificado para a autoridade de certificação raiz confiável de modo que ele seja confiável somente para o protocolo SSL.

Ao registrar computadores Mac, um certificado de usuário para gerenciar o cliente do Configuration Manager é instalado automaticamente. Esse certificado de usuário inclui os certificados raiz confiáveis em sua cadeia confiável. Para restringir a confiança desse certificado raiz apenas ao protocolo SSL, use o seguinte procedimento:  

1.  No computador Mac, abra uma janela de terminal.  

2.  Insira o seguinte comando: `sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access`  

3.  Na caixa de diálogo **Acesso de Conjunto de Chaves** na seção **Conjuntos de chaves**, clique em **Sistema**. Em seguida, na seção **Categoria**, clique em **Certificados**.  

4.  Localize e, em seguida, clique duas vezes no certificado de AC raiz para o certificado do cliente Mac.  

5.  Na caixa de diálogo do certificado de autoridade de certificação raiz, expanda a seção **Confiar** e faça as seguintes alterações:  

    1.  **Ao usar este certificado**: altere a configuração **Sempre Confiar** para **Usar Padrões do Sistema**.  

    2.  **Protocolo SSL**: altere **sem valor especificado** para **Sempre Confiar**.  

6.  Feche a caixa de diálogo. Quando solicitado, insira a senha do administrador e clique em **Atualizar Configurações**.  

Depois de concluir esse procedimento, o certificado raiz só será confiável para validar o protocolo SSL. Outros protocolos que agora são não confiáveis com esse certificado raiz incluem Secure Mail (S/MIME), EAP (Protocolo de Autenticação Extensível) ou assinatura de código.  

> [!NOTE]  
>  Você também pode usar esse procedimento se tiver instalado o certificado do cliente independentemente do Configuration Manager.  



##  <a name="BKMK_SecurityIssues_Clients"></a> Problemas de segurança para clientes do Configuration Manager  

Os seguintes problemas de segurança não têm nenhuma atenuação:  


#### <a name="status-messages-arent-authenticated"></a>Mensagens de status não são autenticadas  

Nenhuma autenticação é realizada em mensagens de status. Quando um ponto de gerenciamento aceita conexões de cliente HTTP, qualquer dispositivo pode enviar mensagens de status para o ponto de gerenciamento. Se o ponto de gerenciamento aceitar somente conexões de cliente HTTPS, um dispositivo deverá ter um certificado de autenticação de cliente válido, mas também poderá enviar qualquer mensagem de status. O ponto de gerenciamento descarta qualquer mensagem de status inválida recebida de um cliente.  

Há alguns possíveis ataques contra essa vulnerabilidade: 
- Um invasor pode enviar uma mensagem de status falsa para associar-se a uma coleção baseada em consultas de mensagens de status. 
- Qualquer cliente pode lançar uma negação de serviço contra o ponto de gerenciamento inundando-o com mensagens de status. 
- Se as mensagens de status provocarem ações em regras de filtro de mensagens de status, um invasor poderá acionar a regra de filtro de mensagens de status. 
- Um invasor pode enviar uma mensagem de status que tornaria as informações de relatórios imprecisas.  


#### <a name="policies-can-be-retargeted-to-non-targeted-clients"></a>As políticas podem ser redirecionadas para clientes que não sejam o alvo  

Existem vários métodos que os invasores podem usar para fazer uma política específica a um cliente ser aplicada a um cliente totalmente diferente. Por exemplo, um invasor em um cliente confiável pode enviar informações falsas de inventário ou descoberta para que o computador seja adicionado a uma coleção à qual ele não deve pertencer. Esse cliente então recebe todas as implantações dessa coleção. 

Os controles existem para ajudar a impedir que invasores modifiquem a política diretamente. No entanto, os invasores poderão pegar uma política existente que reformata e reimplanta um sistema operacional e enviá-la a um computador diferente. Essa política redirecionada pode criar uma negação de serviço. Esses tipos de ataques exigem tempo preciso e amplo conhecimento da infraestrutura do Configuration Manager.  


#### <a name="client-logs-allow-user-access"></a>Logs de cliente permitem o acesso do usuário  

Todos os arquivos de log de cliente permitem ao grupo de **Usuários** acesso de *Leitura* e ao usuário **Interativo** especial, acesso de *Gravação*. Se você permitir log detalhado, os invasores poderão ler os arquivos de log para procurar informações sobre conformidade ou vulnerabilidades do sistema. Processos como o software que o cliente instala em um contexto do usuário devem gravar logs com uma conta de usuário com direitos baixos. Esse comportamento significa que um invasor também pode gravar logs com uma conta de direitos baixos.  

O risco mais grave é que um invasor poderia remover informações nos arquivos de log. Um administrador pode precisar dessas informações para auditoria e detecção de intrusão.  


#### <a name="a-computer-could-be-used-to-obtain-a-certificate-thats-designed-for-mobile-device-enrollment"></a>Um computador pode ser usado para obter um certificado designado para registro do dispositivo móvel  

Quando o Configuration Manager processa uma solicitação de registro, não é possível verificar se a solicitação teve origem em um dispositivo móvel ou em um computador. Se a solicitação for de um computador, ele poderá instalar um certificado PKI que o permita se registrar com o Configuration Manager. 

Para ajudar a evitar um ataque de elevação de privilégio nesse cenário, permita apenas que usuários confiáveis registrem seus dispositivos móveis. Monitore cuidadosamente as atividades de registro de dispositivo no site.  


#### <a name="a-blocked-client-can-still-send-messages-to-the-management-point"></a>Um cliente bloqueado ainda pode enviar mensagens ao ponto de gerenciamento

Quando você bloqueia um cliente em que não confia, mas ele estabeleceu uma conexão de rede para notificação do cliente, o Configuration Manager não desconecta a sessão. O cliente bloqueado pode continuar a enviar pacotes para o seu ponto de gerenciamento até desconectar-se da rede. Esses pacotes são apenas pacotes pequenos do tipo keep alive. Esse cliente não poderá ser gerenciado pelo Configuration Manager até que seja desbloqueado.  


#### <a name="automatic-client-upgrade-doesnt-verify-the-management-point"></a>A atualização automática do cliente não verifica o ponto de gerenciamento

Quando você usa a atualização automática de cliente, o cliente pode ser direcionado para um ponto de gerenciamento para baixar os arquivos de origem do cliente. Nesse cenário, o cliente não verifica o ponto de gerenciamento como uma fonte confiável.  


#### <a name="when-users-first-enroll-mac-computers-theyre-at-risk-from-dns-spoofing"></a>Quando os usuários registram computadores Mac pela primeira vez, eles correm risco de falsificação de DNS  

Quando o computador Mac se conecta ao ponto proxy do registro durante o registro, é improvável que o computador Mac já tenha o certificado de AC raiz confiável. Nesse ponto, o computador Mac não confia no servidor e solicita que o usuário continue. Se um servidor DNS invasor resolver o FQDN (nome de domínio totalmente qualificado) do ponto proxy do registro, ele poderá direcionar o computador Mac para um ponto proxy do registro invasor para instalar certificados de uma fonte não confiável. Para reduzir esse risco, siga as práticas recomendadas para evitar a falsificação de DNS em seu ambiente.  


#### <a name="mac-enrollment-doesnt-limit-certificate-requests"></a>O registro do Mac não limita as solicitações de certificado  

Os usuários podem registrar novamente seus computadores Mac, cada vez solicitando um novo certificado de cliente. O Configuration Manager não verifica múltiplas solicitações nem limita o número de certificados solicitados de um único computador. Um usuário invasor pode executar um script que repita a solicitação de registro de linha de comando. Esse ataque pode causar uma negação de serviço na rede ou na AC (autoridade de certificação) emissora. Para reduzir esse risco, monitore cuidadosamente a autoridade de certificação emissora sobre esse tipo de comportamento suspeito. Bloqueie imediatamente da hierarquia do Configuration Manager qualquer computador que apresente esse padrão de comportamento.  


#### <a name="a-wipe-acknowledgment-doesnt-verify-that-the-device-has-been-successfully-wiped"></a>Uma confirmação de apagamento não verifica se o dispositivo foi apagado com êxito  

Quando você inicia uma ação de apagamento para um dispositivo móvel e o Configuration Manager reconhece o apagamento, a verificação é que o Configuration Manager *enviou* a mensagem com êxito. Ele não verifica que o dispositivo *agiu* quanto à solicitação. 

Para dispositivos móveis gerenciados pelo conector do Exchange Server, uma confirmação de apagamento verifica se o comando foi recebido pelo Exchange, não pelo dispositivo.  


#### <a name="if-you-use-the-options-to-commit-changes-on-windows-embedded-devices-accounts-might-be-locked-out-sooner-than-expected"></a>Se você usar as opções para confirmar alterações em dispositivos do Windows Embedded, as contas poderão ser bloqueadas antes do esperado  

Se o dispositivo Windows Embedded estiver executando uma versão de sistema operacional anterior ao Windows 7 e um usuário tentar entrar enquanto os filtros de gravação estiverem desabilitados pelo Configuration Manager, o Windows permitirá apenas metade do número configurado de tentativas incorretas antes do bloqueio da conta. 

Por exemplo, você pode configurar a política de domínio para que o **Limite de bloqueio de conta** seja de seis tentativas. Um usuário digita incorretamente sua senha três vezes e a conta é bloqueada. Esse comportamento cria efetivamente uma negação de serviço. Se os usuários entrarem em dispositivos inseridos nesse cenário, alerte-os sobre a possibilidade de um limite de bloqueio reduzido.  



##  <a name="BKMK_Privacy_Clients"></a> Informações de privacidade para clientes do Configuration Manager  

Quando você implanta o cliente do Configuration Manager, habilita configurações de cliente para recursos do Configuration Manager. As configurações que você usa para configurar os recursos podem se aplicar a todos os clientes na hierarquia do Configuration Manager. Esse comportamento é o mesmo estejam eles diretamente conectados à rede interna, conectados por meio de uma sessão remota ou conectados à Internet.  

As informações do cliente são armazenadas no banco de dados do Configuration Manager no SQL Server e não são enviadas à Microsoft. As informações são mantidas no banco de dados até que sejam excluídas pelas tarefas de manutenção do site **Excluir Dados Antigos de Descoberta** a cada 90 dias. Você pode configurar o intervalo de exclusão. 

Alguns dados de diagnóstico e de uso resumidos ou agregados são enviados à Microsoft. Para obter mais informações, consulte [Dados de diagnóstico e de uso](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).  

Antes de configurar o cliente do Configuration Manager, considere seus requisitos de privacidade.  


### <a name="privacy-information-for-mobile-devices-that-are-enrolled-by-configuration-manager"></a>Informações de privacidade para dispositivos móveis registrados pelo Configuration Manager  

Para obter informações de privacidade para quando você registrar um dispositivo móvel pelo Configuration Manager, veja a [Política de privacidade do System Center Configuration Manager – adendo do dispositivo móvel](/sccm/core/misc/privacy/privacy-statement-mobile-device-addendum).  


### <a name="client-status"></a>Status do cliente  

O Configuration Manager monitora as atividades dos clientes. Periodicamente, ele avalia o cliente do Configuration Manager e pode corrigir problemas com o cliente e suas dependências. O status do cliente é habilitado por padrão. Ele usa as métricas do lado do servidor para as verificações de atividade do cliente. O status do cliente usa ações do lado do cliente para autoverificações, correção e envio de informações de status do cliente ao site. O cliente executa as autoverificações de acordo com um agendamento que você pode configurar. O cliente envia os resultados das verificações para o site do Configuration Manager. Essas informações são criptografadas durante a transferência.  

As informações de status do cliente são armazenadas no banco de dados do Configuration Manager no SQL Server e não são enviadas à Microsoft. As informações não são armazenadas em formato criptografado no banco de dados do site. Essas informações são mantidas no banco de dados até serem excluídas de acordo com o valor definido na configuração de status do cliente **Manter o histórico de status do cliente durante o seguinte número de dias**. O valor padrão dessa configuração é a cada 31 dias.  

Para poder instalar o cliente do Configuration Manager com verificação de status do cliente, considere seus requisitos de privacidade.  



##  <a name="BKMK_Privacy_ExchangeConnector"></a> Informações de privacidade para dispositivos móveis gerenciados com o conector do Exchange Server  

O conector do Exchange Server localiza e gerencia dispositivos que se conectam a um Exchange Server local ou hospedado usando o protocolo ActiveSync. Os registros localizados pelo conector do Exchange Server são armazenados no banco de dados do Configuration Manager no seu SQL Server. As informações são coletadas do Exchange Server. Ele não contém nenhuma informação adicional do que os dispositivos móveis enviam para o Exchange Server.  

As informações do dispositivo móvel não são enviadas à Microsoft. As informações do dispositivo móvel são armazenadas no banco de dados do Configuration Manager no seu SQL Server. As informações são retidas no banco de dados até que sejam excluídas pela tarefa de manutenção de site **Excluir Dados Antigos de Descoberta** a cada 90 dias. Você configura o intervalo de exclusão.  

Para poder instalar e configurar o conector do Exchange Server, considere os requisitos de privacidade.  
