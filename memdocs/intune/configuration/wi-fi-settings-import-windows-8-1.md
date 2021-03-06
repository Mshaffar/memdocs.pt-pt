---
title: Importar definições de Wi-Fi para dispositivos Windows no Microsoft Intune – Azure | Microsoft Docs
description: Exporte definições de Wi-Fi de um dispositivo Windows como um ficheiro XML através do comando netsh wlan. Em seguida, importe este ficheiro no Intune para criar um perfil Wi-Fi para dispositivos com o Windows 8.1, Windows 10 e Windows Holographic for Business.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d17614424cdb20d2d88d818fcdd015c229150d66
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556341"
---
# <a name="import-wi-fi-settings-for-windows-devices-in-intune"></a>Importar definições de Wi-Fi para dispositivos Windows no Intune

Para dispositivos com Windows, pode importar um perfil de configuração de Wi-Fi que tenha sido anteriormente exportado para um ficheiro. **Para dispositivos com o Windows 10 e posterior, também pode [criar um perfil Wi-Fi](wi-fi-settings-windows.md) diretamente no Intune**.

Esta funcionalidade aplica-se a:

- Windows 8.1 e posterior
- Windows 10 e posterior
- Computadores ou dispositivos móveis com o Windows 10
- Windows Holographic for Business

## <a name="before-you-begin"></a>Antes de começar

[Crie um perfil de dispositivo](wi-fi-settings-configure.md). O nome do perfil **deve** ser o mesmo que o nome atribuído no perfil Wi-Fi xml. Caso contrário, falhará.

## <a name="import-the-wi-fi-settings-into-intune"></a>Importar as definições de Wi-Fi para o Intune

- **Nome da ligação**: introduza um nome para a ligação Wi-Fi. Este nome é mostrado aos utilizadores quando navegam nas redes Wi-Fi disponíveis.
- **Perfil XML**: Selecione o botão de navegação e selecione o ficheiro XML que contém as definições de perfil Wi-Fi que pretende importar.
- **Conteúdos do ficheiro**: mostra o código XML do perfil de configuração que selecionou.

## <a name="export-wi-fi-settings-from-a-windows-device"></a>Exportar definições de Wi-Fi a partir de um dispositivo Windows

No Windows, utilize `netsh wlan` para exportar um perfil Wi-Fi existente para um ficheiro XML, que pode ser lido pelo Intune. A chave tem de ser exportada em texto simples para utilizar o perfil com êxito.

Num computador Windows que já tenha o perfil Wi-Fi necessário instalado, siga estes passos:

1. Crie uma pasta local para os perfis Wi-Fi exportados, tais como **c:\WiFi**.
2. Abra uma linha de comandos como administrador.
3. Execute o comando `netsh wlan show profiles`. Repare o nome do perfil que gostaria de exportar. Neste exemplo, o nome do perfil é **WiFiName**.
4. Execute o comando `netsh wlan export profile name="ProfileName" folder=c:\Wifi`. Este comando o cria um ficheiro do perfil Wi-Fi com o nome **Wi-Fi-WiFiName.xml** na sua pasta de destino.

> [!IMPORTANT]
>
> - Se estiver a exportar um perfil Wi-Fi que inclua uma chave pré-partilhada, **deve** adicionar `key=clear` ao comando. Por exemplo, introduza: 
>
>   `netsh wlan export profile name="ProfileName" key=clear folder=c:\Wifi`
>
> - A utilização de uma chave pré-partilhada com o Windows 10 provoca um erro de reparação a mostrar em Intune. Quando isto acontece, o perfil Wi-Fi é atribuído corretamente ao dispositivo e funciona conforme esperado.
> - Se exportar um perfil Wi-Fi que inclua uma chave pré-partilhada, certifique-se de que o ficheiro está protegido. Como a chave se encontra em texto simples, é sua responsabilidade protegê-la.

## <a name="next-steps"></a>Próximos passos

[Atribuir o perfil,](device-profile-assign.md) [e monitorizar o seu estado](device-profile-monitor.md).

Consulte a visão geral das [definições de Wi-Fi,](wi-fi-settings-configure.md)incluindo outras plataformas disponíveis.
