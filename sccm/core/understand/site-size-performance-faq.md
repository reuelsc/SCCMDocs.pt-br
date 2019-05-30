---
title: Perguntas frequentes sobre o desempenho e o tamanho do site
titleSuffix: Configuration Manager
description: Respostas para perguntas comuns sobre o System Center Configuration Manager referentes ao desempenho e ao dimensionamento do site.
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 8157ee2212e18d4938beabd40f16e66a319d0b8c
ms.sourcegitcommit: cab3dba5ebfe90f28cedee03c1840c9a395160cc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/17/2019
ms.locfileid: "65849290"
---
# <a name="system-center-configuration-manager-site-sizing-and-performance-faq"></a>Perguntas frequentes sobre o desempenho e o dimensionamento do site do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este documento aborda perguntas frequentes sobre problemas de desempenho comuns e diretrizes de dimensionamento do site do Configuration Manager.

## <a name="machine-and-disk-configuration-faqs-and-examples"></a>Perguntas frequentes sobre a configuração do computador e do disco e exemplos

### <a name="how-should-i-format-the-disks-on-my-site-server-and-sql-server"></a>Como devo formatar os discos em meu servidor do site e no SQL Server?

Separe os arquivos SQL e as caixas de entrada do Configuration Manager em, pelo menos, dois volumes diferentes. Essa separação permite otimizar os tamanhos de alocação de cluster para os diferentes tipos de E/S executados. 

Para o volume que hospeda as caixas de entrada do servidor do site, use o NTFS com unidades de alocação de 4K ou 8K. O ReFS grava em 64k mesmo para arquivos pequenos. O Configuration Manager tem muitos arquivos pequenos, portanto, o ReFS pode produzir uma sobrecarga de disco desnecessária.

Para discos que contêm arquivos de banco de dados SQL, use a formatação NTFS ou ReFS, com unidades de alocação de 64K.

### <a name="how-and-where-should-i-lay-out-my-sql-database-files"></a>Como e em que local devo organizar meus arquivos de banco de dados SQL?

As matrizes modernas dos SSDs (unidades de estado sólido) e o Armazenamento Premium do Azure podem fornecer uma IOPS alta em um único volume, com alguns discos. Geralmente, você adiciona mais unidades a uma matriz para armazenamento adicional, não uma taxa de transferência adicional. Se você estiver usando discos físicos baseados em eixo, talvez precise de mais IOPS do que poderá gerar em um único volume. Você deve alocar 60% da total recomendado de IOPS e espaço em disco para o arquivo *.mdf*, 20% para o arquivo *.ldf* e 20% para os arquivos temporários de log e de dados. Todos os arquivos *.ldf* e temporários podem residir em um único volume com 40% (20% + 20%) da IOPS alocada.

Por padrão, o SQL cria um arquivo de dados temporário. Você deve criar mais, para evitar bloqueios de SQL e evitar aguardar o acesso a um único arquivo. As opiniões da comunidade variam sobre o melhor número de arquivos de dados temporários a serem criados, de quatro a oito. Os testes revelam pouca diferença entre quatro a oito, portanto, você pode criar quatro arquivos de dados temporários *do mesmo tamanho*. Os arquivos de dados de tempdb devem ter até 20 a 25% do tamanho do banco de dados completo.

### <a name="are-there-any-other-recommendations-for-disk-setup"></a>Há outras recomendações para a configuração do disco?

Quando configurável, defina a memória do controlador RAID com uma alocação de 70% para operações de gravação e 30% para operações de leitura. Em geral, use uma configuração de matriz RAID 10 para o banco de dados do site. O RAID 1 também será aceitável para sites em pequena escala com baixos requisitos de E/S ou se você usar SSDs rápidos. Com matrizes de disco maiores, configure discos sobressalentes para substituir automaticamente os discos com falha.

**Exemplo: Computador físico com discos físicos** 

As [diretrizes de dimensionamento](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) para um servidor do site colocado e um SQL Server com **100.000** clientes são 1.200 IOPS para caixas de entrada do servidor do site e 5.000 IOPS para arquivos do SQL Server.

A configuração de disco resultante poderá ser semelhante a:

| Unidades<sup>1</sup> | RAID | Formato | Conteúdo do volume | IOPS mínima necessária| Número aprox. de IOPS fornecida<sup>2</sup>  |
|----------------|-----------|-------------|----------------------|---------------------|------------------|
| 2x10k          | 1         | -           | Windows              |                     | -                |
| 6x15k          | 10        | NTFS 8k     | Caixas de entrada do ConfigMgr    |     1.700            | 1.751             |
| 12x15k         | 10        | 64k ReFS    | .mdf do SQL             | 60%*5.000 = 3.000     | 3.476             |
| 8x15k          | 10        | 64k ReFS    | Arquivos temporários .ldf SQL | 40%*5.000 = 2.000     | 2.322             |

1. Não inclui os discos sobressalentes recomendados. 
2. Esse valor foi obtido de [Configurações de disco de exemplo](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). 

### <a name="i-use-hyper-v-on-windows-server-how-should-i-configure-the-disks-for-my-configuration-manager-vms-for-best-performance"></a>Eu uso o Hyper-V no Windows Server. Como devo configurar os discos para minhas VMs do Configuration Manager para obter melhor desempenho?

O Hyper-V proporciona um desempenho semelhante a um servidor físico, caso os recursos de hardware (núcleos de CPU e armazenamento de passagem) sejam 100% dedicados à VM (máquina virtual). O uso de arquivos de disco *.vhd* ou *.vhdx* de tamanho fixo causa um impacto mínimo no desempenho de E/S de 1 a 5%. O uso da expansão dinâmica de arquivos de disco *.vhd* ou *.vhdx* causa um impacto de desempenho de E/S de até 25% na carga de trabalho do Configuration Manager. Caso você precise de discos de expansão dinâmica, compense isso pela adição de um desempenho de IOPS de 25% adicional na matriz.

Ao executar o servidor do site do Configuration Manager ou o SQL em uma VM, isole as unidades de sistema operacional do host do Hyper-V das unidades de dados e de sistema operacional da VM.

Para obter mais informações sobre como otimizar VMs, confira [Como ajustar o desempenho de Hyper-V Servers](/windows-server/administration/performance-tuning/role/hyper-v-server/).

**Exemplo: Servidor do site baseado em uma VM do Hyper-V** 

As [diretrizes de dimensionamento](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) para um servidor do site colocado e um SQL Server com **150.000** clientes são 1.800 IOPS para caixas de entrada do servidor do site e 7.400 IOPS para arquivos do SQL Server.

A configuração de disco resultante poderá ser semelhante a:

| Unidades<sup>1</sup> | RAID | Formato<sup>2</sup> | Conteúdo do volume | IOPS mínima necessária| Número aprox. de IOPS fornecida<sup>3</sup>  |
|----------------|-----------|----------------|---------------------------|----------------------|------------------|
| 2x10k          | 1         | -              | Sistema operacional do host do Hyper-V           | -                    | -                |
| 2x10k          | 1         | -              | Sistema operacional do servidor do site (VM)       | -                    | -                |
| 2xSSD SAS      | 1         | NTFS 8k        | Caixas de entrada do ConfigMgr (VM)    | 1.800                 | 7.539             |
| 4xSSD SAS      | 10        | 64k ReFS       | SQL do host (VM) (todos os arquivos) | 7.400                 | 14346            |

1. Não inclui os discos sobressalentes recomendados. 
2. *.vhdx* de tamanho fixo e de passagem para a unidade de VM dedicada ao volume subjacente. 
3. Esse valor foi obtido de [Configurações de disco de exemplo](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). 

### <a name="are-there-any-suggestions-for-configuration-manager-environments-in-microsoft-azure"></a>Há sugestões para ambientes do Configuration Manager no Microsoft Azure?

Comece lendo as [Perguntas frequentes sobre o Configuration Manager no Azure](configuration-manager-on-azure.md).

As VMs IaaS (infraestrutura como serviço) do Azure que aproveitam discos baseados no Armazenamento Premium podem ter uma IOPS alta. Nessas VMs, configure discos adicionais para as necessidades previstas de espaço em disco, em vez de IOPS adicional.

O Armazenamento do Azure é inerentemente redundante e não exige vários discos para disponibilidade. Você pode distribuir discos no Gerenciador de Disco ou nos Espaços de Armazenamento para fornecer espaço e desempenho adicionais.

Para obter mais informações e recomendações sobre como maximizar o desempenho do Armazenamento Premium e executar servidores SQL em VMs IaaS do Azure, confira:

- [Otimizar o desempenho do aplicativo](/azure/storage/storage-premium-storage-performance#optimize-application-performance)
 
- [Diretrizes de discos](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)

**Exemplo: Servidor do site baseado no Azure** 

As [diretrizes de dimensionamento](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) para um servidor do site colocado e um SQL Server com **50.000** clientes são oito núcleos, 32 GB e 1.200 IOPS para caixas de entrada do servidor do site e 2.800 IOPS para arquivos do SQL Server.

O computador do Azure resultante pode ser um DS13v2 (oito núcleos, 56 GB) com a seguinte configuração de disco:

| Unidades | Formato | Contém | IOPS mínima necessária| Número aprox. de IOPS fornecida<sup>1</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;padrão&gt; | -             | Sistema operacional do servidor do site     | -                    | -                |
| 1xP20 (512 GB)    | NTFS 8k       | Caixas de entrada do ConfigMgr  | 1.200                 | 2.334             |
| 1xP30 (1.024 GB)   | 64k ReFS      | SQL (todos os arquivos<sup>2</sup>) | 2.800                 | 3.112             |

1. Esse valor foi obtido de [Configurações de disco de exemplo](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations).
2. As [diretrizes do Azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) permitem a colocação do tempdb na unidade *D:* local baseada em SSD, considerando que ela não excederá o espaço disponível e permitirá a distribuição adicional de E/S de disco.

**Exemplo: Servidor do site baseado no Azure (para aumento instantâneo de desempenho)** 

A taxa de transferência de disco do Azure é limitada pelo tamanho da VM. A configuração no exemplo anterior do Azure pode limitar a expansão futura ou o desempenho adicional. Se você adicionar mais discos durante a implantação inicial da VM do Azure, poderá fazer o upsizing da VM do Azure para uma maior capacidade de processamento no futuro, com investimento inicial mínimo. É muito mais simples planejar com antecedência o aumento do desempenho do site conforme os requisitos são alterados, em vez de precisar fazer uma migração mais complicada posteriormente.

Altere os discos no exemplo anterior do Azure para ver como a IOPS é alterada.

**DS13v2** 

| Unidades<sup>1</sup> | Formato | Contém | IOPS mínima necessária| Número aprox. de IOPS fornecida<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;padrão&gt; | -             | Sistema operacional do servidor do site     | -                    | -                |
| 2xP20 (1.024 GB)   | NTFS 8k       | Caixas de entrada do ConfigMgr  | 1.200                 | 3.984             |
| 2xP30 (2.048 GB)   | 64k ReFS      | SQL (todos os arquivos<sup>3</sup>) | 2.800                 | 3.984             |

1. Os discos são distribuídos usando os Espaços de Armazenamento.
2. Esse valor foi obtido de [Configurações de disco de exemplo](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). O tamanho da VM limita o desempenho.
3. As [diretrizes do Azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) permitem a colocação do tempdb na unidade *D:* local baseada em SSD, considerando que ela não excederá o espaço disponível e permitirá a distribuição adicional de E/S de disco.

Caso você precise de mais desempenho no futuro, poderá fazer o upsizing da VM para um DS14v2, o que duplicará a CPU e a memória. A largura de banda de disco adicional permitida pelo tamanho da VM também aumentará instantaneamente a IOPS de disco disponível nos discos configurados anteriormente.

**DS14v2**

| Unidades<sup>1</sup> | RAID | Formato | Contém | IOPS mínima necessária| Número aprox. de IOPS fornecida<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;padrão&gt; | -             | Sistema operacional do servidor do site     | -                    | -                |
| 2xP20 (1.024 GB)   | NTFS 8k       | Caixas de entrada do ConfigMgr  | 1.200                 | 4.639             |
| 2xP30 (2.048 GB)   | 64k ReFS      | SQL (todos os arquivos<sup>3</sup>) | 2.800                 | 6.182             |

1. Os discos são distribuídos usando os Espaços de Armazenamento.
2. Esse valor foi obtido de [Configurações de disco de exemplo](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). O tamanho da VM limita o desempenho.
3. As [diretrizes do Azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) permitem a colocação do tempdb na unidade *D:* local baseada em SSD, considerando que ela não excederá o espaço disponível e permitirá a distribuição adicional de E/S de disco.

## <a name="other-common-sql-server-related-performance-questions"></a>Outras perguntas comuns sobre desempenho relacionadas ao SQL Server 

### <a name="is-it-better-to-run-with-sql-colocated-with-the-site-server-or-run-it-on-a-remote-server"></a>É melhor fazer a execução com o SQL colocado junto com o servidor do site ou executá-lo em um servidor remoto?

Ambos podem ter um bom desempenho, supondo que o único servidor seja dimensionado adequadamente ou a conectividade de rede seja suficiente entre os dois servidores.

O SQL remoto exige o custo inicial e operacional de um servidor adicional, mas é comum entre a maioria dos clientes de grande escala. Os benefícios dessa configuração incluem:

- Mais opções de disponibilidade do site, como Always On do SQL
- Capacidade de executar relatórios pesados com menos sobrecarga no processamento do site
- Recuperação de desastre mais simples em algumas situações
- Gerenciamento de segurança mais fácil
- Separação de funções para o gerenciamento do SQL, como com uma equipe de DBA separada

O SQL colocado exige um único servidor e é comum para a maioria dos clientes de pequena escala. Os benefícios dessa configuração incluem:

- Redução dos custos de computadores, licenças e manutenção
- Menos pontos de falha no site
- Melhor controle do planejamento de tempo de inatividade

### <a name="how-much-ram-should-i-allocate-for-sql"></a>Qual é a quantidade de RAM que devo alocar para o SQL?

Por padrão, o SQL usa toda a memória disponível no servidor, potencialmente privando o sistema operacional e outros processos no computador. Para evitar possíveis problemas de desempenho, é importante alocar memória para o SQL explicitamente. Em servidores do site colocados com servidores SQL, verifique se o sistema operacional tem RAM suficiente para o cache de arquivo e outras operações. Garanta que haja RAM suficiente restante para o SMSExec e outros processos do Configuration Manager. Durante a execução do SQL em um servidor remoto, você pode alocar a *maior parte* da memória para o SQL, mas não toda. Examine as diretrizes iniciais nas [diretrizes de dimensionamento](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines). 

A alocação de memória do SQL Server deve ser arredondada para GB inteiro. Além disso, à medida que RAM aumenta para grandes quantidades, você pode deixar o SQL ter um percentual mais alto. Por exemplo, quando 256 GB ou mais de RAM estiverem disponíveis, você poderá configurar o SQL para até 95%, pois isso ainda preserva muita memória para o sistema operacional. O monitoramento do arquivo de paginação é uma boa maneira de garantir que haja memória suficiente para o sistema operacional e todos os processos do Configuration Manager.

### <a name="cores-are-cheap-these-days-should-i-just-add-a-bunch-of-them-to-my-sql-server"></a>Os núcleos são baratos hoje em dia. Devo apenas adicionar vários deles ao SQL Server?

Você poderá enfrentar problemas de contenção de memória se houver mais de 16 núcleos físicos e RAM insuficiente no SQL Server. A carga de trabalho do Configuration Manager tem um melhor desempenho quando, pelo menos, 3 a 4 GB de RAM por núcleo estão disponíveis para o SQL. Ao adicionar núcleos aos servidores SQL, lembre-se de aumentar a RAM em quantidades proporcionais.

### <a name="will-sql-always-on-impact-my-performance"></a>O Always On do SQL afetará o desempenho?

Em geral, o Always On do SQL tem mínimo impacto no desempenho do sistema quando há rede suficiente disponível entre os servidores de réplica do SQL. Você pode ter um aumento repentino do arquivo *.ldf* do log de banco de dados em um ambiente ocupado do Always On do SQL. No entanto, o espaço do arquivo de log é liberado automaticamente após um backup de banco de dados bem-sucedido. Adicione um trabalho do SQL ao banco de dados do Configuration Manager para executar um backup, por exemplo, a cada 24 horas, e um backup de *.ldf* a cada seis horas. Para obter mais informações sobre o Always On do SQL e o Configuration Manager, incluindo mais sobre as estratégias de backup do SQL, confira [Always On do SQL Server para um banco de dados do site altamente disponível](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

### <a name="should-i-enable-sql-compression-on-my-database"></a>Devo habilitar a compactação do SQL em meu banco de dados?

A compactação do SQL não é recomendada para o banco de dados do Configuration Manager. Embora não haja nenhum problema funcional com a habilitação da compactação em um banco de dados do Configuration Manager, os resultados de teste não mostram uma economia significativa de tamanho comparado ao impacto potencial no desempenho dimensionável do sistema.

### <a name="should-i-enable-sql-encryption-on-my-database"></a>Devo habilitar a criptografia do SQL em meu banco de dados?

Os segredos do banco de dados do Configuration Manager já são armazenados com segurança, mas a adição da criptografia do SQL pode adicionar outra camada de segurança. Não há nenhum problema funcional com a habilitação da criptografia no banco de dados, mas poderá haver uma degradação do desempenho de até 25%, dependendo das tabelas que você optar por criptografar e da versão do SQL utilizada. Portanto, faça a criptografia com cuidado, especialmente em ambientes de grande escala. Além disso, lembre-se de atualizar seus planos de backup e recuperação para garantir que possa recuperar com êxito os dados criptografados.

### <a name="what-version-of-sql-should-i-run"></a>Qual versão do SQL devo executar?

Para obter as versões do SQL compatíveis, confira [Suporte para versões do SQL Server](../plan-design/configs/support-for-sql-server-versions.md). Do ponto de vista do desempenho, todas as versões do SQL compatíveis atendem aos critérios de desempenho necessários. No entanto, o SQL 2012 e o SQL 2016 ou mais recente tendem a superar o desempenho do SQL 2014 em alguns aspectos da carga de trabalho do Configuration Manager. Além disso, a execução do SQL 2014 no nível de compatibilidade do SQL 2012 (110) melhora o desempenho em geral. No momento da instalação, os bancos de dados do Configuration Manager em execução no SQL 2012 e no SQL 2014 são definidos para o nível de compatibilidade 110. O SQL 2016 ou mais recente é definido com o nível de compatibilidade padrão dessa versão do SQL, como 130 para o SQL 2016. A atualização in-loco do SQL não atualizará os níveis de compatibilidade enquanto você não instalar a próxima versão principal do branch atual do Configuration Manager. 

Se você observar tempos limite incomuns ou lentidão em determinadas consultas SQL no SQL 2016 ou posterior, como ao usar o RBAC no Console do Administrador, tente alterar o nível de compatibilidade do SQL no banco de dados do Configuration Manager para 110. Há suporte completo para a execução do nível de compatibilidade do SQL 110 no SQL 2014 e em versões mais recentes do SQL. Para obter mais informações, confira [A consulta SQL atinge o tempo limite ou o desempenho do console fica lento em algumas consultas de banco de dados do Configuration Manager](https://support.microsoft.com/help/3196320/sql-query-times-out-or-console-slow-on-certain-configuration-manager-d).

A partir de janeiro de 2018, você deverá *evitar* as seguintes versões do SQL devido a diversos problemas relacionados ao desempenho ou outros possíveis problemas conhecidos:

- SQL 2012 SP3 CU1 a CU5
- SQL 2014 SP1 CU6 a SP2 CU2
- SQL 2016 RTM a CU3, SP1 CU3 a CU5

### <a name="should-i-implement-any-additional-sql-indexing-tasks"></a>Devo implementar alguma tarefa adicional de indexação do SQL?

Sim, atualize os índices com uma frequência de uma vez por semana e as estatísticas com uma frequência de uma vez por dia para melhorar o desempenho do SQL. Os scripts de terceiros e as informações adicionais disponíveis nas comunidades do Configuration Manager e do SQL podem ajudar a otimizar essas tarefas.

Em sites grandes, algumas tabelas SQL, como CI\_CurrentComplianceStatusDetails e HinvChangeLog, podem ser grandes, dependendo dos padrões de uso. Talvez você precise reduzir ou alterar sua abordagem de manutenção para elas individualmente.

### <a name="when-should-i-use-full-sql-server-instead-of-sql-express-on-my-secondary-sites"></a>Quando devo usar o SQL Server completo em vez do SQL Express em meus sites secundários?

O SQL Express não tem nenhuma implicação de desempenho significativa nos sites secundários e é adequado para a maioria dos clientes. Ele também é fácil de ser implantado e gerenciado, e é a configuração recomendada para quase todos os clientes de qualquer porte.

Há uma situação em que uma instalação do SQL Server completo pode ser necessária. Se você tiver um grande número de pontos de distribuição e pacotes ou fontes em seu ambiente, será possível exceder o limite de tamanho de 10 GB do SQL Express. Se o número de pacotes multiplicado pelo número de pontos de distribuição for superior a 4.000.000, como 2.000 DPs com 2.000 itens de conteúdo, considere o uso do SQL Server completo nos sites secundários. 

### <a name="should-i-change-maxdop-settings-on-my-database"></a>Devo alterar as configurações de MaxDOP em meu banco de dados?

Manter a configuração em 0 (usar todos os processadores disponíveis) é ideal para o desempenho do processamento geral na maioria das circunstâncias.

Muitos administradores do Configuration Manager seguem as diretrizes de [Recomendações e diretrizes para a opção de configuração "grau máximo de paralelismo" do SQL Server](https://support.microsoft.com/help/2806535/recommendations-and-guidelines-for-the-max-degree-of-parallelism-confi). Na maioria dos equipamentos grandes de hardware mais modernos, essas diretrizes sugerem uma configuração máxima igual a oito. No entanto, se você executar muitas consultas menores em comparação ao número de processadores, talvez seja útil defini-lo com um número maior. Limitar-se a oito não será necessariamente a melhor configuração em sites maiores quando houver mais núcleos disponíveis. 

Em servidores SQL com mais de oito núcleos, comece com uma configuração igual a 0 e só faça alterações se você enfrentar problemas de desempenho ou bloqueio excessivo. Caso você precise alterar o MaxDOP por estar tendo problemas de desempenho com o valor 0, comece com um novo valor, pelo menos, superior ou igual ao número mínimo recomendado de núcleos para o dimensionamento do SQL Server do site. Escolher um número menor que esse valor sempre tem implicações negativas de desempenho. Por exemplo, um SQL Server remoto para um site de 100.000 clientes precisa de, pelo menos, 12 núcleos. Se o SQL Server tiver 16 núcleos, comece testando a configuração de MaxDOP com um valor igual a 12.

## <a name="other-common-performance-related-questions"></a>Outras perguntas comuns relacionadas ao desempenho

### <a name="which-folders-on-the-site-server-or-other-roles-should-i-exclude-for-antivirus-software"></a>Quais pastas no servidor do site (ou outras funções) devo excluir do software antivírus?

Tome cuidado ao desabilitar a proteção antivírus em qualquer sistema. Em ambientes seguros e de alto volume, recomendamos desabilitar o *monitoramento ativo* para um desempenho ideal.

Para obter mais informações sobre as exclusões de antivírus recomendadas, confira [Exclusões de antivírus recomendadas para clientes, sistemas de sites e servidores do site do Configuration Manager 2012 e do Branch Atual](https://support.microsoft.com/help/327453/recommended-antivirus-exclusions-for-configuration-manager-2012-and-cu).

### <a name="what-can-i-do-to-make-wsus-perform-better-when-its-used-with-configuration-manager"></a>O que pode ser feito para melhorar o desempenho do WSUS quando ele é usado com o Configuration Manager?

A alteração de algumas configurações principais do IIS, como o limite do Comprimento da Fila e da Memória Privada de WsusPool, pode melhorar o desempenho do WSUS, até mesmo em instalações menores. Para obter mais informações, confira [Hardware recomendado](../plan-design/configs/recommended-hardware.md).

Além disso, verifique se você tem as últimas atualizações instaladas para o sistema operacional que executa o WSUS:

- Windows Server 2012: Qualquer atualização não cumulativa "Somente segurança" lançada em outubro de 2017 ou após essa data. ([KB4041690](https://support.microsoft.com/help/4041690/windows-server-2012-update-kb4041690))
- Windows Server 2012 R2: Qualquer atualização não cumulativa "Somente segurança" lançada em agosto de 2017 ou após essa data. ([KB4039871](https://support.microsoft.com/help/4039871/windows-8-1-windows-server-2012-r2-update-kb4039871))
- Windows Server 2016: qualquer atualização não cumulativa "Somente segurança" lançada em agosto de 2017 ou após essa data. ([KB4039396](https://support.microsoft.com/help/4039396/windows-10-update-kb4039396))

### <a name="what-type-of-maintenance-should-i-run-on-my-wsus-servers"></a>Que tipo de manutenção devo executar em meus servidores WSUS?

Confira [O guia completo para manutenção do Microsoft WSUS e do Configuration Manager SUP](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint).

### <a name="i-want-to-set-up-basic-performance-monitoring-for-my-site-what-should-i-watch"></a>Desejo configurar o monitoramento de desempenho básico para meu site. O que devo inspecionar?

O monitoramento tradicional de desempenho do servidor funciona de forma eficaz para o Configuration Manager em geral. Aproveite também os vários pacotes de gerenciamento do System Center Operations Manager para o Configuration Manager, o SQL Server e o Windows Server a fim de monitorar a integridade básica dos servidores. Monitore também diretamente os contadores do PerfMon (Monitor de Desempenho) do Windows fornecidos pelo Configuration Manager. Monitore as listas de pendências nas várias caixas de entrada em busca de sinais de aviso antecipados de possíveis problemas de desempenho do site ou listas de pendências.

## <a name="see-also"></a>Consulte também

- [Diretrizes sobre desempenho e dimensionamento do site](../plan-design/configs/site-size-performance-guidelines.md)
- [Perguntas frequentes sobre o Configuration Manager no Azure](configuration-manager-on-azure.md)
