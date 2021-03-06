---
title: Inscrever dispositivos com perfil de trabalho do Android Enterprise no Intune
titleSuffix: Microsoft Intune
description: Saiba como inscrever dispositivos com perfil de trabalho do Android Enterprise no Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 5/13/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c3da384efb87e5510e64954ed7b1badfb98f6583
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83987504"
---
# <a name="set-up-enrollment-of-android-enterprise-work-profile-devices"></a>Configurar a inscrição de dispositivos com perfil de trabalho do Android Enterprise

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune ajuda-o a implementar aplicações e configurações para dispositivos de perfil de trabalho Android Enterprise para garantir que o trabalho e as informações pessoais são separados. Para mais detalhes sobre o Android Enterprise, consulte [os requisitos do Android Enterprise](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).

Para configurar a gestão de perfis de trabalho do Android Enterprise, siga estes passos:

1. [Ligue a sua conta do inquilino do Intune à sua conta do Android Enterprise](connect-intune-android-enterprise.md).
2. Especifique as definições de inscrição dos perfis de trabalho do Android Enterprise. Os perfis de trabalho do Android Enterprise [só são suportados em determinados dispositivos Android](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012%20style=%22target=new_window%22). Qualquer dispositivo que suporte os perfis de trabalho do Android Enterprise também suporta a gestão de administrador de dispositivos Android. O Intune permite-lhe especificar a forma como os dispositivos que suportam os perfis de trabalho do Android Enterprise devem ser geridos a partir das [Restrições de Inscrição](enrollment-restrictions-set.md).
    - **Bloco**: Todos os dispositivos Android, incluindo dispositivos que suportam perfis de trabalho Android Enterprise, serão matriculados como dispositivos de administrador de dispositivos Android, a menos que a inscrição do administrador de dispositivos Android também esteja bloqueada. 
    - **Permitir (definido por padrão)**: Todos os dispositivos que suportam perfis de trabalho Android Enterprise estão matriculados como dispositivos de perfil de trabalho Android Enterprise. Qualquer dispositivo Android que não suporte os perfis de trabalho do Android Enterprise está inscrito como um dispositivo de administrador de dispositivos Android, a menos que a inscrição do administrador do dispositivo Android esteja bloqueada. 
> [!NOTE]
> O incumprimento definido para **permitir** é válido para novos inquilinos a partir de julho de 2019. Todos os inquilinos anteriores não sentirão qualquer alteração às suas Restrições de Inscrição, e verão quaisquer políticas que tenham estabelecido nas Restrições de Inscrição. Para inquilinos anteriores que nunca tiveram alterações nas Restrições de Inscrição, o **Block** continuará a ser o padrão para os perfis de trabalho do Android Enterprise.

3. [Indique aos seus utilizadores como devem inscrever os dispositivos](../user-help/enroll-device-android-work-profile.md).  

Se pretender inscrever dispositivos utilizando perfis de trabalho android Enterprise, mas esses dispositivos já estavam matriculados com o administrador de dispositivos Android, esses dispositivos devem primeiro não se inscrever e depois reinscrever-se.
> [!NOTE]
> Como administrador, pode fazê-lo remotamente utilizando a função **Retire.** Esta função pode ser encontrada no menu de ações depois de selecionar o dispositivo a partir da lâmina **All Devices.**

Se estiver a inscrever dispositivos com perfil de trabalho do Android Enterprise com uma conta de [Gestor de Inscrições de Dispositivos](device-enrollment-manager-enroll.md), existirá um limite de 10 dispositivos para inscrição por conta.

Para obter mais informações, veja [Dados que o Intune envia para a Google](../protect/data-intune-sends-to-google.md).

## <a name="next-steps-for-android-enterprise-work-profiles"></a>Passos seguintes para os perfis de trabalho do Android Enterprise
- [Implementar aplicações do perfil de trabalho do Android Enterprise](../apps/apps-add-android-for-work.md)
- [Adicionar políticas de configuração de perfis de trabalho do Android Enterprise](../configuration/device-profiles.md)

## <a name="see-also"></a>Consulte também

[Configuração e resolução de problemas dispositivos Android Enterprise no Microsoft Intune](https://support.microsoft.com/help/4476974)
