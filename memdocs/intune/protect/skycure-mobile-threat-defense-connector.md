---
title: Conector da Symantec com o Microsoft Intune
titleSuffix: Microsoft Intune
description: Saiba mais sobre como integrar o Symantec Endpoint Protection Mobile para controlar o acesso de dispositivos móveis aos seus recursos empresariais.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: df4ce3f6-a093-432c-ab86-7a83865e389e
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3dcca264716b35600addd917e0ee7f309f530b70
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988340"
---
# <a name="symantec-endpoint-protection-mobile-connector"></a>Conector do Symantec Endpoint Protection Mobile

Pode controlar o acesso de dispositivos móveis a recursos corporativos utilizando o Acesso Condicional com base na avaliação de risco realizada pela Symantec Endpoint Protection Mobile (SEP Mobile), uma solução de defesa de ameaças móveis que se integra com a Microsoft Intune. O risco é avaliado com base na telemetria recolhida dos dispositivos com o SEP Mobile, incluindo:

- Defesa física

- Defesa da rede

- Defesa da aplicação

- Defesa contra vulnerabilidades

Pode permitir a avaliação de risco seP Mobile através de políticas de conformidade de dispositivos Intune e, em seguida, utilizar políticas de Acesso Condicional para permitir ou bloquear o acesso não conforme do dispositivo aos recursos corporativos com base em ameaças detetadas.

> [!NOTE]
> Este fornecedor de Defesa de Ameaças Móveis não é suportado para dispositivos não matriculados.

## <a name="supported-platforms"></a>Plataformas suportadas

- **Android 4.1 e posterior**

- **iOS 8 e posterior**

## <a name="pre-requisites"></a>Pré-requisitos

- Azure Active Directory Premium

- Subscrição do Microsoft Intune

- Subscrição do Symantec Endpoint Protection Mobile

Para obter mais informações, veja o [site da Symantec](https://help.symantec.com/cs/sep_mobile/SEPMOBILE/v131237277_v127904070/Integrating-Microsoft-Intune-with-Endpoint-Protection-Mobile?locale=EN_US).

## <a name="how-do-intune-and-sep-mobile-help-protect-your-company-resources"></a>Como é que o Intune e o SEP Mobile ajudam a proteger os recursos da empresa?

O aplicativo SEP Mobile para Android ou iOS/iPadOS captura sistema de ficheiros, pilha de rede, dispositivo e telemetria de aplicações sempre que disponível, envia-o depois para o serviço de nuvem Symantec para avaliar o risco do dispositivo para ameaças móveis.

A política de conformidade de dispositivos do Intune inclui uma regra para o SEP Mobile, que se baseia na avaliação de riscos do SEP Mobile. Quando esta regra está ativada, o Intune avalia a conformidade do dispositivo com a política que ativou.

Se o dispositivo for considerado não conforme, o acesso a recursos como o Exchange Online e o SharePoint Online será bloqueado. Os utilizadores com os dispositivos bloqueados recebem orientações da aplicação SEP Mobile para resolver o problema e recuperar o acesso aos recursos empresariais.

O Intune suporta dois modos de integração com o SEP Mobile:

- A **Configuração básica**, que é um modo só de leitura que permite a visibilidade do SEP Mobile para dispositivos no Intune.

- A **Integração total**, que permite ao SEP Mobile comunicar detalhes de incidentes de segurança e riscos do dispositivo ao Intune.

## <a name="sample-scenarios"></a>Cenários de exemplo

Seguem-se alguns cenários comuns:

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Controlar o acesso com base em ameaças de aplicações maliciosas

Quando forem detetadas aplicações maliciosas, como software maligno, nos dispositivos, pode bloquear os dispositivos até a ameaça ser resolvida:

- Ligar ao e-mail empresarial

- Sincronizar ficheiros empresariais com a aplicação OneDrive for Work

- Aceder às aplicações da empresa

*Bloquear quando as aplicações maliciosas forem detetadas:*

![Imagem conceptual de aplicações maliciosas detetada](./media/skycure-mobile-threat-defense-connector/symantec-arch-1.png)

*Acesso concedido na remediação:*

![Imagem de Acesso concedida em reparação após aplicações maliciosas detetadas](./media/skycure-mobile-threat-defense-connector/symantec-arch-2.png)

### <a name="control-access-based-on-threat-to-network"></a>Controlar o acesso com base em ameaças à rede

Detete ameaças como **Man-in-the-middle** na rede e proteja o acesso às redes Wi-Fi com base no risco do dispositivo.

*Bloquear o acesso à rede através do Wi-Fi:*

![Bloquear o acesso à rede através de Wi-Fi](./media/skycure-mobile-threat-defense-connector/symantec-arch-3.png)

*Acesso concedido na remediação:*

![Acesso concedido na remediação](./media/skycure-mobile-threat-defense-connector/symantec-arch-4.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controlar o acesso ao SharePoint Online com base em ameaças à rede

Detete ameaças na rede, tais como ataques **Man-in-the-middle**, e impeça a sincronização de ficheiros empresariais com base no risco do dispositivo.

*Block SharePoint Online quando são detetadas ameaças de rede:*

![Bloquear o SharePoint Online quando forem detetadas ameaças à rede](./media/skycure-mobile-threat-defense-connector/symantec-arch-5.png)

*Acesso concedido na remediação:*

![Exemplo de acesso concedido na remediação para o SharePoint](./media/skycure-mobile-threat-defense-connector/symantec-arch-6.png)

<!-- 
### Control access on unenrolled devices based on threats from malicious apps

When the Symantec Endpoint Protection Mobile Threat Defense solution considers a device to be infected:
![App protection policy blocks due to detected malware](./media/skycure-mobile-threat-defense-connector/symantec-app-policy-block.png)

Access is granted on remediation:

![Access is granted on remediation for App protection policy](./media/skycure-mobile-threat-defense-connector/symantec-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Passos seguintes

Veja a seguir os passos necessários para integrar o Intune com o SEP Mobile:

- [Configurar a integração do SEP Mobile com o Intune](skycure-mtd-connector-integration.md)

- [Adicione e atribua aplicações SEP Mobile, Microsoft Authenticator e iOS/iPadOS política de configuração de apps](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Criar a política de conformidade de dispositivos do SEP Mobile com o Intune](mtd-device-compliance-policy-create.md)

- [Ativar o conector do SEP Mobile MTD no Intune](mtd-connector-enable.md)
