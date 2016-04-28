---
# required metadata

title: 이벤트 수집 구성 | Microsoft Advanced Threat Analytics
description: ATA를 사용하여 이벤트 수집을 구성하는 옵션을 설명합니다.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 이벤트 수집 구성
ATA의 Pass-the-Hash 공격 검색 기능을 개선하려면 ATA에서 Windows 이벤트 로그 ID 4776을 사용해야 합니다. 두 가지 방법으로 ATA Gateway에 이 ID를 전달할 수 있습니다. 그 중 하나는 ATA Gateway가 SIEM 이벤트를 수신하도록 구성하는 것이고, 다른 하나는 [Windows 이벤트 전달을 구성](#configuring-windows-event-forwarding)하는 것입니다.

## 이벤트 수집
ATA는 도메인 컨트롤러에서 보내고 받는 네트워크 트래픽을 수집 및 분석할 수 있을 뿐 아니라 Windows 이벤트 4776을 사용하여 ATA Pass-the-Hash 검색 기능을 추가로 개선할 수 있습니다. 이 이벤트는 SIEM에서 수신될 수도 있고 도메인 컨트롤러에서 Windows 이벤트 전달을 설정하여 수신할 수도 있습니다. 수집된 이벤트는 도메인 컨트롤러 네트워크 트래픽을 통해서는 사용할 수 없는 추가 정보를 ATA에 제공합니다.

### SIEM/Syslog
ATA가 Syslog 서버에서 데이터를 사용할 수 있도록 하려면 다음을 수행해야 합니다.

-   SIEM/Sylog 서버에서 전달되는 이벤트를 수신하고 수락하도록 ATA Gateway 서버 중 하나를 구성합니다.

-   ATA Gateway로 특정 이벤트를 전달하도록 SIEM/Syslog 서버를 구성합니다.

> [!IMPORTANT]
> -   ATA Gateway로 모든 Syslog 데이터를 전달하지 마세요.
> -   ATA는 SIEM/Syslog 서버의 UDP 트래픽을 지원합니다.

다른 서버로의 특정 이벤트 전달을 구성하는 방법은 SIEM/Syslog 서버의 제품 설명서를 참조하세요. ATA로 전달되는 이벤트에 대한 자세한 내용은 [이벤트 수집 구성](configure-event-collection.md)을 참조하세요.

### Windows 이벤트 전달
SIEM/Syslog 서버를 사용하지 않는 경우 ATA에서 수집하고 분석할 Windows 이벤트 ID 4776을 전달하도록 Windows 도메인 컨트롤러를 구성할 수 있습니다. Windows 이벤트 ID 4776에서는 NTLM 인증에 대한 데이터를 제공합니다.

## SIEM 이벤트를 수신하도록 ATA Gateway 구성

1.  ATA Gateway 구성에서 **Syslog 수신기 UDP**를 사용하도록 설정합니다.

    아래 그림에 설명된 대로 수신 대기 IP 주소를 설정합니다. 기본 포트는 514입니다.

    ![Syslog 수신기 UDP 설정 이미지](media/ATA-enable-siem-forward-events.png)

2.  위에서 선택한 IP 주소로 Windows 이벤트 ID 4776을 전달하도록 SIEM 또는 Syslog 서버를 구성합니다. SIEM을 구성하는 방법에 대한 자세한 내용은 SIEM 온라인 도움말 또는 각 SIEM 서버의 특정 형식 지정 요구 사항에 대한 기술 지원 옵션을 참조하세요.

### SIEM 지원
ATA는 다음 형식의 SIEM 이벤트를 지원합니다.

#### RSA 보안 분석
&lt;Syslog Header&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   Syslog 헤더는 선택 사항입니다.

-   "\n" 문자 구분 기호는 모든 필드 사이에 필요합니다.

-   필드는 순서대로 다음과 같습니다.

    1.  RsaSA 상수(표시되어야 함)

    2.  실제 이벤트의 타임스탬프(SIEM에 도착한 타임스탬프 또는 ATA에 전송된 시간이 아닌지 확인). 밀리초 단위의 정확도를 사용하는 것이 좋습니다. 이는 매우 중요합니다.

    3.  Windows 이벤트 ID

    4.  Windows 이벤트 공급자 이름

    5.  Windows 이벤트 로그 이름

    6.  이벤트를 수신하는 컴퓨터의 이름(이 예제의 경우 DC)

    7.  인증하는 사용자의 이름

    8.  원본 호스트 이름

    9. NTLM의 결과 코드

-   순서가 중요하며, 그 밖에 어떤 것도 메시지에 포함되어서는 안 됩니다.

#### HP Arcsight
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|The domain controller attempted to validate the credentials for an account.|Low| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Reason or Error Code

-   프로토콜 정의를 준수해야 합니다.

-   Syslog 헤더가 없습니다.

-   헤더 부분(파이프로 구분된 부분)이 있어야 합니다(프로토콜에 명시된 대로).

-   _Extension_ 부분의 다음 키가 이벤트에 있어야 합니다.

    -   externalId = Windows 이벤트 ID

    -   rt = 실제 이벤트의 타임스탬프(SIEM에 도착한 타임스탬프 또는 전송 받은 시간이 아닌지 확인). 밀리초 단위의 정확도를 사용하는 것이 좋습니다. 이는 매우 중요합니다.

    -   cat = Windows 이벤트 로그 이름

    -   shost = 원본 호스트 이름

    -   dhost = 이벤트를 수신하는 컴퓨터의 이름(이 예제의 경우 DC)

    -   duser = 인증하는 사용자의 이름

-   _Extension_ 부분에는 순서가 중요하지 않습니다.

-   다음 두 필드에 대한 사용자 지정 키 및 키 레이블이 있어야 합니다.

    -   “EventSource”

    -   “Reason or Error Code” = NTLM의 결과 코드

#### Splunk
&lt;Syslog Header&gt;\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

The computer attempted to validate the credentials for an account.

Authentication Package:              MICROSOFT_AUTHENTICATION_PACKAGE_V1_0

Logon Account: Administrator

Source Workstation:       SIEM

Error Code:         0x0

-   Syslog 헤더는 선택 사항입니다.

-   모든 필수 필드 사이에 "\r\n" 문자 구분 기호가 있습니다.

-   필드는 키=값 형식입니다.

-   다음 키가 존재해야 하며 값이 있어야 합니다.

    -   EventCode = Windows 이벤트 ID

    -   Logfile = Windows 이벤트 로그 이름

    -   SourceName = Windows 이벤트 공급자 이름

    -   TimeGenerated = 실제 이벤트의 타임스탬프(SIEM에 도착한 타임스탬프 또는 ATA에 전송된 시간이 아닌지 확인). 형식은 yyyyMMddHHmmss.FFFFFF와 일치해야 합니다. 밀리초 단위의 정확도를 사용하는 것이 좋습니다. 이는 매우 중요합니다.

    -   ComputerName = 원본 호스트 이름

    -   Message = Windows 이벤트의 원래 이벤트 텍스트

-   메시지 키와 값은 마지막 키와 값이어야 합니다.

-   키=값 쌍에는 순서가 중요하지 않습니다.

## Windows 이벤트 전달 구성
SIEM 서버가 없는 경우 ATA Gateway 중 하나로 직접 Windows 이벤트 ID 4776을 전달하도록 도메인 컨트롤러를 구성할 수 있습니다.

1.  관리자 권한의 도메인 계정을 사용하여 모든 도메인 컨트롤러와 ATA Gateway 컴퓨터에 로그온합니다.
2. 모든 도메인 컨트롤러 및 연결하려는 ATA Gateway가 동일한 도메인에 가입되어 있는지 확인합니다.
3.  각 도메인 컨트롤러의 관리자 권한 명령 프롬프트에서 다음을 입력합니다.
```
winrm quickconfig
```
4.  ATA Gateway의 관리자 권한 명령 프롬프트에서 다음을 입력합니다.
```
wecutil qc
```
5.  각 도메인 컨트롤러의 **Active Directory 사용자 및 컴퓨터**에서 **Builtin** 폴더로 이동하여 **Event Log Readers** 그룹을 두 번 클릭합니다.
![wef_ad_eventlogreaders](media/wef_ad_eventlogreaders.png)
마우스 오른쪽 단추를 클릭하고 **속성**을 선택합니다. **멤버** 탭에서 각 ATA Gateway의 컴퓨터 계정을 추가합니다.
![wef_ad event log reader popup](media/wef_ad-event-log-reader-popup.png)
6.  ATA Gateway에서 이벤트 뷰어를 열고 **구독**을 마우스 오른쪽 단추로 클릭한 다음 **구독 만들기**를 선택합니다.  

    a.  **구독 유형 및 원본 컴퓨터** 아래에서 **컴퓨터 선택**을 클릭하고 도메인 컨트롤러를 추가한 다음 연결을 테스트합니다.
    ![wef_subscription prop](media/wef_subscription-prop.png)

    b.  **수집할 이벤트** 아래에서 **이벤트 선택**을 클릭합니다. **로그**를 선택하고 아래로 스크롤하여 **보안**을 선택합니다. 그런 다음 **이벤트 ID 포함/제외**에서 **4776**을 입력합니다.
    ![wef_4776](media/wef_4776.png)

    c. **사용자 계정 변경 또는 고급 설정 구성** 아래에서 **고급**을 클릭합니다.
        **프로토콜**을 **HTTP**로 설정하고 **포트**를 **5985**로 설정합니다.
    ![wef_http](media/wef_http.png)

 7. [선택 사항] 폴링 간격을 줄이려면 보다 빠른 폴링 속도를 위해 ATA Gateway에서 구독 하트비트를 5초로 설정합니다.

```
wecutil ss <CollectionName>/cm:custom
wecutil ss <CollectionName> /hi:5000
```

8. ATA Gateway 구성 페이지에서 **Windows 이벤트 전달 수집**을 사용하도록 설정합니다.

    > [!NOTE]
    > 이 설정을 사용하도록 설정하면 ATA Gateway가 전달된 이벤트 로그에서 도메인 컨트롤러로부터 전달된 Windows 이벤트를 찾습니다.

자세한 내용은 [이벤트를 전달하고 수집하도록 컴퓨터 구성](https://technet.microsoft.com/en-us/library/cc748890)을 참조하세요.

## 참고 항목
- [ATA 설치](/advanced-threat-analytics/DeployUse/install-ata)
- [지원이 필요한 경우 포럼을 확인하세요.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


