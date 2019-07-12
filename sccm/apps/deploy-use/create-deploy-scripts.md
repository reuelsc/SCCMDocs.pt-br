---
title: Criar e executar scripts
titleSuffix: Configuration Manager
description: Crie e execute scripts do Powershell em dispositivos clientes.
ms.date: 06/20/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28d1f01cbdd6238754cafc36be8d30499b041597
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67676209"
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Criar e executar scripts do PowerShell do console do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

<!--1236459-->
O System Center Configuration Manager tem uma capacidade integrada para executar scripts do PowerShell. O PowerShell oferece a vantagem de criar scripts automatizados sofisticados que são entendidos e compartilhados com uma comunidade maior. Os scripts simplificam a criação de ferramentas personalizadas para administrar o software e permitem realizar tarefas rotineiras rapidamente, possibilitando concluir trabalhos grandes com mais facilidade e consistência.  

> [!TIP]  
> Esse recurso foi introduzido pela primeira vez na versão 1706 como um [recurso de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir da versão 1802, esse recurso deixa de ser um recurso de pré-lançamento.  


> [!Note]  
> O Configuration Manager não habilita esse recurso opcional por padrão. É necessário habilitar esse recurso antes de usá-lo. Para obter mais informações, consulte [Enable optional features from updates (Habilitar recursos opcionais de atualizações)](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


Com essa integração no System Center Configuration Manager, você pode usar a funcionalidade *Executar Scripts* para fazer o seguinte:

- Criar e editar scripts a serem usados com o System Center Configuration Manager.
- Gerenciar o uso de script por meio de funções e escopos de segurança. 
- Executar scripts em coleções ou em computadores Windows individuais gerenciados localmente.
- Obter resultados rápidos do script agregado dos dispositivos clientes.
- Monitorar a execução do script e exibir os resultados do relatório da saída do script.

>[!WARNING]
>Considerando a potência dos scripts, lembre-se de usá-los com uma intenção definida e com cuidado. Inserimos proteções adicionais para ajudá-lo, além de funções segregadas e escopos. Valide a precisão dos scripts antes de executá-los e confirme se eles são de uma fonte confiável, para impedir uma execução não intencional do script. Preste atenção em caracteres estendidos ou outras ofuscações e aprenda como proteger scripts. [Saiba mais sobre a segurança de script do PowerShell](/sccm/apps/deploy-use/learn-script-security)

## <a name="prerequisites"></a>Pré-requisitos

- Para executar scripts do PowerShell, o cliente deve executar o PowerShell versão 3.0 ou posterior. No entanto, se um script for executado contendo funcionalidades de uma versão posterior do PowerShell, o cliente no qual o script estiver sendo executado deverá estar executando essa versão do PowerShell.
- Clientes do Configuration Manager devem estar executando o cliente da versão 1706 ou posterior para executar scripts.
- Para usar scripts, você deve ser membro da função de segurança apropriada do Configuration Manager.
- Para importar e criar scripts – sua conta deve ter permissões **Criar** para **Scripts do SMS**.
- Para aprovar ou negar scripts – sua conta deve ter permissões **Aprovar** para **Scripts do SMS**.
- Para executar scripts – sua conta deve ter permissões **Executar Script** para **Coleções**.

Para obter mais informações sobre as funções de segurança do Configuration Manager:</br>
[Escopos de segurança para executar scripts](#security-scopes)</br>
[Funções de segurança para executar scripts](#bkmk_ScriptRoles)</br>
[Fundamentos da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration).

## <a name="limitations"></a>Limitações

No momento, o recurso Executar Scripts dá suporte para:

- Linguagens de scripts: PowerShell
- Tipos de parâmetro: inteiro, cadeia de caracteres e lista.


>[!WARNING]
>Lembre-se de que, ao usar parâmetros, ele abre uma área de superfície para o risco de possíveis ataques de injeção do PowerShell. Há várias maneiras de atenuar e resolver o problema, como usando expressões regulares para validar a entrada de parâmetro ou usando parâmetros predefinidos. A melhor prática comum é não incluir segredos nos scripts do PowerShell (sem senhas, etc.). [Saiba mais sobre a segurança de script do PowerShell](/sccm/apps/deploy-use/learn-script-security) <!--There are external tools available to validate your PowerShell scripts such as the [PowerShell Injection Hunter](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) tool. -->


## <a name="run-script-authors-and-approvers"></a>Autores e aprovadores do recurso Executar Script

O recurso Executar Scripts usa o conceito de *autores de script* e *aprovadores e script* como funções separadas para a implementação e a execução de um script. A separação das funções de autor e aprovador permite um processo de verificação importante para a potente ferramenta Executar Scripts. Há mais uma função de *executores de script* que permite a execução, mas não a criação nem a aprovação de scripts. Consulte [Criar funções de segurança para scripts](#bkmk_ScriptRoles).

### <a name="scripts-roles-control"></a>Controle de funções de scripts

Por padrão, os usuários não é possível aprovar um script que eles já criados. Como os scripts são eficientes, versáteis e potencialmente implantados em muitos dispositivos, você pode separar as funções entre a pessoa que cria o script e a pessoa que o aprova. Essas funções proporcionam um nível a mais de segurança contra a execução de um script sem supervisão. É possível desativar a aprovação secundária para facilitar o teste.

### <a name="approve-or-deny-a-script"></a>Aprovar ou negar um script

Os scripts precisam ser aprovados pela função *aprovador de script*, antes de serem executados. Para aprovar um script:

1. No console do Configuration Manager, clique em **Biblioteca de Software**.
2. No workspace **Biblioteca de Software**, clique em **Scripts**.
3. Na lista **Script**, escolha o script que você quer aprovar ou negar e, na guia **Início**, no grupo **Script**, clique em **Aprovar/Negar**.
4. Na caixa de diálogo **Aprovar ou negar o script**, selecione **Aprovar** ou **Negar** para o script. Opcionalmente, insira um comentário sobre sua decisão.  Se você negar um script, ele não poderá ser executado em dispositivos cliente. <br>
![Script – Aprovação](./media/run-scripts/RS-approval.png)
1. Conclua o assistente. Na lista **Script**, você verá a coluna **Estado de Aprovação** mudar dependendo da ação executada.

### <a name="allow-users-to-approve-their-own-scripts"></a>Permitir que os usuários aprovem seus próprios scripts

Essa aprovação é usada principalmente para a fase de teste do desenvolvimento do script.

1. No console do Configuration Manager, clique em **Administração**.
2. No workspace **Administração**, expanda **Configuração do Site** e clique em **Sites**.
3. Na lista de sites, escolha seu site e, depois, na guia **Início**, no grupo **Sites**, clique em **Configurações de Hierarquia**.
4. Na guia **Geral** da caixa de diálogo **Propriedades de configurações de hierarquia**, desmarque a caixa de seleção **Autores de scripts exigem um aprovador de script adicional**.

>[!IMPORTANT]
>Como prática recomendada, você não deve permitir que um autor de script aprove seus próprios scripts. Isso deve ser permitido somente em uma configuração de laboratório. Considere atentamente o possível impacto de alterar essa configuração em um ambiente de produção.

## <a name="security-scopes"></a>Escopos de segurança
*(Introduzido na versão 1710)*  
O recurso Executar Scripts usa os escopos de segurança, um recurso existente do Configuration Manager, para controlar a criação e execução de scripts por meio da atribuição de marcas que representam grupos de usuários. Para obter mais informações de como usar escopos de segurança, consulte [Configurar administração baseada em funções para o System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="bkmk_ScriptRoles"></a> Criar funções de segurança para scripts
As três funções de segurança usadas para executar scripts não são criadas por padrão no Configuration Manager. Para criar as funções de executores, autores e aprovadores de script, siga as etapas descritas.

1. No console do Configuration Manager, acesse **Administração** >**Segurança** >**Funções de Segurança**
2. Clique com o botão direito do mouse em uma função e clique em **Copiar**. A função copiada tem permissões já atribuídas. Use somente as permissões desejadas. 
3. Forneça à função personalizada um **Nome** e uma **Descrição**. 
4. Atribua a função de segurança às permissões descritas abaixo.  

### <a name="security-role-permissions"></a>Permissões de função de segurança  

**Nome da Função**: Executores de Script  
- **Descrição**: com essas permissões, a função executa apenas os scripts que foram criados anteriormente e aprovados por outras funções.  
- **Permissões:** verifique se a opção a seguir está definida como **Sim**.  

|Categoria|Permissão|Estado|
|---|---|---|
|Coleta|Executar Script|Sim|
|Site|Ler|Sim|
|Scripts do SMS|Ler|Sim|


**Nome da Função**: Autores do Script  
- **Descrição**: com essas permissões, a função cria scripts, mas elas não podem aprová-los nem os executar.  
- **Permissões**: verifique se as permissões a seguir estão definidas.
 
|Categoria|Permissão|Estado|
|---|---|---|
|Coleta|Executar Script|Não|
|Site|Ler|Sim|
|Scripts do SMS|Criar|Sim|
|Scripts do SMS|Ler|Sim|
|Scripts do SMS|Excluir|Sim|
|Scripts do SMS|Modificar|Sim|


**Nome da Função**: aprovadores do script  
- **Descrição**: com essas permissões, a função aprova scripts, mas elas não podem criá-los nem executá-los.  
- **Permissões:** verifique se as permissões a seguir estão definidas.  

|Categoria|Permissão|Estado|
|---|---|---|
|Coleta|Executar Script|Não|
|Site|Ler|Sim|
|Scripts do SMS|Ler|Sim|
|Scripts do SMS|Aprovar|Sim|
|Scripts do SMS|Modificar|Sim|

     
**Exemplo de permissões de Scripts do SMS para a função de criadores de script**  

 ![Exemplo de permissões de Scripts do SMS para a função de criadores de script](./media/run-scripts/script_authors_permissions.png)


## <a name="create-a-script"></a>Criar um script

1. No console do Configuration Manager, clique em **Biblioteca de Software**.
2. No workspace **Biblioteca de Software**, clique em **Scripts**.
3. Na guia **Início**, no grupo **Criar**, clique em **Criar Script**.
4. Na página **Script** do assistente para Criar **Script**, configure o seguinte:
    - **Nome do Script** - insira um nome para o script. Embora você possa criar vários scripts com o mesmo nome, o uso de nomes duplicados dificultará mais a localização do script necessário no console do Configuration Manager.
    - **Linguagem do script** – Atualmente, apenas scripts do PowerShell têm suporte.
    - **Importar** - importe um script do PowerShell no console. O script é exibido no campo **Script**.
    - **Limpar** – Remove o script atual do campo Script.
    - **Script** - exibe o script importado no momento. Edite o script neste campo conforme o necessário.
5. Conclua o assistente. O novo script é exibido na lista **Script** com um status de **Aguardando aprovação**. Antes de executar esse script em dispositivos cliente, você deve aprová-lo. 

> [!IMPORTANT]
> Evite gerar script de uma reinicialização do dispositivo ou de um reinício do agente do Configuration Manager quando usar o recurso Executar Scripts. Isto pode levar a um estado contínuo de reinicialização. Se necessário, há melhorias no recurso de notificação de cliente que permitem reiniciar os dispositivos, começando na versão 1710 do Configuration Manager. A [coluna de reinicialização pendente](/sccm/core/clients/manage/manage-clients#restart-clients) pode ajudar a identificar os dispositivos que precisam de uma reinicialização. 
> <!--SMS503978  -->

## <a name="script-parameters"></a>Parâmetros do script
*(Introduzido na versão 1710)*  
Adicionar parâmetros a um script oferece maior flexibilidade para o seu trabalho. Você pode incluir até dez parâmetros. A seguir, é descrita a funcionalidade atual do recurso Executar Scripts com os parâmetros do script para os tipos de dados *String* e *Integer*. Também há listas de valores predefinidos disponíveis. Se o seu script tiver tipos de dados sem suporte, você receberá um aviso.

Na caixa de diálogo **Criar Script**, clique em **Parâmetros do Script** em **Script**.

Cada um dos parâmetros do script tem sua própria caixa de diálogo para adicionar mais detalhes e validação. Se houver um parâmetro padrão no script, ele será enumerado na interface de usuário do parâmetro e você poderá defini-lo. O Configuration Manager não substituirá o valor padrão, pois ele nunca modificará o script diretamente. Você pode pensar nisso como "valores sugeridos pré-preenchidos" são fornecidos na interface do usuário, mas o Configuration Manager não fornece acesso a valores "padrão" em tempo de execução. Isso pode ser contornado editando o script para ter os padrões corretos. <!--17694323-->

>[!IMPORTANT]
> Os valores de parâmetro não podem conter um apóstrofo. </br></br>
> Há um problema conhecido no Configuration Manager versão 1802, em que os parâmetros com espaços não são passados ​​para o script corretamente. Se um espaço é usado no parâmetro, somente o primeiro item no parâmetro é passado para o script e todo o conteúdo depois do espaço não é passado. Os administradores podem criar scripts para isso, substituindo espaços por espaços de caracteres alternativos e convertendo-os, ou usando outros métodos.


### <a name="parameter-validation"></a>Validação de parâmetro

Cada parâmetro no script tem uma caixa de diálogo **Propriedades do Parâmetro do Script** para adicionar validação para esse parâmetro. Depois de adicionar a validação, ao inserir um valor para o parâmetro que não esteja de acordo com a sua validação, você receberá um erro.

#### <a name="example-firstname"></a>Exemplo: *FirstName*

Neste exemplo, é possível definir as propriedades do parâmetro de cadeia de caracteres *FirstName*.

![Parâmetros de script – cadeia de caracteres](./media/run-scripts/RS-parameters-string.png)


A seção de validação da caixa de diálogo **Propriedades do Parâmetro de Script** contém os seguintes campos para seu uso:

- **Tamanho Mínimo** – número mínimo de caracteres do campo *FirstName*.
- **Tamanho Máximo** – número máximo de caracteres do campo *FirstName*.
- **RegEx** – abreviação de *Expressão Regular*. Para saber mais sobre como usar a Expressão Regular, confira a próxima seção, *Usar a validação de Expressão Regular*.
- **Erro Personalizado** – útil para adicionar sua própria mensagem de erro personalizada que substitui qualquer mensagem de erro de validação do sistema.

#### <a name="using-regular-expression-validation"></a>Uso da validação de Expressões Regulares

Uma expressão regular é uma forma compacta de programação para verificação de uma cadeia de caracteres com base em uma validação codificada. Por exemplo, você pode verificar a ausência de um caractere alfabético maiúsculo no campo *FirstName* colocando `[^A-Z]` no campo *RegEx*.

A expressão regular que processa essa caixa de diálogo tem suporte do .NET Framework. Para obter orientação sobre como usar expressões regulares, confira [Expressão Regular do .NET](https://docs.microsoft.com/dotnet/standard/base-types/regular-expressions). 


## <a name="script-examples"></a>Exemplos de script

Aqui estão alguns exemplos que ilustram os scripts que você poderá usar com essa capacidade.

### <a name="create-a-new-folder-and-file"></a>Criar uma nova pasta e arquivo

Esse script cria uma pasta e um arquivo na pasta, considerando a entrada de nomenclatura.

``` powershell
Param(
[Parameter(Mandatory=$True)]
[string]$FolderName,
[Parameter(Mandatory=$True)]
[string]$FileName
)

New-Item $FolderName -type directory
New-Item $FileName -type file
```

### <a name="get-os-version"></a>Obter a versão do SO

Esse script usa a WMI para consultar o computador sobre a versão do SO.

``` powershell
Write-Output (Get-WmiObject -Class Win32_operatingSystem).Caption
```

## <a name="bkmk_psedit"></a> Editar ou copiar os scripts do PowerShell
<!--3705507-->
*(Introduzido na versão 1902)*  
É possível **Editar** ou **Copiar** um script existente do PowerShell usado com o recurso **Executar Scripts**. Em vez de recriar um script que você precisa alterar, agora pode editá-lo diretamente. As duas ações usam a mesma experiência do assistente de quando você cria um novo script. Quando você edita ou copia um script, o Configuration Manager não persiste o estado de aprovação.

> [!Tip]  
> Não edite um script que esteja sendo executado ativamente nos clientes. Eles não concluirão a execução do script original, e você pode não obter os resultados esperados desses clientes.  

### <a name="edit-a-script"></a>Editar um script

1. Vá para o **Scripts** nó sob o **biblioteca de Software** espaço de trabalho.
1. Selecione o script para editar e, em seguida, clique em **editar** na faixa de opções. 
1. Alterar ou importe novamente o script na **detalhes do Script** página.
1. Clique em **próxima** para exibir o **resumo** , em seguida, **fechar** quando tiver terminado de edição.

### <a name="copy-a-script"></a>Copiar um script

1. Vá para o **Scripts** nó sob o **biblioteca de Software** espaço de trabalho.
1. Selecione o script para copiar e, em seguida, clique em **cópia** na faixa de opções.
1. Renomeie o script a **nome do Script** campo e faça as edições adicionais que talvez seja necessário.
1. Clique em **próxima** para exibir o **resumo** , em seguida, **fechar** quando tiver terminado de edição.


## <a name="run-a-script"></a>Executar um script

Após a aprovação de um script, ele poderá ser executado em um dispositivo único ou uma coleção. Após o início da execução do script, ele é iniciado rapidamente por meio de um sistema de alta prioridade e o tempo limite esgota em uma hora. Os resultados do script são retornados usando um sistema de mensagem de estado.

Para selecionar uma coleção de destinos para seu script:

1. No console do Configuration Manager, clique em **Ativos e Conformidade**.
2. No workspace Ativos e Conformidade, clique em **Coleções de Dispositivos**.
3. Na lista **Coleções de Dispositivos**, clique na coleção de dispositivos na qual você deseja executar o script.
4. Selecione uma coleção de sua escolha, clique em **Executar Script**.
5. Na página **Script** do assistente **Executar Script**, escolha um script na lista. Somente scripts aprovados são exibidos.
6. Clique em **Avançar** e conclua o assistente.

> [!IMPORTANT]
> Se o script não for executado, por exemplo, porque um dispositivo de destino está desligado durante o período de uma hora, será necessário executá-lo novamente.

### <a name="target-machine-execution"></a>Execução do computador de destino

O script é executado como a conta do *sistema* ou do *computador* nos clientes de destino. Essa conta tem acesso à rede limitado. Qualquer acesso do script a sistemas remotos e locais deve ser provisionado adequadamente.

## <a name="script-monitoring"></a>Monitoramento do script

Depois de iniciar a execução de um script em uma coleção de dispositivos, use o procedimento a seguir para monitorar a operação. Começando na versão 1710, é possível monitorar um script em tempo real conforme ele é executado e também retornar a um relatório de uma determinada execução do recurso Executar Script. Os dados de status do script são limpos como parte da [tarefa de manutenção Excluir Operações Antigas do Cliente](../../core/servers/manage/reference-for-maintenance-tasks.md) ou da exclusão do script.<br>

![Monitor de script – Status da Execução do Script](./media/run-scripts/RS-monitoring-three-bar.png)

1. No console do Configuration Manager, clique em **Monitoramento**.
2. No workspace **Monitoramento**, clique em **Status do Script**.
3. Na lista **Status do Script**, veja os resultados de cada script executado em dispositivos cliente. Um código de saída do script de **0** geralmente indica que o script foi executado com êxito.
    - A partir do Configuration Manager 1802, a saída de script é truncada em 4 KB para permitir uma melhor experiência de exibição.  <!--510013-->
   
   ![Monitor de script – script truncado](./media/run-scripts/Script-monitoring-truncated.png)

## <a name="script-output-in-1810"></a>Saída de script no 1810

Você pode exibir a saída detalhada do script em formato JSON bruto ou estruturado. Essa formatação facilita a leitura e a análise da saída. Se o script retornar um texto formatado em JSON válido, exiba a saída detalhada como **Saída JSON** ou **Saída Raw**. Caso contrário, a única opção será **Saída do Script**.

### <a name="example-script-output-is-valid-json"></a>Exemplo: a saída do script é um JSON válido
Comando: `$PSVersionTable.PSVersion`  

Saída:  
```
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

### <a name="example-script-output-isnt-valid-json"></a>Exemplo: a saída do script não é um JSON válido
Comando: `Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

Saída:  
```
Microsoft Windows 10 Enterprise
```

- Os clientes do 1810 retornam uma saída menor do que 80 KB para o site por meio de um canal de comunicação rápido. Essa alteração aumenta o desempenho da exibição da saída do script ou da consulta.  

  - Se a saída do script ou da consulta for maior que 80 KB, o cliente enviará os dados por meio de uma mensagem de estado.  
  - Clientes anteriores a versão 1802 continuam a usar mensagens de estado.

## <a name="script-output-pre-1810"></a>Saída de script pré-1810

- A partir do Configuration Manager versão 1802, a saída de script é retornada com a formatação JSON. Este formato retorna consistentemente uma saída de script legível. 
- Os scripts que obtêm um resultado desconhecido ou em que o cliente estava offline, não serão mostrados no conjunto de dados ou nos gráficos. <!--507179-->
- Evite retornar uma saída de script grande, pois ela será truncada em 4 KB. <!--508488-->
- Algumas funcionalidades com a formatação de saída de script não estão disponíveis durante a execução do Configuration Manager versão 1802 ou posterior com uma versão de nível inferior do cliente. <!--508487-->
    - Quando você tiver um cliente do Configuration Manager anterior ao 1802, poderá obter uma saída de cadeia de caracteres.
    -  Para o cliente do Configuration Manager versão 1802 e superior, você obtém a formatação JSON.
        - Por exemplo, você pode obter resultados que indicam TEXT em uma versão do cliente e “TEXT” (a saída é colocada entre aspas duplas) em outra versão, o que será colocado no gráfico como duas categorias diferentes.
        - Se você precisar solucionar esse problema, considere a possibilidade de executar o script em duas coleções diferentes. Uma com clientes anteriores à 1802 e outra com clientes 1802 e superiores. Ou você pode converter um objeto de enumeração em um valor de cadeia de caracteres nos scripts, para que eles sejam exibidos corretamente na formatação JSON. 
- Converta um objeto de enumeração em um valor de cadeia de caracteres nos scripts para que sejam exibidos corretamente na formatação JSON. <!--508377-->

   ![Converter um objeto de enumeração em um valor de cadeia de caracteres](./media/run-scripts/enum-tostring-JSON.png)

## <a name="log-files"></a>Arquivos de log

A partir da versão 1810, o registro em log extra foi adicionado para solução de problemas.

- No cliente, por padrão, em C:\Windows\CCM\logs:  
  - **Scripts.log**  
  - **CcmMessaging.log**  

- No MP, por padrão em C:\SMS_CCM\Logs:
  - **MP_RelayMsgMgr.log**  

- No servidor do site, por padrão, em C:\Arquivos de Programas\Configuration Manager\Logs:
  - **SMS_Message_Processing_Engine.log**

## <a name="see-also"></a>Consulte também

- [Configurar administração baseada em funções para o System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
- [Fundamentos da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration)
