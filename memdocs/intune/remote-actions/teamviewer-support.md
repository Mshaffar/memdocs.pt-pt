---
title: Administrar remotamente dispositivos no Microsoft Intune – Azure | Microsoft Docs
description: Veja as funções necessárias para utilizar o TeamViewer, como instalar o conector do TeamViewer e orientação passo a passo para administrar remotamente dispositivos com o Microsoft Intune no portal do Azure
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 72cdd888-efca-46e6-b2e7-fb9696bb2fba
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b94146cc429f2a7f7b196f15527e8687368e6d78
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988239"
---
# <a name="use-teamviewer-to-remotely-administer-intune-devices"></a>Utilizar o TeamViewer para administrar remotamente dispositivos do Intune

Os dispositivos geridos pelo Intune podem ser administrados remotamente com o [TeamViewer](https://www.teamviewer.com). O TeamViewer é um programa de terceiros que pode comprar separadamente. Este tópico mostra-lhe como configurar o TeamViewer no Intune e como administrar remotamente um dispositivo. 

## <a name="prerequisites"></a>Pré-requisitos

- Utilize um dispositivo suportado. O Administrador de Dispositivos Android gerido sintonizado, o Perfil de Trabalho Android, o Windows, o iOS/iPadOS e os dispositivos macOS suportam a administração remota. O TeamViewer pode não suportar o Windows Holographic (HoloLens), Windows Team (Surface Hub) ou Windows 10 S. Para conhecer a suportabilidade e obter todas as atualizações, veja [TeamViewer](https://www.teamviewer.com).

> [!NOTE]
> Android Dedicado e Totalmente Gerido não são suportados.

- O administrador do Intune no portal do Azure tem de ter as seguintes [funções do Intune](../fundamentals/role-based-access-control.md):  

  - **Atualizar Assistência Remota**: permite que os administradores modifiquem as definições do conector do TeamViewer
  - **Pedir Assistência Remota**: permite que os administradores iniciem uma nova sessão de assistência remota para qualquer utilizador. Os utilizadores com esta função não estão limitados pelas funções do Intune num âmbito. Além disso, os grupos de utilizadores ou dispositivos com uma função do Intune num âmbito também podem pedir assistência remota. 

- Uma conta [TeamViewer](https://www.teamviewer.com) com as credenciais de inscrição. Apenas algumas licenças TeamViewer podem apoiar a integração com o Intune. Para obter necessidades específicas do TeamViewer, consulte [TeamViewer Integration Partner: Microsoft Intune](https://www.teamviewer.com/integrations/microsoft-intune/).

Ao utilizar o TeamViewer, está a permitir que o Conector do TeamViewer para o Intune crie sessões do TeamViewer, leia os dados do Active Directory e guarde o token de acesso da conta do TeamViewer.

## <a name="configure-the-teamviewer-connector"></a>Configurar o conector do TeamViewer

Para fornecer assistência remota a dispositivos, configure o conector do TeamViewer no Intune através dos seguintes passos:

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Tenant administration**  >  **Conectores e fichas**  >  **teamviewer**de administração do inquilino.
3. Selecione **Ligar** e, em seguida, aceite o contrato de licença.
4. Selecione **Iniciar sessão no TeamViewer para autorizar**.
5. É aberta uma página da Web para o site do TeamViewer. Introduza as suas credenciais de licença do TeamViewer e, em seguida, clique em **Iniciar Sessão**.

## <a name="remotely-administer-a-device"></a>Administrar remotamente um dispositivo

Após o conector estar configurado, estará pronto para administrar remotamente um dispositivo. Utilize os passos seguintes: 

1. No centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Dispositivos** e, em seguida, selecione **Todos os dispositivos**.
3. A partir da lista, selecione o dispositivo que pretende administrar remotamente > **...**  >  **Nova Sessão de Assistência Remota.**
4. Quando o Intune estiver ligado ao serviço do TeamViewer, verá algumas informações sobre o dispositivo. Selecione **Ligar** para iniciar a sessão remota.

![Utilizar o TeamViewer para administrar remotamente dispositivos Android – exemplo](./media/teamviewer-support/android-teamviewer.png)

Quando inicia uma sessão remota, os utilizadores vêem uma bandeira de notificação no ícone da aplicação do Portal da Empresa no seu dispositivo. Uma notificação também aparece quando a aplicação abre. Os utilizadores podem então aceitar o pedido de assistência remota.

> [!NOTE]
> Os dispositivos Windows que estão matriculados utilizando métodos "sem uso", como o Gestor de Inscrição de Dispositivos (DEM) e o Designer de Configuração do Windows (WCD), não mostram a notificação do TeamViewer na aplicação Portal da Empresa. Nestes cenários, recomenda-se utilizar o portal TeamViewer para gerar a sessão.

No TeamViewer, pode realizar diversas ações no dispositivo, incluindo assumir o controlo do mesmo. Para obter detalhes completos do que pode fazer, veja [Orientação do TeamViewer](https://www.teamviewer.com/support/documents/).

Quando terminar, feche a janela do TeamViewer.
