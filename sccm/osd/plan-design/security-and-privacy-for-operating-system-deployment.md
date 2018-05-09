---
title: Segurança e privacidade para implantação de sistema operacional
titleSuffix: Configuration Manager
description: Saiba sobre as práticas recomendadas de segurança e privacidade para a implantação de sistema operacional no System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 5ee5928f-3d72-4b00-8156-1e0d1030a96c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4ec1457fafabe2e40106ec76310d9ff64b2aa267
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="security-and-privacy-for-operating-system-deployment-in-system-center-configuration-manager"></a>Segurança e privacidade para a implantação de sistema operacional no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico contém informações de segurança e privacidade para a implantação de sistema operacional no System Center Configuration Manager.  

##  <a name="BKMK_Security_HardwareInventory"></a> Práticas recomendadas de segurança para a implantação de sistema operacional  
 Use as práticas recomendadas de segurança a seguir para quando você implantar sistemas operacionais com o Configuration Manager:  

-   **Implementar controles de acesso para proteger a mídia inicializável**  

     Ao criar uma mídia inicializável, sempre atribua uma senha para ajudar a proteger a mídia. No entanto, mesmo com uma senha, somente os arquivos que contêm informações confidenciais são criptografados, e todos os arquivos pode ser substituídos.  

     Controle o acesso físico à mídia para impedir que um invasor use ataques de criptografia para obter o certificado de autenticação de cliente.  

     Para ajudar a impedir que um cliente instale algum conteúdo ou alguma política do cliente que foi violada, o conteúdo contém um hash e deve ser usado com a política original.  Se o hash de conteúdo falhar ou a verificação do conteúdo corresponder à política, o cliente não usará a mídia inicializável. Somente o conteúdo está com hash; a política não, mas está criptografada e protegida quando você especifica uma senha, o que dificulta mais a ação de um invasor para modificar a política com êxito.  

-   **Usar um local seguro quando você cria mídia para imagens do sistema operacional**  

     Se usuários não autorizados tiverem acesso ao local, eles poderão violar os arquivos que você cria e usar todo o espaço em disco disponível para que ocorra falha na criação da mídia.  

-   **Proteger arquivos (.pfx) do certificado com uma senha forte e, se você armazená-los na rede, proteger o canal de rede ao importá-los para o Configuration Manager**  

     Quando você requer uma senha para importar o certificado de autenticação de cliente que você usa para a mídia inicializável, isso ajuda a proteger o certificado de um invasor.  

     Use a assinatura SMB ou o IPsec entre o local de rede e o servidor de site para impedir que um invasor viole o arquivo de certificado.  

-   **Se o certificado do cliente estiver comprometido, bloqueie o certificado do Configuration Manager e revogue-o se ele for um certificado PKI**  

     Para implantar um sistema operacional usando a mídia inicializável e a inicialização PXE, você deve ter um certificado de autenticação de cliente com uma chave privada. Se esse certificado estiver comprometido, bloqueie-o no nó **Certificados** no espaço de trabalho **Administração** , no nó **Segurança** .  

-   **Quando o Provedor de SMS está em um computador ou computadores diferentes do servidor do site, proteger o canal de comunicação para proteger imagens de inicialização**  

     Quando imagens de inicialização são modificadas e o Provedor de SMS é executado em um servidor que não é o servidor do site, as imagens de inicialização estão vulneráveis a ataque. Proteja o canal de rede entre esses computadores usando a assinatura SMB ou IPsec.  

-   **Habilitar pontos de distribuição para comunicação do cliente PXE apenas em segmentos de rede segura**  

     Quando um cliente enviar uma solicitação de inicialização PXE, você não tem como verificar se a solicitação é atendida por um ponto de distribuição válido habilitado para PXE. Esse cenário tem os seguintes riscos de segurança:  

    -   Um ponto de distribuição não autorizado que responde às solicitações de PXE pode fornecer uma imagem violada aos clientes.  

    -   Um invasor pode iniciar um ataque de falsificação contra o protocolo TFTP que é usado pelo PXE e enviar código mal-intencionado com os arquivos do sistema operacional, ou pode criar um cliente não autorizado para fazer solicitações do TFTP diretamente ao ponto de distribuição.  

    -   Um invasor pode usar um cliente mal-intencionado para iniciar um ataque de negação de serviço contra o ponto de distribuição.  

     Use proteção abrangente para proteger os segmentos de rede onde os clientes terão acesso a pontos de distribuição para solicitações de PXE.  

    > [!WARNING]  
    >  Por conta desses riscos de segurança, não habilite um ponto de distribuição para comunicação PXE quando ele estiver em uma rede não confiável, como uma rede de perímetro.  

-   **Configurar pontos de distribuição habilitados para PXE para responder às solicitações de PXE somente em interfaces de rede especificadas**  

     Se você permitir que o ponto de distribuição responda às solicitações de PXE em todas as interfaces de rede, essa configuração pode expor o serviço PXE a redes não confiáveis.  

-   **Exigir uma senha para a inicialização PXE**  

     Quando você exige uma senha para a inicialização PXE, essa configuração adiciona um nível extra de segurança ao processo de inicialização PXE, para ajudar a proteger contra clientes não autorizados que ingressam na hierarquia do Configuration Manager.  

-   **Não incluir aplicativos de linha de negócios ou software que contenha dados confidenciais em uma imagem que será usada para inicialização PXE ou multicast**  

     Por conta dos riscos de segurança inerentes envolvidos com a inicialização PXE e multicast, reduza is riscos se o computador não autorizado baixar a imagem do sistema operacional.  

-   **Não incluir aplicativos de linha de negócios ou software que contenha dados confidenciais em pacotes de software instalados usando variáveis de sequências de tarefas**  

     Quando você implanta pacotes de software usando variáveis de sequências de tarefas, o software pode ser instalado em computadores e usuários que não estão autorizados a receber esse software.  

-   **Quando você migra o estado do usuário, proteja o canal de rede entre o cliente e o ponto de migração do estado usando assinatura SMB ou IPsec**  

     Após a conexão inicial sobre HTTP, os dados de migração de estado do usuário serão transferidos usando SMB.  Se você não proteger o canal de rede, um invasor poderá ler e modificar esses dados.  

-   **Usar a versão mais recente da USMT (Ferramenta de Migração do Usuário) à qual o Configuration Manager dá suporte**  

     A versão mais recente da USMT fornece aprimoramentos de segurança e mais controle para quando você migrar dados de estado do usuário.  

-   **Excluir manualmente as pastas no ponto de migração de estado quando elas são encerradas**  

     Quando você remove uma pasta do ponto de migração de estado no console do Configuration Manager nas propriedades do ponto de migração de estado, a pasta física não é excluída. Para proteger os dados de migração de estado contra divulgação de informações, você deve remover manualmente o compartilhamento de rede e excluir a pasta.  

-   **Não configurar a política de exclusão para excluir imediatamente o estado do usuário**  

     Se você configurar a política de exclusão no ponto de migração de estado para remover dados marcados para exclusão imediatamente e se um invasor recuperar os dados de estado do usuário antes que o computador válido, os dados de estado do usuário serão excluídos imediatamente. Defina o intervalo **Excluir depois** para que seja longo o suficiente para verificar a restauração com êxito dos dados de estado do usuário.  

-   **Excluir manualmente as associações de computador quando a restauração de dados de migração de estado do usuário for concluída e verificada**  

     O Configuration Manager não remove automaticamente as associações de computador. Ajude a proteger a identidade dos dados de estado do usuário excluindo manualmente associações de computador que não são mais necessárias.  

-   **Fazer backup dos dados de migração de estado do usuário manualmente no ponto de migração de estado**  

     O backup do Configuration Manager não inclui os dados de migração de estado do usuário.  

-   **Lembre-se de habilitar o BitLocker depois que o sistema operacional for instalado**  

     Se um computador der suporte ao BitLocker, você deverá desabilitá-lo usando uma etapa de sequência de tarefas se desejar instalar o sistema operacional autônomo. O Configuration Manager não habilita o BitLocker após a instalação do sistema operacional, por isso você deve habilitar o BitLocker novamente.  

-   **Implementar controles de acesso para proteger a mídia em pré-teste**  

     Controle o acesso físico à mídia para impedir que um invasor use ataques de criptografia para obter o certificado de autenticação de cliente e dados confidenciais.  

-   **Implementar controles de acesso para proteger o processo de geração de imagens do computador de referência**  

     Verifique se o computador de referência usado para capturar imagens do sistema operacional está em um ambiente seguro com controles de acesso apropriados para que nenhum software inesperado ou mal-intencionado seja instalado e incluído inadvertidamente na imagem capturada. Ao capturar a imagem, verifique se o local do compartilhamento do arquivo de destino na rede está protegido para que a imagem não seja violada depois de ser capturada.  

-   **Sempre instalar as atualizações de segurança mais recentes no computador de referência**  

     Quando o computador de referência tem atualizações de segurança, ele ajuda a reduzir a janela de vulnerabilidade para novos computadores quando são inicializados pela primeira vez.  

-   **Se você tiver de implantar sistemas operacionais em um computador desconhecido, implemente controles de acesso para impedir que computadores não autorizados se conectem à rede**  

     Embora o provisionamento de computadores desconhecidos forneça um método conveniente para implantar novos computadores sob demanda, ele também pode permitir que um invasor se torne um cliente confiável na sua rede. Restrinja o acesso físico à rede e monitore os clientes para detectar computadores não autorizados. Além disso, computadores que respondem à implantação de sistema operacional iniciada por PXE devem ter todos os dados destruídos durante a implantação, o que pode resultar em perda de disponibilidade de sistemas reformatados inadvertidamente.  

-   **Habilitar a criptografia de pacotes multicast**  

     Para cada pacote de implantação de sistema operacional, você tem a opção de habilitar a criptografia quando o Configuration Manager transfere o pacote usando multicast. Essa configuração ajuda a impedir que computadores não autorizados ingressem na sessão multicast e ajuda a impedir que invasores violem a transmissão.  

-   **Monitorar pontos de distribuição não autorizados habilitados para multicast**  

     Se os invasores puderem ter acesso à rede, eles poderão configurar servidores multicast não autorizados para falsificar a implantação de sistema operacional.  

-   **Quando você exporta sequências de tarefas para um local de rede, proteja o local e o canal de rede**  

     Restrinja quem pode acessar a pasta de rede.  

     Use a assinatura SMB ou o IPsec entre o local de rede e o servidor do site para impedir que um invasor viole a sequência de tarefas exportada.  

-   **Proteger o canal de comunicação ao carregar um disco rígido virtual no Virtual Machine Manager.**  

     Para prevenir a violação de dados durante a transferência pela rede, use o IPsec (segurança do Protocolo Internet) ou SMB (protocolo SMB) entre o computador que executa o console do Configuration Manager e o computador executando o Virtual Machine Manager.  

-   **Se você tiver de usar a Execução de Sequência de Tarefas como Conta, tome precauções de segurança adicionais**  

     Se você usar a Execução de Sequência de Tarefas como Conta, siga estas etapas de precaução:  

    -   Use uma conta com o mínimo possível de permissões.  

    -   Não use a Conta de Acesso à Rede para essa conta.  

    -   Nunca faça da conta um administrador de domínio.  

     Além disso:  

    -   Nunca configure perfis móveis para esta conta. Quando a sequência de tarefas for executada, ela baixará o perfil móvel da conta, o que deixará o perfil vulnerável a acesso no computador local.  

    -   Limite o escopo da conta. Por exemplo, crie uma Execução de Sequência de Tarefas como Contas para cada sequência de tarefas; desse modo, se uma conta for comprometida, somente os computadores cliente aos quais a conta tem acesso ficarão comprometidos. Se a linha de comando exigir acesso administrativo no computador, considere a criação de uma conta de administrador local exclusivamente para a Execução de Sequência de Tarefas como Conta em todos os computadores que executarão a sequência de tarefas e exclua a conta assim que ele não for mais necessária.  

-   **Restringir e monitorar os usuários administrativos que recebem a função de segurança do Gerenciador de Implantação de Sistema Operacional**  

     Os usuários administrativos que recebem a função de segurança do Gerenciador de Implantação de Sistema Operacional podem criar certificados autoassinados que podem ser usados para representar um cliente e obter a política do cliente do Configuration Manager.  

### <a name="security-issues-for-operating-system-deployment"></a>Problemas de segurança da implantação de sistema operacional  
 Embora a implantação de sistema operacional possa ser uma forma conveniente de implantar os sistemas operacionais e as configurações mais seguras para computadores em sua rede, ela tem os seguintes riscos de segurança:  

-   Divulgação de informações e negação de serviço  

     Se um invasor tiver controle da sua infraestrutura do Configuration Manager, ele poderá executar sequências de tarefas, o que poderá incluir formatação dos discos rígidos de todos os computadores cliente. As sequências de tarefas podem ser configuradas para conter informações confidenciais, como contas que têm permissões para ingressar no domínio e nas chaves de licenciamento por volume.  

-   Representação e elevação de privilégios  

     As sequências de tarefas podem ingressar em um computador para o domínio, o que pode fornecer a um computador não autorizado acesso autenticado à rede. Outra consideração de segurança importante para implantação de sistema operacional é proteger o certificado de autenticação de cliente usado para mídia inicializável de sequência de tarefas e para implantação de inicialização PXE. Quando você captura um certificado de autenticação de cliente, isso permite que um invasor tenha a oportunidade de obter a chave privada no certificado e represente um cliente válido na rede.  

     Se um invasor obtiver o certificado do cliente usado para mídia inicializável da sequência de tarefas e para implantação de inicialização PXE, esse certificado poderá ser usado para representar um cliente válido para o Configuration Manager. Nesse cenário, o computador não autorizado pode baixar a política, que pode conter dados confidenciais.  

     Se os clientes usam a conta de acesso à rede para acessar dados armazenados no ponto de migração de estado, eles compartilham efetivamente a mesma identidade e podem acessar os dados de migração de estado de outro cliente que utiliza a conta de acesso à rede. Os dados são criptografados para que somente o cliente original possa lê-los, mas os dados podem ser violados ou excluídos.  

-   A autenticação do cliente no ponto de migração de estado é obtida usando um token do Configuration Manager emitido pelo ponto de gerenciamento.  

     Além disso, o Configuration Manager não limita nem gerencia o volume de dados armazenado no ponto de migração de estado e um invasor pode preencher o espaço em disco disponível e causar uma negação de serviço.  

-   Se você usar variáveis da coleção, os administradores locais poderão ler as informações potencialmente confidenciais  

     Embora as variáveis da coleção ofereçam um método flexível para implantar sistemas operacionais, isso pode resultar em divulgação de informações confidenciais.  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Informações de privacidade da implantação de sistema operacional  
 Além de implantar sistemas operacionais em computadores sem sistema operacional, o Configuration Manager pode ser usado para migrar arquivos e configurações de usuários de um computador para outro. O administrador configura quais informações transferir, incluindo arquivos de dados pessoais, configurações e cookies do navegador.  

 As informações são armazenadas em um ponto de migração de estado e criptografadas durante a transmissão e o armazenamento. As informações podem ser recuperadas pelo novo computador associado às informações de estado. Se o novo computador perder a chave para recuperar as informações, um administrador do Configuration Manager com o direito para Exibir Informações de Recuperação em objetos de instância da associação do computador poderá acessar as informações e associá-las a um novo computador. Depois que o novo computador restaura as informações de estado, por padrão ele exclui os dados depois de um dia. A configuração pode ser feita quando o ponto de migração de estado remove os dados marcados para exclusão. As informações de migração de estado não são armazenadas no banco de dados do site e não são enviadas à Microsoft.  

 Se você usar a mídia de inicialização para implantar as imagens do sistema operacional, sempre utilize a opção padrão para proteger por senha a mídia de inicialização. A senha criptografa quaisquer variáveis armazenadas na sequência de tarefas, mas as informações não armazenadas em uma variável podem estar vulneráveis à divulgação.  

 A implantação de sistema operacional pode usar as sequências de tarefas para executar muitas tarefas diferentes durante o processo de implantação, inclusive a instalação de aplicativos e atualizações de software. Ao configurar as sequências de tarefas, você deve estar ciente das implicações de privacidade da instalação de software.  

 Se você carregar um disco rígido virtual para o Virtual Machine Manager sem primeiro usar o Sysprep para limpar a imagem, o disco rígido virtual carregado pode conter dados pessoais da imagem original.  

 O Configuration Manager não implementa implantações de sistema operacional por padrão e exige diversas etapas de configuração antes de você coletar informações do estado do usuário ou criar sequências de tarefas ou imagens de inicialização.  

 Antes de configurar a implantação de sistema operacional, considere seus requisitos de privacidade.  
