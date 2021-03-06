---
title: Conector da Defesa Contra Ameaças para Dispositivos Móveis do Pradeo com o Intune
titleSuffix: Intune on Azure
description: Aprenda a integrar o Intune com o conector Pradeo Mobile Threat Defense para controlar o acesso de dispositivos móveis aos seus recursos corporativos.
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
ms.assetid: cde4d389-1770-4226-85a3-a2f3b3fb92a3
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5cde4c4e90004dd9bb287b9e86f9dfcc541e4a33
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83984969"
---
# <a name="pradeo-mobile-threat-defense-connector-with-intune"></a>Conector da Defesa Contra Ameaças para Dispositivos Móveis do Pradeo com o Intune

Pode controlar o acesso de dispositivos móveis a recursos corporativos utilizando o Acesso Condicional com base na avaliação de risco realizada pela Pradeo, uma solução de Defesa de Ameaças Móveis (MTD) que se integra com a Microsoft Intune. O risco é avaliado com base na telemetria recolhida dos dispositivos a executar a aplicação Pradeo.

Pode configurar políticas de Acesso Condicional com base na avaliação de risco pradeo ativada através de políticas de conformidade de dispositivos Intune, que pode utilizar para permitir ou bloquear dispositivos não conformes para aceder a recursos corporativos com base em ameaças detetadas.

> [!NOTE]
> Este fornecedor de Defesa de Ameaças Móveis não é suportado para dispositivos não matriculados.

## <a name="supported-platforms"></a>Plataformas suportadas

- **Android 4.0.3 e posterior**

- **iOS 7 e posterior**

## <a name="prerequisites"></a>Pré-requisitos

- Azure Active Directory Premium

- Subscrição do Microsoft Intune

- Segurança do Pradeo para a subscrição da Defesa Contra Ameaças para Dispositivos Móveis

  - Para obter mais informações, consulte o [site do Pradeo](https://www.pradeo.com/en-US/mobile-threat-protection).

## <a name="how-do-intune-and-pradeo-help-protect-your-company-resources"></a>Como é que o Intune e o Pradeo ajudam a proteger os recursos da empresa?

A aplicação Pradeo para Android e iOS/iPadOS captura sistema de ficheiros, stack de rede, dispositivo e telemetria de aplicações sempre que disponível, e depois envia os dados de telemetria para o serviço de nuvem Pradeo para avaliar o risco do dispositivo para ameaças móveis.

A política de conformidade de dispositivos do Intune inclui uma regra para a Defesa Contra Ameaças para Dispositivos Móveis do Pradeo, que se baseia na avaliação de riscos do Pradeo. Quando esta regra está ativada, o Intune avalia a conformidade do dispositivo com a política que ativou. Caso se verifique que o dispositivo não está em conformidade, será bloqueado o acesso dos utilizadores aos recursos empresariais como o Exchange Online e o SharePoint Online. Os utilizadores também recebem orientações da aplicação Pradeo instalada nos respetivos dispositivos para resolver o problema e recuperar o acesso a recursos empresariais.

## <a name="sample-scenarios"></a>Cenários de exemplo

Seguem-se alguns cenários comuns.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Controlar o acesso com base em ameaças de aplicações maliciosas

Quando forem detetadas aplicações maliciosas, como software maligno, nos dispositivos, pode impedir os dispositivos de fazer as seguintes ações até a ameaça ser resolvida:

- Ligar ao e-mail empresarial

- Sincronizar ficheiros empresariais com a aplicação OneDrive for Work

- Aceder às aplicações da empresa

*Bloquear quando as aplicações maliciosas forem detetadas:*

![Imagem conceptual de aplicações maliciosas detetada](./media/pradeo-mobile-threat-defense-connector/pradeo-maliciousapps-blocked.png)

*Acesso concedido na remediação:*

![Acesso concedido a aplicações maliciosas detetadas](./media/pradeo-mobile-threat-defense-connector/pradeo-maliciousapps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Controlar o acesso com base em ameaças à rede

Detete ameaças à rede, tal como ataques **Man-in-the-middle**, e proteja o acesso a redes Wi-Fi com base no risco do dispositivo.

*Bloquear o acesso à rede através do Wi-Fi:*

![Bloquear o acesso à rede através de Wi-Fi](./media/pradeo-mobile-threat-defense-connector/pradeo-network-wifi-blocked.png)

*Acesso concedido na remediação:*

![Imagem conceptual do Acesso concedido na reparação](./media/pradeo-mobile-threat-defense-connector/pradeo-network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controlar o acesso ao SharePoint Online com base em ameaças à rede

Detete ameaças à sua rede, tal como ataques **Man-in-the-middle**, e impeça a sincronização de ficheiros empresariais com base no risco do dispositivo.

*Block SharePoint Online quando são detetadas ameaças de rede:*

![Bloquear o SharePoint Online quando forem detetadas ameaças à rede](./media/pradeo-mobile-threat-defense-connector/pradeo-network-spo-blocked.png)

*Acesso concedido na remediação:*

![Imagem conceptual do Acesso concedido na reparação por exemplo sharepoint](./media/pradeo-mobile-threat-defense-connector/pradeo-network-spo-unblocked.png)

<!-- 
### Control access on unenrolled devices based on threats from malicious apps

When the Pradeo Mobile Threat Defense solution considers a device to be infected:

![App protection policy blocks due to detected malware](./media/pradeo-mobile-threat-defense-connector/pradeo-app-policy-block.png)

Access is granted on remediation:

![Access is granted on remediation for App protection policy](./media/pradeo-mobile-threat-defense-connector/pradeo-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Passos seguintes

- [Integrar o Pradeo com o Intune](pradeo-mtd-connector-integration.md)

- [Configurar as aplicações do Pradeo](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Criar uma política de conformidade de dispositivo do Pradeo](mtd-device-compliance-policy-create.md)

- [Ativar o conector de MTD do Pradeo](mtd-connector-enable.md)
