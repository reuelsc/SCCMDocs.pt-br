---
title: Estender o inventário de hardware
titleSuffix: Configuration Manager
description: Saiba como estender o inventário de hardware no System Center Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1dc296dabe56ec95c736c84f4ddf5e9fb8086be2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56136840"
---
# <a name="how-to-extend-hardware-inventory-in-system-center-configuration-manager"></a>Como estender o inventário de hardware no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O inventário de hardware lê as informações de Computadores Windows usando o WMI (Instrumentação de Gerenciamento do Windows). O WMI é a implementação da Microsoft do WBEM (Web-Based Enterprise Management), um padrão do setor para o acesso a informações de gerenciamento em uma empresa. Nas versões anteriores do Configuration Manager, você estendia o inventário de hardware modificando o arquivo sms_def.mof no servidor do site. Este arquivo continha uma lista de classes WMI que podia ser lida pelo inventário de hardware. Editando esse arquivo, você podia habilitar e desabilitar as classes existentes e também criar novas classes no inventário.  

O arquivo Configuration.mof é usado para definir as classes de dados a ser inventariadas pelo inventário de hardware no cliente e permanece inalterado desde o Configuration Manager 2012. É possível criar classes de dados para inventariar classes de dados de repositório WMI existentes ou personalizadas ou chaves de Registro presentes nos sistemas cliente.  

 O arquivo MOF também define e registra os provedores WMI que acessam informações de dispositivo durante o inventário de hardware. Registrar provedores define o tipo de provedor a ser usado e as classes que o provedor oferece suporte.  

 Quando os clientes do Configuration Manager solicitam a política, o Configuration.mof é anexado ao corpo da política. Esse arquivo é baixado e compilado pelos clientes. Quando você adicionar, modificar ou excluir classes de dados do arquivo MOF, clientes compilação automaticamente essas alterações são feitas para classes de dados relacionados ao estoque. Nenhuma ação adicional é necessária para classes de inventário de dados novos ou modificados nos clientes do Configuration Manager. Esse arquivo está localizado em **<CMInstallLocation\>\Inboxes\clifiles.src\hinv\\** nos servidores do site primário.  

 No Configuration Manager, você não mais edita o arquivo sms_def.mof como fazia no Configuration Manager 2007. Em vez disso, você pode habilitar e desabilitar classes WMI e adicionar novas classes para coletar por inventário de hardware usando as configurações do cliente. O Configuration Manager fornece os seguintes métodos para estender o inventário de hardware.  

> [!NOTE]  
>  Se você alterava manualmente o arquivo Configuration.mof para adicionar classes de inventário personalizadas, essas alterações eram substituídas ao atualizar para a versão 1602. Para continuar usando classes personalizadas após a atualização, adicione-as à seção "Extensões adicionadas" do arquivo Configuration.mof após a atualização para 1602.  
> No entanto, não modifique nada acima desta seção, pois essas seções são reservadas para modificação pelo Configuration Manager. Um backup de seu Configuration.mof personalizado pode ser encontrado em:  
> **<CM Install dir\>\data\hinvarchive\\**.  

|Método|Mais informações|  
|------------|----------------------|  
|Habilitar ou desabilitar as classes existentes de inventário|Habilitar ou desabilitar as classes de inventário padrão ou criar configurações de cliente personalizadas que permitem que você colete as diferentes classes de inventário de hardware de coleções especificadas de clientes. Veja o procedimento [Para habilitar ou desabilitar as classes de inventário existentes](#BKMK_Enable) neste artigo.|  
|Adicione uma nova classe de inventário|Adicionar uma nova classe de inventário do namespace WMI de outro dispositivo. Veja o procedimento [Para adicionar uma nova classe de inventário](#BKMK_Add) neste artigo.|  
|Importar e exportar classes de inventário de hardware|Importar e exportar arquivos MOF (Managed Object Format) que contêm classes de inventário do console do Configuration Manager. Veja os procedimentos [Para importar classes de inventário de hardware](#BKMK_Import) e [Para exportar classes de inventário de hardware](#BKMK_Export) neste artigo.|  
|Criar arquivos NOIDMIF|Use arquivos NOIDMIF para coletar informações sobre dispositivos de cliente que não podem ser inventariados pelo Configuration Manager. Por exemplo, você talvez queira coletar informações de número de ativo dispositivo que existe apenas como um rótulo no dispositivo. Inventário NOIDMIF é associado automaticamente a que foram coletado do dispositivo cliente. Consulte [Para criar arquivos NOIDMIF](#BKMK_NOIDMIF) neste artigo.|  
|Criar arquivos IDMIF|Use arquivos IDMIF para coletar informações sobre os ativos em sua organização que não estão associados a um cliente do Configuration Manager, por exemplo, projetores, fotocopiadoras e impressoras de rede. Consulte [Para criar arquivos IDMIF](#BKMK_IDMIF) neste artigo.|  

## <a name="procedures-to-extend-hardware-inventory"></a>Procedimentos para estender o inventário de hardware  
Esses procedimentos ajudam a configurar as configurações padrão do cliente de inventário de hardware e se aplicam a todos os clientes em sua hierarquia. Se quiser que essas configurações se apliquem somente a alguns clientes, crie uma configuração personalizada do dispositivo de cliente e a atribua a uma coleção de clientes específicos. Consulte [Como definir as configurações do cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

###  <a name="BKMK_Enable"></a> Para habilitar ou desabilitar as classes de inventário existentes  

1.  No console do Configuration Manager, escolha **Administração** > **Configurações do Cliente** > **Configurações do Cliente Padrão**.  

4.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

5.  No caixa de diálogo **Configurações do Cliente Padrão**, escolha **Inventário de Hardware**.  

6.  No **configurações do dispositivo** clique em **Definir Classes**.  

7.  No **Classes de inventário de Hardware** caixa de diálogo caixa, marque ou desmarque as classes e propriedades de classe seja coletado pelo inventário de hardware. Você pode expandir classes para marcar ou desmarcar as propriedades individuais dentro dessa classe. Use o **Pesquisar classes de inventário** campo para procurar classes individuais.  

    > [!IMPORTANT]  
    >  Quando você adiciona novas classes ao inventário de hardware do Configuration Manager, aumenta o tamanho do arquivo de inventário que é coletado e enviado ao servidor do site. Isso pode afetar negativamente o desempenho da rede e do site do Configuration Manager. Habilite somente as classes de inventário que você deseja coletar.  


###  <a name="BKMK_Add"></a> Para adicionar uma nova classe de inventário  

Você pode adicionar classes de inventário somente do servidor de nível superior da hierarquia modificando as configurações padrão do cliente. Essa opção não está disponível quando você cria configurações personalizadas do dispositivo.

1. No console do Configuration Manager, escolha **Administração** > **Configurações do Cliente** > **Configurações do Cliente Padrão**.  

2. Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

3. No caixa de diálogo **Configurações do Cliente Padrão**, escolha **Inventário de Hardware**.  

4. Na lista **Configurações do Dispositivo**, escolha **Definir Classes**.  

5. Na caixa de diálogo **Classes de Inventário de Hardware**, escolha **Adicionar**.  

6. No **Adicionar classe de inventário de Hardware** caixa de diálogo, clique em **conectar**.  

7. No **conectar ao Windows Management Instrumentation (WMI)** caixa de diálogo, especifique o nome do computador do qual você recuperará as classes WMI e o namespace a ser usado para recuperar as classes WMI. Se você quiser recuperar todas as classes abaixo o namespace WMI que você especificou, clique em **recursiva**. Se o computador que você está se conectando não estiver no computador local, forneça as credenciais de logon para uma conta que tenha permissão para acessar o WMI no computador remoto.  

8. Escolha **Conectar**.  

9. Na caixa de diálogo **Adicionar Classe de Inventário de Hardware**, na lista **Classes de inventário**, selecione as classes WMI que deseja adicionar ao inventário de hardware do Configuration Manager.  

10. Se você quiser editar informações sobre a classe WMI selecionada, escolha **Editar** e, na caixa de diálogo **Qualificadores de classe**, forneça as seguintes informações:  

    - **Nome de exibição** – esse nome será exibido no Gerenciador de Recursos.  

    - **Propriedades** – especifique as unidades em que cada propriedade da classe WMI será exibida.  

      Você também pode designar propriedades como uma propriedade de chave para ajudar a identificar exclusivamente cada instância da classe. Se nenhuma chave estiver definida para a classe e várias instâncias da classe são informadas do cliente, apenas a instância mais recente encontrada é armazenada no banco de dados.  

      Quando terminar de configurar as propriedades, clique em **OK** para fechar a caixa de diálogo **Qualificadores de classe** e as outras caixas de diálogo abertas. 

###  <a name="BKMK_Import"></a> Para importar classes de inventário de hardware  

Você só pode importar classes de inventário quando você modifica as configurações de cliente padrão. No entanto, você pode usar configurações personalizadas do cliente para importar as informações que não incluem uma alteração de esquema, como a alteração da propriedade de uma classe existente de **True** para **False**.  

1.  No console do Configuration Manager, escolha **Administração** >  **Configurações do Cliente** > **Configurações do Cliente Padrão**.  

4.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

5.  No caixa de diálogo **Configurações do Cliente Padrão**, escolha **Inventário de Hardware**.  

6.  Na lista **Configurações do Dispositivo**, escolha **Definir Classes**.  

7.  Na caixa de diálogo **Classes de Inventário de Hardware**, escolha **Importar**.  

8.  Na caixa de diálogo **Importar**, selecione o arquivo MOF (Managed Object Format) que deseja importar e, em seguida, escolha **OK**. Examine os itens que serão importados e, em seguida, clique em **Importar**.  

###  <a name="BKMK_Export"></a> Para exportar classes de inventário de hardware  

1.  No console do Configuration Manager, escolha **Administração** > **Configurações do Cliente** > **Configurações do Cliente Padrão**.  

4.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

5.  No caixa de diálogo **Configurações do Cliente Padrão**, escolha **Inventário de Hardware**.  

6.  Na lista **Configurações do Dispositivo**, escolha **Definir Classes**.  

7.  Na caixa de diálogo **Classes de Inventário de Hardware**, escolha **Exportar**.  

    > [!NOTE]  
    >  Quando você exporta classes, todas as classes atualmente selecionadas serão exportadas.  

8.  Na caixa de diálogo **Exportar**, especifique o arquivo MOF (Managed Object Format) para o qual deseja exportar as classes e, em seguida, escolha **Salvar**.  

### <a name="bkmk_GreaterThan255"></a> Configurar o inventário de hardware para coletar cadeias de caracteres com mais de 255 caracteres
A partir do Configuration Manager 1802, você pode especificar o tamanho das cadeias de caracteres para que tenham mais de 255 caracteres nas propriedades de inventário de hardware. Essa alteração se aplica apenas às classes recém-adicionadas e às propriedades de inventário de hardware que não são chaves. <!-- 1357389 -->

1. No workspace **Administração**, clique em **Configurações do Cliente**, realce uma configuração de dispositivo cliente a ser editada, clique com o botão direito do mouse e selecione **Propriedades**.

2. Selecione **Inventário de Hardware** e, em seguida, **Definir Classes** e **Adicionar**.

3. Clique no botão **Conectar**.

4. Preencha **Nome do Computador**, **Namespace do WMI**, selecione **recursivo** se necessário. Forneça credenciais, se necessário, para se conectar. Clique em **Conectar** para exibir as classes do namespace.

5. Selecione uma nova classe e clique em **Editar**.

6. Altere o **Tamanho** da propriedade que é uma cadeia de caracteres, não uma chave, tornando-o maior que 255. Clique em **OK**. 

7. Certifique-se de que a propriedade editada está selecionada para **Adicionar Classe de Inventário de Hardware** e clique em **OK**. 


## <a name="how-to-use-management-information-files-mif-files-to-extend-hardware-inventory"></a>Como usar arquivos MIF (Arquivos de Informações de Gerenciamento) para estender o inventário de hardware  
 Use arquivos MIF (Management Information Format) para estender as informações de inventário de hardware coletadas de clientes pelo Configuration Manager. Durante o inventário de hardware, as informações armazenadas em arquivos MIF são adicionadas ao relatório de inventário de cliente e armazenadas no banco de dados do site, onde você pode usar os dados da mesma maneira que você use dados de inventário de cliente padrão. Há dois tipos de arquivos MIF: NOIDMIF e IDMIF.

> [!IMPORTANT]  
>  Antes de adicionar informações de arquivos MIF ao banco de dados do Configuration Manager, você deve criar ou importar informações de classe para eles. Para obter mais informações, consulte as seções [Para adicionar uma nova classe de inventário](#BKMK_Add) e [Para importar classes de inventário de hardware](#BKMK_Import) neste artigo.  

###  <a name="BKMK_NOIDMIF"></a> Para criar arquivos NOIDMIF  
 Os arquivos NOIDMIF podem ser usados para adicionar informações a um inventário de hardware do cliente que, normalmente, não pode ser coletado pelo Configuration Manager e está associado a um dispositivo cliente específico. Por exemplo, muitas empresas rotulam cada computador na organização com um número de ativo e, em seguida, catalogam esses números manualmente. Quando você cria um arquivo NOIDMIF, essas informações podem ser adicionadas ao banco de dados do Configuration Manager e ser usadas para consultas e relatórios. Para obter informações sobre como criar arquivos NOIDMIF, veja a documentação do SDK do Configuration Manager.  

> [!IMPORTANT]  
>  Quando você cria um arquivo NOIDMIF, ele deve ser salvo em um formato codificado em ANSI. Arquivos NOIDMIF salvos no formato codificado UTF-8 não podem ser lidos pelo Configuration Manager.  

 Depois de criar um arquivo NOIDMIF, armazene-o na pasta _%Windir%_**\CCM\Inventory\Noidmifs** em cada cliente. O Configuration Manager coleta informações de arquivos NODMIF nesta pasta durante o próximo ciclo de inventário de hardware agendado.  

###  <a name="BKMK_IDMIF"></a> Para criar arquivos IDMIF  
 Os arquivos IDMIF podem ser usados para adicionar informações sobre ativos, que normalmente não podem ser inventariados pelo Configuration Manager e que não estão associados a um dispositivo cliente específico, ao banco de dados do Configuration Manager. Por exemplo, você pode usar arquivos IDMIF para coletar informações sobre projetores, players de DVD, fotocopiadoras ou outros equipamentos que não têm um cliente do Configuration Manager. Para obter informações sobre como criar arquivos IDMIF, veja a documentação do SDK do Configuration Manager.  

 Depois de criar um arquivo IDMIF, armazene-o na pasta _%Windir%_**\CCM\Inventory\Idmifs** nos computadores cliente. O Configuration Manager coleta informações desse arquivo durante o próximo ciclo de inventário de hardware agendado. Você deve declarar novas classes para informações contidas no arquivo adicionando ou importá-los.  

> [!NOTE]
> Os arquivos MIF podem conter grandes quantidades de dados e a coleta desses dados pode prejudicar o desempenho de seu site. Habilite a coleta de MIF somente quando necessário e configure a opção **Tamanho máximo de arquivo MIF personalizado (KB)** nas configurações de inventário de hardware. Para mais informações, consulte [Introdução ao inventário de hardware no System Center Configuration Manager](introduction-to-hardware-inventory.md).
