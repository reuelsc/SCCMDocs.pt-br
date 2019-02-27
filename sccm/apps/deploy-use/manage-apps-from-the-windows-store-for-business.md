---
title: Microsoft Store para Empresas
titleSuffix: Configuration Manager
description: Gerencie e implante aplicativos da Microsoft Store para Empresas com o Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d0a32357001f37f537f13fe85e71a41f9cb658ac
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56122433"
---
# <a name="manage-apps-from-the-microsoft-store-for-business-with-configuration-manager"></a>Gerenciar aplicativos da Microsoft Store para Empresas com o Configuration Manager

Na [Microsoft Store para Empresas](https://www.microsoft.com/business-store), você pode encontrar e adquirir aplicativos Windows para sua organização. Ao conectar a loja ao Configuration Manager, você sincronizará a lista dos seus aplicativos adquiridos. Exiba esses aplicativos no console do Configuration Manager e implante-os como você implanta qualquer outro aplicativo.


## <a name="bkmk_apps"></a> Aplicativos online e offline

A Microsoft Store para Empresas é compatível com dois tipos de aplicativo:

- **Online**: esse tipo de licença exige que usuários e dispositivos se conectem à loja para obter um aplicativo e sua licença. Os dispositivos Windows 10 precisam ter ingressado em um domínio do Azure AD (Active Directory).  

- **Offline**: esse tipo permite armazenar aplicativos e licenças em cache para implantá-los diretamente na rede local. Os dispositivos não precisam se conectar à loja nem ter uma conexão com a Internet.

[Leia mais](https://docs.microsoft.com/microsoft-store/microsoft-store-for-business-overview) sobre a Microsoft Store para Empresas.

O Configuration Manager dá suporte ao gerenciamento de aplicativos da Microsoft Store para Empresas em dispositivos Windows 10 com o cliente do Configuration Manager, bem como dispositivos Windows 10 registrados no Microsoft Intune. O Configuration Manager oferece as seguintes funcionalidades para aplicativos online e offline:


|Funcionalidade|Aplicativos offline|Aplicativos online|
|------------|------------|------------|
|Sincronizar dados do aplicativo com o Configuration Manager<br>(a sincronização ocorre a cada 24 horas)|Sim|Sim|
|Criar aplicativos do Configuration Manager de aplicativos da loja|Sim|Sim|
|Suporte para aplicativos gratuitos da loja|Sim|Sim|
|Suporte para aplicativos pagos da loja|Não|Sim<sup>1</sup>|
|Suporte para implantações obrigatórias em coleções de usuários ou dispositivos|Sim|Sim|
|Suporte para implantações disponíveis em coleções de usuários ou dispositivos|Sim|Sim|
|Suporte a aplicativos de linha de negócios da loja|Sim|Sim|
|Provisionar um aplicativo da loja para todos os usuários em um dispositivo<sup>2</sup><!--1358310-->|Sim|Sim|

- <sup>1</sup> Para implantar aplicativos licenciados online em dispositivos Windows 10 com o cliente do Configuration Manager, eles precisam estar executando o Windows 10, versão 1703 ou posteriores.  

- <sup>2</sup> Começando na versão 1806. Para obter mais informações, confira [Criar aplicativos Windows](/sccm/apps/get-started/creating-windows-applications#bkmk_provision).  


### <a name="deploying-online-apps-using-the-microsoft-store-for-business-to-devices-that-run-the-configuration-manager-client"></a>Implantando aplicativos online usando a Microsoft Store para Empresas em dispositivos que executam o cliente do Configuration Manager

Antes de implantar aplicativos da Microsoft Store para Empresas em dispositivos que executam o cliente completo do Configuration Manager, considere os seguintes pontos:

- Para garantir a funcionalidade completa, os dispositivos precisam estar executando o Windows 10, versão 1703 ou posteriores.  

- Os dispositivos precisam ter ingressado no Azure AD no mesmo locatário em que você registrou a Microsoft Store para Empresas como ferramenta de gerenciamento.  

- Quando a conta de administrador local entra no dispositivo, ela não consegue acessar os aplicativos da Microsoft Store para Empresas.  

- Os dispositivos precisam ter uma conexão de Internet dinâmica com a Microsoft Store para Empresas. Para obter mais informações, inclusive a configuração de proxy, confira [Pré-requisitos](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business).  


### <a name="notes-for-devices-running-earlier-versions-of-windows-10"></a>Observações para dispositivos que executam versões anteriores do Windows 10

Em dispositivos com o cliente do Configuration Manager que executam o Windows 10 versão 1607 ou anterior, aplica-se a seguinte funcionalidade:  

Quando você impõe a instalação do aplicativo no dispositivo por um dos seguintes métodos:  

- O usuário instala o aplicativo  

- A implantação atinge sua data limite de instalação   

- Reavaliação de pós-instalação para as implantações necessárias  

Em seguida, ocorrem os seguintes comportamentos:  

- O cliente do Configuration Manager "impõe" o aplicativo iniciando o aplicativo da Microsoft Store para Empresas  

- O usuário precisa concluir a instalação pela loja  

- No console do Configuration Manager, o status de implantação do aplicativo relata falha com o seguinte erro: “O aplicativo da Microsoft Store foi aberto no computador cliente e está aguardando que o usuário conclua a instalação.”  

No próximo ciclo de avaliação do aplicativo:  

- Se o usuário instalou o aplicativo da loja, o aplicativo relatará o status **Sucesso**  

- Se o usuário não tiver tentado instalar o aplicativo da loja:  

    - Para implantações necessárias, o cliente do Configuration Manager tenta iniciar o aplicativo da loja novamente  

    - As implantações disponíveis não são impostas novamente


#### <a name="further-notes-for-devices-running-earlier-versions-of-windows-10"></a>Outras observações para dispositivos que executam versões anteriores do Windows 10:

- Não é possível implantar aplicativos de linha de negócios da Microsoft Store para Empresas  

- Quando você implanta aplicativos pagos da loja, os usuários precisam entrar na loja e adquirir o aplicativo em si  

- Se você implantar uma política de grupo para desabilitar o acesso à versão de consumidor da Microsoft Store, as implantações da Microsoft Store para Empresas não funcionarão. Esse comportamento ocorre mesmo quando a Microsoft Store para Empresas está habilitada.  



## <a name="bkmk_setup"></a> Configurar a sincronização da Microsoft Store para Empresas

A sincronização da lista de aplicativos adquiridos pela sua organização permite que você veja esses aplicativos no console do Configuration Manager.

Conectar o site do Configuration Manager ao Azure AD e à Microsoft Store para Empresas. Para obter mais informações e detalhes desse processo, confira [Configurar serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard). Crie uma conexão com o serviço da **Microsoft Store para Empresas**.


### <a name="bkmk_config"></a> Informações de configuração e complementares 

Na página **Aplicativo** do Assistente de Serviços do Azure, primeiro selecione o **Ambiente do Azure** e o **Aplicativo Web**. Em seguida, leia a seção **Mais Informações** na parte inferior da página. Essas informações incluem as seguintes ações adicionais no portal da Microsoft Store para Empresas:  

- Configure o Configuration Manager como a ferramenta de gerenciamento da loja. Para obter mais informações, confira [Configurar o provedor de gerenciamento](https://docs.microsoft.com/microsoft-store/configure-mdm-provider-microsoft-store-for-business).  

- Habilite o suporte para aplicativos licenciados offline. Para obter mais informações, confira [Distribuir aplicativos offline](https://docs.microsoft.com/microsoft-store/distribute-offline-apps).  

- Adquira pelo menos um aplicativo. Para obter mais informações, confira [Encontrar e adquirir aplicativos](https://docs.microsoft.com/microsoft-store/find-and-acquire-apps-overview).  

Na página **Configurações** do Assistente de Serviços do Azure, especifique as seguintes informações:  

- **Caminho para o armazenamento de conteúdo de aplicativo da Microsoft Store para Empresas**: especifique um caminho de rede compartilhado, incluindo uma pasta. Por exemplo, `\\server\share\folder`. Quando o servidor do site é sincronizado com a loja, ele armazena o conteúdo em cache nesse local. Quando você cria um aplicativo no Configuration Manager, o servidor do site copia o conteúdo do aplicativo desse cache local para a biblioteca de conteúdo do site.  

- **Idiomas selecionados**: selecione os idiomas a serem sincronizados da loja e exibidos para os usuários no Centro de Software. Por exemplo, se o usuário configura o Windows para alemão, o Centro de Software mostra cadeias de caracteres em alemão para o aplicativo da loja. Esse comportamento exige que esse idioma seja sincronizado e exista para o aplicativo específico.    

- **Idioma padrão**: se o idioma do usuário não estiver disponível, selecione um idioma padrão a ser usado.  



## <a name="bkmk_deploy"></a> Criar e implantar um aplicativo do Configuration Manager de um aplicativo da Microsoft Store para Empresas

Após a sincronização, crie e implante os aplicativos da loja como qualquer outro aplicativo.

1.  No workspace **Biblioteca de Software** do console do Configuration Manager, expanda **Gerenciamento de Aplicativos** e clique em **Informações sobre Licença para Aplicativos da Loja**.  

2.  Escolha o aplicativo que deseja implantar e clique em **Criar Aplicativo** na faixa de opções.  

O site cria um aplicativo do Configuration Manager que contém o aplicativo da Microsoft Store para Empresas. 

Em seguida, implante e monitore o aplicativo, como você faria com qualquer outro aplicativo do Configuration Manager. Para obter mais informações, consulte os seguintes artigos:  
- [Implantar aplicativos](/sccm/apps/deploy-use/deploy-applications)
- [Monitorar aplicativos do console](/sccm/apps/deploy-use/monitor-applications-from-the-console)

> [!IMPORTANT]  
> Para dispositivos registrados no Microsoft Intune, os aplicativos implantados ficam disponíveis somente para o usuário que registrou o dispositivo originalmente. Nenhum outro usuário pode acessar o aplicativo.



## <a name="next-steps"></a>Próximas etapas

No workspace **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** e clique em **Informações sobre Licença para Aplicativos da Loja**.

É possível exibir as seguintes informações sobre cada aplicativo da loja que você gerencia:
- Nome do aplicativo
- Plataforma do aplicativo
- O número de licenças para o aplicativo que você tem
- O número de licenças disponíveis

Depois que os aplicativos online são implantados, todas as atualizações dos aplicativos vêm diretamente da Microsoft Store. Além disso, o Configuration Manager não verifica a conformidade da versão de aplicativos online, ele apenas verifica se o Windows relata o aplicativo como instalado.  

Ao implantar aplicativos offline em dispositivos Windows 10 com o cliente do Configuration Manager, não permita que os usuários atualizem aplicativos externos a implantações do Configuration Manager. O controle de atualizações em aplicativos offline é especialmente importante em ambientes de vários usuários, como salas de aula. Uma opção é desabilitar a Microsoft Store usando uma [política de grupo](https://docs.microsoft.com/windows/configuration/stop-employees-from-using-microsoft-store#a-href-idblock-store-group-policyablock-microsoft-store-using-group-policy). 

Depois que o administrador da Microsoft Store para Empresas adquirir um aplicativo offline, não publique o aplicativo aos usuários por meio da loja. Essa configuração garante que os usuários não possam instalar nem atualizar online. Os usuários somente recebem atualizações de aplicativos offline por meio do Configuration Manager. 
