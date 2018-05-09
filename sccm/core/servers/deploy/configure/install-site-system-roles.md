---
title: Instalar funções do sistema de site
titleSuffix: Configuration Manager
description: Os assistentes ajudam a adicionar funções do sistema de sites a um servidor do sistema de sites novo ou existente no site.
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 61f5c774-7667-44ae-b8e4-a4951318b183
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7edfc72195b289488242adcbd1903dbacf26bfe2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="install-site-system-roles-for-system-center-configuration-manager"></a>Instalar funções do sistema de sites ao System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O console do System Center Configuration Manager tem dois assistentes que você pode usar para instalar funções de sistema de sites:  

-   **Assistente para Adicionar Funções do Sistema de Site**: Use esse assistente para adicionar funções do sistema de site para um servidor do sistema de site existente no site.  

-   **Assistente para Criar Servidor do Sistema de Site**: Use esse assistente para especificar um novo servidor com um servidor do sistema de site e instale uma ou mais funções do sistema de site no servidor. Esse assistente é o mesmo que o **Assistente para Adicionar Funções do Sistema de Site**, exceto que na primeira página, você deve especificar o nome do servidor para usar e o site no qual você deseja instalá-lo.  

Ao instalar a função do sistema de site em um computador remoto (incluindo uma instância do Provedor de SMS), a conta do computador do computador remoto é adicionada ao grupo local no servidor de site. Quando o site é instalado em um controlador de domínio, o grupo no servidor de sites é um grupo de domínio, ao invés de um grupo local. Nesse caso, a função de sistema do site remoto não fica operacional até a reinicialização do computador da função de sistema do site ou até que o tíquete Kerberos para a conta do computador remoto seja atualizado. Para obter mais informações, consulte [Contas usadas no System Center Configuration Manager](../../../../core/plan-design/hierarchy/accounts.md).  

Antes de instalar a função do sistema de sites, o Configuration Manager verifica o computador de destino para garantir que ele atenda aos pré-requisitos para as funções do sistema de sites selecionadas. Compreenda o seguinte sobre a instalação de funções do sistema de site:  

-   Por padrão, quando o Configuration Manager instala uma função do sistema de sites, os arquivos de instalação são instalados na primeira unidade de disco com formatação NTFS disponível que contém o maior espaço livre em disco disponível. Para impedir que o Configuration Manager instale em unidades específicas, crie um arquivo vazio chamado **no_sms_on_drive.sms**. Copie-o para a pasta raiz da unidade antes de instalar o servidor do sistema de sites.  

-   O Configuration Manager usa a **Conta de Instalação do Sistema de Sites** para instalar as funções do sistema de sites. Você determina essa conta ao executar o assistente aplicável para criar um novo servidor de sistema de site ou adicionar funções do sistema de site a um servidor de sistema de site existente. Por padrão, essa conta é a conta do sistema local do computador do servidor do site, mas, você pode especificar uma conta de usuário do domínio para usar como a Conta de Instalação do Sistema de Site. Para obter mais informações, consulte [Contas usadas no System Center Configuration Manager](../../../../core/plan-design/hierarchy/accounts.md).  

##  <a name="bkmk_Install"></a> Para instalar funções do sistema de sites em um servidor do sistema de sites existente  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Configuração de Site**e clique em **Funções de Servidores e Sistema de Site**. Em seguida, selecione o servidor que deseja usar para as novas funções de sistema de site.  

3.  Na guia **Início** , no grupo **Servidor** , clique em **Adicionar Funções do Sistema de Site**.  

4.  Na página **Geral** , examine as configurações e clique em **Próximo**.  

    > [!TIP]  
    >  Para acessar a função do sistema de site da Internet, é necessário especificar um FQDN (nome de domínio totalmente qualificado).  

5.  Na página **Proxy**, especifique as configurações para o servidor proxy, caso as funções do sistema de site executadas precisem de um servidor proxy para se conectarem a locais na Internet. Clique em **Avançar**.  

6.  Na página **Seleção de Função do Sistema** , selecione as funções do sistema de site que deseja adicionar e clique em **Próximo**.  

7.  Conclua o assistente.  

> [!TIP]  
>  O cmdlet do Windows PowerShell, New-CMSiteSystemServer, executa a mesma função que esse procedimento. Para mais informações, consulte [New-CMSiteSystemServer](http://go.microsoft.com/fwlink/p/?LinkID=271414) na documentação de Referência de Cmdlet do System Center 2012 Configuration Manager SP1.  

## <a name="to-install-site-system-roles-on-a-new-site-system-server"></a>Para instalar funções do sistema de site em um novo servidor do sistema de site  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Configuração de Site**e clique em **Funções de Servidores e Sistema de Site**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Servidor do Sistema de Site**.  

4.  Na página **Geral** , especifique as configurações gerais para o sistema de site e clique em **Próximo**.  

    > [!TIP]  
    >  Para acessar a nova função do sistema de site da Internet, é necessário especificar um FQDN de Internet.  

5.  Na página **Proxy**, especifique as configurações para o servidor proxy, caso as funções do sistema de site executadas precisem de um servidor proxy para se conectarem a locais na Internet. Clique em **Avançar**.  

6.  Na página **Seleção de Função do Sistema** , selecione as funções do sistema de site que deseja adicionar e clique em **Próximo**.  

7.  Conclua o assistente.  

> [!TIP]  
>  O cmdlet do Windows PowerShell, New-CMSiteSystemServer, executa a mesma função que esse procedimento. Para mais informações, consulte [New-CMSiteSystemServer](http://go.microsoft.com/fwlink/p/?LinkID=271414) na documentação de Referência de Cmdlet do System Center 2012 Configuration Manager SP1.  
