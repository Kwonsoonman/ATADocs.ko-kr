---
title: "Advanced Threat Analytics 알림 설정 | Microsoft 문서"
description: "의심스러운 활동이 감지되었을 때 알림을 받도록 ATA 경고를 설정하는 방법을 설명합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: dce36e1943ee18f27dfc11d5bc9094c5fd97edb6
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*



# <a name="set-ata-notifications"></a>ATA 알림 설정
ATA는 의심스러운 활동을 감지하면 메일을 통해 또는 ATA 이벤트 전달 기능을 사용한 후 이벤트를 SIEM/syslog 서버에 전달하여 알릴 수 있습니다. 수신하려는 알림을 선택하기 전에 [메일 서버 및 Syslog 서버를 설정](setting-syslog-email-server-settings.md)해야 합니다.

> [!NOTE]
> -   메일 알림에는 발견된 의심스러운 활동으로 사용자를 직접 이동하는 링크가 포함됩니다. 링크의 호스트 이름 부분은 ATA 센터 페이지에서 ATA 콘솔 URL을 설정하여 가져옵니다. 기본적으로 ATA 콘솔 URL은 ATA 센터의 설치 중에 선택한 IP 주소입니다. 메일 알림을 구성하려는 경우 FQDN을 ATA 콘솔 URL로 사용하는 것이 좋습니다.
> -   알림은 ATA 센터에서 SMTP 서버 또는 Syslog 서버로 전송됩니다.


알림을 수신하려면 다음 매개 변수를 설정합니다.


1. ATA 콘솔의 도구 모음에서 설정 옵션을 선택하고 **구성**을 선택합니다.

![ATA 구성 설정 아이콘](media/ATA-config-icon.png)

2. **알림 및 보고서** 섹션에서 **알림**을 선택합니다.
3. **메일 알림**에서 새로운 의심스러운 활동, 새로운 상태 문제 등 메일을 통해 보낼 알림을 지정합니다. 의심스러운 활동과 상태 경고에 대해 알림을 보낼 메일 주소를 각각 설정하여, 예를 들어 의심스러운 활동 알림은 보안 분석가에게 보내고 상태 경고 알림은 IT 관리자에게 보낼 수 있습니다.
>   [!NOTE]
>   의심스러운 활동에 대한 전자 메일 경고는 의심스러운 활동이 생성될 때만 전송됩니다.
3. **Syslog 알림**에서 새로운 의심스러운 활동, 업데이트된 의심스러운 활동, 새로운 상태 문제 등 Syslog 서버에 보낼 알림을 지정합니다.
5. **Save**을 클릭합니다.

![ATA 메일 알림 설정 이미지](media/ata-mail-notification-settings.png)




## <a name="see-also"></a>참고 항목
[ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
