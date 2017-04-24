---
title: Manter os clientes Mac | Microsoft Docs
description: "Tarefas de manutenção para os clientes Mac do Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: aaroncz
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cf6337a2-700c-47f3-b6f8-5814f9b81e59
caps.latest.revision: 12
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c74b553ab76a2b77b0d893151351132da05a640d
ms.openlocfilehash: 5b75f3296dc20a6766a894f463e958455ca1d65f
ms.lasthandoff: 01/04/2017


---

# <a name="maintain-mac-clients"></a>Manter os clientes Mac
*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Veja os procedimentos para desinstalar os clientes Mac e para renovar os certificados deles.

##  <a name="uninstalling-the-mac-client"></a>Desinstalando o cliente Mac  

1.  Em um computador Mac, abra uma janela do terminal e navegue até a pasta que contém **macclient.dmg**.  

2.  Navegue até a pasta Ferramentas e digite a seguinte linha de comando:  

     **./CMUninstall -c**  

    > [!NOTE]  
    >  A propriedade **-c** instrui a desinstalação do cliente a também remover os logs de falha do cliente e os arquivos de log. Recomendamos isso para evitar confusão caso deseje reinstalar o cliente mais tarde.  

3.  Se necessário, remova manualmente o certificado de autenticação de cliente que o Configuration Manager estava usando ou revogue-o. CMUnistall não remove nem revoga esse certificado.  

##  <a name="renewing-the-mac-client-certificate"></a>Renovando o certificado do cliente Mac  
 Use um dos seguintes métodos para renovar o certificado de cliente Mac:  

-   [Assistente de renovação de certificado](#renew-certificate-wizard)  

-   [Renovar o certificado manualmente](#renew-certificate-manually)  

###  <a name="renew-certificate-wizard"></a>Assistente de renovação de certificado  

1.  Configure os seguintes valores como *cadeias de caracteres* no arquivo ccmclient.plist que controla quando o Assistente de renovação de certificado é aberto:  

 -   **RenewalPeriod1** – especifica, em segundos, o primeiro período de renovação em que os usuários podem renovar o certificado. O valor padrão é 3.888.000 segundos (45 dias). Não configure nenhum valor menor que 300, uma vez que o período será revertido ao padrão. 

 -   **RenewalPeriod2** – especifica, em segundos, o segundo período de renovação em que os usuários podem renovar o certificado. O valor padrão é 259.200 segundos (3 dias). Se esse valor estiver configurado e for maior ou igual a 300 segundos e menor ou igual a **RenewalPeriod1**, o valor será usado. Se **RenewalPeriod1** for maior que 3 dias, um valor de 3 dias será usado para **RenewalPeriod2**.  Se **RenewalPeriod1** for menor que 3 dias, **RenewalPeriod2** será definido como o mesmo valor de **RenewalPeriod1**.  

 -   **RenewalReminderInterval1** – especifica, em segundos, a frequência em que o Assistente de Renovação de Certificado será exibido para os usuários durante o primeiro período de renovação. O valor padrão é 86.400 segundos (1 dia). Se **RenewalReminderInterval1** for maior que 300 segundos e menor que o valor configurado para **RenewalPeriod1**, então será usado o valor configurado. Caso contrário, será usado o valor padrão de 1 dia.  

 -   **RenewalReminderInterval2** – especifica, em segundos, a frequência em que o Assistente de Renovação de Certificado será exibido para os usuários durante o segundo período de renovação. O valor padrão é de 28.800 segundos (8 dias). Se **RenewalReminderInterval2** for maior que 300 segundos, menor ou igual a **RenewalReminderInterval1** e menor ou igual a **RenewalPeriod2**, o valor configurado será usado. Caso contrário, será usado um valor de 8 horas.  

     **Exemplo:** se os valores forem deixados como seus padrões, 45 dias antes do vencimento do certificado, o assistente será aberto a cada 24 horas.  No prazo de até 3 dias do vencimento do certificado, o assistente será aberto a cada 8 horas.  

     **Exemplo:** use a seguinte linha de comando, ou um script, para definir o primeiro período de renovação para 20 dias.  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2.  Quando o Assistente de renovação de certificado é aberto, os campos **Nome de usuário** e **Nome do servidor** são, normalmente, populados previamente e o usuário só precisa inserir a senha para renovar o certificado.  

    > [!NOTE]  
    >  Se o assistente não abrir, ou se você o fechar acidentalmente, clique em **Renovar** na página de preferências do **Configuration Manager** para abri-lo.  

###  <a name="renew-certificate-manually"></a>Renovar o certificado manualmente  
 Um período de validade típico para o certificado do cliente Mac é de 1 ano. O Configuration Manager não renova automaticamente o certificado do usuário solicitado durante o registro, por isso você precisa usar o procedimento a seguir para renovar o certificado manualmente.  

> [!IMPORTANT]  
>  Se o certificado expirar, você deverá desinstalar, reinstalar e registrar novamente o cliente Mac.  

 Este procedimento remove o SMSID, que é necessário para solicitar um novo certificado para o mesmo computador Mac. Quando você remove e substitui o SMSID do cliente, todo o histórico armazenado do cliente, como o inventário, é excluído depois que você excluir o cliente do console do Configuration Manager.  

1.  Crie e popule uma coleção de dispositivos para os computadores Mac que devem renovar os certificados de usuário.  

    > [!WARNING]  
    >  O Configuration Manager não monitora o período de validade do certificado registrado para computadores Mac. É necessário monitorá-lo independentemente do Configuration Manager para identificar os computadores Mac a serem adicionados a essa coleção.  

2.  No espaço de trabalho **Ativos e Conformidade** , inicie o **Assistente de Criação de Item de Configuração**.  

3.  Na página **Geral** , especifique as seguintes informações:  

    -   **Nome:remover SMSID para Mac**  

    -   **Tipo:Mac OS X**  

4.  Na página **Plataformas com Suporte**, verifique se todas as versões do Mac OS X estão selecionadas.  

5.  Na página **Configurações**, escolha **Novo** e, na caixa de diálogo **Criar Configuração**, especifique as seguintes informações:  

    -   **Nome:remover SMSID para Mac**  

    -   **Tipo de configuração:script**  

    -   **Tipo de dados:cadeia de caracteres**  

6.  Na caixa de diálogo **Criar Configuração**, para **Script de descoberta**, escolha **Adicionar script** para especificar um script que descobre computadores Mac com um SMSID configurado.  

7.  Na caixa de diálogo **Editar Script de Descoberta** , insira o seguinte Script de Shell:  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Escolha **OK** para fechar a caixa de diálogo **Editar Script de Descoberta**.  

9. Na caixa de diálogo **Criar Configuração**, para **Script de correção (opcional)**, escolha **Adicionar script** para especificar um script que remove o SMSID quando ele é encontrado em computadores Mac.  

10. Na caixa de diálogo **Criar Script de Correção** , insira o seguinte Script de Shell:  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Escolha **OK** para fechar a caixa de diálogo **Criar Script de Correção**.  

12. Na página do assistente **Regras de Conformidade** , clique em **Novo**e na caixa de diálogo **Criar Regra** , especifique as seguintes informações:  

    -   **Nome:remover SMSID para Mac**  

    -   **Configuração selecionada:** escolha **Procurar** e selecione o script de descoberta especificado anteriormente.  

    -   Em **os seguintes valores** digite **O par domínio/padrão (com.microsoft.ccmclient, SMSID) não existe**.  

    -   Habilite a opção **Executar o script de correção especificado quando esta configuração não for compatível**.  

13. Conclua o Assistente de Criação de Item de Configuração.  

14. Crie uma linha de base de configuração que contenha o item de configuração que você acabou de criar e implante-a na coleção de dispositivos criada na etapa 1.  

     Para obter mais informações sobre como criar e implantar linhas de base de configuração, consulte [Como criar linhas de base de configuração no System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md) e [Como implantar linhas de base de configuração no System Center Configuration Manager](../../../compliance/deploy-use/deploy-configuration-baselines.md).  

15. Em computadores Mac com o SMSID removido, execute o seguinte comando para instalar um novo certificado:  

    ```  
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     Quando solicitado, digite a senha da conta do superusuário para executar o comando e a senha da conta de usuário do Active Directory.  

16. Para limitar o certificado registrado ao Configuration Manager, no computador Mac, abra uma janela do terminal e faça as seguintes alterações:  

    a.  Digite o comando **sudo /Aplicativos/Utilitários/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  No diálogo **Acesso ao Conjunto de Chaves**, na seção **Conjuntos de Chaves**, escolha **Sistema** e, na seção **Categoria**, escolha **Chaves**.  

    c.  Expanda as chaves para exibir os certificados do cliente. Quando você tiver identificado o certificado com uma chave privada recém-instalada, clique duas vezes na chave.  

    d.  Na guia **Controle de Acesso**, escolha **Confirmar antes de permitir acesso**.  

    e.  Navegue até **/Library/Application Support/Microsoft/CCM**, selecione **CCMClient** e escolha **Adicionar**.  

    f.  Escolha **Salvar Alterações** e feche a caixa de diálogo **Acesso ao Conjunto de Chaves**.  

17. Reinicie o computador Mac.  


