---
title: Instalar a aplicação Portal da Empresa para Windows | Documentos da Microsoft
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/23/2017
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d65e3452-5bbf-4d26-a06e-401ddcc47f39
searchScope:
- User help
ROBOTS: ''
ms.reviewer: priyar
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 35724775af5aa5d4333062eaf03367fe0951066f
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83882360"
---
# <a name="what-happens-if-you-install-the-company-portal-app-and-enroll-your-windows-device-in-intune"></a>O que acontece se instalar a aplicação do Portal da Empresa e inscrever o seu dispositivo Windows no Intune?

Quando instala a aplicação Portal da Empresa e a utiliza para inscrever um dispositivo Windows ou Windows Phone, está a dar permissão ao suporte da empresa para gerir o seu dispositivo de forma a ajudar a manter os dados da sua empresa ou escola em segurança. Este tópico descreve o que acontece em dispositivos anteriores ao Windows 10. Para dispositivos com o Windows 10, consulte o [tópico relacionado](about-cp-app-for-windows-10.md).  

## <a name="what-happens-to-all-windows-devices-after-enrollment"></a>O que acontece a todos os dispositivos Windows após a inscrição
Inscrever o seu dispositivo Windows ou Windows Phone no Intune permite-lhe:

- Aceda à rede da empresa e aos seus ficheiros de e-mail e trabalho.

- Obter aplicações da empresa a partir do site do Portal da Empresa. (__Nota__: para o Windows 7 e o Windows Vista, só pode obter aplicações da empresa a partir do site do Portal da Empresa.)

- Configurar automaticamente a sua conta de e-mail escolar ou profissional.

- Repor o telemóvel para as definições de fábrica em caso de perda ou roubo.

Quando inscreve o seu dispositivo, está a dar permissão ao suporte da empresa para fazer coisas como:

- Reponha o seu dispositivo de volta às definições predefinidas do fabricante. Esta ação é útil em caso de perda ou roubo do dispositivo.

- Remover apenas aplicações empresariais e ficheiros relacionados com a empresa. *Os seus dados pessoais e configurações não são removidos.*

- O suporte da empresa consegue ver o software que tem instalado no dispositivo, incluindo o software que tem instalado para utilização pessoal.

- Definir requisitos no seu dispositivo, como exigir que tenha uma palavra-passe de dispositivo ou um PIN para ajudar a proteger os dados da empresa. O suporte da empresa também pode limitar o número de vezes que o utilizador pode introduzir uma palavra-passe incorreta e poderá bloquear a sua utilização do dispositivo se tentar demasiadas vezes.

- Exigir-lhe que faça a encriptação dos dados no seu dispositivo para ajudar a proteger os dados da empresa em caso de perda ou roubo do seu dispositivo.

- O administrador de TI pode exigir que aceite os termos e condições.

- Impedir que tire fotografias de dados relacionados com a empresa.

## <a name="what-happens-to-all-windows-pcs-after-enrollment"></a>O que acontece a todos os PCs Windows após a inscrição

- Será instalado software no seu computador para permitir que o suporte da empresa faça a gestão do mesmo e o utilizador aceda a recursos da empresa, como aplicações e informações de suporte. O suporte da empresa poderá atualizar automaticamente este software.

- O Endpoint Protection do Intune poderá ser instalado no seu computador. Este software verifica a existência de vírus e software maligno.

- O suporte da sua empresa pode recolher ou eliminar dados do disco rígido do computador.

- O suporte da empresa pode instalar aplicações e atualizações no seu computador.

## <a name="what-happens-every-eight-hours-after-device-enrollment"></a>O que acontece a cada oito horas após a inscrição de dispositivos

A cada oito horas, os dispositivos inscritos irão:

- Transferir atualizações de políticas ou aplicações disponibilizadas pelo suporte da empresa.

- Enviar atualizações de inventário de hardware.

- Enviar atualizações de inventário de aplicações da empresa.

Se tiver dúvidas, contacte o suporte da empresa. Para encontrar as informações de contacto dele, verifique o [site do Portal da Empresa](https://go.microsoft.com/fwlink/?linkid=2010980).
