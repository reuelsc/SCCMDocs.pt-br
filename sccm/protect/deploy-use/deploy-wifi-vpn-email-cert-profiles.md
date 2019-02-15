---
title: Implantar perfis de Wi-Fi, VPN, email e certificado
titleSuffix: Configuration Manager
description: Saiba como implantar perfis Wi-Fi, VPN, de email e de certificado no System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 63b52b42a9957ed8728d0942988067fef2be6271
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129707"
---
# <a name="deploy-profiles-in-system-center-configuration-manager"></a>Implantar perfis no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os perfis deverão ser implantados em uma ou mais coleções para poderem ser usados.  

 Use a caixa de diálogo **Implantar Perfil Wi-Fi**, **Implantar Perfil VPN**, **Implantar Perfil do Exchange ActiveSync** ou **Implantar Perfil de Certificado** para configurar a implantação desses perfis. Como parte da configuração, defina a coleção na qual o perfil deverá ser implantado e especifique com que frequência esse perfil será avaliado quanto à sua conformidade.  

> [!NOTE]
>  Se você implantar vários perfis de acesso aos recursos da empresa para o mesmo usuário, ocorrerá o seguinte comportamento:  
> 
> - Se uma configuração conflitante contiver um valor opcional, ele não será enviado para o dispositivo.  
>   -   Se uma configuração conflitante contiver um valor obrigatório, o valor padrão será enviado para o dispositivo. Se não houver nenhum valor padrão, o perfil de acesso de recursos de toda a empresa falhará. Por exemplo, se você implantar dois perfis de email para o mesmo usuário e os valores especificados para **Host do Exchange ActiveSync** ou **Endereço de Email** forem diferentes, ambos os perfis de email falharão, pois essas são configurações obrigatórias.  
> 
> - Antes de implantar perfis de certificado, primeiro você deve configurar a infraestrutura e criar perfis de certificado. Para mais informações, consulte os seguintes tópicos:  
> 
>   -   [Configurando infraestrutura de certificado no System Center Configuration Manager](certificate-infrastructure.md)  
> - [Como criar perfis de certificado no System Center Configuration Manager](create-certificate-profiles.md)    
> 
> [!IMPORTANT]
>  Quando uma implantação do perfil VPN é removida, ele não é removido dos dispositivos cliente. Se quiser remover o perfil dos dispositivos, você deverá removê-lo manualmente.

## <a name="deploying--profiles"></a>Implantando perfis  


1.  No console do System Center Configuration Manager, escolha **Ativos e Conformidade**.  

2.  No workspace **Ativos e Conformidade**, expanda **Configurações de Conformidade**, **Acesso aos Recursos da Empresa** e escolha o tipo de perfil apropriado, como **Perfis Wi-Fi**.  

3.  Na lista de perfis, selecione o perfil que você deseja implantar e, na guia **Início**, no grupo **Implantação**, clique em **Implantar**.  

4.  Na caixa de diálogo para implantar perfil, especifique as seguintes informações:  

    -   **Coleção** – Clique em **Procurar** para selecionar a coleção de usuários na qual você deseja implantar o perfil.  

    -   **Gerar um alerta** – Habilite esta opção para configurar um alerta que será gerado se a conformidade do perfil for menor do que um percentual especificado por uma data e uma hora determinadas. Você também pode especificar se deseja que um alerta seja enviado para o System Center Operations Manager.  

    -   -   **Atraso aleatório (horas)**: (somente para perfis de certificado que contêm as configurações do protocolo SCEP) – Especifica uma janela de atraso para evitar o processamento excessivo no Serviço de Registro de Dispositivo de Rede. O valor padrão é **64** horas.  

    -   **Especificar o agendamento de avaliação de conformidade para este perfil <type>** – Especifique o agendamento com base no qual o perfil implantado será avaliado nos computadores cliente. O agendamento poderá ser simples ou personalizado.  

        > [!NOTE]  
        >  O perfil será avaliado por computadores cliente quando o usuário fizer logon.  

5.  Clique em **OK** para fechar a caixa de diálogo e criar a implantação.

### <a name="see-also"></a>Consulte também  

[Como monitorar perfis Wi-Fi, VPN e de email no System Center Configuration Manager](monitor-wifi-email-vpn-profiles.md)

[Como monitorar perfis de certificado no System Center Configuration Manager](monitor-certificate-profiles.md)
