---
title: Estabelecer uma ligação ao Armazém de Dados com o Power BI
titleSuffix: Microsoft Intune
description: Pode transferir um ficheiro para utilizar com o Microsoft Power BI que lhe permite carregar relatórios interativos gerados automaticamente para o seu inquilino do Microsoft Intune.
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/03/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 5E5A35D3-88F8-441B-8A0B-C5D7A1E5137B
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6dfba55c8e516e2e689513f063d56f5a43d52d9
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79331725"
---
# <a name="connect-to-the-data-warehouse-with-power-bi"></a>Estabelecer uma ligação ao Armazém de Dados com o Power BI

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Pode utilizar a aplicação de Conformidade do Power BI para carregar relatórios interativos, gerados dinamicamente para o seu inquilino do Intune. Além disso, pode carregar os dados do inquilino no Power BI através da ligação do OData. O Intune fornece definições de ligação para o seu inquilino para que possa visualizar os seguintes relatórios e gráficos de exemplo relativos ao seguinte:  

- Dispositivos
- Inscrição
- Política de proteção de aplicações
- Política de conformidade
- Perfis de configuração de dispositivos
- Atualizações de software
- Relatórios do inventário de dispositivos

Também existem tendências destacadas para a inscrição, conformidade, perfil de configuração do dispositivo e atualizações de software. Os relatórios e gráficos de exemplo aplicam filtros fáceis de utilizar à tela. Para utilizar filtros avançados, consulte o painel **Filtros** no Power BI Desktop.

Os seguintes passos mostram como transferir o ficheiro do Power BI e como utilizar a ligação de OData com o Power BI.

[!INCLUDE [reports-credential-reqs](../includes/reports-credential-reqs.md)]

## <a name="install-power-bi"></a>Instalar o Power BI

Instale a versão mais recente do [Power BI Desktop](https://aka.ms/intune/datawarehouseapi/installpowerbi). Para obter mais informações, veja [Power BI Desktop](https://powerbi.microsoft.com/desktop)

## <a name="load-the-data-and-reports-using-the-power-bi-intune-compliance-data-warehouse-app"></a>Carregar dados e relatórios com a Aplicação Data Warehouse de Conformidade do Intune do Power BI

A aplicação Power BI [Intune Compliance (Data Warehouse)](https://aka.ms/intune/datawarehouseapi/getpowerbiapp) contém informações para o seu inquilino e um conjunto de relatórios pré-construídos com base no modelo de dados do Data Warehouse.

1. Navegue na página **AppSource** da aplicação [Intune Compliance (Data Warehouse)](https://aka.ms/intune/datawarehouseapi/getpowerbiapp) para iniciar o processo de instalação.
2. Clique no botão **Get It Now** e, em seguida, clique em **Continuar**.
3. Quando for solicitado a instalação da aplicação Power BI, clique em **Instalar**.
4. Depois de concluída a instalação, clique no azulejo da aplicação **Intune Compliance (Data Warehouse).**
5. Clique no botão **Ligar.** O diálogo **Connect to Intune Compliance (Data Warehouse)** é apresentado.
6. Clique no botão **Iniciar sessão**.
7. Inicie sessão com uma conta de utilizador que tenha acesso ao Data Warehouse do Intune para o inquilino com os relatórios que pretende visualizar.
8. Para ver o painel de instrumentos incluído, clique no separador **Dashboards** e, em seguida, clique no painel de visão geral de **conformidade.**
9. Para ver todos os relatórios disponíveis, clique no separador **Relatórios** e, em seguida, clique no relatório **Compliance V1.0.** Navegue pelas páginas do relatório clicando nos separadores na parte inferior.
10. Para facilitar o acesso a estes relatórios mais tarde, clique na estrela junto ao relatório **Conformidade V1.0**. Esta ação adicionará o relatório aos seus favoritos do Power BI.

Em alternativa, pode instalar a aplicação a partir do portal do Intune:

1. Inscreva-se no portal Azure e escolha **Monitorização + Intune** > **de**Gestão . Também pode procurar recursos para o Intune.
2. Abra o painel **Configurar Data Warehouse do Intune**.
3. Selecione **Obter Aplicação do Power BI** para aceder e partilhar relatórios do Power BI previamente criados para o seu inquilino no browser.
4. Siga os passos 2-10 acima.

## <a name="load-the-data-in-power-bi-using-the-odata-link"></a>Carregue os dados no Power BI com a ligação de OData

Com um cliente autenticado no Azure AD, o URL de OData liga-se ao ponto final RESTful na API do Armazém de Dados que expõe o modelo de dados ao seu cliente de relatórios. Siga estas instruções para utilizar o Power BI Desktop para ligar e criar os seus próprios relatórios. Não está limitado ao Power BI Desktop, mas pode utilizar a sua ferramenta de análise favorita com o URL de OData fornecido. O cliente suporta autenticações OAUTH2.0 e OData v4.0 Standard.

1. Inscreva-se em [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
2. Clique em **Configurar O Armazém** de Dados Intune sob a secção **Outras tarefas** no lado direito da lâmina de visão geral. A lâmina **intune Data Warehouse** será exibida.
3. Recupere o URL de alimentação personalizado da lâmina de reporte, por exemplo:<br>
    `https://fef.{yourinfo}.manage.microsoft.com/ReportingService/DataWarehouseFEService/dates?api-version=v1.0`
4. Open **Power BI Desktop**.
5. Escolha **ficheiro** > **Obter Dados**. Selecione **Feed OData**.
6. Selecione **Básico**.
7. Escreva ou cole o **URL de OData** na caixa URL.
8. Selecione **OK**.
9. Se não tiver sido autenticado no Azure AD para o seu inquilino do cliente de ambiente de trabalho do Power BI, escreva as suas credenciais. Para obter acesso aos seus dados, tem de conceder autorização com o Azure Active Directory (Azure AD) com OAuth 2.0.  
    1. Selecione **Conta organizacional**.  
    2. Escreva o nome de utilizador e a palavra-passe.  
    3. Selecione **Iniciar sessão.**  
    4. Selecione **Ligar**.  
10. Selecione **Carregar**.

## <a name="next-steps"></a>Passos seguintes

Pode encontrar respostas a perguntas sobre o seu ambiente, como o número de dispositivos inscritos por dia durante a última semana. Pode obter informações sobre o seu inquilino do Intune e população de clientes através dos relatórios do Power BI do Data Warehouse do Intune obtido no painel do Azure. No entanto, o Intune proporciona muitas outras formas de expandir ou reutilizar os dados. O Power BI e a API do Data Warehouse do Intune fornecem funcionalidades adicionais, por exemplo:

<!-- - You can use Power BI Desktop to create additional report types with your data. For example, you could create a custom chart representing the ratio of device manufactures in your enterprise. For more information about creating custom reports with Power BI and the Intune Data Warehouse, see `BLOG POST ON POWER BI`. -->
- Os dados do inquilino estão organizados para o ajudar a extrair informações dos seus dados. Para obter mais informações sobre a forma como os dados estão organizados, veja [Modelo de Dados do Armazém de Dados](reports-ref-data-model.md).
- Também pode aceder a dados de uma interface RESTful e incorporar os dados na sua própria aplicação. Para obter mais informações, veja [Get data from the Data Warehouse API with a REST client (Obter dados a partir da API do Armazém de Dados com um cliente REST)](reports-proc-data-rest.md).
