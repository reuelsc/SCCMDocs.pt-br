---
title: Conectar o Configuration Manager
titleSuffix: Configuration Manager
description: Um guia de instruções para conectar o Configuration Manager com a análise de área de trabalho.
ms.date: 04/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 11979d35829660633dd77059562dcf519e0af05b
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62206118"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>Como conectar o Configuration Manager com a análise de área de trabalho

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Análise da área de trabalho está totalmente integrado com o Configuration Manager. Primeiro, verifique se que o site é atualizado para dar suporte a recursos mais recentes. Em seguida, crie a conexão de área de trabalho de análise no Configuration Manager. Por fim, monitore a integridade de conexão.


## <a name="bkmk_hotfix"></a> Atualizar o site

Primeiro, certifique-se de que seu site do Configuration Manager está em execução pelo menos a versão 1810. Para obter mais informações, confira [Instalar atualizações no console](/sccm/core/servers/manage/install-in-console-updates).

Você também precisará instalar a versão 1810 Update Rollup 2 (4488598) para dar suporte à integração com a área de trabalho de análise. Para obter mais informações sobre esta atualização, consulte [Update Rollup 2 para o branch atual do Configuration Manager, versão 1810](https://support.microsoft.com/help/4488598).

1. Atualize o site com o pacote cumulativo de atualizações da versão 1810. Para obter mais informações, confira [Instalar atualizações no console](/sccm/core/servers/manage/install-in-console-updates).  

2. Atualize clientes. Para simplificar este processo, considere o uso da atualização automática do cliente. Para obter mais informações, consulte [Atualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  



## <a name="bkmk_connect"></a> Conectar-se ao serviço

Use este procedimento para conectar o Configuration Manager para análise de área de trabalho e definir as configurações do dispositivo. Esse procedimento é um processo único para anexar a sua hierarquia para o serviço de nuvem.  

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e selecione o nó **Serviços do Azure**. Selecione **configurar serviços do Azure** na faixa de opções.  

2. Sobre o **serviços do Azure** página do Assistente de serviços do Azure, defina as seguintes configurações:  

    - Especifique um **Nome** para o objeto no Configuration Manager.  

    - Especifique uma **Descrição** opcional para ajudá-lo a identificar o serviço.  

    - Selecione **análise de área de trabalho** na lista de serviços disponíveis.  
  
   Selecione **Avançar**.  

3. Sobre o **aplicativo** , selecione apropriado **ambiente do Azure**. Em seguida, selecione **importação** para o aplicativo web. Defina as seguintes configurações na **importar aplicativos** janela:  

    - **Nome do locatário do Azure AD**: Esse nome é como ele é chamado no Configuration Manager  

    - **ID de locatário do Azure AD**: O **ID de diretório** você copiou do Azure AD  

    - **ID do cliente**: O **ID do aplicativo** você copiou do aplicativo Azure AD  

    - **Chave secreta**: A tecla **valor** você copiou do aplicativo Azure AD  

    - **Vencimento da Chave Secreta**: A mesma data de expiração da chave  

    - **URI da ID do aplicativo**: Essa configuração deve preencher automaticamente com o seguinte valor: `https://cmmicrosvc.manage.microsoft.com/`  
  
   Selecione **Verify**e, em seguida, selecione **Okey** para fechar a janela Importar aplicativos. Selecione **próxima** na página do aplicativo do Assistente de serviços do Azure.  

4. Sobre o **dados de diagnóstico** página, defina as seguintes configurações:  

    - **ID comercial**: esse valor deve preencher automaticamente com a ID. da sua organização Se ele não abrir, verifique se o servidor proxy está configurado necessário colocar todos os [pontos de extremidade](/sccm/desktop-analytics/enable-data-sharing#endpoints) antes de continuar. Como alternativa, recuperar sua ID comercial do **serviços conectados** painel na [portal de análise de área de trabalho](https://aka.ms/m365aprod).  

    - **Nível de dados de diagnóstico do Windows 10**: Selecione pelo menos **avançado (limitado)**  

    - **Permitir que o nome do dispositivo nos dados de diagnóstico**: selecione **habilitar**  

        > [!Note]  
        > Começando com o Windows 10 versão 1803, o nome do dispositivo não será enviado à Microsoft por padrão. Se você não enviar o nome do dispositivo, ele aparece na área de trabalho de análise como "Desconhecido". Esse comportamento pode tornar difícil de identificar e avaliar os dispositivos.  

   Selecione **Avançar**. O **funcionalidade disponível** página mostra a funcionalidade de análise de área de trabalho que está disponível com as configurações de dados de diagnóstico da página anterior. Selecione **próxima** para continuar ou **Previous** para fazer alterações.  

    ![Exemplo de página de funcionalidade disponível no Assistente de serviços do Azure](media/available-functionality.png)

5. Sobre o **coleções** página, defina as seguintes configurações:  

    - **Nome de exibição**: O portal de análise de área de trabalho exibe essa conexão do Configuration Manager usando esse nome. Usá-lo para diferenciar entre hierarquias diferentes. Por exemplo, *laboratório de teste* ou *produção*.  

    - **Coleção de destino**: Esta coleção inclui todos os dispositivos que o Configuration Manager configura com sua ID comercial e as configurações de dados de diagnóstico. É o conjunto completo de dispositivos do Configuration Manager se conecta ao serviço de análise de área de trabalho.  

    - **Dispositivos na coleção de destino usam um proxy de usuário autenticado para comunicação de saída**: Por padrão, esse valor é **não**. Se for necessário em seu ambiente, definido como **Sim**.  

    - **Selecione as coleções específicas para sincronizar com a área de trabalho de análise**: Selecione **adicionar** incluir coleções adicionais. Essas coleções estão disponíveis no portal de análise de área de trabalho para o agrupamento com planos de implantação. Certifique-se de incluir coleções de exclusão do projeto-piloto e piloto.  

        Essas coleções continuam a sincronização como suas alterações de associação. Por exemplo, o seu plano de implantação usa uma coleção com uma regra de associação do Windows 7. Como esses dispositivos de atualização para o Windows 10, e o Configuration Manager avalia a associação da coleção, esses dispositivos soltem fora a coleta e o plano de implantação.  

        > [!Important]  
        > Certifique-se de limitar essas coleções adicionais na coleção de destino. Sobre as propriedades dessas coleções adicionais, o **limitação de coleção** deve ser a mesma coleção de análise de área de trabalho **coleção de destino**.<!-- 4097528 -->  

6. Conclua o assistente.  

O Configuration Manager cria uma política de configurações para configurar dispositivos na coleção de destino. Esta política inclui as configurações de dados de diagnóstico para habilitar dispositivos para enviar dados à Microsoft. Por padrão, clientes atualizam a política a cada hora. Depois de receber as novas configurações, pode ser mais várias horas, antes que os dados estão disponíveis na área de trabalho de análise.



## <a name="bkmk_monitor"></a> Monitorar a integridade de conexão

Monitore a configuração de seus dispositivos para análise de área de trabalho. No console do Configuration Manager, vá para o **biblioteca de Software** espaço de trabalho, expanda o **manutenção do Microsoft 365** nó e selecione o **integridade de Conexão** painel.  

Para obter mais informações, consulte [monitorar a integridade de conexão](/sccm/desktop-analytics/troubleshooting#monitor-connection-health).

Configuration Manager sincroniza qualquer plano de implantação de área de trabalho de análise dentro de 15 minutos de criar a conexão. No console do Configuration Manager, vá para o **biblioteca de Software** espaço de trabalho, expanda o **manutenção do Microsoft 365** nó e selecione o **planos de implantação** nó.



## <a name="next-steps"></a>Próximas etapas

Avance para o próximo artigo para registrar dispositivos para análise de área de trabalho.
> [!div class="nextstepaction"]  
> [Registrar dispositivos](/sccm/desktop-analytics/enroll-devices)  
