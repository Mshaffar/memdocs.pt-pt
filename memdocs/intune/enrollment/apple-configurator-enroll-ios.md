---
title: inscrição no dispositivo iOS/iPadOS - Apple Configurator-Setup Assistant
titleSuffix: Microsoft Intune
description: Saiba como utilizar o Configurator Apple para inscrever dispositivos iOS/iPadOS corporativos com o Assistente de Configuração.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/04/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 671e4d76-0c61-11e8-ba89-0ed5f89f718b
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b836d3d2f319ca5ec9833e5902e6fcbb94b8dd65
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83987115"
---
# <a name="set-up-iosipados-device-enrollment-with-apple-configurator"></a>Configurar a inscrição de dispositivos iOS/iPadOS com o Apple Configurator

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune suporta a inscrição de dispositivos iOS/iPadOS utilizando o [Configurator Apple](https://itunes.apple.com/app/apple-configurator-2/id1037126344) em execução num computador Mac. Inscrever-se no Configurator apple requer que ligue usb cada dispositivo iOS/iPadOS a um computador Mac para configurar a inscrição corporativa. Pode inscrever dispositivos no Intune com o Apple Configurator de duas formas:
- **Inscrição no Assistente de Configuração** – limpa o dispositivo e prepara-o para a inscrição durante o Assistente de Configuração.
- **Inscrição direta** - Não limpa o dispositivo e inscreveu o dispositivo através das definições iOS/iPadOS. Este método só suporta dispositivos **sem afinidade do utilizador**.

Os métodos de inscrição do Apple Configurator não podem ser utilizados com o [gestor de inscrições de dispositivos](device-enrollment-manager-enroll.md).

## <a name="prerequisites"></a>Pré-requisitos

- Acesso físico a dispositivos iOS/iPadOS
- [Definir autoridade do MDM](../fundamentals/mdm-authority-set.md)
- [Um certificado push de MDM da Apple](apple-mdm-push-certificate-get.md)
- Números de série dos dispositivos (apenas inscrição no Assistente de Configuração)
- Cabos de ligação USB
- Computador macOS a executar o [Apple Configurator 2.0](https://itunes.apple.com/app/apple-configurator-2/id1037126344)

## <a name="create-an-apple-configurator-profile-for-devices"></a>Criar um perfil do Apple Configurator para dispositivos

Um perfil de inscrição de dispositivos especifica as definições aplicadas durante a inscrição. Estas definições são aplicadas apenas uma vez. Siga estes passos para criar um perfil de inscrição para inscrever dispositivos iOS/iPadOS com o Configurator Apple.

1. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha **dispositivos**  >  **iOS**  >  **iOS matriculando**  >  Os perfis**configuradores apple configurator**  >  **Profiles**  >  **Create**.

    ![Criar um perfil para o Apple Configurator](./media/apple-configurator-enroll-ios/apple-config-create-profile.png)

2. Em **Criar Perfil de Inscrição**, introduza um **Nome** e uma **Descrição** para o perfil para efeitos administrativos. Os utilizadores não verão estes detalhes. Pode utilizar este campo Nome para criar um grupo dinâmico no Azure Active Directory. Utilize o nome de perfil para definir o parâmetro enrollmentProfileName para atribuir dispositivos com este perfil de inscrição. Saiba mais sobre os grupos dinâmicos do Azure Active Directory.

    ![Captura de ecrã do ecrã Criar perfil com a opção Inscrever com afinidade do utilizador selecionada](./media/apple-configurator-enroll-ios/apple-configurator-profile-create.png)

3. Na **Afinidade do Utilizador**, escolha se os dispositivos com este perfil têm de ser inscritos com ou sem um utilizador atribuído.

    - **Inscreva-se com a finidade** do utilizador - Escolha esta opção para dispositivos que pertencem aos utilizadores e que pretendam utilizar o portal da empresa para serviços como a instalação de apps. O dispositivo tem de ser afiliado a um utilizador com o Assistente de Configuração e, em seguida, pode aceder ao e-mail e aos dados da empresa. Só é suportada para a inscrição no Assistente de Configuração. A afinidade do utilizador necessita do [WS-Trust 1.3 Username/Mixed endpoint](https://technet.microsoft.com/library/adfs2-help-endpoints). [Saiba mais](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint).

    - **Inscrever sem Afinidade do Utilizador** – escolha esta opção para dispositivos não associados a um único utilizador. Utilize esta opção para dispositivos que realizem tarefas sem aceder aos dados de utilizador locais. As aplicações que requerem a filiação do utilizador (incluindo a aplicação Portal da Empresa utilizada para instalar aplicações de linha de negócio) não funcionam. Obrigatório para a inscrição direta.

     > [!NOTE]
     > Quando estiver selecionado o 'Enroll' com a finidade do **utilizador, certifique-se** de que o dispositivo está afiliado a um utilizador com o Assistente de Configuração nas primeiras 24 horas do dispositivo que está matriculado. Caso contrário, a inscrição poderá falhar e será necessário um reset de fábrica para inscrever o dispositivo.

4. Se tiver escolhido **Inscrever com Afinidade do Utilizador**, tem a opção para permitir que os utilizadores se autentiquem com o Portal da Empresa em vez do Assistente de Configuração da Apple.

    > [!NOTE]
    > Se quiser realizar alguma das seguintes ações, defina **Autenticar com o Portal da Empresa em vez do Assistente de Configuração da Apple** para **Sim**.
    >    - utilizar a autenticação multifator
    >    - pedir aos utilizadores para alterar a palavra-passe ao iniciar sessão pela primeira vez
    >    - Pedir aos utilizadores para reporem as respetivas palavras-passe expiradas durante a inscrição
    >
    > Estas ações não são suportadas durante a autenticação com o Assistente de Configuração da Apple.


6. Escolha **Criar** para guardar o perfil.

## <a name="setup-assistant-enrollment"></a>Inscrição através do Assistente de Configuração

### <a name="add-apple-configurator-serial-numbers"></a>Adicionar números de série do Apple Configurator

1. Crie uma lista de valores de duas colunas, separados por vírgulas (.csv) sem cabeçalho. Adicione o número de série na coluna da esquerda e os detalhes na coluna da direita. O máximo atual para a lista é de 5000 linhas. Num editor de texto, a lista .csv tem o seguinte aspeto:

    F7TLWCLBX196,detalhes do serviço</br>
    DLXQPCWVGHMJ,detalhes do dispositivo

   Saiba como encontrar um número de série do [dispositivo iOS/iPadOS](https://support.apple.com/HT204073).
2. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha **dispositivos**  >  **iOS**  >  **iOS matriculadispositivos**  >  **Configurator**  >  **Devices**  >  **Add**.

5. Selecione um **Perfil de inscrição** para aplicar os números de série que está a importar. Se quiser que os detalhes do novo número de série substituam quaisquer detalhes existentes, escolha **Substituir os detalhes por identificadores existentes**.
6. Em **Importar Dispositivos**, procure o ficheiro csv de números de série e selecione **Adicionar**.

### <a name="reassign-a-profile-to-device-serial-numbers"></a>Reatribuir um perfil a números de série de dispositivos

Pode atribuir um perfil de inscrição quando importar números de série iOS/iPadOS para a inscrição do Configurator da Apple. Também pode atribuir perfis a partir de dois locais no portal do Azure:
- **Dispositivos do Apple Configurator**
- **Perfis de AC**

#### <a name="assign-from-apple-configurator-devices"></a>Atribuir a partir de dispositivos do Apple Configurator
1. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha **dispositivos**  >  **iOS**  >  **iOS matriculadispositivos**  >  **configuradores apple configurator**> escolher os  >  **números** de série > perfil de **atribuição**.
2. Em **Atribuir Perfil**, escolha o **Novo perfil** que quer atribuir e, em seguida, escolha **Atribuir**.

#### <a name="assign-from-profiles"></a>Atribuir a partir de perfis
1. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha **dispositivos**  >  **iOS**  >  **iOS matriculando**  >  Os Perfis**Configuradores**da Apple  >  **Profiles** > escolher um perfil.
2. No perfil, escolha **Dispositivos atribuídos** e, em seguida, escolha **Atribuir**.
3. Filtre para encontrar os números de série dos dispositivos que pretende atribuir ao perfil, selecione os dispositivos e, em seguida, selecione **Atribuir**.

### <a name="export-the-profile"></a>Exportar o perfil
Após criar o perfil e atribuir números de série, tem de exportar o perfil do Intune como um URL. Em seguida, importe-o para o Apple Configurator num Mac para implementar em dispositivos.

1. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha **dispositivos**  >  **iOS**  >  **iOS matriculando**  >  Os perfis configuradores da Apple**Configurator**> escolher o perfil para  >  **Profiles** exportar.
2. No perfil, selecione **Exportar Perfil**.
3. Copie o **URL do Perfil**. Em seguida, pode adicioná-lo no Configurator Apple para definir o perfil Intune utilizado pelos dispositivos iOS/iPadOS.

   Em seguida, importa este perfil para o Configurator Apple no seguinte procedimento para definir o perfil Intune utilizado pelos dispositivos iOS/iPadOS.

### <a name="enroll-devices-with-setup-assistant"></a>Inscrever dispositivos com o Assistente de Configuração

1. Num computador Mac, abra o **Apple Configurator 2**. Na barra de menus, selecione **Apple Configurator 2** e selecione **Preferências**.
    > [!WARNING]
    > Os dispositivos são repostos para as configurações de fábrica durante o processo de inscrição. Como melhor prática, reponha o dispositivo e ligue-o. Os dispositivos deverão aparecer no ecrã **Hello** quando liga o dispositivo.
    > Se o dispositivo já estava registado na conta Apple ID, o dispositivo deve ser eliminado do iCloud da Apple antes de iniciar o processo de inscrição. O erro de aviso aparece como "Incapaz de ativar [nome do dispositivo]".

2. No painel de **preferências,** selecione **Servers** e escolha o símbolo plus (+) para lançar o assistente do Servidor MDM. Escolha **Seguinte**.
3. Introduza o nome ou URL do **anfitrião** e o URL de **inscrição** para o servidor MDM no âmbito da inscrição do Assistente de Configuração para dispositivos iOS/iPadOS com o Microsoft Intune. Para o URL de Inscrição, introduza o URL do perfil de inscrição exportado do Intune. Escolha **Seguinte**.  
    Pode ignorar o aviso "URL do servidor não verificado" em segurança. Para continuar, selecione **Seguinte** até que o assistente esteja concluído.
4. Ligue os dispositivos móveis iOS/iPadOS ao computador Mac com um adaptador USB.
5. Selecione os dispositivos iOS/iPadOS que pretende gerir e, em seguida, escolha **Preparar**. No painel de **dispositivos Prepare iOS/iPadOS,** selecione **Manual**, e depois escolha **Seguinte**.
6. No painel **Inscrever no Servidor MDM**, selecione o nome do servidor que criou e escolha **Seguinte**.
7. No painel **de Dispositivos De Supervisão,** selecione o nível de supervisão e, em seguida, escolha **Seguinte**.
8. No painel **Criar uma Organização**, escolha a **Organização** ou crie uma nova e escolha **Seguinte**.
9. No painel de assistente de **configuração iOS/iPadOS,** escolha os passos a apresentar ao utilizador e, em seguida, escolha **Preparar**. Se lhe for pedido, autentique para atualizar as definições de fidedignidade.  
10. Quando o dispositivo iOS/iPadOS terminar de se preparar, desligue o cabo USB.  

### <a name="distribute-devices"></a>Distribuir dispositivos
Os dispositivos estão agora prontos para a inscrição na empresa. Desligue os dispositivos e distribua-os pelos utilizadores. Quando os utilizadores ligarem os seus dispositivos, o Assistente de Configuração será iniciado.

Após os utilizadores receberem os dispositivos, os mesmos têm de concluir o Assistente de Configuração. Os dispositivos configurados com a afinidade de utilizador podem instalar e executar a aplicação do Portal da Empresa para transferir aplicações e gerir dispositivos.

## <a name="direct-enrollment"></a>Inscrição direta
Quando inscreveu diretamente dispositivos iOS/iPadOS com o Configurator Apple, pode inscrever um dispositivo sem adquirir o número de série do dispositivo. Também pode dar um nome ao dispositivo para fins de identificação antes de o Intune capturar o nome do dispositivo durante a inscrição. A aplicação Portal da Empresa não é suportada para os dispositivos inscritos diretamente. Este método não apaga o dispositivo.

As aplicações que necessitam de afiliação de utilizadores, incluindo a aplicação Portal da Empresa utilizada para instalar aplicações de linha de negócios, não podem ser instaladas.

### <a name="export-the-profile-as-mobileconfig-to-iosipados-devices"></a>Exportar o perfil como .mobileconfig para dispositivos iOS/iPadOS

1. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha **dispositivos**  >  **iOS**  >  **iOS matriculando**  >  **Perfis Configuradores**Apple > escolher o perfil para exportar > Perfil de  >  **Profiles** **Exportação**.
2. Em **Inscrição direta**, escolha **Transferir perfil** e guarde o ficheiro. Um ficheiro de perfil de inscrição só é válido durante duas semanas e, após este período de tempo, terá de voltar a criá-lo.
3. Transfira o ficheiro para um computador Mac que executa o [Configurator Apple](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) para pressionar diretamente como um perfil de gestão para dispositivos iOS/iPadOS.
4. Prepare o dispositivo com o Apple Configurator ao realizar os seguintes passos:
    1. Num computador Mac, abra o Apple Configurator 2.0.
    2. Ligue o dispositivo iOS/iPadOS ao computador Mac com um cabo USB. Feche Fotografias, o iTunes e outras aplicações que são abertas para o dispositivo quando o dispositivo é detetado.
    3. No Configurator Apple, escolha o dispositivo iOS/iPadOS conectado e, em seguida, escolha o botão **Adicionar.** As opções que podem ser adicionadas ao dispositivo aparecem na lista pendente. Selecione **Perfis**.

        ![Captura de ecrã da opção Exportar Perfil para a Inscrição no Assistente de Configuração com o URL do Perfil realçado](./media/apple-configurator-enroll-ios/ios-apple-configurator-add-profile.png)

    4. Utilize o seletor de ficheiros para selecionar o ficheiro .mobileconfig que exportou a partir do Intune e, em seguida, selecione **Adicionar**. O perfil é adicionado ao dispositivo. Se o dispositivo for Não supervisionado, a instalação exige a aceitação no dispositivo.
5. Utilize os seguintes passos para instalar o perfil no dispositivo iOS/iPadOS. O dispositivo já tem de ter concluído o Assistente de Configuração e estar pronto a utilizar. Se a inscrição implicar implementações de aplicações, o dispositivo deve ter um ID Apple configurado porque a implementação da aplicação exige que tenha um ID Apple registado na App Store.
    1. Desbloqueie o dispositivo iOS/iPadOS.
    2. Na caixa de diálogo **Instalar perfil** de **Perfil de gestão**, escolha **Instalar**.
    3. Indique o Código de Acesso do Dispositivo ou o ID Apple, se for necessário.
    4. Aceite o **Aviso** e selecione **Instalar**.
    5. Aceite o **Aviso Remoto** e selecione **Confiar**.
    6. Quando a caixa **Perfil instalado** confirmar que o perfil foi Instalado, escolha **Concluído**.

6. No dispositivo iOS/iPadOS, abra **As Definições** e vá ao Perfil **geral**de  >  **Gestão**de Dispositivos  >  **Management Profile**. Confirme que a instalação do perfil está listada e verifique as restrições de política iOS/iPadOS e aplicações instaladas. As restrições de política e as aplicações poderão demorar até 10 minutos a aparecer no dispositivo.

7. Distribua os dispositivos. O dispositivo iOS/iPadOS está agora matriculado em Intune e gerido.





