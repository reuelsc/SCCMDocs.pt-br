---
title: Ajuda do cliente Endpoint Protection
titleSuffix: Configuration Manager
description: Saiba mais sobre recursos e aprimoramentos no Endpoint Protection que ajudam a proteger seu computador contra ameaças.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: fdcee455-22e3-451d-bcf3-e7b62792f04a
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 580218b701b01af388b56bbd2b7293f67cf5d77d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32348922"
---
# <a name="endpoint-protection-client-help"></a>Ajuda do cliente Endpoint Protection

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Essa versão do Windows Defender ou do Endpoint Protection inclui os seguintes recursos para ajudar a proteger seu computador contra ameaças:  

-   **Integração do Firewall do Windows.** A configuração do Endpoint Protection permite ligar ou desligar o Firewall do Windows.  
-   **Sistema de Inspeção da Rede.** Este recurso aprimora a proteção em tempo real ao inspecionar o tráfego de rede para ajudar a bloquear de forma pró-ativa a exploração de vulnerabilidades conhecidas de rede.  
-   **Mecanismo de proteção.** A proteção em tempo real localiza e interrompe a instalação ou execução de malware em seu computador. O mecanismo atualizado oferece recursos de detecção e limpeza aprimorados com melhor desempenho.  

O Windows Defender é fornecido como parte do sistema operacional Windows 10.  Em versões anteriores do Windows, o administrador pode fornecer o Windows Defender ou o Endpoint Protection usando software de gerenciamento.

Você também pode encontrar uma lista de [perguntas frequentes sobre o Windows Defender e o Endpoint Protection](endpoint-protection-client-faq.md). Para ajuda de solução de problemas, consulte [Solução de problemas do cliente Windows Defender ou Endpoint Protection](troubleshoot-endpoint-client.md). Para obter uma lista dos novos recursos, consulte [Novidades no cliente Windows Defender](https://support.microsoft.com/help/29276/windows-10-whats-new-in-windows-defender).

## <a name="windows-firewall-integration"></a>Integração do Firewall do Windows  
 O Firewall do Windows pode ajudar a impedir que invasores ou softwares maliciosos tenham acesso ao seu computador pela Internet ou por uma rede. Agora, quando você instala o Endpoint Protection, o assistente de instalação verifica se o Firewall do Windows está ativado. Se você tiver desativado o Firewall do Windows intencionalmente, poderá desmarcar uma caixa de seleção para evitar ativá-lo. É possível alterar as configurações do Firewall do Windows a qualquer momento, via Sistema e Segurança no Painel de Controle.  

## <a name="network-inspection-system"></a>Sistema de Inspeção da Rede  
 Os invasores cada vez mais realizam ataques com base em redes e se aproveitam das vulnerabilidades expostas antes que os fornecedores de software possam desenvolver e distribuir atualizações de segurança. Os estudos de vulnerabilidades mostram que pode levar um mês ou mais do momento do início de um ataque antes que uma atualização de segurança apropriada seja desenvolvida, testada e lançada. Essa falha na proteção deixa muitos computadores vulneráveis a ataques e explorações por um período significativo. O Sistema de Inspeção de Rede trabalha com proteção em tempo real para protegê-lo melhor de ataques com base em redes. Para isso, ele reduz o tempo entre descobertas de vulnerabilidades e implantação de atualizações de semanas para apenas algumas horas.  

## <a name="award-winning-protection-engine"></a>Mecanismo de proteção premiado  
 Nos bastidores do Windows Defender ou do Endpoint Protection está o premiado mecanismo de proteção, atualizado regularmente. O mecanismo conta com o suporte de uma equipe de pesquisadores antimalware do Centro de Proteção contra Malware da Microsoft, fornecendo respostas às ameaças de malware mais recentes, 24 horas por dia.  

## <a name="windows-defender-settings"></a>Configurações do Windows Defender
As configurações do Windows Defender habilitam configurações que ajudam a proteger seu computador contra software mal-intencionado. O administrador pode gerenciar algumas configurações do Windows Defender pra você. Você pode gerenciar outras usando as configurações do Windows Defender. Recomendamos que você habilite as configurações do Windows Defender para ajudar a proteger seu computador e seus dados.

Para exibir as configurações do Windows Defender, pesquise `Windows Defender` em seu computador. Abra o **Windows Defender** e selecione **Configurações**. As configurações do Windows Defender incluem:
- **Proteção em tempo real** – localiza e interrompe a instalação ou execução de malware em seu computador.
- **Proteção baseada em nuvem** – o Windows Defender envia informações à Microsoft sobre possíveis ameaças de segurança.
- **Envio automático de amostra** – permite que o Windows Defender envie amostras de arquivos suspeitos para a Microsoft para ajudar a melhorar a detecção de malware.
- **Exclusões** – é possível excluir determinados arquivos, pastas, extensões de arquivos ou processos da verificação do Windows Defender.
- **Notificação aprimorada** – habilita notificações que informam sobre a integridade do seu computador. Mesmo **Desligado**, você receberá notificações críticas.
- **Windows Defender Offline** – é possível executar o Windows Defender Offline para ajudar a localizar e remover software mal-intencionado. Essa verificação reiniciará o seu computador e levará cerca de 15 minutos.

### <a name="see-also"></a>Consulte também  
 [Perguntas frequentes sobre o cliente do Endpoint Protection](endpoint-protection-client-faq.md)   
 [Solucionando problemas do cliente Windows Defender ou Endpoint Protection](troubleshoot-endpoint-client.md)
