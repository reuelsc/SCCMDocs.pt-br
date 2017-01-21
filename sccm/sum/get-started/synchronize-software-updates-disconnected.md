---

title: "Sincronizar atualizações de software de um ponto de atualização de software desconectado | Microsoft Docs"
description: "Siga estes procedimentos para verificar se a sincronização de atualizações de software foi bem-sucedida no servidor de exportação, exportar atualizações e importar metadados de atualizações."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 1a997c30-8e71-4be5-89ee-41efb2c8d199
translationtype: Human Translation
ms.sourcegitcommit: e6cf8c799b5be2f7dbb6fadadddf702ec974ae45
ms.openlocfilehash: 73a54ddb896bfa7fb770e02d188a262230762c7f



---

# <a name="synchronize-software-updates-from-a-disconnected-software-update-point"></a>Sincronizar atualizações de software por meio de um ponto de atualização de software desconectado  

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 Quando o ponto de atualização de software no site de nível superior está desconectado da Internet, você deve usar as funções de exportar e importar da ferramenta WSUSUtil para sincronizar os metadados de atualizações de software. É possível escolher um servidor WSUS existente que não está em sua hierarquia do Configuration Manager como a origem de sincronização. Este tópico fornece informações sobre como usar as funções de exportar e importar da ferramenta WSUSUtil.  

 Para exportar e importar metadados de atualizações de software, você deve exportar os metadados de atualizações de software do banco de dados do WSUS em um servidor de exportação especificado, copiar os arquivos de termos de licença armazenados localmente para o ponto de atualização de software desconectado e importar os metadados de atualizações de software no banco de dados do WSUS no ponto de atualização de software desconectado.  

 Use a tabela a seguir para identificar o servidor de exportação para o qual os metadados de atualizações de software devem ser exportados.  

|Ponto de atualização de software|Origem da atualização upstream para pontos de atualização de software conectados|Servidor de exportação para um ponto de atualização de software desconectado|  
|---------------------------|-----------------------------------------------------------------|------------------------------------------------------------|  
|Site de administração central|Microsoft Update (Internet)<br /><br /> Servidor do WSUS existente|Escolha um servidor do WSUS que está sincronizado com o Microsoft Update usando as classificações, os produtos e os idiomas da atualização de software que você necessita em seu ambiente do Configuration Manager.|  
|Site primário autônomo|Microsoft Update (Internet)<br /><br /> Servidor do WSUS existente|Escolha um servidor do WSUS que está sincronizado com o Microsoft Update usando as classificações, os produtos e os idiomas da atualização de software que você necessita em seu ambiente do Configuration Manager.|  

 Para poder iniciar o processo de exportação, verifique se a sincronização de atualizações de software está concluída no servidor de exportação selecionado para garantir que os metadados de atualizações de software mais recentes sejam sincronizados. Para verificar se a sincronização de atualizações de software foi concluída com êxito, use o procedimento a seguir.  

#### <a name="to-verify-that-software-updates-synchronization-has-completed-successfully-on-the-export-server"></a>Para verificar se a sincronização de atualizações de software foi concluída com êxito no servidor de exportação  

1.  Abra o console de Administração do WSUS e conecte-se ao banco de dados do WSUS no servidor de exportação.  

2.  No console de Administração do WSUS, clique em **Sincronizações**. Uma lista de tentativas de sincronização de atualizações de software são exibidas no painel de resultados.  

3.  No painel de resultados, encontre a tentativa mais recente de sincronização de atualizações de software e verifique se ela foi concluída com êxito.  

> [!IMPORTANT]  
>  A ferramenta WSUSUtil deve ser executada localmente no servidor de exportação para exportar os metadados de atualizações de software e deve ser também executada no servidor do ponto de atualização de software desconectado para importar os metadados de atualizações de software. Além disso, o usuário que executa a ferramenta WSUSUtil deve ser um membro do grupo local de administradores em cada servidor.  

## <a name="export-process-for-software-updates"></a>Processo de exportação para atualizações de software  
 O processo de exportação para atualizações de software consiste em duas etapas principais: copiar os arquivos de termos de licença armazenados localmente para o ponto de atualização de software desconectado e exportar os metadados de atualizações de software do banco de dados do WSUS no servidor de exportação.  

 Use o procedimento a seguir para copiar os metadados de termos de licença locais para o ponto de atualização de software desconectado.  

#### <a name="to-copy-local-files-from-the-export-server-to-the-disconnected-software-update-point-server"></a>Para copiar arquivos locais do servidor de exportação para o servidor de ponto de atualização de software desconectado  

1.  No servidor de exportação, navegue até a pasta onde as atualizações de software e os termos de licença para as atualizações de software estão armazenados. Por padrão, o servidor do WSUS armazena os arquivos em <*WSUSInstallationDrive*>\WSUS\WSUSContent\\, em que *WSUSInstallationDrive* é a unidade em que o WSUS está instalado.  

2.  Copie todos os arquivos e pastas desse local na pasta WSUSContent no servidor de ponto de atualização de software desconectado.  

 Use o procedimento a seguir para exportar os metadados de atualizações de software do banco de dados do WSUS no servidor de exportação.  

#### <a name="to-export-software-updates-metadata-from-the-wsus-database-on-the-export-server"></a>Para exportar os metadados de atualizações de software do banco de dados do WSUS no servidor de exportação  

1.  No prompt de comando do servidor de exportação, navegue até a pasta que contém WSUSutil.exe. Por padrão, a ferramenta está localizada em %*ProgramFiles*%\Update Services\Tools. Por exemplo, se a ferramenta estiver localizada no local padrão, digite **cd %ProgramFiles%\Update Services\Tools**.  

2.  Digite o seguinte para exportar os metadados de atualizações de software para um arquivo de pacote:  

     **wsusutil.exe export**  *packagename*  *logfile*  

     Por exemplo:  

     **wsusutil.exe export export.cab export.log**  

     O formato pode ser resumido da seguinte maneira: o WSUSutil.exe é seguido da opção de exportação, do nome do arquivo .cab de exportação que é criado durante a operação de exportação e do nome de um arquivo de log. O WSUSutil.exe exporta os metadados do servidor de exportação e cria um arquivo de log da operação.  

    > [!NOTE]  
    >  O pacote (arquivo. cab) e o nome do arquivo de log devem ser exclusivos na pasta atual.  

3.  Transfira o pacote de exportação para a pasta que contém o WSUSutil.exe no servidor do WSUS de importação.  

    > [!NOTE]  
    >  Se você transferir o pacote para essa pasta, a experiência de importação poderá ser mais fácil. Você pode transferir o pacote para qualquer local que seja acessível para o servidor de importação e especifique o local ao executar o WSUSutil.exe.  

## <a name="import-software-updates-metadata"></a>Importar metadados de atualizações de software  
 Use o procedimento a seguir para importar os metadados de atualizações de software do servidor de exportação para o ponto de atualização de software desconectado.  

> [!IMPORTANT]  
>  Nunca importe dados exportados de uma fonte não confiável. Se você importa o conteúdo de uma fonte não confiável, isso pode comprometer a segurança de seu servidor do WSUS.  

#### <a name="to-import-metadata-to-the-database-of-the-import-server"></a>Para importar metadados para o banco de dados do servidor de importação  

1.  No prompt de comando do servidor do WSUS de importação, navegue até a pasta que contém WSUSutil.exe. Por padrão, a ferramenta está localizada em %*ProgramFiles*%\Update Services\Tools.  

2.  Digite o seguinte:  

     **wsusutil.exe import**  *packagename*  *logfile*  

     Por exemplo:  

     **wsusutil.exe import export.cab import.log**  

     O formato pode ser resumido da seguinte maneira: o WSUSutil.exe é seguido do comando de importação, do nome do arquivo de pacote (.cab) criado durante a operação de exportação, do caminho do arquivo de pacote, caso ele esteja em uma pasta diferente, e do nome de um arquivo de log. O WSUSutil.exe importa os metadados do servidor de exportação e cria um arquivo de log da operação.  

## <a name="next-steps"></a>Próximas etapas
Depois de sincronizar as atualizações de software pela primeira vez ou depois que houver novas classificações ou produtos disponíveis, você deverá [configurar as novas classificações e produtos](configure-classifications-and-products.md) para sincronizar atualizações de software com os novos critérios.

Depois de sincronizar as atualizações de software com os critérios de que você precisa, [gerencie as configurações de atualizações de software](manage-settings-for-software-updates.md).  



<!--HONumber=Dec16_HO3-->


