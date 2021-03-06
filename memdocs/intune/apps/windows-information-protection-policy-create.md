---
title: Política de proteção de aplicações para proteção de informações do Windows (WIP)
titleSuffix: Microsoft Intune
description: Criar e implementar a política de Proteção de Informação do Windows (WIP) com a Microsoft Intune
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/25/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 4e3627bd-a9fd-49bc-b95e-9b7532f0ed55
ms.reviewer: joglocke
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 66ea84d8defa1d1d5b79f686537b391452cf3c30
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990279"
---
# <a name="create-and-deploy-windows-information-protection-wip-policy-with-intune"></a>Criar e implementar a política de Proteção de Informação do Windows (WIP) com o Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Pode utilizar as políticas de Proteção de Informação do Windows (WIP) com aplicações do Windows 10 para proteger aplicações sem a inscrição do dispositivo.

## <a name="before-you-begin"></a>Antes de começar

Tem de compreender alguns conceitos ao adicionar uma política WIP:

### <a name="list-of-allowed-and-exempt-apps"></a>Lista de aplicações permitidas e excluídas

- **Aplicações protegidas:** estas são as aplicações que precisam de cumprir esta política.

- **Aplicações excluídas:** estas aplicações estão excluídas desta política e podem aceder aos dados empresariais sem restrições.

### <a name="types-of-apps"></a>Tipos de aplicações

- **Aplicativos recomendados:** Uma lista pré-povoada de aplicações (principalmente Microsoft Office) que lhe permitem importar facilmente para a política.
- **Aplicações da Loja:** pode adicionar qualquer aplicação da loja Windows à política.
- **Aplicações de ambiente de trabalho do Windows:** pode adicionar qualquer aplicação de ambiente de trabalho à política (por exemplo, .exe, .dll)

## <a name="prerequisites"></a>Pré-requisitos

Tem de configurar o fornecedor MAM antes de poder criar uma política wip. Saiba mais sobre [como configurar o fornecedor de MAM com o Intune](app-protection-policies-configure-windows-10.md).  

> [!IMPORTANT]
> O WIP não suporta várias identidades, apenas pode existir uma identidade gerida de cada vez. Para obter mais informações sobre as capacidades e limitações do WIP, consulte Proteja os seus dados empresariais utilizando a Proteção de [Informação do Windows (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip).

Além disso, tem de ter a seguinte licença e atualização:

- Licença [Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium)
- [Atualização para Criativos do Windows](https://blogs.windows.com/windowsexperience/2017/04/11/how-to-get-the-windows-10-creators-update/#o61bC2PdrHslHG5J.97)





## <a name="to-add-a-wip-policy"></a>Para adicionar uma política WIP

Depois de configurar o Intune na sua organização, pode criar uma política específica do WIP.

> [!TIP]  
> Para obter informações relacionadas sobre a criação de políticas WIP do Intune, incluindo as definições disponíveis e como configurá-las, veja [Create a Windows Information Protection (WIP) policy with MAM using the Azure portal for Microsoft Intune](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-mam-intune-azure) (Criar uma política Windows Information Protection (WIP) com a MAM no portal do Azure para o Microsoft Intune) na biblioteca de documentação de Segurança do Windows. 


1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Políticas**de proteção de  >  **aplicativos**  >  **Criar política**.
3. Adicione os seguintes valores:
    - **Nome:** introduza um nome (obrigatório) para a nova política.
    - **Descrição:** (opcional) escreva uma descrição.
    - **Plataforma:** Escolha o **Windows 10** como plataforma suportada para a sua política wip.
    - **Estado de inscrição:** escolha **Sem inscrição** como o estado de inscrição da política.
4. Escolha **Criar**. A política é criada e aparece na tabela sobre o painel de políticas de proteção da **App.**

## <a name="to-add-recommended-apps-to-your-protected-apps-list"></a>Para adicionar aplicações recomendadas à lista de aplicações protegidas

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **políticas**de proteção de  >  **aplicativos**.
3. No painel de políticas de proteção da **App,** escolha a política que pretende modificar. O painel **de proteção de aplicações Intune** é apresentado.
4. Escolha **aplicativos protegidos** do painel de proteção de **aplicações intune.** O painel de **aplicações protegidas** abre mostrando-lhe todas as aplicações que já estão incluídas na lista para esta política de proteção de aplicações.
5. Selecione **Adicionar aplicações**. As informações **Adicionar aplicações** mostram uma lista de aplicações filtrada. A lista na parte superior do painel permite alterar o filtro da lista.
6. Selecione todas as aplicações que pretende que acedam aos seus dados empresariais.
7. Clique em **OK**. O painel de **aplicações protegidas** é atualizado mostrando todas as aplicações selecionadas.
8. Clique em **Guardar**.

## <a name="add-a-store-app-to-your-protected-apps-list"></a>Adicionar uma aplicação da loja à lista de aplicações protegidas

**Para adicionar uma aplicação da Loja**

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **políticas**de proteção de  >  **aplicativos**.
3. No painel de políticas de proteção da **App,** escolha a política que pretende modificar. O painel **de proteção de aplicações Intune** é apresentado.
4. Escolha **aplicativos protegidos** do painel de proteção de **aplicações intune.** O painel de **aplicações protegidas** abre mostrando-lhe todas as aplicações que já estão incluídas na lista para esta política de proteção de aplicações.
5. Selecione **Adicionar aplicações**. As informações **Adicionar aplicações** mostram uma lista de aplicações filtrada. A lista na parte superior do painel permite alterar o filtro da lista.
6. A partir da lista, selecione **Aplicações da loja**.
7. Introduza os valores para **Nome**, **Fabricante**, **Nome do Produto** e **Ação**. Certifique-se de que define o valor **Ação** para **Permitir**, para que a aplicação tenha acesso aos seus dados empresariais.
9. Clique em **OK**. O painel de **aplicações protegidas** é atualizado mostrando todas as aplicações selecionadas.
10. Clique em **Guardar**.

## <a name="add-a-desktop-app-to-your-protected-apps-list"></a>Adicionar uma aplicação de ambiente de trabalho à lista de aplicações protegidas

**Para adicionar uma aplicação de desktop**
1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **políticas**de proteção de  >  **aplicativos**.
3. No painel de políticas de proteção da **App,** escolha a política que pretende modificar. O painel **de proteção de aplicações Intune** é apresentado.
4. Escolha **aplicativos protegidos** do painel de proteção de **aplicações intune.** O painel de **aplicações protegidas** abre mostrando-lhe todas as aplicações que já estão incluídas na lista para esta política de proteção de aplicações.
5. Selecione **Adicionar aplicações**. As informações **Adicionar aplicações** mostram uma lista de aplicações filtrada. A lista na parte superior do painel permite alterar o filtro da lista.
6. A partir da lista, selecione **Aplicações de ambiente de trabalho**.
7. Introduza os valores para **Nome**, **Fabricante**, **Nome do Produto**, **Ficheiro**, **Versão Mínima**, **Versão Máxima** e **Ação**. Certifique-se de que define o valor **Ação** para **Permitir**, para que a aplicação tenha acesso aos seus dados empresariais.
9. Clique em **OK**. O painel de **aplicações protegidas** é atualizado mostrando todas as aplicações selecionadas.
10. Clique em **Guardar**.

## <a name="wip-learning"></a>Aprendizagem de WIP
Depois de adicionar as aplicações que pretende proteger com o WIP, tem de aplicar um modo de proteção através da **Aprendizagem de WIP**.

### <a name="before-you-begin"></a>Antes de começar

A Aprendizagem de WIP é um relatório que lhe permite monitorizar as suas aplicações com o WIP e as aplicações desconhecidas de WIP. As aplicações desconhecidas são as que não foram implementadas pelo departamento de TI da sua organização. Pode exportar estas aplicações a partir do relatório e adicioná-las às suas políticas wip para evitar perturbações de produtividade antes de impor o WIP no modo "Block".

<!-- 1631908 -->
Para além de ver informações sobre aplicações com o WIP, agora pode ver um resumo dos dispositivos que partilharam dados profissionais com sites. Com estas informações, pode determinar os sites que devem ser adicionados às políticas WIP dos grupos e dos utilizadores. O resumo mostra que URLs de sites são acedidos por aplicações com o WIP.

Quando estiver a trabalhar com aplicações com o WIP e aplicações desconhecidas de WIP, recomendamos que comece com **Silencioso** ou **Permitir Substituições** enquanto verifica com um pequeno grupo que tenha as aplicações corretas na sua lista de aplicações protegidas. Depois de terminar, pode alterar a política de imposição final, **Bloquear**.

### <a name="what-are-the-protection-modes"></a>O que são os modos de proteção?

#### <a name="block"></a>Bloquear
O WIP procura práticas de partilha de dados inadequadas e impede o utilizador de concluir a ação. As ações bloqueadas podem incluir a partilha de informações em aplicações não protegidas pela empresa e a partilha de dados empresariais entre outras pessoas e dispositivos fora da sua organização.

#### <a name="allow-overrides"></a>Permitir Substituições
O WIP procura partilhas de dados inadequadas e avisará os utilizadores quando estes realizarem alguma ação considerada potencialmente não segura. No entanto, este modo permite ao utilizador substituir a política e partilhar os dados, registando a ação no registo de auditorias.

#### <a name="silent"></a>Automática
O WIP é executado no modo silencioso e regista as partilhas de dados inadequadas sem bloquear nada que pedisse a interação do funcionário durante o modo Permitir Substituição. As ações não permitidas, tais como aplicações que estejam a tentar aceder inadequadamente a um recurso de rede ou a dados protegidos pelo WIP, continuam a ser interrompidas.

#### <a name="off-not-recommended"></a>Desativado (não recomendado)
O WIP está desativado e não ajuda a proteger ou a auditar os seus dados.

Depois de desativar o WIP, é realizada uma tentativa para desencriptar quaisquer ficheiros etiquetados pelo WIP nas unidades ligadas localmente. Note que a desencriptação anterior e informações políticas não são automaticamente reaplicadas se voltar a ligar a proteção WIP.

### <a name="add-a-protection-mode"></a>Adicionar um modo de proteção

1. A partir do painel de política da **App,** escolha o nome da sua apólice e, em seguida, escolha **as definições necessárias**.

    ![Screenshot do painel do modo de aprendizagem](./media/windows-information-protection-policy-create/learning-mode-sc1.png)

1. Selecione uma definição e, em seguida, selecione **Guardar**.

### <a name="use-wip-learning"></a>Utilizar a Aprendizagem de WIP

1. Abra o [portal Azure.](https://portal.azure.com) Selecione **Todos os serviços**. Escreva **Intune** no filtro da caixa de texto.

3. Escolha **Intune**  >  **Aplicativos**Intune .

4. Escolha **o estado de proteção de aplicativos**  >  **reporta**a aprendizagem da  >  **proteção de informações do Windows**.  

    Depois de as aplicações aparecerem no relatório de registo da Aprendizagem de WIP, pode adicioná-las às políticas de proteção de aplicações.

## <a name="allow-windows-search-indexer-to-search-encrypted-items"></a>Permitir que o Indexador do Windows Search procure itens encriptados
Permite ou proíbe a indexação de itens. Este parâmetro é para o Indexador do Windows Search, que controla a indexação de itens que são encriptados, tais como os ficheiros protegidos do Windows Information Protection (WIP).

Esta opção de política de proteção de aplicações está nas **Definições avançadas** da política do Windows Information Protection. A política de proteção de aplicações tem de ser definida para a plataforma do *Windows 10* e a política de aplicação **Estado da inscrição** tem de ser definida para **Com inscrição**.

Quando a política está ativada, os itens protegidos pelo WIP são indexados e os respetivos metadados são armazenados numa localização não encriptada. Os metadados incluem conteúdos como o caminho do ficheiro e a data de modificação.

Quando a política está desativada, os itens protegidos pelo WIP não são indexados e não são apresentados nos resultados na Cortana ou no explorador de ficheiros. O desempenho das aplicações de fotografias e do Groove também poderá ser afetado se existirem muitos ficheiros multimédia protegidos pelo WIP no dispositivo.

## <a name="add-encrypted-file-extensions"></a>Adicionar extensões do ficheiro encriptado

Além de definir a opção **Permitir que o Indexador do Windows Search procure itens encriptados**, pode especificar uma lista de extensões de ficheiros. Os ficheiros com estas extensões são encriptados ao copiar de uma partilha do protocolo SMB (Server Message Block) dentro do limite empresarial como definido na lista de localizações de rede. Quando esta política não é especificada, é aplicado o comportamento de encriptação automática existente. Quando esta política é configurada, apenas os ficheiros com extensões na lista são encriptados.

## <a name="deploy-your-wip-app-protection-policy"></a>Implementar a política de proteção de aplicações do WIP

> [!IMPORTANT]
> Estas informações aplicam-se ao WIP sem inscrição de dispositivos.

<!---not sure why you need the Important note. Isn't this what the topic is about? app protection w/o enrollment?--->

Depois de criar a política de proteção de aplicações do WIP, tem de a implementar na sua organização através da MAM.

1. No painel de política da **App,** escolha a sua política de proteção de aplicações recém-criada, escolha **grupos de utilizadores**  >  **Adicionar grupo de utilizadores**.

    Uma lista de grupos de utilizadores, composto por todos os grupos de segurança do seu Diretório Ativo Azure, abre no painel do **grupo de utilizadores Add.**

2. Selecione o grupo ao qual pretende aplicar a sua política e, em seguida, escolha **Selecionar** para implementá-la.

## <a name="next-steps"></a>Passos seguintes

Para saber mais sobre o Windows Information Protection, veja [Proteger os dados empresariais com o Windows Information Protection (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip).
