---
title: "Pré-requisitos do perfil de certificado | Microsoft Docs"
description: "Saiba mais sobre os perfis de certificado no System Center Configuration Manager e suas dependências externas e dependências dentro do produto."
ms.custom: na
ms.date: 11/27/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0317fd02-3721-4634-b18b-7c976a4e92bf
caps.latest.revision: 9
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 593fbd0587d54490246f48ae54f666bac6b7830d
ms.openlocfilehash: 08fb30da2060728142648f13846be737f98f2276


---
# <a name="prerequisites-for-certificate-profiles-in-system-center-configuration-manager"></a>Pré-requisitos dos perfis de certificado no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Os perfis de certificado no System Center Configuration Manager (também conhecido como ConfigMgr ou SCCM) têm dependências externas e dependências dentro do produto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Uma AC (autoridade de certificação) emissora corporativa executando AD CS (Serviços de Certificados do Active Directory).<br /><br /> Para revogar certificados, a conta de computador do servidor do site no topo da hierarquia exige direitos para *Emitir e Gerenciar Certificados* para cada modelo de certificado usado por um perfil de certificado no Configuration Manager. Como alternativa, conceda permissões do Gerenciador de Certificados para fornecer permissões em todos os modelos de certificado usados pela AC<br /><br /> Suporte para aprovação do gerente às solicitações de certificado. No entanto, os modelos de certificado usados para emitir certificados devem ser configurados para **Fornecer na solicitação** para a entidade do certificado, de forma que o System Center Configuration Manager possa fornecer esse valor automaticamente.|Para obter mais informações sobre os Serviços de Certificados do Active Directory, confira a documentação do Windows Server.<br /><br /> Para o Windows Server 2012: [Visão geral dos Serviços de Certificados do Active Directory](http://go.microsoft.com/fwlink/p/?LinkId=286744)<br /><br /> Para o Windows Server 2008: [Serviços de Certificados do Active Directory no Windows Server 2008](http://go.microsoft.com/fwlink/p/?LinkId=115018)|  
|O serviço de função do Serviço de Registro de Dispositivo de Rede para Serviços de Certificados do Active Directory, em execução no Windows Server 2012 R2.<br /><br /> Além disso:<br /><br /> Números de porta diferentes de TCP 443 (para HTTPS) ou TCP 80 (para HTTP) não têm suporte para a comunicação entre o cliente e o Serviço de Registro de Dispositivo de Rede.<br /><br /> O servidor que executa o Serviço de Registro de Dispositivo de Rede deve estar em um servidor diferente da AC emissora.|O System Center Configuration Manager se comunica com o Serviço de Registro de Dispositivo de Rede no Windows Server 2012 R2 para gerar e verificar solicitações do protocolo SCEP.<br /><br /> Se você emitir certificados aos usuários ou dispositivos que se conectam pela Internet, tais como dispositivos gerenciados pelo Microsoft Intune, então estes dispositivos deverão poder acessar o servidor executando o Serviço de Registro de Dispositivo de Rede pela Internet. Por exemplo, instale o servidor em uma rede de perímetro (também conhecida como Rede de perímetro, e sub-rede filtrada).<br /><br /> Se você tiver um firewall entre o servidor que executa o Serviço de Registro de Dispositivo de Rede e a AC emissora, deverá configurar o firewall para permitir o tráfego de comunicação (DCOM) entre os dois servidores. Este requisito de firewall também se aplica ao servidor executando o servidor do site do System Center Configuration Manager e a AC emissora, para que o System Center Configuration Manager possa revogar certificados.<br /><br /> Se o Serviço de Registro de Dispositivo de Rede estiver configurado para solicitar SSL (uma prática recomendada de segurança), verifique se os dispositivos de conexão podem acessar a CRL (lista de certificados revogados) para validar o certificado do servidor.<br /><br /> Para mais informações sobre o Serviço de Registro de Dispositivo de Rede no Windows Server 2012 R2, consulte [Using a Policy Module with the Network Device Enrollment Service (Usando um Módulo de Política com o Serviço de Registro de Dispositivo de Rede)](http://go.microsoft.com/fwlink/p/?LinkId=328657).|  
|Se a AC emissora executa o Windows Server 2008 R2, este servidor requer um hotfix para solicitações de renovação do SCEP.|Se o hotfix não estiver instalado no computador da AC emissora, instale-o. Para obter mais informações, leia o artigo [2483564: A solicitação de renovação para um certificado SCEP falhará no Windows Server 2008 R2 se o certificado for gerenciado com o NDES](http://go.microsoft.com/fwlink/?LinkId=311945) na Base de Dados de Conhecimento Microsoft.|  
|Um certificado de autenticação cliente PKI e um certificado da AC raiz exportado.|Esse certificado autentica o servidor que executa o Serviço de Registro de Dispositivo de Rede para o System Center Configuration Manager.<br /><br /> Para obter mais informações, consulte [Requisitos de certificado PKI para o System Center Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md).|  
|Sistemas operacionais de dispositivos com suporte.|Você pode implantar perfis de certificado em dispositivos que executam os sistemas operacionais iOS, Windows 8.1, Windows RT 8.1, Windows 10 e Android.|  

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Função de sistema de site do ponto de registro de certificado|Para poder usar perfis de certificado, você deve instalar a função de sistema de site do ponto de registro de certificado. Essa função se comunica com o banco de dados do System Center Configuration Manager, o servidor do site do System Center Configuration Manager e o Módulo de Política do System Center Configuration Manager.<br /><br /> Para obter mais informações sobre os requisitos do sistema para essa função de sistema de sites e onde instalar a função na hierarquia, confira a seção **Requisitos do Sistema de Sites** no tópico [Configurações com suporte para o System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md).<br /><br /> Observe que o ponto de registro de certificado não deve ser instalado no mesmo servidor que executa o Serviço de Registro de Dispositivo de Rede.|  
|O Módulo de Política do System Center Configuration Manager instalado no servidor que executa o serviço de função do Serviço de Registro de Dispositivo de Rede para os Serviços de Certificados do Active Directory|Para implantar perfis de certificado, é necessário instalar o Módulo de Política do System Center Configuration Manager. Você pode encontrar esse módulo de política na mídia de instalação do System Center Configuration Manager.|  
|Dados de descoberta|Os valores para a entidade do certificado e nome alternativo da entidade são fornecidos pelo System Center Configuration Manager e recuperados das informações coletadas na descoberta:<br /><br /> Para certificados de usuário: descoberta de Usuário do Active Directory<br /><br /> Para certificados de computador: Descoberta de Sistemas do Active Directory e Descoberta de Rede|  
|Permissões de segurança específicas para gerenciar os perfis de certificado|Você deve ter as seguintes permissões de segurança para gerenciar configurações de acesso aos recurso da empresa, como perfis de certificado, perfis de Wi-Fi e perfis VPN:<br /><br /> Para exibir e gerenciar alertas e relatórios para perfis de certificado: **Criar**, **Excluir**, **Modificar**, **Modificar Relatório**, **Ler**e **Executar Relatório** para o objeto **Alertas** .<br /><br /> Para criar e gerenciar perfis de certificado: **Criar Política**, **Modificar Relatório**, **Ler** e **Executar Relatório** para o objeto **Perfil de Certificado** .<br /><br /> Para gerenciar implantações de perfil de Wi-Fi, certificado e VPN: **Implantar Políticas de Configuração**, **Modificar Alerta de Status do Cliente**, **Ler**e **Ler Recurso** para o objeto **Coleção** .<br /><br /> Para gerenciar todas as políticas de configuração: **Criar**, **Excluir**, **Modificar**, **Ler** e **Definir Escopo de Segurança** para o objeto **Política de Configuração** .<br /><br /> Para executar consultas relacionadas aos perfis de certificado: permissão para **Ler** para o objeto **Consulta** .<br /><br /> Para exibir as informações de perfis de certificado no console do System Center Configuration Manager: permissão para **Ler** o objeto **Site**.<br /><br /> Para exibir mensagens de status para perfis de certificado: permissão para **Ler** para o objeto **Mensagens de Status** .<br /><br /> Para criar e modificar o perfil de certificado de autoridade de certificação confiável: **Criar Política**, **Modificar Relatório**, **Ler** e **Executar Relatório** para o objeto **Perfil Certificado de Autoridade de Certificação Confiável** .<br /><br /> Para criar e gerenciar Perfis de VPN: **Criar Política**, **Modificar Relatório**, **Ler** e **Executar Relatório** para o objeto **Perfil de VPN** .<br /><br /> Para criar e gerenciar perfis Wi-Fi: permissões para **Criar Política**, **Modificar Relatório**, **Ler** e **Executar Relatório** para o objeto **Perfil Wi-Fi** .<br /><br /> A função de segurança do **Gerente de Acesso de Recurso da Empresa** inclui essas permissões que são necessárias para gerenciar os perfis de certificado no System Center Configuration Manager. Para obter mais informações, consulte a seção **Configure role-based administration** no tópico [Configure security in System Center Configuration Manager](../../core/plan-design/security/configure-security.md) .|  



<!--HONumber=Dec16_HO3-->

