---
title: "ATA 알림 설정 | Microsoft ATA"
description: "의심스러운 활동이 감지되었을 때 알림을 받도록 ATA 경고를 설정하는 방법을 설명합니다."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 03f6f184e7f34d6985103f503b8d88a3fc820c18


---

# ATA 알림 설정
ATA는 의심스러운 활동을 감지하면 메일을 통해 또는 ATA 이벤트 전달 기능을 사용한 후 이벤트를 SIEM/syslog 서버에 전달하여 알릴 수 있습니다. 수신하려는 알림을 선택하기 전에 [메일 서버 및 Syslog 서버를 설정](setting-syslog-email-server-settings.md)해야 합니다.

> [!NOTE]
> -   전자 메일 알림에는 발견된 의심스러운 활동으로 사용자를 직접 이동하는 링크가 포함됩니다. 링크의 호스트 이름 부분은 ATA 센터 페이지에서 ATA 콘솔 URL을 설정하여 가져옵니다. 기본적으로 ATA 콘솔 URL은 ATA 센터의 설치 중에 선택한 IP 주소입니다.  메일 알림을 구성하려는 경우 FQDN을 ATA 콘솔 URL로 사용하는 것이 좋습니다.
> -   알림은 ATA 센터에서 SMTP 서버 또는 Syslog 서버로 전송됩니다.

메일 알림을 수신하려면 다음을 설정합니다.


1. ATA 콘솔의 도구 모음에서 설정 옵션을 선택하고 **구성**을 선택합니다.
![ATA 구성 설정 아이콘](media/ATA-config-icon.JPG)

2. **알림**을 선택합니다.
3. **메일 알림**에서 토글을 사용하여 전송해야 하는 알림을 선택합니다.


    - 새로운 의심스러운 활동이 검색되는 경우
    - 새로운 상태 문제가 검색되는 경우
    - 새 소프트웨어 업데이트를 사용할 수 있는 경우

4. 메일을 통해 알림을 받을 수신자를 지정합니다.

    [!참고:] 의심스러운 활동에 대한 메일 경고는 의심스러운 활동이 생성될 때만 전송됩니다.


5. **저장**을 클릭합니다.

Syslog 알림을 수신하려면 다음을 설정합니다.


1. ATA 콘솔의 도구 모음에서 설정 옵션을 선택하고 **구성**을 선택합니다.
![ATA 구성 설정 아이콘](media/ATA-config-icon.JPG)

2. **알림**을 선택합니다.
3. **Syslog 알림**에서 토글을 사용하여 전송해야 하는 알림을 선택합니다.


    - 새로운 의심스러운 활동이 검색되는 경우
    - 기존의 의심스러운 활동이 업데이트되는 경우
    - 새로운 상태 문제가 검색되는 경우
5. **저장**을 클릭합니다.
![ATA 알림 설정 이미지](media/ATA-notification-settings.png)




## 참고 항목
[ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


