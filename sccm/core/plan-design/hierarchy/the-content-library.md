---
title: A biblioteca de conteúdo
titleSuffix: Configuration Manager
description: Saiba mais sobre a biblioteca de conteúdo que o Configuration Manager usa para reduzir o tamanho geral do conteúdo distribuído.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b6251bfa098f575662d1a1c0dbf742b35af05846
ms.sourcegitcommit: d8d142044586a53709b4478ad945f714737c8d6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58523938"
---
# <a name="the-content-library-in-configuration-manager"></a>A biblioteca de conteúdo no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A biblioteca de conteúdo é um armazenamento de uma única instância de conteúdo no Configuration Manager. Ela é usada pelo site para reduzir o tamanho geral do corpo de conteúdo combinado que você distribui. A biblioteca de conteúdo armazena todos os arquivos de conteúdo das implantações de software, por exemplo: atualizações de software, aplicativos e implantações de sistema operacional.  

- O site cria e mantém automaticamente uma cópia da biblioteca de conteúdo em cada servidor do site e em cada ponto de distribuição.  

- Antes que o Configuration Manager baixe os arquivos de conteúdo para o servidor do site ou copie os arquivos nos pontos de distribuição, ele verifica se cada arquivo de conteúdo já está na biblioteca de conteúdo.  

- Quando o arquivo de conteúdo está disponível, o Configuration Manager não copia o arquivo. Nesse caso, ele associa o arquivo de conteúdo existente ao aplicativo ou pacote.  

Nos servidores de ponto de distribuição, configure as seguintes opções:

- Uma ou mais unidades de disco nas quais você deseja criar a biblioteca de conteúdo.  

- Uma prioridade para cada unidade que você usa.  

O Configuration Manager copia os arquivos de conteúdo na unidade com a prioridade mais alta até que essa unidade contenha menos que uma quantidade mínima de espaço livre que você especifica.  

- Você pode definir as configurações da unidade durante a instalação do ponto de distribuição.  

- Não é possível definir as configurações da unidade nas propriedades do ponto de distribuição após a conclusão da instalação.  


Para obter mais informações de como definir as configurações de unidade para o ponto de distribuição, confira [Gerenciar o conteúdo e a infraestrutura de conteúdo](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  


> [!IMPORTANT]
>  Para mover a biblioteca de conteúdo para um local diferente em um ponto de distribuição após a instalação, use a ferramenta **Transferência de Biblioteca de Conteúdo** nas ferramentas do Configuration Manager. Para obter mais informações, confira a [ferramenta de Transferência de Biblioteca de Conteúdo](/sccm/core/support/content-library-transfer).  



## <a name="about-the-content-library-on-the-central-administration-site"></a>Sobre a biblioteca de conteúdo no site de administração central  
Por padrão, o Configuration Manager cria uma biblioteca de conteúdo no site de administração central quando o site é instalado. A biblioteca de conteúdo é colocada na unidade do servidor do site com mais espaço livre em disco. Como não é possível instalar um ponto de distribuição no site de administração central, você não pode priorizar as unidades a serem usadas pela biblioteca de conteúdo. Semelhante à biblioteca de conteúdo em outros servidores de site e em pontos de distribuição, quando a unidade que contém a biblioteca de conteúdo fica sem espaço em disco disponível, a biblioteca de conteúdo passa automaticamente para a próxima unidade disponível.  

O Configuration Manager usa a biblioteca de conteúdo no site de administração central nos seguintes cenários:  

- Quando você cria conteúdo no site de administração central  

- Quando você migra conteúdo de outro site do Configuration Manager e atribui o site de administração central como o site que gerencia esse conteúdo  

> [!NOTE]  
>  Quando você cria conteúdo em um site primário e o distribui a um site primário diferente ou a um site secundário abaixo de um site primário diferente, o site de administração central armazena temporariamente esse conteúdo na caixa de entrada do agendador no site de administração central, mas não adiciona o conteúdo à sua biblioteca de conteúdo.  

Use as opções a seguir para gerenciar a biblioteca de conteúdo no site de administração central:  

- Para impedir que a biblioteca de conteúdo seja instalada em uma unidade específica, crie um arquivo vazio chamado **no_sms_on_drive.sms**. Copie-o na raiz da unidade antes de criar a biblioteca de conteúdo.  

- Depois que a biblioteca de conteúdo for criada, use a ferramenta **Transferência de Biblioteca de Conteúdo** das ferramentas do Configuration Manager para gerenciar o local da biblioteca de conteúdo. Para obter mais informações, confira a [ferramenta de Transferência de Biblioteca de Conteúdo](/sccm/core/support/content-library-transfer).  

> [!Note]  
> Os pontos de distribuição na nuvem não usam o armazenamento de uma única instância. O site criptografa os pacotes antes de enviá-los ao Azure, e cada pacote tem uma chave criptografada exclusiva. Mesmo se dois arquivos forem idênticos, as versões criptografadas não serão iguais.  



## <a name="bkmk_remote"></a> Configurar uma biblioteca de conteúdo remoto para o servidor do site  
<!--1357525-->
Começando na versão 1806, para configurar a [alta disponibilidade do servidor do site](/sccm/core/servers/deploy/configure/site-server-high-availability) ou liberar espaço no disco rígido na administração central ou nos servidores de site primário, realoque a biblioteca de conteúdo para outro local de armazenamento. Mova a biblioteca de conteúdo para outra unidade no servidor do site, para um servidor separado ou para discos tolerantes a falhas em uma rede SAN (rede de área de armazenamento). A SAN é recomendada, porque é altamente disponível e fornece armazenamento elástico que aumenta ou diminui ao longo do tempo para atender às necessidades dinâmicas de conteúdo. Para obter mais informações, confira [Opções de alta disponibilidade](/sccm/protect/understand/high-availability-options).

A biblioteca de conteúdo remota é um pré-requisito para [alta disponibilidade da função de servidor do site](/sccm/core/servers/deploy/configure/site-server-high-availability). 

> [!Note]  
> Essa ação só move a biblioteca de conteúdo no servidor do site. Ela não afeta a localização da biblioteca de conteúdo nos pontos de distribuição. 

> [!Tip]  
> Além disso, planeje o gerenciamento de conteúdo da origem do pacote, que é externo à biblioteca de conteúdo. Cada objeto de software no Configuration Manager tem uma fonte de pacote em um compartilhamento de rede. Considere a centralização de todas as fontes em um único compartilhamento, mas verifique se esse local é redundante e altamente disponível. 
> 
> Se você mover a biblioteca de conteúdo para o mesmo volume de armazenamento que suas origens de pacote, não poderá marcar este volume para eliminação de duplicação de dados. Embora a biblioteca de conteúdo tenha suporte para eliminação de duplicação de dados, o volume de fontes de pacote não dá suporte a isso. Para obter mais informações, confira [Eliminação de duplicação de dados](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#bkmmk_datadedup).<!--SCCMDOcs issue #831-->  


### <a name="prerequisites"></a>Pré-requisitos  

- A conta de computador do servidor do site precisa de permissões de **Controle total** para o caminho de rede para o qual você está transferindo a biblioteca de conteúdo. Essa permissão se aplica ao compartilhamento e ao sistema de arquivos. Nenhum dos componentes são instalados no sistema remoto.

- O servidor do site não pode ter a função de ponto de distribuição. O ponto de distribuição também usa a biblioteca de conteúdo, e essa função não dá suporte para biblioteca de conteúdo remota. Depois de mover a biblioteca de conteúdo, você não pode mais adicionar a função de ponto de distribuição ao servidor do site.  

> [!Important]  
> Não reutilize um local de rede compartilhada entre vários sites. Por exemplo, não use o mesmo caminho para um site de administração central e um site primário filho. Essa configuração pode corromper a biblioteca de conteúdo e exigir que você a recompile.<!--SCCMDocs-pr issue 2764-->  


### <a name="process-to-manage-the-content-library"></a>Processo para gerenciar a biblioteca de conteúdo

1. Crie uma pasta em um compartilhamento de rede como o destino da biblioteca de conteúdo. Por exemplo, `\\server\share\folder`.  

    > [!Warning]  
    > Não reutilize uma pasta existente com conteúdo. Por exemplo, não use a mesma pasta que suas fontes de pacote. Antes de copiar a biblioteca de conteúdo, o Configuration Manager remove qualquer conteúdo existente do local especificado.  

2. No console do Configuration Manager, alterne para o workspace **Administração**. Expanda **Configuração do Site**, selecione o nó **Sites** e selecione o site. Na guia **Resumo** na parte inferior do painel de detalhes, observe uma nova coluna para a **Biblioteca de Conteúdo**.  

3. Clique em **Gerenciar Biblioteca de Conteúdo** na faixa de opções.   

4. Na janela Gerenciar Biblioteca de Conteúdo, o campo **Local Atual** mostra a unidade e o caminho local. Insira um caminho de rede válido para o **novo Local**. Esse caminho é a localização para o qual o site move a biblioteca de conteúdo. Ele precisa incluir um nome de pasta que já exista no compartilhamento, por exemplo, `\\server\share\folder`. Clique em **OK**.  

5. Observe o valor de **Status** na coluna Biblioteca de Conteúdo na guia Resumo do painel de detalhes. Ela é atualizada para mostrar o progresso da transferência da biblioteca de conteúdo.  

   - Enquanto o processo está **Em andamento**, o valor de **Progresso da movimentação (%)** exibe o percentual concluído.  

        > [!Note]  
        > Se você tiver uma grande biblioteca de conteúdo, poderá ver o progresso de `0%` no console por um tempo. Por exemplo, com uma biblioteca de 1 TB, ele precisa copiar 10 GB antes de mostrar `1%`. Revise o **distmgr.log**, que mostra o número de arquivos e bytes copiados. Começando na versão 1810, o arquivo de log também mostra um tempo estimado restante.

   - Se houver um estado de erro, o status exibirá o erro. Os erros comuns incluem **acesso negado** ou **disco cheio**.  

   - Ao concluir, ele exibe **Concluído**.  
    
     Consulte o **distmgr.log** para obter detalhes. Para saber mais, confira [Logs do servidor do site e do sistema de sites](/sccm/core/plan-design/hierarchy/log-files#BKMK_SiteSiteServerLog).  

Para obter mais informações sobre esse processo, confira [Fluxograma – gerenciar biblioteca de conteúdo](/sccm/core/plan-design/hierarchy/manage-content-library-flowchart).

Na verdade, o site *copia* os arquivos da biblioteca de conteúdo para o local remoto. Esse processo não exclui os arquivos da biblioteca de conteúdo no local original no servidor do site. Para liberar espaço, um administrador precisa excluir manualmente esses arquivos originais.

Se a biblioteca de conteúdo original abranger duas unidades, ela será mesclada em uma única pasta no novo destino. 

Começando na versão 1810, durante o processo de cópia, o site interrompe os componentes **Despooler** e **Gerenciador de distribuição**. Essa ação garante que o conteúdo não seja adicionado à biblioteca durante a transferência. Independentemente disso, agende essa alteração durante uma manutenção do sistema.

Se você precisar mover a biblioteca de conteúdo de volta para o servidor do site, repita esse processo, mas insira uma unidade local e o caminho para o **Novo Local**. Ele precisa incluir um nome de pasta que já exista na unidade, por exemplo, `D:\SCCMContentLib`. Quando o conteúdo original ainda existir, o processo moverá rapidamente a configuração do local para o servidor do site. 

> [!Tip]  
> Para mover o conteúdo para outra unidade no servidor do site, use a ferramenta **Transferência da Biblioteca de Conteúdo**. Para obter mais informações, confira a [ferramenta de Transferência de Biblioteca de Conteúdo](/sccm/core/support/content-library-transfer).  



## <a name="inside-the-content-library"></a>Por dentro da biblioteca de conteúdo

> [!Warning]  
> A seção a seguir é fornecida apenas para fins informativos. Não altere, adicione ou remova arquivos ou pastas na biblioteca de conteúdo. Isso pode corromper os pacotes, o conteúdo ou a biblioteca de conteúdo como um todo. Se você suspeitar que há dados ausentes, corrompidos ou inválidos de alguma forma, use o recurso de validação no console do Configuration Manager para detectar esses problemas. Em seguida, redistribua o conteúdo afetado para corrigir os problemas. 

Por padrão, a biblioteca de conteúdo é armazenada na raiz de uma unidade em uma pasta chamada **SCCMContentLib**. Essa pasta é compartilhada por padrão como **SCCMContentLib$**. A pasta e o compartilhamento têm permissões restritas para evitar danos acidentais. Todas as alterações devem ser feitas no console do Configuration Manager. Dentro dessa pasta estão os seguintes objetos:  

- A biblioteca de pacotes (pasta **PkgLib**): informações sobre quais pacotes estão presentes no ponto de distribuição.  

- A biblioteca de dados (pasta **DataLib**): informações sobre a estrutura original dos pacotes.  

- A biblioteca de arquivos (pasta **FileLib**): os arquivos originais no pacote. Essa pasta normalmente é a que usa a maior parte do armazenamento.  

![Visão geral do diagrama da biblioteca de conteúdo do Configuration Manager](media/content-library-overview.png)

> [!Tip]  
> Use a ferramenta **Gerenciador da Biblioteca de Conteúdo** nas ferramentas do Configuration Manager para procurar o conteúdo da biblioteca de conteúdo. Não é possível usar essa ferramenta para modificar o conteúdo. Ela fornece insights sobre o que está presente e o também permite a validação e a redistribuição. Para obter mais informações, confira o [Gerenciador da Biblioteca de Conteúdo](/sccm/core/support/content-library-explorer).  


### <a name="package-library"></a>Biblioteca de pacotes
A pasta da biblioteca de pacotes, **PkgLib**, inclui um arquivo para cada pacote distribuído ao ponto de distribuição. O nome do arquivo é a ID do pacote, por exemplo, `ABC00001.INI`. Nesse arquivo, na seção `[Packages]`, há uma lista de IDs de conteúdo que fazem parte do pacote e outras informações, como a versão. Por exemplo, **ABC00001** é um pacote herdado na versão **1**. A ID do conteúdo deste arquivo é `ABC00001.1`.


### <a name="data-library"></a>Biblioteca de dados
A pasta da biblioteca de dados, **DataLib**, inclui um arquivo e uma pasta para cada um dos conteúdos de cada pacote. Por exemplo, esse arquivo e pasta são nomeados como `ABC00001.1.INI` e `ABC00001.1`, respectivamente. O arquivo inclui informações de validação. A pasta recria a estrutura de pasta do pacote original. 

Os arquivos na biblioteca de dados são substituídos pelos arquivos INI com o nome do arquivo original no pacote. Por exemplo, `MyFile.exe.INI`. Esses arquivos incluem informações sobre o arquivo original, como o tamanho, a hora da modificação e o hash. Use os quatro primeiros caracteres do hash para localizar o arquivo original na biblioteca de arquivos. Por exemplo, o hash em MyFile.exe.INI é **DEF98765** e os primeiros quatro caracteres são **DEF9**.


### <a name="file-library"></a>Biblioteca de arquivos
Se a biblioteca de conteúdo abranger várias unidades, os arquivos de pacote poderão estar na pasta da biblioteca de arquivos, **FileLib**, em qualquer uma dessas unidades.

Localize um arquivo específico usando os quatro primeiros caracteres do hash encontrado na biblioteca de dados. Dentro da pasta da biblioteca de arquivos há muitas pastas, cada uma com um nome de quatro caracteres. Localize a pasta que corresponde aos quatro primeiros caracteres do hash. Depois de encontrar essa pasta, veja que ela inclui um ou mais conjuntos de três arquivos. Esses arquivos compartilham o mesmo nome, mas um tem a extensão INI, uma tem a extensão SIG e um não tem nenhuma extensão de arquivo. O arquivo original é aquele sem nenhuma extensão cujo nome é igual ao hash da biblioteca de dados.

Por exemplo, a pasta **DEF9** inclui `DEF98765.INI`, `DEF98765.SIG` e `DEF98765`. `DEF98765` é o `MyFile.exe` original. O arquivo INI inclui uma lista de IDs de "usuários" ou de conteúdo que compartilham o mesmo arquivo. O site não remove um arquivo, a menos que todos esses conteúdos também sejam removidos.


### <a name="drive-spanning"></a>Abrangência de unidade

A biblioteca de conteúdo pode abranger várias unidades. Ao criar o ponto de distribuição, você escolhe essas unidades. Por padrão, o Configuration Manager escolhe automaticamente as unidades ao abranger a biblioteca de conteúdo.

Quando você escolher as unidades, selecione uma unidade primária e uma secundária. O site armazena todos os metadados na unidade principal. Ele abrange apenas a biblioteca de arquivos até a unidade de secundária. O nome do compartilhamento da pasta das unidades secundárias inclui a letra da unidade. Por exemplo, se D: e E: forem unidades secundárias da biblioteca de conteúdo, os nomes de compartilhamento serão **SCCMContentLibD** e **SCCMContentLibE$**.

Se você escolher a opção **Automático**, o Configuration Manager selecionará a unidade com mais espaço livre disponível como sua principal unidade. Ele armazenará todos os metadados nessa unidade. O site abrange a biblioteca de arquivos apenas até as unidades secundárias. 

Você pode especificar uma quantidade de espaço de reserva durante a configuração. O Configuration Manager tentará usar um disco secundário quando o disco com maior espaço disponível tiver apenas essa quantidade de espaço de reserva restante livre. Sempre que uma nova unidade é selecionada para ser usada, a unidade com mais espaço livre disponível é selecionada.

Você não pode especificar que um ponto de distribuição deve usar todas as unidades, exceto para um conjunto específico. Evite esse comportamento criando um arquivo vazio na raiz da unidade, chamada `NO_SMS_ON_DRIVE.SMS`. Coloque esse arquivo antes que o Configuration Manager selecione a unidade a ser usada. Se o Configuration Manager detectar esse arquivo na raiz da unidade, ele não usará a unidade para a biblioteca de conteúdo. 



## <a name="troubleshooting"></a>Solução de problemas

As dicas a seguir podem ajudá-lo a solucionar problemas com a biblioteca de conteúdo:  

- Examine os logs no servidor do site (**distmgr.log** e **PkgXferMgr.log**) e o ponto de distribuição (**smsdpprov.log**) para buscar indicações sobre o motivo das falhas.  

- Use a ferramenta [Gerenciador da Biblioteca de Conteúdo](/sccm/core/support/content-library-explorer).  

- Verifique se há bloqueios de arquivo causados por outros processos, como software antivírus. Exclua a biblioteca de conteúdo em todas as unidades das verificações automáticas de antivírus, bem como o diretório de preparo temporário **SMS_DP$**, em cada unidade.  

- Para saber se há alguma incompatibilidade de hash, valide o pacote no console do Configuration Manager.  

- Como último recurso, redistribua o conteúdo. Essa ação deve resolver a maioria dos problemas.  

