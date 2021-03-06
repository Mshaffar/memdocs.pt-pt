---
title: Adicionar aplicações de linha de negócio iOS ao Microsoft Intune
titleSuffix: ''
description: Saiba como adicionar uma aplicação iOS (LOB) à Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/07/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 099101e8-4b22-40ac-ba19-82ba5c71944c
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f4aee16fc0dacce46e75735a161ae2c56d3bdb15
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990669"
---
# <a name="add-an-ios-line-of-business-app-to-microsoft-intune"></a>Adicionar aplicações de linha de negócio iOS ao Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Utilize as informações neste artigo para o ajudar a adicionar aplicações de linha de negócio (LOB) iOS ao Microsoft Intune. Uma aplicação de linha de negócios (LOB) é uma aplicação que adiciona ao Intune a partir de um ficheiro de instalação de aplicações IPA. Normalmente, este tipo de aplicação é criado internamente. Primeiro terá de se juntar ao programa iOS Developer Enterprise. Para mais informações sobre como fazê-lo consulte o [site da Apple](https://developer.apple.com/programs/ios/enterprise/).

> [!NOTE]
> Os utilizadores de dispositivos iOS podem remover algumas aplicações iOS incorporadas, tal como Bolsa e Mapas. Não pode utilizar o Intune para implementar novamente essas aplicações. Se os utilizadores eliminarem essas aplicações, terão de aceder à loja de aplicações e reinstalá-las manualmente.
>
> As aplicações iOS LOB têm um limite máximo de tamanho de 2 GB por app.

> [!NOTE]
> Os identificadores de pacote (por exemplo, *com.contoso.app)* destinam-se a identificar de forma única uma aplicação. Por exemplo, para instalar uma versão beta de uma aplicação LOB ao lado da versão de produção para fins de teste, a versão beta deve ter um identificador único diferente (por exemplo, *com.contoso.app-beta).* Caso contrário, a versão beta sobrepor-se-á à produção e será tratada como uma atualização. Renomear o ficheiro .ipa não tem qualquer efeito neste comportamento.

## <a name="select-the-app-type"></a>Selecione o tipo de aplicativo

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Apps**  >  **Todas as aplicações**  >  **Adicionar**.
3. No painel do **tipo de aplicação Select,** sob os **outros** tipos de aplicações, selecione **app Line-of-business**.
4. Clique em **Selecionar**. Os passos da **aplicação Add** são apresentados.

## <a name="step-1---app-information"></a>Passo 1 - Informações sobre aplicativos

### <a name="select-the-app-package-file"></a>Selecione o ficheiro de pacote de aplicativos

1. No painel de **aplicações Adicionar,** clique em Selecionar o ficheiro de pacote de **aplicativos**. 
2. No painel **Ficheiro de pacote de aplicação**, selecione o botão Procurar. Em seguida, selecione um ficheiro de instalação iOS com a extensão **.ipa**.
   Os detalhes da aplicação serão apresentados.
3. Quando terminar, selecione **OK** no painel de **ficheiros** do pacote app para adicionar a aplicação.

### <a name="set-app-information"></a>Definir informações de aplicativos

1. Na página de informações da **App,** adicione os detalhes para a sua aplicação. Consoante a aplicação que tenha escolhido, alguns dos valores neste painel podem ser preenchidos automaticamente.
    - **Nome**: introduza o nome da aplicação tal como aparece no portal da empresa. Certifique-se de que todos os nomes de aplicações que utiliza são exclusivos. Se existir o mesmo nome duas vezes, só aparece uma das aplicações no portal da empresa.
    - **Descrição**: introduza a descrição da aplicação. A descrição aparece no portal da empresa.
    - **Editor**: Insira o nome do editor da app.
    - **Sistema Operativo Mínimo**: na lista, escolha a versão mínima do sistema operativo no qual a aplicação pode ser instalada. Se atribuir a aplicação a um dispositivo com um sistema operativo anterior, não será instalada.
    - **Categoria**: Selecione uma ou mais categorias de aplicações incorporadas ou selecione uma categoria que criou. As categorias permitem que os utilizadores encontrem a aplicação mais facilmente quando procurarem no portal da empresa.
    - **Mostre isto como uma aplicação em destaque no Portal da Empresa**: Mostrar a aplicação em destaque na página principal do portal da empresa quando os utilizadores navegam para apps.
    - **URL de Informações**: opcionalmente, introduza o URL de um site que contenha informações sobre esta aplicação. O URL aparece no portal da empresa.
    - **URL de Privacidade**: opcionalmente, introduza um URL para um site que contenha informações sobre a privacidade desta aplicação. O URL aparece no portal da empresa.
    - **Programador**: opcionalmente, introduza o nome do programador da aplicação.
    - **Proprietário**: opcionalmente, introduza o nome do proprietário desta aplicação. Por exemplo, **Departamento de RH**.
    - **Notas**: introduza quaisquer notas que queira associar a esta aplicação.
    - **Logótipo**: carregue um ícone associado à aplicação. Este ícone é apresentado com a aplicação quando os utilizadores procurarem no portal da empresa.
2. Clique em **Seguir** para exibir a página **de tags scope.**

## <a name="step-2---select-scope-tags-optional"></a>Passo 2 - Selecione etiquetas de âmbito (opcional)
Pode utilizar etiquetas de âmbito para determinar quem pode ver informações sobre aplicações do cliente no Intune. Para mais detalhes sobre etiquetas de âmbito, consulte [Use o controlo de acesso baseado em funções e as etiquetas](../fundamentals/scope-tags.md)de âmbito para TI distribuídos .

1. Clique em **Selecionar etiquetas** de âmbito para adicionar opcionalmente etiquetas de âmbito para a aplicação. 
2. Clique em **Seguir** para exibir a página **de Tarefas.**

## <a name="step-3---assignments"></a>Passo 3 - Atribuições

1. Selecione o **Necessário**, **Disponível para dispositivos matriculados,** **disponível com ou sem inscrição,** ou **desinstale** as atribuições do grupo para a aplicação. Para mais informações, consulte [grupos Add para organizar utilizadores e dispositivos](../fundamentals/groups-add.md) e [atribuir aplicações a grupos com](apps-deploy.md)o Microsoft Intune .
2. Clique em **Seguir** para exibir a página **Review + criar.**

## <a name="step-4---review--create"></a>Passo 4 - Rever + criar

1. Reveja os valores e configurações que inseriu para a aplicação.
2. Quando terminar, clique em **Criar** para adicionar a app ao Intune.

    A lâmina **de visão geral** para a aplicação de linha de negócio seleção é apresentada.

A aplicação criada agora aparece na lista de aplicações. Na lista, pode atribuir as aplicações aos grupos que escolher. Para obter ajuda, veja [Como atribuir aplicações a grupos](apps-deploy.md).

> [!NOTE]
> Os perfis de aprovisionamento de aplicações LOB para iOS apresentam um aviso com 30 dias de antecedência antes de expirarem.

## <a name="step-5-update-a-line-of-business-app"></a>Passo 5: atualizar uma aplicação de linha de negócio

[!INCLUDE [shared-proc-lob-updateapp](../includes/shared-proc-lob-updateapp.md)]

A atualização para a aplicação de linha de negócio sairá automaticamente instalada.

> [!NOTE]
> Para o serviço do Intune implementar com êxito um novo ficheiro IPA no dispositivo, tem de incrementar a cadeia `CFBundleVersion` no ficheiro Info.plist do pacote IPA.

## <a name="next-steps"></a>Passos seguintes

- A aplicação criada aparece na lista de aplicações. Agora pode atribuí-la aos grupos que escolher. Para obter ajuda, veja [Como atribuir aplicações a grupos](apps-deploy.md).

- Saiba mais sobre as formas como pode monitorizar as propriedades e atribuições da sua aplicação. Veja [Como monitorizar informações e atribuições da aplicação](apps-monitor.md).

- Saiba mais sobre o contexto da sua aplicação no Intune. Veja [Descrição geral dos ciclos de vida de dispositivos e aplicações](../fundamentals/device-lifecycle.md).
