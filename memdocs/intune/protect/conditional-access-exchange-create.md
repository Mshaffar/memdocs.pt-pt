---
title: Criar política de acesso condicional de intercâmbio
titleSuffix: Microsoft Intune
description: Configure acesso condicional para troca no local e legacy Exchange Online Dedicado em Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 127dafcb-3f30-4745-a561-f62c9f095907
ms.reviewer: demerson
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 530d6de8194a1ca74b72567c98c5d2afcb327170
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990310"
---
# <a name="configure-exchange-on-premises-access-for-intune"></a>Configure Exchange on-presacesso para Intune

Este artigo mostra-lhe como configurar o Acesso Condicional para O Intercâmbio no local com base na conformidade do dispositivo.

Se tiver um ambiente do Exchange Online Dedicado e precisar de saber se está na configuração nova ou legada, contacte o seu gestor de conta. Para controlar o acesso por e-mail ao Exchange on-pre-preser ou ao seu legado ambiente dedicado ao Exchange Online, configure o Acesso Condicional à Troca no Local Intune.

## <a name="before-you-begin"></a>Antes de começar

Antes de configurar o Acesso Condicional, verifique se existem as seguintes configurações:

- A sua versão Exchange é **Exchange 2010 SP3 ou mais tarde**. Matriz de Servidor de Acesso de Cliente (CAS) do Exchange Server é suportada.

- Instalou e utiliza o [conector Exchange ActiveSync no local,](exchange-connector-install.md)que liga o Intune à Troca no local.

    >[!IMPORTANT]  
    >O Intune suporta múltiplos Exchange Connectors no local por subscrição.  No entanto, cada conector de intercâmbio no local é específico de um único inquilino intune e não pode ser utilizado com qualquer outro inquilino.  Se tiver mais do que uma organização do Exchange no local, pode configurar um conector separado para cada organização do Exchange.

- O conector para uma organização de intercâmbio no local pode instalar-se em qualquer máquina desde que essa máquina possa comunicar com o servidor Exchange.

- Este conector suporta o **ambiente do Exchange CAS**. Intune suporta a instalação do conector no servidor Exchange CAS diretamente. Recomendamos que o instale num computador separado devido à carga adicional que o conector coloca no servidor. Quando configurar o conector, tem de configurá-lo para comunicar com um dos servidores do Exchange CAS.

- O **Exchange ActiveSync** tem de ser configurado com a autenticação baseada em certificado ou com a entrada de credenciais de utilizador.

- Quando as políticas de Acesso Condicional são configuradas e direcionadas a um utilizador, antes de um utilizador poder ligar-se ao seu e-mail, o **dispositivo** que utilizam deve ser:
  - **Inscrito** no Intune ou ser um PC associado a um domínio.
  - **Registado no Azure Active Directory**. Além disso, o ID do Exchange ActiveSync do cliente tem de ser registado no Azure Active Directory.

- O Serviço de Registo de Dispositivos do Azure AD (DRS) é automaticamente ativado para os clientes do Intune e do Office 365. Os clientes que já tenham implantado o Serviço de Registo de Dispositivos ADFS não vêem dispositivos registados no seu Diretório Ativo no local. **Isto não é aplicável a PC com Windows ou a dispositivos Windows Phone**.

- **Conforme** com todas as políticas de conformidade implementadas nesse dispositivo.

- Se o dispositivo não cumprir as definições de Acesso Condicional, o utilizador é apresentado com uma das seguintes mensagens quando iniciar o seu sessão:
  - Se o dispositivo não estiver matriculado no Intune, ou não estiver registado no Diretório Ativo do Azure, uma mensagem exibe instruções sobre como instalar a aplicação Portal da Empresa, inscrever o dispositivo e ativar o e-mail. Este processo também associa o ID do Exchange ActiveSync do dispositivo ao registo do dispositivo no Azure Active Directory.
  - Se o dispositivo não estiver em conformidade, uma mensagem mostra que direciona o utilizador para o website do Portal da Empresa Intune ou para a aplicação Portal da Empresa. A partir do portal da empresa, podem encontrar informações sobre o problema e como corrigi-lo.

### <a name="support-for-mobile-devices"></a>Suporte para dispositivos móveis

- **Windows Phone 8.1 e mais tarde** - Para criar a política de acesso condicional, consulte Criar políticas de [acesso condicional](../protect/create-conditional-access-intune.md)
- **Aplicativo de e-mail nativo no iOS/iPadOS** - Para criar política de acesso condicional, consulte [Criar políticas de acesso condicional](../protect/create-conditional-access-intune.md)
- Clientes de **correio eletrónico EAS como o Gmail no Android 4 ou mais tarde** - Para criar a política de acesso condicional, consulte Criar políticas de Acesso [Condicional](../protect/create-conditional-access-intune.md)

- Clientes de **correio eletrónico EAS em administrador de dispositivos Android** - Para criar política de acesso condicional, consulte Criar políticas de Acesso [Condicional](../protect/create-conditional-access-intune.md)

- Clientes de **correio eletrónico EAS em dispositivos** de perfil de trabalho Android - Apenas o *Gmail* e o Nine Work para *Android Enterprise* são suportados em dispositivos de perfil de trabalho Android. Para o Acesso Condicional ao trabalho com perfis de trabalho Android, você deve implementar um perfil de e-mail para a aplicação *Gmail* ou *Nine Work para Android Enterprise,* e também implementar essas aplicações como uma instalação necessária. Depois de implementar a aplicação, pode configurar o Acesso Condicional baseado no dispositivo.


#### <a name="to-set-up-conditional-access-for-android-work-profile-devices"></a>Para configurar o Acesso Condicional para dispositivos de perfil de trabalho Android

  1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
  
  2. Implemente a aplicação Gmail ou Nine Work conforme **necessário**.

  3. Selecione **Perfis**de configuração de  >  **dispositivos**  >  **Criar perfil,** introduzir **nome** e **descrição** para o perfil.

  4. Selecione **empresa Android** na **Plataforma**, selecione **Email** no **tipo perfil**.

  5. Configure as definições de perfil de [e-mail](https://docs.microsoft.com/intune/configuration/email-settings-android-enterprise#android-enterprise).

  6. Quando terminar, selecione **OK**  >  **Create** para guardar as suas alterações.

  7. Depois de criar o perfil de e-mail, [atribua-o a grupos](https://docs.microsoft.com/intune/device-profile-assign).

  8. Configurar [o acesso condicional baseado no dispositivo.](https://docs.microsoft.com/intune/protect/conditional-access-intune-common-ways-use#device-based-conditional-access)

> [!NOTE]
> O Microsoft Outlook para Android e iOS/iPadOS não é suportado através do conector Exchange on-premises. Se pretender alavancar as políticas de acesso condicional do Diretório Ativo Azure e as Políticas de Proteção de Aplicações Intune com Outlook para iOS/iPadOS e Android para as suas caixas de correio no local, consulte [A autenticação moderna híbrida com Outlook para iOS/iPadOS e Android.](https://docs.microsoft.com/Exchange/clients/outlook-for-ios-and-android/use-hybrid-modern-auth)

### <a name="support-for-pcs"></a>Suporte de PCs

A aplicação de **correio** nativo no Windows 8.1 e mais tarde (quando inscrito no MDM com Intune)

## <a name="configure-exchange-on-premises-access"></a>Configurar o acesso ao Exchange no local

Antes de poder utilizar o seguinte procedimento para configurar o controlo de acesso exchange on-local, deve instalar e configurar pelo menos um [conector de intercâmbio intune](exchange-connector-install.md) no local para o Exchange on-premido.

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vá à **administração do Inquilino**  >  **Trocar de acesso**e, em seguida, selecione exchange **on-presacesso**.

3. No painel **de acesso exchange on-local,** escolha **Sim** para permitir o controlo de acesso ao exchange *no local*.

   > [!div class="mx-imgBorder"]
   > ![Screenshot exemplo do ecrã de acesso exchange on-local](./media/conditional-access-exchange-create/exchange-on-premises-access.png)

4. Em **fase de tarefas,** escolha **selecione grupos para incluir**, e, em seguida, selecione um ou mais grupos para configurar o acesso.

   Os membros dos grupos selecionados têm a política de acesso condicional para o acesso ao exchange no local aplicado aos mesmos. Os utilizadores que recebem esta política devem inscrever os seus dispositivos em Intune e estar em conformidade com os perfis de conformidade antes de poderem aceder ao Exchange on-premis.

   > [!div class="mx-imgBorder"]
   > ![Selecione grupos para incluir](./media/conditional-access-exchange-create/select-groups.png)

5. Para excluir grupos, escolha **grupos Select para excluir**, e, em seguida, selecione um ou mais grupos isentos de requisitos para inscrever dispositivos e para estar em conformidade com os perfis de conformidade antes de aceder ao Exchange on-pre-pres.

   Selecione **Guardar** para salvar a sua configuração e volte ao painel de acesso ao **Exchange.**

6. Em seguida, configure as definições para o conector de troca intune on-premises. Na consola, selecione o conector de acesso ao câmbio do **Inquilino**  >  **Exchange** >  **Access ActiveSync no local** e, em seguida, selecione o conector para a organização Exchange que pretende configurar.

7. Para **notificações do Utilizador,** selecione **Editar** para abrir o fluxo de trabalho da **Organização editar** onde pode modificar a mensagem de notificação do *Utilizador.*

   > [!div class="mx-imgBorder"]
   > ![Exemplo de screenshot do fluxo de trabalho da Organização edita para notificações](./media/conditional-access-exchange-create/edit-organization-user-notification.png)

   Modifique a mensagem de e-mail padrão que é enviada aos utilizadores se o seu dispositivo não estiver em conformidade e quiser aceder ao Exchange on-premis. O modelo de mensagem utiliza Linguagem de markup. Também pode ver a pré-visualização de como a mensagem parece à medida que escreve

   Selecione **Review + guardar**, e, em seguida, **guarde** para guardar as suas edições para completar a configuração do acesso ao Exchange on-pre-local.

   > [!TIP]
   > Para saber mais sobre a Linguagem de markup, veja este [artigo](https://en.wikipedia.org/wiki/Markup_language) da Wikipédia.

8. Em seguida, selecione as definições de **acesso Advanced Exchange ActiveSync** para abrir o fluxo de trabalho de definições de acesso Advanced Exchange *ActiveSync* onde configura as regras de acesso ao dispositivo.

   > [!div class="mx-imgBorder"]
   > ![Screenshot exemplo do fluxo de trabalho da Organização de Edição para configurações avançadas](./media/conditional-access-exchange-create/edit-organization-advanced-settings.png)

   - Para o acesso não gerido do **dispositivo,** depreie a regra de incumprimento global para o acesso a partir de dispositivos que não sejam afetados pelo Acesso Condicional ou outras regras:

     - **Permitir o acesso** - Todos os dispositivos podem aceder imediatamente ao Exchange on-preser. Os dispositivos que pertencem aos utilizadores nos grupos configurados como incluídos no procedimento anterior são bloqueados se forem posteriormente avaliados como não conformes com as políticas conformes ou não matriculados no Intune.

     - **Acesso** ao bloco e **quarentena** – Todos os dispositivos estão imediatamente bloqueados de aceder inicialmente ao Exchange on-pre-preser. Os dispositivos que pertencem aos utilizadores nos grupos configurados como incluídos no procedimento anterior têm acesso após a inscrição do dispositivo em Intune e são avaliados como conformes.

       Os dispositivos Android que *não* executam o padrão Samsung Knox não suportam esta definição e estão sempre bloqueados.

   - Para exceções à **plataforma do Dispositivo,** selecione **Adicionar**e, em seguida, especificar detalhes conforme necessário para o seu ambiente.

      Se a definição de acesso ao **dispositivo não gerido** estiver definida para **bloqueada**, os dispositivos que estão matriculados e em conformidade são permitidos mesmo que haja uma exceção da plataforma para bloqueá-los.  

9. Selecione **OK** para guardar as suas edições.

10. Selecione **Review + guardar,** e, em seguida, **guardar** para salvar a política de acesso condicional de troca.

## <a name="next-steps"></a>Passos seguintes

Em seguida, crie uma política de conformidade e atribua-a aos utilizadores para que a Intune avalie os seus dispositivos móveis, o See [Get começou com](device-compliance-get-started.md)a conformidade do dispositivo .

[Resolução de problemas Intune on-premises Exchange conector em Microsoft Intune](https://support.microsoft.com/help/4471887)
