---

title: "Segurança e privacidade das atualizações de software | Microsoft Docs"
description: "Siga essas práticas recomendadas de segurança para atualizações de software e saiba mais sobre como o Configuration Manager lida com informações de privacidade."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 41d6d5d8-ba84-4efb-b105-4d1eed239824
translationtype: Human Translation
ms.sourcegitcommit: e6cf8c799b5be2f7dbb6fadadddf702ec974ae45
ms.openlocfilehash: 4b4f045138abc14b6e93b3b990c5f3a8b4f2f952



---
# <a name="security-and-privacy-for-software-updates-in-system-center-configuration-manager"></a>Segurança e privacidade das atualizações de software no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico contém as informações de segurança e privacidade do atualizações de software no System Center Configuration Manager.  

##  <a name="a-namebkmksecurityhardwareinventorya-security-best-practices-for-software-updates"></a><a name="BKMK_Security_HardwareInventory"></a> Práticas recomendadas de segurança para atualizações de software  
 Use as seguintes práticas recomendadas de segurança quando você implantar atualizações de software aos clientes:  

-   Não altere as permissões padrão nos pacotes de atualização de software.  

     Por padrão, os pacotes de atualização de software são definidos para permitir que os administradores de **Controle Total** e usuários tenham acesso de **Leitura** . Se você alterar essas permissões, isso permitirá que um invasor adicione, remova ou exclua as atualizações de software.  

-   Controle o acesso ao local de download de atualizações de software.  

     As contas de computador para o Provedor de SMS, o servidor do site e o usuário administrativo que realmente baixam as atualizações de software para o local de download requerem acesso de **Gravação** para o local de download. Restrinja o acesso ao local de download para reduzir o risco de ataques de falsificação aos arquivos de origem de atualizações de software no local de download.  

     Além disso, se você usar um compartilhamento UNC para o local de download, proteja o canal de rede usando assinatura IPsec ou SMB para evitar falsificação dos arquivos de origem de atualizações de software quando eles forem transferidos via rede.  

-   Use o UTC para avaliar horários de implantação.  

     Se for usado o horário local em vez do UTC, os usuários poderão ter um atraso na instalação das atualizações de software por conta da mudança de fuso horário em seus computadores  

-   Habilite SSL no WSUS e siga as práticas recomendadas para proteger o WSUS (Windows Server Update Services).  

     Identifique e siga as práticas recomendadas de segurança para a versão do WSUS que você usa com o Configuration Manager.  

    > [!IMPORTANT]  
    >  Caso configure o ponto de atualização de software para habilitar comunicações SSL para o servidor WSUS, configure raízes virtuais para SSL no servidor WSUS.  

-   Habilite verificação de CRL.  

     Por padrão, o Configuration Manager não verifica a CRL (lista de certificados revogados) para confirmar a assinatura nas atualizações de software antes de serem implantadas nos computadores. Verificar a CRL sempre que um certificado é usado oferece mais segurança contra o uso de certificado revogado, mas gera atraso de conexão e incorre em processamentos adicionais no computador em que a verificação é executada.  

     Para obter mais informações sobre como habilitar a verificação de CRL para atualizações de software, consulte [Como habilitar a verificação CRL para atualizações de software no System Center Configuration Manager](../get-started/manage-settings-for-software-updates.md#crl-checking-for-software-updates).  

-   Configure o WSUS para usar um site personalizado.  

     Quando você instala o WSUS no ponto de atualização de software, pode usar o site Padrão do IIS existente ou criar um site personalizado do WSUS. Crie um site personalizado para o WSUS de forma que o IIS hospede os serviços do WSUS em um site virtual dedicado, em vez de compartilhar o mesmo site usado por outros sistemas de sites do Configuration Manager ou outros aplicativos.  

     Para mais informações, consulte [Configurar o WSUS para usar um site da Web personalizado](plan-for-software-updates.md#BKMK_CustomWebSite).  

##  <a name="a-namebkmkprivacyhardwareinventorya-privacy-information-for-software-updates"></a><a name="BKMK_Privacy_HardwareInventory"></a> Informações de privacidade para atualizações de software  
 As atualizações de software verificam os computadores cliente para determinar quais atualizações de software são necessárias, e então enviam as informações de volta ao banco de dados do site. Durante o processo de atualizações de software, o Configuration Manager pode transmitir informações entre clientes e servidores que identificam o computador e as contas de logon.  

 O Configuration Manager mantém informações de estado sobre o processo de implantação de software. As informações de estado não são criptografadas durante a transmissão ou o armazenamento. As informações de estado são armazenadas no banco de dados do Configuration Manager e excluídas pelas tarefas de manutenção do banco de dados. Nenhuma informação de estado é enviada à Microsoft.  

 O uso de atualizações de software do Configuration Manager para instalar atualizações de software em computadores cliente pode estar sujeito aos termos de licença de software dessas atualizações, que são separados dos Termos de Licença de Software do System Center Configuration Manager. Sempre examine e concorde com os Termos de Licenciamento de Software antes de instalar as atualizações de software usando o Configuration Manager.  

 O Configuration Manager não implementa atualizações de software por padrão e requer diversas etapas de configuração para que as informações sejam coletadas.  

 Antes de configurar as atualizações de software, considere os requisitos de privacidade.  



<!--HONumber=Dec16_HO3-->


