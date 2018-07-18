---
title: Habilitar o Lookout MTD no Intune
description: Habilite o Lookout MTD (defesa contra ameaças móveis) no portal do Microsoft Intune.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7e4ada34-63bf-4b9f-8246-31816aa44196
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 179aae5fdbd8d6c09a34dca6dd01437d5f61f7b8
ms.sourcegitcommit: 0a4556820fabe004d45a82b0ee1176f6891ac9f0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2018
ms.locfileid: "37949587"
---
# <a name="enable-lookout-mtd-connection-in-the-intune-admin-console"></a>Habilitar a conexão com o Lookout MTD no console do administrador do Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo mostra como habilitar a conexão com o Lookout MTD (defesa contra ameaças móveis) no Microsoft Intune. Você já deve ter configurado o Conector do Intune no console do Lookout antes de realizar essa etapa. Siga as etapas descritas em [Configurar sua assinatura com a defesa contra ameaças móveis do Lookout](set-up-your-subscription-with-lookout.md), caso você ainda não tenha feito isso.



## <a name="enable-the-lookout-mtd-connector"></a>Habilitar o conector do Lookout MTD

1. Acesse o [portal do Azure](https://portal.azure.com) e entre com suas credenciais do Intune. Depois que você entrar com êxito, o **Painel do Azure** será exibido.  

2. No **Painel do Azure**, escolha **Todos os serviços** no menu à esquerda, em seguida, digite **Intune** no filtro da caixa de texto.  

3. Escolha **Intune**. O **Painel do Intune** será aberto.  

4. No **Painel do Intune**, escolha **Conformidade do dispositivo** e selecione **Defesa Contra Ameaças Móveis** na seção **Instalação**.  

5. No painel **Defesa Contra Ameaças Móveis**, escolha **Adicionar**.  

6. Escolha **Lookout** como o **Conector de Defesa Contra Ameaças Móveis a ser instalado** na lista suspensa.  

7. Habilite as opções de alternância de acordo com os requisitos da sua organização.  



## <a name="mtd-toggle-options"></a>Opções de alternância de MTD

Você pode decidir quais opções de alternância de MTD você precisa habilitar de acordo com os requisitos da sua organização. Aqui estão mais detalhes:

- **Conectar dispositivos Android 4.1 ou superiores à MTD do Lookout for Work**: quando você habilitar essa opção, os dispositivos Android 4.1 ou superiores poderão relatar riscos de segurança para o Intune.  
    - **Marcar como não compatível, se nenhum dado for recebido**: se o Intune não receber nenhum dado sobre um dispositivo nessa plataforma do Lookout, considere o dispositivo como não compatível.  

- **Conectar dispositivos iOS 8.0 ou superiores à MTD do Lookout for Work**: quando você habilitar essa opção, os dispositivos iOS 8.0 ou superiores poderão relatar riscos de segurança para o Intune.
    - **Marcar como não compatível, se nenhum dado for recebido**: se o Intune não receber nenhum dado sobre um dispositivo nessa plataforma do Lookout, considere o dispositivo como não compatível.  

> [!TIP]  
> Você pode ver o **Status de conexão** e o horário da **Última sincronização** entre o Intune e o Lookout no painel Defesa Contra Ameaças Móveis.



## <a name="next-steps"></a>Próximas etapas
Isso conclui a instalação da integração do Lookout e do Intune. As próximas etapas para implementar essa solução envolvem a implantação de [Aplicativos Lookout for Work](configure-and-deploy-lookout-for-work-apps.md) e a configuração da política de [conformidade](enable-device-threat-protection-rule-compliance-policy.md).

>[!IMPORTANT]
> Você *deve* configurar o aplicativo Lookout for Work antes de criar regras de política de conformidade e configurar o acesso condicional. Essa ação garante que o aplicativo esteja pronto e disponível para ser instalado pelos usuários finais antes que eles possam ter acesso ao email ou outros recursos da empresa.

[Configurar o aplicativo Lookout for Work](configure-and-deploy-lookout-for-work-apps.md)
