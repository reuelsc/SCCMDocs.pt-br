---
title: Pré-declarar dispositivos com número de série do iOS ou IMEI
titleSuffix: Configuration Manager
description: Pré-declare dispositivos corporativos com o número de série do iOS ou IMEI deles.
ms.date: 09/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ddb4c68e-e7f7-475a-89e2-7379a86e44c4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 86ef14c871f476df39923e01e47874702271a08d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Pré-declarar dispositivos com número de série do iOS ou IMEI

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode identificar os dispositivos corporativos importando seus números IMEI (identidade internacional de equipamento móvel) ou números de série do iOS. Você pode carregar um arquivo .csv (valores separados por vírgula) que contém os números IMEI do dispositivo ou inserir manualmente as informações sobre o dispositivo.  As informações importadas definirão a **Propriedade** dos dispositivos registrados como **Corporativo** nas listas de dispositivos. Uma licença do Intune ainda é necessária para cada usuário que acessa o serviço.  

Quando você carrega os números de série para dispositivos iOS de propriedade da empresa, eles devem ser combinados com um perfil de registro corporativo. Os dispositivos devem então ser registrados usando o programa de registro do dispositivo (DEP) da Apple ou o Apple Configurator para eles aparecerem como sendo da empresa.

>[!NOTE]
>Dispositivos Android, exceto dispositivos Samsung Knox Standard, devem ter um número de telefone atribuído a eles para serem pré-declarados e registrados como um dispositivo da empresa com um número IMEI.

## <a name="how-to-predeclare-corporate-owned-devices"></a>Como pré-declarar dispositivos corporativos

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Visão Geral** > **Todos os dispositivos de propriedade corporativa** > **Dispositivos pré-declarados**.

2.  Clique em **Criar Dispositivos Pré-declarados**. O assistente Criar Dispositivos Pré-declarados abre.

3.  Escolha como você deseja adicionar as informações do dispositivo:

     -  **Carregar um arquivo CSV contendo o IMEI ou os números de série e os detalhes**

        Para essa opção, clique em **Procurar** para especificar o arquivo .csv que contém as informações para declarar os dispositivos corporativos. O arquivo. csv deve estar formatado corretamente. Para mais informações, confira [Formato para carregar arquivos .csv](#format-for-uploading-csv-files).

     -  **Adicionar manualmente o IMEI ou os números de série e os detalhes**

        Para inserir manualmente as informações, digite o número IMEI ou o número de série do iOS e os detalhes dos dispositivos. Corrija todos os erros ou avisos antes de continuar.

    Clique em **Avançar**.

4. Se você carregou um arquivo. csv, examine os resultados da importação do arquivo. Se um número de dispositivo tiver sido importado anteriormente, o Configuration Manager exibirá os **Detalhes** dos dispositivos e da substituição. Selecione os dispositivos cujos detalhes você deseja substituir. Os detalhes do dispositivo só podem ser modificados importando novamente a identificação do dispositivo ou o número de série.

  Se você optar por inserir manualmente o número, preencha o formulário para os dispositivos que deseja pré-declarar.

  Clique em **Próximo** para continuar.

4. Se sua lista incluir números de série iOS, selecione **Perfil de Registro para Atribuir** na lista de perfis disponíveis e clique em **Avançar**.

5. Clique em **Avançar** para examinar os detalhes e, em seguida, clique em **Avançar** novamente para carregar os dados.

6. Clique em **Fechar** para concluir.

## <a name="format-for-uploading-csv-files"></a>Formato para carregar arquivos .csv

O arquivo .csv que você usa para identificar dispositivos pelo IMEI ou pelo número de série de iOS deve ter o seguinte formato, exceto a linha superior, que é fornecida apenas para orientação. Cada linha deve conter um número de identificação, pode ser um número IMEI ou o número de série do iOS. Para dispositivos iOS, você pode incluir ambos. Os números de IMEI podem ser usados para dispositivos Android, iOS e Windows. Esta tabela contém dados de exemplo:

| Nº do IMEI  | Nº de série do iOS  | Sistema operacional | Detalhes |
|------------ |---------------|-----|-----|
| 123456789012345    |   | WINDOWS | Dispositivo Windows de propriedade da empresa|
|   | A1B2C3D4E5C6 | IOS |  Dispositivo iOS de propriedade da empresa|
| 223456789012345 | E6D5C4B3A210 |   IOS |  Outro dispositivo iOS|
| 323456789012345 |        |   IOS |    Um terceiro dispositivo iOS|
| 123456789012346 |         |   ANDROID |   Dispositivo Android de propriedade da empresa|

Não inclua uma linha de cabeçalho no seu arquivo .csv. O exemplo a seguir mostra os mesmos dados de exemplo no formato CSV:

```
123456789012345,,WINDOWS,Company-owned Windows device
,A1B2C3D4E5C6,IOS,Company-owned iOS device
223456789012345,E6D5C4B3A210,IOS,Another iOS device
323456789012345,,IOS,A third iOS device
123456789012346,,ANDROID,Company-owned Android device
```

As colunas no arquivo .csv aceitam os seguintes valores:

| Coluna 1 | Coluna 2 | Coluna 3 | Coluna 4 |
|---|---|---|---|
|Número IMEI sem espaços | Número de série do iOS | IOS, WINDOWS ou ANDROID | Detalhes do dispositivo opcionais (limite de 1024 caracteres) |
