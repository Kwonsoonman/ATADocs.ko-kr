---
# required metadata

title: ATA 경고 설정 | Microsoft Advanced Threat Analytics
description: ATA가 의심스러운 활동을 검색할 때 경고하는 방식(전자 메일 또는 ATA 이벤트 전달)을 설명합니다. 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 경고 설정
ATA는 의심스러운 활동을 감지하면 전자 메일을 통해 또는 ATA 이벤트 전달 기능을 사용한 후 이벤트를 SIEM/syslog 서버에 전달하여 경고할 수 있습니다. 이러한 유형의 경고 중 하나 또는 둘 다를 사용하도록 설정하면 다음을 설정할 수 있습니다.

> [!NOTE]
> -   전자 메일 알림에는 발견된 의심스러운 활동으로 사용자를 직접 이동하는 링크가 포함됩니다. 링크의 호스트 이름 부분은 ATA 센터 페이지에서 ATA 콘솔 URL을 설정하여 가져옵니다. 기본적으로 ATA 콘솔 URL은 ATA 센터의 설치 중에 선택한 IP 주소입니다.  전자 메일 알림을 구성하려는 경우 FQDN을 ATA 콘솔 URL로 사용하는 것이 좋습니다.
> -   시스템 상태 경고 알림은 전자 메일을 통해서만 전송됩니다.
> -   경고는 ATA 센터에서 SMTP 서버 또는 Syslog 서버로 전송됩니다.
> -   의심스러운 활동에 대한 전자 메일 경고는 의심스러운 활동이 생성될 때만 전송됩니다.

## 언어 및 빈도 설정
**언어** 설정은 전자 메일을 통해 전송된 알림과 Syslog 서버로 전송된 알림에 적용됩니다.

**빈도** 설정은 Syslog 서버로 전송된 알림에만 적용됩니다.

1.  ATA 콘솔을 엽니다.

2.  도구 모음에서 설정 옵션을 선택하고 **구성**을 선택합니다.

    ![ATA 구성 설정 아이콘](media/ATA-config-icon.JPG)

3.  **경고**를 선택합니다.

4.  **언어** 아래에서 원하는 언어를 선택합니다.

5.  새 경고가 생성될 때만 간단한 알림을 수신하려면 **빈도** 아래에서 **낮은 빈도**를 선택합니다. 새로운 경고가 생성될 때 뿐만 아니라 기존 경고가 수정되는 경우에도 자세한 알림을 수신하려면 **높은 빈도**를 선택합니다.

    ![경고의 자세한 정도 구성 이미지](media/ATA-alerts-verbosity-language.png)

6.  **저장**을 클릭합니다.

## 전자 메일 경고 설정
ATA는 의심스러운 활동을 검색한 경우 경고를 제공할 수 있습니다. 전자 메일 알림을 사용하도록 설정하면 다음을 설정할 수 있습니다.

1.  ATA 센터 서버의 바탕 화면에서 **Microsoft Advanced Threat Analytics 관리** 아이콘을 클릭합니다.

2.  사용자 이름과 암호를 입력하고 **로그인**을 클릭합니다.

3.  도구 모음에서 설정 옵션을 선택하고 **구성**을 선택합니다.

    ![ATA 구성 설정 아이콘](media/ATA-config-icon.JPG)

4.  **경고**를 선택합니다.

5.  **메일**을 켜서 전자 메일 경고를 사용하도록 설정하고 다음 정보를 입력합니다.

    |필드|설명|값|
    |---------|---------------|---------|
    |SMTP 서버 끝점(필수)|SMTP 서버의 FQDN을 입력합니다.|예를 들면 다음과 같습니다.<br />smtp.contoso.com|
    |SSL|SMTP 서버에 SSL이 필요한 경우 SSL을 전환합니다. **참고:** SSL을 사용하도록 설정하면 포트 번호도 변경해야 합니다.|기본값은 사용 안 함입니다.|
    |인증|SMTP 서버에 인증이 필요하면 사용하도록 설정합니다. **참고:** 인증을 사용하도록 설정하는 경우 SMTP 서버에 연결할 수 있는 권한이 있는 전자 메일 계정의 사용자 이름 및 암호를 제공해야 합니다.|기본값은 사용 안 함입니다.|
    |보낸 사람(필수)|전자 메일을 보낸 사람의 전자 메일 주소를 입력합니다.|예를 들면 다음과 같습니다.<br />ATA@contoso.com|
    |받는 사람(필수)|ATA가 의심스러운 활동을 검색할 때 전자 메일을 받는 사용자 또는 전자 메일 그룹의 전자 메일 주소를 입력합니다. **참고:** 한 번에 하나씩 전자 메일 주소를 입력하고 더하기 기호를 클릭하여 추가합니다.|예를 들면 다음과 같습니다.<br />securityteam@contoso.com|

## SIEM에 대한 ATA 이벤트 전달 설정
ATA는 Syslog 서버에 경고를 전송하여 의심스러운 활동이 감지될 때 경고할 수 있습니다. Syslog 알림을 사용하도록 설정하면 다음을 설정할 수 있습니다.

1.  Syslog 경고를 구성하기 전에 SIEM 관리자와 협력하여 다음 정보를 찾습니다.

    -   SIEM 서버의 FQDN 또는 IP 주소

    -   SIEM 서버가 수신 대기하는 포트

    -   UDP, TCP 또는 보안 TCP를 사용하는 전송

    -   데이터 RFC 3164 또는 5424를 보낼 형식

2.  ATA 센터 서버의 바탕 화면에서 **Microsoft Advanced Threat Analytics 관리** 아이콘을 클릭합니다.

3.  사용자 이름과 암호를 입력하고 **로그인**을 클릭합니다.

4.  도구 모음에서 설정 옵션을 선택하고 **구성**을 선택합니다.

    ![ATA 구성 설정 아이콘](media/ATA-config-icon.JPG)

5.  **경고**를 선택합니다.

6.  **Syslog**를 켜서 의심스러운 활동에 대한 경고가 Syslog 서버로 전송되도록 하고 다음 정보를 입력합니다.

    |필드|설명|
    |---------|---------------|
    |Syslog 서버 끝점|Syslog 서버의 FQDN|
    |전송|UDC, TCP 또는 보안 TCP일 수 있음|
    |형식|ATA이 SIEM 서버에 이벤트를 전송하는 데 사용하는 형식(RFC 5424 또는 RFC 3164)입니다.|

## 참고 항목
[지원이 필요한 경우 포럼을 확인하세요.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


