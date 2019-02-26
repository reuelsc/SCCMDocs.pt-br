---
title: Acesso condicional com o cogerenciamento
titleSuffix: Configuration Manager
description: Controlar o acesso do usuário aos recursos organizacionais com base nas regras de conformidade do Intune
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
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754518"
---
# <a name="conditional-access-with-co-management"></a>Acesso condicional com o cogerenciamento

Acesso condicional garante que apenas usuários confiáveis podem acessar recursos organizacionais em dispositivos confiáveis usando aplicativos confiáveis. Ele é criado do zero na nuvem. Se você estiver gerenciando dispositivos com o Intune ou estender a implantação do Configuration Manager com o cogerenciamento, ele funciona da mesma maneira.

No vídeo a seguir, gerente de programa sênior Joey Glocke e Ainley Locky do gerente de marketing de produto discutem e demonstração do acesso condicional com o cogerenciamento:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/The-Security-Benefits-of-Conditional-Access/player]

Com o cogerenciamento, o Intune avalia todos os dispositivos em sua rede para determinar a confiabilidade é. Ele faz essa avaliação de duas maneiras a seguir:

1. Intune torna-se de que um dispositivo ou aplicativo é gerenciado e configurado com segurança. Essa seleção depende de como você pode definir políticas de conformidade da sua organização. Por exemplo, certifique-se de habilitar a criptografia de todos os dispositivos e não são desbloqueados.  

    - Essa avaliação é a violação de segurança pré e baseada em configuração  

    - Para dispositivos cogerenciados, Configuration Manager também faz a avaliação de configuração. Por exemplo, necessária conformidade de atualizações ou aplicativos. Intune combina essa avaliação junto com sua própria avaliação.  

2. Intune detecta incidentes de segurança do Active Directory em um dispositivo. Ele usa a segurança inteligente da [Windows Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/get-started) e outras [provedores de defesa contra ameaças móveis](https://www.lookout.com/about/partners/microsoft). Esses parceiros executar análise de comportamento em andamento nos dispositivos. Essa análise detecta incidentes ativos e, em seguida, passa essas informações para o Intune para avaliação de conformidade em tempo real.  

    - Essa avaliação é a violação de segurança pós-implantação e baseado em incidentes  

Microsoft vice-presidente corporativo, Brad Anderson, discute o acesso condicional em camadas com demonstrações ao vivo durante a palestra do Ignite de 2018. 

> [!VIDEO https://www.youtube.com/embed/7tDbUhVCX_I?start=1071]

Acesso condicional também fornece um local centralizado para ver a integridade de todos os dispositivos conectados à rede. Você obtém as vantagens da escala de nuvem, que é especialmente importante para instâncias de produção de teste do Configuration Manager.


## <a name="benefits"></a>Benefícios

Cada equipe de TI é voltada a segurança de rede. É obrigatório para certificar-se de que cada dispositivo atende aos seus requisitos de segurança e de negócios antes de acessar sua rede. Com acesso condicional, você pode determinar os seguintes fatores: 
- Se todos os dispositivos são criptografados  
- Se o malware está instalado  
- Se suas configurações são atualizadas  
- Se ele está desbloqueado ou modificado  

Acesso condicional combina um controle granular sobre dados organizacionais com uma experiência de usuário que maximiza a produtividade de trabalho em qualquer dispositivo em qualquer local.

A seguir mostra vídeo como [proteção avançada de Thread](https://www.microsoft.com/windowsforbusiness/windows-atp) (ATP) é integrado ao cenários comuns que você enfrentar regularmente:

> [!VIDEO https://www.youtube.com/embed/A7IrxAH87wc?start=178]

Com o cogerenciamento, o Intune pode incorporar responsabilidades do Configuration Manager para avaliar sua conformidade com padrões de segurança dos aplicativos ou atualizações necessárias. Esse comportamento é importante para qualquer organização de TI que deseja continuar usando o Configuration Manager para aplicativos complexos e gerenciamento de patches.

Acesso condicional também é uma parte crítica do desenvolvimento de sua [Zero Trust Network](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/14/building-zero-trust-networks-with-microsoft-365/) arquitetura. Com acesso condicional, controles de acesso do dispositivo em conformidade abrangem as camadas básicas de rede de confiança do Zero. Essa funcionalidade é uma grande parte de como você protege sua organização no futuro.

Para obter mais informações, consulte o postagem no blog sobre [aprimorando o acesso condicional com os dados de risco de máquina do Windows Defender Advanced Threat Protection](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Enhancing-conditional-access-with-machine-risk-data-from-Windows/ba-p/250559).



## <a name="case-studies"></a>Estudos de caso

A TI Wipro empresa de consultoria usa o acesso condicional para proteger e gerenciar os dispositivos usados por todos os 91,000 funcionários. Em um estudo de caso recente, o vice-presidente de IT em Wipro observado:

> *O acesso condicional é uma grande vitória para Wipro. Agora, todos os nossos funcionários têm acesso móvel a informações sob demanda. * 
>  *Aprimoramos nossa produtividade de funcionário e a postura de segurança. Agora, os 91,000 funcionários se beneficiar de acesso altamente seguro para mais de 100 aplicativos de qualquer dispositivo, em qualquer lugar.*

<!-- waiting for the case study to be public
For more information, see [Wipro drives mobile productivity with Microsoft cloud security tools to improve customer engagements](https://customers.microsoft.com/story/446f72f9-2f50-4697-b688-6d279786e010)
-->

Outros exemplos incluem: 

- Nestle, que usa o acesso condicional baseado em aplicativo para os funcionários mais de 150.000  

- A empresa de software de automação, cadência, que agora pode Certifique-se de que "somente dispositivos gerenciados tem acesso a aplicativos do Office 365, como as equipes e a intranet da empresa." Eles também possam oferecer sua força de trabalho "acesso mais seguro para outros aplicativos baseados em nuvem, como o Salesforce e o dia de trabalho". Para obter mais informações sobre a experiência da cadência com o Intune, consulte [cadência aumenta o ritmo dos negócios com ferramentas de colaboração móvel no Microsoft 365](https://customers.microsoft.com/story/cadence-partner-professional-services-microsoft-365).

Intune é também totalmente integrado com parceiros, como Cisco ISE, Aruba Clear Pass e Citrix NetScaler. Com esses parceiros, você pode manter os controles de acesso com base no registro do Intune e o estado de conformidade do dispositivo através dessas outras plataformas.

Para obter mais informações, consulte os seguintes vídeos:
- [Acesso condicional de demonstrações de Brad Anderson em detalhes](https://youtu.be/8321obNofgM?t=547)  
- [Detalhes adicionais de 1805 de zona do ponto de extremidade](https://youtu.be/f-ILlEuBFZg?t=196)  


## <a name="value-proposition"></a>Proposta de valor

Com acesso condicional e a integração de ATP, você está fortalecendo um componente fundamental de cada organização de TI: proteger o acesso de nuvem.

Em mais de 63% de todas as violações de dados, os invasores obtiverem acesso à rede da organização por meio de credenciais de usuário fracas, padrão ou roubado. Como acesso condicional concentra-se sobre como proteger a identidade do usuário, ela restringe o roubo de credenciais. Acesso condicional gerencia e protege suas identidades com privilégios ou sem privilégios. Não há nenhuma maneira melhor para proteger os dispositivos e os dados neles.

Como o acesso condicional é um componente principal do Enterprise Mobility + Security (EMS), não há nenhuma configuração local ou a arquitetura necessária. Com o Intune e Azure Active Directory (Azure AD), você pode configurar o acesso condicional rapidamente na nuvem. Se atualmente você estiver usando o Configuration Manager, você pode facilmente estender seu ambiente para a nuvem com o cogerenciamento e começar a usá-lo no momento.

Para obter mais informações sobre a integração de ATP, consulte esta postagem de blog [pontuação de risco de dispositivo do Windows Defender ATP expõe cibernético novo, unidades de acesso condicional para proteger as redes](https://cloudblogs.microsoft.com/microsoftsecure/2018/11/28/windows-defender-atp-device-risk-score-exposes-new-cyberattack-drives-conditional-access-to-protect-networks/). Fornece detalhes sobre como um grupo de hackers avançado usado nunca antes vistas ferramentas. A nuvem da Microsoft detectados e interrompido-los, porque os usuários de destino tinham acesso condicional. A invasão ativado a política de acesso condicional com base no risco do dispositivo. Embora o invasor já estabelecida entram na rede, as máquinas exploradas eram restritos automaticamente contra o acesso aos serviços organizacionais e os dados gerenciados pelo Azure AD.



## <a name="configure"></a>Configurar

Acesso condicional é fácil de usar quando você [habilitar o cogerenciamento](/sccm/comanage/how-to-enable). Ele requer movendo o **políticas de conformidade** carga de trabalho para o Intune. Para saber mais, consulte [Como mudar as cargas de trabalho do Configuration Manager para o Intune](/sccm/comanage/how-to-switch-workloads). 

Para obter mais informações sobre como usar o acesso condicional, consulte os seguintes artigos: 

- [Acesso condicional no Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)  

- [Políticas de conformidade de dispositivo do Intune](https://docs.microsoft.com/intune/device-compliance)  

- [Acesso condicional baseado em aplicativo com o Intune](https://docs.microsoft.com/intune/app-based-conditional-access-intune)  

> [!Note]  
> Recursos de acesso condicional ficam disponíveis imediatamente para o Azure híbrido dispositivos ingressados no AD. Esses recursos incluem a autenticação multifator e híbrido de controle de acesso de junção do Azure AD. Esse comportamento ocorre porque elas são baseadas em Propriedades do Azure AD. Para aproveitar a avaliação com base em configuração do Intune e Configuration Manager, habilite o cogerenciamento. Essa configuração fornece a você controle de acesso diretamente do Intune para dispositivos em conformidade. Ele também fornece recursos de avaliação de políticas de conformidade do Intune.  

