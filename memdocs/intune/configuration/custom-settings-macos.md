---
title: Adicionar definições personalizadas para dispositivos macOS no Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Exporte definições do macOS com as ferramentas Apple Configurator ou Gestor de Perfis da Apple e, em seguida, importe estas definições para o Microsoft Intune. Estas definições podem criar, utilizar e controlar configurações personalizadas e funcionalidades em dispositivos macOS. Em seguida, este perfil personalizado pode ser atribuído ou distribuído pelos dispositivos macOS na sua organização, para criar uma linha de base ou um padrão.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/04/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e92315377a839a537dfc4c2da00d282d2cddf58f
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429095"
---
# <a name="use-custom-settings-for-macos-devices-in-microsoft-intune"></a>Utilizar definições personalizadas para dispositivos macOS no Microsoft Intune

Ao utilizar o Microsoft Intune, pode adicionar ou criar definições personalizadas para os seus dispositivos macOS com um "perfil personalizado". Os perfis personalizados são uma funcionalidade do Intune. Foram concebidos para adicionar definições e funcionalidades de dispositivos que não estão incorporadas Intune.

Ao utilizar dispositivos macOS, existem duas formas de obter as definições personalizadas no Intune:

- [Apple Configurator](https://itunes.apple.com/app/apple-configurator-2/id1037126344?mt=12)
- [Gestor de Perfis da Apple](https://support.apple.com/profile-manager)

Pode utilizar estas ferramentas para exportar definições para um perfil de configuração. No Intune, irá importar este ficheiro e, em seguida, atribuir o perfil aos seus utilizadores e dispositivos macOS. Uma vez atribuídas, as definições são distribuídas. Também criam uma linha de base ou padrão para o macOS na sua organização.

Este artigo fornece algumas orientações sobre a utilização do Apple Configurator e do Apple Profile Manager, e descreve as propriedades que pode configurar.

## <a name="before-you-begin"></a>Antes de começar

[Criar um perfil personalizado macOS.](custom-settings-configure.md)

## <a name="what-you-need-to-know"></a>O que tem de saber

- Ao utilizar o **Configurator Apple** para criar o perfil de configuração, certifique-se de que as definições que exporta são compatíveis com a versão macOS dos dispositivos. Para obter informações sobre como resolver definições incompatíveis, procure **Configuration Profile Reference** (Referência de Perfil de Configuração) e **Mobile Device Management Protocol Reference** (Referência do Protocolo de Gestão de Dispositivos Móveis) no site [Apple Developer](https://developer.apple.com/).

- Ao utilizar o **Gestor de Perfis da Apple**, certifique-se de que:

  - Ativa a [gestão de dispositivos móveis](https://help.apple.com/serverapp/mac/5.7/#/apd05B9B761-D390-4A75-9251-E9AD29A61D0C) no Gestor de Perfis.
  - Adiciona os [dispositivos macOS](https://help.apple.com/profilemanager/mac/5.7/#/pm9onzap1984) no Gestor de Perfis.
  - Depois de adicionar um dispositivo no Profile Manager, vá a **Under the Library**  >  **Devices** > selecione o seu dispositivo > **Definições**. Introduza as definições gerais e de segurança, privacidade, diretório e certificado do dispositivo.

    Transfira e guarde este ficheiro. Irá introduzi-lo no perfil do Intune. 

  - Certifique-se de que as definições que exporta do Apple Profile Manager são compatíveis com a versão macOS nos dispositivos. Para obter informações sobre como resolver definições incompatíveis, procure **Configuration Profile Reference** (Referência de Perfil de Configuração) e **Mobile Device Management Protocol Reference** (Referência do Protocolo de Gestão de Dispositivos Móveis) no site [Apple Developer](https://developer.apple.com/).

## <a name="custom-configuration-profile-settings"></a>Definições de perfil de configuração personalizada

- Nome do **perfil de configuração**: Introduza um nome para a apólice. Este nome é apresentado no dispositivo e no estado do Intune.
- **Ficheiro de perfil**de configuração : Navegue para o `.xml` ou ficheiro que criou utilizando o `.mobileconfig` Configurador Apple ou o Apple Profile Manager. O tamanho máximo do ficheiro é de 1000000 bytes (pouco menos de 1 MB). O ficheiro que importa é mostrado. Também pode **remover** um ficheiro depois de adicionado.

  Também pode adicionar fichas de dispositivo aos seus `.mobileconfig` ficheiros. As fichas do dispositivo são usadas para adicionar informações específicas do dispositivo. Por exemplo, para mostrar o número de série, insira `{{serialnumber}}` . No dispositivo, o texto mostra semelhante ao `123456789ABC` , que é único em cada dispositivo. Ao introduzir variáveis, certifique-se de que utiliza suportes encaracolados `{{ }}` . [Os tokens](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list) de configuração da aplicação incluem uma lista de variáveis que podem ser usadas. Também pode utilizar `deviceid` ou qualquer outro valor específico do dispositivo.

  > [!NOTE]
  > As variáveis não são validadas na UI, e são sensíveis ao caso. Como resultado, pode ver perfis guardados com entrada incorreta. Por exemplo, se introduzir `{{DeviceID}}` em vez de , `{{deviceid}}` então a corda literal é mostrada em vez do ID único do dispositivo. Certifique-se de introduzir a informação correta.

## <a name="next-steps"></a>Próximos passos

[Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).

Criar um [perfil personalizado nos dispositivos iOS/iPadOS](custom-settings-ios.md).
