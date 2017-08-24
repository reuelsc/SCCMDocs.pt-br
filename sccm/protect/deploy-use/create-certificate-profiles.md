---
title: Como criar perfis de certificado SCEP | Microsoft Docs
description: "Saiba como usar perfis de certificado para provisionar dispositivos gerenciados com os certificados necessários no System Center Configuration Manager."
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 634d612c-92d7-4c03-873a-b2e730c9a72d
caps.latest.revision: "16"
caps.handback.revision: "0"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 1e00804d27ecef2aadd8bfa395db1919c46243ee
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="create-certificate-profiles"></a>Criar perfis de certificado

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Use perfis de certificado no SCCM (Configuration Manager) para provisionar dispositivos gerenciados com os certificados necessários para acessar recursos da empresa. Antes de criar perfis de certificado, defina a infraestrutura do certificado conforme descrito em [Configurar a infraestrutura de certificados para o System Center Configuration Manager](certificate-infrastructure.md).  

Este tópico descreve como criar perfis de certificado SCEP e de raiz confiável. Se você quiser criar perfis de certificado PFX, consulte [Criar perfis de certificado PFX](../../protect/deploy-use/create-pfx-certificate-profiles.md).

Para criar um perfil de certificado:

1.  Inicie o Assistente para Criar Perfil de Certificado.
1.  Forneça informações gerais sobre o perfil de certificado.
1.  Configure um certificado de AC (autoridade de certificado) confiável.  
1.  Configure as informações de certificado SCEP (somente para certificados SCEP).  
1.  Especifique as plataformas com suporte para o perfil de certificado.


## <a name="start-the-create-certificate-profile-wizard"></a>Iniciar o Assistente para Criar Perfil de Certificado  

1.  No console do System Center Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , expanda **Configurações de Conformidade**, expanda **Acesso ao Recurso da Empresa**e clique em **Perfis de Certificado**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Perfil Certificado**.  

## <a name="provide-general-information-about-the-certificate-profile"></a>Fornecer informações gerais sobre o perfil de certificado  

Na página **Geral** do Assistente para Criar Perfil de Certificado, especifique as seguintes informações:  

-   **Nome**: insira um nome exclusivo para o perfil de certificado. Você pode usar no máximo 256 caracteres.  

-   **Descrição**: forneça uma descrição que ofereça uma visão geral do perfil de certificado e outras informações relevantes que ajudem a identificá-lo no console do System Center Configuration Manager. Você pode usar no máximo 256 caracteres.  

-   **Especifique o tipo de perfil de certificado que deseja criar**: escolha um dos seguintes tipos de perfil de certificado:  

-   **Certificado de AC confiável**: selecione este tipo de perfil de certificado se desejar implantar uma AC (autoridade de certificação) raiz confiável ou intermediar o certificado da AC para formar uma cadeia de confiança de certificados para quando o usuário, ou dispositivo, precisar autenticar outro dispositivo. Por exemplo, o dispositivo pode ser um servidor RADIUS ou VPN (rede virtual privada). Você também deve configurar um perfil de certificado de autoridade de certificação confiável antes de criar um perfil de certificado SCEP. Neste caso, o certificado de autoridade de certificação confiável tem que ser o certificado confiável raiz da AC que emitirá o certificado para o usuário ou dispositivo.  

-   **Configurações do protocolo SCEP**: selecione este tipo de perfil de certificado se desejar solicitar um certificado para um usuário ou dispositivo usando o protocolo SCEP e o serviço de função de Serviço de Registro de Dispositivo de Rede.

-   **Troca de Informações Pessoais – Configurações PKCS #12 (PFX) – Importar**: selecione esta opção para importar um certificado PFX. Para saber mais sobre a criação de certificado PFX, confira [Importar perfis de certificado PFX](/sccm/mdm/deploy-use/import-pfx-certificate-profiles.md).

-   **Troca de Informações Pessoais – Configurações PKCS #12 (PFX) – Criar**: selecione isso para processar certificados PFX usando uma autoridade de certificação. Para saber mais sobre a criação de certificado PFX, consulte [Criar perfis de certificado PFX](/sccm/mdm/deploy-use/create-pfx-certificate-profiles.md).


## <a name="configure-a-trusted-ca-certificate"></a>Configurar um certificado de Autoridade de Certificação confiável  

> [!IMPORTANT]  
>  Você deve configurar pelo menos um perfil de certificado de autoridade de certificação confiável antes de criar um perfil de certificado SCEP.    
>  
>  Se você alterar qualquer um desses valores depois que o certificado for implantado, um novo certificado será solicitado:
>  -  Provedor de armazenamento de chaves
>  -  Nome do modelo de certificado
>  -  Tipo de certificado
>  -  Formato de nome de entidade
>  -  Nome alternativo da entidade
>  -  Período de validade do certificado
>  -  Uso de chave
>  -  Tamanho da chave
>  -  Uso estendido de chave
>  -  Certificado de AC raiz

1.  Na página **Certificado da AC Confiável** do Assistente para Criar Perfil de Certificado, especifique as seguintes informações:  

 -   **Arquivo de certificado**: clique em **Importar** e procure o arquivo de certificado que deseja usar.  

 -   **Armazenamento de destino**: para dispositivos que contêm mais de um repositório de certificados, selecione o local em que o certificado será armazenado. Para dispositivos que têm apenas um repositório, esta configuração será ignorada.  

2.  Use o valor da **Impressão digital do certificado** para verificar se importou o certificado correto.  


## <a name="configure-scep-certificate-information-only-for-scep-certificates"></a>Configurar as informações de certificado SCEP (somente para certificados SCEP)  

1.  Na página **Servidores SCEP** do assistente Criar Perfil de Certificado, especifique as URLs para os Servidores NDES que emitirão certificados por meio do SCEP. Você pode optar por atribuir automaticamente uma URL de NDES com base na configuração do servidor do sistema de site do ponto de registro de certificado ou adicionar as URLs manualmente.  

2.  Preencha a página **Registro do SCEP** do Assistente para Criar Perfil de Certificado.

 -  **Repetições**: especifique o número de vezes que o dispositivo tenta novamente, de modo automático, solicitar o certificado ao servidor que executa o Serviço de Registro de Dispositivo de Rede. Esta configuração oferece suporte ao cenário em que o gerenciador da AC deve aprovar uma solicitação de certificado antes que ela seja aceita. Esta configuração é normalmente usada em ambientes de alta segurança ou caso tenha uma AC emissora autônoma, ao invés de uma AC corporativa. Você também pode usar essa configuração para fins de teste, a fim de inspecionar as opções de solicitação de certificado antes que os processos da AC emissora processe a solicitação de certificado. Use essa configuração com a **Intervalo entre tentativas (minutos)** .  

 -   **Intervalo entre repetições (minutos)**: especifique o intervalo, em minutos, entre cada tentativa de registro ao usar uma aprovação de gerenciador de AC antes que a AC emissora processe a solicitação de certificado. Se for usar a aprovação de gerenciador para fins de teste, provavelmente vai preferir especificar um valor baixo para não ter que ficar esperando muito tempo até que o dispositivo tente solicitar o certificado novamente depois que você aprovou a solicitação. No entanto, se for usar a aprovação de gerenciador em uma rede de produção, provavelmente vai preferir especificar um valor alto para dar tempo suficiente ao administrador da AC para que verifique e aprove ou recuse as aprovações pendentes.  

 -   **Limite de renovação (%)**: especifique o percentual do tempo de vida do certificado restante antes da renovação das solicitações de dispositivo do certificado.  

 -   **KSP (Provedor de Armazenamento de Chave)**: especifique o local em que a chave do certificado será armazenada. Escolha um destes valores:  

   -   **Instalar no TPM (Trusted Platform Module) se houver**: instala a chave no TPM. Se o TPM não estiver presente, a chave será instalada no provedor de armazenamento para a chave de software.  

   -   **Instalar no TPM (Trusted Platform Module); caso contrário, falha**: instala a chave no TPM. Se o módulo TPM não estiver presente, a instalação falhará.  

   -   **Instalar no Windows Hello para Empresas; caso contrário, falha**: esta opção está disponível para dispositivos Windows 10 Desktop e Mobile. Registra a chave no **Windows Hello para Empresas**, descrita nas configurações do [Windows Hello para Empresas no System Center Configuration Manager](../../protect/deploy-use/windows-hello-for-business-settings.md). Essa opção também permite que você **exija o Multi-Factor Authentication** durante o registro de dispositivos antes de emitir certificados para esses dispositivos. Veja a seção [Proteger dispositivos Windows com o Multi-Factor Authentication](https://technet.microsoft.com/library/dn889751.aspx) para obter mais informações.

   > [!NOTE]  
   > 
   > Quando um usuário cria um PIN do Windows Hello para Empresas, o Windows envia uma notificação que o Configuration Manager escuta. Isso permite que o Configuration Manager reconheça rapidamente quais usuários criaram um PIN do Windows Hello para Empresas. O Configuration Manager também poderá emitir novos certificados para esses usuários se o Windows Hello for usado como o Provedor de Armazenamento de Chaves em um perfil de certificado.  

   -   **Instalar o Provedor de Armazenamento de Chaves de Software**: instala a chave no provedor de armazenamento para a chave de software.  

 -   **Dispositivos para registro de certificado**: se o perfil de certificado for implantado em uma coleção de usuários, escolha se deseja permitir o registro do certificado apenas no dispositivo primário do usuário ou em todos os dispositivos em que o usuário fizer logon. Se o perfil de certificado for implantado em uma coleção de dispositivos, escolha permitir se o registro do certificado é feito apenas pelo usuário primário do dispositivo ou por todos os usuários que fazem logon nele.  

3.  Na página **Propriedades do Certificado** do Assistente para Criar Perfil de Certificado, especifique as seguintes informações:  

 -   **Nome do modelo de certificado**: clique em **Procurar** para selecionar o nome de um modelo de certificado que o Serviço de Registro de Dispositivo de Rede está configurado para usar e que foi adicionado a uma AC emissora. Para procurar pelos modelos de certificado, a conta de usuário que você estiver usando para executar o console do System Center Configuration Manager deve ter permissão de Leitura para o modelo de certificado. Alternativamente, se não puder usar **Procurar**, digite o nome do modelo de certificado.  

 > [!IMPORTANT]
 >   
 >  Se o nome do modelo de certificado contiver caracteres não ASCII (ex.: caracteres do alfabeto chinês), o certificado não será implantado. Para garantir que o certificado será implantado, primeiro crie uma cópia do modelo do certificado na AC e renomeie a cópia usando caracteres ASCII.  

   Observe o seguinte, dependendo se você navega até o modelo de certificado ou digita o nome do certificado:  

 -   Se você navega para selecionar o nome do modelo de certificado, alguns campos da página são automaticamente populados por meio do modelo de certificado. Em alguns casos, você não pode alterar esses valores, a menos que escolha um modelo de certificado diferente.  

 -   Caso digite o nome do modelo de certificado, certifique-se de que o nome corresponda exatamente com um dos modelos de certificado relacionados no registro do servidor executando o Serviço de Registro de Dispositivo de Rede. Certifique-se de especificar o nome do modelo de certificado e não o nome para exibição do modelo de certificado.  

   Para localizar os nomes dos modelos de certificado, navegue até a seguinte chave: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP. Você verá os modelos de certificado listados como os valores para **EncryptionTemplate**, **GeneralPurposeTemplate**e **SignatureTemplate**. Por padrão, o valor para todos os modelos de certificado é **IPSECIntermediateOffline**, que mapeia até o nome de exibição do modelo do **IPSec (solicitação offline)**.  

   > [!WARNING]  
   > 
   >  Como o System Center Configuration Manager não pode verificar o conteúdo do modelo de certificado quando você digita o nome do modelo de certificado, em vez de procurar por ele, selecione as opções às quais o modelo de certificado não dá suporte e que acarretarão uma falha na solicitação de certificado. Quando isso acontece, uma mensagem de erro é exibida para o w3wp.exe no arquivo CPR.log informando que o nome do modelo no CSR não corresponde com o desafio.  
   >   
   >  Ao digitar o nome do modelo do certificado especificado para o valor de **GeneralPurposeTemplate** , você deve selecionar a **Codificação de chave** e as opções de **Assinatura digital** para este perfil de certificado. No entanto, se deseja habilitar apenas a opção **Codificação de chave** neste perfil de certificado, especifique o nome do modelo de certificado para a chave **EncryptionTemplate** . Do mesmo modo, se deseja habilitar apenas a opção **Assinatura digital** neste perfil de certificado, especifique o nome do modelo de certificado para a chave **SignatureTemplate** .  

 -   **Tipo de certificado**: selecione se o certificado será implantado em um dispositivo ou usuário.  
 -   **Formato de nome da entidade**: na lista, selecione o modo como o System Center Configuration Manager cria automaticamente o nome da entidade na solicitação de certificado. Se o certificado for para um usuário, você também pode incluir o endereço de email do usuário no nome da entidade. 
    
   > [!NOTE]  
   > 
   > Selecionar o **Número IMEI** ou o **Número de série** permite diferenciar dispositivos diferentes que pertencem ao mesmo usuário. Por exemplo, esses dispositivos podem compartilhar um nome comum, mas não o número IMEI ou o número de série. Se o dispositivo não relatar um IMEI ou um número de série, o certificado será emitido com o nome comum.

 -   **Nome alternativo da entidade**: especifique como o System Center Configuration Manager criará automaticamente os valores para o SAN (nome alternativo da entidade) na solicitação de certificado. Se tiver selecionado um tipo de certificado de usuário, por exemplo, você pode incluir o UPN no nome alternativo da entidade.  Se o certificado do cliente for usado para autenticar em um Servidor de Políticas de Rede, você deve definir o nome alternativo da entidade como o UPN.  

   > [!NOTE]  
   >  - Dispositivos iOS oferecem suporte a formatos de nome de entidade limitados e a nomes alternativos de entidade em certificados SCEP. Se você especificar um formato sem suporte, os certificados não serão registrados em dispositivos iOS. Ao configurar um perfil de certificado SCEP para ser implantado em dispositivos iOS, use o **nome Comum** para o **Formato do nome da entidade**e o **nome DNS**, o **endereço de email** ou o **UPN** para o **Nome alternativo da entidade**.  

 -   **Período de validade do certificado**: se você executou o comando certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE na AC emissora, o que permite um período de validade personalizado, pode especificar a quantidade de tempo restante antes que o certificado expire. Para obter mais informações sobre esse comando, consulte o tópico [Infraestrutura de certificado no System Center Configuration Manager](../../protect/deploy-use/certificate-infrastructure.md).  

   Você pode especificar um valor inferior ao período de validade do modelo de certificado especificado, mas não superior. Por exemplo, se o período de validade do certificado em um modelo de certificado for de dois anos, você pode especificar um valor de um ano, mas não de cinco anos. O valor também tem que ser inferior ao período de validade restante do certificado da AC emissora.  

 -   **Uso de chave**: especifique opções de uso de chave para o certificado. Você pode escolher entre as seguintes opções:  

        -   **Codificação de chave**: permitir a troca de chaves apenas quando a chave é criptografada.  

        -   **Assinatura digital**: permita a troca de chaves apenas quando uma assinatura digital ajudar a proteger a chave.  

   Se você selecionou um modelo de certificado usando **Procurar**, talvez não seja possível alterar essas definições a não ser que você selecione um modelo de certificado diferente.  

   O modelo de certificado selecionado por você deve ser configurado com uma ou ambas as opções acima de uso da chave. Se não for assim, você verá a mensagem **Uso da chave no CSR não corresponde ao desafio** no arquivo de log do ponto de registro de certificado, **Crp.log**.  


   -   **Tamanho da chave (bits)**: selecione o tamanho da chave em bits.  

   -   **Uso estendido de chave**: clique em **Selecionar** para adicionar valores para a finalidade desejada do certificado. Na maioria dos casos, o certificado exigirá **Autenticação de cliente** para que o usuário ou dispositivo possa autenticar-se em um servidor. No entanto, você pode adicionar outros usos da chave conforme necessário.  


   -   **Algoritmo de hash**: selecione um dos tipos de algoritmo de hash disponíveis a ser usado com esse certificado. Selecione o nível mais alto de segurança que dá suporte aos dispositivos de conexão.  

   > [!NOTE]  
   > 
   >  O**SHA-2** dá suporte ao SHA-256, SHA-384 e SHA-512. O**SHA-3** dá suporte apenas ao SHA-3.  

   -   **Certificado da CA raiz**: clique em **Selecionar** para escolher um perfil de certificado de AC raiz configurado anteriormente e implantado no usuário ou dispositivo. Esse certificado AC deve ser o certificado raiz da AC que emite o certificado que você está configurando nesse perfil de certificado.  

   > [!IMPORTANT]  
   >  Se você especificar um certificado de AC raiz que não está implantado no usuário ou no dispositivo, o System Center Configuration Manager não iniciará a solicitação de certificado que você está configurando nesse perfil de certificado.  


##  <a name="specify-supported-platforms-for-the-certificate-profile"></a>Especificar as plataformas com suporte para o perfil de certificado  

1. Na página **Plataformas com suporte** do Assistente para Criar Perfil de Certificado, selecione os sistemas operacionais nos quais deseja instalar o perfil de certificado. Ou, clique em **Selecionar Tudo** para instalar o perfil de certificado em todos os sistemas operacionais disponíveis.
2. Examine a página **Resumo** do assistente e escolha **Concluir**. 
 
 
O novo perfil de certificado aparece no nó **Perfis de Certificado** no espaço de trabalho **Ativos e Conformidade** e está pronto para ser implantado nos usuários ou dispositivos, conforme descrito em [Como implantar perfis no System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  