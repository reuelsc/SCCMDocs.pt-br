---
title: Suporte do servidor proxy
titleSuffix: Configuration Manager
description: Saiba mais sobre o suporte do System Center Configuration Manager para servidores proxy usados pelos servidores de sistema de sites e clientes.
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 909c56f6087b6ed7b6600b6f3fc693dbd5b4d1b5
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="proxy-server-support-in-system-center-configuration-manager"></a>Suporte do servidor proxy no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os clientes e os servidores do sistema de sites do System Center Configuration Manager podem usar um servidor proxy.  

## <a name="site-system-servers"></a>Servidores de sistema de sites  
Quando as funções do sistema de sites precisarem se conectar à Internet, você pode configurá-las para usar um servidor proxy.  

-   Um computador que hospeda um servidor de sistema de sites dá suporte a uma configuração de servidor proxy único que é compartilhado por todas as funções do sistema de sites no mesmo computador. Se precisar de servidores proxy separados para diferentes funções ou instâncias de uma função, você deverá colocar essas funções em servidores de sistema de sites separados.  

-   Quando você define novas configurações de servidor proxy para um servidor de sistema de sites que já tem uma configuração de servidor proxy, a configuração original é substituída.  

-   Conexões com o proxy usam a conta de **Sistema** do computador que hospeda a função de sistema de sites.  

As seguintes funções do sistema de sites se conectam à Internet e podem exigir um servidor proxy.  Com uma exceção, as funções de sistema de sites que podem usar um proxy o fazem sem nenhuma configuração adicional. A exceção é o ponto de atualização de software. A lista a seguir contém informações sobre as configurações adicionais que um ponto de atualização de software requer:  

**Ponto de sincronização do Asset Intelligence**: essa função do sistema de sites conecta-se à Microsoft e usa uma configuração de servidor proxy no computador que hospeda o ponto de sincronização do Asset Intelligence.  

**Ponto de distribuição baseado em nuvem**: para configurar um servidor proxy para um ponto de distribuição baseado em nuvem, você deve configurar o proxy no site primário que gerencia o ponto de distribuição baseado em nuvem.  

Para essa configuração, o servidor do site primário:  

-   Deve ser capaz de se conectar ao Microsoft Azure para configurar, monitorar e distribuir conteúdo para o ponto de distribuição.  

-   Usa a conta de sistema do computador para fazer a conexão.  

-   Usa o navegador da Web padrão do computador.  

Não é possível configurar um servidor proxy em um ponto de distribuição baseado em nuvem no Microsoft Azure.  

**Ponto de conexão de nuvem**: essa função do sistema de sites conecta-se ao serviço de nuvem do Configuration Manager para baixar atualizações de versão do Configuration Manager, e usa um servidor proxy configurado no computador que hospeda o ponto de conexão de serviço.  

**Conector do Exchange Server**: essa função do sistema de sites conecta-se a um Exchange Server e usa uma configuração de servidor proxy no computador que hospeda o conector do Exchange Server.  

**Ponto de conexão de serviço**: essa função do sistema de sites conecta-se ao Microsoft Intune e usa uma configuração de servidor proxy no computador que hospeda o ponto de conexão de serviço.  

**Ponto de atualização de software** - essa função do sistema de sites pode usar o proxy quando se conecta ao Microsoft Update para baixar patches e sincronizar informações sobre atualizações. Os pontos de atualização de software só usam um proxy para as duas opções a seguir quando você habilita essa opção durante a configuração do ponto de atualização de software:  

-   **Usar um servidor proxy ao sincronizar atualizações de software**  

-   **Usar um servidor proxy ao baixar conteúdo usando regras de implantação automática** (embora esteja disponível para uso, esta configuração não é usada por pontos de atualização de software em sites secundários.)  

Definir as configurações do servidor proxy na página de Ponto de atualização de software ativo do Assistente para Adicionar funções do sistema de sites ou na guia **Geral** nas **Propriedades do componente de ponto de atualização de software**.  

-   As configurações do servidor proxy estão associadas apenas com o ponto de atualização de software no site.  

-   Opções de servidor proxy estão disponíveis somente quando já existe um servidor proxy configurado para o servidor do sistema de sites que hospeda o ponto de atualização de software.  

> [!NOTE]  
>  Por padrão, a conta de **Sistema** do servidor em que uma regra de implantação automática foi criada é usada para conectar-se à Internet e baixar atualizações de software quando as regras de implantação automática forem executadas.  
>   
>  Quando essa conta não tem acesso à Internet, as atualizações de software não são baixadas e a seguinte entrada é registrada em ruleengine.log: **Falha ao baixar a atualização da Internet. Erro = 12007.**  

#### <a name="to-set-up-the-proxy-server-for-a-site-system-server"></a>Para configurar o servidor proxy para um servidor do sistema de sites  

1.  No console do Configuration Manager, clique em **Administração**, expanda **Configuração do Site** e clique em **Funções de Servidores e Sistema de Site**.  

2.  Selecione o servidor do sistema de sites que você deseja editar; no painel de detalhes, clique com o botão direito do mouse em **Sistema de site** e clique em **Propriedades**.  

3.  Em Propriedades do Sistema de site, selecione a guia **Proxy** e defina as configurações de proxy para esse servidor do site primário.  

4.  Clique em **OK** para salvar a nova configuração do servidor proxy.  
