---
title: Inscrever um dispositivo macOS fornecido pela organização para gestão | Microsoft Docs
description: Descreve como pode inscrever um dispositivo macOS no Intune que foi adquirido e fornecido pela sua organização.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/29/2018
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: japoehlm
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 4a20e1b26df1d07a80d8919f8e59e0d9117f891d
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83880269"
---
# <a name="enroll-your-organization-provided-macos-device-in-management"></a>Inscrever um dispositivo macOS fornecido pela organização para gestão

Saiba como gerir o seu novo dispositivo macOS no Intune.  

Os dispositivos que são fornecidos pela sua empresa ou escola são, muitas vezes, pré-configurados antes de os receber. A sua organização enviará estas definições pré-configuradas para o seu dispositivo depois de o ligar e iniciar sessão no mesmo pela primeira vez. Assim que a configuração do seu dispositivo terminar, terá acesso aos recursos da escola ou do trabalho.

Para iniciar a configuração da gestão, ligue o seu dispositivo e inicie sessão com as credenciais da sua conta escolar ou profissional. O resto deste artigo descreve os passos e ecrãs que irá ver à medida que avançar no Assistente de Configuração.

## <a name="what-is-apple-dep"></a>O que é o DEP da Apple?

A sua organização poderá ter comprado os respetivos dispositivos através de algo designado por *Programa de Registo de Aparelho da Apple* (DEP). O DEP da Apple permite que as organizações comprem grandes quantidades de dispositivos iOS ou macOS. Posteriormente, podem configurar e gerir esses dispositivos no respetivo fornecedor de gestão de dispositivos móveis preferido, como o Intune. Se for administrador e quiser obter mais informações sobre o DEP da Apple, veja [Inscrever automaticamente dispositivos iOS com o Programa de Registo de Aparelho da Apple](https://docs.microsoft.com/intune/enrollment/device-enrollment-program-enroll-macos).  

## <a name="get-your-device-managed"></a>Gerir o seu dispositivo

Conclua os seguintes passos para inscrever o seu dispositivo macOS para gestão. Se estiver a utilizar o seu próprio dispositivo em vez de um dispositivo fornecido pela organização, siga os passos para [dispositivos pessoais e BYOD](enroll-your-device-in-intune-macos-cp.md).  

1. Ligue o seu dispositivo macOS.
2. Escolha o seu país/região e clique **em Continuar**.  

   ![Captura do ecrã do Assistente de Configuração de dispositivos macOS "Welcome" (Bem-vindo), a mostrar uma lista dos idiomas disponíveis para seleção.](./media/macos-dep-welcome-1808.png)
3. Selecione um esquema de teclado. A lista mostra uma ou mais opções baseadas no seu país/região selecionados. Para ver todas as opções de layout, independentemente do seu país/região selecionado, clique em **Mostrar Tudo**. Quando tiver terminado, clique em **Continue** (Continuar).  

   ![Captura do ecrã do Assistente de Configuração de dispositivos macOS "Setup Assistant Keyboard" (Teclado do Assistente de Configuração), a mostrar uma lista de idiomas de teclado para seleção, a opção Show All (Mostrar Todos) desselecionada e os botões Back (Retroceder) e Continue (Continuar).](./media/macos-dep-keyboard-1808.png)  
4. Selecione a sua rede Wi-Fi. Tem de ter uma ligação à Internet para prosseguir com a configuração. Se não vir a sua rede ou tiver de estabelecer ligação através de uma rede com fios, clique em **Other Network Options** (Outras Opções de Rede). Quando terminar, clique em **Continuar**.  

   ![Captura do ecrã do Assistente de Configuração de dispositivos macOS "Select Your Wi-Fi Network screen" (Selecione a Sua Rede Wi-Fi), a mostrar uma lista das redes disponíveis. Também mostra os botões Other Network Options (Outras Opções de Rede), Back (Retroceder) e Continue (Continuar).](./media/macos-dep-wifi-1808.png)  
5. Assim que estiver ligado ao Wi-Fi, o ecrã **Remote Management** (Gestão Remota) será apresentado. A gestão remota permite que o administrador da sua organização configure remotamente o seu dispositivo com as contas, definições, aplicações e redes exigidas pela empresa. Leia a explicação da gestão remota para o ajudar a compreender a forma como o seu dispositivo é gerido. Em seguida, clique em **Continuar**.  

   ![Captura do ecrã do Assistente de Configuração de dispositivos macOS "Remote Management" (Gestão Remota), com uma explicação sobre a gestão remota e uma ligação para documentação com informações adicionais. Também mostrar os botões Back (Retroceder) e Continue (Continuar).](./media/macos-dep-remote-management-1-1808.png)  
6. Quando lhe for pedido, inicie sessão com a sua conta escolar ou profissional. Após a sua autenticação, o dispositivo irá instalar um perfil de gestão. O perfil configura e permite o seu acesso aos recursos da sua organização.  
7. Leia mais sobre o ícone de dados e privacidade da Apple, para que possa identificar mais tarde quando as suas informações pessoais estiverem a ser recolhidas. Em seguida, clique em **Continuar**.  

   ![Captura do ecrã do Assistente de Configuração de dispositivos macOS "Data & Privacy" (Dados e Privacidade), a mostrar uma imagem de duas pessoas a darem um aperto de mãos e a descrever a utilização informações pessoais por parte da Apple. Também mostra os botões Back (Retroceder) e Continue (Continuar).](./media/macos-dep-apple-data-privacy-1808.png)  
8. Assim que o dispositivo estiver inscrito, poderá ter de concluir alguns passos adicionais. Os passos que lhe são apresentados dependem da forma como a sua organização personalizou a experiência de configuração. Estes passos podem pedir-lhe que:
    * Inicie sessão numa conta Apple
    * Aceite os Termos e condições
    * Crie uma conta de computador
    * Conclua uma configuração rápida
    * Configure o seu Mac

## <a name="get-the-company-portal-app"></a>Obtenha a aplicação Portal da Empresa

Transfira a aplicação Portal da Empresa do Intune para macOS no seu dispositivo. A aplicação permite-lhe monitorizar, sincronizar, adicionar e remover o seu dispositivo da gestão, bem como instalar aplicações. Estes passos também descrevem a forma como pode registar o seu dispositivo com o Portal da Empresa.

1. No seu dispositivo macOS, vá para [https://portal.manage.microsoft.com/EnrollmentRedirect.aspx](https://portal.manage.microsoft.com/EnrollmentRedirect.aspx) .
2. Inicie sessão no site do Portal da Empresa com a sua conta escolar ou profissional. 
3. Clique em **Get the App** (Obter a Aplicação) para transferir o instalador do Portal da Empresa para macOS.
4. Quando lhe for pedido, abra o ficheiro .pkg e conclua os passos de instalação.
5. Abra a aplicação Portal da Empresa e inicie sessão com a sua conta escolar ou profissional.
6. Localize o seu dispositivo e clique em **Register** (Registar).
7. Clique em **Continuar**  >  **Feito**. O seu dispositivo deverá agora aparecer na aplicação Portal da Empresa como um dispositivo empresarial e em conformidade.

Ainda precisa de ajuda? Contacte o suporte da empresa. Para encontrar as informações de contacto dele, verifique o [site do Portal da Empresa](https://go.microsoft.com/fwlink/?linkid=2010980).
