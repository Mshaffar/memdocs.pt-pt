---
title: Determinar os requisitos de cenários de casos de utilização
titleSuffix: Microsoft Intune
description: Este artigo ajuda-o a determinar os requisitos de cenários de casos de utilização e de casos de subutilização para uma implementação apenas na cloud do Microsoft Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: fd8cb5f7-19f0-4d80-8825-2bafa49624af
ms.reviewer: jeffbu, cgerth
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6e002b62fb00c4e2e8523848c4c64ad7a54ce024
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331037"
---
# <a name="determine-use-case-scenario-requirements"></a>Determinar os requisitos de cenários de casos de utilização

Nesta secção, determina os requisitos para cada grupo organizacional dentro de cada cenário de caso de utilização. Este processo ajuda-o a preparar-se para as outras áreas de planeamento de implementação do Intune, tais como a arquitetura e a estrutura, a integração e a implementação. Também pode ajudá-lo a identificar potenciais lacunas e desafios relacionados com o seu projeto de implementação do Intune.

Poderá ter diferentes conjuntos de requisitos para cada um dos seus cenários de casos de utilização e de casos de subutilização, bem como para os grupos organizacionais e as plataformas de dispositivos móveis associados. Por exemplo, os seus requisitos de cenários de casos de utilização empresarial podem exigir dispositivos para inscrição no Intune com um conjunto mais restritivo de definições do dispositivo, como um PIN de 6 carateres ou a cópia de segurança na cloud desativada. O seu cenário de casos de utilização “bring your own device” (BYOD) poderá ser menos restritivo e permitir um PIN de 4 carateres e a cópia de segurança na cloud.

Também poderá ter grupos organizacionais para o cenário de caso de utilização empresarial com diferentes conjuntos de requisitos (por exemplo, definições de PIN, perfil de Wi-Fi ou VPN, aplicações implementadas). Os seus requisitos poderão ser igualmente determinados pelas capacidades da plataforma do dispositivo móvel (por exemplo, leitor de impressões digitais, perfil de e-mail).

Veja alguns exemplos de requisitos de casos de utilização de uma organização que apresentam diferentes conjuntos de requisitos para cada cenário de casos de utilização e casos de subutilização, grupo organizacional e plataforma de dispositivo móvel. Também pode utilizar a tabela seguinte para introduzir os requisitos de caso de utilização da sua organização:

| **Casos de utilização** | **Casos de subutilização** | **Grupos** | **Plataformas de dispositivos** | **Requisitos** |
|:---:|:---:|:---:|:---:|:---:|
| Empresarial | Técnico de informação | RH, Finanças | iOS/iPadOS | E-mail seguro, definições do dispositivo, perfis, aplicações |                                                          
| Empresarial | Executivos | RH, Finanças | iOS/iPadOS | E-mail seguro, definições do dispositivo, perfis, aplicações |                                                         
| Empresarial | Local Público | Revenda | Android | Definições do dispositivo, perfis e aplicações |
| BYOD | Técnico de informação | Marketing, Vendas | iOS/iPadOS | E-mail seguro, definições do dispositivo, perfis, aplicações |                                                         
| BYOD | Executivos | Marketing, Vendas | iOS/iPadOS | E-mail seguro, definições do dispositivo, perfis, aplicações |

Pode [transferir um modelo da tabela acima](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) para introduzir os requisitos de casos de utilização e de casos de subutilização da sua organização.


## <a name="examples-of-requirements"></a>Exemplos de requisitos

Veja mais alguns exemplos que podem ser utilizados na coluna “Requisitos”:

- **E-mail seguro**
  - Acesso Condicional para Troca Online / No Local
  - Políticas de proteção de aplicações do Outlook

- **Definições do dispositivo**
  - PIN com quatro ou seis carateres
  - Restrição da cópia de segurança na cloud

- **Perfis**
  - Wi-Fi
  - VPN
  - E-mail (Windows 10 Mobile)

- **Aplicações**
  - Office 365 com políticas de proteção de aplicações
  - Linha de negócio (LOB) com políticas de proteção de aplicações

## <a name="next-steps"></a>Próximos passos

A secção seguinte fornece orientações relativas a [como pode desenvolver um plano de implementação do Intune](planning-guide-rollout-plan.md).