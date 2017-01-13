---
title: Configurar o cliente do Endpoint Protection | Microsoft Docs
description: "Saiba como definir configurações personalizadas do cliente para o Endpoint Protection que podem ser implantadas em coleções do computador em sua hierarquia."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 2d7ec9cc626f3ccfded990cf8ba392c4979adfee


---

# <a name="configure-custom-client-settings-for-endpoint-protection"></a>Definir configurações personalizadas do cliente para o Endpoint Protection

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este procedimento define as configurações personalizadas do cliente do Endpoint Protection que podem ser implantadas em coleções de computadores na sua hierarquia.

> [!IMPORTANT]
>  Defina apenas as configurações padrão do cliente do Endpoint Protection, a menos que tenha certeza de que deseja aplicá-las a todos os computadores na hierarquia.

## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>Para habilitar o Endpoint Protection e definir configurações personalizadas do cliente

1.  No console do Configuration Manager, clique em **Administração**.

2.  No espaço de trabalho **Administração** , clique em **Configurações do Cliente**.

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Configurações Personalizadas do Dispositivo do Cliente**.

4.  Na caixa de diálogo **Criar Configurações Personalizadas do Dispositivo do Cliente** , forneça um nome e uma descrição para o grupo de configurações e selecione **Endpoint Protection**.

5.  Defina as configurações do cliente do Endpoint Protection necessárias. Para obter uma lista completa das configurações de cliente do Endpoint Protection que você pode configurar, consulte a seção Endpoint Protection em [Sobre as configurações de cliente no System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).

   > [!IMPORTANT]
   >  Você deve instalar a função do sistema de sites do Endpoint Protection antes de definir as configurações do cliente do Endpoint Protection.

6.  Clique em **OK** para fechar a caixa de diálogo **Criar Configurações Personalizadas do Dispositivo do Cliente** . As novas configurações do cliente são exibidas no nó **Configurações do Cliente** do espaço de trabalho **Administração** .

7.  Antes de usar as configurações personalizadas do cliente, você deve implantá-las em uma coleção. Selecione as configurações personalizadas do cliente que você deseja implantar e, na guia **Início** , no grupo **Configurações do Cliente** , clique em **Implantar**.

8.  Na caixa de diálogo **Selecionar Coleção** , escolha a coleção na qual você deseja implantar as configurações do cliente e clique em **OK**. A nova implantação é mostrada na guia **Implantações** do painel de detalhes.

Os computadores cliente serão definidos com essas configurações durante o próximo download da política do cliente. Para iniciar a recuperação de política para um único cliente, veja a seção Iniciar recuperação de política de um cliente do Configuration Manager em [Como gerenciar clientes no System Center Configuration Manager](../../core/clients/manage/manage-clients.md).

## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image-in-configuration-manager"></a>Como configurar o cliente do Endpoint Protection em uma imagem de disco no Configuration Manager
É possível instalar o cliente do Endpoint Protection em um computador que você queira usar como origem da imagem de disco para implantação do sistema operacional do Configuration Manager. Normalmente, esse computador é chamado de computador de referência. Depois de criar a imagem do sistema operacional, você poderá usar a implantação do sistema operacional do Configuration Manager para implantar a imagem que pode conter pacotes de software, incluindo o Endpoint Protection, nos seus computadores cliente.

Use os procedimentos deste tópico para ajudá-lo a instalar e configurar o cliente do Endpoint Protection em um computador de referência

### <a name="prerequisites-for-installing-the-endpoint-protection-client-on-the-reference-computer"></a>Pré-requisitos para instalação cliente do Endpoint Protection no computador de referência
A lista a seguir contém os pré-requisitos necessários para instalar o software cliente do Endpoint Protection em um computador de referência.

-   Você deve ter acesso ao pacote de instalação de cliente do Endpoint Protection, **scepinstall.exe**. Esse pacote pode ser encontrado na pasta **Cliente** da pasta de instalação do Microsoft System Center Configuration Manager no servidor do site.

-   Para verificar se o cliente do Endpoint Protection está implantado com a configuração necessária na sua organização, crie um política antimalware e exporte essa política. Em seguida, você pode especificar a política antimalware a ser usada quando você instala manualmente o cliente do Endpoint Protection. Para mais informações, consulte [Como criar e implantar políticas antimalware para o Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md).

   > [!NOTE]
   >  A **Política de Antimalware do Cliente Padrão** não pode ser exportada.

-   Se desejar instalar o cliente do Endpoint Protection com as definições mais recentes, baixe-as no [Centro de Proteção contra Malware da Microsoft](http://go.microsoft.com/fwlink/?LinkID=200965).

### <a name="how-to-install-the-endpoint-protection-client-software-on-the-reference-computer"></a>Como instalar o software cliente do Endpoint Protection no computador de referência
Você pode instalar o cliente do Endpoint Protection localmente no computador de referência de um prompt de comando. Para fazer isso, primeiro é necessário obter o arquivo de instalação **scepinstall.exe**. Além disso, você pode instalar o cliente com uma política antimalware pré-configurada ou com um política antimalware exportada anteriormente.

## <a name="to-install-the-endpoint-protection-client-from-a-command-prompt"></a>Para instalar o cliente do Endpoint Protection a partir de um prompt de comando

1.  Copie **scepinstall.exe** da pasta **Cliente** na mídia de instalação do System Center Configuration Manager para o computador no qual você deseja instalar o software cliente do Endpoint Protection.

2.  Abra um prompt de comando com privilégios de administrador, navegue até a pasta em que o **scepinstall.exe** está localizado e execute o seguinte comando, adicionando quaisquer propriedades adicionais de linha de comando que você precise:

   ```
   scepinstall.exe
   ```

    Você pode especificar uma das seguintes propriedades de linha de comando:

   |Propriedade|Descrição|
   |--------------|-----------------|
   |/s|Especifica que uma instalação silenciosa será executada.|
   |/q|Especifica que uma extração silenciosa dos arquivos de instalação será executada.|
   |/i|Especifica que deve ser realizada uma instalação normal.|
   |/noreplace|Especifica que o software antimalware de terceiros não é desinstalado durante a instalação.|
   |/policy|Especifica um arquivo de política antimalware a ser usado para configurar o cliente durante a instalação.|
   |/sqmoptin|Especifica que a instalação do software cliente foi aceita pelo Programa de Aperfeiçoamento da Experiência do Usuário da Microsoft.|

3.  Siga as instruções na tela para concluir a instalação cliente.

4.  Se você tiver baixado o pacote de definição com atualização mais recente, copie o pacote para o computador cliente e clique duas vezes no pacote de definição para instalá-lo.

   > [!NOTE]
   >  Depois que a instalação cliente do Endpoint Protection estiver concluída, o cliente executa automaticamente uma verificação de atualização da definição. Se a verificação de atualização for bem-sucedida, você não precisará instalar manualmente o pacote de atualização da definição mais recente.

## <a name="to-install-the-client-software-with-an-antimalware-policy-from-the-command-prompt"></a>Para instalar o software cliente com uma política antimalware do prompt de comando

1.  Copie **scepinstall.exe** e a política antimalware exportada ou pré-configurada para o computador no qual você deseja instalar o software cliente do Endpoint Protection.

2.  Abra um prompt de comando com os privilégios de administrador, navegue até a pasta onde **scepinstall.exe** e a política antimalware estão localizados e execute o seguinte comando:

   ```
   scepinstall.exe /policy <full path>\<policy file>
   ```

3.  Siga as instruções na tela para concluir a instalação cliente.

4.  Se você tiver baixado o pacote de definição mais recente, copie o pacote para o computador cliente e clique duas vezes no pacote de definição para instalá-lo.

   > [!NOTE]
   >  Depois que a instalação cliente do Endpoint Protection estiver concluída, o cliente executa automaticamente uma verificação de atualização da definição. Se a verificação de atualização for bem-sucedida, você não precisará instalar manualmente o pacote de atualização da definição mais recente.

## <a name="verify-that-the-endpoint-protection-client-is-installed-correctly"></a>Verificar se o cliente do Endpoint Protection está instalado corretamente
Depois de instalar o cliente do Endpoint Protection no seu computador de referência, verifique se o cliente está funcionando corretamente.

### <a name="to-verify-that-the-endpoint-protection-client-is-installed-correctly"></a>Para verificar se o cliente do Endpoint Protection está instalado corretamente

1.  No computador de referência, abra **System Center Endpoint Protection** das notificações do Windows.

2.  Na guia **Início** da caixa de diálogo **System Center Endpoint Protection**, verifique se **Proteção em tempo real** está definido como **Ativo**.

3.  Verifique se **Atualizado** é exibido para **Definições de vírus e spyware**.

4.  Para ajudar a confirmar se seu computador de referência está pronto para geração de imagens, em **Opções de verificação**, selecione **Completa**e clique em **Verificar agora**.

### <a name="how-to-prepare-the-endpoint-protection-client-for-imaging"></a>Como preparar o cliente do Endpoint Protection para geração de imagens
Depois de verificar se o cliente do Endpoint Protection está instalado corretamente no computador de referência, você poderá preparar o computador para geração de imagens. Execute as seguintes etapas para preparar o cliente do Endpoint Protection para geração de imagens.


Para obter mais informações sobre implantação de sistema operacional no Configuration Manager, consulte [Gerenciar imagens do sistema operacional com o System Center Configuration Manager](/sccm/osd/get-started/manage-operating-system-images).

### <a name="to-prepare-the-endpoint-protection-client-for-imaging"></a>Para preparar o cliente do Endpoint Protection para geração de imagens

1.  No computador de referência, faça logon como um usuário com privilégios administrativos.

2.  Baixe e instale **PsTools** do [Site Windows SysInternals](http://go.microsoft.com/fwlink/?LinkId=215263) na TechNet.

3.  Abra um prompt de comando elevado, navegue até a pasta na qual você instalou PsTools e digite o seguinte comando

   ```
   Psexec.exe -s -i regedit.exe
   ```

   > [!IMPORTANT]
   >  Tenha cuidado ao executar o Editor do Registro dessa maneira; a opção -s no PsExec.exe executa o Editor do Registro com privilégios do LocalSystem.

4.  No Editor do Registro, navegue até cada uma das seguintes chaves do Registro e exclua-as.

   > [!IMPORTANT]
   >  Você deve excluir as chaves do Registro como última etapa antes da geração de imagens do computador de referência. As chaves do Registro são recriadas quando o cliente do Endpoint Protection é iniciado. Se você reiniciar o computador de referência, deverá excluir as chaves do Registro novamente.

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID**

Depois de concluir as etapas anteriores, você poderá preparar o computador de referência para geração de imagens. Para obter mais informações sobre implantação de sistema operacional no Configuration Manager, consulte [Gerenciar imagens do sistema operacional com o System Center Configuration Manager](/sccm/osd/get-started/manage-operating-system-images).

Quando uma imagem que contém o software cliente do Endpoint Protection é implantada, o cliente do Endpoint Protection reporta automaticamente as informações para o site do Configuration Manager ao qual o computador está atribuído, e a política aplicável ao computador cliente é baixada e aplicada.



<!--HONumber=Dec16_HO3-->


