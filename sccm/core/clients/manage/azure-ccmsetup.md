---
title: Fluxo de trabalho de autenticação do Azure AD
titleSuffix: Configuration Manager
description: Detalhes do processo de instalação de cliente do Configuration Manager em um dispositivo Windows 10 com o sistema de autenticação do Azure Active Directory
ms.date: 05/24/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 9aaf466a-3f40-4468-b3cd-f0010f21f05a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c422e5134ca798c1a5422cd518d550ed4c188e9a
ms.sourcegitcommit: bfb8a17f60dcb9905e739045a5141ae45613fa2c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66213797"
---
# <a name="azure-ad-authentication-workflow"></a>Fluxo de trabalho de autenticação do Azure AD

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo é uma referência técnica para o processo de instalação de cliente do Configuration Manager em um dispositivo Windows 10 associado ao Azure Active Directory (Microsoft Azure AD). Ele fornece detalhes sobre o processo de fluxo de trabalho para a instalação de cliente e autenticação de dispositivo.  
 

## <a name="azure-ad-token-request-workflow"></a>Fluxo de trabalho de solicitação de token do Microsoft Azure AD

![Diagrama do fluxo de trabalho de ccmsetup do Microsoft Azure AD](media/azure-ad-install-workflow.png)  

### <a name="1-azure-ad-token-request"></a>1. Solicitação de token do Microsoft Azure AD

Um cliente associado a um domínio do Microsoft Azure AD do Windows 10 usa parâmetros do Microsoft Azure AD para solicitar um token. As entradas a seguir são registradas no arquivo **ccmsetup.log**:

- Solicitar token de dispositivo do Microsoft Azure AD:

    ```
    Getting AAD (device) token with: ClientId = 22ed38d9-XXXX-4036-XXXX-a98452fda4fc, ResourceUrl = https://ConfigMgrService, AccountId = https://login.microsoftonline.com/common/oauth2/token
    ```

- Se não for possível obter um token de dispositivo, ele solicita um token de usuário do Microsoft Azure AD:

    ```
    Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
    ```

> [!NOTE]
> O cliente deve obter um certificado Workplace Join (WPJ) ao ingressar no Azure AD. Se o certificado Workplace Join não for encontrado, o cliente não tentará criar a solicitação usando o canal de comunicação do Serviço de Token de Segurança (CCM_STS). Esse comportamento ocorre porque o cliente não consegue adicionar um token do Microsoft Azure AD à solicitação. Normalmente, o dispositivo não tem esse certificado quando o cliente não está corretamente associado ao Microsoft Azure AD.
>
> Além disso, se o token não for válido, o Gateway de Gerenciamento de Nuvem não encaminhará a solicitação para as funções internas do site. O token pode ser inválido, caso o locatário não esteja registrado como um serviço de gerenciamento de nuvem no Configuration Manager.


### <a name="2-configuration-manager-client-token-request"></a>2. Solicitação de token de cliente do Configuration Manager

Quando o cliente tiver um token do Microsoft Azure AD, ele solicitará um token de cliente do Configuration Manager.

As entradas a seguir são registradas no arquivo **ccmsetup.log** da máquina virtual do Gateway de Gerenciamento de Nuvem:

```
Getting CCM Token from STS server 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216'
Getting CCM Token from https://CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216/CCM_STS
```

#### <a name="21-cmg-gets-request"></a>2.1 O Gateway de Gerenciamento de Nuvem obtém a solicitação

As entradas a seguir são registradas no arquivo **IIS.log**:

```
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="22-cmg-forwards-request-to-cmg-connection-point"></a>2.2 O Gateway de Gerenciamento de Nuvem encaminha a solicitação para o respectivo ponto de conexão

As entradas a seguir são registradas no arquivo **CMGService.log**:

```
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="23-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>2.3 O ponto de conexão do Gateway de Gerenciamento de Nuvem transforma a solicitação do cliente do Gateway de Gerenciamento de Nuvem em uma solicitação de cliente do ponto de gerenciamento

As entradas a seguir são registradas no arquivo **SMS_Cloud_ProxyConnector.log**:

```
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="24-management-point-verifies-user-token-in-site-database"></a>2.4 O ponto de gerenciamento verifica o token de usuário no banco de dados do site

As entradas a seguir são registradas no arquivo **CCM_STS.log**:

```
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0aebad80-77d2-4f0a-9639-676ee4764bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```


## <a name="content-location-request"></a>Solicitação de localização de conteúdo

Quando o cliente obtém uma resposta com o token do Gateway de Gerenciamento de Nuvem, ele armazena a resposta em cache e a usa para solicitar as informações do site e a localização do conteúdo por meio do Gateway de Gerenciamento de Nuvem. As entradas a seguir são registradas no arquivo **ccmsetup.log**:

```
Cached encrypted token for 'S-1-5-18'. Will expire at '00/99/2999 00:00:00'
Sending location request to 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216' with payload '< Request >
Appending CCM Token to the header.
```


## <a name="client-installation"></a>Instalação do cliente

O dispositivo baixa o conteúdo do cliente e inicia a instalação.

### <a name="communication-validation"></a>Validação da comunicação

- O Gateway de Gerenciamento de Nuvem (CMG) valida o token do cliente via CMG, ponto de conexão do CMG e HTTP(S), além da solicitação do banco de dados do ponto de gerenciamento.
- O cliente verifica o certificado de serviço ou de gerenciamento do Gateway de Gerenciamento de Nuvem
- PKI para certificado de serviço do Gateway de Gerenciamento de Nuvem: o cliente solicita a Autoridade de Certificação Raiz do certificado do Gateway de Gerenciamento de Nuvem em um repositório local
- Certificado de serviço de terceiros do Gateway de Gerenciamento de Nuvem: os clientes validam automaticamente um certificado com a respectiva Autoridade de Certificação Raiz publicada na Internet


## <a name="common-issues"></a>Problemas comuns

- Ausência de Autoridade de Certificação Raiz
- Verificação de CRL habilitada: publicar uma CRL na Internet ou usar a opção **/NoCRLcheck** na linha de comando
- Certificado WPJ não encontrado: o cliente está registrado mas não está associado ao Azure AD

O uso da opção /NoCRLCheck funciona apenas para inicialização de ccmsetup. Para que os clientes sejam totalmente funcionais, publique a CRL na Internet. Como alternativa, é possível desabilitar a verificação de CRL na configuração da comunicação com cliente do site. Caso contrário, depois de atualizar as configurações de segurança pelo serviço de localização, os clientes deixarão de se comunicar com o servidor.
