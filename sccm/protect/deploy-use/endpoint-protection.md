---
title: Endpoint Protection
titleSuffix: Configuration Manager
description: Saiba como gerenciar as políticas antimalware e a segurança do Firewall do Windows para clientes.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 160713fe480b0a47c2ad57376c4a1dccdbfb00b1
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53418944"
---
# <a name="endpoint-protection"></a>Endpoint Protection

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Endpoint Protection gerencia políticas antimalware e a segurança do Firewall do Windows para computadores cliente na sua hierarquia do Configuration Manager.  

> [!IMPORTANT]  
>  Você deve ter licença para usar o Endpoint Protection para gerenciar clientes na sua hierarquia do Configuration Manager.  

 Ao usar o Endpoint Protection com o Configuration Manager, você tem os seguintes benefícios:  

-   Configure políticas antimalware, configurações do Firewall do Windows e gerencie a Proteção Avançada contra Ameaças do Windows Defender para alguns grupos de computadores  
-   Use as atualizações de software do Configuration Manager para baixar os arquivos de definição antimalware mais recentes para manter os computadores cliente atualizados  
-   Envie notificações por email, use o monitoramento no console e exiba relatórios. Essas ações informam os usuários administrativos quando um malware é detectado nos computadores cliente.  

A partir dos computadores Windows 10 e Windows Server 2016, o Windows Defender já vem instalado. Para esses sistemas operacionais, um cliente de gerenciamento para Windows Defender é instalado durante a instalação do cliente do Configuration Manager. No Windows 8.1 e em computadores mais antigos, o Endpoint Protection é instalado com o cliente do Configuration Manager. O Windows Defender e o cliente do Endpoint Protection têm os seguintes recursos:  

-   Detecção e correção de malware e spyware  
-   Detecção e correção de rootkits  
-   Avaliação de vulnerabilidades crítica e atualizações automáticas de mecanismos e definições  
-   Detecção de vulnerabilidade de rede por meio do Sistema de Inspeção de Rede  
-   Integração com o Cloud Protection Service para relatar a presença de malware à Microsoft. Ao optar por fazer parte desse serviço, o cliente do Endpoint Protection ou o Windows Defender baixará as definições mais recentes do Centro de Proteção contra Malware quando for detectado malware não identificado em um computador.  

> [!NOTE]  
>  O cliente do Endpoint Protection pode ser instalado em um servidor que executa o Hyper-V e em máquinas virtuais convidadas com sistemas operacionais com suporte. Para evitar o uso excessivo de CPU, as ações do Endpoint Protection têm um atraso aleatório interno para que os serviços de proteção não sejam executados simultaneamente.  

 Além disso, você gerencia as configurações do Firewall do Windows com o Endpoint Protection no console do Configuration Manager.  

 [Cenário de exemplo: usar o System Center Endpoint Protection para proteger os computadores contra malware no System Center Configuration Manager](scenarios-endpoint-protection.md) Endpoint Protection e no Firewall do Windows.  


## <a name="managing-malware-with-endpoint-protection"></a>Gerenciando malware com o Endpoint Protection  
 O Endpoint Protection no Configuration Manager permite que você crie políticas antimalware que contêm configurações para o cliente do Endpoint Protection. Implantar essas políticas antimalware nos computadores cliente. Em seguida, monitore a conformidade no nó **Status do Endpoint Protection** em **Segurança** no workspace **Monitoramento**. Use também os relatórios do Endpoint Protection no nó **Relatórios**.  

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


 Para obter mais informações, consulte [Como criar e implantar políticas do Firewall do Windows para o Endpoint Protection](create-windows-firewall-policies.md).  


## <a name="windows-defender-advanced-threat-protection"></a>Proteção Avançada contra Ameaças do Windows Defender

O Endpoint Protection gerencia e monitora a ATP (Proteção Avançada contra Ameaças) do Windows Defender. O serviço Windows Defender ATP ajuda as empresas a detectar, investigar e responder a ataques avançados contra a rede corporativa. Para obter mais informações, consulte [Proteção Avançada contra Ameaças do Windows Defender](windows-defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Fluxo de trabalho do Endpoint Protection  
 Use o diagrama a seguir para ajudá-lo a entender o fluxo de trabalho para implementar o Endpoint Protection em sua hierarquia do Configuration Manager.  

 ![Fluxo de trabalho do Endpoint Protection](../media/Endpoint-Protection-Workflow.gif)  



## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Cliente do Endpoint Protection para computadores Mac e servidores Linux  

> [!Important]  
> O suporte do SCEP (System Center Endpoint Protection) para Mac e Linux (todas as versões) será encerrado em 31 de dezembro de 2018. A disponibilidade de novas definições de vírus do SCEP para Mac e do SCEP para Linux poderá ser descontinuada após o encerramento do suporte. Para obter mais informações, consulte a [postagem no blog sobre o encerramento do suporte](https://go.microsoft.com/fwlink/?linkid=870182).  

 O System Center Endpoint Protection inclui um cliente do Endpoint Protection para Linux e para computadores Mac. O Configuration Manager não é fornecido a esses clientes. Baixe os seguintes produtos do [Centro de Serviços de Licenciamento por Volume da Microsoft](https://www.microsoft.com/licensing/servicecenter/default.aspx):  

-   System Center Endpoint Protection para Mac  

-   System Center Endpoint Protection para Linux  


> [!Note]  
>  Você deve ser um cliente de Licença de volume da Microsoft para baixar os arquivos de instalação do Endpoint Protection para Linux e Mac.  

 Esses produtos não podem ser gerenciados no console do Configuration Manager. Um pacote de gerenciamento do System Center Operations Manager é fornecido com os arquivos de instalação, o que permite que você gerencie o cliente para Linux.  

### <a name="how-to-get-the-endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Como obter o cliente do Endpoint Protection para computadores Mac e servidores Linux

Use as etapas a seguir para baixar o arquivo de imagem que contém o software cliente do Endpoint Protection e a documentação para computadores Mac e servidores Linux.
1. Entre no [Centro de Serviços de Licenciamento por Volume da Microsoft](https://www.microsoft.com/licensing/servicecenter/default.aspx).
2. Selecione a guia **Downloads e Chaves** na parte superior do site.
3. Aplique filtro no produto **System Center Endpoint Protection (branch atual)**.
4. Clique no link **Download**
5. Clique em **Continue**. Você verá vários arquivos, incluindo um denominado: **System Center Endpoint Protection (branch atual – versão 1606) para o sistema operacional Linux e Macintosh OS Multilanguage 32/64 bits 1878 MB ISO**.
6. Para baixar o arquivo, clique no ícone de seta. O nome do arquivo é **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_-3_EptProt_Lin_Mac_MLF_X21-67050.ISO**.

A atualização de janeiro de 2018 (X21-67050) inclui as seguintes versões:

- System Center Endpoint Protection para Mac 4.5.32.0 (suporte para macOS 10.13 High Serra)
- System Center Endpoint Protection para Linux 4.5.20.0 

  Para obter mais informações sobre como instalar e gerenciar clientes do Endpoint Protection em computadores Linux e Mac, use a documentação que acompanha esses produtos. Esta documentação de produto está na pasta **Documentação** do arquivo .ISO.
