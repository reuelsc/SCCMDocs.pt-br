---
title: "Publicação e o esquema do Active Directory"
titleSuffix: Configuration Manager
description: Estenda o esquema do Active Directory para o System Center Configuration Manager para simplificar o processo de implantar e configurar clientes.
ms.custom: na
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bc15ee7e-4d0a-4463-ae2c-f72d8d45d65d
caps.latest.revision: "17"
caps.handback.revision: "0"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: d495c7934b92d6042399f66fe578007c32ae10f4
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2017
---
# <a name="prepare-active-directory-for-site-publishing"></a>Preparar o Active Directory para publicação de sites

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Ao estender o esquema do Active Directory para o System Center Configuration Manager, você introduz novas estruturas para o Active Directory usadas pelos sites do Configuration Manager para publicar informações chave em um local seguro onde os clientes podem acessá-las facilmente.  

É recomendável usar o Configuration Manager com um esquema do Active Directory estendido ao gerenciar clientes locais. Um esquema estendido pode simplificar o processo de implantação e configuração de clientes. Um esquema estendido também permite que os clientes localizem com eficiência recursos como servidores de conteúdo e serviços adicionais, que fornecem diferentes funções do sistema de sites do Configuration Manager.  

-   Se você não estiver familiarizado com qual esquema estendido fornece uma implantação do Configuration Manager, leia [Extensões de esquema para o System Center Configuration Manager](../../../core/plan-design/network/schema-extensions.md) para ajudá-lo a tomar essa decisão.  

-   Quando você não usa um esquema estendido, pode configurar outros métodos, como DNS e WINS, para localizar servidores do sistema de sites e serviços. Esses métodos de localização de serviço necessitam configurações adicionais e não são o método que os clientes preferem para local do serviço. Para saber mais sobre isso, leia [Entender como os clientes encontram serviços e recursos do site para o System Center Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

-   Se o esquema do Active Directory tiver sido estendido para o Configuration Manager 2007 ou o System Center 2012 Configuration Manager, você não precisará fazer mais nada. As extensões de esquema permanecerão inalteradas e já estarão em vigor.  

Estender o esquema é uma ação única para qualquer floresta. Para estender e, em seguida, usar o esquema estendido do Active Directory, siga estas etapas:  

## <a name="step-1-extend-the-schema"></a>Etapa 1. Estender o esquema  
Para estender o esquema do Configuration Manager:  

-   Use uma conta que seja membro do grupo de segurança Administradores de Esquema.  

-   Esteja conectado ao controlador de domínio mestre do esquema.  

-   Execute a ferramenta **Extadsch.exe** ou use o utilitário de linha de comando LDIFDE com o arquivo **ConfigMgr_ad_schema.ldf** . A ferramenta e o arquivo estão na pasta **SMSSETUP\BIN\X64** na mídia de instalação do Configuration Manager.  

#### <a name="option-a-use-extadschexe"></a>Opção A: usar Extadsch.exe  

1.  Execute **extadsch.exe** para adicionar as novas classes e atributos ao esquema do Active Directory.  

    > [!TIP]  
    >  Execute essa ferramenta em uma linha de comando para exibir comentários enquanto ela é executada.  

2.  Verifique se a extensão do esquema foi realizada com sucesso analisando extadsch.log na raiz da unidade do sistema.  

#### <a name="option-b-use-the-ldif-file"></a>A opção B: usar o arquivo LDIF  

1.  Edite o arquivo **ConfigMgr_ad_schema.ldf** para definir o domínio raiz do Active Directory que deseja estender:  

    -   Substitua todas as instâncias do texto **DC=x** no arquivo pelo nome completo do domínio a estender.  

    -   Por exemplo, se o nome completo do domínio a ser estendido for widgets.microsoft.com, altere todas as instâncias de DC=x no arquivo para **DC=widgets, DC=microsoft, DC=com**.  

2.  Use o utilitário de linha de comando LDIFDE para importar o conteúdo do arquivo **ConfigMgr_ad_schema.ldf** para o Active Directory Domain Services:  

    -   Por exemplo, a seguinte linha de comando importará as extensões do esquema para o Active Directory Domain Services, ativará o registro em log detalhado e criará um arquivo de log durante o processo de importação: **ldifde -i -f ConfigMgr_ad_schema.ldf -v -j &lt;local para armazenar o arquivo de log\>**.  

3.  Para verificar se a extensão do esquema foi bem-sucedida, analise um arquivo de log criado pela linha de comando na etapa anterior.  

## <a name="step-2--create-the-system-management-container-and-grant-sites-permissions-to-the-container"></a>Etapa 2.  Criar contêiner do System Management e conceder permissões de sites para o contêiner  
 Depois de estender o esquema, você deve criar um repositório denominado **System Management** nos AD DS (Active Directory Domain Services):  

-   Crie esse contêiner uma vez em cada domínio que tenha um site primário ou secundário que publicará dados no Active Directory.  

-   Para cada contêiner, conceda permissões para a conta de computador de cada servidor de site primário e secundário que publicará dados nesse domínio. Cada conta deve ter **Controle Total** sobre o contêiner, com a permissão avançada **Aplicar em** igual a **Este objeto e todos os descendentes**.  

#### <a name="to-add-the-container"></a>Para adicionar o contêiner  

1.  Use uma conta que tenha a permissão **Criar Todos os Objetos Filho** no contêiner do **Sistema** nos Serviços de Domínio do Active Directory.  

2.  Execute o **Editor ADSI** (adsiedit.msc) e conecte-se ao domínio do servidor do site.  

3.  Crie o contêiner:  

    -   Expanda o &lt;nome de domínio totalmente qualificado do computador\> do **Domínio**, expanda o &lt;nome diferenciado\>, clique com o botão direito do mouse em **CN=System**, clique em **Novo** e em **Objeto**.  

    -   Na caixa de diálogo **Criar Objeto**, selecione **Contêiner** e clique em **Avançar**.  

    -   Na caixa **Valor**, digite **System Management** e clique em **Avançar**.  

4.  Atribuir permissões:  

    > [!NOTE]  
    >  se preferir, você pode usar outras ferramentas, como a ferramenta administrativa Computadores e Usuários do Active Directory (dsa.msc) para adicionar permissões ao contêiner.  

    -   Clique com o botão direito do mouse em **CN=System Management** e clique em **Propriedades**.  

    -   Selecione a guia **Segurança**, clique em **Adicionar** e, em seguida, adicione a conta de computador do servidor de sites com permissão **Controle Total**.  

    -   Clique em **Avançado**, selecione a conta de computador do servidor de sites e clique em **Editar**.  

    -   Na lista **Aplicar em**, selecione **Este objeto e todos os descendentes**.  

5.  Clique em **OK** para fechar o console e salvar a configuração.  

## <a name="step-3-set-up-sites-to-publish-to-active-directory-domain-services"></a>Etapa 3. Configurar sites para publicarem no Active Directory Domain Services  
 Depois que o repositório estiver configurado, as permissões tiverem sido concedidas e você tiver instalado um site primário do Configuration Manager, é possível configurar esse site para publicar dados no Active Directory.  

 Para saber mais sobre a publicação, veja [Publicar dados do site para o System Center Configuration Manager](../../../core/servers/deploy/configure/publish-site-data.md).  
