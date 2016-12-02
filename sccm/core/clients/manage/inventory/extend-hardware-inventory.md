---
title: "Estender o inventário de hardware | System Center Configuration Manager"
description: "Saiba como estender o inventário de hardware no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
caps.latest.revision: 10
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: 4a42e266c4152145a4a1c291804ff98934671692


---
# <a name="how-to-extend-hardware-inventory-in-system-center-configuration-manager"></a>Como estender o inventário de hardware no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O inventário de hardware do System Center Configuration Manager lê as informações sobre dispositivos de PCs com Windows usando o WMI (Instrumentação de Gerenciamento do Windows). O WMI é a implementação pela Microsoft do WBEM (Web-Based Enterprise Management), que é um padrão da indústria para o acesso a informações de gerenciamento em um ambiente corporativo. Nas versões anteriores do Configuration Manager, você pode estender o inventário de hardware, modificando o arquivo sms_def.mof no servidor do site. Este arquivo continha uma lista de classes WMI que pode ser lido pelo inventário de hardware do Configuration Manager. Se você editou esse arquivo, você poderia habilitar e desabilitar as classes existentes e também criar novas classes no inventário.  

 O arquivo Configuration.mof é usado para definir as classes de dados a ser inventariadas pelo inventário de hardware no cliente e permanece inalterado desde o Configuration Manager 2012. É possível criar classes de dados para inventariar classes de dados de repositório WMI existentes ou personalizadas ou chaves de Registro presentes nos sistemas cliente.  

 O arquivo MOF também define e registra os provedores WMI que acessam informações de dispositivo durante o inventário de hardware. Registrar provedores define o tipo de provedor a ser usado e as classes que o provedor oferece suporte.  

 Quando os clientes do Configuration Manager solicitam a política, por exemplo, durante o intervalo de sondagem da política de cliente padrão, o Configuration.mof é anexado ao corpo da política. Esse arquivo é baixado e compilado pelos clientes. Quando você adicionar, modificar ou excluir classes de dados do arquivo MOF, clientes compilação automaticamente essas alterações são feitas para classes de dados relacionados ao estoque. Nenhuma ação adicional é necessária para classes de inventário de dados novos ou modificados nos clientes do Configuration Manager. Esse arquivo está localizado em **<CMInstallLocation\>\Inboxes\clifiles.src\hinv\\** nos servidores do site primário.  

 No Configuration Manager, você não mais edita o arquivo sms_def.mof como fazia no Configuration Manager 2007. Em vez disso, você pode habilitar e desabilitar classes WMI e adicionar novas classes para coletar por inventário de hardware usando as configurações do cliente. O Configuration Manager fornece os seguintes métodos para estender o inventário de hardware.  

> [!NOTE]  
>  Se você tiver alterado manualmente o arquivo Configuration.mof para adicionar classes de inventário personalizados, essas alterações serão substituídas quando você atualizar para a versão 1602. Para continuar usando classes personalizadas após a atualização, adicione-as à seção “Extensões adicionadas” do arquivo Configuration.mof após a atualização para 1602.  
> No entanto, não modifique nada acima desta seção, pois essas seções são reservadas para modificação do Configuration Manager. Um backup de seu Configuration.mof personalizado pode ser encontrado em:  
> **<CM Install dir\>\data\hinvarchive\\**.  

|Método|Mais informações|  
|------------|----------------------|  
|Habilitar ou desabilitar as classes existentes de inventário|Você pode habilitar ou desabilitar as classes de inventário padrão usadas pelo Configuration Manager ou pode criar configurações personalizadas do cliente que permitem que você colete as classes de inventário de hardware diferentes de coleções especificadas de clientes. Para obter mais informações, veja o procedimento [Para habilitar ou desabilitar as classes de inventário existentes](#BKMK_Enable) neste tópico.|  
|Adicione uma nova classe de inventário|Você pode adicionar uma nova classe de inventário do namespace WMI de outro dispositivo. Para obter mais informações, veja o procedimento [Para adicionar uma nova classe de inventário](#BKMK_Add) neste tópico.|  
|Importar e exportar classes de inventário de hardware|Você pode importar e exportar arquivos MOF (Managed Object Format) que contêm classes de inventário no console do Configuration Manager. Para obter mais informações, veja os procedimentos [Para importar classes de inventário de hardware](#BKMK_Import) e [Para exportar classes de inventário de hardware](#BKMK_Export) neste tópico.|  
|Criar arquivos NOIDMIF|Use arquivos NOIDMIF para coletar informações sobre dispositivos de cliente que não podem ser inventariados pelo Configuration Manager. Por exemplo, você talvez queira coletar informações de número de ativo dispositivo que existe apenas como um rótulo no dispositivo. Inventário NOIDMIF é associado automaticamente a que foram coletado do dispositivo cliente. Para obter mais informações, consulte [Para criar arquivos NOIDMIF](#BKMK_NOIDMIF) neste tópico.|  
|Criar arquivos IDMIF|Use arquivos IDMIF para coletar informações sobre os ativos em sua organização que não estão associados a um cliente do Configuration Manager, por exemplo, projetores, fotocopiadoras e impressoras de rede. Para obter mais informações, consulte [Para criar arquivos IDMIF](#BKMK_IDMIF) neste tópico.|  

## <a name="procedures-to-extend-hardware-inventory"></a>Procedimentos para estender o inventário de hardware  
 Use os procedimentos a seguir para estender o inventário de hardware, como descrito na tabela anterior.  

 Esses procedimentos ajudam a configurar as configurações padrão do cliente de inventário de hardware e se aplicam a todos os clientes em sua hierarquia. Se quiser que essas configurações se apliquem somente a alguns clientes, crie uma configuração personalizada do dispositivo de cliente e a atribua a uma coleção que contém os dispositivos que deseja inventariar. Para obter mais informações sobre como criar configurações personalizadas do cliente, consulte [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

###  <a name="a-namebkmkenablea-to-enable-or-disable-existing-inventory-classes"></a><a name="BKMK_Enable"></a> Para habilitar ou desabilitar as classes de inventário existentes  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , clique em **Configurações do Cliente**.  

3.  Clique em **Configurações do Cliente Padrão**.  

4.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  No **configurações do cliente padrão** caixa de diálogo, clique em **inventário de Hardware**.  

6.  No **configurações do dispositivo** clique em **Definir Classes**.  

7.  No **Classes de inventário de Hardware** caixa de diálogo caixa, marque ou desmarque as classes e propriedades de classe seja coletado pelo inventário de hardware. Você pode expandir classes para marcar ou desmarcar as propriedades individuais dentro dessa classe. Use o **Pesquisar classes de inventário** campo para procurar classes individuais.  

    > [!IMPORTANT]  
    >  Quando você adiciona novas classes ao inventário de hardware do Configuration Manager, aumenta o tamanho do arquivo de inventário que é coletado e enviado ao servidor do site. Isso pode afetar negativamente o desempenho da rede e do site do Configuration Manager. Habilite somente as classes de inventário que você deseja coletar.  

8.  Clique em **OK** para salvar suas alterações e fechar o **Classes de inventário de Hardware** caixa de diálogo.  

###  <a name="a-namebkmkadda-to-add-a-new-inventory-class"></a><a name="BKMK_Add"></a> Para adicionar uma nova classe de inventário  

1.  No console do Configuration Manager, clique em **Administração**.  

    > [!IMPORTANT]  
    >  Você só pode adicionar classes de inventário do servidor de nível superior na hierarquia e modificando as configurações de cliente padrão. Essa opção não está disponível quando você cria configurações personalizadas do dispositivo.  

2.  No espaço de trabalho **Administração** , clique em **Configurações do Cliente**.  

3.  Clique em **Configurações do Cliente Padrão**.  

4.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  No **configurações do cliente padrão** caixa de diálogo, clique em **inventário de Hardware**.  

6.  No **configurações do dispositivo** clique em **Definir Classes**.  

7.  No **Classes de inventário de Hardware** caixa de diálogo, clique em **Add**.  

8.  No **Adicionar classe de inventário de Hardware** caixa de diálogo, clique em **conectar**.  

9. No **conectar ao Windows Management Instrumentation (WMI)** caixa de diálogo, especifique o nome do computador do qual você recuperará as classes WMI e o namespace a ser usado para recuperar as classes WMI. Se você quiser recuperar todas as classes abaixo o namespace WMI que você especificou, clique em **recursiva**. Se o computador que você está se conectando não estiver no computador local, forneça as credenciais de logon para uma conta que tenha permissão para acessar o WMI no computador remoto.  

10. Clique em **Conectar**.  

11. Na caixa de diálogo **Adicionar Classe de Inventário de Hardware**, na lista **Classes de inventário**, selecione as classes WMI que deseja adicionar ao inventário de hardware do Configuration Manager.  

12. Se você quiser editar informações sobre a classe WMI selecionada, clique em **Editar**, e no **classe qualificadores** caixa de diálogo caixa, forneça as seguintes informações:  

    -   **Nome de exibição** – especifique um nome amigável para a classe que será exibido no Gerenciador de Recursos.  

    -   **Propriedades** – especifique as unidades em que cada propriedade da classe WMI será exibida.  

     Você também pode designar propriedades como uma propriedade de chave para ajudar a identificar exclusivamente cada instância da classe. Se nenhuma chave estiver definida para a classe e várias instâncias da classe são informadas do cliente, apenas a instância mais recente encontrada é armazenada no banco de dados.  

     Quando você terminar de configurar as propriedades, clique em **OK** para fechar o **classe qualificadores** caixa de diálogo.  

13. Clique em OK para fechar o **Adicionar classe de inventário de Hardware** caixa de diálogo.  

14. Clique em **OK** para fechar o **Classes de inventário de Hardware** caixa de diálogo.  

15. Clique em **OK** para fechar a caixa de diálogo **Configurações do Cliente Padrão** .  

###  <a name="a-namebkmkimporta-to-import-hardware-inventory-classes"></a><a name="BKMK_Import"></a> Para importar classes de inventário de hardware  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , clique em **Configurações do Cliente**.  

3.  Clique em **Configurações do Cliente Padrão**.  

    > [!IMPORTANT]  
    >  Você só pode importar classes de inventário quando você modifica as configurações de cliente padrão. No entanto, você pode usar configurações personalizadas do cliente para importar as informações que não contém uma alteração de esquema, como alterar a propriedade de uma classe existente de **True** para **False**.  

4.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  No **configurações do cliente padrão** caixa de diálogo, clique em **inventário de Hardware**.  

6.  No **configurações do dispositivo** clique em **Definir Classes**.  

7.  No **Classes de inventário de Hardware** caixa de diálogo, clique em **importação**.  

8.  No **importar** caixa de diálogo, selecione o formato MOF (Managed Object) do arquivo que você deseja importar e clique **OK**.  

9. No **Resumo da importação** caixa de diálogo caixa, revise os itens que serão importados e, em seguida, clique em **importação**.  

###  <a name="a-namebkmkexporta-to-export-hardware-inventory-classes"></a><a name="BKMK_Export"></a> Para exportar classes de inventário de hardware  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , clique em **Configurações do Cliente**.  

3.  Clique em **Configurações do Cliente Padrão**.  

4.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  No **configurações do cliente padrão** caixa de diálogo, clique em **inventário de Hardware**.  

6.  No **configurações do dispositivo** clique em **Definir Classes**.  

7.  No **Classes de inventário de Hardware** caixa de diálogo, clique em **exportar**.  

    > [!NOTE]  
    >  Quando você exporta classes, todas as classes atualmente selecionadas serão exportadas.  

8.  Na caixa de diálogo **Exportar** , especifique o arquivo MOF (Managed Object Format) para o qual deseja exportar as classes e clique em **Salvar**.  

## <a name="how-to-use-management-information-files-mif-files-to-extend-hardware-inventory"></a>Como usar arquivos MIF (Arquivos de Informações de Gerenciamento) para estender o inventário de hardware  
 Use arquivos MIF (Management Information Format) para estender as informações de inventário de hardware coletadas de clientes pelo Configuration Manager. Durante o inventário de hardware, as informações armazenadas em arquivos MIF são adicionadas ao relatório de inventário de cliente e armazenadas no banco de dados do site, onde você pode usar os dados da mesma maneira que você use dados de inventário de cliente padrão. Há dois tipos de arquivos MIF, NOIDMIF e IDMIF. 

> [!IMPORTANT]  
>  Antes de adicionar informações de arquivos MIF ao banco de dados do Configuration Manager, você deve criar ou importar informações de classe para eles. Para obter mais informações, veja as seções [Para adicionar uma nova classe de inventário](#BKMK_Add) e [Para importar classes de inventário de hardware](#BKMK_Import) neste tópico.  

###  <a name="a-namebkmknoidmifa-to-create-noidmif-files"></a><a name="BKMK_NOIDMIF"></a> Para criar arquivos NOIDMIF  
 Arquivos NOIDMIF podem ser usados para adicionar informações a um inventário de hardware do cliente que normalmente não pode ser coletado pelo Configuration Manager e está associado a um dispositivo de cliente específico. Por exemplo, muitas empresas rotular cada computador da organização com um número de ativo e catálogo esses manualmente. Quando você cria um arquivo NOIDMIF, essas informações podem ser adicionadas ao banco de dados do Configuration Manager e ser usadas para consultas e relatórios. Para obter informações sobre como criar arquivos NOIDMIF, veja a documentação do SDK do Configuration Manager.  

> [!IMPORTANT]  
>  Quando você cria um arquivo NOIDMIF, isso deve ser salvo em um formato codificado de ANSI. Arquivos NOIDMIF salvos no formato codificado UTF-8 não podem ser lidos pelo Configuration Manager.  

 Depois de criar um arquivo NOIDMIF, armazená-la na pasta *% Windir %***\System32\CCM\Inventory\Noidmifs** pasta em cada cliente. O Configuration Manager coleta informações de arquivos NODMIF nesta pasta durante o próximo ciclo de inventário de hardware agendado.  

###  <a name="a-namebkmkidmifa-to-create-idmif-files"></a><a name="BKMK_IDMIF"></a> Para criar arquivos IDMIF  
 Os arquivos IDMIF podem ser usados para adicionar informações sobre ativos ao banco de dados do Configuration Manager, que normalmente não poderiam ser inventariadas pelo Configuration Manager e que não estão associadas a um dispositivo de cliente específico. Por exemplo, você pode usar arquivos IDMIF para coletar informações sobre projetores, players de DVD, fotocopiadoras ou outros equipamentos que não contém um cliente do Configuration Manager. Para obter informações sobre como criar arquivos IDMIF, veja a documentação do SDK do Configuration Manager.  

 Depois de criar um arquivo IDMIF, armazená-la na pasta *% Windir %***\System32\CCM\Inventory\Idmifs** pasta nos computadores cliente. O Configuration Manager coleta informações desse arquivo durante o próximo ciclo de inventário de hardware agendado. Você deve declarar novas classes para informações contidas no arquivo adicionando ou importá-los.  

> [!NOTE] 
> Os arquivos MIF podem conter grandes quantidades de dados e a coleta desses dados pode prejudicar o desempenho de seu site. Habilite a coleta de MIF somente quando necessário e configure a opção **Tamanho máximo de arquivo MIF personalizado (KB)** nas configurações de inventário de hardware. Para mais informações, consulte [Introdução ao inventário de hardware no System Center Configuration Manager](introduction-to-hardware-inventory.md).



<!--HONumber=Nov16_HO1-->


