---
title: 'Registrar dispositivos com o gerenciador de registro de dispositivo '
titleSuffix: Configuration Manager
description: Registrar dispositivos de propriedade da empresa com a conta de gerente de registro de dispositivo com o System Center Configuration Manager.
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 2905f26e-7859-497d-b995-5ff48261efa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cc1be1d602c3f9f8e65e0523d64c5b6a8e579c90
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53415545"
---
# <a name="enroll-devices-with-device-enrollment-manager-with-configuration-manager"></a>Registrar dispositivos com o gerenciador de registro de dispositivo no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch atual)*

As organizações podem usar o Intune para gerenciar um grande número de dispositivos móveis com uma única conta de usuário. A conta do *DEM* (gerenciador de registro de dispositivos) é uma conta especial do usuário usada para registrar dispositivos. Adicionar usuários existentes à conta do DEM para fornecer recursos de DEM especiais. Cada dispositivo registrado usa uma única licença. Recomendamos o uso de dispositivos registrados com essa conta como dispositivos compartilhados sem afinidade de usuário em vez de dispositivos pessoais dedicados.  

## <a name="enroll-corporate-owned-devices-with-the-device-enrollment-manager"></a>Registrar dispositivos corporativos com o gerenciador de registro de dispositivo  
 Você pode atribui-la a um gerente da loja ou supervisor, por exemplo, como um conta de usuário de gerenciador de registro de dispositivos, para permitir que ela faça o seguinte:  

-   Registrar até 1.000 dispositivos para gerenciamento  
-   Use o aplicativo Portal da Empresa para instalar aplicativos da empresa  
-   Configurar o acesso aos dados da empresa  

As seguintes limitações se aplicam a dispositivos gerenciados usando uma conta de Gerenciador de registro de dispositivo:

- O gerenciador de armazenamento não redefine o dispositivo a partir do portal da empresa.  
- Dispositivos não podem ser ingressados no local de trabalho ou no Azure Active Directory. Isso impede tais dispositivos de usar o acesso condicional.
- Para implantar aplicativos da empresa em dispositivos gerenciados com o gerenciador de registro de dispositivo, implante o aplicativo de Portal da Empresa como uma **Instalação obrigatória** na conta de usuário do gerenciador de registro de dispositivo. O gerenciador de registro de dispositivo poderá então iniciar o aplicativo Portal da Empresa para instalar os aplicativos adicionais.
- Para melhorar o desempenho, o aplicativo Portal da Empresa mostra apenas o dispositivo local. O gerenciamento remoto de outros dispositivos DEM só pode ser feito no console do Configuration Manager e por um administrador
- O site do Portal da Empresa não está disponível para contas de gerenciador de registro de dispositivo. Use o aplicativo Portal da Empresa.
- Se você usar o DEM para registrar dispositivos iOS, não poderá usar o Apple Configurator ou o DEP (Programa de registro de dispositivo) da Apple para registrar dispositivos. (somente iOS) 

  **Exemplos de cenários do gerenciador de registro de dispositivo:**   
  Um restaurante quer tablets de ponto de venda para sua equipe e faz o pedido de monitores para sua equipe da cozinha. Os funcionários nunca precisam ter acesso aos dados da empresa ou fazer logon como um usuário. O administrador do Intune cria uma conta de gerenciador de registro de dispositivos e registra os dispositivos da empresa usando essa conta. Como alternativa, o administrador pode conceder credenciais de gerenciador de registro de dispositivos a um gerente do restaurante, permitindo que ele registre e gerencie os dispositivos.  

  O administrador ou o gerente podem implantar aplicativos específicos da função para os dispositivos do restaurante. Um administrador também pode selecionar um dispositivo no console e desativá-lo de gerenciamento de dispositivo móvel.  

#### <a name="add-a-device-enrollment-manager"></a>Adicionar um gerenciador de registro de dispositivo  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No workspace **Administração**, expanda **Serviços de Nuvem**e clique em **Assinaturas do Microsoft Intune**. Selecione a assinatura do Microsoft Intune à qual você adicionará um gerenciador de registro de dispositivo e clique em **Propriedades**.  

3.  Na caixa de diálogo Propriedades da Assinatura do Microsoft Intune, clique na guia **Gerenciador de Registro de Dispositivo**.  

4.  Clique em **Adicionar/Remover**.  

5.  No diálogo **Gerenciador de Registro de Dispositivo**, digite o nome de usuário que você deseja adicionar como um gerenciador de registro de dispositivo e clique em **Pesquisar**. Selecione o usuário que deseja adicionar como um Gerenciador de Registro de Dispositivo e clique em **Adicionar**.  

6.  Confirme a conta de usuário que será um gerenciador de registro de dispositivo e clique em **Adicionar/Remover**.  Uma licença de assinatura é necessária para cada usuário que acessa o serviço e o *gerenciador de registro de dispositivo* não pode ser um administrador do Intune. Determine se você precisa adicionar mais licenças antes de usar esse recurso.  

7.  Agora, o gerenciador de registro de dispositivo pode registrar dispositivos móveis usando o mesmo procedimento usado por um usuário final para um cenário BYOD (traga seu próprio dispositivo) no portal da empresa.  

#### <a name="delete-a-device-enrollment-manager-from-intune"></a>Excluir um gerenciador de registro de dispositivos do Intune  
Excluir um gerenciador de registro de dispositivos não afeta os dispositivos registrados. Quando um gerenciador de registro de dispositivos é excluído:  
- Nenhum dispositivo registrado tem seu registro cancelado  
- Os dispositivos registrados continuam sendo totalmente gerenciados  
- As credenciais da conta do gerenciador de registro de dispositivo excluído continuam válidas para fazer logon no portal da empresa para acessar aplicativos  
- As credenciais da conta do gerenciador de registro de dispositivos excluído não podem mais apagar ou desativar dispositivos  
- A relação da conta do gerenciador de registro de dispositivos excluído com os dispositivos registrados permanece, mas nenhum dispositivo adicional pode ser registrado

1.  No console do Configuration Manager, clique em **Administração**.  
2.  No workspace **Administração**, expanda **Serviços de Nuvem**e clique em **Assinaturas do Microsoft Intune**. Selecione a assinatura do Microsoft Intune à qual você adicionará um gerenciador de registro de dispositivo e clique em **Propriedades**.  
3.  Na caixa de diálogo Propriedades da Assinatura do Microsoft Intune, clique na guia **Gerenciador de Registro de Dispositivo**.  
4.  **Pesquise** o gerenciador de registro de dispositivo que deseja excluir, clique em **Remover** e em **OK**.  
