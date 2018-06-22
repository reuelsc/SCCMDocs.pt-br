---
title: Criar perfis de certificado PFX usando uma autoridade de certificação
titleSuffix: Configuration Manager
description: Saiba como usar arquivos PFX no System Center Configuration Manager para gerar certificados específicos do usuário que dão suporte à troca de dados criptografados.
ms.date: 11/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: d240a836-c49b-49ab-a920-784c062d6748
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a186e0b2c4b355cabcaaeb3b3124b65d3588fbc8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32350955"
---
# <a name="how-to-create-pfx-certificate-profiles-using-a-certificate-authority"></a>Como criar perfis de certificado PFX usando uma autoridade de certificação

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Aqui, você aprenderá a criar um perfil de certificado que usa uma autoridade de certificação para credenciais.

[Perfis de certificado](../../protect/deploy-use/introduction-to-certificate-profiles.md) fornece informações gerais sobre como criar e configurar perfis de certificado. Este tópico destaca algumas informações específicas sobre perfis de certificado relacionados aos certificados PFX.

## <a name="pfx-certificate-profiles"></a>Perfis de certificado PFX
O System Center Configuration Manager permite que você crie um perfil de certificado PFX usando credenciais emitidas por uma autoridade de certificação.  A partir da versão 1706, você pode escolher Microsoft ou Entrust como sua autoridade de certificação.  Quando são implantados em dispositivos de usuário, os arquivos de troca de informações pessoais (.pfx) geram certificados específicos do usuário para dar suporte à troca de dados criptografados.

Para importar as credenciais de certificado de arquivos de certificado existentes, confira [Como criar perfis de certificado PFX importando detalhes do certificado](../../mdm/deploy-use/import-pfx-certificate-profiles.md).

## <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Criar e implantar um perfil de certificado PFX (Troca de Informações Pessoais)  

### <a name="get-started"></a>Introdução

1.  No console do System Center Configuration Manager, escolha **Ativos e Conformidade**.  
2.  No espaço de trabalho **Ativos e Conformidade**, escolha **Configurações de Conformidade**, escolha &gt;Acesso ao Recurso da Empresa**e clique em** &gt; **Perfis de Certificado**.  

3.  Na guia **Início**, no grupo **Criar**, escolha **Criar Perfil Certificado**.

4.  Na página **Geral** do Assistente para **Criar Perfil de Certificado** , especifique as seguintes informações:  

    -   **Nome**: insira um nome exclusivo para o perfil de certificado. Você pode usar no máximo 256 caracteres.  

    -   **Descrição**: forneça uma descrição que ofereça uma visão geral do perfil de certificado e outras informações relevantes que ajudem a identificá-lo no console do System Center Configuration Manager. Você pode usar no máximo 256 caracteres.  

    -   Em **Especificar o tipo de perfil de certificado que você deseja criar**, escolha **Troca de Informações Pessoais – Configurações de PKCS #12 (PFX) – Criar** e, depois, escolha sua autoridade de certificação na lista suspensa.  A partir da versão 1706, você pode escolher **Microsoft** ou **Entrust**.

### <a name="select-supported-platforms"></a>Selecionar as plataformas com suporte

A página Plataformas com Suporte identifica os dispositivos e sistemas operacionais para os quais o perfil de certificado dá suporte.  

Os perfis de certificado podem dar suporte a vários sistemas operacionais e dispositivos, no entanto, determinadas combinações de sistema operacional ou dispositivo podem exigir configurações diferentes.  Nesses casos, é melhor criar perfis separados para cada conjunto exclusivo de configurações.  

A partir da versão 1710, as seguintes opções estão disponíveis:

- Windows 10
    - Todos os Windows 10 (64 bits)
    - Todos os Windows 10 (32 bits)
    - Todos os Windows 10 (ARM64)
    - Todos os Windows 10 Holographic Enterprise e mais recentes
    - Todos os Windows 10 Holographic e mais recentes
    - Todos os Windows 10 Team e mais recentes
    - Todos os Windows 10 Mobile e superior
- iPhone
- iPad
- Android
- Android for Work

> [!Note]  
> Atualmente, não há suporte para dispositivos MacOS/OSX.  

Quando nenhuma outra opção estiver selecionada, a caixa de seleção **Selecionar Tudo** selecionará todas as opções disponíveis.  Quando uma ou mais opções forem selecionadas, **Selecionar Tudo** limpará as seleções existentes. 

1.  Selecione uma ou mais plataformas com suporte do perfil de certificado.

1.  Escolha **Avançar** para continuar.  


### <a name="configure-certification-authorities"></a>Configurar autoridades de certificação

Aqui, você pode escolher o ponto de registro de certificado (CRP) para processar os certificados PFX.  

1.  Na lista **Site Primário**, escolha o servidor que contém a função CRP para a autoridade de certificação.
1.  Na lista de **Autoridades de certificação**, escolha a CA relevante colocando uma marca de seleção na coluna esquerda.
1.  Quando estiver pronto para continuar, escolha **Avançar**.

Para saber mais, confira [Infraestrutura do certificado](../../protect/deploy-use/certificate-infrastructure.md).


### <a name="configure-certificate-settings-for-microsoft-ca"></a>Definir configurações de certificado para AC da Microsoft

Para definir configurações do certificado ao usar a Microsoft como a AC:

1.  Na lista suspensa **Nome do modelo de certificado**, escolha o modelo de certificado.

1.  Marque a caixa de seleção **Uso do certificado** para usar o perfil de certificado para assinatura ou criptografia S/MIME.

    Quando você marca essa opção ao usar Microsoft como a AC, todos os certificados PFX associados ao usuário de destino são entregues a todos os dispositivos registrados pelo usuário.  Quando essa caixa de seleção está desmarcada, cada dispositivo recebe um certificado exclusivo.  

1.  Defina **Formato do nome da entidade** como **Nome comum** ou **Nome totalmente distinto**.  Se não tiver certeza de qual usar, contate o administrador da autoridade de certificação.

1.  Para **Nome alternativo da entidade**, habilite o **Endereço de email** e **Nome principal de usuário (UPN)** conforme apropriado para sua AC.

1.  **Limite de renovação** determina quando os certificados são automaticamente renovados, com base na porcentagem de tempo restante antes da expiração.

1.  Defina o **Período de validade do certificado** como o tempo de vida do certificado.  O período é especificado pela configuração de um número (1-100) e do período (anos, meses ou dias).

1.  A **Publicação do Active Directory** é habilitada quando o ponto de registro de certificado especificar credenciais do Active Directory.  Habilite a opção para publicar o perfil de certificado no Active Directory.

1.  Se você selecionou uma ou mais plataformas do Windows 10 ao especificar as plataformas com suporte:

    1.  Defina **Repositório de certificados do Windows** como **Usuário**.  (A opção **Computador Local** não implanta certificados e não deve ser escolhida.)
    1.  Selecione o **Provedor de Armazenamento de Chave (KSP)** de uma das seguintes opções:

        - **Instalar em um TPM (Trusted Platform Module), se houver**  
        - **Instalar em um TPM (Trusted Platform Module); caso contrário, ocorrerá uma falha** 
        - **Instalar para o Windows Hello para Empresas, caso contrário, falhará** 
        - **Instalar o Provedor de Armazenamento de Chaves de Software** 

1.  Quando terminar, escolha **Avançar** ou **Resumo**.

### <a name="configure-certificate-settings-for-entrust-ca"></a>Definir as configurações de certificado para a AC Entrust

Para definir as configurações de certificado ao usar Entrust como a AC:

1.  Na lista suspensa **Configuração de ID Digital**, escolha o perfil de configuração.  As opções de configuração de ID digital são criadas pelo administrador Entrust.

1.  Quando marcada, a opção **Uso do certificado** usa o perfil de certificado para assinatura ou criptografia S/MIME.

    Ao usar o Entrust como a AC, todos os certificados PFX associados ao usuário de destino são entregues a todos os dispositivos registrados pelo usuário.    Quando essa opção *não* é marcada, cada dispositivo recebe um certificado exclusivo.  (Alterações de comportamento para CAs diferentes; para saber mais, confira a seção correspondente.)

1.  Use o botão **Formato** para mapear tokens de **Formato de nome de entidade** do Entrust para campos do ConfigMgr.  

    A caixa de diálogo **Formatação de Nome de Certificado** lista as variáveis de configuração de ID Digital do Entrust.  Para cada variável do Entrust, escolha a variável LDAP apropriada na lista suspensa associada.

1.  Use o botão **Formato** para mapear tokens de **Nome Alternativo da Entidade** do Entrust para variáveis LDAP com suporte.  

    A caixa de diálogo **Formatação de Nome de Certificado** lista as variáveis de configuração de ID Digital do Entrust.  Para cada variável do Entrust, escolha a variável LDAP apropriada na lista suspensa associada.

1.  **Limite de renovação** determina quando os certificados são automaticamente renovados, com base na porcentagem de tempo restante antes da expiração.

1.  Defina o **Período de validade do certificado** como o tempo de vida do certificado.  O período é especificado pela configuração de um número (1-100) e do período (anos, meses ou dias).

1.  A **Publicação do Active Directory** é habilitada quando o ponto de registro de certificado especificar credenciais do Active Directory.  Habilite a opção para publicar o perfil de certificado no Active Directory.

1.  Se você selecionou uma ou mais plataformas do Windows 10 ao especificar as plataformas com suporte:

    1.  Defina **Repositório de certificados do Windows** como **Usuário**.  (A opção **Computador Local** não implanta certificados e não deve ser escolhida.)
    1.  Selecione o **Provedor de Armazenamento de Chave (KSP)** de uma das seguintes opções:

        - **Instalar em um TPM (Trusted Platform Module), se houver**  
        - **Instalar em um TPM (Trusted Platform Module); caso contrário, ocorrerá uma falha** 
        - **Instalar para o Windows Hello para Empresas, caso contrário, falhará** 
        - **Instalar o Provedor de Armazenamento de Chaves de Software** 

1.  Quando terminar, escolha **Avançar** ou **Resumo**.


### <a name="finish-up"></a>Concluir

1.  Na página Resumo, revise suas seleções e verifique suas escolhas.

1.  Quando estiver pronto, escolha **Avançar** para criar o perfil.  

1.  O perfil de certificado que contém o arquivo PFX agora está disponível do espaço de trabalho **Perfis de Certificado** . 

1.  Para implantar o perfil:

    1. Abra o espaço de trabalho **Ativos e Conformidade**.
    1. Escolha **Configurações de Conformidade** > **Acesso aos Recursos da Empresa** > **Perfis de Certificado**
    1. Clique o perfil de certificado desejado e escolha **Implantar**. 


## <a name="see-also"></a>Consulte também
[Criar um novo perfil de certificado](../../protect/deploy-use/create-certificate-profiles.md) orienta você pelo Assistente para criar perfil de certificado.

[Como criar perfis de certificado PFX importando detalhes do certificado](../../mdm/deploy-use/import-pfx-certificate-profiles.md)

[Implantar perfis de Wi-Fi, VPN, email e de certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) descreve como implantar perfis de certificado.