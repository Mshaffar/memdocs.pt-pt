---
title: 'Guia de Início Rápido: enviar notificações para dispositivos não conformes'
titleSuffix: Microsoft Intune
description: Neste arranque rápido, utiliza o Microsoft Intune para enviar notificações de e-mail para dispositivos não conformes.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/21/2019
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a1b89f2d-7937-46bb-926b-b05f6fa9c749
ms.reviewer: jinyoon
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d02329f65d7b7ecec1dbfeaf84ecbe5c8fb53013
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079489"
---
# <a name="quickstart-send-notifications-to-noncompliant-devices"></a>Guia de Início Rápido: enviar notificações para dispositivos não conformes

Neste arranque rápido, utilizará o Microsoft Intune para enviar uma notificação de e-mail aos membros da sua força de trabalho que tenham dispositivos não conformes.

Por predefinição, quando o Intune deteta um dispositivo não conforme, este marca imediatamente o dispositivo como não conforme. [Acesso Condicional](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) do Diretório Ativo Azure (Azure AD) bloqueia o dispositivo. Quando um dispositivo não é compatível, o Intune permite-lhe adicionar ações por incumprimento, o que lhe dá flexibilidade para decidir o que fazer. Por exemplo, pode conceder um período de tolerância aos utilizadores para que estes estejam em conformidade antes de bloquear dispositivos não conformes.

Uma das medidas a tomar quando um dispositivo não cumpre a conformidade é enviar e-mail para o utilizador dos dispositivos. Também pode personalizar uma notificação de e-mail antes de enviá-la. Mais concretamente, pode personalizar os destinatários, o assunto e o corpo da mensagem, incluindo o logótipo da empresa e as informações de contacto. Intune também inclui detalhes sobre o dispositivo não conforme na notificação de e-mail.

Se não tiver uma subscrição Intune, [inscreva-se numa conta de teste gratuita](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Pré-requisitos

Ao utilizar as políticas de conformidade do dispositivo para bloquear dispositivos a partir de recursos corporativos, o Azure AD Conditional Access deve ser configurado. Se tiver concluído a política de conformidade com [o dispositivo Create,](quickstart-set-password-length-android.md) está a utilizar o Diretório Ativo Azure. Para mais informações sobre o Azure AD, consulte [acesso condicional em Diretório Ativo Azure](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) e [formas comuns de utilizar](../protect/conditional-access-intune-common-ways-use.md)o Acesso Condicional com Intune .

## <a name="sign-in-to-intune"></a>Iniciar sessão no Intune

Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) como administrador [global](../fundamentals/users-add.md#types-of-administrators) ou administrador de [serviço](../fundamentals/users-add.md#types-of-administrators)intune . Se criou uma subscrição intune Trial, a conta com a qual criou a subscrição é o administrador global.

## <a name="create-a-notification-message-template"></a>Criar um modelo de mensagem de notificação

Para enviar um e-mail aos seus utilizadores, crie um modelo de mensagem de notificação. Quando um dispositivo não estiver em conformidade, os detalhes que introduzir no modelo são apresentados no e-mail enviado aos utilizadores.

1. Intune, selecione **Devices** > **Compliance Policies** > **Notificações** > **Criar notificação**.
2. Introduza as seguintes informações:

   - **Nome**: *Administrador da Contoso*
   - **Assunto**: *Conformidade do dispositivo*
   - **Mensagem**: O seu dispositivo não está neste momento a cumprir os *requisitos de conformidade da nossa organização.*
   - **Cabeçalho do e-mail – Incluir logótipo da empresa**: defina a opção como **Ativado** para mostrar o logótipo da sua organização.
   - **Rodapé do e-mail – Incluir nome da empresa**: defina a opção como **Ativado** para mostrar o nome da sua organização.
   - **Rodapé do e-mail – Incluir informações de contacto**: defina a opção como **Ativado** para mostrar as informações de contacto da sua organização.

   ![Exemplo de uma mensagem de notificação de conformidade no Intune](./media/quickstart-send-notification/quickstart-send-notification-01.png)

3. Selecione **Next** e reveja a sua notificação. Selecione **Criar** e o modelo de mensagem de notificação está pronto a ser utilizado.

   > [!NOTE]
   > Também pode editar um modelo de Notificação criado anteriormente.

Para mais informações sobre a definição do nome da sua empresa, informações de contacto da empresa e logotipo da empresa, consulte os seguintes artigos:

- [Informações e declaração de privacidade da empresa](../apps/company-portal-app.md#configuration)
- [Informações de suporte](../apps/company-portal-app.md#support-information)
- [Personalizando a experiência do utilizador.](../apps/company-portal-app.md#customizing-the-user-experience)

## <a name="add-a-noncompliance-policy"></a>Adicionar uma política de não conformidade

Quando cria uma política de conformidade do dispositivo, o Intune cria automaticamente uma ação de não conformidade. Insintonize então os dispositivos como incompatíveis quando não cumprem a sua política de conformidade. Pode personalizar o intervalo de tempo durante o qual o dispositivo está marcado como não conforme. Também pode adicionar outra ação quando criar uma política de conformidade ou atualizar uma política de conformidade existente.

Os seguintes passos descrevem como pode criar uma política de conformidade para dispositivos com o Windows 10.

1. Em Intune, selecione **Devices** > **Compliance Policies** > **Create Policy**.

2. Introduza as seguintes informações:

   - **Nome**: *Política de conformidade do Windows 10*
   - **Descrição**: *Política de conformidade do Windows 10*
   - **Plataforma**: Windows 10 e mais tarde

3. Selecione **Definições** > **Segurança do Sistema** para visualizar as definições relacionadas com a segurança do dispositivo.

4. Configure as seguintes opções:

   - Defina a opção **Exigir uma palavra-passe para desbloquear os dispositivos móveis** para **Exigir**. Esta definição especifica quando deve ser exigido aos utilizadores que introduzam uma palavra-passe antes de ser concedido o acesso a informações nos respetivos dispositivos móveis.

   - Defina a opção **Comprimento mínimo da palavra-passe** para **6**. Esta definição especifica o número mínimo de dígitos ou carateres na palavra-passe.

   ![Definições de Segurança do Sistema para criar uma nova política de conformidade](./media/quickstart-send-notification/system-security-settings-01.png)

5. Selecione **OK** > **OK** > **Criar** para criar a sua política de conformidade.

6. Selecione **Properties** > **Action for noncompliance** > **Add**.

7. Na caixa pendente **Ação**, confirme se a opção **Enviar mensagem de e-mail ao utilizador final** está selecionada.

8. Selecione **o modelo de mensagem,** o modelo que criou anteriormente neste artigo e, em seguida, **selecione** para selecionar o modelo de mensagem.

9. Selecione ADD**OK** >  **Guarde** > para guardar as suas alterações.**Save**

## <a name="assign-the-policy"></a>Atribuir a política

Pode atribuir a política de conformidade a um grupo específico de utilizadores ou a todos os utilizadores. Quando a Intune reconhece que um dispositivo não está em conformidade, o utilizador é notificado de que deve atualizar o seu dispositivo para cumprir a política de conformidade. Utilize os seguintes passos para atribuir a apólice.

1. Intune vá para**as Políticas** de Conformidade de **Dispositivos** > e selecione a política de **conformidade do Windows 10** que criou anteriormente.

2. Selecione **Atribuições**.

3. Na caixa pendente **Atribuir a**, selecione **Todos os Utilizadores**. Esta ação irá selecionar todos os utilizadores. Todos os utilizadores que tiverem um dispositivo com o **Windows 10 e posterior** que não cumpra esta política de conformidade serão notificados.

    > [!NOTE]
    > Pode incluir e excluir grupos ao atribuir políticas de conformidade.

4. Clique em **Guardar**.

Quando tiver criado e salvo com sucesso a política, ela aparecerá na lista de políticas de **conformidade - Políticas**. Repare se a opção **Atribuído** na lista está definida como **Sim**.

## <a name="next-steps"></a>Passos seguintes

Neste guia de início rápido, utilizou o Intune para criar e atribuir uma política de conformidade aos dispositivos com o Windows 10 da sua força de trabalho para exigir uma palavra-passe de pelo menos seis carateres de comprimento. Para obter mais informações sobre como criar políticas de conformidade para dispositivos Windows, veja [Adicionar uma política de conformidade para dispositivos Windows no Intune](compliance-policy-create-windows.md).

Para seguir esta série de guias de início rápido do Intune, continue para o próximo guia de início rápido.

> [!div class="nextstepaction"]
> [Guia de Início Rápido: adicionar e atribuir uma aplicação cliente](../apps/quickstart-add-assign-app.md)
