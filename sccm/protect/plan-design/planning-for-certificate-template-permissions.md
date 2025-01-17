---
title: Planejar permissões de modelo de certificado
titleSuffix: Configuration Manager
description: Saiba mais sobre o planejamento das permissões que você precisa para configurar os modelos de certificado que o System Center Configuration Manager usa.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: eab0e09d-b09e-4c14-ab14-c5f87472522e
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 817dc9a2fcce8580bf01d57053536ce78b4d1ed3
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500335"
---
# <a name="planning-for-certificate-template-permissions-for-certificate-profiles-in-system-center-configuration-manager"></a>Planejando permissões de modelo de certificado para perfis de certificado no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


As informações a seguir podem ajudar a planejar como configurar permissões para os modelos de certificado que o System Center Configuration Manager usa quando você implanta perfis de certificado.  

## <a name="default-security-permissions-and-considerations"></a>Considerações e permissões de segurança padrão  
 As permissões de segurança padrão necessárias para os modelos de certificado que o System Center Configuration Manager usará ao solicitar certificados para os usuários e dispositivos são as seguintes:  

- Leitura e Registro para a conta usada pelo pool de aplicativos do Serviço de Registro de Dispositivo de Rede  

- Leitura para a conta que executa o console do System Center Configuration Manager  

  Para saber mais sobre estas permissões de segurança, veja [Configuração de infraestrutura de certificado](../deploy-use/certificate-infrastructure.md).  

  Quando você utiliza essa configuração padrão, os usuários e os dispositivos não podem solicitar diretamente certificados dos modelos de certificado, e todas as solicitações devem ser iniciadas pelo Serviço de Registro de Dispositivo de Rede. Essa é uma restrição importante, pois esses modelos de certificado devem ser configurados com **Fornecer na solicitação** para a Entidade do certificado, o que significa que existe um risco de representação se um usuário não autorizado ou um dispositivo comprometido solicitar um certificado. Na configuração padrão, o Serviço de Registro de Dispositivo de Rede deve iniciar essa solicitação. No entanto, esse risco de representação permanece se o serviço que executa o Serviço de Registro de Dispositivo de Rede está comprometido. Para evitar esse risco, siga todas as práticas recomendadas de segurança para o Serviço de Registro de Dispositivo de Rede e o computador que executa esse serviço de função.  

  Se as permissões de segurança padrão não atenderem a seus requisitos de negócios, você terá outra opção para configurar as permissões de segurança nos modelos de certificado: é possível adicionar permissões de Leitura e Registro para usuários e computadores.  

## <a name="adding-read-and-enroll-permissions-for-users-and-computers"></a>Adicionando permissões de Leitura e Registro para usuários e computadores  
 Este procedimento poderá ser adequado se uma equipe diferente gerenciar sua equipe de infraestrutura de AC (autoridade de certificação) e desejar que o System Center Configuration Manager verifique se os usuários têm uma conta válida do Active Directory Domain Services antes de enviar a eles um perfil de certificado para solicitar um certificado de usuário. Para essa configuração, você deve especificar um ou mais grupos de segurança que contenham os usuários e conceder a esses grupos permissões de Leitura e Registro nos modelos de certificado. Nesse cenário, o administrador de autoridade de certificação gerencia o controle de segurança.  

 Da mesma forma, você pode especificar um ou mais grupos que contenham contas de computador e conceder a esses grupos permissões de Leitura e Registro nos modelos de certificado. Se você implantar um perfil de certificado de computador em um computador que seja membro do domínio, a conta desse computador deverá receber permissões de Leitura e Registro. Essas permissões não serão necessárias se o computador não for membro do domínioâ€”, por exemplo, se ele for um computador de grupo de trabalho ou um dispositivo móvel pessoal.  

 Embora essa configuração use um controle de segurança adicional, ela não é uma prática recomendada. O motivo disso é que os usuários ou os proprietários especificados dos dispositivos podem solicitar certificados de maneira independente do System Center Configuration Manager e fornecer valores para a Entidade do certificado que podem ser usados para representar outro usuário ou dispositivo.  

 Além disso, se você especificar que as contas não podem ser autenticadas no momento da solicitação do certificado, a solicitação falhará por padrão. Por exemplo, a solicitação de certificado falhará se o servidor que estiver executando o Serviço de Registro de Dispositivo de Rede estiver em uma floresta do Active Directory não confiável para a floresta que contém o servidor do sistema de site do ponto de registro de certificado. Você poderá configurar o ponto de registro de certificado para continuar se não for possível autenticar uma conta porque não há resposta de um controlador de domínio. No entanto, essa não é uma prática recomendada de segurança.  

 Observe que, se o ponto de registro de certificado estiver configurado para verificar permissões de conta e um controlador de domínio estiver disponível e rejeitar a solicitação de autenticação (por exemplo, a conta está bloqueada ou foi excluída), ocorrerá falha na solicitação de registro de certificado.  

#### <a name="to-check-for-read-and-enroll-permissions-for-users-and-domain-member-computers"></a>Para verificar as permissões de Leitura e Registro dos usuários e dos computadores membros do domínio  

1.  No servidor do sistema de sites que hospeda o ponto de registro de certificado, crie a seguinte chave do Registro DWORD para que ela tenha o valor de 0: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheck  

2.  Se não for possível autenticar uma conta porque não há resposta de um controlador de domínio, e você desejar ignorar a verificação de permissão:  

    -   No servidor do sistema de sites que hospeda o ponto de registro de certificado, crie a seguinte chave do Registro DWORD para que ela tenha o valor de 1: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheckOnlyIfAccountAccessDenied  

3.  Na autoridade de certificação emissora, na guia **Segurança** , nas propriedades do modelo de certificado, adicione um ou mais grupos de segurança para conceder permissões de Leitura e Registro às contas de usuário ou dispositivo.  
