---
title: Ativos na análise da área de trabalho
titleSuffix: Configuration Manager
description: Saiba mais sobre dispositivos, aplicativos, os aplicativos do Office, suplementos do Office e as macros do Office na área de trabalho de análise.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 149c5f2a4469a353c6dce6fde86527ca95518484
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754544"
---
# <a name="assets-in-desktop-analytics"></a>Ativos na análise da área de trabalho 

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Depois que dispositivos relatam dados para análise de área de trabalho, ele fornece um inventário de ativos a seguir:
- Dispositivos  
- Drivers de hardware  
- Aplicativos instalados  
- Aplicativos do Office  
- Suplementos do Office  
- Macros do Office  

No portal do serviço, selecione **ativos** no menu de análise de área de trabalho.


## <a name="devices"></a>Dispositivos

O **dispositivos** guia exibe informações importantes sobre todos os dispositivos em sua organização que podem ser registrados para análise de área de trabalho. Você pode classificar qualquer coluna ou filtro para valores específicos.

> [!NOTE]  
> Se o painel não está relatando o número de dispositivos que você espera para o seu ambiente, consulte [solução de problemas de análise de área de trabalho](/sccm/desktop-analytics/troubleshooting).  



## <a name="apps"></a>Aplicativos

O **aplicativos** guia instalado mostra todos os aplicativos que o serviço detecta nos seus dispositivos Windows.

**Vale a pena observar** aplicativos são instalados em mais de 2% de dispositivos registrados. <!--You can change the threshold of "noteworthy" by {doing something}.--> 

Configurar o **importância** de aplicativos, definindo uma das seguintes categorias:

- Crítico
- Importante
- Ignorar
- Não revisado

Selecione o aplicativo na lista e, em seguida, selecione **editar**. Essa ação exibe os detalhes para o aplicativo. Selecione o **importância** menu suspenso e defina um valor. Você também pode atribuir um **proprietário**. Se você fizer alterações, selecione **salvar**. 


## <a name="office-apps"></a>Aplicativos do Office

O **aplicativos do Office** guia é semelhante à guia aplicativos. Ela mostra apenas os aplicativos como Microsoft Word ou Excel, e não há nenhuma categorização ou contagem digno de nota. Defina a importância e o proprietário para aplicativos do Office da mesma forma que com outros aplicativos.


## <a name="office-add-ins"></a>Suplementos do Office

O **suplementos do Office** guia mostra que dão suporte a ferramentas, por exemplo, a proteção de informações do Microsoft Azure ou as ferramentas de análise. Essa guia é semelhante à guia aplicativos, e inclui a contagem digno de nota. Defina a importância e o proprietário, assim como acontece com aplicativos. 


## <a name="office-macros"></a>Macros do Office

O **macros do Office** guia mostra se todos os dispositivos têm todos os arquivos que podem incluir macros acessados recentemente. 

<!-- (For a detailed list of these file types, see [File formats supported in the 2007 Office system (corrected)](https://blogs.technet.microsoft.com/office_resource_kit/2009/04/04/file-formats-supported-in-the-2007-office-system-corrected/) at the Office IT Pro blog.)
 -->

> [!NOTE]  
> Se você também usar o [Readiness Toolkit](https://aka.ms/readinesstoolkit) para suplementos do Office e o Visual Basic para macros Applications (VBA), essa guia também exibe dados adicionais a partir desses dispositivos. 
> 
> Você não precisa usar o Readiness Toolkit para usar a análise de área de trabalho.  



## <a name="next-steps"></a>Próximas etapas

- [Saiba mais sobre planos de implantação de área de trabalho de análise](/sccm/desktop-analytics/about-deployment-plans)  

- [Saiba mais sobre atualizações de segurança e de recurso](/sccm/desktop-analytics/about-updates)  

