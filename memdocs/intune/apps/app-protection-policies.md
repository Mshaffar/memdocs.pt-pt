---
title: Criar e implementar políticas de proteção de aplicações
titleSuffix: Microsoft Intune
description: Este tópico descreve como criar e atribuir políticas de proteção de aplicações (APP) do Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f31b2964-e932-4cee-95c4-8d5506966c85
ms.reviewer: joglocke
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 91ca1e8a710e13e393af5bb3723ca1086e37887d
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988599"
---
# <a name="how-to-create-and-assign-app-protection-policies"></a>Como criar e atribuir políticas de proteção de aplicações

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Saiba como criar e atribuir políticas de proteção de aplicações (APP) da Microsoft Intune para os utilizadores da sua organização. Este tópico também descreve como fazer alterações a políticas existentes.

## <a name="before-you-begin"></a>Antes de começar

As políticas de proteção de aplicações podem ser aplicadas às aplicações em execução nos dispositivos que podem ou não ser geridos pelo Intune. Para uma descrição mais detalhada de como as políticas de proteção de aplicações funcionam e os cenários que são apoiados por políticas de proteção de aplicações Intune, consulte a visão geral das políticas de proteção de [aplicações.](app-protection-policy.md)

As opções disponíveis nas políticas de proteção de aplicações (APP) permitem às organizações adaptar a proteção às suas necessidades específicas. Para alguns, pode não ser óbvio quais as definições de política necessárias para implementar um cenário completo. Para ajudar as organizações a priorizar o endurecimento do ponto final do cliente móvel, a Microsoft introduziu taxonomia para o seu quadro de proteção de dados APP para a gestão de aplicações móveis iOS e Android.

O quadro de proteção de dados da APP é organizado em três níveis distintos de configuração, com cada nível de construção fora do nível anterior:

- **A proteção básica de dados da empresa** (Nível 1) garante que as aplicações estão protegidas com um PIN e encriptadas e realizam operações de limpeza seletiva. Para dispositivos Android, este nível valida o atestado do dispositivo Android. Esta é uma configuração de nível de entrada que fornece um controlo de proteção de dados semelhante nas políticas de caixa de correio Exchange Online e introduz TI e a população utilizadora para APP.
- **A empresa reforçada proteção de dados** (Nível 2) introduz mecanismos de prevenção de fugas de dados de APP e requisitos mínimos de SO. Esta é a configuração que é aplicável à maioria dos utilizadores móveis que acedem a dados do trabalho ou da escola.
- **A alta proteção de dados** da empresa (Nível 3) introduz mecanismos avançados de proteção de dados, configuração PIN melhorada e APP Mobile Threat Defense. Esta configuração é desejável para os utilizadores que acedem a dados de alto risco.

Para ver as recomendações específicas para cada nível de configuração e as aplicações mínimas que devem ser protegidas, reveja o quadro de proteção de dados utilizando políticas de proteção de [aplicações](app-protection-framework.md).

Se procura uma lista de aplicações que integraram o Intune SDK, consulte [aplicações protegidas](apps-supported-intune-apps.md)microsoft Intune .

Para obter mais informações sobre como adicionar as aplicações de linha de negócio (LOB) da sua organização ao Microsoft Intune, para se preparar para as políticas de proteção de aplicações, veja [Adicionar aplicações ao Microsoft Intune](apps-add.md).

## <a name="app-protection-policies-for-iosipados-and-android-apps"></a>Políticas de proteção de aplicativos para aplicações iOS/iPadOS e Android

Ao criar uma política de proteção de aplicações para aplicações iOS/iPadOS e Android, segue um fluxo de processo moderno intune que resulta numa nova política de proteção de aplicações.

### <a name="create-an-iosipados-or-android-app-protection-policy"></a>Criar uma política de proteção de aplicações iOS/iPadOS ou Android

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. No portal Intune, escolha políticas de proteção de **Apps**  >  **apps.** Esta seleção abre o painel **Políticas de proteção de aplicações**, onde pode criar novas políticas e editar as já existentes.
3. Selecione **Criar a política** e selecione **iOS/iPadOS** ou **Android**. O painel **de política Create** é exibido.
4. Na página Basics, adicione os **seguintes valores:**

    | Valor | Descrição |
    |--------------|------------------------------------------------|
    | Name | O nome desta política de proteção de aplicações. |
    | Descrição | [Opcional] A descrição desta política de proteção de aplicações. |


    O valor da **Plataforma** é definido com base na sua escolha acima.

    ![Screenshot da página Basics do painel de política Criar](./media/app-protection-policies/app-protection-add-policies-01.png)

5. Clique em **Seguir** para exibir a página **apps.**<br>
    A página **Apps** permite-lhe escolher como pretende aplicar esta política a aplicações em diferentes dispositivos. Deve adicionar pelo menos uma aplicação.<p>

    | Valor/Opção | Descrição |
    |-------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | Alvo para aplicações em todos os tipos de dispositivos | Utilize esta opção para direcionar a sua política para aplicações em dispositivos de qualquer estado de gestão. Escolha **não** para direcionar aplicações em tipos de dispositivos específicos. Para obter informações, consulte as políticas de [proteção de aplicações Target com base no estado de gestão](#target-app-protection-policies-based-on-device-management-state) de dispositivos |
    |     Tipos de dispositivos | Utilize esta opção para especificar se esta política se aplica a dispositivos geridos pelo MDM ou a dispositivos não geridos. Para as políticas de APLICAÇÃO iOS/iPadOS, selecione a partir de dispositivos **não geridos** e **geridos.** Para as políticas de APLICAÇÃO Android, selecione entre **Não gerido,** **administrador de dispositivos Android**e Android **Enterprise.**  |
    | Aplicativos públicos | Clique em **Selecionar aplicações públicas** para escolher as aplicações para o alvo. |
    | Aplicativos personalizados | Clique em **Selecionar aplicações personalizadas** para selecionar aplicações personalizadas para direcionar com base num ID do Bundle. |

    As aplicações que selecionou aparecerão na lista de aplicações públicas e personalizadas.
6. Clique em **Seguir** para visualizar a página de **proteção de dados.**<br>
    Esta página fornece configurações para controlos de prevenção de perdas de dados (DLP), incluindo restrições de corte, cópia, pasta e restrições de poupança. Estas definições determinam como os utilizadores interagem com os dados nas aplicações que esta política de proteção de aplicações se aplica.

    **Definições de proteção de dados:**<br>
    - **proteção de dados iOS/iPadOS** - Para obter informações, consulte as definições da política de proteção de [aplicações iOS/iPadOS - Proteção de Dados](app-protection-policy-settings-ios.md#data-protection).
    - **Proteção de dados Android** - Para obter informações, consulte as definições de política de proteção de [aplicações Android - Proteção de Dados](app-protection-policy-settings-android.md#data-protection).

7. Clique em **Seguir** para visualizar a página **de requisitos** de Acesso.<br>
    Esta página fornece configurações que lhe permitem configurar os requisitos PIN e credenciais que os utilizadores devem cumprir para aceder a apps num contexto de trabalho.
 
    **Definições de requisitos de acesso:**<br>
    - **requisitos de acesso iOS/iPadOS** - Para obter informações, consulte as definições da política de proteção de [aplicações iOS/iPadOS - Requisitos de acesso](app-protection-policy-settings-ios.md#access-requirements).
    - **Requisitos de acesso android** - Para obter informações, consulte as definições de política de proteção de [aplicações Android - Requisitos de acesso](app-protection-policy-settings-android.md#access-requirements).

8. Clique em **Seguir** para exibir a página de **lançamento condicional.**<br>
    Esta página fornece configurações para definir os requisitos de segurança de início de sessão para a sua política de proteção de aplicações. Selecione uma **Definição** e introduza o **Valor** que os utilizadores têm de cumprir para iniciar sessão na sua aplicação da empresa. Em seguida, selecione a **Ação** que pretende tomar se os utilizadores não cumprirem os seus requisitos. Em alguns casos, é possível configurar múltiplas ações para uma única definição.

    **Definições de lançamento condicional:**<br>
    - **lançamento condicional iOS/iPadOS** - Para obter informações, consulte as definições da política de proteção de [aplicações iOS/iPadOS - Lançamento condicional](app-protection-policy-settings-ios.md#conditional-launch).
    - **Lançamento condicional do Android** - Para obter informações, consulte as definições de política de proteção de [aplicações Android - Lançamento condicional](app-protection-policy-settings-android.md#conditional-launch).

9. Clique em **Seguir** para exibir a página **de Tarefas.**<br>
   A página **De missões** permite-lhe atribuir a política de proteção de aplicações a grupos de utilizadores.

10. Clique **em Seguinte: Rever + criar** para rever os valores e definições que inseriu para esta política de proteção de aplicações.

11. Quando terminar, clique em **Criar** para criar a política de proteção de aplicações em Intune.

    > [!TIP]
    > Estas definições de política apenas são impostas quando utilizar aplicações no contexto profissional. Quando os utilizadores finais utilizam a aplicação para realizar uma tarefa pessoal, estes não são afetados por estas políticas. Tenha em atenção que, ao criar um novo ficheiro, este é considerado um ficheiro pessoal.

Os utilizadores finais podem transferir as aplicações a partir da Apple Store ou do Google Play. Para obter mais informações, consulte:
* [O que esperar quando a aplicação Android é gerida por políticas de proteção de aplicações](../fundamentals/end-user-mam-apps-android.md)
* [O que esperar quando a sua aplicação iOS/iPadOS for gerida por políticas de proteção de aplicações](../fundamentals/end-user-mam-apps-ios.md)

## <a name="change-existing-policies"></a>Alterar políticas existentes
Pode editar uma política existente e aplicá-la aos utilizadores visados. No entanto, ao alterar as políticas existentes, os utilizadores que já estão inscritos nas aplicações não verão as alterações durante um período de oito horas.

Para ver o efeito das alterações imediatamente, o utilizador final tem de terminar sessão na aplicação e voltar a iniciar sessão.

### <a name="to-change-the-list-of-apps-associated-with-the-policy"></a>Para alterar a lista de aplicações associadas à política

1. No painel **Políticas de proteção de aplicações**, selecione a política que pretende alterar.

2. No painel *de proteção de aplicações intune,* selecione **Propriedades**.

3. Ao lado da secção intitulada *Apps,* **selecione Editar**.

4. A página **Apps** permite-lhe escolher como pretende aplicar esta política a aplicações em diferentes dispositivos. Deve adicionar pelo menos uma aplicação.<p>
    
    | Valor/Opção | Descrição |
    |-------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | Alvo para aplicações em todos os tipos de dispositivos | Utilize esta opção para direcionar a sua política para aplicações em dispositivos de qualquer estado de gestão. Escolha **não** para direcionar aplicações em tipos de dispositivos específicos. Pode ser necessária uma configuração adicional da aplicação para esta definição. Para obter mais informações, veja [Direcionar políticas de proteção de aplicações com base no estado de gestão do dispositivo](#target-app-protection-policies-based-on-device-management-state). |
    |     Tipos de dispositivos | Utilize esta opção para especificar se esta política se aplica a dispositivos geridos pelo MDM ou a dispositivos não geridos. Para as políticas de APLICAÇÃO iOS/iPadOS, selecione a partir de dispositivos **não geridos** e **geridos.** Para as políticas de APLICAÇÃO Android, selecione entre **Não gerido,** **administrador de dispositivos Android**e Android **Enterprise.**  |
    | Aplicativos públicos | Clique em **Selecionar aplicações públicas** para escolher as aplicações para o alvo. |
    | Aplicativos personalizados | Clique em **Selecionar aplicações personalizadas** para selecionar aplicações personalizadas para direcionar com base num ID do Bundle. |

    As aplicações que selecionou aparecerão na lista de aplicações públicas e personalizadas.

5. Clique em **Rever + criar** para rever as aplicações selecionadas para esta política.

6. Quando terminar, clique em **Guardar** para atualizar a política de proteção de aplicações.
 
#### <a name="to-change-the-list-of-user-groups"></a>Para alterar a lista de grupos de utilizadores

1. No painel **Políticas de proteção de aplicações**, selecione a política que pretende alterar.

2. No painel *de proteção de aplicações intune,* selecione **Propriedades**.

3. Ao lado da secção intitulada *Atribuições,* **selecione Editar**.

4. Para adicionar um novo grupo de utilizadores à política, no separador *Incluir*, selecione **Selecionar grupos para incluir** e selecione o grupo de utilizadores. Escolha **Selecionar** para adicionar o grupo. 

5. Para excluir um grupo de utilizadores, no separador *Excluir*, escolha **Selecionar grupos a excluir** e selecione o grupo de utilizadores. Selecione a opção **Selecionar** para remover o grupo de utilizadores.  

6. Para eliminar grupos que foram adicionados anteriormente, no separador *Incluir* ou *Excluir*, selecione as reticências (...) e, em seguida, **Eliminar**.

7. Clique em **Rever + criar** para rever os grupos de utilizadores selecionados para esta política.

8. Quando tiver concluído as alterações às atribuições, selecione **Guardar** para guardar a configuração e implementar a política para o novo conjunto de utilizadores. Se selecionar **Cancelar** antes de guardar a configuração, irá descartar todas as alterações que fez nos separadores *Incluir* e *Excluir.*

### <a name="to-change-policy-settings"></a>Para alterar definições de política

1. No painel **Políticas de proteção de aplicações**, selecione a política que pretende alterar.

2. No painel *de proteção de aplicações intune,* selecione **Propriedades**.

3. Junto à secção correspondente às definições que pretende alterar, **selecione Editar**. Em seguida, altere as definições para novos valores.

7. Clique em **Rever + criar** para rever as definições atualizadas para esta política.

4. Selecione o **Save** para guardar as suas alterações. Repita o processo de selecionar uma área de definições, alterá-la e guardar as alterações até concluir todas as suas alterações. Em seguida, pode abrir o painel *Proteção de Aplicações do Intune – Propriedades*. 

## <a name="target-app-protection-policies-based-on-device-management-state"></a>Aplicar políticas de proteção de aplicações com base no estado de gestão do dispositivo
Em muitas organizações, é comum permitir que os utilizadores finais utilizem dispositivos geridos pela Intune Mobile Device Management (MDM), como dispositivos corporativos e dispositivos não geridos protegidos apenas com políticas de proteção de aplicações Intune. Os dispositivos não geridos são normalmente denominados BYOD (Bring Your Own Devices).

Uma vez que as políticas de proteção de aplicações Intune visam a identidade de um utilizador, as definições de proteção para um utilizador podem aplicar-se tanto a dispositivos matriculados (geridos pelo MDM) como a dispositivos não inscritos (sem MDM). Por isso, pode direcionar uma política de proteção de aplicações Intune para dispositivos intune ou iOS/iPadOS e Android. Pode ter uma política de proteção para dispositivos não geridos em que existem controlos rigorosos de prevenção da perda de dados (DLP) e uma política de proteção separada para dispositivos geridos pelo MDM, onde os controlos DLP podem ser um pouco mais relaxados. Para obter mais informações sobre como isto funciona em dispositivos pessoais do Android Enterprise, consulte políticas de proteção de [aplicações e perfis de trabalho.](android-deployment-scenarios-app-protection-work-profiles.md)

Para criar estas políticas, **Apps**navegue nas políticas de  >  **proteção** de Apps App na consola Intune e, em seguida, selecione **a política Create**. Também pode editar uma política de proteção de aplicações existente. Para que a política de proteção de aplicações se aplique tanto a dispositivos geridos como não geridos, navegue na página **apps** e confirme que **o Target para aplicações em todos os tipos de dispositivos** está definido para **Sim**, o valor padrão. Se quiser atribuir granularly com base no estado de gestão, detete **o Target para aplicações em todos os tipos de dispositivos** para **No**. 

### <a name="device-types"></a>Tipos de dispositivos

- **Não geridos**: Dispositivos não geridos são dispositivos em que a gestão do MDM intune não tenha sido detetada. Isto inclui dispositivos geridos por fornecedores de MDM de terceiros.
- **Dispositivos geridos intune**: Os dispositivos geridos são geridos pelo INTUNE MDM.
- **Administrador de dispositivos Android**: Dispositivos geridos por Intune utilizando a API da Administração de Dispositivos Android.
- **Android Enterprise**: Dispositivos geridos por Intune utilizando perfis de trabalho android enterprise ou Android Enterprise Full Device Management.

No Android, os dispositivos Android irão solicitar a instalação da aplicação Intune Company Portal, independentemente do tipo dispositivo escolhido. Por exemplo, se selecionar 'Android Enterprise' então os utilizadores com dispositivos Android não geridos continuarão a ser solicitados.

Para iOS/iPadOS, para que a seleção do tipo 'Dispositivo' seja aplicada a dispositivos 'não geridos', são necessárias configurações adicionais de configuração de aplicações. Estas configurações comunicarão ao serviço APP que uma determinada aplicação é gerida - e que as definições de APP não se aplicarão:

- **IntuneMAMUPN** tem de ser configurado para todas as aplicações geridas pela MDM. Para mais informações, consulte [como gerir a transferência de dados entre as aplicações iOS/iPadOS no Microsoft Intune](data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm).
- **O IntuneMAMDeviceID** deve ser configurado para todas as aplicações geridas por MDM de terceiros e de linha de negócio. O **IntuneMAMDeviceID** deve ser configurado para o token de ID do dispositivo. Por exemplo, `key=IntuneMAMDeviceID, value={{deviceID}}`. Para mais informações, consulte Adicionar políticas de configuração de [aplicações para dispositivos geridos iOS/iPadOS](app-configuration-policies-use-ios.md).
- Se apenas o **IntuneMAMDeviceID** for configurado, a aplicação do Intune irá considerar o dispositivo como não gerido.

> [!NOTE]
> Para informações específicas sobre o suporte iOS/iPadOS sobre políticas de proteção de aplicações baseadas no estado de gestão de dispositivos, consulte as políticas de [proteção mam direcionadas com base no estado](../fundamentals/whats-new-archive.md#mam-protection-policies-targeted-based-on-management-state)de gestão .

## <a name="policy-settings"></a>Definições de política
Para ver uma lista completa das definições de política para iOS/iPadOS e Android, selecione uma das seguintes links:

- [políticas iOS/iPadOS](app-protection-policy-settings-ios.md)
- [Políticas para Android](app-protection-policy-settings-android.md)

## <a name="next-steps"></a>Passos seguintes
[Monitorizar o estado do utilizador e de conformidade](app-protection-policies-monitor.md)

## <a name="see-also"></a>Consulte também
* [O que esperar quando a aplicação Android é gerida por políticas de proteção de aplicações](../fundamentals/end-user-mam-apps-android.md)
* [O que esperar quando a sua aplicação iOS/iPadOS for gerida por políticas de proteção de aplicações](../fundamentals/end-user-mam-apps-ios.md)
