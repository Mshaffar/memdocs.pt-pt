---
title: Restrições de dispositivos no Microsoft Intune para o Windows 10 Team
titleSuffix: ''
description: Saiba mais sobre as restrições de dispositivos disponíveis para dispositivos Windows 10 Team.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 3/6/2018
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 31457667612617bb573ddfb145ed26f70de33159
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332269"
---
# <a name="microsoft-intune-windows-10-team-device-restriction-settings"></a>Definições de restrição de dispositivos Windows 10 Team do Microsoft Intune

Este artigo mostra-lhe as definições de restrição de dispositivos do Microsoft Intune que pode configurar para dispositivos Windows 10 Team.

## <a name="apps-and-experience"></a>Aplicações e experiência

- **Ativar ecrã quando alguém entra na sala** – Permite ao dispositivo ser reativado automaticamente quando o sensor deteta alguém na sala.
- **Informações sobre a reunião apresentadas no ecrã de boas-vindas** – ative esta opção para escolher as informações que são apresentadas no mosaico Reuniões do ecrã de boas-vindas. É possível:
  - **Mostrar apenas organizador e hora**
  - **Mostrar organizador, hora e assunto (assunto oculto para reuniões privadas)**
- **URL da imagem de fundo do ecrã de boas-vindas** – Ative esta definição para apresentar um fundo personalizado no ecrã **Bem-vindo** dos dispositivos Windows 10 Team a partir do URL especificado.<br>A imagem tem de estar no formato PNG e o URL tem de começar por **https://** .

## <a name="azure-operational-insights"></a>Informações operacionais do Azure

- **Informações Operacionais do Azure** – as Informações Operacionais do Azure, parte do conjunto de aplicações Microsoft Operations Manager, recolhe, armazena e analisa os dados dos ficheiros de registo a partir de dispositivos com o Windows 10 Team.
Para ligar às Informações Operacionais do Azure, tem de especificar um **ID da Área de Trabalho** e uma **Chave da Área de Trabalho**.

## <a name="maintenance"></a>Manutenção

- **Janela de manutenção de atualizações** – Configura a janela quando podem ocorrer atualizações ao dispositivo. Pode configurar a **Hora de início** da janela e a **Duração em horas** (de 1 a 5 horas).

## <a name="wireless-projection"></a>Projeção sem fios

- **PIN para projeção sem fios** – Especifica se deve introduzir um PIN para poder utilizar as capacidades de projeção sem fios do dispositivo.
- **Projeção sem fios Miracast** – se quiser permitir que o dispositivo com o Windows 10 Team utilize dispositivos preparados para Miracast para projeção, selecione esta opção.
- **Canal de projeção sem fios Miracast** – selecione o canal Miracast que é utilizado para estabelecer a ligação.

## <a name="next-steps"></a>Próximos passos

Utilize as informações em [Como configurar definições de restrições de dispositivos](device-restrictions-configure.md) para guardar e atribuir o perfil a utilizadores e dispositivos.