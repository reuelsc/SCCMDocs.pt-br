---
title: Saiba mais sobre a segurança de script do PowerShell
titleSuffix: Configuration Manager
description: Recursos para ajudar a saber mais sobre a segurança de script do PowerShell.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: a0bd093d-67a5-4f74-bf79-dd604889f5ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 376d35ae0eaca282b9634e2c3eeb50b9c814f270
ms.sourcegitcommit: a6a6507e01d819217208cfcea483ce9a2744583d
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2019
ms.locfileid: "66748006"
---
# <a name="learn-more-about-powershell-script-security"></a>Saiba mais sobre a segurança de script do PowerShell

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

É responsabilidade do administrador validar o uso proposto do PowerShell e de parâmetros do PowerShell no ambiente. Estes são alguns recursos úteis para ajudar a instruir os administradores sobre o poder do PowerShell e as superfícies de risco potenciais. Isso tem como finalidade ajudar a atenuar as superfícies de risco potenciais e permitir o uso de scripts seguros.

## <a name="powershell-script-security"></a>Segurança de script do PowerShell
Há um recurso interno em Executar Scripts para examinar visualmente e aprovar os scripts que são solicitados a serem executados no ambiente. Os administradores devem estar cientes de que os scripts do PowerShell podem ter um script oculto: um script mal-intencionado e difícil de ser detectado com a inspeção visual durante o processo de aprovação de script. Como uma melhor prática, o uso de determinadas ferramentas de inspeção, além de examinar visualmente os scripts do PowerShell, ajudará a detectar problemas de scripts suspeitos. Essas ferramentas nem sempre podem determinar a intenção do autor do PowerShell, para que possa chamar a atenção para um script suspeito. No entanto, as ferramentas exigirão que o administrador avalie se ela é uma sintaxe de script mal-intencionada ou intencional.

## <a name="recommendations"></a>Recomendações
- Familiarize-se com as melhores práticas de segurança do PowerShell usando os vários links referenciados abaixo.
- **Assinar os scripts**: outro método para manter os scripts seguros é fazer com que eles sejam verificados e, em seguida, assinados antes de importá-los para uso.
- Não armazenar segredos (como senhas) em scripts do PowerShell e saiba mais sobre como lidar com segredos.


## <a name="general-information-about-powershell-security-best-practices"></a>Informações gerais sobre as melhores práticas de segurança do PowerShell

Essa coleção de links foi escolhida para fornecer aos administradores do Configuration Manager como um ponto de partida para saber mais sobre as melhores práticas de segurança de script do PowerShell.  

[Introdução às melhores práticas de segurança do PowerShell](https://blogs.msdn.microsoft.com/powershell/2013/12/16/powershell-security-best-practices/ )

[PowerPoint sobre as melhores práticas de segurança do PowerShell](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/74/metablogapi/1055.PowerShell-Security-Best-Practices_3CA24C32.pptx)

<iframe src="https://channel9.msdn.com/Events/Blue-Hat-Security-Briefings/BlueHat-Security-Briefings-Fall-2013-Sessions/PowerShell-Best-Practices/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

[Blog da equipe do PowerShell Defending Against PowerShell Attacks (Defendendo-se de ataques ao PowerShell)](https://blogs.msdn.microsoft.com/powershell/2017/10/23/defending-against-powershell-attacks/)

[Twitter Defending Against PowerShell Attacks (Defendendo-se de ataques ao PowerShell), do defensor de segurança e do Microsoft PowerShell Lee Holmes](https://twitter.com/Lee_Holmes/status/922462821081694208)

[Protegendo contra a injeção de código mal-intencionado](https://blogs.msdn.microsoft.com/powershell/2006/11/22/protecting-against-malicious-code-injection/)

[A Equipe Azul do PowerShell discute o log de bloco de Script Profundo, o Log de Eventos Protegidos, a Interface de Verificação de Antimalware e as APIs de Geração de Código Seguro](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)

[Para o Windows 10, há uma API para uma interface de verificação de antimalware](https://cloudblogs.microsoft.com/microsoftsecure/2015/06/09/windows-10-to-offer-application-developers-new-malware-defenses/?source=mmpc)

## <a name="powershell-parameters-security"></a>Segurança de parâmetros do PowerShell
Passar parâmetros é uma maneira de ter flexibilidade com os scripts e adiar as decisões até o tempo de execução. Ele também expõe outra superfície de risco. As melhores práticas para impedir a injeção de script ou de parâmetros mal-intencionados são:

- Permitir somente o uso de parâmetros predefinidos.
- Usar o recurso de expressão regular para validar os parâmetros permitidos.
    - Exemplo: se apenas determinado intervalo de valores for permitido, use uma expressão regular para verificar apenas esses caracteres ou valores que compõem o intervalo.
    - A validação de parâmetros pode ajudar a impedir que os usuários tentem usar determinados caracteres que podem ter escape, como aspas. Lembre-se de que pode haver vários tipos de aspas e, portanto, o uso de expressões regulares para validar quais caracteres você decidiu que são permitidos costuma ser mais fácil do que tentar definir todas as entradas que não são permitidas.
- Utilize o módulo do PowerShell ["caçador de injeção"](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) na Galeria do PowerShell.
    - Pode haver falsos positivos; portanto, procure a intenção quando algo for sinalizado como suspeito para determinar se ele é um problema real ou não. 
- O Microsoft Visual Studio tem um analisador de Script, que pode ajudar com a verificação da sintaxe do PowerShell.
- Este vídeo intitulado “DEF CON 25 - Lee Holmes - Get $pwnd: Attacking Battle Hardened Windows Server” (Atacando um Windows Server protegido para a batalha) fornece uma visão geral dos tipos de problemas contra os quais você pode proteger (especialmente, a seção 12:20 a 17:50):     <iframe width="560" height="315" src="https://www.youtube.com/embed/ahxMOAAani8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## <a name="environment-recommendations"></a>Recomendações para o ambiente
Recomendações gerais para administradores do PowerShell.
1. Implante a última versão do PowerShell, como a versão 5 ou superior, interna no Windows 10. Como alternativa, você pode implantar o [Windows Management Framework](https://www.microsoft.com/en-us/download/details.aspx?id=54616), disponível até e incluindo o Windows 7 e o Windows Server 2008 R2. 
2. Habilite e colete logs do PowerShell, incluindo, opcionalmente, o Log de Eventos Protegidos. Incorpore esses logs em suas assinaturas, caçada e fluxos de trabalho de resposta a incidentes.
3. Implemente a Administração Just Enough em sistemas de alto valor para eliminar ou reduzir o acesso administrativo irrestrito a esses sistemas.
4. Implante políticas do Controle de Aplicativos/Device Guard para permitir que tarefas administrativas pré-aprovadas usem a capacidade total da linguagem do PowerShell, limitando o uso interativo e não aprovado a um subconjunto limitado da linguagem do PowerShell.
5. Implante o Windows 10 para conceder acesso completo ao provedor de antivírus a todo o conteúdo (incluindo o conteúdo gerado ou revelado em tempo de execução) processado pelos Hosts de Script do Windows, incluindo o PowerShell.
