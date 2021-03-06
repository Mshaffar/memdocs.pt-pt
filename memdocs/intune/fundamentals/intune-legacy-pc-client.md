---
title: Legacy Intune CLIENTE e Intune em Azure
description: Considerações ao utilizar o Intune no Azure para gerir os dispositivos Windows da sua organização.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/15/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.assetid: 1f104923-12df-453c-9c20-942ef65a0945
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 41b5b4116359864c4d1251515d29005b9d9af425
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82077942"
---
# <a name="intune-on-azure-console-and-legacy-intune-pc-client"></a>Insintonize na consola Azure e no legado Intune PC cliente

Intune usa uma arquitetura de serviço de aplicação SaaS baseada em Azure. O Azure oferece melhorias significativas ao nível da escala, capacidade e desempenho. Isto oferece experiências avançadas de administração Intune e fluxos de trabalho otimizados no portal Azure. 

Ao utilizar o Intune no Azure para gerir os dispositivos Windows da sua organização, considere os seguintes pontos:

## <a name="manage-windows-10-devices-by-using-mdm"></a>Gerir dispositivos Windows 10 com a MDM

Recomendamos que utilize a [Gestão de Dispositivos Móveis (MDM) para gerir os dispositivos Windows 10](../configuration/device-restrictions-windows-10.md), em vez de utilizar o cliente de PC do Intune legado. A capacidade para gerir o Windows 10 com a MDM está disponível no Intune no portal do Azure. A MDM do Windows 10 proporciona muitas capacidades de segurança e gestão novas que não estão disponíveis através do cliente de PC do Intune legado.

## <a name="legacy-pc-client-features-are-only-available-in-the-silverlight-console"></a>As funcionalidades do Cliente de PC legadas só estão disponíveis na consola do Silverlight

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

Os fluxos de trabalho de gestão do Cliente de PC do Intune utilizam a [Consola de Administração do Intune baseada no Silverlight](https://manage.microsoft.com/), que tem as seguintes consequências:

- Para todas as tarefas de gestão não agrupadas que utilizam o Cliente de PC do Intune, tem de utilizar a consola do Silverlight.
- Quando gerir grupos, tem de utilizar o [Intune no portal do Azure](https://portal.azure.com/). Este requisito existe porque o Intune agora utiliza Grupos do Azure AD, em vez de Grupos do Intune legados. 

Devido à mudança para os Grupos AD Azure, a filtragem "baseada em grupo" nas vistas do painel de consolasilverlight mudou ligeiramente. Para filtrar na UI do Silverlight atualizada, siga estes passos:

1. Selecione uma vista.
2. Na caixa **Filtros**, introduza o nome do grupo pelo qual quer filtrar e prima Enter. Deste modo, vai filtrar a vista de lista dos dispositivos nesse grupo específico.

   ![Entrada de dropdown de filtros com Nenhuma selecionada](./media/intune-legacy-pc-client/image01.png)


## <a name="continue-to-manage-windows-7-by-using-intune-pc-client"></a>Continuar a gerir o Windows 7 com o Cliente de PC do Intune

Para o Windows 7, que não pode ser gerido utilizando MDM, continuaremos a suportar as capacidades existentes do Cliente Intune PC apenas na consola Silverlight. Considere migrar para a gestão MDM quando atualizar para o Windows 10.

## <a name="mdm-capabilities"></a>Capacidades da MDM

Para ver uma comparação detalhada entre as capacidades da MDM e do Cliente de PC, veja [Comparar a gestão de PCs Windows como computadores ou dispositivos móveis](pc-management-comparison.md). As atualizações da MDM continuarão a proporcionar novas capacidades de gestão aos dispositivos Windows 10 inscritos na MDM, incluindo opções de avaliação para aplicações do Win32. Veja o [What's New](whats-new.md) para as mais recentes adições de lançamento ao serviço.

## <a name="switch-from-pc-client-to-mdm"></a>Mudar do Cliente de PC para a MDM

Para mudar da gestão de dispositivos Windows 10 com o Cliente de PC do Intune para a gestão com a MDM, siga estes passos:

1. Na consola do Silverlight, execute uma **Eliminação seletiva** para anular a inscrição do dispositivo do Cliente de PC.
  ![Aviso popup com o botão de rádio "Limpar seletivamente o dispositivo" selecionado](./media/intune-legacy-pc-client/image02.png)
2. Volte a inscrever o dispositivo através da [MDM (e/ou Associação Azure AD)](../enrollment/windows-enroll.md).

## <a name="next-steps"></a>Passos seguintes
[Inscrever dispositivos Windows](../enrollment/windows-enroll.md)
