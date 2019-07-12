---
title: Administrar remotamente o computador Windows
titleSuffix: Configuration Manager
description: Administre um computador cliente Windows remoto usando o System Center Configuration Manager.
ms.date: 04/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3c9648c4-645e-4e47-ae10-2da817b8c83b
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b1a18371a7f75935b3d72262b35385f8f4e81923
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67677665"
---
# <a name="how-to-remotely-administer-a-windows-client-computer-by-using-system-center-configuration-manager"></a>Como administrar remotamente um computador cliente com Windows usando o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch atual)* O Configuration Manager permite que você se conecte aos computadores cliente que usam o **Controle Remoto do Configuration Manager**. Antes de começar a usar o controle remoto, certifique-se de que você revisou as informações nos seguintes artigos:  

-   [Pré-requisitos para o controle remoto no System Center Configuration Manager](../../../../core/clients/manage/remote-control/prerequisites-for-remote-control.md)  

-   [Configurando o controle remoto no System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md)  

Aqui estão três maneiras de iniciar o visualizador de controle remoto:  

-   No console do Configuration Manager.  

-   Em um prompt de comando do Windows.  

-   No menu **Iniciar** do Windows, em um computador que executa o console do Configuration Manager, no grupo de programas do **Microsoft System Center**.  

## <a name="to-remotely-administer-a-client-computer-from-the-configuration-manager-console"></a>Para administrar remotamente um computador cliente no console do Configuration Manager  

1.  No console do Configuration Manager, escolha **Ativos e Conformidade** > **Dispositivos** ou **Coleções de Dispositivos**.  

3.  Selecione o computador que deseja administrar remotamente e, na guia **Início**, no grupo **Dispositivo**, escolha **Iniciar** > **Controle Remoto**.  

    > [!IMPORTANT]  
    >  Se a permissão **Solicitar o controle remoto ao usuário** da configuração do cliente for definida como **True**, a conexão não será iniciada até que o usuário no computador remoto concorde com o prompt de controle remoto. Para mais informações, consulte [Configurar o controle remoto no System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md).  

4.  Depois que a janela **Controle Remoto do Configuration Manager** for aberta, você poderá administrar remotamente o computador cliente. Use as opções a seguir para configurar a conexão.  

    > [!NOTE]  
    >  Se o computador ao qual você se conectar tiver vários monitores, a exibição de todos os monitores será mostrada na janela do controle remoto.  

    -   **File**
        - **Conectar** – Conecta a outro computador. Essa opção não está disponível quando uma sessão de controle remoto está ativa.  
        -   **Desconectar** – Desconecta a sessão ativa de controle remoto, mas não fecha a janela **Controle Remoto do Configuration Manager**.  
        - **Sair** – Desconecta a sessão ativa de controle remoto e fecha a janela **Controle Remoto do Configuration Manager**.  

        > [!NOTE]  
        >  Quando você desconecta uma sessão de controle remoto, o conteúdo da Área de Transferência do Windows no computador que está sendo exibido é excluído.


    - **Exibir**
      - **Profundidade de cor** – Escolha 16 bits ou 32 bits por pixel.
      -  **Tela inteira** – Maximiza a janela do **Controle Remoto do Configuration Manager**. Para sair do modo de tela inteira, pressione Ctrl+Alt+Break.  
      - **Otimizar para conexão de baixa largura de banda** – Escolha esta opção se a conexão for de baixa largura de banda.
      - **Exibição:**
        - **Todas as telas** – Adicionado no Configuration Manager 1902. Se o computador ao qual você se conectar tiver vários monitores, a exibição de todos os monitores será mostrada na janela do controle remoto. **Todas as telas** – É o único modo de exibição para computadores com vários monitores antes de 1902.
        -  **Primeira tela** – Adicionado no Configuration Manager 1902. A *primeira tela* fica na parte extrema esquerda superior, conforme mostrado nas configurações de exibição do Windows. Não é possível selecionar uma tela específica. Quando você alternar a configuração do visualizador, reconecte a sessão remota. O visualizador salvará sua preferência para conexões futuras.
        -  **Dimensionar para Ajustar** – Dimensiona o monitor do computador remoto para se ajustar ao tamanho da janela do **Controle Remoto do Configuration Manager**.
        - **Barra de Status** – Alterna a exibição da barra de status da janela do **Controle Remoto do Configuration Manager**.  

       > [!NOTE]  
       >  O visualizador salvará sua preferência para conexões futuras.

    -   **Ação**
        - **Enviar tecla Ctrl+Alt+Del** – Envia uma combinação de teclas Ctrl+Alt+Del ao computador remoto. 
        - **Habilitar o compartilhamento da área de transferência** – Permite copiar e colar itens no computador remoto. Se você alterar esse valor, será necessário reiniciar a sessão de controle remoto para que a alteração tenha efeito.   
          - Se não desejar que o compartilhamento de área de transferência seja habilitado no console do Configuration Manager, no computador que executa o console, defina o valor da chave do registro **HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\Remote Control\Clipboard Sharing** como **0**.
        - **Habilitar conversão do teclado** – Converte o layout do teclado do computador que executa o console para o layout do dispositivo conectado.
        - **Bloqueio do teclado e mouse remotos** – Bloqueia o teclado e o mouse para impedir que o usuário opere o computador remoto.  

    -   **Ajuda**
        - **Sobre o controle remoto** – Exibe a versão atual do visualizador.  

5.  Os usuários no computador remoto podem exibir mais informações sobre a sessão de controle remoto ao clicar no ícone de **Controle remoto** do Configuration Manager. O ícone está na área de notificação do Windows ou na barra da sessão de controle remoto.  

## <a name="to-start-the-remote-control-viewer-from-the-windows-command-line"></a>Para iniciar o visualizador de controle remoto na linha de comando do Windows  

-   No prompt de comando do Windows, digite _<Pasta de instalação do Configuration Manager\>_ **\AdminConsole\Bin\x64\CmRcViewer.exe**  

O CmRcViewer.exe dá suporte às seguintes opções de linha de comando:  

- *Endereço* – Especifica o nome NetBIOS, o FQDN (nome de domínio totalmente qualificado) ou o endereço IP do computador cliente ao qual você deseja se conectar.
- *Nome do Servidor do Site* – Especifica o nome do servidor do site do System Center Configuration Manager ao qual você deseja enviar mensagens de status relacionadas à sessão de controle remoto.
- **/?** – Exibe as opções de linha de comando para o visualizador de controle remoto.  
     
**Exemplo:CmRcViewer.exe** *<Endereço\>* *<\\\Nome do Servidor do Site>*  
