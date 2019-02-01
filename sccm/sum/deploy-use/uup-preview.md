---
title: Versão prévia do UUP
titleSuffix: Configuration Manager
description: Instruções para a versão prévia da integração deUUP
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 0b0da585-0096-410b-8035-6b7a312f37f5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 27a960758d8d3939798ae270404d5dd1afbea62d
ms.sourcegitcommit: ad25a7bdd983c5a0e4c95bffdc61c9a1ebcbb765
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2019
ms.locfileid: "55072978"
---
# <a name="uup-private-preview-instructions"></a>Instruções para a versão prévia privada do UUP

> [!Note]  
> Essa informação está relacionada a uma versão prévia do recurso, a qual pode ser substancialmente modificada antes de seu lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

## <a name="benefits"></a>Benefícios

### <a name="feature-updates"></a>Atualizações de recursos

As atualizações de recurso com a Plataforma de Atualização Unificada (UUP) do Windows 10 são projetadas para minimizar os vários problemas que os clientes têm atualmente com manutenção. Experimente as atualizações de recurso de UUP, incluindo:

- Atualizar direto para o nível de conformidade de segurança mais recente, você não precisa instalar atualizações de segurança imediatamente após a atualização para estar em conformidade. A cada mês, uma nova atualização de recurso será publicada para incluir a atualização de segurança cumulativa mais recente. Você não precisará baixar novamente ou distribuir a maior parte do conteúdo de atualização de recurso a cada mês, apenas o componente de atualização de segurança, que também é compartilhado com a atualização cumulativa.

- Todos os Recursos sob Demanda (FODs) e pacotes de idioma devem ser preservados e não perdidos durante o processo de atualização.

- As atualizações de recurso com UUP dão suporte a arquivos de instalação expressa, permitindo que os clientes reduzam a quantidade de conteúdo que cada cliente deve baixar.

Saiba mais sobre a UUP na postagem do blog do Windows [Uma atualização em nossa Plataforma de Atualização Unificada (UUP)](https://blogs.windows.com/windowsexperience/2017/03/02/an-update-on-our-unified-update-platform-uup/).


### <a name="cumulative-updates"></a>Atualizações cumulativas

As atualizações cumulativas com UUP permitem que o conteúdo para FODs e pacotes de idiomas sejam distribuídos offline, permitindo que os usuários finais os adquiram sob demanda, sem necessidade de acessar a Internet nem de esforços de preparo entediantes por parte dos administradores.



## <a name="set-up-instructions"></a>Instruções de configuração

### <a name="1-send-your-wsus-id-to-your-uup-preview-contact-at-microsoft"></a>1. Enviar sua ID do WSUS para seu contato de versão prévia do UUP na Microsoft

Para participar da versão prévia privada do UUP, você deve compartilhar sua ID do WSUS com a Microsoft para que possamos incluir seu ambiente na lista de permissões para a versão prévia. Sem essa ID, não será possível ver todas as atualizações de UUP até a versão prévia tornar-se pública.

Para recuperar sua ID do WSUS:

```PowerShell
$server = Get-WsusServer
$config = $server.GetConfiguration()
$config.ServerId

# also check MUUrl
$config.MUUrl
```

A propriedade **MUUrl** deve ser `https://sws.update.microsoft.com`. Para alterá-la, confira a resolução no seguinte artigo de suporte: [Falha na sincronização do WSUS com SoapException](https://support.microsoft.com/help/4482416/wsus-synchronization-fails-with-soapexception)


### <a name="2-update-configmgr"></a>2. Atualizar o ConfigMgr

Se você estiver sincronizando arquivos de instalação expressa em seu ambiente, o branch atual do ConfigMgr 1810 será necessário para os ambientes de produção ou o branch 1812 de visualização técnica para os ambientes de laboratório.

Se você não estiver sincronizando arquivos de instalação expressa em seu ambiente, o hotfix KB4482615 do ConfigMgr 1810 também será necessário para os ambientes de produção ou o branch 1812 de visualização técnica para os ambientes de laboratório.


#### <a name="diagnostics-and-usage-data-level"></a>Nível de dados de diagnóstico e de uso
Considere aumentar o nível de dados de diagnóstico e de uso do Configuration Manager durante esta versão prévia. O nível **Completo** ajuda a Microsoft a analisar e solucionar problemas de uma maneira melhor com esse novo recurso. Para obter mais informações, confira [Níveis de coleta de dados de diagnóstico e de uso da versão 1810](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1810).


#### <a name="update-rollup-for-configmgr-1810-4486457"></a>Pacote cumulativo de atualizações do ConfigMgr 1810 (4486457)

1. Atualize o site com o pacote cumulativo de atualizações da versão 1810. Para obter mais informações, confira [Instalar atualizações no console](/sccm/core/servers/manage/install-in-console-updates).  

2. Atualize clientes.  

    - Para simplificar este processo, considere o uso da atualização automática do cliente. Para obter mais informações, consulte [Atualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  

    - Todos os clientes aos quais que você direcionar atualizações de UUP precisam ser atualizados para evitar **baixar desnecessariamente cerca de 6 GB** de conteúdo não utilizado para o cliente.

Para obter mais informações sobre essa atualização, confira [Update rollup for System Center Configuration Manager current branch, version 1810](https://support.microsoft.com/help/4486457) (Pacote cumulativo de atualizações do branch atual do System Center Configuration Manager, versão 1810).


<!-- 
#### 1812 Technical Preview
The 1812 Technical Preview is equivalent in supported UUP scenarios to the ConfigMgr 1810 UUP Hotfix (KB4482615).

The only note is that client upgrade of 1812 Technical Preview is broken from 1810.1 TP or 1811 TP. To work around this issue, you'll need to uninstall 1810.1 TP and 1811 TP clients, then install the 1812 TP client cleanly. All clients you target UUP updates to must be on 1812 Technical Preview (or later) to prevent **unnecessarily downloading around 6 GB** of unused content to the client.
 -->


### <a name="3-update-windows-clients-to-supported-versions"></a>3. Atualizar clientes do Windows para as versões compatíveis

#### <a name="for-express-installation-file-sync"></a>Para sincronização de arquivos de instalação expressa
Para conteúdo expresso, as versões compatíveis do Windows incluem:

- **Windows 10 versão 1809** com a atualização cumulativa não relacionada a segurança [KB4476976](https://support.microsoft.com/help/4476976/windows-10-update-kb4476976) (lançada em 1/22) ou posterior. Esta atualização só está disponível no catálogo e não sincroniza diretamente para o WSUS. Para importar a atualização para o seu ambiente a fim de implantá-la, confira [Importar atualizações do catálogo do Microsoft Update](/sccm/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog).

- **Windows 10 versão 1803** com [KB4284835](https://support.microsoft.com/help/4284835) (atualização de segurança cumulativa de junho de 2017) ou posterior  

- **Windows 10 versão 1709** com [KB4338825](https://support.microsoft.com/help/4338825) (atualização de segurança cumulativa de julho de 2017) ou posterior  


#### <a name="for-non-express-installation-file-sync"></a>Para sincronização de arquivos de instalação não expressa
Para conteúdo não expresso, um patch adicional precisa ser aplicado. Esta atualização é crítica para evitar o download desnecessário de cerca de 6 GB de conteúdo não usado para o cliente. As versões do Windows compatíveis incluem os seguintes builds:

- **Windows 10 versão 1809** com a atualização cumulativa não relacionada a segurança [KB4476976](https://support.microsoft.com/help/4476976/windows-10-update-kb4476976) (lançada em 1/22) ou posterior. Esta atualização só está disponível no catálogo e não sincroniza diretamente para o WSUS. Para importar a atualização para o seu ambiente a fim de implantá-la, confira [Importar atualizações do catálogo do Microsoft Update](/sccm/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog).


- Os clientes do **Windows 10 versão 1803** e do **Windows 10 versão 1709** precisam ter um nível base de atualização cumulativa mais a atualização não cumulativa:
    - Atualização cumulativa
        - 1803: [KB4284835](https://support.microsoft.com/help/4284835) (atualização de segurança cumulativa de junho de 2017) até atualização de segurança cumulativa de janeiro de 2019, inclusive
        - 1709: [KB4338825](https://support.microsoft.com/help/4338825) (atualização de segurança cumulativa de julho de 2017) até atualização de segurança cumulativa de janeiro de 2019, inclusive
    - Atualização não cumulativa: Esta atualização só está disponível no catálogo e não sincroniza diretamente para o WSUS. Para importar a atualização para o seu ambiente a fim de implantá-la, confira [Importar atualizações do catálogo do Microsoft Update](/sccm/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog).
        - 1803: [KB4483541](https://support.microsoft.com/help/4483541)
        - 1709: [KB4483530](https://support.microsoft.com/help/4483530)


### <a name="4-enable-express-installation-on-clients-in-client-settings"></a>4. Habilitar a instalação expressa nos clientes nas configurações do cliente

A configuração para habilitar a instalação expressa do cliente precisa ser definida para atualizações de UUP, independentemente de o conteúdo expresso ser sincronizado ou não. Com essa configuração, o ConfigMgr pode permitir que o WUA (Windows Update Agent) determine o conteúdo necessário a baixar para os clientes, em vez de fazer com que o ConfigMgr baixe todo o conteúdo associado à atualização da UUP. Essa configuração é necessária mesmo para cenários não expressos, pois há conteúdo opcional de FOD e de pacote de idiomas, resultando em uma quantidade não significativa de dados extra que não são necessários para todos os clientes associados à atualização.

Habilitar essa configuração não afetará os downloads de conteúdo do servidor, somente os comportamentos de download do cliente. É importante que você tenha o ConfigMgr e as versões de cliente do Windows articuladas acima antes de habilitar essa configuração se ela ainda não foi habilitada, pois essas versões corrigem alguns problemas de compatibilidade com a aprovação de atualizações diretamente no WSUS, além de habilitarem o ConfigMgr a usar esse canal para atualizações de UUP, mesmo se o conteúdo expresso não estiver sincronizado.

Para habilitar a instalação expressa nos clientes:

1. No console do Configuration Manager, vá até **Administração** \ **Configurações do Cliente**  

2. Abra as propriedades das Configurações do Cliente que você deseja usar ou crie um novo para implantar conforme apropriado.  

3. No grupo **Atualizações de Software**, defina **Habilitar a instalação de arquivos de instalação expressos em clientes** para **Sim**

![Realçando a configuração do cliente no grupo de Atualizações de Software](../media/uup-preview-client-settings.png)


### <a name="5-make-sure-your-adrs-are-set-as-desired"></a>5. Verifique se as ADRs estão definidas conforme desejado 

Antes de habilitar a sincronização de atualizações da UUP, considere suas regras de implantação automática (ADRs) e qualquer outra infraestrutura de atualização em vigor. Se você não quiser que essas atualizações sejam implantadas automaticamente como parte de suas ADRs e planos de manutenção existentes, não deixe de atualizar suas ADRs para filtrá-las. Confira [Como localizar atualizações de UUP sincronizadas](#how-to-find-synced-uup-updates). Planos de serviço existentes implantarão não UPP somente por padrão, mas você pode atualizá-los para alterar esse comportamento.

Considere também se essas atualizações afetarão qualquer um dos seus relatórios de conformidade ou outras infraestruturas apenas sincronizando-os e faça quaisquer modificações desejadas com antecedência. Por exemplo, se você medir a conformidade para todos os produtos, você verá agora ambas a atualização do Windows 10 cumulativa UPP e a não UPP como em conformidade ou sem conformidade, o que causará, portanto, uma distorção em seus números.



## <a name="enable-uup-and-start-testing"></a>Habilitar UUP e começar a testar

### <a name="select-products-and-classifications-to-sync"></a>Selecionar os produtos e classificações a sincronizar

Depois que você está pronto para começar a sincronizar atualizações de UUP e experimentá-las, bem como recebeu uma comunicação da Microsoft informando que habilitamos o seu WSUS para ver o piloto, habilite os novos produtos.

1. [Sincronizar Atualizações de Software](/sccm/sum/get-started/synchronize-software-updates) para permitir que os novos produtos sejam populados  

2. No console do Configuration Manager, acesse **Administração** \ **Configuração do Site** \ **Sites**  

3. Selecione seu site de nível superior, que é um site de administração central (CAS) ou um autônomo primário  

4. Abra **Configurar Componentes do Site** \ **Ponto de Atualização do Software**  

5. Na guia **Produtos**, depois que o servidor do WSUS é adicionado à versão prévia, dois novos produtos deverão aparecer. Esses produtos contêm a conteúdo da versão prévia de UUP.  

    - **Versão prévia do Windows 10 UUP**  
    - **Versão prévia do Windows Server UUP**  

6. Na guia **Classificações**, não deixe de selecionar:  

    - **Atualizações de Segurança**: Para ver as Atualizações Cumulativas do UUP  
    - **Atualizações**: Para ver as Atualizações de Recurso do UUP  

7. Sincronizar atualizações de software para ver as novas atualizações de UUP


### <a name="how-to-find-synced-uup-updates"></a>Como encontrar atualizações de UUP sincronizadas

Depois de ter sincronizado atualizações de UUP em seu ambiente, você desejará encontrá-las para que sejam testadas. Há duas maneiras fáceis de encontrar as atualizações de versão prévia dentro do console do Configuration Manager.

- Como essas atualizações de versão prévia estão em produtos separados, você sempre pode usar o produto para filtrar ou encontrar essas atualizações. O filtro de produto foi adicionado a Planos de Manutenção para que você possa selecionar se deseja implantar as atualizações de recurso UUP ou não UUP.  

- Há uma nova coluna opcional **Marca**, nos nós **Todas as Atualizações de Software** e **Todas as Atualizações do Windows 10** da biblioteca de Software, bem como um filtro em ADRs. Esse campo é definido como **UUP** para atualizações de UUP e em branco para atualizações não UUP.  


### <a name="updates-available-during-preview"></a>Atualizações disponíveis durante a versão prévia

- Atualizações Cumulativas do Windows 10 1809
    - Atualização de segurança de fevereiro (12/2)  

- Atualizações Cumulativas do Windows 10 1803
    - Atualização de segurança de dezembro (11/12)
    - Atualização de segurança de janeiro (8/1)
    - Atualização não de segurança de janeiro (15/1)
    - Atualização de segurança de fevereiro (12/2)  

- Atualizações Cumulativas do Windows 10 1709
    - Atualização de segurança de dezembro (11/12)
    - Atualização de segurança de janeiro (8/1)
    - Atualização não de segurança de janeiro (15/1)
    - Atualização de segurança de fevereiro (12/2)  

- Atualizações de Recursos do Windows 10 1809 (de 1709 a 1803)
    - Conformidade de atualizações de segurança de dezembro (11/12)
    - Conformidade de atualizações de segurança de janeiro (8/1)
    - Conformidade de atualizações de segurança de fevereiro (12/2)  

- Atualizações de Recursos do Windows 10 1803 (de 1709 a 1803)   
    - Conformidade de atualizações de segurança de dezembro (11/12)
    - Conformidade de atualizações de segurança de janeiro (8/1)
    - Conformidade de atualizações de segurança de fevereiro (12/2)  

Se necessário, a atualização de segurança de março e outras futuras continuarão a ser publicadas em todas essas áreas enquanto o UUP ainda estiver em versão prévia (pública ou privada). Depois de concluirmos a versão prévia, somente as Atualizações Cumulativas do Windows 10 versão 1809 e Atualizações de Recurso (do Windows 10 versão 1803 em diante) serão compatíveis em produção.


### <a name="scenarios-to-try"></a>Cenários para experimentar

#### <a name="feature-updates"></a>Atualizações de recursos
- Atualizar diretamente para o nível de conformidade de segurança de sua escolha  

- Atualizar com FODs e pacotes de idiomas instalados antes da atualização, eles são preservados durante a atualização  

- Opcionalmente, habilite a sincronização de arquivos de instalação expressa para atualizações de recursos para reduzir a quantidade de conteúdo que cada cliente deve baixar.  

    > [!Note]  
    > Esse benefício do cliente ocorre às custas de maior download de servidor e a distribuição, como é o caso para arquivos de instalação expressa para atualizações cumulativas.  

#### <a name="cumulative-updates"></a>Atualizações cumulativas
Durante a versão prévia, mantenha os clientes em conformidade usando a atualização do tipo de UUP para várias atualizações consecutivas, a fim de conhecer continuamente as expectativas.

#### <a name="content"></a>Conteúdo
A primeira atualização de cada versão principal (1809, 1803, 1709), arquitetura e combinação de idioma parecerá ser grande, em número de arquivos e espaço em disco, em comparação com as atualizações anteriores que não eram da UUP. Este conteúdo extra é principalmente para todos os pacotes de idiomas e de FOD para as atualizações cumulativas. Para atualizações de recurso, especialmente se a expressa está habilitada, há conteúdo adicional que é grande para essa primeira atualização. 

No entanto, as atualizações subsequentes (as atualizações cumulativas e as atualizações de recurso mensal em níveis mais altos de conformidade), a quantidade de conteúdo novo que precisa ser baixado e distribuído será muito menor, já que todo o conteúdo de pacote de idiomas e de FOD é compartilhado de forma inteligente entre as atualizações, em vez de baixado novamente ou redistribuído. Durante a versão prévia, em 1709 e 1803, esse download mensal será aproximadamente equivalente ao tamanho das atualizações cumulativas que você vê em cenários não UUP. No entanto, na 1809, a história fica muito melhor, pois o download incremental da atualização cumulativa é muito menor de mês a mês. 

Quando você vê o conteúdo total baixado e distribuído em um período de 12 meses para não expressa, a 1803 sem UUP deve ser aproximadamente equivalente à 1809 com UUP e, depois desse ponto de virada, o conteúdo total baixado e distribuído em todo o tempo de vida da versão é menor na 1809 com UUP. Para a expressa, o ponto de virada é mais cedo do que com a 1809, pois a expressa é somente para atualizações de recursos não cumulativas e, portanto, o custo da expressa para conteúdo do servidor de grande porte é apenas uma vez por versão, em vez de mensal.

#### <a name="supported-content-channels"></a>Canais de conteúdo compatíveis
Para a versão prévia, teste com o que você usa em seus ambientes empresariais reais. O UUP dará suporte a todos os canais de conteúdo, incluindo:
- Otimização de Entrega do Windows
- Cache par do Configuration Manager
- Windows BranchCache
- Implantar sem baixar para o servidor (sem pacote de implantação) para baixar diretamente do site Microsoft Update, cujo uso se recomenda em conjunto com a otimização de entrega
- Provedores terceiros de conteúdo alternativo

Para obter mais informações, confira [Otimizar a entrega de atualização do Windows 10](/sccm/sum/deploy-use/optimize-windows-10-update-delivery).
