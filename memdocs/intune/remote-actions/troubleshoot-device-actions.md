---
title: Ações de dispositivos de resolução de problemas no Microsoft Intune - Azure Microsoft Docs
description: Obtenha ajuda para resolver problemas de ação do dispositivo.
keywords: ''
author: erikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ROBOTS: ''
ms.reviewer: coferro
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2ad644d8438b23f36eccad24bee31ee92de5c040
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078856"
---
# <a name="troubleshoot-device-actions-in-intune"></a>Ações de dispositivo de resolução de problemas em Intune

A Microsoft Intune tem muitas ações que o ajudam a gerir dispositivos. Este artigo fornece respostas para algumas questões comuns que podem ajudá-lo a resolver as ações do dispositivo.

## <a name="disable-activation-lock-action"></a>Desativar a ação de bloqueio de ativação

### <a name="i-clicked-the-disable-activation-lock-action-in-the-portal-but-nothing-happened-on-the-device"></a>Clicei na ação "Desativação" no portal, mas nada aconteceu no dispositivo.
Isto era esperado. Depois de iniciar a ação de bloqueio de ativação de sactivação, intune é solicitado um código atualizado da Apple. Introduzirá manualmente o código no campo de código de acesso depois de o seu dispositivo estar no ecrã 'Bloqueio de Activação'. Este código só é válido por 15 dias, por isso certifique-se de clicar na ação e copiar o código antes de emitir a Limpeza.

### <a name="why-dont-i-see-the-disable-activation-lock-code-in-the-hardware-overview-blade-of-my-iosipados-device"></a>Por que não vejo o código de bloqueio de ativação de sactivação na lâmina de visão geral do hardware do meu dispositivo iOS/iPadOS?
As razões mais prováveis incluem:
- O código expirou e foi retirado do serviço.
- O dispositivo não é supervisionado com a Política de Restrição do Dispositivo para permitir o bloqueio de ativação.

Pode verificar o código no Graph Explorer com a seguinte consulta:

```GET - https://graph.microsoft.com/beta/deviceManagement/manageddevices('deviceId')?$select=activationLockBypassCode.```

### <a name="why-is-the-disable-activation-lock-action-greyed-out-for-my-iosipados-device"></a>Porque é que a ação de bloqueio de ativação para desativação está acinzentada para o meu dispositivo iOS/iPadOS?
As razões mais prováveis incluem: 
- O código expirou e foi retirado do serviço.
- O dispositivo não é supervisionado com a Política de Restrição do Dispositivo para permitir o bloqueio de ativação.

### <a name="is-the-disable-activation-lock-code-case-sensitive"></a>O código de bloqueio de ativação desativação é sensível?
Não. E não precisas de entrar nas traços.

## <a name="remove-devices-action"></a>Remover a ação dos dispositivos

### <a name="how-do-i-tell-who-started-a-retirewipe"></a>Como posso dizer quem começou um aposentado/limpo?
No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)aceda aos**registos** de auditoria da **administração do** > Inquilino > verificar a coluna **Iniciada por** Coluna.
Se não vir uma entrada, a pessoa mais provável de ter iniciado a ação é o utilizador do dispositivo. Provavelmente usaram a aplicação do Portal da Empresa ou portal.manage.microsoft.com.

### <a name="why-wasnt-my-application-uninstalled-after-using-retire"></a>Porque é que a minha aplicação não foi desinstalada depois de usar o Reforma?
Porque não era considerado uma aplicação gerida. Neste contexto, uma aplicação gerida é uma aplicação que foi instalada através do serviço Intune. Isto inclui:
- A aplicação foi implementada como necessário
- A aplicação foi implementada como Disponível e depois instalada pelo utilizador final a partir da App Portal da Empresa.

### <a name="why-is-wipe-grayed-out-for-android-enterprise-work-profile-devices"></a>Porque é que a Wipe está acinzentada para dispositivos Android Enterprise Work Profile?
Este comportamento está previsto. A Google não permite a Reposição de Dispositivos de Perfil de Trabalho da Fábrica do Fornecedor de MDM.

### <a name="why-can-i-sign-back-into-my-office-apps-after-my-device-was-retired"></a>Por que posso voltar a entrar nas minhas aplicações do Office depois do meu dispositivo ter sido retirado?
Porque reformar um dispositivo não revoga fichas de acesso. Pode utilizar políticas de Acesso Condicional para mitigar esta condição.

### <a name="how-can-i-monitor-a-retirewipe-action-after-it-was-issued"></a>Como posso monitorizar uma ação de aposentadoria/limpeza depois de ter sido emitida?
No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)vá aos > **registos**de auditoria da **administração do Arrendatário.**

### <a name="why-do-wipes-sometimes-show-as-pending-indefinitely"></a>Por que as toalhetes às vezes aparecem como pendentes indefinidamente?
Os dispositivos nem sempre reportam o seu estado de volta ao serviço Intune antes do reset. Então, a ação mostra como Pendente. Se confirmou que a ação foi bem sucedida, elimine o dispositivo do serviço.

### <a name="what-happens-if-i-start-a-retirewipe-on-an-offline-device-or-a-device-that-hasnt-communicated-with-the-service-in-a-while"></a>O que acontece se eu começar uma aposentadoria/limpeza num dispositivo offline ou um dispositivo que não comunica com o serviço há algum tempo?
O dispositivo permanecerá em **Estado de Aposentadoria/Limpeza Até** que o certificado DE MDM expire. O certificado de MDM tem a duração de um ano a partir da inscrição, e renova automaticamente todos os anos. Se o dispositivo fizer o check-in antes de expirar o certificado de MDM, este será retirado/limpo. Se o dispositivo não fizer o check-in antes de expirar o certificado de MDM, não poderá fazer o check-in no serviço. 180 dias após o termo do certificado MDM, o dispositivo será automaticamente removido do portal Azure.


## <a name="reset-passcode-action"></a>Redefinir a ação passcode

### <a name="why-is-the-reset-passcode-action-greyed-out-on-my-android-device-admin-enrolled-device"></a>Porque é que a ação de Reset Passcode está acinzentada no meu dispositivo Android Device Admin?
Para combater o ransom ware, a Google removeu a funcionalidade de redefinição da código de acesso no API do Dispositivo (aplica-se à versão 7.0 do Android ou dispositivos superiores).

### <a name="why-do-i-get-a-not-supported-message-when-i-issue-a-passcode-reset-to-my-android-80-or-later-work-profile-enrolled-device"></a>Porque recebo uma mensagem "Não Suportada" quando emito uma redefinição da código de acesso ao meu dispositivo inscrito no Android 8.0 ou posterior?
Porque o Token reset não foi ativado no dispositivo. Para ativar o Token de Reset:
1. Deve necessitar de uma senha de perfil de trabalho na sua Política de Configuração.
2. O utilizador final deve definir uma senha de perfil de trabalho adequada.
3. O utilizador final deve aceitar a solicitação secundária para permitir a redefinição da código de acesso.
Depois de concluídos estes passos, não deverá mais receber esta resposta.

### <a name="why-am-i-prompted-to-set-a-new-passcode-on-my-iosipados-device-when-i-issue-the-remove-passcode-action"></a>Por que sou solicitado a definir uma nova senha no meu dispositivo iOS/iPadOS quando emito a ação Remover o Código de Acesso?
Porque uma das suas políticas de conformidade requer uma senha.


## <a name="wipe-action"></a>Ação Limpar

### <a name="i-cant-restart-a-windows-10-device-after-using-the-wipe-action"></a>Não posso reiniciar um dispositivo Windows 10 depois de usar a ação de limpeza
Isto pode ser causado se utilizar o dispositivo Wipe e **continuar a limpar mesmo que os dispositivos percam energia. Se selecionar esta opção, tenha em atenção que poderá impedir que alguns dispositivos do Windows 10 voltem a funcionar.** num dispositivo Windows 10.

Isto pode ser causado quando a instalação do Windows tem uma grande corrupção que está a impedir a reinstalação do sistema operativo. Neste caso, o processo falha e deixa o sistema no Ambiente de [Recuperação]( https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference)do Windows .

### <a name="i-cant-restart-a-bitlocker-encrypted-device-after-using-the-wipe-action"></a>Não posso reiniciar um dispositivo encriptado BitLocker depois de usar a ação de limpeza
Isto pode ser causado se utilizar o dispositivo Wipe e **continuar a limpar mesmo que os dispositivos percam energia. Se selecionar esta opção, tenha em atenção que poderá impedir que alguns dispositivos do Windows 10 voltem a funcionar.** opção num dispositivo encriptado BitLocker.

Para resolver este problema, utilize meios de comunicação saqueados para reinstalar o Windows 10 no dispositivo.


## <a name="next-steps"></a>Passos seguintes

Obtenha [ajuda de suporte da Microsoft](../fundamentals/get-support.md), ou use os [fóruns comunitários](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).
