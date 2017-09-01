---
title: "Advanced Threat Analytics 설치 - 6단계 | Microsoft 문서"
description: "ATA 설치의 이 단계에서는 데이터 원본을 구성합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/29/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ac591d960028268f6c1ebd74706839a3b91597da
ms.sourcegitcommit: 9ce330726e5de8c05eae6a20d3e6c1d8bef3cd0e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*



# <a name="install-ata---step-6"></a>ATA 설치 - 6단계

>[!div class="step-by-step"]
[« 5단계](install-ata-step5.md)

## <a name="step-6-configure-event-collection-and-vpn"></a>6단계. 이벤트 수집 및 VPN 구성
### <a name="configure-event-collection"></a>이벤트 수집 구성
검색 기능을 강화하려면 ATA에 Windows 이벤트 4776, 4732, 4733, 4728, 4729, 4756, 4757이 있어야 합니다. 이러한 이벤트는 ATA 경량 게이트웨이에서 자동으로 읽거나, ATA 경량 게이트웨이가 배포되지 않은 경우 두 가지 방법 중 하나로 ATA 게이트웨이에 전달될 수 있습니다. 하나는 ATA 게이트웨이가 SIEM 이벤트를 수신하도록 구성하는 것이고, 다른 하나는 [Windows 이벤트 전달을 구성](configure-event-collection.md)하는 것입니다.

> [!NOTE]
> ATA 버전 1.8 이상에서는 ATA 경량 게이트웨이에 이벤트 수집 구성이 더 이상 필요하지 않습니다. 이제 ATA 경량 게이트웨이가 이벤트 전달을 구성하지 않고도 로컬에서 이벤트를 읽을 수 있습니다.

ATA는 도메인 컨트롤러에서 보내고 받는 네트워크 트래픽을 수집 및 분석할 수 있을 뿐 아니라 Windows 이벤트를 사용하여 검색 기능을 추가로 개선할 수 있습니다. 다양한 검색을 개선하는 NTLM용 이벤트 4776과 중요한 그룹 수정 검색을 개선하는 이벤트 4732, 4733, 4728, 4729, 4756 및 4757을 사용합니다. 이 이벤트는 SIEM에서 수신될 수도 있고 도메인 컨트롤러에서 Windows 이벤트 전달을 설정하여 수신할 수도 있습니다. 수집된 이벤트는 도메인 컨트롤러 네트워크 트래픽을 통해서는 사용할 수 없는 추가 정보를 ATA에 제공합니다.

#### <a name="siemsyslog"></a>SIEM/Syslog
ATA가 Syslog 서버에서 데이터를 사용할 수 있도록 하려면 다음을 수행해야 합니다.

-   SIEM/Syslog 서버에서 전달되는 이벤트를 수신하고 수락하도록 ATA Gateway 서버를 구성합니다.
> [!NOTE]
> ATA는 IPv4에서만 수신하며 IPv6에서 수신하지 않습니다. 
-   ATA Gateway로 특정 이벤트를 전달하도록 SIEM/Syslog 서버를 구성합니다.

> [!IMPORTANT]
> -   ATA Gateway로 모든 Syslog 데이터를 전달하지 마세요.
> -   ATA는 SIEM/Syslog 서버의 UDP 트래픽을 지원합니다.

다른 서버로의 특정 이벤트 전달을 구성하는 방법은 SIEM/Syslog 서버의 제품 설명서를 참조하세요. 

> [!NOTE]
>SIEM/Syslog 서버를 사용하지 않는 경우 ATA에서 수집하고 분석할 Windows 이벤트 ID 4776을 전달하도록 Windows 도메인 컨트롤러를 구성할 수 있습니다. Windows 이벤트 ID 4776에서는 NTLM 인증에 대한 데이터를 제공합니다.

#### <a name="configuring-the-ata-gateway-to-listen-for-siem-events"></a>SIEM 이벤트를 수신하도록 ATA 게이트웨이 구성

1.  ATA 구성의 **데이터 원본**에서 **SIEM**을 클릭하고 **Syslog**를 켠 다음 **저장**을 클릭합니다.

    ![Syslog 수신기 UDP 설정 이미지](media/ATA-enable-siem-forward-events.png)

2.  ATA 게이트웨이 중 IP 주소 하나로 Windows 이벤트 ID 4776을 전달하도록 SIEM 또는 Syslog 서버를 구성합니다. SIEM을 구성하는 방법에 대한 자세한 내용은 SIEM 온라인 도움말 또는 각 SIEM 서버의 특정 형식 지정 요구 사항에 대한 기술 지원 옵션을 참조하세요.

ATA는 다음 형식의 SIEM 이벤트를 지원합니다.  

#### <a name="rsa-security-analytics"></a>RSA 보안 분석
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

#### <a name="hp-arcsight"></a>HP Arcsight
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

#### <a name="splunk"></a>Splunk
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

#### <a name="qradar"></a>QRadar
QRadar는 에이전트를 통해 이벤트 컬렉션을 사용하도록 설정합니다. 에이전트를 사용하여 데이터를 수집하는 경우 시간 형식은 밀리초 데이터 없이 수집됩니다. ATA에는 밀리초 단위의 데이터가 필요하기 때문에 에이전트 없는 Windows 이벤트 컬렉션을 사용하도록 QRadar를 설정해야 합니다. 자세한 내용은 [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: Agentless Windows Events Collection using the MSRPC Protocol(QRadar: MSRPC 프로토콜을 사용하는 에이전트 없는 Windows 이벤트 컬렉션)")을 참조하세요.

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

필요한 필드는 다음과 같습니다.

- 컬렉션용 에이전트 유형
- Windows 이벤트 로그 공급자 이름
- Windows 이벤트 로그 원본
- DC 정규화된 도메인 이름
- Windows 이벤트 ID

TimeGenerated는 실제 이벤트의 타임스탬프(SIEM에 도착한 타임스탬프 또는 ATA에 전송된 시간이 아닌지 확인)입니다. 형식은 yyyyMMddHHmmss.FFFFFF와 일치해야 합니다. 밀리초 단위의 정확도를 사용하는 것이 좋습니다. 이는 매우 중요합니다.

Message는 Windows 이벤트의 원래 이벤트 텍스트입니다.

키=값 쌍 사이에 \t가 있는지 확인합니다.

>[!NOTE] 
> Windows 이벤트 컬렉션용 WinCollect는 사용할 수 없습니다.


### <a name="configuring-vpn"></a>VPN 구성

ATA는 컴퓨터가 네트워크에 연결하는 위치를 프로파일링하는 데 도움이 되는 VPN 데이터를 수집합니다.

VPN 데이터를 구성하려면 **구성** > **VPN**으로 이동한 다음 VPN의 **Radius 계정 공유 암호**를 입력합니다.

![VPN 구성](./media/vpn.png)

공유 암호를 가져오려면 VPN 설명서를 참조하세요. 지원되는 VPN 공급업체는 다음과 같습니다.

- Microsoft
- F5
- Check Point
- Cisco ASA



>[!div class="step-by-step"]
[«5 단계](install-ata-step5.md)
[7 단계»](install-ata-step7.md)



## <a name="related-videos"></a>관련 동영상
- [올바른 ATA 게이트웨이 유형 선택](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>참고 항목
- [ATA POC 배포 가이드](http://aka.ms/atapoc)
- [ATA 크기 조정 도구](http://aka.ms/atasizingtool)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [이벤트 수집 구성](configure-event-collection.md)
- [ATA 필수 구성 요소](ata-prerequisites.md)

