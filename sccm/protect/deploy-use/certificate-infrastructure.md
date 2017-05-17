---
title: "Configuração de infraestrutura de certificado | Microsoft Docs"
description: Saiba como configurar registro de certificado no System Center Configuration Manager.
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 29ae59b7-2695-4a0f-a9ff-4f29222f28b3
caps.latest.revision: 7
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 859a8da10f55e314b205b7a4a415a1d2a60a920a
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017

---

# <a name="certificate-infrastructure"></a>Infraestrutura de certificado

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Aqui estão as etapas, detalhes e mais informações sobre como configurar certificados no System Center Configuration Manager. Antes de começar, verifique quais são os pré-requisitos relacionados em [Pré-requisitos dos perfis de certificado no System Center Configuration Manager](../../protect/plan-design/prerequisites-for-certificate-profiles.md).  

Use estas etapas para configurar sua infraestrutura para certificados SCEP ou PFX.

## <a name="step-1---install-and-configure-the-network-device-enrollment-service-and-dependencies-for-scep-certificates-only"></a>Etapa 1: Instalar e configurar o Serviço de Registro de Dispositivo de Rede e dependências (apenas para certificados SCEP)

 Você deve instalar e configurar o serviço da função do Serviço de Registro de Dispositivo de Rede para os Serviços de Certificados do Active Directory (AD CS), alterar as permissões de segurança nos modelos de certificado, implantar um certificado de autenticação de cliente da infraestrutura de chave pública (PKI) e editar o registro para aumentar o tamanho limite da URL padrão dos Serviços de Informações da Internet (IIS). Se necessário, você também deve configurar a AC (autoridade de certificação) emissora para permitir um período de validade personalizado.  

> [!IMPORTANT]  
>  Antes de configurar o System Center Configuration Manager para trabalhar com o Serviço de Registro de Dispositivo de Rede, verifique a instalação e a configuração do Serviço de Registro de Dispositivo de Rede. Se essas dependências não estiverem funcionando corretamente, você terá problemas ao solucionar problemas de registro de certificado usando o System Center Configuration Manager.  

### <a name="to-install-and-configure-the-network-device-enrollment-service-and-dependencies"></a>Para instalar e configurar o Serviço de Registro de Dispositivo de Rede e as dependências  

1.  Em um servidor que está executando o Windows Server 2012 R2, instale e configure o serviço de função Serviço de Registro de Dispositivo de Rede para a função de servidor Serviços de Certificados do Active Directory. Para mais informações, consulte [Diretrizes do Serviço de Registro de Dispositivo de Rede](http://go.microsoft.com/fwlink/p/?LinkId=309016) na biblioteca de Serviços de Certificados do Active Directory no TechNet.  

2.  Verifique e, se necessário, modifique as permissões de segurança dos modelos de certificado que o Serviço de Registro de Dispositivo de Rede está usando:  

    -   Para a conta que executa o console do System Center Configuration Manager: permissão de **leitura**.  

         Essa permissão é necessária para que, quando executar o Assistente para Criar Perfil de Certificado, você possa procurar pelo modelo de certificado que deseja utilizar e selecioná-lo ao criar um perfil de configurações do SCEP. Selecionar um modelo de certificado significa que algumas configurações do assistente são preenchidas automaticamente, de forma que você tenha menos configurações para definir e de que haja menos risco de selecionar configurações não compatíveis com os modelos de certificado que o Serviço de Registro de Dispositivo de Rede está usando.  

    -   Para a conta de serviço do SCEP que o pool de aplicativos do Serviço de Registro de Dispositivo de Rede usa: permissões **Ler** e **Registrar** .  

         Este requisito não é específico para o System Center Configuration Manager, mas faz parte da configuração do Serviço de Registro de Dispositivo de Rede. Para mais informações, consulte [Diretrizes do Serviço de Registro de Dispositivo de Rede](http://go.microsoft.com/fwlink/p/?LinkId=309016) na biblioteca de Serviços de Certificados do Active Directory no TechNet.  

    > [!TIP]  
    >  Para identificar quais modelos de certificado o Serviço de Registro de Dispositivo de Rede está usando, exiba a seguinte chave do Registro no servidor que está executando o Serviço de Registro de Dispositivo de Rede: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP.  

    > [!NOTE]  
    >  Essas são as permissões de segurança padrão adequadas para a maioria dos ambientes. No entanto, você pode usar uma configuração de segurança alternativa. Para obter mais informações, consulte [Planejando permissões de modelo de certificado para os perfis de certificado no System Center Configuration Manager](../../protect/plan-design/planning-for-certificate-template-permissions.md).  

3.  Implante um certificado PKI neste servidor que ofereça suporte à autenticação de clientes. Talvez você já tenha um certificado apropriado instalado no computador que possa usar, ou talvez tenha que (ou ainda prefira) implantar um certificado especificamente para este propósito. Para obter mais informações sobre os requisitos desse certificado, consulte os detalhes para Servidores que executam o Módulo de Política do Configuration Manager com o serviço de função Serviço de Registro de Dispositivo de Rede na seção **Certificados PKI para servidores** no tópico [Requisitos de certificado PKI para o System Center Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md).  

    > [!TIP]  
    >  Se precisar de ajuda para implantar esse certificado, será possível usar as instruções para [Implantando o certificado do cliente para pontos de distribuição](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012), porque os requisitos de certificado são os mesmos, porém com uma exceção:  
    >   
    >  -   Não selecione a caixa de seleção **Permitir que a chave particular seja exportada** na guia **Tratamento de solicitação** das propriedades do modelo de certificado.  
    >   
    >  Não é necessário exportar este certificado com a chave privada, porque você poderá navegar até o repositório do Computador local e selecioná-lo ao configurar o Módulo de Política do System Center Configuration Manager.  

4.  Localize o certificado raiz ao qual o certificado de autenticação de cliente se encadeia. Em seguida, exporte esse certificado da AC raiz para um arquivo de certificado (.cer). Salve esse arquivo em local seguro de onde possa acessá-lo mais tarde quando for instalar e configurar o servidor de sistema para o ponto de registro de certificado.  

5.  No mesmo servidor, use o editor do Registro para aumentar o limite de tamanho da URL padrão para o IIS, definindo os seguintes valores de DWORD da chave do Registro em HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\HTTP\Parameters:  

    -   Defina a chave **MaxFieldLength** como **65534**.  

    -   Defina a chave **MaxRequestBytes** como **16777216**.  

     Para obter mais informações, leia o artigo [820129: Configurações de Registro Http.sys para Windows](http://go.microsoft.com/fwlink/?LinkId=309013) na Base de Dados de Conhecimento Microsoft.  

6.  No mesmo servidor, no Gerenciador do IIS (Serviços de Informações da Internet), modifique as configurações de filtragem de solicitação do aplicativo /certsrv/mscep e reinicie o servidor. Na caixa de diálogo **Editar Configurações de Filtragem de Solicitações** , as configurações de **Limites de Solicitações** devem ser as seguintes:  

    -   **Tamanho máximo de conteúdo permitido (Bytes)**: **30000000**  

    -   **Tamanho máximo da URL (Bytes)**: **65534**  

    -   **Cadeia de caracteres de consulta máxima (Bytes)**: **65534**  

     Para obter mais informações sobre estas configurações e sobre como defini-las, consulte [Limites de solicitações](http://go.microsoft.com/fwlink/?LinkId=309014) na Biblioteca de Referência do IIS.  

7.  Se deseja poder solicitar um certificado com um período de validade inferior ao do modelo do certificado que está utilizando: Por padrão, essa configuração é desabilitada para uma AC corporativa. Para habilitar essa opção em uma AC corporativa, use a ferramenta de linha de comando Certutil, pare e reinicie o serviço de certificado usando os comandos a seguir:  

    1.  **certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE**  

    2.  **net stop certsvc**  

    3.  **net start certsvc**  

     Para mais informações, consulte [Configurações e Ferramentas dos Serviços de Certificados](http://go.microsoft.com/fwlink/p/?LinkId=309015) na biblioteca de Tecnologias PKI no TechNet.  

8.  Verifique se o Serviço de Registro de Dispositivo de Rede está funcionando usando o seguinte link como exemplo: **https://server.contoso.com/certsrv/mscep/mscep.dll**. Você deverá ver a página da Web interna do Serviço de Registro de Dispositivo de Rede. Esta página da Web explica sobre o que é o serviço e explica que os dispositivos de rede usam a URL para submeterem os pedidos de certificado.  

 Agora que o Serviço de Registro de Dispositivo de Rede e as dependências estão configuradas, você está pronto para instalar e configurar o ponto de registro de certificado.


## <a name="step-2---install-and-configure-the-certificate-registration-point"></a>Etapa 2: instalar e configurar o ponto de registro de certificado.

É necessário instalar e configurar pelo menos um ponto de registro de certificado na hierarquia do System Center Configuration Manager e é possível instalar esta função do sistema de sites no site da administração central ou em um site primário.  

> [!IMPORTANT]  
>  Antes de instalar o ponto de registro de certificado, consulte a seção **Requisitos de Sistema do Site** no tópico [Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md) para os requisitos de sistema operacional e as dependências para ponto de registro de certificado.  

##### <a name="to-install-and-configure-the-certificate-registration-point"></a>Para instalar e configurar o ponto de registro de certificado  

1.  No console do System Center Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Configuração de Site**, clique em **Funções de Servidores e Sistema de Site**e selecione o servidor a ser usado para o ponto de registro do certificado.  

3.  Na guia **Início** , no grupo **Servidor** , clique em **Adicionar Funções do Sistema de Site**.  

4.  Na página **Geral** , especifique as configurações gerais para o sistema de site e clique em **Próximo**.  

5.  Na página **Proxy** , clique em **Avançar**. O ponto de registro de certificado não usa as configurações de proxy da internet.  

6.  Na página **Seleção de Função do Sistema** , selecione **Ponto de Registro de Certificado** na lista de funções disponíveis e clique em **Avançar**. 

8. Na página **Modo de registro de certificado**, selecione se deseja que este registro de certificado aponte para **Processar solicitações de certificado SCEP** ou **Processar solicitações de certificado PFX**. Um ponto de registro de certificado não pode processar os dois tipos de solicitações, mas você pode criar vários pontos de registro de certificado se estiver trabalhando com os dois tipos de certificado.

7.  Na página **Configurações de ponto de registro de certificado**, as configurações feitas dependem do tipo de certificado que o ponto de registro de certificado processará:
    -   Se você selecionou **Processar solicitações de certificado SCEP**, configure o seguinte:
        -   **Nome do site**, **Número da Porta HTTPS** e **Nome do aplicativo Virtual** para o ponto de registro de certificado. Esses campos são preenchidos automaticamente com valores padrão. 
        -   **URL para o serviço de registro do dispositivo de rede e certificado de Autoridade de Certificação raiz** -clique em **Adicionar**, em seguida, na caixa de diálogo **Adicionar URL e certificado de AC raiz**, especifique o seguinte:
            - **URL do Serviço de Registro de Dispositivo de Rede**: especifique a URL no seguinte formato: https://*<server_FQDN>*/certsrv/mscep/mscep.dll. Por exemplo, se o FQDN do servidor que está executando o Serviço de Registro de Dispositivo de Rede for server1.contoso.com, digite **https://server1.contoso.com/certsrv/mscep/mscep.dll**.
            - **Certificado de AC Raiz**: Navegue até e selecione o arquivo de certificado (.cer) criado e salvo na **Etapa 1: Instale e configure o Serviço de Registro de Dispositivo de Rede e dependências**. Este certificado de AC raiz permite que o ponto de registro de certificado valide o certificado de autenticação de cliente que o Módulo de Política do System Center Configuration Manager usará.  
    - Se você selecionou **Processar solicitações de certificado PFX**, configure o seguinte:
        - **Autoridades de Certificação (AC) e a conta precisam se conectar a cada autoridade de certificação** - clique em **Adicionar**, em seguida, na caixa de diálogo **Adicionar uma Autoridade de Certificação e uma Conta**, especifique o seguinte:
            - **Nome do servidor da autoridade de certificado** - insira o nome do seu servidor de autoridade de certificado.
            - **Conta da Autoridade de Certificado** - clique em **Definir** para selecionar ou crie a conta que tem permissões para se inscrever em modelos na autoridade de certificação.
        - **Conta de Conexão do Ponto de Registro de Certificado** - seleciona ou conecta a conta que conecta o ponto de registro do certificado ao banco de dados do Configuration Manager. Como alternativa, você pode usar a conta de computador local do computador que hospeda o ponto de registro de certificado.
        - **Conta de Publicação de Certificado do Active Directory** - selecione uma conta ou crie uma nova conta que será usada para publicar certificados para objetos de usuário no Active Directory.
8.  Na caixa de diálogo **Adicionar URL e Certificado da AC Raiz** , especifique o seguinte e clique em **OK**:  

9. Clique em **Próximo** e conclua o assistente.  

10. Espere alguns minutos até que a instalação seja finalizada e verifique se o ponto de registro de certificado foi instalado com êxito, usando qualquer um dos métodos a seguir:  

    -   No espaço de trabalho **Monitoramento** , expanda **Status do Sistema**, clique em **Status do Componente**e procure pelas mensagens de status do componente **SMS_CERTIFICATE_REGISTRATION_POINT** .  

    -   No servidor do sistema de sites, use o arquivo *<ConfigMgr Installation Path\>*\Logs\crpsetup.log e o arquivo *<ConfigMgr Installation Path\>*\Logs\crpmsi.log. Uma instalação bem-sucedida retornará um código de saída igual a 0.  

    -   Usando um navegador, verifique se é possível se conectar à URL do ponto de registro de certificado, por exemplo, https://server1.contoso.com/CMCertificateRegistration. Uma página de **Erro do Servidor** será exibida para o nome do aplicativo com uma descrição HTTP 404.  

11. Localize o arquivo de certificado exportado para a AC raiz que o ponto de registro de certificado criou automaticamente na seguinte pasta no computador do servidor do site primário: *<ConfigMgr Installation Path\>*\inboxes\certmgr.box. Salve este arquivo em um local seguro em que você possa acessá-lo mais tarde quando for instalar o Módulo de Política do System Center Configuration Manager no servidor que está executando o Serviço de Registro de Dispositivo de Rede.  

    > [!TIP]  
    >  Este certificado não está imediatamente disponível nessa pasta. Talvez você precise esperar um pouco (por exemplo, meia hora) até que o System Center Configuration Manager copie o arquivo para este local.  


## <a name="step-3----install-the-system-center-configuration-manager-policy-module-for-scep-certificates-only"></a>Etapa 3: instalar o Módulo de Política do System Center Configuration Manager (somente para certificados SCEP).

É necessário instalar e configurar o Módulo de Política do System Center Configuration Manager em cada servidor especificado na **Etapa 2: instalar e configurar o ponto de registro de certificado** como uma **URL para o Serviço de Registro de Dispositivo de Rede** nas propriedades do ponto de registro de certificado.  

##### <a name="to-install-the-policy-module"></a>Para instalar o Módulo de Política  

1.  No servidor que executa o Serviço de Registro de Dispositivo de Rede, faça logon como administrador de domínio e copie os seguintes arquivos da pasta <ConfigMgrInstallationMedia\>\SMSSETUP\POLICYMODULE\X64 na mídia de instalação do System Center Configuration Manager em uma pasta temporária:  

    -   PolicyModule.msi  

    -   PolicyModuleSetup.exe  

    Além disso, se você possuir uma pasta LanguagePack na mídia de instalação, copie essa pasta e todo o seu conteúdo.  

2.  Na pasta temporária, execute PolicyModuleSetup.exe para iniciar o Assistente de Instalação do Módulo de Política do System Center Configuration Manager.  

3.  Na página inicial do assistente, clique em **Avançar**, aceite os temos da licença e clique em **Avançar**.  

4.  Na página **Pasta de Instalação** , aceite a pasta de instalação padrão do módulo de política ou especifique uma pasta alternativa e clique em **Avançar**.  

5.  Na página **Ponto de Registro de Certificado** , especifique a URL do ponto de registro de certificado usando o FQDN do servidor de sistema do site e o nome do aplicativo virtual especificado nas propriedades do ponto de registro de certificado. O nome padrão do aplicativo virtual é CMCertificateRegistration. Por exemplo, se o servidor de sistema do site tiver um FQDN igual a server1.contoso.com e você usou o nome padrão do aplicativo virtual, especifique **https://server1.contoso.com/CMCertificateRegistration**.  

6.  Aceite a porta padrão **443** ou especifique o número alternativo de porta que o ponto de registro de certificado está utilizando e clique em **Avançar**.  

7.  Na página **Certificado do Cliente para o Módulo de Política**, navegue até e especifique o certificado de autenticação de cliente implantado na **Etapa 1: Instale e configure o Serviço de Registro de Dispositivo de Rede e dependências**e clique em **Próximo**.  

8.  Na página **Certificado do Ponto de Registro de Certificado** , clique em **Procurar** para selecionar o arquivo de certificado exportado para a AC raiz localizado e salvo ao final da **Etapa 2: Instale e configure o ponto de registro de certificado**.  

    > [!NOTE]  
    >  Se você não salvou este arquivo de certificado anteriormente, ele estará localizado em <ConfigMgr Installation Path\>\inboxes\certmgr.box no computador do servidor do site.  

9. Clique em **Próximo** e conclua o assistente.  

 Se você desejar desinstalar o Módulo de Política do System Center Configuration Manager, use **Programas e Recursos** no Painel de Controle. 

 
Agora que você concluiu as etapas de configuração, está pronto para implantar certificados para usuários e dispositivos criando e implantando os perfis de certificado. Para obter mais informações sobre como criar perfis de certificado, consulte [Como criar perfis de certificado no System Center Configuration Manager](../../protect/deploy-use/create-certificate-profiles.md).  

