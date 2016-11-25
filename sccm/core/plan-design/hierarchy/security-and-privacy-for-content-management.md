---
title: "Segurança e privacidade do gerenciamento de conteúdo | System Center Configuration Manager"
description: "Otimize a segurança e a privacidade do gerenciamento de conteúdo no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: fcc3c74e50a4cdac9337178f5fcfe710f0fa17a5


---
# <a name="security-and-privacy-for-content-management-for-system-center-configuration-manager"></a>Segurança e privacidade do gerenciamento de conteúdo no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico contém informações de segurança e privacidade para o gerenciamento de conteúdo no System Center Configuration Manager. Leia-o em conjunto com os seguintes tópicos:  

-   [Segurança e privacidade para gerenciamento de aplicativos no System Center Configuration Manager](../../../apps/plan-design/security-and-privacy-for-application-management.md)  

-   [Segurança e privacidade das atualizações de software no System Center Configuration Manager](/sccm/sum/plan-design/security-and-privacy-for-software-updates)  

-   [Segurança e privacidade para a implantação de sistema operacional no System Center Configuration Manager](../../../osd/plan-design/security-and-privacy-for-operating-system-deployment.md)  

##  <a name="a-namebkmksecuritycontentmanagementa-security-best-practices-for-content-management"></a><a name="BKMK_Security_ContentManagement"></a> Melhores práticas de segurança para gerenciamento de conteúdo  
 Use as seguintes práticas recomendadas de segurança para gerenciamento de conteúdo:  

 **Para pontos de distribuição na intranet, considere as vantagens e desvantagens do uso de HTTPS e HTTP** – na maioria dos cenários, usar o HTTP e as contas de acesso de pacote para autorização oferece mais segurança do que o HTTPS com criptografia, mas sem autorização. No entanto, se você possui dados confidenciais em seu conteúdo e deseja que sejam criptografados durante a transferência, use o HTTPS.  

-   **Quando você usa o HTTPS para um ponto de distribuição**, o Configuration Manager não usa contas de acesso de pacote para autorizar o acesso ao conteúdo, mas o conteúdo é criptografado quando transferido pela rede.  

-   **Quando você usa o HTTP para um ponto de distribuição**, você pode usar as contas de acesso de pacote para autorização, mas o conteúdo não é criptografado quando transferido pela rede.  


**Se você utiliza um certificado de autenticação de cliente PKI em vez do certificado autoassinado para o ponto de distribuição, proteja o arquivo do certificado (.pfx) com uma senha forte. Se você armazenar o arquivo na rede, proteja o canal da rede quando importar o arquivo para o Configuration Manager** – quando você exige uma senha para importar o certificado de autenticação de cliente que usa para que o ponto de distribuição se comunique com os pontos de gerenciamento, isso ajuda a proteger o certificado de um invasor. Use a assinatura SMB ou o IPsec entre o local de rede e o servidor de site para impedir que um invasor viole o arquivo de certificado.  

**Remova a função de ponto de distribuição do servidor do site** - por padrão, um ponto de distribuição é instalado no mesmo servidor que o servidor do site. Os clientes não precisam se comunicar diretamente com o servidor do site, então para reduzir a superfície sujeita a ataques, atribua a função do ponto de distribuição a outros sistemas de site e remova-a do servidor do site.  

**Proteja o conteúdo no nível de acesso de pacote** – o compartilhamento do ponto de distribuição permite acesso de Leitura a todos os usuários. Para restringir quais usuários podem acessar o conteúdo, use as contas de acesso de pacote quando o ponto de distribuição está configurado para HTTP. Isso não se aplica a pontos de distribuição baseados em nuvem, que não dão suporte para contas de acesso de pacote. Para obter mais informações sobre a Conta de Acesso ao Pacote, consulte a seção [Gerenciar contas para acessar conteúdo](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).


**Se o Configuration Manager instalar o IIS quando você adicionar uma função do sistema de sites do ponto de distribuição, remova o Redirecionamento HTTP e as Ferramentas e Scripts de Gerenciamento do IIS quando a instalação do ponto de distribuição estiver concluída** – o ponto de distribuição não exige Redirecionamento HTTP e as Ferramentas e Scripts de Gerenciamento do IIS. Para reduzir a superfície de ataque, remova esses serviços de função para a função de servidor Web (IIS).  Para obter mais informações sobre os serviços de função para a função de servidor Web (IIS) para pontos de distribuição, consulte [Site and site system prerequisites (Pré-requisitos do site e do sistema de sites)](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  

**Definir as permissões de acesso ao pacote ao criar o pacote** – como as alterações às contas de acesso nos arquivos de pacote terão efeito somente quando você redistribuir o pacote, defina as permissões de acesso ao pacote com cuidado ao criar pela primeira vez o pacote. Isso será especialmente importante quando o pacote for grande ou distribuído a muitos pontos de distribuição e quando a capacidade da largura de banda da rede para distribuição de conteúdo for limitada.  

**Implemente controles de acesso para proteger a mídia que contém o conteúdo de pré-teste** – o conteúdo de pré-teste está compactado, mas não criptografado. Um invasor pode ler e modificar os arquivos que são baixados nos dispositivos. Os clientes do Configuration Manager rejeitarão o conteúdo que foi adulterado, mas eles ainda o baixarão.  

**Importe o conteúdo pré-teste usando somente a ferramenta de linha de comando ExtractContent (ExtractContent.exe) fornecida com o Configuration Manager e certifique-se de que ela esteja assinada pela Microsoft** – para evitar a violação e elevação de privilégios, use somente a ferramenta de linha de comando autorizada fornecida com o Configuration Manager.  

**Proteja o canal de comunicação entre o servidor do site e o local de origem do pacote** – use IPsec ou assinatura SMB entre o servidor de site e o local de origem do pacote para quando criar aplicativos e pacotes. Isso ajuda a impedir que um invasor viole os arquivos de origem.  

**Se você alterar a opção de configuração do site para usar um site personalizado em vez do site padrão após a instalação das funções de ponto de distribuição, remova os diretórios virtuais padrão** – quando você passa a usar um site personalizado em vez do site padrão, o Configuration Manager não remove os diretórios virtuais antigos. Remova os diretórios virtuais que o Configuration Manager criou originalmente no site da Web padrão:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  

**Para pontos de distribuição baseados em nuvem, proteja seus detalhes da assinatura e certificados** – ao usar pontos de distribuição baseados em nuvem, proteja itens de alto valor, incluindo o nome de usuário e a senha da sua assinatura do Azure, o certificado de gerenciamento do Azure e o certificado de serviço do ponto de distribuição baseado em nuvem. Armazene os certificados com segurança e se você os procura pela rede quando você configura o ponto de distribuição baseado em nuvem, use o IPsec ou a assinatura SMB entre o servidor de site e o local de origem.  

**Pontos de distribuição baseados em nuvem: para ter continuidade dos serviços, monitore a data de expiração dos certificados** –o Configuration Manager não o avisa quando os certificados importados para o gerenciamento do serviço de ponto de distribuição baseado em nuvem estão prestes a expirar. É necessário monitorar as datas de expiração independentemente do Configuration Manager e se certificar de renovar e depois importar o novo certificado antes da data de expiração. Isso é importante se você compra um certificado de serviço do ponto de distribuição baseado em nuvem para o Configuration Manager proveniente de uma AC (autoridade de certificação) externa, pois você pode precisar de mais tempo para obter um certificado renovado.  

 Se um desses certificados expira, o **Gerenciador de Serviços em Nuvem** gera uma mensagem de status com a ID **9425** e o arquivo **CloudMgr.log** contém uma entrada que indica que o certificado **is in expired state**, com a data de expiração também registrada em UTC.  

## <a name="security-considerations-for-content-management"></a>Considerações de segurança para o gerenciamento de conteúdo  
Considere o seguinte ao planejar o gerenciamento de conteúdo:  

-   Clientes não validam o conteúdo até depois que ele é baixado  

     Os clientes do Configuration Manager validam o hash no conteúdo somente após ele é baixado em seu cache do cliente. Se um invasor viola a lista de arquivos a baixar ou seu próprio conteúdo, o processo de download pode comprometer de modo considerável a largura de banda de rede para o cliente depois descartar o conteúdo ao encontrar um hash inválido.  

-   Quando você usa pontos de distribuição baseados em nuvem, o acesso ao conteúdo é automaticamente restrito à sua empresa e você não pode restringi-lo posteriormente a usuários ou grupos selecionados.  

-   Quando você usa pontos de distribuição baseados em nuvem, os clientes são autenticados pelo ponto de gerenciamento e usam um token do Configuration Manager para acessar os pontos de distribuição baseados em nuvem. O token é válido por 8 horas então se você bloquear um cliente porque ele não é mais confiável, ele poderá continuar a baixar o conteúdo de um ponto de distribuição baseado em nuvem até que o período de validade desse token estiver expirado. Nesse ponto, o ponto de gerenciamento não emitirá outro token para o cliente, pois ele está bloqueado.  

     Para evitar que um cliente bloqueado baixe conteúdo durante essa janela de 8 horas, é possível interromper o serviço de nuvem no nó **Nuvem**, **Configuração da Hierarquia**, no espaço de trabalho **Administração** no console do Configuration Manager.  

##  <a name="a-namebkmkprivacycontentmanagementa-privacy-information-for-content-management"></a><a name="BKMK_Privacy_ContentManagement"></a> Informações de privacidade para gerenciamento de conteúdo  
 O Configuration Manager não inclui dados do usuário nos arquivos de conteúdo, embora o usuário administrativo possa optar por fazê-lo.  

 Para poder configurar o gerenciamento de conteúdo, considere seus requisitos de privacidade.  



<!--HONumber=Nov16_HO1-->


