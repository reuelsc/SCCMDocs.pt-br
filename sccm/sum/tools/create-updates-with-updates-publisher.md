---
title: Criar atualizações
titleSuffix: Configuration Manager
description: Criar e agrupar atualizações de software com o System Center Updates Publisher
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 46a1a8ac-126c-4ee6-ae09-32dfbdb83368
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e60ce54c5f792f7ea9c7a6c6d05b32c79c1e9b8d
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67678789"
---
# <a name="create--software-updates-and-update-bundles-with-updates-publisher"></a>Criar atualizações de software e pacotes de atualização com o Updates Publisher

*Aplica-se ao: System Center Updates Publisher*

Com o Updates Publisher, você pode usar o assistente **Criar Atualização** para criar suas próprias atualizações, e o assistente **Criar Pacote** para criar pacotes de atualizações.

Como esses dois assistentes têm um fluxo de trabalho semelhante, o procedimento para criar um pacote de atualização refere-se ao procedimento para criar atualizações, apenas com as diferenças relevantes detalhadas.

## <a name="use-the-create-update-wizard"></a>Usar o assistente para Criar Atualizações
1. No console, acesse o **Workspace de Atualizações** e, no painel **Introdução**, escolha **Atualização** na guia **Início** da faixa de opções. Isso abre o assistente para **Criar Atualização**.

2. Na página **Pacote**, use as seguintes informações para ajudar a configurar a atualização:

   -   Escolha **Procurar** para localizar o pacote de atualização de software que você usará como uma origem do pacote. As origens válidas incluem arquivos .MSI, .MSP ou .EXE. O Updates Publisher requer acesso ao arquivo para criar um hash de arquivo. O hash e o nome do arquivo são usados nos metadados da atualização que você está criando.

   -   Especifique o local de origem do conteúdo dessa atualização. Normalmente, esse é o local de onde os binários de atualização serão baixados durante a publicação para um servidor do WSUS.  Se a opção **Usar um local de origem para publicar o conteúdo de atualização de software** estiver selecionada, o caminho não será necessário.

       Posteriormente, quando a atualização for publicada em um servidor WSUS, o Updates Publisher baixará os binários da atualização no local de origem indicado.  Se nenhum caminho for fornecido, o Update Publisher pesquisará o [caminho de publicação da origem local](/sccm/sum/tools/updates-publisher-options#advanced) para os binários de atualização.

   -   Especifique o **Idioma binário** da atualização de software.

   -   Especifique os **Códigos de retorno em caso de êxito** e os **Códigos de reinicialização pendente em caso de êxito** da atualização. Separe vários códigos de retorno usando vírgulas. Use os códigos de retorno para determinar quando a instalação da atualização foi bem-sucedida e quando uma reinicialização é necessária.

       -   Os arquivos do instalador e patches do Windows (arquivos .MSI e .MSP) definem automaticamente esses valores e não podem ser modificados.

       -   Para atualizações em .EXE, os códigos padrão definidos pelo arquivo .EXE são usados se nenhum código de retorno for especificado.

   -   Especifique quaisquer argumentos de linha de comando exigidos para a instalação da atualização de software.

       -   Os arquivos do instalador e patches do Windows (arquivos .MSI e .MSP) definem automaticamente esses valores. Para esses tipos de arquivos os argumentos devem ser especificados como **\[nome\]=\[valor\]** . Além disso, todas as opções que começam com um **/** (como **/qn**) não têm suporte para atualizações de software .MSI ou .MSP.

       -   Para atualizações .EXE, todos os argumentos são válidos.

3. Na página **Informações**, especifique os detalhes sobre a atualização que são incluídas quando a atualização for publicada ou exportada. Os detalhes incluem propriedades localizadas, como o nome das atualizações (título) e a descrição. Em seguida, especifique detalhes mais gerais, como a classificação, o fornecedor, o produto e onde aprender mais sobre a atualização.

    __Propriedades localizadas:__

   - **Idioma**: selecione um idioma e especifique um título e uma descrição. Selecione outros idiomas, um por vez, e o próprio título e descrição de cada um deles.

   - **Título**: insira o nome do banco de dados. Esse nome é exibido no Workspace de Atualizações do console Updates Publisher.

   - **Descrição**: uma descrição amigável da atualização. Você pode incluir o que a atualização instala e porque ou quando ela deve ser usada.

   **Classificação:** as opções a seguir são descrições comuns para classificações diferentes.

   - **Atualizar**: uma atualização para um aplicativo ou arquivo instalado no momento.

   - **Crítica**: uma atualização lançada em larga escala para um problema específico que soluciona um bug crítico não relacionado à segurança.

   - **Pacote de Recursos**: novos recursos de produtos que são distribuídos fora de um lançamento de produto e que normalmente são incluídos no próximo lançamento do produto completo.

   - **Segurança**: uma atualização lançada em larga escala para um problema específico a um produto relacionado à segurança.

   - **Pacote Cumulativo de Atualizações**: um conjunto cumulativo de hotfixes reunidos para facilitar a implantação. Esses hotfixes podem incluir atualizações de segurança, atualizações críticas, atualizações e assim por diante. Um pacote cumulativo de atualizações geralmente aborda uma área específica, como segurança ou um recurso do produto.

   - **Service Pack**: um conjunto cumulativo de hotfixes que são aplicados a um aplicativo. Esses hotfixes podem incluir atualizações de segurança, atualizações críticas, atualizações de software e assim por diante.

   - **Ferramenta**: especificam uma ferramenta ou recurso que ajuda a concluir uma ou mais tarefas.

   - **Driver**: uma atualização de um driver de software.

   **Fornecedor**: especifica um fornecedor para a atualização. Use a lista suspensa para usar valores de atualizações que estão no repositório. Quando você especifica um fornecedor, o assistente cria uma pasta com o nome desse fornecedor em **Todas as Atualizações de Software** no **Workspace de Atualizações**, caso essa pasta ainda não exista. Os nomes a seguir são nomes do WSUS (Windows Server Update Services) reservados que não podem ser inseridos para as atualizações criadas por você:
   - Microsoft Corporation
   - Microsoft
   - Atualização
   - Atualização de Software
   - Ferramentas
   - Ferramenta
   - Crítico
   - Atualizações Críticas
   - Segurança
   - Atualizações de Segurança
   - Pacote de Recursos
   - Pacote Cumulativo de Atualizações
   - Service Pack
   - Driver
   - Atualização de Driver
   - Pacote
   - Atualização do Pacote

   **Produto**: especifique o tipo de produto da atualização. Use a lista suspensa para usar valores de atualizações que estão no repositório. A mesma lista com os nomes reservados do WSUS que não podem ser usados para **Fornecedor**, não pode ser usada para **Produto**.

   **URL de informações adicionais**: especifique a URL onde você pode encontrar mais informações sobre essa atualização. Use letras minúsculas para **https** ou **http** quando inserir essa URL.

4. Na página **Informações Opcionais**, configure os detalhes que fornecem mais informações sobre a atualização.

   -   **ID do Boletim**: IDs de boletim são normalmente, mas nem sempre, oferecidas pelos fornecedores de atualização.

   -   **ID do Artigo**: se um artigo de atualização de software estiver disponível, a ID do Artigo poderá ser útil para pessoas que buscam informações adicionais sobre a atualização.

   -   **IDs de CVE:** lista um ou mais identificadores de CVE (Vulnerabilidades e exposições comuns) que fornecem informações de segurança sobre a atualização ou pacote de atualizações. Ao listar mais de um, use um ponto e vírgula para separar os CVEs, como neste exemplo: *CVE1; CVE2.*

   -   **URL de Suporte:** lista a URL que contém informações de suporte para esta atualização, se houver alguma disponível. Use letras minúsculas para **https** ou **http** quando inserir essa URL.

   -   **Gravidade:** defina o nível de gravidade dessa atualização.

   -   **Impacto:** as opções a seguir podem ser usadas para especificar o impacto:
       -   **Normal –** use para indicar que a atualização exige procedimentos de instalação típicos.
       -   **Secundário –** use para indicar que a atualização exige procedimentos mínimos de instalação.
       -   **Requer um tratamento exclusivo –** use para indicar que a atualização deve ser instalada sozinha, separada de outras atualizações.   <br /><br />

   -   **Comportamento de Reinicialização:** use para fornecer informações sobre o comportamento de reinicialização das atualizações. Essa configuração não afeta o comportamento real da instalação da atualização.

       -   **Nunca reinicia**: o computador nunca executa uma reinicialização do sistema após a instalação da atualização de software.
       -   **Sempre exige reinicialização**: o computador sempre executa uma reinicialização do sistema após a instalação da atualização de software.
       -   **Pode solicitar reinicialização**: depois de instalar a atualização de software, o computador solicitará uma reinicialização do sistema somente se for necessário. O usuário tem a opção de adiar a reinicialização. Este é o valor padrão. <br /><br />

5. Na página **Pré-requisito**, especifique os pré-requisitos que devem ser instalados em um computador para que essa atualização possa ser instalada. Os pré-requisitos podem ser **detectoids** ou outras atualizações. Detectoids são regras de alto nível, como uma que exige que a CPU dos computadores seja um processador de 64 bits. Os detectoids também podem especificar as atualizações específicas que devem ser instaladas antes que essa atualização possa ser instalada.

   -   Para obter o melhor desempenho, use detectoids em vez de criar *regras instaláveis* e *instaladas* que realizam a mesma verificação ou ação.

   Use a opção de pesquisa para encontrar **Atualizações de software e detectoids disponíveis** para ajudar você a encontrar atualizações ou detectoids específicos. Por exemplo, pesquise na **CPU** para localizar os detectoids que permitem a limitação da instalação com base na arquitetura de CPU específica.

   Você pode selecionar um ou mais itens por vez para adicioná-los como um pré-requisito. Ao adicionar os pré-requisitos, os detectoids selecionados são adicionados como um ou mais grupos. Para se qualificar para a instalação, um computador deve atender aos requisitos de pelo menos um membro de cada grupo configurado:

   -   Quando você clica em **Adicionar Pré-requisito**, todos os itens que você selecionou são adicionados a grupos individuais e separados. Para se qualificar para essa atualização, um computador deve atender aos pré-requisitos desse grupo e passar os requisitos a todos os grupos adicionais configurados.

   -   Quando você clica em **Adicionar Grupo**, todos os itens que você selecionou são adicionados a um único grupo. Para se qualificar para essa atualização, um computador deve atender a pelo menos um dos pré-requisitos desse grupo e passar os requisitos a todos os grupos adicionais configurados.

6. Na página **Substituição**, especifique as atualizações que são substituídas por essa atualização. Quando essa atualização for publicada, o Configuration Manager marcará cada atualização substituída como **Expirada**. Os clientes instalarão essa atualização em vez das atualizações substituídas.

7. Na página **Aplicabilidade**, use o **Editor de Regras** para definir um conjunto de regras que determina se um dispositivo precisa dessa atualização. (Esta página é semelhante à página **Instaladas**, que vem logo em seguida.)

   Para adicionar uma nova regra, clique em ![Nova Regra](media/newrule.png). Isso abre a página Regra de Aplicabilidade, na qual é possível configurar regras.

   Entre os tipos de regras que você pode criar estão:

   -   **Arquivo** – use essa regra para exigir que um dispositivo tenha um arquivo com propriedades que atendam a um ou mais critérios especificados por você antes que essa atualização possa ser aplicada.

   -   **Registro –** use este tipo para especificar detalhes do registro que devem estar presentes para que um dispositivo se qualifique para instalar essa atualização.

   -   **Sistema –** essa regra usa os detalhes do sistema para determinar a aplicabilidade. Você pode escolher entre a definição de uma versão do Windows, um idioma do Windows, a arquitetura do processador ou especificar uma consulta no WMI para identificar o sistema operacional dos dispositivos.

   -   **Windows Installer –** use esse tipo de regra para determinar a aplicabilidade com base em um .MSI instalado ou em um patch do Windows Installer (.MSP). Você também pode determinar se há recursos ou componentes específicos instalados como parte do requisito.

       > [!IMPORTANT]  
       > Em dispositivos gerenciados, o Windows Update Agent não pode detectar pacotes de instalação do Windows instalados por usuário. Ao usar esse tipo de regra, configure outras regras de aplicabilidade, como versões de arquivo ou valores de chave do Registro, para que o pacote do Windows Installer possa ser detectado corretamente, independentemente de ter base no usuário ou no sistema.

   -   **Salvar regra –** Essa opção permite que você localize e use regras *criadas por você no Workspace de Regras*.

       Depois de criar uma regra, use os outros ícones para modificar a regra e, se houver várias regras, para definir relações entre essas regras.

   Após a conclusão da criação e adição de regras, clique em **OK** na caixa de diálogo **Criar Conjunto de Regras** para salvar esse conjunto. Depois, crie uma **Nova** regra e adicione-a ao conjunto também.

   Quando você tiver várias regras ou conjuntos de regras para adicionar a uma atualização, use os operadores lógicos no **Editor de Regras** para determinar as condições entre as regras e ordem na qual são processadas.

8. Na página**Instaladas**, use o **Editor de Regras** para definir um conjunto de regras que determinam se um dispositivo já instalou a atualização que você está configurando. (Essa página é semelhante á página **Aplicabilidade**, que vem antes desta página.)

   Esta página do assistente oferece suporte a regras de configuração com as mesmas opções e critérios que a página **Aplicabilidade**.

   Após a conclusão do assistente, a nova atualização é adicionada a um nó no **Workspace de Atualizações** identificado pelo nome do **Fornecedor** e **Produto** usado para essa atualização.

## <a name="use-the-create-bundle-wizard"></a>Usar o assistente para Criar Pacote
Como o assistente usa o mesmo fluxo de trabalho que o [assistente para Criar Atualização](#use-the-create-update-wizard), use o fluxo de trabalho, mas observe as seguintes diferenças para pacotes:

1.  Para iniciar o assistente, no console, acesse **Workspace de Atualizações** e selecione **Pacote** na guia **Início** da faixa de opções.

2.  Diferentemente do assistente para Criar Atualização, não há uma página Pacote durante a criação de um pacote.

3.  Na página **Informações**, especifique os detalhes sobre o pacote de atualizações incluído quando a atualização for publicada ou exportada.

4.  Na página **Informações Opcionais**, configure os detalhes que fornecem mais informações sobre o pacote de atualizações. As opções disponíveis são as mesmas para a criação de uma atualização. No entanto, as opções de Impacto e Comportamento de Reinicialização não estão disponíveis, pois não se aplicam aos pacotes.

5.  Na página **Pré-requisito**, especifique os pré-requisitos que devem ser instalados em um computador para que esse pacote possa ser instalado. Essas regras são as mesmas para as atualizações individuais.

6.  Na página **Substituição**, especifique as atualizações que são substituídas por esse pacote. Essas regras são as mesmas para as atualizações individuais.

7.  Na página **Membros**, selecione as atualizações para adicionar ao pacote de atualizações. Somente as atualizações criadas ou importadas no Updates Publisher estarão disponíveis.

Após a conclusão do assistente, o novo pacote de atualizações é adicionado a um nó no **Workspace de Atualizações** identificado pelo nome do **Fornecedor** usado para o pacote de atualizações.
