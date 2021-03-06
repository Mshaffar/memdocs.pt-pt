---
title: Resolver conflitos de políticas de GPO e do Intune
titleSuffix: Microsoft Intune
description: Saiba como resolver conflitos entre as Políticas de Grupos e as políticas de configuração do Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/01/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: e76af5b7-e933-442c-a9d3-3b42c5f5868b
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9a159d9d2cb31090fdb38ef2fc692f6af0297166
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79330685"
---
# <a name="resolve-group-policy-objects-gpo-and-microsoft-intune-policy-conflicts"></a>Resolver conflitos de políticas de Objetos de Política de Grupo (GPO) e do Microsoft Intune

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

> [!NOTE]
> As informações neste tópico aplicam-se apenas a computadores Windows que está a gerir como PCs através do cliente de software do Intune.

O Intune utiliza políticas que o ajudam a gerir definições em PCs Windows. Por exemplo, pode utilizar uma política para controlar as definições da Firewall do Windows nos PCs. Muitas das definições do Intune são semelhantes às definições que poderá configurar com a Política de Grupo do Windows. No entanto, é possível que, por vezes, os dois métodos entrem em conflito um com o outro.

Quando os conflitos acontecem, a Política de Grupo de nível de domínio tem precedência sobre a política intune, a menos que o PC não possa assinar no domínio. Neste caso, a política do Intune é aplicada ao PC cliente.

## <a name="what-to-do-if-you-are-using-group-policy"></a>O que fazer se estiver a utilizar a Política de Grupo
Certifique-se de que as políticas que aplicar não estão a ser geridas pela Política de Grupo. Para ajudar a impedir conflitos, pode utilizar um ou mais dos seguintes métodos:

- Antes de instalar o cliente do Intune, mova os seus PC para uma unidade organizacional (UO) do Active Directory que não tenha definições de Política de Grupo aplicadas. Também pode bloquear a herança da Política de Grupo em UO que contenham PC inscritos no Intune aos quais não pretenda aplicar definições da Política de Grupo.

- Utilize um filtro de grupo de segurança para restringir GPO apenas a PC que não são geridos pelo Intune.

- Desative ou remova os Objetos de Política de Grupo que estiverem em conflito com as políticas do Intune.

Para obter mais informações sobre o Active Directory e a Política de Grupo do Windows, consulte a sua Documentação do Windows Server.

## <a name="how-to-filter-existing-gpos-to-avoid-conflicts-with-intune-policy"></a>Como filtrar GPOs existentes para evitar conflitos com políticas do Intune
Se detetou GPOs com definições que estão em conflito com políticas do Intune, pode utilizar filtros de grupos de segurança para restringir esses GPOs apenas a PCs que não são geridos pelo Intune.

<!--- ### Use WMI filters
WMI filters selectively apply GPOs to computers that satisfy the conditions of a query. To apply a WMI filter, deploy a WMI class instance to all PCs in the enterprise before you enroll any PCs in the Intune service.

#### To apply WMI filters to a GPO

1. Create a management object file by copying and pasting the following into a text file, and then saving it to a convenient location as **WIT.mof**. The file contains the WMI class instance that you deploy to PCs that you want to enroll in the Intune service.

    ```
    //Beginning of MOF file.
    #pragma classflags("forceupdate")
    #pragma namespace ("\\\\.\\Root")
    instance of __Namespace
    {
       Name = "WindowsIntune";
    };

    #pragma namespace ("\\\\.\\Root\\WindowsIntune")
    [
       Description("This class defines Microsoft Intune common properties")
    ]
    class WindowsIntune_ManagedNode
    {
       [ read, Description("This defines whether Microsoft Intune Policy is enabled"): DisableOverride ToSubClass ]
       boolean WindowsIntunePolicyEnabled;
       [ read, key, Description("This property defines the version." "Example: 1.0"): ToSubClass ]
       string Version;
    };

    instance of WindowsIntune_ManagedNode
    {
       Version = "1.0";
       WindowsIntunePolicyEnabled = 1;
    };
    ```

2. Use either a startup script or Group Policy to deploy the file. The following is the deployment command for the startup script. The WMI class instance must be deployed before you enroll client PCs in the Intune service.

    **C:/Windows/System32/Wbem/MOFCOMP &lt;path to MOF file&gt;\wit.mof**

3. Run either of the following commands to create the WMI filters, depending on whether the GPO you want to filter applies to PCs that are managed by using Intune or to PCs that are not managed by using Intune.

    - For GPOs that apply to PCs that are not managed by using Intune, use the following:

        ```
        Namespace:root\WindowsIntune
        Query:  SELECT WindowsIntunePolicyEnabled FROM WindowsIntune_ManagedNode WHERE WindowsIntunePolicyEnabled=0
        ```

    - For GPOs that apply to PCs that are managed by Intune, use the following:

        ```
        Namespace:root\WindowsIntune
        Query:  SELECT WindowsIntunePolicyEnabled FROM WindowsIntune_ManagedNode WHERE WindowsIntunePolicyEnabled=1
        ```

4. Edit the GPO in the Group Policy Management console to apply the WMI filter that you created in the previous step.

    - For GPOs that should apply only to PCs that you want to manage by using Intune, apply the filter **WindowsIntunePolicyEnabled=1**.

    - For GPOs that should apply only to PCs that you do not want to manage by using Intune, apply the filter **WindowsIntunePolicyEnabled=0**.

For more information about how to apply WMI filters in Group Policy, see the blog post [Security Filtering, WMI Filtering, and Item-level Targeting in Group Policy Preferences](https://go.microsoft.com/fwlink/?LinkId=177883). --->


Pode aplicar GPOs apenas aos grupos de segurança especificados na área **Filtragem de Segurança** da consola de Gestão de Políticas de Grupo de um GPO selecionado. Por predefinição, todos os GPOs se aplicam aos *Utilizadores Autenticados*.

- No snap-in **Utilizadores e Computadores do Active Directory**, crie um novo grupo de segurança que contenha computadores e contas de utilizador que não pretende gerir com o Intune. Por exemplo, pode dar o nome *Não Pertencentes ao Microsoft Intune*.

- Na consola de Gestão de Políticas de Grupo, no separador **Delegação** do GPO selecionado, clique com o botão direito do rato no novo grupo de segurança para delegar as permissões **Ler** e **Aplicar Política de Grupo** adequadas, tanto aos utilizadores como aos computadores no grupo de segurança. (As permissões**Aplicar Política de Grupo** estão disponíveis na caixa de diálogo **Avançadas**.)

- Em seguida, aplique o novo filtro de grupo de segurança a um GPO selecionado e remova o filtro predefinido **Utilizadores Autenticados**.

O novo grupo de segurança deve ser mantido à medida que a inscrição no serviço Intune é alterada.

## <a name="see-also"></a>Consulte também
[Gerir PCs Windows com o Microsoft Intune](manage-windows-pcs-with-microsoft-intune.md)
