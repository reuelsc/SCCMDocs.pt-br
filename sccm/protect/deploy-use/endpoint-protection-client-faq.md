---
title: Perguntas frequentes sobre o cliente do Endpoint Protection | Microsoft Docs
description: Obtenha respostas para as perguntas frequentes sobre o Windows Defender e o Endpoint Protection.
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3aaa9d2-a40e-42b1-ad75-5a115351729e
caps.latest.revision: 15
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 017bd5b899b364fc832c721d63cc7dbad0a11671
ms.openlocfilehash: b88bc5f734b85527b81e5848deb0617db4c8dfbc


---
# <a name="endpoint-protection-client-frequently-asked-questions"></a>Perguntas frequentes sobre o cliente Endpoint Protection

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Essas perguntas frequentes são para usuários de computador cujo administrador de TI implantou o Windows Defender ou Endpoint Protection em seus computadores gerenciados. Aqui, o conteúdo pode não se aplicar a outros softwares antimalware. O Microsoft System Center Endpoint Protection gerencia o Windows Defender no Windows 10. Ele também pode implantar e gerenciar o cliente do Endpoint Protection em computadores antes do Windows 10. Embora o Windows Defender seja descrito neste artigo, suas informações também se aplicam ao Endpoint Protection.  

-   [Por que preciso de software antivírus e antispyware?](#why-do-i-need-antivirus-and-antispyware-software)  
-   [Como saber se meu computador está infectado com um software mal-intencionado?](#how-can-i-tell-if-my-computer-is-infected-with-malicious-software)
-   [Como encontrar a versão do Windows Defender?](#how-can-i-find-the-version-of-windows-defender)
-   [O que devo fazer se o Windows Defender ou o Endpoint Protection detectar software mal-intencionado no meu computador?](#what-should-i-do-if-windows-defender-or-endpoint-protection-detects-software-on-my-computer)  
-   [O que é um vírus?](#what-is-a-virus)  
-   [O que é um spyware?](#what-is-spyware)  
-   [Qual é a diferença entre vírus, spywares e outros softwares potencialmente prejudiciais?](#hat-s-the-difference-between-viruses-spyware-and-other-potentially-harmful-software)  
-   [De onde vêm vírus, spywares e outros softwares potencialmente indesejados?](#where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from)  
-   [Posso obter software mal-intencionado sem saber?](#can-i-get-malicious-software-without-knowing-it)  
-   [Por que é importante examinar os contratos de licença antes de instalar o software?](#why-is-it-important-to-review-license-agreements-before-installing-software)  
-   [Qual é a diferença entre o Windows Defender e o Endpoint Protection?](#what-s-the-difference-between-endpoint-protection-and-windows-defender)  
-   [Por que o Windows Defender não detecta cookies?](#why-doesn-t-windows-defender-detect-cookies)  
-   [Como posso evitar malwares?](#how-can-i-prevent-malware)  
-   [Quais são as definições de vírus e spyware?](#what-are-virus-and-spyware-definitions)  
-   [Como posso manter as definições de vírus e spyware atualizadas?](#how-do-i-keep-virus-and-spyware-definitions-up-to-date)  
-   [Como remover ou restaurar itens da quarentena pelo Windows Defender ou Endpoint Protection?](#how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection)  
-   [O que é proteção em tempo real?](#what-is-real-time-protection)  
-   [Como saber se o Windows Defender ou o Endpoint Protection está em execução no meu computador?](#how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer)
-   [Como configurar alertas do Windows Defender ou do Endpoint Protection?](#how-to-set-up-windows-defender-or-endpoint-protection-alerts)  

##  <a name="why-do-i-need-antivirus-and-antispyware-software"></a>Por que preciso de software antivírus e anti-spyware?  

 É importante se certificar de que o seu computador está executando um software que o protege contra software mal-intencionado. Software mal-intencionado, que inclui vírus, spyware ou outro software potencialmente indesejado, pode tentar se instalar no computador a qualquer momento que você se conectar à Internet. Ele também pode infectar o computador quando você instalar um programa usando um CD, DVD ou outra mídia removível. Software mal-intencionado, também pode ser programado para ser executado em momentos inesperados, não somente quando é instalado.  

 O Windows Defender ou o Endpoint Protection oferece três formas para ajudar a impedir que um software mal-intencionado infecte o computador:  

-   **Usando proteção em tempo real** – A proteção em tempo real permite que o Windows Defender monitore o computador em tempo integral e o alerte quando software mal-intencionado, incluindo vírus, spyware ou outro software potencialmente indesejado, tenta se instalar ou ser executado no computador. Em seguida, o Windows Defender suspende o software e permite que você siga a recomendação no software ou execute uma ação alternativa.  

    |**Opção de proteção em tempo real** |**Objetivo** |

    |-|-|  
    |Verificar todos os downloads|Essa opção monitora arquivos e programas baixados, inclusive arquivos baixados automaticamente por meio do Windows Internet Explorer e Microsoft Outlook® Express, como controles ActiveX® e programas de instalação de software. Esses arquivos podem ser baixados, instalados ou executados pelo próprio navegador. Softwares mal-intencionados, incluindo vírus, spywares e outros softwares potencialmente indesejados, podem ser incluídos nesses arquivos e instalados sem seu conhecimento.<br /><br /> Usando a opção de proteção em tempo real, o Windows Defender monitora o tempo todo o computador e verifica os arquivos ou programas mal-intencionados que você possa ter baixado. Esse recurso de monitoramento significa que o Windows Defender não precisa tornar mais lenta sua experiência de navegação ou email, exigindo uma verificação de arquivos ou programas que você queira baixar.|  
    |Monitorar atividade de arquivo e programa em seu computador|Esta opção monitora quando os arquivos e programas começam a ser executados no computador e o alerta sobre quaisquer ações executadas por eles ou neles. Isso é importante, pois o software mal-intencionado pode usar as vulnerabilidades nos programas que você instalou para executar software mal-intencionado ou indesejado sem seu conhecimento. Por exemplo, spyware pode ser executado em segundo plano quando você inicia um programa que usa com frequência. O Windows Defender monitora os programas e o alerta quando detecta atividade suspeita.|  
    |Habilitar monitoramento de comportamento|Esta opção monitora coleções de padrões de comportamento suspeitos que não podem ser detectados por métodos de detecção de antivírus tradicionais.|  

    |Habilitar Sistema de Inspeção de Rede|Esta opção ajuda a proteger o computador contra explorações de "dia zero" de vulnerabilidades conhecidas, reduzindo a janela de tempo entre o momento em que uma vulnerabilidade é descoberta e a aplicação de uma atualização.|  

-   **Opções de verificação** – é possível usar o Windows Defender para verificar possíveis ameaças, como vírus, spywares e outros softwares mal-intencionados que possam colocar o computador em risco. Você também pode usá-lo para agendar verificações regularmente, bem como remover softwares mal-intencionados detectados durante uma verificação.  

-   **Comunidade do Microsoft Active Protection Service** – A comunidade online do Microsoft Active Protection Service ajuda você a ver como outras pessoas respondem a software ainda não classificado quanto a riscos. Você pode usar essas informações para ajudá-lo a escolher se deve permitir esse software no computador. Por sua vez, se você participar, suas escolhas serão adicionadas às classificações da comunidade, a fim de ajudar outras pessoas a decidir o que fazer.  

##  <a name="how-can-i-tell-if-my-computer-is-infected-with-malicious-software"></a>Como saber se meu computador está infectado com um software mal-intencionado?  

 Você poderá ter algum tipo de software mal-intencionado, incluindo vírus, spywares ou outros softwares potencialmente indesejados no computador, se:  

-   Perceber novas barras de ferramentas, links ou favoritos não adicionados intencionalmente no navegador da Web.  

-   A home page, o ponteiro do mouse ou o programa de pesquisa mudar inesperadamente.  

-   Você digita o endereço de um site específico, como um mecanismo de pesquisa, mas é direcionado para um site diferente sem aviso.  

-   Arquivos são automaticamente excluídos do computador.  

-   O computador é usado para atacar outros computadores.  

-   Você vê anúncios de pop-up, mesmo quando não está na Internet.  

-   Seu computador, de repente, começa a ser executado mais lentamente do que o habitual. Nem todos os problemas de desempenho do computador são causados por software mal-intencionado, mas o software mal-intencionado, especialmente spyware, pode causar uma alteração perceptível.  

Pode haver um software mal-intencionado no computador mesmo se você não percebe nenhum sintoma. Esse tipo de software pode coletar informações sobre você e o computador sem seu conhecimento ou consentimento. Para ajudar a proteger sua privacidade e o computador, você deve executar o Windows Defender ou Endpoint Protection em todos os momentos.  

## <a name="how-can-i-find-the-version-of-windows-defender"></a>Como encontrar a versão do Windows Defender?
 Para exibir a versão do Windows Defender em execução no computador, abra o Windows Defender (clique em **Iniciar** e procure **Windows Defender**), clique em **Configurações** e role até o fim das configurações para localizar as **Informações de versão** do Windows Defender.

##  <a name="what-should-i-do-if-windows-defender-or-endpoint-protection-detects-malicious-software-on-my-computer"></a>O que devo fazer se o Windows Defender ou o Endpoint Protection detectar software mal-intencionado no computador?  

 Se o Windows Defender detectar software mal-intencionado ou software potencialmente indesejado no computador (seja ao monitorar o computador usando proteção em tempo real ou após executar uma verificação), ele o notificará sobre o item detectado exibindo uma mensagem de notificação no canto direito inferior da tela.  

 A área de notificação inclui um botão **Limpar computador** e um link **Mostrar detalhes** , que permite que você exiba informações adicionais sobre o item detectado. Clique no link **Mostrar detalhes** para abrir a janela **Detalhes da possível ameaça** para obter informações adicionais sobre o item detectado. Agora, você pode escolher qual ação aplicar ao item ou clicar em **Limpar computador**. Se for necessário determinar qual ação aplicar ao item detectado, use o nível de alerta que o Windows Defender atribuiu ao item como seu guia (para obter mais informações, consulte Compreendendo os níveis de alerta).  

 Níveis de alerta ajudam na escolha de como responder a vírus, spyware e outros softwares potencialmente indesejados. Embora o Windows Defender recomende que você remova todos os vírus e spywares, nem todo software sinalizado é mal-intencionado ou indesejado. As informações a seguir podem ajudá-lo a decidir o que fazer se o Windows Defender detecta software potencialmente indesejado no computador.  

 Dependendo do nível de alerta, você pode escolher uma das seguintes ações a serem aplicadas ao item detectado:  

-   **Remover** — Esta ação exclui permanentemente o software do computador.  

-   **Quarentena** — Esta ação coloca o software em quarentena para que ele não possa ser executado. Quando o Windows Defende coloca o software em quarentena, ele o move para outro local no computador e impede a execução do software até que você escolha restaurá-lo ou removê-lo do computador.  

-   **Permitir** – Esta ação adiciona o software à lista de permissões do Windows Defender e permite que ele seja executado no computador. O Windows Defender interromperá os alertas dos riscos que o software possa apresentar à sua privacidade ou ao computador.  

 Se você escolher **Permitir** para um item, como um software, o Windows Defender interromperá os alertas dos riscos que esse software possa apresentar à sua privacidade ou ao computador. Portanto, adicione o software à lista de permissões somente se você confiar no software e no fornecedor de software.  

### <a name="how-to-remove-potentially-harmful-software"></a>Como remover software potencialmente prejudicial

Para remover todos os itens indesejados ou potencialmente prejudiciais que o Windows Defender detecta de modo rápido e fácil, use a opção **Limpar computador** .  

1.  Quando você vir a mensagem de notificação exibida na área de Notificação após a detecção de possíveis ameaças, clique em **Limpar computador**.  

2.  O Windows Defender remove a possível ameaça (ou ameaças) e o notifica quando tiver concluído a limpeza do computador.  

3.  Para saber mais sobre as ameaças detectadas, clique na guia **Histórico** e selecione **Todos os itens detectados**.  

4.  Se você não conseguir ver todos os itens detectados, clique em **Exibir detalhes**. Se for solicitada uma confirmação ou senha do administrador, digite a senha ou confirme a ação. Em sistemas que executam o Windows XP, poderá ser necessário fazer logon como administrador nesse computador.  

> [!NOTE]  
>  Durante a limpeza do computador, sempre que possível, o Windows Defender remove somente a parte infectada de um arquivo, e não o arquivo inteiro.  

##  <a name="what-is-a-virus"></a>O que é um vírus?  
 Vírus de computador são programas deliberadamente desenvolvidos para interferir na operação do computador, gravar, corromper ou excluir dados ou infectar outros computadores na Internet. Os vírus geralmente desaceleram ou causam outros problemas no processo.  

##  <a name="what-is-spyware"></a>O que é um spyware?  
 Spyware é um software que pode se instalar ou ser executado no computador sem seu consentimento ou sem aviso ou controle adequado. O Spyware pode não apresentar sintomas depois de infectar o computador, mas muitos programas mal-intencionados ou indesejados podem afetar o funcionamento do computador. Por exemplo, o spyware pode monitorar o comportamento online ou coletar informações sobre você (incluindo informações que podem identificá-lo ou outras informações confidenciais), alterar configurações no computador ou torná-lo lento.  

##  <a name="whats-the-difference-between-viruses-spyware-and-other-potentially-harmful-software"></a>Qual é a diferença entre vírus, spywares e outros softwares potencialmente prejudiciais?  
 Vírus e spyware estão instalados no computador sem seu conhecimento e têm o potencial de serem destrutivos e intrusivos. Eles também têm a capacidade de capturar informações no computador e danificar ou excluir essas informações. Ambos podem afetar negativamente o desempenho do computador.  

 As principais diferenças entre vírus e spyware é como eles se comportam no computador. Vírus, como organismos vivos, querem infectar um computador, reproduzir-se e se espalhar para tantos outros computadores quanto possível. Spyware, no entanto, é mais parecido com uma toupeira – ele quer “se mover” para dentro do computador e permanecer lá o máximo possível, enviando informações valiosas sobre seu computador a uma fonte externa enquanto estiver lá.  

##  <a name="where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from"></a>De onde vêm vírus, spywares e outros softwares potencialmente indesejados?  
 Softwares indesejados, como vírus, podem ser instalados por sites ou por programas que você baixou ou instalou usando um CD, DVD, disco rígido externo ou um dispositivo. Spyware geralmente é instalado por meio de software gratuito, como compartilhamento de arquivos, protetores de tela ou barras de ferramentas de pesquisa.  

##  <a name="can-i-get-malicious-software-without-knowing-it"></a>Posso obter software mal-intencionado sem saber?  
 Sim, alguns software mal-intencionados podem ser instalados de um site por meio de um script ou programa inserido em uma página da Web. Alguns software mal-intencionados requerem sua ajuda para serem instalados. Esses software usam pop-ups da Web ou software gratuito que exigem que você aceite um arquivo baixável. No entanto, se você mantém o Microsoft Windows® atualizado e não reduz as configurações de segurança, pode minimizar as chances de uma infecção.  

##  <a name="why-is-it-important-to-review-license-agreements-before-installing-software"></a>Por que é importante examinar os contratos de licença antes de instalar o software?  
 Ao visitar sites, não concorde em baixar automaticamente qualquer coisa que o site oferece. Se você baixar um software gratuito, como programas de compartilhamento de arquivos ou proteções de tela, leia atentamente o contrato de licença. Procure cláusulas que digam que você deve aceitar anúncios e pop-ups da empresa ou que o software enviará certas informações ao fornecedor de software.  

##  <a name="whats-the-difference-between-endpoint-protection-and-windows-defender"></a>Qual é a diferença entre o Windows Defender e o Endpoint Protection?  
 O Endpoint Protection é software antimalware, o que significa que ele foi projetado para detectar e ajudar a proteger seu computador contra uma grande variedade de softwares mal-intencionados, incluindo vírus, spywares e outros softwares potencialmente indesejados. O Windows Defender, instalado automaticamente com o sistema operacional Windows, é um software que detecta e interrompe spyware.  

##  <a name="why-doesnt-windows-defender-detect-cookies"></a>Por que o Windows Defender não detecta cookies?  
 Cookies são pequenos arquivos de texto que os sites colocam no computador para armazenar informações sobre você e suas preferências. Sites usam cookies para oferecer a você uma experiência personalizada e reunir informações sobre uso de sites da Web. O Windows Defender não detecta cookies, porque ele não os considera uma ameaça à sua privacidade ou à segurança do computador. A maioria dos programas de navegador da Internet permite que você bloqueie cookies.  

##  <a name="how-can-i-prevent-malware"></a>Como posso evitar malwares?  
 Duas das maiores preocupações para os usuários de computador hoje são vírus e spywares. Em ambos os casos, embora eles sejam um problema, você pode se defender deles muito bem com apenas um pouco de planejamento:  

-   Mantenha o software do computador atualizado e lembre-se de instalar todos os patches. Lembre-se de atualizar o sistema operacional regularmente.  

-   Verifique se o software antivírus e antispyware, o Windows Defender, está usando as atualizações mais recentes contra possíveis ameaças (veja Como manter definições de vírus e spyware atualizadas?). Certifique-se também de estar sempre usando a última versão do Windows Defender.  

-   Baixe atualizações apenas de fontes confiáveis. Para sistemas operacionais Windows, sempre vá para [Microsoft Update](http://go.microsoft.com/fwlink/?LinkID=96304) (http://go.microsoft.com/fwlink/?LinkID=96304) e para outros software use sempre sites legítimos da empresa ou da pessoa que os produz.  

-   Se você receber um email com um anexo e não tiver certeza da origem, exclua-o imediatamente. Não baixe nenhum aplicativo ou arquivos de fontes desconhecidas e seja cuidadoso ao trocar arquivos com outros usuários.  

-   Instale e use um firewall. É recomendável que você habilite o firewall do Windows.  

##  <a name="what-are-virus-and-spyware-definitions"></a>Quais são as definições de vírus e spyware?  
 Ao usar o Windows Defender ou Endpoint Protection, é importante ter as definições de spyware e vírus atualizadas. Definições são arquivos que atuam como uma enciclopédia crescente de possíveis ameaças de software. O Windows Defender ou o Endpoint Protection usa definições para determinar se o software detectado é um vírus, um spyware ou outro software potencialmente indesejado, e também para alertá-lo quanto a possíveis riscos. Para ajudar a manter as definições atualizadas, o Windows Defender ou Endpoint Protection funciona com o Microsoft Update para instalar automaticamente novas definições, à medida que elas são lançadas. Você também pode definir o Windows Defender ou Endpoint Protection para conferir online se há definições atualizadas antes da verificação.  

##  <a name="how-do-i-keep-virus-and-spyware-definitions-up-to-date"></a>Como posso manter as definições de vírus e spyware atualizadas?  
 Definições de vírus e spyware são arquivos que atuam como uma enciclopédia de softwares mal-intencionados conhecidos, incluindo vírus, spywares e outros softwares potencialmente indesejados. Como o software mal-intencionado está em constante evolução, o Windows Defender ou o Endpoint Protection conta com definições atualizadas para determinar se o software que está tentando instalar, executar ou alterar configurações em seu computador é um vírus, spyware ou outro software potencialmente indesejado.  

### <a name="to-automatically-check-for-new-definitions-before-scheduled-scans-recommended"></a>Para verificar automaticamente novas definições antes das verificações agendadas (recomendado)  

1.  Abra o cliente Windows Defender ou Endpoint Protection clicando no ícone na área de notificação ou iniciando-o no menu **Iniciar** .  

2.  Clique em **Configurações**e em **Verificação agendada**.  

3.  Verifique se a caixa de seleção **Verificar definições de vírus e spyware mais recentes antes de executar uma verificação agendada** está marcada e, seguida, clique em **Salvar alterações**. Se for solicitada uma confirmação ou senha do administrador, digite a senha ou confirme a ação.  

### <a name="to-check-for-new-definitions-manually"></a>Para verificar manualmente se há novas definições

 O Windows Defender ou Endpoint Protection atualiza automaticamente as definições de vírus e spyware no computador. Se as definições não tiverem sido atualizadas por mais de sete dias (por exemplo, se você não tiver ligado o computador por uma semana), o Windows Defender ou o Endpoint Protection notificará que as definições estão desatualizadas.  

1.  Abra o cliente Windows Defender ou Endpoint Protection clicando no ícone na área de notificação ou iniciando-o no menu **Iniciar** .  

2.  Para verificar se há novas definições manualmente, clique na guia **Atualizar** e, em seguida, clique em **Atualizar definições**.  

##  <a name="how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a>Como remover ou restaurar itens da quarentena pelo Windows Defender ou Endpoint Protection?  

 Quando o Windows Defender ou Endpoint Protection coloca o software em quarentena, ele move o software para outro local no computador e impede a execução do software até que você escolha restaurá-lo ou removê-lo do computador.  

 Para todas as etapas mencionadas nesse procedimento, digite a senha ou forneça a confirmação, se for solicitada uma confirmação ou senha do administrador.  

###  <a name="to-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a>Como remover ou restaurar itens da quarentena pelo Windows Defender ou Endpoint Protection


1.  Clique na guia **Histórico** , selecione **Itens em quarentena**e depois a opção **Itens em quarentena** .  

2.  Clique em **Exibir detalhes** para ver todos os itens.  

3.  Verifique cada item e, para cada um deles, clique em **Remover** ou **Restaurar**. Se desejar remover todos os itens em quarentena do computador, clique em **Remover tudo**.  

##  <a name="what-is-real-time-protection"></a>O que é proteção em tempo real?  

 A proteção em tempo real permite que o Windows Defender monitore o computador o tempo todo e o alerte quando possíveis ameaças, como vírus e spyware, tentam se instalar ou ser executados no computador. Como esse recurso é um elemento importante na maneira pela qual o Windows Defender ajuda a proteger o computador, você deve garantir que a proteção em tempo real esteja sempre ligada. Se a proteção em tempo real for desligada, o Windows Defender o avisará e alterará o status do computador para 'Em risco'.  

 Sempre que a proteção em tempo real detecta uma ameaça ou possível ameaça, o Windows Defender exibe uma notificação. Você pode escolher entre as seguintes opções:  

-   Clicar em **Limpar computador** para remover o item detectado. O Windows Defender removerá automaticamente o item do seu computador.  

-   Clicar no link **Mostrar detalhes** para exibir Detalhes da possível ameaça e, em seguida, escolher qual ação aplicar ao item detectado.  

 Você pode escolher o software e as configurações que quer que o Windows Defender monitore, mas recomendamos que ative a proteção em tempo real e habilite todas as opções de proteção em tempo real. A tabela a seguir explica as opções disponíveis.  

|||  
|-|-|  
|**Opção de proteção em tempo real**|**Finalidade**|  
|Verificar todos os downloads|Essa opção monitora arquivos e programas baixados, inclusive arquivos baixados automaticamente por meio do Windows Internet Explorer e Microsoft Outlook® Express, como controles ActiveX® e programas de instalação de software. Esses arquivos podem ser baixados, instalados ou executados pelo próprio navegador. Softwares mal-intencionados, incluindo vírus, spywares e outros softwares potencialmente indesejados, podem ser incluídos nesses arquivos e instalados sem seu conhecimento.<br /><br /> Usando a opção de proteção em tempo real, o Windows Defender monitora o tempo todo o computador e verifica os arquivos ou programas mal-intencionados que você possa ter baixado. Esse recurso de monitoramento significa que o Windows Defender não precisa tornar mais lenta sua experiência de navegação ou email, exigindo uma verificação de arquivos ou programas que você queira baixar.|  
|Monitorar atividade de arquivos e programas no computador|Essa opção monitora quando os arquivos e programas começam a ser executados no computador e o alerta sobre quaisquer ações executadas por eles ou neles. Isso é importante, pois o software mal-intencionado pode usar as vulnerabilidades nos programas que você instalou para executar software mal-intencionado ou indesejado sem seu conhecimento. Por exemplo, spyware pode ser executado em segundo plano quando você inicia um programa que usa com frequência. O Windows Defender monitora os programas e o alerta quando detecta atividade suspeita.|  
|Habilitar o comportamento de monitoramento|Essa opção monitora coleções de padrões de comportamento suspeitos que não podem ser detectados por métodos de detecção de antivírus tradicionais.|  
|Ativar o sistema de inspeção de rede|Esta opção ajuda a proteger o computador contra explorações de "dia zero" de vulnerabilidades conhecidas, diminuindo a janela de tempo entre o momento em que uma vulnerabilidade é descoberta e a aplicação de uma atualização.|  

### <a name="to-turn-off-real-time-protection"></a>Para desligar a proteção em tempo real  

1.  Clique em **Configurações**e em **Proteção em tempo real.**  

2.  Desmarque as opções de proteção em tempo real que você quer desligar e, em seguida, clique em **Salvar alterações**. Se for solicitada uma confirmação ou senha do administrador, digite a senha ou confirme a ação.  

##  <a name="how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer"></a>Como saber se o Windows Defender ou o Endpoint Protection está em execução no meu computador?  

 Depois de instalar o Windows Defender no computador, você pode fechar a janela principal e deixar que o Windows Defender seja executado em segundo plano. O Windows Defender continuará em execução no computador, a monitorá-lo e a ajudar a protegê-lo contra ameaças.  

 Certamente você saberá se o Windows Defender está em execução sempre que ele exibir mensagens de notificação na área de notificação. Essas notificações alertam você sobre possíveis ameaças que o Windows Defender detectou.  

 Você também receberá outras notificações de alertas, por exemplo, se por algum motivo, a proteção em tempo real for desativada, se você não tiver atualizado as suas definições de vírus e spyware por vários dias ou quando as atualizações do programa estiverem disponíveis. O Windows Defender também exibirá rapidamente uma notificação para avisá-lo que está verificando o computador.  

> [!TIP]  

>Se você não vir o ícone do Windows Defender na área de notificação, clique na seta na área de notificação para mostrar ícones ocultos, incluindo o ícone do Windows Defender.  


 A cor do ícone depende do status atual do computador:  

-   Verde indica que o status do computador é "protegido".  

-   Amarelo indica que o status do computador é "potencialmente desprotegido".  

-   Vermelho indica que o status do computador é "em risco".  

##  <a name="how-to-set-up-windows-defender-or-endpoint-protection-alerts"></a>Como configurar alertas do Windows Defender ou do Endpoint Protection?  
 Quando o Windows Defender está em execução no computador, ele o alerta automaticamente se detecta vírus, spywares ou outros softwares potencialmente indesejados. Você também poderá definir o Windows Defender para alertá-lo se executar algum software que ainda não foi analisado e optar por ser alertado quando um software fizer alterações no computador.  

### <a name="to-set-up-alerts"></a>Para configurar os alertas  

1.  Clique em **Configurações**e em **Proteção em tempo real.**  

2.  Certifique-se de que a caixa de seleção **Ativar a proteção em tempo real (recomendado)** esteja marcada.  

3.  Marque as caixas de seleção ao lado das opções de proteção em tempo real que deseja executar e clique em **Salvar alterações**. Se for solicitada uma confirmação ou senha do administrador, digite a senha ou confirme a ação.  

### <a name="see-also"></a>Consulte também  
 [Solucionando problemas do cliente Windows Defender ou Endpoint Protection](troubleshoot-endpoint-client.md)   

 [Ajuda do cliente do Endpoint Protection](endpoint-protection-client-help.md)



<!--HONumber=Feb17_HO3-->


