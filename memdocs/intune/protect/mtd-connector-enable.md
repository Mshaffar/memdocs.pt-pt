---
title: Ativar o conector da Defesa Contra Ameaças para Dispositivos Móveis no Microsoft Intune
titleSuffix: Microsoft Intune
description: Ative o conector entre o seu parceiro de Defesa Contra Ameaças para Dispositivos Móveis (MTD) e o Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/19/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: dbb6a37e-ba47-4b69-922c-d25e66c279f6
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ee2d88e444941f2b75e6dcc716748c442de459a6
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329149"
---
# <a name="enable-the-mobile-threat-defense-connector-in-intune"></a>Ativar o conector da Defesa Contra Ameaças para Dispositivos Móveis no Intune

Durante a configuração da Mobile Threat Defense (MTD), configuraste uma política para classificar ameaças na consola de parceiros de Defesa de Ameaças Móveis e criaste a política de conformidade do dispositivo em Intune. Se já configurar o conector Intune na consola de parceiros MTD, pode agora ativar a ligação MTD para aplicações parceiras MTD.

> [!NOTE]
> Este tópico aplica-se a todos os parceiros de Defesa Contra Ameaças para Dispositivos Móveis.

## <a name="classic-conditional-access-policies-for-mtd-apps"></a>Políticas clássicas de acesso condicional para aplicações MTD

Quando integra uma nova aplicação para intune Mobile Threat Defense e permite a ligação a Intune, Intune cria uma política clássica de acesso condicional no Diretório Ativo Azure. Cada aplicação MTD que integra, incluindo [o Defender ATP](advanced-threat-protection.md) ou qualquer um dos [nossos parceiros mTD](mobile-threat-defense.md#mobile-threat-defense-partners)adicionais, cria uma nova política clássica de acesso condicional. Estas políticas podem ser ignoradas, mas não devem ser editadas, eliminadas ou desativadas.

Se a política clássica for eliminada, terá de apagar a ligação ao Intune que foi responsável pela sua criação e, em seguida, instalá-la novamente. Este processo recria a política clássica. Não é suportado para migrar políticas clássicas para aplicações MTD para o novo tipo de política para acesso condicional.

Políticas clássicas de acesso condicional para aplicações MTD:

- São utilizados pela Intune MTD para exigir que os dispositivos estejam registados em Azure AD para que tenham um ID de dispositivo antes de comunicarem com os parceiros MTD. O ID é necessário para que os dispositivos e possam reportar com sucesso o seu estado a Intune.

- Não tenha qualquer efeito em quaisquer outras aplicações ou Recursos cloud.

- São diferentes das políticas de acesso condicional que pode criar para ajudar a gerir o MTD.

- Por defeito, não interaja com outras políticas de acesso condicional que utiliza para avaliação.

Para ver as políticas clássicas de acesso condicional, em [Azure,](https://portal.azure.com/#home)vá ao **Azure Ative Directory** > **Acesso Condicional** > **Políticas Clássicas.**

## <a name="to-enable-the-mobile-threat-defense-connector"></a>Para ativar o conector de defesa de ameaças móveis

1. Inscreva-se no [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione **a administração do Inquilino** > **Conectores e fichas** > **Defesa de Ameaças Móveis.**

3. No painel de defesa de **ameaças móveis,** selecione **Adicionar**.

4. Para **configurar o conector mobile Threat Defense,** selecione a sua solução MTD na lista de drop-down.

5. Ative as opções de alternância de acordo com os requisitos da sua organização. As opções de alternância visíveis variam consoante o parceiro MTD.  Por exemplo, a seguinte imagem mostra as opções disponíveis para proteção de endpoint symantec:

   ![Configuração da MTD do Intune no portal do Azure](./media/mtd-connector-enable/enable-mtd-connector-1.png)

## <a name="mobile-threat-defense-toggle-options"></a>Opções de alternância da Defesa de Ameaças Móveis

Pode decidir quais as opções de alternância da MTD que necessita de ativar de acordo com os requisitos da sua organização. Nem todas as seguintes opções são apoiadas por todos os parceiros de Defesa de Thread Móvel:

**Definições de política de conformidade do MDM**

- **Conecte os dispositivos Android da versão _\<versões suportadas>_ _para\<nome de parceiro MTD>_** : Quando ativar esta opção, pode ter dispositivos Android 4.1+ reportando risco de segurança de volta ao Intune.

- **Conecte a versão de dispositivos iOS _\<versões suportadas>_ para _\<nome de parceiro MTD>_** : Quando ativar esta opção, pode ter dispositivos iOS 8.0+ reportando risco de segurança de volta ao Intune.

- **Ativar Sincronização de Aplicações para Dispositivos iOS**: permite que o parceiro de Defesa Contra Ameaças para Dispositivos Móveis peça metadados de aplicações iOS a partir do Intune para utilizar para fins de análise de ameaças.

- **Bloquear versões do SO não suportadas**: bloquear se o dispositivo estiver a executar um sistema operativo inferior à versão mínima suportada.

**Definições de política de proteção de aplicativos**

- **Conecte os dispositivos Android da versão *\<versões suportadas>* para *\<nome de parceiro MTD>* para avaliação**da política de proteção de aplicações : Quando ativar esta opção, as políticas de proteção de aplicações utilizando a regra do Nível de Ameaça de Dispositivo avaliarão dispositivos, incluindo dados deste conector.

- **Conecte a versão de dispositivos iOS *\<versões suportadas>* para *\<nome de parceiro MTD>* para avaliação**da política de proteção de aplicações : Quando ativar esta opção, as políticas de proteção de aplicações utilizando a regra do Nível de Ameaça de Dispositivo avaliarão dispositivos, incluindo dados deste conector.

Para saber mais sobre a utilização de conectores de defesa de ameaças móveis para avaliação da política de proteção de aplicações intune, consulte [Configurar a Defesa de Ameaças Móveis para dispositivos não matriculados](mtd-enable-unenrolled-devices.md).

**Definições comuns partilhadas**

- **Número de dias até o parceiro ficar não responsivo**: número de dias de inatividade antes de o Intune considerar o parceiro como não responsivo devido a perda da ligação. O Intune ignora o estado de conformidade para parceiros MTD não responsivos.

> [!IMPORTANT]
> Sempre que possível, recomendamos que adicione e atribua as aplicações MTD antes de criar a conformidade do dispositivo e as regras da política de acesso condicional. Isto ajuda a garantir que a aplicação MTD está pronta e disponível para os utilizadores finais instalarem antes de poderem ter acesso a e-mails ou outros recursos da empresa.

> [!TIP]
> Pode ver o **Estado da ligação** e a hora da **Última sincronização** entre o Intune e o parceiro MTD no painel de Defesa Contra Ameaças para Dispositivos Móveis.

## <a name="next-steps"></a>Próximos passos

- Crie a política de proteção de [aplicações mobile Threat Defense (MTD) com intune](mtd-app-protection-policy.md).