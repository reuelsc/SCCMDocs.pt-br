---
title: Configurar Endpoint Protection
titleSuffix: Configuration Manager
description: Saiba como definir configurações personalizadas do cliente do Endpoint Protection.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6299163813edca74c198bba4b778288bab1b77d6
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500482"
---
# <a name="configure-custom-client-settings-for-endpoint-protection"></a>Definir configurações personalizadas do cliente para o Endpoint Protection

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Esse procedimento define as configurações personalizadas do cliente do Endpoint Protection, que você pode implantar em coleções de dispositivos em sua hierarquia.

> [!IMPORTANT]  
>  Defina apenas as configurações padrão do cliente do Endpoint Protection, caso tenha certeza de que deseja aplicá-las a todos os computadores na hierarquia. 



## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>Para habilitar o Endpoint Protection e definir configurações personalizadas do cliente

1. No console do Configuration Manager, clique em **Administração**.  

2. No workspace **Administração**, clique em **Configurações do Cliente**.  

3. Na guia **Início** , no grupo **Criar** , clique em **Criar Configurações Personalizadas do Dispositivo do Cliente**.  

4. Na caixa de diálogo **Criar Configurações Personalizadas do Dispositivo do Cliente** , forneça um nome e uma descrição para o grupo de configurações e selecione **Endpoint Protection**.  

5. Defina as configurações do cliente do Endpoint Protection necessárias. Para obter uma lista completa das configurações do cliente do Endpoint Protection que você pode definir, confira a seção Endpoint Protection em [Sobre as configurações do cliente](/sccm/core/clients/deploy/about-client-settings#endpoint-protection).  

   > [!IMPORTANT]  
   >  Instale a função de sistema de sites do Endpoint Protection antes de definir as configurações de cliente do Endpoint Protection.  

6. Clique em **OK** para fechar a caixa de diálogo **Criar Configurações Personalizadas do Dispositivo do Cliente** . As novas configurações do cliente são exibidas no nó **Configurações do Cliente** do workspace **Administração**.  

7. Em seguida, implante as configurações personalizadas do cliente em uma coleção. Selecione as configurações personalizadas do cliente que você deseja implantar. Na guia **Início**, no grupo **Configurações do Cliente**, clique em **Implantar**.  

8. Na caixa de diálogo **Selecionar Coleção** , escolha a coleção na qual você deseja implantar as configurações do cliente e clique em **OK**. A nova implantação é mostrada na guia **Implantações** do painel de detalhes.  

Os clientes serão definidos com essas configurações quando baixarem a próxima política do cliente. Para obter mais informações, confira [Iniciar recuperação de política para um cliente do Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  



## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image"></a>Como provisionar o cliente do Endpoint Protection em uma imagem de disco

Instale o cliente do Endpoint Protection em um computador que você pretende usar como origem da imagem de disco para a implantação do sistema operacional do Configuration Manager. Normalmente, esse computador é chamado de computador de referência. Depois de criar a imagem do sistema operacional, use a implantação do sistema operacional do Configuration Manager para implantar a imagem.

> [!Important]  
> O Windows 10 e o Windows Server 2016 já têm o Windows Defender instalado por padrão. Esse procedimento não é necessário nessas versões do Windows.  

Use os procedimentos a seguir para ajudá-lo a instalar e configurar o cliente do Endpoint Protection em um computador de referência.


### <a name="prerequisites"></a>Pré-requisitos

A lista a seguir contém os pré-requisitos necessários para instalar o software cliente do Endpoint Protection em um computador de referência.

- Você deve ter acesso ao pacote de instalação de cliente do Endpoint Protection, **scepinstall.exe**. Localize esse pacote na pasta **Cliente** da pasta de instalação do Configuration Manager no servidor do site.  

- Para implantar o cliente do Endpoint Protection com a configuração necessária para sua organização, crie e exporte uma política de antimalware. Ao instalar manualmente o cliente do Endpoint Protection, especifique essa política. Para obter mais informações, confira [Como criar e implantar políticas antimalware](/sccm/protect/deploy-use/endpoint-antimalware-policies).  

  > [!NOTE]  
  >  Não é possível exportar a **Política antimalware do cliente padrão**.  

- Se você quiser instalar o cliente do Endpoint Protection com as definições mais recentes, baixe-o de [Windows Defender Security Intelligence](https://www.microsoft.com/wdsi) (Inteligência em segurança do Windows Defender).  

> [!NOTE]  
> Começando no Configuration Manager 1802, você não precisa mais instalar o agente do Endpoint Protection (SCEPInstall) em dispositivos Windows 10. Se ele já estiver instalado nos dispositivos Windows 10, o Configuration Manager não o removerá. Os administradores podem remover o agente do Endpoint Protection dos dispositivos Windows 10 que executam, no mínimo, a versão de cliente 1802. O SCEPInstall.exe ainda poderá estar presente no C:\Windows\ccmsetup em alguns computadores, mas as novas instalações do cliente não o baixarão. <!--503654-->


### <a name="how-to-install-the-endpoint-protection-client-on-the-reference-computer"></a>Como instalar o cliente do Endpoint Protection no computador de referência

Instale o cliente do Endpoint Protection localmente no computador de referência usando um prompt de comando. Primeiro, obtenha o arquivo de instalação **scepinstall.exe**. Para obter mais informações, confira [Instalar o cliente do Endpoint Protection usando um prompt de comando](#bkmk_manual-install).

Se necessário, também inclua uma política antimalware pré-configurada ou uma política antimalware que você já tenha exportado. 



## <a name="bkmk_manual-install"></a> Para instalar o cliente do Endpoint Protection usando um prompt de comando

1. Copie **scepinstall.exe** da pasta **Cliente** da pasta de instalação do Configuration Manager para o computador no qual você deseja instalar o software cliente do Endpoint Protection.  

2. Abra um prompt de comando como administrador. Mude de diretório para a pasta que contém o instalador. Em seguida, execute `scepinstall.exe`, adicionando todas as propriedades de linha de comando adicionais necessárias:


   |  Propriedade   |                                  Descrição                                   |
   |-------------|--------------------------------------------------------------------------------|
   |    `/s`     |                           Execute o instalador silenciosamente                           |
   |    `/q`     |                        Extraia os arquivos de instalação silenciosamente                        |
   |    `/i`     |                           Execute o instalador normalmente                           |
   |  `/policy`  | Especifique um arquivo de política antimalware para configurar o cliente durante a instalação |
   | `/sqmoptin` |     Aceite o CEIP (Programa de Aperfeiçoamento da Experiência do Usuário) da Microsoft     |


3. Siga as instruções na tela para concluir a instalação do cliente.  

4. Se você tiver baixado o pacote de definição com atualização mais recente, copie o pacote para o computador cliente e clique duas vezes no pacote de definição para instalá-lo.  

   > [!NOTE]  
   >  Depois que a instalação cliente do Endpoint Protection for concluída, o cliente executará automaticamente uma verificação de atualização da definição. Se essa verificação de atualização for bem-sucedida, você não precisará instalar manualmente o último pacote de atualização da definição.  

#### <a name="example-install-the-client-with-an-antimalware-policy"></a>Exemplo: instalar o cliente com uma política antimalware

`scepinstall.exe /policy <full path>\<policy file>`



## <a name="verify-the-endpoint-protection-client-installation"></a>Verificar a instalação do cliente do Endpoint Protection

Depois de instalar o cliente do Endpoint Protection no seu computador de referência, verifique se o cliente está funcionando corretamente.

1.  No computador de referência, abra **System Center Endpoint Protection** na área de notificação do Windows.  

2.  Na guia **Início** da caixa de diálogo **System Center Endpoint Protection**, verifique se **Proteção em tempo real** está definido como **Ativo**.  

3.  Verifique se a opção **Atualizado** é exibida para **Definições de vírus e spyware**.  

4.  Para confirmar se o computador de referência está pronto para geração de imagens, em **Opções de verificação**, selecione **Completa** e clique em **Verificar agora**.  



## <a name="prepare-the-endpoint-protection-client-for-imaging"></a>Preparar o cliente do Endpoint Protection para geração de imagens

Execute as seguintes etapas para preparar o cliente do Endpoint Protection para geração de imagens:

1. No computador de referência, entre como um administrador.  

2. Baixe e instale **PsExec** de [Windows SysInternals](https://docs.microsoft.com/sysinternals/downloads/psexec).  

3. Execute um prompt de comando como administrador, mude de diretório para a pasta na qual você instalou o PsTools e, em seguida, digite o seguinte comando:  

   `psexec.exe -s -i regedit.exe`  

   > [!IMPORTANT]  
   >  Tenha cuidado ao executar o Editor do Registro dessa maneira. O PsExec.exe o executará no contexto do LocalSystem.  

4. No Editor do Registro, exclua as seguintes chaves do Registro:  

   > [!IMPORTANT]  
   >  Exclua essas chaves do Registro como última etapa antes da geração de imagens do computador de referência. O cliente do Endpoint Protection recriará essas chaves ao ser iniciado. Se você reiniciar o computador de referência, exclua as chaves do Registro novamente.  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID`   

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID`

Agora você está pronto para preparar o computador de referência para geração de imagens.

Quando você implanta uma imagem do sistema operacional que contém o cliente do Endpoint Protection, ele relata informações automaticamente para o site do Configuration Manager atribuído ao dispositivo. O cliente baixa e aplica todas as políticas antimalware necessárias.  



## <a name="see-also"></a>Consulte também

Para obter mais informações sobre a implantação do sistema operacional no Configuration Manager, confira [Gerenciar imagens do sistema operacional](/sccm/osd/get-started/manage-operating-system-images).

