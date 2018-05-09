---
title: Configurações do Windows Hello para Empresas
titleSuffix: Configuration Manager
description: Saiba como integrar o Windows Hello para Empresas com o System Center Configuration Manager.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 60dcf98b83fb4650a10e5503d42b9f49d3aba359
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>Windows Hello para Empresas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

<!--1245704-->
O System Center Configuration Manager permite que você se integre com o Windows Hello para Empresas (anteriormente conhecida como Microsoft Passport para Windows), um método de entrada alternativo para dispositivos Windows 10. O Hello para Empresas usa o Active Directory ou uma conta do Azure Active Directory para substituir uma senha, cartão inteligente ou cartão inteligente virtual.  

O Hello para Empresas permite que você use um **gesto do usuário** para fazer logon, em vez de uma senha. O gesto do usuário pode ser um PIN simples, uma autenticação biométrica ou um dispositivo externo, como um leitor de impressão digital.

Para obter mais informações, confira [Windows Hello para Empresas](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification).


> [!Note]  
> O Configuration Manager não habilita esse recurso opcional por padrão. É necessário habilitar esse recurso antes de usá-lo. Para obter mais informações, veja [Habilitar recursos opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


 O Configuration Manager integra-se com o Windows Hello para Empresas de duas maneiras:  

-   É possível usar o Configuration Manager para controlar quais gestos os usuários podem e não podem usar para se conectar.  

-   Você pode armazenar certificados de autenticação no KSP (provedor de armazenamento de chaves) do Windows Hello para Empresas. Para obter mais informações, consulte [Certificate profiles (Perfis de Certificado)](introduction-to-certificate-profiles.md).  

- É possível implantar as políticas do Windows Hello para Empresas em dispositivos Windows 10 ingressados em domínio que executam o cliente do Configuration Manager. Essa configuração é descrita na seção [Configurar o Windows Hello para Empresas em dispositivos Windows 10 ingressados em domínio](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices). Quando você usa o Configuration Manager com o Microsoft Intune (híbrido), você pode definir essas configurações em dispositivos com Windows 10 e Windows 10 Mobile. Para obter mais informações, confira [Configurar o Windows Hello para Empresas (híbrido)](../../mdm/deploy-use/windows-hello-for-business-settings.md).

## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>Configurar o Windows Hello para Empresas em dispositivos Windows 10 ingressados em domínio
Você pode controlar o Windows Hello para Empresas em dispositivos com Windows 10 ingressados em domínio por meio da criação e implantação de um perfil de negócios do Windows Hello para Empresas. Essa abordagem é recomendada.


Se você estiver usando a autenticação baseada em certificado, também será necessário implantar um perfil de certificado, conforme descrito em [Configurar um perfil de certificado](#configure-a-certificate-profile). Se você estiver usando a autenticação baseada em chave, não será necessário implantar um perfil de certificado.

## <a name="configure-a-windows-hello-for-business-profile"></a>Configurar um perfil para o Windows Hello para empresas  

No console do Configuration Manager, em **Acesso ao Recurso da Empresa**, clique com o botão direito do mouse em **Perfil do Windows Hello para Empresas** e escolha **Novo** para iniciar o assistente de perfil. Forneça as configurações solicitadas pelo assistente, reveja-as e confirme-as na última página e clique em **Fechar**. Aqui está um exemplo de como será a aparência de suas configurações:  

![Assistente de Política do Windows Hello para Empresas, mostrando a lista de configurações disponíveis](../media/Hello-for-Business-settings.png)

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>Configure um perfil de certificado para registrar o certificado de registro do Windows Hello para Empresas no Configuration Manager  
 Se você quiser usar o logon baseado em certificado do Windows Hello para Empresas, configure os seguintes componentes:  

-   Um perfil de certificado do Configuration Manager.  

-   No perfil de certificado, selecione um modelo que usa o logon do cartão inteligente EKU.  

-   Se você pretende armazenar perfis de certificado no contêiner de chaves do Windows Hello para Empresas, e o perfil de certificado usa o EKU de **Logon de Cartão Inteligente**, deverá configurar as seguintes permissões para registro de chave para garantir que o certificado seja validado corretamente.
Você primeiro deverá ter criado o **Administradores de Chave** e adicionado a esse grupo todos os computadores do ponto de gerenciamento do Configuration Manager como membros.

Talvez algumas configurações não exijam a configuração de permissões, ou podem exigir mais configurações. Consulte a tabela a seguir para obter mais ajuda:

|Versão do cliente do Windows|Configuration Manager 1602 ou 1606|Configuration Manager 1610|Configuration Manager 1702 ou posterior|
|-|-|-|-|
|Atualização de Aniversário do Windows 10|Nenhum hotfix necessário<br><br>Nenhuma permissão necessária<br><br>Nenhuma atualização de esquema do Windows necessário|Nenhum hotfix necessário (confira **Aviso**)<br><br>Nenhuma permissão necessária<br><br>Nenhuma atualização de esquema do Windows necessário|Configurar as permissões<br><br>Aplicar o esquema do Windows Server 2016 ao Active Directory|
|Atualização do Windows 10 para Criadores ou posterior|Sem suporte|Instalar [este hotfix](https://support.microsoft.com/help/4010155/update-rollup-for-system-center-configuration-manager-current-branch-v)<br><br>Configurar as permissões<br><br>Aplicar o esquema do Windows Server 2016 ao Active Directory|Configurar as permissões<br><br>Aplicar o esquema do Windows Server 2016 ao Active Directory|

> [!WARNING]
> Embora [o hotfix](https://support.microsoft.com/help/4010155/update-rollup-for-system-center-configuration-manager-current-branch-v) não seja necessário para o Configuration Manager 1610 e a Atualização de Aniversário do Windows 10, talvez ele esteja instalado.  Se o hotfix estiver instalado, você precisará configurar as permissões e aplicar o esquema do Windows Server 2016 ao Active Directory.

## <a name="to-configure-permissions"></a>Para configurar as permissões

1.  Entre em uma estação de trabalho de controlador de domínio ou de gerenciamento com as credenciais do administrador de domínio ou equivalentes.
2.  Abra **usuários e computadores do Active Directory**.
3.  No painel de navegação, clique com o botão direito no seu nome de domínio e, em seguida, clique em **Propriedades**.
4.  Na guia **Segurança** da caixa de diálogo *<domain name>* **Propriedades**, clique em **Avançado**. Se a guia **Segurança** não for exibida, habilite **Recursos Avançados** no menu **Exibição** de **Usuários e Computadores do Active Directory**.
5.  Clique em **Adicionar**.
6.  Na caixa de diálogo **Entrada de Permissão para** *<domain name>*, clique em **Selecionar uma entidade**.
7.  Na caixa de diálogo **Selecionar Usuário, Computador, Conta de Serviço ou Grupo**, digite **Administradores de Chave** na caixa de texto **Insira o nome do objeto para selecionar**. Clique em **OK**.
8.  Da lista **Aplica-se a**, selecione **Objetos do Usuário Descendente**.
9.  Role até a parte inferior da página e clique em **Limpar tudo**.
10. Na seção **Propriedades**, selecione **Ler msDS-KeyCredentialLink**.
11. Clique em **OK** três vezes para concluir a tarefa.


## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, consulte [Certificate profiles (Perfis de Certificado)](introduction-to-certificate-profiles.md).  




