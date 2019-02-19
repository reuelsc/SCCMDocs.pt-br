---
title: Criar consultas
titleSuffix: Configuration Manager
description: Descubra como criar e importar consultas no System Center Configuration Manager. Inclui dicas e consultas de exemplo.
ms.date: 12/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 46b052b02ebc55beeb27f26a0a302d10dc516e18
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124993"
---
# <a name="how-to-create-queries-in-system-center-configuration-manager"></a>Como criar consultas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode usar este tópico para ajudar a criar ou a importar consultas no System Center Configuration Manager.  

##  <a name="BKMK_Create"></a> Como criar consultas  
 Use este procedimento para ajudar a criar consultas no Configuration Manager.  

#### <a name="to-create-a-query"></a>Para criar uma consulta  

1.  No console do Configuration Manager, escolha **Monitoramento**.  

2.  No workspace **Monitoramento**, escolha **Consultas**. Em seguida, na guia **Início**, no grupo **Criar**, escolha **Criar Consulta**.  

3.  Na guia **Geral** do **Assistente para Criar Consulta**, especifique um nome exclusivo e um comentário opcional para a consulta.  

4.  Se você quiser importar uma consulta existente para usar como base para a nova consulta, escolha **Importar instrução de consulta**. Na caixa de diálogo **Procurar Consulta**, selecione uma consulta existente que você deseja importar e, em seguida, escolha **OK**.  

5.  Na lista **Tipo de Objeto**, selecione o tipo de objeto que deseja que a consulta retorne. A seguinte tabela descreve alguns exemplos do tipo de objeto pelos quais você pode procurar:  

    |Tipo de Objeto|Descrição|  
    |-----------------|-----------------|  
    |**Recursos do sistema**|Use para procurar atributos típicos do sistema, como o nome NetBIOS de um dispositivo, a versão do cliente, o endereço IP do cliente e as informações dos Serviços de Domínio do Active Directory.|  
    |**Recursos de usuário**|Use para procurar informações típicas de usuário, como nomes de usuário, nomes de grupos de usuário e nomes de grupos de segurança.|  
    |**Implantação**|Use para procurar atributos típicos de uma implantação, como o nome da implantação, o agendamento e a coleção à qual ele foi implantado.|  

6.  Escolha **Editar Instrução de Consulta** para abrir a caixa de diálogo *&lt;Propriedades de Consulta\>* **do Nome da Consulta**.  

7.  Na guia **Geral** da caixa de diálogo *&lt;Propriedades da Instrução\>* **do Nome da Consulta**, especifique os atributos que esta consulta retorna e como eles devem ser exibidos. Escolha o ícone **Novo** para adicionar um novo atributo. Você também pode escolher **Mostrar Linguagem de Consulta** para inserir ou editar a consulta diretamente no WQL (WMI Query Language). Para obter exemplos de consultas WMI, veja a seção [Example WQL queries](#BKMK_Example) neste tópico.  

    > [!TIP]  
    > Você pode usar a seguinte documentação de referência do MSDN para ajudá-lo a criar suas próprias consultas WQL:  
    >   
    > -   [WQL (SQL para WMI)](http://go.microsoft.com/fwlink/p/?LinkId=256653)  
    > -   [Cláusula WHERE](http://go.microsoft.com/fwlink/p/?LinkId=256654)  
    > -   [Operadores WQL](http://go.microsoft.com/fwlink/p/?LinkId=256655)  

8.  Na caixa de diálogo **Critérios** da *&lt;Propriedade da Instrução\>* **do Nome da Consulta**, especifique os critérios usados para refinar os resultados da consulta. Por exemplo, você pode retornar apenas os recursos que contêm um código do site de **XYZ** nos resultados da consulta. Você pode configurar vários critérios para uma consulta.  

    > [!IMPORTANT]  
    > Se você criar uma consulta sem critérios, a consulta retornará todos os dispositivos na coleção **Todos os Sistemas** .  

9. Na guia **Junções** da caixa de diálogo *&lt;Propriedades da Instrução\>* **do Nome da Consulta**, é possível combinar dados de dois atributos diferentes nos resultados da consulta. Embora o Configuration Manager crie automaticamente junções de consulta quando você escolhe diferentes atributos para o resultado da consulta, a guia **Junções** fornece opções mais avançadas. As classes de atributo com suporte do System Center 2012 Configuration Manager são mostradas nesta tabela:  

    |Tipo de junção|Descrição|  
    |---------------|-----------------|  
    |Interno|Exibe apenas os resultados correspondentes – sempre usados por junções que são criadas automaticamente.|  
    |Esquerda|Exibe todos os resultados para o atributo base e apenas os resultados correspondentes para o atributo de junção.|  
    |Direita|Exibe todos os resultados para o atributo de junção e apenas os resultados correspondentes para o atributo base.|  
    |Completo|Exibe todos os resultados para o atributo base e o atributo de junção.|  

     Para saber mais sobre como usar as operações de junção, veja a documentação do SQL Server.  

10. Clique em **OK** para fechar a caixa de diálogo *&lt;Propriedades de Instrução\>* **do Nome da Consulta**.  

11. Na guia **Geral** do **Assistente para Criar Consulta**, especifique se os resultados dessa consulta não são limitados aos membros de uma coleção, se são limitados aos membros de uma coleção especificada ou se indicam uma coleção sempre que a consulta é executada.  

12. Conclua o assistente para criar a consulta. A nova consulta é exibida no nó **Consultas** do workspace **Monitoramento**.  

##  <a name="BKMK_Import"></a> Como importar consultas  
 Use este procedimento para ajudar a importar uma consulta para o Configuration Manager. Para obter informações sobre como exportar consultas, consulte [Como gerenciar consultas no System Center Configuration Manager](../../../core/servers/manage/manage-queries.md).  

#### <a name="to-import-a-query"></a>Para importar uma consulta  

1.  No console do Configuration Manager, escolha **Monitoramento**.  

2.  No workspace **Monitoramento**, escolha **Consultas**. Na guia **Início**, no grupo **Criar**, escolha **Importar Objetos**.  

3.  Na página **Nome do Arquivo MOF** do **Assistente para Importar Objetos**, escolha **Procurar** para selecionar o arquivo MOF (Managed Object Format) que contém a consulta que você deseja importar.  

4.  Reveja as informações sobre a consulta a ser importadas e conclua o assistente. A nova consulta é exibida no nó **Consultas** do workspace **Monitoramento**.  

##  <a name="BKMK_Example"></a> Example WQL queries

Esta seção contém as consultas WMI de exemplo que você pode usar em sua hierarquia ou modificá-las para outras finalidades. Para usar essas consultas, escolha **Mostrar Idioma de Consulta** na caixa de diálogo **Propriedades da Instrução de Consulta**. Em seguida, copie e cole a consulta no campo **Instrução de Consulta**.  

> [!TIP]  
> Use o caractere curinga `%` para indicar qualquer cadeia de caracteres. Por exemplo, o `%Visio%` retorna o Microsoft Office Visio 2010.  

### <a name="computers-that-run-windows-7"></a>Computadores que executam o Windows 7

Use a consulta a seguir para retornar a versão de sistema operacional e o nome NetBIOS de todos os computadores que executam o Windows 7.  

> [!TIP]  
> Para retornar os computadores que executam o Windows Server 2008 R2, altere `%Workstation 6.1%` para `%Server 6.1%`.  

```  
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from    
SMS_R_System where   
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 6.1%"  
```  

### <a name="computers-with-a-specific-software-package-installed"></a>Computadores com um pacote de software específico instalado  

Use a consulta a seguir para retornar o nome NetBIOS e o nome do pacote de software de todos os computadores que têm um pacote de software específico instalado. Este exemplo exibe todos os computadores com uma versão do Microsoft Visio instalada. Substitua `Microsoft%Visio%` pelo pacote de software que você deseja consultar.  

> [!TIP]  
> Essa consulta pesquisa o pacote de software usando os nomes que são exibidos na lista de programas no Painel de Controle do Windows.  

```  
select SMS_R_System.NetbiosName,   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from    
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on   
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =   
SMS_R_System.ResourceId where   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "Microsoft%Visio%"  
```  

### <a name="computers-that-are-in-a-specific-active-directory-domain-services-organizational-unit"></a>Computadores que estão em uma unidade organizacional específica dos Serviços de Domínio do Active Directory

Use a consulta a seguir para retornar o nome NetBIOS e o nome da UO (unidade organizacional) de todos os computadores em uma UO especificada. Substitua o texto `OU Name` pelo nome da UO que você deseja consultar.  

```  
select SMS_R_System.NetbiosName,   
SMS_R_System.SystemOUName from    
SMS_R_System where   
SMS_R_System.SystemOUName = "OU Name"  
```  

### <a name="computers-with-a-specific-netbios-name"></a>Computadores com um nome NetBIOS específico

Use a consulta a seguir para retornar o nome NetBIOS de todos os computadores que começam com uma cadeia de caracteres específica. Neste exemplo, a consulta retorna todos os computadores com um nome NetBIOS que começa com `ABC`.  

```  
select SMS_R_System.NetbiosName from    
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="BKMK_DeviceType"></a> Dispositivos de um tipo específico

Os tipos de dispositivo são armazenados no banco de dados do Configuration Manager, na classe de recurso **sms_r_system** e no nome do atributo **AgentEdition**. Use a seguinte consulta para recuperar apenas os dispositivos que correspondem à edição de agente do tipo de dispositivo especificado:  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

Use um dos seguintes valores para *&lt;ID do Dispositivo\>*:  

|Tipo de dispositivo|Valor de AgentEdition|  
|-----------------|---------------------------|  
|Computador desktop ou laptop com o Windows|0|  
|Dispositivo baseado em ARM do Windows (executando o Windows RT)|1|  
|Windows Mobile 6.5|2|  
|Nokia Symbian|3|  
|Windows Phone|4|  
|Computadores Mac|5|  
|Windows CE|6|  
|Windows Embedded|7|  
|iOS|8|  
|iPad|9|  
|iPod Touch|10|  
|Android|11|  
|Sistema em um chip da Intel|12|  
|Servidores Unix e Linux|13|  
|Apple macOS (MDM)|14|
|Microsoft HoloLens (MDM)|15|
|Microsoft Surface Hub (MDM)|16|
|Android for Work|17|

 Por exemplo, se você quiser que a consulta retorne somente computadores Mac, use a seguinte consulta:  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## <a name="see-also"></a>Consulte também  
 [Operações e manutenção de consultas no System Center Configuration Manager](../../../core/servers/manage/operations-and-maintenance-for-queries.md)
