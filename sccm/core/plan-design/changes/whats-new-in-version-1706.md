---
title: "Nova versão 1706"
titleSuffix: Configuration Manager
description: "Veja os detalhes das alterações e os novos recursos introduzidos na versão 1706 do System Center Configuration Manager."
ms.custom: na
ms.date: 08/11/2017
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ac034143-003e-4629-aac2-99eaffef4db1
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 2889de0709096aa481ca6203c5ab2bac1f064d5e
ms.sourcegitcommit: c4a1bafcd004638d264a93d307c70d8b6f7fe023
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="what39s-new-in-version-1706-of-system-center-configuration-manager"></a>Novidades da versão 1706 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A atualização 1706 da ramificação atual do System Center Configuration Manager está disponível como uma atualização no console para sites instalados anteriormente que executam a versão 1606, 1610 ou 1702.

> [!TIP]  
> Para instalar um novo site, você deve usar uma versão de linha de base do Configuration Manager.  
>  Saiba mais sobre:    
>   - [Instalação de novos sites](https://technet.microsoft.com/library/mt590197.aspx)  
>   - [Instalação de atualizações em sites](https://technet.microsoft.com/library/mt607046.aspx)  
>   - [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

As seções a seguir fornecem detalhes sobre as alterações e novas funcionalidades introduzidas na versão 1706 do Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated features](/sccm/core/plan-design/changes/removed-and-deprecated-features).

Version 1706 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infraestrutura do site

### <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Suporte do Cache Par do Cliente para arquivos de instalação expressa para Windows 10 e Office 365  
<!-- 1352486 -->
A partir desta versão, o Cache Par dá suporte à distribuição de arquivos de instalação expressa de conteúdo para Windows 10 e dos arquivos de atualização para o Office 365. Nenhuma configuração adicional é necessária para oferecer suporte a essa alteração.

### <a name="updates-for-the-data-warehouse"></a>Atualizações para o data warehouse
<!-- 1277922 -->
O data warehouse não é mais um recurso de pré-lançamento. Também atualizamos os pré-requisitos para incluir suporte para o banco de dados no SQL Server AlwaysOn em grupos de disponibilidade e em clusters de failover. Para saber mais, veja o [Ponto de serviço do Data Warehouse](/sccm/core/servers/manage/data-warehouse).

### <a name="accessibility-improvements"></a>Aprimoramentos na acessibilidade
<!-- 1253000 -->
Adicionamos outros aprimoramentos de acessibilidade ao console do Configuration Manager. Para obter detalhes, confira [Recursos de acessibilidade](/sccm/core/understand/accessibility-features).

### <a name="improvements--for-sql-server-always-on-availability-groups"></a>Aprimoramentos para Grupos de Disponibilidade Always On do SQL Server
<!-- 1352094 -->
Com esta versão, agora você pode usar réplicas de confirmação assíncrona nos grupos de disponibilidade AlwaysOn do SQL Server usados com o Configuration Manager. Isso significa que você pode adicionar mais réplicas a seus grupos de disponibilidade para usar como backups fora do local (remotos) e, em seguida, usá-los em um cenário de recuperação de desastres.  
  -   O Configuration Manager dá suporte ao uso de réplica de confirmação assíncrona para recuperar sua réplica síncrona. Confira [Opções de recuperação do banco de dados do site](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption) no tópico Backup e recuperação para obter informações sobre como fazer isso.
  -   Esta versão não dá suporte a failover para usar a réplica de confirmação assíncrona como seu banco de dados do site.
Para saber mais, confira [Preparar para usar os Grupos de Disponibilidade Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

### <a name="update-reset-tool"></a>Ferramenta de redefinição de atualização
<!-- 1324589 -->
A partir da versão 1706, os sites primários do Configuration Manager e os sites de administração central incluem a Ferramenta de Redefinição de Atualização do Configuration Manager, **CMUpdateReset.exe**. Use essa ferramenta com qualquer versão do branch atual que permanece com suporte para corrigir problemas de download ou replicação de atualizações no console. Para saber mais, confira [Ferramenta de redefinição de atualização](/sccm/core/servers/manage/update-reset-tool).

### <a name="high-dpi-console-support"></a>Suporte de console com alto DPI  
<!-- 1353476 -->
Com esta versão, devem ser corrigidos os problemas com o modo como o console do Configuration Manager pode ser expandido e exibe diferentes partes da interface do usuário quando é exibido em dispositivos de DPI alto (como um livro do Surface).

### <a name="improved-boundary-groups-for-software-update-points"></a>Grupos de limites aprimorados para os pontos de atualização de software
<!-- 1324591 -->
Esta versão inclui aprimoramentos no funcionamento dos pontos de atualização de software com grupos de limites. O exemplo a seguir resume o novo comportamento de fallback:
-   Agora, o fallback para pontos de atualização de software usa um tempo configurável para fallback para grupos de limites vizinhos.
-   Independentemente da configuração de fallback, um cliente tenta acessar o último ponto de atualização de software usado durante 120 minutos. Após não conseguir acessar o servidor durante 120 minutos, o cliente verifica seu pool de pontos de atualização de software disponíveis, para poder encontrar um novo.
-   Após não conseguir acessar o servidor original durante duas horas, o cliente muda para um ciclo mais curto a fim de entrar em contato com um novo ponto de atualização de software. Isso significa que, se um cliente não conseguir se conectar com um novo servidor, ele selecionará rapidamente o próximo servidor a partir do pool de servidores disponíveis e tentará contatá-lo.

Para saber mais, confira [pontos de atualização de software](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) no tópico Grupos de limites do Branch Atual.

### <a name="azure-ad-integration-with-configuration-manager"></a>Integração do Azure AD com o Configuration Manager
<!-- 1248187, 1290765, 1258052, 1298097, 1319334, 1319883, 1352135, 1353331 -->
Com esta versão, aprimoramos a integração do Configuration Manager e do Azure Active Directory (Azure AD).  Esses aprimoramentos simplificam o modo como configuramos os serviços do Azure que você usa com o Configuration Manager, e ajudam você a gerenciar clientes e usuários que autenticam pelo Azure AD.

A integração aprimorada possibilita o seguinte:  
  -   Assistente para Serviços do Azure – Esse Assistente fornece uma experiência de configuração comum que substitui os fluxos de trabalho individuais para configurar os seguintes serviços do Azure usados com o Configuration Manager.
      - **Gerenciamento de Nuvem** permite que os clientes autentiquem usando o Azure Active Directory (Azure AD). Você também pode configurar a Descoberta de Usuário do Azure AD.
      - **Conector do OMS** Conecte-se ao OMS (Operations Manager Suite) e sincronize dados como coleções com o OMS Log Analytics.
      - **Upgrade Readiness** Conecte-se ao Upgrade Readiness e exiba dados de compatibilidade de atualização do cliente.
      - **Windows Store para Empresas** Conecte-se ao repositório online do Windows Store para Empresas e obtenha aplicativos para a sua organização que podem ser implantados com o Configuration Manager.


  Isso é feito usando um [aplicativo Web de servidor do Azure](/azure/azure/app-service/app-service-authentication-overview#service-to-service-authentication) para fornecer os detalhes da assinatura e de configuração que você inseriria sempre que configurasse um novo componente ou serviço do Configuration Manager com o Azure. Para saber mais, confira [Assistente para Serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard).

-   Use o Azure AD para autenticar clientes na Internet a fim de acessar seus sites do Configuration Manager. O Azure AD substitui a necessidade de configurar e usar certificados de autenticação de cliente. Isso exige a função do sistema de site de gateway de gerenciamento de nuvem. Para saber mais, confira [Instalar e atribuir clientes do Configuration Manager na Internet usando o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

-   Instalar e gerenciar o cliente do Configuration Manager em computadores localizados na Internet. Isso exige o uso da função do sistema de site de gateway de gerenciamento de nuvem. Para saber mais, confira [Instalar e atribuir clientes do Configuration Manager na Internet usando o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

-   Configurar a Descoberta de Usuário do Azure AD.  Use o Assistente para Serviços do Azure para configurar esse novo método de descoberta. Esse novo método consulta seu Azure AD em busca de dados de usuário que você pode usar junto com dados de descoberta tradicionais.  Há suporte para a sincronização completa e delta.  Para saber mais, confira [Descoberta de Usuário do Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).

### <a name="peer-cache-improvements"></a>Aprimoramentos de cache de pares
<!-- 1252345 -->
O cache de pares não usa mais a Conta de Acesso de Rede para autenticar solicitações de download dos pares. Há uma limitação para isso quando a conta permanece exigida pelos clientes. Isso permanece um requisito para clientes que iniciam no WinPE e, depois, acessam o conteúdo de uma fonte de cache de pares. Para saber mais, confira [Requisitos e considerações para cache de pares](/sccm/core/plan-design/hierarchy/client-peer-cache#requirements-and-considerations-for-peer-cache).


<!-- ## Migration  -->


<!-- ## Client management  -->


## <a name="compliance-settings"></a>Configurações de conformidade

### <a name="new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client"></a>Novas definições de configuração para dispositivos com Windows 10 que não são gerenciados com o cliente do Configuration Manager
<!-- 1354715 -->
Nesta versão, adicionamos novas definições de item de configuração para dispositivos com Windows 10 registrados com o Intune, ou gerenciados no Configuration Manager local. As configurações são:

- **Senha**
    - Criptografia de Dispositivo
- **Dispositivo**
    - Modificação das configurações de região (somente desktop)
    - Modificação das configurações de energia e suspensão
    - Modificação das configurações de idioma
    - Modificação do horário do sistema
    - Modificação do nome do dispositivo
- **Repositório**
    - Atualização automática de aplicativos da store
    - Usar somente armazenamento particular
    - Inicialização de aplicativo proveniente do armazenamento
- **Microsoft Edge**
    - Bloquear o acesso à página about:flags
    - Substituição de prompt SmartScreen
    - Substituição de prompt SmartScreen para arquivos
    - Endereço IP do localhost WebRTC
    - Mecanismo de pesquisa padrão
    - URL de XML OpenSearch
    - Home pages (somente desktop)

Para obter detalhes de todas as configurações de Windows 10, confira [Como criar itens de configuração para dispositivos Windows 10 e Windows 8.1 gerenciados sem o cliente do System Center Configuration Manager](/sccm/mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client).

### <a name="new-device-compliance-policy-rules"></a>Novas regras de política de conformidade do dispositivo

* **Tipo de senha necessária**. Especifica se o usuário deve criar uma senha alfanumérica ou numérica. Para senhas alfanuméricas, especifique também o número mínimo de conjuntos de caracteres que a senha deverá conter. Há quatro conjuntos de caracteres: minúsculas, maiúsculas, letras, símbolos e números.

 **Com suporte em:**
 * Windows Phone 8+
 * Windows 8.1+
 * iOS 6+
<br></br>
* **Bloquear a depuração de USB no dispositivo**. Você não precisa definir essas configurações, pois a depuração de USB já está desabilitada em dispositivos com Android for Work.

 **Com suporte em:**
 * Android 4.0+
 * Samsung KNOX Standard 4.0+
<br></br>
* **Bloquear aplicativos de fontes desconhecidas**. Exija que dispositivos impeçam a instalação de aplicativos de fontes desconhecidas. Você não precisa definir essa configuração, pois os dispositivos com Android for Work sempre restringem a instalação de fontes desconhecidas.

  **Com suporte em:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
<br></br>
* **Exigir verificação de ameaças em aplicativos**. Essa configuração especifica que o recurso Verificar aplicativos fique habilitado no dispositivo.

 **Com suporte em:**
 * Android 4.2 a 4.4
 * Samsung KNOX Standard 4.0+

Confira [criar e implantar uma política de conformidade do dispositivo](https://docs.microsoft.com/sccm/mdm/deploy-use/create-compliance-policy) para experimentar as novas regras de conformidade do dispositivo

## <a name="application-management"></a>Gerenciamento de aplicativos

### <a name="run-powershell-scripts-from-the-configuration-manager-console"></a>Executar scripts do PowerShell do console do Configuration Manager
<!-- 1236459 -->

No Configuration Manager, você pode implantar scripts em dispositivos de cliente usando pacotes e programas. Nesta versão, adicionamos uma nova funcionalidade que permite a execução das seguintes ações:

- Importar scripts do PowerShell no Configuration Manager
- Editar os scripts no console do Configuration Manager (apenas para scripts não assinados)
- Marcar scripts como aprovados ou negados, a fim de melhorar a segurança
- Execute scripts em coleções de computadores de cliente com Windows e em computadores com Windows gerenciados localmente. Você não implanta os scripts, em vez disso, eles são executados quase em tempo real nos dispositivos cliente.
- Examine os resultados retornados pelo script no console do Configuration Manager.

Para saber mais, confira [Criar e executar scripts do PowerShell do console do Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).

### <a name="new-mobile-application-management-policy-settings"></a>Novas configurações de política de gerenciamento de aplicativo móvel    
<!--1324760-->
A partir desta versão, você pode usar três novas configurações de política MAM (gerenciamento de aplicativo móvel):

- **Bloquear captura de tela (somente dispositivos Android):** especifica que as funcionalidades de captura de tela do dispositivo sejam bloqueadas ao usar esse aplicativo.

Veja [proteger aplicativos usando políticas de proteção de aplicativos no Configuration Manager](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies) para testar as novas configurações de política de proteção do aplicativo.


## <a name="operating-system-deployment"></a>Implantação de sistema operacional

### <a name="hardware-inventory-collects-secure-boot-information"></a>O inventário de hardware coleta informações de Inicialização Segura
O inventário de hardware agora coleta informações para mostrar se a Inicialização Segura está habilitada nos clientes. Essas informações são armazenadas na classe **SMS_Firmware** (introduzida na versão 1702) e habilitada no inventário de hardware por padrão. Para saber mais sobre o inventário de hardware, confira [Como configurar o inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

### <a name="collapsible-task-sequence-groups"></a>Grupos de sequências de tarefas recolhíveis
Esta versão apresenta a capacidade de expandir e recolher grupos de sequência de tarefas. Você pode expandir ou recolher grupos individuais ou expandir ou recolher todos os grupos de uma só vez.

### <a name="reload-boot-images-with-current-windows-pe-version"></a>Recarregue as imagens de inicialização com a versão atual do Windows PE
Quando você executa **Atualizar Pontos de Distribuição** em uma imagem de inicialização selecionada, agora pode optar por recarregar a versão mais recente do Windows PE (a partir do diretório de instalação do Windows ADK) na imagem de inicialização. Para saber mais, confira [Atualizar pontos de distribuição com a imagem de inicialização](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image).

## <a name="software-updates"></a>Atualizações de software

### <a name="improvements-to-express-update-download-time"></a>Aprimoramentos no tempo de download de Atualização Expressa
Nesta versão, aprimoramos consideravelmente o tempo de download das Atualizações Expressas. Para saber mais, confira [Gerenciar os arquivos de instalação expressa para atualizações do Windows 10](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).

### <a name="manage-microsoft-surface-driver-updates"></a>Gerenciar atualizações de driver do Microsoft Surface
<!-- 1098490 -->
Agora você pode usar o Configuration Manager para gerenciar atualizações de driver do Microsoft Surface.    


#### <a name="prerequisites"></a>Pré-requisitos
- Todos os pontos de atualização de software devem executar o Windows Server 2016.    
- Este é um recurso de pré-lançamento que você deve ativar para que ele fique disponível. Para obter mais informações, consulte [Usar recursos de pré-lançamento de atualizações](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

#### <a name="to-manage-surface-driver-updates"></a>Para gerenciar atualizações de driver do Surface

1. Habilite a sincronização para os drivers do Microsoft Surface. Use o procedimento em [Configurar classificação e produtos](/sccm/sum/get-started/configure-classifications-and-products) e marque a caixa de seleção **Incluir drivers e atualizações de firmware do Microsoft Surface** na guia **Classificações** para habilitar os drivers do Surface.
2. [Sincronizar os drivers do Microsoft Surface](/sccm/sum/get-started/synchronize-software-updates).
3. [Implantar os drivers sincronizados do Microsoft Surface](/sccm/sum/deploy-use/deploy-software-updates)

### <a name="configure-windows-update-for-business-deferral-policies"></a>Configurar as políticas de adiamento do Windows Update for Business
<!-- 1290890 -->
Agora você pode configurar as políticas de adiamento para as Atualizações de Recurso do Windows 10 ou Atualizações de Qualidade para dispositivos com Windows 10 gerenciados diretamente pelo Windows Update for Business. Você pode gerenciar as políticas de adiamento no novo nó **Políticas do Windows Update for Business** em **Biblioteca de Software** > **Manutenção do Windows 10**.

Para obter detalhes, confira [Integração com o Windows Update for Business no Windows 10](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).

### <a name="improved-user-notifications-for-office-365-updates"></a>Notificações de usuário aprimoradas para atualizações do Office 365
Melhorias foram feitas para aproveitar a experiência de usuário do Office com Clique para Executar quando um cliente instala uma atualização do Office 365. Isso inclui notificações pop-up e no aplicativo, e uma experiência de contagem regressiva. Para saber mais, confira [Comportamento de reinicialização e notificações do cliente para atualizações do Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#restart-behavior-and-client-notifications-for-office-365-updates)

## <a name="reporting"></a>Relatórios

### <a name="use-windows-analytics-with-configuration-manager"></a>Usar o Windows Analytics com o Configuration Manager
<!-- 1318608 -->
O Windows Analytics é um conjunto de soluções executado no Operations Management Suite. As soluções permitem que você obtenha informações sobre o estado atual de seu ambiente. Os dispositivos em seu ambiente reportam dados telemétricos do Windows. Os dados podem ser acessados por meio do Portal da Web do Operations Management Suite. No caso do Upgrade Readiness, os dados estão diretamente disponíveis no nó de monitoramento do console do Configuration Manager.

Para saber mais, confira [Usar o Windows Analytics com o Configuration Manager](/sccm/core/clients/manage/monitor-windows-analytics).


<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Gerenciamento de dispositivos móveis

### <a name="updates-to-android-for-work-sharing-configuration"></a>Atualizações para configuração de compartilhamento do Android for Work
<!-- 1338403 -->
Com esta versão, os valores para a configuração **Permitir o compartilhamento de dados entre o perfil de trabalho e pessoal** no grupo de configurações **Perfil de Trabalho** foram atualizados. Também adicionamos uma configuração personalizada para bloquear a ação de copiar e colar entre perfis pessoais e de trabalho.

Para saber mais, confira [Itens de configuração para dispositivos com Android for Work](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client).

### <a name="android-and-ios-enrollment-restrictions"></a>Restrições de inscrição do Android e iOS
<!-- 1290826 -->
Com essa versão, agora você pode especificar que os usuários não podem inscrever dispositivos Android ou iOS pessoais. Novas configurações de restrição de dispositivo permitem que você limite o registro de dispositivos Android a dispositivos pré-declarados. Para dispositivos iOS, você pode bloquear o registro de todos os dispositivos, exceto aqueles registrados com o Programa de registro de dispositivos da Apple, com o Apple Configurator ou com a conta do gerenciador de registro de dispositivo do Intune.
- Para saber mais sobre as restrições de registro do Android, veja [Configurar o gerenciamento de dispositivo do Android](/sccm/mdm/deploy-use/enroll-hybrid-android).
- Para saber mais sobre as restrições de registro do iOS, veja [Configurar as restrições de registro de iOS](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac#configure-enrollment-restrictions).

## <a name="protect-devices"></a>Proteger dispositivos

### <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Incluir relação de confiança para arquivos e pastas específicos em uma política de Proteção do Dispositivo
<!--1324676-->
Nesta versão, adicionamos mais recursos para o gerenciamento de política de Proteção do Dispositivo.

Agora, você tem a opção de adicionar a relação de confiança para arquivos específicos e pastas em uma política de Proteção do Dispositivo. Isso permite que você:

- Solucione problemas de comportamentos do instalador gerenciado
- Confie em aplicativos de linha de negócios que não podem ser implantados com o Configuration Manager
- Confie em aplicativos que estão incluídos em uma imagem de implantação de sistema operacional

Para obter mais detalhes, confira [Gerenciamento de Proteção do Dispositivo com Configuration Manager](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager).
