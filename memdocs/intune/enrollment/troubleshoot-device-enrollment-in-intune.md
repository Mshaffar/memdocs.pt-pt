---
title: Resolver problemas de inscrição de dispositivos
titleSuffix: Microsoft Intune
description: Sugestões para problemas de resolução de problemas de problemas de problemas de inscrição de dispositivos em Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 11/09/2018
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6982ba0e-90ff-4fc4-9594-55797e504b62
ROBOTS: NOINDEX,NOFOLLOW
ms.reviewer: damionw
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic;seoapril2019
ms.collection: M365-identity-device-management
ms.openlocfilehash: ac29e27c85ad43ccc078c54dd9d5b8b659206f57
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81397769"
---
# <a name="troubleshoot-device-enrollment-in-microsoft-intune"></a>Inscrição de dispositivo de resolução de problemas no Microsoft Intune

Este artigo fornece sugestões para problemas de problemas com a [inscrição](device-enrollment.md) de dispositivos. Se estas informações não resolverem o problema, veja [Como obter suporte para o Microsoft Intune](../fundamentals/get-support.md) para ver mais formas de obter ajuda.

## <a name="initial-troubleshooting-steps"></a>Passos iniciais de resolução de problemas

Antes de iniciar a resolução de problemas, certifique-se de que configurou o Intune corretamente para permitir a inscrição. Pode ler sobre estes requisitos de configuração em:

- [Preparar a inscrição de dispositivos no Microsoft Intune](../fundamentals/setup-steps.md)
- [Configurar a gestão do iOS/iPadOS e do dispositivo Mac](ios-enroll.md)
- [Configurar a gestão de dispositivos Windows](windows-enroll.md)
- [Configurar a gestão de dispositivos Android](android-enroll.md) –não são precisos passos adicionais

Também pode confirmar que a hora e a data no dispositivo do utilizador estão definidas corretamente:

1. Reinicie o dispositivo.
2. Confirme que a data e a hora estão definidas para próximo da hora padrão de GMT (+ ou - 12 horas) para o fuso horário do utilizador final.
3. Desinstale e reinstale o portal da empresa do Intune (se aplicável).

Os utilizadores de dispositivos geridos podem recolher registos de inscrição e de diagnóstico para que possa analisá-los. Pode encontrar instruções de utilizador para recolher os registos em:

- [Enviar erros de inscrição de dispositivos Android para o seu administrador de TI](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-using-cable-android)
- [Envie erros iOS/iPadOS para o seu administrador de TI](https://docs.microsoft.com/mem/intune/user-help/send-errors-to-your-it-admin-ios)


## <a name="general-enrollment-issues"></a>Problemas de inscrição gerais
Estes problemas podem ocorrer em todas as plataformas de dispositivos.

### <a name="device-cap-reached"></a>Limite de dispositivos atingido
**Emissão:** Um utilizador recebe um erro durante a inscrição (como **portal da empresa temporariamente indisponível).**

**Resolução:**

#### <a name="check-number-of-devices-enrolled-and-allowed"></a>Verificar número de dispositivos inscritos e permitidos

Verifique se o utilizador não possui um número de dispositivos atribuídos superior ao máximo permitido ao seguir estes passos:

1. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha **restrições** > de**inscrição Dispositivos Restrições** > de**dispositivos Restrições**limite . Observe o valor apresentado na coluna **Limite de dispositivos**.

2. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha **utilizadores** > **Todos os utilizadores** > selecionem o utilizador > **Dispositivos**. Observe o número de dispositivos inscritos.

3. Se o número de dispositivos inscritos do utilizador for igual à respetiva restrição de limite de dispositivos, o utilizador não poderá inscrever mais dispositivos até:
    - [Os dispositivos existentes serem removidos](../remote-actions/devices-wipe.md) ou
    - Aumentar o limite de dispositivos ao [definir restrições de dispositivos](enrollment-restrictions-set.md).

Para evitar atingir limites de dispositivos, certifique-se de que remove os registos de dispositivos obsoletos.

> [!NOTE]
> 
> Pode evitar o limite máximo de inscrições de dispositivos com a conta Gestor de Inscrição de Dispositivos, conforme descrito em [Enroll corporate-owned devices with the Device Enrollment Manager in Microsoft Intune (Inscrever dispositivos pertencentes à empresa com o Gestor de Inscrição de Dispositivos no Microsoft Intune)](device-enrollment-manager-enroll.md).
> 
> A inscrição de uma conta de utilizador adicionada à conta Gestores de Inscrição de Dispositivos não pode ser concluída quando a política de Acesso Condicional é imposta para o início de sessão desse utilizador específico.

### <a name="company-portal-temporarily-unavailable"></a>Portal da Empresa Temporariamente Indisponível
**Problema:** os utilizadores recebem um erro **Portal da Empresa Temporariamente Indisponível** no dispositivo.

**Resolução:**

1. Remova a aplicação Portal da Empresa do Intune do dispositivo.

2. No dispositivo, abra o navegador, [https://portal.manage.microsoft.com](https://portal.manage.microsoft.com)navegue para, e experimente um login do utilizador.

3. Se o utilizador não conseguir iniciar sessão, deverá experimentar outra rede.

4. Se isso falhar, valide que as credenciais do utilizador tenham sincronizado corretamente com o Diretório Ativo Azure.

5. Se o utilizador iniciar sessão com sucesso, um dispositivo iOS/iPadOS irá pedir-lhe para instalar a aplicação Intune Company Portal e inscrever-se. Num dispositivo Android, terá de instalar manualmente a aplicação Portal da Empresa do Intune, podendo a seguir repetir a inscrição.

### <a name="mdm-authority-not-defined"></a>Autoridade de MDM não definida
**Problema:** Um utilizador recebe um erro **Autoridade de MDM não definida**.

**Resolução:**

1. Verifique se a Autoridade MDM foi [definida adequadamente](../fundamentals/mdm-authority-set.md).
    
2. Verifique se as credenciais do utilizador sincronizaram corretamente com o Diretório Ativo Azure. Pode verificar se a UPN do utilizador corresponde às informações do Diretório Ativo no centro de administração da Microsoft 365.
    Se o UPN não corresponder às informações do Active Directory:

    1. Desative o DirSync no servidor local.

    2. Elimine o utilizador sem correspondência da lista de utilizadores **Portal de Contas do Intune**.

    3. Aguarde cerca de uma hora para permitir que o serviço do Azure remova os dados incorretos.

    4. Ative novamente o DirSync e verifique se o utilizador está agora sincronizado corretamente.

### <a name="unable-to-create-policy-or-enroll-devices-if-the-company-name-contains-special-characters"></a>Não é possível criar a política ou inscrever dispositivos se o nome da empresa incluir carateres especiais
**Problema:** não é possível criar a política ou inscrever dispositivos.

**Resolução:** No [centro de administração da Microsoft 365,](https://admin.microsoft.com/)remova os caracteres especiais do nome da empresa e guarde as informações da empresa.

### <a name="unable-to-sign-in-or-enroll-devices-when-you-have-multiple-verified-domains"></a>Não é possível iniciar sessão ou inscrever dispositivos quando tem vários domínios verificados
**Problema:** este problema pode ocorrer quando adicionar um segundo domínio verificado ao seu AD FS. Os utilizadores com o sufixo de nome principal de utilizador (UPN) do segundo domínio podem não conseguir iniciar sessão nos portais ou inscrever dispositivos.


<strong>Resolução:</strong> os Clientes do Microsoft Office 365 terão de implementar uma instância separada do Serviço de Federação do AD FS 2.0 para cada sufixo se:
- utilizarem o início de sessão único (SSO) através do AD FS 2.0 e
- tiverem vários domínios de nível superior para sufixos de UPN dos utilizadores dentro da respetiva organização (por exemplo, @contoso.com ou @fabrikam.com).


Um [rollup para o AD FS 2.0](https://support.microsoft.com/kb/2607496) funciona em conjunto com o comutador <strong>SupportMultipleDomain</strong> para permitir que o servidor do AD FS suporte este cenário sem necessitar de servidores do AD FS 2.0 adicionais. Para mais informações, consulte [este blog.](https://blogs.technet.microsoft.com/abizerh/2013/02/05/supportmultipledomain-switch-when-managing-sso-to-office-365/)


## <a name="android-issues"></a>Problemas do Android

### <a name="android-enrollment-errors"></a>Erros de inscrição de dispositivos Android

A seguinte tabela indica os erros que os utilizadores finais poderão ver ao inscrever dispositivos Android no Intune.

|Mensagem de erro|Problema|Resolução|
|---|---|---|
|**O administrador de TI tem de lhe atribuir uma licença para obter acesso**<br>O seu administrador de TI ainda não lhe deu acesso para utilizar esta aplicação. Obtenha ajuda do seu administrador de TI ou tente novamente mais tarde.|Não é possível inscrever o dispositivo porque a conta do utilizador não tem a licença necessária.|Antes de os utilizadores poderem inscrever os respetivos dispositivos, é preciso que lhes tenha sido atribuída a licença necessária. Esta mensagem indica que têm o tipo de licença errado para a autoridade de gestão de dispositivos móveis. Por exemplo, verão este erro se as seguintes situações se verificarem:<ol><li>O Intune foi definido como a autoridade de gestão de dispositivos móveis</li><li>Estão a utilizar uma licença do System Center 2012 R2 Configuration Manager.</li></ol>Para obter mais informações, veja [Atribuir licenças do Intune às suas contas de utilizador](/intune/licenses-assign).|
|**O administrador de TI tem de definir a autoridade MDM**<br>Reparámos que o seu administrador de TI não definiu uma autoridade MDM. Obtenha ajuda do seu administrador de TI ou tente novamente mais tarde.|A autoridade de gestão de dispositivos móveis não foi definida.|A autoridade de gestão de dispositivos móveis não foi definida no Intune. Saiba mais sobre como [definir a autoridade de gestão de dispositivos móveis](/intune/mdm-authority-set).|


### <a name="devices-fail-to-check-in-with-the-intune-service-and-display-as-unhealthy-in-the-intune-admin-console"></a>Os dispositivos não conseguem registar com o serviço Intune e são apresentados como em "Mau estado de funcionamento" na consola de administração do Intune
**Problema:** alguns dispositivos Samsung a executar as versões Android 4.4.x e 5.x poderão deixar de fazer o registo com o serviço do Intune. Se os dispositivos não fizerem o registo:

- Não podem receber políticas, aplicações e comandos remotos a partir do serviço do Intune.
- Mostram o Estado de Gestão **Mau estado de funcionamento** na consola do administrador.
- Os utilizadores protegidos por políticas de Acesso Condicional podem perder o acesso aos recursos corporativos.

O software Samsung Smart Manager, incluído em determinados dispositivos Samsung, pode desativar o Portal da Empresa do Intune e os respetivos componentes. Quando o Portal da Empresa está num estado desativado, este não pode ser executado em segundo plano e não pode contactar o serviço do Intune.

**Resolução #1:**

Informe os utilizadores para iniciarem manualmente a aplicação Portal da Empresa. Depois de a aplicação reiniciar, o dispositivo faz o registo com o serviço do Intune.

> [!IMPORTANT]
> Abrir a aplicação Portal da Empresa manualmente é uma solução temporária, uma vez que o Samsung Smart Manager poderá desativar novamente a aplicação Portal da Empresa.

**Resolução #2:**

Informe os utilizadores para tentarem atualizar para Android 6.0. O problema da desativação não ocorre em dispositivos com Android 6.0. Para verificar se existe uma atualização, vá a **Definições** > Sobre as atualizações do**dispositivo** > **Descarregue manualmente** > siga as indicações.

**Resolução #3:**

Se a Resolução n.º 2 não funcionar, solicite aos seus utilizadores que sigam estes passos para fazer com o que o Smart Manager exclua a aplicação Portal da Empresa:

1. Inicie a aplicação Smart Manager no dispositivo.

   ![Selecione o ícone do Smart Manager no dispositivo](./media/troubleshoot-device-enrollment-in-intune/smart-manager-app-icon.png)

2. Escolha o mosaico **Bateria**.

   ![Selecione o mosaico Bateria](./media/troubleshoot-device-enrollment-in-intune/smart-manager-battery-tile.png)

3. Em **Poupança de energia da aplicação** ou **Otimização da aplicação**, selecione **Detalhes**.

   ![Selecionar Detalhes em Poupança de energia da aplicação ou Otimização da aplicação](./media/troubleshoot-device-enrollment-in-intune/smart-manager-app-power-saving-detail.png)

4. Escolha **Portal da Empresa** da lista de aplicações.

   ![Selecionar o Portal da Empresa da lista de aplicações](./media/troubleshoot-device-enrollment-in-intune/smart-manager-company-portal.png)

5. Marque **Desativado**.

   ![Selecionar Desativado na caixa de diálogo Otimização da aplicação](./media/troubleshoot-device-enrollment-in-intune/smart-manager-app-optimization-turned-off.png)

6. Em **Poupança de energia da aplicação** ou **Otimização da aplicação**, confirme que o Portal da Empresa está desativado.

   ![Confirmar que o Portal da Empresa está desativado](./media/troubleshoot-device-enrollment-in-intune/smart-manager-verify-comp-portal-turned-off.png)


### <a name="profile-installation-failed"></a>Falha na instalação do perfil
**Problema:** um utilizador recebe o erro **Falha na instalação do perfil** num dispositivo Android.

**Resolução:**

1. Confirme que foi atribuída ao utilizador uma licença adequada para a versão do serviço Intune que estiver a utilizar.

2. Confirme se o dispositivo já está inscrito noutro fornecedor de MDM.

3. Confirme se o dispositivo tem um perfil de gestão instalado.

4. Confirme que o Chrome para Android é o browser predefinido e que os cookies estão ativados.

### <a name="android-certificate-issues"></a>Problemas de certificados do Android

**Problema**: os utilizadores recebem a mensagem seguinte no dispositivo: *Não pode iniciar sessão porque está em falta um certificado obrigatório no seu dispositivo.*

**Resolução 1:**

O utilizador poderá conseguir obter o certificado em falta ao seguir as instruções em [O dispositivo tem um certificado necessário em falta](../user-help/your-device-is-missing-an-IT-required-certificate-android.md). Se o erro persistir, tente a Resolução 2.

**Resolução 2:**

Após introduzir as credenciais empresariais e ser redirecionado para o início de sessão federado, os utilizadores ainda poderão ver o erro de certificado em falta. Neste caso, o erro pode significar que um certificado intermédio está em falta no seu servidor de Serviços de Federação do Active Directory (AD FS)

O erro de certificado ocorre porque os dispositivos Android exigem que os certificados intermédios sejam incluídos num [hello do Servidor SSL](https://technet.microsoft.com/library/cc783349.aspx). Atualmente, um servidor predefinido do AD FS ou a instalação do servidor Proxy do AD FS envia apenas o certificado SSL de serviço do AD FS na resposta hello do servidor SSL ao hello do Cliente SSL.

Para corrigir o problema, importe os certificados para os Certificados dos Computadores Pessoais no servidor do AD FS ou nos proxies da seguinte forma:

1. Nos servidores ADFS e proxy, clique à direita **Start** > **Run** > **certlm.msc** para lançar a Consola de Gestão de Certificados de Máquina Local.
2. Expanda **Pessoal** e escolha **Certificados**.
3. Localize o certificado para a comunicação de serviço do AD FS (um certificado assinado publicamente) e faça duplo clique para ver as respetivas propriedades.
4. Escolha o separador Caminho de **Certificação** para ver o certificado/s-mãe do certificado.
5. Em cada certificado principal, escolha **Ver Certificado**.
6. Escolha **Detalhes** > **Copiar para arquivar...**.
7. Siga as instruções do assistente para exportar ou guardar a chave pública do certificado principal numa localização do ficheiro à sua escolha.
8. **Certificados** > de clique à direita**Todas as tarefas** > **importam**.
9. Siga as instruções do assistente para importar os certificados principais para **Computador Local\Pessoal\Certificados**.
10. Reinicie os servidores do AD FS.
11. Repita os passos acima em todos os servidores do AD FS e do proxy.

Para verificar uma instalação adequada do certificado, [https://www.digicert.com/help/](https://www.digicert.com/help/)pode utilizar a ferramenta de diagnóstico disponível em . Na caixa **de Endereços** do Servidor, introduza o FQDN do seu servidor ADFS (IE: sts.contso.com) e clique em **'Verificar Servidor**' .

**Para validar que o certificado foi instalado corretamente**:

Os passos seguintes descrevem apenas um dos vários métodos e ferramentas que pode utilizar para validar que o certificado está instalado corretamente.

1. Aceda à [ferramenta gratuita Digicert](https://www.digicert.com/help/).
2. Introduza o nome de domínio totalmente qualificado do seu servidor AD FS (por exemplo, sts.contoso.com) e selecione **CHECK SERVER**.

Se o certificado de Servidor estiver corretamente instalado, verá todas as marcas de verificação nos resultados. Se o problema acima existente, vê um X vermelho nas secções "Certificate Name Matches" e as secções "SSL Certificate is correctly Installed" do relatório.


## <a name="iosipados-issues"></a>problemas iOS/iPadOS

### <a name="iosipados-enrollment-errors"></a>erros de inscrição iOS/iPadOS
A tabela seguinte enumera erros que os utilizadores finais podem ver ao inscrever dispositivos iOS/iPadOS no Intune.

|Mensagem de erro|Problema|Resolução|
|-------------|-----|----------|
|NoEnrollmentPolicy|Nenhuma política de inscrição encontrada|Verifique se foram criados todos os pré-requisitos de inscrição, como o certificado do Apple Push Notification Service (APNs) e que "iOS/iPadOS como plataforma" está ativado. Para obter instruções, consulte [Configurar a gestão do iOS/iPadOS e do dispositivo Mac](ios-enroll.md).|
|DeviceCapReached|Já existem demasiados dispositivos móveis inscritos.|O utilizador tem de remover um dos respetivos dispositivos móveis atualmente inscritos do Portal da Empresa antes de inscrever outro. Consulte as instruções para o tipo de dispositivo que está a utilizar: [Android,](../user-help/unenroll-your-device-from-intune-android.md) [iOS/iPadOS,](../user-help/unenroll-your-device-from-intune-ios.md) [Windows](../user-help/unenroll-your-device-from-intune-windows.md).|
|APNSCertificateNotValid|Há um problema com o certificado que permite ao dispositivo móvel comunicar com a rede da sua empresa.<br /><br />|O Apple Push Notification Service (APNs) fornece um canal para contactar dispositivos iOS/iPadOS matriculados. A inscrição irá falhar e será apresentada esta mensagem se:<ul><li>Os passos para obter um certificado do APNs não foram concluídos ou</li><li>O certificado do APNs tiver expirado.</li></ul>Reveja as informações sobre como configurar utilizadores em [Sincronizar o Active Directory e adicionar utilizadores ao Intune](../fundamentals/users-add.md) e em [Organizar utilizadores e dispositivos](../fundamentals/groups-add.md).|
|AccountNotOnboarded|Há um problema com o certificado que permite ao dispositivo móvel comunicar com a rede da sua empresa.<br /><br />|O Apple Push Notification Service (APNs) fornece um canal para contactar dispositivos iOS/iPadOS matriculados. A inscrição irá falhar e será apresentada esta mensagem se:<ul><li>Os passos para obter um certificado do APNs não foram concluídos ou</li><li>O certificado do APNs tiver expirado.</li></ul>Para mais informações, reveja [Configurar a gestão iOS/iPadOS e Mac com](ios-enroll.md)a Microsoft Intune .|
|DeviceTypeNotSupported|O utilizador poderá ter tentado inscrever-se através de um dispositivo não iOS. O tipo de dispositivo móvel que está a tentar inscrever não é suportado.<br /><br />Confirme que o dispositivo está a funcionar iOS/iPadOS versão 8.0 ou posterior.<br /><br />|Certifique-se de que o dispositivo do utilizador está a executar a versão 8.0 do iOS/iPadOS.|
|UserLicenseTypeInvalid|O dispositivo não pode ser inscrito porque a sua conta de utilizador ainda não é um membro de um grupo de utilizadores necessário.<br /><br />|Para poderem inscrever os dispositivos, os utilizadores têm de ser membros do grupo de utilizadores correto. Esta mensagem indica que têm o tipo de licença errado para a autoridade de gestão de dispositivos móveis. Por exemplo, verão este erro se as seguintes situações se verificarem:<ol><li>O Intune foi definido como a autoridade de gestão de dispositivos móveis</li><li>Estão a utilizar uma licença do System Center 2012 R2 Configuration Manager.</li></ol>Reveja os seguintes artigos para obter mais informações:<br /><br />Review [Configurar a gestão iOS/iPadOS e Mac com](ios-enroll.md) o Microsoft Intune e informações sobre como configurar os utilizadores no Sync Ative [Directory e adicionar utilizadores ao Intune](../fundamentals/users-add.md) e [organizar utilizadores e dispositivos.](../fundamentals/groups-add.md)|
|MdmAuthorityNotDefined|A autoridade de gestão de dispositivos móveis não foi definida.<br /><br />|A autoridade de gestão de dispositivos móveis não foi definida no Intune.<br /><br />Reveja o primeiro item na secção "Passo 6: inscrever dispositivos móveis e instalar uma aplicação", em [Começar com uma versão de avaliação de 30 dias do Microsoft Intune](../fundamentals/free-trial-sign-up.md).|

### <a name="devices-are-inactive-or-the-admin-console-cant-communicate-with-them"></a>Os dispositivos estão inativos ou a consola de administração não consegue comunicar com os mesmos
**Problema:** os dispositivos iOS/iPadOS não estão a fazer o check-in com o serviço Intune. Os dispositivos têm de dar entrada no serviço periodicamente para manter o acesso aos recursos empresariais protegidos. Se os dispositivos não fizerem o registo:

- Não podem receber políticas, aplicações e comandos remotos a partir do serviço do Intune.
- Mostram o Estado de Gestão **Mau estado de funcionamento** na consola do administrador.
- Os utilizadores protegidos por políticas de Acesso Condicional podem perder o acesso aos recursos corporativos.

**Resolução:** partilhe as seguintes resoluções com os seus utilizadores finais para ajudá-los a recuperar o acesso aos recursos empresariais.

Quando os utilizadores iniciam a aplicação iOS/iPadOS Company Portal, pode dizer se o seu dispositivo perdeu o contacto com o Intune. Se a aplicação detetar que não existe contacto, tentará automaticamente sincronizar com o Intune para voltar a ligar-se (os utilizadores verão a notificação inline **A tentar sincronizar…** ).

  ![Notificação A tentar sincronizar](./media/troubleshoot-device-enrollment-in-intune/ios_cp_app_trying_to_sync_notification.png)

Se a sincronização for bem sucedida, vê uma notificação inline de **sincronização bem sucedida** na aplicação iOS/iPadOS Company Portal, indicando que o seu dispositivo está em estado saudável.

  ![Notificação Sincronização efetuada com êxito](./media/troubleshoot-device-enrollment-in-intune/ios_cp_app_sync_successful_notification.png)

Se a sincronização não for bem sucedida, os utilizadores vêem uma Notificação Inline **Incapaz** na aplicação iOS/iPadOS Company Portal.

  ![Notificação Não é possível sincronizar](./media/troubleshoot-device-enrollment-in-intune/ios_cp_app_unable_to_sync_notification.png)

Para resolver o problema, os utilizadores têm de selecionar o botão **Configurar**, que se encontra à direita da notificação **Não é possível sincronizar**. O botão Configurar direciona os utilizadores para o ecrã do fluxo Configuração de Acesso à Empresa, onde podem seguir as instruções para inscrever o dispositivo.

  ![Ecrã Configuração de Acesso à Empresa](./media/troubleshoot-device-enrollment-in-intune/ios_cp_app_company_access_setup.png)

Após a inscrição, os dispositivos regressam a um bom estado e recuperam o acesso aos recursos da empresa.

### <a name="verify-ws-trust-13-is-enabled"></a>Confirmar se WS-Trust 1.3 está ativado
**Edição** Dispositivos automatizados de inscrição de dispositivos (ADE) iOS/iPadOS não podem ser matriculados

A inscrição de dispositivos ADE com afinidade do utilizador requer que o Nome de Utilizador/Ponto Final Misto WS-Trust 1.3 seja ativado para solicitar fichas ao utilizador. O Active Directory ativa este ponto final por predefinição. Para obter uma lista dos pontos finais ativados, utilize o cmdlet Get-AdfsEndpoint do PowerShell e procure o ponto final de confiança/13/Nome de Utilizador Misto. Por exemplo:

      Get-AdfsEndpoint -AddressPath "/adfs/services/trust/13/UsernameMixed"

Para obter mais informações, veja [a documentação do Get-AdfsEndpoint](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint).

Para obter mais informações, veja o artigo [Práticas recomendadas para proteger os Serviços de Federação do Active Directory](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/best-practices-securing-ad-fs). Para ajuda em determinar se o Nome de Utilizador/Misto WS-Trust 1.3 está ativado no seu fornecedor de federação de identidade:
- entre em contacto com Suporte da Microsoft se utilizar o AD FS
- contacte o fornecedor de identidade de terceiros.


### <a name="profile-installation-failed"></a>Falha na instalação do perfil
**Emissão:** Um utilizador recebe um erro falhado de **instalação de Perfil** num dispositivo iOS/iPadOS.

### <a name="troubleshooting-steps-for-failed-profile-installation"></a>Passos de resolução de problemas para a falha na instalação do perfil

1. Confirme que foi atribuída ao utilizador uma licença adequada para a versão do serviço Intune que estiver a utilizar.

2. Confirme se o dispositivo já está inscrito noutro fornecedor de MDM.

3. Confirme se o dispositivo já tem um perfil de gestão instalado.

4. Navegue [https://portal.manage.microsoft.com](https://portal.manage.microsoft.com) para e tente instalar o perfil quando solicitado.

5. Confirme que o Safari para iOS/iPadOS é o navegador padrão e que os cookies estão ativados.

### <a name="users-iosipados-device-is-stuck-on-an-enrollment-screen-for-more-than-10-minutes"></a>O dispositivo iOS/iPadOS do utilizador está preso num ecrã de inscrição por mais de 10 minutos

**Problema**: um dispositivo de inscrição pode ficar bloqueado em qualquer um de dois ecrãs:
- Aguardando a configuração final de "Microsoft"
- Aplicação de Acesso Guiado indisponível. Contacte o administrador.

Este problema pode acontecer se:
- existir uma falha temporária nos serviços da Apple ou
- A inscrição do iOS/iPadOS está definida para usar fichas VPP como mostrado na tabela, mas há algo de errado com o símbolo VPP.

| Definições de inscrição | Valor |
| ---- | ---- |
| Plataforma | iOS/iPadOS |
| Afinidade de Utilizador | Inscrever com a Afinidade de Utilizador |
|Autenticar com o Portal da Empresa em vez do Assistente de Configuração da Apple | Sim |
| Instalar o Portal da Empresa com VPP | Utilizar token: endereço do token |
| Executar o Portal da Empresa no Modo de Aplicação Única até à autenticação | Sim |

**Resolução**: para corrigir o problema, tem de:
1. Determinar se existe um problema com o token VPP e corrigi-lo.
2. Identificar quais os dispositivos que estão bloqueados.
3. Apagar os dispositivos afetados.
4. Indicar ao utilizador que deve reiniciar o processo de inscrição.

#### <a name="determine-if-theres-something-wrong-with-the-vpp-token"></a>Determinar se existe um problema com o token VPP
1. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha **dispositivos** > **iOS iOS** > **inscrição Programa de** **inscrição** > > nome simbólico > **Perfis** > nome de perfil > **Gerir** > **Propriedades**.
2. Reveja as propriedades para ver se são apresentados erros semelhantes aos seguintes:
    - Este token expirou.
    - Este token está sem licenças do Portal da Empresa.
    - Este token está a ser utilizado por outro serviço.
    - Este token está a ser utilizado por outro inquilino.
    - Este token foi eliminado.
3. Corrija os problemas do token.

#### <a name="identify-which-devices-are-blocked-by-the-vpp-token"></a>Identificar quais os dispositivos que estão bloqueados pelo token de VPP
1. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha **dispositivos** > **iOS**k > programa de **inscrição** > iOS**tokens** > nome simbólico > **Dispositivos**.
2. Filtre a coluna **Estado do perfil** por **Bloqueado**.
3. Anote os números de série de todos os dispositivos que estão **Bloqueados**.

#### <a name="remotely-wipe-the-blocked-devices"></a>Apagar remotamente os dispositivos bloqueados
Depois de ter corrigido os problemas com o símbolo VPP, tem de limpar os dispositivos que estão bloqueados.
1. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha**dispositivos Todos os** >  **dispositivos** > **Série** > **de série** > **Aplicação**. 
2. Para cada dispositivo bloqueado, selecione-o na lista **Todos os dispositivos** e, em seguida, selecione **Apagar** > **Sim**.

#### <a name="tell-the-users-to-restart-the-enrollment-process"></a>Indique aos utilizadores que devem reiniciar o processo de inscrição
Depois de apagar os dispositivos bloqueados, pode indicar aos utilizadores que devem reiniciar o processo de inscrição.

## <a name="macos-issues"></a>Problemas do macOS

### <a name="macos-enrollment-errors"></a>Erros de inscrição do macOS
**Mensagem de erro 1:** *Parece que estás a usar uma máquina virtual. Certifique-se de que configura completamente a sua máquina virtual, incluindo o número de série e o modelo de hardware. Se isto não for uma máquina virtual, contacte o suporte.*  

**Error message 2:** *Estamos a ter problemas em conseguir que o seu dispositivo seja gerido. Este problema pode ser causado se estiver a usar uma máquina virtual, tiver um número de série restrito, ou se este dispositivo já estiver atribuído a outra pessoa. Saiba como resolver estes problemas ou contacte o suporte da sua empresa.*

**Problema:** esta mensagem pode ser resultado de qualquer um dos seguintes motivos:  
- Uma máquina virtual macOS (VM) não foi configurada corretamente  
- Ativou as restrições de dispositivos que necessitam que o dispositivo seja propriedade da empresa ou que tenha um número de série do dispositivo registado no Intune  
- O dispositivo já foi inscrito e continua atribuído a outra pessoa no Intune  

**Resolução:** primeiro, entre em contacto com o utilizador para determinar os problemas que estão a afetar o dispositivo. Em seguida, conclua a mais relevante das seguintes soluções:

- Se o utilizador estiver a inscrever uma VM para teste, certifique-se de que foi totalmente configurada para que o Intune possa reconhecer o respetivo número de série e modelo de hardware. Saiba mais sobre como [configurar VMs](macos-enroll.md#enroll-virtual-macos-machines-for-testing) no Intune.
- Se a sua organização ativou as restrições de inscrição que bloqueiam dispositivos macOS pessoais, tem de [adicionar o número de série do dispositivo pessoal](corporate-identifiers-add.md#manually-enter-corporate-identifiers) manualmente ao Intune.  
- Se o dispositivo continuar atribuído a outro utilizador no Intune, o proprietário anterior não utilizou a aplicação Portal da Empresa para o remover ou repor. Para limpar o registo de dispositivo obsoleto do Intune:  

    1. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)inscreva-se com as suas credenciais administrativas.
    2. Escolha **dispositivos** > **Todos os dispositivos**.  
    3. Localize o dispositivo com o problema de inscrição. Procure pelo nome do dispositivo ou Endereço MAC/HW para restringir os seus resultados.
    4. Selecione o dispositivo > **Eliminar**. Elimine todas as outras entradas associadas ao dispositivo.  

## <a name="pc-issues"></a>Problemas do PC

|Mensagem de erro|Problema|Resolução|
|---|---|---|
|**O administrador de TI tem de lhe atribuir uma licença para obter acesso**<br>O seu administrador de TI ainda não lhe deu acesso para utilizar esta aplicação. Obtenha ajuda do seu administrador de TI ou tente novamente mais tarde.|Não é possível inscrever o dispositivo porque a conta do utilizador não tem a licença necessária.|Antes de os utilizadores poderem inscrever os respetivos dispositivos, é preciso que lhes tenha sido atribuída a licença necessária. Esta mensagem indica que têm o tipo de licença errado para a autoridade de gestão de dispositivos móveis. Por exemplo, verão este erro se as seguintes situações se verificarem: <ol><li>O Intune foi definido como a autoridade de gestão de dispositivos móveis</li><li>Estão a utilizar uma licença do System Center 2012 R2 Configuration Manager.</li></ol>Consulte informações sobre [como atribuir licenças Intune às suas contas de utilizador](../fundamentals/licenses-assign.md).|

### <a name="the-machine-is-already-enrolled---error-hr-0x8007064c"></a>O computador já está inscrito - Erro hr 0x8007064c

**Problema:** a inscrição falha com o erro **O computador já está inscrito**. O registo de inscrição mostra o erro **hr 0x8007064c**.

Esta falha pode ocorrer porque o computador:

- foi anteriormente inscrito ou
- tem a imagem clonada de um computador que já tinha sido inscrito.
O certificado de conta da conta anterior ainda está presente no computador.

**Resolução:**

1. No menu **Início**, escreva **Executar** -> **MMC**.
1. Escolha adicionar **ficheiros/** > **remover snap-ins**.
1. Faça duplo clique em **Certificados**, selecione **Conta de computador** > **Seguinte** e selecione **Computador Local**.
1. Faça duplo clique em **Certificados (Computador local)** e selecione **Certificados Pessoais**.
1. Procure o certificado do Intune emitido por Sc_Online_Issuing e elimine-o, se estiver presente.
1. Elimine esta chave de registo, se existir: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\OnlineManagement regkey** e todas as subchaves.
1. Tente voltar a inscrever.
1. Se o PC ainda não conseguir fazer a inscrição, procure e elimine esta chave, se existir: **KEY_CLASSES_ROOT\Installer\Products\6985F0077D3EEB44AB6849B5D7913E95**.
1. Tente voltar a inscrever.

    > [!IMPORTANT]
    > Esta secção, método ou tarefa contém passos que indicam como modificar o registo. Poderão, no entanto, ocorrer problemas graves se modificar o registo incorretamente. Por isso, certifique-se de que segue estes passos cuidadosamente. Para proteção adicional, faça uma cópia de segurança do registo antes de o modificar. Em seguida, pode restaurar o registo se ocorrer um problema.
    > Para obter mais informações sobre como criar cópias de segurança e restaurar o registo, leia o artigo [Como fazer cópias de segurança e restaurar o registo no Windows](https://support.microsoft.com/kb/322756)

## <a name="general-enrollment-error-codes"></a>Códigos de erros de inscrição gerais

|Código de erro|Possível problema|Resolução sugerida|
|--------------|--------------------|----------------------------------------|
|0x80CF0437 |O relógio no computador cliente não está definido com a hora correta.|Certifique-se de que o relógio e o fuso horário no computador cliente estão definidos com a hora e fuso horário corretos.|
|0x80240438, 0x80CF0438, 0x80CF402C|não é possível ligar ao serviço Intune. Verifique as definições de proxy do cliente.|Certifique-se de que o Intune suporta a configuração de proxy no computador cliente. Certifique-se de que o computador cliente tem acesso à Internet.|
|0x80240438, 0x80CF0438|As definições de proxy no Internet Explorer e no Sistema Local não estão configuradas.|não é possível ligar ao serviço Intune. Verifique as definições de proxy do cliente. Certifique-se de que o Intune suporta a configuração de proxy no computador cliente. Certifique-se de que o computador cliente tem acesso à Internet.|
|0x80043001, 0x80CF3001, 0x80043004, 0x80CF3004|O pacote de inscrição está desatualizado.|Transfira e instale o pacote de software de cliente atual a partir da área de trabalho Administração .|
|0x80043002, 0x80CF3002|A conta está em modo de manutenção.|Não pode inscrever novos computadores cliente quando a conta estiver em modo de manutenção. Para ver as definições da sua conta, inicie sessão na conta.|
|0x80043003, 0x80CF3003|A conta foi eliminada.|Verifique se a sua conta e subscrição do Intune ainda estão ativas. Para ver as definições da sua conta, inicie sessão na conta.|
|0x80043005, 0x80CF3005|O computador cliente foi extinguido.|Aguarde algumas horas, remova todas as antigas versões do software de cliente do computador e, em seguida, tente instalar o software de cliente novamente.|
|0x80043006, 0x80CF3006|O número máximo de estações permitidas para a conta foi atingido.|A sua organização tem de comprar licenças adicionais para que possa inscrever mais computadores cliente no serviço.|
|0x80043007, 0x80CF3007|Não foi possível localizar o ficheiro de certificado na mesma pasta que o programa do instalador.|Extraia todos os ficheiros antes de iniciar a instalação. Não mude o nome ou a localização de nenhum dos ficheiros extraídos: todos os ficheiros têm de estar na mesma pasta ou a instalação irá falhar.|
|0x8024D015, 0x00240005, 0x80070BC2, 0x80070BC9, 0x80CFD015|O software não pode ser instalado porque existe um reinício pendente do computador cliente.|Reinicie o computador e, em seguida, tente instalar o software de cliente novamente.|
|0x80070032|Um ou mais pré-requisitos para a instalação do software de cliente não foram encontrados no computador cliente.|Certifique-se de que todas as atualizações necessárias estão instaladas no computador cliente e, em seguida, tente instalar o software de cliente novamente.|
|0x80043008, 0x80CF3008|Falha ao iniciar o serviço Microsoft Online Management Update.|Contacte o Suporte da Microsoft, conforme descrito em [How to get support for Microsoft Intune (Como obter suporte para o Microsoft Intune)](../fundamentals/get-support.md).|
|0x80043009, 0x80CF3009|O computador cliente já está inscrito no serviço.|Tem de extinguir o computador cliente para o poder inscrever novamente no serviço.|
|0x8004300B, 0x80CF300B|Não é possível executar o pacote de instalação do software de cliente porque a versão do Windows que está a ser executada no cliente não é suportada.|O Intune não suporta a versão do Windows que está a ser executada no computador cliente.|
|0xAB2|O Windows Installer não conseguiu aceder ao tempo de execução de VBScript de uma ação personalizada.|Este erro é causado por uma ação personalizada baseada em DLLs (Dynamic-Link Libraries). Ao resolver problemas com o DLL, pode ter de utilizar as ferramentas descritas no artigo [KB198038 do Suporte da Microsoft: Ferramentas Úteis para Problemas de Empacotamento e Implementação](https://support.microsoft.com/kb/198038).|
|0x80cf0440|A ligação ao ponto final do serviço foi terminada.|A conta de avaliação ou paga está suspensa. Crie uma nova conta de avaliação ou paga e volte a inscrever.|

## <a name="next-steps"></a>Passos seguintes

Se estas informações de resolução de problemas não o ajudarem, contacte o Microsoft Support conforme descrito em Como obter suporte para o [Microsoft Intune](../fundamentals/get-support.md).
