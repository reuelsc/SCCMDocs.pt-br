---
title: Referência técnica de controles de criptografia
titleSuffix: Configuration Manager
description: Saiba mais sobre como a assinatura e a criptografia podem ajudar a impedir que os ataques leiam dados no System Center Configuration Manager.
ms.date: 12/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 253710602ca4c46e3ed0d929fb62edea6c3efeb3
ms.sourcegitcommit: 18a94eb78043cb565b05cd0e9469b939b29cccf0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66354826"
---
# <a name="cryptographic-controls-technical-reference"></a>Referência técnica de controles de criptografia

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


O System Center Configuration Manager usa a assinatura e a criptografia para ajudar a proteger o gerenciamento de dispositivos na hierarquia do Configuration Manager. Com a assinatura, se os dados foram alterados em trânsito, eles serão descartados. A criptografia ajuda a impedir que um invasor leia os dados usando um analisador de protocolo de rede.  

 O principal algoritmo de hash usado pelo Configuration Manager para a assinatura é SHA-256. Quando dois sites do Configuration Manager se comunicam entre si, eles assinam suas comunicações com o SHA-256. O principal algoritmo de criptografia implementado no Configuration Manager é o 3DES. Isso é usado para armazenar dados no banco de dados do Configuration Manager e para comunicação de cliente HTTP. Ao usar comunicação do cliente via HTTPS, você pode configurar sua PKI (infraestrutura de chave pública) para usar certificados RSA com o máximo de algoritmos de hash e comprimentos de chave que estão documentados nos [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Para a maioria das operações de criptografia para sistemas operacionais baseados no Windows, o Configuration Manager usa os algoritmos SHA-2, 3DES, AES e RSA do rsaenh.dll da biblioteca CryptoAPI do Windows.  

> [!IMPORTANT]  
>  Veja informações sobre as alterações recomendadas em resposta às vulnerabilidades do SSL em [Sobre as vulnerabilidades do SSL](#about-ssl-vulnerabilities).  

##  <a name="cryptographic-controls-for-configuration-manager-operations"></a>Controles de criptografia para operações do Configuration Manager  
 As informações no Configuration Manager podem ser assinadas e criptografadas, quer você use ou não certificados PKI com o Configuration Manager.  

### <a name="policy-signing-and-encryption"></a>Criptografia e assinatura de política  
 As atribuições de política do cliente são assinadas pelo certificado de assinatura do servidor do site autoassinado para ajudar a evitar o risco de segurança de um ponto de gerenciamento comprometido enviando políticas que foram violadas. Isso será importante se você estiver usando o gerenciamento de clientes baseado na Internet, pois este ambiente requer um ponto de gerenciamento exposto à comunicação da Internet.  

 A política é criptografada com o 3DES quando ele contém dados confidenciais. A política que contém dados confidenciais é enviada somente aos clientes autorizados. A política que não tem dados confidenciais não é criptografada.  

 Ao armazenar a política em clientes, ela é criptografada com a DPAPI (Interface de programação de aplicativo de Proteção de Dados).  

### <a name="policy-hashing"></a>Hash de política  
 Quando os clientes do Configuration Manager solicitam a política, primeiro eles obtêm uma atribuição da política para que conheçam aquelas que se aplicam a eles e, em seguida, solicitam somente os corpos dessas políticas. Cada atribuição de política contém o hash calculado para o corpo da política correspondente. O cliente recupera o corpo de política aplicável e, em seguida, calcula o hash nesse corpo. Se o hash no corpo da política baixada não corresponder ao hash na atribuição da política, o cliente descartará o corpo da política.  

 O algoritmo de hash para a política é SHA-1 e SHA-256.  

### <a name="content-hashing"></a>Hash de conteúdo  
 O serviço do gerenciador de distribuição no servidor do site mistura os arquivos de conteúdo para todos os pacotes. O provedor de política inclui o hash na política de distribuição de software. Quando o cliente do Configuration Manager baixa o conteúdo, o cliente regenera o hash localmente e o compara a um fornecido na política. Se os hashes corresponderem, o conteúdo não foi alterado e o cliente o instala. Se um único byte do conteúdo foi alterado, os hashes não irão corresponder e o software não será instalado. Essa verificação ajuda a garantir que o software correto seja instalado, pois o conteúdo real está comparado com a política.  

 O algoritmo de hash padrão para o conteúdo é o SHA-256. Para alterar este padrão, veja a documentação do SDK (Software Development Kit) do Configuration Manager.  

 Nem todos os dispositivos podem oferecer suporte a conteúdo de hash. As exceções incluem:  

-   Clientes do Windows quando transmitem conteúdo do App-V.  

-   Clientes do Windows Phone, entretanto, esses clientes verificam a assinatura de um aplicativo que está assinado por uma fonte confiável.  

-   Clientes do Windows RT, entretanto, esses clientes verificam a assinatura de um aplicativo que está assinado por uma fonte confiável e também usam validação PFN (nome completo do pacote).  

-   O iOS, entretanto, esses dispositivos verificam a assinatura de um aplicativo que está assinado por algum certificado do desenvolvedor de uma fonte confiável.  

-   Clientes Nokia, entretanto, esses clientes verificam a assinatura de um aplicativo que usa um certificado autoassinado. Ou, a assinatura de um certificado de uma fonte confiável e o certificado podem assinar aplicativos SIS (Symbian Installation Source) da Nokia.  

-   Android. Além disso, esses dispositivos não usam a validação de assinatura para instalação do aplicativo.  

-   Clientes que executam versões do Linux e UNIX que não dão suporte ao SHA-256. Para obter mais informações, veja [Planejando a implantação do cliente em computadores Linux e UNIX](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers).  

### <a name="inventory-signing-and-encryption"></a>Criptografia e assinatura de inventário  
 O inventário que os clientes enviam para pontos de gerenciamento sempre é assinado por dispositivos, independentemente de eles se comunicarem com pontos de gerenciamento via HTTP ou HTTPS. Se eles usam HTTP, você pode optar por criptografar esses dados, que é uma prática recomendada de segurança.  

### <a name="state-migration-encryption"></a>Criptografia de migração de estado  
 Os dados armazenados em pontos de migração de estado para implantação do sistema operacional sempre são criptografados pela USMT (Ferramenta de Migração do Usuário) usando 3DES.  

### <a name="encryption-for-multicast-packages-to-deploy-operating-systems"></a>Criptografia de pacotes de multicast para implantar sistemas operacionais  
 Para cada pacote de implantação de sistema operacional, você pode habilitar a criptografia quando o pacote é transferido para o computador usando multicast. A criptografia usa AES (Advanced Encryption Standard). Se você habilitar a criptografia, nenhuma configuração de certificado adicional será necessária. O ponto de distribuição habilitado para multicast gera automaticamente chaves simétricas para criptografar o pacote. Cada pacote tem uma chave de criptografia diferente. A chave é armazenada no ponto de distribuição habilitado para multicast usando APIs padrão do Windows. Quando o cliente se conecta a uma sessão de multicast, a troca de chaves ocorre em um canal criptografado com o certificado de autenticação do cliente emitido pela PKI (quando o cliente usa HTTPS) ou o certificado autoassinado (quando o cliente usa HTTP). O cliente armazena a chave na memória somente pela duração da sessão de multicast.  

### <a name="encryption-for-media-to-deploy-operating-systems"></a>Criptografia de mídia para implantar sistemas operacionais  
 Quando você usa mídia para implantar sistemas operacionais e especificar uma senha para proteger a mídia, as variáveis de ambiente são criptografadas usando AES. Outros dados na mídia, incluindo pacotes e conteúdo para aplicativos, não são criptografados.  

### <a name="encryption-for-content-that-is-hosted-on-cloud-based-distribution-points"></a>Criptografia de conteúdo hospedado nos pontos de distribuição baseados em nuvem  
 A partir do System Center 2012 Configuration Manager SP1, ao usar pontos de distribuição baseados em nuvem, o conteúdo carregado nesses pontos de distribuição é criptografado por meio da criptografia AES com um tamanho de chave de 256 bits. O conteúdo é criptografado novamente sempre que você atualizá-lo. Quando os clientes baixam o conteúdo, ele é criptografado e protegido pela conexão HTTPS.  

### <a name="signing-in-software-updates"></a>Assinando atualizações de software  
 Todas as atualizações de software devem ser assinadas por um editor confiável para proteção contra violação. Em computadores cliente, o WUA (Windows Update Agent) verifica atualizações do catálogo, mas não irá instalar a atualização se não conseguir localizar o certificado digital na loja de Editores Confiáveis no computador local. Se um certificado autoassinado foi usado para publicar o catálogo de atualizações, como os Editores WSUS autoassinados, o certificado também deve estar na loja de certificados das Autoridades de Certificação Raiz Confiável no computador local para verificar a validade do certificado. O WUA também verifica se a configuração **Permitir conteúdo assinado da política de grupo de local do serviço de atualização da intranet da Microsoft** está habilitada no computador local. Essa configuração da política deve ser habilitada para que o WUA procure atualizações que foram criadas e publicadas com o Updates Publisher.  

 Quando as atualizações do software são publicadas no System Center Updates Publisher, um certificado digital assina as atualizações de software quando elas são publicadas em um servidor de atualização. Você pode especificar um certificado PKI ou configurar o Updates Publisher para gerar um certificado autoassinado para assinar a atualização de software.  

### <a name="signed-configuration-data-for-compliance-settings"></a>Dados de configuração assinados para configurações de conformidade  
 Quando você importa dados de configuração, o Configuration Manager verifica a assinatura digital do arquivo. Se os arquivos não foram assinados, ou se a verificação da assinatura digital falhar, você será avisado e consultado se deseja continuar a importação. Continue a importar os dados de configuração somente se você confiar totalmente no editor e na integridade dos arquivos.  

### <a name="encryption-and-hashing-for-client-notification"></a>Criptografia e hash para notificação do cliente  
 Se você usa notificação do cliente, todas as comunicações usam TLS e a criptografia máxima que o servidor e os sistemas operacionais do cliente podem negociar. Por exemplo, um computador cliente que executa Windows 7 e um ponto de gerenciamento que executa o Windows Server 2008 R2 podem oferecer suporte à criptografia AES de 128 bits, enquanto um computador cliente que executa Vista para o mesmo ponto de gerenciamento negociará para a criptografia 3DES. A mesma negociação ocorre para misturar os pacotes que são transferidos durante a notificação do cliente, que usa SHA-1 ou SHA-2.  

##  <a name="certificates-used-by-configuration-manager"></a>Certificados usados pelo Configuration Manager  
 Para ver uma lista de certificados de PKI (infraestrutura de chave pública) que podem ser usados pelo Configuration Manager, requisitos especiais ou limitações e saber como os certificados são usados, veja os [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements). Essa lista inclui os algoritmos de hash e os comprimentos de chave com suporte. A maioria dos certificados tem suporte a SHA-256 e 2048 bits de comprimento de chave.  

> [!NOTE]  
>  Todos os certificados que o Configuration Manager usa devem conter comente caracteres de byte único no nome da entidade ou no nome alternativo da entidade.  

 Certificados PKI são necessários para os seguintes cenários:  

- Quando você gerencia clientes do Configuration Manager na Internet.  

- Quando você gerencia clientes do Configuration Manager em dispositivos móveis.  

- Quando você gerencia computadores Mac.  

- Quando você usa pontos de distribuição com base em nuvem.  

  Para a maioria das outras comunicações do Configuration Manager que requerem certificados para autenticação, assinatura ou criptografia, o Configuration Manager usará certificados PKI automaticamente, se estiverem disponíveis. Se não estiverem disponíveis, o Configuration Manager gerará certificados autoassinados.  

  O Configuration Manager não usa certificados PKI quando gerencia dispositivos móveis usando o conector do Exchange Server.  

### <a name="mobile-device-management-and-pki-certificates"></a>Gerenciamento de dispositivo móvel e certificados PKI  
 Se o dispositivo móvel não foi bloqueado pelo operador móvel, você pode usar o Configuration Manager ou o Microsoft Intune para solicitar e instalar um certificado do cliente. Esse certificado fornece autenticação mútua entre o cliente no dispositivo móvel e os sistemas do site do Configuration Manager ou os serviços do Microsoft Intune. Se o dispositivo móvel estiver bloqueado, você não poderá usar o Configuration Manager nem o Intune para implantar certificados.  

 Se você habilitar inventário de hardware para dispositivos móveis, o Configuration Manager ou o Intune também preparará inventários dos certificados instalados no dispositivo móvel.   

### <a name="operating-system-deployment-and-pki-certificates"></a>Implantação do sistema operacional e certificados PKI  
 Quando você usa o Configuration Manager para implantar sistemas operacionais e um ponto de gerenciamento exigir conexões de cliente HTTPS, o computador cliente também deve ter um certificado para se comunicar com o ponto de gerenciamento, mesmo que seja em uma fase de transição, como a inicialização de mídia de sequência de tarefas ou um ponto de distribuição habilitado para PXE. Para dar suporte a este cenário, é necessário criar um certificado de autenticação de cliente PKI, exportá-lo com a chave privada e, em seguida, importá-lo para as propriedades do servidor do site, além de adicionar o certificado AC raiz confiável do ponto de gerenciamento.  

 Se você criar uma mídia inicializável, importe o certificado de autenticação de cliente durante a criação da mídia inicializável. Configure uma senha na mídia inicializável para ajudar a proteger a chave privada e outros dados confidenciais configurados na sequência de tarefas. Cada computador que inicia por meio da mídia inicializável apresentará o mesmo certificado ao ponto de gerenciamento, conforme exigido para as funções de cliente, como a solicitação da política do cliente.  

 Se você usar inicialização PXE, importará o certificado de autenticação do cliente para o ponto de distribuição habilitado para PXE e ele usará o mesmo certificado para cada cliente que iniciar por meio daquele ponto de distribuição habilitado para PXE. Como prática recomendada de segurança, peça que os usuários que conectam seus computadores a um serviço PXE para fornecer uma senha para ajudar a proteger a chave privada e outros dados confidenciais nas sequências de tarefas.  

 Se um desses certificados de autenticação do cliente estiver comprometido, bloqueie os certificados no nó **Certificados** no workspace **Administração**, no nó **Segurança**. Para gerenciar esses certificados, você deve ter direitos para **Gerenciar certificado de implantação de sistema operacional** .  

 Depois que o sistema operacional for implantado e o Configuration Manager for instalado, o cliente exigirá seu próprio certificado de autenticação de cliente PKI para comunicação do cliente HTTPS.  

### <a name="isv-proxy-solutions-and-pki-certificates"></a>Soluções de proxy de ISV e certificados PKI  
 ISVs (Fornecedores Independentes de Software) podem criar aplicativos que estendem o Configuration Manager. Por exemplo, um ISV ​​pode criar extensões para dar suporte a plataformas de cliente não Windows, como computadores Macintosh ou UNIX. No entanto, se os sistemas de sites exigirem conexões de cliente HTTPS, esses clientes também devem usar certificados PKI para a comunicação com o site. O Configuration Manager inclui a capacidade de atribuir um certificado ao proxy de ISV que habilita a comunicação entre os clientes de proxy de ISV e o ponto de gerenciamento. Se você usa extensões que requerem certificados de proxy de ISV, consulte a documentação do produto. Para mais informações sobre como criar certificados de proxy de ISV, consulte o SDK (Software Developer Kit) do Configuration Manager.  

 Se um desses certificados ISV estiver comprometido, bloqueie os certificados no nó **Certificados** no workspace **Administração**, no nó **Segurança**.  

### <a name="asset-intelligence-and-certificates"></a>Asset Intelligence e certificados  
 O Configuration Manager instala um certificado X.509 usado pelo ponto de sincronização do Asset Intelligence para se conectar à Microsoft. O Configuration Manager usa este certificado para solicitar um certificado de autenticação de cliente do serviço de certificado da Microsoft. O certificado de autenticação do cliente é instalado no servidor de sistema de site do ponto de sincronização do Asset Intelligence e é usado para autenticar o servidor na Microsoft. O Configuration Manager usa o certificado de autenticação do cliente para baixar o catálogo do Asset Intelligence e carregar os títulos do software.  

 Esse certificado tem um comprimento de chave de 1.024 bits.  

### <a name="cloud-based-distribution-points-and-certificates"></a>Pontos de distribuição e certificados baseados em nuvem  
 A partir do System Center 2012 Configuration Manager SP1, os pontos de distribuição baseados em nuvem exigem um certificado de gerenciamento (autoassinado ou PKI) que você carrega no Microsoft Azure. Esse certificado de gerenciamento requer recursos de autenticação de servidor e um comprimento de chave de certificado de 2.048 bits. Além disso, você deve configurar um certificado de serviço para cada ponto de distribuição baseado em nuvem, que não pode ser autoassinado, mas também tenha recurso de autenticação de servidor e um comprimento mínimo de chave de certificado de 2.048 bits.  

> [!NOTE]  
>  O certificado de gerenciamento autoassinado é para fins apenas de teste e não para uso em redes de produção.  

 Os clientes não necessitam de um certificado PKI para usar os pontos de distribuição baseados em nuvem; eles se autenticam no gerenciamento usando um certificado autoassinado ou um certificado PKI de cliente. O ponto de gerenciamento emite então um token de acesso ao Configuration Manager ao cliente, que o cliente apresenta ao ponto de distribuição baseado em nuvem. O token é válido por 8 horas.  

### <a name="the-microsoft-intune-connector-and-certificates"></a>O conector e os certificados do Microsoft Intune  
 Quando o Microsoft Intune registra dispositivos móveis, você pode gerenciá-los no Configuration Manager criando um conector do Microsoft Intune. O conector usa um certificado PKI com funcionalidade de autenticação de cliente para autenticar o Configuration Manager no Microsoft Intune e transferir todas as informações entre eles usando SSL. O tamanho da chave do certificado é de 2.048 bits e usa o algoritmo de hash SHA-1.  

 Ao instalar o conector, um certificado de assinatura é criado e armazenado no servidor do site para as chaves de sideload, e um certificado de criptografia é criado e armazenado no ponto de registro de certificado a fim de criptografar o desafio do Protocolo SCEP. Esses certificados também têm um tamanho de chave de 2048 bits e usam o algoritmo de hash SHA-1.  

 Quando o Intune registra dispositivos móveis, ele instala um certificado PKI no dispositivo móvel. Esse certificado tem recurso de autenticação do cliente, usa um tamanho de chave de 2.048 bits e usa o algoritmo de hash SHA.  

 Esses certificados PKI são automaticamente solicitados, gerados e instalados pelo Microsoft Intune.  

### <a name="crl-checking-for-pki-certificates"></a>Verificação CRL de certificados PKI  
 Uma CRL (Lista de Certificados Revogados) aumenta a sobrecarga administrativa e o processamento, mas é mais segura. No entanto, se a verificação de CRL estiver habilitada, mas a CRL estiver inacessível, a conexão de PKI falhará. Para mais informações, veja [Segurança e privacidade para o Configuration Manager](/sccm/core/plan-design/security/security-and-privacy).  

 A verificação da CRL (lista de certificados revogados) é habilitada por padrão no IIS, por isso, se você está usando uma CRL com a implantação de PKI, não há nada adicional para configurar na maioria dos sistemas de sites do Configuration Manager que executa IIS. A exceção são as atualizações de software, que requerem uma etapa manual para permitir a verificação da CRL para verificar as assinaturas nos arquivos de atualização de software.  

 A verificação da CRL é habilitada por padrão em computadores cliente quando eles usam conexões de cliente HTTPS. Não é possível desabilitar a verificação CRL para clientes em computadores Mac no Configuration Manager SP1 ou posterior.  

 A verificação da CRL não tem suporte nas seguintes conexões no Configuration Manager:  

-   Conexões de servidor para servidor.  

-   Dispositivos móveis registrados pelo Configuration Manager.  

-   Dispositivos móveis registrados pelo Microsoft Intune.  

##  <a name="cryptographic-controls-for-server-communication"></a>Controles de criptografia para a comunicação do servidor  
 O Configuration Manager usa os seguintes controles de criptografia para comunicação do servidor.  

### <a name="server-communication-within-a-site"></a>Comunicação do servidor dentro de um site  
 Cada servidor do sistema de sites usa um certificado para transferir dados para outros sistemas de sites no mesmo site do Configuration Manager. Algumas funções do sistema de site também usam certificados para autenticação. Por exemplo, se você instalar o ponto de proxy de registro em um servidor e o ponto de registro em outro servidor, eles poderão autenticar um ao outro usando este certificado de identidade. Quando o Configuration Manager usar um certificado para essa comunicação, se houver um certificado PKI disponível com funcionalidade de autenticação do servidor, o Configuration Manager o usará automaticamente. Se não, o Configuration Manager gerará um certificado autoassinado. Este certificado autoassinado tem uma funcionalidade de autenticação de servidor, usa o SHA-256 e tem um comprimento de chave de 2.048 bits. O Configuration Manager copia o certificado no repositório de Pessoas Confiáveis nos outros servidores do sistema de sites que podem precisar confiar no sistema de sites. Os sistemas de site, então, podem confiar um outro usando esses certificados e PeerTrust.  

 Além desse certificado para cada servidor do sistema de sites, o Configuration Manager gera um certificado autoassinado para a maioria das funções do sistema de sites. Quando há mais de uma instância da função do sistema de site no mesmo site, elas compartilham o mesmo certificado. Por exemplo, você pode ter vários pontos de gerenciamento ou vários pontos de registro no mesmo site. Este certificado autoassinado também usa o SHA-256 e tem um comprimento de chave de 2.048 bits. Ele também é copiado no armazenamento de pessoas confiáveis nos servidores do sistema de site que podem precisar confiar nele. As seguintes funções do sistema de site geram este certificado:  

- Ponto de serviços Web do Catálogo de Aplicativos  

- Ponto de sites da Web do Catálogo de Aplicativos  

- Ponto de sincronização do Asset Intelligence  

- Ponto de registro de certificado  

- Ponto do Endpoint Protection  

- Ponto de registro  

- Ponto de status de fallback  

- Ponto de gerenciamento  

- Ponto de distribuição habilitado para multicast  

- Ponto de serviço fora da banda  

- Ponto do Reporting Services  

- Ponto de atualização de software  

- Ponto de migração de estado  

- Ponto do Validador da Integridade do Sistema  

- Conector do Microsoft Intune  

  Esses certificados são gerenciados automaticamente pelo Configuration Manager, e, quando necessário, são gerados automaticamente.  

  O Configuration Manager também usa um certificado de autenticação de cliente para enviar mensagens de status do ponto de distribuição para o ponto de gerenciamento. Quando o ponto de gerenciamento é configurado para conexões de cliente HTTPS somente, você deve usar um certificado PKI. Se o ponto de gerenciamento aceitar conexões HTTP, você pode usar um certificado PKI ou selecionar a opção para usar um certificado autoassinado com recurso de autenticação do cliente, SHA-256, e com um comprimento de chave de 2.048 bits.  

### <a name="server-communication-between-sites"></a>Comunicação de servidor entre sites  
 O Configuration Manager transfere dados entre sites usando a replicação de banco de dados e a replicação baseada em arquivo. Para obter mais informações, veja [Comunicações entre pontos de extremidade](/sccm/core/plan-design/hierarchy/communications-between-endpoints).  

 O Configuration Manager configurará automaticamente a replicação de banco de dados entre os sites e usará certificados PKI com funcionalidade de autenticação de servidor se estiverem disponíveis; se não, o Configuration Manager criará certificados autoassinados para autenticação do servidor. Em ambos os casos, a autenticação entre os sites é estabelecida pelo uso de certificados no armazenamento de Pessoas Confiáveis que usam o PeerTrust. Esse repositório de certificados é usado para garantir que apenas computadores SQL Server usados ​​pela hierarquia do Configuration Manager participem da replicação entre sites. Considerando que os sites primários e o site de administração central podem replicar alterações de configuração em todos os sites na hierarquia, os sites secundários só podem replicar alterações de configuração em seu site pai.  

 Servidores de site estabeleçam comunicação entre sites usando uma troca segura de chaves que ocorre automaticamente. O servidor do site de envio gera um hash e o assina com sua chave privada. O servidor do site receptor verifica a assinatura usando a chave pública e compara o hash com um valor gerado localmente. Se forem iguais, o site receptor aceitará os dados replicados. Se os valores não coincidirem, o Configuration Manager rejeitará os dados de replicação.  

 A replicação de banco de dados no Configuration Manager utiliza o SQL Server Service Broker para transferir dados entre sites usando os seguintes mecanismos:  

- Conexão do SQL Server com o SQL Server: usa as credenciais do Windows para autenticação do servidor e certificados autoassinados com 1.024 bits para assinar e criptografar os dados usando o algoritmo de criptografia AES. Se houver certificados PKI com recurso de autenticação de servidor, esses serão usados. O certificado deve estar localizado no armazenamento pessoal de certificados do computador.  

- SQL Server Service Broker: usa certificados autoassinados com 2.048 bits para autenticação e para assinar e criptografar os dados usando o algoritmo de criptografia AES. O certificado deve estar localizado no banco de dados mestre do SQL Server.  

  Replicação baseada em arquivo usa o protocolo SMB (Server Message Block) e usa SHA-256 para assinar esses dados que não são criptografados, mas não contêm dados confidenciais. Se você quiser criptografar esses dados, use o IPsec e implemente isso independentemente do Configuration Manager.  

##  <a name="cryptographic-controls-for-clients-that-use-https-communication-to-site-systems"></a>Controles de criptografia para clientes que usam comunicação HTTPS para sistemas de sites  
 Quando as funções do sistema de site aceitam conexões de clientes, você pode configurá-las para aceitar conexões HTTPS e HTTP, ou apenas as conexões HTTPS. Funções do sistema de site que aceitam conexões da Internet só aceitam conexões de cliente via HTTPS.  

 Conexões do cliente em HTTPS oferecem maior nível de segurança pela integração com uma PKI para ajudar a proteger a comunicação cliente-servidor. No entanto, a configuração de conexões do cliente HTTPS sem uma compreensão completa de planejamento, implantação e operações de PKI ainda poderiam deixá-lo vulnerável. Por exemplo, se você não proteger sua raiz CA, os invasores podem comprometer a confiança de toda a sua infraestrutura de PKI. Deixar de implantar e gerenciar certificados PKI usando processos controlados e seguros pode resultar em clientes não gerenciados que não podem receber atualizações críticas de software ou pacotes.  

> [!IMPORTANT]  
>  Certificados PKI usados ​​para comunicação com o cliente protegem a comunicação somente entre o cliente e alguns sistemas de site. Eles não protegem o canal de comunicação entre o servidor do site e os sistemas de site ou entre servidores do site.  

### <a name="communication-that-is-unencrypted-when-clients-use-https-communication"></a>Comunicação não criptografada quando os clientes usam comunicação HTTPS  
 Quando os clientes se comunicam com sistemas de site usando HTTPS, as comunicações geralmente são criptografadas pelo SSL. No entanto, nas situações a seguir, o clientes se comunicam com sistemas de site sem usar criptografia:  

- O cliente não consegue fazer uma conexão HTTPS na intranet e voltará a usar HTTP quando os sistemas de site permitirem essa configuração  

- Comunicação com as seguintes funções do sistema de site:  

  -   O cliente envia mensagens de estado para o ponto de status de fallback  

  -   O cliente envia solicitações PXE para um ponto de distribuição habilitado para PXE  

  -   O cliente envia dados de notificação para um ponto de gerenciamento  

  Pontos de serviços de relatório são configurados para usar HTTP ou HTTPS, independentemente do modo de comunicação do cliente.  

##  <a name="cryptographic-controls-for-clients-chat-use-http-communication-to-site-systems"></a>Controles de criptografia para chat de clientes que usam comunicação HTTP para sistemas de sites  
 Quando os clientes usam comunicação HTTP para funções do sistema de sites, eles podem usar certificados PKI para autenticação do cliente, ou certificados autoassinados que o Configuration Manager gera. Quando o Configuration Manager gera certificados autoassinados, eles têm um identificador de objeto personalizado para assinatura e criptografia e esses certificados são usados exclusivamente para identificar o cliente. Para todos os sistemas operacionais com suporte exceto o Windows Server 2003, esses certificados autoassinados usam o SHA-256 e têm comprimento de chave de 2048 bits. Para o Windows Server 2003, o SHA1 é usado com um comprimento de chave de 1024 bits.  

### <a name="operating-system-deployment-and-self-signed-certificates"></a>Implantação do sistema operacional e certificados autoassinados  
 Quando você usa o Configuration Manager para implantar sistemas operacionais com certificados autoassinados, o computador cliente também deve ter um certificado para se comunicar com o ponto de gerenciamento, mesmo que o computador esteja em uma fase de transição, como inicialização de mídia de sequência de tarefas ou um ponto de distribuição habilitado para PXE. Para dar suporte a este cenário para conexões de cliente HTTP, o Configuration Manager gera certificados autoassinados que têm um identificador de objeto personalizado para assinatura e criptografia e esses certificados são usados exclusivamente para identificar o cliente. Para todos os sistemas operacionais com suporte exceto o Windows Server 2003, esses certificados autoassinados usam o SHA-256 e têm comprimento de chave de 2048 bits. Para o Windows Server 2003, o SHA1 é usado com um comprimento de chave de 1024 bits. Se esses certificados autoassinados estiverem comprometidos, para evitar que invasores os usem para representar clientes confiáveis​​, será necessário bloquear os certificados no nó **Certificados** no workspace **Administração**, nó **Segurança**.  

### <a name="client-and-server-authentication"></a>Autenticação de servidor e cliente  
 Quando os clientes se conectam via HTTP, eles autenticam os pontos de gerenciamento usando o Active Directory Domain Services ou usando a chave de raiz confiável do Configuration Manager. Clientes não autenticam outras funções do sistema de site, como pontos de migração de estado ou pontos de atualização de software.  

 Quando um ponto de gerenciamento primeiro autentica um cliente usando o certificado de cliente autoassinado, esse mecanismo fornece segurança mínima, pois qualquer computador pode gerar um certificado autoassinado. Nesse cenário, o processo de identidade do cliente deve ser aumentado pela aprovação. Somente computadores confiáveis devem ser aprovados, automaticamente pelo Configuration Manager ou manualmente por um usuário administrativo. Para obter mais informações, veja a seção de aprovação em [Comunicações entre pontos de extremidade](/sccm/core/plan-design/hierarchy/communications-between-endpoints).  

## <a name="about-ssl-vulnerabilities"></a>Sobre as vulnerabilidades do SSL
Para melhorar a segurança dos servidores e clientes do Configuration Manager, faça o seguinte:

-   Habilitar o TLS 1.2

    Para habilitar o TLS 1.2 no Configuration Manager, confira o artigo [Como habilitar o TLS 1.2 no Configuration Manager](enable-tls-1-2.md).
-   Desabilitar o SSL 3.0, TLS 1.0 e TLS 1.1 
-   Reorganize os pacotes de codificação relacionados a TLS 

Para obter mais informações, consulte [Como restringir o uso de certos algoritmos de criptografia e protocolos no Schannel.dll](https://support.microsoft.com/en-us/kb/245030/) e [Priorizando pacotes de criptografia do Schannel](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx). Esses procedimentos não afetam a funcionalidade do Configuration Manager.

