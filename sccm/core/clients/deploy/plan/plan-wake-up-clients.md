---
title: Ativando clientes | Microsoft Docs
description: "Planeje a ativação de clientes no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 52ee82b2-0b91-4829-89df-80a6abc0e63a
caps.latest.revision: 6
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: 12ee719a6a8b072fab27d083aeb2b8439484058d

---
# <a name="plan-how-to-wake-up-clients-in-system-center-configuration-manager"></a>Planejar a ativação de clientes no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 O Configuration Manager dá suporte a duas tecnologias LAN (rede local) que ativam os computadores no modo de suspensão quando você deseja instalar o software necessário, como atualizações de software e aplicativos: pacotes de ativação tradicionais e comandos de ativação AMT.  

Você pode completar o método tradicional do pacote de ativação usando as configurações de proxy de ativação do cliente. Proxy de ativação usa um protocolo ponto a ponto e computadores selecionados para verificar se outros computadores na sub-rede estão ativos e ativá-los, se necessário. Quando o site está configurado para Wake on LAN e os clientes são configurados para proxy de ativação, o processo funciona da seguinte forma:  

1.  Computadores com o cliente do Configuration Manager instalado e que não estão em suspensão na sub-rede verificam se outros computadores na sub-rede estão ativos. Eles fazem isso enviando uns aos outros um comando ping do TCP/IP a cada 5 segundos.  

2.  Se não houver resposta de outros computadores, supõe-se que estarão em modo de suspensão. Os computadores ativos tornam-se *computadores gerenciadores* da sub-rede.  

     É possível que um computador não responda por outro motivo que não seja a suspensão (por exemplo, está desligado, removido da rede, ou a configuração de proxy de ativação do cliente não é mais aplicada), por isso recebem um pacote de ativação todos os dias às 14h. hora local. Computadores que não respondem não serão mais considerados como em suspensão e não serão despertados pelo proxy de ativação.  

     Para oferecer suporte ao proxy de ativação, pelo menos três computadores devem estar ativos em cada sub-rede. Para conseguir isso, três computadores, de forma não determinista, são escolhidos para serem *computadores guardiões* da sub-rede. Isso significa que permanecem ativos, apesar de qualquer política de ativação configurada para suspensão ou hibernação após um período de inatividade. Computadores guardiões respeitam comandos de desligamento ou reinicialização, por exemplo, como resultado de tarefas de manutenção. Se isso acontecer, os computadores guardiões restantes ativarão outro computador na sub-rede, de modo que a sub-rede continuará a ter três computadores guardiões.  

3.  Computadores gerenciadores solicitam comutador de rede para redirecionar tráfego de rede dos computadores em suspensão para si mesmos.  

     O redirecionamento é alcançado pela transmissão, por parte do computador gerenciador, de uma estrutura de Ethernet que usa o endereço MAC do computador em suspensão como endereço de origem. Isso faz com que o comutador de rede se comporte como se o computador em suspensão tivesse se movido para a mesma porta do computador gerenciador. O computador gerenciador também envia pacotes ARP para os computadores em suspensão, para manter a entrada como nova no cache ARP. O computador gerenciador também responderá a solicitações de ARP em nome do computador em suspensão e responderá com o endereço MAC do computador em suspensão.  

    > [!WARNING]  
    >  Durante esse processo, o mapeamento IP-MAC para o computador em suspensão permanece o mesmo. O proxy de ativação funciona informando ao comutador de rede que um adaptador de rede diferente está usando a porta registrada por outro adaptador de rede. No entanto, esse comportamento é conhecido como flap de MAC e é incomum em operação de rede padrão. Algumas ferramentas de monitoramento de rede procuram esse comportamento e podem supor que algo está errado. Consequentemente, essas ferramentas de monitoramento podem gerar alertas ou fechar portas quando você usa o proxy de ativação.  
    >   
    >  Não use proxy de ativação se sua rede de serviços e ferramentas de monitoramento não permitirem flaps de MAC.  

4.  Quando um computador gerenciador vê uma nova solicitação de conexão TCP para um computador suspenso e a solicitação é para uma porta que esse computador usava como escuta antes de entrar em suspensão, o computador gerenciador envia um pacote de ativação para o computador suspenso e depois interrompe o redirecionamento de tráfego para esse computador.  

5.  O computador em suspensão recebe o pacote e é ativado. O computador de envio automaticamente tenta novamente a conexão e desta vez, o computador está ativo e pode responder.  

 Proxy de ativação tem os seguintes pré-requisitos e limitações:  

> [!IMPORTANT]  
>  Se você dispõe de uma equipe separada responsável pela infraestrutura e pelos serviços de rede, notifique e inclua essa equipe durante o período de avaliação e teste. Por exemplo, em uma rede que usa o controle de acesso de rede 802.1X, o proxy de ativação não funciona e pode interromper o serviço de rede. Além disso, o proxy de ativação pode fazer com que algumas ferramentas de monitoramento de rede gerem alertas quando detectam o tráfego para ativar outros computadores.  

-   Os clientes com suporte são Windows 7, 8 do Windows, Windows Server 2008 R2, Windows Server 2012.  

-   Não há suporte para sistemas operacionais convidados executados em uma máquina virtual.  

-   Os clientes devem ser habilitados para proxy de ativação usando as configurações do cliente. Embora a operação de proxy de ativação não dependa de inventário de hardware, os clientes não informam a instalação do proxy de ativação a menos que estejam habilitados para inventário de hardware e tenham enviado pelo menos um inventário de hardware.  

-   Adaptadores de rede (e possivelmente o BIOS) devem ser habilitados e configurados para pacotes de ativação. Se o adaptador de rede não estiver configurado para pacotes de ativação ou se essa configuração estiver desabilitada, o Configuration Manager vai configurá-la e habilitá-la automaticamente em um computador ao receber a configuração do cliente para habilitar o proxy de ativação.  

-   Se um computador tiver mais de um adaptador de rede, não será possível configurar qual adaptador usar para o proxy de ativação; a escolha é não determinista. No entanto, o adaptador escolhido é registrado no arquivo SleepAgent_<DOMAIN\>@SYSTEM_0.log.  

-   A rede deve permitir solicitações de eco ICMP (pelo menos dentro da sub-rede). Não é possível configurar o intervalo de 5 segundos usado para enviar os comandos de ping ICMP.  

-   A comunicação é descriptografada e não autenticada e não há suporte para IPsec.  

-   Não há suporte para as seguintes configurações de rede:  

    -   802.1 X com autenticação de porta  

    -   Redes sem fio  

    -   Comutadores de rede que conectam endereços MAC a portas específicas  

    -   Redes somente IPv6  

    -   Durações de concessão de DHCP inferior a 24 horas  

Se você desejar ativar computadores para instalação de software agendada, deverá configurar todos os sites primários para usar pacotes de ativação.  

 Para usar proxy de ativação, você deve implantar as configurações de cliente do proxy de ativação do Gerenciamento de Energia, além de configurar o site primário.  

Você também deve decidir se pretende usar pacotes de difusão para sub-rede, ou pacotes unicast, e que número da porta UDP usar. Por padrão, pacotes de ativação profissionais são transmitidos usando a porta UDP 9, mas para ajudar a aumentar a segurança, você pode selecionar uma porta alternativa para o site se essa porta alternativa tiver suporte para roteadores e firewalls intermediários.  

### <a name="choose-between-unicast-and-subnet-directed-broadcast-for-wake-on-lan"></a>Escolha entre as transmissões unicast e de sub-rede para Wake on LAN  
 Se você escolher ativar computadores enviando pacotes de ativação tradicionais, deve decidir se quer transmitir pacotes unicast ou pacotes de transmissão direcionados à sub-rede. Se você utilizar proxy de ativação, deverá usar pacotes unicast. Caso contrário, use a tabela a seguir para ajudá-lo a determinar qual método de transmissão escolher.  

|Método de transmissão|Vantagem|Desvantagem|  
|-------------------------|---------------|------------------|  
|Unicast|Solução mais segura do que transmissões direcionadas a sub-rede porque o pacote é enviado diretamente a um computador, em vez de a todos os computadores de uma sub-rede.<br /><br /> Pode não ser necessário reconfigurar os roteadores (talvez seja necessário configurar o cache do ARP).<br /><br /> Consome menos largura de banda de rede de transmissões de difusão direcionadas à sub-rede.<br /><br /> Compatível com IPv4 e IPv6.|Pacotes de ativação não encontram computadores de destino que alteraram seu endereço de sub-rede após o último agendamento de inventário de hardware.<br /><br /> Talvez seja necessário configurar os comutadores para encaminhar pacotes UDP.<br /><br /> Alguns adaptadores de rede podem não responder a pacotes de ativação em todos os estados de suspensão quando usam unicast como o método de transmissão.|  
|Transmissão direcionada à sub-rede|Taxa de sucesso superior do que unicast se houver computadores que mudam frequentemente de endereço IP na mesma sub-rede.<br /><br /> Nenhuma reconfiguração de comutador é necessária.<br /><br /> Alta taxa de compatibilidade com adaptadores de computador para todos os estados de suspensão, porque as transmissões direcionadas à sub-rede eram o método de transmissão original para o envio de pacotes de ativação.|Solução menos segura do que usar unicast porque um invasor pode enviar fluxos contínuos de solicitações de eco ICMP por meio de um endereço de origem falso para o endereço de transmissão direcionado. Isso faz com que todos os hosts respondam a esse endereço de origem. Quando os roteadores são configurados para permitir transmissões direcionadas à sub-rede, a configuração adicional é recomendada por razões de segurança:<br /><br /> -   Configure os roteadores para permitir somente transmissões direcionadas a IP do servidor do site do Configuration Manager usando um número da porta UDP especificado.<br />-   Configure o Configuration Manager para usar o número da porta não padrão especificado.<br /><br /> Pode ser necessário reconfigurar todos os roteadores intermediários para habilitar transmissões direcionadas a sub-redes.<br /><br /> Consome mais largura de banda de rede que as transmissões em unicast.<br /><br /> Compatível somente com IPv4. Não há suporte para IPv6.|  

> [!WARNING]  
>  Há riscos de segurança associados com transmissões direcionadas a sub-redes: Um invasor pode enviar fluxos contínuos de eco ICMP (Internet Control Message Protocol) de um endereço de origem falsificado para o endereço de transmissão direcionado, o que faz com que todos os hosts respondam àquele endereço de origem. Esse tipo de ataque de negação de serviço é comumente chamado de ataque smurf e é geralmente mitigado não permitindo transmissões direcionadas a sub-redes.



<!--HONumber=Dec16_HO3-->


