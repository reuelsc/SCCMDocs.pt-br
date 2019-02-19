---
title: Segurança e privacidade do gerenciamento de conteúdo
titleSuffix: Configuration Manager
description: Otimize a segurança e a privacidade para gerenciamento de conteúdo no Configuration Manager.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5f665ea8315266e89e5ed94918823fc1b97becea
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56136425"
---
# <a name="security-and-privacy-for-content-management-in-configuration-manager"></a>Segurança e privacidade para gerenciamento de conteúdo no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo contém informações de segurança e privacidade para o gerenciamento de conteúdo no Configuration Manager. 



##  <a name="BKMK_Security_ContentManagement"></a> Melhores práticas de segurança para gerenciamento de conteúdo  


#### <a name="advantages-and-disadvantages-of-https-or-http-for-intranet-distribution-points"></a>Vantagens e desvantagens de HTTP ou HTTPS para pontos de distribuição de intranet
Para pontos de distribuição na intranet, considere as vantagens e desvantagens do uso de HTTPS e HTTP. Na maioria dos cenários, usar o HTTP e as contas de acesso de pacote para autorização oferece mais segurança do que o HTTPS com criptografia mas sem autorização. No entanto, se você possui dados confidenciais em seu conteúdo e deseja que sejam criptografados durante a transferência, use o HTTPS.  

-   **Quando você usa o HTTPS para um ponto de distribuição**, o Configuration Manager não usa contas de acesso ao pacote para autorizar o acesso ao conteúdo, mas o conteúdo é criptografado quando transferido pela rede.  

-   **Quando você usa o HTTP para um ponto de distribuição**, você pode usar as contas de acesso de pacote para autorização, mas o conteúdo não é criptografado quando transferido pela rede.  

Começando na versão 1806, considere a habilitação do **HTTP aprimorado** para o site. Esse recurso permite que os clientes usem a autenticação do Azure Active Directory para se comunicar com segurança com um ponto de distribuição de HTTP. Para obter mais informações, confira [HTTP aprimorado](/sccm/core/plan-design/hierarchy/enhanced-http).

#### <a name="protect-the-client-authentication-certificate-file"></a>Proteger o arquivo de certificado de autenticação de cliente
Se você utiliza o certificado de autenticação de cliente PKI em vez do certificado autoassinado para o ponto de distribuição, proteja o arquivo do certificado (.pfx) com uma senha forte. Se você armazena o arquivo na rede, projeta o canal de rede ao importar o arquivo para o Configuration Manager.

Quando você requer uma senha para importar o certificado de autenticação de cliente que o ponto de distribuição usa para se comunicar com os pontos de gerenciamento, essa configuração ajuda a proteger o certificado de um invasor. Use a assinatura do protocolo SMB ou o IPsec entre o local de rede e o servidor do site para impedir que um invasor viole o arquivo de certificado.  

#### <a name="remove-the-distribution-point-role-from-the-site-server"></a>Remover a função de ponto de distribuição do servidor do site
Por padrão, a instalação do Configuration Manager instala um ponto de distribuição no servidor do site. Os clientes não precisam se comunicar diretamente com o servidor do site. Para reduzir a superfície sujeita a ataques, atribua a função do ponto de distribuição a outros sistemas de site e remova-a do servidor do site.  

#### <a name="secure-content-at-the-package-access-level"></a>Proteger o conteúdo no nível de acesso do pacote
O compartilhamento de ponto de distribuição permite o acesso de leitura para todos os usuários. Para restringir quais usuários podem acessar o conteúdo, use as contas de acesso de pacote quando o ponto de distribuição está configurado para HTTP. Essa configuração não se aplica a pontos de distribuição na nuvem, que não dão suporte para contas de acesso de pacote. Para obter mais informações, confira [Contas de acesso de pacote](/sccm/core/plan-design/hierarchy/accounts#package-access-account).

#### <a name="configure-iis-on-the-distribution-point-role"></a>Configurar o IIS na função de ponto de distribuição
Se o Configuration Manager instalar o IIS quando você adicionar uma função do sistema de site do ponto de distribuição, remova o Redirecionamento HTTP ou Ferramentas e Scripts de Gerenciamento do IIS quando a instalação do ponto de distribuição estiver concluída. O ponto de distribuição não exige Redirecionamento HTTP e Ferramentas ou Scripts de Gerenciamento do IIS. Para reduzir a superfície de ataque, remova esses serviços de função para a função de servidor Web.  Para obter mais informações sobre os serviços de função para a função de servidor Web para pontos de distribuição, confira [Pré-requisitos do site e do sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  

#### <a name="set-package-access-permissions-when-you-create-the-package"></a>Defina as permissões de acesso ao pacote ao criar o pacote
Como as alterações às contas de acesso nos arquivos de pacote terão efeito somente quando você redistribui o pacote, defina as permissões de acesso ao pacote com cuidado ao criar pela primeira vez o pacote. Essa configuração será importante quando o pacote for grande ou distribuído a muitos pontos de distribuição e quando a capacidade da largura de banda da rede para distribuição de conteúdo for limitada.  

#### <a name="implement-access-controls-to-protect-media-that-contains-prestaged-content"></a>Implemente controles de acesso para proteger a mídia que contém o conteúdo de pré-teste
O conteúdo de pré-teste está compactado, mas não criptografado. Um invasor pode ler e modificar os arquivos que são baixados nos dispositivos. Os clientes do Configuration Manager rejeitam o conteúdo que foi adulterado, mas eles ainda o baixam.  

#### <a name="import-prestaged-content-with-extractcontent"></a>Importar o conteúdo de pré-teste com ExtractContent
Somente importe conteúdo de pré-teste usando a ferramenta de linha de comando ExtractContent.exe. Para evitar violação ou elevação de privilégios, use somente a ferramenta de linha de comando autorizada que é fornecida com o Configuration Manager.  

#### <a name="secure-the-communication-channel-between-the-site-server-and-the-package-source-location"></a>Proteja o canal de comunicação entre o servidor de site e o local de origem do pacote
Use IPsec ou assinatura SMB entre o servidor de site e a localização de origem do pacote quando criar aplicativos e pacotes. Essa configuração ajuda a impedir que um invasor viole os arquivos de origem.  

#### <a name="remove-default-virtual-directories-for-custom-website-with-the-distribution-point-role"></a>Remover diretórios virtuais padrão para o site da Web personalizado com a função de ponto de distribuição
Se você alterar a opção de configuração de site para usar um site da Web personalizado em vez de um site da Web padrão após a instalação de uma função de ponto de distribuição, remova os diretórios virtuais padrão. Quando você muda do site da Web padrão para um site da Web personalizado, o Configuration Manager não remove os diretórios virtuais antigos. Remova os diretórios virtuais a seguir que o Configuration Manager criou originalmente no site padrão:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  


#### <a name="for-cloud-distribution-points-protect-your-azure-subscription-details-and-certificates"></a>Pontos de distribuição na nuvem, proteja seus certificados e detalhes da assinatura do Azure
Ao usar pontos de distribuição na nuvem, proteja os seguintes itens importantes:
- O nome de usuário e a senha de sua assinatura do Azure
- O certificado de gerenciamento do Azure 
- O certificado de serviço do ponto de distribuição na nuvem

Armazene os certificados com segurança. Se você os procura pela rede quando você configura o ponto de distribuição na nuvem, use o IPsec ou a assinatura SMB entre o servidor de site e a localização de origem.  

#### <a name="for-service-continuity-monitor-the-expiry-date-of-the-cloud-distribution-point-certificates"></a>Para continuidade de serviços, monitore a data de expiração dos certificados de ponto de distribuição na nuvem
O Configuration Manager não avisa quando os certificados importados para o ponto de distribuição na nuvem estão prestes a expirar. Monitore as datas de expiração independentemente do Configuration Manager. Não deixe de renovar e depois importar os novos certificados antes da data de expiração. Essa ação será importante se você adquirir um certificado de autenticação de servidor de um provedor externo, público, porque você poderá precisar de mais tempo para adquirir um certificado renovado.  

 Se um desses certificados expirar, o Gerenciador de Serviços de Nuvem gerará a ID de mensagem de status **9425**. O arquivo CloudMgr.log contém uma entrada para indicar que o certificado **está em estado expirado**, com a data de expiração também registrada em UTC.  



## <a name="security-considerations-for-content-management"></a>Considerações de segurança para o gerenciamento de conteúdo  

Considere os seguintes pontos ao planejar o gerenciamento de conteúdo:  

-   Clientes não validam o conteúdo até depois que ele é baixado.  

     Os clientes do Configuration Manager validam o hash no conteúdo somente após ele é baixado em seu cache do cliente. Se um invasor viola a lista de arquivos a baixar ou seu próprio conteúdo, o processo de download pode comprometer de modo considerável a largura de banda de rede apenas para o cliente depois descartar o conteúdo ao encontrar um hash inválido.  

-   Quando você usa pontos de distribuição na nuvem, o acesso ao conteúdo é automaticamente restrito à sua empresa. Você não pode restringi-lo posteriormente a usuários ou grupos selecionados.  

-   Quando você usa pontos de distribuição na nuvem, os clientes são autenticados pelo ponto de gerenciamento e usam um token do Configuration Manager para acessar os pontos de distribuição na nuvem. O token é válido por oito horas. Esse comportamento significa que se você bloquear um cliente porque ele não é mais confiável, ele poderá continuar a baixar o conteúdo de um ponto de distribuição na nuvem até que o período de validade desse token tiver expirado. Nesse ponto, o ponto de gerenciamento não emitirá outro token para o cliente, pois ele está bloqueado.  

     Para evitar que um cliente bloqueado baixe conteúdo durante essa janela de oito horas, pare o serviço de nuvem. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e selecione o nó **Pontos de Distribuição na Nuvem**.  



##  <a name="BKMK_Privacy_ContentManagement"></a> Informações de privacidade para gerenciamento de conteúdo  

 O Configuration Manager não inclui dados do usuário nos arquivos de conteúdo, embora o usuário administrativo possa optar por fazer essa ação.  



## <a name="see-also"></a>Consulte também

- [Conceitos fundamentais para o gerenciamento de conteúdo](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)  

- [Segurança e privacidade para gerenciamento de aplicativos](/sccm/apps/plan-design/security-and-privacy-for-application-management)  

- [Segurança e privacidade das atualizações de software](/sccm/sum/plan-design/security-and-privacy-for-software-updates)  

- [Segurança e privacidade para implantação do sistema operacional](/sccm/osd/plan-design/security-and-privacy-for-operating-system-deployment)  
