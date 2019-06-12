---
title: Como criar planos de implantação
titleSuffix: Configuration Manager
description: Um guia de instruções para a criação de planos de implantação na área de trabalho de análise.
ms.date: 06/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: b65a700f5c9cdf3225dfb2ecd3c48d76119110f2
ms.sourcegitcommit: 0bd336e11c9a7f2de05656496a1bc747c5630452
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66834920"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>Como criar planos de implantação na área de trabalho de análise

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Este artigo fornece as etapas para criar um plano de implantação na área de trabalho de análise. Antes de começar, primeiramente [Saiba mais sobre planos de implantação](/sccm/desktop-analytics/about-deployment-plans).

Siga as etapas neste artigo para usar a análise de área de trabalho para criar um plano de implantação do Windows 10.

1. Abra o [portal de análise de área de trabalho](https://aka.ms/m365aprod). Usar credenciais que tenham pelo menos **colaboradores do espaço de trabalho** permissões.  

2. Selecione **planos de implantação** no grupo gerenciar.  

3. No **planos de implantação** painel, selecione **criar**.  

4. No **criar plano de implantação** painel, defina as seguintes configurações:  

    - **Nome**: Um nome exclusivo para o plano de implantação  

    - **Produtos e versões**: Escolha qual versão do Windows 10 para implantar. A Microsoft recomenda a criação de planos de implantação que usam a versão mais recente.  

    - **Grupos de dispositivos**: Selecione um ou mais grupos e, em seguida, selecione **definido como grupos de destino**. Grupos com **SCCM** como a fonte são coleções sincronizadas do Configuration Manager.  

    - **Regras de preparação**: Essas regras ajudam a determinar quais dispositivos está qualificado para atualização.  

    - **Data de conclusão**: Escolha a data pelo qual Windows devem ser totalmente implantada para todos os dispositivos de destino.  

5. Selecione **Criar**. O novo plano é exibida na lista de planos de implantação ao seu que está sendo processado. Para acelerar o processamento, solicite uma atualização de dados sob demanda. Para obter mais informações, consulte [perguntas frequentes sobre análise de área de trabalho](/sccm/desktop-analytics/faq##can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

6. Abra o plano de implantação, selecionando seu nome.  

7. No menu de plano de implantação, nos **preparação** grupo, selecione **identificar importância**.  

    1. Sobre o **aplicativos** , selecione para mostrar apenas **não revisado** ativos.  

    2. Selecione cada aplicativo e, em seguida, selecione **editar**. Você pode selecionar mais de um aplicativo para editar ao mesmo tempo.  

    3. Escolha um nível de importância do **importância** lista. Se quiser que a área de trabalho de análise para validar o aplicativo durante o piloto, selecione **crítica** ou **importante**. Ele não valida os aplicativos marcados como **importante não**. Considere a [riscos de compatibilidade](/sccm/desktop-analytics/compat-risk) e outras informações de plano ao se atribuírem níveis de importância.  

        Ao se atribuírem níveis de importância, você também pode escolher o decisão de atualização.  

    4. Selecione **salvar** ao concluir.  

8. No menu de plano de implantação, nos **preparação** grupo, selecione **identificar piloto**.  

    1. Examine os dispositivos recomendados para o piloto.  

    2. Selecione cada dispositivo e selecione **adicionar ao projeto-piloto**. Se discordar com a recomendação, selecione **substituir**.  

        Para obter mais informações sobre como a área de trabalho de análise torna essas recomendações, selecione o ícone de informações no canto superior direito dos **Identify piloto** painel.



### <a name="next-steps"></a>Próximas etapas

Avance para o próximo artigo para implantar em dispositivos piloto.
> [!div class="nextstepaction"]  
> [Implantar o piloto](/sccm/desktop-analytics/deploy-pilot)  
