---
title: "Localização de fonte de conteúdo | Microsoft Docs"
description: "Saiba mais sobre as configurações do System Center Configuration Manager que permitem que os clientes localizem conteúdo em uma rede lenta."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 70b5cbc0-64ba-49bd-8b34-fb4c09b2b95b
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1a4a9da88caba55d9e340c7fb1f31f4e3b957f3e
ms.openlocfilehash: b0f54daecfc3e958d3196f3f0b08606725d86c39

---
# <a name="content-source-location-scenarios-in-system-center-configuration-manager"></a>Cenários de local de origem de conteúdo no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Nas versões anteriores à 1610, o System Center Configuration Manager dá suporte a várias configurações que se combinam para definir como e onde os clientes devem encontrar conteúdo quando estão em uma rede lenta. As combinações possíveis afetam o local do conteúdo que os clientes usam e se eles podem usar um local de fallback com êxito quando uma origem preferencial do conteúdo não está disponível.  

> [!IMPORTANT]  
> **Se seus sites executam a versão 1511, 1602 ou 1606**, as informações neste tópico aplicam-se à sua infraestrutura. Consulte também [Grupos de limites para as versões 1511, 1602 e 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) para obter informações específicas para grupos de limites com essas versões do Configuration Manager.
>
> **Se seus sites executam a versão 1610 ou posterior**, use as informações nos [Grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups) para entender como os clientes localizam pontos de distribuição com conteúdo disponível.





**As três configurações a seguir definem o comportamento quando os clientes solicitam conteúdo:**

-  **Permitir local de origem de fallback para conteúdo** (habilitada ou não habilitada): essa é uma opção que você pode habilitar na guia Grupos de Limites de um ponto de distribuição.  Isso permite que o cliente use um ponto de distribuição configurado como um local de fallback quando o conteúdo não estiver disponível em um ponto de distribuição preferencial.  

 - **Comportamento de implantação para velocidade de conexão de rede**: cada implantação é configurada com um dos seguintes comportamentos a ser usado quando a conexão com o ponto de distribuição estiver lenta:  

    -   **Baixar conteúdo do ponto de distribuição e executá-lo localmente**  

    -   **Não baixar conteúdo**: essa opção é usada apenas quando um cliente usa um local de fallback para obter conteúdo  

    A velocidade da conexão para um ponto de distribuição é configurada na guia Referências do grupo de limites e é específica a esse grupo de limites.  

 -  **Distribuição de pacote sob demanda** (a pontos de distribuição preferenciais): isso é habilitado quando você escolhe a opção **Distribuir o conteúdo deste pacote para os pontos de distribuição preferenciais** na guia Configurações de Distribuição das propriedades de um pacote ou aplicativos. Quando habilitada, essa opção orienta o Configuration Manager a copiar automaticamente o conteúdo para um ponto de distribuição preferencial que ainda não tem o conteúdo depois que um cliente solicita esse conteúdo desse ponto de distribuição.  


 **Os seguintes requisitos se aplicam a todos os cenários:**


-   O conteúdo está disponível em um ponto de distribuição de fallback  

-   Os pontos de distribuição estão online e acessíveis  


## <a name="scenario-1"></a>Cenário 1  
 Aplica-se na seguinte configuração:  

-   **O conteúdo está disponível em um ponto de distribuição preferencial**  

-   **Permitir fallback**: não habilitada  

-   **Comportamento de implantação para rede lenta**: qualquer configuração  


**Detalhes:** (a configuração de distribuição de pacote sob demanda não é relevante nesse cenário)  

1.  O cliente envia uma solicitação de conteúdo para o ponto de gerenciamento.  

2.  Uma lista do local do conteúdo é devolvida ao cliente do ponto de gerenciamento com os pontos de distribuição preferenciais que contêm o conteúdo.  

3.  O cliente baixa o conteúdo de um ponto de distribuição preferencial na lista.  

## <a name="scenario-2"></a>Cenário 2  
 A configuração é a seguinte:  

-   **O conteúdo está disponível em um ponto de distribuição preferencial**  

-   **Permitir fallback**: habilitada  

-   **Comportamento de implantação para rede lenta**: não baixar conteúdo  


**Detalhes:** (a configuração de distribuição de pacote sob demanda não é relevante nesse cenário)  

1.  O cliente envia uma solicitação de conteúdo para o ponto de gerenciamento. O cliente inclui um sinalizador com a solicitação que indica que pontos de distribuição de fallback são permitidos.  

2.  Uma lista do local do conteúdo é devolvida ao cliente do ponto de gerenciamento com os pontos de distribuição preferenciais e os pontos de distribuição de fallback que contêm o conteúdo.  

3.  O cliente baixa o conteúdo de um ponto de distribuição preferencial na lista.  

## <a name="scenario-3"></a>Cenário 3:  
 A configuração é a seguinte:  

-   **O conteúdo está disponível em um ponto de distribuição preferencial**  

-   **Permitir fallback**: habilitada  

-   **Comportamento de implantação para rede lenta**: baixar e instalar conteúdo  


**Detalhes:** (a configuração de distribuição de pacote sob demanda não é relevante nesse cenário)  

1.  O cliente envia uma solicitação de conteúdo para o ponto de gerenciamento. O cliente inclui um sinalizador com a solicitação que indica que pontos de distribuição de fallback são permitidos.  

2.  Uma lista do local do conteúdo é devolvida ao cliente do ponto de gerenciamento com os pontos de distribuição preferenciais e os pontos de distribuição de fallback que contêm o conteúdo.  

3.  O cliente baixa o conteúdo de um ponto de distribuição preferencial na lista.  

## <a name="scenario-4"></a>Cenário 4  
 A configuração é a seguinte:  

-   **O conteúdo não está disponível em um ponto de distribuição preferencial**  

-   **Distribuir o conteúdo deste pacote para os pontos de distribuição preferenciais** não está habilitada  

-   **Permitir fallback**: não habilitada  

-   **Comportamento de implantação para rede lenta**: qualquer configuração  


**Detalhes:**  

1.  O cliente envia uma solicitação de conteúdo para o ponto de gerenciamento  

2.  Uma lista do local do conteúdo é devolvida ao cliente do ponto de gerenciamento com os pontos de distribuição preferenciais que têm o conteúdo. Não há pontos de distribuição preferenciais na lista.  

3.  O cliente falha com a mensagem **O conteúdo não está disponível** e entra no modo de repetição. Uma nova solicitação de conteúdo é iniciada a cada hora  

## <a name="scenario-5"></a>Cenário 5  
 A configuração é a seguinte:  

-   **O conteúdo não está disponível em um ponto de distribuição preferencial**  

-   **Distribuir o conteúdo deste pacote para os pontos de distribuição preferenciais** não está habilitada  

-   **Permitir fallback**: habilitada  

-   **Comportamento de implantação para rede lenta**: não baixar conteúdo  


**Detalhes:**  

1.  O cliente envia uma solicitação de conteúdo para o ponto de gerenciamento. O cliente inclui um sinalizador com a solicitação que indica que pontos de distribuição de fallback são permitidos.  

2.  Uma lista do local do conteúdo é devolvida ao cliente do ponto de gerenciamento com os pontos de distribuição preferenciais e os pontos de distribuição de fallback que têm o conteúdo. Não há pontos de distribuição preferenciais que têm o conteúdo, mas pelo menos um ponto de distribuição de fallback possui o conteúdo.  

3.  O conteúdo não é baixado, pois a propriedade de implantação referente a quando o cliente usa um ponto de distribuição de fallback está definida como **Não baixar conteúdo** (que é usada quando os clientes fazem fallback para obter o conteúdo). O cliente falha com a mensagem **O conteúdo não está disponível** e entra no modo de repetição. O cliente faz uma nova solicitação de conteúdo a cada hora.  

## <a name="scenario-6"></a>Cenário 6  
 A configuração é a seguinte:  

-   **O conteúdo não está disponível em um ponto de distribuição preferencial**  

-   **Distribuir o conteúdo deste pacote para os pontos de distribuição preferenciais** não está habilitada  

-   **Permitir fallback**: habilitada  

-   **Comportamento de implantação para rede lenta**: baixar e instalar conteúdo  


**Detalhes:**  

1.  O cliente envia uma solicitação de conteúdo para o ponto de gerenciamento. O cliente inclui um sinalizador com a solicitação indicando que os pontos de distribuição de fallback estão habilitados.  

2.  Uma lista do local do conteúdo é devolvida ao cliente do ponto de gerenciamento com os pontos de distribuição preferenciais e os pontos de distribuição de fallback que têm o conteúdo. Não há pontos de distribuição preferenciais que têm o conteúdo, mas pelo menos um ponto de distribuição de fallback que possui o conteúdo.  

3.  O conteúdo é baixado de um ponto de distribuição de fallback na lista, pois a propriedade de implantação referente a quando o cliente usa um ponto de distribuição de fallback está definida como **Baixar e instalar o conteúdo**.  

## <a name="scenario-7"></a>Cenário 7  
 A configuração é a seguinte:  

-   **O conteúdo não está disponível em um ponto de distribuição preferencial**  

-   **Distribuir o conteúdo deste pacote para os pontos de distribuição preferenciais** está habilitada  

-   **Permitir fallback**: não habilitada  

-   **Comportamento de implantação para rede lenta**: qualquer configuração  


**Detalhes:**  

1.  O cliente envia uma solicitação de conteúdo para o ponto de gerenciamento.  

2.  Uma lista do local do conteúdo é devolvida ao cliente do ponto de gerenciamento com os pontos de distribuição preferenciais que têm o conteúdo. Não há nenhum ponto de distribuição preferencial que tenha o conteúdo.  

3.  O cliente falha com a mensagem **O conteúdo não está disponível** e entra no modo de repetição. Uma nova solicitação de conteúdo é feita a cada hora.  

4.  O ponto de gerenciamento cria um gatilho para que o Gerenciador de Distribuição distribua o conteúdo a todos os pontos de distribuição do cliente que fez a solicitação de conteúdo.  

5.  O Gerenciador de Distribuição distribui o conteúdo para todos os pontos de distribuição preferenciais. Na maioria dos casos, o conteúdo é distribuído com êxito para os pontos de distribuição preferenciais em até uma hora.  

6.  Uma nova solicitação de conteúdo é iniciada pelo cliente para o ponto de gerenciamento.  

7.  Uma lista do local do conteúdo é devolvida ao cliente do ponto de gerenciamento com os pontos de distribuição preferenciais que têm o conteúdo. O cliente baixa o conteúdo de um ponto de distribuição preferencial na lista.  

## <a name="scenario-8"></a>Cenário 8  
 A configuração é a seguinte:  

-   **O conteúdo não está disponível em um ponto de distribuição preferencial**  

-   **Distribuir o conteúdo deste pacote para os pontos de distribuição preferenciais** está habilitada  

-   **Permitir fallback**: habilitada  

-   **Comportamento de implantação para rede lenta**: não baixar conteúdo  


**Detalhes:**  

1.  O cliente envia uma solicitação de conteúdo para o ponto de gerenciamento. O cliente inclui um sinalizador com a solicitação que indica que pontos de distribuição de fallback são permitidos.  

2.  Uma lista do local do conteúdo é devolvida ao cliente do ponto de gerenciamento com os pontos de distribuição preferenciais e os pontos de distribuição de fallback que têm o conteúdo. Não há pontos de distribuição preferenciais que têm o conteúdo, mas pelo menos um ponto de distribuição de fallback que possui o conteúdo.  

3.  O conteúdo não é baixado, pois a propriedade de implantação referente a quando o cliente usa um ponto de distribuição de fallback está definida como **Não baixar**. O cliente falha com a mensagem **O conteúdo não está disponível** e entra no modo de repetição. O cliente faz uma nova solicitação de conteúdo a cada hora.  

4.  O ponto de gerenciamento cria um gatilho para que o Gerenciador de Distribuição distribua o conteúdo a todos os pontos de distribuição do cliente que fez a solicitação de conteúdo.  

5.  O Gerenciador de Distribuição distribui o conteúdo para todos os pontos de distribuição preferenciais. Na maioria dos casos, o conteúdo é distribuído com êxito para os pontos de distribuição preferenciais em até uma hora.  

6.  Uma nova solicitação de conteúdo é iniciada pelo cliente para o ponto de gerenciamento.  

7.  Uma lista do local do conteúdo é devolvida ao cliente do ponto de gerenciamento com os pontos de distribuição preferenciais que têm o conteúdo.  

8.  O cliente baixa o conteúdo de um ponto de distribuição preferencial na lista.  

## <a name="scenario-9"></a>Cenário 9  
 A configuração é a seguinte:  

-   **O conteúdo não está disponível em um ponto de distribuição preferencial**  

-   **Distribuir o conteúdo deste pacote para os pontos de distribuição preferenciais** está habilitada  

-   **Permitir fallback**: habilitada  

-   **Comportamento de implantação para rede lenta**: baixar e instalar conteúdo  


**Detalhes:**  

1.  O cliente envia uma solicitação de conteúdo para o ponto de gerenciamento. O cliente inclui um sinalizador com a solicitação que indica que pontos de distribuição de fallback são permitidos.  

2.  Uma lista do local do conteúdo é devolvida ao cliente do ponto de gerenciamento com os pontos de distribuição preferenciais e os pontos de distribuição de fallback que têm o conteúdo. Não há pontos de distribuição preferenciais que têm o conteúdo, mas pelo menos um ponto de distribuição de fallback que possui o conteúdo.  

3.  O conteúdo é baixado de um ponto de distribuição de fallback na lista, pois a propriedade de implantação referente a quando o cliente usa um ponto de distribuição de fallback está definida como **Baixar e instalar o conteúdo**. Essa configuração de implantação permite que um cliente que deve usar um local de conteúdo de fallback obtenha o conteúdo desse local.  

4.  O ponto de gerenciamento cria um gatilho para que o Gerenciador de Distribuição distribua o conteúdo a todos os pontos de distribuição do cliente que fez a solicitação de conteúdo.  

5.  O Gerenciador de Distribuição distribui o conteúdo a todos os pontos de distribuição preferenciais, o que permite que clientes adicionais obtenham o conteúdo sem usar um ponto de distribuição de fallback.  



<!--HONumber=Dec16_HO3-->


