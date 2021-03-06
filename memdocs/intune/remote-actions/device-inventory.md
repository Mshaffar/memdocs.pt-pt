---
title: Ver detalhes de dispositivos com o Microsoft Intune – Azure | Microsoft Docs
description: Veja os detalhes do seu dispositivo, incluindo sistemas operativos, espaço de armazenamento, fabricante e modelo. Obtenha uma lista de aplicações instaladas, verifique as políticas de conformidade e configure o TeamViewer com o Microsoft Intune no Azure. Semelhante a ver o inventário dos dispositivos que gere.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/18/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: e71c6bdb-d75c-404f-8e38-24a663be81c2
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3c8b8599c7b207900d6e4a14b7580a324a238dfe
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989900"
---
# <a name="see-device-details-in-intune"></a>Consultar os detalhes do dispositivo no Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

A funcionalidade **Dispositivos** fornece detalhes adicionais para os dispositivos que gere, incluindo o respetivo hardware e as aplicações instaladas.

Este artigo mostra como ver todos os seus dispositivos e as respetivas propriedades no portal do Azure.

## <a name="view-the-device-details"></a>Ver os detalhes do dispositivo

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Selecione **Dispositivos**  >  **Todos os dispositivos** > selecione um dos seus dispositivos listados para abrir os seus dados:

   - **A visão geral** mostra o nome do dispositivo e lista algumas propriedades chave do dispositivo, como se é um dispositivo pessoal ou corporativo, número de série, utilizador primário, e muito mais. Pode fazer o seguinte no dispositivo:
      - [Extinguir](devices-wipe.md#retire)
      - [Eliminação](devices-wipe.md#wipe)
      - [Eliminar](devices-wipe.md#delete-devices-from-the-intune-portal)
      - [Bloqueio remoto](device-remote-lock.md)
      - [Sincronização](device-sync.md)
      - [Repor código de acesso](device-passcode-reset.md)
      - [Reiniciar](device-restart.md) (apenas windows)
      - [Início Fresco](device-fresh-start.md) (apenas janelas)
      - [Reset do piloto automático](/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset) (apenas para o Windows)
      - [Sondagem rápida](../configuration/device-restrictions-windows-10.md) (apenas windows 10)
      - [Digitalização completa](../configuration/device-restrictions-windows-10.md) (apenas windows 10)
      - Atualizar a inteligência de segurança do Windows Defender
      - [Rotação da chave BitLocker](https://docs.microsoft.com/mem/intune/protect/encrypt-devices#to-rotate-the-bitlocker-recovery-key)
      - [Mudar o nome de dispositivos](device-rename.md)
      - [Nova Sessão de Assistência Remota](https://docs.microsoft.com/mem/intune/remote-actions/teamviewer-support)
   - Utilize as **Propriedades** para atribuir uma [categoria de dispositivo que tenha criado](../enrollment/device-group-mapping.md) e alterar a propriedade do dispositivo para um dispositivo pessoal ou um dispositivo da empresa.
   - **O hardware** inclui muitos detalhes sobre o dispositivo, como o ID do dispositivo, sistema operativo e versão, espaço de armazenamento e mais detalhes.
   - **Aplicações detetadas**: apresenta uma lista de todas as aplicações que o Intune encontrou instaladas no dispositivo e das versões das aplicações. Para mais informações, consulte [intune aplicações descobertas.](../apps/app-discovered-apps.md)
   - **Conformidade do dispositivo**: apresenta uma lista de todas as políticas de conformidade atribuídas e indica se o dispositivo está ou não em conformidade.
   - **Configuração do dispositivo**: mostra todas as políticas de configuração de dispositivos atribuídas ao dispositivo e indica se a política foi concluída com êxito ou falhou.
   - **Configuração de aplicativos** 
   - **Configuração de segurança de ponto final**
   - **As chaves de recuperação** mostram as chaves BitLocker disponíveis encontradas para o dispositivo
   - **As aplicações geridas** listam todas as aplicações geridas que intune configuraram e implementaram para o dispositivo. 

## <a name="hardware-device-details"></a>Detalhes de dispositivos de hardware
Dependendo da transportadora utilizada pelos dispositivos, nem todos os detalhes podem ser recolhidos

> [!Note]  
> O inventário de hardware e software é atualizado no serviço Intune a cada 7 dias.

|Detalhes|Descrição|Plataforma| 
|--------------|----------------------|----|  
|Name|O nome do dispositivo.|Windows, iOS|
|Nome da gestão|O nome do dispositivo utilizado apenas na consola. Alterar este nome não irá alterar o nome no dispositivo.|Windows, iOS|
|UDID|O Identificador de Dispositivo Exclusivo do dispositivo.|Windows, iOS|
|ID de Dispositivo do Intune|Um GUID que identifica exclusivamente o dispositivo.|Windows, iOS|
|Número de série|O número de série dado pelo fabricante do dispositivo.|Windows, iOS|
|Dispositivo partilhado|Se definido como **Sim**, o dispositivo é partilhado por mais do que um utilizador.|Windows, iOS|
|Inscrição de utilizador aprovado|Se **Sim**, então o dispositivo tem o utilizador aprovado a inscrição que permite aos administradores gerir certas definições de segurança no dispositivo.|Windows, iOS|
|Sistema operativo|O sistema operativo utilizado no dispositivo.|Windows, iOS|
|Versão do sistema operativo|A versão do sistema operativo do dispositivo.|Windows, iOS|
|Idioma do sistema operativo|O idioma definido para o sistema operativo no dispositivo.|Windows, iOS|
|Número de construção|O número de construção do sistema operativo.|Android|
|Nível de patch de segurança|O nível de correção de segurança do dispositivo.|Android|
|Espaço de armazenamento total|O espaço de armazenamento total no dispositivo (em gigabytes).|Windows, iOS|
|Espaço de armazenamento livre|O espaço de armazenamento não utilizado no dispositivo (em gigabytes).|Windows, iOS|
|IMEI|A Identidade Internacional do Equipamento Móvel do dispositivo.|Windows, iOS/iPadOS, Android|
|MEID|O identificador de equipamento móvel do dispositivo.|Windows, iOS/iPadOS, Android|
|Fabricante|O fabricante do dispositivo.|Windows, iOS/iPadOS, Android|
|Modelo|O modelo do dispositivo.|Windows, iOS/iPadOS, Android|
|Número de telefone|O número de telemóvel atribuído ao dispositivo.|Windows, iOS/iPadOS, Android*|
|Operadora subscrita|A operadora sem fios do dispositivo.|Windows, iOS/iPadOS, Android|
|Tecnologia de rede móvel|O sistema de rádio utilizado pelo dispositivo.|Windows, iOS/iPadOS, Android|
|MAC Wi-Fi|O endereço MAC (Media Access Control) do dispositivo.|Windows, iOS/iPadOS, Android|
|ICCID|O Identificador de Cartão de Circuito Integrado, que é o número de identificação exclusivo de um cartão SIM.|Windows, iOS/iPadOS, Android|
|Data de inscrição|A data e hora em que o dispositivo foi inscrito no Intune.|Windows, iOS/iPadOS, Android|
|Último contacto|A data e hora em que o dispositivo foi ligado pela última vez ao Intune.|Windows, iOS/iPadOS, Android|
|Código para ignorar o bloqueio de ativação|O código que pode ser utilizado para desativar o bloqueio de ativação.|iOS|
|Azure AD registado|Se definido como **Sim**, o dispositivo é registado com o Azure Directory.|Windows, iOS/iPadOS, Android|
|Intune registado|Se **Sim,** o dispositivo está registado na Intune|Windows, iOS/iPadOS, Android|
|Conformidade|O estado de conformidade do dispositivo.|Windows, iOS/iPadOS, Android|
|EAS ativado|Se definido como **Sim**, o dispositivo é sincronizado com a caixa de correio do Exchange.|Windows, iOS/iPadOS, Android|
|ID de ativação do EAS|O identificador do Exchange ActiveSync do dispositivo.|Windows, iOS/iPadOS, Android|
|Supervisionado|Se definido como **Sim**, os administradores têm controlo avançado sobre o dispositivo.|Windows, iOS/iPadOS, Android|
|Encriptados|Se definido como **Sim**, os dados armazenados no dispositivo são encriptados.|Windows, iOS/iPadOS, Android|

> [!Note]  
> O número de telefone não é inventariado em dispositivos Android Enterprise Dedicados ou Totalmente Geridos.

## <a name="next-steps"></a>Passos seguintes
Veja o que mais pode fazer para [gerir os seus dispositivos](device-management.md) com o Intune.
