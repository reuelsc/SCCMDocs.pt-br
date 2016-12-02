---
itle: 'Upgrade clients | Microsoft Docs | Linux UNIX '
description: Atualize um cliente em um servidor Linux ou UNIX no System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d2bb377-1005-4a55-bd1f-b80a6d0b22e1
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: eea9faaac579ecafd67eaac05dc7ee7ca7819db7


---
# <a name="how-to-upgrade-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>Como atualizar clientes de servidor Linux e UNIX no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode atualizar a versão do cliente para Linux e UNIX em um computador para uma versão mais recente do cliente sem precisar desinstalar o cliente atual antes. Para fazer isso, instale pacote de instalação do novo cliente no computador usando a propriedade de linha de comando **-keepdb** . Quando é instalado, o cliente para Linux e UNIX substitui os dados do cliente existente pelos arquivos do novo cliente. No entanto, a propriedade de linha de comando **–keepdb** instrui o processo de instalação a manter o GUID (identificador exclusivo), banco de dados local de informações e o repositório de certificados do cliente. Essas informações são usadas pela instalação do novo cliente.  

 Por exemplo, você tem um RHEL5 x64 computador que executa o cliente a partir da versão original do cliente do Gerenciador de Configurações para Linux e UNIX. Para atualizar esse cliente para a versão do cliente da atualização cumulativa 1, execute manualmente o script **install** para instalar o pacote do cliente aplicável da atualização cumulativa 1 com o acréscimo da opção de linha de comando **–keepdb**. A linha de comando usada se parece com a seguinte: **./install -mp <nome do host\> -sitecode <código\> -keepdb ccm-Universal-x64.<build\>.tar**  

## <a name="how-to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Como usar uma implantação de software para atualizar o cliente em servidores Linux e UNIX  
 Você pode usar uma implantação de software para atualizar o cliente para Linux e UNIX para uma nova versão de cliente No entanto, o cliente do System Center Configuration Manager não pode executar diretamente o script de instalação para instalar o novo cliente porque a instalação de um novo cliente precisa, primeiro, desinstalar o cliente atual. Isso terminaria o processo do cliente Configuration Manager que executa o script de instalação antes do início da instalação do novo cliente. Para usar uma implantação de software para instalar o novo cliente com sucesso, você deve agendar a instalação para ser iniciada no futuro e para ser executada pelos recursos internos de agendamento do sistema operacional.  

 Para fazer isso, use uma implantação de software para, primeiro, copiar os arquivos do novo pacote de instalação do cliente para o computador cliente e, em seguida, implantar e executar um script para agendar o processo de instalação do cliente. O script usa o comando **at** interno do sistema operacional para atrasar o início. Em seguida, quando o script é executado, sua operação é gerenciada pelo sistema operacional cliente e não pelo cliente do Configuration Manager no computador. Isso permite que a linha de comando chamada pelo script primeiro desinstale o cliente do Configuration Manager e depois instale o novo cliente, concluindo o processo de atualização do cliente no computador Linux ou UNIX. Após a conclusão da atualização, o cliente atualizado permanece sendo gerenciado pelo Configuration Manager.  

 Use o procedimento a seguir para ajudá-lo a configurar uma implantação de software para atualizar o cliente para Linux e UNIX. As etapas e os exemplos a seguir atualizam um computador RHEL5 x64 que executa a versão inicial do cliente para a versão do cliente da atualização cumulativa 1.  

#### <a name="to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Para usar uma implantação de software para atualizar o cliente em servidores Linux e UNIX  

1.  Copie o arquivo do pacote de instalação do novo cliente para o computador que executa o cliente do Configuration Manager que você planeja atualizar.  

     Por exemplo, você pode colocar o pacote de instalação do cliente e o script de instalação da atualização cumulativa 1 no seguinte local no computador cliente: **/tmp/PATCH**  

2.  Crie um script para gerenciar a atualização do cliente do Configuration Manager e, em seguida, coloque uma cópia do script na mesma pasta do computador cliente em que estiverem os arquivos de instalação do cliente da etapa 1.  

     O script não requer um nome específico, mas deve conter linhas de comando suficientes para usar os arquivos de instalação do cliente de uma pasta local no computador cliente e para instalar o pacote de instalação do cliente usando a propriedade de linha de comando **-keepdb**. Use a propriedade de linha de comando **– keepdb** para manter o identificador exclusivo do cliente atual para que ele seja usado pelo novo cliente que você está instalando.  

     Por exemplo, você pode criar um script chamado **upgrade.sh** que contém as linhas a seguir e, em seguida, copiá-lo para a pasta **/tmp/PATCH** no computador cliente:  

    ```  
    #!/bin/sh  
    #  
    /tmp/PATCH/install -sitecode <code> -mp <hostname> -keepdb /tmp/PATCH/ccm-Universal-x64.<build>.tar  

    ```  

3.  Use a implantação de software para fazer com que cada cliente use o comando interno **at** do computador para executar o script **upgrade.sh** com um pequeno atraso antes da execução do script.  

     Por exemplo, use a seguinte linha de comando para executar o script: **at –f /tmp/upgrade.sh –m now + 5 minutes**  

 Após o cliente agendar com êxito a execução do script **upgrade.sh** , o cliente envia uma mensagem de status indicando que a implantação do software foi concluída com êxito. No entanto, a instalação do cliente real é gerenciada pelo computador após o atraso. Após a conclusão da atualização do cliente, valide a instalação examinando o arquivo **/var/opt/microsoft/scxcm.log** no computador cliente. Além disso, é possível confirmar se o cliente está instalado e se comunicando com o site exibindo detalhes do cliente no nó **Dispositivos** do espaço de trabalho **Ativos e Conformidade** do console do Configuration Manager.  



<!--HONumber=Nov16_HO4-->


