---
title: Acesso condicional com o cogerenciamento
titleSuffix: Configuration Manager
description: Controlar o acesso dos usuários a recursos organizacionais com base nas regras de conformidade do Intune
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cf640b3-610c-4c3c-b966-c62e9f5654ff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2d5e5c7d6075697431f8c537366dc16164fedd1f
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754518"
---
# <a name="conditional-access-with-co-management"></a>Acesso condicional com o cogerenciamento

O acesso condicional garante que apenas usuários confiáveis possam acessar recursos organizacionais em dispositivos confiáveis usando aplicativos confiáveis. Ele é criado do zero na nuvem. Se você estiver gerenciando dispositivos com o Intune ou estendendo a implantação do Configuration Manager com o cogerenciamento, ele funcionará da mesma maneira.

No vídeo a seguir, o gerente de programas sênior Joey Glocke e o gerente de marketing de produtos Locky Ainley discutem e demonstram o acesso condicional com o cogerenciamento:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/The-Security-Benefits-of-Conditional-Access/player]

Com o cogerenciamento, o Intune avalia todos os dispositivos em sua rede para determinar a confiabilidade deles. Ele faz essa avaliação de duas maneiras:

1. O Intune verifica se um dispositivo ou aplicativo é gerenciado e configurado com segurança. Essa verificação depende do modo como você define as políticas de conformidade da sua organização. Por exemplo, garantir que todos os dispositivos estejam com criptografia habilitada e que não tenham jailbreak.  

    - Essa avaliação é baseada em configuração e precede a violação de segurança  

    - Para dispositivos cogerenciados, o Configuration Manager também faz a avaliação baseada na configuração. Por exemplo, atualizações necessárias ou conformidade de aplicativos. O Intune combina essa avaliação com sua própria avaliação.  

2. O Intune detecta incidentes de segurança ativos em um dispositivo. Ele usa a segurança inteligente da [Proteção Avançada contra Ameaças do Windows Defender](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/get-started) e de outros [provedores de defesa contra ameaças móveis](https://www.lookout.com/about/partners/microsoft). Esses parceiros executam uma análise de comportamento contínua nos dispositivos. Essa análise detecta incidentes ativos, depois transmite essas informações ao Intune para uma avaliação de conformidade em tempo real.  

    - Essa avaliação ocorre após a violação de segurança e é baseada em incidentes  

O vice-presidente corporativo da Microsoft, Brad Anderson, fala detalhadamente sobre o acesso condicional, com demonstrações ao vivo, durante a palestra no Ignite 2018. 

> [!VIDEO https://www.youtube.com/embed/7tDbUhVCX_I?start=1071]

O acesso condicional também oferece um local centralizado para ver a integridade de todos os dispositivos conectados à rede. Você obtém as vantagens da escala de nuvem, o que é especialmente importante para testar instâncias de produção do Configuration Manager.


## <a name="benefits"></a>Benefícios

Toda equipe de TI preocupa-se muito com a segurança da rede. É obrigatório garantir que todos os dispositivos atendam aos requisitos de segurança e de negócios antes de acessar sua rede. Com o acesso condicional, você pode determinar os seguintes fatores: 
- Se todos os dispositivos são criptografados  
- Se há malware instalado  
- Se suas configurações estão atualizadas  
- Se ele está desbloqueado por jailbreak ou rooting  

O acesso condicional combina um controle granular sobre os dados organizacionais com uma experiência de usuário que maximiza a produtividade de trabalho em qualquer dispositivo e em qualquer local.

O vídeo a seguir mostra como a [Proteção Avançada Contra Ameaças](https://www.microsoft.com/windowsforbusiness/windows-atp) (ATP) é integrada a cenários comuns que você enfrenta com frequência:

> [!VIDEO https://www.youtube.com/embed/A7IrxAH87wc?start=178]

Com o cogerenciamento, o Intune pode incorporar responsabilidades do Configuration Manager para avaliar sua conformidade com padrões de segurança dos aplicativos ou atualizações necessárias. Esse comportamento é importante para qualquer organização de TI que queira continuar usando o Configuration Manager para aplicativos complexos e gerenciamento de patches.

O acesso condicional também é uma parte essencial do desenvolvimento da arquitetura da sua [Rede de Confiança Zero](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/14/building-zero-trust-networks-with-microsoft-365/). Com o acesso condicional, controles de acesso de dispositivo em conformidade abrangem as camadas básicas da Rede de Confiança Zero. Essa funcionalidade é uma grande parte do modo como você protege sua organização no futuro.

Para saber mais, confira a postagem no blog sobre [Como aprimorar o acesso condicional com os dados de risco de computador da Proteção Avançada contra Ameaças do Windows Defender](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Enhancing-conditional-access-with-machine-risk-data-from-Windows/ba-p/250559).



## <a name="case-studies"></a>Estudos de caso

A empresa de consultoria de TI Wipro usa o acesso condicional para proteger e gerenciar os dispositivos usados por 91.000 funcionários. Em um estudo de caso recente, o vice-presidente de TI da Wipro fez esta observação:

> *Alcançar o acesso condicional é uma grande vitória para a Wipro. Agora, todos os nossos funcionários têm acesso móvel às informações sob demanda.*
> *Melhoramos nossa postura de segurança e a produtividade dos funcionários. Agora, 91.000 funcionários se beneficiam de um acesso altamente seguro a mais de 100 aplicativos a partir de qualquer dispositivo, em qualquer lugar.*

<!-- waiting for the case study to be public
For more information, see [Wipro drives mobile productivity with Microsoft cloud security tools to improve customer engagements](https://customers.microsoft.com/story/446f72f9-2f50-4697-b688-6d279786e010)
-->

Outros exemplos incluem: 

- A Nestlé, que usa o acesso condicional baseado em aplicativo para mais de 150.000 funcionários  

- A empresa de software de automação Cadence, que agora pode garantir que “apenas os dispositivos gerenciados tenham acesso a aplicativos do Office 365, como o Teams, e à Intranet da empresa”. Eles também podem oferecer a seus funcionários um acesso mais seguro a outros aplicativos baseados em nuvem, como o Workday e o Salesforce. Para saber mais sobre a experiência da Cadence com o Intune, confira [Cadence aumenta o ritmo dos negócios com ferramentas de colaboração móveis no Microsoft 365](https://customers.microsoft.com/story/cadence-partner-professional-services-microsoft-365).

O Intune também é totalmente integrado a parceiros como Cisco ISE, Aruba Clear Pass e Citrix NetScaler. Com esses parceiros, você pode manter controles de acesso baseados no registro no Intune e no estado de conformidade do dispositivo nessas outras plataformas.

Para saber mais, confira os seguintes vídeos:
- [Brad Anderson demonstra o acesso condicional em detalhes](https://youtu.be/8321obNofgM?t=547)  
- [Detalhes adicionais da zona de ponto de extremidade 1805](https://youtu.be/f-ILlEuBFZg?t=196)  


## <a name="value-proposition"></a>Proposta de valor

Com o acesso condicional e a integração da ATP, você fortalece um componente fundamental de toda organização de TI: o acesso seguro à nuvem.

Em mais de 63% de todas as violações de dados, os invasores obtêm acesso à rede da organização por meio de credenciais de usuário fracas, padronizadas ou roubadas. Como o acesso condicional concentra-se na proteção da identidade dos usuários, ele restringe o roubo de credenciais. O acesso condicional gerencia e protege suas identidades, sejam elas privilegiadas ou não. Não há melhor maneira de proteger os dispositivos e os dados contidos neles.

Como o acesso condicional é um componente essencial do Enterprise Mobility + Security (EMS), não é necessária nenhuma configuração ou arquitetura local. Com o Intune e o Azure Active Directory (Azure AD), você pode configurar rapidamente o acesso condicional na nuvem. Se você está usando o Configuration Manager, é possível estender com facilidade seu ambiente para a nuvem com o cogerenciamento e começar a usá-lo imediatamente.

Para saber mais sobre a integração à ATP, confira esta postagem do blog [A pontuação de risco do dispositivo da ATP do Windows Defender expõe novos ataques cibernéticos e impulsiona o acesso Condicional para proteger as redes](https://cloudblogs.microsoft.com/microsoftsecure/2018/11/28/windows-defender-atp-device-risk-score-exposes-new-cyberattack-drives-conditional-access-to-protect-networks/). Ela detalha como um grupo avançado de hackers usou ferramentas jamais vistas. A nuvem da Microsoft as detectou e interrompeu porque os usuários visados tinham o acesso condicional. A invasão ativou a política de acesso condicional baseada em riscos do dispositivo. Embora o invasor já tivesse estabelecido um ponto de apoio na rede, os computadores explorados foram automaticamente impedidos de acessar serviços organizacionais e dados gerenciados pelo Azure AD.



## <a name="configure"></a>Configurar

O acesso condicional é fácil de usar quando você [habilita o cogerenciamento](/sccm/comanage/how-to-enable). Ele requer a transferência da carga de trabalho **Políticas de Conformidade** para o Intune. Para saber mais, confira [Como mudar as cargas de trabalho do Configuration Manager para o Intune](/sccm/comanage/how-to-switch-workloads). 

Para saber mais sobre como usar o acesso condicional, confira os seguintes artigos: 

- [Acesso condicional no Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)  

- [Políticas de conformidade do dispositivo do Intune](https://docs.microsoft.com/intune/device-compliance)  

- [Acesso condicional baseado no aplicativo com o Intune](https://docs.microsoft.com/intune/app-based-conditional-access-intune)  

> [!Note]  
> Os recursos de acesso condicional ficam disponíveis imediatamente para dispositivos híbridos do Azure AD. Esses recursos incluem a autenticação multifator e o controle de acesso de ingresso ao Azure AD híbrido. Esse comportamento ocorre porque eles são baseados em propriedades do Azure AD. Para aproveitar a avaliação baseada em configuração do Intune e do Configuration Manager, habilite o cogerenciamento. Essa configuração fornece controle de acesso diretamente do Intune para dispositivos em conformidade. Também oferece recursos de avaliação de políticas de conformidade do Intune.  

