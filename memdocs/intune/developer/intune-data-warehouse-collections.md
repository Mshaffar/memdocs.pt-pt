---
title: Coleções do Armazém de Dados do Intune
titleSuffix: Microsoft Intune
description: As coleções do Armazém de Dados do Intune proporcionam detalhes relacionados com a API do Armazém de Dados.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/16/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 29f09230-dc56-43db-b599-d961967bda49
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: 997a2db8917da1443531d8446176c21db3a5dbf6
ms.sourcegitcommit: dba89b827d7f89067dfa75a421119e0c973bb747
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/20/2020
ms.locfileid: "83709456"
---
# <a name="intune-data-warehouse-collections"></a>Coleções do Armazém de Dados do Intune

As seguintes coleções do Armazém de Dados do Intune proporciona as propriedades, descrições e exemplos para coleções v1.0 das entidades da API do Armazém de Dados. 

## <a name="apprevisions"></a>appRevisions
A entidade **appRevision** apresenta uma lista de todas as versões das aplicações.

|          Propriedade          |                                      Descrição                                      |                Exemplo               |
|:--------------------------:|:-------------------------------------------------------------------------------------:|:------------------------------------:|
| AppKey                     | Identificador exclusivo da Aplicação.                                                         | 123                                  |
| ApplicationID              | Identificador exclusivo da Aplicação – semelhante à AppKey, mas esta é uma chave natural.        | b66bc706-ffff-7437-0340-032819502773 |
| Revisão                   | A versão como mencionada pelo administrador durante o carregamento do binário.                   | 2                                    |
| Título                      | Nome da aplicação.                                                                     | Excel                                |
| Publisher                  | Publicador da aplicação.                                                                 | Microsoft                            |
| UploadState                | Estado de carregamento da aplicação.                                                              | 1                                    |
| AppTypeKey                 | Referência ao AppType descrito na secção seguinte.                            | 1                                    |
| VppProgramTypeKey          | Referência ao VppProgramType descrito abaixo.                                        | 30876                                |
| HoraDaCriação               | A hora em que esta revisão foi criada.                                            | 11/23/2016 0:00                      |
| ModifiedTime               | A última vez em que algo relacionado com esta revisão foi alterado.                            | 11/23/2016 0:00                      |
| Tamanho                       | Tamanho do binário em bytes.                                                          | 120 392 000                          |
| StartDateInclusiveUTC      | Data e hora em UTC em que a revisão da Aplicação foi criada no armazém de dados.      | 11/23/2016 0:00                      |
| EndDateExclusiveUTC        | Data e hora em UTC em que a revisão desta aplicação se tornou obsoleta.                        | 11/23/2016 0:00                      |
| IsCurrent                  | Indica se a versão desta Aplicação é atual ou não no armazém de dados.         | Verdadeiro/Falso                           |
| RowLastModifiedDateTimeUTC | Data e hora em UTC em que esta versão da aplicação foi modificada pela última vez no armazém de dados. | 11/23/2016 0:00                      |

## <a name="apptypes"></a>appTypes
A entidade **appType** apresenta uma lista da origem da instalação de uma aplicação.

|   Propriedade  |        Descrição        |
|:-----------:|:-------------------------:|
| AppTypeID   | ID do tipo           |
| AppTypeKey  | Chave de substituição da chave |
| AppTypeName | Tipo de aplicação                  |

### <a name="example"></a>Exemplo

| AppTypeID |                Name               |                     Descrição                     |
|:---------:|:---------------------------------:|:---------------------------------------------------:|
| 0         | Aplicação da loja Android               | Uma aplicação da loja Android.                             |
| 1         | Aplicação LOB Android                 | Uma aplicação de linha de negócios Android.                  |
| 2         | Aplicação gerida da loja Android (MAM) | Uma aplicação da loja Android com gestão ativada. |
| 3         | Aplicação da loja iOS                   | Uma aplicação da loja iOS.                                 |
| 4         | Aplicação LOB iOS                     | Uma aplicação de linha de negócios iOS.                      |
| 5         | Aplicação da loja iOS gerida (MAM)     | Uma aplicação da loja iOS com gestão ativada.       |
| 6         | O365 Pro Plus Suite             | As Aplicações Microsoft 365 para windows 10.     |
| 7         | Aplicação Web                         | Uma aplicação Web.                                        |
| 8         | Aplicação da loja Windows Phone 8.1     | Uma aplicação da loja Windows Phone 8.1.                    |
| 9         | Aplicação da loja Windows               | Uma aplicação da loja Windows.                              |
| 10        | Aplicação LOB do Windows                | Uma aplicação de linha de negócio AppX do Windows.              |
| 11        | Windows Mobile MSI              | Uma aplicação de linha de negócios MSI.                      |
| 12        | Aplicação LOB para Windows Phone           | Uma aplicação de linha de negócio do Windows Phone.             |

## <a name="compliancepolicystatusdeviceactivities"></a>compliancePolicyStatusDeviceActivities
A tabela seguinte apresenta um resumo dos estados de atribuição de políticas de conformidade a dispositivos. Esta tabela indica a contagem de dispositivos detetados em cada estado de conformidade.

|    Propriedade   |                                                                                      Descrição                                                                                     |  Exemplo |
|:-------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:--------:|
| DateKey       | Chave da data em que o resumo da política de conformidade foi criado.                                                                                                                   | 20161204 |
| Desconhecido       | Número de dispositivos que estão offline ou que não conseguiram comunicar com o Intune ou o Azure AD por outros motivos.                                                                           | 5        |
| NotApplicable | Número de dispositivos em que as políticas de conformidade visadas pelo administrador não são aplicáveis.                                                                                     | 201      |
| Compatível     | Número de dispositivos que aplicaram com êxito uma ou mais políticas de conformidade do dispositivo visadas pelo administrador.                                                                        | 4083     |
| InGracePeriod | Número de dispositivos que não estão em conformidade, embora se encontrem no período de tolerância definido pelo administrador.                                                                                  | 57       |
| NonCompliant  | Número de dispositivos que não conseguiram aplicar uma ou mais definições de políticas de conformidade do dispositivo visadas pelo administrador ou nos quais o utilizador ainda não está a cumprir as políticas visadas pelo administrador. | 43       |
|    Erro      |    Número de dispositivos que não conseguiram comunicar com o Intune ou o Azure AD e devolveram uma mensagem de erro.                                                                          |    3     |

## <a name="compliancepolicystatusdeviceperpolicyactivities"></a>compliancePolicyStatusDevicePerPolicyActivities
A tabela seguinte apresenta um resumo dos estados de atribuição de políticas de conformidade a dispositivos por política e por tipo de política. Esta tabela indica a contagem de dispositivos detetados em cada estado de conformidade para todas as políticas de conformidade atribuídas.

|      Propriedade     |                                                                                      Descrição                                                                                     |  Exemplo |
|:-----------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:--------:|
| DateKey           | Chave da data em que o resumo da política de conformidade foi criado.                                                                                                                   | 20161219 |
| PolicyKey         | Chave da política de conformidade para a qual o resumo foi criado.                                                                                                                   | 10178    |
| PolicyPlatformKey | Chave do tipo de plataforma da política de conformidade para a qual o resumo foi criado.                                                                                            | 5        |
| Desconhecido           | Número de dispositivos que estão offline ou que não conseguiram comunicar com o Intune ou o Azure AD por outros motivos.                                                                           | 13       |
| NotApplicable     | Número de dispositivos em que as políticas de conformidade visadas pelo administrador não são aplicáveis.                                                                                     | 3        |
| Compatível         | Número de dispositivos que aplicaram com êxito uma ou mais políticas de conformidade do dispositivo visadas pelo administrador.                                                                        | 45       |
| InGracePeriod     | Número de dispositivos que não estão em conformidade, embora se encontrem no período de tolerância definido pelo administrador.                                                                                  | 3        |
| NonCompliant      | Número de dispositivos que não conseguiram aplicar uma ou mais definições de políticas de conformidade do dispositivo visadas pelo administrador ou nos quais o utilizador ainda não está a cumprir as políticas visadas pelo administrador. | 7        |
| Erro             | Número de dispositivos que não conseguiram comunicar com o Intune ou o Azure AD e devolveram uma mensagem de erro.                                                                             | 3        |
## <a name="compliancestates"></a>complianceStates

|      Propriedade      |                       Descrição                      |
|:------------------:|:------------------------------------------------------:|
| complianceStatus   | Estado de conformidade de dispositivos com mdmStatusKey       |
| complianceStateKey | Chave de conformidade para corresponder ao estado do dispositivo e de conformidade |
| complianceStateID  | O ID para corresponder a este estado de conformidade                |

### <a name="example"></a>Exemplo

|  complianceStatus  |                       Descrição                      |
|:------------------:|:------------------------------------------------------:|
|    Desconhecido         |    Desconhecido.                                                                        |
|    Compatível       |    Compatível.                                                                      |
|    Não compatível    |       O dispositivo não está em conformidade e está bloqueado a partir de recursos da empresa.             |
|    Conflito        |    Está em conflito com outras regras.                                                      |
|    Erro           |       Error.                                                                       |
|    ConfigManager   |    Gerido pelo Config Manager.                                                      |
|    InGracePeriod   |       O dispositivo não está em conformidade, mas ainda tem acesso aos recursos da empresa          |

## <a name="dates"></a>datas
A entidade **date** representa as datas que são referenciadas em múltiplas entidades do armazém de dados.

|     Propriedade    |                       Descrição                      |    Exemplo    |
|:---------------:|:------------------------------------------------------:|:-------------:|
| DateKey         | Identificador exclusivo para esta data no armazém de dados. | 20160703      |
| FullDate        | A data atual representada em formato Data/Hora completo.        | 7/3/2016 0:00 |
| DiaDaSemana       | Dia da semana                                            | 1             |
| DiaDoMês      | Dia do mês                                           | 3             |
| DayOfYear       | Dia do ano                                            | 185           |
| SemanaDoAno      | Semana do ano                                           | 28            |
| MêsDoAno     | Mês do ano                                      | 7             |
| CalendarQuarter | Trimestre civil                                       | 3             |
| CalendarYear    | Ano civil                                          | 2016          |
| DateKey         | Identificador exclusivo para esta data no armazém de dados. | 20160703      |
| FullDate        | A data atual representada em formato Data/Hora completo.        | 7/3/2016 0:00 |
| DiaDaSemana       | Dia da semana                                            | 1             |
| DiaDoMês      | Dia do mês                                           | 3             |
| DayOfYear       | Dia do ano                                            | 185           |
| SemanaDoAno      | Semana do ano                                           | 28            |
| MêsDoAno     | Mês do ano                                      | 7             |
| CalendarQuarter | Trimestre civil                                       | 3             |
| CalendarYear    | Ano civil                                          | 2016          |

## <a name="devicecategories"></a>deviceCategories

|      Propriedade      |                                    Descrição                                   |                Exemplo               |
|:------------------:|:--------------------------------------------------------------------------------:|:------------------------------------:|
| deviceCategoryID   | Identificador exclusivo para a categoria do dispositivo.                                       | fb415ba2-7c08-41f6-a5e5-685b50da2c4c |
| deviceCategoryKey  | Identificador exclusivo da categoria do dispositivo no armazém de dados – chave de substituição | 1                                    |
| deviceCategoryName | Nome a apresentar para a categoria do dispositivo.                                            | Smartphones                          |

## <a name="deviceconfigurationprofiledeviceactivities"></a>deviceConfigurationProfileDeviceActivities
A entidade **DeviceConfigurationProfileDeviceActivity** apresenta uma lista do número de dispositivos no estado com êxito, pendente, com falhas ou com erros por dia. O número reflete os Perfis de configuração de dispositivos atribuídos à entidade. Por exemplo, se um dispositivo estiver no estado com êxito em todas as políticas atribuídas, o contador de casos com êxito tem um incremento de um para esse dia. Se um dispositivo tiver dois perfis atribuídos, um no estado com êxito e outro num estado com erros, a entidade incrementa o contador do estado com êxito (Succeeded) e coloca o dispositivo no estado com erros. A entidade apresenta uma lista de quantos dispositivos estão em cada um dos estados num determinado dia nos últimos 30 dias.

|  Propriedade |                                          Descrição                                          |  Exemplo |
|:---------:|:---------------------------------------------------------------------------------------------:|:--------:|
| DateKey   | Data-chave de quando a entrada do Perfil de Configuração do Dispositivo foi registada no armazém de dados. | 20160703 |
| Pendente   | Número de Dispositivos exclusivos no estado pendente.                                                    | 123      |
| Bem-sucedido | Número de Dispositivos exclusivos no estado com êxito.                                                    | 12       |
| Erro     | Número de Dispositivos exclusivos no estado com erros.                                                      | 10       |
| Falhou    | Número de Dispositivos exclusivos no estado com falhas.                                                     | 2        |

## <a name="deviceconfigurationprofileuseractivities"></a>deviceConfigurationProfileUserActivities 
A entidade **DeviceConfigurationProfileUserActivity** apresenta uma lista do número de utilizadores no estado com êxito, pendente, com falhas ou com erros por dia. O número reflete os Perfis de configuração de dispositivos atribuídos à entidade. Por exemplo, se um utilizador estiver no estado com êxito em todas as políticas atribuídas, sobe o contador com êxito em um para esse dia. Se um utilizador tiver dois perfis atribuídos, um no estado com êxito e outro no estado com erros, é contado o utilizador no estado com erros. A entidade **DeviceConfigurationProfileUserActivity** apresenta uma lista de quantos utilizadores estão em que estado num determinado dia nos últimos 30 dias. 

| Propriedade  | Descrição  | Exemplo  |
|------------|----------------------------------------------------------------------------------------------|-----------|
| DateKey  | Data-chave de quando a entrada do Perfil de Configuração do Dispositivo foi registada no armazém de dados.  | 20160703  |
| Pendente  | Número de Utilizadores exclusivos no estado pendente.  | 123  |
| Bem-sucedido  | Número de Utilizadores exclusivos no estado com êxito.  | 12  |
| Erro  | Número de Utilizadores exclusivos no estado com erros.  | 10  |
| Falhou  | Número de Utilizadores exclusivos no estado com falhas.  | 2  |

## <a name="devicepropertyhistories"></a>devicePropertyHistories

|          Propriedade          |                                                                                      Descrição                                                                                     |
|:--------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| DateKey                    | Referência à tabela de data que indica o dia.                                                                                                                                          |
| DeviceKey                  | Identificador exclusivo do dispositivo no armazém de dados – chave de substituição. Esta é uma referência à tabela Dispositivos que contém o ID de dispositivo do Intune.                               |
| DeviceName                 | Nome do dispositivo nas plataformas que permitem atribuir um nome aos dispositivos. Noutras plataformas, o Intune cria um nome a partir de outras propriedades. O atributo não pode estar disponível para todos os dispositivos. |
| DeviceRegistrationStateKey | Chave do atributo de estado do registo do dispositivo para este dispositivo.                                                                                                                    |
| OwnerTypeKey               | Chave do atributo de tipo de proprietário para este dispositivo: corporate, personal ou unknown.                                                                                                  |
| ManagementStateKey         | Chave do estado de gestão associado a este dispositivo a indicar o estado mais recente de uma ação remota ou se foi desbloqueado por jailbreak/rooting.                                                |
| AzureADRegistered          | Se o dispositivo está registado no Azure Active Directory.                                                                                                                             |
| ComplianceStateKey         | Uma chave para o ComplianceState.                                                                                                                                                            |
| OSVersion                  | Versão do SO.                                                                                                                                                                          |
| JailBroken                 | Se o dispositivo está desbloqueado por jailbreak ou rooting.                                                                                                                                         |
| DeviceCategoryKey          | Chave do atributo da categoria do dispositivo para este dispositivo.                                                                                                                                    |


## <a name="deviceregistrationstates"></a>deviceRegistrationStates
A entidade **DeviceRegistrationState** representa o tipo de registo referenciado por outras coleções do armazém de dados. 

|           Propriedade          |                                     Descrição                                     |
|:---------------------------:|:-----------------------------------------------------------------------------------:|
| deviceRegistrationStateID   | Identificador exclusivo para o estado do registo                                            |
| deviceRegistrationStateKey  | Identificador exclusivo do estado do registo no armazém de dados – chave de substituição |
| deviceRegistrationStateName | Estado do registo                                                                  |
|    NotRegistered                     |    Não registado                                                                                                                                                                  |
|    Registado                        |       Registado                                                                                                                                                                   |
|    Revoked                           |       Este estado significa que o administrador de TI bloqueou o cliente e o cliente pode ser desbloqueado. Um dispositivo também pode estar em estado Revoked após ser apagado ou extinto.        |
|    KeyConflict                       |    Conflito de chaves                                                                                                                                                                    |
|    ApprovalPending                   |    Aprovação pendente                                                                                                                                                                |
|    CertificateReset                  |    Repor Certificado                                                                                                                                                               |
|    NotRegisteredPendingEnrollment    |    Não registado, inscrição pendente                                                                                                                                               |
|    Desconhecido                           |    Estado desconhecido                                                                                                                                                                   |

## <a name="devices"></a>dispositivos
A entidade **device** lista todos os dispositivos inscritos sob gestão e as propriedades correspondentes.

|          Propriedade          |                                                                                       Descrição                                                                                      |
|:--------------------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| DeviceKey                  | Identificador exclusivo do dispositivo no armazém de dados – chave de substituição.                                                                                                               |
| DeviceId                   | Identificador exclusivo do dispositivo.                                                                                                                                                     |
| DeviceName                 | Nome do dispositivo nas plataformas que permitem atribuir um nome aos dispositivos. Noutras plataformas, o Intune cria um nome a partir de outras propriedades. O atributo não pode estar disponível para todos os dispositivos. |
| DeviceTypeKey              | Chave do atributo de tipo de dispositivo para este dispositivo.                                                                                                                                    |
| DeviceRegistrationState    | Chave do atributo de estado do registo do cliente para este dispositivo.                                                                                                                      |
| OwnerTypeKey               | Chave do atributo de tipo de proprietário para este dispositivo: corporate, personal ou unknown.                                                                                                    |
| EnrolledDateTime           | A data e hora em que o dispositivo foi inscrito.                                                                                                                                         |
| LastSyncDateTime           | Última entrada de dispositivo conhecida com o Intune.                                                                                                                                              |
| ManagementAgentKey         | Chave do agente de gestão associado a este dispositivo.                                                                                                                             |
| ManagementStateKey         | Chave do estado de gestão associado a este dispositivo a indicar o estado mais recente de uma ação remota ou se foi desbloqueado por jailbreak/rooting.                                                |
| AzureADDeviceId            | O deviceID do Azure para este dispositivo.                                                                                                                                                  |
| AzureADRegistered          | Se o dispositivo está registado no Azure Active Directory.                                                                                                                             |
| DeviceCategoryKey          | Chave da categoria associada a este dispositivo.                                                                                                                                     |
| DeviceEnrollmentType       | Chave do tipo de inscrição associado a este dispositivo, indicando o método de inscrição.                                                                                             |
| ComplianceStateKey         | Chave do estado de Conformidade associado a este dispositivo.                                                                                                                             |
| OSVersion                  | Versão do sistema operativo do dispositivo.                                                                                                                                                |
| EasDeviceId                | Troque o ID ActiveSync do dispositivo.                                                                                                                                                  |
| SerialNumber               | SerialNumber                                                                                                                                                                           |
| IDUtilizador                     | O Identificador Exclusivo para o utilizador associado ao dispositivo.                                                                                                                           |
| RowLastModifiedDateTimeUTC | A data e hora em UTC em que este dispositivo foi modificado pela última vez no armazém de dados.                                                                                                       |
| Fabricante               | Fabricante do dispositivo                                                                                                                                                             |
| Modelo                      | Modelo do dispositivo                                                                                                                                                                    |
| OperatingSystem            | Sistema operativo do dispositivo. Windows, iOS/iPadOS, etc.                                                                                                                                   |
| IsDeleted                  | O binário para mostrar se o dispositivo é eliminado ou não.                                                                                                                                 |
| AndroidSecurityPatchLevel  | Nível do patch de segurança para Android                                                                                                                                                           |
| MEID                       | MEID                                                                                                                                                                                   |
| isSupervised               | Estado supervisionado do dispositivo                                                                                                                                                               |
| FreeStorageSpaceInBytes    | Armazenamento gratuito em bytes.                                                                                                                                                                 |
| EncryptionState            | Estado de encriptação no dispositivo.                                                                                                                                                      |
| SubscriberCarrier          | Operadora subscritora do dispositivo                                                                                                                                                       |
| PhoneNumber                | Número de telefone do dispositivo                                                                                                                                                             |
| IMEI                       | IMEI                                                                                                                                                                                   |
| CellularTechnology         | Tecnologia de rede móvel do dispositivo                                                                                                                                                    |
| WiFiMacAddress             | MAC Wi-Fi                                                                                                                                                                              |


## <a name="devicetypes"></a>deviceTypes
A entidade **deviceType** representa o tipo de dispositivo referenciado por outras entidades do armazém de dados. Normalmente, o tipo de dispositivo descreve o modelo do dispositivo, o fabricante ou ambos.

|    Propriedade    |                                  Descrição                                 |
|:--------------:|:----------------------------------------------------------------------------:|
| DeviceTypeID   | Identificador exclusivo do tipo de dispositivo                                       |
| DeviceTypeKey  | Identificador exclusivo do tipo de dispositivo no armazém de dados – chave de substituição |
| DeviceTypeName | Tipo de dispositivo                                                                |

### <a name="example"></a>Exemplo

| deviceTypeID |        Name       |                      Descrição                      |
|:------------:|:-----------------:|:-----------------------------------------------------:|
| -1           | Não disponível   | O tipo de dispositivo não está disponível.                     |
| 0            | Ambiente de trabalho           | Dispositivo de Ambiente de Trabalho do Windows                              |
| 1            | Windows           | Dispositivo Windows                                      |
| 2            | WinMO6            | Dispositivo Windows Mobile 6.0                           |
| 3            | Nokia             | Dispositivo Nokia                                        |
| 4            | WindowsPhone      | Dispositivo Windows Phone                                |
| 5            | Mac               | Dispositivo Mac                                          |
| 6            | WinCE             | Dispositivo Windows CE                                   |
| 7            | WinEmbedded       | Dispositivo Windows Embedded                             |
| 8            | IPhone            | Dispositivo iPhone                                       |
| 9            | IPad              | Dispositivo iPad                                         |
| 10           | IPod              | Dispositivo iPod                                         |
| 11           | Android           | Dispositivo Android gerido através do Administrador de Dispositivos   |
| 12           | ISocConsumer      | Dispositivo iSoc Consumer                                |
| 13           | Unix              | Dispositivo UNIX                                         |
| 14           | MacMDM            | Dispositivo Mac OS X gerido com o agente MDM incorporado |
| 15           | HoloLens          | Dispositivo HoloLens                                       |
| 16           | SurfaceHub        | Dispositivo Surface Hub                                  |
| 17           | AndroidForWork    | Dispositivo Android gerido através do Proprietário do Perfil Android  |
| 18           | AndroidEnterprise | Dispositivo empresarial Android.                          |
| 100          | Blackberry        | Dispositivo Blackberry                                   |
| 101          | Palm              | Dispositivo Palm                                         |
| 255          | Desconhecido           | Tipo de dispositivo desconhecido                                 |

## <a name="deviceenrollmenttypes"></a>deviceEnrollmentTypes
A entidade **deviceEnrollmentType** indica como um dispositivo foi inscrito. O tipo de inscrição captura o método de inscrição. Os exemplos listam os diferentes tipos de inscrição e o seu significado.

|         Propriedade         |                                    Descrição                                    |
|:------------------------:|:---------------------------------------------------------------------------------:|
| deviceEnrollmentTypeID   | Identificador exclusivo do tipo de inscrição.                                       |
| deviceEnrollmentTypeKey  | Identificador exclusivo do tipo de inscrição no armazém de dados – chave de substituição. |
| deviceEnrollmentTypeName | Nome do tipo de inscrição.                                                           |

### <a name="example"></a>Exemplo

| enrollmentTypeID |                Name                |                                        Descrição                                       |
|:----------------:|:----------------------------------:|:----------------------------------------------------------------------------------------:|
| 0                | Desconhecido                            | Não foi recolhido o tipo de inscrição                                                      |
| 1                | UserEnrollment                     | Inscrição controlada pelo utilizador através do canal BYOD.                                           |
| 2                | DeviceEnrollmentManager            | Inscrição de utilizadores com uma conta de gestor de inscrição de dispositivos.                              |
| 3                | AppleBulkWithUser                  | Inscrição em massa da Apple com o desafio de utilizador. (DEP, Apple Configurator)                   |
| 4                | AppleBulkWithoutUser               | Inscrição em massa da Apple sem o desafio de utilizador.   (DEP, Apple Configurator, Mobile Config) |
| 5                | WindowsAzureADJoin                 | Associação ao Azure AD para o Windows 10.                                                                |
| 6                | WindowsBulkUserless                | Inscrição em massa do Windows 10 através do ICD com certificado.                               |
| 7                | WindowsAutoEnrollment              | Inscrição automática de dispositivos Windows 10.   (Adicionar conta profissional)                                    |
| 8                | WindowsBulkAzureDomainJoin         | Associação ao Azure AD em massa no Windows 10.                                                           |
| 9                | WindowsCoManagement                | Cogestão do Windows 10 desencadeada pela Política de AutoPilot ou Grupo.                       |
| 10               | WindowsAzureADJoinsUsingDeviceAuth | Associação ao Azure AD no Windows 10 através da Autenticação do Dispositivo.                                            |

## <a name="enrollmentactivities"></a>inscriçõesAtividades 
A entidade De Atividade sinuosa indica a atividade de inscrição de um dispositivo. **EnrollmentActivity**

| Propriedade                      | Descrição                                                               |
|-------------------------------|---------------------------------------------------------------------------|
| dateKey                       | Chave da data em que esta atividade de inscrição foi registada.               |
| deviceEnrollmentTypeKey       | Chave do tipo de inscrição.                                        |
| dispositivoTypeKey                 | Chave do tipo de dispositivo.                                                |
| inscriçõesEventStatusKey      | Chave do estado indicando o sucesso ou falha da inscrição.    |
| inscriçãoFalhaCategoriaChave  | Chave da categoria de falha de inscrição (se a matrícula falhar).        |
| inscriçãoFalhaReasonKey    | Chave do motivo de falha de inscrição (se a inscrição falhou).          |
| osVersion                     | A versão do sistema operativo do dispositivo.                               |
| count                         | Contagem total de atividades de inscrição correspondentes às classificações acima referidas.  |

## <a name="enrollmenteventstatuses"></a>inscriçõesEventStatuses 
A entidade **RegistrationEventStatus** indica o resultado de uma inscrição no dispositivo.

| Propriedade                   | Descrição                                                                       |
|----------------------------|-----------------------------------------------------------------------------------|
| inscriçõesEventStatusKey   | Identificador único do estado de inscrição no armazém de dados (chave de substituição)  |
| inscriçãoEventStatusName  | O nome do estado de inscrição. Veja os exemplos abaixo.                            |

### <a name="example"></a>Exemplo

| inscriçãoEventStatusName  | Descrição                            |
|----------------------------|----------------------------------------|
| Êxito                    | Uma inscrição bem sucedida do dispositivo         |
| Falhou                     | Uma inscrição falhada do dispositivo             |
| Não Disponível              | O estado da inscrição não está disponível.  |

## <a name="enrollmentfailurecategories"></a>inscriçõesNãoCategorias de Insucesso 
A entidade **de Categoria de Falhas de Matrícula** indica porque é que uma matrícula do dispositivo falhou. 

| Propriedade                       | Descrição                                                                                 |
|--------------------------------|---------------------------------------------------------------------------------------------|
| inscriçãoFalhaCategoriaChave   | Identificador único da categoria de falha de inscrição no armazém de dados (chave de substituição)  |
| inscriçãoNome de categorias de falhas  | O nome da categoria de falha de inscrição. Veja os exemplos abaixo.                            |

### <a name="example"></a>Exemplo

| inscriçãoNome de categorias de falhas   | Descrição                                                                                                   |
|---------------------------------|---------------------------------------------------------------------------------------------------------------|
| Não Aplicável                  | A categoria de falha de inscrição não é aplicável.                                                            |
| Não Disponível                   | A categoria de falha de inscrição não está disponível.                                                             |
| Desconhecido                         | Uma margem de erro desconhecida.                                                                                                |
| Autenticação                  | Falha na autenticação.                                                                                        |
| Autorização                   | A chamada foi autenticada, mas não autorizada a inscrever-se.                                                         |
| Validação de Contas               | Não validou a conta para inscrição. (Conta bloqueada, inscrição não ativada)                      |
| Validação de Utilizadores                  | O utilizador não pôde ser validado. (Utilizador não existe, licença em falta)                                           |
| DispositivoNotSuportado              | O dispositivo não é suportado para a gestão de dispositivos móveis.                                                         |
| InManutenção                   | A conta está na manutenção.                                                                                    |
| BadRequest                      | O cliente enviou um pedido que não é compreendido/suportado pelo serviço.                                        |
| RecursoNotSupported             | As características utilizadas por esta inscrição não são suportadas para esta conta.                                        |
| Restrições de InscriçãoForçada  | As restrições de inscrição configuradas pela administração bloquearam esta inscrição.                                          |
| Cliente Desligado              | O cliente cronometrado ou a inscrição foi abortado pelo utilizador final.                                                        |
| Abandono de Utilizadores                 | A inscrição foi abandonada pelo utilizador final. (Utilizador final começou a embarcar mas não o completou atempadamente)  |

## <a name="enrollmentfailurereasons"></a>inscriçãoFalhaRaz  
A entidade **RegistrationFailureReason** indica uma razão mais detalhada para uma falha de inscrição de dispositivos dentro de uma determinada categoria de falha.  

| Propriedade                     | Descrição                                                                               |
|------------------------------|-------------------------------------------------------------------------------------------|
| inscriçãoFalhaReasonKey   | Identificador único do motivo de falha de inscrição no armazém de dados (chave de substituição)  |
| inscriçãoFaltanomeReason  | O nome da razão de falha de inscrição. Veja os exemplos abaixo.                            |

### <a name="example"></a>Exemplo

| inscriçãoFaltanomeReason      | Descrição                                                                                                                                                                                            |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Não Aplicável                   | O motivo da falha de inscrição não é aplicável.                                                                                                                                                       |
| Não Disponível                    | O motivo da falha de inscrição não está disponível.                                                                                                                                                        |
| Desconhecido                          | Erro desconhecido.                                                                                                                                                                                         |
| UserNotLicensed                  | O utilizador não foi encontrado em Intune ou não tem uma licença válida.                                                                                                                                     |
| UserUnknown                      | O utilizador não é conhecido de Intune.                                                                                                                                                                           |
| Dispositivo BulkAlreadyEnrolled        | Apenas um utilizador pode inscrever um dispositivo. Este dispositivo foi previamente matriculado por outro utilizador.                                                                                                                |
| InscriçãoOnboardingIssue        | A autoridade de gestão de dispositivos móveis intune (MDM) ainda não está configurada.                                                                                                                                 |
| AppleChallengeIssue              | A instalação do perfil de gestão do iOS foi adiada ou falhou.                                                                                                                                         |
| AppleOnboardingIssue             | É necessário um certificado de push Apple MDM para se inscrever no Intune.                                                                                                                                       |
| Tampa de Dispositivo                        | O utilizador tentou inscrever mais dispositivos do que o máximo permitido.                                                                                                                                        |
| AutenticaçãoRequirementNãoMet  | O serviço de inscrição intonou não autorizou este pedido.                                                                                                                                            |
| Tipo de Dispositivo não suportado            | Este dispositivo não satisfaz os requisitos mínimos para a inscrição intune.                                                                                                                                  |
| Critérios de InscriçãoNotMet         | Este dispositivo não se inscreveu devido a uma regra de restrição de inscrição configurada.                                                                                                                          |
| GranelDeviceNotPreregistro       | O identificador internacional de equipamentos móveis deste dispositivo (IMEI) ou número de série não foi encontrado.  Sem este identificador, os dispositivos são reconhecidos como dispositivos pessoais que estão atualmente bloqueados.  |
| RecursoNotSupported              | O utilizador estava a tentar aceder a uma funcionalidade que ainda não foi lançada para todos os clientes ou que não é compatível com a sua configuração Intune.                                                            |
| Abandono de Utilizadores                  | A inscrição foi abandonada pelo utilizador final. (Utilizador final começou a embarcar mas não o completou atempadamente)                                                                                           |
| APNSCertificadocado           | Os dispositivos apple não podem ser geridos com um certificado de push Apple MDM expirado.                                                                                                                            |

## <a name="intunemanagementextensions"></a>intuneManagementExtensions
A **intuneManagementExtension** apresenta o estado de funcionamento da **intuneManagementExtension** em cada dispositivo Windows 10 por dia. Os dados são mantidos relativamente aos últimos 60 dias.

|       Propriedade      |                          Descrição                          | Exemplo |
|:-------------------:|:-------------------------------------------------------------:|:-------:|
| DateKey             | Identificador exclusivo da Data.                                | 123     |
| TenantKey           | Identificador exclusivo do Inquilino.                              | 456     |
| DeviceKey           | Identificador exclusivo do Dispositivo.                              | 789     |
| ExtensionVersionKey | Identificador exclusivo da versão da IntuneManagementExtension. | 1       |
| ExtensionStateKey   | Identificador exclusivo do estado de funcionamento.                            | 2       |

## <a name="intunemanagementextensionhealthstates"></a>intuneManagementExtensionHealthStates
O **IntuneManagementExtensionHealthState** apresenta todos os estados de funcionamento possíveis da **IntuneManagementExtension**.

|      Propriedade     |                   Descrição                  | Exemplo |
|:-----------------:|:----------------------------------------------:|:-------:|
| ExtensionStateKey | Identificador exclusivo do estado de funcionamento.           | 2       |
| ExtensionState    | Estado de funcionamento de uma IntuneManagementExtension. | Bom estado de funcionamento |

## <a name="intunemanagementextensionversions"></a>intuneManagementExtensionVersions
A entidade **IntuneManagementExtensionVersion** apresenta todas as versões utilizadas pela **IntuneManagementExtension**.

|       Propriedade      |                          Descrição                          | Exemplo |
|:-------------------:|:-------------------------------------------------------------:|:-------:|
| ExtensionVersionKey | Identificador exclusivo da versão da IntuneManagementExtension. | 1       |
| ExtensionVersion    | O número da versão de quatro dígitos.                                   | 1.0.2.0 |

## <a name="mamapplications"></a>Aplicações mamaplicações

A entidade **MamApplication** lista aplicações Linha de Negócio (LOB) que são geridas através da Gestão de Aplicações Móveis (MAM) sem inscrição na sua empresa.

| Propriedade | Descrição | Exemplo |
|---------|------------|--------|
| mamApplicationKey |Identificador único da aplicação MAM. | 432 |
| nome de aplicação mama |Nome da aplicação MAM. |Nome da exemplo da aplicação MAM |
| mamApplicationId |Id de aplicação da aplicação MAM. | 123 |
| IsDeleted |Indica se este registo da aplicação MAM foi atualizado. <br>True: a aplicação MAM tem um novo registo com campos atualizados nesta tabela. <br>False: o registo mais recente desta aplicação MAM. |Verdadeiro/Falso |
| StartDateInclusiveUTC |Data e hora em UTC em que esta aplicação MAM foi criada no armazém de dados. |11/23/2016 12:00:00 AM |
| DeletedDateUTC |Data e hora em UTC em que a propriedade IsDeleted foi alterada para True. |11/23/2016 12:00:00 AM |
| RowLastModifiedDateTimeUTC |Data e hora em UTC em que esta aplicação MAM foi modificada pela última vez no armazém de dados. |11/23/2016 12:00:00 AM |


## <a name="mamapplicationinstances"></a>MamApplicationCasos

A entidade **MamApplicationInstance** lista aplicações geridas da Gestão de Aplicações Móveis (MAM) como instâncias singulares por utilizador e dispositivo. Todos os utilizadores e dispositivos listados na entidade estão protegidos, ou seja, têm pelo menos uma Política de MAM atribuída.


|          Propriedade          |                                                                                                  Descrição                                                                                                  |               Exemplo                |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
|   ApplicationInstanceKey   |                                                               Identificador exclusivo de instância da aplicação MAM no armazém de dados – chave de substituição.                                                                |                 123                  |
|           IDUtilizador           |                                                                              Id do utilizador do utilizador que tem esta aplicação MAM instalada.                                                                              | b66bc706-ffff-7437-0340-032819502773 |
|   ApplicationInstanceId    |                                              Identificador exclusivo de instância da aplicação MAM, semelhante à propriedade ApplicationInstanceKey, apesar de o identificador ser uma chave natural.                                              | b66bc706-ffff-7437-0340-032819502773 |
| mamApplicationId | Id de aplicação do pedido mam para o qual esta Instância de Aplicação Mam foi criada.   | 11/23/2016 12:00:00 AM   |
|     ApplicationVersion     |                                                                                     Versão desta aplicação MAM.                                                                                      |                  2                   |
|        CreatedDate         |                                                                 Data em que este registo da instância da aplicação MAM foi criado. O valor pode ser nulo.                                                                 |        11/23/2016 12:00:00 AM        |
|          Plataforma          |                                                                          Plataforma do dispositivo no qual esta aplicação MAM está instalada.                                                                           |                  2                   |
|      PlatformVersion       |                                                                      Versão de plataforma do dispositivo no qual esta aplicação MAM está instalada.                                                                       |                 2,2                  |
|         SdkVersion         |                                                                            A versão de SDK MAM com a qual esta aplicação MAM foi encapsulada.                                                                            |                 3.2                  |
| mamDeviceId | Id do dispositivo com o qual a MAM Application Instance está associada.   | 11/23/2016 12:00:00 AM   |
| mamDeviceType | Tipo de dispositivo do dispositivo com o qual a MAM Application Instance está associada.   | 11/23/2016 12:00:00 AM   |
| nome do dispositivo mamdevice | Nome do dispositivo com o qual a MAM Application Instance está associada.   | 11/23/2016 12:00:00 AM   |
|         IsDeleted          | Indica se este registo de instância da aplicação MAM foi atualizado. <br>True: esta instância de aplicação MAM tem um novo registo com campos atualizados nesta tabela. <br>False: o registo mais recente desta instância da aplicação MAM. |              Verdadeiro/Falso              |
|   StartDateInclusiveUtc    |                                                              Data e hora em UTC em que esta instância da aplicação MAM foi criada no armazém de dados.                                                               |        11/23/2016 12:00:00 AM        |
|       DeletedDateUtc       |                                                                             Data e hora em UTC em que a propriedade IsDeleted foi alterada para True.                                                                              |        11/23/2016 12:00:00 AM        |
| RowLastModifiedDateTimeUtc |                                                           Data e hora em UTC em que esta instância da aplicação MAM foi modificada pela última vez no armazém de dados.                                                            |        11/23/2016 12:00:00 AM        |

## <a name="mamcheckins"></a>MamCheckins

A entidade **MamCheckin** representa dados recolhidos quando uma instância de Gestão de Aplicações Móveis (MAM) deu entrada no Serviço do Intune. 

> [!Note]  
> Quando uma instância de aplicação dá entrada várias vezes por dia, o armazém de dados armazena-a como uma entrada única.

| Propriedade | Descrição | Exemplo |
|---------|------------|--------|
| DateKey |Chave da data quando a entrada da aplicação MAM foi registada no armazém de dados. | 20160703 |
| ApplicationInstanceKey |Chave da instância da aplicação associada a esta entrada da aplicação MAM. | 123 |
| UserKey |Chave do utilizador associado a esta entrada da aplicação MAM. | 4323 |
| mamApplicationKey |Chave de aplicação associada ao check-in da aplicação MAM. | 432 |
| DeviceHealthKey |Chave de DeviceHealth associada a esta entrada da aplicação MAM. | 321 |
| PlatformKey |Representa a plataforma do dispositivo associado a esta entrada da aplicação MAM. |123 |
| LastCheckInDate |Data e hora em que esta aplicação MAM deu entrada pela última vez. O valor pode ser nulo. |11/23/2016 12:00:00 AM |

## <a name="mamdevicehealths"></a>MamDeviceHealths

A entidade **MamDeviceHealth** representa dispositivos que têm políticas de Gestão de Aplicações Móveis (MAM) implementadas nos mesmos, mesmo que tenham sido desbloqueados por jailbreak.

| Propriedade | Descrição | Exemplo |
|---------|------------|--------|
| DeviceHealthKey |Identificador exclusivo do dispositivo e respetivo estado de funcionamento associado no armazém de dados – chave de substituição. |123 |
| DeviceHealth |Identificador exclusivo do dispositivo e respetivo estado de funcionamento associado, semelhante a DeviceHealthKey, mas o identificador é uma chave natural. |b66bc706-ffff-7777-0340-032819502773 |
| DeviceHealthName |Representa o estado do dispositivo. <br>Not available: não existem informações sobre este dispositivo. <br>Healthy: o dispositivo não foi desbloqueado por jailbreak. <br>Unhealthy: o dispositivo foi desbloqueado por jailbreak. |Not Available Healthy Unhealthy |
| RowLastModifiedDateTimeUtc |Data e hora em UTC em que o Estado de Funcionamento deste Dispositivo MAM específico foi modificado pela última vez no armazém de dados. |11/23/2016 12:00:00 AM |

## <a name="mamplatforms"></a>MamPlatforms

A entidade **MamPlatform** lista os nomes e tipos de plataformas em que uma aplicação da Gestão de Aplicações Móveis (MAM) foi instalada.


|          Propriedade          |                                    Descrição                                    |                         Exemplo                         |
|----------------------------|-----------------------------------------------------------------------------------|---------------------------------------------------------|
|        PlatformKey         |     Identificador exclusivo da plataforma no armazém de dados – chave de substituição.      |                           123                           |
|          Plataforma          | Identificador exclusivo da plataforma, semelhante a PlatformKey, mas é uma chave natural. |                           123                           |
|        PlatformName        |                                   Nome da plataforma                                   | Não Disponível <br>Nenhum <br>Windows <br>iOS <br>Android. |
| RowLastModifiedDateTimeUtc | Data e hora em UTC em que esta plataforma foi modificada pela última vez no armazém de dados.  |                 11/23/2016 12:00:00 AM                  |

## <a name="managementagenttypes"></a>managementAgentTypes
A entidade **managementAgentType** representa os agentes utilizados para gerir um dispositivo.

|         Propriedade        |                                       Descrição                                       |
|:-----------------------:|:---------------------------------------------------------------------------------------:|
| ManagementAgentTypeID   | Identificador exclusivo do tipo de agente de gestão.                                         |
| ManagementAgentTypeKey  | Identificador exclusivo do tipo de agente de gestão no armazém de dados – chave de substituição. |
| ManagementAgentTypeName | Indica que tipo de agente é utilizado para gerir o dispositivo.                              |

### <a name="example"></a>Exemplo

| ManagementAgentTypeID |                Name               |                                  Descrição                                 |
|:---------------------:|:---------------------------------:|:----------------------------------------------------------------------------:|
| 1                     | EAS                               | O dispositivo é gerido através do Exchange Active Sync                         |
| 2                     | MDM                               | O dispositivo é gerido através de um agente MDM                                   |
| 3                     | EasMdm                            | O dispositivo é gerido através do Exchange Active Sync e de um agente MDM        |
| 4                     | IntuneClient                      | O dispositivo é gerido pelo agente de PC do Intune                               |
| 5                     | EasIntuneClient                   | O dispositivo é gerido através do Exchange Active Sync e do agente de PC do Intune |
| 8                     | ConfigManagerClient               | O dispositivo é gerido pelo agente 'Gestor de Configuração'     |
| 10                    | ConfigurationManagerClientMdm     | O dispositivo é gerido pelo Configuration Manager e MDM.                    |
| 11                    | ConfigurationManagerCLientMdmEas  | O dispositivo é gerido por Configuração Manager, MDM e Exchange Ative Sync.               |
| 16                    | Desconhecido                           | Tipo de agente de gestão desconhecido                                              |
| 32                    | Jamf                              | Os atributos do dispositivo são obtidos a partir do Jamf.                               |
| 64                    | GoogleCloudDevicePolicyController |  O dispositivo é gerido pelo CloudDPC da Google.                                 |

## <a name="managementstates"></a>managementStates
A entidade **ManagementState** disponibiliza detalhes sobre o estado do dispositivo. Os detalhes podem ser úteis nos casos em que são aplicadas ações remotas ou quando o dispositivo foi desbloqueado por jailbreak ou rooting.

|       Propriedade      |                                     Descrição                                    |
|:-------------------:|:----------------------------------------------------------------------------------:|
| managementStateID   | Identificador exclusivo do estado de gestão.                                       |
| managementStateKey  | Identificador exclusivo do estado de gestão no armazém de dados – chave de substituição. |
| managementStateName | Indica o estado da ação remota aplicada a este dispositivo.                 |

### <a name="example"></a>Exemplo

| managementStateID |      Name      |                                                   Descrição                                                   |
|:-----------------:|:--------------:|:---------------------------------------------------------------------------------------------------------------:|
| 0                 | Geridos        | Gerido sem ações remotas pendentes.                                                                       |
| 1                 | RetirePending  | Existe um comando de extinção pendente para o dispositivo.                                                             |
| 2                 | RetireFailed   | O comando de extinção no dispositivo falhou.                                                                      |
| 3                 | WipePending    | Existe um comando para apagar pendente para o dispositivo.                                                               |
| 4                 | WipeFailed     | O comando para apagar falhou no dispositivo.                                                                        |
| 5                 | Mau estado de funcionamento      | Mau estado de funcionamento.                                                                                              |
| 6                 | DeletePending  | Existe um comando de eliminação pendente para o dispositivo.                                                             |
| 7                 | RetireIssued   | Foi emitido um comando de extinção para o dispositivo.                                                               |
| 8                 | WipeIssued     | Foi emitido um comando para apagar.                                                                               |
| 9                 | WipeCanceled   | O comando para apagar foi cancelado.                                                                               |
| 10                | RetireCanceled | O comando de extinção foi cancelado.                                                                             |
| 11                | Discovered     | O dispositivo foi detetado recentemente no Intune. Após dar entrada pela primeira vez, será movido para o estado Managed. |

## <a name="mobileappinstallstates"></a>mobileAppInstallStates
A entidade MobileAppInstallState representa o estado de instalação de uma aplicação móvel depois de ser atribuída a um grupo que contém dispositivos, utilizadores ou ambos.

|       Propriedade      |                        Descrição                       |
|:-------------------:|:--------------------------------------------------------:|
| AppInstallStateKey  | O ID exclusivo do estado de instalação da aplicação da sua conta. |
| AppInstallState     | Valor Enum do estado de instalação da aplicação.                     |
| AppInstallStateName | Nome do estado de instalação da aplicação.                           |

## <a name="mobileappinstallstatuscounts"></a>mobileAppInstallStatusCounts
Representa um estado de instalação da aplicação móvel para um determinado tipo de dispositivo de destino através da Gestão de Aplicações Móveis com o Microsoft Intune.

|      Propriedade      |                                                          Descrição                                                          |
|:------------------:|:-----------------------------------------------------------------------------------------------------------------------------:|
| DateKey            | A chave da data quando o estado de instalação da aplicação foi registado.                                                                     |
| AppKey             | A chave da aplicação móvel que serve para identificar uma instância de AppRevision.                                                          |
| DeviceTypeKey      | A chave do Tipo de Dispositivo associado à Aplicação Móvel.                                                              |
| AppInstallStateKey | A chave do estado de instalação da aplicação que serve para identificar uma instância de MobileAppInstallState.                                         |
| CódigoDoErro          | O código de erro devolvido pelo instalador de aplicações, pela plataforma móvel ou pelo serviço relativo à instalação da aplicação. |
| Contagem              | Contagem total.                                                                                                                  |

## <a name="ownertypes"></a>ownerTypes
A entidade **ownerType** indica se um dispositivo é empresarial, pessoal ou desconhecido.

|    Propriedade   |                                                                                     Descrição                                                                                    |           Exemplo          |
|:-------------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:--------------------------:|
| ownerTypeID   | Identificador exclusivo do tipo de proprietário.                                                                                                                                               |                            |
| ownerTypeKey  | Identificador exclusivo do tipo de proprietário no armazém de dados – chave de substituição.                                                                                                       |                            |
| ownerTypeName | Representa o tipo proprietário dos dispositivos: Corporate - Device is enterprise owned.  Personal – o dispositivo é propriedade pessoal (BYOD).   Unknown – não existem informações sobre este dispositivo. | Corporate Personal Unknown |

> [!Note]  
> Para o `ownerTypeName` filtro em AzureAD ao criar Grupos Dinâmicos para dispositivos, é necessário definir o valor `deviceOwnership` como `Company` . Para mais informações, consulte [Regras para dispositivos](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices). 

## <a name="policies"></a>políticas
A entidade **Policy** apresenta uma lista de perfis de configuração de dispositivos, perfis de configuração de aplicações e políticas de conformidade. Pode atribuir as políticas com a Gestão de Dispositivos Móveis (MDM) a um grupo na sua empresa.

|          Propriedade          |                                                                       Descrição                                                                      |                Exemplo               |
|:--------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------:|:------------------------------------:|
| PolicyKey                  | Chave exclusiva para representar a política no armazém de dados.                                                                                              | 123                                  |
| PolicyId                   | Identificador exclusivo da Política no armazém de dados.                                                                                                 | b66bc706-ffff-7437-0340-032819502773 |
| PolicyName                 | Nome da Política.                                                                                                                                    | "Linha de Base do Windows 10"                |
| PolicyVersion              | Versão da Política. Quando a política é editada ou alterada, é criada uma versão mais recente.                                                             | 1, 2, 3                              |
| IsDeleted                  | Indica se o registo da Política foi atualizado.  True – a política tem um novo registo com campos atualizados.  False – o registo mais recente da política. | Verdadeiro/Falso                           |
| StartDateInclusiveUTC      | Data e hora em UTC em que a política foi criada no armazém de dados.                                                                              | 11/23/2016 0:00                      |
| DeletedDateUTC             | Data e hora em UTC em que a propriedade IsDeleted foi alterada para True.                                                                                                   | 11/23/2016 0:00                      |
| RowLastModifiedDateTimeUTC | Data e hora em UTC em que a política foi modificada pela última vez no armazém de dados.                                                                        | 11/23/2016 0:00                      |

## <a name="policydeviceactivities"></a>policyDeviceActivities
A tabela seguinte mostra o número de dispositivos no estado com êxito, pendente, com falhas ou com erros por dia. O número apresentado reflete os perfis de dados por Tipo de Política. Por exemplo, se um dispositivo estiver no estado com êxito em todas as políticas atribuídas, o contador de casos com êxito tem um incremento de um para esse dia. Se um dispositivo tiver dois perfis atribuídos, um no estado com êxito e outro num estado com erros, a entidade incrementa o contador do estado com êxito (Succeeded) e coloca o dispositivo no estado com erros. A entidade **policyDeviceActivity** apresenta uma lista de quantos dispositivos estão em cada um dos estados num determinado dia nos últimos 30 dias.

|  Propriedade |                                           Descrição                                           |        Exemplo        |
|:---------:|:-----------------------------------------------------------------------------------------------:|:---------------------:|
| DateKey   | Data-chave de quando a entrada do Perfil de Configuração do Dispositivo foi registada no armazém de dados. | 20160703              |
| Pendente   | Número de Dispositivos exclusivos no estado pendente.                                                    | 123                   |
| Bem-sucedido | Número de Dispositivos exclusivos no estado com êxito.                                                    | 12                    |
| PolicyKey | A chave de Política pode ser acompanhada pela Política para obter o policyName.                                  | Linha de base do Windows 10 |
| Erro     | Número de Dispositivos exclusivos no estado com erros.                                                      | 10                    |
| Falhou    | Número de Dispositivos exclusivos no estado com falhas.                                                     | 2                     |

## <a name="policyplatformtypes"></a>policyPlatformTypes

|        Propriedade        |                      Descrição                      |     Exemplo    |
|:----------------------:|:-----------------------------------------------------:|:--------------:|
| PolicyPlatformTypeKey  | A chave exclusiva do tipo de plataforma da política.        | 20170519       |
| PolicyPlatformTypeId   | O identificador exclusivo do tipo de plataforma da política. | 1              |
| PolicyPlatformTypeName | O nome do tipo de plataforma da política.              | AndroidForWork |

## <a name="policytypeactivities"></a>policyTypeActivities
A entidade **PolicyTypeActivity** apresenta uma lista do número cumulativo de dispositivos no estado com êxito, pendente, com falhas ou com erros por dia. Apresenta uma lista destes estados relativamente a um perfil de configuração de dispositivo, perfil de configuração de aplicação ou política de conformidade por dia.

|    Propriedade   |                                          Descrição                                          |           Exemplo           |
|:-------------:|:---------------------------------------------------------------------------------------------:|:---------------------------:|
| DateKey       | Data-chave de quando a entrada do Perfil de configuração do dispositivo foi registada no armazém de dados. | 20160703                    |
| PolicyKey     | A chave de política pode ser acompanhada pela Política para obter o policyName.                                | Linha de base do Windows 10         |
| PolicyTypeKey | O tipo de Chave de Política pode ser acompanhado do Tipo de Política para obter o nome do tipo de política.             | Política de Compatibilidade do Windows 10 |
| Pendente       | Número de dispositivos exclusivos no estado pendente.                                                    | 123                         |
| Bem-sucedido     | Número de dispositivos exclusivos no estado com êxito.                                                    | 12                          |
| Erro         | Número de dispositivos exclusivos no estado com erros.                                                      | 10                          |
| Falhou        | Número de dispositivos exclusivos no estado com falhas.                                                     | 2                           |

## <a name="policytypes"></a>policyTypes
A entidade **PolicyType** apresenta uma lista dos tipos de perfis de configuração de dispositivos, perfis de configuração de aplicações e políticas de conformidade. Pode atribuir as políticas com a Gestão de Dispositivos Móveis (MDM) a um grupo na sua empresa.

|    Propriedade    |                       Descrição                      |            Exemplo            |
|:--------------:|:------------------------------------------------------:|:-----------------------------:|
| PolicyTypeId   | Identificador exclusivo da política no sistema de origem.  | 123                           |
| PolicyTypeKey  | Identificador exclusivo da política no armazém de dados. | 1                             |
| PolicyTypeName | Nome do tipo de política.                               | Política de Conformidade do Windows 10. |

## <a name="policyuseractivities"></a>policyUserActivities
A tabela seguinte mostra o número de utilizadores no estado com êxito, pendente, com falhas ou com erros por dia. O número apresentado reflete os perfis de dados por Tipo de Política. Por exemplo, se um utilizador estiver no estado com êxito em todas as políticas atribuídas, sobe o contador com êxito em um para esse dia. Se um utilizador tiver dois perfis atribuídos, um no estado com êxito e outro no estado com erros, é contado o utilizador no estado com erros. A entidade **PolicyUserActivity** lista quantos utilizadores estão em que estado num determinado dia ao longo dos últimos 30 dias.

|  Propriedade |                                          Descrição                                          |       Exemplo       |
|:---------:|:---------------------------------------------------------------------------------------------:|:-------------------:|
| DateKey   | Data-chave de quando a entrada do Perfil de Configuração do Dispositivo foi registada no armazém de dados. | 20160703            |
| Pendente   | Número de Dispositivos exclusivos no estado pendente.                                                    | 123                 |
| Bem-sucedido | Número de Dispositivos exclusivos no estado com êxito.                                                    | 12                  |
| PolicyKey | A chave de política pode ser acompanhada pela Política para obter o policyName.                                | Linha de base do Windows 10 |
| Erro     | Número de Dispositivos exclusivos no estado com erros.                                                      | 10                  |

## <a name="termsandconditions"></a>termsAndConditions
A entidade **termsAndConditions** representa os metadados e o conteúdo de uma determinada política de Termos e Condições (T&C). O conteúdo das políticas de T&C é apresentado aos utilizadores após a sua primeira tentativa de inscrição no Intune e, em seguida, após as edições em que um administrador tiver exigido uma nova aceitação. Permitem que os administradores comuniquem as cláusulas que um utilizador tem de aceitar para inscrever dispositivos no Intune.

|    Propriedade        |    Descrição    |    Exemplo        |
|----------------------------------|-----------------------------------------------------------------------------------------------|-----------------------------------------------------------|
|    termsAndConditionsKey    |    Uma chave correspondente a uma entrada na coleção 'userTermsAndConditionsAccepts'    |    123    |
|    termsAndCondidionsId    |    O ID para esta entrada termsAndConditions    |    276edcb7-7440-4339-b6c5-8b6fc556fee6    |
|    termsAndConditionsVersion    |    A versão da entrada destes termos e condições    |    1    |
|    name    |    O nome da entrada destes termos e condições.        |    Termos de utilização do Intune     |
|    descrição    |    A descrição para estes termos e condições.     |         |
|    título    |    O título para estes termos e condições.     |    Política empresarial da gestão de dispositivos        |
|    summaryOfTerms    |    O resumo dos termos que o utilizador recebeu.     |    Concordo com os termos e condições.    |
|    termsAndConditionsBodyText    |    O corpo do texto para estes termos e condições.       |    *Encriptação de dispositivos* Imposição do PIN com 6 dígitos    |
|    isDeleted    |    Valor de verdadeiro ou falso para saber se este valor foi eliminado.     |    Falso    |
|    startDateInclusiveUTC    |    A data de início dos termos e condições.     |    8/23/2018 4:01:34    |
|    endDateEclusiveUTC    |    A data de fim destes termos e condições.     |    12/31/9999 00:00:00    |

## <a name="userdeviceassociations"></a>userDeviceAssociations
A entidade **UserDeviceAssociation** contém associações de dispositivos do utilizador na sua organização.

|        Name        |                                             Descrição                                            |     Exemplo     |
|:------------------:|:--------------------------------------------------------------------------------------------------:|:---------------:|
| UserKey            | Identificador exclusivo do utilizador no armazém de dados.   (Chave de substituição).                            | 123             |
| DeviceKey          | Identificador exclusivo do dispositivo no armazém de dados.                                             | 123             |
| CreatedDateTimeUTC | Data e hora em que a associação de dispositivos do utilizador foi criada. Utiliza o formato UTC.                     | 11/23/2016 0:00 |
| IsDeleted          | Indica que o utilizador anulou a inscrição desse dispositivo e essa associação já não está atualizada. | Verdadeiro/Falso      |
| EndedDateTimeUTC   | Data e hora em UTC em que a propriedade IsDeleted foi alterada para True.                                               | 6/23/2017 0:00  |

## <a name="users"></a>utilizadores
A entidade **user** lista todos os utilizadores do Azure Active Directory (Azure AD) com licenças atribuídas na sua empresa.

A recolha da entidade **utilizadora** contém dados do utilizador. Estes registos incluem estados do utilizador durante o período de recolha dos dados, mesmo que o utilizador tenha sido removido. Por exemplo, um utilizador pode ser adicionado ao Intune e, em seguida, removido no decorrer do mês anterior. Apesar de este utilizador não estar presente no momento do relatório, o utilizador e o estado estão presentes nos dados do mês anterior. Pode criar um relatório que mostrará a duração da presença no histórico do utilizador nos seus dados.

|          Propriedade          |                                                                                                           Descrição                                                                                                          |                Exemplo               |
|:--------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:------------------------------------:|
| UserKey                    | Identificador exclusivo do utilizador no armazém de dados – chave de substituição.                                                                                                                                                         | 123                                  |
| IDUtilizador                     | Identificador exclusivo do utilizador – semelhante a UserKey, mas é uma chave natural.                                                                                                                                                    | b66bc706-ffff-7437-0340-032819502773 |
| UserEmail                  | Endereço de e-mail do utilizador.                                                                                                                                                                                                     | John@constoso.com                    |
| userPrincipalName                        | O nome principal do utilizador.                                                                                                                                                                                               | John@constoso.com                    |
| DisplayName                | Nome a apresentar do utilizador.                                                                                                                                                                                                      | John                                 |
| IntuneLicensed             | Especifica se este utilizador tem ou não licença do Intune.                                                                                                                                                                              | Verdadeiro/Falso                           |
| IsDeleted                  | Indica se todas as licenças do utilizador expiraram e se o utilizador foi, por conseguinte, removido do Intune. Para um único registo, este sinalizador não se altera. Em vez disso, é criado um novo registo para um novo estado do utilizador. | Verdadeiro/Falso                           |
| RowLastModifiedDateTimeUTC | Data e hora em UTC quando o registo foi modificado pela última vez no armazém de dados                                                                                                                                                 | 11/23/2016 0:00                      |

## <a name="usertermsandconditionsacceptances"></a>userTermsAndConditionsAcceptances
A entidade **userTermsAndConditionsAcceptance** representa o estado de aceitação de uma determinada Política de Termos e Condições (T&C) por um determinado utilizador. Os utilizadores têm de aceitar a versão mais atualizada dos termos para manter o acesso ao Portal da Empresa.

|    Propriedade    |    Descrição    |    Exemplo    |
|-------------------------------|--------------------------------------------------------------------------------|----------------------------|
|    dateKey    |    Uma chave correspondente aos valores de data na coleção 'datas'.     |    20180823    |
|    userKey    |    Um mapeamento de chave de utilizador para um utilizador na coleção 'utilizadores'.     |    20 000    |
|    termsAndConditionsKey    |    Uma chave correspondente a uma entrada na coleção 'termsAndConditions'    |    1    |
|    acceptedDateTimeUTC    |    A hora em que o utilizador aceitou estes termos e condições    |    8/23/2018 4:01:34    |
|    lastModifiedDateTimeUTC    |    A última vez que esta entrada foi modificada.     |    8/23/2018 4:01:34    |

## <a name="vppprogramtypes"></a>vppProgramTypes 
A entidade **vppProgramType** apresenta uma lista de tipos de programas VPP possíveis para uma aplicação.

|      Propriedade      |          Descrição         |
|:------------------:|:----------------------------:|
| VppProgramTypeID   | ID do tipo.           |
| VppProgramTypeKey  | Chave de substituição da chave. |
| VppProgramTypeName | Tipo de Programa VPP.          |

### <a name="example"></a>Exemplo

|             VppProgramID             |         Name        | Descrição                |
|:------------------------------------:|:-------------------:|----------------------------|
| 3DDA2474-470B-4503-9830-2665C21C1945 | Microsoft           | Programa VPP da Microsoft. |
| 00000000-0000-0000-0000-000000000000 | Ainda não está disponível | Valor predefinido, Sem VPP.   |
| B54814E0-68EA-4BA4-8088-B5AAB58E737B | Apple               | Programa VPP da Apple.     |

## <a name="next-steps"></a>Próximos passos

Para obter mais informações sobre o Armazém de Dados do Intune, veja [Modelo de dados do Armazém de Dados](reports-ref-data-model.md).
