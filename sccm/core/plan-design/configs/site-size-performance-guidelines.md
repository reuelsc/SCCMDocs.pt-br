---
title: Diretrizes sobre o porte e o desempenho do site
titleSuffix: Configuration Manager
description: Diretrizes, metodologia e resultados de teste de desempenho relacionados ao tamanho do site.
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/23/2019
ms.openlocfilehash: f6374e6237d586bb995e701e5577bfc553a5a689
ms.sourcegitcommit: cab3dba5ebfe90f28cedee03c1840c9a395160cc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/17/2019
ms.locfileid: "65849280"
---
# <a name="system-center-configuration-manager-site-size-and-performance-guidelines"></a>Diretrizes de desempenho e tamanho do site do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager é líder do setor em escalabilidade e desempenho. Outros documentos abordam os [limites de escalabilidade compatíveis máximos](size-and-scale-numbers.md) e as [diretrizes de hardware](recommended-hardware.md) para sites em execução nos maiores tamanhos de ambiente. Este artigo fornece diretrizes complementares de desempenho para ambientes de todos os tamanhos. Essas diretrizes podem ajudá-lo a estimar com mais precisão o hardware necessário para implantar o Configuration Manager.

Este artigo enfoca o fator que mais contribui para os gargalos de desempenho do Configuration Manager: o subsistema ou a IOPS de entrada/saída do disco. O artigo:

- Apresenta os detalhes e os resultados de teste com foco na IOPS
- Documenta como reproduzir os testes com seus próprios ambientes e hardware
- Sugere os requisitos de IOPS de disco para ambientes de vários tamanhos 

## <a name="performance-test-methodology"></a>Metodologia de teste de desempenho

Você pode implantar o Configuration Manager de muitas maneiras exclusivas, mas é importante entender algumas variáveis em discussões de dimensionamento. Uma variável é o *intervalo de recurso*, como um ciclo de inventário. Outra variável é o número de usuários, as implantações de software ou outros *objetos* referenciados ou implantados pelo sistema. O teste de desempenho aplica essas variáveis como parte de uma *carga*. A carga gera os objetos em uma taxa normal para clientes empresariais que usam implantações de produção em ambientes de diferentes tamanhos.

> [!NOTE] 
> Os dados telemétricos do cliente permitem o teste de builds do branch atual com os cenários, as configurações e as definições mais comuns para a maioria dos clientes. As recomendações deste artigo baseiam-se nessas médias. Suas experiências podem variar de acordo com o tamanho do ambiente e a configuração. Em geral, o Configuration Manager exige bom senso quando se trata de objetos e intervalos. Só porque você pode coletar todos os arquivos em um sistema ou definir o intervalo de um ciclo como um minuto, isso não significa que você deve fazer isso.

As seções a seguir destacam algumas das principais definições e configurações a serem usadas ao testar e modelar as necessidades de processamento para empresas de grande porte. Essas diretrizes ajudam a definir as expectativas do desempenho básico do sistema para os tamanhos de hardware sugeridos.

### <a name="feature-intervals-settings"></a>Configurações de intervalos de recurso 
A maioria dos testes deve usar intervalos padrão para os principais ciclos no sistema. Por exemplo, os testes de inventário de hardware ocorrem uma vez por semana com um arquivo *.mof* maior que o padrão. Alguns intervalos de recurso recorrentes, especialmente os ciclos de inventário de hardware e software, podem ter efeitos significativos nas características de desempenho de um ambiente. Os ambientes que permitem intervalos padrão agressivos para a coleta de dados precisam de um hardware extremamente grande, diretamente proporcional ao aumento da atividade. Por exemplo, digamos que você tenha 25.000 clientes de desktop e deseje coletar o inventário de hardware duas vezes mais rápido do que o intervalo padrão. Você deverá começar pelo dimensionamento do hardware do site, como se tivesse 50.000 clientes.

### <a name="objects"></a>Objetos 
Os testes devem usar a *média superior* dos objetos que as empresas de grande porte tendem a usar com o sistema. Os valores típicos são milhares de coleções e aplicativos, que são implantados em centenas de milhares de usuários ou sistemas. Os testes devem ser executados simultaneamente em *todos* os objetos do sistema nesses limites. Muitos clientes aproveitam vários recursos, mas geralmente não usam todos os recursos do produto nesses limites superiores. O teste com todos os recursos do produto ajuda a garantir o melhor desempenho possível de todo o sistema e permite um buffer para os recursos que alguns clientes podem usar acima da média. 

### <a name="loads"></a>Cargas 
Os testes também devem ser executados em cargas de um *dia médio* maiores que o padrão, com a execução de simulações que geram picos de demanda de uso no sistema. Um exemplo é a simulação de distribuições de Patch Tuesday, para garantir que o sistema possa retornar dados de conformidade de atualizações imediatamente durante esses dias de atividade de pico. Outro exemplo é a simulação de uma atividade do site durante um ataque de malware generalizado, a fim de garantir que uma notificação e uma resposta oportunas sejam possíveis. Embora os computadores implantados do tamanho recomendado possam ser subutilizados em qualquer dia especificado, situações mais extremas exigem um buffer de processamento.

### <a name="configurations"></a>Configurações
Execute os testes em uma variedade de tipos de hardware físico, do Hyper-V e do Azure, com uma combinação de sistemas operacionais e versões do SQL Server compatíveis. Sempre valide os piores casos para a configuração compatível. Em geral, o Hyper-V e o Azure retornam resultados de desempenho comparáveis para hardware físico equivalente quando configurados de forma similar. Os sistemas operacionais de servidor mais recentes tendem a ter um desempenho igual ou superior aos sistemas operacionais de servidor compatíveis mais antigos. Embora todas as plataformas compatíveis atendam aos requisitos mínimos, geralmente, as últimas versões de produtos de suporte, como o Windows e o SQL, produzem um desempenho ainda melhor. 

A maior variação é proveniente das versões do SQL Server em uso. Para obter mais informações sobre as versões do SQL Server, confira [Qual versão do SQL deve ser executada?](../../understand/site-size-performance-faq.md#what-version-of-sql-should-i-run). 

## <a name="key-performance-determinants"></a>Principais fatores determinantes de desempenho

Você pode testar e medir o desempenho do Configuration Manager com uma variedade de configurações, de diferentes maneiras e diferentes tamanhos de sites. As configurações e os objetos a seguir podem afetar drasticamente o desempenho. Lembre-se de considerá-los ao testar e modelar o desempenho em seu ambiente.

> [!CAUTION]
> Embora alguns aspectos do Configuration Manager tenham limites máximos oficiais ou de interface do usuário que impeçam o uso excessivo, ultrapassar as diretrizes pode ter efeitos adversos consideráveis no desempenho de um site. Exceder os níveis recomendados ou ignorar as diretrizes de dimensionamento normalmente exige um hardware maior e pode tornar seu ambiente não gerenciável até que você reduza a frequência ou a contagem de vários objetos.

### <a name="hardware-inventory"></a>Inventário de hardware
Para testar o desempenho de linha de base, defina a coleta de inventário de hardware como uma vez por semana, com o tamanho do arquivo *.mof* padrão, mais aproximadamente 20% propriedades adicionais. Não habilite todas as propriedades e colete apenas as propriedades de que você realmente precisa. Preste atenção especial durante a coleta de propriedades, como memória virtual disponível, que *sempre* serão alteradas a *cada* ciclo de inventário. A coleta dessas propriedades pode causar variação excessiva em cada ciclo de inventário de cada cliente.

### <a name="software-inventory"></a>Inventário de software
Para testar o desempenho de linha de base, defina a coleta de inventário de software como uma vez por semana, com os detalhes *somente produto*. A coleta de muitos arquivos pode colocar uma tensão significativa no subsistema de inventário. Evite especificar filtros que possam acabar coletando milhares de arquivos entre muitos clientes, como *\*.exe* ou *\*.dll*.

### <a name="collections"></a>Coleções
O teste de desempenho de linha de base pode incluir vários milhares de coleções com uma variedade de escopo, tamanho, complexidade e configurações de atualização. O desempenho do site não é uma função direta do número absoluto de coleções em um site. O desempenho também é um produto cruzado da complexidade da consulta das coleções, da frequência de alteração e atualizações completas e incrementais, das dependências entre coleções e dos números de clientes nas coleções.

Sempre que possível, minimize as coleções que tenham consultas de regra dinâmica custosas ou complicadas. Para coleções que exigem esses tipos de regras, defina intervalos de atualização apropriados e atualize os horários para minimizar o impacto de reavaliação da coleção no sistema. Por exemplo, faça a atualização à meia-noite, em vez de às 8h.

A habilitação de atualizações incrementais em coleções garante atualizações rápidas e oportunas na associação de coleta. No entanto, mesmo que as atualizações incrementais sejam eficientes, elas ainda colocam uma carga no sistema. Equilibre a frequência de alteração prevista com a necessidade de atualizações quase em tempo real na associação. Por exemplo, digamos que você espere uma variação intensa nos membros da coleção, mas não precise de atualizações de associação quase em tempo real. Atualizar a coleção com uma atualização completa agendada em um intervalo é mais eficiente e produz menos carga no sistema do que habilitar atualizações incrementais. 

Quando você habilitar atualizações incrementais, reduza as atualizações completas agendadas nas mesmas coleções. Elas são apenas um método de backup da avaliação, pois as atualizações incrementais devem manter a associação da coleta atualizada quase em tempo real. [Melhores práticas para coleções](../../clients/manage/collections/best-practices-for-collections.md#do-not-use-incremental-updates-for-a-large-number-of-collections) recomenda um número máximo total de coleções para atualizações incrementais, mas como o artigo indica, sua experiência poderá variar com base em muitos fatores.

As coleções com apenas regras de associação direta e com uma limitação de coleção que não esteja executando atualizações incrementais não precisam de atualizações completas agendadas. Desabilite os agendamentos de atualização para esses tipos de coleções para impedir uma carga desnecessária no sistema. Se a limitação de coleção usar atualizações incrementais, as coleções com apenas regras de associação direta poderão não refletir as atualizações de associação em até 24 horas ou até que ocorra uma atualização agendada.

Embora não seja uma melhor prática, algumas organizações criam centenas ou milhares de coleções como parte de vários processos empresariais. Se você usar a automação para criar coleções, será importante habilitar as atualizações incrementais necessárias corretamente. Minimize e distribua os agendamentos de atualização completa para evitar pontos de acesso de avaliação da coleção durante um único período de tempo. Estabeleça um processo regular de limpeza para excluir coleções não utilizadas, especialmente se você criar automaticamente coleções de que não precisa mais após algum tempo.

Lembre-se de que o Configuration Manager cria políticas para todos os objetos em suas coleções quando você tem tarefas como destino, como implantações nelas. As alterações de associação, por meio de atualização agendada ou atualizações incrementais, podem criar muitos outros tipos de trabalho para todo o sistema. Os últimos builds do branch atual têm otimizações de política especiais para as coleções Todos os Sistemas e Todos os Usuários. Ao ter toda a sua empresa como destino, use as coleções internas, em vez de um clone dessas coleções internas.

Para investigar ainda mais profundamente o desempenho da coleção, você pode usar o CEViewer (Collection Evaluation Viewer) no [Kit de ferramentas do Configuration Manager](https://www.microsoft.com/download/details.aspx?id=50012).

### <a name="discovery-methods"></a>Métodos de descoberta
Para testes de desempenho de linha de base, execute métodos de descoberta baseada em servidor uma vez por semana habilitando a descoberta de deltas, conforme apropriado, para manter os dados atualizados durante a semana. Os testes devem descobrir uma quantidade de objetos proporcional ao porte da empresa simulada. O teste de linha de base de desempenho para a descoberta de pulsação também deve ser executado uma vez por semana.

Os dados de descoberta são dados globais. Um problema comum relacionado ao desempenho é a configuração incorreta dos métodos de descoberta baseada em servidor em uma hierarquia, causando a descoberta duplicada dos mesmos recursos de vários sites primários. Configure cuidadosamente os métodos de descoberta para otimizar a comunicação com o serviço de destino, como controladores de domínio do Active Directory, evitando a duplicação do mesmo escopo de descoberta em vários sites primários.

## <a name="general-sizing-guidelines"></a>Diretrizes gerais de dimensionamento 

Com base na [metodologia de teste de desempenho](#performance-test-methodology) anterior, a tabela a seguir fornece diretrizes gerais de requisitos de hardware *mínimo* para um número específico de clientes gerenciados. Esses valores devem permitir que a maioria dos clientes com o número especificado de clientes processe objetos rápido o suficiente para administrar o site especificado. O preço da capacidade de computação continua diminuindo todos os anos e alguns dos requisitos abaixo são simples em termos de configurações de hardware de servidor moderno. O hardware que excede as diretrizes a seguir aumenta proporcionalmente o desempenho de sites que exigem capacidade de processamento adicional ou que têm padrões de uso especial de produto. 

| Clientes de desktop  | Tipo/função do site  | Núcleos<sup>1</sup>   | Memória (GB)   | Alocação de memória do SQL  | IOPS:  Caixas de entrada<sup>2</sup>  | IOPS: SQL<sup>2</sup>   | Espaço de armazenamento necessário (GB)<sup>3</sup>   |
|------|-------------------------------------------------------------|-----|-----|-----|------|------|------|
| 25 mil  | Primário ou CAS com função de site do banco de dados no mesmo servidor   | 6   | 24  | 65% | 600  | 1.700 | 350  |
| 25 mil  | Primário ou CAS                                              | 4   | 8   |     | 600  |      | 100  |
|      | SQL remoto                                                  | 4   | 16  | 70% |      | 1.700 | 250  |
|      |                                                             |     |     |     |      |      |      |
| 50 mil  | Primário ou CAS com função de site do banco de dados no mesmo servidor   | 8   | 32  | 70% | 1.200 | 2.800 | 600  |
| 50 mil  | Primário ou CAS                                              | 4   | 8   |     | 1.200 |      | 200  |
|      | SQL remoto                                                  | 8   | 24  | 70% |      | 2.800 | 400  |
|      |                                                             |     |     |     |      |      |      |
| 100 mil | Primário ou CAS com função de site do banco de dados no mesmo servidor   | 12  | 64  | 70% | 1.200 | 5000 | 1.100 |
| 100 mil | Primário ou CAS                                              | 6   | 12  |     | 1.200 |      | 300  |
|      | SQL remoto                                                  | 12  | 48  | 80% |      | 5000 | 800  |
|      |                                                             |     |     |     |      |      |      |
| 150 mil | Primário ou CAS com função de site do banco de dados no mesmo servidor   | 16  | 96  | 70% | 1.800 | 7.400 | 1.600 |
| 150 mil | Primário ou CAS                                   | 8   | 16   |     | 1.800  |         | 400   |
|      | SQL remoto                                       | 16  | 72   | 90% |       | 7.400    | 1.200  |
|      |                                                             |     |     |     |      |      |      |
| 700 mil | CAS com função de site do banco de dados no mesmo servidor   | Mais de 20 | Mais de 128 | 80% | Mais de 1.800 | Mais de 9.000   | Mais de 5.000 |
| 700 mil | CAS                                              | Mais de 8  | Mais de 16  |     | Mais de 1.800 |         | Mais de 500  |
|      | SQL remoto                                       | Mais de 16 | Mais de 96  | 90% |       | Mais de 9.000   | Mais de 4.500 |
|      |                                                             |     |     |     |      |      |      |
| 5 mil   | Site secundário                                   | 4   | 8    |     | 500   | -       | 200   |
| 15 mil  | Site secundário                                   | 8   | 16   |     | 500   | -       | 300   |

**Observações**

1. **Núcleos**: O Configuration Manager executa muitos processos simultâneos, portanto, precisa de determinado número mínimo de núcleos de CPU para diversos tamanhos de site. Embora os núcleos fiquem mais rápidos de cada ano, é importante garantir que determinado número mínimo de núcleos funcione em paralelo. Em geral, qualquer CPU no nível de servidor produzido após 2015 atende às necessidades de desempenho básico dos núcleos especificados na tabela. O Configuration Manager aproveita os núcleos adicionais além das recomendações, mas em geral, quando você tiver o mínimo de núcleos sugeridos, deverá priorizar o investimento em recursos de CPU para aumentar a velocidade dos núcleos existentes, não adicionar outros núcleos mais lentos. Por exemplo, o Configuration Manager terá um melhor desempenho em tarefas de processamento básicas com 16 núcleos rápidos do que com 24 núcleos mais lentos, supondo que outros recursos do sistema suficientes, como IOPS de disco, estejam disponíveis.
   
   A relação entre os núcleos e a memória também é importante. Em geral, ter menos de 3 a 4 GB de RAM por núcleo reduz a capacidade de processamento total nos servidores SQL. Você precisa de mais RAM por núcleo quando o SQL é colocado com os componentes do servidor do site.
   
   > [!NOTE]
   > Todo o teste define o plano de energia do computador para permitir o máximo desempenho e consumo de energia da CPU.
   
2. **IOPS: Caixas de entrada e IOPS: SQL** se refere às necessidades de IOPS para as unidades lógicas do Configuration Manager e do SQL. A coluna **IOPS: Caixas de entrada** mostra os requisitos de IOPS para a unidade lógica na qual residem os diretórios de caixa de entrada do Configuration Manager. A coluna **IOPS: SQL** mostra as necessidades totais de IOPS para as unidades lógicas usadas por vários arquivos SQL. Essas colunas são diferentes porque as duas unidades devem ter uma formatação diferente. Para obter mais informações e exemplos sobre as melhores práticas de arquivo e configurações de disco SQL sugeridas, incluindo detalhes sobre como dividir arquivos entre vários volumes, confira as [Perguntas frequentes sobre desempenho e dimensionamento do site](../../understand/site-size-performance-faq.md).
   
   Essas duas colunas da IOPS usam dados da ferramenta padrão do setor, *Diskspd*. Confira [Como medir o desempenho do disco](#how-to-measure-disk-performance) para obter instruções sobre como duplicar essas medidas. Em geral, depois que você atende aos requisitos básicos de memória e de CPU, o subsistema de armazenamento tem o maior impacto no desempenho do site, e melhorias aqui gerarão o maior retorno sobre o investimento.
   
3.  **Espaço de armazenamento necessário:** Esses valores do mundo real podem ser distintos de outras recomendações documentadas. Fornecemos esses números apenas como diretrizes gerais; os requisitos individuais podem variar amplamente. Planeje cuidadosamente as necessidades de espaço em disco antes da instalação do site. Suponha que uma quantidade desse armazenamento permaneça como espaço livre em disco na maioria das vezes. Você pode usar esse espaço do buffer em um cenário de recuperação ou para cenários de atualização que precisam de espaço livre em disco para expansão do pacote de instalação. Seu site pode exigir armazenamento adicional para grandes quantidades de coleta de dados, períodos mais longos de retenção de dados e grandes quantidades de conteúdo de distribuição de software. Você também pode armazenar esses itens em volumes separados e de taxa de transferência mais baixa.

## <a name="how-to-measure-disk-performance"></a>Como medir o desempenho do disco 

Use a ferramenta padrão do setor *Diskspd* para fornecer sugestões padronizadas para a IOPS exigida por ambientes de vários tamanhos do Configuration Manager. Embora não sejam completas, as etapas do teste e as linhas de comando a seguir fornecem uma maneira simples e reproduzível de estimar a taxa de transferência do subsistema de disco de seus servidores. Compare os resultados com a IOPS mínima recomendada na tabela [Diretrizes gerais de dimensionamento](#general-sizing-guidelines). 

Confira [Configurações de disco de exemplo](#example-disk-configurations) para obter resultados de teste de uma variedade de configurações de hardware em ambientes de laboratório. É possível usar os dados para um ponto de partida aproximado ao projetar o subsistema de armazenamento para um novo ambiente do zero.

### <a name="to-test-disk-iops"></a>Para testar a IOPS de disco  
1. Baixe o utilitário *Diskspd* aqui: [https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62](https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62).
   
1. Verifique se você tem, pelo menos, 100 GB de espaço livre em disco. Desabilite todos os aplicativos que possam interferir ou causar carga extra no disco, como o exame ativo de antivírus do diretório, o SQL ou o SMSExec.
   
1. Execute *Diskspd* em um prompt de comandos com privilégios elevados. 
   
   Execute duas execuções da ferramenta na sequência para o volume que deseja testar. O primeiro teste executa operações de gravação aleatória com um tamanho de 64 mil por um minuto. Esse teste garante o carregamento do cache do controlador e a alocação do espaço em disco, caso o volume esteja se expandindo dinamicamente. Descarte os resultados do primeiro teste. O segundo teste deve ser realizado *imediatamente* após o primeiro teste e executar a mesma carga por cinco minutos.
   
   Por exemplo, use as linhas de comando específicas a seguir para testar o volume G:\\.
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d60 -h -L G:\\test\testfile.dat` 
   
   `del G:\\test\testfile.dat`
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d300 -h -L G:\\test\testfile.dat`
   
1. Examine a saída do segundo teste para localizar a IOPS total na coluna **E/S por segundo**. No exemplo a seguir, a IOPS total é de **3.929,18**.
   
   ```
   Total IO
   | thread |  bytes      |  I/Os   |  MB/s  | I/O per s | AvgLat | LatStdDev |
   |--------|-------------|---------|--------|-----------|--------|-----------| 
   |   1    |  9651814400 |  147275 |  30.68 |    490.92 | 16.294 | 10.210    | 
   |   2    |  9676652544 |  147654 |  30.76 |    492.18 | 16.252 |  9.998    |
   |   3    |  9638248448 |  147068 |  30.64 |    490.23 | 16.317 | 10.295    |
   |   4    |  9686089728 |  147798 |  30.79 |    492.66 | 16.236 | 10.072    | 
   |   5    |  9590931456 |  146346 |  30.49 |    487.82 | 16.398 | 10.384    | 
   |   6    |  9677242368 |  147663 |  30.76 |    492.21 | 16.251 | 10.067    |
   |   7    |  9637330944 |  147054 |  30.64 |    490.18 | 16.319 | 10.249    | 
   |   8    |  9692577792 |  147897 |  30.81 |    492.99 | 16.225 | 10.125    | 
   | Total: | 77250887680 | 1178755 | 245.57 |   3929.18 | 16.286 | 10.176    |
   ```

## <a name="example-disk-configurations"></a>Configurações de disco de exemplo

As tabelas a seguir mostram os resultados da execução das etapas do teste em [Como medir o desempenho do disco](#how-to-measure-disk-performance) com várias configurações de laboratório de teste. Use os dados para um ponto de partida *aproximado* ao projetar o subsistema de armazenamento para um novo ambiente do zero. 

### <a name="physical-machines-and-hyper-v"></a>Computadores físicos e o Hyper-V 
O hardware está sempre sendo aprimorado. Espere que as gerações mais novas de hardware e diferentes combinações de hardware, como SSDs e SANs, excedam o desempenho indicado abaixo. Esses resultados são um ponto de partida básico a ser considerado ao criar um servidor ou conversar com o fornecedor de hardware.

A tabela a seguir mostra os resultados de teste em vários subsistemas de disco, incluindo o eixo e as unidades de disco rígido baseado em SSD, em várias configurações de laboratório de teste. Todas as configurações formatam os discos com clusters de 64k e os anexam a um controlador de disco de nível empresarial. Além da contagem de discos da matriz RAID, cada um deles tem, pelo menos, um disco sobressalente.

| Tipo de disco   | Contagem de discos, não incluindo mais um disco sobressalente | RAID     | IOPS medida  |
|------------------|----------------------------------------------------|---------------|---------------|
| 15k SAS          | 2                                                  |           1   | 620           |
| 15k SAS          | 4                                                  |           10  | 1.206          |
| 15k SAS          | 6                                                  |           10  | 1.751          |
| 15k SAS          | 8                                                  |           10  | 2.322          |
| 15k SAS          | 10                                                 |           10  | 2.882          |
| 15k SAS          | 12                                                 |           10  | 3.476          |
| 15k SAS          | 16                                                 |           10  | 4.236          |
| 15k SAS          | 20                                                 |           10  | 5.148          |
| 15k SAS          | 30                                                 |           10  | 7.398          |
| 15k SAS          | 40                                                 |           10  | 9.913          |
| SSD SATA         | 2                                                  |           1   | 3.300          |
| SSD SATA         | 4                                                  |           10  | 5.542          |
| SSD SATA         | 6                                                  |           10  | 7201          |
| SSD SAS          | 2                                                  |           1   | 7.539          |
| SSD SAS          | 4                                                  |           10  | 14346         |
| SSD SAS          | 6                                                  |           10  | 15.607         |

Estes são os dispositivos usados pelo exemplo. Essas informações não são uma recomendação de qualquer fabricante ou modelo de hardware específico. 

| Tipo de disco    | Modelo      | Controlador RAID | Memória cache e configuração |
|-------------------|-----------------|----------------------|-------------------------------------|
| HD SAS de 15k RPM    | HP EH0300JDYTH  | Smart Array P822     | 2 GB, 20% de leitura/80% de gravação           |
| SSD SATA          | ATA MK0200GCTYV | Smart Array P420i    | 1 GB, 20% de leitura/80% de gravação           |
| SSD SAS           | HP MO0800 JEFPB | Smart Array P420i    | 1 GB, 20% de leitura/80% de gravação           |

### <a name="azure-machine-and-disk-performance"></a>Desempenho do disco e do computador do Azure 
O desempenho do disco do Azure depende de vários fatores, como o tamanho da VM do Azure e o número e o tipo de discos usados. O Azure também está constantemente adicionando novos tipos de computadores e velocidades de disco que são diferentes do mostrado no gráfico a seguir. Para obter mais informações sobre o Configuration Manager em execução no Azure e noções básicas da E/S de disco no Azure, confira [Perguntas frequentes sobre o Configuration Manager no Azure](../../understand/configuration-manager-on-azure.md).

Todos os discos são formatados como NTFS com um tamanho de cluster de 64k, e as linhas com mais de um disco são configuradas como volumes distribuídos por meio do utilitário de Gerenciamento de Disco do Windows.

| VM do Azure| Disco do Azure| Contagem de discos | Espaço disponível | IOPS medida   | Fator limitante   |
|--------------------------------------------|-------------------------|---------------------|---------------------------|-------|-----------------|
| **DS2/DS11**                              | P20                     | 1                   | 512 MB                    | 965   | Tamanho da VM do Azure   |
| **DS2/DS11**                              | P20                     | 2                   | 1.024 MB                   | 996   | Tamanho da VM do Azure   |
| **DS2/DS11**                              | P30                     | 1                   | 1.024 MB                   | 996   | Tamanho da VM do Azure   |
| **DS2/DS11**                              | P30                     | 2                   | 2.048 MB                   | 996   | Tamanho da VM do Azure   |
| **DS3/DS12/F4S**                          | P20                     | 1                   | 512 MB                    | 1.994  | Tamanho da VM do Azure   |
| **DS3/DS12/F4S**                          | P20                     | 2                   | 1.024 MB                   | 1.992  | Tamanho da VM do Azure   |
| **DS3/DS12/F4S**                          | P30                     | 1                   | 1.024 MB                   | 1.993  | Tamanho da VM do Azure   |
| **DS3/DS12/F4S**                          | P30                     | 2                   | 2.048 MB                   | 1.992  | Tamanho da VM do Azure   |
| **DS4/DS13/F8S**                          | P20                     | 1                   | 512 MB                    | 2.334  | Disco P20        |
| **DS4/DS13/F8S**                          | P20                     | 2                   | 1.024 MB                   | 3.984  | Tamanho da VM do Azure   |
| **DS4/DS13/F8S**                          | P20                     | 3                   | 1.536 MB                   | 3.984  | Tamanho da VM do Azure   |
| **DS4/DS13/F8S**                          | P30                     | 1                   | 1.024 MB                   | 3.112  | Disco P30        |
| **DS4/DS13/F8S**                          | P30                     | 2                   | 2.048 MB                   | 3.984  | Tamanho da VM do Azure   |
| **DS4/DS13/F8S**                          | P30                     | 3                   | 3.072 MB                   | 3.996  | Tamanho da VM do Azure   |
| **DS5/DS14/F16S**                         | P20                     | 1                   | 512 MB                    | 2.335  | Disco P20        |
| **DS5/DS14/F16S**                         | P20                     | 2                   | 1.024 MB                   | 4.639  | Disco P20        |
| **DS5/DS14/F16S**                         | P20                     | 3                   | 1.536 MB                   | 6.913  | Disco P20        |
| **DS5/DS14/F16S**                         | P20                     | 4                   | 2.048 MB                   | 7.966  | Tamanho da VM do Azure   |
| **DS5/DS14/F16S**                         | P30                     | 1                   | 1.024 MB                   | 3.112  | Disco P30        |
| **DS5/DS14/F16S**                         | P30                     | 2                   | 2.048 MB                   | 6.182  | Disco P30        |
| **DS5/DS14/F16S**                         | P30                     | 3                   | 3.072 MB                   | 7.963  | Tamanho da VM do Azure   |
| **DS5/DS14/F16S**                         | P30                     | 4                   | 4.096 MB                   | 7.968  | Tamanho da VM do Azure   |
| **DS15**                                  | P30                     | 1                   | 1.024 MB                   | 3.113  | Disco P30        |
| **DS15**                                  | P30                     | 2                   | 2.048 MB                   | 6.184  | Disco P30        |
| **DS15**                                  | P30                     | 3                   | 3.072 MB                   | 9225  | Disco P30        |
| **DS15**                                  | P30                     | 4                   | 4.096 MB                   | 10.200 | Tamanho da VM do Azure   |

## <a name="see-also"></a>Consulte também

- [Perguntas frequentes sobre o desempenho e o dimensionamento do site](../../understand/site-size-performance-faq.md)
- [Perguntas frequentes sobre o Configuration Manager no Azure](../../understand/configuration-manager-on-azure.md)
- [Números de tamanho e escala](size-and-scale-numbers.md)
- [Hardware recomendado](recommended-hardware.md)

