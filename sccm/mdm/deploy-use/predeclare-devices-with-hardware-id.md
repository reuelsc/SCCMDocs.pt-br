---
title: "Pré-declarar dispositivos com número de série do iOS ou IMEI"
description: "Pré-declare dispositivos corporativos com o número de série do iOS ou IMEI deles."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddb4c68e-e7f7-475a-89e2-7379a86e44c4
caps.latest.revision: 3
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6cd640085e90b2945326e3fa942ae9bd7b8f7e24
ms.openlocfilehash: 2550fef062b5ef508e4c0492a5a9c63ffcb9084a

---
# <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Pré-declarar dispositivos com número de série do iOS ou IMEI

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode identificar os dispositivos corporativos importando seus números IMEI (identidade internacional de equipamento móvel) ou números de série do iOS. Você pode carregar um arquivo .csv (valores separados por vírgula) que contém os números IMEI do dispositivo ou inserir manualmente as informações sobre o dispositivo.  As informações importadas definirão a **Propriedade** dos dispositivos que registram como "**Corporativo**" nas listas de dispositivos. Uma licença do Intune ainda é necessária para cada usuário que acessa o serviço.  

## <a name="predeclare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>Pré-declarar dispositivos corporativos com número de série do iOS ou IMEI

1.  No console do Configuration Manager, navegue até Ativos e Conformidade > Visão geral > Todos os Dispositivos Pertencentes à Empresa > Dispositivos pré-declarados > e, em seguida, clique em Adicionar dispositivos pré-declarados. O assistente de Dispositivos pré-declarados é aberto.
2.  Especifique como você deseja adicionar as informações do dispositivo:
     -  Carregar um arquivo .csv que contém os números IMEI e os detalhes
     -  Adicione manualmente os números IMEI e os detalhes. Para inserir manualmente as informações, digite o número IMEI ou o número de série do iOS e os detalhes dos dispositivos.

      Para arquivos carregados, navegue até o arquivo .csv que contém informações para pré-declarar dispositivos corporativos. O arquivo deve ter o seguinte formato, exceto a linha superior que foi fornecida apenas para fins de orientação. Cada linha deve conter um número IMEI ou o número de série do iOS. Somente os números de série de dispositivos iOS podem ser pré-declarados; use o número IMEI para outras plataformas de dispositivo. Esta tabela contém dados de exemplo:
      | IMEI #  | Nº de série do iOS #  | Sistema operacional | Detalhes |
      | :------------ |:---------------|:-----|:-----|
      | 123456789012345    |   | WINDOWS | Dispositivo Windows de propriedade da empresa|
      |       | A1B2C3D4E5C6 |   iOS |  Dispositivo iOS de propriedade da empresa|
      | 223456789012345 | E6D5C4B3A210 |   iOS |    Outro dispositivo iOS|
      | 323456789012345 |        |   iOS |  Um terceiro dispositivo iOS|
      | 123456789012346 |         |   Android |     Dispositivo Android de propriedade da empresa|

    Não inclua uma linha de cabeçalho no seu arquivo .csv. O exemplo acima inclui um cabeçalho apenas para fins de esclarecimento.

    **As colunas aceitam os seguintes valores:**    
      - Coluna 1: número IMEI sem espaços
      - Coluna 2: número de série do iOS
      - Coluna 3: o sistema de operacional do dispositivo:
         - IOS – todos os dispositivos iOS
         - WINDOWS – inclui Windows Phone e Windows 10 Mobile e computadores Windows
         - ANDROID – Todos os dispositivos Android
      - Coluna 4: detalhes (opcional) – informações de dispositivo adicionais exibidas no console do Configuration Manager. Limite de 1024 caracteres.

    Clique em **Avançar**.

3. Examine os resultados da importação do arquivo. Se um número de dispositivo foi importado anteriormente, o Configuration Manager exibe os **Detalhes** dos dispositivos e da substituição. Selecione os dispositivos cujos detalhes você deseja substituir. Os detalhes do dispositivo só podem ser modificados importando novamente a identificação do dispositivo ou o número de série. Clique em **Avançar** para continuar ou em **Voltar** para preservar os detalhes atualizados e conclua o assistente.

4. Se a importação incluir números de série do iOS, será necessário atribuir esses dispositivos a um perfil de registro. Selecione **Perfil de Registro para Atribuir** na lista de perfis disponíveis e clique em **Avançar**.

5. Clique em **Avançar** para exibir o Resumo e, em seguida, conclua o assistente.



<!--HONumber=Nov16_HO1-->


