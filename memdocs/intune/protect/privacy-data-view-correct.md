---
title: View and correct personal data (Ver e corrigir dados pessoais)
titleSuffix: Microsoft Intune
description: Saiba como ver e corrigir dados pessoais.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1ba77bc7-505e-4eca-a49e-dcdaa75d0043
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6c2bacea3e1e87e6bd1a14c14b22bd6f4c2870fd
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79325309"
---
# <a name="view-and-correct-personal-data"></a>View and correct personal data (Ver e corrigir dados pessoais)

Os administradores do Intune podem ver alguns dados pessoais com base nas respetivas permissões de acesso, mas apenas os utilizadores finais podem alterar os respetivos dados pessoais do dispositivo.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-dsr-and-stp-note.md)]


## <a name="view-personal-data"></a>Ver dados pessoais

Os administradores podem ver informações pessoais de utilizadores finais em vários painéis na IU do Intune. Os seguintes artigos descrevem o tipo de informações a que os administradores têm ou não acesso:
- [See device details (Ver os detalhes do dispositivo)](../remote-actions/device-inventory.md) no Intune, explica a forma como pode consultar os detalhes sobre o dispositivo de um utilizador final.
- [Monitor app information and assignments (Monitorizar informações e atribuições da aplicação)](../apps/apps-monitor.md) explica a forma como pode ver os detalhes sobre as aplicações instaladas no dispositivo de um utilizador final.
- O artigo [What information can my company see when I enroll my device? (Que informações é que a minha empresa pode ver quando inscrevo o meu dispositivo?)](https://docs.microsoft.com/user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune) disponibiliza aos utilizadores finais uma lista dos dados que as respetivas empresas podem e não podem ver. Recomenda-se que diga claramente aos utilizadores que tipo de dados está a recolher e por que motivo o está a fazer. Este artigo pode representar o primeiro passo para essa transparência.

### <a name="who-can-view-the-data"></a>Quem pode ver os dados?

A Microsoft utiliza controlos rigorosos para regular o acesso aos dados dos clientes ao conceder o nível mais baixo de acesso necessário para concluir tarefas essenciais e ao revogar o acesso quando este deixa de ser necessário. 

Pode proteger e controlar o acesso aos dados pessoais do utilizador final com o controlo de administração baseada em funções (RBAC). Para obter mais informações, veja [RBAC com o Microsoft Intune](../fundamentals/role-based-access-control.md).

Para saber mais sobre as práticas de dados da Microsoft, leia os Termos dos Serviços Online e a [Declaração de Privacidade do Microsoft Online Services](https://go.microsoft.com/fwlink/p/?linkid=131004&clcid=0x409). 

## <a name="correct-end-user-personal-data"></a>Corrigir dados pessoais do utilizador final

Os administradores não podem atualizar informações específicas do dispositivo ou da aplicação. Se o utilizador final quiser corrigir algum dado pessoal, por exemplo o nome do dispositivo, tem de o fazer diretamente no dispositivo. Essas alterações serão sincronizadas na próxima vez que o utilizador se ligar ao Intune.


## <a name="next-steps"></a>Próximos passos

Saiba como [auditar, exportar ou eliminar](privacy-data-audit-export-delete.md) dados pessoais no Intune.