---
title: Novidades no arquivo do portal clássico do Microsoft Intune
description: Anúncios de Novidades do Microsoft Intune arquivados
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/08/2017
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ed2db991-4729-49a7-a1e6-be2ffa0d03d1
ROBOTS: noindex,nofollow
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: e3c939b2b21bc8bfbf82a997c05f24d91c487a9e
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81681975"
---
# <a name="whats-new-in-the-intune-classic-portal---previous-months"></a>Novidades no portal clássico do Intune – meses anteriores

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

Esta página apresenta as novas funcionalidades e avisos anunciados anteriormente na [página Novidades](whats-new.md) do portal clássico do Intune.

## <a name="april-2017"></a>Abril de 2017

### <a name="new-capabilities"></a>Novas funcionalidades

#### <a name="myapps-available-for-managed-browser---822308-822303--"></a>My Apps disponível para o Managed Browser  <!--822308, 822303-->

O Microsoft My Apps agora tem melhor suporte no Managed Browser. Os utilizadores do Managed Browser que não forem geridos poderão aceder diretamente ao serviço My Apps e às aplicações SaaS aprovisionadas pelo administrador. Os utilizadores geridos através do Intune poderão continuar a aceder ao My Apps a partir do marcador incorporado no Managed Browser.

#### <a name="new-icons-for-the-managed-browser-and-the-company-portal---918433-918431-971473--"></a>Novos ícones para o Managed Browser e o Portal da Empresa  <!--918433, 918431, 971473-->

O Managed Browser receberá ícones atualizados nas versões para Android e iOS da aplicação. O novo ícone incluirá o emblema do Intune atualizado para o tornar mais consistente com as outras aplicações no Enterprise Mobility + Security (EM+S). Pode ver o novo ícone do Managed Browser na [página Novidades na IU da aplicação Intune](whats-new-app-ui.md).

O Portal da Empresa também receberá ícones atualizados para as versões para Android, iOS e Windows da aplicação para melhorar a consistência com as outras aplicações no EM+S. Estes ícones serão lançados gradualmente nas plataformas a partir de abril até finais de maio.

#### <a name="sign-in-progress-indicator-in-android-company-portal---953374--"></a>Indicador de progresso de início de sessão no Portal da Empresa para Android  <!--953374-->

Uma atualização à aplicação Portal da Empresa para Android mostra um indicador de progresso de início de sessão quando o utilizador inicia ou retoma a aplicação. O indicador mostra novos estados de progresso, a começar com “A ligar...”, “A iniciar sessão...” e “A verificar os requisitos de segurança...” antes de o utilizador poder aceder à aplicação. Pode ver os novos ecrãs para a aplicação Portal da Empresa para Android na [página Novidades na IU da Aplicação Intune](whats-new-app-ui.md).

#### <a name="block-apps-from-accessing-sharepoint-online----679339---"></a>Impedir que as aplicações acedam ao SharePoint Online <!-- 679339 -->

Agora pode criar uma política de acesso condicional baseada em aplicações para bloquear aplicações, que não têm políticas de proteção de aplicações aplicadas, desde o acesso ao [SharePoint Online](../protect/app-based-conditional-access-intune-create.md). No cenário de Acesso Condicional baseado em aplicações, pode especificar as aplicações que pretende ter acesso ao SharePoint Online através do portal Azure.

#### <a name="single-sign-on-support-from-the-company-portal-for-ios-to-outlook-for-ios---834012--"></a>Suporte de início de sessão único a partir do Portal da Empresa para iOS para o Outlook para iOS  <!--834012-->
Os utilizadores já não precisam de iniciar sessão na aplicação Outlook se já tiverem sessão iniciada no Portal da Empresa para iOS no mesmo dispositivo com a mesma conta. Quando os utilizadores iniciarem o Outlook, poderão selecionar a conta e iniciar sessão automaticamente. Também estamos a trabalhar no sentido de adicionar esta funcionalidade a outras aplicações da Microsoft.

#### <a name="improved-status-messaging-in-the-company-portal-app-for-ios---744866--"></a>Mensagem de estado melhorada na aplicação Portal da Empresa para iOS  <!--744866-->
Serão apresentadas novas mensagens mais específicas na aplicação Portal da Empresa para iOS para fornecer informações mais acessíveis sobre as ocorrências nos dispositivos. Estes erros eram anteriormente incluídos numa mensagem de erro geral que informava "O Portal da Empresa Está Temporariamente Indisponível". Além disso, se um utilizador iniciar o Portal da Empresa em iOS sem estar ligado à Internet, verá uma barra de estado persistente na home page a informar "Sem Ligação à Internet."

#### <a name="improved-app-install-status-for-the-windows-10-company-portal-app---676495--"></a>Estado da instalação de aplicações melhorado para a aplicação Portal da Empresa do Windows 10  <!--676495-->

Novas melhorias para a instalação de apps iniciadas na aplicação Portal da Empresa Do Windows 10 incluem:
- Relatórios mais rápidos do progresso da instalação para pacotes MSI
- Relatórios mais rápidos do progresso da instalação para aplicações modernas em dispositivos com a Atualização de Aniversário do Windows 10 e versões superiores
- Nova barra de progresso para as instalações de aplicações modernas em dispositivos com a Atualização de Aniversário do Windows 10 e versões superiores

Pode ver a nova barra de progresso na [página Novidades na IU da aplicação Intune](whats-new-app-ui.md).

#### <a name="bulk-enroll-windows-10-devices----747607---"></a>Inscrever dispositivos Windows 10 em massa <!-- 747607 -->

Agora, pode juntar-se a um grande número de dispositivos que executam a atualização para Criativos do Windows 10 para o Azure Active Directory e o Intune com o Windows Configuration Designer (WCD). Para ativar a [inscrição na MDM em massa](../enrollment/windows-bulk-enroll.md) para o seu inquilino do Azure AD, crie um pacote de aprovisionamento que associe dispositivos ao seu inquilino do Azure AD através do Windows Configuration Designer e aplique o pacote aos dispositivos pertencentes à empresa que pretende inscrever e gerir em massa. Assim que o pacote for aplicado aos dispositivos, estes são associados ao Azure AD, inscritos no Intune e estarão prontos para os seus utilizadores do Azure AD iniciarem sessão.  Os utilizadores do Azure AD são utilizadores padrão nestes dispositivos e obtêm as políticas atribuídas e as aplicações necessárias. De momento, os cenários Self-service e Portal da Empresa não são suportados.

### <a name="whats-new-in-the-public-preview-of-intune-in-the-azure-portal--736542--"></a>Novidades na pré-visualização pública do Intune no portal do Azure <!--736542-->

No início do ano civil de 2017 vamos migrar a nossa experiência de administração completa para o Azure, permitindo uma gestão poderosa e integrada dos fluxos de trabalho em EMS centrais numa plataforma de serviço moderna que é extensível usando APIs gráficos.

Os novos inquilinos de avaliação começarão a ver a pré-visualização pública da nova experiência de administrador no portal do Azure este mês. Enquanto estiverem no estado de pré-visualização, as capacidades e a paridade com a consola do Intune existente serão proporcionadas iterativamente.

A experiência de administração no portal do Azure irá utilizar a já anunciada nova funcionalidade de agrupamento e filtragem; quando o seu inquilino existente é migrado para a nova experiência de agrupamento, o utilizador também será migrado para pré-visualizar a nova experiência de administração do inquilino. Entretanto, se pretende testar ou observar qualquer uma das novas funcionalidades até que o seu inquilino seja migrado, inscreva-se para uma nova conta de avaliação do Intune ou veja a [nova documentação](whats-new.md).

Pode encontrar as novidades na pré-visualização do Intune no Azure [aqui](whats-new.md).

### <a name="notices"></a>Avisos

#### <a name="direct-access-to-apple-enrollment-scenarios---951869--"></a>Acesso direto aos cenários de inscrição da Apple <!--951869-->

Para as contas do Intune criadas depois de janeiro de 2017, o Intune ativou o acesso direto aos cenários de inscrição da Apple através da carga de trabalho Inscrever Dispositivos no portal de pré-visualização do Azure. Anteriormente, a pré-visualização da inscrição da Apple apenas estava acessível a partir de ligações no portal do Azure. As contas do Intune criadas antes de Janeiro de 2017 precisam de uma única migração antes de estas funcionalidades ficarem disponíveis no Azure. A agenda para a migração ainda não foi anunciada, mas os detalhes serão disponibilizados logo que possível. Recomendamos vivamente a criação de uma conta de avaliação para testar a nova experiência se a conta existente não conseguir aceder à pré-visualização.

#### <a name="whats-coming-for-appx-in-intune-in-the-azure-portal----1000270---"></a>Novidades futuras para Appx no Intune no portal do Azure  <!-- 1000270 -->

Como parte da migração do Intune para o portal do Azure, estamos a efetuar três alterações à aplicação appx:

1. Adicionar um novo tipo de aplicação appx na consola do Intune que só pode ser implementada em dispositivos inscritos em MDM.
2. Alterar o tipo de aplicação appx existente para apenas ser direcionada para PCs geridos através do agente do Intune para PC.
3. Converter todas as appxs existentes em appxs de MDM com a migração.

##### <a name="how-does-this-affect-me"></a>Como é que isto me afeta?

Não irá afetar as suas implementações existentes em dispositivos geridos através do agente do Intune para PC. No entanto, após a migração, não poderá implementar appxs migradas em novos dispositivos geridos através do agente do Intune para PC que não tenham sido abrangidas anteriormente.

##### <a name="what-action-do-i-need-to-take"></a>Que medidas tenho de tomar

Após a migração, terá de voltar a carregar a appx como uma appx para PC, se quiser efetuar novas implementações em PC. Para saber mais, veja [Appx changes in Intune on Azure (Alterações à aplicação appx no Intune no Azure)](https://aka.ms/appxchange) no blogue da Equipa de Suporte do Intune.  

#### <a name="administration-roles-being-replaced-in-azure-portal"></a>Substituição das funções de administração no portal do Azure

As funções de administração de gestão de aplicações móveis (MAM) existentes (Contribuidor, Proprietário e Só de leitura) utilizadas no portal clássico do Intune (Silverlight) estão a ser substituídas por um conjunto completo de novos controlos de administração baseados em funções (RBAC) no portal do Azure no Intune. Após concluir a migração para o portal do Azure, terá de atribuir novamente os seus administradores a estas novas funções de administração. Para obter mais informações sobre as RBAC e as novas funções, veja [Controlo de acesso baseado em funções do Microsoft Intune](role-based-access-control.md).

### <a name="whats-coming"></a>Novidades futuras

#### <a name="improved-sign-in-experience-across-company-portal-apps-for-all-platforms---user-story-1132123--"></a>Experiência de início de sessão melhorada nas aplicações Portal da Empresa para todas as plataformas <!--User Story 1132123-->

Anunciamos uma alteração que ficará disponível nos próximos meses e irá melhorar a experiência de início de sessão nas aplicações do Portal da Empresa do Intune para Android, iOS e Windows. A nova experiência de utilizador será apresentada automaticamente em todas as plataformas da aplicação Portal da Empresa quando o Azure AD fizer esta alteração. Além disso, os utilizadores podem agora iniciar sessão no Portal da Empresa a partir de outro dispositivo com um código gerado, de utilização única. Tal é especialmente útil nos casos em que os utilizadores precisam de iniciar sessão sem credenciais.

Pode encontrar capturas de ecrã da experiência de início de sessão anterior, a nova experiência de início de sessão com credenciais e a experiência de início de sessão a partir de outro dispositivo na página [Novidades na IU da aplicação](whats-new-app-ui.md).

#### <a name="plan-for-change-intune-is-changing-the-intune-partner-portal-experience----1050016---"></a>Planear a alteração: o Intune vai alterar a experiência do Portal de Parceiros do Intune  <!-- 1050016 -->

A partir da atualização de serviço que se realizará em meados de maio de 2017, iremos remover a página Parceiro do Intune de manage.microsoft.com.  

Se for um administrador parceiro, já não poderá ver e agir em nome dos clientes a partir da página Parceiro do Intune. Em vez disso, terá de iniciar sessão num dos dois outros portais de parceiro da Microsoft.

Tanto o [Microsoft Partner Center](https://partnercenter.microsoft.com/) como o Microsoft [365 administrador center](https://admin.microsoft.com/) permitir-lhe-ão assinar nas contas de clientes que gere. De futuro, utilize um destes sites para gerir os seus clientes.


#### <a name="apple-to-require-updates-for-application-transport-security---748318--"></a>A Apple passará a exigir atualizações para a Segurança de Transporte de Aplicações  <!--748318-->

A Apple anunciou que irá impor requisitos específicos para a Segurança de Transporte de Aplicações (ATS). A ATS é utilizada para impor medidas de segurança mais rigorosas em todas as comunicações feitas por aplicações através de HTTPS. Esta alteração irá afetar os clientes do Intune que utilizam as aplicações do Portal da Empresa para iOS.

Disponibilizamos uma versão da aplicação do Portal da Empresa para iOS através do programa TestFlight da Apple que impõe os novos requisitos da ATS. Se quiser experimentá-lo para que possa testar a <a href="mailto:CompanyPortalBeta@microsoft.com?subject=Register to TestFlight ATS Company Portal app">CompanyPortalBeta@microsoft.com</a> sua conformidade com o ATS, envie um e-mail com o seu primeiro nome, apelido, endereço de e-mail e nome da empresa. Consulte o nosso [blogue de suporte do Intune](https://aka.ms/compportalats) para obter mais detalhes.

## <a name="march-2017"></a>Março de 2017

### <a name="new-capabilities"></a>Novas Funcionalidades

#### <a name="support-for-skycure"></a>Suporte para Skycure

Agora pode controlar o acesso de dispositivos móveis a recursos corporativos utilizando o Acesso Condicional com base na avaliação de risco realizada pela Skycure, uma solução de defesa de ameaças móveis que se integra com a Microsoft Intune. O risco é avaliado com base na telemetria recolhida dos dispositivos através do Skycure, incluindo:

- Defesa física
- Defesa da rede
- Defesa da aplicação
- Defesa contra vulnerabilidades

Pode configurar as políticas de acesso condicional em EMS com base na avaliação de risco Symantec Endpoint Protection Mobile (Skycure) ativada através de políticas de conformidade do dispositivo Intune. Pode utilizar estas políticas para permitir ou bloquear o acesso de dispositivos não conformes aos recursos empresariais, com base nas ameaças detetadas. Para mais informações, consulte o [conector Symantec Endpoint Protection Mobile](../protect/skycure-mobile-threat-defense-connector.md).

#### <a name="new-user-experience-for-the-company-portal-app-for-android---621622--"></a>Nova experiência de utilizador da aplicação Portal da Empresa para Android <!--621622-->

A aplicação Portal da Empresa para Android irá atualizar a respetiva interface de utilizador para obter um aspeto mais moderno e a melhor experiência de utilizador. As atualizações relevantes são:

- Cores: os cabeçalhos dos separadores do Portal da Empresa têm as cores da imagem corporativa definida pelas TI.
- Aplicações: no separador **Aplicações**, os botões **Aplicações em Destaque** e **Todas as Aplicações** são atualizados.
- Pesquisar: no separador **Aplicações**, o botão **Pesquisar** é um botão de ação flutuante.
- Navegar em Aplicações: a vista **Todas as Aplicações** mostra uma vista com os separadores **Em Destaque**, **Todas** e **Categorias** para uma navegação mais fácil.
- Suporte: os separadores **Os Meus Dispositivos** e **Contactar TI** são atualizados para melhorar a legibilidade.

Para obter mais detalhes sobre estas alterações, veja [Atualização da IU para aplicações de utilizadores finais do Intune](whats-new-app-ui.md).

#### <a name="non-managed-devices-can-access-assigned-apps---664691--"></a>Os dispositivos não geridos podem aceder a aplicações atribuídas <!--664691-->

Como parte das alterações de estrutura no site do Portal da Empresa, os utilizadores de iOS e Android poderão instalar aplicações atribuídas a eles próprios como "disponíveis sem inscrição" nos seus dispositivos não geridos. Com as suas credenciais do Intune, os utilizadores poderão iniciar sessão no site do Portal da Empresa e ver as listas de aplicações atribuídas a eles próprios. Os pacotes de aplicações das aplicações "disponíveis sem inscrição" estão disponíveis para transferência através do site do Portal da Empresa. As aplicações que requerem inscrição para instalação não são afetadas por esta alteração, uma vez que será solicitado aos utilizadores que inscrevam o seu dispositivo se quiserem instalar essas aplicações.

#### <a name="signing-script-for-windows-10-company-portal---941642--"></a>Script de Assinatura para o Portal da Empresa do Windows 10  <!--941642-->

Se precisar de transferir e de carregar em sideload a aplicação Portal da Empresa do Windows 10, poderá agora utilizar um script para simplificar e otimizar o processo de assinatura de aplicações para a sua organização.   Para transferir o script e as instruções para o utilizar, veja [Microsoft Intune Signing Script for Windows 10 Company Portal (Script de Assinatura do Microsoft Intune para o Portal da Empresa do Windows 10)](https://aka.ms/win10cpscript) na Galeria do TechNet. Para obter mais detalhes sobre este anúncio, veja [Updating your Windows 10 Company Portal app (Atualizar a aplicação do Portal da Empresa do Windows 10)](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) no Blogue da Equipa de Suporte do Intune.


### <a name="notices"></a>Avisos

#### <a name="support-for-ios-103"></a>Suporte para iOS 10.3

A versão do iOS 10.3 começou a ser implementada a 27 de março de 2017 para os utilizadores de iOS. Todos os cenários existentes de INTUNE MDM e MAM são compatíveis com a versão mais recente do OS da Apple. Prevemos que todas as funcionalidades existentes do Intune atualmente disponíveis para gerir dispositivos iOS continuem a funcionar quando os utilizadores atualizarem os seus dispositivos e aplicações para o iOS 10.3.

Não existem atualmente problemas conhecidos para partilhar. Caso se depare com problemas com o iOS 10.3, contacte a [equipa de suporte do Intune](get-support.md).

#### <a name="improved-support-for-android-users-based-in-china---720444--"></a>Suporte melhorado para os utilizadores do Android sediados na China <!--720444-->

Devido à ausência da Google Play Store na China, os dispositivos Android têm de obter aplicações a partir de mercados chineses. O Portal da Empresa suportará este fluxo de trabalho ao redirecionar os utilizadores do Android na China para transferirem as aplicações Portal da Empresa e Outlook a partir de lojas de aplicações locais. Deste modo, irá melhorar a experiência do utilizador quando as políticas de Acesso Condicional são ativadas, tanto para a Gestão de Dispositivos Móveis como para a Gestão de Aplicações Móveis. As aplicações Portal da Empresa e Outlook para Android estão disponíveis nas seguintes lojas de aplicações chinesas:

- [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
- [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
- [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
- [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

#### <a name="best-practice-make-sure-your-company-portal-apps-are-up-to-date---879465--"></a>Melhor prática: confirme se as aplicações do Portal da Empresa estão atualizadas  <!--879465-->

Em dezembro de 2016, lançamos uma atualização que permitia a imposição da autenticação multifator (MFA) num grupo de utilizadores no momento da inscrição de um dispositivo iOS, Android, Windows 8.1 e superior ou Windows Phone 8.1 e superior. Esta funcionalidade não pode funcionar sem determinadas versões de linha de base da aplicação Portal da Empresa para Android (v5.0.3419.0+) e iOS (v2.1.17+).

A Microsoft está continuamente a melhorar o Intune ao adicionar novas funções à consola e às aplicações Portal da Empresa em todas as plataformas suportadas. Como resultado, a Microsoft apenas lança correções para problemas que encontramos na versão atual da aplicação Portal da Empresa. Como tal, recomendamos que utilize as versões mais recentes das aplicações Portal da Empresa para obter a melhor experiência de utilizador.

>[!Tip]
> Solicite aos seus utilizadores que configurem os dispositivos para atualizarem automaticamente as aplicações da loja de aplicações adequada. Se tiver disponibilizado a aplicação Portal da Empresa do Android numa partilha de rede, poderá transferir a versão mais recente a partir do [Centro de Transferências da Microsoft](https://www.microsoft.com/download/details.aspx?id=49140).

#### <a name="microsoft-teams-is-now-enabled-for-mam-on-ios-and-android"></a>O Microsoft Teams está agora ativado para a MAM no iOS e no Android

A Microsoft anunciou a disponibilidade geral do Microsoft Teams. As aplicações Microsoft Teams atualizadas para iOS e Android estão agora ativadas com capacidades de gestão de aplicações móveis (MAM) do Intune para permitir que as suas equipas trabalhem livremente em vários dispositivos, garantindo que as conversas e os dados empresariais estão sempre protegidos. Para obter mais detalhes, veja [o anúncio do Microsoft Teams](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/) no blogue do Enterprise Mobility and Security.


## <a name="february-2017"></a>Fevereiro de 2017

### <a name="new-capabilities"></a>Novas Funcionalidades

### <a name="modernizing-the-company-portal-website---753980--"></a>Modernizar o site do Portal da Empresa  <!--753980-->
O site do Portal da Empresa irá suportar aplicações visadas para utilizadores que não têm dispositivos geridos. O site será alinhado com outros produtos e serviços Microsoft através de um novo esquema de cores contrastante, ilustrações dinâmicas e um menu de opções, ![Pequena imagem do menu de opções adicionado ao canto superior esquerdo do site do Portal da Empresa](./media/whats-new-archive-classic/CP_hamburger_menu.png).

### <a name="notices"></a>Avisos

#### <a name="group-migration-will-not-require-any-updates-to-groups-or-policies-for-ios-devices---898837--"></a>A migração de grupos não irá necessitar de atualizações de grupos ou políticas para dispositivos iOS  <!--898837-->
Para cada grupo de dispositivos Intune pré-atribuído por um perfil de Inscrição de Dispositivos Corporativos, um grupo de dispositivos dinâmicos correspondente será criado em AAD com base no nome do perfil de Inscrição de Dispositivos Corporativos, durante a migração para grupos de dispositivos de Diretório Ativo Azure. Essa ação irá garantir que, à medida que os dispositivos forem inscritos, os mesmos serão agrupados automaticamente e receberão as mesmas políticas e aplicações que o grupo original do Intune.

Quando um inquilino iniciar o processo de migração para agrupamento e direcionamento, o Intune irá criar automaticamente um grupo dinâmico do AAD para corresponder a um grupo do Intune visado por um perfil de Inscrição de Dispositivos da Empresa. Se o Administrador do Intune eliminar o grupo visado do Intune, o grupo dinâmico do AAD correspondente não será eliminado. A consulta dinâmica e os membros do grupo serão desmarcados, mas o grupo em si permanecerá até o Administrador de TI o eliminar através do portal do AAD.

Do mesmo modo, se o Administrador de TI alterar o grupo do Intune visado por um perfil de Inscrição de Dispositivos da Empresa, o Intune irá criar um grupo dinâmico novo que reflita a nova atribuição de perfil, mas não irá eliminar o grupo dinâmico criado para a atribuição antiga.

### <a name="defaulting-to-managing-windows-desktop-devices-through-windows-settings---663050--"></a>Utilizar a predefinição para gerir computadores Windows através das definições do Windows <!--663050-->
O comportamento predefinido de inscrição de computadores com Windows 10 irá mudar. As novas inscrições seguirão o fluxo de inscrição do agente MDM normal, em vez de através do agente de PC. O site do Portal da Empresa irá fornecer aos utilizadores de computadores com Windows 10 instruções para ajudá-los durante o processo de adicionar computadores com Windows 10 como dispositivos móveis. Isto não afetará os PCs atualmente inscritos e a sua organização pode continuar a gerir os computadores com Windows 10 através do agente de PC, [se preferir](manage-windows-pcs-with-microsoft-intune.md).

#### <a name="improving-mobile-app-management-support-for-selective-wipe---581242--"></a>Melhorar o suporte de gestão de aplicações móveis para eliminação seletiva  <!--581242-->
Os utilizadores finais receberão orientações adicionais sobre como recuperar o acesso a dados escolares ou profissionais se esses dados forem automaticamente removidos devido à política "Intervalo offline antes de os dados da aplicação serem apagados".<!--, or the removal of the Intune Company Portal on Android.-->

#### <a name="company-portal-for-ios-links-open-inside-the-app---665954--"></a>As ligações do Portal da Empresa para iOS são abertas dentro da aplicação  <!--665954-->
As ligações na aplicação Portal da Empresa para iOS, incluindo as referentes a documentação e aplicações, serão abertas diretamente na aplicação Portal da Empresa através de uma vista do Safari na aplicação. Esta atualização será fornecida separadamente da atualização do serviço em janeiro.

#### <a name="new-mdm-server-address-for-windows-devices---893007--"></a>Novo endereço do servidor MDM para dispositivos Windows  <!--893007-->
Os utilizadores do Windows e do Windows Phone não conseguirão inscrever um dispositivo se introduzirem __manage.microsoft.com__ como endereço do servidor MDM (se solicitado). O endereço do servidor MDM será alterado de __manage.microsoft.com__ para __enrollment.manage.microsoft.com__. Informe o seu utilizador para utilizar __enrollment.manage.microsoft.com__ como endereço do servidor MDM, se solicitado durante a inscrição de um dispositivo Windows ou Windows Phone. Não necessita de efetuar alterações à configuração do seu CNAME. Para obter mais informações sobre esta alteração, visite [aka.ms/intuneenrollsvrchange](https://aka.ms/intuneenrollsvrchange).

#### <a name="new-user-experience-for-the-company-portal-app-for-android---621622--"></a>Nova experiência de utilizador da aplicação Portal da Empresa para Android <!--621622-->
A partir de março, a aplicação Portal da Empresa para Android seguirá as [diretrizes de conceção do material](https://material.io/guidelines/material-design/introduction.html) para criar um aspeto e funcionalidade mais modernos. Esta experiência de utilizador melhorada inclui:

* __Cores__: os cabeçalhos dos separadores podem ser coloridos de acordo com a sua paleta de cores personalizada.
* __Interface__: Apps em destaque e todos os botões de apps foram atualizados no separador Apps. O botão 'Busca' é agora um botão de ação flutuante.
* __Navegação__: Todas as Aplicações mostram uma visão atabada de Featured, All and Categories para uma navegação mais fácil.
* __Serviço__: os separadores Os Meus Dispositivos e Contactar TI foram melhorados para facilitar a leitura.

Poderá encontrar imagens de antes e depois na [página de atualizações de IU](whats-new-app-ui.md).

### <a name="associate-multiple-management-tools-with-the-microsoft-store-for-business---926135--"></a>Associar várias ferramentas de gestão à Loja Microsoft para Empresas  <!--926135-->
Se estiver a utilizar mais do que uma ferramenta de gestão para implementar aplicações da Loja Microsoft para Empresas, antes só podia associar uma destas com a Loja Microsoft para Empresas. Agora, pode associar várias ferramentas de gestão com a loja, como o Intune e o Configuration Manager. Para obter mais detalhes, veja [Gerir aplicações compradas na Loja Microsoft para Empresas com o Microsoft Intune](../apps/windows-store-for-business.md).

## <a name="whats-new-in-the-public-preview-of-intune-in-the-azure-portal---736542--"></a>Novidades na pré-visualização pública do Intune no portal do Azure  <!--736542-->

No início do ano civil de 2017 vamos migrar a nossa experiência de administração completa para o Azure, permitindo uma gestão poderosa e integrada dos fluxos de trabalho em EMS centrais numa plataforma de serviço moderna que é extensível usando APIs gráficos.

Os novos inquilinos de avaliação começarão a ver a pré-visualização pública da nova experiência de administrador no portal do Azure este mês. Enquanto estiverem no estado de pré-visualização, as capacidades e a paridade com a consola do Intune existente serão proporcionadas iterativamente.

A experiência de administração no portal do Azure irá utilizar a já anunciada nova funcionalidade de agrupamento e filtragem; quando o seu inquilino existente é migrado para a nova experiência de agrupamento, o utilizador também será migrado para pré-visualizar a nova experiência de administração do inquilino. Entretanto, se pretende testar ou observar qualquer uma das novas funcionalidades até que o seu inquilino seja migrado, inscreva-se para uma nova conta de avaliação do Intune ou veja a [nova documentação](whats-new.md).

Pode encontrar as novidades na pré-visualização do Intune no Azure [aqui](whats-new.md).

## <a name="january-2017"></a>Janeiro de 2017

### <a name="new-capabilities"></a>Novas Funcionalidades

#### <a name="in-console-reports-for-mam-without-enrollment---677961--"></a>Relatórios na consola para MAM sem inscrição  <!--677961-->
Foram adicionados novos relatórios de proteção de aplicações para dispositivos inscritos e não inscritos. Saiba mais sobre como pode monitorizar as políticas de gestão de [aplicações móveis com](../apps/app-protection-policies-monitor.md)o Intune .

#### <a name="android-711-support---694397--"></a>Suporte para Android 7.1.1  <!--694397-->
Agora, o Intune suporta e gere totalmente o Android 7.1.1.

#### <a name="resolve-issue-where-ios-devices-are-inactive-or-the-admin-console-cannot-communicate-with-them---unknown--"></a>Resolver o problema no qual os dispositivos iOS estão inativos ou a consola de administração não consegue comunicar com os mesmos <!--unknown-->
Quando os dispositivos dos utilizadores perdem o contacto com a Intune, pode dar-lhes novas medidas de resolução de problemas para os ajudar a recuperar o acesso aos recursos da empresa. Consulte [Os dispositivos estão inativos ou a consola de administração não consegue comunicar com os mesmos](../enrollment/troubleshoot-device-enrollment-in-intune.md#devices-are-inactive-or-the-admin-console-cant-communicate-with-them).

### <a name="notices"></a>Avisos

#### <a name="defaulting-to-managing-windows-desktop-devices-through-windows-settings---663050--"></a>Utilizar a predefinição para gerir computadores Windows através das definições do Windows <!--663050-->
O comportamento predefinido de inscrição de computadores com Windows 10 irá mudar. As novas inscrições seguirão o fluxo de inscrição do agente MDM normal, em vez de através do agente de PC.

O site do Portal da Empresa irá fornecer aos utilizadores de computadores com Windows 10 instruções para ajudá-los durante o processo de adicionar computadores com Windows 10 como dispositivos móveis. Isto não afetará os PCs atualmente inscritos e a sua organização pode continuar a gerir os computadores com Windows 10 através do agente de PC, [se preferir](manage-windows-pcs-with-microsoft-intune.md).

#### <a name="improving-mobile-app-management-support-for-selective-wipe---581242--"></a>Melhorar o suporte de gestão de aplicações móveis para eliminação seletiva  <!--581242-->
Os utilizadores finais receberão orientações adicionais sobre como recuperar o acesso a dados escolares ou profissionais se esses dados forem automaticamente removidos devido à política "Intervalo offline antes de os dados da aplicação serem apagados".<!--, or the removal of the Intune Company Portal on Android.-->

#### <a name="company-portal-for-ios-links-open-inside-the-app---665954--"></a>As ligações do Portal da Empresa para iOS são abertas dentro da aplicação  <!--665954-->
As ligações na aplicação Portal da Empresa para iOS, incluindo as referentes a documentação e aplicações, serão abertas diretamente na aplicação Portal da Empresa através de uma vista do Safari na aplicação. Esta atualização será fornecida separadamente da atualização do serviço em janeiro.

#### <a name="modernizing-the-company-portal-website---753980--"></a>Modernizar o site do Portal da Empresa  <!--753980-->
A partir de fevereiro, o site do Portal da Empresa irá suportar aplicações visadas para utilizadores que não têm dispositivos geridos. O site será alinhado com outros produtos e serviços Microsoft através de um novo esquema de cores contrastante, ilustrações dinâmicas e um menu de opções, ![Menu de opções do site do Portal da Empresa](./media/whats-new-archive-classic/CP_hamburger_menu.png).

#### <a name="new-documentation-for-app-protection-policies---583398--"></a>Nova documentação para políticas de proteção de aplicações  <!--583398-->
Atualizámos a nossa documentação para administradores e programadores de aplicações que querem ativar políticas de proteção de aplicações (conhecidas como políticas MAM) nas respetivas aplicações iOS e Android através da Ferramenta de Encapsulamento de Aplicações do Intune ou do SDK da Aplicação Intune.

Foram atualizados os seguintes artigos:

* [Decidir como preparar as aplicações para a gestão de aplicações móveis com o Microsoft Intune](../developer/apps-prepare-mobile-application-management.md)
* [Preparar aplicações iOS para gestão de aplicações móveis com a Ferramenta de Encapsulamento de Aplicações num Wrapper do Intune](../developer/app-wrapper-prepare-ios.md)
* [Introdução ao SDK da Aplicação do Microsoft Intune](../developer/app-sdk-get-started.md)
* [Intune App SDK para guia de desenvolvimento iOS](../developer/app-sdk-ios.md)

Os seguintes artigos são novas adições à biblioteca de documentos:

* [Plug-in do Cordova do SDK da Aplicação do Intune](../developer/app-sdk.md)
* [Componente Xamarin do SDK da Aplicação do Intune](../developer/app-sdk-xamarin.md)

#### <a name="progress-bar-when-launching-the-company-portal-on-ios---665978--"></a>Barra de progresso ao iniciar o Portal da Empresa no iOS  <!--665978-->
O Portal da Empresa para iOS passará a apresentar uma barra de progresso no ecrã inicial para fornecer ao utilizador informações sobre os processos de carregamento que ocorrem. É possível que haja uma implementação faseada da barra de progresso para substituir a animação giratória. Isto significa que alguns dos seus utilizadores verão a nova barra de progresso enquanto outros continuarão a ver a animação giratória.

## <a name="december-2016"></a>Dezembro de 2016

### <a name="public-preview-of-intune-in-the-azure-portal--736542--"></a>Pré-visualização pública do Intune no portal do Azure<!--736542-->
No início do ano civil de 2017, estaremos a migrar a nossa experiência de administração completa para o Azure, permitindo uma gestão poderosa e integrada dos fluxos de trabalho em EMS centrais numa plataforma de serviço moderna que é extensível usando APIs gráficos. Antes da disponibilidade geral deste portal para todos os inquilinos do Intune, estamos entusiasmados por anunciar que iremos começar a lançar uma pré-visualização desta nova experiência de administração ainda este mês para selecionar os inquilinos.

A experiência de administração no portal do Azure irá utilizar a já anunciada nova funcionalidade de agrupamento e filtragem; quando o seu inquilino existente é migrado para a nova experiência de agrupamento, o utilizador também será migrado para pré-visualizar a nova experiência de administração do inquilino. Entretanto, pode obter mais informações sobre o que temos reservado para o Microsoft Intune no portal do Azure na nossa [nova documentação](what-is-intune.md).

__Integração de gestão de despesas de telecomunicações na visualização pública do portal Azure__ <!--747605-->
Estamos agora a começar a pré-visualizar a integração com os serviços de gestão de despesas de telecomunicações (TEM) de terceiros no portal do Azure. Pode utilizar o Intune para impor limites de utilização de dados nacionais e itinerantes. Estamos a começar essas integrações com [Saaswedo](http://www.saaswedo.com/). Para ativar esta funcionalidade no seu inquilino de avaliação, [contacte o suporte da Microsoft](get-support.md).

### <a name="new-capabilities"></a>Novas Funcionalidades

__Autenticação de vários fatores em todas as plataformas__ <!--747590-->
Agora pode impor a autenticação multifator (MFA) num grupo selecionado de utilizadores quando estes inscrevem um dispositivo iOS, Android, Windows 8.1+ ou Windows Phone 8.1+ a partir do Portal de Gestão do Azure ao configurar a MFA na aplicação de Inscrição do Microsoft Intune no Azure Active Directory.

__Capacidade para restringir a inscrição de dispositivos móveis__ <!--747596-->
O Intune está a adicionar novas restrições de inscrição que controlam as plataformas de dispositivos móveis autorizadas a inscrever. O Intune separa plataformas de dispositivos móveis como iOS, macOS, Android, Windows e Windows Mobile.
* A restrição da inscrição de dispositivos móveis não restringe a inscrição do cliente de PC.
* Especificamente para iOS, existe uma opção adicional para bloquear a inscrição de dispositivos pessoais.

O Intune marca todos os novos dispositivos como pessoais, a menos que o administrador de TI os marque como pertencentes à empresa, conforme explicado [neste artigo](../enrollment/device-enrollment.md).

### <a name="notices"></a>Avisos

__Autenticação multi-factor na inscrição movendo-se para o portal Azure__ <!--VSO 750545-->
Anteriormente, os administradores utilizariam a consola do Intune ou a consola do Gestor de Configuração (anterior à versão de outubro 2016) para configurar a MFA para inscrições no Intune. Com esta funcionalidade atualizada, irá agora iniciar a sessão no [portal do Microsoft Azure](https://manage.windowsazure.com) com as suas credenciais do Intune e configurar as definições da MFA através do Azure AD. Saiba mais sobre o assunto [aqui](/azure/active-directory/authentication/howto-mfa-mfasettings).

__App Portal da empresa para Android já disponível na China__ <!--VSO 658093-->
Estamos a disponibilizar a aplicação Portal da Empresa para Android para transferência na China.Devido à ausência da Google Play Store na China, os dispositivos Android têm de obter aplicações a partir de mercados de aplicações chineses. A aplicação Portal da Empresa para Android estará disponível para transferência através das seguintes lojas:
* [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
* [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
* [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
* [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

A aplicação Portal da Empresa para Android utiliza os Serviços do Google Play para comunicar com o serviço Microsoft Intune. Uma vez que os Serviços do Google Play ainda não estão disponíveis na China, pode demorar até 8 horas a concluir a realização de qualquer uma das seguintes tarefas.

|Consola de Administração do Intune| Aplicação Portal da Empresa do Intune para Android |Site do Portal da Empresa do Intune|
|---|---|---|
|Eliminação completa| Remover um dispositivo remoto| Remover dispositivo (local e remoto)|
|Eliminação seletiva| Repor dispositivo| Repor dispositivo|
|Implementações de aplicações novas ou atualizadas| Instalar aplicações de linha de negócio disponíveis| Repor código de acesso do dispositivo|
|Bloqueio remoto|||
|Repor código de acesso|||

### <a name="deprecations"></a>Depreciação

__Firefox já não suporta Silverlight__ <!--VSO TBA-->
A Mozilla vai remover o suporte do Silverlight na versão 52 do [browser Firefox](https://www.mozilla.org/firefox), a partir de março de 2017. Como resultado, já não será possível iniciar sessão na consola do Intune existente quando utilizar versões do Firefox superiores a 51. Recomendamos que utilize o Internet Explorer 10 ou 11 para aceder à consola de administração ou uma [versão do Firefox anterior à versão 52](https://ftp.mozilla.org/pub/firefox/releases/). A transição do Intune para o portal do Azure irá permitir suportar um número de [browsers modernos](/azure/azure-preview-portal-supported-browsers-devices) sem dependência do Silverlight.

__Remoção de políticas de caixa de entrada móvel online de intercâmbio__ <!--770687-->
A partir de dezembro, os administradores deixarão de ser capazes de ver ou configurar políticas de caixa de correio móvel do Exchange Online (EAS) na consola do Intune. Esta alteração vai ser implementada em todos os inquilinos do Intune entre dezembro e janeiro. Todas as políticas existentes permanecerão tal como configuradas. Para configurar novas políticas, utilize a Shell de Gestão do Exchange. Saiba mais informações [aqui](https://technet.microsoft.com/library/bb123783%28v=exchg.150%29.aspx).

__As aplicações Intune AV Player, Image Viewer e PDF Viewer já não são suportadas no Android__ <!--747553-->
A partir de meados de dezembro de 2016, os utilizadores já não poderão utilizar as aplicações Leitor do Intune AV, Visualizador de Imagens e Visualizador de PDFs. Estas aplicações foram substituídas pela aplicação Azure Information Protection. Saiba mais sobre a aplicação Azure Information Protection [aqui](/information-protection/rms-client/mobile-app-faq).

## <a name="november-2016"></a>Novembro de 2016

### <a name="new-capabilities"></a>Novas funcionalidades

__Novo Portal da Empresa do Microsoft Intune disponível para dispositivos com o Windows 10__ A Microsoft lançou uma nova [aplicação do Portal da Empresa do Microsoft Intune para dispositivos com o Windows 10](https://www.microsoft.com/store/apps/9wzdncrfj3pz). Esta aplicação, que tira partido do novo formato do Windows 10 Universal, irá oferecer ao utilizador uma experiência atualizada na aplicação e experiências idênticas em todos os dispositivos, PC e dispositivos móveis semelhantes com o Windows 10, permitindo que todos tenham a mesma funcionalidade atual.

A nova aplicação também irá permitir aos utilizadores tirarem partido de funcionalidades de plataforma adicionais, como o início de sessão único (SSO) e a autenticação baseada em certificados em dispositivos com o Windows 10. A aplicação será disponibilizada como uma atualização das instalações existentes do Portal da Empresa do Windows 8.1 e do Portal da Empresa do Windows Phone 8.1 a partir da Loja Microsoft. Para mais detalhes, aceda a [aka.ms/intunecp_universalapp](https://aka.ms/intunecp_universalapp).

> [!IMPORTANT]
> __Uma Atualização no Intune e no Android for Work__ – Embora possa implementar aplicações Android for Work com uma ação de __Obrigatório__, só poderá implementar aplicações como __Disponível__ se os seus grupos do Intune tiverem sido migrados para a nova experiência de grupos do Azure AD.

__Intune App SDK for Cordova plugin agora suporta MAM sem inscrição__ Os desenvolvedores de aplicações podem agora utilizar o Intune App SDK para o Plugin Cordova para permitir a funcionalidade MAM sem a inscrição de dispositivos nas suas aplicações baseadas no Cordova para Android e iOS/iPadOS.

__Intune App SDK Xamarin componente agora suporta MAM sem inscrição__ Os desenvolvedores de aplicações podem agora utilizar o componente Intune App SDK Xamarin para permitir a funcionalidade MAM sem a inscrição de dispositivos nas suas aplicações baseadas em Xamarin para Android e iOS/iPadOS. Pode encontrar o componente Xamarin do SDK da Aplicação do Intune [aqui](https://www.npmjs.com/package/cordova-plugin-ms-intune-mam).

### <a name="notices"></a>Avisos

__O certificado de assinatura Symantec já não precisa do Portal da Empresa do Windows Phone 8 assinado para carregamento__ O carregamento do certificado de assinatura Symantec já não precisa de uma aplicação do Portal da Empresa do Windows Phone 8 assinado. O certificado pode ser carregado de forma independente.

### <a name="deprecations"></a>Depreciação

__Suporte para o Portal da Empresa do Windows Phone 8__ O suporte para o Portal da Empresa do Windows Phone 8 será preterido. O suporte para as plataformas do Windows Phone 8 e do WinRT foi preterido em outubro de 2016. O suporte para o Portal da Empresa do Windows 8 também foi preterido em outubro de 2016.


## <a name="see-also"></a>Consulte também
Veja [o que há de novo no Microsoft Intune](whats-new.md) para mais detalhes sobre os recentes desenvolvimentos.
