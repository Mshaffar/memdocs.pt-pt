---
title: Integrar ponto de verificação SandBlast MTD
titleSuffix: Microsoft Intune
description: Como configurar a Defesa Contra Ameaças para Dispositivos Móveis (MTD) do Check Point SandBlast com o Intune para controlar o acesso de dispositivos móveis aos seus recursos empresariais.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/21/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1e9b1576-b239-48cc-a672-da6b5fb7be0a
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a02880f6da2e8a7810a37658bd19736b4631a9f8
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989228"
---
# <a name="integrate-check-point-sandblast-mobile-with-intune"></a>Integrar o Check Point SandBlast Mobile com o Intune

Complete os seguintes passos para integrar a solução de Defesa de Ameaças Móveis Check Point SandBlast com intune.

> [!NOTE]
> Este fornecedor de Defesa de Ameaças Móveis não é suportado para dispositivos não matriculados.

## <a name="before-you-begin"></a>Antes de começar

As instruções deste artigo são feitas na [consola Check Point SandBlast Mobile](https://intune-4.eu1.locsec.net/). 

Antes de iniciar o processo de integração do Check Point SandBlast Mobile com o Intune, certifique-se de que tem o seguinte:

- Subscrição do Microsoft Intune

- Credenciais de administrador do Azure Active Directory para conceder as seguintes permissões:

  - Iniciar sessão e ler o perfil de utilizador

  - Aceder ao diretório como o utilizador com sessão iniciada

  - Ler os dados do diretório

  - Enviar informações do dispositivo para o Intune

- Credenciais de administrador para aceder à consola MTD do Check Point SandBlast Mobile.

### <a name="check-point-sandblast-app-authorization"></a>Autorização da aplicação Check Point SandBlast

O processo de autorização da aplicação Check Point SandBlast consiste no seguinte:

- Permitir que o serviço Check Point SandBlast Mobile comunique informações relacionadas com o estado de funcionamento do dispositivo ao Intune.

- CheckPoint SandBlast Mobile sincroniza-se com a adesão do Grupo de Inscrição AD Azure para preencher a base de dados do seu dispositivo.

- Permitir que a consola do administrador do Check Point SandBlast utilize o Início de Sessão Único (SSO) do Azure AD.

- Permitir que a aplicação Check Point SandBlast Mobile inicie sessão com o SSO do Azure AD.

## <a name="to-set-up-check-point-sandblast-mobile-integration"></a>Para configurar a integração do Check Point SandBlast Mobile

1. Aceda à [consola MTD do Check Point SandBlast Mobile](https://intune-4.eu1.locsec.net/) e inicie sessão com as suas credenciais.

2. Clique no separador **Definições**.

3. Selecione **Gestão de dispositivos** e, em seguida, selecione **Definições**.

4. Selecione **Microsoft Intune** na lista pendente **Serviço MDM**.

5. Assim que definir o Microsoft Intune como o Serviço MDM, surge a janela **microsoft Intune Configuration,** escolha o **Add para a minha organização** para cada plataforma de dispositivos: iOS/iPadOS, Android e Windows para autorizar o Check Point SandBlast Mobile a comunicar com a AD Intune e Azure.

    ![Imagem que mostra a configuração do Check Point MTD do Intune](./media/checkpoint-sandblast-mobile-mtd-connector-integration/checkpoint-MTD-1.PNG)

    > [!IMPORTANT]
    > Tem de adicionar todas as plataformas de dispositivos para avançar para o passo seguinte.

6. Selecione **Aceitar** para autorizar que a aplicação Check Point SandBlast Mobile comunique com o Intune e o Azure Active Directory.

7. Assim que ativar todas as plataformas de dispositivos, tem de introduzir o grupo de segurança do Azure AD.

8. Selecione **Verificar**. Assim que o grupo de segurança do Azure AD for verificado com êxito, selecione **Guardar**.

## <a name="next-steps"></a>Passos seguintes

- [Set up Check Point SandBlast Mobile apps (Configurar aplicações do Check Point SandBlast Mobile)](mtd-apps-ios-app-configuration-policy-add-assign.md)
