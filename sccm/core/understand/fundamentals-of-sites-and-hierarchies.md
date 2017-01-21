---
title: "Conceitos básico de sites e hierarquias | Microsoft Docs"
description: "Obtenha as informações de conceitos básicos sobre os sites e hierarquias do System Center Configuration Manager."
ms.custom: na
ms.date: 12/08/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4db1e15f-e832-4cf9-be33-d3971e635a55
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1b64b5f6e208b85a5ec2ef02bab34afee451c484
ms.openlocfilehash: cda27b9478e915bca99f5784ec6bcbedc989e841


---
# <a name="fundamentals-of-sites-and-hierarchies-for-system-center-configuration-manager"></a>Conceitos básicos de sites e hierarquias do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Uma implantação do System Center Configuration Manager deve ser instalada em um domínio do Active Directory e tem uma base de um ou mais sites do Configuration Manager que formam uma hierarquia de sites. De um único site para uma hierarquia com vários sites, o tipo e o local dos sites instalados fornecem a capacidade de escalar verticalmente (expandir) sua implantação quando necessário, bem como fornecer serviços a usuários e dispositivos gerenciados.

## <a name="hierarchies-of-sites"></a>Hierarquias de sites
Quando você instala o System Center Configuration Manager pela primeira vez, o primeiro site do Configuration Manager instalado determina o escopo da hierarquia ‑ a base da qual você gerenciará dispositivos e usuários em sua empresa. Esse primeiro site deve ser um site de administração central ou um site primário autônomo.  

 Um **site de administração central** é adequado para implantações de grande escala, além de fornecer um ponto central de administração e a flexibilidade para ser compatível com dispositivos distribuídos em uma infraestrutura de rede global. Depois de instalar um site de administração central, você precisará instalar um ou mais sites primários como sites filho.  Isso porque um site de administração central não oferece suporte direto ao gerenciamento de dispositivos, que é a função de um site primário. Um site de administração central permite vários sites primários filho, que você usa para gerenciar diretamente dispositivos e controlar a largura de banda da rede quando os dispositivos gerenciados estão em diferentes locais geográficos.  

 Um **site primário autônomo** é adequado para implantações menores, podendo ser usado para gerenciar dispositivos sem ter que instalar sites adicionais. Embora um site primário autônomo possa limitar o tamanho da sua implantação, ele não aceita um cenário para expandir a hierarquia posteriormente instalando um novo site de administração central. Com esse cenário de expansão do site, o site primário autônomo se torna um site primário filho e você pode então instalar sites primários filho adicionais abaixo do novo site de administração central.  Isso permite expandir a implantação inicial para futuro crescimento de sua empresa.  

> [!TIP]  
>  Um site primário autônomo e um site primário filho são na realidade do mesmo tipo: um site primário. A diferença no nome se baseia na relação de hierarquia que é criada quando você também usa um site de administração central.  Essa relação de hierarquia também pode limitar a instalação de certas funções do sistema de sites que estendem a funcionalidade Configuration Manager. Isso ocorre porque determinadas funções do sistema de sites só podem ser instaladas no site de nível superior da hierarquia, em um site de administração central ou site primário autônomo.  

 Depois de instalar seu primeiro site, você poderá instalar sites adicionais.  Se seu primeiro site foi um site de administração central, você poderá instalar um ou mais sites primários filho.  Depois de instalar um site primário (autônomo ou primário filho), você poderá instalar um ou mais sites secundários.  

 Um **site secundário** só pode ser instalado como um site filho abaixo de um site primário. Esse tipo de site estende o alcance de um site primário para gerenciamento de dispositivos em locais que têm uma conexão de rede lenta com o site primário.   Embora o site secundário estenda o site primário, os clientes continuam sendo gerenciados pelo site primário. O site secundário oferece suporte a dispositivos no local remoto compactando e gerenciando a transferência de informações na rede que você envia (implanta) para clientes, e esses clientes enviam de volta para o site.  

 Os diagramas a seguir mostram alguns exemplos de designs de site.  

 ![Exemplos de hierarquia](media/Hierarchy_examples.png)  

 Para mais informações, consulte os seguintes tópicos:  

-   [Introduction to System Center Configuration Manager](../../core/understand/introduction.md)  

-   [Criar uma hierarquia de sites para o System Center Configuration Manager](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)  

-   [Instalar sites do System Center Configuration Manager](/sccm/core/servers/deploy/install/installing-sites)  

## <a name="site-system-servers-and-site-system-roles"></a>Servidores do sistema de site e funções do sistema de site  
 Cada site do Configuration Manager instala **funções do sistema de sites** que dão suporte às operações de gerenciamento.  Algumas funções são instaladas por padrão quando você instala um site, como a função de **servidor do site** (que é atribuída ao computador em que o site é instalado) e a função de servidor de banco de dados do site (que é atribuída ao SQL Server que hospeda o banco de dados do site). Outras funções do sistema de sites são opcionais e usadas somente quando você quer usar a funcionalidade que uma função do sistema de sites permite.  Qualquer computador que hospede uma função do sistema de sites é conhecido como servidor do sistema de sites.  

 Para uma implantação menor do Configuration Manager, inicialmente, você pode executar todas as funções do sistema de sites diretamente no computador do servidor do site. Depois, conforme o ambiente é gerenciado e precisa crescer, é possível instalar servidores adicionais do sistema de sites para hospedar mais funções do sistema de sites, a fim de aprimorar a eficiência dos sites no fornecimento de serviços a mais dispositivos.  

 Para obter informações sobre como planejar diferentes funções do sistema de sites, consulte [Site system roles](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) (Funções de sistema de sites) em [Plan for site system servers and site system roles for System Center Configuration Manager](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md) (Planejar servidores de sistema de sites e funções de sistema de sites no System Center Configuration Manager).  

## <a name="publishing-site-information-to-active-directory-domain-services"></a>Publicando informações de sites nos Serviços de Domínio Active Directory  
 Para simplificar o gerenciamento do Configuration Manager, é possível estender o esquema do Active Directory para aceitar detalhes usados pelo Configuration Manager e, assim, os sites publicam suas principais informações no AD DS (Active Directory Domain Services). Isso permite que os computadores que você deseja gerenciar recuperem com segurança as informações relacionadas da fonte confiável do AD DS. As informações que os clientes podem recuperar identificam sites disponíveis, servidores do sistema de sites e os serviços que esses servidores do sistema de sites fornecem.  

 **A extensão do esquema do Active Directory** é feita apenas uma vez por floresta e pode ser feita antes ou depois da instalação do Configuration Manager.   Ao estender o esquema, você deve criar um novo contêiner do Active Directory denominado **System Management** em cada domínio que contenha um site do Configuration Manager que publicará dados que os clientes vão encontrar. Para obter mais informações,consulte [Estender o esquema do Active Directory para o System Center Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md).  

 **A publicação de dados do site** aprimora a segurança da hierarquia do Configuration Manager e reduz a sobrecarga administrativa, mas não é obrigatória para funcionalidades básicas do Configuration Manager.  



<!--HONumber=Dec16_HO3-->


