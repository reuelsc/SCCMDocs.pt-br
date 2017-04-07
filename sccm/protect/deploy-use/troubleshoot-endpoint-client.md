---
title: Solucionando problemas do cliente Windows Defender ou Endpoint Protection | Microsoft Docs
description: Saiba como solucionar problemas com o Windows Defender e o Endpoint Protection.
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d837253e-fcc2-422a-9e2c-c78b938dfd8c
caps.latest.revision: 7
caps.handback.revision: 0
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6accec2d356861b273b25ba2b6338d9684a46ff6
ms.openlocfilehash: 1b096e71f5131214fb4e235e84d0b7f63e566831
ms.lasthandoff: 03/29/2017


---
# <a name="troubleshooting-windows-defender-or-endpoint-protection-client"></a>Solucionando problemas do cliente Windows Defender ou Endpoint Protection

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Se você tiver problemas com o Windows Defender ou Endpoint Protection, entre em contato com o administrador de segurança para obter suporte. Você também pode tentar solucionar os seguintes problemas:  

-   [Atualizar o Windows Defender ou o Endpoint Protection](#update-windows-defender-or-endpoint-protection)  
-   [Iniciar o serviço do Windows Defender ou do Endpoint Protection](#starting-windows-defender-or-endpoint-protection-service)  
-   [Problemas de conexão com a Internet](#internet-connection-issues)  
-   [A ameaça detectada não pode ser corrigida](#detected-threat-cant-be-remediated)  
-   [Instalar o cliente do Endpoint Protection](#install-the-endpoint-protection-client)  

##  <a name="update-windows-defender-or-endpoint-protection"></a>Atualizar o Windows Defender ou o Endpoint Protection  
 O Windows Defender ou Endpoint Protection funciona automaticamente com o Microsoft Update para garantir que suas definições de vírus e spyware estejam atualizadas.  

 **Sintomas**  

 Este artigo aborda problemas comuns com as atualizações automáticas, incluindo as seguintes situações:  

-   Ver mensagens de erro indicando que as atualizações falharam.  

-   Quando você procurar atualizações, você recebe uma mensagem de erro que as atualizações de definições de vírus e spyware não podem ser verificadas, baixadas ou instaladas.  

-   Mesmo que você esteja conectado à Internet, as atualizações falham.  

-   As atualização não são instaladas conforme agendado.  

 **Causa**  

 As causas mais comuns para problemas de atualização são problemas de conectividade com a Internet. No entanto, se você souber que está conectado à internet porque você pode navegar para outros sites da Web, o problema pode ser causado por conflitos com as configurações no Windows Internet Explorer.  

> [!IMPORTANT]  
>  Você precisa sair do Internet Explorer para concluir essas etapas. Portanto, imprimi-as, anote-as, ou copie-as para outro arquivo e, em seguida, marque este tópico para acesso futuro.  

### <a name="step-1-reset-your-internet-explorer-settings"></a>Etapa 1: Redefinir as configurações do Internet Explorer  

1.  Saia de todos os programas abertos, incluindo o Internet Explorer.  

    > [!NOTE]  
    >  Redefina essas configurações no Internet Explorer exclui arquivos temporários, cookies, histórico de navegação e suas senhas online. No entanto, seus favoritos não serão excluídos.  

2.  Clique em **Iniciar** e procure por **inetcpl.cpl**, e depois pressione **Enter**.  

3.  Na caixa de diálogo **Opções da Internet** , clique na guia **Avançado** .  

4.  Nas **configurações Redefinir o Internet Explorer**, clique em **Redefinir**, e, em seguida, clique em **Redefinir** novamente.  

5.  Aguarde até que o Internet Explorer termine de redefinir as configurações e, em seguida, clique em **OK**.  

6.  Abra o Internet Explorer.  

7.  Abra o Microsoft Security Essentials, clique na guia **atualização** e, em seguida, clique em **Atualização**.  

8.  Se o problema persistir, prossiga para a próxima etapa.  

### <a name="step-2-set-internet-explorer-as-the-default-browser"></a>Etapa 2: Configurar o Internet Explorer como navegador padrão  

1.  Saia de todos os programas abertos, incluindo o Internet Explorer.  

2.  Clique em **Iniciar** e procure por **inetcpl.cpl**, e depois pressione **Enter**.  

3.  Na caixa de diálogo **Opções da Internet** , clique na guia **Programas** .  

4.  Em **navegador da Web padrão**, clique em **Tornar padrão**.  

5.  Clique em **OK**.  

6.  Abra o Windows Defender ou o Endpoint Protection. Clique na guia **Atualização** e depois em **Atualizar**.  

7.  Se o problema persistir, prossiga para a próxima etapa.  

### <a name="step-3-ensure-that-the-date-and-time-are-set-correctly-on-your-computer"></a>Etapa 3: Verificar se data e hora estão definidas corretamente no computador  

1.  Abra o Windows Defender ou o Endpoint Protection.  

2.  Se a mensagem de erro que você recebeu contiver o código 0x80072f8f, o problema é provavelmente causado por uma data incorreta ou configuração de tempo em seu computador.  

3.  Para redefinir sua configuração de data ou hora, [siga as etapas em corrigir os atalhos da área de trabalho e manutenção do sistema comum](http://go.microsoft.com/fwlink/?LinkId=155579) (http://go.microsoft.com/fwlink/?LinkId=155579).  

### <a name="step-4-rename-the-software-distribution-folder-on-your-computer"></a>Etapa 4: Renomear a pasta de distribuição de software em seu computador  

1. Pare o serviço de atualizações automáticas  

    1.  Clique em **Iniciar** e procure por **services.msc**, e pressione **Enter**.  

    2.  Clique com o botão direito do mouse em **serviço de Atualizações Automáticas**e clique em **Parar**.  

    3.  Minimize o snap-in serviços.  

2.  Renomeie o diretório **SoftwareDistribution** da seguinte maneira:  

    1.  Clique em **Iniciar** , procure por  **cmd**, e pressione **OK**.  

    2.  Digite **cd %windir%**e pressione **Enter**.  

    3.  Digite **ren SoftwareDistribution SDTemp**e pressione **Enter**.  

    4.  Digite **exit**e pressione **Enter**.  

3.  Inicie o serviço de atualizações automáticas conforme a seguir:  

    1.  Maximize o snap-in serviços.  

    2.  Clique com o botão direito do mouse em **serviço de Atualizações Automáticas**e clique em **Iniciar**.  

    3.  Feche o snap-in serviços.  

### <a name="step-5-reset-the-microsoft-antivirus-update-engine-on-your-computer"></a>Etapa 5: Redefinir o mecanismo de atualização de antivírus da Microsoft no computador  

1.  Clique em **Iniciar** , procure por  **cmd**, clique em **OK**e, em seguida, clique com botão direito do mouse em **Prompt de Comando**, depois selecione **Executar como administrador**.  

2.  Na janela do **Prompt de comando** , digite os seguintes comandos e pressione **Enter** após cada comando:  

     **Cd\\**  

     **Cd program files\windows defender**  

     **Mpcmdrun -RemoveDefinitions -all**  

     **Sair**  

3.  Reinicie o computador.  

4.  Abra o Windows Defender ou  
          Endpoint Protection, clique na guia **Atualizar**, depois clique em **Atualizar**.  

5.  Se o problema persistir, prossiga para a próxima etapa.  

### <a name="step-6-manually-install-the-virus-and-spyware-definition-updates"></a>Etapa 6: Instalar manualmente as atualizações de definições de vírus e spyware  

-   Se você estiver executando um sistema operacional do Windows de 32 bits, baixe as atualizações mais recentes manualmente a [http://go.microsoft.com/fwlink/?LinkID=87342](http://go.microsoft.com/fwlink/?LinkID=87342) (http://go.microsoft.com/fwlink/?LinkID=87342).  

-   Se você estiver executando um sistema operacional do Windows de 64 bits, baixe as atualizações mais recentes manualmente a [http://go.microsoft.com/fwlink/?LinkID=87341](http://go.microsoft.com/fwlink/?LinkID=87341) (http://go.microsoft.com/fwlink/?LinkID=87341).  

-   Clique em **Executar**. As últimas atualizações são instaladas manualmente em seu computador.  


### <a name="step-7-contact-support"></a>Etapa 7: Entrar em contato com o suporte  

-   Se as etapas não resolveram o problema, contate o suporte. Para obter mais informações, consulte [Suporte ao cliente](http://go.microsoft.com/fwlink/?LinkID=196174) (http://go.microsoft.com/fwlink/?LinkID=196174).  

##  <a name="starting-windows-defender-or-endpoint-protection-service"></a>Iniciar o serviço do Windows Defender ou Endpoint Protection  
 **Sintoma**  

 Você recebe uma mensagem informando que o **Windows Defender ou o Endpoint Protection não está monitorando seu computador porque o serviço do programa foi interrompido. Reinicie-o agora.** 

 **Solução**  

### <a name="step-1-restart-your-computer"></a>Etapa 1: Reiniciar o computador.  

-   Feche todos os aplicativos e reinicie o computador.  

### <a name="step-2-make-sure-the-windows-defender-or-endpoint-protection-service-is-set-to-automatic-and-is-started"></a>Etapa 2: Verificar se o serviço "Windows Defender" ou "Endpoint Protection" está definido como automático e foi iniciado  

1.  Clique em **Iniciar** , procure por **services.msc**e pressione **Enter**.  

2.  Pesquise **Serviço de antimalware da Microsoft**. Clique com o botão direito do mouse e selecione **Propriedades** ou clique nele duas vezes para abrir o serviço.  

3.  Verifique se o "**Tipo de inicialização**" está definido como "**Automático**".  

4.  Clique no botão **Iniciar** para iniciar o serviço. Se o botão **Iniciar** não estiver disponível, clique no botão **Parar** e no botão **Iniciar** para reiniciar o serviço.  

5.  Se você observar erros exibidos durante esse processo, envie um caso online e inclua as informações do erro.  

### <a name="step-3-remove-any-existing-internet-security-programs"></a>Etapa 3: Remover os programas de segurança da Internet existentes  

1.  Clique em **Iniciar** , procure por **appwiz.cpl**e pressione **Enter**.  

2.  Na lista de programas instalados, desinstale todos os programas de segurança da Internet de terceiros.*  

3.  Reinicie o computador e tente instalar novamente o Windows Defender ou  
          o Endpoint Protection.  

> [!NOTE]  
>  Alguns aplicativos de segurança da Internet não são totalmente desinstalados. Talvez seja necessário baixar e executar um utilitário de limpeza para seu aplicativo de segurança anterior para que ele seja totalmente removido.  

> [!CAUTION]  
>  Quando você remover os programas de segurança da Internet, o seu computador ficará sem proteção. Se você tiver problemas na instalação   
>       do Endpoint Protection depois de remover os programas de segurança da Internet existentes, entre em contato com o Windows Defender ou  
>       Suporte do Endpoint Protection com envio de caso online (para mais informações, consulte [Como enviar um caso online](http://www.microsoft.com/en-ph/security_essentials/Support/8c9074b6-1558-4d14-bc39-d294ced11096.aspx)).  

### <a name="step-4-uninstallreinstall-endpoint-protection"></a>Etapa 4: Desinstalar/reinstalar o Endpoint Protection  

1.  Clique em **Iniciar** , procure por **appwiz.cpl**e pressione **Enter**.  

2.  Na lista de programas instalados, clique em **Endpoint Protection**e desinstale-o.  

3.  Se solicitado, reinicie o computador e tente instalar novamente o Endpoint Protection.  

##  <a name="internet-connection-issues"></a>Problemas de conexão com a Internet  
 Para certificar-se de que o computador receba as atualizações mais recentes do Windows Update, você deve estar conectado à Internet.  

### <a name="step-1-verify-that-your-computer-is-connected-to-the-internet"></a>Etapa 1: Verificar se o computador está conectado à Internet  

1.  Clique em **Iniciar**, procure por **ncpa.cpl**e pressione **Enter**.  

2.  Clique com o botão direito do mouse no nome da conexão e clique em **Status**.  

3.  Se o computador estiver conectado, no Windows XP o status da conexão será exibido como **Conectado**, **Habilitado**, ou **Autenticação** foi bem-sucedida. No Windows Vista e Windows 7, o **IPv4** status será exibido como **Internet**.  

4.  Se o computador parece não estar conectado, clique com o botão direito do mouse no nome da conexão e, em seguida, clique em **Conectar**, **Habilitar**, **Autenticar**, ou **Reparar**.  

### <a name="step-3-restart-your-computer"></a>Etapa 3: Reiniciar o computador  

-   Feche os programas abertos e reinicie o computador.  

### <a name="step-4-if-you-still-cant-connect-to-the-internet-check-your-connections"></a>Etapa 4: Se você ainda não puder se conectar à Internet, verifique as conexões  

1.  Se você usar uma conexão discada, verifique se a conexão de cabo do telefone na tomada e seu modem está conectado.  

2.  Se você usar um modem com cabe, verifique se a conexão de cabo com o modem e a conexão do modem ao seu computador estão firmemente conectados.  

3.  Se você usar um modem com cabo ou um roteador DSL, verifique se as conexões com o roteador e para o computador está conectado. Tente desligar e desativar o roteador e o modem. Aguarde alguns minutos, conecte o modem primeiro, espere um minuto, e em seguida, conecte o roteador e reinicie o computador.  

##  <a name="detected-threat-cant-be-remediated"></a>Ameaça detectada não pode ser corrigida  
 Quando o Windows Defender ou  
      o Endpoint Protection detectar uma ameaça em potencial escondida em um arquivo compactado com extensão de nome de arquivo .zip ou em um compartilhamento de rede, ele tentará colocá-la em quarentena ou removê-la.  

### <a name="remove-or-scan-the-file"></a>Remova ou verifique o arquivo  

-   Se a ameaça detectada estiver em um arquivo .zip, navegue até arquivo .zip e remova o arquivo ou verifique-o clicando com o botão direito do mouse nele e selecionando **Verificar com o Windows Defender** ou **Verificar com o Endpoint Protection**. Se o Windows Defender ou o Endpoint Protection detectar ameaças adicionais no arquivo, ele notificará sobre essas ameaças e permitirá que você escolha a ação apropriada.  

-   Se a ameaça detectada estiver em um compartilhamento de rede, navegue até o compartilhamento de rede e examine-a clicando duas vezes no arquivo e selecionando **Verificar com o Windows Defender** ou **Verificar com o Endpoint Protection**. Se o Windows Defender ou o Endpoint Protection detectar ameaças adicionais no compartilhamento de rede, ele notificará sobre essas ameaças e permitirá que você escolha a ação apropriada.  

-   Se você não tiver certeza sobre a origem do arquivo, uma das melhores soluções será executar uma verificação completa no computador. Uma verificação completa pode demorar um pouco para ser concluída, mas permite que o Windows Defender ou o Endpoint Protection procure a origem da infecção e a limpe.  

##  <a name="install-the-endpoint-protection-client"></a>Instalar o cliente Endpoint Protection  

> [!NOTE]  
>  O Windows Defender é instalado com o sistema operacional em PCs com Windows 10.  

 **Sintomas**  

 A instalação falha por algum motivo desconhecido ou você recebe uma mensagem de erro com um código de erro, como 0x80070643, 0X8007064A, 0x8004FF2E, 0x8004FF01, 0x8004FF07, 0x80070002, 0x8007064C, 0x8004FF00, 0x80070001, 0x80070656, 0x8004FF40, 0xC0000156, 0x8004FF41 0x8004FF0B, 0x8004FF11, 0x80240022, 0x8004FF04, 0x80070660, 0x800106B5, 0x80070715, 0x80070005, 0x8004EE00, 0x8007003, 0x800B0100, 0x8007064E ou 0x8007007E.  

 Se o seu computador estiver executando o Windows XP Service Pack 2 (SP2), você poderá receber uma ou mais das seguintes mensagens de erro:  

-   O Assistente de Instalação está sem um pacote de rollup do gerenciador de filtros necessário para concluir a instalação.  

-   KB914882 Erro de Configuração. A Configuração não pode atualizar os arquivos do Windows XP porque o idioma instalado no sistema é diferente do idioma de atualização.  

 **Causa**  

 O Endpoint Protection não pode ser instalado em um computador que esteja executando outros programas de segurança. Às vezes, mesmo que você remova outros programas de segurança, eles não serão desinstalados completamente. Você deve estar executando uma versão original do sistema operacional Windows para instalar o Endpoint Protection.  

 **Solução**  

> [!IMPORTANT]  
>  Será necessário reiniciar o computador ao solucionar esse problema. Marque esta página nos favoritos (marque-a como Favorita) para localizar este tópico com mais facilidade posteriormente ou imprima-a para facilitar a referência.  

### <a name="step-1-remove-any-existing-security-programs"></a>Etapa 1: Remover programas de segurança existentes  
**Somente Endpoint Protection**

1.  Desinstale completamente todos os programas de segurança da Internet existentes.  

2.  Reinicie o computador.  

3.  Instale o Endpoint Protection novamente. Se isso não solucionar o problema, prossiga para a próxima etapa.  

### <a name="step-2-ensure-that-the-windows-installer-service-is-running"></a>Etapa 2: Verificar se o serviço Windows Installer está em execução  

1.  Clique em **Iniciar** , procure por **services.msc**e pressione **Enter**.  

2.  Clique com o botão direito do mouse em **Windows Installer**, e clique em **Iniciar**. Se a opção **Iniciar** não estiver disponível e as opções **Parar** e **Reiniciar** estiverem disponíveis, significa que o serviço já foi iniciado.  

3.  Na página **Serviços** , no menu **Arquivo** , clique em **Sair**.  

4.  Clique em **Iniciar** e pesquise **prompt de comando**. Clique com o botão direito em **Prompt de Comando**e em **Executar como administrador**.  

5.  Digite **MSIEXEC /REGSERVER**, e pressione **Enter**.  

    > [!NOTE]  
    >  Não há indicação de que esse comando teve êxito ou falhou.  

6.  Instale o Endpoint Protection novamente. Se isso não solucionar o problema, prossiga para a próxima etapa.  

### <a name="step-3-start-windows-in-selective-startup-mode"></a>Etapa 3: Iniciar o Windows no modo Inicialização Seletiva  

1.  Clique em **Iniciar** , procure **services.msc**, e pressione **Enter**.  

2.  Na guia **Geral** clique em **Inicialização Seletiva**, e desmarque a caixa de seleção **Carregar Itens de Inicialização** .  

3.  Na guia **Serviços** marque a caixa de seleção **Ocultar Todos os Serviços Microsoft** e desmarque todas as caixas de seleção dos serviços que permanecem na lista.  

4.  Clique em **OK**, e clique em **Reiniciar** para reiniciar o computador.  

5.  Tente instalar novamente o Endpoint Protection.  



### <a name="see-also"></a>Consulte também  
 [Perguntas frequentes sobre o cliente do Endpoint Protection](../../protect/deploy-use/endpoint-protection-client-faq.md)   

 [Ajuda do cliente do Endpoint Protection](../../protect/deploy-use/endpoint-protection-client-help.md)

