---
title: Segurança e privacidade para aplicativos
titleSuffix: Configuration Manager
description: Diretrizes e recomendações de segurança e privacidade ao gerenciar aplicativos no Configuration Manager.
ms.date: 08/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: be4f60bbc6114abc1c4537cc83ee8c2dd0aeef42
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421919"
---
# <a name="security-and-privacy-for-application-management-in-configuration-manager"></a>Segurança e privacidade para gerenciamento de aplicativos no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


##  <a name="security-guidance-for-application-management"></a>Diretrizes de segurança para o gerenciamento de aplicativos  


### <a name="use-the-new-software-center-without-the-application-catalog"></a>Usar o novo Centro de Software sem o Catálogo de Aplicativos
<!--1358309--> A partir da versão 1806, as funções do catálogo de aplicativos não são mais necessárias para exibir aplicativos disponíveis ao usuário no Centro de Software. Essa configuração ajuda a reduzir a infraestrutura de servidor necessária para fornecer aplicativos aos usuários. Reduzir infraestrutura de servidor também reduz a superfície de ataque. 

Para fornecer uma experiência consistente e segura de aplicativos para clientes baseados na Internet, use o Azure Active Directory e o gateway de gerenciamento de nuvem.

Para saber mais, veja [Configurar Centro de Software](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex). 


### <a name="use-https-with-the-application-catalog"></a>Usar HTTPS com o Catálogo de Aplicativos

Configure o ponto de sites da Web do catálogo de aplicativos e o ponto de serviços Web do catálogo de aplicativos para aceitar conexões HTTPS. Com essa configuração, o servidor é autenticado para usuários. Os dados transmitidos são protegidos contra violação e exibição. 

Ajude a evitar ataques de engenharia social ensinando os usuários a se conectar apenas a sites confiáveis. Instrua os usuários sobre os perigos de sites maliciosos.

Quando você não usar HTTPS, não use as opções de configuração de identidade visual. Essas configurações mostram o nome da sua organização no Catálogo de Aplicativos como prova de identidade.  


### <a name="use-role-separation"></a>Usar a separação de funções

Instale o ponto de sites do Catálogo de Aplicativos e o ponto de serviços da Web do catálogo de aplicativos em servidores separados. Se o ponto de sites da Web do Catálogo de Aplicativos estiver comprometido, ele será separado do ponto de serviços Web do catálogo de aplicativos. Esse design ajuda a proteger os clientes e a infraestrutura do Configuration Manager. Essa configuração é especialmente importante se o ponto de sites da Web do Catálogo de Aplicativos aceita conexões de cliente da Internet. Isso torna o servidor mais vulnerável a ataques.  


### <a name="close-browser-windows"></a>Fechar a janela do navegador

Treinar os usuários para fechar a janela do navegador quando terminarem de usar o catálogo de aplicativos. Se os usuários navegarem para um site externo na mesma janela do navegador que usaram para o catálogo de aplicativos, o navegador continuará usando as configurações de segurança adequadas para sites confiáveis na intranet.  


### <a name="centrally-specify-user-device-affinity"></a>Especificar a afinidade de dispositivo de usuário de forma centralizada

Especificar manualmente a afinidade de dispositivo de usuário, em vez de permitir que os usuários identifiquem o dispositivo primário. Não habilitar a configuração baseada em uso.

Não considere informações coletadas dos usuários ou do dispositivo para autorização. Se você implantar o software usando a afinidade de dispositivo de usuário não especificada por um administrativo confiável, o software poderá ser instalado em computadores e em usuários não autorizados a receber esse software.  


### <a name="dont-run-deployments-from-distribution-points"></a>Não executar implantações de pontos de distribuição

Sempre configurar implantações para baixar conteúdo dos pontos de distribuição em vez de executar de pontos de distribuição. Quando você configura implantações para baixar conteúdo de um ponto de distribuição e executar localmente, o cliente do Configuration Manager verifica o hash do pacote depois de baixar o conteúdo. O cliente descartará o pacote se o hash não corresponder ao hash na política. 

Se você configurar a implantação para ser executada diretamente em um ponto de distribuição, o cliente do Configuration Manager não verifica o hash do pacote. Esse comportamento significa que o cliente do Configuration Manager pode instalar um software adulterado.

Se precisar executar implantações diretamente em pontos de distribuição, use as permissões mínimas do NTFS nos pacotes nos pontos de distribuição. Use também o protocolo IPsec para proteger o canal entre o cliente e os pontos de distribuição e entre os pontos de distribuição e o servidor do site.


### <a name="bkmk_interact"></a> Não deixe que os usuários interajam com os processos elevados
  
Se você habilitar as opções para **Executar com direitos administrativos** ou **Instalar para o sistema**, não permita que os usuários interajam com esses aplicativos. Ao configurar um aplicativo, defina a opção como **Permitir que os usuários exibam e interajam com a instalação do programa**. Essa configuração permite que os usuários respondam aos prompts obrigatórios na interface do usuário. Se você configurar também o aplicativo para **Executar com direitos administrativos** ou, a partir da versão 1802, **Instalar para o sistema**, um invasor no computador que executa o programa poderá usar a interface do usuário para escalar privilégios no computador cliente.

Usar programas que usam o Windows Installer para instalação e privilégios elevados para cada usuário para implantações de software que exigem credenciais administrativas. A instalação deve ser executada no contexto de um usuário que não tem credenciais administrativas. Os privilégios elevados por usuário do Windows Installer fornecem a maneira mais segura para implantar aplicativos que têm esse requisito.


### <a name="restrict-whether-users-can-install-software-interactively"></a>Restringir se os usuários podem instalar software interativamente

Definir as configurações de cliente de **Permissões de instalação** no grupo **Agente de Computador**. Essa configuração restringe os tipos de usuários que podem instalar software usando o Catálogo de Aplicativos ou Centro de Software. 

Por exemplo, crie uma configuração personalizada do cliente com as **Permissões de instalação** definidas como **Somente administradores**. Aplique essa configuração de cliente a uma coleção de servidores. Essa configuração impede que os usuários sem permissões administrativas instalem software nesses servidores.  


### <a name="for-mobile-devices-deploy-only-applications-that-are-signed"></a>Para dispositivos móveis, implantar somente os aplicativos assinados

Implante aplicativos de dispositivos móveis somente se eles têm assinatura por código de uma AC (autoridade de certificação) que seja confiável pelo dispositivo móvel. 

Por exemplo:
- Um aplicativo de um fornecedor, que é assinado por uma AC já conhecida, como a VeriSign.  

- Um aplicativo interno que você assina independente do Configuration Manager, usando a AC interna.  

- Um aplicativo interno que você assina usando o Configuration Manager ao criar o tipo de aplicativo e usar um certificado de autenticação.


### <a name="secure-the-location-of-the-mobile-device-application-signing-certificate"></a>Proteja o local do certificado de assinatura de aplicativo de dispositivo móvel

Se você assinar aplicativos de dispositivos móveis usando o **Assistente para Criar Aplicativo** no Configuration Manager, proteja o local do certificado de autenticação e o canal de comunicação. Para ajudar a proteger contra a elevação de privilégios e ataques "man-in-the-middle", armazene o arquivo do certificado de autenticação em uma pasta protegida. 

Use o IPsec entre os seguintes computadores:
- O computador que executa o console do Configuration Manager
- O computador que armazena o arquivo do certificado de autenticação
- O computador que armazena os arquivos de origem do aplicativo

Como alternativa, assine o aplicativo independente do Configuration Manager e antes de executar o **Assistente para Criar Aplicativo**.


### <a name="implement-access-controls"></a>Implementar controles de acesso

Para proteger os computadores de referência, implemente controles de acesso. Quando você configura o método de detecção em um tipo de implantação navegando para um computador de referência, verifique se o computador não está comprometido.


### <a name="restrict-and-monitor-administrative-users"></a>Restringir e monitorar usuários administrativos

Restrinja e monitore os usuários administrativos aos quais você concede as seguintes funções de segurança baseada em funções para o gerenciamento de aplicativos:
- **Administrador de Aplicativos**
- **Autor de Aplicativos**
- **Gerenciador de Implantação de Aplicativos**

Mesmo quando você configura a administração baseada em funções, os usuários administrativos que criar e implantam aplicativos podem ter mais permissões do que você imagina. Por exemplo, os usuários administrativos que criam ou alteram um aplicativo, podem selecionar aplicativos dependentes que não estão em seu escopo de segurança.


### <a name="configure-app-v-apps-in-virtual-environments-with-the-same-trust-level"></a>Configurar aplicativos App-V em ambientes virtuais com o mesmo nível de confiança

Ao configurar ambientes virtuais do Microsoft Application Virtualization (App-V), selecione aplicativos no ambiente virtual que tem o mesmo nível de confiança. Como os aplicativos em um ambiente virtual do App-V podem compartilhar recursos, como a área de transferência, configure o ambiente virtual de modo que os aplicativos selecionados tenham o mesmo nível de confiança.

Para mais informações, confira [Criar ambientes virtuais App-V](/sccm/apps/deploy-use/create-app-v-virtual-environments).


### <a name="make-sure-macos-apps-are-from-a-trustworthy-source"></a>Verifique se os aplicativos macOS são de uma fonte confiável

Se você implantar aplicativos de dispositivos macOS, verifique se os arquivos de origem são de uma fonte confiável. A ferramenta CMAppUtil não valida a assinatura do pacote de origem. Verifique se o pacote vem de uma fonte confiável. A ferramenta CMAppUtil não é capaz de detectar se os arquivos foram violados.


### <a name="secure-the-cmmac-file-for-macos-apps"></a>Proteger o arquivo cmmac para aplicativos macOS

Se você implantar aplicativos para computadores macOS, proteja o local do arquivo **.cmmac**. A ferramenta CMAppUtil gera esse arquivo e, em seguida, você o importa para o Configuration Manager. Esse arquivo não está assinado nem validado. 

Proteja o canal de comunicação ao importar esse arquivo para o Configuration Manager. Para ajudar a evitar a violação desse arquivo, armazene-o em uma pasta protegida. Use o IPsec entre os seguintes computadores:
- O computador que executa o console do Configuration Manager  
- O computador que armazena o arquivo **.cmmac**  


### <a name="use-https-for-web-applications"></a>Usar HTTPS para aplicativos Web

Se for configurar um tipo de implantação de aplicativo Web, use HTTPS para proteger a conexão. Se você implantar um aplicativo Web usando um link HTTP em vez de um link HTTPS, o dispositivo poderá ser redirecionado para um servidor não autorizado. Os dados transferidos entre o dispositivo e o servidor poderão ser adulterados.



##  <a name="security-issues-for-application-management"></a>Problemas de segurança para gerenciamento de aplicativos  

-   Usuários com direitos limitados podem copiar arquivos do cache de cliente no computador cliente.  

     Os usuários podem ler o cache do cliente, mas não podem gravar nada nele. Com permissões de leitura, um usuário pode copiar arquivos de instalação do aplicativo de um computador para outro.  

-   Usuários com direitos limitados podem alterar os arquivos que registram o histórico de implantação de software no computador cliente.  

     Como as informações de histórico do aplicativo não estão protegidas, um usuário pode alterar os arquivos que relatam se um aplicativo está instalado.  

-   Os pacotes do App-V não são assinados.  

     Os pacotes do App-V no Configuration Manager não dão suporte à autenticação. As assinaturas digitais verificam se o conteúdo é proveniente de uma origem confiável e não foi alterado em trânsito. Não há nenhuma mitigação para esse problema de segurança. Siga a melhor prática de segurança de baixar o conteúdo de uma origem confiável e de um local seguro.  

-   Aplicativos publicados do App-V podem ser instalados por todos os usuários no computador.  

     Quando um aplicativo do App-V é publicado em um computador, todos os usuários que entrarem nesse computador poderão instalar o aplicativo. Não é possível restringir os usuários que podem instalar o aplicativo após sua publicação.  

-   Você não pode restringir as permissões de instalação para o portal da empresa em dispositivos móveis.  

     Embora você possa definir uma configuração do cliente para restringir permissões de instalação, essa configuração não funciona para o portal da empresa. Esse problema pode resultar em uma elevação de privilégios. Os usuários podem instalar um aplicativo que eles não têm permissão para instalar.  



##  <a name="BKMK_CertificatesSilverlight5"></a> Certificados para o Microsoft Silverlight 5 e modo de confiança elevada necessários para o catálogo de aplicativos  

> [!Important]  
> A partir do Configuration Manager versão 1802, o cliente não instala o Silverlight automaticamente.
> 
> A partir da versão 1806, não há mais suporte para a **experiência do usuário do Silverlight** para o ponto do site do Catálogo de Aplicativos. Os usuários devem usar o novo Centro de Software. Para saber mais, veja [Configurar Centro de Software](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex).  

 Os clientes do Configuration Manager versão 1710 e mais recente exigem o Microsoft Silverlight 5, que deve ser executado em modo de confiança elevada para que os usuários instalem o software do Catálogo de Aplicativos. Por padrão, os aplicativos Silverlight são executados no modo de confiança parcial para impedir que os aplicativos acessem dados do usuário. Se ele ainda não estiver instalado, o Configuration Manager instalará automaticamente o Microsoft Silverlight 5 nos clientes. Por padrão, o Configuration Manager define a configuração do cliente do Agente de computador **Permitir que os aplicativos Silverlight sejam executados no modo de confiança elevada** para **Sim**. Essa configuração permite que os aplicativos Silverlight assinados e confiáveis solicitem o modo de confiança elevada.  

 Quando você instala a função do sistema de site do ponto de sites da Web do catálogo de aplicativos, o cliente também instala um certificado de autenticação da Microsoft no repositório de certificados do computador de Editores Confiáveis em cada computador cliente do Configuration Manager. Os aplicativos Silverlight assinados por esse cerificado são executados no modo de confiança elevada, que os computadores exigem para instalar o software do Catálogo de Aplicativos. O Configuration Manager gerencia automaticamente este certificado de assinatura. Para garantir a continuidade do serviço, não exclua manualmente nem mova esse certificado de autenticação da Microsoft.  

> [!WARNING]  
>  Quando habilitada, a configuração do cliente **Permitir que os aplicativos Silverlight sejam executados no modo de confiança elevada** permite que todos os aplicativos Silverlight, assinados por certificados no repositório de certificados de Fornecedores Confiáveis no repositório do computador ou do usuário, sejam executados no modo de confiança elevada. A configuração do cliente não pode habilitar o modo de confiança elevada especificamente para o Catálogo de Aplicativos do Configuration Manager ou para o repositório de certificados de Fornecedores Confiáveis no repositório do computador. Se um malware adicionar um certificado não autorizado ao repositório de Fornecedores Confiáveis, o malware que usa seu próprio aplicativo Silverlight também poderá ser executado no modo de confiança elevada.  

 Se você definir a configuração do cliente **Permitir que os aplicativos Silverlight sejam executados no modo de confiança elevada** como **Não**, os clientes não removerão o certificado de autenticação da Microsoft.  

 Para saber mais sobre aplicativos confiáveis no Silverlight, consulte [Aplicativos confiáveis](https://go.microsoft.com/fwlink/p/?LinkId=252842).  



##  <a name="privacy-information-for-application-management"></a>Informações de privacidade sobre gerenciamento de aplicativos  

 O gerenciamento de aplicativos permite executar qualquer aplicativo, programa ou script em qualquer cliente na hierarquia. O Configuration Manager não tem controle sobre os tipos de aplicativos, programas ou scripts que são executados ou sobre os tipos de informações que eles transmitem. Durante o processo de implantação do aplicativo, o Configuration Manager pode transmitir informações que identificam o dispositivo e as contas de logon entre clientes e servidores.  

 O Configuration Manager mantém informações de status sobre o processo de implantação de software. As informações de status da implantação de software não são criptografadas durante a transmissão, a menos que o cliente se comunique usando HTTPS. As informações de status não são armazenadas de forma criptografada no banco de dados.  

 O uso da instalação do aplicativo do Configuration Manager para instalar software remotamente, de forma interativa ou silenciosa em clientes, pode estar sujeita aos termos da licença de software desse software. Esse uso é separado dos termos de licença de Software do System Center Configuration Manager. Sempre leia e concorde com os Termos de Licença para Software antes de implantar software usando o Configuration Manager.  

 O Configuration Manager coleta dados de diagnóstico e de uso sobre aplicativos, que são usados pela Microsoft para aprimorar as versões futuras. Para obter mais informações, consulte [Dados de diagnóstico e de uso](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).

 A implantação do aplicativo não ocorre por padrão e exige várias etapas de configuração.  

 Os seguintes recursos ajudam a implantação de software eficiente:   

- **A afinidade de dispositivo de usuário** mapeia um usuário para dispositivos. Um administrador do Configuration Manager implanta um software em um usuário. O cliente instala automaticamente o software em um ou mais computadores que o usuário usa com mais frequência.  

- O **Catálogo de Aplicativos** é um site que permite aos usuários solicitar o software a ser instalado.  

    > [!Note]  
    > A partir do Configuration Manager 1802, a principal funcionalidade do Catálogo de Aplicativos agora está incluída no Centro de Software. Para saber mais, veja [Configurar Centro de Software](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex).  

- O **Centro de Software** é instalado automaticamente em um dispositivo durante a instalação do cliente do Configuration Manager. Os usuários alteram configurações, procuram e instalam aplicativos do Centro de Software.  

  Exiba as seguintes seções para obter informações de privacidade sobre a [afinidade de dispositivo de usuário](#bkmk_privacy-uda) e o [Centro de Software e Catálogo de Aplicativos](#bkmk_privacy-userex).  

  Para poder configurar o gerenciamento de aplicativos, considere seus requisitos de privacidade.  


### <a name="bkmk_privacy-uda"></a> Afinidade de dispositivo do usuário  

-  O Configuration Manager pode transmitir informações entre clientes e sistema de sites do ponto de gerenciamento. As informações podem identificar o computador e a conta de logon e o uso resumido das contas de logon.  

-  As informações transmitidas entre o cliente e o servidor não são criptografadas, a não ser que o ponto de gerenciamento esteja configurado para exigir que os clientes se comuniquem usando HTTPS.  

-  As informações do computador e de uso da conta de entrada, usadas para mapear um usuário para um dispositivo, são armazenadas em computadores cliente, enviadas aos pontos de gerenciamento e, em seguida, armazenadas no banco de dados do Configuration Manager. As informações antigas são excluídas do banco de dados por padrão após 90 dias. O comportamento de exclusão é configurável, definindo a tarefa de manutenção do site **Excluir Dados Antigos de Afinidade de Dispositivo de Usuário** .  

-  O Configuration Manager mantém informações de status sobre afinidade de dispositivo de usuário. As informações de status não são criptografadas durante a transmissão, a menos que os clientes sejam configurados para se comunicar com pontos de gerenciamento usando HTTPS. As informações de status não são armazenadas de forma criptografada no banco de dados.  

-  Informações de uso do computador e entrada, usadas para estabelecer afinidade de dispositivo e de usuário, estão sempre habilitadas. Os usuários e os usuários administrativos podem fornecer informações de afinidade de dispositivo de usuário.  


### <a name="bkmk_privacy-userex"></a> Centro de Software e o Catálogo de Aplicativos  

-  O Centro de Software e o Catálogo de Aplicativos permitem que o administrador do Configuration Manager publique qualquer aplicativo, programa ou script para os usuários executarem. O Configuration Manager não tem controle sobre os tipos de programas ou scripts que são publicados no catálogo ou sobre os tipos de informações que eles transmitem.  

-  O Configuration Manager pode transmitir informações entre clientes e as funções do sistema de sites do Catálogo de Aplicativos. As informações podem identificar as contas de computador e de entrada. As informações transmitidas entre o cliente e os servidores não são criptografadas, a não ser que essas funções do sistema de sites sejam configuradas para exigir que os clientes se conectem usando HTTPS.  

-  As informações sobre a solicitação de aprovação do aplicativo são armazenadas no banco de dados do Configuration Manager. As solicitações canceladas ou negadas e as entradas de histórico de solicitação correspondentes são excluídas por padrão após 30 dias. O comportamento de exclusão é configurável, definindo a tarefa de manutenção do site **Excluir Dados Antigos de Solicitação de Aplicativo** . As solicitações de aprovação de aplicativo que estão em estado aprovado e pendente nunca são excluídas.  

-  O Centro de Software é instalado automaticamente durante a instalação do cliente do Configuration Manager em um dispositivo.  

-  O Catálogo de Aplicativos não está instalado por padrão. Essa instalação requer várias etapas de configuração.  
