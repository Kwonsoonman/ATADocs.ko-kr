---
title: "메일 설정 지정 | Microsoft 문서"
description: "ATA가 의심스러운 활동을 검색할 때 알리는 방식(메일 또는 ATA 이벤트 전달)을 설명합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: bff20bf7-8b53-49da-81e5-b818a1c3b24e
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: fca7f1b2b8260cad6e0ce32aad1c9e1b53fc0ad5
ms.openlocfilehash: d967cbf2674c5f561e63f66b64640ac08daad6c0


---

*적용 대상: Advanced Threat Analytics 버전 1.7*



# <a name="provide-ata-with-up-your-email-server-settings"></a>ATA에 메일 서버 설정 제공
ATA는 의심스러운 활동을 검색한 경우 알림을 제공할 수 있습니다. ATA에서 메일 알림을 보낼 수 있도록 하려면 먼저 **메일 서버 설정**을 구성해야 합니다.

1.  ATA 센터 서버의 바탕 화면에서 **Microsoft Advanced Threat Analytics 관리** 아이콘을 클릭합니다.

2.  사용자 이름과 암호를 입력하고 **로그인**을 클릭합니다.

3.  도구 모음에서 설정 옵션을 선택하고 **구성**을 선택합니다.

    ![ATA 구성 설정 아이콘](media/ATA-config-icon.JPG)

4.  **알림** 섹션의 **메일 서버**에 다음 정보를 입력합니다.

    |필드|설명|값|
    |---------|---------------|---------|
    |SMTP 서버 끝점(필수)|SMTP 서버의 FQDN을 입력하고 포트 번호를 선택적으로 변경합니다(기본값은 25).|예를 들면 다음과 같습니다.<br />smtp.contoso.com|
    |SSL|SMTP 서버에 SSL이 필요한 경우 SSL을 전환합니다. **참고:** SSL을 사용하도록 설정하면 포트 번호도 변경해야 합니다.|기본값은 사용 안 함입니다.|
    |인증|SMTP 서버에 인증이 필요하면 사용하도록 설정합니다. **참고:** 인증을 사용하도록 설정하는 경우 SMTP 서버에 연결할 수 있는 권한이 있는 전자 메일 계정의 사용자 이름 및 암호를 제공해야 합니다.|기본값은 사용 안 함입니다.|
    |보낸 사람(필수)|전자 메일을 보낸 사람의 전자 메일 주소를 입력합니다.|예를 들면 다음과 같습니다.<br />ATA@contoso.com|
    ![ATA 메일 서버 설정 이미지](media/ATA-email-server-1.7.png)

## <a name="provide-ata-with-your-syslog-server-settings"></a>ATA에 Syslog 서버 설정 제공
ATA는 의심스러운 활동이 검색되면 Syslog 서버에 알림을 전송하여 알릴 수 있습니다. Syslog 알림을 사용하도록 설정하면 다음을 설정할 수 있습니다.

1.  Syslog 알림을 구성하기 전에 SIEM 관리자와 협력하여 다음 정보를 찾습니다.

    -   SIEM 서버의 FQDN 또는 IP 주소

    -   SIEM 서버가 수신 대기하는 포트

    -   사용할 전송: UDP, TCP 또는 TLS(보안 Syslog)

    -   데이터 RFC 3164 또는 5424를 보낼 형식

2.  ATA 센터 서버의 바탕 화면에서 **Microsoft Advanced Threat Analytics 관리** 아이콘을 클릭합니다.

3.  사용자 이름과 암호를 입력하고 **로그인**을 클릭합니다.

4.  도구 모음에서 설정 옵션을 선택하고 **구성**을 선택합니다.

    ![ATA 구성 설정 아이콘](media/ATA-config-icon.JPG)

5.  알림 섹션에서 **Syslog 서버**를 선택하고 다음 정보를 입력합니다.

    |필드|설명|
    |---------|---------------|
    |Syslog 서버 끝점|Syslog 서버의 FQDN을 입력하고 포트 번호를 선택적으로 변경합니다(기본값은 514).|
    |전송|UDP, TCP 또는 TLS(보안 Syslog)일 수 있음|
    |형식|ATA이 SIEM 서버에 이벤트를 전송하는 데 사용하는 형식(RFC 5424 또는 RFC 3164)입니다.|

 ![ATA Syslog 서버 설정 이미지](media/ata-syslog-server-settings-1.7.png)



## <a name="see-also"></a>참고 항목
[ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Nov16_HO3-->


