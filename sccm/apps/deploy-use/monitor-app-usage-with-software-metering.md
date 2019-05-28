---
title: Monitorar o uso de aplicativos com a medição de software
titleSuffix: Configuration Manager
description: Saiba mais sobre as operações que estão disponíveis na medição de software do System Center Configuration Manager.
ms.date: 09/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b1fdaee2-2816-4447-94cd-609f6948f215
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 652c10cfcb4d53b32409dd5af83e7d55f2676463
ms.sourcegitcommit: f531d0a622f220739710b2fe6644ea58d024064a
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65933474"
---
# <a name="software-metering-in-system-center-configuration-manager"></a>Medição de software no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico contém uma referência para todas as operações que você pode executar ao usar a medição de software do System Center Configuration Manager.

> [!IMPORTANT]
>  A medição de software é usada para monitorar aplicativos de desktop para PCs com Windows com um nome de arquivo que termina em **.exe**. A medição de software não monitora aplicativos modernos do Windows (como aqueles usados pelo Windows 8).

##  <a name="prerequisites-for-software-metering"></a>Pré-requisitos para a medição de software
A medição de software não tem dependências externas, apenas dependências internas no produto.

|Dependência|Mais informações|
|----------------|----------------------|
|Configurações do cliente para a medição de software.|Para usar a medição de software, a configuração do cliente **Habilitar medição de software em clientes** deve estar habilitada e implantada nos computadores. Você pode implantar as configurações de medição de software em todos os computadores na hierarquia ou implantar configurações personalizadas em grupos de computadores. Consulte **Configurar a medição de software** neste tópico.|
|O ponto do Reporting Services.|É necessário configurar um ponto do Reporting Services antes de exibir relatórios de medição de software. Para obter mais informações, consulte [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).|

##  <a name="configure-software-metering"></a>Configurar medição de software
 Este procedimento define as configurações padrão do cliente para a medição de software e se aplica a todos os computadores em sua hierarquia. Se quiser que essas configurações se apliquem somente a alguns computadores, crie uma configuração personalizada do cliente de dispositivo e a implante em uma coleção que contém os computadores nos quais deseja usar a medição de software. Para obter mais informações sobre como criar configurações personalizadas do dispositivo, consulte [Definir as configurações do cliente](../../core/clients/deploy/configure-client-settings.md).

1. No console do Configuration Manager, clique em **Administração** > **Configurações do Cliente** > **Configurações do Cliente Padrão**.

2. Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.

3. Na caixa de diálogo **Configurações Padrão** , clique em **Medição de Software**.

4. Na lista **Configurações do Dispositivo** , configure o seguinte:

   -   **Habilitar medição de software em clientes**: selecione **True** para habilitar a medição de software.

   -   **Agendar coleta de dados**: configure a frequência com que os dados de medição de software são coletados dos computadores cliente. Use o valor padrão de cada **7 dias** ou clique em **Agendamento** para especificar um agendamento personalizado.

5. Clique em **OK** para fechar a caixa de diálogo **Configurações Padrão** .

   Os computadores cliente são definidos com essas configurações na próxima vez que baixarem a política do cliente. Para iniciar a recuperação de política para um cliente individual, consulte [Gerenciar clientes](../../core/clients/manage/manage-clients.md).

##  <a name="create-software-metering-rules"></a>Criar regras de medição de software
 Use o assistente para Criar Regra de Medição de Software para criar uma nova regra de medição de software para seu site do Configuration Manager.

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Medição de Software**.

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Regra de Medição de Software**.

4.  Na página **Geral** do assistente para Criar Regra de Medição de Software, especifique as seguintes informações:

    -   **Nome** - O nome da regra de medição de software. Isso deve ser exclusivo e descritivo.

        > [!NOTE]
        >  As regras de medição de software podem compartilhar o mesmo nome se o nome de arquivo contido nas regras for diferente.

    -   **Nome do Arquivo** - O nome do arquivo de programa que deseja medir. Você pode clicar em **Procurar** para exibir a caixa de diálogo **Abrir** , na qual é possível selecionar o arquivo de programa a ser usado.

        > [!NOTE]
        >  Se você digitar o nome do arquivo executável na caixa **Nome de arquivo** , nenhuma verificação será executada para determinar se esse arquivo existe ou se ele contém as informações de cabeçalho necessárias. Quando possível, clique em **Procurar** e selecione o arquivo executável a ser medido.
        >
        >  Caracteres curinga não são permitidos no nome do arquivo.
        >
        >  Essa caixa será opcional se um valor para **Nome do arquivo original** for especificado.

    -   **Nome do arquivo original** - O nome do arquivo executável que deseja medir. Esse nome corresponde às informações no cabeçalho do arquivo, e não ao nome do próprio arquivo, para que ele possa ser útil em casos em que o arquivo executável foi renomeado, mas você deseja medi-lo pelo nome original.

        > [!NOTE]
        >  Caracteres curinga não são permitidos no nome do arquivo original.
        >
        >  Essa caixa será opcional se um valor para **Nome de Arquivo** for especificado.

    -   **Versão** - A versão do arquivo executável que deseja medir. Você pode usar o caractere curinga ( &#42; ) para representar qualquer cadeia de caracteres ou o caractere curinga ( ? ) para representar qualquer caractere único. Se quiser medir todas as versões de um arquivo executável, use o valor padrão ( &#42; ).

    -   **Idioma** - O idioma do arquivo executável a ser medido. O valor padrão é a localidade atual do sistema operacional que está sendo usado. Se você selecionar um arquivo executável para ser monitorado clicando no botão **Procurar** , essa caixa será preenchida automaticamente se as informações de idioma estiverem presentes no cabeçalho do arquivo. Para medir todas as versões de idioma de um arquivo, selecione **Qualquer** na lista suspensa.

    -   **Descrição** - Uma descrição opcional para a regra de medição de software.

    -   **Aplicar esta regra de medição de software aos seguintes clientes** – Selecione se deseja aplicar a regra de medição de software a todos os clientes na hierarquia ou aos clientes que foram atribuídos ao site especificado na lista **Site** .

5.  Para continuar, clique em **Avançar**.

6.  Examine e confirme as configurações e conclua o assistente para criar a regra de medição de software. As regras de medição de software novo é exibido no nó **Medição de Software** no workspace **Ativos e Conformidade**.

##  <a name="configure-automatic-software-metering-rules"></a>Configurar regras de medição de software automáticas
 Você pode configurar a medição de software no Configuration Manager para gerar automaticamente regras de medição de software desabilitadas dos dados de inventário de uso recentes mantidos no banco de dados do site. Você pode configurar esses dados de inventário para que sejam criadas regras de medição somente para os aplicativos que são usados em um percentual especificado de computadores. Você também pode especificar o número máximo de regras de medição de software geradas automaticamente permitidas no site.

> [!NOTE]
>  Por padrão, as regras de medição de software que são criadas automaticamente são desabilitadas. Antes de começar a coletar dados de uso dessas regras, você deve habilitá-las.

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Medição de Software** e, na guia **Início**, no grupo **Configurações**, clique em **Propriedades de Medição de Software**.

3.  Na caixa de diálogo **Propriedades de Medição de Software** , configure o seguinte:

    -   **Retenção de dados (em dias)** -Especifica a quantidade de tempo que os dados gerados pelas regras de medição de software são mantidos no banco de dados do site. O valor padrão é **90** dias.

    -   Habilite a opção **Criar automaticamente regras de medição desabilitadas dos dados de inventário de uso recente**.

    -   **Especificar o percentual de computadores na hierarquia que devem usar um programa antes que uma regra de medição de software seja criada automaticamente** - O valor padrão é **10%** .

    -   **Especificar o número de regras de medição de software que devem ser excedidas na hierarquia antes que a criação automática de regras seja desabilitada** - O valor padrão é **100** regras.

4.  Clique em **OK** para fechar a caixa de diálogo **Propriedades de Medição de Software** .

##  <a name="manage-software-metering-rules"></a>Gerenciar regras de medição de software
 No workspace **Ativos e Conformidade**, selecione **Medição de Software**, selecione a regra de medição de software a ser gerenciada e uma tarefa de gerenciamento.

 Use a tabela a seguir para obter mais informações sobre as tarefas de gerenciamento que podem requerer informações adicionais antes de você selecioná-las.

|Tarefa de gerenciamento|Detalhes|
|---------------------|-------------|
|**Habilitar**<br /><br /> **Desabilitar**|Habilita ou desabilita um regra de medição de software. Essa configuração é baixada para computadores cliente de acordo com o **Intervalo de sondagem da política do cliente** na seção **Política do cliente** das configurações do cliente (por padrão, a cada 60 minutos).<br /><br /> Consulte [Definir as configurações do cliente](../../core/clients/deploy/configure-client-settings.md).|

##  <a name="monitor-software-metering"></a>Monitorar a medição de software
 A medição de software no Configuration Manager inclui vários relatórios internos que permitem monitorar informações sobre operações de medição de software. Esses relatórios contêm a categoria de relatório **Medição de software**.

 Para obter mais informações sobre como configurar relatórios no Configuration Manager, consulte [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).

 Além disso, você pode criar consultas e coleções com base nos dados armazenados no banco de dados do Configuration Manager por meio da medição de software.

 Para obter mais informações sobre coleções no Configuration Manager, consulte [Introdução a coleções](/sccm/core/clients/manage/collections/introduction-to-collections).

 Para obter mais informações sobre consultas no Configuration Manager, consulte [Introdução a consultas](/sccm/core/servers/manage/introduction-to-queries).

##  <a name="security-and-privacy-for-software-metering"></a>Segurança e privacidade da medição de software

### <a name="security-issues-for-software-metering"></a>Problemas de segurança para a medição de software
 Um invasor pode enviar informações de medição de software inválidas para o Configuration Manager, que serão aceitas pelo ponto de gerenciamento mesmo quando a configuração do cliente de medição de software estiver desabilitada. Isso poderá resultar em um grande número de regras de medição que são replicadas em toda a hierarquia, provocando uma negação de serviço na rede e aos servidores do site do Configuration Manager.

 Como um invasor pode criar dados de medição de software inválidos, não considere confiáveis as informações de medição de software.

 Medição de software está habilitada por padrão como uma configuração de cliente.

###  <a name="privacy-information-for-software-metering"></a>Informações de privacidade para medição de Software
 Medição de software monitora o uso de aplicativos em computadores cliente. A medição de software é habilitada por padrão. É necessário configurar os aplicativos a ser medidos. As informações da medição são armazenadas no banco de dados do Configuration Manager. As informações são criptografadas durante a transferência para um ponto de gerenciamento, mas não são armazenadas em formato criptografado no banco de dados do Configuration Manager.

 Essas informações são mantidas no banco de dados até que sejam excluídas pelas tarefas de manutenção do site **Excluir Dados Antigos de Medição de Software** (a cada cinco dias) e **Excluir Dados Antigos de Resumo de Medição de Software** (a cada 270 dias). Você pode configurar o intervalo de exclusão. As informações de medição não são enviadas à Microsoft.

 Antes de configurar a medição de software, considere seus requisitos de privacidade.

## <a name="example-scenario-for-using-software-metering"></a>Cenário de exemplo de uso da medição de software
 Nesta seção, você criará uma regra de medição de software de exemplo que pode ajudá-lo a resolver os seguintes requisitos de negócios:

- Determinar quantas cópias de um determinado aplicativo estão em sua empresa

- Descobrir quaisquer cópias não utilizadas de um aplicativo

- Determinar quais usuários usam um determinado aplicativo regularmente

  O Woodgrove Bank implantou o Microsoft Office 2010 como seu conjunto de produtividade do office padrão. No entanto, para dar suporte a um aplicativo herdado, alguns computadores devem continuar executando o Microsoft Office Word 2003. O departamento de TI deseja reduzir os custos de licenciamento e suporte removendo essas cópias do Word 2003 se o aplicativo herdado não for mais utilizado. O suporte técnico também deseja identificar os usuários que usam o aplicativo herdado.

  O gerente de sistemas de TI do Woodgrove Bank usa a medição de software no Configuration Manager para atingir esses objetivos de negócios. O administrador executa as seguintes ações:

- Verifica os pré-requisitos da medição de software e confirma que o ponto do Reporting Services está instalado e operacional.
- Define as configurações do cliente padrão para a medição de software:<br>O administrador habilita a medição de software e usa a agenda de coleta de dados padrão de uma vez a cada sete dias.<br>O administrador configura inventário de software para arquivos de inventário que têm a extensão .exe definindo a configuração do cliente de inventário de software como **Inventariar esses tipos de arquivo**.<br>O administrador adiciona um novo regra de medição de software, chamada **woodgrove.exe**, para monitorar o aplicativo herdado.
- Aguarde sete dias, após os quais os computadores cliente começam a relatar os dados de uso para o executável **woodgrove.exe**.
- O administrador usa o relatório **Base de instalação de todos os programas de software medidos** do Configuration Manager para ver quais computadores têm o aplicativo **woodgrove.exe** carregado.
- Depois de seis meses, o administrador executa o relatório **Computadores que têm um programa medido instalado mas não executaram o programa desde uma data especificada**, especificando a regra de medição de software e uma data seis meses no passado. Este relatório identifica 120 computadores que não executaram o programa nos últimos seis meses.
- O administrador faz algumas verificações adicionais para confirmar que o aplicativo herdado não é necessário nos computadores identificados. O administrador desinstala o aplicativo herdado e a cópia do Word 2003 desses computadores.<br>O administrador executa o relatório **Usuários que executaram um programa de software medido específico** para fornecer à assistência técnica uma lista de usuários que continuam usando o aplicativo herdado.
- O administrador continua verificando os relatórios de medição de software semanalmente e toma medidas corretivas, se necessário.

  Como resultado deste curso de ação, os custos de licenciamento e suporte de TI são reduzidos removendo os aplicativos que não são mais necessários. Além disso, o suporte técnico agora tem a lista que gostaria de ter com os usuários que executam o aplicativo herdado.
