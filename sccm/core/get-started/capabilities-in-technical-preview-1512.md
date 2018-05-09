---
title: Recursos no Technical Preview 1512
titleSuffix: Configuration Manager
description: Saiba mais sobre os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1512.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e4d9e414-1346-4ed4-85d0-64d602b68731
author: aczechowski
robots: noindex,nofollow
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 939a767820983c1fe2d575d7a745d6dabb45f25c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="capabilities-in-technical-preview-1512-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1512 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1512. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview. Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de um technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos em um technical preview.  

 Veja a seguir os novos recursos que você pode experimentar nesta versão.  

##  <a name="bkmk_devicehealth"></a> Atestado de integridade do dispositivo  
 Começando com o Technical Preview 1512, os administradores podem ver o status do atestado de integridade de dispositivo Windows 10 no console do Configuration Manager.  Essa funcionalidade está disponível para o Configuration Manager e o Configuration Manager com o Microsoft Intune. O atestado de integridade do dispositivo permite que o administrador garanta que os computadores cliente têm configurações confiáveis de BIOS, TPM e software de inicialização. Para dar suporte de atestado de integridade do dispositivo, os dispositivos do cliente devem estar executando o Win10 com o TPM 2 habilitado. O atestado de integridade do dispositivo exibe o número de dispositivos habilitados para cada um dos seguintes:  

-   Antimalware de inicialização antecipada  

-   BitLocker  

-   Inicialização Segura  

-   Integridade do código  

O console também exibe as principais configurações de atestado de integridade ausentes com o número de dispositivos.  

Para visualizar a exibição do atestado de integridade do dispositivo no console do Configuration Manager, acesse o espaço de trabalho **Monitoramento**, clique no nó **Segurança** e clique em **Atestado de Integridade**.  

##  <a name="bkmk_viewterms"></a> Monitoramento no console dos termos e condições  
A partir do Technical Preview 1512, ao integrar o Configuration Manager ao Microsoft Intune, você poderá usar o console do Configuration Manager para ver quais usuários aceitaram os termos e condições configurados pelo departamento de TI, e quais não aceitaram.  

**Para exibir informações de resumo:**  

-   No console do Configuration Manager, acesse **Monitoramento** > **Visão Geral** > **Implantações** e selecione a implantação de termos e condições que você deseja exibir.  

**Para exibir informações detalhadas:**  

1.  No console do Configuration Manager, acesse **Ativos e Conformidade** > **Visão Geral** > **Configurações de Conformidade** > **Termos e Condições** e selecione os termos e condições que você deseja exibir.  

2.  Na parte inferior do console, selecione a guia **Implantações**, selecione a implantação e clique em **Exibir Status.**  

##  <a name="bkmk_EPpolicy"></a> Aprimoramentos nas configurações da política do Endpoint Protection  
Na Visualização Técnica 1512, adicionamos as seguintes novas configurações na política antimalware do Endpoint Protection:  

-   Proteção em tempo real: **Bloco de aplicativos potencialmente indesejados no download e antes da instalação**  

    -   PUA (Aplicativos Potencialmente Indesejados) é uma classificação de risco com base na reputação e identificação voltadas para a pesquisa. Normalmente, esses são agregadores de aplicativos indesejados ou seus aplicativos empacotados.  

    -   A configuração de política de proteção está habilitada (definida como "Sim") por padrão. Quando habilitada, essa configuração impede PUA no momento de download e instalação. No entanto, você pode excluir arquivos específicos ou pastas para atender às necessidades específicas do seu ambiente.  

-   Configurações de verificação: **Verificação de unidades de rede mapeadas ao executar uma verificação completa**  

    -   Essa configuração fornece maior granularidade ao administrador para permitir verificações sob demanda de arquivos de rede sem o risco de sempre verificar unidades de rede mapeadas durante uma verificação completa agendada.  

    -   A configuração **Verificar arquivos de rede** deve primeiro ser habilitada (“Sim”) para que essa configuração esteja disponível para configurar.  

    -   Por padrão, essa configuração é definida como "Não", o que significa que uma verificação completa não acessará as unidades de rede mapeadas.  

-   Configurações de envio de arquivo de exemplo automático:  

     O mecanismo antimalware pode solicitar que amostras de arquivo sejam enviadas à Microsoft para análise posterior. Por padrão, ele solicitará sempre antes de enviar esses exemplos. Os administradores agora podem gerenciar as configurações a seguir para configurar esse comportamento:  

    -   Avançado ‑ **Permitir o envio de arquivo de amostra automático para ajudar a Microsoft a determinar se certos itens detectados são maliciosos**: altere essa configuração para "Sim" para habilitar o envio automático de amostra. Por padrão, essa configuração é "Não", o que significa que o envio automático de amostra está desabilitado e os usuários serão avisados antes do envio de amostras.   (Essa configuração foi introduzida no System Center 2012 R2 Configuration Manager SP1)  

    -   Avançado ‑ **Permitir que usuários modifiquem configurações de envio do arquivo de amostra automática**: essa configuração determina se um usuário com direitos administrativos em um dispositivo pode alterar a configuração de envio do arquivo de amostra automática na interface do cliente. Por padrão, essa configuração é definida como “Não”, o que significa que as configurações só podem ser alteradas no console do Configuration Manager e os administradores locais em um dispositivo não podem alterar essa configuração.  

         Por exemplo, o código a seguir mostra a configuração do Windows Defender no Windows 10 definida pelo administrador como habilitada e o usuário não tem permissão para modificá-la:  

         ![TechRef&#95;WinDefender](../../core/get-started/media/TechRef_WinDefender.png "TechRef_WinDefender")  

    Além disso, a configuração existente **Excluir arquivos e pastas** na seção "Configurações de exclusão" da política antimalware do Endpoint Protection foi aprimorada para permitir exclusões de dispositivo. Por exemplo, agora você pode especificar o seguinte como uma exclusão: **\device\mvfs** (para o sistema de arquivos Multiversion). A política não valida o caminho do dispositivo; a política do Endpoint Protection é fornecida ao mecanismo antimalware do cliente que deve ser capaz de interpretar a cadeia de caracteres do dispositivo.  

**Pré-requisitos para usar as políticas do Endpoint Protection:**  

Antes de usar as políticas do Endpoint Protection, você deve instalar e gerenciar o cliente Endpoint Protection usando as configurações de cliente do Endpoint Protection. Isso é feito usando o cliente do System Center Endpoint Protection para Windows 7, Windows 8, Windows 8.1 ou Windows Defender para Windows 10 gerenciado. Consulte [Endpoint Protection no System Center Configuration Manager](../../protect/deploy-use/endpoint-protection.md).  
