---
title: Mensagens de estado
titleSuffix: Configuration Manager
description: Descrições das mensagens de estado nas versões do Configuration Manager com suporte.
ms.date: 02/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f04c0a71-57bc-4443-a47c-592373050d04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9e3a30211b95e483b30caf1507b74a7737d156bb
ms.sourcegitcommit: 223549003829fce7c6dc63959ee71e8b88542417
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/27/2019
ms.locfileid: "56951861"
---
# <a name="state-messages-in-configuration-manager"></a>Mensagens de estado no Configuration Manager 

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As mensagens de estado contêm informações concisas sobre as condições no cliente do Configuration Manager. O sistema das mensagens de estado é usado por componentes específicos do Configuration Manager, como atualizações de software e parâmetros de configuração.

Os clientes do Configuration Manager enviam mensagens de estado ao ponto de status de fallback ou aos sistemas de sites do ponto de gerenciamento para relatar o estado atual das operações. É possível criar relatórios para exibir as mensagens de estado enviadas pelos clientes do Configuration Manager.

Cada recurso do Configuration Manager que usa as mensagens de estado é identificado pelo tipo de tópico da mensagem de estado. Os tipos de tópico das mensagem de estado listados neste artigo podem ser usados para definir o recurso do Configuration Manager com o qual uma mensagem se relaciona.

> [!NOTE]  
> Um valor de zero (0) da ID da mensagem de estado geralmente indica que o tipo de tópico está em um estado desconhecido.

## <a name="300-statetopictypesumassignmentcompliance"></a>300 STATE_TOPICTYPE_SUM_ASSIGNMENT_COMPLIANCE

|      ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|       0   | Estado de conformidade desconhecido|
|   1   | compatível | 
|   2   | Sem conformidade | 

## <a name="301-statetopictypesumassignmentenforcement"></a>301 STATE_TOPICTYPE_SUM_ASSIGNMENT_ENFORCEMENT

|       ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   0    | Estado de imposição desconhecido |
|   1    | Instalando atualização(ões)        | 
|   2    | Aguardando reinicialização              | 
|   3    | Aguardando a conclusão de outra instalação         | 
|   4    | Atualização instalada com êxito(2)             | 
|   5    | Reinicialização do sistema pendente           | 
|   6    | Falha ao instalar a(s) atualização(ões)          | 
|   7    | Baixando a(s) atualização(ões)   | 
|   8    | Atualização(ões) baixada(s)    | 
|   9    | Falha ao baixar a(s) atualização(ões)     | 
|   10   | Aguardando a janela de manutenção antes da instalação         | 
|   11   | Aguardando orquestração            | 

## <a name="302-statetopictypesumassignmentevaluation"></a>302 STATE_TOPICTYPE_SUM_ASSIGNMENT_EVALUATION

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|      
|0|        Estado de avaliação desconhecido|                 
|   1    |Avaliação ativada       |
|   2    |Avaliação bem-sucedida      |
|   3    |Falha na avaliação         |


## <a name="400-statetopictypesumcidetection"></a>400 STATE_TOPICTYPE_SUM_CI_DETECTION

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
| 0  | Estado de detecção desconhecido|
|   1|  Não é necessária      |
|   2|  Não Detectado          |
|   3|  Detectado      |

## <a name="401-statetopictypesumcicompliance"></a>401 STATE_TOPICTYPE_SUM_CI_COMPLIANCE

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|0| Estado de conformidade desconhecido|
|   1   |compatível         |
|   2   |Sem conformidade         |
|   3   |Conflito detectado     |
|   4   |Erro             |
|   5   |Desconhecida           |
|   6   |Conformidade parcial   |
|   7   |Conformidade não configurada     |

## <a name="402-statetopictypesumcienforcement"></a>402 STATE_TOPICTYPE_SUM_CI_ENFORCEMENT

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
| 0 | Estado de imposição desconhecido|
|   1   |Imposição iniciada                   |
|   2   |Imposição aguardando conteúdo               |
|   3   | Aguardando a conclusão de outra instalação         |
|   4   |Aguardando a janela de manutenção antes da instalação              |
|   5   |Requer reinicialização antes da instalação            |
|   6   |Falha geral           |
|   7   |Instalação pendente              |
|   8   |Instalando atualização                 |
|   9   |Reinicialização do sistema pendente        |
|   10  |Atualização instalada com êxito             |
|   11  |Falha ao instalar a atualização          |
|   12  |Baixando atualização        |
|   13  | Atualização baixada        |
|   14  |Falha ao baixar a atualização         |

## <a name="500-statetoptctypesumupdatedetection"></a>500 STATE_TOPTCTYPE_SUM_UPDATE_DETECTION

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|0 |Estado de detecção desconhecido|
|   1   | A atualização não é necessária     |
|   2   | A atualização é necessária         |
|   3   | Atualização instalada    |

## <a name="501-statetopictypesumupdatesourcescan"></a>501 STATE_TOPICTYPE_SUM_UPDATE_SOURCE_SCAN

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|0 |Estado de verificação desconhecido|
|   1   | Verificação aguardando conteúdo        |
|   2   | Verificação em execução            |
|   3   | Verificação concluída          |
|   4   | Verificação pendente de repetição      |
|   5   | Falha na verificação        |
|   6   | Verificação concluída com erros |

## <a name="700-statetopictyperesyncstatemsg"></a>700 STATE_TOPICTYPE_RESYNC_STATE_MSG

    No State IDs.

## <a name="701-statetopictypesystemheartbeat"></a>701 STATE_TOPICTYPE_SYSTEM_HEARTBEAT

    No State IDs.

## <a name="702-statetopictypeckdupdate"></a>702 STATE_TOPICTYPE_CKD_UPDATE
 
    No State IDs.

## <a name="800-statetopictypeclientdeployment"></a>800 STATE_TOPICTYPE_CLIENT_DEPLOYMENT

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   100 |Implantação do cliente iniciada             |          
|   101 |Aguardando download                  |          
|   102 |Implantação agendada                  |          
|   103 | Aguardando a janela antes da implantação |
|   104 |Implantação ignorada                |          
|   301 |Falha na implantação de cliente desconhecido |          
|   302 |Falha ao criar o serviço ccmsetup  |         
|   303 |Falha ao excluir o serviço ccmsetup |          
|   304 |Não é possível instalar no sistema operacional inserido com o Driver de Filtro de Gravação com Base em Arquivos (FBWF) habilitado na unidade do sistema |          
|   305 |O modo de segurança nativa não é válido no Windows 2000  |         
|   306 |Falha ao iniciar o processo de download de ccmsetup  |         
|   307 |A linha de comando ccmsetup não é válida |        
|   308 |Falha ao baixar o arquivo no WINHTTP no endereço |        
|   309 |Falha ao baixar os arquivos através do BITS no endereço |       
|   310 |Falha ao instalar a versão do BITS |         
|   311 |Não é possível verificar se o arquivo de pré-requisito está assinado pela MS  |          
|   312 |Falha ao copiar o arquivo porque o disco está cheio |       
|   313 |Falha na instalação de client.msi com erro de MSI |          
|   314 |Falha no carregamento do arquivo de manifesto ccmsetup.xml |          
|   315 |Falha ao obter um certificado do cliente  |         
|   316 |Arquivo de pré-requisito não assinado pela MS |         
|   317 |Reinicialização necessária para continuar a instalação  |          
|   318 |Não é possível instalar o cliente no MP porque as versões do MP e do cliente não correspondem |        
|   319 |Não há suporte para o sistema operacional ou para o service pack  |        
|   320 |Não há suporte para a implantação                  |          
|   321 |Bits ausentes                      |          
|   322 |Pasta de origem indisponível                  |          
|   323 |Não há suporte para Appv                    |          
|   324 |Versão do site incorreta                    |          
|   325 |Incompatibilidade de hash do pré-requisito                |          
|   326 |Falha no cancelamento de registro do MDM             |          
|   327 |Registro do MDM detectado             |          
|   328 |Intune detectado                   |          
|   329 |Rede limitada não permitida            |          
|   400 |Implantação do cliente com êxito |  
|   401 |Implantação bem-sucedida, reinicialização necessária          |          
|   402 |Implantação bem-sucedida, reinicialização bem-sucedida         |
|   500 |Atribuição do cliente iniciada|
|   601 |Falha na atribuição de cliente desconhecido|
|   602 |O código de site a seguir é inválido|
|   603 |Falha ao atribuir ao MP|
|   604 |Falha ao descobrir o ponto de gerenciamento padrão|
|   605 |Falha ao baixar o certificado de autenticação do site|
|   606 |Falha na descoberta automática do código de site|
|   607 |Falha na atribuição do site; a versão do cliente é mais nova que a do site|
|   608 |Falha ao obter a Versão do Site do Active Directory Domain Services e SLP|
|   609 |Falha ao obter a versão do cliente|
|   700 |Atribuição do cliente com êxito|

## <a name="801-statetopictypedeviceclientdeployment"></a>801 STATE_TOPICTYPE_DEVICE_CLIENT_DEPLOYMENT

    No State IDs.

## <a name="810-statetopictypeclientcomanagement"></a>810 STATE_TOPICTYPE_CLIENT_COMANAGEMENT

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   100 | Status do registro         |
|   101 | Registro agendado          |
|   102 | Registro cancelado           |
|   105 | Registro iniciado            |
|   106 | O registro foi bem-sucedido, mas não está provisionado   
|   107 | O registro foi bem-sucedido e está provisionado   
|   108 | Registro sem usuário ativo         |
|   110 | Falha no registro         |


## <a name="820--statetopictypeclientwufb"></a>820  STATE_TOPICTYPE_CLIENT_WUFB

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   | Status do cliente do Windows Update para Empresas| 

## <a name="900-statetopictypebranchdp"></a>900 STATE_TOPICTYPE_BRANCH_DP

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   | Espaço em disco      | 

## <a name="901-statetopictyperemotedpmonitoring"></a>901 STATE_TOPICTYPE_REMOTE_DP_MONITORING

    No State IDs.

## <a name="902-statetopictypepulldpmonitoring"></a>902 STATE_TOPICTYPE_PULL_DP_MONITORING

    No State IDs.

## <a name="903-statetopictypedpusage"></a>903 STATE_TOPICTYPE_DP_USAGE

    No State IDs.

## <a name="1000--statetopictypeclientframeworkcomm"></a>1000  STATE_TOPICTYPE_CLIENT_FRAMEWORK_COMM

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1      | O cliente está se comunicando com êxito com o ponto de gerenciamento |
|   2      | Falha do cliente ao se comunicar com o ponto de gerenciamento |

## <a name="1001-statetopictypeclientframeworklocal"></a>1001 STATE_TOPICTYPE_CLIENT_FRAMEWORK_LOCAL

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Cliente recuperou com êxito o certificado do armazenamento de certificados local       |
|   2   |Falha do cliente ao recuperar o certificado do armazenamento de certificados local |

## <a name="1002-statetopictypedeviceclientframeworkcomm"></a>1002 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_COMM

    No State IDs.

## <a name="1003-statetopictypedeviceclientframeworklocal"></a>1003 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_LOCAL

    No State IDs.

## <a name="1004-statetopictypedeviceclientframeworkcertificate"></a>1004 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_CERTIFICATE

    No State IDs.

## <a name="1005-statetopictypedeviceclientwipe"></a>1005 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE

    No State IDs.

## <a name="1006-statetopictypedeviceclientretire"></a>1006 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE

    No State IDs.

## <a name="1007-statetopictypedeviceclientwipeintune"></a>1007 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE_INTUNE

    No State IDs.

## <a name="1008-statetopictypedeviceclientretireintune"></a>1008 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE_INTUNE

    No State IDs.

## <a name="1009-statetopictypedeviceclientdevicelock"></a>1009 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK

    No State IDs.

## <a name="1010-statetopictypedeviceclientdevicelockintune"></a>1010 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK_INTUNE

    No State IDs.

## <a name="1011-statetopictypedeviceclientdevicepinreset"></a>1011 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET

    No State IDs.

## <a name="1012-statetopictypedeviceclientdevicepinresetintune"></a>1012 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_INTUNE

    No State IDs.

## <a name="1013-statetopictypedeviceclientdevicepinresetonprem"></a>1013 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_ONPREM

    No State IDs.

## <a name="1014-statetopictypedeviceclientdevicealbypass"></a>1014 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS

    No State IDs.

## <a name="1015-statetopictypedeviceclientdevicealbypassintune"></a>1015 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS_INTUNE

    No State IDs.

## <a name="1100-statetopictypeclientframeworkmodereadiness"></a>1100 STATE_TOPICTYPE_CLIENT_FRAMEWORK_MODEREADINESS

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |O cliente não está pronto para o modo nativo  |
|   2   |O cliente está pronto para o modo nativo       |


## <a name="1300-statetopictypeclienthealth"></a>1300 STATE_TOPICTYPE_CLIENT_HEALTH

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |   Êxito|    
|   2   |   Sem êxito |    

## <a name="1401-statetopictypestatereport"></a>1401 STATE_TOPICTYPE_STATE_REPORT

    No State IDs.

## <a name="1500-statetopictypecaltrackut"></a>1500 STATE_TOPICTYPE_CAL_TRACK_UT

    No State IDs.

## <a name="1502-statetopictypecaltrackmt"></a>1502 STATE_TOPICTYPE_CAL_TRACK_MT

    No State IDs.

## <a name="1503-statetopictypecaltrackml"></a>1503 STATE_TOPICTYPE_CAL_TRACK_ML

    No State IDs.   

## <a name="1600-statetopictypeuseraffinity"></a>1600 STATE_TOPICTYPE_USER_AFFINITY

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Conjunto de afinidades do usuário        |
|   2   |Afinidades do usuário removidas        |

## <a name="1700-statetopictypeappciscan"></a>1700 STATE_TOPICTYPE_APP_CI_SCAN

    No State IDs.

## <a name="1701-statetopictypeappcicompliance"></a>1701 STATE_TOPICTYPE_APP_CI_COMPLIANCE

    No State IDs.

## <a name="1702-statetopictypeappcienforcement"></a>1702 STATE_TOPICTYPE_APP_CI_ENFORCEMENT

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1000    |Item de configuração bem-sucedido                      |
|   1001    |Item de configuração bem-sucedido, já instalado            |
|   1002    |Simulação bem-sucedida do item de configuração                |
|   1003    |Status rápido bem-sucedido do item de configuração                  |
|   2000    |Item de configuração em andamento                    |
|   2001    |Item de configuração em andamento, aguardando conteúdo            |
|   2002    |Instalação em andamento do item de configuração                 |
|   2003    |Item de configuração em andamento, aguardando reinicialização             |
|   2004    |Item de configuração em andamento, aguardando janela de manutenção         |
|   2005    |Item de configuração em andamento, aguardando agendamento               |
|   2006    |Item de configuração em andamento, baixando conteúdo dependente     |
|   2007    |Item de configuração em andamento, instalando dependências        |
|   2008    |Item de configuração em andamento, reinicialização pendente             |
|   2009    |Item de configuração em andamento, conteúdo baixado             |
|   2010    |Item de configuração em andamento, atualização pendente             |
|   2011    |Item de configuração em andamento, aguardando usuário reconectar         |
|   2012    |Item de configuração em andamento, aguardando usuário sair              |
|   2013    |Item de configuração em andamento, aguardando usuário entrar               |
|   2014    |Item de configuração em andamento, aguardando instalação            |
|   2015    |Item de configuração em andamento, aguardando nova tentativa              |
|   2016    |Item de configuração em andamento, aguardando presmode               |
|   2017    |Item de configuração em andamento, aguardando orquestração          |
|   2018    |Item de configuração em andamento, aguardando rede            |
|   2019    |Item de configuração em andamento, VE de atualização pendente              |
|   2020    |Item de configuração em andamento, atualizando VE            |
|   3000    |Requisitos não atendidos do item de configuração                       |
|   3001    |Requisitos não atendidos do item de configuração, host não aplicável           |
|   4000    |Item de configuração desconhecido                    |
|   5000    |Erro de item de configuração                          |
|   5001    |Erro ao avaliar item de configuração                   |
|   5002    |Erro ao instalar item de configuração                   |
|   5003    |Erro ao recuperar conteúdo de item de configuração               |
|   5004    |Erro ao instalar dependência de item de configuração            |
|   5005    |Erro ao recuperar dependência de conteúdo de item de configuração        |
|   5006    |Erro de conflito de regras de item de configuração                   |
|   5007    |Erro ao aguardar nova tentativa de item de configuração                |
|   5008    |Erro ao desinstalar substituição de item de configuração        |
|   5009    |Erro ao baixar substituição de item de configuração               |
|   5010    |Erro ao atualizar VE de item de configuração                  |
|   5011    |Erro ao instalar licença de item de configuração               |
|   5012    |Erro ao recuperar permissão para todos os aplicativos confiáveis de item de configuração       |
|   5013    |Erro de item de configuração, não há licenças disponíveis            |
|   5014    |Erro de item de configuração, não há suporte para o sistema operacional                 |
|   6000    |A inicialização de item de configuração foi bem-sucedida                           |
|   6010    |Erro de inicialização de item de configuração                           |
|   6020    |Inicialização de item de configuração desconhecida|

## <a name="1703-statetopictypeappciassignmentevaluatio"></a>1703 STATE_TOPICTYPE_APP_CI_ASSIGNMENT_EVALUATIO

    No State IDs.

## <a name="1704-statetopictypeappcilaunch"></a>1704 STATE_TOPICTYPE_APP_CI_LAUNCH

    No State IDs.

## <a name="1800-statetopictypeeventintrinsic"></a>1800 STATE_TOPICTYPE_EVENT_INTRINSIC

    No State IDs.

## <a name="1801-statetopictypeeventextrinsic"></a>1801 STATE_TOPICTYPE_EVENT_EXTRINSIC

    No State IDs.

## <a name="1900-statetopictypeepaminfection"></a>1900 STATE_TOPICTYPE_EP_AM_INFECTION

    No State IDs.

## <a name="1901-statetopictypeepamhealth"></a>1901 State_Topictype_Ep_Am_Health

    No State IDs.

## <a name="1902-statetopictypeepmalware"></a>1902 STATE_TOPICTYPE_EP_MALWARE

    No State IDs.

## <a name="1950-statetopictypeatphealthstatus"></a>1950 STATE_TOPICTYPE_ATP_HEALTH_STATUS

    No State IDs.

## <a name="2001-statetopictypeepclientdeployment"></a>2001 STATE_TOPICTYPE_EP_CLIENT_DEPLOYMENT

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Endpoint Protection não gerenciado       |
|   2   |Endpoint Protection aguardando instalação  |
|   3   |Endpoint Protection gerenciado         |
|   4   |Falha na instalação do Endpoint Protection     |
|   5   |Reinicialização pendente do Endpoint Protection  |
|   6   |Não há suporte para o Endpoint Protection       |
|   7   |Endpoint Protection cogerenciado      |

## <a name="2002-statetopictypeepclientpolicyapplication"></a>2002 STATE_TOPICTYPE_EP_CLIENT_POLICYAPPLICATION

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   0   |Status da aplicação da política do Endpoint Protection desconhecido        |
|   1   |Êxito na aplicação da política do Endpoint Protection         |
|   2   |Falha na aplicação da política do Endpoint Protection        |

## <a name="2003-statetopictypeclientaction"></a>2003 STATE_TOPICTYPE_CLIENT_ACTION

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   0   |  Desconhecida           |
|   1   |  Ativo            |
|   2   |  Inactive          |

## <a name="2100-statetopictypewpclientdeployment"></a>2100 STATE_TOPICTYPE_WP_CLIENT_DEPLOYMENT

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   | O proxy de ativação não está instalado          |
|   2   | O proxy de ativação está aguardando instalação       |
|   3   | O proxy de ativação foi instalado          |
|   4   | Falha na instalação do proxy de ativação       |
|   5   | O proxy de ativação está aguardando a reinicialização         |
|   6   | Não há suporte para o proxy de ativação neste sistema operacional   |
|   7   | Recusa do servidor de proxy de ativação        |
|   8   | Falha na desinstalação do proxy de ativação      |
|   9   | Não há suporte para o tempo de execução do proxy de ativação         |

## <a name="2200-statetopictypefdm"></a>2200 STATE_TOPICTYPE_FDM

    No State IDs.

## <a name="2201-statetopictypeccmcertbinding"></a>2201 STATE_TOPICTYPE_CCM_CERT_BINDING

    No State IDs.

## <a name="2202-statetopictypeserverstatistic"></a>2202 STATE_TOPICTYPE_SERVER_STATISTIC

    No State IDs.

## <a name="3000-statetopictypedmwnschannel"></a>3000 STATE_TOPICTYPE_DM_WNS_CHANNEL

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|0  | Configuração do canal do serviço de Notificação por push do Windows|

## <a name="4000-statetopictypemdmdeviceproperty"></a>4000 STATE_TOPICTYPE_MDM_DEVICE_PROPERTY

    No State IDs.

## <a name="4002-statetopictypemdmclientidenitity"></a>4002 STATE_TOPICTYPE_MDM_CLIENT_IDENITITY

    No State IDs.

## <a name="4003-statetopictypemdmapplicationrequest"></a>4003 STATE_TOPICTYPE_MDM_APPLICATION_REQUEST

    No State IDs.

## <a name="4004-statetopictypemdmapplicationstate"></a>4004 STATE_TOPICTYPE_MDM_APPLICATION_STATE

    No State IDs.

## <a name="4005-statetopictypemdmlicensedevicerelation"></a>4005 STATE_TOPICTYPE_MDM_LICENSE_DEVICE_RELATION

    No State IDs.

## <a name="4006-statetopictypemdmlicensekeys"></a>4006 STATE_TOPICTYPE_MDM_LICENSE_KEYS

    No State IDs.

## <a name="4007-statetopictypemdmpolicyassignment"></a>4007 STATE_TOPICTYPE_MDM_POLICY_ASSIGNMENT

    No State IDs.

## <a name="4008-statetopictypemdmandroidcount"></a>4008 STATE_TOPICTYPE_MDM_ANDROID_COUNT

    No State IDs.

## <a name="4009-statetopictypemdmslkstatus"></a>4009 STATE_TOPICTYPE_MDM_SLK_STATUS

    No State IDs.

## <a name="4010-statetopictypemdmusercompanytermacceptance"></a>4010 STATE_TOPICTYPE_MDM_USER_COMPANY_TERM_ACCEPTANCE

    No State IDs.

## <a name="4022-statetopictypemdmdepsyncnowstatus"></a>4022 STATE_TOPICTYPE_MDM_DEP_SYNCNOW_STATUS

    No State IDs.

## <a name="4023-statetopictypemdmmamstoreappsync"></a>4023 STATE_TOPICTYPE_MDM_MAM_STORE_APP_SYNC

    No State IDs.

## <a name="5000-statetopictypecertificateenrollment"></a>5000 STATE_TOPICTYPE_CERTIFICATE_ENROLLMENT

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Desafio emitido                    |
|   2   |Falha na emissão do desafio              |
|   3   |Falha na criação da solicitação                 |
|   4   |Falha no envio da solicitação               |
|   5   |Êxito na validação do desafio          |
|   6   |Falha na validação do desafio             |
|   7   |Falha na emissão                    |
|   8   |Emissão pendente                   |
|   9   |Emitido                      |
|   10  |Falha no processamento da resposta          |
|   11  |Resposta pendente                    |
|   12  |Registro bem-sucedido                    |
|   13  |Registro não necessário                   |
|   14  |Revogado                         |
|   15  |Removido da coleção                 |
|   16  |Renovação verificada                  |
|   17  |Falha na instalação              |
|   18  |Instalado                   |
|   19  |Falha na exclusão                   |
|   20  |Excluído                     |
|   21  |Renovação solicitada               |


## <a name="5001-statetopictypecertificatecrp"></a>5001 STATE_TOPICTYPE_CERTIFICATE_CRP

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Desafio emitido                       |
|   2   |Falha na emissão do desafio                 |
|   3   |Falha na criação da solicitação                    |
|   4   |Falha no envio da solicitação                  |
|   5   |Êxito na validação do desafio             |
|   6   |Falha na validação do desafio                |
|   7   |Falha na emissão                       |
|   8   |Emissão pendente                      |
|   9   |Emitido                         |
|   10  |Falha no processamento da resposta             |
|   11  |Resposta pendente                       |
|   12  |Registro bem-sucedido                       |
|   13  |Registro não necessário                      |
|   14  |Revogado                            |
|   15  |Removido da coleção                    |
|   16  |Renovação verificada                     |
|   17  |Falha na instalação                 |
|   18  |Instalado                      |
|   19  |Falha na exclusão                      |
|   20  |Excluído                        |
|   21  |Renovação solicitada                  |

## <a name="5200-statetopictyperesourceaccessstatus"></a>5200 STATE_TOPICTYPE_RESOURCE_ACCESS_STATUS

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   | Êxito na configuração de pin de status                   |
|   2   | Falha na configuração de pin de status                  |
|   3   | Não há suporte para a configuração de pin de status               |
|   4   | Configuração de pin de status em andamento             |

## <a name="6000-statetopictyperemoteappsubscriptionstatus"></a>6000 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_STATUS

    No State IDs.

## <a name="6001-statetopictyperemoteappsubscriptionsyncstatus"></a>6001 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_SYNC_STATUS

    No State IDs.

## <a name="6002-statetopictyperemoteappauthcookiessyncstatus"></a>6002 STATE_TOPICTYPE_REMOTEAPP_AUTHCOOKIES_SYNC_STATUS

    No State IDs.

## <a name="6003-statetopictyperemoteapplicationssyncstatus"></a>6003 STATE_TOPICTYPE_REMOTEAPPLICATIONS_SYNC_STATUS

    No State IDs.

## <a name="6004-statetopictyperemoteapplockresult"></a>6004 STATE_TOPICTYPE_REMOTEAPP_LOCK_RESULT

    No State IDs.

## <a name="7000-statetopictypeusercompanytermacceptance"></a>7000 STATE_TOPICTYPE_USER_COMPANY_TERM_ACCEPTANCE

    No State IDs.

## <a name="7001-statetopictypepfxcertificate"></a>7001 STATE_TOPICTYPE_PFX_CERTIFICATE

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Desafio emitido               |
|   2   |Falha na emissão do desafio         |
|   3   |Falha na criação da solicitação            |
|   4   |Falha no envio da solicitação          |
|   5   |Êxito na validação do desafio     |
|   6   |Falha na validação do desafio        |
|   7   |Falha na emissão               |
|   8   |Emissão pendente              |
|   9   |Emitido                 |
|   10  |Falha no processamento da resposta     |
|   11  |Resposta pendente               |
|   12  |Registro bem-sucedido               |
|   13  |Registro não necessário              |
|   14  |Revogado                    |
|   15  |Removido da coleção            |
|   16  |Renovação verificada             |
|   17  |Falha na instalação         |
|   18  |Instalado              |
|   19  |Falha na exclusão              |
|   20  |Excluído                |
|   21  |Renovação solicitada          |

## <a name="7010-statetopictypeconditionalaccesscompliance"></a>7010 STATE_TOPICTYPE_CONDITIONAL_ACCESS_COMPLIANCE

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
||  1   | Êxito na conformidade             |
|   2   | Falha de conformidade no pacote de gerenciamento      |
|   3   | Falha de conformidade no cliente      |
|   4   | Falha de conformidade no Intune      |
|   5   | Falha de conformidade no AAD         |
|   6   | Conformidade no comgmt Intune       |

## <a name="7200-statetopictypesuperpeerupdatecachemap"></a>7200 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CACHE_MAP

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Fonte de cache par adicionada                |
|   2   |Fonte de cache par removida          |

## <a name="7201-statetopictypesuperpeerupdateconfig"></a>7201 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CONFIG

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Fonte de cache par desativada              |
|   2   |A fonte de cache par está ativa                |

## <a name="7202-statetopictypedownloadaggregatedata"></a>7202 STATE_TOPICTYPE_DOWNLOAD_AGGREGATE_DATA
|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Baixar o upload de dados agregados       |

## <a name="7203-statetopictypepeersourcereqrejectionstats"></a>7203 STATE_TOPICTYPE_PEERSOURCE_REQ_REJECTION_STATS

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Upload de dados de rejeição da origem par     |

## <a name="7300-statetopictypeproxytraffic"></a>7300 STATE_TOPICTYPE_PROXY_TRAFFIC

    No State IDs.

## <a name="7301-statetopictypeproxyconnection"></a>7301 STATE_TOPICTYPE_PROXY_CONNECTION

    No State IDs.

## <a name="7302-statetopictypesrsusagedata"></a>7302 STATE_TOPICTYPE_SRS_USAGE_DATA

    No State IDs.

## <a name="7303-statetopictypeproxytrafficidentity"></a>7303 STATE_TOPICTYPE_PROXY_TRAFFIC_IDENTITY

    No State IDs.

## <a name="8001-statetopictypehasreport"></a>8001 STATE_TOPICTYPE_HAS_REPORT

|     ID da mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Há suporte para o atestado de integridade         |
|   2   |Não há suporte para o atestado de integridade         |

## <a name="statetopictypedeviceclientedplog"></a>STATE_TOPICTYPE_DEVICE_CLIENT_EDPLOG

    No State IDs.

## <a name="8003-statetopictypeenablelostmode"></a>8003 STATE_TOPICTYPE_ENABLE_LOSTMODE

    No State IDs.

## <a name="8004-statetopictypedisablelostmode"></a>8004 STATE_TOPICTYPE_DISABLE_LOSTMODE

    No State IDs.

## <a name="8005-statetopictypelocatedevice"></a>8005 STATE_TOPICTYPE_LOCATE_DEVICE

    No State IDs.

## <a name="8006-statetopictyperebootdevice"></a>8006 STATE_TOPICTYPE_REBOOT_DEVICE

    No State IDs.

## <a name="8007-statetopictypelogoutuser"></a>8007 STATE_TOPICTYPE_LOGOUTUSER

    No State IDs.

## <a name="8008-statetopictypeuserslist"></a>8008 STATE_TOPICTYPE_USERSLIST

    No State IDs.

## <a name="8009-statetopictypedeleteuser"></a>8009 STATE_TOPICTYPE_DELETEUSER

    No State IDs.

## <a name="8010-statetopictypecleanpcretaininguserdata"></a>8010 STATE_TOPICTYPE_CLEANPCRETAININGUSERDATA

    No State IDs.

## <a name="8011-statetopictypecleanpcwithoutretaininguserdata"></a>8011 STATE_TOPICTYPE_CLEANPCWITHOUTRETAININGUSERDATA

    No State IDs.

## <a name="8012-statetopictypesetdevicename"></a>8012 STATE_TOPICTYPE_SETDEVICENAME

    No State IDs.

## <a name="9000-statetopictypebookcicompliance"></a>9000 STATE_TOPICTYPE_BOOK_CI_COMPLIANCE

    No State IDs.

## <a name="9001-statetopictypebookcienforcement"></a>9001 STATE_TOPICTYPE_BOOK_CI_ENFORCEMENT

    No State IDs.

## <a name="next-steps"></a>Próximas etapas

- [Descrição das mensagens de estado no Configuration Manager](https://support.microsoft.com/help/4459394/description-of-state-messaging-in-system-center-configuration-manager)
- [Whitepaper de gerenciamento de atualizações de software para o Configuration Manager](https://www.microsoft.com/download/details.aspx?id=44578)
