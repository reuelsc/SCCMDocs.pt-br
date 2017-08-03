# Visão geral
## [O que é um MDM híbrido?](understand/hybrid-mobile-device-management.md)
## [Escolher Intune autônomo ou MDM híbrido](understand/choose-between-standalone-intune-and-hybrid-mobile-device-management.md)
## [Novidades no MDM híbrido](understand/whats-new-in-hybrid-mobile-device-management.md)

# [Planejamento e design](plan-design/plan-hybrid-mobile-device-management.md)
## [Plataformas de dispositivos com suporte](plan-design/supported-device-platforms-for-hybrid.md)
## [Métodos de registro do dispositivo](plan-design/device-enrollment-methods.md)

# [Introdução](deploy-use/setup-hybrid-mdm.md)
## [Criar uma coleção de MDM](deploy-use/create-mdm-collection.md)
## [Confirmar requisitos de nome de domínio](deploy-use/confirm-dns.md)
## [Configurar a assinatura do Intune](deploy-use/configure-intune-subscription.md)
## [Adicionar termos e condições](deploy-use/terms-and-conditions.md)
## [Criar um ponto de conexão de serviço](deploy-use/create-service-connection-point.md)
## [Habilitar o registro de plataforma](deploy-use/enable-platform-enrollment.md)
### [iOS e Mac](deploy-use/enroll-hybrid-ios-mac.md)
### [Windows](deploy-use/enroll-hybrid-windows.md)
### [Android](deploy-use/enroll-hybrid-android.md)
## [Configurar gerenciamento adicional](deploy-use/set-up-additional-management.md)
## [Verificar a configuração do MDM](deploy-use/verify-mdm-configuration.md)

# Instruções
## [Registrar dispositivos de propriedade do usuário (BYOD)](deploy-use/enroll-user-owned-devices.md)
## [Registrar dispositivos corporativos](deploy-use/enroll-company-owned-devices.md)
### [Registro de DEP iOS](deploy-use/ios-device-enrollment-program-for-hybrid.md)
### [Registro do Apple Configurator](deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)
### [Gerenciador de registro de dispositivos](deploy-use/enroll-devices-with-device-enrollment-manager.md)
### [Pré-declarar ID de hardware](deploy-use/predeclare-devices-with-hardware-id.md)
### [Gerenciar o bloqueio de ativação do iOS](deploy-use/manage-ios-activation-lock.md)
### [Afinidade de dispositivo de usuário](deploy-use/user-affinity-for-hybrid-managed-devices.md)

## [Desativar/apagar, bloquear, redefinir dispositivos](deploy-use/wipe-lock-reset-devices.md)
## [Configurar o inventário de hardware](deploy-use/mobile-device-hardware-inventory-hybrid.md)
## [Configurar o inventário de software](deploy-use/software-inventory-mobile-devices.md)

## [Gerenciar configurações de conformidade](deploy-use/manage-compliance-settings.md)
### [Windows 8.1 e Windows 10](deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
### [Windows Phone](deploy-use/create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)
### [iOS e Mac OS X](deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)
### [Android e Samsung KNOX Standard](deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)
### [Android for Work](deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client.md)

## [Sincronizar dispositivos registrados no Intune](deploy-use/sync-intune-device.md)

## [Gerenciar aplicativos](deploy-use/management-tasks-applications.md)
### [Criar aplicativos iOS](deploy-use/creating-ios-applications.md)
### [Políticas de configuração de aplicativo iOS](deploy-use/configure-ios-apps-with-app-configuration-policies.md)
### [Aplicativos iOS comprados por volume](deploy-use/manage-volume-purchased-ios-apps.md)
### [Criar aplicativos do Windows Phone](deploy-use/creating-windows-phone-applications.md)
### [Criar aplicativos Android](deploy-use/creating-android-applications.md)
### [Políticas de gerenciamento de aplicativos móveis](deploy-use/protect-apps-using-mam-policies.md)
### [Políticas do Managed Browser](deploy-use/manage-internet-access-using-managed-browser-policies.md)
### [Aplicativos da Windows Store para Empresas](deploy-use/windows-store-for-business.md)

## [Gerenciar uma assinatura do Intune](deploy-use/manage-intune-subscriptions.md)

## [Alterar sua autoridade de MDM](deploy-use/change-mdm-authority.md)

## Gerenciar o acesso de recursos
### [Criar perfis de Wi-Fi](deploy-use/create-wifi-profiles.md)
### [Criar perfis de certificado PFX](deploy-use/create-pfx-certificate-profiles.md)
### [Importar perfis de certificado PFX](deploy-use/import-pfx-certificate-profiles.md)
### [Perfis de VPN](deploy-use/create-vpn-profiles.md)
### [Criar perfis de email](deploy-use/create-exchange-activesync-profiles.md)
### [Configurações do Windows Hello para Empresas ](deploy-use/windows-hello-for-business-settings.md)

## [Gerenciar acesso condicional](deploy-use/manage-access-to-services.md)
### [Políticas de conformidade do dispositivo](deploy-use/device-compliance-policies.md)
### [Criar uma política de conformidade do dispositivo](deploy-use/create-compliance-policy.md)
### [Gerenciar o acesso ao email](deploy-use/manage-email-access.md)
### [Gerenciar o acesso ao SharePoint Online](deploy-use/manage-sharepoint-online-access.md)
### [Gerenciar o acesso do Skype for Business Online](deploy-use/manage-skype-for-business-online-access.md)
### [Gerenciar o acesso ao Dynamics CRM Online](deploy-use/manage-dynamics-crm-online-access.md)
### [Gerenciar o acesso do computador aos serviços do O365](deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)

## [Gerenciar o acesso com base em riscos de dispositivo](deploy-use/mobile-threat-defense.md)
### [Lookout no Configuration Manager](deploy-use/lookout-mobile-threat-defense-in-configuration-manager.md)
#### [Configurar o recurso Lookout Mobile Threat Defense](deploy-use/set-up-your-subscription-with-lookout.md)
#### [Habilitar o Lookout no Intune](deploy-use/enable-lookout-connection-in-intune.md)
#### [Implantar o Lookout para aplicativos de trabalho](deploy-use/configure-and-deploy-lookout-for-work-apps.md)
#### [Criar política de conformidade do Lookout](deploy-use/enable-device-threat-protection-rule-compliance-policy.md)
#### [Solucionar problemas de integração do Lookout](deploy-use/troubleshoot-lookout-integration.md)
#### [Monitorar o recurso Mobile Threat Defense](deploy-use/monitor-mobile-threat-defense-compliance.md)

# MDM (Gerenciamento de dispositivos móveis) local
## [O que é o MDM local](understand/manage-mobile-devices-with-on-premises-infrastructure.md)
## [Planejamento de MDM local](plan-design/plan-on-premises-mdm.md)

## [Etapas de instalação](get-started/preparation-steps-for-on-premises-mdm.md)
### [Configurar a assinatura do Intune](get-started/set-up-intune-subscription-on-premises-mdm.md)
### [Instalar funções locais](get-started/install-site-system-roles-for-on-premises-mdm.md)
### [Configurar certificados](get-started/set-up-certificates-on-premises-mdm.md)
### [Configurar para registro](get-started/set-up-device-enrollment-on-premises-mdm.md)

## [Registrar dispositivos para MDM local](deploy-use/enroll-devices-on-premises-mdm.md)
### [Registro de usuário](deploy-use/user-enroll-devices-on-premises-mdm.md)
### [Registro em massa](deploy-use/bulk-enroll-devices-on-premises-mdm.md)
## [Gerenciar dispositivos](deploy-use/onprem-manage-devices.md)
## [Gerenciar aplicativos](deploy-use/onprem-manage-applications.md)
## [Proteger dados e dispositivos](deploy-use/onprem-protect-data-devices.md)

# [Gerenciamento de dispositivo com o Exchange](deploy-use/manage-mobile-devices-with-exchange-activesync.md)
