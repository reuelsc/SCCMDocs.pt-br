---
title: Certificados e segurança
titleSuffix: Configuration Manager
description: Gerenciar certificados e segurança para o System Center Updates Publisher
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: a7f91e63-4750-402e-9970-dd14be7f76a3
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 045a1daef8da0863ed7957ce4c9d3d48cfacca64
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65496187"
---
# <a name="manage-certificates-and-security-for-updates-publisher"></a>Gerenciar certificados e segurança para o Updates Publisher

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os procedimentos a seguir podem ajudar você a configurar o repositório de certificados no servidor de atualização, configurar um certificado autoassinado no computador cliente e configurar a Política de Grupo para permitir que o Windows Update Agent nos computadores verifique se há atualizações de publicação.

## <a name="configure-the-certificate-store-on-the-update-server"></a>Configurar o armazenamento de certificados no servidor de atualização
 O Updates Publisher usa um certificado digital para assinar as atualizações nos catálogos nos quais publica. Antes de publicar um catálogo no servidor de atualização, esse certificado deve estar no repositório de certificados do servidor de atualização e no repositório de certificados do computador do Updates Publisher, se esse computador for remoto com relação ao servidor de atualização.

O procedimento a seguir é um dos vários métodos possíveis para adicionar o certificado ao repositório de certificados no servidor de atualização.

### <a name="to-configure-the-certificate-store"></a>Para configurar o repositório de certificados
1.  Em um computador que possa acessar o computador do Updates Publisher e o servidor de atualização, clique em **Iniciar**, em **Executar**, digite **MMC** na caixa de texto e clique em **OK** para abrir o MMC (Console de Gerenciamento da Microsoft).

2.  Clique em **Arquivo**, clique em **Adicionar/Remover Snap-in**, clique em **Adicionar**, em **Certificados**, clique em **Adicionar**, selecione **Conta do computador** e clique em **Avançar**.

3.  Selecione **Outro computador**, digite o nome do servidor de atualização ou clique em **Procurar** para localizar o computador do servidor de atualização, clique em **Concluir**, em **Fechar** e clique em **OK**.

4.  Expanda **Certificados (*nome do servidor de atualização*)**, expanda **WSUS** e, em seguida, clique em **Certificados**.

5.  No painel de resultados, clique com o botão direito no certificado desejado, clique em **Todas as Tarefas** e clique em **Exportar**.

6.  No Assistente para Exportar Certificados, use as configurações padrão para criar um arquivo de exportação com o nome e o local especificados no assistente. Esse arquivo deve estar disponível para o servidor de atualização antes de prosseguir para a próxima etapa.

7.  Clique com botão direito em **Editores Confiáveis**, clique em **Todas as Tarefas** e, em seguida, clique em **Importar**. Conclua o Assistente para Importar Certificados usando o arquivo exportado na etapa 6.

8.  Se um certificado autoassinado for usado, como **Editores WSUS Autoassinados**, clique com botão direito em **Autoridades de Certificação Raiz Confiáveis**, clique em **Todas as Tarefas** e, em seguida, clique em **Importar**. Conclua o Assistente para Importar Certificados usando o arquivo exportado na etapa 6.

9.  Clique com o botão direito do mouse em **Certificados (*nome do servidor de atualização*)**, clique em **Conectar a outro computador**, insira o nome do computador do Updates Publisher e clique em **OK**.

10. Se o Updates Publisher for remoto com relação ao servidor de atualização, repita as etapas 7 a 9 para importar o certificado para o repositório de certificados no computador do Updates Publisher.



## <a name="configure-a-self-signing-certificate-on-client-computers"></a>Configurar um certificado autoassinado em computadores cliente
Em computadores cliente, o WUA (Windows Update Agent) verifica se há atualizações no catálogo. Esse processo não conseguirá instalar as atualizações quando o agente não conseguir localizar o certificado digital no repositório de Editores Confiáveis no computador local. Se um certificado autoassinado tiver sido usado para publicar o catálogo de atualizações, como os **Editores WSUS Autoassinados**, o certificado também deverá estar no repositório de certificados das Autoridades de Certificação Raiz Confiáveis no computador local para que o agente verifique a validade do certificado.

Você pode usar um dentre vários métodos para configurar certificados em computadores cliente, como usar a Política de Grupo e o **Assistente para Importar Certificados**, ou usando a distribuição de software e a ferramenta Certutil.

Veja a seguir um exemplo de como configurar o certificado de autenticação em computadores cliente.

### <a name="to-configure-a-self-signing-certificate-on-client-computers"></a>Para configurar um certificado autoassinado em computadores cliente
1. Em um computador com acesso ao servidor de atualização, clique em **Iniciar**, em **Executar**, digite **MMC** na caixa de texto e clique em **OK** para abrir o MMC (Console de Gerenciamento da Microsoft).

2. Clique em **Arquivo**, clique em **Adicionar/Remover Snap-in**, clique em **Adicionar**, em **Certificados**, clique em **Adicionar**, selecione **Conta do computador** e clique em **Avançar**.

3. Selecione **Outro computador**, digite o nome do servidor de atualização ou clique em **Procurar** para localizar o computador do servidor de atualização, clique em **Concluir**, em **Fechar** e clique em **OK**.

4. Expanda **Certificados (*nome do servidor de atualização*)**, expanda **WSUS** e, em seguida, clique em **Certificados**.

5. Clique com o botão direito no certificado no painel de resultados, clique em **Todas as Tarefas** e clique em **Exportar**. Complete o **Assistente para Exportar Certificados** usando as configurações padrão para criar um arquivo de certificado de exportação com o nome e o local especificados no assistente.

6. Use um dos métodos a seguir para adicionar o certificado usado para assinar o catálogo de atualizações para cada computador cliente que usará o WUA para verificar a existência de atualizações no catálogo. Adicione o certificado no computador cliente da seguinte maneira:

   -   Para os certificados autoassinados: adicione o certificado aos repositórios de certificado **Autoridades de Certificação Raiz Confiáveis** e **Editores Confiáveis**.

   -   Para certificados emitidos por uma CA (autoridade de certificação): adicione o certificado ao repositório de certificados **Editores Confiáveis**.

   > [!NOTE]
   > O WUA também verifica se a configuração **Permitir conteúdo assinado da política de grupo de local do serviço de atualização da intranet da Microsoft** está habilitada no computador local. Essa configuração da política deve ser habilitada para que o WUA procure atualizações que foram criadas e publicadas com o Updates Publisher. Para saber mais sobre como habilitar essa configuração de Política de Grupo, confira [Como configurar a Política de Grupo em computadores cliente](<https://technet.microsoft.com/library/bb530967.aspx(d=robot>).



## <a name="configuring-group-policy-to-allow-wuaon-computers-to-scan-for-published-updates"></a>Configurar a Política de Grupo para permitir que o WUA em computadores verifique se há atualizações publicadas
Antes de o WUA (Windows Update Agent) nos computadores verificarem se há atualizações que foram criadas e publicadas com o Updates Publisher, habilite uma configuração de política para permitir um conteúdo assinado da localização do serviço de atualização da intranet da Microsoft. Habilitada a configuração de política, o WUA aceitará as atualizações recebidas através de uma localização de intranet se as atualizações estiverem assinadas no repositório de certificados de **Editores Confiáveis** no computador local. Há vários métodos para configurar a Política de Grupo em computadores no ambiente.

Para computadores que não estão no domínio, é possível configurar uma chave do Registro que permite conteúdo assinado de um local de serviço da intranet do Microsoft Update.

Os procedimentos a seguir fornecem as etapas básicas que podem ser usadas para configurar a Política de Grupo para computadores no domínio, e um valor de chave do Registro em computadores que não estão no domínio.

### <a name="to-configure-group-policy-to-allow-wua-to-scan-for-published-updates"></a>Para configurar a Política de Grupo a fim de permitir que o WUA verifique se há atualizações publicadas
1.  Abra o snap-in do MMC (Console de Gerenciamento Microsoft) do Editor de Objetos da Política de Grupo com um usuário que tenha os direitos de segurança apropriados para configurar a Política de Grupo.

2.  Clique em **Procurar** e selecione o domínio, a UO ou os GPOs vinculados ao site no qual a Política de Grupo configurada será propagada para os computadores cliente desejados. Clique em **OK**, clique em **Concluir**, em **Fechar** e clique em **OK**.

3.  Expanda a configuração da política selecionada na árvore do console, expanda **Configuração do Computador**, expanda **Modelos Administrativos**, expanda **Componentes do Windows**e clique em **Windows Update**.

4.  No painel de resultados, clique com o botão direito em **Permitir conteúdo assinado do local de serviço de atualização da Microsoft na intranet** , clique em **Propriedades**, clique em **Habilitado**e clique em **OK**.
