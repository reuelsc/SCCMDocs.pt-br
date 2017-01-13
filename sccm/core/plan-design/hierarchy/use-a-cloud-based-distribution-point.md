---
title: "Ponto de distribuição baseado em nuvem | Microsoft Docs"
description: "Saiba mais sobre as configurações e limitações para usar um ponto de distribuição baseado em nuvem com o System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
caps.latest.revision: 9
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 840f7be09f234d598bc7856d53e278665808fef1


---
# <a name="use-a-cloud-based-distribution-point-with-system-center-configuration-manager"></a>Use um ponto de distribuição baseado em nuvem com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Um ponto de distribuição baseado em nuvem é um ponto de distribuição do System Center Configuration Manager que é hospedado no Microsoft Azure. As informações a seguir têm o objetivo de ajudá-lo a saber mais sobre as configurações e limitações de uso de um ponto de distribuição baseado em nuvem.

Após ter instalado um site primário e quando estiver pronto para instalar um ponto de distribuição baseado em nuvem, consulte [Instalar pontos de distribuição baseados em nuvem no Microsoft Azure](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md).


## <a name="plan-to-use-a-cloud-based-distribution-point"></a>Planejar o uso de ponto de distribuição baseado em nuvem
Ao usar pontos de distribuição baseados em nuvem, você:  

-   **Define configurações do cliente** para permitir que usuários e dispositivos acessem o conteúdo  

-   **Especifica um site primário para gerenciar a transferência de conteúdo** ao ponto de distribuição  

-   **Especifica limites** para o volume de conteúdo que você deseja armazenar no ponto de distribuição e o volume de conteúdo que deseja permitir que os clientes transfiram do ponto de distribuição  


Com base nos limites configurados, o Configuration Manager pode acionar alertas que avisam quando o volume combinado de conteúdo que você armazenou no ponto de distribuição está próximo do volume de armazenamento especificado ou quando as transferências de dados pelos clientes estão próximas aos limites definidos.  

Pontos de distribuição com base em nuvem oferecem suporte aos seguintes recursos que também são compatíveis com os pontos de distribuição no local:  

-   Gerenciamento de pontos de distribuição com base em nuvem individualmente ou como membros de grupos de pontos de distribuição.  

-   Uso de um ponto de distribuição com base em nuvem como local de conteúdo de fallback.  

-   Recebimento de suporte para clientes baseados na Internet e em intranet.  


Um ponto de distribuição com base em nuvem oferece os seguintes benefícios adicionais:  

-   O conteúdo enviado para o ponto de distribuição baseado em nuvem é criptografado pelo Configuration Manager antes de o Configuration Manager enviá-o para o Microsoft Azure.  

-   No Microsoft Azure, é possível dimensionar manualmente o serviço de nuvem para atender às demandas em constante mudança por solicitação de conteúdo pelos clientes, sem a necessidade de instalar e provisionar pontos de distribuição adicionais.  

-   O ponto de distribuição com base em nuvem oferece suporte para o download de conteúdo por clientes configurados para o Windows BranchCache.  


Os pontos de distribuição baseados em nuvem têm as seguintes limitações:  

-   Você não pode usar um ponto de distribuição com base na nuvem para hospedar pacotes de atualização de software.  

-   Você não pode usar um ponto de distribuição com base em nuvem para PXE ou implantações habilitadas para multicast.  

-   Não é oferecido um ponto de distribuição baseado em nuvem aos clientes como local de conteúdo para uma sequência de tarefas implantada usando a opção de implantação **Baixar conteúdo localmente quando necessário, executando a sequência de tarefas**. No entanto, as sequências de tarefas implantadas com a opção de implantação **Baixar todo o conteúdo localmente antes de iniciar a sequência de tarefas** podem usar um ponto de distribuição baseado em nuvem como um local de conteúdo válido.  

-   Não oferecem suporte a pacotes executados no ponto de distribuição. Todo o conteúdo deve ser baixado pelo cliente e, em seguida, executado localmente.  

-   Não oferecem suporte a aplicativos de streaming usando o Application Virtualization ou programas semelhantes.  

-   Não oferecem suporte a conteúdo pré-configurado. O Gerenciador de Distribuição do site primário que gerencia o ponto de distribuição transfere todo o conteúdo para o ponto de distribuição.  

-   Não podem ser configurados como pontos de distribuição de recepção.  

##  <a name="a-namebkmkprereqsclouddpa-prerequisites-for-cloud-based-distribution-points"></a><a name="BKMK_PrereqsCloudDP"></a> Pré-requisitos para pontos de distribuição baseados em nuvem  
 Estes são os pré-requisitos para o uso de pontos de distribuição baseados em nuvem:  

-   Uma assinatura do Microsoft Azure.  (Consulte, [Sobre assinaturas e certificados](#BKMK_CloudDPCerts) neste tópico)

-   Um certificado de gerenciamento autoassinado ou PKI para a comunicação de um servidor do site primário do Configuration Manager para o serviço de nuvem no Microsoft Azure.  (Consulte, [Sobre assinaturas e certificados](#BKMK_CloudDPCerts) neste tópico)

-   Um certificado de serviço (PKI) que os clientes do Configuration Manager usam para se conectar a pontos de distribuição baseados em nuvem e baixar conteúdo usando HTTPS.  

-   Para acessar conteúdo de um ponto de distribuição baseado em nuvem, um dispositivo ou usuário deve receber a configuração de cliente de **Serviços de Nuvem** em **Permitir acesso aos pontos de distribuição na nuvem** definida como **Sim**. Por padrão, esse valor é definido como **Não**.  

-   Os clientes devem ser capazes de resolver o nome do serviço de nuvem, que requer um alias DNS (Sistema de Nomes de Domínio), um registro CNAME, no seu namespace DNS.  

-   Os clientes devem ser capazes de acessar a Internet para usar o ponto de distribuição baseado em nuvem.  

##  <a name="a-namebkmkclouddpcosta-cost-of-using-cloud-based-distribution"></a><a name="BKMK_CloudDPCost"></a> Custo da utilização de uma distribuição baseada em nuvem  
 Quando você usa um ponto de distribuição baseado em nuvem, planeje o custo de armazenamento de dados e das transferências de download que os clientes do Configuration Manager executarão.  

 O Configuration Manager inclui opções para ajudar a controlar os custos e monitorar o acesso a dados:  

-   Você pode controlar e monitorar a quantidade de conteúdo armazenado em um serviço de nuvem.  

-   Você pode configurar o Configuration Manager para alertá-lo quando os **limites** para downloads do cliente atingirem ou excederem o limite mensal.  

-   Além disso, você pode usar o cache de sistemas pares (BranchCache) para ajudar a reduzir o número de transferências de dados de pontos de distribuição baseados em nuvem por clientes. Por padrão, os clientes do Configuration Manager configurados para o Windows BranchCache podem transferir conteúdo usando pontos de distribuição baseados em nuvem.  


**Opções:**  

-   **Configurações do Cliente para Nuvem**: você controla o acesso a todos os pontos de distribuição baseados em nuvem em uma hierarquia usando as **Configurações do Cliente**.  

     Nas **Configurações do Cliente**, a categoria **Configurações de Nuvem** dá suporte à configuração **Permitir acesso aos pontos de distribuição na nuvem**. Por padrão, essa configuração é definida como **Não**. Você pode habilitar essa configuração para usuários e dispositivos.  

-   **Limites para transferências de dados**: é possível configurar limites para o volume de dados que você deseja armazenar no ponto de distribuição e para o volume de dados que os clientes baixam do ponto de distribuição.  

     Os limites para pontos de distribuição baseados em nuvem incluem:  

    -   **Limite de alerta de armazenamento**: Um limite de alerta de armazenamento define um limite superior no volume de dados ou conteúdo que você deseja armazenar no ponto de distribuição baseado em nuvem. É possível especificar o Configuration Manager para gerar um alerta de aviso quando o espaço livre restante de seu limite de alerta de armazenamento atingir o nível especificado.  

    -   **Limite de alerta de transferência**: Um limite de alerta de transferência ajuda a monitorar o volume de conteúdo que você transfere do ponto de distribuição para clientes num período de 30 dias. O limite de alerta de transferência monitora a transferência de dados dos últimos 30 dias, e pode emitir um alerta de aviso e um crítico quando as transferências atingem os valores definidos.  

        > [!IMPORTANT]  
        >  O Configuration Manager monitora a transferência de dados, mas não interrompe a transferência de dados que está além do limite de alerta de transferência especificado.  

 Você pode especificar limites para cada ponto de distribuição baseado em nuvem durante a instalação do ponto de distribuição, ou pode editar as propriedades de cada ponto de distribuição baseado em nuvem após ele ser instalado.  

-   **Alertas**: é possível configurar o Configuration Manager para emitir alertas sobre transferências bidirecionais de dados em cada ponto de distribuição baseado em nuvem, de acordo com os limites de transferência de dados que você especificar. Esses alertas servem como auxílio no monitoramento de transferências de dados e podem ajudar a decidir quando parar o serviço de nuvem a fim de evitar seu uso, quando ajustar o conteúdo armazenado no ponto de distribuição ou modificar quais clientes podem usar os pontos de distribuição baseados em nuvem.  

     Em um ciclo por hora, o site primário que monitora o ponto de distribuição baseado em nuvem baixa dados de transação do Microsoft Azure e os armazena em CloudDP-&lt;ServiceName\>.log no servidor do site. O Configuration Manager avalia estas informações em relação às cotas de armazenamento e transferência para cada ponto de distribuição baseado em nuvem. Quando a transferência de dados atingir ou exceder o volume especificado para alertas de aviso ou críticos, o Configuration Manager gerará o alerta apropriado.  

    > [!WARNING]  
    >  Como as informações sobre transferências de dados são baixadas do Microsoft Azure a cada hora, esse uso de dados pode exceder um limite de aviso ou crítico antes que o Configuration Manager possa acessar os dados e emitir um alerta.  

    > [!NOTE]  
    >  Os alertas de um ponto de distribuição baseado em nuvem dependem de estatísticas de uso do Windows Azure, e podem levar 24 horas para ficar disponíveis. Para obter informações sobre Análise de Armazenamento do Windows Azure, inclusive com que frequência o Windows Azure atualiza as estatísticas de uso, consulte [Análise de Armazenamento](http://go.microsoft.com/fwlink/p/?LinkID=275111) na Biblioteca MSDN.  


-   **Interromper ou iniciar o serviço de nuvem sob demanda**: é possível usar a opção de interromper ou iniciar o serviço de nuvem a qualquer momento, a fim de evitar que clientes usem o serviço continuamente. Quando você interrompe o serviço de nuvem, os clientes imediatamente são impedidos de baixar conteúdo adicional do serviço. Além disso, você pode reiniciar o serviço de nuvem para restaurar o acesso para clientes. Por exemplo, talvez você queira parar um serviço de nuvem quando os limites de dados são atingidos.  

     Quando você para um serviço de nuvem, ele não exclui o conteúdo do ponto de distribuição e não impede que o servidor de site transfira conteúdo adicional para o ponto de distribuição baseado em nuvem.  

     Para interromper um serviço de nuvem, no console do Configuration Manager, selecione o ponto de distribuição no nó **Pontos de Distribuição em Nuvem**, em **Serviços em Nuvem**, no espaço de trabalho **Administração**. Em seguida, clique em **Parar serviço** para interromper o serviço de nuvem que executa no Windows Azure.  

##  <a name="a-namebkmkclouddpcertsa-about-subscriptions-and-certificates-for-cloud-based-distribution-points"></a><a name="BKMK_CloudDPCerts"></a> Sobre assinaturas e certificados para pontos de distribuição baseados em nuvem  
 Pontos de distribuição baseados em nuvem requerem certificados para habilitar o Configuration Manager a gerenciar o serviço de nuvem que hospeda o ponto de distribuição, e para os clientes acessarem o conteúdo do ponto de distribuição. Veja a seguir uma visão geral desses certificados. Para obter informações mais detalhadas, consulte [Requisitos de certificado PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

 **Certificados**  

-   **Certificado de gerenciamento para comunicação do servidor do site com o ponto de distribuição**: o certificado de gerenciamento estabelece uma relação de confiança entre a API de gerenciamento do Microsoft Azure e o Configuration Manager. Esta autenticação permite que o Configuration Manager chame a API do Microsoft Azure quando você executa tarefas como implantação de conteúdo ou inicialização e interrupção do serviço de nuvem. Usando o Microsoft Azure, os clientes podem criar seus próprios certificados de gerenciamento, que podem ser um certificado autoassinado ou outro emitido por uma AC (autoridade de certificação):  

    -   Forneça o arquivo .cer do certificado de gerenciamento para o Microsoft Azure ao configurar o Microsoft Azure para o Configuration Manager. O arquivo. cer contém a chave pública do certificado de gerenciamento. Você deve carregar este certificado no Microsoft Azure antes de instalar um ponto de distribuição baseado em nuvem. Este certificado permite que o Configuration Manager acesse a API do Microsoft Azure.  

    -   Forneça o arquivo .pfx do certificado de gerenciamento ao Configuration Manager ao instalar um ponto de distribuição baseado em nuvem. O arquivo .pfx contém a chave privada do certificado de gerenciamento. O Configuration Manager armazena este certificado no banco de dados do site. Como o arquivo .pfx contém a chave privada, você deve fornecer a senha para importar esse arquivo de certificado para o banco de dados do Configuration Manager.  

    Se você criar um certificado autoassinado, primeiro deverá exportar o certificado como um arquivo .cer e depois exportá-lo novamente como um arquivo .pfx.  

    Opcionalmente, é possível especificar um arquivo **.publishsettings** de versão 1 do Microsoft Azure SDK 1.7. Para obter mais informações sobre arquivos .publishsettings, veja a documentação do Microsoft Azure.  

    Para obter mais informações, veja [Como criar um certificado de gerenciamento](http://go.microsoft.com/fwlink/p/?LinkId=220281) e [Como adicionar um certificado de gerenciamento a uma assinatura do Microsoft Azure](http://go.microsoft.com/fwlink/p/?LinkId=241722) na seção Plataforma Microsoft Azure da Biblioteca MSDN.  

-   **Certificado de serviço para comunicação do cliente com o ponto de distribuição**: o certificado de serviço do ponto de distribuição baseado em nuvem do Configuration Manager estabelece uma relação de confiança entre os clientes do Configuration Manager e esse ponto de distribuição, além de proteger os dados que os clientes baixam dele usando SSL por HTTPS.  

    > [!IMPORTANT]  
    >  O nome comum indicado na caixa de entidade do certificado de serviço deve ser exclusivo no seu domínio e não deve corresponder a nenhum dispositivo ingressado no domínio.  

   Para ver um exemplo de implantação deste certificado, consulte a seção *Implantando o certificado de serviço em pontos de distribuição baseados em nuvem* no tópico [Exemplo de implantação passo a passo dos certificados PKI para o System Center Configuration Manager: Autoridade de Certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="a-namebkmktasksa-common-management-tasks-for-cloud-based-distribution-points"></a><a name="bkmk_Tasks"></a> Tarefas comuns de gerenciamento para pontos de distribuição baseados em nuvem  

-   **Comunicação do servidor do site com o ponto de distribuição baseado em nuvem**: quando instalar um ponto de distribuição baseado em nuvem, atribua um site primário para gerenciar a transferência de conteúdo para o serviço de nuvem. Essa ação equivale a instalar a função do sistema de site do ponto de distribuição em um site específico.  

-   **Comunicação do cliente com o ponto de distribuição baseado em nuvem**: quando um dispositivo ou o usuário de um dispositivo estiver configurado com a opção de cliente que permite o uso de um ponto de distribuição baseado em nuvem, ele poderá receber esse ponto de distribuição como um local de conteúdo válido:  

    -   Um ponto de distribuição baseado em nuvem é considerado um ponto de distribuição remoto quando um cliente avalia os locais de conteúdo disponíveis  

    -   Clientes na intranet somente usarão pontos de distribuição baseados em nuvem como uma opção de fallback se os pontos de distribuição local de distribuição não estiverem disponíveis  

    Mesmo que você instale pontos de distribuição baseados em nuvem em regiões específicas do Microsoft Azure, os clientes que usam pontos de distribuição baseados em nuvem não reconhecem as regiões do Microsoft Azure e selecionam de forma não determinística um ponto de distribuição baseado em nuvem. Isso significa que, se você instalar pontos de distribuição baseados em nuvem em várias regiões, e um cliente receber vários pontos de distribuição baseados em nuvem como locais de conteúdo, ele não poderá usar um ponto de distribuição baseado em nuvem de uma região do Microsoft Azure igual à dele.  

    Clientes que podem usar pontos de distribuição baseados em nuvem usam a sequência a seguir para solicitações de localização de conteúdo  

    1.  Um cliente configurado para usar pontos de distribuição baseados em nuvem sempre tentará obter o conteúdo de um ponto de distribuição preferencial primeiro.  

    2.  Quando um ponto de distribuição preferencial não estiver disponível, o cliente utilizará um ponto de distribuição remoto, se a implantação oferecer suporte a essa opção e se houver um ponto de distribuição remoto disponível.  

    3.  Quando um ponto de distribuição preferencial ou remoto não está disponível, o cliente pode, então, retornar para obter o conteúdo de um ponto de distribuição baseado em nuvem.  

        > [!NOTE]  
        >  Clientes na Internet que recebem a um ponto de distribuição baseado na Internet e um ponto de distribuição baseado em nuvem como locais de conteúdo para uma implantação, só tentam recuperar conteúdo do ponto de distribuição baseado na Internet. Se o cliente na Internet não recuperar o conteúdo do ponto de distribuição baseado na Internet, ele não tentará acessar o ponto de distribuição baseado em nuvem.  


  Quando um cliente usa um ponto de distribuição baseado em nuvem como um local de conteúdo, ele se autentica para esse ponto de distribuição usando o token de acesso ao Configuration Manager. Se o cliente confiar no certificado do ponto de distribuição baseado em nuvem do Configuration Manager, ele poderá baixar o conteúdo solicitado.  

-   **Monitorar pontos de distribuição baseados em nuvem**: é possível monitorar o conteúdo que você implanta em cada ponto de distribuição baseado em nuvem, bem como monitorar o serviço de nuvem que hospeda o ponto de distribuição.  

    -   **Conteúdo**: você monitora o conteúdo que implanta em um ponto de distribuição baseado em nuvem da mesma maneira que implanta conteúdo em pontos de distribuição locais.  

    -   **Serviço de nuvem**: o Configuration Manager verificará periodicamente o serviço do Microsoft Azure e emitirá um alerta se o serviço não estiver ativo ou se houver problemas de assinatura ou de certificado. Também é possível ver detalhes sobre o ponto de distribuição no nó **Pontos de Distribuição de Nuvem** em **Serviços de Nuvem** no espaço de trabalho **Administração** do console do Configuration Manager. Desse local, você exibe informações de alto nível sobre o ponto de distribuição, ou seleciona um ponto de distribuição e então edita suas **Propriedades**.  

    Quando você edita as propriedades de um ponto de distribuição baseado em nuvem, você pode:  

    -   Ajustar os limites de dados para armazenamento e alertas  

    -   Gerenciar conteúdo como faria em um ponto de distribuição local  

    Finalmente, para cada ponto de distribuição baseado em nuvem, é possível exibir, mas não editar, a ID da assinatura, o nome de serviço e outros detalhes relacionados que são especificados quando a distribuição baseada em nuvem é instalada.  

-   **Backup e recuperação de pontos de distribuição baseados em nuvem**: quando usar um ponto de distribuição baseado em nuvem em sua hierarquia, use as informações a seguir como auxílio para fazer backup ou recuperar o ponto de distribuição:  

    -   Quando você utiliza a tarefa de manutenção predefinida **Servidor do Site de Backup**, o Configuration Manager inclui automaticamente as configurações do ponto de distribuição baseado em nuvem.  

    -   É prática recomendada fazer backup e salvar uma cópia dos certificados de gerenciamento e de serviço em uso com um ponto de distribuição baseado em nuvem. No caso de restaurar o site primário do Configuration Manager que gerencia o ponto de distribuição baseado em nuvem para um computador diferente, reimporte os certificados para continuar a usá-los.  

-   **Desinstalar um ponto de distribuição baseado em nuvem**: para desinstalar um ponto de distribuição baseado em nuvem, selecione o ponto de distribuição no console do Configuration Manager e selecione **Excluir**.  

    Quando um ponto de distribuição baseado em nuvem é excluído de uma hierarquia, o Configuration Manager remove o conteúdo do serviço de nuvem no Microsoft Azure.  



<!--HONumber=Dec16_HO3-->


