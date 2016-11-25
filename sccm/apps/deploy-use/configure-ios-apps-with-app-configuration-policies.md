---
title: "Configurar aplicativos iOS com políticas de configuração de aplicativos | System Center Configuration Manager"
description: "Ajude a eliminar problemas de configuração em dispositivos que executam o iOS 8 ou posterior ao implantar políticas de configuração de aplicativos para os usuários antes que eles executem aplicativos."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-app
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 74d5d776-e37d-45de-bdba-43541b03d12c
caps.latest.revision: 10
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9cbf28afbbe69f9a027ffad2a699b9d6b625e690


---
# <a name="configure-ios-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>Configure iOS apps with app configuration policies in System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Use políticas de configuração de aplicativo no System Center Configuration Manager para fornecer as configurações que possam ser necessárias quando o usuário executar um aplicativo. Por exemplo, um aplicativo pode exigir que o usuário especifique:
- Um número de porta personalizado
- Configurações de idioma
- Configurações de segurança
- Configurações de identidade visual, como um logotipo da empresa

Se essas configurações forem inseridas incorretamente pelo usuário, isso pode aumentar a carga do suporte técnico e também reduzir a adoção de novos aplicativos.
As políticas de configuração de aplicativo podem ajudar a eliminar esses problemas, permitindo que você implante essas configurações para os usuários em uma política antes que eles executem o aplicativo. As configurações então são fornecidas automaticamente e o usuário não precisa executar nenhuma ação.
Você não implanta essas políticas diretamente para usuários e dispositivos. Em vez disso, associe a política ao tipo de implantação quando implantar o aplicativo. As configurações de política serão usadas sempre que o aplicativo verificá-las (normalmente, na primeira vez que é executado).

As políticas de configuração de aplicativo atualmente estão disponíveis somente para dispositivos que executam iOS 8 e posterior e dão suporte aos seguintes tipos de aplicativos:

- **Pacote de aplicativo para iOS (*arquivo .ipa)**
- **Pacote de aplicativo para iOS da App Store**

Para obter mais informações sobre tipos de instalação do aplicativo, consulte [Introdução ao gerenciamento de aplicativos](/sccm/apps/understand/introduction-to-application-management).

## <a name="create-an-app-configuration-policy"></a>Criar uma política de configuração do aplicativo

1. No console do Configuration Manager, clique em **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Políticas de Configuração de Aplicativos**.
3. Na guia **Início**, no grupo **Políticas de Configuração de Aplicativos**, clique em **Criar Nova Política de Configuração de Aplicativo**.
4. Na página **Geral** do **Assistente Criar Política de Configuração de Aplicativo**, especifique as seguintes informações:
    - **Nome**: especifique um nome exclusivo para a política.
    - **Descrição**: como opção, especifique uma descrição para a política que ajuda você a identificá-la.
    - **Categorias atribuídas para aprimorar a pesquisa e a filtragem**: se desejar, clique em **Categorias** para criar e atribuir categorias para a política. Isso torna mais fácil classificar e localizar itens no console do Configuration Manager.
5. Na página **Política do iOS**, escolha como você especificará as informações da política de configuração:
    - **Especifique pares de nome e valor**: é possível usar esta opção para arquivos de lista de propriedades que não usam aninhamento.
    Para especificar pares de nome e valor
        - Para adicionar um novo par, clique em **Novo**.
        - Na caixa de diálogo **Adicionar Par Nome/Valor**, especifique o seguinte:
            - **Tipo**: da lista, escolha o tipo de valor que você deseja especificar.
            - **Nome**: insira o nome da chave de lista de propriedades para o qual você deseja especificar um valor.
            - **Valor**: insira o valor que será aplicado à chave que você inseriu.
        - Navegue até um arquivo de lista de propriedades: use essa opção se você já tiver um arquivo XML de configuração do aplicativo ou para arquivos mais complexos que usam o aninhamento.
        Para navegar até um arquivo de lista de propriedade
            - No campo **Política de configuração do aplicativo**, insira as informações da lista de propriedades no formato XML correto.
            Para obter mais informações sobre listas de propriedades XML, consulte [Noções básicas sobre listas de propriedades XML](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html) na biblioteca do desenvolvedor do iOS.
            O formato da lista de propriedades XML vai variar dependendo do aplicativo que você está configurando. Entre em contato com o fornecedor do aplicativo para obter detalhes sobre o formato exato a ser usado.
            O Intune dá suporte aos seguintes tipos de dados em uma lista de propriedades:
            ```
            <integer>
            <real>
            <string>
            <array>
            <dict>
            <true /> or <false />
            ```
            Para obter mais informações sobre tipos de dados, consulte o artigo [Sobre listas de propriedades](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/PropertyLists/AboutPropertyLists/AboutPropertyLists.html) na biblioteca do desenvolvedor do iOS.
            Além disso, o Intune dá suporte aos seguintes tipos de token na lista de propriedades:
            ```
            {{userprincipalname}} - (Example: John@contoso.com)
            {{mail}} - (Example: John@contoso.com)
            {{partialupn}} - (Example: John)
            {{accountid}} - (Example: fc0dc142-71d8-4b12-bbea-bae2a8514c81)
            {{deviceid}} - (Example: b9841cd9-9843-405f-be28-b2265c59ef97)
            {{userid}} - (Example: 3ec2c00f-b125-4519-acf0-302ac3761822)
            {{username}} - (Example: John Doe)
            {{serialnumber}} - (Example: F4KN99ZUG5V2) for iOS devices
            {{serialnumberlast4digits}} - (Example: G5V2) for iOS devices

            The {{ and }} characters are used by token types only and must not be used for other purposes.
            ```
            Clique também em **Selecionar arquivo** para importar um arquivo XML que você criou anteriormente.
6. Clique em **Avançar**. Se houver erros no código XML, você precisará corrigi-los antes de continuar.
6. Conclua o assistente.

A nova política de configuração de aplicativo é exibida no nó **Políticas de Configuração de Aplicativos** no espaço de trabalho **Biblioteca de Software**.

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>Associar uma política de configuração de aplicativo a um aplicativo do Gerenciador de Configurações

Para associar uma política de configuração do aplicativo com a implantação de um aplicativo iOS, implante o aplicativo como normalmente faria com o procedimento no tópico [Implantar aplicativos](/sccm/apps/deploy-use/deploy-applications).
Na página **Políticas de Configuração de Aplicativos** do **Assistente de implantação de Software**, clique em **Novo**. Em seguida, na caixa de diálogo **Selecionar Política de Configuração de Aplicativo**, escolha um tipo de implantação do aplicativo e uma política de configuração de aplicativo à qual você deseja associar.
Quando o tipo de implantação for instalado, as configurações de política de configuração do aplicativo serão aplicadas automaticamente.

## <a name="example-format-for-the-mobile-app-configuration-xml-file"></a>Exemplo de formato para o arquivo XML de configuração de aplicativo móvel

Quando você cria um arquivo de configuração de aplicativo móvel, pode especificar um ou mais dos seguintes valores usando este formato:

```
<dict>
  <key>userprincipalname</key>
  <string>{{userprincipalname}}</string>
  <key>mail</key>
  <string>{{mail}}</string>
  <key>partialupn</key>
  <string>{{partialupn}}</string>
  <key>accountid</key>
  <string>{{accountid}}</string>
  <key>deviceid</key>
  <string>{{deviceid}}</string>
  <key>userid</key>
  <string>{{userid}}</string>
  <key>username</key>
  <string>{{username}}</string>
  <key>serialnumber</key>
  <string>{{serialnumber}}</string>
  <key>serialnumberlast4digits</key>
  <string>{{serialnumberlast4digits}}</string>
  <key>udidlast4digits</key>
  <string>{{udidlast4digits}}</string>
</dict>
```



<!--HONumber=Nov16_HO1-->


