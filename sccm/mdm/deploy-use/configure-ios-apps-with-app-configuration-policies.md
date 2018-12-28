---
title: Configure iOS apps with app configuration policies
titleSuffix: Configuration Manager
description: Ajude a eliminar problemas de configuração em dispositivos que executam o iOS 8 ou posterior ao implantar políticas de configuração de aplicativos para os usuários antes que eles executem aplicativos.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: f0a78038-ea22-4826-9c07-1771b7dd2e8d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 19b55204566c49c95e76a3eff3f88206df553e13
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416156"
---
# <a name="apply-settings-to-ios-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>Aplicar configurações a aplicativos iOS com políticas de configuração de aplicativo no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch atual)*


Você pode usar políticas de configuração de aplicativo no System Center Configuration Manager (Configuration Manager) para distribuir as configurações que podem ser necessárias quando um usuário executa um aplicativo. Por exemplo, um aplicativo pode exigir que um usuário especifique estes detalhes:
- Um número de porta personalizado
- Configurações de idioma
- Configurações de segurança
- Configurações de identidade visual, como um logotipo da empresa

Se o usuário inserir as configurações incorretamente, a correção poderá sobrecarregar o suporte técnico e a implantação do aplicativo ficará lenta.
Para evitar esses problemas, você pode usar políticas de configuração de aplicativo para implantar as configurações necessárias para os usuários antes que eles executem o aplicativo. As configurações são associadas a um usuário automaticamente. O usuário não precisa executar nenhuma ação.
Para usar uma política de configuração de aplicativo no Configuration Manager, em vez de implantar as políticas de configuração diretamente para o usuários e dispositivos, você associa uma política a um tipo de implantação ao implantar o aplicativo. As configurações de política são aplicadas sempre que o aplicativo as verifica (normalmente, na primeira vez em que o aplicativo é executado).

Atualmente, as políticas de configuração de aplicativo estão disponíveis somente em dispositivos com iOS 8 e posterior e para estes tipos de aplicativos:

- **pacote do aplicativo para iOS (arquivo *.ipa)**
- **pacote do aplicativo para iOS da App Store**

Para obter mais informações sobre os tipos de instalação de aplicativos, consulte a [introdução ao gerenciamento de aplicativos](/sccm/apps/understand/introduction-to-application-management).

## <a name="create-an-app-configuration-policy"></a>Criar uma política de configuração do aplicativo

1. No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Políticas de Configuração de Aplicativo**.
2. Na guia **Início**, no grupo **Políticas de Configuração de Aplicativo**, escolha **Criar Nova Política de Configuração de Aplicativo**.
3. No Assistente para Criar Política de Configuração de Aplicativo, na página **Geral** defina estas informações de política:
   - **Nome**. Insira um nome exclusivo para a política.
   - **Descrição**. (Opcional) Para facilitar a identificação da política, você pode adicionar uma descrição.
   - **Categorias atribuídas para melhorar a pesquisa e a filtragem**. (Opcional) Para criar e atribuir categorias para a política, escolha **Categorias**. As categorias facilitam a classificação e a localização de itens no console do Configuration Manager.
4. Na página **Política do iOS**, escolha como definir as informações da política de configuração:
   - **Especificar pares nome-valor**. Você pode usar essa opção para arquivos de lista de propriedades que não usam aninhamento.

      *Para especificar um par nome-valor*
        1. Para adicionar um novo par, escolha **Novo**.
        2. Na caixa de diálogo **Adicionar Par Nome/Valor**, especifique o seguinte:
            - **Tipo**. Na lista, selecione o tipo de valor que deseja especificar.
            - **Nome**. Insira o nome da chave de lista de propriedades para o qual deseja especificar um valor.
            - **Valor**. Insira o valor que será aplicado à chave inserida.

   - **Procure um arquivo de lista de propriedades**. Use essa opção se você já tiver um arquivo XML de configuração de aplicativo ou para arquivos mais complexos que usam aninhamento.

     *Para procurar um arquivo de lista de propriedades*

     1. No campo **Política de configuração do aplicativo**, insira as informações da lista de propriedades no formato XML correto.

        Para obter mais informações sobre listas de propriedades XML, consulte [Noções básicas sobre listas de propriedades XML](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html) na biblioteca do desenvolvedor do iOS.

O formato da lista de propriedades XML varia dependendo do aplicativo que você está configurando. Entre em contato com o fornecedor do aplicativo para obter detalhes sobre o formato a ser usado.
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
O Intune também dá suporte aos seguintes tipos de token na lista de propriedades:
            
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
            ```

Os caracteres {{ e }} são usados apenas por tipos de token e não devem ser usados para outras finalidades.
            
5. Para importar um arquivo XML que você criou anteriormente, escolha **Selecionar arquivo**.
6. Escolha **Próxima**. Se houver erros no código XML, você precisará corrigi-los antes de continuar.
7. Conclua as etapas mostradas no assistente.

A nova política de configuração de aplicativo é mostrada no workspace **Biblioteca de Software**, no nó **Políticas de Configuração de Aplicativo**.

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>Associar uma política de configuração de aplicativo a um aplicativo do Gerenciador de Configurações

Para associar uma política de configuração de aplicativo à implantação de um aplicativo iOS, implante o aplicativo da maneira normal, usando o procedimento no tópico [Implantar aplicativos](/sccm/apps/deploy-use/deploy-applications).

No Assistente para Implantar Software, na página **Políticas de configuração de aplicativo**, escolha **Novo**. Na caixa de diálogo **Selecionar Política de Configuração de Aplicativo**, escolha um tipo de implantação de aplicativo e a política de configuração de aplicativo à qual deseja associá-lo.
Quando o tipo de implantação for instalado, as definições da política de configuração de aplicativo serão aplicadas automaticamente.

## <a name="example-format-for-the-mobile-app-configuration-xml-file"></a>Exemplo de formato para o arquivo XML de configuração de aplicativo móvel

Ao criar um arquivo de configuração de aplicativo móvel, você pode usar este formato para especificar um ou mais dos seguintes valores:

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
