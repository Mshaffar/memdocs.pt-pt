---
title: Definições de conformidade do dispositivo iOS/iPadOS no Microsoft Intune - Azure Microsoft Docs
description: Consulte uma lista de todas as definições que pode utilizar ao definir a conformidade com os dispositivos iOS/iPadOS no Microsoft Intune. Exigir uma mensagem de e-mail, verificar dispositivos desbloqueados por jailbreak ou rooting, definir o sistema de operativo mínimo e máximo permitido, definir restrições de palavra-passe, incluindo inatividade do dispositivo e o comprimento da palavra-passe, restringir aplicações e muito mais.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/01/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 3cfb8222-d05b-49e3-ae6f-36ce1a16c61d
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 536ad36120a8fb5dc4ad0d16b8f265e56260d461
ms.sourcegitcommit: 56bb5419c41c2e150ffed0564350123135ea4592
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/02/2020
ms.locfileid: "82729262"
---
# <a name="iosipados-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>definições iOS/iPadOS para marcar dispositivos como conformes ou não conformes usando Intune

Este artigo lista e descreve as diferentes definições de conformidade que pode configurar em dispositivos iOS/iPadOS em Intune. Como parte da solução de gestão de dispositivos móveis (MDM), utilize estas definições para exigir uma mensagem de e-mail, marcar os dispositivos desbloqueados por rooting (jailbreak) como não conformes, definir um nível de ameaça permitido, definir a expiração de palavras-passe e muito mais.

Esta funcionalidade aplica-se a:

- iOS
- iPadOS

Enquanto administrador do Intune, utilize estas definições de conformidade para ajudar a proteger os recursos da sua organização. Para saber mais sobre as políticas de conformidade e para o que servem, veja a [introdução à conformidade de dispositivos](device-compliance-get-started.md).

## <a name="before-you-begin"></a>Antes de começar

[Criar uma política](create-compliance-policy.md#create-the-policy)de conformidade. Para **plataforma**, selecione **iOS/iPadOS**.

## <a name="email"></a>Email

- **Incapaz de configurar e-mail no dispositivo**  
  - **Não configurado** *(predefinido)*- Esta definição não é avaliada para conformidade ou incumprimento.
  - **Exigir** - É necessária uma conta de e-mail gerida. Se o utilizador já tiver uma conta de e-mail no dispositivo, a conta de e-mail deve ser removida para que a Intune possa configurar uma corretamente. Se não existir nenhuma conta de e-mail no dispositivo, o utilizador deve contactar o administrador de TI para configurar uma conta de e-mail gerida.

  O dispositivo é considerado não conforme nas seguintes situações:  
  - O perfil de e-mail é atribuído a um grupo de utilizadores diferente do grupo de utilizadores visado pela política de conformidade.
  - O utilizador já configurou uma conta de e-mail no dispositivo que corresponde ao perfil de e-mail do Intune implementado no dispositivo. O Intune não é capaz de substituir o perfil de utilizador configurado e não o consegue gerir. Para estar conforme, o utilizador final tem de remover as definições de e-mail existentes. Em seguida, o Intune pode instalar o perfil de e-mail gerido.  

Para obter informações sobre os perfis de e-mail, veja [configurar o acesso ao e-mail organizacional através de perfis de e-mail com o Intune](../configuration/email-settings-configure.md).

## <a name="device-health"></a>Estado de Funcionamento do Dispositivo

- **Dispositivos jailbroken**  
  *Suportado para iOS 8.0 e mais tarde*

  - **Não configurado** *(predefinido)*- Esta definição não é avaliada para conformidade ou incumprimento.
  - **Bloco** - Mark dispositivos enraizados (jailbroken) como não conformes.  

- **Exigir que o dispositivo esteja no nível de ameaça do dispositivo ou abaixo do nível de ameaça do dispositivo**  
  *Suportado para iOS 8.0 e mais tarde*

  utilize esta definição para assumir a avaliação de riscos como uma condição para conformidade. Escolha o nível de ameaça permitido:
  - **Não configurado** *(predefinido)*- Esta definição não é avaliada para conformidade ou incumprimento.
  - **Secured** - Esta opção é a mais segura, e significa que o dispositivo não pode ter ameaças. Se forem detetadas ameaças de qualquer nível no dispositivo, o mesmo será avaliado como não conforme.
  - **Baixo** - O dispositivo é avaliado como conforme se apenas houver ameaças de baixo nível. Qualquer nível mais alto coloca o dispositivo num estado de não conforme.
  - **Médio** - O dispositivo é avaliado como conforme se as ameaças presentes no dispositivo forem de baixo ou médio nível. Se forem detetadas ameaças de nível alto no dispositivo, este será determinado como não conforme.
  - **Alta** - Esta opção é a menos segura, pois permite todos os níveis de ameaça. Poderá ser útil se utilizar esta solução apenas para fins de relatórios.

## <a name="device-properties"></a>Propriedades do Dispositivo

### <a name="operating-system-version"></a>Versão do Sistema Operativo  

- **Versão mínima do SO**  
  *Suportado para iOS 8.0 e mais tarde*

  Quando um dispositivo não cumpre o requisito de versão mínima do SO, será reportado como não conforme. É apresentada uma hiperligação com informações sobre como atualizar. O utilizador final pode optar por atualizar o dispositivo. Depois, pode aceder aos recursos da organização.

- **Versão máxima do SO**  
  *Suportado para iOS 8.0 e mais tarde*

  quando um dispositivo utiliza uma versão do SO posterior à versão na regra, o acesso aos recursos da organização é bloqueado. É pedido ao utilizador final para contactar o administrador de TI. O dispositivo não poderá aceder aos recursos da organização, enquanto a regra não for alterada para permitir a versão do SO.

- **Versão mínima de construção de Os**  
  *Suportado para iOS 8.0 e mais tarde*

  quando a Apple publica atualizações de segurança, o número da compilação é normalmente atualizado, não a versão do SO. Utilize esta funcionalidade para introduzir um número mínimo de compilação permitido no dispositivo.

- **Versão máxima de construção de Os*  
  *Suportado para iOS 8.0 e mais tarde*

  quando a Apple publica atualizações de segurança, o número da compilação é normalmente atualizado, não a versão do SO. Utilize esta funcionalidade para introduzir um número máximo de compilação permitido no dispositivo.

## <a name="system-security"></a>Segurança do sistema

### <a name="password"></a>Palavra-passe

> [!NOTE]
> Depois de uma política de conformidade ou configuração ser aplicada a um dispositivo iOS/iPadOS, os utilizadores são solicitados a definir uma senha a cada 15 minutos. Os utilizadores continuam a receber o pedido até que seja definido um código de acesso. Quando é definida uma senha para o dispositivo iOS/iPadOS, o processo de encriptação inicia-se automaticamente. O dispositivo permanece encriptado até que a senha seja desativada.

- **Palavra-passe obrigatória para desbloquear os dispositivos móveis**  
  - **Não configurado** *(predefinido)*- Esta definição não é avaliada para conformidade ou incumprimento.  
  - **Exigir** - Os utilizadores devem introduzir uma palavra-passe antes de poderem aceder ao seu dispositivo. Os dispositivos iOS/iPadOS que utilizam uma palavra-passe são encriptados.

- **Senhas simples**  
  *Suportado para iOS 8.0 e mais tarde*

  - **Não configurado** *(predefinido)*- Os utilizadores podem criar senhas simples como **1234** ou **1111**.
  - **Bloco** - Os utilizadores não podem criar senhas simples, tais como **1234** ou **1111**.

- **Comprimento mínimo da palavra-passe**  
  *Suportado para iOS 8.0 e mais tarde*

  introduza o número mínimo de dígitos ou carateres que a palavra-passe tem de ter.

- **Tipo obrigatório de palavra-passe**  
  *Suportado para iOS 8.0 e mais tarde*

  escolha se uma palavra-passe deve ter apenas carateres **Numéricos** ou se deve existir uma combinação de números e de outros carateres (**Alfanuméricos**).

- **Número de carateres não alfanuméricos na palavra-passe**  
  introduza o número mínimo de carateres especiais, como `&`, `#`, `%`, `!` e assim por diante, que têm de existir na palavra-passe.

  Definir um número mais relevado exige que o utilizador crie uma palavra-passe mais complexa.

- **Máximos minutos após bloqueio do ecrã antes da palavra-passe ser necessária**  
  *Suportado para iOS 8.0 e mais tarde*

  Especifique a rapidqual é a rapidqual após o bloqueio do ecrã antes de um utilizador introduzir uma palavra-passe para aceder ao dispositivo. As opções incluem o padrão de *Não configurado*, *Imediatamente*, e de *1 Minuto* a 4 *horas*.

- **Máximo de minutos de inatividade até o ecrã ser bloqueado**  
  Introduza o tempo de marcha lenta antes de o dispositivo trancar o ecrã. As opções incluem o padrão de *Não configurado*, *Imediatamente*, e de *1 Minuto* a *15 Minutos*.

- **Expiração da Palavra-passe (dias)**  
  *Suportado para iOS 8.0 e mais tarde*

  selecione o número de dias antes de a palavra-passe expirar e ser necessário criar uma nova.

- **Número de senhas anteriores para evitar a reutilização**  
  *Suportado para iOS 8.0 e mais tarde*

  introduza o número de palavras-passe utilizadas anteriormente que não podem ser utilizadas.

### <a name="device-security"></a>Segurança do Dispositivo

- **Aplicações restritas**  
  Pode restringir aplicações ao adicionar os respetivos IDs do pacote à política. Se um dispositivo tiver a aplicação instalada, o dispositivo será marcado como não conforme.

  - Nome da **aplicação** - Introduza um nome fácil de usar para o ajudar a identificar o ID do pacote.
  - **App Bundle ID** - Introduza o identificador de pacote único atribuído pelo fornecedor de aplicações. Para encontrar o ID do pacote, consulte [como encontrar o ID do pacote para uma aplicação iOS/iPadOS](https://support.microsoft.com/help/4294074/how-to-find-the-bundle-id-for-an-ios-app) (abre outro web site da Microsoft).  

## <a name="next-steps"></a>Passos seguintes

- [Adicionar ações para dispositivos não conformes](actions-for-noncompliance.md) e [utilizar etiquetas de âmbito para filtrar políticas](../fundamentals/scope-tags.md).
- [Monitorizar as políticas de conformidade](compliance-policy-monitor.md).
- Veja as [definições de política de conformidade para dispositivos macOS](compliance-policy-create-mac-os.md).
