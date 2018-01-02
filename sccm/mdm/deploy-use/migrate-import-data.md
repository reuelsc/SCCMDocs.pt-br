---
title: Importar dados para o Microsoft Intune
titleSuffix: Configuration Manager
description: 
keywords: 
author: dougeby
manager: dougeby
ms.date: 12/05/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: b552391d-abc0-48a2-a429-93605a13a66a
ms.openlocfilehash: d42a5fd64b5baead8ef87d8c08a99ec659f94633
ms.sourcegitcommit: 8c6e9355846ff6a73c534c079e3cdae09cf13c45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/06/2017
---
# <a name="import-configuration-manager-data-to-microsoft-intune"></a>Importar dados do Configuration Manager para o Microsoft Intune 

*Aplica-se a: System Center Configuration Manager (Branch Atual)*    

A primeira fase recomendada do processo para [migrar usuários e dispositivos do MDM híbrido para o Intune autônomo](migrate-hybridmdm-to-intunesa.md) na configuração somente de nuvem é usar a ferramenta Importador de Dados do Intune. Se desejar, você poderá ignorar esta fase e passar para a fase [Preparar o Intune para migração de usuários](migrate-prepare-intune.md). No entanto, essa ferramenta executa as seguintes funções que podem ajudar a poupar tempo na próxima fase: 
1.  Coleta dados sobre os objetos que você seleciona na hierarquia do Configuration Manager. 
2.  Fornece detalhes sobre os objetos que você pode selecionar para importar e as informações sobre o motivo pelo qual alguns objetos não podem ser importados.
3.  Importa os objetos selecionados em seu locatário do Microsoft Intune. 

A ferramenta Importador de Dados não altera seu ambiente do Configuration Manager de nenhuma maneira e, portanto, você pode importar objetos para o Intune e confirmar se tudo está funcionando conforme o esperado, sem o risco de deixar os dispositivos de MDM híbridos em um estado não gerenciado. 

## <a name="what-objects-can-this-tool-import"></a>Quais objetos essa ferramenta pode importar?
A ferramenta de importação pode coletar informações sobre os seguintes tipos de objeto no Configuration Manager e informa se os objetos coletados podem ser importados: 
- Itens de configuração
- Perfis de certificado
- Perfis de email
- Perfis de VPN
- Perfis de Wi-Fi
- Políticas de conformidade
- Aplicativos
- Implantações

> [!Note]    
> A importação de implantações só é útil para outros tipos de objeto importados. Por exemplo, se você importar perfis de VPN e implantações, você só poderá importar as implantações dos perfis de VPN que você selecionar. As implantações no Intune são chamadas de atribuições. Se você desejar importar uma implantação de um objeto importado anteriormente, será necessário importar esse objeto novamente ou criar a atribuição manualmente no Intune no Azure. Por exemplo, se você importar perfis de VPN e não implantações, será necessário executar a ferramenta novamente e selecionar os perfis de VPN e as implantações ou criar a atribuição manualmente no Intune no Azure.  Se você executar a ferramenta novamente, poderão ser criados objetos duplicados que você poderá excluir mais tarde no Intune no Azure.  

> [!Important]    
> Se a coleção de uma implantação for baseada em um grupo do Active Directory que tenha sido replicado para AAD (Azure Active Directory), a ferramenta será automaticamente direcionada aos objetos migrados para os grupos se você selecionar a implantação apropriada ao executar a ferramenta. Quando houver coleções mais complexas ou coleções de associações diretas, você deverá recriá-las manualmente no AAD e direcionar as atribuições de objeto à elas manualmente no Intune no Azure.


## <a name="things-to-know-before-you-run-the-tool"></a>O que você deve saber antes de executar a ferramenta
- A execução da ferramenta não alterará seu ambiente do Configuration Manager de nenhuma forma.
- É recomendável que primeiro você teste o processo de importação de dados usando um locatário de avaliação. Em seguida, depois de confirmar que os dados esperados foram importados, você poderá usar o mesmo processo com seu locatário do Intune de produção.
- O importador de dados importa os dados do Configuration Manager somente uma vez. Ele não continua acompanhando os objetos no Configuration Manager nem no Intune. No entanto, se você executar o importador novamente no mesmo computador que antes, ele informará quais objetos já foram importados anteriormente. A ferramenta não saberá se o objeto ainda existe no Intune ou se algum objeto foi alterado. Se você importar dados para o Intune mais de uma vez, poderá ocorrer a duplicação de objetos.
- Nem todas as configurações de perfil podem ser importadas. Por exemplo, não é possível importar configurações de PFX ou de modo de quiosque. 
- Se você tiver uma política do Configuration Manager com configurações que não sejam aplicáveis às plataformas selecionadas, a ferramenta poderá ignorar essas configurações durante a importação. Ignorar as configurações ajuda a verificar se a política pode ser importada e ela se terá suporte no Intune. 
- A ferramenta tentará fornecer um motivo pelo qual algum objeto não pode ser importado. Em alguns casos, antes de importar objetos para o Intune, você pode acessar o console do Configuration Manager, corrigir o problema, iniciar a verificação de descoberta de objetos do Configuration Manager novamente e, em seguida, importar os objetos. Às vezes, pode ser necessário ou você pode querer recriar esses objetos manualmente no Intune.
- Há alguns perfis que dependem de outros objetos. Se você quiser importar um perfil que dependa de outro objeto, como um perfil de email que dependa de um certificado, você deverá importar os dois objetos ao mesmo tempo, a menos que tenha importado anteriormente o outro objeto do mesmo computador, com o mesmo usuário.  
- Depois que você executar a ferramenta, poderá ser necessário executar etapas manuais adicionais. Por exemplo, direcionar aplicativos e políticas para grupos do AAD. 

## <a name="prerequisites"></a>Pré-requisitos
- Configuration Manager versão 1610 ou posterior – é recomendável que você especifique o site de nível superior e execute a ferramenta com um usuário que tenha acesso a todos os objetos na hierarquia do site. A ferramenta só descobre os objetos que são acessíveis para o usuário que executa a ferramenta. 
- Um Administrador Global deve executar a ferramenta Importador de Dados pela primeira vez usando o seguinte parâmetro ***intunedataimporter.exe -GlobalConsent***. Em seguida, um Administrador Global ou um Administrador do Intune pode executar a ferramenta.  


<!-- ## Objects that cannot be imported
There are some Configuration Manager objects that the importer tool cannot import to Intune. You must manually create these objects in Intune. 
- Collections based on direct membership or that are based on a query. The only collections that are imported are based on a single AD group. For all other collections, you must create the assignment in Intune and add the assignment to the appropriate objects. 
- Profiles <list what we cannot import>
- Policies <??>
- Etc.
-->

## <a name="download-the-data-importer-tool"></a>Baixar a ferramenta Importador de Dados
A ferramenta Importador de Dados está disponível para download no repositório do GitHub ConfigMgrTools/Intune-Data-Importer. Use o procedimento a seguir para baixar a ferramenta.

1. Acesse a página [Versões do Intune Data Importer no GitHub](https://github.com/ConfigMgrTools/Intune-Data-Importer/releases).
2. Para obter a versão mais recente, clique em **Microsoft.Intune.Data.Importer.exe**.
3. Salve e execute (ou só execute) o .exe e escolha uma pasta de destino para extrair a ferramenta Intune Data Importer.

## <a name="run-the-data-importer-tool"></a>Execute a ferramenta Importador de Dados
O assistente da ferramenta Importador de Dados pode ser dividido em três etapas principais. Esta seção fornece informações para ajudá-lo a concluir cada seção do assistente e importar dados do Configuration Manager no Intune com êxito. Cada etapa continua no ponto em que a etapa anterior terminou.

### <a name="provide-permission-for-the-data-importer-tool-to-access-resources"></a>Fornecer permissão para a ferramenta Importador de Dados acessar recursos
Antes de executar a ferramenta Importador de Dados, você deverá usar uma conta de Administrador Global para conceder à ferramenta Importador de Dados a permissão para acessar recursos no Azure. Em seguida, você poderá executar a ferramenta usando uma conta de Administrador Global ou de Administrador do Intune.   

1.  Um Administrador Global deve executar a ferramenta pela primeira vez usando o seguinte parâmetro:  ***intunedataimporter.exe -GlobalConsent*** 
2. Quando a ferramenta é iniciada, uma tela de logon exibe onde você deve entrar usando uma conta com a função de Administrador Global no Azure. 
3. Clique em **Aceitar** para criar um aplicativo no Azure com os direitos apropriados no Microsoft Graph. A ferramenta Importador de Dados precisa desses direitos para importar objetos para o Microsoft Intune.   

   > [!Important]
   > Ao clicar em **Aceitar**, você concede permissão à ferramenta para fazer o seguinte:
   > - Ler todos os grupos
   > - Entrar e ler o perfil do usuário
   > - Ler e gravar a configuração e as políticas de dispositivos do Intune
   > - Ler e gravar aplicativos do Intune
   > - Ler e gravar as políticas do controle de administração baseada em funções do Intune
   > - Ler e gravar dispositivos do Intune
   > - Ler e gravar a configuração do Intune
1. Depois que você aceitar o consentimento, qualquer outro Administrador Global ou Administrador do Intune poderá executar a ferramenta para importar dados do Configuration Manager para o Intune no Azure.    
        
    > [!Note]
    > Se o consentimento não for aceito primeiro por um Administrador Global, a ferramenta poderá exibir **Não é possível acessar este aplicativo** depois que um Administrador do Intune executar a ferramenta Importador de Dados e fizer logon na assinatura do Intune.

### <a name="manually-map-collections-to-azure-ad-groups"></a>Mapear manualmente coleções nos grupos do Azure AD
Quando você executa a ferramenta Data Importer, ela extrai o nome do grupo do AD das coleções com uma única regra que direciona um único grupo do AD. Quando as atribuições são criadas no Intune, o Data Importer procura um grupo do Azure AD com o mesmo nome que o grupo do AD e, se existir, atribui o objeto importado para esse grupo do Azure AD. Substitua o nome do grupo do AD encontrado pelo Data Importer para uma coleção e forneça um ou mais grupos do Azure AD para usar para essa coleção. O uso do arquivo de mapeamento de coleção fornece uma maneira de mapear coleções que normalmente não podem ser importadas com o Data Importer para os grupos do Azure AD.
#### <a name="find-the-collections-that-cannot-be-imported"></a>Localizar as coleções que não podem ser importadas
Obtenha uma lista com todas as coleções que não podem ser importadas, para que você possa adicioná-las ao seu arquivo .csv de mapeamento de coleção. 
1. Execute a ferramenta Data Importer e selecione os objetos para importação. Use os procedimentos na [Fase 1: Descobrir objetos do Configuration Manager e coletar dados](#phase-1:-discover-configuration-manager-objects-and-collect-data) e [Fase 2: Resolver problemas e selecionar os objetos para importação](#phase-2:-resolve-issues-and-select-the-objects-to-import) para descobrir e escolher os objetos. Depois, na página **Resumo**, escolha **Exportar Detalhes** para criar um arquivo .csv com detalhes sobre todas as opções selecionadas para importação, incluindo os objetos que não podem ser importados e implantações. 
2. Abra o arquivo .csv no Microsoft Excel e filtre os dados com base em **Implantação** para a coluna **Tipo** e **Não** para a coluna **Importável**. A colune de nome da coleção mostra todas as coleções que precisam ser adicionadas a um arquivo de mapeamento de coleção para que essas implantações possam ser importadas.

#### <a name="create-the-collection-mapping-file"></a>Criar o arquivo de mapeamento de coleção
O arquivo de mapeamento de coleção é um arquivo CSV (valores separados por vírgula) em que a primeira coluna é o nome de coleção do Configuration Manager, e a segunda coluna é o nome de grupo do Azure AD a ser usado para essa coleção. Para especificar mais de um grupo do Azure AD para uma única coleção do Configuration Manager, crie várias linhas no arquivo CSV com esse nome de coleção. O exemplo a seguir é um arquivo CSV que contém duas coleções. A primeira coleção é mapeada para um único grupo do Azure AD, e a segunda coleção é mapeada para dois grupos do Azure AD.

![Exemplo de arquivo csv de mapeamento de coleção](..\media\migrate-collectionmapping.png)

#### <a name="start-the-data-importer-tool-using-collection-mapping"></a>Iniciar a ferramenta Data Importer usando o mapeamento de coleção
Para usar um arquivo de mapeamento de coleção, inicie a ferramenta Data Importer usando o parâmetro de linha de comando *-CollectionMappingFile* e o caminho completo até o arquivo .csv de mapeamento de coleção que você criou. Por exemplo:

```IntuneDataImporter.exe -CollectionMappingFile c:\Users\myuser\Documents\collectionmapping.csv```

> [!Note]
> O Data Importer não exibe nada na página de qualquer assistente para indicar que o arquivo de mapeamento de coleção foi carregado. No entanto, a ferramenta exibe os erros encontrados durante a leitura do arquivo .csv. Além disso, na página **Resumo** do assistente, você pode ver os tipos de **Implantação**. A ferramenta exibe **Sim** na coluna Importável e lista os grupos do Azure AD que atribuirá aos objetos na coluna **Notas**.

### <a name="phase-1-discover-configuration-manager-objects-and-collect-data"></a>Etapa 1: Descobrir objetos do Configuration Manager e coletar dados
Na fase 1, você selecionará os objetos a serem descobertos e fará com que a ferramenta colete informações sobre os objetos selecionados. 
1. Abra a ferramenta e clique em **Iniciar**.  
2. Leia as informações e, em seguida, clique em **Avançar**. 
3. Escolha se quer importar um conjunto de dados exportado anteriormente ou selecione os tipos de objeto para importação:
   - **Importar conjunto de dados exportado anteriormente**: escolha **Importar conjunto de dados exportado de uma execução anterior do Intune Data Importer**, e clique em **Procurar** para **Pasta de dados exportada** a fim de selecionar um conjunto de dados exportado anteriormente usando o Data Importer Tool. O usuário que importa o conjunto de dados deve ser o mesmo usuário que exportou os dados. Após a importação dos dados, um resumo com os objetos é listado na página **Resumo** do assistente. Se o resumo estiver correto, pule para a [Fase 3: Importar objeto selecionado para o Intune](phase-3:-import-selected-object-to-intune).
 
      > [!Note]
      > Depois de descobrir e selecionar objetos em seu site para importação, exporte os objetos para um conjunto de dados na página **Entrar no Intune** do assistente. Depois, você pode importar o conjunto de dados nessa página. O conjunto de dados é criptografado usando as credenciais de usuário do Windows do usuário conectado, de modo que apenas o usuário que exportou o conjunto de dados possa importar o conjunto de dados na ferramenta. 
   - **Selecione os tipos de objeto para importação**: escolha **Selecionar tipos de objeto para importação** para selecionar os tipos de objeto para importação e descobrir objetos em seu ambiente. Forneça as seguintes informações sobre seu site e os objetos que você deseja importar.
      - **Nome do servidor do site**: forneça o nome de domínio totalmente qualificado do servidor do site do qual os objetos serão importados. A ferramenta só descobre os objetos que são acessíveis para o usuário que executa a ferramenta. Geralmente, você especifica o site de nível superior e executa a ferramenta com um usuário que tenha acesso a todos os objetos na hierarquia do site.
      - **Código do site**: forneça o código do site para o servidor do site. Você pode encontrar o código de três letras na parte superior do console do Configuration Manager.
      - **Tipos de objeto a serem importados**: escolha os objetos que você deseja que a ferramenta colete. Você pode escolher **Selecionar tudo** para escolher todos os objetos ou selecionar tipos de objeto individuais. 
4.  Clique em **Avançar** para iniciar a descoberta de objetos no site. A ferramenta exibe o progresso de cada um dos tipos de objeto. 
    - Quando a ferramenta não descobre nenhum dado de um tipo de objeto selecionado, a barra de progresso é imediatamente exibida como concluída para esse tipo de objeto.
    - Os objetos que você não selecionou não são exibidos na página de dados **Coletar**. 
    - Você pode executar a ferramenta novamente para os objetos que não foram coletados ou que você cancelou durante o processo de coleta.

### <a name="phase-2-resolve-issues-and-select-the-objects-to-import"></a>Fase 2: Resolver problemas e selecionar os objetos para importação  
Na fase 2, você examinará os objetos encontrados pela ferramenta, resolverá os problemas que impedem que o objeto seja importado para o Intune e selecionará os objetos para importação. Depois de corrigir os problemas, retorne para a página **Descobrir ambiente** do assistente para redescobrir os objetos. 
5.  Clique em **Avançar** para examinar os objetos coletados. Uma página de seleção de item está disponível para cada tipo de objeto coletado. 
 <!--   > [!Tip]     
    > On each item selection page, you can create a filter to help you find the objects that you want to import. However, take note of the following:
    > - When you are on an item selection page and the view is filtered, the Select all checkboxes only apply to the displayed items. Any hidden objects because of a filter are not included when using the checkboxes.
    > - Objects are always grouped under their parent item even when you sort or filter the objects.
-->
6.  Em cada página de seleção de item, classifique os objetos pela coluna Importável e examine os objetos que não podem ser importados. As informações na coluna Observações fornecem detalhes sobre o motivo pelo qual a ferramenta não pode importar o objeto. 
7.  Agora você deve decidir se deseja corrigir os problemas dos objetos que não podem ser importados. Se você corrigir um ou mais problemas, clique em Anterior até chegar à página Selecionar dados do Configuration Manager e coletar os dados novamente para ver se o problema foi resolvido. Você pode continuar a corrigir problemas até ficar satisfeito com os objetos que podem ser importados. 
8.  Em cada página de seleção de item, selecione os objetos que você deseja importar. As colunas a seguir são listadas:
    - **Nome**: nome do objeto do Configuration Manager. 
    - **Importável**: especifica se um objeto pode ser importado. Você só poderá escolher objetos que tenham Sim na coluna Importável. 
    - **Plataforma**: especifica a plataforma com suporte do objeto.
    - **Já importado**: especifica se o objeto já foi importado usando a ferramenta neste computador. 
    - **Substituído** (para aplicativos): especifica se o aplicativo foi substituído por outro aplicativo. Marque a caixa de seleção **Mostrar aplicativos substituídos** na parte superior da página para mostrar os aplicativos substituídos.
    - **Observações**: fornece informações sobre o motivo pelo qual um objeto não pode ser importado. A coluna **Notas** também mostra informações sobre as configurações que foram ignoradas (para alguns tipos de objeto), mas o objeto ainda pode ser importado sem essas configurações.
    - **Linhas de base de configuração** (para itens de configuração): especifica as linhas de base de configuração que estão associadas a um item de configuração.
    - **Certificado necessário** (para perfis e políticas): especifica se há um certificado associado ao objeto. Quando há um certificado associado ao objeto, você também deve importar o certificado.
9.  Depois que você escolher os objetos para importação, eles serão listados na página Resumo. As seguintes ações estão disponíveis: 
    - **Exportar detalhes**: cria um arquivo .csv que contém as informações exibidas na tela. Também mostra objetos que não podem ser importados e o motivo. Você pode manter esse arquivo em seus registros. 
    - **Exportar dados de erro**: exporta um arquivo compactado que contém informações sobre os dados que a ferramenta não pôde converter ou importar. 

### <a name="phase-3-import-selected-objects-to-intune"></a>Fase 3: Importar os objetos selecionados no Intune
Na fase 3, você entrará no Intune e importará os objetos selecionados. 
10. Clique em **Avançar** e, em seguida, clique em **Entrar no Intune** para entrar no locatário do Intune para a importação de dados ou escolha exportar os dados.

    - **Exportar**: depois de descobrir e selecionar objetos em seu site para importação, exporte os objetos para um conjunto de dados. Isso permite que você descubra objetos de um computador que não tem acesso à Internet, exporte os dados e, depois, importe os dados de um computador com acesso à Internet. O conjunto de dados é criptografado usando as credenciais de usuário do Windows do usuário conectado, de modo que apenas o usuário que exportou o conjunto de dados possa importar o conjunto de dados na ferramenta. Quando você escolher essa opção, escolha o caminho até os dados exportados. 
      1. Clique em **Exportar** na página **Entrar no Intune**. 
      2. Clique em **Procurar** para selecionar a pasta de destino para a exportação. A pasta deve estar vazia. 
      3. Clique em **Iniciar** para exportar os dados e, após a conclusão da exportação, clique em **Fechar** para completar a assistente e fechar o Data Importer.
      4. Inicie o Data Importer de outro computador com acesso à Internet usando as mesmas credenciais e selecione **Importar conjunto de dados exportado anteriormente** na segunda página do assistente. Após a importação dos dados, o assistente levará você até a página **Entrar no Intune**. 
    - **Entrar no Intune**: você deve entrar com uma conta de Administrador Global ou de Administrador do Intune. Depois que você entrar, o processo de importação será iniciado.
    
      > [!Important]
      > É recomendável que primeiro você teste o processo de importação de dados usando um locatário de avaliação. Em seguida, depois de confirmar que os dados esperados foram importados, você poderá usar o mesmo processo com seu locatário do Intune de produção.
12. A página Progresso fornece o progresso à medida que os objetos são importados. Clique em **Avançar** quando a importação for concluída. 
13. Na página Conclusão, são listados os objetos importados. Verifique o status de todos os objetos que encontraram um erro durante o processo de importação. As seguintes ações estão disponíveis: 
    - **Exportar detalhes**: cria um arquivo .csv que contém as informações exibidas na tela. Você pode manter esse arquivo em seus registros. 
    - **Exportar dados de erro**: exporta um arquivo compactado que contém informações sobre os dados que a ferramenta não pôde converter ou importar.

## <a name="next-steps"></a>Próximas etapas
Depois de importar os dados para o Intune, você deve executar as etapas para [Preparar o Intune para migração de usuários](migrate-prepare-intune.md). 