---
title: "Segurança e privacidade de perfis de certificado"
titleSuffix: Configuration Manager
description: "Saiba mais sobre as práticas recomendadas de segurança para gerenciar perfis de certificado para usuários e dispositivos no System Center Configuration Manager."
ms.custom: na
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3393db41-900a-44c5-b950-2d46a35a198c
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: e36df89f86afe95e922b7afa3bb1e6029b832b4d
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="security-and-privacy-for-certificate-profiles-in-system-center-configuration-manager"></a>Segurança e privacidade de perfis de certificado no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


##  <a name="security-best-practices-for-certificate-profiles"></a>Práticas recomendadas de segurança para perfis de certificado  
 Use as seguintes práticas recomendadas de segurança ao gerenciar perfis de certificado para usuários e dispositivos.  

|Prática recomendada de segurança|Mais informações|  
|----------------------------|----------------------|  
|Identifique e siga todas as práticas recomendadas de segurança para o Serviço de Registro de Dispositivo de Rede, que inclui a configuração do site da Web desse serviço no IIS (Serviços de Informações da Internet) para exigir SSL e ignorar certificados de cliente.|Consulte as [Diretrizes do Serviço de Registro de Dispositivo de Rede](http://go.microsoft.com/fwlink/p/?LinkId=309016) na biblioteca de Serviços de Certificados do Active Directory no TechNet.|  
|Ao configurar os perfis de certificado do SCEP, escolha as opções mais seguras que os dispositivos e a sua infraestrutura podem dar suporte.|Identifique, implemente e siga as práticas recomendadas de segurança que foram sugeridas para os dispositivos e a infraestrutura.|  
|Especificar manualmente a afinidade de dispositivo de usuário, em vez de permitir que os usuários identifiquem o dispositivo principal. Além disso, não habilitar a configuração baseada em uso.|Se você clicar na opção **Permitir a inscrição de certificados apenas no dispositivo primário do usuário** em um perfil de certificado SCEP, não considere as informações coletadas dos usuários ou do dispositivo como autoritativas. Se você implantar perfis de certificado SCEP com essa configuração, e um usuário administrativo confiável não especificar a afinidade de dispositivo de usuário, é possível que usuários não autorizados recebam privilégios elevados, bem como certificados para autenticação.<br /><br /> **Observação:** se você habilitar a configuração baseada em uso, essas informações serão coletadas usando mensagens de estado que não são protegidas pelo System Center Configuration Manager. Para ajudar a reduzir essa ameaça, use IPsec ou assinatura SMB entre computadores cliente e o ponto de gerenciamento.|  
|Não adicione permissões Ler e Registrar para usuários aos modelos de certificado, ou configure o ponto de registro de certificado para ignorar a verificação do modelo de certificado.|Embora o Configuration Manager dê suporte à verificação adicional, se você adicionar as permissões de segurança Ler e Registrar para os usuários e se puder configurar o ponto de registro de certificado para pular essa verificação caso a autenticação não seja possível, nenhuma das configurações será uma prática recomendada de segurança. Para obter mais informações, consulte [Planejando permissões de modelo de certificado para os perfis de certificado no System Center Configuration Manager](../../protect/plan-design/planning-for-certificate-template-permissions.md).|  

## <a name="privacy-information-for-certificate-profiles"></a>Informações de privacidade para perfis de certificado  
 Você pode usar perfis de certificado para implantar certificados de cliente e da AC (autoridade de certificação) raiz e avaliar se esses dispositivos tornam-se compatíveis depois que os perfis são aplicados. O ponto de gerenciamento envia informações de conformidade ao servidor do site, e o System Center Configuration Manager armazena essas informações no banco de dados do site. As informações de conformidade incluem propriedades do certificado, como nome da entidade e impressão digital. As informações são criptografadas quando os dispositivos as enviam para o ponto de gerenciamento, mas não são armazenadas em formato criptografado no banco de dados do site. O banco de dados mantém as informações até que a tarefa de manutenção de site **Excluir Dados Antigos de Gerenciamento da Configuração** as exclua após o intervalo padrão de 90 dias. Você pode configurar o intervalo de exclusão. As informações de conformidade não são enviadas à Microsoft.  

 Os perfis de certificado utilizam as informações que o Configuration Manager coleta usando a descoberta. Para mais informações sobre informações de privacidade para descoberta, consulte a seção **Informações de Privacidade para Descoberta** em [Security and privacy for System Center Configuration Manager](../../core/plan-design/security/security-and-privacy.md).  

> [!NOTE]  
>  Os certificados emitidos para usuários ou dispositivos podem permitir o acesso a informações confidenciais.  

 Por padrão, os dispositivos não avaliam perfis de certificado. Além disso, você deve configurar os perfis de certificado e implantá-los nos usuários ou dispositivos.  

 Antes de configurar os perfis de certificado, considere seus requisitos de privacidade.  
