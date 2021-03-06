---
title: Utilize o Microsoft Defender ATP no Microsoft Intune - Azure Microsoft Docs
description: Utilize o Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) com a Intune, incluindo configuração e configuração, embarque dos seus dispositivos Intune com ATP e, em seguida, utilize uma avaliação de risco ATP de dispositivos com o seu dispositivo Intune e políticas de acesso condicional para proteger os recursos da rede.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 35871aba60d45719b9a6da50184a6113f72e6044
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989292"
---
# <a name="enforce-compliance-for-microsoft-defender-atp-with-conditional-access-in-intune"></a>Impor cumprimento do Microsoft Defender ATP com acesso condicional em Intune

Pode integrar o Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) com o Microsoft Intune como uma solução de Defesa de Ameaças Móveis. A integração pode ajudá-lo a prevenir falhas de segurança e limitar o impacto de violações dentro de uma organização. O Microsoft Defender ATP funciona com dispositivos que executam o Windows 10 ou mais tarde, e com dispositivos Android.

Para ter sucesso, utiliza as seguintes configurações em concerto:

- **Estabeleça uma ligação serviço-a-serviço entre intune e Microsoft Defender ATP**. Esta ligação permite ao Microsoft Defender ATP recolher dados sobre o risco da máquina a partir do Windows 10, e dispositivos Android que gere com o Intune.
- **Utilize um perfil de configuração**do dispositivo para dispositivos a bordo com o Microsoft Defender ATP . Você a bordo de dispositivos para configurá-los para comunicar com o Microsoft Defender ATP e fornecer dados que ajudam a avaliar o seu nível de risco.
- **Utilize uma política de conformidade do dispositivo para definir o nível de risco que pretende permitir**. Os níveis de risco são reportados pelo Microsoft Defender ATP. Os dispositivos que excedam o nível de risco permitido são identificados como não conformes.
- **Utilize uma política de acesso condicional** para impedir que os utilizadores acedam a recursos corporativos a partir de dispositivos que não sejam conformes.

Quando integrar o Intune com o Microsoft Defender ATP, pode tirar partido da ATPs Threat & Vulnerability Management (TVM) e [utilizar o Intune para remediar a fraqueza do ponto final identificada pela TVM](atp-manage-vulnerabilities.md).

## <a name="example-of-using-microsoft-defender-atp-with-intune"></a>Exemplo de utilização do Microsoft Defender ATP com Intune

O exemplo que se segue ajuda a explicar como estas soluções funcionam em conjunto para ajudar a proteger a sua organização. Para este exemplo, o Microsoft Defender ATP e o Intune já estão integrados.

Considere um evento onde alguém envia um anexo Word com código malicioso incorporado a um utilizador dentro da sua organização.

- O utilizador abre o anexo e ativa o conteúdo.
- Um ataque de privilégio elevado começa, e um agressor de uma máquina remota tem direitos de administração sobre o dispositivo da vítima.
- O atacante, em seguida, acede remotamente aos outros dispositivos do utilizador. Esta falha de segurança pode afetar toda a organização.

O Microsoft Defender ATP pode ajudar a resolver eventos de segurança como este cenário.

- No nosso exemplo, o Microsoft Defender ATP deteta que o dispositivo executou código anormal, experimentou uma escalada de privilégio de processo, injetou código malicioso e emitiu uma concha remota suspeita.
- Com base nestas ações do dispositivo, o Microsoft Defender ATP [classifica o dispositivo como de alto risco](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity) e inclui um relatório detalhado de atividades suspeitas no portal Microsoft Defender Security Center.

Como tem uma política de conformidade do dispositivo Intune para classificar os dispositivos com um *nível* de risco médio ou *alto* como não conforme, o dispositivo comprometido é classificado como incompatível. Esta classificação permite que a sua política de acesso condicional inicie e bloqueie o acesso desse dispositivo aos seus recursos corporativos.

## <a name="prerequisites"></a>Pré-requisitos

Para utilizar o Microsoft Defender ATP com intune, certifique-se de que tem o seguinte configurado e pronto para ser utilizado:

- Um inquilino com licença para o Enterprise Mobility + Security E3 e o Windows E5 (ou Microsoft 365 Enterprise E5)
- Ambiente Intune da Microsoft, com [Intune gerido](../enrollment/windows-enroll.md) Windows 10, ou dispositivos Android que também são Azure AD
- [Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) e acesso ao Microsoft Defender Security Center (portal ATP)

> [!NOTE]
> O Microsoft Defender ATP não é suportado com políticas de proteção de aplicações iOS/iPadOS e Android Intune.

## <a name="enable-microsoft-defender-atp-in-intune"></a>Ativar o Microsoft Defender ATP em Intune

O primeiro passo que dá é configurar a ligação serviço-a-serviço entre intune e microsoft Defender ATP. Isto requer acesso administrativo tanto ao Microsoft Defender Security Center, como ao Intune.

### <a name="to-enable-defender-atp"></a>Para ativar o Defender ATP

Só precisa de permitir ao Defender ATP uma única vez por inquilino.

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione **segurança endpoint**  >  **Microsoft Defender ATP**, e, em seguida, selecione **Abra o Microsoft Defender Security Center**.

   ![Selecione para abrir o Microsoft Defender Security Center](./media/advanced-threat-protection/atp-device-compliance-open-microsoft-defender.png)

3. No **Microsoft Defender Security Center:**
   1. Selecione **Settings**  >  **Definições Características avançadas**.
   2. Em **Ligação do Microsoft Intune**, escolha **Ligado**:

      ![Ativar a ligação ao Intune](./media/advanced-threat-protection/atp-security-center-intune-toggle.png)

   3. Selecione **Guardar preferências**.

4. Volte ao **Microsoft Defender ATP** no centro de administração do Microsoft Endpoint Manager. De acordo com **as Definições**de Política de Conformidade do MDM, dependendo das necessidades da sua organização:
   - **Detete connect Windows versão 10.0.15063 e acima para Microsoft Defender ATP** para **On** e/ou
   - **Detete os dispositivos Android da versão 6.0.0 e acima para o Microsoft Defender ATP** to **On**.

5. Selecione **Guardar**.

> [!TIP]
> Quando integra uma nova aplicação para intune Mobile Threat Defense e permite a ligação a Intune, Intune cria uma política clássica de acesso condicional no Diretório Ativo Azure. Cada aplicação MTD que integra, incluindo [o Defender ATP](advanced-threat-protection.md) ou qualquer um dos [nossos parceiros mTD](mobile-threat-defense.md#mobile-threat-defense-partners)adicionais, cria uma nova política clássica de acesso condicional. Estas políticas podem ser ignoradas, mas não devem ser editadas, eliminadas ou desativadas.
>
> Se a política clássica for eliminada, terá de apagar a ligação ao Intune que foi responsável pela sua criação e, em seguida, instalá-la novamente. Isto recria a política clássica. Não é suportado para migrar políticas clássicas para aplicações MTD para o novo tipo de política de acesso condicional.
>
> Políticas clássicas de acesso condicional para aplicações MTD:
>
> - São utilizados pela Intune MTD para exigir que os dispositivos estejam registados em Azure AD para que tenham um ID de dispositivo antes de comunicarem com os parceiros MTD. O ID é necessário para que os dispositivos e possam reportar com sucesso o seu estado a Intune.
> - Não tenha qualquer efeito em quaisquer outras aplicações ou Recursos cloud.
> - São diferentes das políticas de acesso condicional que pode criar para ajudar a gerir o MTD.
> - Por defeito, não interaja com outras políticas de acesso condicional que utiliza para avaliação.
>
> Para ver as políticas clássicas de acesso condicional, em [Azure,](https://portal.azure.com/#home)vá às políticas clássicas de acesso condicional do **Diretório Ativo Azure.**  >  **Conditional Access**  >  **Classic policies**

## <a name="onboard-windows-devices-by-using-a-configuration-profile"></a>Dispositivos Windows a bordo utilizando um perfil de configuração 

Para a plataforma Windows, depois de estabelecer a ligação serviço-a-serviço entre intune e microsoft Defender ATP, você a bordo dos seus dispositivos geridos intune para ATP para que os dados sobre o seu nível de risco possam ser recolhidos e utilizados. Para os dispositivos a bordo, utiliza um perfil de configuração do dispositivo para o MICROSOFT Defender ATP.

Quando estabeleceu a ligação ao Microsoft Defender ATP, intune recebeu um pacote de configuração atp do Microsoft Defender a partir do MICROSOFT Defender ATP. Esta embalagem é implantada para dispositivos com o perfil de configuração do dispositivo. O pacote de configuração configura dispositivos para comunicar com [os serviços ATP do Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) para digitalizar ficheiros, detetar ameaças e reportar o risco ao Microsoft Defender ATP. Depois de embarcar num dispositivo utilizando um pacote de configuração, não precisa voltar a fazê-lo. Também pode embarcar em dispositivos utilizando uma política de [grupo ou o Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints).

### <a name="create-the-device-configuration-profile"></a>Criar o perfil de configuração do dispositivo

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **perfis**de configuração de  >  **dispositivos**  >  **Criar perfil**.
3. Introduza um **Nome** e uma **Descrição**.
4. Para **plataforma**, selecione **Windows 10 e mais tarde** 
5. Para **o tipo de perfil,** selecione Microsoft Defender **ATP (Windows 10 Desktop)**.
6. Configure as definições:

   - Tipo de pacote de configuração do **cliente MICROSOFT Defender ATP**: Selecione No **quadro** para adicionar o pacote de configuração ao perfil. Selecione **Descarregar** para remover o pacote de configuração do perfil.
  
     > [!NOTE]
     > Se estabeleceu corretamente uma ligação com o Microsoft Defender ATP, o Intune irá automaticamente **embarcar** no perfil de configuração para si e a definição do tipo de pacote de configuração do **cliente MICROSOFT Defender ATP** não estará disponível.
  
   - **Partilha de amostras para todos os ficheiros**: **Enable** permite recolher amostras e partilhada com o Microsoft Defender ATP. Por exemplo, se vir um ficheiro suspeito, pode submetê-lo ao Microsoft Defender ATP para análise profunda. **Não configurado** não partilha nenhuma amostra para o Microsoft Defender ATP.
   - **Acelere a frequência**de reporte de telemetria : Para dispositivos de alto risco, **ative** esta definição para que reporte telemetria ao serviço ATP microsoft Defender com mais frequência.

     [As máquinas a bordo do Windows 10 que utilizam o Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-sccm) têm mais detalhes sobre estas definições ATP do Microsoft Defender.

7. Selecione **OK** e **Criar** para guardar as alterações. O perfil será criado.
8. [Atribuir o perfil de configuração do dispositivo](../configuration/device-profile-assign.md) aos dispositivos que pretende avaliar com o Microsoft Defender ATP.

## <a name="create-and-assign-the-compliance-policy"></a>Criar e atribuir a política de conformidade

Tanto para dispositivos Windows como Android, a política de conformidade determina o nível de risco que considera aceitável para um dispositivo.

Se não estiver familiarizado com a criação de uma política de conformidade, consulte o Procedimento [de Política Criar um](../protect/create-compliance-policy.md#create-the-policy) procedimento de conformidade no artigo Microsoft *Intune.* As seguintes informações são específicas para configurar o Defender ATP como parte de uma política de conformidade.

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione Políticas de conformidade de **dispositivos**  >  **Compliance policies**  >  **Policies**  >  **Criar política**.

3. Para **a Plataforma** selecione Windows *10 e mais tarde*, administrador de **dispositivos Android**, e/ou Android **Enterprise**. Em seguida, selecione **Criar** para abrir a janela de configuração da **política Criar.**

4. Especifique um **nome** que o ajude a identificar isto mais tarde. Também pode optar por especificar uma **Descrição**.
  
5. No separador **de definições** de Conformidade, expanda o grupo **ATP** do Microsoft Defender e desloque-se Exigir que o dispositivo esteja na pontuação de risco da **máquina ou abaixo da pontuação** de risco da máquina ao nível preferido.

   As classificações de nível de ameaça são [determinadas pelo Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue).

   - **Seguro**: este é o nível mais seguro. O dispositivo não pode ter ameaças existentes e ainda aceder aos recursos da empresa. Se forem detetadas ameaças, o dispositivo será avaliado como não conforme. (Microsoft Defender ATP utiliza o valor *Secure*.)
   - **Baixo**: o dispositivo estará em conformidade se só existirem ameaças de nível baixo. Dispositivos com níveis de ameaça médios ou elevados não são compatíveis.
   - **Médio**: o dispositivo estará conforme se as ameaças encontradas no dispositivo forem de nível baixo ou médio. Se forem detetadas ameaças de nível alto, o estado do dispositivo será determinado como não conforme.
   - **Alto**: Este nível é o menos seguro e permite todos os níveis de ameaça. Assim, os dispositivos que com níveis de ameaça elevados, médios ou baixos são considerados conformes.

6. Complete a configuração da política, incluindo a atribuição da política aos grupos aplicáveis.

## <a name="create-a-conditional-access-policy"></a>Criar uma política de acesso condicional

A política de Acesso Condicional bloqueia o acesso a recursos para dispositivos que excedam o nível de ameaça que definiu na sua política de conformidade. Pode bloquear o acesso do dispositivo a recursos corporativos, como o SharePoint ou o Exchange Online.

> [!TIP]
> O Acesso Condicional é uma tecnologia do Azure Active Directory (Azure AD). O nó de Acesso Condicional acedido a partir do centro de administração do Microsoft Endpoint Manager é o mesmo nó a que o *Azure AD*.

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione **segurança de fim de**ponta Acesso  >  **condicional**  >  **Nova política**.

3. Introduza um **Nome** para a política e selecione **Utilizadores e grupos**. Utilize as opções Incluir ou Excluir para adicionar os grupos à política e selecione **Concluído**.

4. Selecione **Aplicações na cloud** e escolha as aplicações que quer proteger. Por exemplo, escolha **Selecionar aplicações** e selecione **Office 365 SharePoint Online** e **Office 365 Exchange Online**.

   Selecione **Concluído** para guardar as alterações.

5. Selecione **Conditions**  >  **Condições Aplicações cliente** para aplicar a política a apps e navegadores. Por exemplo, selecione **Sim** e, em seguida, ative **Browser** e **Aplicações móveis e clientes de ambiente de trabalho**.

   Selecione **Concluído** para guardar as alterações.

6. Selecione **Grant** para aplicar acesso condicional com base na conformidade do dispositivo. Por exemplo, selecione **Acesso de concessão**Exigir que  >  **o dispositivo seja marcado como conforme**.

    Escolha **Selecionar** para guardar as alterações.

7. Selecione **Ativar política** e, em seguida, **Criar** para guardar as alterações.

## <a name="monitor-device-compliance"></a>Monitorizar a conformidade do dispositivo

Em seguida, monitorize o estado dos dispositivos que têm a política de conformidade ATP do Microsoft Defender.

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione **Dispositivos**  >  **Monitor**  >  **De conformidade**com a política .

3. Encontre a sua política ATP microsoft Defender na lista e veja quais os dispositivos conformes ou não conformes.

Também pode utilizar o relatório *operacional* para dispositivos não conformes a partir do mesmo local:

1. Selecione **dispositivos**  >  **Monitor de**  >  **dispositivos não conformes**.

Para obter mais informações sobre relatórios, consulte [os relatórios Intune](../fundamentals/reports.md).

## <a name="view-onboarding-status"></a>Ver estado de embarque

Para ver o estado de embarque de todos os dispositivos do Windows 10 geridos por Intune, pode ir para a **segurança Endpoint**  >  **Microsoft Defender ATP**. A partir desta página, também pode iniciar a criação de um perfil de configuração do dispositivo para embarcar mais dispositivos para o MICROSOFT Defender ATP.

## <a name="next-steps"></a>Passos seguintes

[Microsoft Defender ATP Acesso Condicional](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access)

[Painel de risco ATP do Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)

[Utilize tarefas de segurança com a Gestão de Vulnerabilidades ATPs para remediar problemas nos dispositivos](atp-manage-vulnerabilities.md).

[Introdução às políticas de conformidade de dispositivos](device-compliance-get-started.md)
