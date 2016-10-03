---
title: "이벤트 수집 구성 | Microsoft ATA"
description: "ATA를 사용하여 이벤트 수집을 구성하는 옵션을 설명합니다."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d2c1c00ff649557c1a0a16385e025c9d597c3bbf
ms.openlocfilehash: 91ce3a3fef27673712a708aa1e92c32298cedd84


---

*적용 대상: Advanced Threat Analytics 버전 1.6 및 1.7*



# 이벤트 수집 구성
검색 기능을 강화하려면 ATA에 Windows 이벤트 로그 ID 4776이 있어야 합니다. 두 가지 방법으로 ATA Gateway에 이 ID를 전달할 수 있습니다. 그 중 하나는 ATA Gateway가 SIEM 이벤트를 수신하도록 구성하는 것이고, 다른 하나는 [Windows 이벤트 전달을 구성](#configuring-windows-event-forwarding)하는 것입니다.

## 이벤트 수집
ATA는 도메인 컨트롤러에서 보내고 받는 네트워크 트래픽을 수집 및 분석할 수 있을 뿐 아니라 Windows 이벤트 4776을 사용하여 ATA Pass-the-Hash 검색 기능을 추가로 개선할 수 있습니다. 이 이벤트는 SIEM에서 수신될 수도 있고 도메인 컨트롤러에서 Windows 이벤트 전달을 설정하여 수신할 수도 있습니다. 수집된 이벤트는 도메인 컨트롤러 네트워크 트래픽을 통해서는 사용할 수 없는 추가 정보를 ATA에 제공합니다.

### SIEM/Syslog
ATA가 Syslog 서버에서 데이터를 사용할 수 있도록 하려면 다음을 수행해야 합니다.

-   SIEM/Syslog 서버에서 전달되는 이벤트를 수신하고 수락하도록 ATA Gateway 서버를 구성합니다.

-   ATA Gateway로 특정 이벤트를 전달하도록 SIEM/Syslog 서버를 구성합니다.

> [!IMPORTANT]
> -   ATA Gateway로 모든 Syslog 데이터를 전달하지 마세요.
> -   ATA는 SIEM/Syslog 서버의 UDP 트래픽을 지원합니다.

다른 서버로의 특정 이벤트 전달을 구성하는 방법은 SIEM/Syslog 서버의 제품 설명서를 참조하세요. 

### Windows 이벤트 전달
SIEM/Syslog 서버를 사용하지 않는 경우 ATA에서 수집하고 분석할 Windows 이벤트 ID 4776을 전달하도록 Windows 도메인 컨트롤러를 구성할 수 있습니다. Windows 이벤트 ID 4776에서는 NTLM 인증에 대한 데이터를 제공합니다.

## SIEM 이벤트를 수신하도록 ATA 게이트웨이 구성

1.  ATA 구성의 "이벤트" 탭에서 **Syslog**를 사용하도록 설정하고 **저장**을 누릅니다.

    ![Syslog 수신기 UDP 설정 이미지](media/ATA-enable-siem-forward-events.png)

2.  ATA 게이트웨이 중 IP 주소 하나로 Windows 이벤트 ID 4776을 전달하도록 SIEM 또는 Syslog 서버를 구성합니다. SIEM을 구성하는 방법에 대한 자세한 내용은 SIEM 온라인 도움말 또는 각 SIEM 서버의 특정 형식 지정 요구 사항에 대한 기술 지원 옵션을 참조하세요.

### SIEM 지원
ATA는 다음 형식의 SIEM 이벤트를 지원합니다.  

#### RSA 보안 분석
&lt;Syslog 헤더&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

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
&lt;Syslog 헤더&gt;\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

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

#### QRadar
QRadar는 에이전트를 통해 이벤트 컬렉션을 사용하도록 설정합니다. 에이전트를 사용하여 데이터를 수집하는 경우 시간 형식은 밀리초 데이터 없이 수집됩니다. ATA에는 밀리초 단위의 데이터가 필요하기 때문에 에이전트 없는 Windows 이벤트 컬렉션을 사용하도록 QRadar를 설정해야 합니다. 자세한 내용은 [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: Agentless Windows Events Collection using the MSRPC Protocol(QRadar: MSRPC 프로토콜을 사용하는 에이전트 없는 Windows 이벤트 컬렉션)")을 참조하세요.

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

필요한 필드는 다음과 같습니다.

- 컬렉션용 에이전트 유형
- Windows 이벤트 로그 공급자 이름
- Windows 이벤트 로그 소스
- DC 정규화된 도메인 이름
- Windows 이벤트 ID

TimeGenerated는 실제 이벤트의 타임스탬프(SIEM에 도착한 타임스탬프 또는 ATA에 전송된 시간이 아닌지 확인)입니다. 형식은 yyyyMMddHHmmss.FFFFFF와 일치해야 합니다. 밀리초 단위의 정확도를 사용하는 것이 좋습니다. 이는 매우 중요합니다.

Message는 Windows 이벤트의 원래 이벤트 텍스트입니다.

키=값 쌍 사이에 \t가 있는지 확인합니다.

>[!NOTE] 
> Windows 이벤트 컬렉션용 WinCollect는 사용할 수 없습니다.

## Windows 이벤트 전달 구성

### 포트 미러링으로 ATA 게이트웨이에 대한 WEF 구성

도메인 컨트롤러에서 ATA 게이트웨이로의 미러링을 구성하고 나면 원본에서 시작된 구성을 사용하여 아래 지침에 따라 Windows 이벤트 전달을 구성합니다. 이것이 Windows 이벤트 전달을 구성하는 한 가지 방법입니다. 

**1단계: 도메인 Event Log Readers 그룹에 네트워크 서비스 계정 추가** 

이 시나리오에서는 ATA 게이트웨이가 도메인의 멤버라고 간주합니다.

1.  Active Directory 사용자 및 컴퓨터를 열고 **Builtin** 폴더로 이동하여 **Event Log Readers** 그룹을 두 번 클릭합니다. 
2.  **멤버**를 선택합니다.
4.  **네트워크 서비스**가 목록에 없으면 **추가**를 클릭하고, **선택할 개체 이름을 입력하십시오** 필드에 **네트워크 서비스**를 입력합니다. **이름 확인**클릭한 다음 **확인**을 두 번 클릭합니다. 

**2단계: 대상 구독 관리자 구성 설정을 위해 도메인 컨트롤러에서 정책 만들기** 
> [!Note] 
> 이러한 설정에 대한 그룹 정책을 만들고 ATA 게이트웨이에서 모니터링할 각 도메인 컨트롤러에 그룹 정책을 적용할 수 있습니다. 다음 단계는 도메인 컨트롤러의 로컬 정책을 수정합니다.     

1.  각 도메인 컨트롤러에서 *winrm quickconfig* 명령을 실행합니다.
2.  명령 프롬프트에 *gpedit.msc*를 입력합니다.
3.  **컴퓨터 구성 정책 > 관리 템플릿 > Windows 구성 요소 > 이벤트 전달**을 확장합니다.

 ![로컬 정책 그룹 편집기 이미지](media/wef 1 local group policy editor.png)

4.  **대상 가입 관리자 구성**을 두 번 클릭합니다.
   
    1.  **사용**을 선택합니다.
    2.  **옵션**에서 **표시**를 클릭합니다.
    3.  **SubscriptionManagers**에서 다음 값을 입력하고 **확인**을 클릭합니다. *Server=http://<fqdnATAGateway>:5985/wsman/SubscriptionManager/WEC,Refresh=10* (For example: Server=http://atagateway9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10)
 
   ![대상 구독 구성 이미지](media/wef 2 config target sub manager.png)
   
    5.  **확인**을 클릭합니다.
    6.  관리자 권한 명령 프롬프트에서 *gpupdate /force*를 입력합니다. 

**3단계: ATA Gateway 서버에서 다음 단계 수행** 

1.  관리자 권한 명령 프롬프트를 열고 *wecutil qc*를 입력합니다.
2.  **이벤트 뷰어**를 엽니다. 
3.  마우스 오른쪽 단추로 **구독**을 클릭하고 **구독 만들기**를 클릭합니다. 

   1.   구독에 대한 이름과 설명을 입력합니다. 
   2.   **대상 로그**에서 **전달된 이벤트**가 선택되어 있는지 확인합니다. ATA에서 이벤트를 읽으려면 대상 로그가 **전달된 이벤트**여야 합니다. 
   3.   **원본 컴퓨터 시작**을 선택하고 **컴퓨터 그룹 선택**을 클릭합니다.
        1.  **도메인 컴퓨터 추가**를 클릭합니다.
        2.  **선택할 개체 이름을 입력하십시오** 필드에 도메인 컨트롤러의 이름을 입력합니다. **이름 확인**을 클릭하고 **확인**을 클릭합니다. 
       
        ![이벤트 뷰어 이미지](media/wef3 event viewer.png)
   
        
        3.  **확인**을 클릭합니다.
   4.   **이벤트 선택**을 클릭합니다.

        1. **로그 기준**을 클릭하고 **보안**을 선택합니다.
        2. **이벤트 ID 포함/제외** 필드에 **4776**을 입력하고 **확인**을 클릭합니다. 

 ![쿼리 필터 이미지](media/wef 4 query filter.png)

   5.   만들어진 구독을 마우스 오른쪽 단추로 클릭하고 **런타임 상태**를 선택하여 상태에 문제가 있는지 확인합니다. 
   6.   몇 분 후 이벤트 4776이 ATA 게이트웨이에서 전달된 이벤트에 표시되는지 확인합니다.


### ATA 경량 게이트웨이에 대한 WEF 구성
도메인 컨트롤러에 ATA 경량 게이트웨이를 설치하는 경우 자신에게 이벤트가 전달되도록 도메인 컨트롤러를 설정할 수 있습니다. ATA 경량 게이트웨이를 사용하는 경우 Windows 이벤트 전달을 구성하려면 다음 단계를 수행합니다. 이것이 Windows 이벤트 전달을 구성하는 한 가지 방법입니다.  

**1단계: 도메인 Event Log Readers 그룹에 네트워크 서비스 계정 추가** 

1.  Active Directory 사용자 및 컴퓨터를 열고 **Builtin** 폴더로 이동하여 **Event Log Readers** 그룹을 두 번 클릭합니다. 
2.  **멤버**를 선택합니다.
3.  **네트워크 서비스**가 목록에 없으면 **추가**를 클릭하고, **선택할 개체 이름을 입력하십시오** 필드에 **네트워크 서비스**를 입력합니다. **이름 확인**클릭한 다음 **확인**을 두 번 클릭합니다. 

**2단계: ATA 경량 게이트웨이가 설치된 후 도메인 컨트롤러에서 다음 단계 수행** 

1.  관리자 권한 명령 프롬프트를 열고 *winrm quickconfig* 및 *wecutil qc*를 입력합니다. 
2.  **이벤트 뷰어**를 엽니다. 
3.  마우스 오른쪽 단추로 **구독**을 클릭하고 **구독 만들기**를 클릭합니다. 

   1.   구독에 대한 이름과 설명을 입력합니다. 
   2.   **대상 로그**에서 **전달된 이벤트**가 선택되어 있는지 확인합니다. ATA에서 이벤트를 읽으려면 대상 로그가 전달된 이벤트여야 합니다.

        1.  **수집기 시작**을 선택하고 **컴퓨터 선택**을 클릭합니다. 그런 다음 **도메인 컴퓨터 추가**를 클릭합니다.
        2.  **선택할 개체 이름을 입력하십시오**에 도메인 컨트롤러의 이름을 입력합니다. **이름 확인**을 클릭하고 **확인**을 클릭합니다.

            ![구독 속성 이미지](media/wef 5 sub properties computers.png)

        3.  **확인**을 클릭합니다.
   3.   **이벤트 선택**을 클릭합니다.

        1.  **로그 기준**을 클릭하고 **보안**을 선택합니다.
        2.  **이벤트 ID 포함/제외**에 *4776*을 입력하고 **확인**을 클릭합니다. 

![쿼리 필터 이미지](media/wef 4 query filter.png)


  4.    만들어진 구독을 마우스 오른쪽 단추로 클릭하고 **런타임 상태**를 선택하여 상태에 문제가 있는지 확인합니다. 

> [!Note] 
> 설정을 적용하려면 도메인 컨트롤러를 다시 부팅해야 할 수 있습니다. 

몇 분 후 이벤트 4776이 ATA 게이트웨이에서 전달된 이벤트에 표시되는지 확인합니다.



자세한 내용은 [이벤트를 전달하고 수집하도록 컴퓨터 구성](https://technet.microsoft.com/library/cc748890)을 참조하세요.

## 참고 항목
- [ATA 설치](install-ata.md)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Sep16_HO4-->


