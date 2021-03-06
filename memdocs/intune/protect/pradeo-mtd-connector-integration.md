---
title: Configurar a integração do Pradeo com o Intune
titleSuffix: Intune on Azure
description: Integração do conector Pradeo com o Intune
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
ms.assetid: 82872ba6-80f8-4cc9-adf4-0ccd8ff26dd2
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2fb2317474b49dcb4bb39a0590c8ad7fa4ac8aa4
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83984872"
---
# <a name="integrate-pradeo-mobile-threat-defense-with-intune"></a>Integrar a Defesa de Ameaças Móveis do Pradeo com Intune

Tem de realizar os passos seguintes para integrar a solução de Defesa Contra Ameaças para Dispositivos Móveis do Pradeo com o Intune.

> [!NOTE]  
> Este fornecedor de Defesa de Ameaças Móveis não é suportado para dispositivos não matriculados.

## <a name="before-you-begin"></a>Antes de começar

> [!NOTE]
> Os seguintes passos devem ser realizados na [consola do Pradeo Security](https://pradeo-security.com/).

Antes de iniciar o processo de integração do Pradeo com o Intune, certifique-se de que tem os seguintes elementos:

- Subscrição do Microsoft Intune

- Credenciais de administrador do Azure Active Directory para conceder as seguintes permissões:

  - Iniciar sessão e ler o perfil de utilizador

  - Aceder ao diretório como o utilizador com sessão iniciada

  - Ler os dados do diretório

  - Enviar informações do dispositivo para o Intune

- Credenciais de administrador para aceder à consola do Pradeo Security.

### <a name="pradeo-app-authorization"></a>Autorização da aplicação Pradeo

O processo de autorização da aplicação Pradeo consiste no seguinte:

- Permitir que o serviço do Pradeo transmita informações relacionadas com o estado de funcionamento do dispositivo ao Intune.

- Pradeo sincroniza com a filiação do Grupo de Inscrição Da Azure AD para preencher a base de dados do seu dispositivo.

- Permitir que a consola de administração do Pradeo utilize o Início de Sessão Único (SSO) do Azure AD.

- Permitir que a aplicação Pradeo inicie sessão através do SSO do Azure AD.

## <a name="to-set-up-pradeo-integration"></a>Para configurar a integração do Pradeo

1. Aceda à [consola do Pradeo Security](https://www.pradeo-security.com) e inicie sessão com as suas credenciais.

2. Selecione **Administração – Gestão de Mobilidade Empresarial** no menu.

3. Selecione o **logótipo do Intune**.

4. Na janela **EMM (Gestão de mobilidade empresarial) – Intune**, em **Passo 1**, selecione o botão **Conector do Pradeo**. 

    ![Screenshot da janela Pradeo EMM Intune](./media/pradeo-mtd-connector-integration/pradeo_setup.png)

5. Na janela de ligação do Microsoft Intune, introduza as suas credenciais do Intune.

5. A página Web do Pradeo é reaberta. Em **Passo 2**, selecione o botão **Estado de Funcionamento dos Dispositivos do Pradeo**.

7. Na janela Conector do Pradeo-Intune, selecione **Aceitar**. 

8. Na janela Conector de API de dispositivo do Pradeo, selecione **Aceitar**.

9. A página Web do Pradeo é reaberta. Em **Passo 3**, selecione o botão **Ligar à Microsoft**. 

10. Na janela de autenticação do Microsoft Intune, introduza as suas credenciais do Intune.

11. Quando a mensagem **Integração Bem-sucedida** for apresentada, significa que a integração foi concluída.

## <a name="next-steps"></a>Passos seguintes

- [Configurar aplicativos Pradeo para dispositivos matriculados](mtd-apps-ios-app-configuration-policy-add-assign.md)
