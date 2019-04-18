---
title: Como criar planos de implantação
titleSuffix: Configuration Manager
description: Um guia de instruções para a criação de planos de implantação na área de trabalho de análise.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 35e8e883acafaa1d606d81402b868b8a755d0887
ms.sourcegitcommit: 6f4c2987debfba5d02ee67f6b461c1a988a3e201
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59673455"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>Como criar planos de implantação na área de trabalho de análise 

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Este artigo fornece as etapas para criar um plano de implantação na área de trabalho de análise. Antes de começar, primeiramente [Saiba mais sobre planos de implantação](/sccm/desktop-analytics/about-deployment-plans).

Siga as etapas neste artigo para usar a análise de área de trabalho para criar um plano para implantar o Windows 10 e Office 365 ProPlus. Crie planos de implantação para Windows 10, Office 365 ProPlus ou ambos.

1. Abra o [portal de análise de área de trabalho](https://aka.ms/m365aprod). Usar credenciais que tenham pelo menos **colaboradores do espaço de trabalho** permissões.  

2. Selecione **planos de implantação** no grupo gerenciar.  

3. No **planos de implantação** painel, selecione **criar**.  

4. No **criar plano de implantação** painel, defina as seguintes configurações:  

    - **Nome**: Um nome exclusivo para o plano de implantação  

    - **Produtos e versões**: Escolha quais produtos e versões para implantar. A Microsoft recomenda a criação de planos de implantação para Office e do Windows juntos e usando as versões mais recentes.  

    - **Grupos de dispositivos**: Selecione um ou mais grupos e, em seguida, selecione **definido como grupos de destino**. Grupos com **SCCM** como a fonte são coleções sincronizadas do Configuration Manager.  

    - **Regras de preparação**: Essas regras ajudam a determinar quais dispositivos está qualificado para atualização. 

    - **Data de conclusão**: Escolha a data pelo qual Windows e do Office devem ser totalmente implantados em todos os dispositivos de destino.  

5. Selecione **Criar**. O novo plano é exibida na lista de planos de implantação ao seu que está sendo processado. O processamento pode levar até 48 horas antes de prosseguir para a próxima etapa.   

6. Abra o plano de implantação, selecionando seu nome.  

7. No menu de plano de implantação, nos **preparação** grupo, selecione **identificar importância**.  

    1. Sobre o **aplicativos** , selecione para mostrar apenas **não revisado** ativos.  

    2. Selecione cada aplicativo e, em seguida, selecione **editar**. Você pode selecionar mais de um aplicativo para editar ao mesmo tempo.   

    3. Escolha um nível de importância do **importância** lista. Se quiser que a área de trabalho de análise para validar o suplemento durante o piloto, selecione **crítica** ou **importante**. Ele não valida os suplementos marcados como **importante não**. Considere a [riscos de compatibilidade](/sccm/desktop-analytics/compat-risk) e outras informações de plano ao se atribuírem níveis de importância.  

        Ao se atribuírem níveis de importância, você também pode escolher o decisão de atualização.  

    4. Selecione **salvar** ao concluir.  

    5. Repita essas etapas para o **suplementos do Office**.  

8. No menu de plano de implantação, nos **preparação** grupo, selecione **identificar piloto**.  

    1. Examine os dispositivos recomendados para o piloto.  

    2. Selecione cada dispositivo e selecione **adicionar ao projeto-piloto**. Se discordar com a recomendação, selecione **substituir**.  

        Para obter mais informações sobre como a área de trabalho de análise torna essas recomendações, selecione o ícone de informações no canto superior direito dos **Identify piloto** painel.



### <a name="next-steps"></a>Próximas etapas

Avance para o próximo artigo para implantar em dispositivos piloto.
> [!div class="nextstepaction"]  
> [Implantar o piloto](/sccm/desktop-analytics/deploy-pilot)  
