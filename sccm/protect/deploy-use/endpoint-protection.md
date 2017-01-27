---
title: Endpoint Protection | Microsoft Docs
description: "Saiba como gerenciar políticas antimalware e a segurança do Firewall do Windows para computadores cliente na sua hierarquia do Configuration Manager."
ms.custom: na
ms.date: 01/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
caps.latest.revision: 11
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f66288f1c2e0566d5de8686a005624dd81557563
ms.openlocfilehash: addb315afe3775722a58a16b00d41cbe32a5009c


---
# <a name="endpoint-protection-in-system-center-configuration-manager"></a>Endpoint Protection no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Endpoint Protection no System Center Configuration Manager permite gerenciar políticas antimalware e a segurança do Firewall do Windows para computadores cliente em sua hierarquia do Configuration Manager.  

> [!IMPORTANT]  
>  Você deve ter licença para usar o Endpoint Protection para gerenciar clientes na sua hierarquia do Configuration Manager.  

 Ao usar o Endpoint Protection com o Configuration Manager, você tem os seguintes benefícios:  

-   Configure políticas antimalware, configurações do Firewall do Windows e gerencie a Proteção Avançada contra Ameaças do Windows Defender para alguns grupos de computadores  

-   Use as atualizações de software do Configuration Manager para baixar os arquivos de definição antimalware mais recentes para manter os computadores cliente atualizados  

-   Envie notificações por email, use o monitoramento no console e exiba relatórios para manter usuários administrativos informados quando for detectado malware nos computadores cliente  

Computadores Windows 10 não exigem nenhum cliente adicional para o gerenciamento do Endpoint Protection. No Windows 8.1 e em computadores mais antigos, o Endpoint Protection instala seu próprio cliente além do cliente do Configuration Manager. Endpoint Protection pode gerenciar. O cliente do Endpoint Protection tem os seguintes recursos:  

-   Detecção e correção de malware e spyware  

-   Detecção e correção de rootkits  

-   Avaliação de vulnerabilidades crítica e atualizações automáticas de mecanismos e definições  

-   Detecção de vulnerabilidade de rede por meio do Sistema de Inspeção de Rede  

-   Integração com o Cloud Protection Service para relatar a presença de malware à Microsoft. Ao optar por fazer parte desse serviço, o cliente do Endpoint Protection ou o Windows Defender poderá baixar as definições mais recentes do Centro de Proteção contra Malware quando for detectado malware não identificado em um computador.  

> [!NOTE]  
>  O cliente do Endpoint Protection pode ser instalado em um servidor que executa o Hyper-V e em máquinas virtuais convidadas com sistemas operacionais com suporte. Para evitar o uso excessivo de CPU, as ações do Endpoint Protection têm um atraso aleatório interno para que os serviços de proteção não sejam executados simultaneamente.  

 Além disso, o Endpoint Protection no Configuration Manager permite gerenciar as configurações do Firewall do Windows no console do Configuration Manager.  

 [Cenário de exemplo: usar o System Center Endpoint Protection para proteger os computadores contra malware no System Center Configuration Manager](scenarios-endpoint-protection.md) Endpoint Protection e o Firewall do Windows.  


## <a name="managing-malware-with-endpoint-protection"></a>Gerenciando malware com o Endpoint Protection  
 O Endpoint Protection no Configuration Manager permite que você crie políticas antimalware que contêm configurações para o cliente do Endpoint Protection. Você pode implantar essas políticas antimalware nos computadores cliente e monitorá-los no nó **Status do Endpoint Protection** em **Segurança** no espaço de trabalho **Monitoramento** ou usando relatórios do Configuration Manager.  

 Informações adicionais:  

-   [Como criar e implantar políticas antimalware para o Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md) – Crie, implante e monitore políticas antimalware com uma lista das configurações que você pode definir  

-   [Como monitorar o Endpoint Protection no System Center Configuration Manager](monitor-endpoint-protection.md) – Monitoramento de relatórios de atividade, computadores cliente infectados e muito mais.  

-   [Como gerenciar políticas antimalware e configurações de firewall para o Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-firewall.md) ‑ Remediar malware encontrado em computadores cliente  


## <a name="managing-windows-firewall-with-endpoint-protection"></a>Gerenciando o firewall do Windows com o Endpoint Protection  
 O Endpoint Protection no Configuration Manager fornece gerenciamento básico do Firewall do Windows em computadores cliente. Para cada perfil de rede, você pode definir as seguintes configurações:  

-   Habilitar ou desabilitar o Firewall do Windows.  

-   Bloquear conexões de entrada, incluindo aquelas na lista de programas permitidos.  

-   Notificar o usuário quando o Firewall do Windows bloquear um novo programa.  

> [!NOTE]  
>  O Endpoint Protection dá suporte apenas ao gerenciamento do Firewall do Windows.  


 Para obter mais informações sobre como criar e implantar políticas do Firewall do Windows para o Endpoint Protection, consulte [Como criar e implantar políticas do Firewall do Windows para o Endpoint Protection no System Center Configuration Manager](create-windows-firewall-policies.md).  


## <a name="windows-defender-advanced-threat-protection"></a>Proteção Avançada contra Ameaças do Windows Defender

Começando com a versão 1606 do Configuration Manager (ramificação atual), o Endpoint Protection pode ajudar a gerenciar e monitorar a ATP (Proteção Avançada contra Ameaças) do Windows Defender. A ATP do Windows Defender é um novo serviço que ajudará as empresas a detectar, investigar e responder a ataques avançados em suas redes. Consulte [Proteção Avançada contra Ameaças do Windows Defender](windows-defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Fluxo de trabalho do Endpoint Protection  
 Use o diagrama a seguir para ajudá-lo a entender o fluxo de trabalho para implementar o Endpoint Protection em sua hierarquia do Configuration Manager.  

 ![Fluxo de trabalho do Endpoint Protection](../media/Endpoint-Protection-Workflow.gif)  

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Cliente do Endpoint Protection para computadores Mac e servidores Linux  
 O System Center Endpoint Protection inclui um cliente do Endpoint Protection para Linux e para computadores Mac. Esses clientes não são fornecidos com o Configuration Manager. Você precisa baixar os seguintes produtos do [Centro de Serviços de Licenciamento por Volume da Microsoft](https://www.microsoft.com/licensing/servicecenter/default.aspx).  

-   System Center 2012 Endpoint Protection para Mac  

-   System Center 2012 Endpoint Protection para Linux  


> [!IMPORTANT]  
>  Você deve ser um cliente de Licença de volume da Microsoft para baixar os arquivos de instalação do Endpoint Protection para Linux e Mac.  

 Esses produtos não podem ser gerenciados no console do Gerenciador de Configurações. No entanto, um pacote de gerenciamento do System Center Operations Manager é fornecido com os arquivos de instalação, o que permite que você gerencie o cliente para Linux usando o Operations Manager.  

### <a name="how-to-get-the-endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Como obter o cliente do Endpoint Protection para computadores Mac e servidores Linux

Use as etapas a seguir para baixar o arquivo de imagem que contém o software cliente do Endpoint Protection e a documentação para computadores Mac e servidores Linux.
1. Faça logon no [Centro de Serviços de Licenciamento por Volume da Microsoft](https://www.microsoft.com/licensing/servicecenter/default.aspx).
2. Selecione a guia **Downloads e Chaves** na parte superior do site.
3. Aplique filtro no produto **System Center Endpoint Protection (branch atual)**.
4. Clique no link **Download**
5. Clique em **Continue**. Você verá vários arquivos, incluindo um denominado: **System Center Endpoint Protection (branch atual – versão 1606) para o sistema operacional Linux e o sistema operacional Macintosh Multilanguage 32/64 bits 1507 MB ISO**.
6. Clique no ícone de seta para baixar o arquivo. O nome do arquivo é **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_EptProt_Lin_Mac_MLF_X21-30777.ISO**.

 Para obter mais informações sobre como instalar e gerenciar clientes do Endpoint Protection em computadores Linux e Mac, use a documentação que acompanha esses produtos, que está localizado na pasta **Documentação** .



<!--HONumber=Jan17_HO3-->


