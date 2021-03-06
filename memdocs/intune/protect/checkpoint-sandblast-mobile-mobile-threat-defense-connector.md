---
title: Configurar o ponto de verificação SandBlast MTD
titleSuffix: Microsoft Intune
description: Saiba como integrar o Intune com a solução de Defesa Contra Ameaças Check Point SandBlast Mobile para controlar o acesso aos seus recursos empresariais a partir de dispositivos móveis.
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
ms.assetid: 706a4228-9bdf-41e0-b8d1-64c923dd2d2b
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: e9c1450af064caa1f7572da0ab4753e9db68484c
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989268"
---
# <a name="check-point-sandblast-mobile-threat-defense-connector-with-intune"></a>Conector de Defesa Contra Ameaças do Check Point SandBlast Mobile no Intune

Pode controlar o acesso de dispositivos móveis a recursos corporativos utilizando o Acesso Condicional com base na avaliação de risco realizada pelo Check Point SandBlast Mobile, uma solução de defesa de ameaças móveis que se integra com a Microsoft Intune. O risco é avaliado com base na telemetria recolhida dos dispositivos que executam a aplicação Check Point SandBlast Mobile.

Pode configurar políticas de acesso condicional com base na avaliação de risco móvel Check Point SandBlast, ativada através de políticas de conformidade do dispositivo Intune, que pode utilizar para permitir ou bloquear dispositivos não conformes para aceder a recursos corporativos com base em ameaças detetadas.

> [!NOTE]
> Este fornecedor de Defesa de Ameaças Móveis não é suportado para dispositivos não matriculados.

## <a name="supported-platforms"></a>Plataformas suportadas

- **Android 4.1 e posterior**

- **iOS 8 e posterior**

## <a name="pre-requisites"></a>Pré-requisitos

- Azure Active Directory Premium

- Subscrição do Microsoft Intune

- Subscrição do Check Point SandBlast Mobile – Defesa Contra Ameaças
  - Veja o [site do Check Point SandBlast](https://www.checkpoint.com/) para obter mais informações.

## <a name="how-do-intune-and-check-point-sandblast-mobile-help-protect-your-company-resources"></a>De que forma o Intune e o Check Point SandBlast Mobile ajudam a proteger os recursos da sua empresa?

Check Point Sandblast Mobile aplicação para Android e iOS/iPadOS captura sistema de ficheiros, stack de rede, dispositivo e telemetria de aplicações sempre que disponível, em seguida, envia os dados de telemetria para o serviço de nuvem Check Point SandBlast para avaliar o risco do dispositivo para ameaças móveis.

A política de conformidade do dispositivo do Intune inclui uma regra para a Defesa Contra Ameaças do Check Point SandBlast Mobile, que é baseada na avaliação de riscos do Check Point SandBlast. Quando esta regra está ativada, o Intune avalia a conformidade do dispositivo com a política que ativou. Caso se verifique que o dispositivo não está em conformidade, será bloqueado o acesso dos utilizadores aos recursos empresariais como o Exchange Online e o SharePoint Online. Os utilizadores também recebem orientações da aplicação Check Point SandBlast Mobile instalada nos respetivos dispositivos para resolver o problema e recuperar o acesso a recursos empresariais.

Seguem-se alguns cenários comuns:

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Controlar o acesso com base em ameaças de aplicações maliciosas

Quando forem detetadas aplicações maliciosas, como software maligno, nos dispositivos, pode bloquear os dispositivos até a ameaça ser resolvida:

- Ligar ao e-mail empresarial

- Sincronizar ficheiros empresariais com a aplicação OneDrive for Work

- Aceder às aplicações da empresa

*Bloquear quando as aplicações maliciosas forem detetadas:*

> [!div class="mx-imgBorder"]
> ![MTD do Check Point – bloqueio quando as aplicações maliciosas são detetadas](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-2.PNG)

*Acesso concedido na remediação:*

> [!div class="mx-imgBorder"]
> ![MTD do Check Point – acesso concedido](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-3.PNG)

### <a name="control-access-based-on-threat-to-network"></a>Controlar o acesso com base em ameaças à rede

Detete ameaças como **Man-in-the-middle** na rede e proteja o acesso às redes Wi-Fi com base no risco do dispositivo.

*Bloquear o acesso à rede através do Wi-Fi:*

> [!div class="mx-imgBorder"]
> ![MTD do Check Point – bloqueio do acesso à rede através de Wi-Fi](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-4.PNG)

*Acesso concedido na remediação:*

> [!div class="mx-imgBorder"]
> ![MTD do Check Point – acesso Wi-Fi concedido](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-5.PNG)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controlar o acesso ao SharePoint Online com base em ameaças à rede

Detete ameaças na rede, tais como ataques **Man-in-the-middle**, e impeça a sincronização de ficheiros empresariais com base no risco do dispositivo.

*Block SharePoint Online quando são detetadas ameaças de rede:*

> [!div class="mx-imgBorder"]
> ![MTD do Check Point – bloqueio do acesso ao SharePoint Online](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-6.PNG)

*Acesso concedido na remediação:*

> [!div class="mx-imgBorder"]
> ![MTD do Check Point – acesso ao SharePoint Online concedido](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-7.PNG)

<!-- ### Control access on unenrolled devices based on threats from malicious apps

When the Check Point Sandblast Mobile Threat Defense solution considers a device to be infected:
> [!div class="mx-imgBorder"]
> ![App protection policy blocks due to detected malware](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/sandblast-app-policy-block.png)

Access is granted on remediation:

> [!div class="mx-imgBorder"]
> ![Access is granted on remediation for App protection policy](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/sandblast-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Passos seguintes

- [Integrar o Check Point SandBlast com o Intune](checkpoint-sandblast-mobile-mtd-connector-integration.md)

- [Configurar a aplicação Check Point SandBlast Mobile](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Criar a política de conformidade de dispositivos do CheckPoint SandBlast Mobile](mtd-device-compliance-policy-create.md)

- [Ativar o conector da MTD do CheckPoint SandBlast Mobile](mtd-connector-enable.md)
