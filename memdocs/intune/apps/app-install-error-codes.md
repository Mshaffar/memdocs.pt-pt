---
title: Códigos de erro de instalação de aplicações
titleSuffix: Microsoft Intune
description: Utilize os códigos de erro de instalação da aplicação para ajudá-lo a resolver problemas de instalação de aplicações.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/27/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 98567612b31604f79339a550275e274a2c90c3a4
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79326349"
---
# <a name="intune-app-installation-error-reference"></a>Referência de erro de instalação de aplicações intonizada

Além de seguir as medidas fornecidas para resolver erros de aplicação, também pode aprender sobre erros específicos da aplicação com base nos códigos de erro devolvidos. Depois de ter combinado um código de erro, utilize a descrição e informações adicionais para ajudar a resolver o erro.

## <a name="android-app-installation-errors"></a>Erros de instalação de aplicativos Android

Esta secção menciona tanto o Administrador de Dispositivos (DA) como a Samsung Knox. Para mais informações, consulte a [inscrição](../enrollment/android-enroll-device-administrator.md) do administrador do dispositivo Android e [inscreva automaticamente dispositivos Android utilizando a Inscrição Móvel Knox da Samsung.](../enrollment/android-samsung-knox-mobile-enroll.md) 

| Código de erro (Hex) | Código de erro (dez) | Mensagem/código de erro | Descrição |
|--------------------|------------------|---------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0xC7D14FB5 | -942583883 | A aplicação falhou na instalação.  | Esta mensagem de erro é apresentada quando intune não consegue determinar a causa principal do erro de instalação da aplicação Android. Nenhuma informação foi fornecida pelo Android durante a falha. Este erro é devolvido quando o download da APK foi bem sucedido, mas a instalação da aplicação falhou. Este erro pode ocorrer mais comummente devido a um ficheiro APK mau que não pode ser instalado no dispositivo. Uma possível causa pode ser quando o Google Play Protect bloqueia a instalação da app devido a problemas de segurança.   Outra possível causa deste erro é quando um dispositivo não suporta a aplicação. Por exemplo, se a aplicação necessitar da versão API 21+ e o dispositivo tiver aversão a versão API 19. Intune devolve este erro tanto para dispositivos DA como PARA KNOX e, embora possa haver uma notificação de que os utilizadores podem clicar para voltar a tentar, se houver algum problema com a APK, nunca continuará a falhar. Se a aplicação for uma aplicação disponível, a notificação pode ser rejeitada. No entanto, se a aplicação for necessária, não pode ser descartada. |
| 0xC7D14FBA | -942583878 | A instalação da aplicação foi cancelada porque o ficheiro de instalação (APK) foi apagado após o download, mas antes da instalação.  | A APK foi transferida com êxito, mas o ficheiro foi removido do dispositivo antes de o utilizador instalar a aplicação. Isto poderia acontecer se houvesse uma grande diferença de tempo entre o download e a instalação. Por exemplo, o utilizador cancelou a instalação original, esperou e, em seguida, clicou na notificação para tentar novamente.   Esta mensagem de erro é devolvida para apenas cenários de DA. Os cenários knox podem ser feitos silenciosamente. Apresentamos uma notificação para voltar a tentar para que o utilizador possa aceitar em vez de cancelar. Se a aplicação for uma aplicação disponível, a notificação pode ser rejeitada. No entanto, se a aplicação for necessária, a notificação não pode ser dispensada. |
| 0xC7D14FBB | -942583877 | A instalação da aplicação foi cancelada porque o processo foi reiniciado durante a instalação.  | O dispositivo foi reiniciado durante o processo de instalação da APK, resultando numa instalação cancelada. Esta mensagem de erro é devolvida tanto para dispositivos DA como PARA KNOX. Intune apresenta uma notificação que os utilizadores podem clicar para voltar a tentar. No caso de se tratar de uma aplicação disponível, a notificação pode ser dispensada. No entanto, se a aplicação for necessária, a notificação não pode ser dispensada. |
| 0x87D1041C | -2016345060 | A aplicação não foi detetada após a instalação concluída com sucesso.  | O utilizador desinstalou explicitamente a aplicação. Este erro não é devolvido do cliente. É um erro apresentado quando uma aplicação é instalada a determinada altura e depois desinstalada pelo utilizador. Este erro só deverá ocorrer em aplicações necessárias. Os utilizadores podem desinstalar aplicações não necessárias. Este erro só pode ocorrer em dispositivos DA. Os dispositivos KNOX bloqueiam a desinstalação de aplicações geridas. A próxima sincronização recolocará a notificação no dispositivo para que o utilizador instale. O utilizador pode ignorar a notificação. Este erro continuará a ser reportado até que o utilizador instale a aplicação. |
| 0xC7D14FB2 | -942583886 | O download falhou devido a um erro desconhecido.  | Este erro ocorre quando a transferência falha. Este erro pode ocorrer devido a ligações lentas ou problemas de Wi-Fi. Este erro é devolvido apenas para cenários de DA. Para os cenários KNOX, o utilizador não é solicitado a instalar, isto pode ser feito em silêncio. Intune apresenta uma notificação que os utilizadores podem clicar para voltar a tentar. Se a aplicação for uma aplicação disponível, a notificação pode ser rejeitada.   No entanto, se a aplicação for necessária, a notificação não pode ser dispensada. |
| 0xC7D15078 | -942583688 | O download falhou devido a um erro desconhecido. A apólice será novamente julgada da próxima vez que o dispositivo sincronizar.  | Este erro ocorre quando a transferência falha. Este erro pode ocorrer devido a ligações lentas ou problemas de Wi-Fi. Este erro é devolvido apenas para cenários de DA. Para os cenários KNOX, o utilizador não é solicitado a instalar, isto pode ser feito em silêncio. |
| 0xC7D14FB1 | -942583887 | O utilizador final cancelou a instalação da aplicação.  | O utilizador desinstalou explicitamente a aplicação. Este erro é devolvido quando a atividade de instalação do Sistema Operativo Android FOI cancelada pelo utilizador. O utilizador premiu o botão Cancelar quando o pedido de instalação do SO foi apresentado ou ignorou o pedido. Este erro é devolvido apenas para cenários de DA. Para os cenários KNOX, o utilizador não é solicitado a instalar, isto pode ser feito em silêncio. O Intune apresenta uma notificação na qual os utilizadores podem clicar para tentar novamente. Se a aplicação for uma aplicação disponível, a notificação pode ser rejeitada. No entanto, se a aplicação for necessária, não pode ser descartada. Peça ao utilizador para não cancelar a instalação. |
| 0xC7D15015 | -942583787 | O processo de descarregamento de ficheiros foi inesperadamente interrompido.  | O SO parou o processo de transferência antes de ser concluído. Este erro pode ocorrer se o dispositivo tiver pouca bateria ou a transferência demorar demasiado tempo. Este erro só é devolvido em cenários de DA. Em cenários de KNOX, não é apresentado nenhum pedido de instalação ao utilizador e esta operação pode ser feita automaticamente. O Intune apresenta uma notificação na qual os utilizadores podem clicar para tentar novamente. Se a aplicação for uma aplicação disponível, a notificação pode ser rejeitada. No entanto, se a aplicação for necessária, não pode ser descartada. Certifique-se de que o dispositivo tem uma ligação de rede fiável. |
| 0xC7D1507C | -942583684 | O serviço de descarregamento de ficheiros foi inesperadamente interrompido. A apólice será novamente julgada da próxima vez que o dispositivo sincronizar.  | O OS terminou o processo de descarregamento antes de ser concluído. Este erro pode ocorrer se o dispositivo tiver pouca bateria ou a transferência demorar demasiado tempo. Este erro só é devolvido em cenários de DA. Em cenários de KNOX, não é apresentado nenhum pedido de instalação ao utilizador e esta operação pode ser feita automaticamente. Sincronize manualmente o dispositivo ou aguarde 24 horas e verifique o estado. |
| 0xc7d14fb8 | -942583880 | A aplicação não desinstalou.  | Este erro é uma falha genérica de desinstalação. O SISTEMA não especificou por que razão a aplicação não desinstalou. Algumas aplicações de administração não podem simplesmente ser desinstaladas. Verifique se a aplicação pode ser desinstalada manualmente e recolher os registos do Portal da Empresa caso a desinstalação falhe. |
| 0xc7d14fb7 | -942583881 | O ficheiro APK de instalação da aplicação utilizado para a atualização não corresponde à assinatura da aplicação atual no dispositivo.  | O Android OS tem a limitação de exigir que o certificado de assinatura para a versão de upgrade seja exatamente o mesmo que o cert usado para assinar a versão existente. Se o desenvolvedor não puder usar o mesmo certificado para assinar a nova versão, terá de desinstalar a aplicação existente e reimplementar a nova aplicação em vez de atualizar a app existente. |
| 0xc7d14fb9 | -942583879 | O utilizador final cancelou a instalação da aplicação.  | Instrua o utilizador a aceitar a aplicação implementada intune e a instalar a aplicação quando solicitada. |
| 0xc7d14fbc | -942583876 | A desinstalação da aplicação foi cancelada porque o processo foi reiniciado durante a instalação.  | O processo de instalação da aplicação foi encerrado pelo SISTEMA ou o dispositivo foi reiniciado.   Volte a tentar instalar e recolher registos do Portal da Empresa se este erro ocorrer novamente. |
| 0xc7d14fb6 | -942583882 | O ficheiro APK de instalação da aplicação não pode ser instalado porque não foi assinado.  | Por padrão, o Sistema Operativo Android exige que as aplicações sejam assinadas. Certifique-se de que a aplicação é assinada antes da implementação. |
| 0xC7D14FB1  | -942583887 | O utilizador final cancelou a instalação da aplicação. | O utilizador desinstalou explicitamente a aplicação. Este erro é devolvido quando a atividade de instalação do Sistema Operativo Android FOI cancelada pelo utilizador. O utilizador premiu o botão Cancelar quando o pedido de instalação do SO foi apresentado ou ignorou o pedido. Este erro é devolvido apenas para cenários de DA. Para os cenários KNOX, o utilizador não é solicitado a instalar, isto pode ser feito em silêncio. O Intune apresenta uma notificação na qual os utilizadores podem clicar para tentar novamente. Se a aplicação for uma aplicação disponível, a notificação pode ser rejeitada. No entanto, se a aplicação for necessária, não pode ser descartada. Peça ao utilizador para não cancelar a instalação. |
| 0xC7D14FB9 | -942583879 | O utilizador final cancelou a instalação da aplicação. (No pedido de aceitação) | Instrua o utilizador a aceitar a aplicação implementada intune e a instalar a aplicação quando solicitada. |

## <a name="ios-and-ipados-app-installation-errors"></a>Erros de instalação de aplicações iOS e iPadOS

As seguintes mensagens de erro e descrições fornecem detalhes sobre erros de instalação iOS/iPadOS. 

| Código de erro (Hex) | Código de erro (dez) | Mensagem/código de erro | Descrição/Dicas de resolução de problemas |
|--------------------|------------------|------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0x87D12906 | -2016335610 | Erro do Agente Apple MDM: O comando de instalação da aplicação falhou sem nenhuma razão de erro especificada. Instalação de aplicativos de retry. | O Agente MDM da Apple comunicou que o comando da instalação falhou. |
| 0x87D1313C | -2016333508 | A ligação de rede do cliente foi perdida ou interrompida. As tentativas posteriores deverão ter êxito num melhor ambiente de rede. | A ligação de rede foi perdida durante o envio do URL do serviço de transferência atualizado para o dispositivo. Mais concretamente, não foi possível encontrar um servidor com o nome de anfitrião especificado. |
| 0x87D11388 | -2016341112 | O dispositivo iOS/iPadOS está atualmente ocupado.  | O dispositivo iOS/iPadOS estava ocupado, o que resultou num erro. O dispositivo estava bloqueado. O utilizador precisa de desbloquear o dispositivo para instalar a aplicação. |
| 0x87D13B64 | -2016330908 | A instalação da aplicação falhou.  | Ocorreu uma falha ao instalar a aplicação. São necessários registos de consolas iOS/iPadOS para resolver este erro. |
| 0x87D13B66 | -2016330906 | A aplicação é gerida, mas expirou ou foi removida pelo utilizador.  | Ou o utilizador desinstalou explicitamente a aplicação, ou a aplicação expirou, mas não descarregou, ou a deteção da aplicação não corresponde à resposta do dispositivo.   Além disso, este erro pode ocorrer com base num bug de plataforma iOS/iPadOS 9.2.2. |
| 0x87D13B60 | -2016330912 | A aplicação está programada para a instalação, mas precisa de um código de resgate para concluir a transação.  | Este erro ocorre normalmente com aplicações pagas da loja iOS. |
| 0x87D1041C | -2016345060 | A aplicação não foi detetada após a instalação concluída com sucesso.  | O processo de deteção da aplicação não corresponde à resposta do dispositivo. |
| 0x87D13B62 | -2016330910 | O utilizador rejeitou a oferta de instalação da aplicação.  | Durante a instalação inicial da aplicação, o utilizador clicou em Cancelar. Peça ao utilizador que aceite o pedido de instalação da próxima vez. |
| 0x87D13B63 | -2016330909 | O utilizador rejeitou a oferta de atualizar a aplicação.  | O utilizador final clicou em cancelar durante o processo de atualização. Implemente conforme necessário ou instrua o utilizador a aceitar o pedido de atualização. |
| 0x87D103E8 | -2016345112 | Erro desconhecido  | Ocorreu um erro de instalação da aplicação desconhecido. Este é o erro resultante quando outros erros não ocorreram. |
| 0x87D13B93 | -2016330861 | Só é possível instalar aplicações VPP no iPad partilhado. | As aplicações devem ser obtidas utilizando o Apple Volume Purchase Program para instalar num iPad partilhado. |
| 0x87D13B94 | -2016330860 | Não é possível instalar aplicações quando a App Store está desativada. | A App Store deve estar ativada para que o utilizador instale a aplicação. |
| 0x87D13B95 | -2016330859 | Não consigo encontrar licença de VPP para aplicação. | Tente revogar e reatribuir a licença da aplicação. |
| 0x87D13B96 | -2016330858 | Não é possível instalar aplicações do sistema com o seu fornecedor de MDM. | A instalação de aplicações pré-instaladas pelo sistema operativo iOS/iPadOS não é um cenário suportado. |
| 0x87D13B97 | -2016330857 | Não é possível instalar aplicações quando o dispositivo está em Modo Perdido. | Toda a utilização do dispositivo está bloqueada no Modo Perdido. Desativar o Modo Perdido para instalar aplicações. |
| 0x87D13B98 | -2016330856 | Não é possível instalar aplicações quando o dispositivo está em modo quiosque. | Tente adicionar este dispositivo a um grupo de exclusão para a política de configuração do modo quiosque para instalar aplicações. |
| 0x87D13B9C | -2016330852 | Não é possível instalar aplicações de 32 bits neste dispositivo. | O dispositivo não suporta instalar aplicações de 32 bits. Tente implementar a versão de 64 bits da aplicação. |
| 0x87D13B99 | -2016330855 | O utilizador deve iniciar sessão na App Store. | O utilizador precisa de iniciar sessão na App Store antes de a aplicação poder ser instalada. |
| 0x87D13B9A | -2016330854 | Problema desconhecido. Tente novamente. | A instalação da aplicação falhou devido a uma razão desconhecida. Tente novamente mais tarde. |
| 0x87D13B9B | -2016330853 | A instalação da aplicação falhou. Intune tentará novamente da próxima vez que o dispositivo sincronizar. | A instalação da aplicação encontrou um erro do dispositivo. Sincronizar o dispositivo para tentar instalar novamente a aplicação. |
| 0x87d13b7e | -2016330882 | Atribuição de Licença falhou com erro da Apple 'Sem licenças VPP restantes'  | Este comportamento é por desígnio. Para resolver isto, compre licenças VPP adicionais ou recupere licenças de utilizadores que já não são visados. |
| 0x87d13b6e | -2016330898 | Falha de instalação de aplicações 12024: Causa desconhecida.  | A Apple não nos deu informações suficientes para determinar porque é que a instalação falhou.   Nada a relatar. |
| 0x87d13b7f | -2016330881 | A política de configuração de aplicações necessária não está presente, garantir que a política é direcionada para os mesmos grupos.  | App requer config app mas nenhum config de aplicativo é alvo. A Administração deve certificar-se de que os grupos que a app tem como alvo também têm a aplicação config necessária direcionada aos grupos. |
| 0x87d13b69 | -2016330903 | O licenciamento vPP do dispositivo só é aplicável para dispositivos iOS/iPadOS 9.0+.  | Atualização dos dispositivos iOS/iPadOS afetados para iOS/iPadOS 9.0+. |
| 0x87d13b8f | -2016330865 | A aplicação está instalada no dispositivo, mas não é gerida.  | Este erro só acontece com aplicações LOB. A aplicação foi instalada fora de Intune. Para resolver este erro, desinstale a aplicação a partir do dispositivo. Da próxima vez que o dispositivo sincronizar, o dispositivo deverá instalar a aplicação a partir de Intune. |
| 0x87d13b68 | -2016330904 | A gestão de aplicações recusada pelo utilizador recusou  | Peça ao utilizador que aceite a gestão de aplicações. |
| 0x87d1279d | -2016335971 | Erro desconhecido.  | Este erro acontece com aplicações da loja iOS, mas o cenário de erro é desconhecido. |
| 0x87D13B9D | -2016330851 | A versão mais recente da aplicação não foi atualizada a partir de uma versão anterior.  | Esta mensagem de erro é apresentada se a aplicação for instalada e gerida, mas com a versão incorreta no dispositivo. Esta situação inclui quando um dispositivo recebeu um comando para atualizar uma aplicação, mas a nova versão ainda não foi instalada e reportada de volta. Este erro será reportado para o primeiro check-in de um dispositivo após a implementação da atualização, e ocorrerá até que o dispositivo informe que a nova versão está instalada ou falha devido a um erro diferente. |
| 0x87D13B6F | -2016330897 | A sua ligação com intune cronometrada.  | Falha de validação do Manifesto da App devido à conectividade da rede (timeout) |
| 0x87D13B70 | -2016330896 | Perdeu a ligação com a Internet.  | Falha de validação do Manifesto da App devido à conectividade da rede (Não Pode Encontrar o Anfitrião) |
| 0x87D13B72 | -2016330894 | Perdeu a ligação com a Internet.  | Falha de validação do Manifesto da App devido à conectividade da rede (Ligação Perdida) |
| 0x87D13B73 | -2016330893 | Perdeu a ligação com a Internet.  | Falha de validação do Manifesto da App devido à conectividade da rede (Não Ligada à Internet) |
| 0x87D13B77 | -2016330889 | A ligação segura falhou.  | Falha de validação do Manifesto da App devido à conectividade da rede (Ligação Segura falhou) |
| 0x87D13B80 | -2016330880 | Erro de loja não pode connecttoiTunes | Instalação de apps falhou devido a falha na ligação à Loja ITunes |
| 0x87D13B9F  | -2016330849 | A App VPP tem uma atualização disponível | Este código é devolvido quando uma aplicação VPP é instalada, mas há uma versão mais recente disponível. |

## <a name="other-installation-errors"></a>Outros erros de instalação

| Código de erro (Hex) | Código de erro (dez) | Mensagem/código de erro | Descrição |
|--------------------|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0x80073CFF | -2147009281 | (erro do cliente) | Para instalar esta aplicação, tem de ter um sistema de carga lateral. Certifique-se de que o pacote de aplicações é assinado com uma assinatura fidedigna e instalado num dispositivo unificado por domínios que tem a política AllowAllTrustApps ativada, ou um dispositivo que tem uma licença de Sideloading Windows com a política AllowAllTrustApps ativada. Para mais informações, consulte embalagens de resolução de problemas, implementação e consulta de aplicações da Windows Store. |
| 0x80CF201C  | -2133909476 | (erro do cliente) | Para instalar esta aplicação, tem de ter um sistema de carga lateral. Certifique-se de que o pacote de aplicações é assinado com uma assinatura fidedigna e instalado num dispositivo unificado por domínios que tem a política AllowAllTrustApps ativada, ou um dispositivo que tem uma licença de Sideloading Windows com a política AllowAllTrustApps ativada. Para mais informações, consulte embalagens de resolução de problemas, implementação e consulta de aplicações da Windows Store. |
| 0x80073CF0 | -2147009296 | O pacote não está assinado.     O nome do publicador não corresponde ao assunto do certificado de assinatura.     Verifique se o registo do evento AppxPackagingOM está a ver se está a ser informado. Para mais informações, consulte embalagens de resolução de problemas, implementação e consulta de aplicações da Windows Store. | O pacote não podia ser aberto. Causas possíveis: |
| 0x80073CF3 | -2147009296 | O pacote de entrada entra em conflito com um pacote instalado.     Não foi encontrada uma dependência de pacote especificada.     O pacote não suporta a arquitetura de processador correta.     Verifique se há informações sobre o registo do evento AppXDeployment-Server. Para mais informações, consulte embalagens de resolução de problemas, implementação e consulta de aplicações da Windows Store. | O pacote falhou na atualização, dependência ou validação de conflitos. Causas possíveis: |
| 0x80073CFB | -2147009285 | Incremente o número da versão da aplicação, em seguida, reconstrua e reassine o pacote.     Retire a embalagem antiga para cada utilizador do sistema antes de instalar a nova embalagem.     Para mais informações, consulte embalagens de resolução de problemas, implementação e consulta de aplicações da Windows Store.      | A embalagem fornecida já está instalada e a reinstalação da embalagem está bloqueada. Poderá receber este erro se estiver a instalar uma embalagem que não seja idêntica à embalagem que já está instalada. Confirmar que a assinatura digital também faz parte do pacote. Quando um pacote é reconstruído ou re-assinado, esse pacote já não é um pouco idêntico ao pacote previamente instalado. Existem duas opções possíveis para corrigir este erro: |
| 0x87D1041C | -2016345060 | O utilizador final desinstalou a aplicação.     As informações de identidade no pacote não correspondem ao que o dispositivo reporta para aplicações erradas.     Para auto-actualização de MSIs, a versão do produto não corresponde à informação da aplicação depois de atualizada fora de Intune.     Diga ao utilizador para reinstalar a aplicação a partir do portal da empresa. Note que as aplicações necessárias serão reinstaladas automaticamente quando o dispositivo entrar em funcionação. | A instalação da aplicação foi bem sucedida, mas a aplicação não foi detetada. A aplicação foi implementada com sucesso pela Intune, e posteriormente desinstalada. As razões para a aplicação ser desinstalada incluem: |
| 0x8000FF | -2147418113 |   | Ocorreu um erro inesperado durante a instalação. Verifique os registos de instalação para obter informações adicionais. |

## <a name="next-steps"></a>Próximos passos

- Para obter informações adicionais de resolução de problemas, veja [Utilizar o portal de resolução de problemas para ajudar os utilizadores na sua empresa](../fundamentals/help-desk-operators.md). 
- Saiba mais sobre os problemas conhecidos no Microsoft Intune. Para mais informações, consulte [Intune Customer Success](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess).
- Precisa de ajuda adicional? Veja [Como obter suporte para o Microsoft Intune](../fundamentals/get-support.md).