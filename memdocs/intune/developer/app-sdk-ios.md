---
title: Guia para programadores do SDK da Aplicação do Microsoft Intune para iOS
description: O SDK da Aplicação do Microsoft Intune para iOS permite-lhe incorporar as políticas de proteção de aplicações do Intune (também conhecidas como políticas de APLICAÇÕES ou MAM) na sua aplicação iOS nativa.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/02/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 8e280d23-2a25-4a84-9bcb-210b30c63c0b
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 379eacee731c8cdd773fc7a15f556ab85e409f7c
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989886"
---
# <a name="microsoft-intune-app-sdk-for-ios-developer-guide"></a>Guia para programadores do SDK da Aplicação do Microsoft Intune para iOS

> [!NOTE]
> Considere ler o artigo [Guia de Introdução ao SDK da Aplicação do Intune](app-sdk-get-started.md), que explica como preparar a integração em cada plataforma suportada.
>
> Para descarregar o SDK, consulte [O download dos ficheiros SDK](../developer/app-sdk-get-started.md#download-the-sdk-files).

O SDK da Aplicação do Microsoft Intune para iOS permite-lhe incorporar as políticas de proteção de aplicações do Intune (também conhecidas como políticas de APLICAÇÕES ou MAM) na sua aplicação iOS nativa. Uma aplicação preparada para MAM é uma integrada com o SDK da Aplicação Intune. Os administradores de TI podem implementar políticas de proteção de aplicações na aplicação móvel quando o Intune está a gerir a aplicação de forma ativa.

## <a name="prerequisites"></a>Pré-requisitos

* Necessitará de um computador Mac OS que execute os OS X 10.8.5 ou mais tarde, e também tenha Xcode 9 ou posteriormente instalado.

* A sua aplicação deve ser direcionada para o iOS 11 ou superior.

* Consulte os [Termos de Licenciamento do SDK da Aplicação do Intune para iOS](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios/blob/master/Microsoft%20License%20Terms%20Intune%20App%20SDK%20for%20iOS.pdf). Imprima e guarde uma cópia dos termos de licenciamento nos seus registos. Ao transferir e utilizar o SDK da Aplicação do Intune para iOS, aceita esses termos de licenciamento.  Caso não aceite os termos, não deverá utilizar o software.

* Descarregue os ficheiros para o Intune App SDK para iOS no [GitHub](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios).

## <a name="whats-in-the-sdk-repository"></a>O que está no Repositório SDK

Os seguintes ficheiros são relevantes para apps/extensões que não contenham código Swift, ou são compilados com uma versão do Xcode antes de 10.2:

* **IntuneMAM.framework**: estrutura do SDK da Aplicação do Intune. Recomenda-se que ligue esta estrutura à sua app/extensões para permitir a gestão da aplicação do cliente Intune. No entanto, alguns desenvolvedores podem preferir os benefícios de desempenho da biblioteca estática. Veja o seguinte.

* **libIntuneMAM.a**: biblioteca estática do SDK da Aplicação do Intune. Os desenvolvedores podem optar por ligar a biblioteca estática em vez da estrutura. Como as bibliotecas estáticas são incorporadas diretamente na app/extensão binária no momento da construção, existem alguns benefícios de desempenho no tempo de lançamento para usar a biblioteca estática. No entanto, integrá-la na sua app é um processo mais complicado. Se a sua aplicação incluir quaisquer extensões, ligar a biblioteca estática à aplicação e extensões resultará num tamanho maior de pacotede aplicações, uma vez que a biblioteca estática será incorporada em cada aplicação/extensão binária. Ao utilizar a estrutura, as aplicações e extensões podem partilhar o mesmo binário Intune SDK, resultando num tamanho menor de aplicações.

* **IntuneMAMResources.bundle**: Um pacote de recursos que contém recursos em que o SDK depende. O pacote de recursos é necessário apenas para apps que integram a biblioteca estática (libIntuneMAM.a).

Os seguintes ficheiros são relevantes para apps/extensões que contenham código Swift, e são compilados com Xcode 10.2+:

* **IntuneMAMSwift.framework**: The Intune App SDK Swift framework. Esta estrutura contém todos os cabeçalhos para APIs que a sua aplicação irá ligar. Ligue esta estrutura à sua app/extensões para permitir a gestão da aplicação do cliente Intune.

* **IntuneMAMSwiftStub.framework**: The Intune App SdK Swift Stub framework. Esta é uma dependência necessária de IntuneMAMSwift.framework que apps/extensões devem ligar.


Os seguintes ficheiros são relevantes para todas as aplicações/extensões:

* **IntuneMAMConfigurator**: Uma ferramenta utilizada para configurar a app ou a lista info.plist da extensão com as alterações mínimas exigidas para a gestão intune. Dependendo da funcionalidade da sua aplicação ou extensão, poderá ter de efetuar alterações manuais adicionais na lista de Info.plist.

* **Cabeçalhos**: Expõe o público Intune App SDK APIs. Estes cabeçalhos estão incluídos nas estruturas IntuneMAM/IntuneMAMSwift, pelo que os desenvolvedores que consomem qualquer uma das estruturas não precisam de adicionar manualmente os cabeçalhos ao seu projeto. Os desenvolvedores que optarem por ligar-se à biblioteca estática (libIntuneMAM.a) terão de incluir manualmente estes cabeçalhos no seu projeto.

Os seguintes ficheiros de cabeçalho incluem as APIs, tipos de dados e protocolos que o SDK da Aplicação Intune disponibiliza aos programadores:

-  IntuneMAMAppConfig.h
-  IntuneMAMAppConfigManager.h
-  IntuneMAMDataProtectionInfo.h
-  IntuneMAMDataProtectionManager.h
-  IntuneMAMDefs.h
-  IntuneMAMDiagnosticConsole.h
-  IntuneMAMEnrollmentDelegate.h
-  IntuneMAMEnrollmentManager.h
-  IntuneMAMEnrollmentStatus.h
-  IntuneMAMFileProtectionInfo.h
-  IntuneMAMFileProtectionManager.h
-  IntuneMAMLogger.h
-  IntuneMAMPolicy.h
-  IntuneMAMPolicyDelegate.h
-  IntuneMAMPolicyManager.h
-  IntuneMAMVersionInfo.h

Os desenvolvedores podem disponibilizar o conteúdo de todos os cabeçalhos anteriores, importando apenas intuneMAM.h


## <a name="how-the-intune-app-sdk-works"></a>Como funciona o SDK da Aplicação Intune

O objetivo do SDK da Aplicação do Intune para iOS consiste em adicionar capacidades de gestão para aplicações iOS com alterações de código mínimas. Quanto menos o código mudar, menos tempo para o mercado, mas sem afetar a consistência e estabilidade da sua aplicação móvel.


## <a name="build-the-sdk-into-your-mobile-app"></a>Criar o SDK na sua aplicação móvel

Para ativar o SDK da Aplicação Intune, siga estes passos:

1. **Opção 1 - Quadro (recomendado)**: Se estiver a utilizar o Xcode 10.2+ e a sua aplicação/extensão contiver código Swift, link `IntuneMAMSwift.framework` e ao seu `IntuneMAMSwiftStub.framework` alvo: Arraste `IntuneMAMSwift.framework` e para a lista de `IntuneMAMSwiftStub.framework` **Binários Incorporados** do alvo do projeto.

    Caso contrário, `IntuneMAM.framework` ligue-se ao seu alvo: Arraste `IntuneMAM.framework` para a lista de **Binários Incorporados** do alvo do projeto.

   > [!NOTE]
   > Se utilizar a estrutura, terá de retirar manualmente as arquiteturas do simulador da estrutura universal antes de submeter a sua aplicação na App Store. Veja [Enviar a aplicação à App Store](#submit-your-app-to-the-app-store) para obter mais detalhes.

   **Opção 2 - Biblioteca Estática**: Esta opção só está disponível para apps/extensões que não contenham código Swift, ou foram construídas com Xcode < 10.2. Ligação para a `libIntuneMAM.a` biblioteca. Arraste a biblioteca `libIntuneMAM.a` para a lista **Estruturas e Bibliotecas Ligadas** do destino do projeto.

    ![SDK da Aplicação do Intune para iOS: estruturas e bibliotecas ligadas](./media/app-sdk-ios/intune-app-sdk-ios-linked-frameworks-and-libraries.png)

    Adicione `-force_load {PATH_TO_LIB}/libIntuneMAM.a` a qualquer um dos seguintes, substituindo `{PATH_TO_LIB}` pela localização do SDK da Aplicação do Intune:
   * A configuração de configuração de construção do `OTHER_LDFLAGS` projeto.
   * As **Outras Bandeiras**de Linker do Xcode UI.

     > [!NOTE]
     > Para localizar `PATH_TO_LIB`, selecione o ficheiro `libIntuneMAM.a` e escolha **Informações** a partir do menu **Ficheiro**. Copiar e colar a informação **Onde** (o caminho) da secção **geral** da janela **Info.**

     Adicione o pacote de recursos `IntuneMAMResources.bundle` ao projeto, ao arrastar o pacote de recursos em **Copiar Recursos do Pacote** em **Fases de Criação**.

     ![SDK da Aplicação do Intune para iOS: copiar recursos do pacote](./media/app-sdk-ios/intune-app-sdk-ios-copy-bundle-resources.png)
         
2. Adicione estas estruturas de iOS ao projeto:  
-  MessageUI.framework  
-  Security.framework  
-  CoreServices.framework  
-  SystemConfiguration.framework  
-  libsqlite3.tbd  
-  libc++.tbd  
-  ImageIO.framework  
-  LocalAuthentication.framework  
-  AudioToolbox.framework  
-  QuartzCore.framework  
-  WebKit.framework

3. Ative a partilha de keychain (se não estiver já ativada) ao selecionar **Capacidades** no destino de cada projeto e ao ativar o comutador **Partilha de Keychain**. A partilha de keychain é necessária para avançar para o passo seguinte.

   > [!NOTE]
   > O perfil de aprovisionamento tem de suportar os novos valores de partilha de keychain. Os grupos de acesso de keychain devem suportar um caráter universal. Pode verificar isso abrindo o ficheiro .mobileprovision num editor de texto, procurando por **grupos de acesso**à cadeia de chaves, e garantindo que tem um personagem wildcard. Por exemplo:
   >
   >  ```xml
   >  <key>keychain-access-groups</key>
   >  <array>
   >  <string>YOURBUNDLESEEDID.*</string>
   >  </array>
   >  ```

4. Depois de permitir a partilha de porta-chaves, siga os passos para criar um grupo de acesso separado no qual o Intune App SDK armazenará os seus dados. Pode criar um grupo de acesso de keychain com a IU ou o ficheiro de elegibilidade. Se estiver a utilizar a UI para criar o grupo de acesso à porta-chaves, certifique-se de seguir estes passos:

     a. Se a sua aplicação móvel não tiver quaisquer grupos de acesso ao keychain definidos, adicione o ID da aplicação como o **primeiro** grupo.
    
    b. Adicione o grupo de keychain partilhado `com.microsoft.intune.mam` aos seus grupos de acesso existentes. O SDK da Aplicação do Intune utiliza este grupo de acesso para armazenar dados.
    
    c. Adicione `com.microsoft.adalcache` aos seus grupos de acesso existentes.
    
      ![SDK da Aplicação do Intune para iOS: partilha de keychain](./media/app-sdk-ios/intune-app-sdk-ios-keychain-sharing.png)
    
    d. Se estiver a editar diretamente o ficheiro de elegibilidade, em vez de utilizar a IU do Xcode mostrada acima para criar grupos de acesso de keychain, inclua o acesso de keychain no início com `$(AppIdentifierPrefix)` (o Xcode processa o ficheiro automaticamente). Por exemplo:
    
      - `$(AppIdentifierPrefix)com.microsoft.intune.mam`
      - `$(AppIdentifierPrefix)com.microsoft.adalcache`
    
      > [!NOTE]
      > Um ficheiro de elegibilidade é um ficheiro XML exclusivo para a sua aplicação móvel. Serve para especificar permissões e capacidades especiais na aplicação iOS. Se a aplicação não tinha anteriormente nenhum ficheiro de elegibilidade, a ativação da partilha de keychain (passo 3) deverá levar à geração de um ficheiro de elegibilidade pelo Xcode para a aplicação. Certifique-se de que o pacote de identificação da aplicação é a primeira entrada na lista.

5. Inclua cada protocolo transmitido pela aplicação a `UIApplication canOpenURL` na matriz `LSApplicationQueriesSchemes` do ficheiro Info.plist da aplicação. Não se esqueça de guardar as alterações antes de prosseguir para o passo seguinte.

6. Se a sua aplicação ainda não utilizar o FaceID, garanta que a [chave Info.plist NSFaceIDUsageDescription](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW75) está configurada com uma mensagem predefinida. Isto é necessário para que o iOS possa informar o utilizador sobre como é que a aplicação pretende utilizar o FaceID. Uma definição de política de proteção de aplicações do Intune permite que o FaceID seja utilizado como um método para aceder a aplicações quando configurado pelo administrador de TI.

7. Utilize a ferramenta IntuneMAMConfigurator, incluída no [repositório do SDK](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios), para concluir a configuração do ficheiro Info.plist da aplicação. A ferramenta tem três parâmetros:

   |Propriedade|Como utilizá-lo|
   |---------------|--------------------------------|
   |- i |  `<Path to the input plist>` |
   |- e | `<Path to the entitlements file>` |
   |- o |  (Opcional)`<Path to the output plist>` |

Se o parâmetro “-o” não for especificado, o ficheiro de entrada será modificado no local. A ferramenta é idempotent e deve ser executada novamente sempre que forem feitas alterações ao ficheiro Info.plist da aplicações ou tenham sido criadas elegibilidades. Deverá também transferir e executar a versão mais recente da ferramenta ao atualizar o SDK do Intune, caso os requisitos de configuração do ficheiro Info.plist tenham sido alterados na versão mais recente.

## <a name="configure-adalmsal"></a>Configurar ADAL/MSAL

O Intune App SDK pode utilizar a Biblioteca de [Autenticação de DirectórioActivo Azure](https://github.com/AzureAD/azure-activedirectory-library-for-objc) ou a Biblioteca de [Autenticação](https://github.com/AzureAD/microsoft-authentication-library-for-objc) da Microsoft para a sua autenticação e cenários de lançamento condicional. Conta ainda com a ADAL/MSAL para registar a identidade do utilizador junto do serviço MAM para gestão sem cenários de inscrição de dispositivos.

Normalmente, a ADAL/MSAL exige que as aplicações se registem com o Azure Ative Directory (AAD) e criem um ID exclusivo do cliente e redirecionem o URI, para garantir a segurança dos tokens concedidos à app. Se a sua aplicação já utilizar a ADAL ou a MSAL para autenticar os utilizadores, a aplicação deve utilizar os valores de registo existentes e anular os valores predefinidos intune App SDK. Isto garante que os utilizadores não recebem um pedido de autenticação duas vezes (uma vez pelo SDK da Aplicação Intune e uma vez pela aplicação).

Se a sua aplicação ainda não utilizar a ADAL ou a MSAL, e não precisar de aceder a qualquer recurso AAD, não precisa de configurar um registo de aplicações de clientes em AAD se optar por integrar a ADAL. Se decidir integrar o MSAL, terá de configurar um registo de aplicações e anular o ID do cliente intune padrão e redirecionar o URI.  

Recomenda-se que a sua aplicação se ligue ao mais recente lançamento da [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-objc/releases) ou [da MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-objc/releases).

### <a name="link-to-adal-or-msal-binaries"></a>Ligação aos binários ADAL ou MSAL

**Opção 1 -** Siga [estes passos](https://github.com/AzureAD/azure-activedirectory-library-for-objc#download) para ligar a sua aplicação aos binários ADAL.

**Opção 2 -** Em alternativa, pode seguir [estas instruções](https://github.com/AzureAD/microsoft-authentication-library-for-objc#installation) para ligar a sua aplicação aos binários MSAL.

1. Se a sua aplicação não tiver quaisquer grupos de acesso ao keychain definidos, adicione o ID da aplicação como o primeiro grupo.

2. Ativar o sinal único ADAL/MSAL (SSO) adicionando aos grupos de `com.microsoft.adalcache` acesso à porta-chaves.

3. Caso esteja explicitamente a definir o grupo de keychain da cache partilhada da ADAL, certifique-se de que está definido como `<appidprefix>.com.microsoft.adalcache`. A ADAL define isto automaticamente, a menos que efetue uma substituição. Se quiser especificar um grupo de keychain personalizado para substituir o `com.microsoft.adalcache`, especifique-o no ficheiro Info.plist, em IntuneMAMSettings, com a chave `ADALCacheKeychainGroupOverride`.

### <a name="configure-adalmsal-settings-for-the-intune-app-sdk"></a>Configure as definições ADAL/MSAL para o Intune App SDK

Se a sua aplicação já utilizar a ADAL ou a MSAL para autenticação e tiver as suas próprias definições de Diretório Ativo Azure, pode forçar o Intune App SDK a utilizar as mesmas definições durante a autenticação contra a AAD. Esta ação garante que a aplicação não solicita a autenticação ao utilizador duas vezes. Veja [Configurar as definições para o SDK da Aplicação do Intune](#configure-settings-for-the-intune-app-sdk) para obter mais informações sobre o preenchimento das seguintes informações:  

* ADALClientId
* ADALAuthority
* ADALRedirectUri
* ADALRedirectScheme
* ADALCacheKeychainGroupOverride

Se a sua aplicação já utilizar a ADAL ou a MSAL, são necessárias as seguintes configurações:

1. No ficheiro Info.plist do projeto, no dicionário **IntuneMAMSettings** com o nome `ADALClientId` chave, especifique o ID do cliente a ser utilizado para chamadas ADAL.

2. Também no dicionário **IntuneMAMSettings** com o nome de chave `ADALAuthority`, especifique a autoridade do Azure AD.

3. Também no dicionário **IntuneMAMSettings** com o nome de chave `ADALRedirectUri`, especifique o URI de redirecionamento a utilizar nas chamadas da ADAL. Em alternativa, pode especificar `ADALRedirectScheme` se o URI de redirecionamento da aplicação estiver no formato `scheme://bundle_id`.

Além disso, as aplicações podem substituir estas definições do Azure AD no runtime. Para tal, basta definir as propriedades `aadAuthorityUriOverride`, `aadClientIdOverride` e `aadRedirectUriOverride` na instância `IntuneMAMPolicyManager`.

4. Certifique-se de que são seguidas as medidas para dar permissões à sua aplicação iOS para o serviço de política de proteção de aplicações (APP). Utilize as instruções no [início com o guia Intune SDK](app-sdk-get-started.md#next-steps-after-integration) em " Dar à sua aplicação acesso ao serviço de proteção de[aplicações Intune (opcional)](app-sdk-get-started.md#give-your-app-access-to-the-intune-app-protection-service-optional)".  

> [!NOTE]
> Para todas as definições que são estáticas e que não precisam de ser determinadas no runtime, recomenda-se a abordagem do ficheiro Info.plist. Os valores atribuídos às propriedades `IntuneMAMPolicyManager` têm precedência sobre quaisquer valores correspondentes especificados no ficheiro Info.plist e serão mantidos, mesmo depois de a aplicação ser reiniciada. O SDK continuará a utilizá-los para os registos da política até que a inscrição do utilizador seja anulada ou os valores sejam limpos ou alterados.

### <a name="if-your-app-does-not-use-adal-or-msal"></a>Se a sua aplicação não utilizar a ADAL ou a MSAL

Como mencionado anteriormente, o Intune App SDK pode utilizar a Biblioteca de [Autenticação de DirectórioActivo Azure](https://github.com/AzureAD/azure-activedirectory-library-for-objc) ou a Biblioteca de [Autenticação](https://github.com/AzureAD/microsoft-authentication-library-for-objc) da Microsoft para a sua autenticação e cenários de lançamento condicional. Conta ainda com a ADAL/MSAL para registar a identidade do utilizador junto do serviço MAM para gestão sem cenários de inscrição de dispositivos. Se **a sua aplicação não utilizar a ADAL ou a MSAL para o seu próprio mecanismo de autenticação,** então poderá ter de configurar as definições aAD personalizadas, dependendo da biblioteca de autenticação que escolher integrar:   

ADAL - Intune App SDK fornecerá valores predefinidos para parâmetros ADAL e manuseie a autenticação contra a AD Azure. Os desenvolvedores não precisam de especificar quaisquer valores para as definições ADAL anteriormente mencionadas. 

MSAL - Os desenvolvedores precisam criar um registo de aplicação em AAD com um URI de redirecionamento personalizado no formato [aqui](https://github.com/AzureAD/microsoft-authentication-library-for-objc/wiki/Migrating-from-ADAL-Objective-C-to-MSAL-Objective-C#app-registration-migration)especificado . Os desenvolvedores devem definir as `ADALClientID` definições e `ADALRedirectUri` configurações anteriormente mencionadas, ou o equivalente `aadClientIdOverride` e propriedades na `aadRedirectUriOverride` `IntuneMAMPolicyManager` instância. Os desenvolvedores também devem garantir que seguem o passo 4 na secção anterior, para dar à sua app acesso ao serviço de proteção de aplicações Intune.

### <a name="special-considerations-when-using-msal"></a>Considerações especiais ao utilizar o MSAL 

1. **Consulte o seu Webview** - Recomenda-se que as aplicações não utilizem o SFSafariViewController, O SFAuthSession ou o ASWebAuthSession como o seu webview para quaisquer operações interativas de Auth MSAL iniciadas por aplicações. Se, por alguma razão, a sua aplicação tiver de utilizar uma destas webviews para quaisquer operações interativas de auth MSAL, então também deve ser definida `SafariViewControllerBlockedOverride` sob o dicionário na lista `true` `IntuneMAMSettings` info.plist da aplicação. AVISO: Isto desligará os ganchos SafariViewController da Intune para ativar a sessão de auth. Isto arrisca fugas de dados em outros lugares da aplicação se a aplicação usar o SafariViewController para visualizar dados corporativos, pelo que a aplicação não deve apresentar dados corporativos em nenhum desses tipos de webview.
2. **Ligando tanto a ADAL como a MSAL** - Os desenvolvedores devem optar se quiserem que a Intune prefira a MSAL em vez da ADAL neste cenário. Por padrão, a Intune prefere versões ADAL suportadas a versões MSAL suportadas, se ambas estiverem ligadas no prazo de execução. Intune só prefere uma versão MSAL suportada quando, no momento da primeira operação de autenticação de Intune, `IntuneMAMUseMSALOnNextLaunch` estiver `true` em `NSUserDefaults` . Se `IntuneMAMUseMSALOnNextLaunch` estiver ou não `false` definido, Intune recue para o comportamento padrão. Como o nome sugere, uma mudança `IntuneMAMUseMSALOnNextLaunch` entrará em vigor no próximo lançamento.


## <a name="configure-settings-for-the-intune-app-sdk"></a>Configurar as definições para o SDK da Aplicação do Intune

Pode utilizar o dicionário **IntuneMAMSettings** no ficheiro Info.plist da aplicação para configurar e configurar o Intune App SDK. Se o dicionário IntuneMAMSettings não estiver no ficheiro Info.plist, deverá criá-lo.

No dicionário IntuneMAMSettings, pode adicionar as seguintes definições suportadas para configurar o SDK da Aplicação do Intune.

Algumas destas definições podem ter sido abordadas nas secções anteriores e outras não são aplicáveis a todas as aplicações.

Definição  | Tipo  | Definição | Necessário?
--       |  --   |   --       |  --
ADALClientId  | Cadeia  | O identificador de cliente Azure AD da aplicação. | Necessária para todas as aplicações que utilizem MSAL e qualquer aplicação ADAL que aceda a um recurso AAD não intune. |
ADALAuthority | Cadeia | Autoridade do Azure AD da aplicação em utilização. Deve utilizar o seu ambiente onde foram configuradas contas do AAD. | Opcional. Recomendado se a aplicação for uma aplicação personalizada de linha de negócio saqueada para uso dentro de uma única organização/inquilino AAD. Se este valor estiver ausente, a autoridade adi comum é utilizada.|
ADALRedirectUri  | Cadeia  | O redirecionamento do Azure AD da aplicação URI. | AADALRedirectUri ou ADALRedirectScheme é necessária para todas as aplicações que utilizem MSAL e qualquer aplicação ADAL que aceda a um recurso AAD não intune.  |
ADALRedirectScheme  | Cadeia  | O esquema de redirecionamento do Azure AD da aplicação. Pode ser utilizado em vez do ADALRedirectUri se o URI de redirecionamento da aplicação estiver no formato `scheme://bundle_id`. | AADALRedirectUri ou ADALRedirectScheme é necessária para todas as aplicações que utilizem MSAL e qualquer aplicação ADAL que aceda a um recurso AAD não intune. |
ADALLogOverrideDisabled | Booleano  | Especifica se o SDK irá encaminhar todos os registos ADAL/MSAL (incluindo chamadas ADAL da app, se houver) para o seu próprio ficheiro de registo. Assume a predefinição de NO. Configurar para SIM se a aplicação definir o seu próprio log callback ADAL/MSAL. | Opcional. |
ADALCacheKeychainGroupOverride | Cadeia  | Especifica o grupo de porta-chaves a utilizar para a cache ADAL/MSAL, em vez de "com.microsoft.adalcache". Note que isto não tem o prefixo de id da aplicação. Será adicionado como prefixo à cadeia fornecida no tempo de execução. | Opcional. |
AppGroupIdentifiers | Conjunto de cordas  | Conjunto de grupos de aplicações da secção de direitos da aplicação com.apple.security.application-groups. | Necessário se a aplicação utilizar grupos de aplicações. |
ContainingAppBundleId | Cadeia | Especifica a identificação do pacote da aplicação contendo da extensão. | Necessário para as extensões de iOS. |
DebugSettingsEnabled| Booleano | Se for definido como YES, as políticas de teste no pacote de Definições podem ser aplicadas. As aplicações *não* devem ser fornecidas com esta definição ativada. | Opcional. Assume a predefinição de NO. |
AutoEnrollOnLaunch| Booleano| Especifica se a aplicação deve tentar inscrever-se automaticamente quando inicia se for detetada uma identidade gerida existente e ainda não o tiver feito. Assume a predefinição de NO. <br><br> Notas: Se não for encontrada nenhuma identidade gerida ou se não for disponível um símbolo válido para a identidade no cache ADAL/MSAL, a tentativa de inscrição falhará silenciosamente sem solicitar credenciais, a menos que a aplicação também tenha definido MAMPolicyRequired para YES. | Opcional. Assume a predefinição de NO. |
MAMPolicyRequired| Booleano| Especifica se a aplicação será impedida de iniciar se não tiver uma política de proteção de aplicação do Intune. Assume a predefinição de NO. <br><br> Notas: as aplicações não podem ser submetidas à App Store com a MAMPolicyRequired definida como YES. Ao definir a MAMPolicyRequired como YES, a AutoEnrollOnLaunch também deve ser definida como YES. | Opcional. Assume a predefinição de NO. |
MAMPolicyWarnAbsent | Booleano| Especifica se a aplicação irá avisar o utilizador ao iniciar se a aplicação não tiver uma política de proteção de aplicação do Intune. <br><br> Nota: os utilizadores ainda poderão utilizar a aplicação sem a política após ignorarem o aviso. | Opcional. Assume a predefinição de NO. |
MultiIdentity | Booleano| Especifica se a aplicação tem conhecimento de identidades múltiplas. | Opcional. Assume a predefinição de NO. |
SafariViewControllerBlockedOverride | Booleano| Desativa os ganchos SafariViewController da Intune para ativar o AUTH MSAL via SFSafariViewController, SFAuthSession ou ASWebAuthSession. | Opcional. Assume a predefinição de NO. AVISO: pode resultar em fugas de dados se for utilizado de forma inadequada. Permitir apenas se for absolutamente necessário. Consulte [considerações especiais ao utilizar o MSAL](#special-considerations-when-using-msal) para obter mais detalhes.  |
SplashIconFile <br>SplashIconFile~ipad | Cadeia  | Especifica o ficheiro de ícone de ecrã inicial (arranque) do Intune. | Opcional. |
SplashDuration | Número | Quantidade mínima de tempo, em segundos, durante a qual será mostrado o ecrã de arranque do Intune na iniciação da aplicação. Assume a predefinição de 1,5. | Opcional. |
BackgroundColor| Cadeia| Especifica a cor de fundo para os componentes ui do Intune SDK. Aceita uma cadeia RGB hexadecimal sob a forma de "#XXXXXX", sendo que X pode ir de 0 a 9 ou de A a F. O sinal de cardinal pode ser omitido.   | Opcional. Predefinições da cor de fundo do sistema, que podem variar entre versões do iOS e de acordo com a definição do modo escuro do iOS. |
ForegroundColor| Cadeia| Especifica a cor do primeiro plano para os componentes UI do Intune SDK, como a cor do texto. Aceita uma cadeia RGB hexadecimal sob a forma de "#XXXXXX", sendo que X pode ir de 0 a 9 ou de A a F. O sinal de cardinal pode ser omitido.  | Opcional. Predefinições da cor da etiqueta do sistema, que podem variar entre versões do iOS e de acordo com a definição do modo escuro do iOS. |
AccentColor | Cadeia| Especifica a cor do sotaque para os componentes UI do Intune SDK, tais como a cor do texto do botão e a cor de destaque da caixa PIN. Aceita uma cadeia RGB hexadecimal sob a forma de "#XXXXXX", sendo que X pode ir de 0 a 9 ou de A a F. O sinal de cardinal pode ser omitido.| Opcional. Assume a predefinição de azul de sistema. |
Coloração Secundária de Fundo| Cadeia| Especifica a cor de fundo secundária para os ecrãs MTD. Aceita uma cadeia RGB hexadecimal sob a forma de "#XXXXXX", sendo que X pode ir de 0 a 9 ou de A a F. O sinal de cardinal pode ser omitido.   | Opcional. Incumprimentos para branco. |
Coloração Secundária Foreground| Cadeia| Especifica a cor do primeiro plano secundário para os ecrãs MTD, como a cor da nota de rodapé. Aceita uma cadeia RGB hexadecimal sob a forma de "#XXXXXX", sendo que X pode ir de 0 a 9 ou de A a F. O sinal de cardinal pode ser omitido.  | Opcional. Incumprimentos a cinza. |
SuportesDarkMode| Booleano | Especifica se o esquema de cores UI intune sDK deve observar a definição do modo escuro do sistema, se não tiver sido definido nenhum valor explícito para BackgroundColor/ForegroundColor/AccentColor | Opcional. Incumprimentos a sim. |
MAMTelemetryDisabled| Booleano| Especifica se o SDK não envia dados de telemetria de volta para o respetivo back-end.| Opcional. Assume a predefinição de NO. |
MAMTelemetryUsePPE | Booleano | Especifica se o SDK de MAM envia dados para o back-end de telemetria do PPE. Utilize esta opção ao testar as suas aplicações com a política do Intune, para que os dados de telemetria de teste não se misturem com os dados de clientes. | Opcional. Assume a predefinição de NO. |
MaxFileProtectionLevel | Cadeia | Opcional. Permite que a aplicação especifique o `NSFileProtectionType` máximo que pode suportar. Este valor irá substituir a política enviada pelo serviço se o nível for superior ao que a aplicação consegue suportar. Valores possíveis: `NSFileProtectionComplete`, `NSFileProtectionCompleteUnlessOpen`, `NSFileProtectionCompleteUntilFirstUserAuthentication`, `NSFileProtectionNone`.|
OpenInActionExtension | Booleano | Defina como YES para extensões de Ação Abrir em. Veja a secção Partilhar dados através de UIActivityViewController para obter mais informações. |
WebViewHandledURLSchemes | Matriz de Cadeias | Especifica os esquemas de URL processados pela WebView da sua aplicação. | Necessário se a sua aplicação utilizar uma WebView que processa URLs através de ligações e/ou javascript. |
DocumentbrowserFileCachePath | Cadeia | Se a sua aplicação utilizar a aplicação para navegar através de [`UIDocumentBrowserViewController`](https://developer.apple.com/documentation/uikit/uidocumentbrowserviewcontroller?language=objc) ficheiros em vários fornecedores de ficheiros, pode definir este caminho em relação ao diretório inicial na caixa de areia da aplicação para que o Intune SDK possa deixar cair ficheiros geridos desencriptados nessa pasta. | Opcional. Incumprimentos no `/Documents/` diretório. |
VerboseLoggingEnabled | Booleano | Se definido para SIM, Intune iniciará o seu login no modo verbose. | Opcional. Incumprimentos a NO |

## <a name="receive-app-protection-policy"></a>Receber a política de proteção de aplicações

### <a name="overview"></a>Descrição geral

Para receber a política de proteção de aplicações do Intune, as aplicações têm de iniciar um pedido de inscrição com o serviço MAM do Intune. As aplicações podem ser configuradas na consola do Intune para obterem a política de proteção de aplicações, com ou sem a inscrição de dispositivos. A política de proteção de aplicações sem a inscrição de dispositivos, também conhecida como **APP-WE** ou MAM-WE, permite que as aplicações sejam geridas pelo Intune sem a necessidade de o dispositivo ser inscrito na gestão de dispositivos móveis (MDM) do Intune. Em ambos os casos, precisa da inscrição com o serviço MAM do Intune para receber a política.

> [!Important]
> O Intune App SDK para iOS utiliza chaves de encriptação de 256 bits quando a encriptação é ativada por Políticas de Proteção de Aplicações. Todas as aplicações terão de ter uma versão SDK atual para permitir a partilha de dados protegidos.

### <a name="apps-that-already-use-adal-or-msal"></a>Aplicativos que já usam ADAL ou MSAL

As aplicações que já utilizam a ADAL ou a MSAL devem ligar para o `registerAndEnrollAccount` método na ocorrência depois de o utilizador ter sido `IntuneMAMEnrollmentManager` autenticado com sucesso:

```objc
/*
 *  This method will add the account to the list of registered accounts.
 *  An enrollment request will immediately be started.
 *  @param identity The UPN of the account to be registered with the SDK
 */

(void)registerAndEnrollAccount:(NSString *)identity;
```

Ao chamar o método `registerAndEnrollAccount`, o SDK irá registar a conta de utilizador e tentar inscrever a aplicação em nome desta conta. Se a inscrição falhar por algum motivo, o SDK irá automaticamente voltar a tentar a inscrição após 24 horas. Para fins de depuração, a aplicação pode receber [notificações](#status-result-and-debug-notifications), através de um delegado, sobre os resultados de pedidos de inscrição.

Depois de esta API ser invocada, a aplicação pode continuar a funcionar normalmente. Se a inscrição for bem-sucedida, o SDK irá informar o utilizador de que é preciso reiniciar a aplicação. Nessa altura, o utilizador pode reiniciar a aplicação imediatamente.

```objc
[[IntuneMAMEnrollmentManager instance] registerAndEnrollAccount:@"user@foo.com"];
```

### <a name="apps-that-do-not-use-adal-or-msal"></a>Aplicativos que não usam ADAL ou MSAL

As aplicações que não assinem no utilizador utilizando a ADAL ou a MSAL ainda podem receber a política de proteção de aplicações do serviço Intune MAM, ligando para a API para ter o sdk a cabo dessa autenticação. As aplicações devem utilizar esta técnica quando não tiverem autenticado um utilizador com o Azure AD, mas ainda precisam de obter a política de proteção de aplicações para ajudar a proteger dados. A título de exemplo, quando outro serviço de autenticação está a ser utilizado para início de sessão na aplicação ou a aplicação não suporta o início sessão em nenhuma situação. Para tal, a aplicação pode chamar o método `loginAndEnrollAccount` na instância `IntuneMAMEnrollmentManager`:

```objc
/**
 *  Creates an enrollment request which is started immediately.
 *  If no token can be retrieved for the identity, the user will be prompted
 *  to enter their credentials, after which enrollment will be retried.
 *  @param identity The UPN of the account to be logged in and enrolled.
 */
 (void)loginAndEnrollAccount: (NSString *)identity;
```

Ao chamar este método, o SDK pedirá ao utilizador as credenciais se não encontrar nenhum token. O SDK tentará, em seguida, inscrever a aplicação com o serviço MAM do Intune em nome da conta do utilizador indicada. O método pode ser chamado com "nil" como identidade. Neste caso, o SDK será inscrito com o utilizador gerido existente no dispositivo (no caso da MDM) ou solicitará um nome de utilizador ao utilizador, se não for encontrado um utilizador existente.

Se a inscrição falhar, a aplicação deverá considerar chamar esta API novamente numa altura posterior, consoante os detalhes da falha. A aplicação pode receber [notificações](#status-result-and-debug-notifications), através de um delegado, sobre os resultados de pedidos de inscrição.

Depois de esta API ser invocada, a aplicação poderá continuar a funcionar normalmente. Se a inscrição for bem-sucedida, o SDK irá informar o utilizador de que é preciso reiniciar a aplicação.

Exemplo:

```objc
[[IntuneMAMEnrollmentManager instance] loginAndEnrollAccount:@"user@foo.com"];
```

### <a name="let-intune-handle-authentication-and-enrollment-at-launch"></a>Permitir que o Intune processe a autenticação e a inscrição na iniciação

Se quiser que o Intune SDK manuseie toda a autenticação utilizando a ADAL/MSAL e a inscrição antes do lançamento da sua aplicação, e a sua aplicação requer sempre a política de APP, não precisa de usar `loginAndEnrollAccount` API. Pode simplesmente configurar as duas definições abaixo como YES no dicionário IntuneMAMSettings no ficheiro Info.plist.

Definição  | Tipo  | Definição |
--       |  --   |   --       |  
AutoEnrollOnLaunch| Booleano| Especifica se a aplicação deve tentar inscrever-se automaticamente quando inicia se for detetada uma identidade gerida existente e ainda não o tiver feito. Assume a predefinição de NO. <br><br> Nota: Se não for encontrada nenhuma identidade gerida ou se não houver um símbolo válido para a identidade disponível na cache ADAL/MSAL, a tentativa de inscrição falhará silenciosamente sem solicitar credenciais, a menos que a aplicação também tenha definido MAMPolicyRequired para YES. |
MAMPolicyRequired| Booleano| Especifica se a aplicação será impedida de iniciar se não tiver uma política de proteção de aplicação do Intune. Assume a predefinição de NO. <br><br> Nota: as aplicações não podem ser submetidas à App Store com a MAMPolicyRequired definida como YES. Ao definir a MAMPolicyRequired como YES, a AutoEnrollOnLaunch também deve ser definida como YES. |

Se escolher esta opção para a sua aplicação, não tem de processar o reinício da sua aplicação após a inscrição.

### <a name="deregister-user-accounts"></a>Anular o registo de contas de utilizadores

Para que a sessão de um utilizador numa aplicação seja terminada, a aplicação deverá anular o registo do utilizador a partir do SDK. Isto garante que:

1. As repetições de inscrição deixarão de acontecer para a conta do utilizador.

2. A política de proteção de aplicações será removida.

3. Se a aplicação iniciar uma eliminação seletiva (opcional), todos os dados empresariais serão eliminados.

Antes de o utilizador terminar a sessão, a aplicação deve chamar o seguinte método na instância `IntuneMAMEnrollmentManager`:

```objc
/*
 *  This method will remove the provided account from the list of
 *  registered accounts.  Once removed, if the account has enrolled
 *  the application, the account will be un-enrolled.
 *  @note In the case where an un-enroll is required, this method will block
 *  until the Intune APP AAD token is acquired, then return.  This method must be called before  
 *  the user is removed from the application (so that required AAD tokens are not purged
 *  before this method is called).
 *  @param identity The UPN of the account to be removed.
 *  @param doWipe   If YES, a selective wipe if the account is un-enrolled
 */
(void)deRegisterAndUnenrollAccount:(NSString *)identity withWipe:(BOOL)doWipe;
```

Este método deve ser chamado antes de serem suprimidas as fichas adatos da conta de utilizador. O SDK necessita do token(s) da conta de utilizador para fazer pedidos específicos ao serviço Intune MAM em nome do utilizador.

Se a aplicação eliminar os dados corporativos do utilizador por si só, a `doWipe` bandeira pode ser configurada como falsa. Caso contrário, a aplicação pode indicar ao SDK para iniciar uma eliminação seletiva. Isto resultará numa chamada para o delegado de eliminação seletiva da aplicação.

Exemplo:

```objc
[[IntuneMAMEnrollmentManager instance] deRegisterAndUnenrollAccount:@"user@foo.com" withWipe:YES];
```

## <a name="status-result-and-debug-notifications"></a>Notificações de estado, de resultado e de depuração

A aplicação pode receber notificações de estado, de resultado e de depuração relativas aos seguintes pedidos ao serviço MAM do Intune:

* Pedidos de inscrição
* Pedidos de atualização da política
* Pedidos de anulação de inscrição

As notificações são apresentadas através de métodos de delegado no `IntuneMAMEnrollmentDelegate.h`:

```objc
/**
 *  Called when an enrollment request operation is completed.
 * @param status status object containing debug information
 */

(void)enrollmentRequestWithStatus:(IntuneMAMEnrollmentStatus *)status;

/**
 *  Called when a MAM policy request operation is completed.
 *  @param status status object containing debug information
 */
(void)policyRequestWithStatus:(IntuneMAMEnrollmentStatus *)status;

/**
 *  Called when a un-enroll request operation is completed.
 *  @Note: when a user is un-enrolled, the user is also de-registered with the SDK
 *  @param status status object containing debug information
 */

(void)unenrollRequestWithStatus:(IntuneMAMEnrollmentStatus *)status;
```

Estes métodos delegados devolvem um objeto `IntuneMAMEnrollmentStatus` com as seguintes informações:

* A identidade da conta associada ao pedido
* Um código de estado que indica o resultado do pedido
* Cadeia de erro com uma descrição do código de estado
* Um objeto `NSError`. Este objeto é definido em `IntuneMAMEnrollmentStatus.h`, juntamente com os códigos de estado específicos que podem ser devolvidos.

### <a name="sample-code"></a>Código de exemplo

Estes são exemplos de implementações dos métodos delegados:

```objc
- (void)enrollmentRequestWithStatus:(IntuneMAMEnrollmentStatus*)status
{
    NSLog(@"enrollment result for identity %@ with status code %ld", status.identity, (unsigned long)status.statusCode);
    NSLog(@"Debug Message: %@", status.errorString);
}

- (void)policyRequestWithStatus:(IntuneMAMEnrollmentStatus*)status
{
    NSLog(@"policy check-in result for identity %@ with status code %ld", status.identity, (unsigned long)status.statusCode);
    NSLog(@"Debug Message: %@", status.errorString);
}

- (void)unenrollRequestWithStatus:(IntuneMAMEnrollmentStatus*)status
{
    NSLog(@"un-enroll result for identity %@ with status code %ld", status.identity, (unsigned long)status.statusCode);
    NSLog(@"Debug Message: %@", status.errorString);
}
```

## <a name="application-restart"></a>Reinício da aplicação

Quando uma aplicação receber políticas de MAM pela primeira vez, deve reiniciar para aplicar os hooks obrigatórios. Para notificar a aplicação de que é obrigatório reiniciar, o SDK disponibiliza um método delegado em `IntuneMAMPolicyDelegate.h`.

```objc
 - (BOOL) restartApplication
```

O valor deste método devolvido indica ao SDK se a aplicação terá de processar o reinício obrigatório:

* Se o valor devolvido for verdadeiro, a aplicação terá de processar o reinício.

* Se o valor devolvido for False, o SDK irá reiniciar a aplicação após este método ser devolvido. O SDK irá mostrar imediatamente uma caixa de diálogo que indica ao utilizador para reiniciar a aplicação.

## <a name="customize-your-apps-behavior-with-apis"></a>Personalizar o comportamento da sua aplicação com APIs

O SDK da Aplicação do Intune tem várias APIs que pode chamar para obter informações sobre a política APP aplicada à aplicação. Pode utilizar estes dados para personalizar o comportamento da sua aplicação. A tabela seguinte fornece informações sobre algumas aulas insinais essenciais que utilizará.

Classe | Descrição
----- | -----------
IntuneMAMPolicyManager.h | A classe IntuneMAMPolicyManager expõe a política APP do Intune implementada na aplicação. Em particular, expõe as APIs que são úteis para [Ativar identidades múltiplas](app-sdk-ios.md#enable-multi-identity-optional). |
IntuneMAMPolicy.h | A classe IntuneMAMPolicy expõe algumas definições da política MAM que se aplicam à aplicação. Estas definições de política são expostas para que a aplicação possa personalizar a respetiva IU. A maioria das definições de política é imposta pelo SDK e não pela aplicação. A única que a aplicação deve implementar é o controlo de Guardar Como. Esta classe expõe algumas APIs necessárias para implementar o Guardar Como. |
IntuneMAMFileProtectionManager.h | A classe IntuneMAMFileProtectionManager expõe APIs que a aplicação pode utilizar para proteger explicitamente ficheiros e diretórios com base numa identidade fornecida. A identidade pode ser gerida pelo Intune ou pode não ser gerida e o SDK irá aplicar a política MAM adequada. A utilização desta classe é opcional. |
IntuneMAMDataProtectionManager.h | A classe IntuneMAMDataProtectionManager expõe APIs que a aplicação pode utilizar para proteger memórias intermédias de dados aos quais foram fornecidas identidades. A identidade pode ser gerida pelo Intune ou pode não ser gerida e o SDK irá aplicar a encriptação adequada. |

## <a name="implement-allowed-accounts"></a>Implementar Contas Permitidas

Intune permite que os administradores de TI especifiquem quais as contas que podem ser registadas pelo utilizador. As aplicações podem consultar o Intune App SDK para a lista especificada de contas permitidas e, em seguida, garantir que apenas contas permitidas são assinadas no dispositivo.

Para consultar as contas permitidas, a App deve verificar a `allowedAccounts` propriedade no `IntuneMAMEnrollmentManager` . A `allowedAccounts` propriedade é ou um conjunto contendo as contas permitidas ou nulo. Se a propriedade for nula, então não foram especificadas contas permitidas.

As aplicações também podem reagir a alterações da `allowedAccounts` propriedade observando a `IntuneMAMAllowedAccountsDidChangeNotification` notificação. A notificação é publicada sempre que o `allowedAccounts` imóvel muda de valor.

## <a name="implement-save-as-and-open-from-controls"></a>Implementar controlos de poupança e de abertura

Intune permite que os administradores de TI selecionem quais locais de armazenamento uma aplicação gerida pode guardar dados ou abrir dados a partir de. As aplicações podem consultar o Intune MAM SDK para locais de armazenamento autorizados utilizando a `isSaveToAllowedForLocation` API, definida em `IntuneMAMPolicy.h` . As aplicações também podem consultar o Intune MAM SDK para locais de armazenamento abertos permitidos através da `isOpenFromAllowedForLocation` API, definida em `IntuneMAMPolicy.h` .

Antes de as aplicações poderem guardar dados geridos em localizações locais ou de armazenamento na cloud, estas têm de verificar a API `isSaveToAllowedForLocation` para saber se o administrador de TI permitiu que os dados fossem guardados nessas localizações.
Antes de abrir dados para uma aplicação a partir de um armazenamento em nuvem ou local, a aplicação deve consultar a API para saber se o administrador de `isOpenFromAllowedForLocation` TI permitiu que os dados fossem abertos a partir daí.

Quando as aplicações utilizam as `isSaveToAllowedForLocation` APIs ou `isOpenFromAllowedForLocation` APIs, devem passar na UPN para o local de armazenamento, se estiver disponível.

### <a name="supported-save-locations"></a>Localizações para guardar suportadas

A API `isSaveToAllowedForLocation` disponibiliza constantes para verificar se o administrador de TI permite que os dados sejam guardados na seguintes localizações, definidas na `IntuneMAMPolicy.h`:

* IntuneMAMSaveLocationOther
* IntuneMAMSaveLocationOneDriveForBusiness
* IntuneMAMSaveLocationSharePoint
* IntuneMAMSaveLocationLocalDrive
* IntuneMAMSaveLocationAccountDocument

As aplicações devem utilizar as constantes na API `isSaveToAllowedForLocation` para verificar se os dados podem ser guardados em localizações consideradas "geridas," como o OneDrive para Empresas, ou "pessoais". Além disso, a API deve ser utilizada quando a aplicação não consegue determinar se uma localização é "gerida" ou "pessoal".

A constante `IntuneMAMSaveLocationLocalDrive` deve ser utilizada quando a aplicação guarda dados numa localização no dispositivo local.

Se a conta para o local de destino for desconhecida, `nil` deve ser passada. A `IntuneMAMSaveLocationLocalDrive` localização deve ser sempre emparelhada com uma `nil` conta.

### <a name="supported-open-locations"></a>Locais abertos suportados

A `isOpenFromAllowedForLocation` API fornece constantes para verificar se o administrador de TI permite a abertura de dados a partir dos seguintes locais definidos em `IntuneMAMPolicy.h` .

* IntuneMAMOpenLocationOther
* IntuneMAMOpenLocationOneDriveForBusiness
* IntuneMAMOpenLocationSharePoint
* IntuneMAMOpenLocationCamera
* IntuneMAMOpenLocationLocalStorage
* IntuneMAMOpenLocationAccountDocument

As aplicações devem utilizar as constantes `isOpenFromAllowedForLocation` para verificar se os dados podem ser abertos a partir de locais considerados "geridos", como o OneDrive para Negócios, ou "pessoal". Além disso, a API deve ser utilizada quando a aplicação não pode verificar se um local é "gerido" ou "pessoal".

A `IntuneMAMOpenLocationCamera` constante deve ser usada quando a aplicação está a abrir dados da câmara ou do álbum de fotografias.

A `IntuneMAMOpenLocationLocalStorage` constante deve ser utilizada quando a aplicação está a abrir dados de qualquer local do dispositivo local.

A `IntuneMAMOpenLocationAccountDocument` constante deve ser utilizada quando a aplicação está a abrir um documento que tenha uma identidade de conta gerida (ver a secção "Dados Partilhados" abaixo)

Se a conta para a localização da fonte for desconhecida, `nil` deve ser passada. Os `IntuneMAMOpenLocationLocalStorage` `IntuneMAMOpenLocationCamera` locais e locais devem ser sempre emparelhados com uma `nil` conta.

### <a name="unknown-or-unlisted-locations"></a>Locais desconhecidos ou não listados

Quando a localização desejada não estiver listada nos `IntuneMAMSaveLocation` `IntuneMAMOpenLocation` enums ou for desconhecida, deve ser utilizado um dos dois locais.
* Se o local de salvamento estiver a ser acedido com uma conta gerida, então a `IntuneMAMSaveLocationAccountDocument` localização deve ser utilizada `IntuneMAMOpenLocationAccountDocument` (para abrir).
* Caso contrário, utilize a `IntuneMAMSaveLocationOther` localização `IntuneMAMOpenLocationOther` (para abrir).

É importante tornar a distinção clara entre a conta gerida e uma conta que partilha a UPN da conta gerida. Por exemplo, uma conta gerida com UPN user@contoso.com " assinada no OneDrive não é a mesma que uma conta com UPN user@contoso.com " assinada no Dropbox. Se um serviço desconhecido ou não listado for acedido através da assinatura na conta gerida (por exemplo, user@contoso.com " " assinado no OneDrive), este deve ser representado pela `AccountDocument` localização. Se o serviço desconhecido ou não listado entrar através de outra conta (por exemplo, user@contoso.com " " assinado no Dropbox), não está a aceder ao local com uma conta gerida e deve ser representado pela `Other` localização.

### <a name="sharing-blocked-alert"></a>Partilhar alerta bloqueado

Uma função de ajudante de UI pode ser usada quando a Ou `isSaveToAllowedForLocation` `isOpenFromAllowedForLocation` API é chamada e encontrada para bloquear a ação de salvamento/abertura. Se a aplicação quiser notificar o utilizador de que a ação foi bloqueada, pode ligar para a API definida para apresentar uma visão de `showSharingBlockedMessage` alerta com uma mensagem `IntuneMAMUIHelper.h` genérica.

## <a name="share-data-via-uiactivityviewcontroller"></a>Partilhar dados através de UIActivityViewController

A partir da versão 8.0.2, o SDK da Aplicação do Intune poderá filtrar ações de `UIActivityViewController` para que apenas as localizações de partilha geridas pelo Intune estejam disponíveis para seleção. Este comportamento será controlado pela política de transferência de dados de aplicações.

### <a name="copy-to-actions"></a>Ações 'Copy To'

Ao partilhar documentos através do `UIActivityViewController` `UIDocumentInteractionController` iOS, o iOS exibe ações 'Copy to' para cada aplicação que suporta a abertura do documento que está a ser partilhada. As aplicações declaram os tipos de documentos que suportam através da definição `CFBundleDocumentTypes` no ficheiro Info.plist. Este tipo de partilha já não estará disponível se a política proibir a partilha com aplicações não geridas. Em substituição, o utilizador terá de adicionar uma extensão de Ação que não faça parte da IU à aplicação e ligá-la ao SDK da Aplicação do Intune. A extensão de Ação é apenas um stub. O SDK implementará o comportamento de partilha de ficheiros. Siga os passos abaixo:

1. A sua aplicação deve ter pelo menos um esquemaURL definido no seu Info.plist juntamente com a `CFBundleURLTypes` sua `-intunemam` congénere. Por exemplo:
    ```objc
    <key>CFBundleURLSchemes</key>
    <array>
        <string>launch-com.contoso.myapp</string>
        <string>launch-com.contoso.myapp-intunemam</string>
    </array>
    ```

2. Tanto a sua aplicação como a extensão de ação devem partilhar pelo menos um Grupo de Aplicações, e o Grupo app deve ser listado sob `AppGroupIdentifiers` a matriz sob os dicionários IntuneMAMSettings da aplicação e da extensão.

3. Tanto a sua aplicação como a extensão de ação devem ter a capacidade de partilha de keychain e partilhar o `com.microsoft.intune.mam` grupo keychain.

4. Nomeie a extensão de ação "Open in" seguida do nome da aplicação. Localize o ficheiro Info.plist conforme necessário.

5. Forneça um ícone de modelo para a extensão, conforme descrito pela [documentação do desenvolvedor da Apple.](https://developer.apple.com/ios/human-interface-guidelines/extensions/sharing-and-actions/) Em alternativa, a ferramenta IntuneMAMConfigurator pode servir para gerar estas imagens do diretório .app da aplicação. Para fazê-lo, execute:

    ```bash
    IntuneMAMConfigurator -generateOpenInIcons /path/to/app.app -o /path/to/output/directory
    ```

6. Em IntuneMAMSettings na lista info.plist da extensão, adicione uma definição Boolean com `OpenInActionExtension` o valor SIM.

7. Configure o `NSExtensionActivationRule` para suportar um único ficheiro e todos os tipos da aplicação `CFBundleDocumentTypes` pré-fixado com `com.microsoft.intune.mam` . Por exemplo, se a aplicação suportar public.text e public.image, a regra de ativação será:

    ```objc
    SUBQUERY (
        extensionItems,
        $extensionItem,
        SUBQUERY (
            $extensionItem.attachments,
            $attachment,
            ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "com.microsoft.intune.mam.public.text" ||
            ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "com.microsoft.intune.mam.public.image").@count == 1
    ).@count == 1
    ```

### <a name="update-existing-share-and-action-extensions"></a>Atualizar extensões Partilhar e Ação existentes

Se a sua aplicação já tiver as extensões Partilhar ou Ação, a respetiva `NSExtensionActivationRule` terá de ser modificada para permitir os tipos do Intune. Para cada tipo suportado pela extensão, adicione um tipo com o prefixo `com.microsoft.intune.mam`. Por exemplo, se a regra de ativação existente for:  

```objc
SUBQUERY (
    extensionItems,
    $extensionItem,
    SUBQUERY (
        $extensionItem.attachments,
        $attachment,
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.url" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.plain-text" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.image" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.data"
    ).@count > 0
).@count > 0
```

Deverá ser alterada para:

```objc
SUBQUERY (
    extensionItems,
    $extensionItem,
    SUBQUERY (
        $extensionItem.attachments,
        $attachment,
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.url" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.plain-text" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.image" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "public.data" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "com.microsoft.intune.mam.public.url" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "com.microsoft.intune.mam.public.plain-text" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "com.microsoft.intune.mam.public.image" ||
        ANY $attachment.registeredTypeIdentifiers UTI-CONFORMS-TO "com.microsoft.intune.mam.public.data"
    ).@count > 0
).@count > 0
```

> [!NOTE]
> A ferramenta IntuneMAMConfigurator pode servir para adicionar os tipos do Intune à regra de ativação. Se a regra de ativação existente utilizar as constantes de cadeia predefinidas (por exemplo, NSExtensionActivationSupportsFileWithMaxCount NSExtensionActivationSupportsText, etc.), a sintaxe de predicado poderá ficar bastante complexa. A ferramenta IntuneMAMConfigurator também pode servir para converter a regra de ativação das constantes de cadeia para uma cadeia de predicado ao adicionar os tipos de Intune.

### <a name="what-the-ui-should-look-like"></a>O aspeto que a IU deve ter

Antiga IU:

![Partilhar dados - iOS old sharing UI](./media/app-sdk-ios/sharing-UI-old.png)

Nova IU:

![Partilhar dados - iOS nova partilha UI](./media/app-sdk-ios/sharing-UI-new.png)

## <a name="enable-targeted-configuration-appmam-app-config-for-your-ios-applications"></a>Permitir a configuração direcionada (configuração de aplicação APP/MAM) para as suas aplicações iOS

A configuração de MAM direcionada (também denominada configuração de aplicação MAM) permite que uma aplicação receba dados de configuração através do SDK do Intune. O formato e as variantes destes dados têm de ser definidos e comunicados aos clientes do Intune pelo proprietário/programador da aplicação.

Os administradores do Intune podem direcionar e implementar dados de configuração através do portal do Intune no Azure e do Graph API do Intune. A partir da versão 7.0.1 do SDK da Aplicação Intune para iOS, pode proporcionar dados de configuração de MAM direcionada às aplicações que participem na configuração de MAM direcionada através do Serviço MAM. Os dados de configuração de aplicações são emitidos através do nosso Serviço de MAM diretamente para a aplicação em vez de através do canal de MDM. O SDK da Aplicação Intune fornece uma classe para aceder aos dados obtidos através destas consolas. Os seguintes itens são pré-requisitos:

* A aplicação tem de estar inscrita com o serviço MAM do Intune para poder aceder à IU de configuração de MAM direcionada. Para obter mais informações, veja [Receber a política de proteção de aplicações](#receive-app-protection-policy).

* Inclua `IntuneMAMAppConfigManager.h` no ficheiro de origem da sua aplicação.

* Chame `[[IntuneMAMAppConfigManager instance] appConfigForIdentity:]` para apresentar o Objeto Configuração da Aplicação.

* Chame o seletor adequado no objeto `IntuneMAMAppConfig`. Por exemplo, se a chave da aplicação for uma cadeia, é aconselhável utilizar `stringValueForKey` ou `allStringsForKey`. Veja `IntuneMAMAppConfig.h` para obter uma descrição detalhada dos valores devolvidos e das condições de erro.

Para obter mais informações sobre as funcionalidades da Graph API, veja [Referência da Graph API](https://developer.microsoft.com/graph/docs/concepts/overview).

Para obter mais informações sobre como criar uma política de configuração de aplicações direcionada para o MAM no iOS, consulte a secção da aplicação direcionada para o MAM config em Como utilizar as políticas de configuração da [aplicação Microsoft Intune para iOS/iPadOS](../apps/app-configuration-policies-use-ios.md).

## <a name="telemetry"></a>Telemetria

Por predefinição, o SDK da Aplicação do Intune para iOS recolhe dados telemétricos dos seguintes tipos de eventos:

* **Iniciação da aplicação**: para ajudar o Microsoft Intune a saber mais informações sobre a utilização de aplicações ativadas para MAM por tipo de gestão (MAM com MDM, MAM sem inscrição MDM, entre outros).

* **Chamadas de inscrição**: para ajudar o Microsoft Intune a conhecer a taxa de êxito e outras métricas de desempenho das chamadas de inscrição no lado do cliente.

* **Ações do Intune**: para ajudar a diagnosticar problemas e garantir a funcionalidade do Intune, recolhemos informações sobre as ações do SDK do Intune.

> [!NOTE]
> Se optar por não enviar os dados telemétricos do SDK da Aplicação Intune para o Microsoft Intune a partir da sua aplicação móvel, deve desativar a captura de telemetria do SDK da Aplicação Intune. Defina a propriedade `MAMTelemetryDisabled` como YES no dicionário IntuneMAMSettings.

## <a name="enable-multi-identity-optional"></a>Ativar identidades múltiplas (opcional)

Por predefinição, o SDK aplica a política à aplicação como um todo. As identidades múltiplas são uma funcionalidade de MAM que pode ativar para aplicar uma política por identidade. Esta opção requer uma maior participação da aplicação do que outras funcionalidades de MAM.

A aplicação deve informar ao SDK da aplicação quando tenciona alterar a identidade ativa. O SDK também notifica a aplicação quando for necessária uma alteração de identidade. Atualmente, apenas é suportada uma identidade gerida. Depois de o utilizador inscrever o dispositivo ou a aplicação, o SDK utiliza esta identidade e considera-a a identidade gerida primária. Os outros utilizadores na aplicação serão tratados como não geridos, com definições de política não restrita.

Note que uma identidade é simplesmente definida como uma cadeia. As identidades são sensíveis a maiúsculas e minúsculas. Os pedidos de identidade ao SDK podem não devolver a mesma utilização de maiúsculas e minúsculas que tinha sido originalmente utilizada quando a identidade foi definida.

### <a name="identity-overview"></a>Descrição geral de identidade

Uma identidade é apenas o nome de utilizador de uma conta (por exemplo, user@contoso.com). Os programadores podem definir a identidade da aplicação nos seguintes níveis:

* **Identidade de processo**: define a identidade em todo o processo e é maioritariamente utilizada em aplicações de identidade única. Esta identidade afeta todas as tarefas, os ficheiros e a IU.

* **Identidade da IU**: determina que políticas são aplicadas às tarefas de IU no thread principal, como cortar/copiar/colar, PIN, autenticação e partilha de dados. A identidade da IU não afeta as tarefas de ficheiros, tal como encriptação e cópia de segurança.

* **Identidade do thread**: afeta as políticas aplicadas ao thread atual. Esta identidade afeta todas as tarefas, os ficheiros e a IU.

A aplicação é responsável por definir as identidades de forma adequada, independentemente de o utilizador ser gerido ou não.

A qualquer altura, todos os threads têm uma identidade eficaz para tarefas de IU e tarefas de ficheiros. Esta é a identidade que serve para verificar que políticas devem ser aplicadas (se forem aplicadas políticas). Se a identidade for "no identity" ou se o utilizador não for gerido, não serão aplicadas políticas. Os diagramas abaixo mostram como são determinadas as identidades em vigor.

  ![Intune App SDK iOS: Processo de determinação de identidade](./media/app-sdk-ios/ios-thread-identities.png)

### <a name="thread-queues"></a>Filas de threads

As aplicações emitem muitas vezes tarefas assíncronas e síncronas para filas de threads. O SDK interceta chamadas do Grand Central Dispatch (GCD) e associa a atual identidade do thread às tarefas emitidas. Quando as tarefas são concluídas, o SDK altera temporariamente a identidade do thread para a identidade associada às tarefas, conclui as tarefas e, em seguida, restaura a identidade do thread original.


Como o `NSOperationQueue` é criado sobre o GCD, o `NSOperations` será executado na identidade do thread na altura em que as tarefas são adicionadas ao `NSOperationQueue`. O `NSOperations` ou as funções emitidas diretamente através do GCD também podem alterar a identidade do thread atual durante a execução. Esta identidade substitui a identidade herdada do thread emissor.

### <a name="file-owner"></a>Proprietário do ficheiro

O SDK controla as identidades dos proprietários dos ficheiros locais e aplica as políticas de acordo com a mesma. Um proprietário do ficheiro é estabelecido quando um ficheiro é criado ou quando um ficheiro é aberto em modo truncado. O proprietário está definido para a identidade da tarefa do ficheiro efetiva do thread que executa a tarefa.

Em alternativa, as aplicações podem definir a identidade de proprietário do ficheiro explicitamente, ao utilizar o `IntuneMAMFilePolicyManager`. As aplicações podem utilizar o `IntuneMAMFilePolicyManager` para obter o proprietário do ficheiro e definir a identidade de IU antes de mostrarem os conteúdos dos ficheiros.

### <a name="shared-data"></a>Dados partilhados

Se a aplicação criar ficheiros que possuam dados de utilizadores geridos e não geridos, a aplicação é responsável por encriptar os dados do utilizador gerido. Pode encriptar dados com as APIs `protect` e `unprotect` no `IntuneMAMDataProtectionManager`.

O método `protect` aceita uma identidade que pode ser um utilizador gerido ou não gerido. Se o utilizador for gerido, os dados serão encriptados. Se o utilizador for não gerido, será adicionado um cabeçalho aos dados a codificar a identidade, mas os dados não serão encriptados. Pode utilizar o `protectionInfo` método para recuperar o proprietário dos dados.

### <a name="share-extensions"></a>Extensões de partilha

Se a aplicação tem uma extensão de partilha, o proprietário do item partilhado pode ser obtido com recurso ao método `protectionInfoForItemProvider` no `IntuneMAMDataProtectionManager`. Se o item partilhado for um ficheiro, o SDK processará a definição do proprietário do ficheiro. Se o item partilhado consistir em dados, a aplicação é responsável por definir o proprietário do ficheiro se estes dados forem persistentes num ficheiro e chamar a API `setUIPolicyIdentity` antes de mostrar estes dados na IU.

### <a name="turn-on-multi-identity"></a>Ativar múltiplas identidades

Por predefinição, as aplicações são consideradas de identidade única. O SDK define a identidade de processo para o utilizador inscrito. Para ativar o suporte de identidades múltiplas, adicione uma definição booleana com o nome `MultiIdentity` e um valor YES ao dicionário IntuneMAMSettings no ficheiro Info.plist da aplicação.

> [!NOTE]
> Quando as identidades múltiplas estiverem ativadas, as identidades de processo, de IU e de thread são definidas como nulas. A aplicação é responsável pela sua definição adequada.

### <a name="switch-identities"></a>Mudar de identidade

* **Mudança de identidade iniciada pela aplicação**:

    Ao iniciar, considera-se que as aplicações de identidades múltiplas estão a ser executadas numa conta desconhecida e não gerida. A IU de iniciação condicional não será executada e não serão aplicadas políticas na aplicação. A aplicação é responsável por notificar o SDK sempre que a identidade deva ser alterada. Normalmente, este processo ocorre sempre que a aplicação estiver prestes a mostrar os dados de uma conta de utilizador específica.

    Um exemplo desta situação é quando o utilizador tenta abrir um documento, uma caixa de correio ou um separador num bloco de notas. A aplicação tem de notificar o SDK antes que o ficheiro, a caixa de correio ou o separador sejam efetivamente abertos. Este processo é realizado através da API `setUIPolicyIdentity` no `IntuneMAMPolicyManager`. Esta API deve ser chamada quer o utilizador seja gerido ou não. Se o utilizador for gerido, o SDK irá executar as verificações de inicialização condicional, como deteção de jailbreak, PIN e autenticação.

    O resultado da mudança de identidade é devolvido à aplicação de forma assíncrona através de um processador de conclusão. A aplicação deverá adiar a abertura do documento, da caixa de correio ou do separador até que um código de resultado de sucesso seja devolvido. Se a mudança de identidade tiver falhado, a aplicação deverá cancelar a tarefa.

* **Mudança de identidade iniciada pelo SDK**:

    Por vezes, o SDK precisa de pedir à aplicação que mude para uma identidade específica. As aplicações de identidades múltiplas têm de implementar o método `identitySwitchRequired` no `IntuneMAMPolicyDelegate` para processar este pedido.

    Aquando da chamada deste método, se a aplicação conseguir processar o pedido de mudança para a identidade especificada, esta deverá passar o `IntuneMAMAddIdentityResultSuccess` para o processador de conclusão. Se não conseguir processar a mudança de identidade, a aplicação deverá passar o `IntuneMAMAddIdentityResultFailed` para o processador de conclusão.

    A aplicação não tem de chamar o `setUIPolicyIdentity` em resposta a esta chamada. Se o SDK necessitar da aplicação para mudar para uma conta de utilizador não gerida, a cadeia vazia será passada para a chamada do `identitySwitchRequired`.

* **Limpeza seletiva:**

    Quando for efetuada uma eliminação seletiva na aplicação, o SDK chamará o método `wipeDataForAccount` no `IntuneMAMPolicyDelegate`. A aplicação é responsável pela remoção da conta do utilizador especificado e de quaisquer dados que lhe sejam associados. O SDK é capaz de remover todos os ficheiros do utilizador e realizará esta ação se a aplicação devolver FALSE da chamada do `wipeDataForAccount`.

    Tenha em atenção que este método é chamado a partir de um thread de segundo plano. A aplicação não deve devolver um valor até que todos os dados para o utilizador tenham sido removidos (com a exceção dos ficheiros, se a aplicação devolver FALSE).

## <a name="siri-intents"></a>Intenções Siri
Se a sua aplicação se integrar com a Siri Intents, certifique-se de ler os comentários para `areSiriIntentsAllowed` `IntuneMAMPolicy.h` obter instruções sobre o apoio a este cenário. 
    
## <a name="notifications"></a>Notificações
Se a sua aplicação receber notificações, certifique-se de ler os comentários `notificationPolicy` `IntuneMAMPolicy.h` para obter instruções sobre o suporte a este cenário.  Recomenda-se que as aplicações se registem para `IntuneMAMPolicyDidChangeNotification` descrever `IntuneMAMPolicyManager.h` e comuniquem este valor através `UNNotificationServiceExtension` do porta-chaves.
## <a name="displaying-web-content-within-application"></a>Exibindo conteúdo web dentro da aplicação
Se a sua aplicação tiver a capacidade de exibir websites dentro de uma visão web e as páginas web exibidas tiverem a capacidade de navegar para sites arbitrários, a aplicação é ressonável para definir a identidade atual para que os dados geridos não possam ser vazados através da visão web. Exemplos disso são páginas web 'Suggest a Feature' ou 'Feedback' que têm ligações diretas ou indiretas a um motor de busca.
As aplicações multi-identidade devem ligar para intuneMAMPolicyManager setUIPolicyIdentity passando na corda vazia antes de exibir a vista web. Após a demissão da vista web, o pedido deve chamar setUIPolicyIdentity passando na identidade atual.
As aplicações de identidade única devem ligar para intuneMAMPolicyManager setCurrentThreadIdentity passando na cadeia vazia antes de exibir a vista web. Depois de a vista web ser rejeitada, a aplicação deve ligar para o conjuntoCurrentThreadIdentity passando a zero.

## <a name="ios-best-practices"></a>Melhores práticas de iOS

Eis algumas melhores práticas recomendadas para desenvolver para iOS:

* O sistema de ficheiros iOS é sensível às maiúsculas e minúsculas. Confirme que as maiúsculas e minúsculas estão corretas nos nomes dos ficheiros, como `libIntuneMAM.a` e `IntuneMAMResources.bundle`.

* Se o Xcode tiver problemas a localizar `libIntuneMAM.a`, pode corrigir o problema ao adicionar o caminho a esta biblioteca nos caminhos de pesquisa do linker.

## <a name="faqs"></a>FAQs

### <a name="are-all-of-the-apis-addressable-through-native-swift-or-the-objective-c-and-swift-interoperability"></a>As APIs são todas endereçáveis através do Swift nativo ou da interoperabilidade do Objective-C e do Swift?

As APIs do SDK da Aplicação do Intune estão apenas no Objective-C e não suportam o Swift **nativo**. Precisa da interoperabilidade do Swift com o Objective-C.

### <a name="do-all-users-of-my-application-need-to-be-registered-with-the-app-we-service"></a>Todos os utilizadores da minha aplicação têm de estar registados no serviço APP-WE?

Não. De facto, apenas as contas do trabalho ou escolares devem ser registadas no SDK da Aplicação do Intune. As aplicações são responsáveis por determinar se uma conta é utilizada num contexto profissional ou escolar.

### <a name="what-about-users-that-have-already-signed-in-to-the-application-do-they-need-to-be-enrolled"></a>E os utilizadores que já iniciaram sessão na aplicação? Precisam de ser inscritos?

A aplicação é responsável por inscrever os utilizadores após terem sido autenticados com êxito. A aplicação é também responsável por inscrever quaisquer contas existentes que podem ter estado presentes antes de a aplicação possuir a funcionalidades MDM sem MAM.

Para tal, a aplicação deve utilizar o método `registeredAccounts:`. Este método devolve um NSDictionary com todas as contas registadas no serviço MAM do Intune. Se existirem contas na aplicação que não estejam na lista, a aplicação deverá registar e inscrever as respetivas contas através do `registerAndEnrollAccount:`.

### <a name="how-often-does-the-sdk-retry-enrollments"></a>Com que frequência é que o SDK volta a tentar inscrições?

O SDK volta a tentar automaticamente todas as inscrições anteriormente falhadas a cada 24 horas. O SDK faz isto para garantir que, se a organização de um utilizador ativar a MAM após o utilizador ter assinado a aplicação, o utilizador irá inscrever-se e receber políticas com sucesso.

O SDK deixará de voltar a tentar quando detetar que um utilizador se inscreveu na aplicação com êxito. Isto deve-se ao facto de apenas um utilizador poder inscrever uma aplicação num determinado momento. Se a inscrição do utilizador for anulada, as novas tentativas começarão de novo no mesmo intervalo de 24 horas.

### <a name="why-does-the-user-need-to-be-deregistered"></a>Por que motivo tem o registo do utilizador de ser anulado?

O SDK realizará estas ações em segundo plano de forma periódica:

* Se a aplicação ainda não estiver inscrita, esta tentará inscrever todas as contas registadas de 24 em 24 horas.
* Se a aplicação estiver inscrita, o SDK irá procurar atualizações à política de MAM de 8 em 8 horas.

A anulação do registo de um utilizador notifica o SDK que o utilizador deixará de utilizar a aplicação e este pode parar qualquer um dos eventos periódicos da respetiva conta de utilizador. Também aciona uma anulação de inscrição da aplicação e eliminação seletiva, se for preciso.

### <a name="should-i-set-the-dowipe-flag-to-true-in-the-deregister-method"></a>Devo definir o sinalizador doWipe como True no método de anulação do registo?

Este método deve ser chamado antes de o utilizador terminar a sessão na aplicação.  Se os dados do utilizador forem eliminados da aplicação como parte do sign-out, `doWipe` podem ser definidos como falsos. Mas se a aplicação não remover os dados do utilizador, deve ser definido como verdadeiro para `doWipe` que o SDK possa apagar os dados.

### <a name="are-there-any-other-ways-that-an-application-can-be-un-enrolled"></a>Existem outras formas de anular o registo de uma aplicação?

Sim, o administrador de TI pode enviar um comando de eliminação seletiva para a aplicação. Isto irá desregistar e desinscrever o utilizador, e irá limpar os dados do utilizador. O SDK processa este cenário automaticamente e envia uma notificação através do método de delegação de anulação de inscrição.

### <a name="is-there-a-sample-app-that-demonstrates-how-to-integrate-the-sdk"></a>Existe uma aplicação de exemplo que demonstre como integrar o SDK?

Sim! Recentemente, renovámos a nossa aplicação de exemplo open source [Wagr para iOS](https://github.com/Microsoft/Wagr-Sample-Intune-iOS-App). Esta aplicação está ativada para a política de proteção de aplicações com o SDK da Aplicação do Intune.

### <a name="how-can-i-troubleshoot-my-app"></a>Como posso resolver o problema da minha aplicação?

O Intune SDK para iOS 9.0.3+ suporta a capacidade de adicionar uma consola de diagnóstico dentro da aplicação móvel para testar políticas e erros de registo. `IntuneMAMDiagnosticConsole.h`define a `IntuneMAMDiagnosticConsole` interface de classe, que os desenvolvedores podem usar para exibir a consola de diagnóstico Intune. Isto permite que os utilizadores finais ou desenvolvedores durante o teste recolham e partilhem registos Intune para ajudar a diagnosticar qualquer problema que possam ter. Esta API é opcional para os integradores.

## <a name="submit-your-app-to-the-app-store"></a>Envie a sua aplicação à App Store

Tanto a biblioteca estática como as compilações de estrutura do SDK da Aplicação do Intune são binários universais. Isto significa que têm código para todas as arquiteturas de dispositivo e simulador. A Apple rejeita as aplicações submetidas à App Store se estas tiverem código de simulador. Ao compilar com a biblioteca estática em compilações apenas de dispositivo, o linker retira o código de simulador automaticamente. Siga os passos abaixo para garantir que todo o código de simulador é removido antes de carregar a aplicação para a App Store.

1. Confirmar que o `IntuneMAM.framework` está no seu ambiente de trabalho.

2. Execute estes comandos:

    ```bash
    lipo ~/Desktop/IntuneMAM.framework/IntuneMAM -remove i386 -remove x86_64 -output ~/Desktop/IntuneMAM.device_only
    ```

    ```bash
    cp ~/Desktop/IntuneMAM.device_only ~/Desktop/IntuneMAM.framework/IntuneMAM
    ```

    O primeiro comando retira as arquiteturas de simulador do ficheiro DYLIB da estrutura. O segundo comando copia o ficheiro DYLIB apenas para dispositivo de volta para o diretório da estrutura.
