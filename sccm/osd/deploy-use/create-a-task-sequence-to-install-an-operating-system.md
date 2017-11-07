---
title: "Criar uma sequência de tarefas para instalar um sistema operacional"
titleSuffix: Configuration Manager
description: "Use sequências de tarefas no System Center Configuration Manager para instalar automaticamente uma imagem do sistema operacional e outros tipos de conteúdo em um computador de destino."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 217c8a0e-5112-420e-a325-2a6d75326290
caps.latest.revision: "13"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 47210939c66bb31d173c7e406a66c764d5008879
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="create-a-task-sequence-to-install-an-operating-system-in-system-center-configuration-manager"></a>Criar uma sequência de tarefas para instalar um sistema operacional no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use sequências de tarefas no System Center Configuration Manager para instalar automaticamente uma imagem do sistema operacional em um computador de destino. Você cria uma sequência de tarefas que faz referência a uma imagem de inicialização usada para iniciar o computador de destino, a imagem do sistema operacional que deseja instalar no computador de destino e qualquer outro conteúdo adicional, como outros aplicativos ou atualizações de software, que deseja instalar. Em seguida, você implanta a sequência de tarefas em uma coleção que contém o computador de destino.  

##  <a name="BKMK_InstallOS"></a> Criar uma sequência de tarefas para instalar um sistema operacional  
 Há muitos cenários para implantar um sistema operacional em computadores em seu ambiente. Na maioria dos casos, você vai criar uma sequência de tarefas e selecionar **instalar um pacote de imagem existente** no assistente Criar Sequência de Tarefas para instalar o sistema operacional, migrar as configurações do usuário, aplicar atualizações de software e instalar aplicativos. Antes de criar uma sequência de tarefas para instalar um sistema operacional, o seguinte deve estar disponível:   

-   **Necessária**  

    -   A [imagem de inicialização](../get-started/manage-boot-images.md) deve estar disponível no console do Configuration Manager.  

    -   Uma [imagem do sistema operacional](../get-started/manage-operating-system-images.md) deve estar disponível no console do Configuration Manager.  

-   **Necessário (se usado)**  

    -   As [atualizações de software](../../sum/get-started/synchronize-software-updates.md) devem estar sincronizadas no console do Configuration Manager.  

    -   Os [aplicativos](../../apps/deploy-use/create-applications.md) devem ser adicionados ao console do Configuration Manager.  

#### <a name="to-create-a-task-sequence-that-installs-an-operating-system"></a>Para criar uma sequência de tarefas que instala um sistema operacional  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Sequências de Tarefas**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Sequência de Tarefas** para iniciar o Assistente para Criar Sequência de Tarefas.  

4.  Na página **Criar uma nova sequência de tarefas** , clique em **Instalar um pacote de imagem existente**e em **Próximo**.  

5.  Na página **Informações da Sequência de Tarefas** , especifique as seguintes configurações e clique em **Próximo**.  

    -   **Nome da sequência de tarefas**: especifique um nome que identifique a sequência de tarefas.  

    -   **Descrição**: especifique uma descrição da tarefa executada pela sequência de tarefas.  

    -   **Imagem de inicialização**: especifique a imagem de inicialização que instala o sistema operacional no computador de destino. A imagem de inicialização contém uma versão do Windows PE que é usada para instalar o sistema operacional, assim como quaisquer drivers de dispositivos adicionais necessários. Para obter informações, consulte [Gerenciar imagens de inicialização](../get-started/manage-boot-images.md).  

        > [!IMPORTANT]  
        >  A arquitetura da imagem de inicialização deve ser compatível com a arquitetura de hardware do computador de destino.  

6.  Na página **Instalar Windows** , especifique as seguintes configurações e clique em **Próximo**.  

    -   **Pacote da imagem**: especifique o pacote que contém a imagem do sistema operacional para instalação. Para obter mais informações, consulte [Gerenciar imagens do sistema operacional](../get-started/manage-operating-system-images.md).  

    -   **Imagem**: se o pacote de imagens do sistema operacional contém várias imagens, especifique o índice da imagem do sistema operacional para instalação.  

    -   **Particionar e formatar o computador de destino instalando o sistema operacional**: especifique se você deseja que a sequência de tarefas particione e formate o computador de destino antes da instalação do sistema operacional.  

    -   **Chave do produto**: especifique a chave do produto do sistema operacional Windows a instalar. Você pode especificar as chaves de licença de volume codificadas e as chaves do produto padrão. Se você usar uma chave de produto sem codificação, cada grupo de 5 caracteres deverá ser separado por um traço (-). Por exemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    -   **Modo de licenciamento do servidor**: especifique se a licença do servidor é **Por estação**, **Por servidor**ou se nenhuma licença está especificada. Se a licença do servidor for **Por servidor**, especifique também o número máximo de conexões de servidor.  

    -   Especifique como lidar com a conta de administrador usada quando a imagem de sistema operacional é implantada.  

        -   **Desabilitar a conta de administrador local**: especifique se a conta de administrador local deve ser desabilitada quando a imagem de sistema operacional for implantada.  

        -   **Sempre usar a mesma senha de administrador**: especifique se a mesma senha deve ser usada para a conta do administrador local em todos os computadores nos quais a imagem do sistema operacional será implantada.  

7.  Na página **Configurar a Rede** , especifique as seguintes configurações e clique em **Próximo**.  

    -   **Ingressar no grupo de trabalho**: especifique se deseja adicionar o computador de destino a um grupo de trabalho.  

    -   **Ingressar em um domínio**: especifique se deseja adicionar o computador de destino a um domínio. Em **Domínio**, especifique o nome do domínio.  

        > [!IMPORTANT]  
        >  Você pode localizar os domínios na floresta local, mas, para tanto, é necessário especificar o nome de domínio para uma floresta remota.  

         Você também pode especificar uma UO (unidade organizacional). Essa configuração opcional especifica o nome diferenciado do LDAP X.500 da UO na qual a conta do computador será criada, se ela ainda não existir.  

    -   **Conta**: especifique o nome de usuário e senha para a conta que tenha permissões para ingressar no domínio especificado. Por exemplo: *domain\user* ou *%variable%*.  

        > [!IMPORTANT]  
        >  Você deve inserir as credenciais de domínio adequadas se planeja migrar as configurações de domínio ou as configurações do grupo de trabalho.  

8.  Na página **Instalar o Configuration Manager**, especifique o pacote do cliente do Configuration Manager para instalar no computador de destino e clique em **Próximo**.  

9. Na página **Migração de Estado** , especifique as seguintes informações e clique em **Próximo**.  

    -   **Capturar configurações do usuário**: especifique se a sequência de tarefas deve capturar o estado do usuário. Para obter mais informações sobre como capturar e restaurar o estado do usuário, consulte [Gerenciar o estado do usuário](../get-started/manage-user-state.md).  

    -   **Capturar configurações da rede**: especifique se a sequência de tarefas deve capturar as configurações da rede do computador de destino. Você pode capturar a associação do domínio ou grupo de trabalho além das configurações de adaptador de rede.  

    -   **Capturar configurações do Microsoft Windows**:  especifique se a sequência de tarefas deve capturar as configurações do Windows do computador de destino antes de instalar a imagem do sistema operacional. Você pode capturar o nome do computador, nome de usuário e organização registrados e as configurações de fuso horário.  

10. Na página **Incluir Atualizações** , especifique se deseja instalar as atualizações de software necessárias, todas as atualizações ou nenhuma e clique em **Próximo**. Se optar pela instalação das atualizações de software, o Configuration Manager instalará somente aquelas que fizerem parte das coleções das quais o computador de destino é membro.  

11. Na página **Instalar Aplicativos** , especifique os aplicativos a instalar no computador de destino e clique em **Próximo**. Se você especificar vários aplicativos, será possível também definir a continuação da sequência de tarefas em caso de falha na instalação de algum aplicativo.  

12. Conclua o assistente.  

 Agora é possível implantar a sequência de tarefas em uma coleção de computadores.  Para obter mais informações, consulte [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

##  <a name="BKMK_InstallExistingOSImageTSExample"></a> Exemplo de sequência de tarefas para instalar uma imagem do sistema operacional existente  
 Use a tabela a seguir como guia ao criar uma sequência de tarefas que implanta um sistema operacional usando uma imagem do sistema operacional existente. A tabela ajudarão você a decidir a seqüência geral de etapas da sequência de tarefas e como organizar e estruturar as etapas da sequência de tarefas em grupos lógicos. A sequência de tarefas que você criar este exemplo pode variar e pode conter mais ou menos grupos e etapas de sequência de tarefas.  

> [!IMPORTANT]  
>  Você sempre deve usar o Assistente para criar sequência de tarefas para criar essa sequência de tarefas.  

 Quando você usar o Assistente para criar sequência de tarefas para criar essa nova sequência de tarefas, alguns dos nomes de etapa de sequência de tarefas são diferentes do que de que eles seriam se você adicionou manualmente essas etapas de sequência de tarefas para uma sequência de tarefas existente. A tabela a seguir exibe as diferenças de nomenclatura:  

|Criar o nome da etapa de sequência de tarefas do Assistente de sequência de tarefas|Nome da etapa equivalente Editor de sequência de tarefas|  
|---------------------------------------------------------|-----------------------------------------------|  
|Armazenamento de estado do usuário de solicitação|Solicitar Armazenamento de Estado|  
|Capturar configurações e arquivos do usuário|Capturar Estado do Usuário|  
|Armazenamento de estado do usuário de versão|Liberar Armazenamento de Estado|  
|Reiniciar no Windows PE|Reinicialize no Windows PE ou o disco rígido|  
|Particionar Disco 0|Formatar e Particionar Disco|  
|Restaurar configurações e arquivos do usuário|Restaurar Estado do Usuário|  

|Grupo de sequências de tarefas ou etapa|Descrição|  
|---------------------------------|-----------------|  
|Captura de arquivos e configurações - **(novo grupo de sequências de tarefas)**|Crie um grupo de sequências de tarefas. Um grupo de sequências de tarefas mantém etapas da sequência de tarefas semelhantes juntas para melhor organização e controle de erro.<br /><br /> Esse grupo contém as etapas necessárias para capturar os arquivos e configurações do sistema operacional de um computador de referência.|  
|Capturar Configurações do Windows|Use essa etapa de sequência de tarefas para identificar as configurações do Microsoft Windows para capturar do computador de referência. Você pode capturar o nome do computador, usuário e informações organizacionais e as configurações de fuso horário.|  
|Capturar configurações da rede|Use essa etapa de sequência de tarefas para capturar as configurações de rede do computador de referência. Você pode capturar a associação de domínio ou grupo de trabalho do computador de referência e obter informações sobre configuração de adaptador de rede.|  
|Capturar arquivos de usuário e configurações - **(nova tarefa sequência subgrupo)**|Crie um grupo de sequências de tarefas dentro de um grupo de sequências de tarefas. Esse subgrupo contém as etapas necessárias para capturar dados de estado do usuário. Semelhante para o grupo inicial que você adicionou, esse subgrupo mantém controlam semelhante etapas da sequência de tarefas para o erro e melhor organização.|  
|Armazenamento de estado do usuário de solicitação|Use essa etapa de sequência de tarefas para solicitar acesso a um ponto de migração de estado onde os dados de estado do usuário são armazenados. Você pode configurar essa etapa de sequência de tarefas para capturar ou restaurar as informações de estado do usuário.|  
|Capturar Arquivos e Configurações do Usuário|Use essa etapa de sequência de tarefas para usar o User State Migration Tool (USMT) para capturar o estado do usuário e configurações do computador de referência que receberão a sequência de tarefas associada a essa etapa da tarefa. Você pode capturar as opções padrão ou configurar opções capturar.|  
|Armazenamento de estado do usuário de versão|Use essa etapa de sequência de tarefas para notificar o estado do ponto de migração que a ação de captura ou restauração foi concluída.|  
|Instalar o sistema operacional - **(novo grupo de sequências de tarefas)**|Crie outro grupo de subpropriedades de sequência de tarefas. Esse subgrupo contém as etapas necessárias para instalar e configurar o ambiente do Windows PE.|  
|Reiniciar no Windows PE|Use essa etapa de sequência de tarefas para especificar as opções de reinicialização do computador de destino que recebe essa sequência de tarefas. Esta etapa exibirá uma mensagem para o usuário indicando que o computador será reiniciado para que a instalação possa continuar.<br /><br /> Esta etapa usa a variável de sequência de tarefas **_SMSTSInWinPE** de somente leitura. Se o valor for igual a **false** continua a etapa de sequência de tarefas.|  
|Particionar disco 0|Esta etapa especifica as ações necessárias para formatar o disco rígido no computador de destino. O número de disco padrão é **0**.<br /><br /> Esta etapa usa a variável de sequência de tarefas **_SMSTSClientCache** de somente leitura. Esta etapa será executada se o cache do cliente do Configuration Manager não existir.|  
|Aplicar Sistema Operacional|Use essa etapa de sequência de tarefas para instalar a imagem do sistema operacional no computador de destino. Essa etapa se aplica a todas as imagens de volume contidas no arquivo WIM para o volume de disco sequencial correspondente no computador de destino após o primeiro excluir todos os arquivos no volume (com exceção de arquivos de controle específicos do Configuration Manager). Você pode especificar um **sysprep** arquivo de resposta e também configurar a partição de disco é usada para a instalação.|  
|Aplicar as Configurações do Windows|Use essa etapa de sequência de tarefas para configurar as informações de configuração de configurações do Windows no computador de destino. Você pode aplicar as configurações do windows são usuários e informações organizacionais, informações de chave de produto ou licença, fuso horário e a senha de administrador local.|  
|Aplicar Configurações de Rede|Use essa etapa de sequência de tarefas para especificar as informações de configuração de rede ou grupo de trabalho do computador de destino. Você também pode especificar se o computador usa um servidor DHCP ou você pode atribuir estaticamente as informações de endereço IP.|  
|Aplicar Drivers de Dispositivo|Use essa etapa de sequência de tarefas para instalar drivers como parte da implantação do sistema operacional. Você pode permitir que a Instalação do Windows pesquise todas as categorias de driver existentes selecionando a opção **Considerar drivers de todas as categorias** ou limitar quais categorias de driver de Instalação do Windows pesquisarão ao selecionar a opção **Limitar a correspondência de driver para considerar somente os drivers em categorias selecionadas**.<br /><br /> Esta etapa usa somente leitura **_SMSTSMediaType** variável de sequência de tarefas. Essa etapa de sequência de tarefas é executado somente se o valor da variável não é igual a **FullMedia**.|  
|Aplicar pacote de driver|Use essa etapa de sequência de tarefas para disponibilizar todos os drivers de dispositivo em um pacote de driver para uso pela instalação do Windows.|  
|Configurar o sistema operacional - **(novo grupo de sequências de tarefas)**|Crie outro grupo de subpropriedades de sequência de tarefas. Esse subgrupo contém as etapas necessárias para configurar o sistema operacional instalado.|  
|Instalar Windows e ConfigMgr|Use essa etapa de sequência de tarefas para instalar o software cliente do Configuration Manager. O Configuration Manager instala e registra o GUID do cliente do Configuration Manager. Você pode atribuir os parâmetros necessários para a instalação na janela **Propriedades de instalação** .|  
|Instalar atualizações|Use esta etapa de sequência de tarefas para especificar como as atualizações de software serão instaladas no computador de destino. O computador de destino não é avaliado para atualizações de software aplicáveis até que essa etapa de sequência de tarefas seja executada. Nesse momento, o computador de destino é avaliado para atualizações de software semelhantes a qualquer outro cliente gerenciado do Configuration Manager.<br /><br /> Esta etapa usa a variável de sequência de tarefas **_SMSTSMediaType** somente leitura. Essa etapa de sequência de tarefas será executada somente se o valor da variável não for igual a **FullMedia**.|  
|Restaurar Arquivos e Configurações do Usuário - **(Novo Subgrupo de Sequência de Tarefas)**|Crie outro grupo de subpropriedades de sequência de tarefas. Esse subgrupo contém as etapas necessárias para restaurar os arquivos de usuário e configurações.|  
|Solicitar Armazenamento de Estado do Usuário|Use essa etapa de sequência de tarefas para solicitar acesso a um ponto de migração de estado onde os dados de estado do usuário são armazenados.|  
|Restaurar Arquivos e Configurações do Usuário|Use essa etapa de sequência de tarefas para iniciar o User State Migration Tool (USMT) para restaurar o estado do usuário e configurações para um computador de destino.|  
|Armazenamento de estado do usuário de versão|Use essa etapa da sequência de tarefas para notificar o ponto de migração de estado que os dados do estado do usuário não são mais necessários.|  
